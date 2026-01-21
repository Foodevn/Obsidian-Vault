## So sánh quan trọng: Ionic 3 vs Ionic 4

### 1. Tài liệu chuyển đổi (Migration)

Nếu bạn đang có một dự án Ionic 3 và muốn nâng cấp, trang chủ Ionic cung cấp tài liệu hướng dẫn chi tiết từng bước.

- **Nguồn tài liệu**: `ionicframework.com` → **Developers** → **Guide** → **Migration**.
- **Nội dung**: Hướng dẫn chi tiết về những thay đổi trong mã nguồn (code) và cấu hình cần thiết để cập nhật.

### 2. Sự thay đổi về Quy trình & Kiến trúc

#### **Ionic 3 (Cũ)**

- **Phụ thuộc chặt chẽ**: Bắt buộc dùng **[[Ionic CLI]]** để tạo dự án.
- **Công cụ Bridge**: Chỉ tập trung sử dụng **[[Cordova]]** để đóng gói ứng dụng di động.
- **Trọng tâm**: Mục tiêu chính là tạo ra **Mobile App**. Mặc dù có thể tạo [[Progressive Web App]] (PWA), nhưng đó chỉ là tính năng phụ.
- **Bản chất**: Là một dự án Ionic đặc thù, gắn liền với Angular.

#### **Ionic 4+ (Mới & Hiện tại)**

- **Tính linh hoạt (Flexibility)**:
    - Vẫn có thể dùng **[[Ionic CLI]]**.
    - **Mới**: Có thể nhúng trực tiếp qua **[[CDN]]** hoặc cài đặt qua **[[NPM]]** mà không cần CLI hay quy trình build phức tạp (do không còn phụ thuộc Framework).

- **Bản chất dự án**:
    - Là một **Dự án Web chuẩn (Standard Web Project)**.
    - Với Angular: Sử dụng **[[Angular CLI]]** bên dưới (thừa hưởng toàn bộ tính năng của Angular).
    - Tương tự cho [[React]] hay [[Vue]].

- **Đa năng**: Đầu ra là một ứng dụng web tiêu chuẩn, dễ dàng chuyển đổi thành PWA hoặc Native App.

### 3. Công cụ kết nối Native (Native Bridge)

Sự thay đổi lớn về cách ứng dụng web giao tiếp với phần cứng điện thoại:
- **Ionic 3**: Phụ thuộc hoàn toàn vào **[[Cordova]]**.
- **Ionic 4+**:
    - Hỗ trợ cả **[[Cordova]]**.
    - **Khuyến nghị**: Sử dụng **[[Capacitor]]** - công cụ mới hiện đại hơn, ổn định hơn do chính đội ngũ Ionic phát triển (Khóa học này sẽ sử dụng Capacitor).


### Tổng kết

Chủ đề chính của sự thay đổi từ Ionic 3 sang 4 là: **Tăng tính linh hoạt - Tăng độ ổn định - Tăng tốc độ**.

---

**Ghi chú:**

- [[CDN]] (Content Delivery Network): Mạng lưới phân phối nội dung, cho phép nhúng thư viện vào web qua đường dẫn URL mà không cần tải về.
- [[NPM]]: Trình quản lý gói của Node.js.

**Bước tiếp theo:** Bạn có muốn tôi đi sâu vào chi tiết kỹ thuật về **[[Capacitor]]** và tại sao nó lại được coi là sự thay thế vượt trội cho Cordova trong bài tiếp theo không?