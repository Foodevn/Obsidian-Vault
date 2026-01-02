## Bài tập Lập trình 4: Chia Dữ liệu và Chuẩn hóa Đặc trưng

Bài tập này kết hợp hai kỹ thuật quan trọng trong tiền xử lý dữ liệu: **Train-Test Split** và **Feature Scaling** (cụ thể là Standardization).

# Quy trình thực hiện

## 1. Chuẩn bị Thư viện và Dữ liệu

- **Thư viện**: `pandas`, `train_test_split` (từ `sklearn.model_selection`), và `StandardScaler` (từ `sklearn.preprocessing`).
- **Dữ liệu**: Tải file `iris.csv` vào DataFrame.

## 2. Chia Dữ liệu (Splitting)

- Tách biến độc lập (Features - X) và biến phụ thuộc (Target - y).
- Sử dụng `train_test_split` với tỷ lệ **80% train - 20% test**.
- Đặt `random_state=42` để đảm bảo kết quả có thể tái lập (reproducible).

## 3. Chuẩn hóa Đặc trưng (Feature Scaling)

- Sử dụng `StandardScaler` để đưa các đặc trưng về cùng một thang đo (mean=0, std=1).
- **Nguyên tắc vàng**:
    - `fit_transform` trên **X_train** (để tính toán trung bình và độ lệch chuẩn từ tập huấn luyện).
    - Chỉ `transform` trên **X_test** (sử dụng thông số đã tính từ tập huấn luyện).

## Mã nguồn giải pháp (Solution Code)



```python 
# 1. Import thư viện 
import pandas as pd 
from sklearn.model_selection import train_test_split 
from sklearn.preprocessing import StandardScaler 

# 2. Tải bộ dữ liệu 
# Giả định iris.csv có cột cuối là target 
dataset = pd.read_csv('iris.csv') 
# Tách features (X) và target (y) 
X = dataset.iloc[:, :-1].values 
y = dataset.iloc[:, -1].values 

# 3 & 4. Chia dữ liệu (80-20 split, random_state=42) 
X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.2, random_state=42) 

# 5. In kết quả chia dữ liệu (tùy chọn, để kiểm tra) 
print("--- Trước khi Scaling ---") 
print("X_train shape:", X_train.shape) 
print("X_test shape:", X_test.shape) 

# 6. Áp dụng Feature Scaling (StandardScaler) 
scaler = StandardScaler() 
# Fit và Transform trên tập huấn luyện 
X_train = scaler.fit_transform(X_train) 
# Chỉ Transform trên tập kiểm tra (KHÔNG được fit lại) 
X_test = scaler.transform(X_test) 

# 7. In kết quả sau khi Scaling 
print("\n--- Sau khi Scaling (5 dòng đầu) ---") 
print("X_train scaled:\n", X_train[:5]) 
print("X_test scaled:\n", X_test[:5])
```

## Ghi chú quan trọng

- **Tại sao chỉ `transform` trên Test Set?**: Để đảm bảo tập kiểm tra hoàn toàn "khách quan". Nếu ta `fit` lại trên tập test, ta sẽ dùng thông số thống kê của tập test để chuẩn hóa chính nó, dẫn đến sai lệch so với mô hình đã học từ tập train.
- **Kết quả Scaling**: Sau khi chuẩn hóa, các giá trị trong `X_train` và `X_test` sẽ thường nằm trong khoảng nhỏ (ví dụ từ -3 đến 3), thay vì các giá trị gốc.