Chào bạn, tôi là **tóm tắt**. Chúng ta sẽ tiếp tục xây dựng giao diện nhập liệu cho ứng dụng **Budget Planner** bằng cách sử dụng các thành phần Form và Card của Ionic.

---

## Xây dựng Form nhập liệu và sử dụng Card Component

Để giao diện trông chuyên nghiệp và tập trung hơn, chúng ta sẽ không đặt các ô nhập liệu rời rạc mà bao bọc chúng trong một "thẻ" ([[Card]]).

### 1. Thành phần Nhập liệu (Input Components)

Ionic cung cấp cách tổ chức form rất tinh tế thông qua sự kết hợp của 3 thành phần:

- **`<ion-item>`**: Đóng vai trò là một hàng (row) bao bọc, giúp căn chỉnh label và input đồng nhất.
    
- **`<ion-label>`**: Nhãn cho ô nhập liệu. Với thuộc tính `position="floating"`, nhãn sẽ "bay" lên trên khi người dùng nhấn vào ô nhập.
    
- **`<ion-input>`**: Ô nhập liệu thực tế. Bạn có thể quy định kiểu dữ liệu bằng thuộc tính `type` (ví dụ: `text`, `number`, `email`).
    

### 2. Cấu trúc của một Thẻ (Card Structure)

Sử dụng [[ion-card]] giúp tạo ra một khối nội dung có đổ bóng và bo góc, giúp giao diện nổi bật hơn trên màn hình. Cấu trúc chuẩn bao gồm:

- **`<ion-card-header>`**: Chứa tiêu đề của thẻ.
    
- **`<ion-card-title>`**: Định dạng văn bản tiêu đề bên trong header.
    
- **`<ion-card-content>`**: Khu vực chứa nội dung chính (trong trường hợp này là các ô nhập liệu).
    

---

### 3. Thực hành: Mã nguồn cho Form nhập chi tiêu

Dưới đây là đoạn mã nằm bên trong thẻ `<ion-content>`:

HTML

```
<ion-content>
  <ion-card>
    <ion-card-header>
      <ion-card-title>Thêm chi tiêu mới (New Expense)</ion-card-title>
    </ion-card-header>

    <ion-card-content>
      <ion-item>
        <ion-label position="floating">Lý do chi tiêu</ion-label>
        <ion-input type="text"></ion-input>
      </ion-item>

      <ion-item>
        <ion-label position="floating">Số tiền (Amount)</ion-label>
        <ion-input type="number"></ion-input>
      </ion-item>
    </ion-card-content>
  </ion-card>
</ion-content>
```

### 4. Kết quả đạt được

- **Hiệu ứng Floating Label**: Khi bạn click vào ô "Lý do chi tiêu", chữ sẽ thu nhỏ và di chuyển lên trên, tạo không gian cho việc nhập liệu.
    
- **Ràng buộc dữ liệu**: Ô "Số tiền" với `type="number"` sẽ tự động kích hoạt bàn phím số trên thiết bị di động.
    
- **Giao diện Card**: Toàn bộ form được nằm gọn trong một chiếc hộp trắng có đổ bóng nhẹ, tách biệt với nền ứng dụng.
    

---

> [!WARNING] Vấn đề hiển thị
> 
> Hiện tại, trên màn hình máy tính (màn hình rộng), chiếc Card này vẫn kéo dài toàn bộ chiều ngang, trông chưa được tối ưu.

**Bước tiếp theo, bạn có muốn tôi hướng dẫn cách sử dụng hệ thống [[Grid]] (Lưới) của Ionic để giới hạn chiều rộng của Card, giúp ứng dụng trông cân đối hơn trên cả máy tính và điện thoại không?**