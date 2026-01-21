## Các thành phần xây dựng cốt lõi của ứng dụng Ionic (Core Building Blocks)

Để xây dựng một ứng dụng có thể chạy mượt mà trên cả Web và thiết bị di động (Native App), chúng ta cần nắm vững các trụ cột sau:

### 1. Thành phần giao diện người dùng (UI Components)

Đây là **khối xây dựng quan trọng nhất** trong mọi ứng dụng [[Ionic]].
- **Đặc điểm**: Đẹp mắt và sẵn sàng sử dụng ngay lập tức (out of the box).
- **Tùy biến**: Bạn hoàn toàn có thể thay đổi giao diện thông qua chủ đề và kiểu dáng (Theming & Styling) để phù hợp với bộ nhận diện thương hiệu của doanh nghiệp.

### 2. Điều hướng (Navigation)

Ionic cho phép chuyển đổi giữa các trang mà không cần tải lại toàn bộ tài liệu từ máy chủ.
- **Cơ chế**: Hoạt động theo mô hình ứng dụng đơn trang [[Single Page Application (SPA)]].
- **Công cụ hỗ trợ**: Các thư viện như `Angular Router`, `Vue Router` hoặc `React Router` sẽ điều phối việc hiển thị các phần khác nhau của ứng dụng lên màn hình.
- **Trải nghiệm người dùng**: Hỗ trợ các thao tác quen thuộc trên di động như chạm (tapping) để mở trang mới và nút quay lại (back button).

### 3. Quản lý trạng thái (State Management)

Đề cập đến việc quản lý dữ liệu và thông tin khi ứng dụng đang chạy.
- **Ví dụ**:
    - Trạng thái tải dữ liệu (đang gửi yêu cầu thì hiển thị spinner).
    - Danh sách sản phẩm đã được tải về máy.
- **Hỗ trợ**: Các framework như [[Angular]] cung cấp các công cụ mạnh mẽ để quản lý các dữ liệu phức tạp này.

### 4. Tính năng thiết bị gốc (Native Device Features)

Khi xuất bản ứng dụng lên các cửa hàng (App Stores), ứng dụng sẽ được bọc trong một lớp vỏ ứng dụng gốc (Native App Shell) gọi là **Web View**.
- **Cầu nối (Bridge)**: Cho phép ứng dụng web truy cập vào phần cứng thiết bị.
- **Các tính năng**: Camera, Face ID, Touch ID, Vị trí (Location),...
- **Công nghệ hỗ trợ**:
    - [[Capacitor]]: Do đội ngũ Ionic phát triển (khuyên dùng).
    - [[Cordova]]: Nền tảng cũ hơn nhưng vẫn được hỗ trợ.

### 5. Giao diện dòng lệnh & Quy trình (CLI & Workflow)

Bộ công cụ hỗ trợ toàn bộ vòng đời của ứng dụng:
- **CLI (Command Line Interface)**: Hỗ trợ tạo dự án, chạy thử và kiểm tra.
- **Build & Publish**: Quy trình đóng gói và xuất bản ứng dụng lên các kho ứng dụng.

---

### Tổng kết mô hình ứng dụng Ionic

|**Thành phần**|**Vai trò**|**Công nghệ liên quan**|
|---|---|---|
|**UI Components**|Giao diện & Trải nghiệm|Ionic Web Components|
|**Logic/State**|Xử lý dữ liệu & Luồng|Angular, React, Vue|
|**Native Bridge**|Truy cập phần cứng|Capacitor, Cordova|
|**Deployment**|Đóng gói & Phân phối|Ionic CLI|

---

> [!IMPORTANT] Ghi chú quan trọng
> 
> Cho dù bạn xây dựng ứng dụng phức tạp hay đơn giản, chỉ dành cho Web hay cả Mobile, UI Components luôn là điểm bắt đầu và là yếu tố không thể thiếu.
