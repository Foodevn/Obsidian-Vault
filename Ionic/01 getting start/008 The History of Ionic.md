## Lịch sử và Sự tiến hóa của Ionic

Ionic đã trải qua một quá trình chuyển đổi quan trọng về mặt công nghệ, từ việc phụ thuộc hoàn toàn vào Angular sang việc trở thành một nền tảng độc lập.

### 1. Giai đoạn phụ thuộc [[Angular]] (Ionic 1 - 3)

Trong quá khứ, Ionic được thiết kế dành riêng cho Angular.

- **Ionic 1 (2013)**:
    - Xây dựng dựa trên **Angular 1**.
    - Sử dụng các chỉ thị tùy biến của Angular (Custom Angular Directives) để tạo ra các thành phần giao diện.
    - _Lý do_: Thời điểm này trình duyệt chưa hỗ trợ chuẩn [[Web Components]].

- **Ionic 2 (2016)**:
    - Cập nhật để hỗ trợ **Angular 2+** (phiên bản lột xác hoàn toàn so với Angular 1).
    - Vẫn sử dụng các thành phần của Angular (Angular Components), không phải Web Components.

- **Ionic 3**:
    - Là bản nâng cấp tính năng của Ionic 2.
    - Vẫn bị giới hạn: Chỉ hoạt động trong ứng dụng Angular.

### 2. Bước ngoặt công nghệ: [[Ionic 4]] và Kỷ nguyên [[Web Components]]

Từ phiên bản 4 trở đi, Ionic thực hiện một thay đổi mang tính cách mạng để giải quyết vấn đề giới hạn nền tảng.
- **Công nghệ cốt lõi**: Chuyển đổi hoàn toàn sang **Thành phần Web (Web Components)**.
    - Đây là một tiêu chuẩn của trình duyệt (Browser specification), cho phép tạo các thẻ HTML tùy chỉnh.
    - Chạy dựa trên [[JavaScript]] thuần, không phụ thuộc vào framework.
- **Lợi ích to lớn**:
    - **Độc lập Framework (Framework Agnostic)**: Ionic 4+ có thể sử dụng với bất kỳ framework nào ([[React]], [[Vue]], [[Angular]]) hoặc thậm chí không cần framework (Vanilla JS).
    - Mở rộng đối tượng sử dụng, không còn bó hẹp trong cộng đồng Angular.

---

## Lộ trình phát triển và Tương lai

Ionic hiện tại áp dụng quy trình phát triển ổn định và dễ dự đoán, tương tự như quy trình của Angular hiện đại.

- **Chu kỳ phát hành**: Phiên bản mới ra mắt mỗi **6 tháng**.
- **Tính chất cập nhật**:
    - Các thay đổi mang tính **tích lũy nhỏ (Incremental enhancements)**.
    - **Tương thích ngược (Backward Compatible)**: Đảm bảo mã nguồn cũ vẫn hoạt động tốt, không yêu cầu viết lại ứng dụng khi nâng cấp phiên bản.
- **Kết luận**: Ionic 4+ và các phiên bản tương lai mang lại sự linh hoạt tối đa và là phiên bản tốt nhất tính đến nay.

---

**Ghi chú:**

- [[Web Components]]: Một bộ các tiêu chuẩn web cho phép tạo ra các thẻ HTML tùy chỉnh có thể tái sử dụng, với chức năng được đóng gói tách biệt khỏi phần còn lại của mã nguồn ứng dụng.
