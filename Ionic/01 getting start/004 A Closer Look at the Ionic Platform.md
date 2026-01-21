## Hệ sinh thái Ionic (Ionic Ecosystem)

### 1. Kiến trúc cốt lõi

Ionic cho phép bạn xây dựng ứng dụng dựa trên các công nghệ web tiêu chuẩn. Điểm mạnh của nó là sự linh hoạt trong việc kết hợp với các công cụ khác:

- **Ứng dụng Web (Web App)**: Điểm bắt đầu luôn là một ứng dụng web. Bạn có thể phát triển nó thành [[Progressive Web App]] (PWA) để có trải nghiệm nhanh và tin cậy.    
- **Framework Front-end**: Ionic không bắt buộc dùng một framework cụ thể. Bạn có thể sử dụng:
    - [[Angular]] (Trọng tâm của khóa học này).
    - [[React]].
    - [[Vue]].
    - Hoặc thậm chí là [[Vanilla JavaScript]] thuần túy.

### 2. Thành phần Giao diện (UI Components)

Trái tim của Ionic là tập hợp các **Web Components** (Thành phần web).
- **Đặc điểm**: Trông giống như các thẻ HTML thông thường nhưng được tích hợp sẵn logic và giao diện phức tạp.
- **Lợi ích**: Giúp ứng dụng có giao diện chuyên nghiệp và khả năng tương tác cao mà không tốn nhiều công sức tự xây dựng từ đầu.
- **Công nghệ đứng sau**: Các thành phần này được xây dựng bằng [[Stencil]] (một công cụ tạo Web Components của đội ngũ Ionic). _Lưu ý: Bạn không cần học Stencil để sử dụng Ionic._

### 3. Công cụ chuyển đổi sang Native: [[Capacitor]] & [[Cordova]]

Để chạy được trên thiết bị di động như một ứng dụng gốc (Native App), Ionic cần một "cây cầu" kết nối:
- **Vai trò**: Đóng vai trò là lớp trung gian (Bridge) giữa mã nguồn JavaScript và nền tảng Native (iOS/Android).
- **Cơ chế**: Từ mã JavaScript, bạn có thể kích hoạt các chức năng phần cứng của thiết bị thông qua mã Native thực thụ (ví dụ: Mở camera, lấy vị trí GPS, hiển thị thông báo hệ thống).
- **Lựa chọn công cụ**:
    - **Capacitor**: Công cụ hiện đại do chính đội ngũ Ionic phát triển (Được ưu tiên sử dụng trong khóa học).
    - **Cordova**: Giải pháp truyền thống (Có thể dùng kết hợp hoặc thay thế).

### 4. Quy trình phát triển (Workflow)
1. **Viết mã (Code)**: Sử dụng [[Angular]] + [[Ionic Components]].
2. **Quản lý (Tooling)**: Sử dụng [[Ionic CLI]] để quản lý dự án.
3. **Kết nối (Bridge)**: Sử dụng [[Capacitor]] để truy cập tính năng hệ thống.
4. **Xuất bản (Build)**: Tạo ra đồng thời [[Progressive Web App]] và ứng dụng di động cho App Store/Google Play.

---

**Ghi chú:**

- [[Stencil]] là một công cụ mạnh mẽ nếu bạn muốn tự tạo Web Components riêng, nhưng nằm ngoài phạm vi cốt lõi của việc học Ionic.
- Khóa học này sẽ tập trung sâu vào bộ ba: **Ionic + Angular + Capacitor**.

**Bạn có muốn tôi liệt kê chi tiết các lệnh cơ bản trong [[Ionic CLI]] để bạn chuẩn bị cho bài thực hành tiếp theo không?**