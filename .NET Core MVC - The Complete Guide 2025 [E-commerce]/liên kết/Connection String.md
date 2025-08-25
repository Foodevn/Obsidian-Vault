# Connection String

## Tổng quan
Connection String là chuỗi kết nối chứa thông tin cần thiết để ứng dụng kết nối đến cơ sở dữ liệu SQL Server.

## Cấu hình trong appsettings.json

### Cấu trúc cơ bản
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=Bulky;Trusted_Connection=true;MultipleActiveResultSets=true"
  }
}
```

### Với SQL Server
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=BulkyWeb;Trusted_Connection=true;TrustServerCertificate=true"
  }
}
```

### Với SQL Server Authentication
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=BulkyWeb;User Id=sa;Password=YourPassword;TrustServerCertificate=true"
  }
}
```

## Đăng ký trong Program.cs

### Basic Setup
```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

### Với Error Handling
```csharp
var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");
if (string.IsNullOrEmpty(connectionString))
{
    throw new InvalidOperationException("Connection string 'DefaultConnection' not found.");
}

builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(connectionString));
```

## Các thành phần Connection String

### Server
- `Server=localhost` - Local SQL Server
- `Server=(localdb)\\mssqllocaldb` - LocalDB
- `Server=.\\SQLEXPRESS` - SQL Express

### Database
- `Database=BulkyWeb` - Tên database
- `Initial Catalog=BulkyWeb` - Tương đương Database

### Authentication
- `Trusted_Connection=true` - Windows Authentication
- `User Id=sa;Password=password` - SQL Server Authentication
- `Integrated Security=true` - Windows Authentication (alternative)

### Additional Parameters
- `MultipleActiveResultSets=true` - Cho phép multiple result sets
- `TrustServerCertificate=true` - Trust SSL certificate
- `Connection Timeout=30` - Timeout kết nối

## Environment-specific Configuration

### Development
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=BulkyWeb_Dev;Trusted_Connection=true"
  }
}
```

### Production
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=prod-server;Database=BulkyWeb_Prod;User Id=appuser;Password=secure_password"
  }
}
```

## Security Best Practices

### User Secrets (Development)
```bash
dotnet user-secrets set "ConnectionStrings:DefaultConnection" "your-connection-string"
```

### Environment Variables
```csharp
var connectionString = Environment.GetEnvironmentVariable("CONNECTION_STRING") 
    ?? builder.Configuration.GetConnectionString("DefaultConnection");
```

### Azure App Configuration
- Sử dụng Azure Key Vault
- Configuration trong Azure App Service

## Troubleshooting

### Common Issues
1. **Database not found**: Kiểm tra tên database
2. **Authentication failed**: Kiểm tra credentials
3. **Server not found**: Kiểm tra server name
4. **SSL errors**: Thêm `TrustServerCertificate=true`

### Testing Connection
```csharp
public void TestConnection()
{
    using var connection = new SqlConnection(connectionString);
    try
    {
        connection.Open();
        Console.WriteLine("Connection successful!");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Connection failed: {ex.Message}");
    }
}
```

## Trong khóa học
- [[2-25. Connection String]] - Cấu hình connection string
- [[2-27. Setup ApplicationDbContext]] - Sử dụng connection string
- [[3-56. Setup EF Core]] - Setup trong Razor project

## Liên kết nội bộ
- [[Entity Framework Core]] - Framework sử dụng connection string
- [[ApplicationDbContext]] - Context sử dụng connection string
- [[appsettings.json]] - File cấu hình
- [[Program.cs]] - Đăng ký services
- [[SQL Server]] - Database engine
