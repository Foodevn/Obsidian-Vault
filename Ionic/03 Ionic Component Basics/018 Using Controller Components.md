Chào bạn, tôi là **tóm tắt**. Chúng ta sẽ cùng tìm hiểu một thành phần đặc biệt: `ion-alert`. Đây là ví dụ hoàn hảo để thấy cách Ionic tự động điều chỉnh giao diện theo hệ điều hành và tại sao việc dùng Framework (như Angular) sẽ giúp chúng ta xử lý logic dễ dàng hơn.

---

## Sử dụng ion-alert và Alert Controller

Thay vì dùng lệnh `alert()` mặc định của trình duyệt (trông khá thô sơ), Ionic cung cấp `ion-alert` để tạo ra các hộp thoại thông báo có giao diện chuẩn Native ([[iOS]] hoặc [[Android]]).

### 1. Alert Controller là gì?

Một số thành phần trong Ionic không hiển thị trực tiếp bằng thẻ HTML mà được điều khiển thông qua một **Controller**.

- **`ion-alert-controller`**: Là một thành phần "vô hình". Nó không vẽ gì lên màn hình nhưng cung cấp các phương thức JavaScript để tạo và hiển thị thông báo.
    
- **Cách cài đặt**: Thêm thẻ `<ion-alert-controller></ion-alert-controller>` vào trong `ion-app`.
    

### 2. Quy trình hiển thị Alert (Vanilla JS)

Để hiển thị một thông báo, bạn cần thực hiện 3 bước trong JavaScript:

1. **Lấy tham chiếu**: Truy xuất controller bằng `querySelector`.
    
2. **Khởi tạo (Create)**: Gọi phương thức `.create()` và truyền vào một đối tượng cấu hình (config object).
    
3. **Hiển thị (Present)**: Vì việc tạo alert là bất đồng bộ (trả về một **Promise**), bạn cần dùng `.then()` để gọi phương thức `.present()`.
    

---

### 3. Thực hành: Mã nguồn thông báo lỗi

Dưới đây là cách chúng ta tích hợp thông báo vào bước kiểm tra dữ liệu:

JavaScript

```
const alertCtrl = document.querySelector('ion-alert-controller');

confirmBtn.addEventListener('click', () => {
  // ... (logic lấy dữ liệu) ...

  if (enteredReason.trim().length <= 0 || enteredAmount <= 0) {
    // Tạo Alert
    alertCtrl.create({
      header: 'Dữ liệu không hợp lệ',
      message: 'Vui lòng nhập lý do và số tiền hợp lệ!',
      buttons: ['Okay']
    }).then(alertElement => {
      // Hiển thị Alert ra màn hình
      alertElement.present();
    });
    return;
  }
  // ... (tiếp tục xử lý nếu dữ liệu đúng) ...
});
```

### 4. Đặc điểm nổi bật

- **Đa nền tảng (Adaptive Styling)**:
    
    - Trên **Android**: Alert hiển thị ở giữa, nút bấm viết hoa toàn bộ (Material Design).
        
    - Trên **iOS**: Alert có các góc bo tròn hơn, nút bấm có ngăn cách (iOS Style).
        
- **Bất đồng bộ**: Việc sử dụng `.then()` đảm bảo rằng mã nguồn chỉ cố gắng hiển thị Alert sau khi nó đã được chuẩn bị xong trong bộ nhớ.
    

---

### So sánh: Vanilla JS vs. Angular (Xem trước)

|**Đặc điểm**|**Vanilla JavaScript**|**Angular (Sắp học)**|
|---|---|---|
|**Khai báo**|Phải thêm thẻ vào HTML|Không cần thẻ HTML|
|**Truy cập**|Dùng `querySelector`|Dùng Dependency Injection (Inject trực tiếp)|
|**Cú pháp**|Dùng Promise (`.then`)|Dùng `async/await` (gọn gàng hơn)|

---

> [!TIP] Mẹo nhỏ
> 
> Khi bạn chuyển đổi giữa các thiết bị mô phỏng trong trình duyệt (ví dụ từ iPhone sang Pixel), hãy nhớ F5 (Reload) trang để Ionic cập nhật lại kiểu dáng phù hợp với thiết bị đó.

**Ứng dụng Budget Planner của chúng ta đã hoàn thiện về mặt tính năng và giao diện! Bạn có muốn tôi tóm tắt lại toàn bộ các thành phần Ionic chúng ta đã sử dụng trong dự án này để lưu vào sổ tay học tập không?**