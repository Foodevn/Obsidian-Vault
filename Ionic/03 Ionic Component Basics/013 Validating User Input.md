Chào bạn, tôi là **tóm tắt**. Chúng ta sẽ cùng nâng cấp logic xử lý dữ liệu bằng cách thêm bước **kiểm tra tính hợp lệ (Validation)** trước khi cho phép dữ liệu được xử lý tiếp.

---

## Kiểm tra dữ liệu đầu vào (Input Validation)

Trước khi lưu trữ hoặc hiển thị dữ liệu, việc kiểm tra xem người dùng có nhập đúng yêu cầu hay không là cực kỳ quan trọng để tránh lỗi ứng dụng.

### 1. Thu thập dữ liệu từ các Web Components

Dù là `<ion-input>`, chúng ta vẫn truy cập dữ liệu thông qua thuộc tính `.value` giống như các thẻ input chuẩn của trình duyệt.

JavaScript

```
const enteredReason = reasonInput.value;
const enteredAmount = amountInput.value;
```

### 2. Logic kiểm tra tính hợp lệ

Chúng ta cần chặn các trường hợp sau:

- **Lý do chi tiêu**: Để trống hoặc chỉ chứa khoảng trắng.
    
- **Số tiền**: Để trống, bằng 0 hoặc là số âm.
    

**Đoạn mã xử lý trong hàm listener:**

JavaScript

```
confirmBtn.addEventListener('click', () => {
  const enteredReason = reasonInput.value;
  const enteredAmount = amountInput.value;

  // Kiểm tra tính hợp lệ
  if (
    enteredReason.trim().length <= 0 || 
    enteredAmount <= 0 || 
    enteredAmount.trim().length <= 0
  ) {
    // Nếu không hợp lệ, thoát hàm (không làm gì thêm)
    return;
  }

  // Nếu hợp lệ, tiếp tục xử lý
  console.log(enteredReason, enteredAmount);
});
```

### 3. Giải thích các phương thức sử dụng

- **`.trim()`**: Loại bỏ các khoảng trắng dư thừa ở đầu và cuối chuỗi. Điều này ngăn người dùng "lách luật" bằng cách chỉ gõ phím Space.
    
- **`length`**: Kiểm tra độ dài của chuỗi sau khi đã trim.
    
- **So sánh số học (`<= 0`)**: Vì `ion-input` loại `number` trả về giá trị số, chúng ta có thể so sánh trực tiếp để loại bỏ số tiền không hợp lệ.
    

---

### Bảng tóm tắt các điều kiện kiểm tra

|**Trường dữ liệu**|**Điều kiện lỗi**|**Hành động**|
|---|---|---|
|**Reason**|`.trim().length <= 0`|Dừng thực thi (`return`)|
|**Amount**|`value <= 0`|Dừng thực thi (`return`)|
|**Amount**|`.trim().length <= 0`|Dừng thực thi (`return`)|

---

> [!TIP] Trải nghiệm người dùng
> 
> Hiện tại, khi nhập sai, ứng dụng chỉ đơn giản là "im lặng". Ở bài học tới, chúng ta sẽ học cách hiển thị một thông báo lỗi chuyên nghiệp bằng [[ion-alert]] để người dùng biết họ cần sửa chỗ nào.

**Logic kiểm tra đã chạy tốt! Tiếp theo, bạn có muốn tôi hướng dẫn cách tạo các phần tử Ionic (như `ion-item`) một cách linh hoạt bằng JavaScript để hiển thị danh sách chi tiêu ngay dưới form không?**