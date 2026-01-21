## Cài đặt môi trường phát triển

Để bắt đầu làm việc với Ionic, bạn cần chuẩn bị các công cụ sau trên máy tính của mình:
### 1. Cài đặt [[Node.js]]
- **Vai trò**: Cung cấp môi trường chạy JavaScript ngoài trình duyệt. Ionic cần Node.js để hoạt động.
- **Thành phần quan trọng đi kèm**:
    - **[[NPM]] (Node Package Manager)**: Công cụ quản lý các thư viện phụ thuộc (dependencies) cho dự án, tiêu chuẩn của các dự án web hiện đại.
- **Cách cài đặt**: Tải bộ cài từ trang chủ Node.js (khuyến nghị phiên bản LTS).
- **Kiểm tra**: Sau khi cài đặt, Node.js và NPM sẽ có sẵn trong máy.

### 2. Cài đặt [[Ionic CLI]]

Đây là công cụ dòng lệnh giúp tạo, chạy và quản lý dự án Ionic.
- **Câu lệnh cài đặt** (chạy trong Terminal/Command Prompt):
    ```
    npm install -g @ionic/cli
    ```
    
- **Lưu ý về quyền truy cập**:
    - **Windows**: Nên chạy Command Prompt dưới quyền _Administrator_.
    - **macOS/Linux**: Có thể cần thêm `sudo` phía trước câu lệnh (`sudo npm install...`).

---
## Khởi tạo dự án Ionic

### Quy trình tạo dự án mới
1. Di chuyển đến thư mục muốn lưu dự án.
2. Chạy lệnh:
    ```
    ionic start
    ```
3. **Cấu hình dự án** (theo hướng dẫn của CLI):
    - **Tên dự án**: Ví dụ `ionic-angular-course`.
    - **Framework**: Chọn Angular.
    - **Template (Mẫu giao diện)**:
        - `blank`: Dự án rỗng (Sẽ dùng trong khóa học này để học từ đầu).
        - `tabs`: Giao diện có các tab ở đáy.
        - `sidemenu`: Giao diện có menu trượt từ bên cạnh.
    - **Ionic Appflow**: Chọn `No` (Không cần thiết lúc này).

### Chạy ứng dụng (Development Server)

- Di chuyển vào thư mục dự án vừa tạo: `cd ten-du-an`.
- Chạy lệnh:
    ```
    ionic serve
    ```
- **Cơ chế hoạt động**:
    - Lệnh này sử dụng **[[Angular CLI]]** bên dưới để tạo máy chủ phát triển cục bộ.
    - Hỗ trợ **Live Reload**: Tự động tải lại trang khi bạn sửa code.
    - Ứng dụng sẽ chạy trên trình duyệt (thường là cổng 8100).

---

## Công cụ soạn thảo (IDE) & Mẹo phát triển

### 1. [[Visual Studio Code]] (VS Code)
Đây là IDE được khuyến nghị sử dụng.
- **Extensions (Tiện ích mở rộng) nên cài**:
    - **Angular Essentials**: Bộ công cụ hỗ trợ code Angular.
    - **Material Icon Theme**: (Tùy chọn) Giúp hiển thị icon file đẹp và dễ nhìn hơn.

### 2. Mô phỏng thiết bị di động

Để xem ứng dụng hiển thị như thế nào trên điện thoại ngay trên trình duyệt Chrome:

1. Mở **Developer Tools** (F12 hoặc chuột phải -> Inspect).
2. Nhấn vào biểu tượng **Toggle Device Toolbar** (hình điện thoại/máy tính bảng).
3. Chọn thiết bị mong muốn (ví dụ: Pixel 2, iPhone X) và tải lại trang.

---

## Viết ứng dụng đầu tiên ("Hello World")

Chúng ta sẽ chỉnh sửa file để thay đổi nội dung hiển thị. Cấu trúc thư mục Ionic tương tự như Angular thông thường.

### File: `home.page.html`

Sử dụng các **Ionic Web Components** (bắt đầu bằng `ion-`) kết hợp với cú pháp binding của Angular.

```HTML
<ion-header>
  <ion-toolbar>
    <ion-title>Ionic Blank</ion-title>
  </ion-toolbar>
</ion-header>

<ion-content class="ion-padding">
  <p>{{ text }}</p>

  <ion-button (click)="onChangeText()">
    Change Text
  </ion-button>
</ion-content>
```

### File: `home.page.ts`

Xử lý logic nghiệp vụ bằng TypeScript (chuẩn Angular).

```TypeScript
import { Component } from '@angular/core';

@Component({
  selector: 'app-home',
  templateUrl: 'home.page.html',
  styleUrls: ['home.page.scss'],
})
export class HomePage {
  // 1. Khai báo thuộc tính
  text = 'Default starting text';

  constructor() {}

  // 2. Phương thức xử lý sự kiện
  onChangeText() {
    this.text = 'Changed!';
  }
}
```

### Tính năng tự động thích ứng (Platform Adaptability)

Ionic tự động điều chỉnh giao diện dựa trên nền tảng thiết bị:
- **iOS**: Giao diện phẳng, chuẩn Apple.
- Android: Sử dụng Material Design (ví dụ: hiệu ứng Ripple - gợn sóng khi bấm nút).
    → Bạn viết một mã nguồn, Ionic tự lo phần hiển thị chuẩn native.
