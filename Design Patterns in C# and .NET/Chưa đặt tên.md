## 1. Cơ bản

- Singleton pattern là gì? Mục đích của nó là gì?
    
- Tại sao chúng ta lại cần Singleton trong thiết kế phần mềm?
    
- Hãy nêu một số ví dụ thực tế về việc sử dụng Singleton.
    
- Điểm khác nhau giữa Singleton và static class là gì?
    
- Bạn có thể liệt kê các bước cơ bản để triển khai một Singleton đơn giản?
    

---

## 2. Trung cấp

- Có những cách nào để triển khai Singleton trong Java/C#? (ví dụ: Eager initialization, Lazy initialization, Double-Checked Locking)
    
- Sự khác nhau giữa Lazy initialization và Eager initialization là gì? Ưu/nhược điểm của mỗi cách?
    
- Giải thích về thread-safety trong Singleton. Làm thế nào để đảm bảo Singleton hoạt động an toàn trong môi trường đa luồng?
    
- Nếu cần cho phép truyền tham số vào khi khởi tạo Singleton thì xử lý ra sao?
    
- Nếu cần kế thừa từ Singleton, bạn sẽ xử lý như thế nào?
    

---

## 3. Nâng cao

- Những nhược điểm hoặc rủi ro khi dùng Singleton là gì?
    
- Singleton vi phạm nguyên lý nào trong SOLID? Tại sao?
    
- Khi serializing và deserializing một Singleton, làm sao để giữ nguyên tính duy nhất của instance?
    
- Bạn sẽ test (unit test) một class Singleton như thế nào?
    
- Trong mô hình kiến trúc lớn (microservices), Singleton còn phù hợp hay không? Tại sao?
    

---

## 4. Tình huống thực tế

- Trong một hệ thống logging (ghi log), bạn sẽ áp dụng Singleton ra sao?
    
- Nếu ứng dụng web của bạn chạy trên nhiều server (distributed system), Singleton có còn đảm bảo một thể hiện duy nhất không? Giải pháp?
    
- So sánh việc dùng Singleton với việc dùng Dependency Injection trong quản lý các service dùng chung.