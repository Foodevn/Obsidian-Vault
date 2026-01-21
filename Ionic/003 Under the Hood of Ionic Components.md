## Cách sử dụng và Bản chất của Ionic Components

### 1. Cách sử dụng cơ bản

Các thành phần Ionic thực chất là các **Thành phần Web** (Web Components). Bạn sử dụng chúng tương tự như các thẻ HTML tiêu chuẩn.

- **Cú pháp**: Thêm các thẻ có tiền tố `ion-` vào mã HTML.
    
- **Ví dụ về nút bấm (Button)**:
    

HTML

```
<ion-button color="primary" fill="outline">
  Click Me
</ion-button>
```

- **Thuộc tính (Attributes/Properties)**: Bạn có thể cấu hình thành phần thông qua các thuộc tính (như `color`, `fill`) được đội ngũ Ionic định nghĩa sẵn trong tài liệu chính thức.
    
- **Sự kiện (Events)**: Các thành phần có thể phát ra các sự kiện tùy chỉnh (custom events), ví dụ: `ionChange` cho các ô nhập liệu hoặc dropdown.
    

### 2. Cấu tạo bên dưới (Under the Hood)

Mỗi thành phần Ionic là một sự kết hợp chặt chẽ của 3 yếu tố:

1. **HTML**: Các thẻ HTML thuần (vanilla HTML) được đóng gói bên trong.
    
2. **CSS**: Chứa các kiểu dáng được đóng gói. Sử dụng **Biến CSS** (CSS Variables) như `var(--color)` để dễ dàng thay đổi giao diện từ bên ngoài.
    
3. **JavaScript**: Xử lý logic, quản lý thuộc tính và điều khiển hành vi của thành phần.
    

### 3. Các công nghệ hỗ trợ quan trọng

- **Shadow DOM**: Kỹ thuật giúp đóng gói (encapsulation) kiểu dáng. Điều này đảm bảo CSS của thành phần không làm ảnh hưởng đến các phần khác của ứng dụng và ngược lại.
    
- **Polyfills**: Ionic tự động tải các bản vá mã (polyfills) để đảm bảo các thành phần Web hoạt động ổn định trên cả các trình duyệt cũ không hỗ trợ sẵn tiêu chuẩn này.
    
- **Stencil**: Đây là công cụ (compiler) được đội ngũ Ionic phát triển để xây dựng nên chính các thành phần này. Stencil sử dụng [[TypeScript]] và xuất ra các Web Components thuần túy.
    

### 4. Tra cứu mã nguồn (GitHub)

Bạn có thể kiểm tra cách một thành phần được xây dựng bằng cách truy cập kho lưu trữ mã nguồn mở của Ionic:

- **Đường dẫn**: `Ionic Team / ionic` trên GitHub.
    
- **Thư mục**: `core/src/components`.
    
- **Định dạng file**: `.tsx` (do Stencil sử dụng TypeScript và JSX). Tại đây bạn có thể thấy cách họ định nghĩa các thuộc tính như `disabled`, `type`, hay `color`.
    

---

### Bảng so sánh: HTML thuần vs. Ionic Component

|**Đặc điểm**|**HTML Standard (<button>)**|**Ionic Component (<ion-button>)**|
|---|---|---|
|**Giao diện**|Mặc định của trình duyệt|Đã được thiết kế đẹp, chuẩn mobile|
|**Logic**|Cơ bản|Tích hợp sẵn logic phức tạp|
|**Tùy biến**|CSS truyền thống|Biến CSS (CSS Variables)|
|**Đóng gói**|Không có (Global CSS)|Có (Shadow DOM)|

---

> [!TIP] Mẹo học tập
> 
> Mặc dù việc đọc mã nguồn trên GitHub rất thú vị để hiểu bản chất, nhưng cách nhanh nhất để làm việc là tra cứu Official Docs (Tài liệu chính thức) của Ionic để biết các attributes và events được hỗ trợ.

**Bước tiếp theo, bạn có muốn tôi cùng bạn phân tích chi tiết một thành phần cụ thể (ví dụ: `ion-list` hoặc `ion-card`) để xem cách cấu hình thực tế không?**