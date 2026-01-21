## Bố cục cơ bản của một ứng dụng Ionic

Để tạo ra một ứng dụng có giao diện chuẩn di động, Ionic cung cấp các thẻ bao bọc (wrappers) đặc biệt để quản lý không gian và hành vi hiển thị.

### 1. Các thành phần chính (Key Components)

- **`<ion-app>`**:
    - **Vai trò**: Là thẻ bao bọc cấp cao nhất cho toàn bộ ứng dụng.
    - **Lưu ý**: Chỉ sử dụng **duy nhất một lần** trong mỗi file HTML (hoặc trong root component nếu dùng Framework). Nó thiết lập các định dạng CSS toàn cục và hành vi cơ bản của ứng dụng di động.

- **`<ion-header>`**:
    - **Vai trò**: Khu vực đầu trang, thường chứa thanh công cụ.
    - **Đặc điểm**: Khi kết hợp với thanh công cụ bên trong, nó sẽ được cố định ở phía trên cùng của màn hình.

- **`<ion-content>`**:
    - **Vai trò**: Khu vực chứa nội dung chính của ứng dụng.
    - **Đặc điểm**: Tự động quản lý việc cuộn (scrolling) và đảm bảo nội dung không bị che khuất bởi Header hoặc Footer.


### 2. Thanh công cụ và Tiêu đề (Toolbar & Title)

Để tạo thanh tiêu đề cho ứng dụng, chúng ta kết hợp các thẻ sau:

- **`<ion-toolbar>`**: Thanh công cụ nằm trong Header. Bạn có thể thay đổi màu sắc bằng thuộc tính `color`.
- **`<ion-title>`**: Thành phần hiển thị văn bản tiêu đề, tự động căn chỉnh theo chuẩn của từng hệ điều hành ([[iOS]] hoặc [[Android]]).

---

### 3. Thực hành: Mã nguồn cho Header

Dưới đây là đoạn mã để tạo Header màu xanh với tiêu đề "Budget Planner":

```HTML
<ion-app>
  <ion-header>
    <ion-toolbar color="primary">
      <ion-title>Budget Planner</ion-title>
    </ion-toolbar>
  </ion-header>

  <ion-content>
    </ion-content>
</ion-app>
```

### 4. Kiểm tra trên trình duyệt

- Khi lưu file và mở bằng Chrome, bạn sẽ thấy thanh Header màu xanh.
- **Mẹo**: Nhấn `F12`, chọn biểu tượng thiết bị di động (Toggle device toolbar) để giả lập giao diện điện thoại. Bạn sẽ thấy tiêu đề tự động thay đổi vị trí (căn giữa trên iOS hoặc căn trái trên Android) nhờ vào sức mạnh của [[Web Components]].

---

> [!TIP] Quan sát Shadow DOM
> 
> Nếu bạn kiểm tra (Inspect) thẻ <ion-toolbar> trong DevTools, bạn sẽ thấy một phần gọi là #shadow-root. Đây chính là nơi Ionic ẩn các thẻ <div> và CSS nội bộ để tạo nên giao diện phức tạp mà bạn không cần phải tự viết mã.
