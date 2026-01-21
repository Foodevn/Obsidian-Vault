## Thiết lập Môi trường Phát triển với [[Visual Studio Code]]

Để phát triển ứng dụng Angular hiệu quả, chúng ta sử dụng **Visual Studio Code (VS Code)** – một IDE miễn phí, mạnh mẽ và phổ biến nhất hiện nay.

### 1. Cài đặt và Cấu hình cơ bản

- **Tải xuống**: Tại [code.visualstudio.com](https://code.visualstudio.com/).
- **Mở dự án**: Sử dụng menu **File > Open Folder** để mở thư mục dự án Angular vừa tạo.
- **Giao diện (Theme)**:
    - Nhấn tổ hợp phím `Ctrl + Shift + P` (Windows) hoặc `Cmd + Shift + P` (macOS).
    - Gõ `Theme` và chọn **Color Theme**.
    - Gợi ý: Chọn **Dark+** (giao diện tối mặc định).

### 2. Tiện ích mở rộng (Extensions) khuyên dùng

Mở menu Extensions bằng phím tắt `Ctrl + Shift + X` hoặc `Cmd + Shift + X` và cài đặt các gói sau:
- **Angular Essentials**: Bộ công cụ thiết yếu giúp hỗ trợ code Angular (gợi ý cú pháp, debug, snippet...).
- **Material Icon Theme** (Tùy chọn): Thay đổi biểu tượng file/folder đẹp và dễ nhìn hơn.

---

## Chạy Ứng dụng Angular (Development Server)

Chúng ta không mở trực tiếp file HTML mà phải chạy thông qua một máy chủ phát triển.
### 1. Sử dụng Terminal tích hợp

Thay vì chuyển đổi qua lại giữa các cửa sổ, hãy dùng Terminal ngay trong VS Code:
- Vào menu **Terminal > New Terminal**.
- Terminal sẽ tự động mở tại thư mục gốc của dự án.

### 2. Lệnh khởi chạy

Chạy lệnh sau để bắt đầu máy chủ phát triển:

Bash

```
ng serve
```

**Cơ chế hoạt động của `ng serve`:**
- Sử dụng [[Angular CLI]] để biên dịch mã nguồn.
- Theo dõi các thay đổi trong file (File Watching).
- Tự động tải lại trình duyệt khi bạn lưu code (Live Reload).

### 3. Xem ứng dụng

- Truy cập trình duyệt tại địa chỉ: `http://localhost:4200`
- **Lưu ý quan trọng**: Không được mở trực tiếp file `src/index.html` bằng cách double-click.
    1. **Lý do 1**: File trong `src` chưa được biên dịch và đóng gói (bundled).
    2. **Lý do 2**: Ứng dụng cần giao thức [[HTTP Protocol]] (`http://`) để hoạt động, không phải giao thức tệp tin (`file://`).

---

## Hiểu về Quy trình Biên dịch (Build Process)

Angular sử dụng TypeScript, nên trình duyệt không thể hiểu code gốc bạn viết. Nó cần trải qua quá trình biên dịch.

### So sánh `ng serve` và `ng build`

| **Đặc điểm**    | **ng serve (Development)**                         | **ng build (Production/Inspection)**                         |
| --------------- | -------------------------------------------------- | ------------------------------------------------------------ |
| **Nơi lưu trữ** | Biên dịch và lưu trong **Bộ nhớ RAM** (In-memory). | Tạo ra thư mục vật lý **`dist`** trên ổ cứng.                |
| **Mục đích**    | Dùng để phát triển, debug nhanh.                   | Dùng để kiểm tra kết quả cuối cùng hoặc triển khai (deploy). |
| **Kết quả**     | Không thấy file đầu ra.                            | Thấy rõ các file `index.html`, `main.js`,...                 |

### Phân tích kết quả biên dịch

Khi chạy `ng build`, bạn sẽ thấy thư mục `dist` chứa:

- **`index.html`**: File chạy chính của ứng dụng.
- **`main.js`**: Chứa toàn bộ logic ứng dụng và thư viện Angular đã được biên dịch từ [[TypeScript]] sang [[JavaScript]], đóng gói và tối ưu hóa.

> **Tóm lại**: Chúng ta viết code trong thư mục `src` (dễ đọc, có cấu trúc), nhưng trình duyệt sẽ chạy code trong `dist` (hoặc bộ nhớ ảo của `ng serve`) sau khi đã được Angular CLI xử lý.

---

**Ghi chú:**

- [[IDE]]: Môi trường phát triển tích hợp.
- [[Live Reload]]: Tính năng tự động làm mới trang web khi mã nguồn thay đổi.

