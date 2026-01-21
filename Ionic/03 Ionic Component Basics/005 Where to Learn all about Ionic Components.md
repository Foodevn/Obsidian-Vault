## Khám phá Hệ thống Thành phần Ionic qua Tài liệu chính thức

Ionic cung cấp một kho tàng hơn 100 [[Thành phần giao diện]] (UI Components) được xây dựng sẵn. Việc ghi nhớ toàn bộ là không thể, vì vậy kỹ năng quan trọng nhất là biết cách tra cứu tài liệu.
### 1. Nguồn tài liệu đáng tin cậy (The Source of Truth)

Tài liệu chính thức tại **[ionicframework.com/docs](https://ionicframework.com/docs)** là nơi tốt nhất để tra cứu vì:
- **Luôn cập nhật**: Nội dung được tạo tự động từ mã nguồn thực tế.
- **Trực quan**: Có trình mô phỏng hiển thị giao diện theo phong cách [[iOS]] và [[Material Design]] (Android).

### 2. Cấu trúc thông tin của một Thành phần (Component)

Khi xem một thành phần cụ thể (ví dụ: `ion-button`), tài liệu sẽ cung cấp:
- **Mô tả & Cách dùng**: Giải thích chức năng và các chế độ cấu hình cơ bản (ví dụ: `fill="outline"` hoặc `fill="solid"`).
- **Ví dụ mã nguồn (Usage Examples)**: Cung cấp các đoạn mã mẫu cho nhiều nền tảng như [[JavaScript]] thuần, [[Angular]], [[React]], hoặc [[Vue]].
- **Thuộc tính (Properties)**: Danh sách các giá trị bạn có thể truyền vào thông qua `attributes` để điều chỉnh hành vi của thành phần.
- **Sự kiện tùy chỉnh (Events)**: Các sự kiện riêng do Ionic định nghĩa (ví dụ: `ionFocus`, `ionBlur`) bên cạnh các sự kiện HTML mặc định như `click`.
- **Thuộc tính CSS (CSS Custom Properties)**: Danh sách các biến CSS bạn có thể ghi đè để thay đổi màu sắc, khoảng cách mà không phá vỡ cấu trúc [[Shadow DOM]].

### 3. Cách tiếp cận để học tập hiệu quả

- **Không học thuộc lòng**: Hãy học thông qua việc thực hành dự án thực tế.
- **Tra cứu theo nhóm**: Sử dụng danh mục nhóm các thành phần ở cột bên trái tài liệu (như Buttons, Cards, Forms, v.v.) để tìm thành phần phù hợp với nhu cầu.

---

### Bảng tóm tắt các thông tin tra cứu nhanh

|**Mục tra cứu**|**Mục đích**|
|---|---|
|**Properties**|Biết được có thể cấu hình những gì (ví dụ: `disabled`, `expand`).|
|**Events**|Biết khi nào thành phần phản hồi hành động của người dùng.|
|**CSS Shadow Parts**|Cách để can thiệp vào kiểu dáng bên trong của Web Component.|
|**Framework Integration**|Cách cú pháp thay đổi giữa Angular, React và Vue.|

---

> [!TIP] Mẹo nhỏ
> 
> Khi xây dựng ứng dụng [[Budget Planner]], chúng ta sẽ thường xuyên mở song song trang tài liệu này để kiểm tra các thuộc tính của ion-input và ion-item.
