Chào bạn, đây là nội dung ghi chú học tập về **Cơ chế giao tiếp giữa các Component** (cụ thể là truyền dữ liệu từ Cha xuống Con), được biên tập lại từ transcript của bạn.

---

## Giao tiếp giữa các Component: Truyền dữ liệu (Data Binding)

Sau khi đã chia nhỏ ứng dụng thành các Component, việc quan trọng tiếp theo là thiết lập luồng dữ liệu để chúng "nói chuyện" với nhau.

### 1. Định kiểu dữ liệu trong [[TypeScript]]

Trước khi truyền dữ liệu, cần đảm bảo dữ liệu được định nghĩa đúng kiểu. TypeScript hỗ trợ mạnh mẽ việc này:

- **Suy luận kiểu (Type Inference)**: TypeScript tự động hiểu kiểu dữ liệu dựa trên giá trị gán ban đầu.
    
    - Ví dụ: `persons = ['Max', 'Anna']` → TypeScript tự hiểu đây là `string[]` (mảng chuỗi).
        
- **Định kiểu tường minh (Explicit Typing)**: Khai báo rõ ràng kiểu dữ liệu để đảm bảo an toàn.
    
    - Cú pháp: `tên_biến: kiểu_dữ_liệu`.
        

TypeScript

```
// Trong app.component.ts (Component Cha)
export class AppComponent {
  // Khai báo mảng tên người
  persons: string[] = ['Max', 'Manuel', 'Anna'];
}
```

### 2. Truyền dữ liệu từ Cha xuống Con (Parent to Child)

Để truyền dữ liệu từ `AppComponent` (Cha) xuống `PersonsComponent` (Con), chúng ta sử dụng cơ chế **Property Binding** kết hợp với Decorator **`@Input`**.

Quy trình thực hiện gồm 3 bước:

#### Bước 1: Chuẩn bị Component Con (`persons.component.ts`)

Component con cần "mở cổng" để nhận dữ liệu từ bên ngoài. Ta dùng decorator `@Input`.

TypeScript

```
import { Component, Input } from '@angular/core'; // 1. Import Input

@Component({
  selector: 'app-persons',
  templateUrl: './persons.component.html'
})
export class PersonsComponent {
  // 2. Thêm @Input() trước thuộc tính muốn nhận dữ liệu
  // personList là tên thuộc tính sẽ dùng để bind từ bên ngoài
  @Input() personList: string[]; 
}
```

#### Bước 2: Chuẩn bị dữ liệu ở Component Cha (`app.component.ts`)

Như đã khai báo ở mục 1, Component cha đang giữ dữ liệu gốc:

TypeScript

```
persons = ['Max', 'Manuel', 'Anna'];
```

#### Bước 3: Kết nối tại Template của Cha (`app.component.html`)

Sử dụng cú pháp **Property Binding** với dấu ngoặc vuông `[]`.

HTML

```
<app-persons [personList]="persons"></app-persons>
```

**Giải thích cơ chế:**

1. `[personList]`: Target (Đích đến). Đây là tên thuộc tính có `@Input` trong Component con.
    
2. `"persons"`: Source (Nguồn). Đây là tên biến chứa dữ liệu trong Component cha.
    
3. Angular sẽ lấy giá trị của mảng `persons` và gán vào biến `personList` của component con.
    

---

**Ghi chú:**

- [[Property Binding]]: Kỹ thuật liên kết dữ liệu một chiều từ logic (TypeScript) ra giao diện (Template) hoặc giữa các component.
    
- [[Decorator @Input]]: Đánh dấu một thuộc tính là "công khai", cho phép nhận giá trị từ component cha.
    

Bước tiếp theo:

Dữ liệu đã được truyền xuống con thành công, nhưng nó chưa hiển thị lên màn hình. Bạn có muốn tôi hướng dẫn cách sử dụng directive *ngFor để duyệt và hiển thị danh sách này trong bài tiếp theo không?