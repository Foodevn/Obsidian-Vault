# TÀI LIỆU THIẾT KẾ KIẾN TRÚC HỆ THỐNG KHUYẾN NGHỊ THỜI GIAN THỰC ÁP DỤNG THUẬT TOÁN DUOCA

## 1. Tóm tắt Mục tiêu

Xây dựng một hệ thống xử lý luồng dữ liệu bán lẻ tốc độ cao, áp dụng thuật toán DUOCA (Damped Utility Occupancy) để phân tích và cung cấp khuyến nghị sản phẩm theo thời gian thực. Hệ thống phải giải quyết được 3 bài toán lớn: (1) Xung đột Đọc/Ghi khi tính toán, (2) Tràn bộ nhớ (OOM) khi dữ liệu đến liên tục 24/7, và (3) Khả năng phục hồi dữ liệu khi xảy ra sự cố (Fault Tolerance).

## 2. Sơ đồ Kiến trúc Tổng thể (Overall Architecture)

Kiến trúc được thiết kế theo hướng sự kiện (Event-driven) và phân tách luồng (CQRS), kết hợp giữa tính toán trên bộ nhớ (In-memory) và lưu trữ bền vững (Persistent Storage).

```mermaid
graph TD
    subgraph Layer 1: Data Ingestion
        A[Client / E-commerce Web] -->|Giao dịch mua hàng| B(API Gateway)
        B -->|Produce Event| C[Apache Kafka - Write Ahead Log]
    end

    subgraph Layer 2: Stream Processing & Dual-State Memory
        C -->|Consume Stream| D{Apache Flink / Processing Engine}
        D -->|Ghi liên tục| E[(RAM: Active_DUO_List)]
        D -->|Lưu trữ lịch sử| F[(PostgreSQL: Cold Storage)]
        D -.->|Đóng băng 5 phút/lần| G[S3/HDFS: Checkpoints]
        
        H[Trigger: Request/Timer] -->|Copy-on-Write| I[(RAM: Snapshot_DUO_List)]
        E -.->|Clone| I
        I -->|Chạy DUOCA DFS| J[Khai phá Mẫu Tiện ích]
    end

    subgraph Layer 3: Serving & Recommendation
        J -->|Ghi đè luật mới| K[(Redis: Hot Cache)]
        A -->|Truy vấn Gợi ý| L(FastAPI / Recommendation API)
        L -->|O() Query| K
    end
```

## 3. Phân rã Các Thành phần và Giải pháp Kỹ thuật

### 3.1. Tầng Thu thập và Lưu trữ Lỗi (Fault-Tolerant Ingestion)

- **Thành phần:** Apache Kafka.
    
- **Vai trò:** Hoạt động như một bộ đệm (Buffer) khổng lồ. Mọi giao dịch bán lẻ ngay khi diễn ra sẽ được ghi nối đuôi vào ổ cứng của Kafka (Write-Ahead Log) trước khi đưa vào RAM tính toán.
    
- **Giải quyết bài toán:** Đảm bảo không mất dữ liệu. Nếu Server xử lý bị sập nguồn (cúp điện), Kafka vẫn giữ toàn bộ dữ liệu gốc. Khi Server khởi động lại, nó chỉ cần đọc tiếp từ vị trí bị gián đoạn.
    

### 3.2. Tầng Quản lý Trạng thái Kép trên Bộ nhớ (Dual-State In-Memory)

- **Thành phần:** Apache Flink State (RAM).
    
- **Vai trò:** Duy trì 2 danh sách độc lập để tối đa hóa tốc độ (nano-giây):
    
    1. **Active_DUO_List:** Luôn mở để đón nhận giao dịch mới từ Kafka. Sử dụng cấu trúc Lock-free để không cản trở tốc độ luồng.
        
    2. **Snapshot_DUO_List:** Bản sao tĩnh (chụp bằng kỹ thuật Copy-on-Write) được tạo ra khi có yêu cầu phân tích.
        
- **Giải quyết bài toán:** Tránh xung đột Đọc/Ghi. Quá trình duyệt cây tính toán thuật toán mất nhiều thời gian sẽ chạy độc lập trên `Snapshot`, không làm "đóng băng" hệ thống đón dữ liệu của `Active_List`.
    

### 3.3. Tầng Đảm bảo An toàn Bộ nhớ và Lưu trữ Bền vững

- **Giải pháp chống tràn RAM (Memory Pruning):** Lợi dụng đặc tính Hệ số suy hao ($f$) của DUOCA. Khi hệ thống duyệt `Active_DUO_List`, các mặt hàng/giao dịch cũ có điểm Tiện ích (Utility) tụt xuống dưới ngưỡng `min_duo` sẽ bị cắt tỉa (xóa khỏi RAM). RAM chỉ chứa "xu hướng mua sắm gần đây", không bao giờ bị tràn.
    
- **Giải pháp phục hồi nhanh (Checkpointing):** Hệ thống tự động lưu bản sao của RAM (`Active_DUO_List`) xuống đĩa cứng (HDFS/S3) mỗi 5 phút. Khi có sự cố, hệ thống nạp lại Checkpoint này vào RAM thay vì phải chạy lại dữ liệu từ Kafka từ đầu năm đến nay.
    
- **Lưu trữ lịch sử (Cold Storage):** Dữ liệu giao dịch gốc vẫn được luồng xử lý ghi vào cơ sở dữ liệu quan hệ (PostgreSQL) để phục vụ cho các nghiệp vụ phi thời gian thực (ví dụ: báo cáo kế toán, đối soát), tách biệt hoàn toàn khỏi luồng Khuyến nghị.
    

### 3.4. Tầng Phục vụ Khuyến nghị (Low-latency Serving)

- **Thành phần:** Redis & FastAPI.
    
- **Vai trò:** Kết quả đầu ra của thuật toán (Các tập sản phẩm có Độ chiếm dụng Tiện ích Cao) được lưu trực tiếp vào Redis dưới dạng Key-Value (Sorted Sets). Khi người dùng vào trang sản phẩm, API chỉ mất < 10ms để lấy danh sách gợi ý từ Redis trả về Frontend.
    

## 4. Luồng Thực thi (Execution Flow)

1. Khách hàng mua tập sản phẩm $\{A, B\}$.
    
2. Frontend gửi sự kiện về API Gateway $\rightarrow$ Đẩy vào Kafka.
    
3. Flink đọc sự kiện $\rightarrow$ Cập nhật Node $A, B$ trong `Active_DUO_List` (trên RAM), đồng thời ghi lịch sử vào PostgreSQL.
    
4. (Chu kỳ 1 phút/lần) Flink tạo bản `Snapshot_DUO_List` $\rightarrow$ Nhân hệ số suy hao $f$ $\rightarrow$ Chạy thuật toán DUOCA tìm các mẫu thỏa mãn ngưỡng.
    
5. Flink đẩy các mẫu (Ví dụ: "Mua A gợi ý B, độ tin cậy 85%") vào Redis.
    
6. (Chu kỳ quét định kỳ) Flink xóa các Node có Utility quá thấp khỏi `Active_DUO_List` để giải phóng RAM.
    
7. Flink tự động lưu cấu trúc RAM hiện tại xuống ổ cứng mỗi 5 phút để backup.





### 1. Nhóm Tính năng Tương tác Khách hàng (Frontend & Client)

Nhóm này tương ứng với khối `A[Client / E-commerce Web]` trong sơ đồ, tập trung vào trải nghiệm của người dùng cuối (End-user).

- **Tracking Hành vi Mua sắm Thời gian thực:** Khả năng thu thập ngay lập tức các sự kiện "Thêm vào giỏ hàng" (Add to cart) hoặc "Thanh toán" (Checkout) của người dùng cùng với thông tin số lượng (quantity) và giá tiền (price) của từng sản phẩm.
    
- **Hiển thị Gợi ý Cá nhân hóa (Real-time Recommendation UI):** Hiển thị danh sách các sản phẩm "Thường được mua cùng nhau" (Frequently bought together) hoặc "Có thể bạn cũng thích" (You may also like) ngay lập tức khi khách hàng đang xem một sản phẩm hoặc đang ở trang giỏ hàng.
    
- **Tự động Cập nhật Gợi ý:** Giao diện có khả năng làm mới (refresh) danh sách gợi ý mà không cần tải lại trang dựa trên các tương tác mới nhất của khách hàng.
    

### 2. Nhóm Tính năng Thu thập và Phân phối Dữ liệu (Ingestion)

Nhóm này tương ứng với Tầng 1 (Layer 1), tập trung vào khả năng "hứng" luồng dữ liệu lớn mà không bị nghẽn.

- **Tiếp nhận Sự kiện Đồng thời cao (High-Concurrency Event Ingestion):** Khả năng thông qua API Gateway tiếp nhận hàng chục ngàn sự kiện mua sắm cùng lúc vào các dịp cao điểm (như Black Friday).
- **Lưu đệm Dữ liệu (Data Buffering & Queuing):** Đẩy dữ liệu vào Kafka theo cơ chế Write-Ahead Log để đảm bảo không một giao dịch nào bị thất thoát trước khi đưa vào xử lý tính toán.

### 3. Nhóm Tính năng Xử lý Khai phá Lõi (Stream Processing & Mining)

Đây là "trái tim" của hệ thống, tương ứng với Tầng 2 (Layer 2) nơi thuật toán DUOCA hoạt động.

- **Tính toán Tiện ích (Utility Calculation):** Hệ thống tự động tính toán giá trị tiện ích (Utility) của mỗi mặt hàng trong một giao dịch (dựa trên lợi nhuận nhân với số lượng).
- **Cập nhật Trạng thái Kép (Dual-State Management):** Khả năng liên tục cập nhật dữ liệu mới vào RAM (Active_DUO_List) đồng thời có thể chụp ảnh (Snapshot) dữ liệu để chạy thuật toán mà không khóa (lock) hệ thống.
- **Áp dụng Cửa sổ Suy hao (Damped Window Application):** Tính năng tự động nhân hệ số suy hao $f$ vào giá trị của các giao dịch trong quá khứ để giảm dần tầm quan trọng của các xu hướng cũ.
- **Khai phá Mẫu theo yêu cầu (On-demand Pattern Mining):** Kích hoạt thuật toán tìm kiếm theo chiều sâu (DFS) theo chu kỳ (ví dụ: mỗi 1 phút) để tìm ra các mẫu (patterns) có độ chiếm dụng tiện ích cao nhất.
- **Cắt tỉa Bộ nhớ Tự động (Memory Pruning):** Tự động xóa bỏ các mặt hàng/giao dịch đã cũ và có tiện ích dưới ngưỡng `min_duo` để giải phóng RAM.
- **Sao lưu Trạng thái định kỳ (Checkpointing):** Tự động lưu cấu trúc RAM xuống đĩa cứng (S3/HDFS) mỗi 5 phút để dự phòng sự cố.

### 4. Nhóm Tính năng Phục vụ và Quản trị (Serving & Admin)

Nhóm này kết hợp Tầng 3 (Layer 3) và các luồng phụ trợ.

- **Phục vụ Gợi ý Độ trễ cực thấp (Low-latency Serving API):** Cung cấp API (FastAPI) truy vấn siêu tốc (<10ms) vào Redis để lấy ra danh sách các sản phẩm nên gợi ý cho một mặt hàng cụ thể (O(1) Query).
- **Lưu trữ Dữ liệu Lịch sử (Cold Data Archiving):** Ghi toàn bộ lịch sử giao dịch gốc vào Database (PostgreSQL) để phục vụ việc truy xuất hóa đơn và phân tích dài hạn.
- **Giám sát Thông số Hệ thống (System Monitoring):** (Tính năng ẩn cần có) Khả năng theo dõi thông lượng (Throughput), mức sử dụng RAM (Memory Usage) và độ trễ (Latency) của toàn bộ luồng xử lý Flink - Kafka - Redis.


### Bước 1: Khởi tạo và Cập nhật (Construction Procedure)

Quá trình này diễn ra liên tục tại **`E[(RAM: Active_DUO_List)]`**.

1. Khi một giao dịch mới ($T_d$) đến từ Kafka, hệ thống đọc danh sách các mặt hàng (items) và số lượng mua của chúng.
2. Hệ thống nhân số lượng mua với giá niêm yết của mặt hàng (được nạp sẵn từ Database) để ra giá trị tiện ích (Utility).
3. Hệ thống tạo hoặc cập nhật các node trong cấu trúc `Active_DUO_List`. Mỗi node sẽ lưu trữ `tid` (mã giao dịch), `uo` (độ chiếm dụng tiện ích của mặt hàng đó trong giao dịch) và `ruo` (độ chiếm dụng tiện ích còn lại của các mặt hàng đứng sau nó).

### Bước 2: Tái cấu trúc và Áp dụng Suy hao (Restructure Procedure)

Quá trình này được kích hoạt khi có yêu cầu (trigger) tại **`I[(RAM: Snapshot_DUO_List)]`**.

1. Khi hệ thống tạo ra bản sao `Snapshot_DUO_List`, nó sẽ quét qua tất cả các mặt hàng.
2. **Áp dụng Hệ số suy hao ($f$):** Hệ thống lấy thời gian hiện tại trừ đi thời gian của giao dịch ($T_{current} - T_{transaction}$) để tính ra độ lùi thời gian. Sau đó, nó nhân giá trị `uo` và `ruo` với hệ số $f$ (ví dụ: $0.9$) lũy thừa với độ lùi thời gian này. Điều này làm cho các giao dịch cũ bị giảm giá trị.
3. **Cắt tỉa sơ bộ (Pruning):** Nếu tổng giá trị tiện ích đã suy hao của một mặt hàng thấp hơn ngưỡng thiết lập (`min_duo`), mặt hàng đó sẽ bị loại bỏ khỏi danh sách để giảm không gian tìm kiếm.
4. **Sắp xếp (Sorting):** Các mặt hàng còn lại được sắp xếp theo thứ tự độ hỗ trợ (support) tăng dần.

### Bước 3: Mở rộng Mẫu bằng DFS (Pattern Expansion Procedure)

Đây chính là bước cốt lõi tại khối **`J[Khai phá Mẫu Tiện ích]`**.

1. Hệ thống sử dụng thuật toán Tìm kiếm theo chiều sâu (Depth-First Search - DFS) để kết hợp các mặt hàng đơn lẻ thành các tập sản phẩm (patterns). Ví dụ: ghép `A` với `B` thành tập `{A, B}`.
2. Khi tạo ra một tập mẫu mới (ví dụ $P = \{A, B\}$), hệ thống sẽ tính toán lại danh sách `DUO-List` cho riêng tập $P$ này (gọi là `$P_x$-list` trong bài báo) bằng cách giao (intersect) danh sách của $A$ và $B$.
3. **Cắt tỉa sâu (Deep Pruning):** Hệ thống tính toán hai giá trị:
    - **`duo` (Damped Utility Occupancy):** Điểm tiện ích chiếm dụng thực tế của mẫu $P$.
    - **`ubduo` (Upper Bound DUO) hoặc `lubduo` (Local UBDUO):** Điểm tiện ích chiếm dụng tối đa dự kiến nếu tiếp tục mở rộng mẫu $P$.
4. Nếu `duo` $\ge$ `min_duo`, mẫu $P$ được xác nhận là một **Mẫu Tiện ích Chiếm dụng Cao (High DUO Pattern)** và sẽ được đẩy sang Redis (Layer 3).
5. Nếu `ubduo` hoặc `lubduo` $<$ `min_duo`, hệ thống sẽ ngừng mở rộng nhánh đó (không thử ghép thêm `C` vào `{A, B}` nữa) để tiết kiệm thời gian tính toán. Quá trình DFS tiếp tục cho đến khi duyệt hết cây.
