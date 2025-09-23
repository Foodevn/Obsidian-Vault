## Thu Thập Dữ Liệu Web Miễn Phí Với n8n

### Giới Thức Và Lưu Ý Đạo Đức
- Thu thập dữ liệu web (web scraping) phải thực hiện đạo đức và hợp pháp: Chỉ thu thập từ trang web cho phép.
- Kiểm tra quyền thu thập bằng cách thêm `/robots.txt` vào URL trang web:
  - Ví dụ: `flowise.ai/robots.txt` → Cho phép tất cả (allow: /), bao gồm sitemap.
  - Ví dụ: `github.com/robots.txt` hoặc `youtube.com/robots.txt` → Không cho phép (disallow: /), tránh thu thập.
- Nếu không có `robots.txt`, kiểm tra sitemap (sitemap.xml) để lấy danh sách URL hợp lệ.
- Không thu thập từ GitHub, YouTube hoặc trang cấm để tránh vi phạm.

### Tổng Quan Workflow Thu Thập Dữ Liệu
- Workflow chính: Kích hoạt bằng form submission với URL trang web làm input.
- Quy trình:
  - Tạo URL sạch (make nice URLs): Thêm `https://` nếu thiếu, loại bỏ `www.`, chuyển domain thành chữ thường, loại bỏ path/query thừa.
  - Kiểm tra `robots.txt` để lấy sitemap nếu có.
  - Nếu không có `robots.txt`, thử các biến thể sitemap: `sitemap.xml`, `sitemap_index.xml`, `sitemap.json`.
  - Thu thập nội dung từ sitemap: Phân biệt giữa danh mục (categories as XML) hoặc URL trực tiếp.
  - Lấy nội dung HTML qua HTTP request.
  - Chuyển HTML sang Markdown, loại bỏ nội dung thừa (strip unnecessary info).
  - Lưu vào cơ sở dữ liệu vector Pinecone (Pinecone vector database) sử dụng bộ tải dữ liệu mặc định (default data loader), bộ chia văn bản đệ quy (recursive character text splitter), và embeddings OpenAI (OpenAI embeddings, ví dụ: text-embedding-3-small).
- Workflow phụ: Chatbot sử dụng AI agent để truy vấn dữ liệu từ Pinecone qua RAG (Retrieval-Augmented Generation).

[[n8n]] | [[Web Scraping]] | [[Pinecone]] | [[RAG]]

### Cấu Trúc Trang Web Và Sitemap
- Trang web sử dụng `robots.txt` để chỉ định phần cho phép thu thập bởi bot (crawlers như Google).
- Sitemap (`sitemap.xml`): Danh sách URL hoặc danh mục (categories) của trang web.
  - Nếu sitemap chứa URL trực tiếp: Thu thập HTML từ các URL đó.
  - Nếu sitemap chứa danh mục (XML files): Thu thập nội dung từ các XML con để lấy URL chi tiết.
- Ví dụ:
  - Flowise.ai: Có `robots.txt` và sitemap với URL trực tiếp (ví dụ: pricing page).
  - LangChain.com: Không có `robots.txt`, nhưng có sitemap với nhiều URL (37-57 URL).
  - n8n.io: Có `robots.txt` và sitemap với danh mục (12 XML, dẫn đến 57+ URL).

### Chi Tiết Các Node Trong Workflow
- **Form Submission Trigger**: Nhập URL trang web, kích hoạt workflow.
- **Make Nice URLs Node**: Sử dụng GPT-4 Mini để chuẩn hóa URL (output dạng JSON).
- **Check Robots.txt Node**: Thêm `/robots.txt` vào base URL, lấy nội dung qua HTTP request, trích xuất sitemap nếu có.
- **Merge Node**: Kết hợp kết quả từ các kiểm tra sitemap (XML, index XML, JSON).
- **XML Check Node**: Kiểm tra nếu sitemap có danh mục (multiple XML) hay URL trực tiếp:
  - Nếu URL trực tiếp: Sử dụng code block để trích xuất URL sạch.
  - Nếu danh mục: 
    - Lấy link XML từ sitemap.
    - Chuyển XML sang JSON.
    - Trích xuất URL từ JSON.
- **HTTP Request Nodes**: Lấy HTML từ từng URL (có thể song song cho nhiều URL).
- **HTML to Markdown Node**: Chuyển đổi nội dung HTML sang Markdown dễ đọc.
- **Strip Node**: Loại bỏ phần thừa (random stuff) như quảng cáo, navigation.
- **Pinecone Vector Store Node**:
  - Operation: Insert documents.
  - Index: Tùy chỉnh (ví dụ: "scrape", "flows").
  - Embeddings: OpenAI text-embedding-3-small.
  - Splitter: Recursive character, chunk size phù hợp (ví dụ: 500), overlap 20.
- **Code Blocks**: Sử dụng để trích xuất URL từ XML/JSON, đảm bảo chỉ lấy URL hợp lệ.

### Xây Dựng Chatbot (Rack Application)
- Sử dụng AI Agent Node với chat trigger.
- Cấu hình:
  - System Prompt: "You are a helpful assistant for [website]. Use the vector tool to answer questions."
  - Memory: Window Buffer Memory (ví dụ: lưu 12 cuộc chat).
  - Chat Model: OpenAI GPT-4 Omni (gpt-4o).
  - Vector Tool: Pinecone retrieval, top K=4, embeddings OpenAI text-embedding-3-small.
- Ví dụ truy vấn:
  - Trước khi scrape: Hỏi pricing của Flowise → Không trả lời được (vector database rỗng).
  - Sau scrape Flowise: Hỏi pricing → Trả lời chi tiết (Starter $35/1GB, Pro $65/10GB, Enterprise liên hệ).
  - Sau scrape LangChain: Hỏi "Can I use LangSmith without LangChain?" → Có, sử dụng SDK Python/TypeScript hoặc API.
  - Sau scrape n8n: Hỏi "Can FastBots connect with Flagship in n8n?" → Có, sử dụng workflow trong n8n.

### Thực Hành Và Lưu Ý
- Tải workflow mẫu, kết nối API keys (OpenAI, Pinecone).
- Thử với các URL khác nhau: Flowise (1 URL), LangChain (37+ URL), n8n (57+ URL, 452 records).
- Workflow tự động xử lý cấu trúc trang web khác nhau, nhưng chỉ chạy nếu scraping được phép.
- Ưu điểm: Miễn phí, nhanh chóng, lưu trữ Pinecone cho truy vấn RAG.

[[OpenAI Embeddings]] | [[HTTP Request]] | [[Sitemap]]