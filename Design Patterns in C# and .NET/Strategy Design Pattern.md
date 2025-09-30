## Mẫu thiết kế Chiến lược (Strategy Design Pattern)

### Khái niệm
- Mẫu thiết kế Chiến lược (Strategy Design Pattern) cho phép xác định một phần hành vi của hệ thống và bổ sung, mở rộng hành vi đó sau này.
- Mục tiêu: Tách biệt các phần cấp cao (high-level) và cấp thấp (low-level) của một thuật toán, giúp tái sử dụng mã nguồn và linh hoạt trong việc thay đổi hành vi.

### Ý tưởng chính
- Nhiều thuật toán có thể được chia thành hai phần:
  - **Phần cấp cao (High-level)**: Các bước chung, áp dụng cho nhiều trường hợp.
  - **Phần cấp thấp (Low-level)**: Các bước cụ thể, đặc trưng cho từng trường hợp.
- Ví dụ: Quy trình pha trà (tea) hoặc cà phê (coffee) có các bước chung (đun sôi nước, rót nước vào cốc) và các bước đặc trưng (thêm túi trà, thêm sữa hoặc chanh).

### Cách hoạt động
- Mẫu Chiến lược cho phép lựa chọn hành vi cụ thể của hệ thống:
  - **Tại thời điểm chạy (Runtime - Dynamic Strategy)**: Hành vi được chọn khi chương trình đang chạy.
  - **Tại thời điểm biên dịch (Compile-time - Static Strategy)**: Hành vi được xác định trước khi chương trình chạy.
- Mẫu này còn được gọi là **Chính sách (Policy)** trong một số ngôn ngữ lập trình, đặc biệt là C++.

### Ví dụ minh họa
- **Quy trình pha đồ uống nóng (Hot Beverage)**:
  - **Bước cấp cao**:
    - Đun sôi nước.
    - Rót nước vào cốc.
  - **Bước đặc trưng (cho trà)**:
    - Thêm túi trà (tea bag) vào nước.
    - Thêm sữa (nếu theo phong cách Anh) hoặc chanh.
  - **Tái sử dụng**: Các bước cấp cao có thể được dùng lại để pha cà phê hoặc sô-cô-la nóng.

### Lợi ích
- Tăng tính tái sử dụng mã nguồn bằng cách tách biệt các phần chung và phần đặc trưng.
- Linh hoạt trong việc thay đổi hành vi của hệ thống mà không cần sửa đổi mã nguồn cốt lõi.

### Ghi chú thêm
- Mẫu Chiến lược thường được sử dụng trong các hệ thống cần thay đổi thuật toán hoặc hành vi một cách động (dynamic) hoặc tĩnh (static).
- Liên kết: [[Mẫu thiết kế (Design Patterns)]] để tìm hiểu thêm về các mẫu thiết kế khác.

---

**Gợi ý liên kết chéo**:
- [[Quy trình pha đồ uống nóng]]: Để xem chi tiết về các bước pha chế.
- [[Dynamic Strategy]]: Tìm hiểu thêm về cách chọn hành vi tại thời điểm chạy.
- [[Static Strategy]]: Tìm hiểu về cách xác định hành vi tại thời điểm biên dịch.