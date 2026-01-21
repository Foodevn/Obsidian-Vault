Chào bạn, đây là ghi chú học tập về cách **hiển thị danh sách dữ liệu** trong Angular sử dụng chỉ thị `*ngFor` và kỹ thuật nội suy chuỗi.

---

## Hiển thị Danh sách với Chỉ thị (Directives)

Sau khi nhận được dữ liệu từ Component cha (thông qua `@Input`), bước tiếp theo là hiển thị danh sách đó lên giao diện (DOM). Angular cung cấp các công cụ mạnh mẽ để xử lý việc lặp dữ liệu ngay trong HTML.

### 1. Khái niệm Chỉ thị (Directive)

- **Định nghĩa**: Directive là các "lệnh hướng dẫn" được đặt trong mã HTML để báo cho Angular biết cần phải làm gì với phần tử DOM đó.
    
- **Vai trò**: Thay đổi cấu trúc hoặc hành vi của các phần tử DOM.
    

### 2. Vòng lặp với `*ngFor`

Để hiển thị một danh sách, thay vì dùng vòng lặp `for` của JavaScript (không hoạt động trực tiếp trong HTML), ta sử dụng directive có sẵn là `*ngFor`.

- **Nguồn gốc**: Được cung cấp bởi `BrowserModule`.
    
- **Cú pháp**: `*ngFor="let <tên_biến_tạm> of <tên_mảng_dữ_liệu>"`
    
- **Lưu ý quan trọng**: Dấu sao `*` trước `ngFor` là bắt buộc. Nó báo hiệu đây là một chỉ thị cấu trúc (Structural Directive) - có khả năng thêm hoặc bớt phần tử khỏi DOM.
    

### 3. Nội suy chuỗi (String Interpolation)

Để xuất giá trị của biến ra màn hình, ta sử dụng cú pháp hai dấu ngoặc nhọn `{{ }}`.

- **Cú pháp**: `{{ tên_biến }}`
    
- **Cách hoạt động**: Angular sẽ lấy giá trị của biến từ logic (TypeScript) hoặc biến tạm trong vòng lặp và chèn vào vị trí tương ứng trong HTML dưới dạng văn bản (Text).
    

### 4. Thực hành: Hiển thị danh sách Person

Chúng ta sẽ chỉnh sửa file template của component con để duyệt qua mảng `personList`.

**File:** `src/app/persons/persons.component.html`

HTML

```
<ul>
  <li *ngFor="let person of personList">
    {{ person }}
  </li>
</ul>
```

**Phân tích luồng dữ liệu:**

1. **Dữ liệu nguồn**: Mảng `['Max', 'Manuel', 'Anna']` từ Component Cha.
    
2. **Truyền xuống**: Qua `@Input() personList` vào Component Con.
    
3. **Vòng lặp**: `*ngFor` chạy 3 lần.
    
4. **Kết quả DOM**: Angular tạo ra 3 thẻ `<li>` tương ứng:
    
    - `<li>Max</li>`
        
    - `<li>Manuel</li>`
        
    - `<li>Anna</li>`
        

---

**Ghi chú:**

- [[Structural Directives]]: Các chỉ thị làm thay đổi cấu trúc DOM (thêm/xóa phần tử), thường bắt đầu bằng dấu `*` (ví dụ: `*ngFor`, `*ngIf`).
    
- [[String Interpolation]]: Kỹ thuật binding dữ liệu một chiều từ Logic ra View.
    

Bước tiếp theo:

Hiện tại chúng ta đang hiển thị dữ liệu tĩnh. Bạn có muốn học cách xử lý sự kiện (Event Handling) để thêm tương tác người dùng, ví dụ như tạo một nút bấm để thêm người mới vào danh sách không?