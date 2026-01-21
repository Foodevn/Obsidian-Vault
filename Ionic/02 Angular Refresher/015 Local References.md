Chào bạn, đây là ghi chú học tập về kỹ thuật lấy dữ liệu từ người dùng thông qua **Tham chiếu cục bộ (Local Reference)** trong Angular.

---

## Lấy dữ liệu người dùng (User Input) với Tham chiếu cục bộ

Thay vì truy vấn DOM phức tạp, Angular cung cấp một cách đơn giản để tham chiếu trực tiếp đến một phần tử HTML ngay trong Template bằng cách sử dụng dấu thăng `#`.

### 1. Khái niệm Tham chiếu cục bộ ([[Local Reference]])

- **Cú pháp**: Thêm ký tự `#` và một tên tự đặt vào thẻ HTML bất kỳ.
    
    - Ví dụ: `<input #personNameEl>`
        
- **Bản chất**: Biến tham chiếu này (`personNameEl`) sẽ đại diện cho **toàn bộ đối tượng phần tử HTML (DOM Element)** đó, không chỉ riêng giá trị của nó.
    
- **Phạm vi**: Chỉ có thể sử dụng biến này trong phạm vi của Template (file HTML hiện tại).
    

### 2. Các bước thực hiện

Để lấy giá trị từ ô Input và chuyển vào logic xử lý khi người dùng bấm nút:

#### Bước 1: Gắn tham chiếu và truyền tham số trong HTML

Sửa file `person-input.component.html`:

HTML

```
<label for="name">Name</label>
<input type="text" id="name" #personNameEl>

<button (click)="onCreatePerson(personNameEl.value)">Create</button>
```

#### Bước 2: Cập nhật Logic để nhận tham số trong TypeScript

Sửa file `person-input.component.ts` để phương thức `onCreatePerson` có thể nhận dữ liệu đầu vào.

TypeScript

```
export class PersonInputComponent {

  // 3. Khai báo tham số personName với kiểu dữ liệu string
  onCreatePerson(personName: string) {
    console.log('Created a person: ' + personName);
  }
}
```

### 3. Kết quả

1. Người dùng nhập tên (ví dụ: "Max") vào ô Input.
    
2. Nhấn nút "Create".
    
3. Angular lấy giá trị `.value` từ tham chiếu `#personNameEl`.
    
4. Gọi hàm `onCreatePerson("Max")`.
    
5. Console hiển thị: `Created a person: Max`.
    

---

**Ghi chú:**

- [[DOM Element]]: Đối tượng đại diện cho thẻ HTML trong trình duyệt (có các thuộc tính như `value`, `id`, `style`...).
    
- [[Event Binding]]: Kỹ thuật dùng `(click)` để gọi hàm.
    

Bước tiếp theo:

Cách dùng tham chiếu cục bộ (#) rất tốt để lấy dữ liệu một chiều. Tuy nhiên, Angular còn có một kỹ thuật mạnh mẽ hơn gọi là Binding hai chiều (Two-Way Binding), giúp đồng bộ dữ liệu tự động giữa Input và biến TypeScript. Bạn có muốn tìm hiểu về nó ngay bây giờ không?