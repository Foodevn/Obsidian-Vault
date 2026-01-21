## Vai trò của Angular trong phát triển ứng dụng Ionic

### Yêu cầu tiên quyết (Prerequisite)

- **Kiến thức bắt buộc**: Học viên cần có kiến thức cơ bản về [[Angular]] trước khi tham gia khóa học này.    
- **Module ôn tập (Refresher)**:
    - Khóa học cung cấp một phần ôn tập Angular (tùy chọn) sau module đầu tiên.
    - **Lưu ý**: Phần này chỉ dùng để gợi nhớ kiến thức, không dạy lại Angular từ đầu.

### Tổng quan về [[Angular]]

- **Khái niệm**: Là một [[Framework]] giúp phát triển các ứng dụng web dựa trên JavaScript (JavaScript-driven web apps).
- **Lợi ích chính**:
    - Giúp lập trình viên tập trung vào **logic nghiệp vụ (Business Logic)** thay vì các chi tiết kỹ thuật nhỏ nhặt.
    - Tự động hóa việc kết xuất giao diện người dùng ([[Rendering]] UI).
    - Đảm bảo tuân thủ các thực hành tốt nhất (Best practices), tránh lỗi (bugs) thường gặp khi viết bằng [[Vanilla JavaScript]] thuần túy.

### Ứng dụng một trang ([[Single Page Applications]] - SPA)

Angular được sử dụng để xây dựng SPA với cơ chế hoạt động như sau:
- **Cấu trúc**: Ứng dụng chỉ chạy trên một trang HTML duy nhất.
- **Cơ chế**:
    - JavaScript (thông qua Angular) sẽ liên tục kết xuất lại (re-render) các phần của trang web.
    - Tạo cảm giác như người dùng đang chuyển giữa các trang khác nhau, nhưng thực tế chỉ là thay đổi nội dung nội bộ.
- **Ưu điểm**: Chuyển đổi tức thì, không cần chờ phản hồi tải lại trang từ máy chủ (Server response).

### Tại sao sử dụng Angular với [[Ionic]]?

Trong hệ sinh thái Ionic, Angular giải quyết các vấn đề phức tạp của ứng dụng lớn:
- **Quản lý trạng thái (State Management)**: Xử lý dữ liệu giữa các màn hình khác nhau.
- **Định tuyến (Routing/Navigation)**: Quản lý việc điều hướng và truyền dữ liệu giữa các trang.

### Các lựa chọn thay thế (Alternatives)

Ionic hoạt động độc lập với Framework, bạn có thể sử dụng các công nghệ khác nếu không muốn dùng Angular:

- [[React]]
- [[Vue]]
- [[Vanilla JavaScript]] (Không dùng Framework)

> **Ghi chú cho người dùng Framework khác**: Bạn vẫn có thể tham khảo các phần "Quick Start" đầu tiên của khóa học để hiểu cách các thành phần Ionic (Ionic Components) hoạt động, vì cách sử dụng các thành phần này là giống nhau trên mọi nền tảng.

---

**Ghi chú:**

- [[Routing]]: Kỹ thuật điều hướng giữa các view trong SPA.
- [[Business Logic]]: Phần quy tắc xử lý dữ liệu của ứng dụng.

**Bước tiếp theo:** Bạn có muốn tôi chuẩn bị danh sách các lệnh cài đặt môi trường (Environment Setup) cho bài học tiếp theo không?