Chào bạn, tôi là **tóm tắt**. Chúng ta sẽ cùng hoàn thiện phần nhập liệu bằng cách thêm các nút bấm (Buttons) và biểu tượng (Icons), đồng thời tìm hiểu cách tùy chỉnh chúng theo chuẩn giao diện di động.

---

## Làm việc với Buttons, Icons và khái niệm Slots

Sức mạnh của Ionic nằm ở việc kết hợp các thành phần nhỏ để tạo ra giao diện phức tạp mà không cần viết nhiều CSS.

### 1. Tùy chỉnh Nút bấm (ion-button)

Bạn có thể thay đổi ngoại hình của nút thông qua các thuộc tính:

- **`fill`**: Quyết định kiểu đổ màu.
    
    - `solid`: Màu nền đặc (mặc định).
        
    - `outline`: Chỉ có viền, nền trong suốt.
        
    - `clear`: Không viền, không nền (chỉ có chữ).
        
- **`color`**: Sử dụng hệ thống màu mặc định của Ionic (ví dụ: `primary`, `danger`, `success`).
    

### 2. Sử dụng Biểu tượng (ion-icon)

Ionic đi kèm với bộ thư viện biểu tượng miễn phí khổng lồ là **[[Ionicons]]**.

- **Cách dùng**: Truy cập [ionicons.com](https://ionicons.com/) để tìm tên biểu tượng (ví dụ: `add`, `close`, `trash`).
    
- **Cú pháp**: `<ion-icon name="tên-icon"></ion-icon>`.
    

### 3. Khái niệm Slot (Vị trí đặt nội dung)

`slot` là một khái niệm quan trọng trong [[Web Components]], cho phép bạn chỉ định vị trí chính xác của một thành phần bên trong một thành phần khác.

- **`slot="start"`**: Đặt biểu tượng ở phía trước văn bản (bên trái).
    
- **`slot="end"`**: Đặt biểu tượng ở phía sau văn bản (bên phải).
    
- **Tác dụng**: Giúp tự động căn chỉnh khoảng cách (spacing) giữa biểu tượng và chữ một cách chuyên nghiệp.
    

---

### 4. Thực hành: Mã nguồn cho bộ nút điều khiển

Dưới đây là đoạn mã thêm hai nút "Add Expense" và "Clear" vào phía dưới các ô nhập liệu trong `ion-card-content`:

HTML

```
<div class="ion-margin-top ion-text-right">
  <ion-button fill="outline" color="danger">
    <ion-icon slot="start" name="close"></ion-icon>
    Clear
  </ion-button>

  <ion-button>
    <ion-icon slot="start" name="add"></ion-icon>
    Add Expense
  </ion-button>
</div>
```

### 5. Những điểm cần lưu ý

- **Hiệu ứng Ripple**: Trên Android, các nút này sẽ tự động có hiệu ứng "gợn sóng" khi chạm vào, mang lại cảm giác ứng dụng Native thực thụ.
    
- **Tự động thích nghi**: Biểu tượng sẽ tự động thay đổi độ mảnh/đậm tùy theo bạn đang xem trên iOS hay Android.
    

---

> [!CHECK] Thử thách nhỏ
> 
> Bạn có thể thử thay đổi slot="start" thành slot="end" để xem biểu tượng di chuyển sang phía bên phải của chữ như thế nào.

**Các nút bấm đã sẵn sàng! Tiếp theo, bạn có muốn tôi hướng dẫn cách căn lề các nút này sang bên phải và thêm khoảng cách (Margin) để giao diện thoáng đãng hơn không?**