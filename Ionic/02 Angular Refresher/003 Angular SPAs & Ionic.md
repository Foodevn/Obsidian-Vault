## Angular và Mô hình Ứng dụng Một trang (SPA)

### 1. Tổng quan ngữ cảnh

- **Thông thường**: Angular được dùng để xây dựng các ứng dụng web chạy trên trình duyệt.
- **Trong khóa học này**: Angular kết hợp với **[[Ionic]]** để xây dựng ứng dụng di động gốc (Native Mobile Apps).

### 2. Khái niệm [[Single Page Application]] (SPA)

Hầu hết các ứng dụng Angular đều hoạt động theo mô hình SPA.
- **Cấu trúc**: Ứng dụng chỉ có **duy nhất một file HTML** (thường là `index.html`) được gửi từ máy chủ về trình duyệt.
- **Cơ chế tải**: Trên file HTML này, trình duyệt sẽ tải một tệp lệnh (Script) chứa toàn bộ mã nguồn Angular (Framework + Logic ứng dụng của bạn).

### 3. Quy trình Xử lý Kỹ thuật

Để tạo ra SPA, Angular sử dụng quy trình biên dịch hiện đại:
1. **Viết mã**: Lập trình viên viết mã bằng **[[TypeScript]]** (Cấu trúc rõ ràng, dễ quản lý).
2. **Biên dịch (Compile)**: TypeScript được chuyển đổi thành **[[JavaScript]]** (để trình duyệt hiểu được).
3. **Đóng gói (Bundle)**: Mã ứng dụng + Thư viện Angular được đóng gói thành các file JavaScript.
4. **Thực thi**: File `index.html` nhập (import) gói JavaScript này và Angular bắt đầu kiểm soát giao diện.

### 4. Cơ chế Hiển thị (Rendering) & Trải nghiệm người dùng

Angular tạo ra ảo giác về việc "chuyển trang", nhưng thực tế về mặt kỹ thuật:
- **Kết xuất lại (Re-rendering)**: Angular liên tục vẽ lại (re-render) các phần tử HTML trên giao diện dựa trên tương tác người dùng.
- **Không tải lại trang**: Trình duyệt không cần gửi yêu cầu tải trang HTML mới từ máy chủ mỗi khi người dùng bấm nút.

### 5. Ưu điểm & Sự phù hợp với Mobile App

Mô hình SPA biến Angular thành ứng viên hoàn hảo cho việc phát triển ứng dụng di động với Ionic:
- **Hiệu năng cao**: Mọi thứ chạy trên trình duyệt (Client-side) nên phản hồi gần như tức thì.
- **Trải nghiệm mượt mà**: Cảm giác sử dụng giống hệt ứng dụng Native (ấn là chạy, không chờ loading trang trắng).
- **Hoạt động Offline**: Do mã đã được tải về, ứng dụng vẫn có thể hoạt động cơ bản khi mất kết nối internet tạm thời.
- **Xử lý nền**: Việc lấy dữ liệu mới từ Database được thực hiện ngầm (Background Fetching) mà không làm gián đoạn giao diện.

---

**Ghi chú:**

- [[TypeScript]]: Ngôn ngữ lập trình chính để viết Angular, sẽ được biên dịch sang JavaScript.
- [[Client-side]]: Quá trình xử lý diễn ra tại thiết bị người dùng (trình duyệt/điện thoại) thay vì máy chủ.
