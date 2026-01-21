Chào bạn, tôi là **tóm tắt**. Chúng ta sẽ hoàn thiện ứng dụng bằng cách hiển thị danh sách các khoản chi tiêu ngay dưới form nhập liệu bằng cách sử dụng thành phần `ion-list`.

---

## Hiển thị Danh sách Chi tiêu (ion-list)

Để hiển thị dữ liệu một cách ngăn nắp, chúng ta sử dụng thành phần [[ion-list]]. Đây là một Layout Component giúp quản lý các dòng dữ liệu (items) một cách chuyên nghiệp trên giao diện di động.

### 1. Cấu trúc Layout cho Danh sách

Giống như phần Card nhập liệu, chúng ta cần đặt danh sách vào trong hệ thống [[Grid]] để đảm bảo độ rộng của nó cân đối trên màn hình máy tính.

**Mã HTML bổ sung (dưới Row của Card):**

HTML

```
<ion-row>
  <ion-col size-md="6" offset-md="3">
    <ion-list id="expenses-list"></ion-list>
  </ion-col>
</ion-row>
```

### 2. Tạo phần tử động bằng JavaScript

Thay vì viết sẵn HTML, chúng ta sẽ sử dụng JavaScript để tạo các mục chi tiêu mới mỗi khi người dùng nhấn "Add Expense".

**Các bước thực hiện trong `app.js`**:

1. **Lấy tham chiếu**: Truy xuất danh sách qua ID `expenses-list`.
    
2. **Tạo phần tử**: Sử dụng `document.createElement('ion-item')`.
    
3. **Gán nội dung**: Sử dụng thuộc tính `textContent`.
    
4. **Thêm vào danh sách**: Sử dụng phương thức `appendChild()`.
    

**Mã logic hoàn chỉnh:**

JavaScript

```
const expensesList = document.querySelector('#expenses-list');

confirmBtn.addEventListener('click', () => {
  const enteredReason = reasonInput.value;
  const enteredAmount = amountInput.value;

  if (enteredReason.trim().length <= 0 || enteredAmount <= 0) {
    return;
  }

  // 1. Tạo một ion-item mới
  const newItem = document.createElement('ion-item');
  
  // 2. Định dạng nội dung hiển thị (Ví dụ: Food: $12.99)
  newItem.textContent = enteredReason + ': $' + enteredAmount;

  // 3. Gắn item vào list
  expensesList.appendChild(newItem);
});
```

---

### 3. Bản chất của ion-item

Thành phần [[ion-item]] rất linh hoạt:

- **Trong Form**: Nó dùng để bao bọc `ion-label` và `ion-input`.
    
- **Trong List**: Nó đóng vai trò là một dòng (row) chứa dữ liệu hiển thị.
    
- **Tự động hóa**: Khi nằm trong `ion-list`, các `ion-item` sẽ tự động có các đường kẻ phân cách (borders) chuẩn phong cách di động.
    

### 4. Ionic và Framework (Angular/React/Vue)

Trong bài tập này, chúng ta đang thao tác DOM thủ công (manual DOM manipulation).

- **Sau này**: Khi dùng [[Angular]], Framework sẽ tự động làm những việc này thông qua các chỉ thị như `*ngFor`.
    
- **Quan trọng**: Hãy nhớ rằng Angular không "biên dịch" các thành phần này thành mã khác, nó chỉ tương tác trực tiếp với các [[Web Components]] thông qua các API trình duyệt tiêu chuẩn.
    

---

> [!CHECK] Kết quả
> 
> Giờ đây, mỗi khi bạn nhập dữ liệu và nhấn nút, một dòng mới sẽ xuất hiện ngay bên dưới. Bạn đã tạo ra một ứng dụng thực thụ chỉ với HTML và JavaScript cơ bản!

**Ứng dụng đã hoạt động rất tốt! Bước tiếp theo, bạn có muốn tôi hướng dẫn cách thêm tính năng tính Tổng chi tiêu (Total Expenses) và hiển thị nó ở cuối danh sách không?**