# Migration

## Tổng quan
Migration trong Entity Framework Core là cơ chế để quản lý và đồng bộ hóa schema cơ sở dữ liệu với model trong code.

## Khái niệm chính

### Code First Approach
- Định nghĩa model trước
- Tạo migration từ model
- Áp dụng migration để tạo/cập nhật database

### Migration Files
- Chứa các lệnh Up() và Down()
- Up(): Áp dụng thay đổi
- Down(): Rollback thay đổi

## Lệnh Migration cơ bản

### Tạo Migration
```bash
Add-Migration InitialCreate
# hoặc
dotnet ef migrations add InitialCreate
```

### Cập nhật Database
```bash
Update-Database
# hoặc
dotnet ef database update
```

### Xem danh sách Migration
```bash
dotnet ef migrations list
```

### Xóa Migration
```bash
Remove-Migration
# hoặc
dotnet ef migrations remove
```

## Workflow Migration

### 1. Tạo/Sửa Model
- Thêm thuộc tính mới
- Thay đổi [[Data Annotations]]
- Cập nhật [[ApplicationDbContext]]

### 2. Tạo Migration
- Chạy lệnh Add-Migration
- EF Core tự động tạo migration file

### 3. Review Migration
- Kiểm tra file migration được tạo
- Đảm bảo logic Up/Down đúng

### 4. Cập nhật Database
- Chạy Update-Database
- Schema database được cập nhật

## Best Practices

### Naming Convention
- Sử dụng tên có ý nghĩa
- VD: `AddCategoryTable`, `UpdateProductPrice`

### Data Seeding
- Thêm dữ liệu mẫu trong OnModelCreating
- Sử dụng HasData() method

### Rollback Strategy
- Luôn test migration trước khi deploy
- Backup database trước khi migrate

## Trong khóa học
- [[2-28. Create Database]] - Tạo database đầu tiên
- [[2-29. Create Category Table]] - Migration cho Category table
- [[3-56. Setup EF Core]] - Setup trong Razor project

## Liên kết nội bộ
- [[Entity Framework Core]] - Framework chính
- [[ApplicationDbContext]] - Context class
- [[Connection String]] - Cấu hình kết nối
- [[Database Update]] - Cập nhật database
