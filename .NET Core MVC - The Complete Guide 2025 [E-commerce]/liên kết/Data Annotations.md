# Data Annotations

## Tổng quan
Data Annotations là các attribute trong .NET được sử dụng để cấu hình model validation và database mapping trong Entity Framework Core.

## Validation Annotations

### Required
```csharp
[Required(ErrorMessage = "The Name field is required.")]
public string Name { get; set; }
```

### StringLength
```csharp
[StringLength(50, MinimumLength = 3, ErrorMessage = "Name must be between 3 and 50 characters.")]
public string Name { get; set; }
```

### Range
```csharp
[Range(1, 100, ErrorMessage = "Display Order must be between 1-100")]
public int DisplayOrder { get; set; }
```

### RegularExpression
```csharp
[RegularExpression(@"^[a-zA-Z\s]*$", ErrorMessage = "Name can only contain letters and spaces.")]
public string Name { get; set; }
```

### Display
```csharp
[Display(Name = "Category Name")]
public string Name { get; set; }
```

## Database Mapping Annotations

### Key
```csharp
[Key]
public int CategoryId { get; set; }
```

### Column
```csharp
[Column("category_name", TypeName = "varchar(100)")]
public string Name { get; set; }
```

### Table
```csharp
[Table("Categories")]
public class Category
{
    // Properties
}
```

### ForeignKey
```csharp
[ForeignKey("CategoryId")]
public Category Category { get; set; }
```

### NotMapped
```csharp
[NotMapped]
public string FullName { get; set; }
```

## Custom Validation

### Ví dụ trong Category Model
```csharp
public class Category
{
    [Key]
    public int Id { get; set; }
    
    [Required]
    [StringLength(30)]
    [Display(Name = "Category Name")]
    public string Name { get; set; }
    
    [Display(Name = "Display Order")]
    [Range(1, 100, ErrorMessage = "Display Order must be between 1-100")]
    public int DisplayOrder { get; set; }
}
```

## Validation trong Views

### Validation Summary
```html
<div asp-validation-summary="All" class="text-danger"></div>
```

### Field Validation
```html
<span asp-validation-for="Name" class="text-danger"></span>
```

## Client-side Validation

### Scripts cần thiết
```html
@section Scripts {
    @{await Html.RenderPartialAsync("_ValidationScriptsPartial");}
}
```

## Custom Validation Attributes

### Tạo Custom Attribute
```csharp
public class CustomValidationAttribute : ValidationAttribute
{
    protected override ValidationResult IsValid(object value, ValidationContext validationContext)
    {
        // Custom validation logic
        return ValidationResult.Success;
    }
}
```

## Trong khóa học
- [[2-24. Data Annotations]] - Giới thiệu Data Annotations
- [[2-41. Server Side Validations]] - Validation phía server
- [[2-42. Custom Validations]] - Tạo validation tùy chỉnh
- [[2-44. Client Side Validation]] - Validation phía client

## Liên kết nội bộ
- [[Entity Framework Core]] - Framework chính
- [[ApplicationDbContext]] - Context sử dụng annotations
- [[Model Validation]] - Validation concepts
- [[ASP.NET Core MVC]] - Framework sử dụng validation
