Chào bạn, đây là bản tóm tắt các bước **Tạo Component nhập liệu** (`PersonInputComponent`) để chuẩn bị cho việc xử lý tương tác người dùng.

---

## Tạo Component xử lý nhập liệu

Chúng ta sẽ tạo một component mới có chức năng nhận đầu vào từ người dùng (Input) và một nút bấm (Button) để thêm dữ liệu.

### Bước 1: Tạo cấu trúc File

Trong thư mục `src/app/persons`, tạo 3 file mới:

- `person-input.component.ts` (Logic)
    
- `person-input.component.html` (Giao diện)
    
- `person-input.component.css` (Định dạng)
    

### Bước 2: Thiết lập Logic Component (`.ts`)

Mở file `person-input.component.ts` và cấu hình:

TypeScript

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-person-input',                // Tên thẻ: <app-person-input>
  templateUrl: './person-input.component.html',
  styleUrls: ['./person-input.component.css']  // Liên kết file CSS
})
export class PersonInputComponent {
  // Logic xử lý sẽ thêm ở đây
}
```

### Bước 3: Đăng ký Component

Đừng quên bước quan trọng này! Mở `src/app/app.module.ts`:

1. Import `PersonInputComponent`.
    
2. Thêm vào mảng `declarations`.
    

### Bước 4: Thiết kế Giao diện (`.html`)

Mở file `person-input.component.html` và thêm các phần tử HTML cơ bản:

HTML

```
<label for="name">Name</label>
<input type="text" id="name">
<button>Create</button>
```

### Bước 5: Định dạng (`.css`)

Để giao diện gọn gàng hơn, ta thêm chút CSS vào `person-input.component.css`:

CSS

```
label, input, button {
  display: block; /* Hiển thị mỗi phần tử trên một dòng riêng biệt */
  margin-bottom: 10px;
}
```

### Bước 6: Sử dụng Component

Cuối cùng, nhúng component này vào trang chính. Mở `src/app/app.component.html`:

HTML

```
<app-person-input></app-person-input>

<app-persons [personList]="persons"></app-persons>
```

---

Kết quả hiện tại:

Trên trình duyệt, bạn sẽ thấy một ô nhập liệu và nút "Create" nằm phía trên danh sách tên. Tuy nhiên, bấm nút lúc này chưa có tác dụng gì cả.

Bước tiếp theo:

Bạn có muốn tôi hướng dẫn cách lắng nghe sự kiện click ((click)) và lấy dữ liệu từ ô input để thêm vào danh sách không?