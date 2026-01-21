## Giải phẫu Angular Component (`app.component.ts`)

Trong Angular, một Component không chỉ là một file mã nguồn, nó là sự kết hợp của Logic, Giao diện (Template) và Định dạng (Style). Tất cả được kết nối thông qua **Decorator**.

### 1. Decorator `@Component`

Đây là thành phần cốt lõi biến một Class thông thường thành một Angular Component.

- **Nguồn nhập**: Được import từ thư viện `@angular/core`.
    
- **Chức năng**: Cung cấp siêu dữ liệu (metadata) để Angular hiểu cách xử lý, hiển thị và áp dụng kiểu dáng cho component này.
    

TypeScript

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',                // 1. Định danh thẻ HTML
  templateUrl: './app.component.html', // 2. File giao diện HTML
  styleUrls: ['./app.component.css']   // 3. File kiểu dáng CSS
})
export class AppComponent {
  title = 'my-app';
}
```

### 2. Các thuộc tính cấu hình quan trọng

#### A. `selector` (Bộ chọn)

- **Giá trị**: `'app-root'` (trong ví dụ này).
    
- **Ý nghĩa**: Đây là tên thẻ HTML tùy chỉnh (Custom HTML Tag) đại diện cho component này.
    
- **Cơ chế hoạt động**:
    
    1. Khi ứng dụng khởi động, Angular quét file `index.html`.
        
    2. Nó tìm kiếm thẻ `<app-root></app-root>`.
        
    3. Tại vị trí đó, nó sẽ gắn (mount) toàn bộ nội dung của `AppComponent` vào.
        
    
    > **Lưu ý**: Angular chỉ quét tìm selector của **Root Component** (được khai báo trong `bootstrap` của Module) tại file `index.html`. Các component con khác sẽ được quét trong template của component cha.
    

#### B. `templateUrl` (Giao diện)

- **Giá trị**: Trỏ đến file HTML (ví dụ: `./app.component.html`).
    
- **Cơ chế hiển thị (Rendering)**:
    
    - Angular **không** gửi file HTML này trực tiếp cho trình duyệt.
        
    - Nó phân tích (parse) file HTML này và chuyển đổi thành các chỉ thị JavaScript.
        
    - Khi chạy trên trình duyệt, JavaScript sẽ tạo ra các phần tử DOM động (Dynamic DOM elements).
        

#### C. `styleUrls` (Định dạng)

- **Giá trị**: Một mảng chứa đường dẫn đến các file CSS (ví dụ: `['./app.component.css']`).
    
- **Phạm vi (Scoping)**:
    
    - CSS được viết ở đây chỉ áp dụng cho **riêng component này**.
        
    - **Ví dụ**: Nếu bạn định dạng thẻ `h1` màu đỏ trong file này, chỉ các thẻ `h1` thuộc `AppComponent` mới có màu đỏ. Các thẻ `h1` ở component khác không bị ảnh hưởng.
        

---

## Cơ chế hiển thị: View Source vs. Inspect DOM

Đây là điểm mấu chốt để hiểu về **Client-side Rendering** (Kết xuất phía máy khách) của Angular.

### 1. View Page Source (Xem nguồn trang)

Nếu bạn chuột phải chọn "View Source" trên trình duyệt, bạn sẽ chỉ thấy thẻ:

HTML

```
<body>
  <app-root></app-root>
  </body>
```

→ **Lý do**: Đây là những gì Máy chủ (Server) gửi về. Nó chưa chứa nội dung thực tế của ứng dụng.

### 2. Inspect Element (Kiểm tra phần tử / DOM)

Nếu bạn mở Developer Tools (F12) và xem tab Elements, bạn sẽ thấy:

HTML

```
<app-root>
  <h1>Welcome to my app!</h1>
  <ul>...</ul>
</app-root>
```

→ **Lý do**: Đây là **DOM thực tế** sau khi Angular (JavaScript) đã chạy, tính toán và chèn nội dung vào thẻ `<app-root>`.

---

**Ghi chú:**

- [[DOM]] (Document Object Model): Mô hình các đối tượng tài liệu, cấu trúc cây của trang web.
    
- [[Scoped Styles]]: Kỹ thuật đóng gói CSS để tránh xung đột giao diện giữa các thành phần.
    

Bước tiếp theo:

Bây giờ chúng ta đã hiểu cách một Component được cấu tạo và hiển thị. Bạn có muốn bắt tay vào Tự tạo một Component mới để thực hành quy trình này từ đầu không?