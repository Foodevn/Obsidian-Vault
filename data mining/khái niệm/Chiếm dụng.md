# 1. Chiếm dụng là gì?
**Chiếm dụng (occupancy)** đo lường **tỷ lệ phần trăm** mà một mẫu (pattern) chiếm trong một giao dịch. Nói cách khác, nó cho biết mẫu đó **"lấp đầy"** bao nhiêu phần trăm của giao dịch.​
## Ví dụ dễ hiểu

Hãy tưởng tượng bạn đi siêu thị và mua một giỏ hàng:​
**Giỏ hàng của bạn có 10 món đồ:**

- 3 loại trái cây (táo, cam, chuối)
- 2 loại rau (cà chua, dưa chuột)
- 5 món khác

**Mẫu cần xem xét:** {táo, cam, chuối}
**Chiếm dụng (occupancy)** của mẫu này = 3 món / 10 món tổng cộng = **0.3 hoặc 30%​
Điều này có nghĩa là mẫu {trái cây} chiếm **30%** giỏ hàng của bạn.​

## So sánh với ví dụ khác

**Giỏ hàng A:** 10 món, trong đó có 3 món trái cây → Occupancy = 30%  
**Giỏ hàng B:** 5 món, trong đó có 3 món trái cây → Occupancy = 60%

Mặc dù cả hai giỏ đều có **cùng số lượng trái cây** (3 món), nhưng mẫu {trái cây} **chiếm dụng nhiều hơn** trong giỏ hàng B vì nó chiếm tỷ lệ lớn hơn (60% so với 30%).​

## Tại sao chiếm dụng quan trọng?

Chiếm dụng là **thước đo tương đối**, không phải tuyệt đối. Nó giúp ta hiểu:​

**Mức độ quan trọng** của một mẫu trong từng giao dịch cụ thể, không chỉ dựa vào số lượng.​
**Chất lượng của mẫu**: Một mẫu có occupancy cao nghĩa là nó chiếm phần lớn trong các giao dịch mà nó xuất hiện, cho thấy đây là mẫu quan trọng và có ý nghĩa.​

## Khi kết hợp với tiện ích (utility)

Khi ta kết hợp chiếm dụng với tiện ích (giá trị/lợi nhuận), ta được **utility occupancy**:​

**Ví dụ:**

- Giỏ hàng trị giá tổng cộng: 100,000 đồng
- Giá trị 3 món trái cây: 40,000 đồng
- **Utility occupancy** = 40,000 / 100,000 = **40%**

Điều này cho biết các món trái cây không chỉ chiếm 30% về **số lượng** mà còn chiếm 40% về **giá trị** của giỏ hàng.​

## Mẫu chiếm dụng cao (High Occupancy Pattern)

Một mẫu được gọi là **mẫu chiếm dụng cao** khi tỷ lệ chiếm dụng của nó vượt qua ngưỡng do người dùng đặt ra. Ví dụ, nếu ngưỡng là 50%, thì mẫu {trái cây} trong giỏ hàng B (60%) là mẫu chiếm dụng cao, còn trong giỏ hàng A (30%) thì không.​

Tóm lại, **chiếm dụng** đơn giản là đo lường **tỷ lệ phần trăm** mà một nhóm sản phẩm chiếm trong tổng số sản phẩm (hoặc tổng giá trị) của mỗi lần mua hàng.​

# 2.Định nghĩa trong bài báo

**Chiếm dụng tiện ích (Utility Occupancy - uo)** của một mẫu trong giao dịch được định nghĩa là tỷ lệ giữa tiện ích của mẫu đó và tổng tiện ích của toàn bộ giao dịch. Công thức:​
![[{254D402F-693F-49CC-824B-786CBC3AA9B8}.png]]
![[{C287BFAA-902E-47B2-A7A4-209E21D6B078}.png]]
## Điều kiện để là mẫu chiếm dụng tiện ích cao (HUOP)

Một mẫu P được coi là **mẫu chiếm dụng tiện ích cao** (High Utility Occupancy Pattern) khi thỏa mãn **đồng thời hai điều kiện**:​

**Điều kiện 1 - Support (độ hỗ trợ)**: sup(P) ≥ minSupsup(P) , nghĩa là số lần xuất hiện của mẫu phải không nhỏ hơn ngưỡng tối thiểu.​

**Điều kiện 2 - Utility Occupancy**: uo(P) ≥ δuo(P), nghĩa là giá trị chiếm dụng tiện ích của mẫu phải không nhỏ hơn ngưỡng δ\deltaδ do người dùng định nghĩa.​

## Ví dụ cụ thể từ bài báo

Trong Ví dụ 2 của bài báo, giả sử:​

- Item A có uo = **0.167** trong giao dịch T1
- Tổng tiện ích của T1 (TU) = **18**
- Utility của item A trong T1 = 0.167 × 18 = **3**

Điều này có nghĩa là item A chiếm **16.7%** giá trị tiện ích của giao dịch T1.​

## Sự khác biệt với phương pháp truyền thống

**Phương pháp tiện ích cao truyền thống** (High Utility Pattern Mining) chỉ xem xét tổng lợi nhuận và số lượng của các mẫu, không tính đến mức độ đóng góp **tương đối** của mỗi mẫu trong từng giao dịch.​

**Phương pháp chiếm dụng tiện ích cao** không chỉ xem xét lợi nhuận tuyệt đối mà còn xem xét **tỷ lệ phần trăm** mà mẫu đó chiếm trong giao dịch. Điều này giúp phát hiện các mẫu có **ý nghĩa quan trọng tương đối** trong các giao dịch mà chúng xuất hiện.[sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0950705125014923)​

## Ứng dụng thực tế trong bài báo

Trong hệ thống đề xuất cho khách hàng, phương pháp này cho phép khách hàng lựa chọn các sản phẩm tối ưu mà họ có khả năng mua. Người dùng có thể được hiển thị danh sách các sản phẩm có cấu hình tương tự dưới dạng quảng cáo.[sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0950705125014923)​

## Đặc điểm quan trọng

Trong môi trường luồng dữ liệu động, bài báo này còn áp dụng thêm **hệ số suy giảm** (damped window control) để gán tầm quan trọng tương đối cho các mẫu dựa trên thời gian xuất hiện của giao dịch. Các giao dịch mới nhất sẽ có trọng số cao hơn, giúp phát hiện xu hướng gần đây trong dữ liệu.[sciencedirect](https://www.sciencedirect.com/science/article/abs/pii/S0950705125014923)​

1. [https://www.sciencedirect.com/science/article/abs/pii/S0950705125014923](https://www.sciencedirect.com/science/article/abs/pii/S0950705125014923)
2. [https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_84e04851-69a9-4db9-bddd-2cf370ec2e9d/40b4f01e-49d7-4d75-a595-0d47619103e7/1-s2.0-S0950705125014923-main.pdf](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/collection_84e04851-69a9-4db9-bddd-2cf370ec2e9d/40b4f01e-49d7-4d75-a595-0d47619103e7/1-s2.0-S0950705125014923-main.pdf)