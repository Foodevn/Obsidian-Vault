# appsettings.json

## Tổng quan
appsettings.json là file cấu hình chính trong ứng dụng ASP.NET Core, chứa các settings, connection strings và configuration values.

## Cấu trúc cơ bản

### Default Template
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

### Với Entity Framework
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=Bulky;Trusted_Connection=true;MultipleActiveResultSets=true"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft.AspNetCore": "Warning"
    }
  },
  "AllowedHosts": "*"
}
```

## Connection Strings

### SQL Server LocalDB
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=BulkyWeb;Trusted_Connection=true;TrustServerCertificate=true"
  }
}
```

### SQL Server Express
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=.\\SQLEXPRESS;Database=BulkyWeb;Trusted_Connection=true;TrustServerCertificate=true"
  }
}
```

### SQL Server with Authentication
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=BulkyWeb;User Id=sa;Password=YourPassword;TrustServerCertificate=true"
  }
}
```

## Application Settings

### Custom Configuration
```json
{
  "AppSettings": {
    "ApplicationName": "Bulky Web",
    "Version": "1.0.0",
    "MaxFileUploadSize": "5MB",
    "DefaultPageSize": 10
  }
}
```

### Email Configuration
```json
{
  "EmailSettings": {
    "SmtpServer": "smtp.gmail.com",
    "SmtpPort": 587,
    "SenderEmail": "noreply@bulkyweb.com",
    "SenderName": "Bulky Web",
    "UseSSL": true
  }
}
```

### Payment Gateway
```json
{
  "Stripe": {
    "PublishableKey": "pk_test_...",
    "SecretKey": "sk_test_...",
    "WebhookSecret": "whsec_..."
  }
}
```

## Logging Configuration

### Basic Logging
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information",
      "Microsoft": "Warning",
      "Microsoft.Hosting.Lifetime": "Information",
      "Microsoft.EntityFrameworkCore": "Information"
    }
  }
}
```

### File Logging
```json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information"
    },
    "File": {
      "Path": "Logs/app-{Date}.log",
      "MinLevel": "Information"
    }
  }
}
```

## Environment-specific Configuration

### appsettings.Development.json
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=(localdb)\\mssqllocaldb;Database=BulkyWeb_Dev;Trusted_Connection=true"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Debug",
      "Microsoft.EntityFrameworkCore": "Information"
    }
  }
}
```

### appsettings.Production.json
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "Server=prod-server;Database=BulkyWeb_Prod;User Id=appuser;Password=prod_password"
  },
  "Logging": {
    "LogLevel": {
      "Default": "Warning",
      "Microsoft": "Error"
    }
  }
}
```

## Đọc Configuration trong Code

### Trong Program.cs
```csharp
var connectionString = builder.Configuration.GetConnectionString("DefaultConnection");
var appName = builder.Configuration["AppSettings:ApplicationName"];
```

### Configuration Object
```csharp
public class AppSettings
{
    public string ApplicationName { get; set; }
    public string Version { get; set; }
    public int DefaultPageSize { get; set; }
}

// Registration
builder.Services.Configure<AppSettings>(builder.Configuration.GetSection("AppSettings"));
```

### Trong Controller
```csharp
public class HomeController : Controller
{
    private readonly IConfiguration _configuration;

    public HomeController(IConfiguration configuration)
    {
        _configuration = configuration;
    }

    public IActionResult Index()
    {
        var appName = _configuration["AppSettings:ApplicationName"];
        return View();
    }
}
```

### Với Options Pattern
```csharp
public class EmailService
{
    private readonly EmailSettings _emailSettings;

    public EmailService(IOptions<EmailSettings> emailSettings)
    {
        _emailSettings = emailSettings.Value;
    }
}
```

## Security Considerations

### User Secrets (Development)
```bash
dotnet user-secrets init
dotnet user-secrets set "ConnectionStrings:DefaultConnection" "your-connection-string"
dotnet user-secrets set "Stripe:SecretKey" "sk_test_your_secret_key"
```

### Environment Variables
```json
{
  "ConnectionStrings": {
    "DefaultConnection": "#{DB_CONNECTION_STRING}#"
  }
}
```

### Azure App Configuration
```csharp
builder.Configuration.AddAzureAppConfiguration(options =>
{
    options.Connect(builder.Configuration.GetConnectionString("AppConfig"))
           .UseFeatureFlags();
});
```

## Configuration Hierarchy

### Priority Order (Highest to Lowest)
1. Command-line arguments
2. Environment variables
3. User secrets (Development only)
4. appsettings.{Environment}.json
5. appsettings.json

### Override Example
```bash
# Environment variable overrides appsettings.json
set ConnectionStrings__DefaultConnection="Server=localhost;Database=Override;Trusted_Connection=true"
```

## Best Practices

### 1. Environment-specific Files
- appsettings.Development.json cho development
- appsettings.Production.json cho production
- appsettings.Staging.json cho staging

### 2. Sensitive Data
- Không commit secrets vào source control
- Sử dụng User Secrets cho development
- Sử dụng Environment Variables hoặc Key Vault cho production

### 3. Structured Configuration
```json
{
  "Database": {
    "ConnectionStrings": {
      "Main": "...",
      "ReadOnly": "..."
    },
    "CommandTimeout": 30
  },
  "Features": {
    "EnableCaching": true,
    "EnableLogging": true
  }
}
```

### 4. Validation
```csharp
public class DatabaseSettings
{
    [Required]
    public string ConnectionString { get; set; }
    
    [Range(1, 300)]
    public int CommandTimeout { get; set; } = 30;
}
```

## JSON Schema Validation

### Add Schema Reference
```json
{
  "$schema": "https://json.schemastore.org/appsettings.json",
  "ConnectionStrings": {
    "DefaultConnection": "..."
  }
}
```

## Troubleshooting

### Common Issues
1. **Configuration not found**: Kiểm tra file name và location
2. **Override not working**: Kiểm tra environment hierarchy
3. **Invalid JSON**: Validate JSON syntax

### Debug Configuration
```csharp
public void ConfigureServices(IServiceCollection services)
{
    var config = Configuration.AsEnumerable();
    foreach (var item in config)
    {
        Console.WriteLine($"{item.Key}: {item.Value}");
    }
}
```

## Trong khóa học
- [[1-15. wwwroot and appsettings]] - Giới thiệu appsettings.json
- [[2-25. Connection String]] - Cấu hình connection string
- [[Connection String]] - Chi tiết về connection string

## Liên kết nội bộ
- [[Connection String]] - Cấu hình database connection
- [[Program.cs]] - Nơi đọc configuration
- [[Entity Framework Core]] - Sử dụng connection string
- [[User Secrets]] - Bảo mật trong development
- [[Environment Variables]] - Production configuration
