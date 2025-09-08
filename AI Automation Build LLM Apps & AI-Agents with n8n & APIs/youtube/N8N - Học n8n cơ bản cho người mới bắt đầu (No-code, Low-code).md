# Ghi chú học tập: Giới thiệu cơ bản về N8N và tự động hóa quy trình

## Tổng quan về N8N

### Khái niệm
- **N8N** là một công cụ mã nguồn mở giúp tự động hóa quy trình (automation) mà không yêu cầu người dùng phải có kỹ năng lập trình chuyên sâu.
- **Mục tiêu**: Giúp người dùng biến ý tưởng thành hiện thực một cách nhanh chóng và chủ động, giảm phụ thuộc vào các chuyên gia công nghệ.
- **Ứng dụng**: Tăng năng suất, tiết kiệm thời gian trong công việc và cuộc sống thông qua tự động hóa các tác vụ.
- **Tầm quan trọng**:
  - Tự động hóa (Automation) là chìa khóa trong thời đại số để tối ưu hóa hiệu quả công việc.
  - N8N "bình dân hóa" tự động hóa, cho phép người dùng không chuyên về lập trình vẫn có thể xây dựng các quy trình (workflow) tự động.

### Đặc điểm nổi bật
- **Đơn giản nhưng mạnh mẽ**: Dễ sử dụng cho người mới bắt đầu, đồng thời đủ linh hoạt để mở rộng quy mô cho các hệ thống phức tạp.
- **Tích hợp đa dạng**: Kết nối với nhiều ứng dụng bên ngoài như Google Sheets, Gmail, Facebook, Telegram, v.v.
- **Miễn phí và trả phí**:
  - Có thể dùng miễn phí trên nền tảng cloud với 14 ngày dùng thử hoặc cài đặt cục bộ (self-hosted) trên máy tính cá nhân hoặc VPS.
  - Phiên bản trả phí (N8N Cloud) giới hạn số lượng workflow hoạt động (active workflows) và có chi phí khoảng 20 euro/tháng.

### Mức độ quan tâm tại Việt Nam và thế giới
- **Toàn cầu**: Lượng tìm kiếm về N8N tăng đột biến trong 6 tháng gần đây (tính đến tháng 8/2025).
- **Việt Nam**: Đứng thứ 4 thế giới về mức độ quan tâm đến N8N, với các khu vực như Đà Nẵng, Hà Nội, TP.HCM dẫn đầu.

---

## Cài đặt N8N

### Cách 1: Sử dụng N8N Cloud
- **Bước thực hiện**:
  - Truy cập trang chủ [n8n.io](https://n8n.io).
  - Nhấn nút **Get Started** và điền thông tin cá nhân.
  - Xác nhận tài khoản qua email để kích hoạt.
  - Sau khi đăng ký, truy cập vào giao diện N8N Cloud với đường dẫn riêng của người dùng.
- **Ưu điểm**:
  - Dễ dàng sử dụng, không cần cài đặt phức tạp.
  - Phù hợp để thử nghiệm và học tập trong 14 ngày miễn phí.
- **Nhược điểm**:
  - Giới hạn 5 active workflows với phiên bản trả phí (20 euro/tháng).
  - Chi phí tăng nếu cần mở rộng quy mô.

### Cách 2: Cài đặt cục bộ trên máy tính cá nhân (Self-hosted)
- **Yêu cầu**:
  - Cài đặt **Node.js** từ [nodejs.org](https://nodejs.org).
  - Kiểm tra phiên bản Node.js và npm qua lệnh:
    ```bash
    node -v
    npm -v
    ```
- **Bước thực hiện**:
  - Tải và cài đặt Node.js (ví dụ: phiên bản v22.14).
  - Mở Command Prompt (cmd) và chạy lệnh để cài đặt N8N:
    ```bash
    npm install n8n -g
    ```
  - Sau khi cài đặt (khoảng 5 phút), chạy lệnh khởi động:
    ```bash
    n8n start
    ```
  - Truy cập N8N tại `localhost:5678`.
  - Tạo tài khoản và xác nhận qua email để kích hoạt.
- **Ưu điểm**:
  - Miễn phí, không giới hạn số lượng active workflows.
  - Phù hợp cho người dùng muốn kiểm soát hoàn toàn hệ thống.
- **Nhược điểm**:
  - Yêu cầu kiến thức kỹ thuật cơ bản để cài đặt và vận hành.
  - Cần thêm cấu hình phức tạp để truy cập từ Internet.

### Cách 3: Cài đặt trên VPS (Khuyến nghị)
- **Bước thực hiện**:
  - Mua VPS đã cài sẵn N8N hoặc tự cài đặt trên VPS chạy Ubuntu với công cụ như **NGINX** và **PM2**.
  - Xem hướng dẫn chi tiết trên kênh YouTube [[Hồng Vũ]] hoặc nhóm cộng đồng.
- **Ưu điểm**:
  - Hoạt động 24/7, kết nối Internet ổn định.
  - Chi phí thấp hơn so với N8N Cloud (rẻ hơn 20 euro/tháng).
  - Không giới hạn active workflows.
- **Nhược điểm**:
  - Yêu cầu kiến thức kỹ thuật để cấu hình VPS hoặc phụ thuộc vào nhà cung cấp cài sẵn.

---

## Giao diện và các thành phần chính của N8N

### Tổng quan giao diện
- **Thanh bên trái (Sidebar)**: Chứa các tab chính như Workflows, Credentials, Executions.
- **Không gian làm việc (Canvas)**: Nơi thiết kế và xây dựng các quy trình tự động (workflows).

### Các thành phần chính
- **Workflows**:
  - Hiển thị danh sách các quy trình đã xây dựng.
  - Mỗi workflow là một chuỗi các bước (nodes) kết nối với nhau.
- **Credentials**:
  - Lưu trữ các khóa xác thực (API keys) để kết nối với các ứng dụng bên ngoài (như [[Google Sheets]], [[Gmail]], [[Facebook]]).
- **Executions**:
  - Ghi lại lịch sử chạy của các workflows, giúp theo dõi tiến trình và lỗi.
- **Settings**:
  - Hiển thị thông tin phiên bản N8N (ví dụ: v1.93).
  - Phiên bản self-hosted hỗ trợ thêm **Community Nodes** để cài đặt các node bên ngoài (như [[Zalo]]), không có trên N8N Cloud.

---

## Node trong N8N

### Khái niệm
- **Node**: Thành phần cơ bản tạo nên một workflow, tương tự các bước trong một quy trình sản xuất.
- **Ví dụ**: Trong quy trình sản xuất giày, các node có thể là:
  - Nhận yêu cầu từ ban giám đốc.
  - Sản xuất giày thô.
  - Cắt chỉ, xỏ dây.
  - Đóng gói thành phẩm.

### Phân loại Node
1. **Trigger Node (Node kích hoạt)**:
   - Kích hoạt workflow khi một sự kiện xảy ra.
   - Đặc điểm: Hình dạng bo tròn hai cạnh, chỉ có đầu ra (output), không có đầu vào (input).
   - Các loại trigger node:
     - **Manual**: Kích hoạt thủ công bằng cách nhấn nút **Test Workflow**.
     - **On a Schedule**: Kích hoạt định kỳ (ví dụ: mỗi giờ, mỗi 30 phút).
     - **On Form Submission**: Kích hoạt khi người dùng gửi dữ liệu qua biểu mẫu (form).
     - **On Chat Message**: Kích hoạt khi nhận tin nhắn từ giao diện chat.
     - **On Webhook**: Kích hoạt khi một ứng dụng bên ngoài gọi đến URL của node (sử dụng công cụ như [[Postman]]).
     - **On Workflow Call**: Kích hoạt bởi một workflow khác (ít sử dụng).
     - **On App Event**: Kích hoạt bởi sự kiện từ ứng dụng (như thêm dữ liệu vào [[Google Sheets]], nhận email trong [[Gmail]], hoặc tin nhắn từ [[Telegram]]).

2. **Action Node (Node hành động)**:
   - Xử lý dữ liệu hoặc thực thi các bước trong workflow.
   - Đặc điểm: Hình vuông, có cả đầu vào (input) và đầu ra (output).
   - Phân loại:
     - **Node ứng dụng**: Kết nối với các ứng dụng phổ biến như [[Google Sheets]], [[Gmail]], [[Facebook]], [[Telegram]].
     - **Node xử lý dữ liệu**:
       - **Code**: Viết mã JavaScript hoặc Python để xử lý dữ liệu (phù hợp với người biết lập trình).
       - **Edit Field**: Lọc hoặc đổi tên các trường dữ liệu (ví dụ: đổi "họ và tên" thành "full_name").
       - **If**: Kiểm tra điều kiện, rẽ nhánh thành **true** hoặc **false**.
       - **Filter**: Lọc dữ liệu theo tiêu chí (ví dụ: chỉ lấy dữ liệu của học sinh nam).
       - **Merge**: Gộp nhiều đầu vào thành một đầu ra (ví dụ: gộp thông tin từ [[Google Sheets]] và [[Facebook]] để gửi qua [[Telegram]]).
       - **Switch**: Rẽ nhánh dựa trên nhiều điều kiện (ví dụ: xử lý các loại vé khác nhau).
       - **Limit**: Giới hạn số lượng dữ liệu đầu ra (ví dụ: lấy 2 bản ghi đầu tiên).
       - **Loop Over Items**: Lặp qua từng phần tử dữ liệu để xử lý riêng lẻ (ví dụ: gửi email cho từng học sinh).
       - **Wait**: Tạm dừng quy trình trong một khoảng thời gian (ví dụ: chờ 5 giây giữa các email để tránh spam).
       - **HTTP Request**: Kết nối với ứng dụng bên ngoài qua API (ví dụ: lấy dữ liệu thời tiết từ [[WeatherAPI]]).
     - **Node AI**:
       - Hỗ trợ tích hợp AI như [[Open AI]], [[Basic LLM]], [[AI Agent]].
       - AI Agent có thêm các thành phần như **chat model**, **memory**, và **tools** để xử lý phức tạp hơn.

---

## Ví dụ thực tế: Xây dựng Workflow với N8N

### Workflow 1: Lưu thông tin đăng ký và gửi email xác nhận
- **Mục tiêu**: Người dùng nhập thông tin qua form, lưu vào [[Google Sheets]], và nhận email xác nhận.
- **Các bước**:
  1. **Trigger Node - On Form Submission**:
     - Tạo form với các trường: **Họ và tên** (bắt buộc), **Email** (bắt buộc).
     - Test form bằng cách nhập thông tin và submit.
  2. **Action Node - Google Sheets (Append Row)**:
     - Tạo **Credential** để kết nối với tài khoản Google.
     - Tạo file Google Sheets với các cột: **Họ và tên**, **Email**.
     - Kéo dữ liệu từ form vào các cột tương ứng.
     - Test để kiểm tra dữ liệu được lưu vào Google Sheets.
  3. **Action Node - Gmail (Send Message)**:
     - Tạo **Credential** cho Gmail.
     - Cấu hình email:
       - **To**: Kéo trường **Email** từ Google Sheets.
       - **Subject**: "Đăng ký xem phim".
       - **Message**: "Chúc mừng bạn {Họ và tên} đã đăng ký thành công!".
     - Test để kiểm tra email được gửi đúng nội dung.
- **Ghi chú thêm**:
  - Để bỏ ghi chú "Sent by n8n" trong email, vào **Options** của node Gmail và tắt **Append n8n signature**.
  - [[Kênh YouTube Hồng Vũ]] có video hướng dẫn chi tiết về cấu hình Credential cho [[Google Sheets]] và [[Gmail]].

### Workflow 2: Phân loại email dựa trên giới tính
- **Mục tiêu**: Thêm trường **Giới tính** vào form, lưu vào [[Google Sheets]], và gửi email với nội dung khác nhau dựa trên giới tính.
- **Các bước**:
  1. **Trigger Node - On Form Submission**:
     - Thêm trường **Giới tính** (dropdown: Nam, Nữ, Không xác định).
     - Test form để kiểm tra dữ liệu.
  2. **Action Node - Google Sheets (Append Row)**:
     - Thêm cột **Giới tính** vào file Google Sheets.
     - Kéo dữ liệu **Giới tính** từ form vào cột tương ứng.
  3. **Action Node - If**:
     - Kiểm tra điều kiện: Nếu **Giới tính** = "Nam" thì rẽ nhánh **True**, ngược lại rẽ nhánh **False**.
  4. **Action Node - Edit Field (True)**:
     - Tạo trường **Message**: "Chúc mừng bạn {Họ và tên} đã đăng ký thành công. Bạn được tặng một chiếc xe đồ chơi."
  5. **Action Node - Edit Field (False)**:
     - Tạo trường **Message**: "Chúc mừng bạn {Họ và tên} đã đăng ký thành công. Bạn được tặng một búp bê đồ chơi."
  6. **Action Node - Gmail (Send Message)**:
     - Kéo **Email** từ Google Sheets và **Message** từ node Edit Field.
     - Test để kiểm tra email đúng nội dung theo giới tính.
- **Ghi chú thêm**: Node **If** chỉ hỗ trợ 2 nhánh (True/False), phù hợp cho điều kiện đơn giản.

### Workflow 3: Phân loại email dựa trên loại vé
- **Mục tiêu**: Thêm trường **Loại vé** (Tiêu chuẩn, Cao cấp, VIP), lưu vào [[Google Sheets]], và gửi email với nội dung ghế khác nhau.
- **Các bước**:
  1. **Trigger Node - On Form Submission**:
     - Thêm trường **Loại vé** (dropdown: Tiêu chuẩn, Cao cấp, VIP).
  2. **Action Node - Google Sheets (Append Row)**:
     - Thêm cột **Loại vé** vào file Google Sheets.
     - Kéo dữ liệu **Loại vé** từ form vào cột tương ứng.
  3. **Action Node - Switch**:
     - Tạo 3 nhánh:
       - Nhánh 0: **Loại vé** = "Tiêu chuẩn".
       - Nhánh 1: **Loại vé** = "Cao cấp".
       - Nhánh 2: **Loại vé** = "VIP".
  4. **Action Node - Edit Field (Nhánh 0)**:
     - Tạo trường **Message**: "Hàng ghế của bạn thuộc số 51 đến 100."
  5. **Action Node - Edit Field (Nhánh 1)**:
     - Tạo trường **Message**: "Hàng ghế của bạn thuộc số 21 đến 50."
  6. **Action Node - Edit Field (Nhánh 2)**:
     - Tạo trường **Message**: "Hàng ghế của bạn thuộc số 1 đến 20."
  7. **Action Node - Gmail (Send Message)**:
     - Kéo **Email** từ Google Sheets và **Message** từ node Edit Field tương ứng.
     - Test để kiểm tra email đúng nội dung theo loại vé.
- **Ghi chú thêm**: Node **Switch** phù hợp khi cần xử lý nhiều nhánh (3 hoặc hơn).

### Workflow 4: Thêm thông tin thời tiết vào email
- **Mục tiêu**: Bổ sung thông tin thời tiết Hà Nội vào email để người dùng chuẩn bị trang phục.
- **Các bước**:
  1. **Trigger Node - On Form Submission**: Tái sử dụng form từ Workflow 3.
  2. **Action Node - Google Sheets (Append Row)**: Tái sử dụng cấu hình từ Workflow 3.
  3. **Action Node - HTTP Request**:
     - Đăng ký tài khoản tại [weatherapi.com](https://www.weatherapi.com) để lấy **API Key**.
     - Cấu hình node:
       - **URL**: `http://api.weatherapi.com/v1/current.json`
       - **Parameters**:
         - `key`: Dán API Key.
         - `q`: "Hanoi" (hoặc thành phố khác).
         - `aqi`: "yes" (lấy thêm dữ liệu chất lượng không khí).
     - Test để kiểm tra dữ liệu thời tiết trả về (nhiệt độ, chất lượng không khí).
  4. **Action Node - Edit Field**:
     - Lọc 2 trường: **Nhiệt độ** (`temp_c`), **Chất lượng không khí** (`air_quality.pm2_5`).
  5. **Action Node - Merge**:
     - Gộp dữ liệu từ node **Edit Field** (thời tiết) và node **Edit Field** (nội dung ghế).
     - Cấu hình **Mode**: Combine để gộp thành một bản ghi.
  6. **Action Node - Gmail (Send Message)**:
     - Cấu hình email:
       - **To**: Kéo **Email** từ Google Sheets.
       - **Subject**: "Đăng ký xem phim".
       - **Message**: 
         ```
         Hàng ghế của bạn: {Message}
         Nhiệt độ tại Hà Nội: {Nhiệt độ}°C
         Chất lượng không khí: {Chất lượng không khí}
         ```
       - Thêm thẻ `<br>` giữa các dòng để xuống dòng trong email.
     - Test để kiểm tra email chứa đầy đủ thông tin.
- **Ghi chú thêm**:
  - Node **HTTP Request** giúp kết nối với các ứng dụng không được N8N hỗ trợ sẵn thông qua API.
  - Thẻ `<br>` trong HTML đảm bảo định dạng xuống dòng trong email.

---

## Ghi chú thêm
- **Lưu workflow**: Luôn nhấn **Save** sau khi xây dựng workflow để tránh mất dữ liệu.
- **Test workflow**: Kiểm tra từng bước để phát hiện và sửa lỗi trước khi kích hoạt.
- **Kích hoạt workflow**: Nhấn nút **Active** để workflow chạy liên tục (yêu cầu cấu hình Credential đầy đủ).
- **Tài nguyên tham khảo**:
  - Xem các video hướng dẫn trên [[Kênh YouTube Hồng Vũ]] để hiểu chi tiết về cấu hình và ứng dụng N8N.
  - Tham gia nhóm [[Facebook]] hoặc [[Zalo]] của Hồng Vũ để trao đổi kinh nghiệm.
- **Liên kết chéo**:
  - [[Google Sheets]]: Ứng dụng lưu trữ và quản lý dữ liệu.
  - [[Gmail]]: Dịch vụ gửi email.
  - [[WeatherAPI]]: Nguồn cung cấp dữ liệu thời tiết qua API.
  - [[Node.js]]: Công cụ cần thiết để cài đặt N8N cục bộ.

---

**Tóm tắt**: N8N là một công cụ mạnh mẽ để tự động hóa quy trình, dễ sử dụng cho cả người không chuyên về lập trình. Các node như Trigger Node và Action Node cho phép xây dựng các workflow linh hoạt, tích hợp với nhiều ứng dụng phổ biến. Các ví dụ thực tế minh họa cách áp dụng N8N vào lưu trữ dữ liệu, gửi email, và tích hợp API bên ngoài.