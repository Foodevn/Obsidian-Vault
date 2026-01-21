## Cài đặt Môi trường và Khởi tạo Dự án [[Angular]]

Để bắt đầu làm việc với Angular, chúng ta cần thiết lập các công cụ hỗ trợ để tự động hóa quy trình biên dịch và quản lý dự án.

### 1. Vai trò của [[Angular CLI]]

**Angular CLI** (Command Line Interface) là công cụ dòng lệnh giúp đơn giản hóa việc tạo và quản lý dự án.
- **Tại sao cần CLI?**
    - Angular sử dụng **[[TypeScript]]** (không chạy trực tiếp trên trình duyệt).
    - Dự án cần được **biên dịch (compile)** sang JavaScript, **đóng gói (bundle)** các file lại với nhau và **tối ưu hóa (optimize)** hiệu năng.
    - CLI tự động hóa "ma thuật phía sau hậu trường" (behind the scenes magic) này, giúp bạn tập trung vào viết logic và giao diện thay vì cấu hình hệ thống.

### 2. Cài đặt [[Node.js]] & [[NPM]]

Để cài đặt Angular CLI, bạn cần có **Node Package Manager (NPM)**. NPM đi kèm với bộ cài đặt của **Node.js**.
- **Node.js là gì?**: Môi trường chạy JavaScript phía máy chủ (Server-side runtime). Trong khóa học này, chúng ta không dùng nó để viết code server, mà dùng nó để chạy các công cụ quản lý thư viện.
- **Cách cài đặt**:
    1. Truy cập [nodejs.org](https://nodejs.org/).
    2. Tải và cài đặt phiên bản mới nhất (Latest) hoặc ổn định (LTS).
    3. Sau khi cài xong, bạn sẽ có sẵn công cụ `npm` trong máy.

### 3. Cài đặt Angular CLI

Mở Terminal (trên Mac/Linux) hoặc Command Prompt (trên Windows) và chạy lệnh sau:

```Bash
npm install -g @angular/cli
```

**Lưu ý về quyền truy cập:**

- **Windows**: Thường không cần quyền đặc biệt.
- **macOS / Linux**: Nếu gặp lỗi về quyền hạn (permission denied), hãy thêm `sudo` vào trước câu lệnh:
    ```Bash
    sudo npm install -g @angular/cli
    ```
    _(Sau đó nhập mật khẩu máy tính của bạn khi được yêu cầu)._

### 4. Tạo dự án Angular mới

Sau khi cài đặt xong CLI, bạn có thể tạo dự án đầu tiên theo các bước:
1. **Di chuyển đến thư mục làm việc**: Sử dụng lệnh `cd` để vào thư mục bạn muốn chứa dự án.
2. **Chạy lệnh khởi tạo**:
    ```Bash
    ng new ng-refresher
    ```
    _(Trong đó `ng-refresher` là tên dự án, bạn có thể đặt tùy ý)._
3. **Cấu hình dự án** (Chọn các tùy chọn khi được hỏi):
    - **Would you like to add Angular routing?** (Bạn có muốn thêm định tuyến không?): Chọn **No** (`N`) _(Chúng ta sẽ tìm hiểu về Routing sau)_.
    - **Which stylesheet format would you like to use?** (Định dạng style nào?): Chọn **CSS** (Nhấn Enter để chọn mặc định).

Sau bước này, Angular CLI sẽ tạo một thư mục mới, tải các thư viện cần thiết và thiết lập cấu trúc dự án chuẩn cho bạn.

---

**Ghi chú:**

- [[TypeScript]]: Ngôn ngữ lập trình chính của Angular.
- [[Compilation]]: Quá trình chuyển đổi mã TypeScript sang JavaScript.