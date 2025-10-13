# Factory Method – Giải thích dễ hiểu

**Factory Method** là một mẫu thiết kế khởi tạo (Creational Pattern) giúp tách biệt việc **_yêu cầu_** tạo một đối tượng khỏi việc **_xác định_** chính xác lớp nào sẽ được khởi tạo. Thay vì gọi trực tiếp `new ConcreteClass(...)`, bạn gọi một phương thức “nhà máy” (factory) để nhận về một đối tượng qua interface hoặc lớp cha chung.

## Tại sao cần Factory Method?

1. **Giảm phụ thuộc**
    - Client chỉ biết đến interface hoặc lớp cha, không cần biết chi tiết lớp con cụ thể.
    - Khi muốn thêm loại đối tượng mới, chỉ cần tạo lớp con và ghi đè phương thức factory, không phải sửa code client.
2. **Dễ mở rộng**
    - Thêm loại sản phẩm mới mà không ảnh hưởng đến mã đã có.
    - Tuân theo Open/Closed Principle: mở để mở rộng, đóng để sửa đổi.
3. **Quản lý phức tạp**
    - Khi logic tạo đối tượng phức tạp (cấu hình, khởi tạo nhiều tham số…), có thể gom hết vào factory để client gọi cho gọn.

## Cách hoạt động

1. **Định nghĩa interface hoặc lớp trừu tượng** `IProduct`
2. **Khai báo lớp con** `ConcreteProductA`, `ConcreteProductB` cài đặt `IProduct`
3. **Tạo lớp factory** với phương thức trừu tượng hoặc ảo, ví dụ `CreateProduct(string type)`
4. **Lớp con factory** ghi đè `CreateProduct(...)` để trả về `new ConcreteProductA()` hoặc `new ConcreteProductB()` dựa trên tham số



```csharp
// 1. Interface chung cho sản phẩm
public interface IProduct
{
    void DoWork();
}

// 2. Lớp cụ thể
public class ConcreteProductA : IProduct
{
    public void DoWork() => Console.WriteLine("Product A is working.");
}

public class ConcreteProductB : IProduct
{
    public void DoWork() => Console.WriteLine("Product B is working.");
}

// 3. Lớp Factory với phương thức ảo
public abstract class Creator
{
    // Factory Method
    public abstract IProduct CreateProduct(string type);

    // Phương thức sử dụng sản phẩm
    public void SomeOperation(string type)
    {
        var product = CreateProduct(type);
        product.DoWork();
    }
}

// 4. Lớp con ghi đè Factory Method
public class ConcreteCreator : Creator
{
    public override IProduct CreateProduct(string type)
    {
        // Sử dụng switch-case hoặc if-else để quyết định đối tượng cụ thể
        if (type == "A")
            return new ConcreteProductA();
        else if (type == "B")
            return new ConcreteProductB();
        else
            throw new ArgumentException("Unknown product type");
    }
}

// 5. Client gọi
class Program
{
    static void Main()
    {
        Creator creator = new ConcreteCreator();
        creator.SomeOperation("A");  // In ra: Product A is working.
        creator.SomeOperation("B");  // In ra: Product B is working.
    }
}
```

## Minh họa qua ví dụ đời thật

- **Nhà máy xe hơi**:
    - Bạn chỉ cần nói “hãy sản xuất một chiếc xe loại SUV” hoặc “sedan”, mà không cần biết nhà máy dùng loại động cơ nào, khung gầm gì.
    - Factory Method ở đây chính là bộ phận “dây chuyền” chịu trách nhiệm đọc lệnh và chọn linh kiện phù hợp để lắp ráp kiểu xe tương ứng.

## Tổng kết
- Caller chỉ cần tương tác qua **Creator** và **IProduct**, không biết class cụ thể.
- Logic quyết định tạo A hay B nằm gọn trong `CreateProduct`.
- Muốn thêm `ConcreteProductC`, chỉ cần viết thêm class và mở rộng `CreateProduct`, không tác động vào code client.

Nhờ đó, **Factory Method** giúp mã dễ mở rộng, bảo trì và tuân theo nguyên tắc SOLID một cách rõ ràng.