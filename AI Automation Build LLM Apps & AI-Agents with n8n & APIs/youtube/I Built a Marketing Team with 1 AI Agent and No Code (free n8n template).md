# Ghi chú học tập: Xây dựng đội ngũ tiếp thị AI với một tác tử AI

## Tổng quan
- **Mục tiêu**: Hiểu cách xây dựng một tác tử AI (AI agent) để thực hiện các nhiệm vụ tiếp thị như tạo video, bài đăng LinkedIn, bài blog, tạo và chỉnh sửa hình ảnh, cũng như tìm kiếm cơ sở dữ liệu hình ảnh.
- **Nội dung chính**: Tác tử AI sử dụng 6 công cụ, được tích hợp trong một quy trình làm việc (workflow) trên nền tảng n8n, giao tiếp qua Telegram (bằng giọng nói hoặc văn bản).
- **Ứng dụng**: Tự động hóa các tác vụ tiếp thị, giảm thời gian và chi phí, phù hợp cho người làm tiếp thị hoặc nhà phát triển muốn tích hợp AI.

---

## Công cụ và chức năng

### 1. Tổng quan về các công cụ
- Tác tử AI có khả năng sử dụng 6 công cụ chính:
  - **Tạo video**: Tạo video ngắn (20 giây) từ các hình ảnh và âm thanh.
  - **Tạo bài đăng LinkedIn**: Tạo nội dung bài đăng phù hợp với nền tảng LinkedIn.
  - **Tạo bài blog**: Viết bài blog chuyên nghiệp với nghiên cứu từ web.
  - **Tạo hình ảnh**: Tạo hình ảnh từ mô tả văn bản (text prompt).
  - **Chỉnh sửa hình ảnh**: Chỉnh sửa hình ảnh đã tạo để thay đổi chi tiết (ví dụ: làm hình ảnh thực tế hơn).
  - **Tìm kiếm cơ sở dữ liệu hình ảnh**: Tìm kiếm hình ảnh đã tạo trước đó trong Google Drive.

### 2. Quy trình làm việc (Workflows)
- Mỗi công cụ được liên kết với một quy trình làm việc riêng biệt trong n8n:
  - **Tạo video**: Tạo 4 hình ảnh, chuyển thành 4 đoạn video 5 giây, thêm âm thanh, và ghép thành video 20 giây.
  - **Tạo bài đăng LinkedIn/Blog**: Nghiên cứu web bằng công cụ Tavily, tạo nội dung, tạo hình ảnh minh họa.
  - **Tạo/Chỉnh sửa hình ảnh**: Sử dụng mô hình tạo hình ảnh của OpenAI (GPT image model).
  - **Tìm kiếm hình ảnh**: Tìm kiếm trong Google Sheets để lấy ID và liên kết hình ảnh.

---

## Demo thực tế

### 1. Tạo hình ảnh
- **Yêu cầu**: Tạo hình ảnh cho tờ rơi quảng cáo thức ăn cho mèo với chương trình giảm giá nhanh (flash sale).
- **Quy trình**:
  - Gửi yêu cầu qua Telegram (bằng giọng nói hoặc văn bản).
  - Tác tử AI nhận yêu cầu, chuyển thành văn bản (transcribe), và kích hoạt công cụ tạo hình ảnh.
  - Hình ảnh được tạo, lưu vào Google Drive, và ghi lại thông tin (tiêu đề, loại, liên kết) vào Google Sheets.
  - Kết quả: Hình ảnh được gửi lại qua Telegram dưới dạng liên kết.
- **Thời gian**: Khoảng 1 phút/hình ảnh.
- **Ví dụ**:
  - Yêu cầu: "Tạo hình ảnh cho tờ rơi thức ăn cho mèo với flash sale."
  - Kết quả: Hình ảnh một chú mèo dễ thương với thông điệp giảm giá.

### 2. Chỉnh sửa hình ảnh
- **Yêu cầu**: Chỉnh sửa hình ảnh tờ rơi để trông thực tế hơn.
- **Quy trình**:
  - Tác tử tìm kiếm hình ảnh trước đó trong cơ sở dữ liệu (Google Sheets) để lấy ID hình ảnh.
  - Sử dụng API chỉnh sửa hình ảnh của OpenAI, gửi hình ảnh gốc và yêu cầu chỉnh sửa.
  - Hình ảnh chỉnh sửa được lưu vào Google Drive, ghi log, và gửi lại qua Telegram.
- **Kết quả**: Hình ảnh mới với chú mèo trông thực tế hơn, kèm thông điệp giảm giá.
- **Thời gian**: Khoảng 1 phút/chỉnh sửa.

### 3. Tạo bài blog
- **Yêu cầu**: Viết bài blog về tác động của giấc ngủ đến năng suất làm việc.
- **Quy trình**:
  - Tác tử sử dụng Tavily để nghiên cứu web về chủ đề.
  - Tạo bài blog với nội dung chuyên nghiệp, định dạng phù hợp cho đối tượng (người đi làm, sinh viên).
  - Tạo hình ảnh minh họa dựa trên nội dung bài blog.
  - Nội dung và hình ảnh được gửi qua Telegram, lưu vào Google Drive và Google Sheets.
- **Kết quả**: Bài blog hoàn chỉnh với tiêu đề, nội dung, nguồn tham khảo, và hình ảnh minh họa.

### 4. Tạo video
- **Yêu cầu**: Tạo video về một con hải ly xây nhà.
- **Quy trình**:
  - Tác tử chia yêu cầu thành 4 cảnh (scene) để tạo 4 hình ảnh và 4 đoạn video 5 giây.
  - Sử dụng API Flux (PI API) để tạo hình ảnh, Runway để chuyển hình ảnh thành video, và 11 Labs để tạo hiệu ứng âm thanh.
  - Ghép 4 đoạn video thành video 20 giây bằng Creatomate.
  - Video được gửi qua Telegram, lưu vào Google Drive và Google Sheets.
- **Thời gian**: 2-3 phút/video.
- **Lưu ý**: Có lỗi nhỏ khi tác tử chính timeout, nhưng video vẫn được tạo và gửi qua Telegram.

---

## Cấu trúc quy trình làm việc

### 1. Tác tử chính (Main Agent)
- **Nhiệm vụ**: Nhận yêu cầu từ Telegram (giọng nói hoặc văn bản), phân tích, và gọi công cụ phù hợp.
- **Cấu hình**:
  - Chuẩn hóa đầu vào (giọng nói/văn bản) thành trường `text` trong JSON.
  - System prompt: Mô tả tác tử là một đội ngũ tiếp thị AI, liệt kê 6 công cụ và hướng dẫn cách sử dụng.
  - Ví dụ: Nếu người dùng yêu cầu "make it more realistic," tác tử hiểu là chỉnh sửa hình ảnh gần nhất trong cơ sở dữ liệu.
- **Kết quả đầu ra**: Gửi liên kết nội dung (hình ảnh, bài đăng, video) qua Telegram.

### 2. Quy trình tạo hình ảnh (Create Image Workflow)
- **Đầu vào**: Tiêu đề hình ảnh (image title), mô tả hình ảnh (image prompt), ID chat Telegram.
- **Quy trình**:
  - Tác tử tạo mô tả hình ảnh chi tiết (dùng mô hình GPT).
  - Gửi yêu cầu tới API tạo hình ảnh của OpenAI, nhận chuỗi Base64.
  - Chuyển đổi Base64 thành dữ liệu nhị phân (binary data).
  - Gửi hình ảnh qua Telegram, lưu vào Google Drive, ghi log vào Google Sheets (tiêu đề, loại, liên kết).
- **Ví dụ mã**:
  ```json
  {
    "image_title": "Cat food/sale",
    "image_prompt": "Cheerful, attention-grabbing flyer for pet owners",
    "chat_id": "<Telegram_chat_ID>"
  }
  ```

### 3. Quy trình chỉnh sửa hình ảnh (Edit Image Workflow)
- **Đầu vào**: Hình ảnh gốc (ID), yêu cầu chỉnh sửa, ID chat Telegram.
- **Quy trình**:
  - Tìm kiếm ID hình ảnh trong Google Sheets.
  - Tải hình ảnh từ Google Drive, gửi tới API chỉnh sửa của OpenAI.
  - Lưu hình ảnh chỉnh sửa, gửi qua Telegram, và ghi log.
- **Ví dụ**: Thêm tai nghe vào hình ảnh cá sấu nâng tạ.

### 4. Quy trình tìm kiếm hình ảnh (Search Images Workflow)
- **Đầu vào**: Ý định (get/edit), tiêu đề hình ảnh, ID chat Telegram.
- **Quy trình**:
  - Tìm kiếm trong Google Sheets để lấy ID và liên kết hình ảnh.
  - Nếu ý định là "get," gửi hình ảnh qua Telegram.
  - Nếu ý định là "edit," gửi ID hình ảnh cho quy trình chỉnh sửa.
- **Ví dụ**: Tìm hình ảnh "crocodile lifting weights."

### 5. Quy trình tạo bài blog (Blog Post Workflow)
- **Đầu vào**: Chủ đề blog, đối tượng mục tiêu, ID chat Telegram.
- **Quy trình**:
  - Nghiên cứu web bằng Tavily.
  - Tạo bài blog với nội dung chuyên nghiệp, nguồn tham khảo.
  - Tạo hình ảnh minh họa dựa trên nội dung.
  - Gửi bài blog và hình ảnh qua Telegram, lưu vào Google Drive và Google Sheets.
- **Ví dụ**: Bài blog về giấc ngủ và năng suất cho người đi làm/sinh viên.

### 6. Quy trình tạo video (Video Creation Workflow)
- **Đầu vào**: Chủ đề video, ID chat Telegram.
- **Quy trình**:
  - Chia video thành 4 cảnh, tạo 4 mô tả hình ảnh.
  - Tạo 4 hình ảnh bằng Flux API, chuyển thành 4 đoạn video 5 giây bằng Runway.
  - Tạo hiệu ứng âm thanh bằng 11 Labs.
  - Ghép video bằng Creatomate, gửi qua Telegram, lưu vào Google Drive và Google Sheets.
- **Ví dụ mã**:
  ```json
  {
    "video_topic": "Beaver building a house",
    "chat_id": "<Telegram_chat_ID>",
    "scenes": [
      "Stocky beaver gathering sticks",
      "Beaver arranging sticks by riverbank",
      "Close-up of beaver placing sticks",
      "Beaver with finished dam"
    ]
  }
  ```

---

## Chi phí vận hành
- **n8n Cloud**: ~27 USD/tháng.
- **Tạo/Chỉnh sửa hình ảnh (OpenAI)**: 0.19-0.20 USD/hình ảnh.
- **Tạo bài đăng LinkedIn/Blog (OpenAI)**: ~0.20 USD/lần chạy.
- **Tạo hình ảnh (Flux via PI API)**: 0.015 USD/hình ảnh.
- **Tạo video (Runway)**: 0.25 USD/đoạn 5 giây (1 USD/video 20 giây).
- **Creatomate**: 1 credit/video 20 giây (50 credit miễn phí với tài khoản thử).
- **Hiệu ứng âm thanh (11 Labs)**: 5 USD/tháng (kế hoạch starter).
- **Text generation (Open Router)**:
  - 4.1: 2 USD/triệu token đầu vào, 8 USD/triệu token đầu ra.
  - 4.1 Mini: 0.40 USD/triệu token đầu vào, 1.60 USD/triệu token đầu ra.

---

## Hướng dẫn cài đặt

### 1. Tải tài nguyên
- Tham gia cộng đồng Free School để tải:
  - 7 tệp JSON cho quy trình làm việc (1 tác tử chính + 6 công cụ).
  - Mẫu Google Sheets để ghi log.
  - Mẫu Creatomate để ghép video.
- **Liên kết tham khảo**: [[Free School Community]]

### 2. Cài đặt trong n8n
- **Nhập quy trình làm việc**:
  - Vào n8n, chọn "Import from file," tải từng tệp JSON.
  - Đảm bảo liên kết đúng quy trình làm việc trong tác tử chính (ví dụ: chọn "Create Image" trong danh sách).
- **Cấu hình API**:
  - Thêm khóa API: OpenAI, Open Router, Google Drive, Google Sheets, Telegram.
- **Cấu hình Google Sheets**:
  - Tạo bản sao mẫu Google Sheets, sử dụng để ghi log.
- **Cấu hình Creatomate**:
  - Tạo mẫu mới, dán mã nguồn từ cộng đồng.
  - Nhập lệnh curl vào n8n, kéo các biến video/âm thanh vào yêu cầu HTTP.

### 3. Kiểm tra và chạy
- Kiểm tra từng quy trình làm việc bằng cách chạy thử.
- Đảm bảo Telegram nhận được đầu ra (hình ảnh, bài đăng, video).

---

## Ghi chú thêm
- **Liên kết chéo**:
  - [[Tạo hình ảnh với OpenAI]]: Hướng dẫn chi tiết về API tạo hình ảnh.
  - [[Tạo video ngắn]]: Hướng dẫn tạo video ngắn với Flux và Runway.
  - [[Cộng đồng Free School]]: Nguồn tài nguyên và hướng dẫn.
- **Khuyến nghị**:
  - Sử dụng mô hình rẻ hơn (DALL-E 2/3) để giảm chi phí.
  - Thêm cơ chế thăm dò (polling) để đảm bảo tất cả hình ảnh/video được tạo trước khi tiếp tục.
- **Cộng đồng trả phí**:
  - Cung cấp khóa học, hướng dẫn chi tiết, và hỗ trợ qua 5 cuộc gọi trực tiếp/tuần.
  - Liên kết: [[Paid Community]]

---

**Lưu ý**: Ghi chú này được tối ưu hóa để lưu trữ trong Obsidian, với cấu trúc rõ ràng và liên kết chéo để dễ tra cứu.