Chào bạn, tôi là **tóm tắt**. Trong bài học này, chúng ta sẽ tìm hiểu cách tinh chỉnh lề, khoảng cách và căn lề văn bản mà không cần viết bất kỳ dòng CSS thủ công nào bằng cách sử dụng các tiện ích của Ionic.

---

## Tiện ích CSS trong Ionic (CSS Utilities)

Ionic cung cấp một bộ các lớp tiện ích (utility classes) giúp bạn xử lý nhanh bố cục như khoảng cách (margin), vùng đệm (padding) và căn lề văn bản (text alignment).

### 1. Thay đổi quan trọng từ Ionic 5

Trước đây, Ionic sử dụng các thuộc tính (attributes) trực tiếp. Tuy nhiên, từ phiên bản 5 trở đi, bạn phải sử dụng **CSS Classes**.

- **Cú pháp cũ**: `<div text-center>` (Không khuyến khích).
    
- **Cú pháp mới**: `<div class="ion-text-center">`.
    
- **Quy tắc**: Luôn thêm tiền tố `ion-` vào trước tên tiện ích và đặt trong thuộc tính `class`.
    

### 2. Các nhóm tiện ích phổ biến

|**Nhóm**|**Ví dụ Class**|**Công dụng**|
|---|---|---|
|**Căn lề (Text)**|`ion-text-right`, `ion-text-center`|Căn trái, phải hoặc giữa cho nội dung bên trong.|
|**Lề (Margin)**|`ion-margin`, `ion-margin-top`|Thêm khoảng cách bên ngoài phần tử.|
|**Đệm (Padding)**|`ion-padding`, `ion-padding-bottom`|Thêm khoảng cách bên trong phần tử.|

---

### 3. Thực hành: Căn lề và tạo khoảng cách cho các nút bấm

Chúng ta sẽ bao bọc hai nút bấm bằng một thẻ `<div>` HTML tiêu chuẩn và áp dụng các lớp tiện ích của Ionic để định dạng.

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

### 4. Lợi ích của việc dùng CSS Utilities

- **Tính nhất quán**: Sử dụng các khoảng cách mặc định của Ionic giúp ứng dụng có vẻ ngoài đồng bộ, chuyên nghiệp.
    
- **Tốc độ**: Không cần tạo file CSS riêng hay đặt tên class mới cho những thay đổi đơn giản.
    
- **Tiêu chuẩn di động**: Các giá trị margin/padding đã được tối ưu cho trải nghiệm chạm (touch) trên màn hình nhỏ.
    

---

> [!IMPORTANT] Lưu ý
> 
> Bạn hoàn toàn có thể sử dụng các thẻ HTML thuần (như div, span, p) bên trong ứng dụng Ionic. Chúng sẽ hoạt động hoàn hảo khi kết hợp với các lớp ion-.

**Phần nhập liệu đã hoàn thiện và trông rất cân đối! Tiếp theo, bạn có muốn tôi hướng dẫn cách tạo danh sách (List) để hiển thị các khoản chi tiêu mà người dùng đã nhập không?**