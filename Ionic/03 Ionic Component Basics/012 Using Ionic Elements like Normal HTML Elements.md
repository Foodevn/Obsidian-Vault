Chào bạn, tôi là **tóm tắt**. Chúng ta đã hoàn thiện phần giao diện, bây giờ là lúc thêm "linh hồn" cho ứng dụng bằng cách sử dụng **JavaScript thuần (Vanilla JavaScript)** để xử lý các sự kiện click và đọc dữ liệu.

---

## Thêm Logic cho ứng dụng với JavaScript thuần

Một trong những điểm mạnh nhất của Ionic (từ phiên bản 4 trở đi) là tính tương thích cực cao. Vì các thành phần Ionic là [[Web Components]] chuẩn, bạn có thể tương tác với chúng y hệt như các thẻ HTML bình thường (`div`, `button`, `input`).

### 1. Thiết lập tệp Script

Để bắt đầu, chúng ta cần tạo một tệp JavaScript riêng biệt để giữ cho mã nguồn sạch sẽ.

- **Tạo tệp**: `app.js`.
    
- **Nhúng vào HTML**: Thêm thẻ `<script>` vào cuối thẻ `<body>` để đảm bảo trình duyệt đã tải xong giao diện trước khi thực thi code.
    

HTML

```
<script src="app.js"></script>
```

### 2. Định danh các thành phần (Assigning IDs)

Để JavaScript có thể "tìm thấy" các ô nhập liệu và nút bấm, chúng ta gán thuộc tính `id` cho chúng trong file HTML.

|**Thành phần**|**Thuộc tính ID**|
|---|---|
|Ô nhập lý do|`input-reason`|
|Ô nhập số tiền|`input-amount`|
|Nút Hủy (Cancel)|`btn-cancel`|
|Nút Thêm (Confirm)|`btn-confirm`|

### 3. Truy xuất phần tử trong JavaScript

Trong `app.js`, chúng ta sử dụng `document.querySelector` để lấy tham chiếu đến các thành phần Ionic.1

JavaScript

```
const reasonInput = document.querySelector('#input-reason');
const amountInput = document.querySelector('#input-amount');
const cancelBtn = document.querySelector('#btn-cancel');
const confirmBtn = document.querySelector('#btn-confirm');
```

### 4. Lắng nghe sự kiện Click (Event Listeners)

Sau khi đã có tham chiếu, chúng ta thêm trình lắng nghe sự kiện `click`. Khi người dùng nhấn nút "Add Expense", một hàm sẽ được kích hoạt.

JavaScript

```
confirmBtn.addEventListener('click', () => {
  const enteredReason = reasonInput.value;
  const enteredAmount = amountInput.value;

  // Kiểm tra thử xem đã lấy được dữ liệu chưa
  console.log(enteredReason, enteredAmount);
});
```

---

### Tại sao điều này quan trọng?

- **Tính độc lập**: Bạn thấy đấy, chúng ta không cần [[Angular]], [[React]] hay [[Vue]] để làm cho các thành phần Ionic hoạt động.
    
- **Tương tác chuẩn**: Thuộc tính `.value` trên `<ion-input>` hoạt động giống hệt như trên thẻ `<input>` thuần túy. Điều này giúp giảm bớt rào cản học tập nếu bạn đã biết JavaScript cơ bản.
    

---

> [!CHECK] Kiểm tra kết quả
> 
> Hãy mở Developer Tools (F12) -> tab Console. Nhập thông tin vào form và nhấn nút "Add Expense". Nếu bạn thấy nội dung đã nhập hiện lên trong Console, nghĩa là bạn đã kết nối thành công!

**Logic cơ bản đã chạy! Tiếp theo, bạn có muốn tôi hướng dẫn cách kiểm tra dữ liệu đầu vào (Validation) để đảm bảo người dùng không nhập trống hoặc nhập số tiền âm không?**