## Khái niệm Thành phần (Components) trong [[Angular]]

### 1. Tư duy hướng thành phần (Component-driven Development)

Angular xây dựng ứng dụng dựa trên một ý tưởng cốt lõi: chia nhỏ giao diện người dùng thành các phần độc lập gọi là **Components**.

Thay vì nhìn nhận một trang web là một khối code khổng lồ, chúng ta tư duy nó là sự lắp ghép của nhiều mảnh ghép nhỏ.

### 2. Ví dụ phân rã giao diện

Hãy hình dung một trang web điển hình, chúng ta có thể tách nó thành các thành phần riêng biệt:
- **Header Component**: Thanh tiêu đề phía trên.
- **Side Navigation Component**: Thanh điều hướng bên cạnh.
- **List Item Component**: Các mục hiển thị nội dung trong vùng chính.

Các thành phần này sau đó được **kết hợp (compose)** lại với nhau để tạo nên một **Giao diện người dùng (User Interface)** hoàn chỉnh.

### 3. Lợi ích chính: Khả năng tái sử dụng (Reusability)

Đây là ưu điểm lớn nhất của việc sử dụng Components:
- **Định nghĩa một lần**: Bạn chỉ cần thiết lập logic xử lý và giao diện (HTML/CSS) cho một Component (ví dụ: `List Item`) một lần duy nhất.
- **Sử dụng nhiều lần**: Bạn có thể nhúng Component đó vào bất kỳ đâu trong ứng dụng, hoặc lặp lại nó nhiều lần trên cùng một màn hình.

> **Ví dụ**: Trong một danh sách tin tức, bạn thiết kế một `NewsItemComponent`. Nếu trang web cần hiển thị 10 tin tức, bạn chỉ cần tái sử dụng `NewsItemComponent` 10 lần mà không cần viết lại mã nguồn cho từng tin.

---

**Ghi chú:**

- [[User Interface]]: Giao diện tương tác giữa người và máy.
- [[Reusability]]: Khả năng sử dụng lại đoạn mã đã viết, giúp giảm dư thừa và dễ bảo trì.

