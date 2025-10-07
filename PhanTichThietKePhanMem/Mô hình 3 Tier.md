##### **1.1 Mô hình 3 Tier là gì?**

Theo wikipedia: 3-tiers là một kiến trúc kiểu client/server mà trong đó, các yếu tố như:

- Giao diện người dùng (UI-user interface);
- Các quy tắc xử lý(BR-business rule hay BL-business logic);
- Việc lưu trữ dữ liệu được phát triển như những module độc lập.

Là những yếu tố được duy trì trên các nền tảng độc lập. Mô hình 3 tầng (3-tiers) được coi là một kiến trúc phần mềm và là một mẫu thiết kế.

##### **1.2 Các phành phần của 3 Tier**

3 Tier gồm 03 thành phần chính:

- **Presentation tier:** bao gồm các thành phần phần xử lý giao diện Graphic User Interface (GUI). Presentation tỉe dùng để giao tiếp với người dùng. Nhiệm vụ chính là hiển thị dữ liệu và nhận dữ liệu từ người dùng.
- **Business tier:** gồm các thành phần Business Logic Layer (BLL), Data Access Layer (DAL) và Data Tranfer Object (DTO). Được dùng để cung cấp các chức năng của phần mềm
- **Data tier:** lưu trữ dữ liệu, là các hệ quản trị CSDL như MS SQL Server, Oracle, SQLite, MS Access, XML files, text files,…Dùng để lưu trữ dữ liệu, cho phép lớp Business Logic có thể tìm kiếm, trích xuất, cập nhật…

##### **1.3. Ưu điểm và nhược điểm mô hình 3 Tier**

**Ưu điểm:** Dễ dàng mở rộng, thay đổi quy mô của hệ thống: Khi cần tải lớn, người quản trị có thể dễ dàng thêm các máy chủ vào nhóm, hoặc lấy bớt ra trong trường hợp ngược lại.

**Nhược điểm:**
- Việc truyền dữ liệu giữa các tầng sẽ chậm hơn vì phải truyền giữa các tiến trình khác nhau (IPC), dữ liệu cần phải được đóng gói -> truyền đi -> mở gói trước khi có thể dùng được.
- Việc phát triển ứng dụng phức tạp hơn.

