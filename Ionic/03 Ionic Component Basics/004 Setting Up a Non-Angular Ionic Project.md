Chào bạn, tôi là **tóm tắt**. Trong bài học này, chúng ta sẽ tạm gác lại các Framework phức tạp để quay về với bản chất thuần túy nhất của Ionic thông qua việc sử dụng [[CDN]].

---

## Thực hành: Khởi tạo dự án Ionic thuần (Vanilla Ionic)

### 1. Tại sao lại bắt đầu mà không có Angular?

Mặc dù [[Angular]] là một công cụ mạnh mẽ, việc bắt đầu với một tệp HTML thuần giúp chúng ta:

- **Hiểu rõ bản chất**: Chứng minh rằng [[Ionic Components]] hoạt động độc lập với bất kỳ Framework nào.
    
- **Tập trung tối đa**: Loại bỏ sự nhầm lẫn giữa logic của Angular và các thành phần giao diện của Ionic.
    
- **Trải nghiệm sự linh hoạt**: Ionic có thể được nhúng vào bất kỳ trang web nào chỉ với vài dòng mã.
    

### 2. Thiết lập dự án mẫu: Ứng dụng Quản lý chi tiêu (Budget Planner)

Chúng ta sẽ xây dựng một ứng dụng đơn giản để quản lý danh sách chi tiêu và tính tổng số tiền.

**Các bước chuẩn bị**:

1. Xóa toàn bộ nội dung dự án cũ.
    
2. Tạo tệp `index.html`.
    
3. Sử dụng phím tắt trong VS Code (`html` + `Ctrl + Space`) để tạo cấu trúc HTML5 chuẩn.
    

### 3. Tích hợp Ionic qua CDN

Để sử dụng bộ thư viện Ionic mà không cần cài đặt phức tạp, chúng ta nhúng trực tiếp các liên kết từ máy chủ phân phối nội dung ([[CDN]]).

#### Bước 1: Thêm JavaScript (Logic và Web Components)

Thêm đoạn mã sau vào cuối phần thẻ `<head>`:

HTML

```
<script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
<script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
```

#### Bước 2: Thêm CSS (Giao diện và Định dạng mặc định)

Để các thành phần hiển thị đúng phong cách mobile, bạn cần thêm tệp CSS của Ionic:

HTML

```
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />
```

---

### Cấu trúc tệp `index.html` hoàn chỉnh

HTML

```
<!DOCTYPE html>
<html lang="vi">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Budget Planner</title>
  <link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/@ionic/core/css/ionic.bundle.css" />
  <script type="module" src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.esm.js"></script>
  <script nomodule src="https://cdn.jsdelivr.net/npm/@ionic/core/dist/ionic/ionic.js"></script>
</head>
<body>
  </body>
</html>
```

---

> [!NOTE] Lưu ý quan trọng
> 
> File ionic.bundle.css chứa toàn bộ các biến CSS và kiểu dáng mặc định cần thiết để các thành phần như <ion-button> hay <ion-card> hiển thị đúng. Thiếu file này, các thành phần sẽ mất đi "vẻ ngoài" đặc trưng của ứng dụng di động.

**Bước tiếp theo chúng ta sẽ bắt đầu thêm các thành phần giao diện đầu tiên vào thẻ `<body>`. Bạn có muốn tôi liệt kê các thành phần cần thiết để xây dựng Form nhập liệu chi tiêu không?**