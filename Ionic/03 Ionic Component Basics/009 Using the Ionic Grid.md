## Tối ưu hóa giao diện với Hệ thống Lưới (Grid)

Hệ thống lưới của Ionic cực kỳ mạnh mẽ, giúp ứng dụng của bạn trông đẹp mắt cả trên điện thoại (màn hình nhỏ) lẫn máy tính (màn hình lớn).

### 1. Cấu trúc cơ bản của Grid

Một hệ thống lưới tiêu chuẩn luôn tuân theo phân cấp:
- **`<ion-grid>`**: Thẻ bao ngoài cùng.
- **`<ion-row>`**: Đại diện cho một hàng ngang.
- **`<ion-col>`**: Đại diện cho các cột trong hàng.

### 2. Nguyên tắc 12 cột (12-Column System)

Mặc định, Ionic chia chiều ngang màn hình thành **12 phần bằng nhau**.
- Nếu bạn đặt `size="6"`, cột đó sẽ chiếm 50% chiều rộng ($6/12$).
- Nếu đặt `size="12"`, cột đó sẽ chiếm 100% chiều rộng.

### 3. Thiết kế đáp ứng (Responsive Design) với Breakpoints

Để giao diện tự động thay đổi theo thiết bị, chúng ta sử dụng các thuộc tính đi kèm với kích thước màn hình:
- **`xs`** (extra small): Điện thoại nhỏ.
- **`sm`** (small): Điện thoại lớn/Máy tính bảng.
- **`md`** (medium): Máy tính bảng lớn/Laptop.
- **`lg`** (large): Màn hình máy tính để bàn.

Cách áp dụng thực tế:

Thay vì dùng size="6" (cố định cho mọi màn hình), ta dùng size-md="6". Điều này có nghĩa là: "Trên màn hình từ trung bình trở lên, hãy chiếm 6 cột. Còn trên màn hình nhỏ hơn, hãy mặc định chiếm toàn bộ 12 cột".

### 4. Căn giữa nội dung với Offset

Để đưa một khối nội dung vào giữa màn hình, chúng ta sử dụng thuộc tính `offset`.
- **Ví dụ**: Nếu cột rộng 6, ta cần đẩy nó sang phải 3 đơn vị ($3 \text{ (trái)} + 6 \text{ (nội dung)} + 3 \text{ (phải)} = 12$).

---

### 5. Thực hành: Mã nguồn tối ưu cho Budget Planner

Dưới đây là cách chúng ta bao bọc chiếc `ion-card` để nó luôn đẹp:

```HTML
<ion-content>
  <ion-grid>
    <ion-row>
      <ion-col size-md="6" offset-md="3">
        
        <ion-card>
          <ion-card-header>
            <ion-card-title>Thêm chi tiêu mới</ion-card-title>
          </ion-card-header>
          <ion-card-content>
            </ion-card-content>
        </ion-card>

      </ion-col>
    </ion-row>
  </ion-grid>
</ion-content>
```

### Kết quả đạt được

- **Trên Mobile**: Chiếc Card hiển thị tràn màn hình (full-width), dễ dàng thao tác.
- **Trên Desktop**: Chiếc Card thu nhỏ lại còn 50% và nằm chính giữa màn hình, trông rất chuyên nghiệp và cân đối.

---

> [!IMPORTANT] Quy tắc kế thừa
> 
> Các thuộc tính như size-md hay offset-md áp dụng cho kích thước màn hình đó trở lên (ví dụ: tác động đến cả md, lg, xl).
