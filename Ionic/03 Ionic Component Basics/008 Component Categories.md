## Phân loại các thành phần Ionic (Component Categories)

Dù không phải là thuật ngữ chính thức trong tài liệu, việc chia các thành phần thành 3 nhóm sau đây sẽ giúp bạn tư duy thiết kế ứng dụng tốt hơn:

### 1. Thành phần Hiển thị (Output Components)

Dùng để trình bày dữ liệu cho người dùng.
- **Ví dụ**: `ion-img`, `ion-badge`, `ion-label`, `ion-title`, `ion-toolbar`.
- **Đặc điểm**: Tập trung vào việc đưa thông tin lên màn hình.

### 2. Thành phần Bố cục (Layout Components)

Dùng để cấu trúc, sắp xếp và nhóm các thành phần khác lại với nhau.
- **Ví dụ**: `ion-grid`, `ion-list`, `ion-tabs`, `ion-card`.
- **Đặc điểm**: Có thể không hiển thị rõ ràng nhưng giúp kiểm soát vị trí và độ rộng của nội dung.

### 3. Thành phần Nhập liệu (Input Components)

Dùng để người dùng tương tác và nhập dữ liệu.
- **Ví dụ**: `ion-button`, `ion-input`, `ion-textarea`.
- **Đặc điểm**: Cho phép người dùng gõ, nhấn hoặc chọn.


---

## Giải pháp cho vấn đề độ rộng: Hệ thống Lưới (ion-grid)

Khi một thành phần (như `ion-card`) kéo dài hết chiều ngang màn hình lớn, nó trông rất mất cân đối. Để xử lý việc này, chúng ta cần sử dụng sức mạnh của nhóm **Layout Components**, cụ thể là `ion-grid`.

### Hệ thống Lưới (The Grid System)

Hệ thống này dựa trên Flexbox và chia màn hình thành 12 cột ảo. Cấu trúc cơ bản bao gồm:
- **`<ion-grid>`**: Thẻ bao ngoài cùng của hệ thống lưới.
- **`<ion-row>`**: Một hàng nằm trong lưới.
- **`<ion-col>`**: Các cột nằm trong hàng. Bạn có thể quy định một cột chiếm bao nhiêu phần của 12 cột.

### Tại sao dùng ion-grid ở đây?

Bằng cách bao bọc `ion-card` vào trong một hệ thống lưới, chúng ta có thể:
- Giới hạn chiều rộng của Card trên màn hình lớn.
- Căn giữa Card để tạo sự cân đối.
- Tự động giãn ra 100% khi xem trên điện thoại.

---

### Bảng tóm tắt các Layout Components phổ biến

|**Thành phần**|**Công dụng chính**|
|---|---|
|`ion-grid`|Tạo bố cục linh hoạt (Responsive layout)|
|`ion-list`|Hiển thị danh sách các mục dữ liệu|
|`ion-card`|Nhóm nội dung vào một khối có viền và đổ bóng|
|`ion-tabs`|Tạo điều hướng dạng tab ở dưới cùng|

---

> [!IMPORTANT] Tư duy thiết kế
> 
> Khi một giao diện trông "sai sai", hãy kiểm tra xem bạn đã sử dụng đúng các Layout Components để kiểm soát không gian chưa.
