# MVC Architecture

## Tổng quan
Model-View-Controller (MVC) là một architectural pattern tách biệt ứng dụng thành ba thành phần chính: Model, View, và Controller.

## Các thành phần MVC

### Model
**Định nghĩa**: Đại diện cho dữ liệu và business logic của ứng dụng

**Vai trò**:
- Chứa các class định nghĩa cấu trúc dữ liệu
- Xử lý business logic và data validation
- Tương tác với database thông qua Entity Framework

**Ví dụ**:
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
    [Range(1, 100)]
    public int DisplayOrder { get; set; }
}
```

### View
**Định nghĩa**: Đại diện cho presentation layer (giao diện người dùng)

**Vai trò**:
- Hiển thị dữ liệu từ Model
- Nhận input từ user
- Chứa HTML, CSS, JavaScript

**Ví dụ**:
```html
@model List<Category>

<h2>Categories</h2>
<table class="table">
    <thead>
        <tr>
            <th>Name</th>
            <th>Display Order</th>
        </tr>
    </thead>
    <tbody>
        @foreach (var category in Model)
        {
            <tr>
                <td>@category.Name</td>
                <td>@category.DisplayOrder</td>
            </tr>
        }
    </tbody>
</table>
```

### Controller
**Định nghĩa**: Điều phối giữa Model và View, xử lý user input

**Vai trò**:
- Nhận request từ user
- Tương tác với Model để lấy/xử lý dữ liệu
- Chọn View phù hợp để hiển thị
- Trả về response

**Ví dụ**:
```csharp
public class CategoryController : Controller
{
    private readonly IUnitOfWork _unitOfWork;

    public CategoryController(IUnitOfWork unitOfWork)
    {
        _unitOfWork = unitOfWork;
    }

    public IActionResult Index()
    {
        List<Category> objCategoryList = _unitOfWork.Category.GetAll().ToList();
        return View(objCategoryList);
    }

    public IActionResult Create()
    {
        return View();
    }

    [HttpPost]
    public IActionResult Create(Category obj)
    {
        if (ModelState.IsValid)
        {
            _unitOfWork.Category.Add(obj);
            _unitOfWork.Save();
            TempData["success"] = "Category created successfully";
            return RedirectToAction("Index");
        }
        return View();
    }
}
```

## Luồng hoạt động MVC

### Request Flow
1. **User Request**: Người dùng gửi HTTP request
2. **Routing**: ASP.NET Core routing xác định Controller và Action
3. **Controller**: Xử lý request, tương tác với Model
4. **Model**: Cung cấp/xử lý dữ liệu
5. **View**: Render HTML từ dữ liệu
6. **Response**: Trả về HTML cho browser

### Ví dụ Flow
```
URL: /Category/Index
↓
CategoryController.Index()
↓
_unitOfWork.Category.GetAll()
↓
Return View(categories)
↓
Views/Category/Index.cshtml
↓
HTML Response
```

## Routing trong MVC

### Convention-based Routing
```csharp
app.MapControllerRoute(
    name: "default",
    pattern: "{controller=Home}/{action=Index}/{id?}");
```

### Attribute Routing
```csharp
[Route("categories")]
public class CategoryController : Controller
{
    [Route("")]
    [Route("list")]
    public IActionResult Index() { }

    [Route("create")]
    public IActionResult Create() { }

    [Route("edit/{id:int}")]
    public IActionResult Edit(int id) { }
}
```

## Folder Structure

### Controllers
```
Controllers/
├── HomeController.cs
├── CategoryController.cs
└── ProductController.cs
```

### Models
```
Models/
├── Category.cs
├── Product.cs
└── ViewModels/
    ├── CategoryVM.cs
    └── ProductVM.cs
```

### Views
```
Views/
├── Home/
│   ├── Index.cshtml
│   └── Privacy.cshtml
├── Category/
│   ├── Index.cshtml
│   ├── Create.cshtml
│   └── Edit.cshtml
├── Shared/
│   ├── _Layout.cshtml
│   └── Error.cshtml
├── _ViewStart.cshtml
└── _ViewImports.cshtml
```

## Action Results

### ViewResult
```csharp
public IActionResult Index()
{
    return View(); // Returns ViewResult
}
```

### RedirectResult
```csharp
public IActionResult Create(Category category)
{
    // ...
    return RedirectToAction("Index"); // RedirectToActionResult
}
```

### JsonResult
```csharp
public IActionResult GetCategoriesJson()
{
    var categories = _unitOfWork.Category.GetAll();
    return Json(categories); // JsonResult
}
```

### PartialViewResult
```csharp
public IActionResult CategoryPartial()
{
    return PartialView("_CategoryList"); // PartialViewResult
}
```

## Model Binding

### Form Data
```csharp
[HttpPost]
public IActionResult Create(Category category)
{
    // category được bind từ form data
    return View(category);
}
```

### Query Parameters
```csharp
public IActionResult Index(int page = 1, int size = 10)
{
    // page và size từ query string
    return View();
}
```

### Route Parameters
```csharp
public IActionResult Details(int id)
{
    // id từ route parameter
    var category = _unitOfWork.Category.Get(c => c.Id == id);
    return View(category);
}
```

## Validation

### Model Validation
```csharp
[HttpPost]
public IActionResult Create(Category category)
{
    if (ModelState.IsValid)
    {
        _unitOfWork.Category.Add(category);
        _unitOfWork.Save();
        return RedirectToAction("Index");
    }
    return View(category); // Return with validation errors
}
```

### Custom Validation
```csharp
public IActionResult Create(Category category)
{
    if (category.Name == category.DisplayOrder.ToString())
    {
        ModelState.AddModelError("name", "The DisplayOrder cannot exactly match the Name.");
    }
    
    if (ModelState.IsValid)
    {
        // ...
    }
    return View(category);
}
```

## ViewData, ViewBag, TempData

### ViewData
```csharp
public IActionResult Index()
{
    ViewData["Title"] = "Category List";
    return View();
}
```

### ViewBag
```csharp
public IActionResult Index()
{
    ViewBag.Title = "Category List";
    return View();
}
```

### TempData
```csharp
public IActionResult Create(Category category)
{
    _unitOfWork.Category.Add(category);
    _unitOfWork.Save();
    TempData["success"] = "Category created successfully";
    return RedirectToAction("Index");
}
```

## Areas

### Area Structure
```
Areas/
└── Admin/
    ├── Controllers/
    │   └── CategoryController.cs
    └── Views/
        └── Category/
            └── Index.cshtml
```

### Area Controller
```csharp
[Area("Admin")]
public class CategoryController : Controller
{
    // Controller logic
}
```

### Area Routing
```csharp
app.MapControllerRoute(
    name: "areas",
    pattern: "{area:exists}/{controller=Home}/{action=Index}/{id?}");
```

## Best Practices

### 1. Single Responsibility
- Controller chỉ điều phối, không chứa business logic
- Model chứa data và validation logic
- View chỉ hiển thị, không chứa business logic

### 2. Dependency Injection
```csharp
public class CategoryController : Controller
{
    private readonly IUnitOfWork _unitOfWork;
    
    public CategoryController(IUnitOfWork unitOfWork)
    {
        _unitOfWork = unitOfWork;
    }
}
```

### 3. ViewModels
```csharp
public class CategoryCreateViewModel
{
    public string Name { get; set; }
    public int DisplayOrder { get; set; }
    public List<SelectListItem> ParentCategories { get; set; }
}
```

### 4. Action Naming
- GET actions: Index, Details, Create, Edit
- POST actions: Create, Edit, Delete
- Use verb prefixes for clarity

## Advantages of MVC

### Separation of Concerns
- Business logic tách biệt khỏi presentation
- Dễ maintain và test

### Testability
- Controller logic có thể unit test
- Mock dependencies dễ dàng

### Scalability
- Multiple developers có thể làm việc parallel
- Code organization tốt

### Reusability
- Models có thể reuse
- Views có thể share layouts

## Trong khóa học
- [[1-17. MVC Architecture]] - Giới thiệu MVC
- [[1-18. Routing Overview]] - Routing concepts
- [[1-19. Routing in Action]] - Routing trong thực tế

## Liên kết nội bộ
- [[Controller]] - Chi tiết về Controllers
- [[Model]] - Chi tiết về Models
- [[View]] - Chi tiết về Views
- [[Routing]] - URL routing
- [[Action Methods]] - Controller action methods
- [[Model Binding]] - Data binding
- [[Validation]] - Model validation
- [[Dependency Injection]] - DI trong MVC
