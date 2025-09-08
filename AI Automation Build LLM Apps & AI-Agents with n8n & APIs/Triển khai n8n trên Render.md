Dưới đây là hướng dẫn **triển khai n8n trên Render** bằng **Docker Image** và **Neon DB**, được viết lại rõ ràng và dễ thực hành hơn:

---

## **1. Chuẩn bị**

- **Tài khoản**:
    - [Docker Hub](https://hub.docker.com/)
    - [Render](https://render.com/)
    - [Neon DB](https://neon.tech/)
- **Công cụ cần có**:
    - Trình duyệt web
    - Docker CLI (tùy chọn, chỉ để test image)

---
## **2. Lấy Docker Image của n8n**

Truy cập **Docker Hub** và tìm image chính thức của n8n:  
🔗 [https://hub.docker.com/r/n8nio/n8n](https://hub.docker.com/r/n8nio/n8n)

Ví dụ, lấy phiên bản `1.109.2-exp.0`:
```bash
docker pull n8nio/n8n:1.109.2-exp.0
```

> ⚠️ **Tip:** Chọn phiên bản **stable** mới nhất nếu muốn an toàn.

---

## **3. Tạo PostgreSQL Database trên Neon**

1. Vào [https://neon.tech/](https://neon.tech/), đăng ký và tạo **PostgreSQL Database** mới.
    
2. Sau khi tạo xong, lấy **connection string**.  
    Ví dụ:
    ```
    psql 'postgresql://neondb_owner:pg_lPGtuwNzQZ70@ep-ed-fog-a10tztqc-pooler.ap-southeast-1.aws.neon.tech/n8n-db?sslmode=require&channel_binding=require'
    ```
    
3. **Phân tích chuỗi kết nối** để tạo biến môi trường:
    

|Biến môi trường|Giá trị|
|---|---|
|`DB_POSTGRESDB_DATABASE`|`n8n-db`|
|`DB_POSTGRESDB_HOST`|`ep-ed-fog-a10tztqc-pooler.ap-southeast-1.aws.neon.tech`|
|`DB_POSTGRESDB_PASSWORD`|`pg_lPGtuwNzQZ70`|
|`DB_POSTGRESDB_PORT`|`5432`|
|`DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED`|`false`|
|`DB_POSTGRESDB_USER`|`neondb_owner`|
|`DB_TYPE`|`postgresdb`|

---

## **4. Tạo Web Service trên Render**

### **Bước 1: Tạo Service**

- Vào **Dashboard** của Render → **New** → **Web Service**.
- **Source Code:** Chọn **"Deploy an existing image from a registry"**.

### **Bước 2: Nhập thông tin Image**

- **Image URL:**
    ```
    docker.io/n8nio/n8n:1.109.2-exp.0
    ```
- **Region:** Chọn **Singapore** (hoặc khu vực gần bạn nhất).

---

## **5. Nhập Environment Variables**

Trong phần **Environment Variables**, thêm toàn bộ các biến sau:

```env
DB_POSTGRESDB_DATABASE=n8n-db
DB_POSTGRESDB_HOST=ep-ed-fog-a10tztqc-pooler.ap-southeast-1.aws.neon.tech
DB_POSTGRESDB_PASSWORD=pg_lPGtuwNzQZ70
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_SSL_REJECT_UNAUTHORIZED=false
DB_POSTGRESDB_USER=neondb_owner
DB_TYPE=postgresdb

N8N_EDITOR_BASE_URL=https://n8n-zafi.onrender.com
N8N_ENCRYPTION_KEY=3451321
N8N_HOST=0.0.0.0
N8N_PORT=5678
N8N_PROTOCOL=https
PORT=5678
WEBHOOK_URL=https://n8n-zafi.onrender.com
```

> ⚠️ **Lưu ý:**
> - `N8N_ENCRYPTION_KEY` là khóa bảo mật, bạn có thể tự tạo ngẫu nhiên.
> - `N8N_EDITOR_BASE_URL` và `WEBHOOK_URL` **ban đầu** dùng tên miền tạm thời của Render.

---

## **6. Thiết lập Command**

Trong phần **Advanced**, mục **Docker Command**, nhập:

```
n8n start
```

---

## **7. Deploy**

- Nhấn **Deploy** và chờ hệ thống chạy.
- Sau khi thành công, truy cập **URL Render** để kiểm tra.

---

## **8. Cập nhật tên miền chính xác**

Sau khi service hoạt động, cần cập nhật lại 2 biến môi trường để đồng bộ với domain thực tế của Render:

```env
N8N_EDITOR_BASE_URL=https://<tên-miền-render>
WEBHOOK_URL=https://<tên-miền-render>
```

> Ví dụ:

```env
N8N_EDITOR_BASE_URL=https://n8n-zafi.onrender.com
WEBHOOK_URL=https://n8n-zafi.onrender.com
```

Sau đó nhấn **Redeploy** để áp dụng thay đổi.

---

## **9. Hoàn tất**

- Truy cập URL Render để vào giao diện n8n.
- Kiểm tra kết nối với Neon DB bằng cách tạo workflow thử nghiệm.

---

## **Tóm tắt quy trình**

1. Lấy **n8n Docker Image** từ Docker Hub.
2. Tạo **PostgreSQL Database** trên Neon.
3. Tạo **Web Service** trên Render và kết nối với database.
4. Nhập biến môi trường và lệnh `n8n start`.
5. Deploy → Cập nhật domain chính xác → Redeploy.
6. Hoàn thành! 🎉