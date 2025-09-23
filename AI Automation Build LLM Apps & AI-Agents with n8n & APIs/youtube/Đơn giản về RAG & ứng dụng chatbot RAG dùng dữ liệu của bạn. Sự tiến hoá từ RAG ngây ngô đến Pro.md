
![[{55E3D04B-CA35-4725-AA03-AA2D9878CC1D}.png]]
![[{BA2BA966-84C9-409C-92AD-27AD17ADC52D}.png]]


# Retrieval-Augmented Generation (RAG)

### Vấn đề của LLM Độc Lập 
1. kiến thức lỗi thời
2. ảo giác
3. khoảng cách chuyên môn theo lĩnh vực cụ thể
4. thiếu minh bạch và truy vết
5. tốn kén để tinh chỉnh

## Giới thiệu về Retrieval-Augmented Generation (RAG)
Retrieval-Augmented Generation (RAG) là một khung công tác AI (AI framework) mạnh mẽ, cải thiện các mô hình ngôn ngữ lớn (Large Language Models - LLMs) bằng cách tích hợp nguồn tri thức bên ngoài (external knowledge base) để tạo ra câu trả lời chính xác, đáng tin cậy và có ngữ cảnh tốt hơn. RAG giải quyết các hạn chế cố hữu của LLMs, chẳng hạn như thông tin lỗi thời, ảo giác (hallucination), thiếu kiến thức chuyên sâu, thiếu minh bạch và chi phí huấn luyện cao.

### Mục tiêu của RAG
- Tăng cường độ chính xác và tính cập nhật của phản hồi từ mô hình ngôn ngữ.
- Giảm thiểu hiện tượng ảo giác (hallucination) bằng cách sử dụng dữ liệu thực tế từ cơ sở tri thức.
- Cung cấp kiến thức chuyên ngành cho các lĩnh vực cụ thể.
- Cải thiện tính minh bạch và khả năng truy vết (traceability) của thông tin.
- Giảm chi phí so với việc huấn luyện lại hoặc tinh chỉnh (fine-tuning) mô hình.

### Ứng dụng thực tiễn của RAG
- **Hệ thống trả lời câu hỏi (Question Answering):** Cung cấp câu trả lời chính xác, chi tiết cho các câu hỏi chuyên môn.
- **Chatbot hỗ trợ khách hàng:** Tạo chatbot thông minh, cá nhân hóa dựa trên dữ liệu người dùng và tài liệu hướng dẫn.
- **Quản lý tri thức doanh nghiệp:** Giao diện ngôn ngữ tự nhiên (natural language interface) để truy xuất thông tin nội bộ, cải thiện năng suất và hỗ trợ quyết định kinh doanh.
- **Tóm tắt và truy xuất thông tin:** Hỗ trợ xử lý tài liệu dài, thống kê dữ liệu hoặc tự động hóa truy vấn trong các lĩnh vực như y tế, tài chính, pháp lý, giáo dục, thương mại điện tử.

---

## Quy trình cốt lõi của RAG cơ bản

RAG cơ bản bao gồm ba bước chính: **Indexing**, **Retrieval**, và **Generation**.

### 1. Indexing (Lập chỉ mục)
Quy trình chuẩn bị dữ liệu để truy xuất hiệu quả, bao gồm các bước con:

- **Thu thập và chuẩn bị dữ liệu (Data Ingestion and Preparation):**
  - Dữ liệu từ các nguồn như website, tài liệu, PDF, cơ sở dữ liệu được thu thập và tập hợp.
  - [[Thuật ngữ]]: Cơ sở tri thức (Knowledge Base).

- **Phân đoạn (Chunking):**
  - Tài liệu lớn được chia thành các đoạn nhỏ (chunks) để dễ xử lý.
  - Lý do: Các đoạn nhỏ chứa thông tin cụ thể, phù hợp với cửa sổ ngữ cảnh (context window) của mô hình.
  - Phương pháp phân đoạn:
    - Chia theo kích thước ký tự cố định.
    - Chia theo câu hoặc đoạn văn.
    - Đối với mã nguồn, sử dụng phân tích cú pháp (abstract syntax tree - AST).
  - [[Thuật ngữ]]: Phân đoạn (Chunking).

- **Tạo nhúng (Embedding Generation):**
  - Mỗi đoạn văn bản được chuyển thành vector số (embedding) bằng mô hình nhúng (embedding model) như OpenAI Text Embedding hoặc Mure AI.
  - Các vector này nắm bắt ý nghĩa ngữ nghĩa (semantic meaning), giúp các đoạn tương tự nằm gần nhau trong không gian vector.
  - [[Thuật ngữ]]: Nhúng (Embedding).

- **Lưu trữ vector (Vector Storage):**
  - Các vector và đoạn văn bản tương ứng được lưu vào cơ sở dữ liệu vector (vector database) được tối ưu hóa cho tìm kiếm tương đồng.
  - [[Thuật ngữ]]: Cơ sở dữ liệu vector (Vector Database).

### 2. Retrieval (Truy xuất)
Quy trình tìm kiếm thông tin liên quan dựa trên truy vấn của người dùng, diễn ra tại thời điểm suy luận (inference time):

- **Nhúng truy vấn (Query Embedding):**
  - Truy vấn của người dùng được chuyển thành vector nhúng bằng cùng mô hình nhúng đã sử dụng trong bước Indexing.
  - [[Thuật ngữ]]: Truy vấn (Query).

- **Tìm kiếm tương đồng (Similarity Search):**
  - So sánh vector truy vấn với các vector trong cơ sở dữ liệu để tìm các đoạn văn bản liên quan nhất.
  - Kết quả: Trả về các đoạn văn bản có ý nghĩa ngữ nghĩa gần với truy vấn.
  - [[Thuật ngữ]]: Tìm kiếm tương đồng (Similarity Search).

### 3. Generation (Tạo phản hồi)
Quy trình sử dụng mô hình ngôn ngữ để tạo câu trả lời dựa trên dữ liệu truy xuất:

- **Tăng cường lời nhắc (Prompt Augmentation):**
  - Các đoạn văn bản truy xuất được kết hợp với truy vấn gốc để tạo lời nhắc tăng cường (augmented prompt).
  - Lời nhắc được thiết kế (prompt engineering) để hướng dẫn mô hình sử dụng ngữ cảnh hiệu quả.
  - [[Thuật ngữ]]: Lời nhắc tăng cường (Augmented Prompt).

- **Tạo phản hồi từ mô hình ngôn ngữ (LM Response Generation):**
  - Lời nhắc tăng cường được chuyển đến mô hình ngôn ngữ lớn (LLM) như GPT, Gemini hoặc Grok.
  - Mô hình tạo phản hồi dựa trên ngữ cảnh từ dữ liệu truy xuất và truy vấn của người dùng.
  - [[Thuật ngữ]]: Mô hình ngôn ngữ lớn (Large Language Model - LLM).

---

## Hạn chế của RAG cơ bản

Mặc dù RAG cơ bản cung cấp một cách tiếp cận đơn giản để tích hợp tri thức bên ngoài, nó vẫn tồn tại một số hạn chế:

- **Chất lượng truy xuất thấp:**
  - Độ chính xác và độ bao quát của dữ liệu truy xuất có thể không cao.
  - [[Thuật ngữ]]: Độ chính xác truy xuất (Retrieval Accuracy).

- **Dư thừa dữ liệu:**
  - Nhiều đoạn văn bản truy xuất có thể chứa thông tin trùng lặp, dẫn đến phản hồi dài dòng hoặc lặp lại.
  - [[Thuật ngữ]]: Dư thừa dữ liệu (Data Redundancy).

- **Hiện tượng ảo giác (Hallucination):**
  - Nếu ngữ cảnh truy xuất chứa nhiễu (noise), không liên quan hoặc mâu thuẫn, mô hình vẫn có thể tạo ra thông tin không chính xác.
  - Mô hình có thể quay lại sử dụng kiến thức tham số (parametric knowledge) thay vì dữ liệu truy xuất.
  - [[Thuật ngữ]]: Ảo giác (Hallucination).

- **Giới hạn cửa sổ ngữ cảnh (Context Window Limitation):**
  - Mô hình có giới hạn về kích thước cửa sổ ngữ cảnh, dù đã được cải thiện (ví dụ: 1-2 triệu token).
  - Các đoạn văn bản dài hoặc quá nhiều đoạn có thể vượt quá giới hạn hoặc gây mất thông tin giữa chừng (lost-in-the-middle problem).
  - [[Thuật ngữ]]: Cửa sổ ngữ cảnh (Context Window).

- **Hạn chế về hiểu ngữ cảnh:**
  - Mô hình có thể không hiểu đầy đủ hoặc chính xác ngữ cảnh, dẫn đến phản hồi không rõ ràng hoặc không liên quan.
  - [[Thuật ngữ]]: Ngữ cảnh (Context).

- **Khó xử lý truy vấn phức tạp:**
  - RAG cơ bản khó trả lời các câu hỏi phức tạp, cần suy luận hoặc kết nối nhiều mảnh thông tin, đặc biệt trong các lĩnh vực chuyên môn sâu.
  - [[Thuật ngữ]]: Truy vấn phức tạp (Complex Query).

---

## Nhu cầu về RAG nâng cao (Advanced RAG)

Do các hạn chế của RAG cơ bản, cần phát triển các khung công tác RAG nâng cao, tối ưu hóa từng bước trong quy trình. Các cải tiến được chia thành ba module:

### 1. Pre-retrieval (Trước khi truy xuất)
- **Mục tiêu:** Nâng cao chất lượng dữ liệu và xây dựng truy vấn hiệu quả hơn.
- **Phương pháp:**
  - Tối ưu hóa dữ liệu đầu vào (loại bỏ nhiễu, chuẩn hóa định dạng).
  - Tinh chỉnh truy vấn để tăng độ chính xác của tìm kiếm.

### 2. Retrieval (Trong lúc truy xuất)
- **Mục tiêu:** Sử dụng thuật toán tìm kiếm và xếp hạng tinh vi hơn.
- **Phương pháp:**
  - Cải thiện thuật toán tìm kiếm tương đồng.
  - Sử dụng các kỹ thuật xếp hạng nâng cao để chọn lọc dữ liệu phù hợp nhất.

### 3. Post-retrieval (Sau khi truy xuất)
- **Mục tiêu:** Tinh chỉnh ngữ cảnh truy xuất trước khi tạo phản hồi.
- **Phương pháp:**
  - Loại bỏ thông tin dư thừa hoặc không liên quan.
  - Tối ưu hóa ngữ cảnh để phù hợp với cửa sổ ngữ cảnh của mô hình.

### Kiến trúc tự sửa lỗi (Self-Correcting Architecture)
- RAG nâng cao có thể tích hợp các cơ chế tự đánh giá, tự sửa lỗi (self-correcting mechanisms) như Self-RAG hoặc Corrective RAG.
- Mô hình tự phê bình và kiểm tra phản hồi để tăng độ chính xác và đáng tin cậy.
- [[Thuật ngữ]]: Kiến trúc tự sửa lỗi (Self-Correcting Architecture).

---

## So sánh RAG và Fine-Tuning

### RAG
- **Đặc điểm:** Tích hợp tri thức bên ngoài vào mô hình ngôn ngữ tại thời điểm suy luận (inference time) mà không cần thay đổi tham số mô hình.
- **Ưu điểm:**
  - Cập nhật thông tin theo thời gian thực.
  - Minh bạch, cung cấp nguồn tham khảo.
  - Hiệu quả chi phí so với huấn luyện lại mô hình.
- **Hạn chế:** Phụ thuộc vào chất lượng cơ sở tri thức và thuật toán truy xuất.

### Fine-Tuning
- **Đặc điểm:** Huấn luyện lại mô hình trên tập dữ liệu nhỏ, chuyên biệt để điều chỉnh tham số cho một lĩnh vực hoặc nhiệm vụ cụ thể.
- **Ưu điểm:** Tối ưu hóa mô hình cho các tác vụ cụ thể.
- **Hạn chế:**
  - Tốn kém về tài nguyên tính toán và thời gian.
  - Khó cập nhật thông tin mới mà không huấn luyện lại.

| Tiêu chí               | RAG                              | Fine-Tuning                       |
|-----------------------|----------------------------------|-----------------------------------|
| **Độ chính xác**      | Phụ thuộc vào chất lượng truy xuất | Cao cho lĩnh vực cụ thể          |
| **Tính minh bạch**    | Cao, cung cấp nguồn tham khảo    | Thấp, khó truy vết thông tin     |
| **Chi phí**           | Hiệu quả hơn                     | Cao hơn                          |
| **Khả năng mở rộng**  | Dễ dàng cập nhật tri thức        | Khó, cần huấn luyện lại          |

---

## Ghi chú thêm
- Để xây dựng ứng dụng RAG thực tế, có thể sử dụng các công cụ như **n8n** (công cụ tự động hóa AI) để tích hợp cơ sở tri thức và tạo chatbot thông minh.
- Khóa học được đề cập trong transcript ([liên kết khóa học]) hướng dẫn xây dựng chatbot RAG cho doanh nghiệp nhỏ, tập trung vào:
  - Xây dựng cơ sở tri thức từ tài liệu, PDF, bảng biểu.
  - Cào dữ liệu từ web và mạng xã hội.
  - Tạo chatbot hỗ trợ bán hàng, chăm sóc khách hàng và tự động hóa quy trình.

---

## Liên kết chéo
- [[Thuật ngữ]]: Mô hình ngôn ngữ lớn (Large Language Model - LLM)
- [[Thuật ngữ]]: Cơ sở tri thức (Knowledge Base)
- [[Thuật ngữ]]: Tìm kiếm tương đồng (Similarity Search)
- [[Thuật ngữ]]: Ảo giác (Hallucination)
- [[Video]]: Hướng dẫn xây dựng chatbot RAG cơ bản trong n8n

---

**Ghi chú:** Nội dung được diễn giải súc tích từ transcript, tập trung vào các ý chính và lược bỏ phần giới thiệu không cần thiết. Định dạng chuẩn Markdown đảm bảo dễ đọc, dễ tra cứu trong Obsidian.