# Dependency Injection

## Tổng quan
Dependency Injection (DI) là một design pattern và một cơ chế tích hợp sẵn trong ASP.NET Core để quản lý dependencies và đảo ngược control (Inversion of Control - IoC).

## Khái niệm cơ bản

### Dependency
- Một object mà class khác phụ thuộc vào để hoạt động
- Ví dụ: Controller phụ thuộc vào DbContext để truy cập database

### Injection
- Quá trình cung cấp dependency từ bên ngoài thay vì tạo trong class
- Container sẽ tự động inject dependency khi class được khởi tạo

## Service Lifetimes

### Transient
```csharp
builder.Services.AddTransient<IRepository, Repository>();
```
- Tạo instance mới mỗi lần được request
- Sử dụng cho lightweight, stateless services

### Scoped
```csharp
builder.Services.AddScoped<ApplicationDbContext>();
builder.Services.AddScoped<IUnitOfWork, UnitOfWork>();
```
- Một instance per HTTP request
- Sử dụng cho DbContext, Repository patterns

### Singleton
```csharp
builder.Services.AddSingleton<IConfiguration, Configuration>();
```
- Một instance cho toàn bộ application lifetime
- Sử dụng cho configuration, logging

## Cách đăng ký Services

### Generic Method
```csharp
builder.Services.AddScoped<IRepository<Category>, Repository<Category>>();
```

### Factory Method
```csharp
builder.Services.AddScoped<IEmailService>(provider =>
{
    var config = provider.GetRequiredService<IConfiguration>();
    return new EmailService(config.GetConnectionString("EmailConnection"));
});
```

### Multiple Implementations
```csharp
builder.Services.AddScoped<INotificationService, EmailService>();
builder.Services.AddScoped<INotificationService, SmsService>();
```

## Constructor Injection

### Trong Controller
```csharp
public class CategoryController : Controller
{
    private readonly IUnitOfWork _unitOfWork;
    private readonly ILogger<CategoryController> _logger;

    public CategoryController(IUnitOfWork unitOfWork, ILogger<CategoryController> logger)
    {
        _unitOfWork = unitOfWork;
        _logger = logger;
    }
}
```

### Trong Repository
```csharp
public class Repository<T> : IRepository<T> where T : class
{
    private readonly ApplicationDbContext _db;

    public Repository(ApplicationDbContext db)
    {
        _db = db;
    }
}
```

## Service Locator Pattern (Anti-pattern)

### Tránh sử dụng
```csharp
// DON'T DO THIS
public class BadController : Controller
{
    public IActionResult Index()
    {
        var serviceProvider = HttpContext.RequestServices;
        var unitOfWork = serviceProvider.GetService<IUnitOfWork>();
        // ...
    }
}
```

### Sử dụng Constructor Injection thay thế
```csharp
// DO THIS
public class GoodController : Controller
{
    private readonly IUnitOfWork _unitOfWork;

    public GoodController(IUnitOfWork unitOfWork)
    {
        _unitOfWork = unitOfWork;
    }
}
```

## Cấu hình Entity Framework

### DbContext Registration
```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

### Repository Pattern
```csharp
builder.Services.AddScoped<IUnitOfWork, UnitOfWork>();
builder.Services.AddScoped<ICategoryRepository, CategoryRepository>();
```

## Interface và Implementation

### Tạo Interface
```csharp
public interface IEmailService
{
    Task SendEmailAsync(string to, string subject, string body);
}
```

### Implementation
```csharp
public class EmailService : IEmailService
{
    private readonly IConfiguration _config;

    public EmailService(IConfiguration config)
    {
        _config = config;
    }

    public async Task SendEmailAsync(string to, string subject, string body)
    {
        // Implementation
    }
}
```

### Registration
```csharp
builder.Services.AddScoped<IEmailService, EmailService>();
```

## Testing với DI

### Mock Dependencies
```csharp
[Test]
public void Index_ReturnsViewWithCategories()
{
    // Arrange
    var mockUnitOfWork = new Mock<IUnitOfWork>();
    var categories = new List<Category> { /* test data */ };
    mockUnitOfWork.Setup(u => u.Category.GetAll()).Returns(categories);

    var controller = new CategoryController(mockUnitOfWork.Object);

    // Act
    var result = controller.Index();

    // Assert
    var viewResult = Assert.IsType<ViewResult>(result);
    var model = Assert.IsAssignableFrom<List<Category>>(viewResult.Model);
    Assert.Equal(categories.Count, model.Count);
}
```

## Built-in Services

### Logging
```csharp
public class CategoryController : Controller
{
    private readonly ILogger<CategoryController> _logger;

    public CategoryController(ILogger<CategoryController> logger)
    {
        _logger = logger;
    }
}
```

### Configuration
```csharp
public class EmailService
{
    private readonly IConfiguration _configuration;

    public EmailService(IConfiguration configuration)
    {
        _configuration = configuration;
    }
}
```

### HttpContext
```csharp
public class UserService
{
    private readonly IHttpContextAccessor _httpContextAccessor;

    public UserService(IHttpContextAccessor httpContextAccessor)
    {
        _httpContextAccessor = httpContextAccessor;
    }
}
```

## Best Practices

### 1. Prefer Constructor Injection
- Rõ ràng về dependencies
- Compile-time safety
- Testability

### 2. Register Interface, not Implementation
```csharp
// Good
builder.Services.AddScoped<IRepository, Repository>();

// Avoid
builder.Services.AddScoped<Repository>();
```

### 3. Use appropriate lifetimes
- DbContext: Scoped
- Repository: Scoped
- Configuration: Singleton
- Temporary services: Transient

### 4. Avoid Service Locator
- Sử dụng constructor injection
- Dependencies rõ ràng

## Troubleshooting

### Common Errors
1. **Service not registered**: Kiểm tra registration trong Program.cs
2. **Circular dependency**: Refactor để tránh circular references
3. **Wrong lifetime**: Kiểm tra service lifetimes

### Debug DI Container
```csharp
var services = builder.Services.BuildServiceProvider();
var registrations = services.GetService<IServiceCollection>();
```

## Trong khóa học
- [[1-21. What is Dependency Injection]] - Giới thiệu DI
- [[2-27. Setup ApplicationDbContext]] - DI cho DbContext
- [[5-74. Replace DbContext with Category Repository]] - DI cho Repository

## Liên kết nội bộ
- [[Program.cs]] - Nơi đăng ký services
- [[ApplicationDbContext]] - Service được inject
- [[Repository Pattern]] - Pattern sử dụng DI
- [[Unit of Work Pattern]] - Pattern sử dụng DI
- [[ASP.NET Core MVC]] - Framework hỗ trợ DI
- [[Testing]] - DI trong unit testing
