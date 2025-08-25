# Entity Framework Core

## Tổng quan
Entity Framework Core (EF Core) là một Object-Relational Mapping (ORM) framework cho .NET, cho phép developers làm việc với cơ sở dữ liệu sử dụng các đối tượng .NET thay vì viết SQL trực tiếp.

## Các khái niệm chính

### DbContext
- Lớp trung tâm để tương tác với cơ sở dữ liệu
- Quản lý kết nối cơ sở dữ liệu và theo dõi thay đổi (change tracking)
- [[ApplicationDbContext]] - Lớp DbContext tùy chỉnh trong dự án

### Code First Approach
- Định nghĩa model trước, sau đó tạo cơ sở dữ liệu
- Sử dụng [[Migration]] để đồng bộ schema

### Data Annotations
- Thuộc tính để cấu hình model và validation
- [[Data Annotations]] - Chi tiết về các annotation

## Cấu hình trong dự án

### NuGet Packages
Các gói cần thiết:
- [[Microsoft.EntityFrameworkCore]]
- [[Microsoft.EntityFrameworkCore.SqlServer]]
- [[Microsoft.EntityFrameworkCore.Tools]]

### Connection String
- Cấu hình trong [[appsettings.json]]
- [[Connection String]] - Hướng dẫn cấu hình chi tiết

### Dependency Injection
- Đăng ký DbContext trong [[Program.cs]]
- [[Dependency Injection]] trong ASP.NET Core

## Thao tác dữ liệu

### CRUD Operations
- **Create**: Thêm dữ liệu mới
- **Read**: Truy vấn dữ liệu
- **Update**: Cập nhật dữ liệu
- **Delete**: Xóa dữ liệu

### Migration
- [[Migration Commands]] - Các lệnh migration cơ bản
- [[Database Update]] - Cập nhật cơ sở dữ liệu

## Patterns và Architecture

### Repository Pattern
- [[Repository Pattern]] - Tách biệt logic truy cập dữ liệu
- [[IRepository Interface]] - Interface chung cho repository
- [[CategoryRepository]] - Ví dụ cụ thể cho Category

### Unit of Work
- [[Unit of Work Pattern]] - Quản lý transactions
- [[IUnitOfWork]] - Interface Unit of Work

## Trong khóa học

### Section 2: Category CRUD Operations
- [[2-26. Nuget Packages for Entity Framework Core]]
- [[2-27. Setup ApplicationDbContext]]
- [[2-28. Create Database]]
- [[2-29. Create Category Table]]

### Section 3: Razor Project
- [[3-56. Setup EF Core]]
- [[3-58. Display all Categories]]

### Section 5: Repository Pattern
- [[5-70. IRepository Interface]]
- [[5-71. Implement Repository Interface]]
- [[5-72. Implement ICategoryRepository]]
- [[5-73. Implement Category Repository]]
- [[5-74. Replace DbContext with Category Repository]]

## Best Practices

### Performance
- Sử dụng AsNoTracking() cho read-only queries
- Lazy loading vs Eager loading
- [[EF Core Performance]]

### Security
- Parameterized queries (tự động)
- Data validation
- [[Database Security]]

## Liên kết khác
- [[MVC Architecture]] - Vị trí của EF Core trong kiến trúc MVC
- [[N-Tier Architecture]] - EF Core trong kiến trúc nhiều tầng
- [[Database Design]] - Thiết kế cơ sở dữ liệu
- [[SQL Server]] - Cơ sở dữ liệu được sử dụng
- [[LINQ]] - Language Integrated Query với EF Core