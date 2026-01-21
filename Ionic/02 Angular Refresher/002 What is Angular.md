## Tổng quan: Angular là gì?

### 1. Định nghĩa cốt lõi

**Angular** là một [[JavaScript Framework]] chạy ở **phía máy khách (Client-side)**, được sử dụng để xây dựng các giao diện người dùng có tính tương tác cao và phản hồi nhanh ([[Reactive User Interfaces]]).

- **Môi trường hoạt động**: Chạy trực tiếp trên trình duyệt web (Browser), không chạy trên máy chủ (Server) như Node.js hay các ngôn ngữ server-side khác.
- **Ngôn ngữ phát triển**:
    - Mặc dù bản chất là JavaScript, Angular sử dụng **[[TypeScript]]** (một tập siêu - superset của JavaScript) để phát triển.
    - **Lợi ích**: Giúp lập trình viên viết code thuận tiện và chặt chẽ hơn.
    - **Kết quả**: Mã nguồn TypeScript cuối cùng sẽ được biên dịch (compile) thành JavaScript thuần để trình duyệt có thể hiểu và thực thi.

### 2. Vai trò của một "Framework"

Angular cung cấp một tập hợp các **quy tắc** và **công cụ tiện ích (Utility tools)** giúp đơn giản hóa quá trình phát triển:
- **Tự động hóa các tác vụ phức tạp**: Thay vì tự viết logic xử lý từ đầu, Angular hỗ trợ sẵn:
    - **[[HTTP Requests]]**: Gửi và nhận dữ liệu từ server.
    - **[[Routing]]**: Điều hướng và hiển thị nội dung trang dựa trên thao tác người dùng.
    - **[[State Management]]**: Quản lý dữ liệu và trạng thái của ứng dụng.5
- **Tối ưu hóa mã nguồn**: Giúp tạo ra các đoạn mã JavaScript phức tạp và tinh vi một cách dễ dàng, điều mà nếu viết bằng JavaScript thuần (Vanilla JS) sẽ rất khó khăn và tốn thời gian.

### 3. Mục đích sử dụng chính

Angular đặc biệt mạnh mẽ khi xây dựng các ứng dụng web phức tạp:
- **Giao diện phản hồi (Reactive UI)**: Cập nhật nội dung trên trình duyệt ngay lập tức mà không cần tải lại toàn bộ trang (Reload page).
- **Quản lý độ phức tạp**: Giúp kiểm soát logic chặt chẽ trong các ứng dụng lớn, nơi có nhiều tương tác người dùng xảy ra liên tục.

---

**Ghi chú:**

- [[Client-side]]: Phía người dùng, nơi mã chạy trên trình duyệt.
- [[TypeScript]]: Ngôn ngữ phát triển chính của Angular, bổ sung tính năng định kiểu tĩnh (static typing) cho JavaScript.6
