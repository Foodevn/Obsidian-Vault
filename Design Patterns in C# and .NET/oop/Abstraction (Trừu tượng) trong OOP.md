Trừu tượng là một nguyên lý cốt lõi của lập trình hướng đối tượng, cùng với **Encapsulation**, **Inheritance** và **Polymorphism**.

---

### Khái niệm

- **Trừu tượng** nghĩa là chỉ thể hiện **những đặc điểm, hành vi quan trọng cần thiết** cho đối tượng, **che giấu chi tiết triển khai cụ thể**.
- Mục tiêu: Tập trung vào _cái gì_ đối tượng làm, không quan tâm _làm như thế nào_.

---

### Cách thực hiện trừu tượng

Trong hầu hết các ngôn ngữ OOP (như Java, C#), trừu tượng được thể hiện qua:

1. **Abstract class (Lớp trừu tượng)**
    - Là lớp không thể tạo đối tượng trực tiếp.
    - Có thể chứa cả:
        - Phương thức trừu tượng (chỉ khai báo, không có thân hàm).
        - Phương thức đã có cài đặt cụ thể.
    - Các lớp con phải _kế thừa_ và _ghi đè_ các phương thức trừu tượng.
2. **Interface (Giao diện)**
    - Chỉ chứa khai báo phương thức (từ Java 8 có thể có default method).
    - Lớp triển khai (implements) interface phải cung cấp toàn bộ cài đặt cho các phương thức.
    - Một lớp có thể triển khai nhiều interface (đa kế thừa hành vi).

---

### Mục đích

- **Giảm phụ thuộc**: Code bên ngoài chỉ quan tâm đến giao diện (API), không quan tâm cách cài đặt
- **Dễ mở rộng & bảo trì**: Có thể thay đổi cài đặt mà không ảnh hưởng đến nơi sử dụng.
- **Tăng tính linh hoạt**: Dễ áp dụng các mẫu thiết kế (Design Pattern) như Strategy, Factory,…