# ApplicationDbContext

## Tổng quan
ApplicationDbContext là lớp kế thừa từ DbContext, đóng vai trò trung tâm để quản lý kết nối và thao tác với cơ sở dữ liệu trong ứng dụng ASP.NET Core MVC.

## Cấu trúc cơ bản

### Khai báo lớp
```csharp
public class ApplicationDbContext : DbContext
{
    public ApplicationDbContext(DbContextOptions<ApplicationDbContext> options) : base(options)
    {
    }
    
    // DbSet properties
    public DbSet<Category> Categories { get; set; }
}
```

## Cấu hình

### Connection String
- Cấu hình trong [[appsettings.json]]
- Sử dụng [[Connection String]] để kết nối SQL Server

### Dependency Injection
- Đăng ký trong [[Program.cs]]
- Sử dụng [[Dependency Injection]] pattern

### OnModelCreating
```csharp
protected override void OnModelCreating(ModelBuilder modelBuilder)
{
    // Seeding data
    modelBuilder.Entity<Category>().HasData(
        new Category { Id = 1, Name = "Action", DisplayOrder = 1 },
        new Category { Id = 2, Name = "SciFi", DisplayOrder = 2 },
        new Category { Id = 3, Name = "History", DisplayOrder = 3 }
    );
}
```

## Sử dụng trong Controller

### Dependency Injection
```csharp
public class CategoryController : Controller
{
    private readonly ApplicationDbContext _db;
    
    public CategoryController(ApplicationDbContext db)
    {
        _db = db;
    }
}
```

## Liên kết nội bộ
- [[Entity Framework Core]] - Framework chính
- [[DbContext]] - Lớp cơ sở
- [[Migration]] - Quản lý schema database
- [[Data Annotations]] - Cấu hình model
- [[Repository Pattern]] - Alternative pattern
