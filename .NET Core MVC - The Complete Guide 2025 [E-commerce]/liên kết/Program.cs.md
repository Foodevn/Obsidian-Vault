# Program.cs

## Tổng quan
Program.cs là entry point của ứng dụng ASP.NET Core, nơi cấu hình services và pipeline của ứng dụng.

## Cấu trúc cơ bản

### Minimal API Template (.NET 6+)
```csharp
var builder = WebApplication.CreateBuilder(args);

// Add services to the container.
builder.Services.AddControllersWithViews();

var app = builder.Build();

// Configure the HTTP request pipeline.
if (!app.Environment.IsDevelopment())
{
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
}

app.UseHttpsRedirection();
app.UseStaticFiles();

app.UseRouting();

app.UseAuthorization();

app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");

app.Run();
```

## Cấu hình Entity Framework

### Đăng ký DbContext
```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));
```

### Với Repository Pattern
```csharp
builder.Services.AddDbContext<ApplicationDbContext>(options =>
    options.UseSqlServer(builder.Configuration.GetConnectionString("DefaultConnection")));

builder.Services.AddScoped<IUnitOfWork, UnitOfWork>();
```

## Dependency Injection

### Service Lifetimes
```csharp
// Transient - Tạo mới mỗi lần request
builder.Services.AddTransient<ITransientService, TransientService>();

// Scoped - Một instance per request
builder.Services.AddScoped<IScopedService, ScopedService>();

// Singleton - Một instance cho toàn ứng dụng
builder.Services.AddSingleton<ISingletonService, SingletonService>();
```

### Custom Services
```csharp
builder.Services.AddScoped<IEmailSender, EmailSender>();
builder.Services.AddScoped<IFileUpload, FileUpload>();
```

## Authentication & Authorization

### ASP.NET Identity
```csharp
builder.Services.AddDefaultIdentity<IdentityUser>(options => options.SignIn.RequireConfirmedAccount = true)
    .AddEntityFrameworkStores<ApplicationDbContext>();
```

### JWT Authentication
```csharp
builder.Services.AddAuthentication(JwtBearerDefaults.AuthenticationScheme)
    .AddJwtBearer(options =>
    {
        options.TokenValidationParameters = new TokenValidationParameters
        {
            ValidateIssuer = true,
            ValidateAudience = true,
            ValidateLifetime = true,
            ValidateIssuerSigningKey = true,
            ValidIssuer = builder.Configuration["Jwt:Issuer"],
            ValidAudience = builder.Configuration["Jwt:Audience"],
            IssuerSigningKey = new SymmetricSecurityKey(Encoding.UTF8.GetBytes(builder.Configuration["Jwt:Key"]))
        };
    });
```

## Configuration

### appsettings.json
```csharp
var configuration = builder.Configuration;
var connectionString = configuration.GetConnectionString("DefaultConnection");
var jwtKey = configuration["Jwt:Key"];
```

### Environment Variables
```csharp
var environment = builder.Environment;
if (environment.IsDevelopment())
{
    // Development specific configuration
}
```

## Middleware Pipeline

### Request Pipeline Order
```csharp
// Development environment
if (app.Environment.IsDevelopment())
{
    app.UseDeveloperExceptionPage();
}
else
{
    app.UseExceptionHandler("/Home/Error");
    app.UseHsts();
}

// Security
app.UseHttpsRedirection();

// Static files
app.UseStaticFiles();

// Routing
app.UseRouting();

// Authentication & Authorization
app.UseAuthentication();
app.UseAuthorization();

// Endpoints
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

### Custom Middleware
```csharp
app.UseMiddleware<CustomMiddleware>();

// hoặc inline
app.Use(async (context, next) =>
{
    // Do something before
    await next.Invoke();
    // Do something after
});
```

## Routing Configuration

### Default Route
```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

### Custom Routes
```csharp
app.MapControllerRoute(
    name: "category",
    pattern: "Category/{action=Index}/{id?}",
    defaults: new { controller = "Category" });
```

### Areas
```csharp
app.MapControllerRoute(
    name: "areas",
    pattern: "{area:exists}/{controller=Home}/{action=Index}/{id?}");
```

## Static Files & WWW Root

### Static Files
```csharp
app.UseStaticFiles();

// Custom static files
app.UseStaticFiles(new StaticFileOptions
{
    FileProvider = new PhysicalFileProvider(
        Path.Combine(builder.Environment.ContentRootPath, "CustomStaticFiles")),
    RequestPath = "/StaticFiles"
});
```

## Session Configuration

### Session Support
```csharp
builder.Services.AddDistributedMemoryCache();
builder.Services.AddSession(options =>
{
    options.IdleTimeout = TimeSpan.FromMinutes(100);
    options.Cookie.HttpOnly = true;
    options.Cookie.IsEssential = true;
});

// In pipeline
app.UseSession();
```

## Logging

### Configuration
```csharp
builder.Logging.ClearProviders();
builder.Logging.AddConsole();
builder.Logging.AddDebug();
```

### Custom Logging
```csharp
builder.Services.AddLogging(builder =>
{
    builder.AddConsole();
    builder.AddFile("Logs/app-{Date}.txt");
});
```

## CORS

### CORS Policy
```csharp
builder.Services.AddCors(options =>
{
    options.AddPolicy("AllowSpecificOrigin",
        policy =>
        {
            policy.WithOrigins("https://localhost:3000")
                  .AllowAnyHeader()
                  .AllowAnyMethod();
        });
});

// In pipeline
app.UseCors("AllowSpecificOrigin");
```

## Health Checks

### Basic Health Check
```csharp
builder.Services.AddHealthChecks();

app.MapHealthChecks("/health");
```

## So sánh .NET Framework vs .NET Core

### .NET Framework (Startup.cs)
```csharp
public class Startup
{
    public void ConfigureServices(IServiceCollection services)
    {
        // Configure services
    }

    public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
    {
        // Configure pipeline
    }
}
```

### .NET Core (Program.cs)
```csharp
var builder = WebApplication.CreateBuilder(args);
// Configure services
var app = builder.Build();
// Configure pipeline
app.Run();
```

## Trong khóa học
- [[1-16. Program File]] - Giới thiệu Program.cs
- [[2-27. Setup ApplicationDbContext]] - Cấu hình DbContext
- [[Dependency Injection]] - DI trong Program.cs

## Liên kết nội bộ
- [[ApplicationDbContext]] - DbContext configuration
- [[Connection String]] - Database connection
- [[Dependency Injection]] - DI container
- [[Routing]] - Route configuration
- [[Middleware]] - Request pipeline
- [[ASP.NET Identity]] - Authentication setup
