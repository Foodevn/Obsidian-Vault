Chào bạn, đây là ghi chú học tập về cách **xử lý sự kiện (Event Handling)** trong Angular, cụ thể là bắt sự kiện click chuột.

---

## Xử lý Tương tác Người dùng & Liên kết Sự kiện (Event Binding)

Để ứng dụng phản hồi lại hành động của người dùng (như bấm nút), Angular cung cấp cơ chế **Event Binding**.

### 1. Cú pháp Event Binding `( )`

Khác với Property Binding dùng `[ ]` hay String Interpolation dùng `{{ }}`, Event Binding sử dụng cặp dấu ngoặc đơn `( )`.

- **Cú pháp**: `(tên_sự_kiện_gốc)="phương_thức_xử_lý()"`
    
- **Các sự kiện phổ biến**: `(click)`, `(mousedown)`, `(mouseenter)`,...
    

### 2. Thực hành: Bắt sự kiện Click cho nút "Create"

Chúng ta sẽ chỉnh sửa nút bấm trong `PersonInputComponent` để khi người dùng bấm vào, một hàm trong TypeScript sẽ được kích hoạt.

#### Bước 1: Gắn sự kiện trong Template (`.html`)

Mở file `src/app/persons/person-input.component.html`:

HTML

```
<label for="name">Name</label>
<input type="text" id="name">

<button (click)="onCreatePerson()">Create</button>
```

#### Bước 2: Định nghĩa Phương thức trong Class (`.ts`)

Mở file `src/app/persons/person-input.component.ts`. Chúng ta cần khai báo phương thức `onCreatePerson` trùng tên với phương thức đã gọi bên HTML.

TypeScript

```
import { Component } from '@angular/core';

@Component({
  selector: 'app-person-input',
  templateUrl: './person-input.component.html',
  styleUrls: ['./person-input.component.css']
})
export class PersonInputComponent {
  
  // Phương thức xử lý sự kiện
  onCreatePerson() {
    // Tạm thời log ra console để kiểm tra kết nối
    console.log('Created a person!');
  }
}
```

### 3. Kiểm tra kết quả

1. Mở trình duyệt và bật công cụ **Developer Tools** (F12 hoặc chuột phải -> Inspect).
    
2. Chuyển sang tab **Console**.
    
3. Bấm nút **Create** trên giao diện.
    
4. Bạn sẽ thấy dòng chữ `"Created a person!"` xuất hiện trong Console.
    

> **Kết luận**: Chúng ta đã kết nối thành công giao diện (View) với logic xử lý (TypeScript).

---

**Ghi chú:**

- [[Event Binding]]: Cơ chế liên kết luồng thông tin từ View về Logic (Ngược lại với Property Binding).
    
- [[Console Log]]: Công cụ debug cơ bản để kiểm tra code chạy đúng hay không.
    

Bước tiếp theo:

Sự kiện click đã hoạt động, nhưng chúng ta chưa lấy được dữ liệu người dùng nhập vào ô Input. Bạn có muốn tôi hướng dẫn cách lấy giá trị từ ô Input (sử dụng tham chiếu cục bộ hoặc binding 2 chiều) trong bài tiếp theo không?