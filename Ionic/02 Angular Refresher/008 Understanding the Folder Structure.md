## Giải phẫu Cấu trúc Dự án Angular

Sau khi tạo dự án và chạy thử, chúng ta sẽ đi sâu vào thư mục `src` – nơi chứa toàn bộ mã nguồn ứng dụng.

### 1. File khởi động: `main.ts`
Đây là điểm bắt đầu của ứng dụng (Entry Point).
- **Vai trò**: Chứa logic để khởi động (bootstrap) toàn bộ ứng dụng Angular.
- **Cơ chế**:
    - Sử dụng hàm `platformBrowserDynamic().bootstrapModule(AppModule)`.
    - Nó báo cho Angular biết module nào là module gốc (Root Module) để bắt đầu chạy. Ở đây là `AppModule`.

### 2. Module gốc: `app.module.ts`

Đây là nơi cấu hình "bộ não" của ứng dụng.

- **Vị trí**: `src/app/app.module.ts`.
- **Khái niệm**: Angular tổ chức mã nguồn theo các **Modules** (đừng nhầm lẫn với các file module của JavaScript). Mỗi module là một gói chứa các tính năng liên quan.
- **Decorator `@NgModule`**: Đây là thành phần quan trọng nhất, dùng để đánh dấu một class là một Angular Module và cung cấp metadata cấu hình.

#### Các thuộc tính quan trọng trong `@NgModule`:

| **Thuộc tính**     | **Ý nghĩa**                                                                                                                  | **Ví dụ trong code**                                             |
| ------------------ | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| **`declarations`** | Khai báo các **Components** thuộc về module này. Nếu bạn tạo component mới, bạn phải khai báo nó ở đây thì Angular mới hiểu. | `[AppComponent]`                                                 |
| **`imports`**      | Nhập các Module khác cần thiết cho module này hoạt động.                                                                     | `[BrowserModule]` (Module bắt buộc để chạy app trên trình duyệt) |
| **`providers`**    | Nơi khai báo các Services (sẽ học sau).                                                                                      | `[]` (Hiện tại đang trống)                                       |
| **`bootstrap`**    | Chỉ định **Root Component** sẽ được nạp đầu tiên khi ứng dụng chạy.                                                          | `[AppComponent]`                                                 |

### 3. Thành phần gốc: `AppComponent`

- Được khai báo trong `app.module.ts` và thường là thành phần đầu tiên được hiển thị.
- Chúng ta sẽ tìm hiểu chi tiết về file này (`app.component.ts`) ở phần tiếp theo.

---

**Ghi chú:**

- [[Decorator]]: Một tính năng của TypeScript (bắt đầu bằng `@`), giúp bổ sung thông tin (metadata) cho class, method hoặc property. Ví dụ: `@NgModule`, `@Component`.
- [[Class]]: Bản thiết kế (blueprint) để tạo ra các đối tượng.

**Tóm tắt luồng khởi động:**

1. `main.ts` chạy → gọi `AppModule`.
2. `AppModule` chạy → đọc cấu hình `@NgModule`.
3. Tìm `bootstrap: [AppComponent]` → khởi tạo `AppComponent`.
4. `AppComponent` được hiển thị lên trình duyệt.

**Bước tiếp theo:** Bạn có muốn chúng ta "mổ xẻ" file `app.component.ts` để xem một Component thực sự được cấu tạo như thế nào không?