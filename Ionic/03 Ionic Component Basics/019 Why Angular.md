Chào bạn, tôi là **tóm tắt**. Chúng ta vừa kết thúc phần xây dựng ứng dụng bằng JavaScript thuần. Qua bài học này, bạn sẽ hiểu rõ tại sao chúng ta nên chuyển sang dùng [[Angular]] cho phần còn lại của khóa học thay vì tiếp tục với JavaScript truyền thống.

---

## Tại sao nên dùng Framework (Angular) thay vì JavaScript thuần?

Dù chúng ta đã xây dựng thành công ứng dụng **Budget Planner**, việc quản lý ứng dụng sẽ trở nên cực kỳ khó khăn khi quy mô dự án tăng lên. Dưới đây là 3 lý do chính để sử dụng Angular:

### 1. Không cần "tái phát minh bánh xe" (Low-level Implementation)

Trong JavaScript thuần, chúng ta phải tự tay truy cập [[DOM]] (`querySelector`), tự tạo phần tử (`createElement`) và gắn chúng vào cây thư mục (`appendChild`).

- **Với Angular**: Bạn chỉ cần tập trung vào **Logic nghiệp vụ** (Business Logic). Angular sẽ tự động theo dõi sự thay đổi của dữ liệu và cập nhật giao diện (DOM) cho bạn một cách thông minh.
    

### 2. Quản lý trạng thái (State Management)

Khi ứng dụng lớn hơn, việc truyền dữ liệu giữa các phần khác nhau sẽ trở thành một "cơn ác mộng".

- **Vấn đề**: Làm sao để cập nhật danh sách sản phẩm khi người dùng thay đổi cài đặt ở một trang khác?
    
- **Giải pháp của Angular**: Sử dụng **Services** và **Dependency Injection** (Tiêm phụ thuộc).
    
- **Ví dụ với Alert**: Thay vì phải thêm thẻ `<ion-alert-controller>` vào HTML và tìm nó bằng JS, Angular cho phép bạn "inject" trực tiếp controller này vào code và sử dụng ngay lập tức.
    

### 3. Hệ thống điều hướng mạnh mẽ (Powerful Routing)

Ứng dụng thực tế không chỉ có một trang. Chúng ta cần Tabs, Side Drawers, và chuyển đổi qua lại giữa các trang (như Danh sách sản phẩm -> Chi tiết -> Hồ sơ).

- **Angular Router**: Là một giải pháp đã được kiểm chứng qua hàng triệu dự án. Nó hỗ trợ:
    
    - Truyền tham số trên URL (Query Params).
        
    - Tải chậm ([[Lazy Loading]]): Chỉ tải trang khi người dùng cần đến, giúp ứng dụng chạy cực nhanh.
        
    - Bảo mật tuyến đường (Guards).
        

---

## So sánh quy trình làm việc

|**Đặc điểm**|**Vanilla JavaScript**|**Angular + Ionic**|
|---|---|---|
|**Thao tác giao diện**|Thủ công (Imperative)|Tự động (Declarative)|
|**Cấu trúc dự án**|Tự do (Dễ lộn xộn)|Rõ ràng (Components, Directives, Services)|
|**Tương tác Controller**|Truy vấn DOM|Dependency Injection|
|**Điều hướng trang**|Phức tạp, tự viết|Angular Router chuyên nghiệp|

---

> [!IMPORTANT] Ghi chú cốt lõi
> 
> Angular không thay đổi bản chất của Ionic. Các [[Ionic Components]] vẫn là các Web Components tiêu chuẩn. Angular chỉ đóng vai trò là "người quản lý" giúp bạn điều phối dữ liệu và giao diện hiệu quả hơn.

**Chúng ta đã sẵn sàng bước vào thế giới chuyên nghiệp của Angular và Ionic! Bước tiếp theo, bạn có muốn tôi hướng dẫn cách khởi tạo một dự án Angular - Ionic chuẩn bằng [[Ionic CLI]] và giải thích cấu trúc thư mục của nó không?**