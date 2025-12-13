## Bài tập Lập trình 2: Xử lý Dữ liệu Thiếu

Bài tập này tập trung vào việc thực hành quy trình làm sạch dữ liệu bằng cách thay thế các giá trị bị thiếu bằng giá trị trung bình, sử dụng thư viện `scikit-learn`.

## Quy trình thực hiện

## 1. Chuẩn bị và Kiểm tra Dữ liệu

- **Thư viện cần thiết**: `numpy`, `pandas`, và lớp `SimpleImputer` từ `sklearn.impute`.
- **Tải dữ liệu**: Đọc file `pima-indians-diabetes.csv` vào DataFrame.
- **Kiểm tra dữ liệu thiếu**: Trước khi xử lý, cần xác định cột nào chứa dữ liệu thiếu. Việc bỏ qua bước này có thể dẫn đến kết quả huấn luyện mô hình [[Machine Learning]] không chính xác hoặc gây lỗi.

## 2. Chiến lược xử lý (Imputation Strategy)

- **Phương pháp chọn**: Thay thế bằng **giá trị trung bình** (Mean imputation).
- **Lý do**: Đây là phương pháp phổ biến để duy trì phân phối thống kê của dữ liệu mà không cần loại bỏ các mẫu dữ liệu quý giá (như phương pháp xóa dòng/cột).

## 3. Cấu hình và Áp dụng `SimpleImputer`

- **Khởi tạo**: Tạo đối tượng `SimpleImputer` với `missing_values=np.nan` và `strategy='mean'`.
- **Fit**: Tính toán giá trị trung bình trên các cột số của ma trận đặc trưng.
- **Transform**: Thay thế các giá trị `nan` bằng giá trị trung bình vừa tính toán.
- **Cập nhật**: Gán ngược lại dữ liệu đã xử lý vào ma trận gốc.

## Mã nguồn giải pháp (Solution Code)

```python
# Importing the necessary libraries
from sklearn.impute  import SimpleImputer
import pandas as pd
import numpy as np
# Load the dataset
dataset =pd.read_csv('pima-indians-diabetes.csv')
X = dataset.iloc[:, :-1].values
y = dataset.iloc[:, -1].values
# Identify missing data (assumes that missing data is represented as NaN)
print("Số lượng dữ liệu thiếu trên mỗi cột:")
print( (dataset == 0).sum())
# Print the number of missing entries in each column

# Configure an instance of the SimpleImputer class
imputer = SimpleImputer(missing_values=0, strategy='mean')
# Fit the imputer on the DataFrame
imputer.fit(X)
# Apply the transform to the DataFrame
X=imputer.transform(X)
#Print your updated matrix of features
print(X)
```

## Ghi chú quan trọng
- **`fit` vs `transform`**: `fit` chỉ tính toán (học) các thông số từ dữ liệu, còn `transform` mới thực sự áp dụng (sửa đổi) dữ liệu.
- **Phạm vi áp dụng**: Trong bài tập này, chúng ta áp dụng trên toàn bộ ma trận `X` vì bộ dữ liệu Pima Indians Diabetes thường chỉ chứa các chỉ số sinh học dạng số. Nếu dữ liệu có chứa chuỗi (string), cần chỉ định rõ phạm vi cột (ví dụ: `X[:, 1:3]`) để tránh lỗi.