Chào bạn, đây là hướng dẫn chi tiết từng bước để **Tạo và Đăng ký một Component mới** trong Angular, dựa trên bài thực hành của bạn.

---

## Hướng dẫn Tạo Angular Component mới

Trong ví dụ này, chúng ta sẽ tạo một Component tên là `PersonsComponent` để quản lý danh sách người.

### Bước 1: Tạo cấu trúc thư mục và File

Để mã nguồn gọn gàng, chúng ta nên tạo thư mục riêng cho từng component.

1. Trong thư mục `src/app`, tạo thư mục con mới tên là `persons`.
    
2. Trong `src/app/persons`, tạo 2 file mới:
    
    - **`persons.component.ts`**: Chứa logic (TypeScript).
        
    - **`persons.component.html`**: Chứa giao diện (Template).
        

### Bước 2: Viết mã cho Component (`.ts`)

Mở file `persons.component.ts` và thêm nội dung sau:

TypeScript

```
import { Component } from '@angular/core'; // 1. Import Decorator

@Component({
  selector: 'app-persons',                 // 2. Đặt tên thẻ HTML tùy chỉnh (quy tắc: app-tên)
  templateUrl: './persons.component.html'  // 3. Liên kết với file HTML
})
export class PersonsComponent {            // 4. Xuất Class (Tên Class viết hoa chữ cái đầu)
  // Logic sẽ viết ở đây sau này
}
```

> **Quy tắc đặt tên**:
> 
> - Tên file: `tên-thành-phần.component.ts` (viết thường, gạch nối).
>     
> - Tên Class: `TenThanhPhanComponent` (PascalCase - Viết hoa chữ cái đầu mỗi từ).
>     

### Bước 3: Viết mã cho Template (`.html`)

Mở file `persons.component.html` và thêm nội dung hiển thị:

HTML

```
<p>List of Persons (Some persons)</p>
```

### Bước 4: Đăng ký Component với Module

Đây là bước bắt buộc để Angular "biết" sự tồn tại của component mới.

Mở file src/app/app.module.ts:

TypeScript

```
// 1. Import Component vừa tạo
import { PersonsComponent } from './persons/persons.component';

@NgModule({
  declarations: [
    AppComponent,
    PersonsComponent // 2. Thêm vào danh sách declarations
  ],
  imports: [ BrowserModule ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

### Bước 5: Sử dụng Component

Bây giờ bạn có thể dùng thẻ <app-persons> ở bất kỳ component nào khác.

Mở file src/app/app.component.html (Template của component gốc) và sửa thành:

HTML

```
<h1>Welcome to Angular!</h1>
<app-persons></app-persons>
```

### Kết quả

Khi chạy ứng dụng (`ng serve`), Angular sẽ:

1. Khởi chạy `AppComponent`.
    
2. Gặp thẻ `<app-persons>`, nó tìm component tương ứng đã đăng ký.
    
3. Chèn nội dung của persons.component.html vào vị trí đó.
    
    → Bạn sẽ thấy dòng chữ "List of Persons" hiện lên trình duyệt.
    

---

**Ghi chú:**

- [[PascalCase]]: Quy tắc đặt tên viết hoa chữ cái đầu mỗi từ (ví dụ: `MyComponent`).
    
- [[Kebab-case]]: Quy tắc đặt tên viết thường nối bằng dấu gạch ngang (ví dụ: `my-component`).
    

Bước tiếp theo:

Bạn có muốn tìm hiểu cách sử dụng Angular CLI để tạo component tự động chỉ bằng một dòng lệnh (nhanh hơn cách thủ công này rất nhiều) không?