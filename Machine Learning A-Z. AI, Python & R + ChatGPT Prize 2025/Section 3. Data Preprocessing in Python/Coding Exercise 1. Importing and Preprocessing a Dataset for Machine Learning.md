## Bài tập Lập trình 1: Nhập và Tiền xử lý Dữ liệu

Bài tập này tập trung vào quy trình cơ bản để chuẩn bị dữ liệu cho [[Machine Learning]] sử dụng Python và bộ dữ liệu mẫu Iris.

## Yêu cầu bài tập

1. **Import thư viện**:
    - Cần sử dụng thư viện `pandas` để xử lý dữ liệu bảng.
    - Import thêm `numpy` và module `train_test_split` từ thư viện `sklearn.model_selection`.

2. **Tải bộ dữ liệu Iris**:
    - Dữ liệu được lưu trong file `iris.csv`.
    - Sử dụng hàm `read_csv` của thư viện pandas để đọc file.
    - Lưu dữ liệu vào biến DataFrame tên là `dataset`.

3. **Xác định đặc trưng (Features) và biến phụ thuộc (Dependent Variable)**: 
    - **Features (Biến độc lập)**: Bao gồm độ dài/rộng của cánh hoa và đài hoa (tất cả các cột trừ cột cuối cùng).
    - **Dependent Variable (Biến phụ thuộc)**: Loài hoa Iris (cột cuối cùng).

4. **Tạo Ma trận đặc trưng (X) và Vector biến phụ thuộc (y)**:    
    - Sử dụng chỉ mục `iloc` trong pandas để tách dữ liệu.
    - Sử dụng thuộc tính `.values` để chuyển đổi dữ liệu thành mảng `numpy`.
    - Lưu các biến độc lập vào `X`.
    - Lưu biến phụ thuộc vào `y`.

5. **Kiểm tra kết quả**:
    - Sử dụng hàm `print()` để in `X` và `y` ra màn hình để xác nhận dữ liệu đã được tách đúng.        

## Mã nguồn tham khảo (Solution Code)
Dưới đây là đoạn mã thực hiện các yêu cầu trên:



```python
	# Import các thư viện cần thiết 
	import pandas as pd 
	import numpy as np 
	from sklearn.model_selection import train_test_split 
	# Tải bộ dữ liệu 
	# Đọc file csv vào biến dataset 
	dataset = pd.read_csv('iris.csv') 
	# Tạo Ma trận đặc trưng (X) và Vector biến phụ thuộc (y) 
	# X: Lấy tất cả các dòng, tất cả các cột TRỪ cột cuối cùng 
	X = dataset.iloc[:, :-1].values 
	# y: Lấy tất cả các dòng, CHỈ lấy cột cuối cùng
	y = dataset.iloc[:, -1].values 
	# In kết quả để kiểm tra 
	print("Matrix of features (X):") 
	print(X) 
	print("\nDependent variable vector (y):") 
	print(y)
```

## Ghi chú thêm

- **iloc**: Là công cụ mạnh mẽ của Pandas để chọn dữ liệu theo vị trí chỉ số (integer-location based indexing).
    - Cú pháp `[:, :-1]` nghĩa là "lấy mọi hàng, và lấy từ cột đầu đến cột áp chót".
    - Cú pháp `[:, -1]` nghĩa là "lấy mọi hàng, và chỉ lấy cột cuối cùng".
- File `iris.csv` phải nằm cùng thư mục với file code hoặc bạn phải cung cấp đường dẫn tuyệt đối chính xác tới file.