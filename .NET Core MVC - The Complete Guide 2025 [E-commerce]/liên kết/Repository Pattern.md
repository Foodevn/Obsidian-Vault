# Repository Pattern

## Tổng quan
Repository Pattern là một design pattern tách biệt logic truy cập dữ liệu khỏi business logic, tạo ra một lớp abstraction giữa application và data layer.

## Tại sao sử dụng Repository Pattern?

### Lợi ích
- **Separation of Concerns**: Tách biệt rõ ràng data access logic
- **Testability**: Dễ dàng mock repository cho unit testing
- **Maintainability**: Code dễ bảo trì và mở rộng
- **Flexibility**: Dễ dàng thay đổi data source

### Khi nào sử dụng
- Ứng dụng phức tạp với nhiều entities
- Cần test business logic mà không phụ thuộc database
- Muốn thay đổi ORM hoặc database dễ dàng

## Cấu trúc Repository Pattern

### Generic Repository Interface
```csharp
public interface IRepository<T> where T : class
{
    IEnumerable<T> GetAll();
    T Get(Expression<Func<T, bool>> filter);
    void Add(T entity);
    void Update(T entity);
    void Remove(T entity);
    void RemoveRange(IEnumerable<T> entities);
}
```

### Generic Repository Implementation
```csharp
public class Repository<T> : IRepository<T> where T : class
{
    private readonly ApplicationDbContext _db;
    internal DbSet<T> dbSet;

    public Repository(ApplicationDbContext db)
    {
        _db = db;
        this.dbSet = _db.Set<T>();
    }

    public void Add(T entity)
    {
        dbSet.Add(entity);
    }

    public T Get(Expression<Func<T, bool>> filter)
    {
        IQueryable<T> query = dbSet;
        query = query.Where(filter);
        return query.FirstOrDefault();
    }

    public IEnumerable<T> GetAll()
    {
        IQueryable<T> query = dbSet;
        return query.ToList();
    }

    public void Remove(T entity)
    {
        dbSet.Remove(entity);
    }

    public void RemoveRange(IEnumerable<T> entities)
    {
        dbSet.RemoveRange(entities);
    }

    public void Update(T entity)
    {
        dbSet.Update(entity);
    }
}
```

## Specific Repository

### ICategoryRepository
```csharp
public interface ICategoryRepository : IRepository<Category>
{
    void Update(Category obj);
}
```

### CategoryRepository Implementation
```csharp
public class CategoryRepository : Repository<Category>, ICategoryRepository
{
    private ApplicationDbContext _db;
    
    public CategoryRepository(ApplicationDbContext db) : base(db)
    {
        _db = db;
    }

    public void Update(Category obj)
    {
        _db.Categories.Update(obj);
    }
}
```

## Unit of Work Pattern

### Interface
```csharp
public interface IUnitOfWork
{
    ICategoryRepository Category { get; }
    void Save();
}
```

### Implementation
```csharp
public class UnitOfWork : IUnitOfWork
{
    private ApplicationDbContext _db;
    public ICategoryRepository Category { get; private set; }

    public UnitOfWork(ApplicationDbContext db)
    {
        _db = db;
        Category = new CategoryRepository(_db);
    }

    public void Save()
    {
        _db.SaveChanges();
    }
}
```

## Dependency Injection

### Registration trong Program.cs
```csharp
builder.Services.AddScoped<IUnitOfWork, UnitOfWork>();
```

### Sử dụng trong Controller
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
}
```

## So sánh với Direct DbContext

### Trước khi dùng Repository
```csharp
public class CategoryController : Controller
{
    private readonly ApplicationDbContext _db;

    public CategoryController(ApplicationDbContext db)
    {
        _db = db;
    }

    public IActionResult Index()
    {
        List<Category> objCategoryList = _db.Categories.ToList();
        return View(objCategoryList);
    }
}
```

### Sau khi dùng Repository
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
}
```

## Advanced Features

### Include Navigation Properties
```csharp
public IEnumerable<T> GetAll(Expression<Func<T, bool>>? filter = null, string? includeProperties = null)
{
    IQueryable<T> query = dbSet;
    
    if (filter != null)
    {
        query = query.Where(filter);
    }
    
    if (!string.IsNullOrEmpty(includeProperties))
    {
        foreach (var includeProp in includeProperties.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries))
        {
            query = query.Include(includeProp);
        }
    }
    
    return query.ToList();
}
```

## Trong khóa học
- [[5-70. IRepository Interface]] - Tạo interface repository
- [[5-71. Implement Repository Interface]] - Implementation repository
- [[5-72. Implement ICategoryRepository]] - Category repository interface
- [[5-73. Implement Category Repository]] - Category repository implementation
- [[5-74. Replace DbContext with Category Repository]] - Thay thế DbContext

## Liên kết nội bộ
- [[Entity Framework Core]] - ORM được abstract bởi repository
- [[Unit of Work Pattern]] - Pattern bổ sung cho repository
- [[ApplicationDbContext]] - DbContext được wrap bởi repository
- [[IRepository Interface]] - Generic repository interface
- [[CategoryRepository]] - Specific repository implementation
- [[Dependency Injection]] - DI pattern cho repository
