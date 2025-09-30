

Đóng gói (Encapsulation) là một trong bốn trụ cột quan trọng của lập trình hướng đối tượng, bên cạnh **Abstraction (Trừu tượng)**, **Inheritance (Kế thừa)** và **Polymorphism (Đa hình)**.

### Khái niệm

- **Đóng gói** nghĩa là ẩn các chi tiết cài đặt bên trong một lớp (class), chỉ cho phép các phần bên ngoài truy cập dữ liệu hoặc hành vi thông qua các phương thức được cung cấp (thường là getter và setter).
    
- Thuộc tính (field) của lớp thường được khai báo **private**, còn phương thức getter/setter là **public**.
    

### Mục đích

1. **Bảo vệ dữ liệu**: Ngăn việc truy cập trực tiếp từ bên ngoài, tránh thay đổi không kiểm soát.
    
2. **Kiểm soát truy cập**: Có thể giới hạn quyền đọc/ghi, hoặc áp dụng logic kiểm tra dữ liệu khi set giá trị.
    
3. **Dễ bảo trì, mở rộng**: Khi thay đổi cách cài đặt bên trong, mã bên ngoài không bị ảnh hưởng miễn là giữ nguyên giao diện (API) public.