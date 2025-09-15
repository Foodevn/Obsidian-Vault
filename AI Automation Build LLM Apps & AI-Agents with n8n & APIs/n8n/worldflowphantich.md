Dưới đây là **workflow mẫu** được thiết kế trên **n8n** cho một **trợ lý ảo bán hàng**, bao quát từ tiếp nhận tin nhắn khách → phân tích bằng AI → gợi ý sản phẩm → tạo đơn hàng → lưu dữ liệu → chăm sóc khách tự động.

Mình sẽ chia thành 3 **workflow chính** theo từng mục tiêu:

---

# **1. Workflow Chatbot trả lời khách hàng (AI + Zalo OA / Facebook)**

**Mục tiêu:**

* Nhận tin nhắn từ khách hàng (qua Zalo OA hoặc Facebook).
* AI phân tích nhu cầu khách → trả lời thông minh.
* Nếu khách muốn mua hàng → đẩy thông tin sang workflow tạo đơn hàng.

---

### **Sơ đồ tổng quan**

```
[Webhook: Nhận tin nhắn khách] 
   ↓
[Function: Chuẩn hóa dữ liệu]
   ↓
[OpenAI GPT: Phân tích intent + trả lời]
   ↓
[IF: Kiểm tra intent]
   ↙️                   ↘️
[Mua hàng]            [Chỉ hỏi thông tin]
   ↓                     ↓
[HTTP Request - gửi tin nhắn xác nhận]  
```

---

### **Chi tiết các node**

#### **1. Webhook Node (Zalo / Facebook)**

* **Purpose:** Nhận tin nhắn từ khách.
* URL: `https://<domain_n8n>/webhook/chat-incoming`
* Payload mẫu từ Zalo:

```json
{
  "user_id": "zalo_12345",
  "message": "Shop có áo sơ mi size M không?"
}
```

---

#### **2. Function Node – Chuẩn hóa dữ liệu**

```javascript
// Chuẩn hóa message để AI dễ hiểu
return [{
  userId: $json["user_id"],
  text: $json["message"].trim()
}];
```

---

#### **3. OpenAI Node – GPT trả lời**

* **Model:** GPT-4o mini hoặc GPT-4 Turbo.

* **Prompt mẫu:**

  ```
  Bạn là nhân viên bán hàng thân thiện của shop quần áo thời trang.
  - Nếu khách hỏi sản phẩm → gợi ý kèm giá và link mua.
  - Nếu khách muốn đặt hàng → trả về JSON {intent:"order",product:"Tên sản phẩm",size:"Size",quantity:Số lượng}.
  - Nếu khách chỉ hỏi thông tin → trả về JSON {intent:"info",message:"Câu trả lời"}.

  Tin nhắn khách hàng: {{$json["text"]}}
  ```

* **Output mẫu khi khách muốn mua:**

```json
{
  "intent": "order",
  "product": "Áo sơ mi trắng",
  "size": "M",
  "quantity": 2
}
```

---

#### **4. IF Node – Kiểm tra intent**

* **Điều kiện:**

  ```json
  {{$json["intent"]}} == "order"
  ```

* Nếu **true** → chuyển sang workflow tạo đơn hàng.

* Nếu **false** → gửi câu trả lời text về cho khách.

---

#### **5. HTTP Request – Gửi phản hồi về Zalo OA**

* **Phương thức:** POST
* **URL:** `https://openapi.zalo.me/v3.0/oa/message/cs`
* **Body mẫu:**

```json
{
  "recipient": { "user_id": "={{$json["userId"]}}" },
  "message": {
    "text": "={{$json["message"]}}"
  }
}
```

---

---

# **2. Workflow Tạo đơn hàng tự động**

**Mục tiêu:**

* Tự động tạo đơn hàng khi khách đồng ý mua.
* Đồng bộ đơn vào CRM và Shopee/TikTok Shop.
* Thông báo lại cho khách qua Zalo OA.

---

### **Sơ đồ tổng quan**

```
[Webhook: Dữ liệu đơn hàng từ Workflow 1]
   ↓
[Function: Kiểm tra tồn kho]
   ↓
[IF: Còn hàng?]
   ↙️                    ↘️
[Còn hàng]             [Hết hàng]
   ↓                      ↓
[HTTP Request - Tạo đơn]   [Zalo OA - Xin lỗi khách]
   ↓
[PostgreSQL Node - Lưu dữ liệu đơn]
   ↓
[Zalo OA - Gửi xác nhận đơn]
```

---

### **Chi tiết các node**

#### **1. Webhook Node**

* Nhận dữ liệu từ workflow chatbot:

```json
{
  "userId": "zalo_12345",
  "product": "Áo sơ mi trắng",
  "size": "M",
  "quantity": 2
}
```

---

#### **2. Function Node – Kiểm tra tồn kho**

```javascript
const stock = {
  "Áo sơ mi trắng": { "S": 5, "M": 2, "L": 0 }
};

const product = $json["product"];
const size = $json["size"];

if (stock[product] && stock[product][size] >= $json["quantity"]) {
  return [{ available: true }];
} else {
  return [{ available: false }];
}
```

---

#### **3. HTTP Request – Tạo đơn hàng trên Shopee**

* **Phương thức:** POST
* **URL:** `https://partner.shopeemobile.com/api/v2/order/create`
* **Body:**

```json
{
  "product_name": "={{$json["product"]}}",
  "size": "={{$json["size"]}}",
  "quantity": "={{$json["quantity"]}}",
  "customer_id": "={{$json["userId"]}}"
}
```

---

#### **4. PostgreSQL Node – Lưu đơn hàng vào database**

```sql
INSERT INTO orders (customer_id, product, size, quantity, status)
VALUES ({{$json["userId"]}}, {{$json["product"]}}, {{$json["size"]}}, {{$json["quantity"]}}, 'pending');
```

---

#### **5. Zalo OA Node – Xác nhận đơn hàng**

```json
{
  "recipient": { "user_id": "={{$json["userId"]}}" },
  "message": {
    "text": "Đơn hàng của bạn đã được ghi nhận! Shop sẽ liên hệ sớm nhất để xác nhận."
  }
}
```

---

---

# **3. Workflow CRM & Chăm sóc khách hàng tự động**

**Mục tiêu:**

* Chăm sóc khách hàng đã mua hoặc lâu chưa quay lại.
* Gửi tin khuyến mãi, nhắc nhở tự động qua Zalo OA.

---

### **Sơ đồ tổng quan**

```
[Trigger: Hàng ngày 09:00]
   ↓
[Database Query: Lấy khách hàng chưa mua 30 ngày]
   ↓
[Function: Soạn nội dung khuyến mãi]
   ↓
[Zalo OA: Gửi tin tự động]
```

---

#### **1. Cron Node**

* Chạy mỗi ngày **09:00** để quét dữ liệu khách hàng.

---

#### **2. PostgreSQL Node – Query khách hàng**

```sql
SELECT * FROM customers
WHERE last_purchase_date <= NOW() - INTERVAL '30 days';
```

---

#### **3. Function Node – Tạo nội dung tin nhắn**

```javascript
return items.map(item => {
  return {
    json: {
      user_id: item.json.user_id,
      message: `Chào ${item.json.name}! Shop có chương trình giảm giá 20% cho bạn trong hôm nay.`
    }
  };
});
```

---

#### **4. HTTP Request – Gửi tin qua Zalo OA**

```json
{
  "recipient": { "user_id": "={{$json["user_id"]}}" },
  "message": {
    "text": "={{$json["message"]}}"
  }
}
```

---

# **4. Tổ chức workflow trong n8n**

* **Workflow 1: Chatbot → AI → Phân loại yêu cầu.**
* **Workflow 2: Tạo đơn hàng → CRM → Gửi thông báo.**
* **Workflow 3: Marketing tự động → Chăm sóc khách hàng.**

> **Lợi ích tách workflow:**
>
> * Dễ quản lý, debug khi lỗi.
> * Tăng khả năng mở rộng, ví dụ tích hợp thêm TikTok Shop hoặc Lazada.

---

# **5. Tổng kết**

| **Workflow**       | **Chức năng chính**                                   | **Công cụ chính**                 |
| ------------------ | ----------------------------------------------------- | --------------------------------- |
| **Chatbot AI**     | Trả lời khách hàng, phân tích intent, gợi ý sản phẩm. | Webhook, OpenAI Node, Zalo OA API |
| **Tạo đơn hàng**   | Tự động chốt đơn, đồng bộ CRM và Shopee/TikTok.       | PostgreSQL, HTTP Request          |
| **Chăm sóc khách** | Gửi tin nhắn khuyến mãi, upsell.                      | Cron Node, Zalo OA API            |

---

Khi triển khai đầy đủ 3 workflow này, shop có thể:

* **Tự động hóa 70-90% quy trình bán hàng.**
* Quản lý khách hàng tập trung trên CRM.
* Tăng doanh thu nhờ **AI cá nhân hóa** và **marketing tự động**.
