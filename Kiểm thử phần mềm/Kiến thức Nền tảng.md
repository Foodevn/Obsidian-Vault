ựa trên các tài liệu học phần đã cung cấp, dưới đây là tổng hợp những kiến thức và kỹ năng cốt lõi cần nắm vững trong môn học Kiểm thử Phần mềm.

### I. Tổng quan về Học phần và Kiến thức Nền tảng

#### 1. Mục tiêu Môn học (Goals)

Học viên cần đạt được các mục tiêu sau:

- **Hiểu được tổng quan kiểm thử phần mềm** và áp dụng được các phương pháp kiểm thử.
- Hiểu và áp dụng các mức kiểm thử, các loại hình kiểm thử, quy trình kiểm thử, và kiểm thử tự động hóa.
- Có khả năng phân tích vấn đề và lựa chọn giải pháp trong việc xây dựng phần mềm.
- Có khả năng nhận thức và cập nhật kiến thức mới.
- Có khả năng trình bày báo cáo và thuyết trình về đề tài xây dựng phần mềm được phân công.

#### 2. Kiến thức và Kỹ năng Cần Thiết (Prerequisites)

Để theo học môn này hiệu quả, sinh viên cần có:

- **Kỹ năng đọc – hiểu tài liệu chuyên ngành** bằng tiếng Anh và tiếng Việt.
- **Kỹ năng lập trình, debug (gỡ rối), sửa lỗi**.
- Kiến thức cơ bản về công nghệ phần mềm, quy trình phát triển phần mềm, và ngôn ngữ lập trình.
- **Khả năng tư duy logic**, kiến thức về xác suất - thống kê, và tập hợp.

### II. Các Khái niệm Cốt lõi trong Kiểm thử Phần mềm

#### 1. Định nghĩa và Mục tiêu

- **Kiểm thử phần mềm** là quá trình chạy một hệ thống phần mềm để xác định xem phần mềm có phù hợp với đặc tả (specification) và hoạt động trong môi trường như kỳ vọng hay không.
- Mục tiêu chính là **phát hiện càng nhiều lỗi càng tốt** (nhiều nhất có thể).
- Kiểm thử không phải là quá trình chứng minh phần mềm không có lỗi.

#### 2. Phân biệt các Thuật ngữ

Cần phân biệt rõ các thuật ngữ liên quan đến lỗi:

- **ERROR (Sai sót):** Sự nhầm lẫn hoặc hiểu sai trong quá trình phát triển phần mềm của người phát triển.
- **FAULT (Lỗi):** Xuất hiện trong phần mềm như là kết quả của sự sai sót.
- **FAILURE (Hỏng hóc):** Kết quả của lỗi làm cho chương trình không hoạt động được hoặc hoạt động không như mong muốn.
- **Gỡ rối (Debugging):** Quá trình xác định vị trí và sửa chữa hoặc khắc phục lỗi tồn tại trong mã nguồn.

#### 3. Thẩm định và Xác minh (Validation & Verification)

- **Xác minh (Verification):** Chúng ta có xây dựng đúng sản phẩm không? Chương trình có phù hợp với mô tả của nó không?.
- **Thẩm định (Validation):** Chúng ta có xây dựng một sản phẩm đúng không? Hệ thống xử lý có đáp ứng yêu cầu khách hàng, cần thiết và mong đợi không?.

#### 4. Các Phương pháp Kiểm thử Cơ bản

- **Kiểm thử động (Dynamic testing):** Thực hiện bằng cách chạy chương trình để kiểm tra hành vi thực tế.
- **Kiểm thử tĩnh (Static testing):** Không yêu cầu chạy chương trình, thực hiện trong giai đoạn đầu để phát hiện lỗi trong tài liệu, mã nguồn, thiết kế....
- **Kiểm thử hộp đen (Black box):** Tập trung vào chức năng và hành vi, kiểm thử phần mềm mà không cần biết cấu trúc bên trong.
- **Kiểm thử hộp trắng (White box):** Tập trung vào cấu trúc và điều khiển logic, dựa trên việc hiểu rõ cấu trúc nội bộ của hệ thống và logic vận hành.

---

### III. Các Kỹ thuật Kiểm thử Chi tiết

#### 1. Kiểm thử Hộp Đen (Black Box Testing)

Kỹ thuật này được sử dụng để kiểm tra các yêu cầu chức năng thông qua giao diện bên ngoài. Các phương pháp chính gồm:

- **Phân vùng tương đương (Equivalence partitioning):** Chia miền đầu vào thành các nhóm dữ liệu có đặc điểm giống nhau (hợp lệ và không hợp lệ) để chọn trường hợp kiểm thử đại diện.
- **Kiểm thử biên (Boundary testing):** Xây dựng trường hợp kiểm thử tập trung vào các giá trị nằm ở "rìa" của mỗi phân vùng (ví dụ: $a$, $b$, $a-1$, $b+1$ cho phạm vi $(a, b)$).
- **Bảng quyết định (Decision table):** Dùng để kiểm tra logic phức tạp, bao gồm các stub và entry về điều kiện và hành động.
- **Dự đoán lỗi (Error guessing):** Thiết kế trường hợp kiểm thử dựa trên kinh nghiệm và trực giác của kiểm định viên.

#### 2. Kiểm thử Hộp Trắng (White Box Testing)

Kỹ thuật này tập trung vào mã nguồn để kiểm tra logic và cấu trúc nội tại.

- **Phủ kiểm thử (Coverage):** Tỷ lệ giữa số lượng thành phần được kiểm thử và tổng số thành phần liên quan (lệnh, điểm quyết định, điều kiện con).
    - **Phủ cấp 1 (Statement coverage):** Mỗi lệnh được thực thi ít nhất một lần.
    - **Phủ cấp 2 (Branch coverage):** Mỗi điểm quyết định được thực hiện ít nhất một lần cho cả hai trường hợp đúng (TRUE) và sai (FALSE).
    - **Phủ cấp 4 (Branch & sub-condition coverage):** Kiểm thử đầy đủ cả nhánh lẫn điều kiện con.
- **Kiểm thử đường dẫn cơ sở (Basis path):**
    - Sử dụng **Đồ thị dòng (Flow graph)** để biểu diễn logic chương trình.
    - Tính **Độ phức tạp Cyclomatic** theo công thức $V(G) = E - N + 2P$ (hoặc $V(G) = P + 1$) để xác định số lượng đường thi hành tuyến tính độc lập tối thiểu cần kiểm thử.
- **Kiểm thử vòng lặp (Loop testing):** Tập trung vào đánh giá hiệu lực của các cấu trúc lặp (vòng lặp đơn, lồng nhau, nối tiếp) tại các biên quan trọng ($n-1, n, n+1$).

#### 3. Kiểm thử Tĩnh (Static Testing)

Tập trung vào việc đọc, phân tích và đánh giá các sản phẩm công việc (yêu cầu, thiết kế, mã nguồn) mà không chạy chương trình.

- **Công cụ Phân tích Tĩnh:** Dùng để phát hiện các khiếm khuyết điển hình như tham chiếu biến chưa khởi tạo, mã chết, vi phạm tiêu chuẩn lập trình, hoặc lỗ hổng bảo mật.
- **Đánh giá (Review):** Hình thức kiểm tra thủ công các sản phẩm phần mềm.
    - Các hình thức đánh giá chính: Đánh giá không chính thức, Hướng dẫn (Walkthrough), Đánh giá kỹ thuật, và **Đánh giá chính thức (Inspection)** (quy trình chính thức, có vai trò rõ ràng, tập trung phát hiện khiếm khuyết).

---

### IV. Quy trình và Các Mức Độ Kiểm thử

Kiểm thử được thực hiện theo các cấp độ, từ module riêng lẻ đến hệ thống hoàn chỉnh:

|Cấp độ Kiểm thử|Mục tiêu|Trách nhiệm chính|
|:--|:--|:--|
|**Kiểm thử Đơn vị (Unit)**|Đảm bảo các khối xây dựng cơ bản (module, hàm) làm việc chính xác. Kiểm tra giao diện, cấu trúc dữ liệu cục bộ, điều kiện logic.|Lập trình viên.|
|**Kiểm thử Tích hợp (Integration)**|Kiểm tra sự phối hợp giữa các module đã kiểm thử đơn vị.|Lập trình viên, Nhóm kiểm thử độc lập.|
|**Kiểm thử Hệ thống (System)**|Kiểm thử toàn diện phần mềm sau khi tích hợp để đảm bảo mọi chức năng hoạt động chính xác trong môi trường đã định.|Nhóm kiểm thử độc lập.|
|**Kiểm thử Chấp nhận (Acceptance)**|Xác nhận rằng phần mềm đáp ứng đầy đủ yêu cầu thực tế của khách hàng/người dùng cuối.|Khách hàng hoặc người dùng cuối.|

#### 1. Chiến lược Tích hợp

- **Từ trên xuống (Top-down):** Bắt đầu từ module điều khiển chính. Cần sử dụng **Cuống (Stub)** để giả lập hành vi của module cấp dưới chưa hoàn thành.
- **Từ dưới lên (Bottom-up):** Bắt đầu từ các module cấp thấp nhất. Cần sử dụng **Bộ lái (Driver)** để cung cấp đầu vào và kiểm tra đầu ra cho các cụm module.
- **Kiểm thử Hồi quy (Regression testing):** Chạy lại một số kiểm thử đã có để đảm bảo các thay đổi mới không làm ảnh hưởng đến các chức năng đã tồn tại.

#### 2. Kiểm thử Hệ thống Chi tiết

Kiểm thử hệ thống bao gồm nhiều loại chuyên biệt:

- **Kiểm thử Hồi phục (Recovery):** Đánh giá khả năng khôi phục trạng thái hoạt động bình thường của hệ thống sau sự cố.
- **Kiểm thử Khả năng Chịu đựng (Stress):** Đánh giá hệ thống có duy trì hoạt động ổn định khi bị đặt vào điều kiện tải nặng vượt mức thông thường.
- **Kiểm thử Độ An toàn (Security):** Đánh giá khả năng hệ thống bảo vệ dữ liệu và chống truy cập trái phép.
- **Kiểm thử Hiệu suất (Performance):** Đánh giá hiệu năng thời gian chạy, tốc độ xử lý và phản hồi.
- **Kiểm thử Alpha/Beta:** Thử nghiệm trong môi trường giả lập (Alpha) hoặc bởi người dùng cuối thực tế (Beta) trước khi phát hành chính thức.

---

### V. Chủ đề Nâng cao (Web và Di động)

#### 1. Kiểm thử Web

Cần kiểm thử toàn diện trước khi ứng dụng web hoạt động chính thức. Các loại kiểm thử bao gồm:

- **Kiểm thử Chức năng:** Kiểm tra liên kết, biểu mẫu, cơ sở dữ liệu, cookie, HTML/CSS.
- **Kiểm thử Khả năng Sử dụng (Usability):** Đánh giá mức độ tương tác, điều hướng thân thiện, và chất lượng nội dung.
- **Kiểm thử Khả năng Tương thích (Compatibility):** Xác định phần mềm có hoạt động đúng trên các trình duyệt, hệ điều hành và phần cứng khác nhau.
- **Kiểm thử Bảo mật:** Bảo vệ thông tin nhạy cảm, ngăn truy cập trái phép, kiểm tra XSS và SQL Injection.
- **Kiểm thử Hiệu suất:** Đảm bảo ổn định dưới các mức tải khác nhau (tải, căng thẳng).

#### 2. Kiểm thử Di động

Kiểm thử ứng dụng di động có nhiều thách thức do sự đa dạng của thiết bị, hệ điều hành, và nhà mạng.

- **Các loại ứng dụng:** **Native** (phát triển riêng cho từng hệ điều hành, hiệu năng cao), **Web** (hoạt động qua trình duyệt), **Hybrid** (kết hợp cả hai).
- Kiểm thử ứng dụng di động đánh giá chức năng, khả năng sử dụng, hiệu năng, và tính nhất quán trên thiết bị cầm tay.