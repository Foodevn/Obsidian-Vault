## Bài tập Lập trình 3: Mã hóa Dữ liệu Phân loại (Titanic Dataset)

Bài tập này yêu cầu áp dụng kỹ thuật **OneHotEncoding** và **LabelEncoding** để xử lý dữ liệu dạng chữ (categorical) trong bộ dữ liệu nổi tiếng Titanic.

## Quy trình thực hiện

## 1. Chuẩn bị Thư viện và Dữ liệu
- **Thư viện**: Cần `pandas`, `numpy`, `ColumnTransformer` (từ `sklearn.compose`), `OneHotEncoder` và `LabelEncoder` (từ `sklearn.preprocessing`).
- **Dữ liệu**: Tải file `titanic.csv` vào một Pandas DataFrame.

## 2. Xử lý Biến Độc lập (Features)
- **Xác định cột phân loại**: Trong dataset Titanic, các cột thường chứa dữ liệu phân loại là `Sex` (Giới tính), `Embarked` (Cảng đi), và `Pclass` (Hạng vé - dù là số nhưng bản chất là phân loại).
- **OneHotEncoding**: Sử dụng `ColumnTransformer` để áp dụng `OneHotEncoder` lên các cột này.
- **Lưu ý**: Cần danh sách tên cột (hoặc chỉ số cột) để truyền vào `ColumnTransformer`.

## 3. Xử lý Biến Phụ thuộc (Dependent Variable)
- **Cột mục tiêu**: `Survived` (Sống sót).
- **LabelEncoding**: Mặc dù cột này trong dữ liệu gốc có thể đã là 0 và 1, nhưng theo yêu cầu bài tập, ta sử dụng `LabelEncoder` để chuẩn hóa nó thành vector nhị phân.

## Mã nguồn giải pháp (Solution Code)

```python
# Importing the necessary libraries
import pandas as pd
import numpy as np
from sklearn.compose import ColumnTransformer
from sklearn.preprocessing import OneHotEncoder, LabelEncoder
# Load the dataset
df = pd.read_csv('titanic.csv')
# Identify the categorical data
categorical_features = ['Sex', 'Embarked', 'Pclass']
# Implement an instance of the ColumnTransformer class
ct = ColumnTransformer(
    transformers=[
        ('encoder', OneHotEncoder(), categorical_features)
    ], remainder='passthrough')
# Apply the fit_transform method on the instance of ColumnTransformer
X = ct.fit_transform(df)
# Convert the output into a NumPy array
X = np.array(X)
# Use LabelEncoder to encode binary categorical data
le = LabelEncoder()
y = le.fit_transform(df['Survived'])
# Print the updated matrix of features and the dependent variable vector
print("Updated matrix of features: \n", X)
print("Updated dependent variable vector: \n", y)
```

## Ghi chú kỹ thuật
- **`categorical_features`**: Khi làm việc với Pandas DataFrame trong `ColumnTransformer`, bạn có thể truyền trực tiếp **tên cột** (dạng chuỗi) thay vì chỉ số cột (dạng số). Điều này giúp code dễ đọc hơn.
- **`fit_transform`**: Luôn nhớ ép kiểu kết quả trả về của `ColumnTransformer` sang `np.array` để đảm bảo tương thích tốt nhất với các mô hình Scikit-learn sau này.