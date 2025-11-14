# Kịch Bản PowerPoint: Dự Án Obstacle Dodge
## Unity 3D Game Development - Section 2

---

## SLIDE 1: Trang Bìa
**Tiêu đề chính:** DỰ ÁN OBSTACLE DODGE
**Phụ đề:** Unity 3D Game Development with C#
**Thông tin:** Complete C# Unity Game Development Course
**Hình ảnh đề xuất:** Logo Unity + hình ảnh game Obstacle Dodge

**Nội dung thuyết trình:**
- Xin chào mọi người! Hôm nay tôi xin báo cáo về dự án Obstacle Dodge - một dự án game cơ bản nhưng rất quan trọng trong việc học Unity và lập trình C#.

---

## SLIDE 2: Tổng Quan Dự Án
**Tiêu đề:** TỔNG QUAN DỰ ÁN OBSTACLE DODGE

**Nội dung Slide:**
- **Loại game:** Trò chơi tránh chướng ngại vật (Avoidance Game)
- **Mục tiêu:** Học các khái niệm cơ bản Unity & C#
- **Yếu tố chính:**
  - Người chơi di chuyển 4 hướng
  - Camera theo dõi với Cinemachine
  - Chướng ngại vật đa dạng (đạn, vật xoay, vật rơi)
  - Hệ thống điểm số
- **Trải nghiệm:** Tạo cảm giác gấp gáp, hồi hộp

**Nội dung thuyết trình:**
- Obstacle Dodge là một game tránh chướng ngại vật đơn giản nhưng đầy thử thách
- Người chơi phải di chuyển từ điểm A đến điểm B, tránh các chướng ngại vật như đạn bay, vật thể xoay và vật rơi
- Mục tiêu chính là tạo cảm giác hoảng loạn và gấp gáp cho người chơi
- Qua dự án này, chúng ta sẽ học được rất nhiều khái niệm quan trọng

---

## SLIDE 3: Kiến Thức C# Học Được
**Tiêu đề:** KỸ NĂNG LẬP TRÌNH C# ĐẠT ĐƯỢC

**Nội dung Slide:**
**1. Kiến thức cơ bản:**
- ✓ Variables (Biến) - lưu trữ và quản lý dữ liệu
- ✓ Methods (Phương thức) - tạo hàm thực thi hành động
- ✓ If Statements - câu lệnh điều kiện
- ✓ Start() & Update() - vòng đời script Unity

**2. Kiến thức nâng cao:**
- ✓ Collisions - xử lý va chạm
- ✓ Trigger Volumes - phát hiện vùng kích hoạt
- ✓ Player Input - xử lý input người chơi
- ✓ GetComponent() - truy cập component

**Nội dung thuyết trình:**
- Qua dự án này, chúng ta đã làm quen với các khái niệm C# cơ bản nhất
- Từ biến, phương thức cho đến các câu lệnh điều kiện
- Và cũng học được cách xử lý va chạm, input người chơi - những kỹ năng quan trọng trong game development

---

## SLIDE 4: Kiến Thức Unity Học Được
**Tiêu đề:** KỸ NĂNG UNITY ENGINE ĐẠT ĐƯỢC

**Nội dung Slide:**
**Unity Fundamentals:**
- 🎮 Game Objects - tạo và quản lý đối tượng
- 📦 Prefabs - tái sử dụng objects
- 🎥 Cinemachine - quản lý camera động
- 🏷️ Tags - phân loại objects
- 🔧 Components - xây dựng chức năng
- ⚡ Order of Execution - hiểu vòng đời script

**Công cụ & Workflow:**
- Inspector, Hierarchy, Scene View
- SerializeField - điều chỉnh trực tiếp
- Time.deltaTime - chuẩn hóa frame rate

**Nội dung thuyết trình:**
- Về phía Unity, chúng ta đã học cách làm việc với Game Objects và Components
- Hiểu về Prefabs - một tính năng cực kỳ mạnh mẽ để tái sử dụng
- Sử dụng Cinemachine cho camera chuyên nghiệp
- Và làm quen với workflow cơ bản của Unity Editor

---

## SLIDE 5: Bài 1-2 - Thiết Lập Dự Án & Start/Update
**Tiêu đề:** THIẾT LẬP DỰ ÁN & VÒNG ĐỜI SCRIPT

**Nội dung Slide:**
**Thiết lập ban đầu:**
- Tạo dự án Universal 3D Pipeline
- Thêm Ground (Plane) và Player (Cube)
- Tạo Materials cho đối tượng
- Tổ chức thư mục Scripts, Materials

**Start() vs Update():**
```csharp
void Start() 
{
    // Chạy 1 lần khi bắt đầu
    transform.Translate(1f, 0f, 0f);
}

void Update() 
{
    // Chạy mỗi frame
    transform.Translate(0.01f, 0f, 0f);
}
```

**Kết quả:** Nhân vật di chuyển liên tục

**Nội dung thuyết trình:**
- Bước đầu tiên là thiết lập dự án với Universal 3D Pipeline - phù hợp cho prototype
- Chúng ta tạo một mặt phẳng làm mặt đất và một cube làm nhân vật
- Điểm quan trọng đầu tiên là hiểu sự khác biệt giữa Start() và Update()
- Start() chỉ chạy một lần khi bắt đầu, còn Update() chạy mỗi frame
- Đây là nền tảng để tạo chuyển động liên tục trong game

---

## SLIDE 6: Bài 3-4 - Variables & SerializeField
**Tiêu đề:** BIẾN VÀ SERIALIZATION

**Nội dung Slide:**
**Variables (Biến):**
```csharp
float xValue = 0.01f;  // Số thập phân
int score = 0;         // Số nguyên
bool isAlive = true;   // True/False
string name = "Dodgy"; // Chuỗi ký tự
```

**SerializeField - Hiển thị trong Inspector:**
```csharp
[SerializeField] float xValue = 0f;
[SerializeField] float yValue = 0.05f;
[SerializeField] float zValue = 0f;
```

**Lợi ích:**
- ✅ Dễ dàng thay đổi giá trị
- ✅ Thử nghiệm nhanh trong Play Mode
- ✅ Không cần sửa code

**Nội dung thuyết trình:**
- Biến là khái niệm cơ bản nhất trong lập trình - giống như một chiếc hộp chứa dữ liệu
- Có 4 loại biến phổ biến: float, int, bool và string
- SerializeField là một tính năng tuyệt vời của Unity
- Nó cho phép chúng ta hiển thị biến trong Inspector và điều chỉnh trực tiếp
- Điều này giúp tiết kiệm rất nhiều thời gian khi thử nghiệm

---

## SLIDE 7: Bài 5 - C# Formatting
**Tiêu đề:** NGUYÊN TẮC ĐỊNH DẠNG CODE

**Nội dung Slide:**
**1. Comments (Bình luận):**
```csharp
// Đây là bình luận một dòng
// Unity sẽ bỏ qua dòng này
```

**2. White Space (Khoảng trắng):**
- Không ảnh hưởng code
- Dùng để tăng tính dễ đọc

**3. Curly Braces (Dấu ngoặc nhọn):**
```csharp
void Update()
{
    // Code block - phạm vi của hàm
    transform.Translate(x, y, z);
}
```

**4. Variable Scope (Phạm vi biến):**
- Biến khai báo ngoài hàm: toàn cục trong class
- Biến khai báo trong hàm: chỉ tồn tại trong hàm đó

**Nội dung thuyết trình:**
- Định dạng code đúng cách rất quan trọng, đặc biệt khi làm việc nhóm
- Comments giúp giải thích code cho người khác hoặc cho chính mình sau này
- Dấu ngoặc nhọn xác định phạm vi của code block
- Và quan trọng là hiểu scope của biến - biến nào có thể truy cập ở đâu

---

## SLIDE 8: Bài 6-7 - Input & Time.deltaTime
**Tiêu đề:** XỬ LÝ INPUT VÀ CHUẨN HÓA TỐC ĐỘ

**Nội dung Slide:**
**Input System:**
```csharp
float x = Input.GetAxis("Horizontal"); // -1 đến 1
float z = Input.GetAxis("Vertical");   // -1 đến 1
```
- Horizontal: A/D hoặc mũi tên trái/phải
- Vertical: W/S hoặc mũi tên lên/xuống

**Time.deltaTime - Giải quyết vấn đề FPS:**
```csharp
[SerializeField] float moveSpeed = 10f;

void Update() 
{
    float x = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed;
    float z = Input.GetAxis("Vertical") * Time.deltaTime * moveSpeed;
    transform.Translate(x, 0, z);
}
```

**Kết quả:** Tốc độ đồng nhất trên mọi máy tính

**Nội dung thuyết trình:**
- Input.GetAxis cho phép chúng ta đọc input từ bàn phím
- Giá trị trả về từ -1 đến 1, rất tiện cho việc di chuyển mượt mà
- Vấn đề là trên máy nhanh, game chạy nhiều frame hơn nên nhân vật di chuyển nhanh hơn
- Time.deltaTime giải quyết vấn đề này bằng cách chuẩn hóa theo thời gian thực
- Kết hợp với biến moveSpeed, chúng ta có thể điều chỉnh tốc độ dễ dàng

---

## SLIDE 9: Bài 8 - Cinemachine
**Tiêu đề:** CAMERA THEO DÕI VỚI CINEMACHINE

**Nội dung Slide:**
**Cinemachine là gì?**
- 🎥 Gói công cụ camera mạnh mẽ của Unity
- 🆓 Miễn phí, cài qua Package Manager
- 🎬 Quản lý nhiều camera không cần code

**Thành phần chính:**
- **Cinemachine Brain:** Gắn vào Main Camera
- **Virtual Camera:** Camera ảo cung cấp góc nhìn

**Cấu hình Virtual Camera:**
- Tracking Target: Chọn Player
- Follow Mode: Theo dõi vị trí
- Follow Offset: Điều chỉnh khoảng cách (X, Y, Z)
- Position Damping: Độ trễ mượt mà (0-17)
- Hard Look At: Camera luôn nhìn về Player

**Nội dung thuyết trình:**
- Cinemachine là một công cụ tuyệt vời để quản lý camera
- Thay vì phải viết code phức tạp, chúng ta chỉ cần cấu hình trong Inspector
- Virtual Camera tự động theo dõi nhân vật
- Có thể điều chỉnh khoảng cách, góc nhìn và độ trễ để tạo cảm giác mượt mà
- Đây là công cụ được sử dụng trong nhiều game chuyên nghiệp

---

## SLIDE 10: Bài 9 - Collisions
**Tiêu đề:** HỆ THỐNG VA CHẠM (COLLISIONS)

**Nội dung Slide:**
**Tạo khu vực chơi:**
- Thêm tường (Walls) bao quanh
- Thêm vật cản (Obstacles)
- Tổ chức trong GameObject "Environment"

**Components cần thiết:**
**1. Collider:**
- Box Collider, Sphere Collider, etc.
- Xác định vùng va chạm
- Hiển thị dưới dạng đường viền xanh

**2. Rigidbody:**
```csharp
// Cấu hình trong Inspector:
Use Gravity: ❌ Tắt
Freeze Rotation: ✅ X, Y, Z
Freeze Position: ✅ Y
```

**Trigger vs Collision:**
- Collision: Ngăn chặn vật đi qua
- Trigger: Phát hiện nhưng không ngăn (Is Trigger = true)

**Nội dung thuyết trình:**
- Để tạo game thực sự, chúng ta cần hệ thống va chạm
- Collider xác định vùng va chạm của đối tượng
- Rigidbody thêm tính vật lý, nhưng cần cấu hình đúng
- Tắt trọng lực và đóng băng rotation để tránh hành vi không mong muốn
- Có thể dùng Trigger để phát hiện va chạm mà không ngăn chặn

---

## SLIDE 11: Bài 10-11 - Methods
**Tiêu đề:** HIỂU VÀ SỬ DỤNG METHODS (PHƯƠNG THỨC)

**Nội dung Slide:**
**Methods là gì?**
- Khối code có thể tái sử dụng
- Thực hiện một công việc cụ thể
- Giúp tổ chức code tốt hơn

**Cú pháp cơ bản:**
```csharp
void MethodName()
{
    // Code thực thi
}
```

**Ví dụ thực tế:**
```csharp
void PrintWelcome()
{
    Debug.Log("Welcome to Unity!");
}

void MovePlayer()
{
    float x = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed;
    transform.Translate(x, 0, 0);
}

void Update()
{
    MovePlayer(); // Gọi method
}
```

**Lợi ích:**
- ✅ Code sạch hơn, dễ đọc
- ✅ Tái sử dụng nhiều lần
- ✅ Dễ bảo trì và debug

**Nội dung thuyết trình:**
- Methods hay phương thức là cách chúng ta tổ chức code
- Thay vì viết tất cả trong Update(), ta chia thành các methods nhỏ
- Mỗi method thực hiện một nhiệm vụ cụ thể
- Điều này làm code dễ đọc, dễ bảo trì và có thể tái sử dụng
- Đây là nguyên tắc quan trọng trong lập trình

---

## SLIDE 12: Bài 12-13 - OnCollisionEnter & GetComponent
**Tiêu đề:** XỬ LÝ VA CHẠM VÀ TRUY CẬP COMPONENT

**Nội dung Slide:**
**OnCollisionEnter() - Phát hiện va chạm:**
```csharp
void OnCollisionEnter(Collision collision)
{
    Debug.Log("Đã va chạm với: " + collision.gameObject.name);
}
```

**GetComponent() - Truy cập Component:**
```csharp
// Thay đổi màu khi va chạm
MeshRenderer renderer = GetComponent<MeshRenderer>();
renderer.material.color = Color.red;
```

**Ví dụ đầy đủ:**
```csharp
void OnCollisionEnter(Collision collision)
{
    MeshRenderer renderer = GetComponent<MeshRenderer>();
    renderer.material.color = Color.red;
    Debug.Log("Player đã va chạm!");
}
```

**Ứng dụng:**
- Phát hiện va chạm với chướng ngại vật
- Thay đổi màu sắc khi va chạm
- Tăng điểm số
- Kích hoạt hiệu ứng

**Nội dung thuyết trình:**
- OnCollisionEnter là một method đặc biệt của Unity
- Nó tự động được gọi khi có va chạm xảy ra
- GetComponent cho phép chúng ta truy cập các component khác
- Ví dụ như MeshRenderer để thay đổi màu sắc
- Đây là nền tảng để tạo các tương tác trong game

---

## SLIDE 13: Bài 14-15 - Score System & Time
**Tiêu đề:** HỆ THỐNG ĐIỂM VÀ THỜI GIAN

**Nội dung Slide:**
**Tăng điểm số (Incrementing Score):**
```csharp
int score = 0;

void OnCollisionEnter(Collision collision)
{
    score++;  // Hoặc score = score + 1;
    Debug.Log("Score: " + score);
}
```

**Time.time - Đếm thời gian:**
```csharp
void Start()
{
    float startTime = Time.time;
}

void Update()
{
    float currentTime = Time.time - startTime;
    Debug.Log("Thời gian: " + currentTime + " giây");
}
```

**Ứng dụng thực tế:**
- ⏱️ Đếm thời gian chơi
- 🎯 Ghi nhận điểm cao
- ⏰ Tạo cooldown cho skill
- 📊 Hiển thị thống kê

**Nội dung thuyết trình:**
- Hệ thống điểm số là yếu tố quan trọng trong game
- Chúng ta dùng toán tử ++ để tăng điểm mỗi khi va chạm
- Time.time cho biết thời gian từ khi game bắt đầu
- Có thể dùng để tính thời gian chơi, tạo cooldown
- Hoặc thêm các yếu tố thời gian vào gameplay

---

## SLIDE 14: Bài 16-17 - If Statements & Caching
**Tiêu đề:** CÂU LỆNH ĐIỀU KIỆN VÀ TỐI ƯU HÓA

**Nội dung Slide:**
**If Statements - Câu lệnh điều kiện:**
```csharp
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.tag == "Obstacle")
    {
        Debug.Log("Chạm vật cản!");
    }
    else if (collision.gameObject.tag == "Pickup")
    {
        Debug.Log("Nhặt được vật phẩm!");
        score++;
    }
}
```

**Caching Reference - Lưu tham chiếu:**
```csharp
// ❌ Không tốt - Gọi GetComponent mỗi frame
void Update()
{
    GetComponent<MeshRenderer>().material.color = Color.red;
}

// ✅ Tốt hơn - Lưu vào biến
MeshRenderer meshRenderer;
void Start()
{
    meshRenderer = GetComponent<MeshRenderer>();
}
void Update()
{
    meshRenderer.material.color = Color.red;
}
```

**Nội dung thuyết trình:**
- If statements cho phép code ra quyết định
- Kiểm tra điều kiện và thực hiện hành động tương ứng
- Caching reference là kỹ thuật tối ưu quan trọng
- Thay vì gọi GetComponent nhiều lần, ta lưu vào biến một lần
- Điều này tăng hiệu suất đáng kể

---

## SLIDE 15: Bài 18 - Tags
**Tiêu đề:** SỬ DỤNG TAGS ĐỂ PHÂN LOẠI ĐỐI TƯỢNG

**Nội dung Slide:**
**Tags là gì?**
- Nhãn để phân loại Game Objects
- Giúp nhận diện đối tượng dễ dàng
- Unity có sẵn một số tags (Player, MainCamera, etc.)

**Tạo và sử dụng Tags:**
```csharp
// Tạo tag mới:
// Inspector → Tag → Add Tag → "Obstacle"

// Gán tag cho object:
// Chọn object → Inspector → Tag → Chọn "Obstacle"

// Sử dụng trong code:
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.tag == "Obstacle")
    {
        Debug.Log("Va chạm với vật cản!");
    }
}
```

**Lợi ích:**
- 🏷️ Phân loại đối tượng rõ ràng
- 🎯 Dễ dàng xử lý riêng từng loại
- 🔍 Tìm kiếm objects theo tag

**Nội dung thuyết trình:**
- Tags là cách đơn giản để phân loại các đối tượng
- Thay vì kiểm tra tên, ta dùng tag để nhận biết
- Có thể tạo tags tùy chỉnh cho dự án
- Rất hữu ích khi có nhiều loại đối tượng khác nhau
- Ví dụ: Obstacle, Enemy, Pickup, Wall...

---

## SLIDE 16: Bài 19-21 - Advanced Features
**Tiêu đề:** TÍNH NĂNG NÂNG CAO

**Nội dung Slide:**
**1. Rotate Object (Xoay đối tượng):**
```csharp
[SerializeField] float rotateSpeed = 100f;

void Update()
{
    transform.Rotate(0, rotateSpeed * Time.deltaTime, 0);
}
```

**2. Fly At Player (Bay về phía Player):**
```csharp
[SerializeField] GameObject player;
[SerializeField] float speed = 5f;

void Update()
{
    Vector3 direction = player.transform.position - transform.position;
    transform.Translate(direction.normalized * speed * Time.deltaTime);
}
```

**3. Destroy Object (Hủy đối tượng):**
```csharp
void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.tag == "Player")
    {
        Destroy(gameObject); // Hủy chính object này
        // Hoặc: Destroy(collision.gameObject); // Hủy object va chạm
    }
}
```

**Nội dung thuyết trình:**
- Ba tính năng này tạo nên gameplay động
- Xoay đối tượng tạo chướng ngại vật thú vị
- Bay về phía Player tạo áp lực cho người chơi
- Destroy cho phép xóa đối tượng khi cần thiết
- Kết hợp cả ba tạo nên trải nghiệm game phong phú

---

## SLIDE 17: Bài 22 - Trigger Volumes
**Tiêu đề:** VÙNG KÍCH HOẠT (TRIGGER VOLUMES)

**Nội dung Slide:**
**Trigger là gì?**
- Vùng không gian vô hình
- Phát hiện khi đối tượng đi vào/ra
- Không ngăn chặn chuyển động

**Thiết lập Trigger:**
```
1. Tạo Cube/Sphere làm trigger zone
2. Bật "Is Trigger" trong Collider
3. Có thể tắt Mesh Renderer để làm vô hình
```

**Sử dụng trong Code:**
```csharp
void OnTriggerEnter(Collider other)
{
    Debug.Log("Đối tượng đi vào trigger!");
    if (other.tag == "Player")
    {
        // Bắn đạn về phía player
        FireProjectile();
    }
}

void OnTriggerExit(Collider other)
{
    Debug.Log("Đối tượng rời khỏi trigger!");
}
```

**Ứng dụng:**
- 🎯 Kích hoạt bẫy
- 🚀 Bắn đạn khi player gần
- 🚪 Mở cửa tự động
- 📍 Checkpoint trong game

**Nội dung thuyết trình:**
- Trigger volumes rất khác với collision thông thường
- Chúng không ngăn chặn mà chỉ phát hiện
- Rất hữu ích để tạo các vùng kích hoạt vô hình
- Ví dụ: khi player bước vào, kích hoạt bẫy hoặc bắn đạn
- OnTriggerEnter và OnTriggerExit giúp xử lý logic

---

## SLIDE 18: Bài 23 - Prefabs
**Tiêu đề:** PREFABS - TÁI SỬ DỤNG ĐỐI TƯỢNG

**Nội dung Slide:**
**Prefab là gì?**
- 📦 Tài sản tái sử dụng (Reusable Asset)
- 💾 Lưu dưới dạng file .prefab
- 🔄 Tạo nhiều instance từ 1 prefab

**Workflow với Prefab:**
```
1. Tạo Prefab:
   - Kéo GameObject từ Hierarchy vào Project folder

2. Tạo Instance:
   - Kéo Prefab từ Project vào Scene

3. Chỉnh sửa Prefab:
   - Double-click vào Prefab (Isolation Mode)
   - Thay đổi áp dụng cho tất cả instances

4. Override Instance:
   - Sửa riêng 1 instance
   - Apply All / Revert trong Inspector
```

**Lợi ích:**
- ✅ Dễ dàng tạo nhiều đối tượng giống nhau
- ✅ Cập nhật hàng loạt chỉ với 1 thay đổi
- ✅ Giữ consistency trong dự án
- ✅ Tiết kiệm thời gian development

**Nội dung thuyết trình:**
- Prefabs là một trong những tính năng mạnh nhất của Unity
- Cho phép chúng ta tạo template và tái sử dụng nhiều lần
- Khi sửa prefab gốc, tất cả instances đều được cập nhật
- Có thể override riêng từng instance nếu cần
- Rất quan trọng cho các dự án lớn với nhiều đối tượng lặp lại

---

## SLIDE 19: Bài 24 - Unity Order of Execution
**Tiêu đề:** THỨ TỰ THỰC THI TRONG UNITY

**Nội dung Slide:**
**Vòng đời của MonoBehaviour:**

```
🔄 VÒNG ĐỜI SCRIPT UNITY:

1. Awake()           ← Chạy đầu tiên, trước Start()
2. OnEnable()        ← Khi object được kích hoạt
3. Start()           ← Chạy 1 lần, trước frame đầu tiên
4. FixedUpdate()     ← Chạy với tần suất cố định (physics)
5. Update()          ← Chạy mỗi frame
6. LateUpdate()      ← Chạy sau Update()
7. OnDisable()       ← Khi object bị vô hiệu hóa
8. OnDestroy()       ← Khi object bị hủy
```

**Khi nào dùng gì?**
- **Awake()**: Khởi tạo tham chiếu
- **Start()**: Thiết lập ban đầu
- **Update()**: Logic game, input
- **FixedUpdate()**: Physics, Rigidbody
- **LateUpdate()**: Camera follow
- **OnCollisionEnter()**: Va chạm
- **OnTriggerEnter()**: Trigger

**Nội dung thuyết trình:**
- Hiểu thứ tự thực thi rất quan trọng để tránh lỗi
- Awake chạy trước Start, thích hợp cho khởi tạo tham chiếu
- Update chạy mỗi frame, dùng cho logic thường xuyên
- FixedUpdate dùng cho physics, chạy với tần suất cố định
- LateUpdate dùng cho camera để đảm bảo chạy sau khi player đã di chuyển

---

## SLIDE 20: Bài 25-26 - Level Design
**Tiêu đề:** THIẾT KẾ CẤP ĐỘ (LEVEL LAYOUT)

**Nội dung Slide:**
**Nguyên tắc thiết kế Level:**
**1. Khu vực chơi:**
- 🗺️ Xác định rõ ranh giới
- 🏁 Điểm bắt đầu và kết thúc
- 🛣️ Con đường chính rõ ràng

**2. Bố trí chướng ngại vật:**
- 📈 Độ khó tăng dần
- ⚖️ Cân bằng thử thách
- 🎯 Tạo nhiều lựa chọn đường đi

**3. Tổ chức Hierarchy:**
```
Scene
├── Player
├── Main Camera
├── CM vcam1
├── Environment
│   ├── Ground
│   ├── Walls (Group)
│   └── Obstacles (Group)
├── Hazards
│   ├── Spinning Objects
│   ├── Dropping Objects
│   └── Projectile Launchers
└── Lighting
```

**4. Sử dụng Prefabs:**
- Walls, Obstacles, Hazards là prefabs
- Dễ dàng nhân bản và điều chỉnh
- Consistency trong thiết kế

**Nội dung thuyết trình:**
- Thiết kế level cần có cấu trúc rõ ràng
- Tổ chức đối tượng theo nhóm giúp quản lý dễ dàng
- Độ khó nên tăng dần để người chơi làm quen
- Sử dụng prefabs giúp maintain level hiệu quả
- Tạo nhiều con đường để người chơi có lựa chọn

---

## SLIDE 21: Demo và Kết Quả
**Tiêu đề:** DEMO GAME HOÀN CHỈNH

**Nội dung Slide:**
**Tính năng đã hoàn thành:**
- ✅ Nhân vật di chuyển 4 hướng
- ✅ Camera theo dõi mượt mà
- ✅ Va chạm với tường và vật cản
- ✅ Hệ thống điểm số
- ✅ Vật thể xoay (Spinning Objects)
- ✅ Vật rơi (Dropping Objects)
- ✅ Đạn bay (Projectiles)
- ✅ Trigger zones
- ✅ Thay đổi màu khi va chạm

**Video Demo:**
[Chèn video hoặc GIF demo game]

**Screenshot:**
[Chèn 2-3 screenshot quan trọng]

**Nội dung thuyết trình:**
- Đây là kết quả cuối cùng của dự án
- Game có đầy đủ các tính năng đã học
- Người chơi phải khéo léo tránh các chướng ngại vật
- Điểm số tăng khi va chạm với vật cản
- Camera theo dõi mượt mà tạo trải nghiệm tốt

---

## SLIDE 22: Thách Thức và Giải Pháp
**Tiêu đề:** THÁCH THỨC GẶP PHẢI & CÁCH GIẢI QUYẾT

**Nội dung Slide:**
**1. Tốc độ không đồng nhất:**
- ❌ Vấn đề: Frame rate khác nhau → tốc độ khác nhau
- ✅ Giải pháp: Sử dụng Time.deltaTime

**2. Code lặp lại nhiều lần:**
- ❌ Vấn đề: Copy-paste code
- ✅ Giải pháp: Tạo Methods và tái sử dụng

**3. Hiệu suất kém:**
- ❌ Vấn đề: Gọi GetComponent() mỗi frame
- ✅ Giải pháp: Caching reference trong Start()

**4. Khó quản lý nhiều đối tượng:**
- ❌ Vấn đề: Thay đổi từng object riêng lẻ
- ✅ Giải pháp: Sử dụng Prefabs

**5. Camera không theo kịp:**
- ❌ Vấn đề: Viết code camera phức tạp
- ✅ Giải pháp: Dùng Cinemachine

**Bài học:**
- 📚 Luôn có nhiều cách giải quyết vấn đề
- 🔧 Sử dụng công cụ có sẵn (như Cinemachine)
- 💡 Tối ưu hóa ngay từ đầu

**Nội dung thuyết trình:**
- Trong quá trình phát triển, chúng ta gặp nhiều thách thức
- Nhưng mỗi thách thức đều có giải pháp
- Unity cung cấp nhiều công cụ để giải quyết vấn đề phổ biến
- Quan trọng là biết khi nào nên tối ưu hóa
- Và học cách sử dụng các công cụ có sẵn thay vì tự viết mọi thứ

---

## SLIDE 23: Kỹ Năng Đạt Được
**Tiêu đề:** KỸ NĂNG VÀ KINH NGHIỆM ĐẠT ĐƯỢC

**Nội dung Slide:**
**Technical Skills (Kỹ năng kỹ thuật):**
- ✅ Lập trình C# cơ bản
- ✅ Unity Editor workflow
- ✅ Game physics và collisions
- ✅ Input handling
- ✅ Component-based architecture
- ✅ Scene management

**Soft Skills (Kỹ năng mềm):**
- 🎯 Problem solving
- 🔍 Debugging
- 📝 Code organization
- 🎨 Basic game design
- 📚 Learning workflow
- 💪 Perseverance

**Concepts (Khái niệm):**
- Variables, Methods, Conditions
- Start(), Update(), FixedUpdate()
- Collisions & Triggers
- Prefabs & Instances
- Tags & Layers
- Time management

**Nội dung thuyết trình:**
- Qua dự án này, chúng ta đã đạt được rất nhiều kỹ năng
- Không chỉ về mặt kỹ thuật mà còn cả kỹ năng mềm
- Học được cách suy nghĩ logic và giải quyết vấn đề
- Hiểu workflow cơ bản của game development
- Đây là nền tảng vững chắc cho các dự án phức tạp hơn

---

## SLIDE 24: Best Practices Học Được
**Tiêu đề:** NGUYÊN TẮC VÀ THỰC HÀNH TỐT

**Nội dung Slide:**
**Code Quality (Chất lượng code):**
```csharp
// ✅ TỐT
[SerializeField] float moveSpeed = 10f;
MeshRenderer cachedRenderer;

void Start()
{
    cachedRenderer = GetComponent<MeshRenderer>();
}

// ❌ KHÔNG TỐT
void Update()
{
    GetComponent<MeshRenderer>().material.color = Color.red;
}
```

**Organization (Tổ chức):**
- 📁 Tạo folders: Scripts, Materials, Prefabs
- 🏷️ Đặt tên rõ ràng: "Player", "Obstacle", không phải "GameObject"
- 👥 Nhóm objects: Environment, Hazards
- 🎨 Sử dụng colors cho folders

**Performance (Hiệu suất):**
- ⚡ Cache references
- 🔄 Sử dụng Time.deltaTime
- 🎯 Tránh FindObject trong Update
- 💾 Destroy objects không cần thiết

**Workflow:**
- 💾 Save thường xuyên (Ctrl+S)
- ✅ Test sau mỗi thay đổi
- 📝 Comment code phức tạp
- 🔍 Debug bằng Debug.Log()

**Nội dung thuyết trình:**
- Best practices rất quan trọng cho dự án dài hạn
- Code sạch giúp maintain dễ dàng
- Tổ chức tốt giúp tìm kiếm nhanh
- Tối ưu hóa ngay từ đầu tránh vấn đề sau này
- Workflow đúng giúp phát triển hiệu quả

---

## SLIDE 25: Lộ Trình Học Tập
**Tiêu đề:** PHƯƠNG PHÁP HỌC TẬP HIỆU QUẢ

**Nội dung Slide:**
**Spiral Syllabus (Học xoắn ốc):**
```
Cơ bản → Thực hành → Trung cấp → Thực hành → Nâng cao
   ↑                                                ↓
   ←←←←←←←←←←← Lặp lại và củng cố ←←←←←←←←←←←←←←←
```

**Các giai đoạn học:**
**1. Giai đoạn Copy (Sao chép):**
- 📝 Copy code từ tutorial
- 🎯 Hiểu cú pháp cơ bản
- ⚡ Chạy được game đơn giản

**2. Giai đoạn Modify (Điều chỉnh):**
- 🔧 Thay đổi giá trị
- 🎨 Customize features
- 🧪 Thử nghiệm ý tưởng

**3. Giai đoạn Create (Tạo mới):**
- 💡 Tự thiết kế features
- 🎮 Tạo game riêng
- 🚀 Áp dụng kiến thức đa dạng

**Tips học hiệu quả:**
- ⏸️ Pause video khi chưa hiểu
- 🔁 Xem lại 2-5 lần nếu cần
- 💪 Thực hành hàng ngày
- 🤔 Đặt câu hỏi và tìm hiểu sâu

**Nội dung thuyết trình:**
- Khóa học sử dụng phương pháp Spiral Syllabus
- Học từ cơ bản, thực hành, rồi nâng cao dần
- Giai đoạn đầu copy là bình thường, không cần lo
- Quan trọng là hiểu tại sao code hoạt động
- Thực hành hàng ngày là chìa khóa thành công

---

## SLIDE 26: Mở Rộng và Cải Tiến
**Tiêu đề:** Ý TƯỞNG MỞ RỘNG DỰ ÁN

**Nội dung Slide:**
**Tính năng có thể thêm:**

**1. Gameplay:**
- ❤️ Hệ thống máu (Health System)
- ⭐ Power-ups (tăng tốc, vô địch)
- 🎯 Nhiều loại vật cản mới
- 🏆 Hệ thống cấp độ (Levels)
- ⏱️ Time challenge mode

**2. Visual & Audio:**
- 🎨 Particle effects khi va chạm
- 🔊 Sound effects và background music
- 💥 Animation cho nhân vật
- 🌟 Visual feedback rõ ràng hơn
- 🎬 Camera shake khi va chạm mạnh

**3. UI/UX:**
- 📊 Hiển thị score trên màn hình
- ⏰ Timer đếm ngược
- 💔 Health bar
- 🏁 Start menu và Game Over screen
- ⚙️ Settings menu

**4. Technical:**
- 💾 Save/Load system
- 📱 Mobile controls
- 🎮 Controller support
- 🌐 Leaderboard online
- 📈 Analytics tracking

**Nội dung thuyết trình:**
- Dự án hiện tại là nền tảng tốt để mở rộng
- Có thể thêm vô số tính năng mới
- Từ gameplay đơn giản đến phức tạp
- Thêm visual và audio cho hấp dẫn
- UI/UX tốt tạo trải nghiệm professional

---

## SLIDE 27: Resources và Tài Liệu
**Tiêu đề:** TÀI LIỆU THAM KHẢO VÀ HỌC THÊM

**Nội dung Slide:**
**Unity Resources:**
- 📚 Unity Documentation: docs.unity3d.com
- 🎓 Unity Learn: learn.unity.com
- 🎬 Unity YouTube Channel
- 💬 Unity Forum & Answers

**C# Learning:**
- 📖 Microsoft C# Documentation
- 🎯 C# Programming Guide
- 💻 Practice sites: Codewars, LeetCode

**Community:**
- 👥 Reddit: r/Unity3D, r/gamedev
- 💬 Discord servers: Unity, GameDev
- 🎮 Itch.io - game showcase
- 📺 YouTube channels: Brackeys, CodeMonkey

**Assets & Tools:**
- 🎨 Unity Asset Store
- 🎵 Free sounds: Freesound.org
- 🖼️ Free textures: Textures.com
- 🎮 Free models: Sketchfab

**Books:**
- 📕 "Unity in Action" - Joe Hocking
- 📗 "C# Programming" - Microsoft
- 📘 "Game Programming Patterns" - Robert Nystrom

**Nội dung thuyết trình:**
- Có rất nhiều tài liệu miễn phí để học Unity
- Unity Documentation là nguồn chính thức nhất
- Cộng đồng rất sẵn lòng giúp đỡ
- Thực hành với các dự án nhỏ từ Unity Learn
- Tham gia cộng đồng để học hỏi và chia sẻ

---

## SLIDE 28: Lời Khuyên Cuối Cùng
**Tiêu đề:** LỜI KHUYÊN CHO NGƯỜI HỌC

**Nội dung Slide:**
**Mindset (Tư duy):**
- 💪 Kiên nhẫn với bản thân
- 🎯 Tập trung vào progress, không phải perfection
- 🔄 Học từ lỗi sai
- 🌱 Growth mindset - luôn phát triển

**Practice (Thực hành):**
- ⏰ Code ít nhất 30 phút/ngày
- 🎮 Hoàn thành dự án nhỏ trước khi bắt đầu dự án lớn
- 🔄 Làm lại tutorial với ideas riêng
- 🚀 Publish game đầu tiên, dù đơn giản

**Community (Cộng đồng):**
- 🤝 Tham gia group, forum
- 💬 Đặt câu hỏi khi cần
- 🎁 Chia sẻ kiến thức với người khác
- 🎮 Playtest game của nhau

**Career Path (Con đường sự nghiệp):**
- 📁 Xây dựng portfolio
- 🎮 Tham gia game jams
- 💼 Contribute to open source
- 🌐 Networking với developers

**Quote truyền cảm hứng:**
> "The only way to learn programming is by writing programs." 
> - Dennis Ritchie

**Nội dung thuyết trình:**
- Game development là hành trình dài, không phải đích đến
- Kiên nhẫn và thực hành đều đặn là chìa khóa
- Đừng sợ mắc lỗi, đó là cách học tốt nhất
- Tham gia cộng đồng giúp bạn phát triển nhanh hơn
- Publish game đầu tiên là milestone quan trọng

---

## SLIDE 29: Dự Án Tiếp Theo
**Tiêu đề:** BƯỚC TIẾP THEO - ROCKET BOOST

**Nội dung Slide:**
**Preview dự án tiếp theo:**
**Rocket Boost Project:**
- 🚀 Game điều khiển tên lửa
- 🎮 Physics-based movement
- 🔊 Sound effects và particles
- 💥 Fuel system
- 🏆 Multiple levels

**Kiến thức mới sẽ học:**
- Rigidbody.AddForce() - lực vật lý
- Audio Source & Audio Clips
- Particle Systems
- Scene Management
- Level progression
- Input cải tiến hơn

**Chuẩn bị:**
- ✅ Hoàn thành Obstacle Dodge
- ✅ Ôn lại các khái niệm đã học
- ✅ Chuẩn bị mental cho thử thách mới
- ✅ Excited để học tiếp!

**Nội dung thuyết trình:**
- Dự án tiếp theo sẽ phức tạp hơn và thú vị hơn
- Rocket Boost sử dụng physics thật sự
- Thêm sound và visual effects
- Quản lý nhiều scenes và levels
- Đây là bước tiến tự nhiên sau Obstacle Dodge

---

## SLIDE 30: Kết Luận
**Tiêu đề:** KẾT LUẬN

**Nội dung Slide:**
**Tóm tắt:**
- ✅ Đã hoàn thành dự án Obstacle Dodge
- ✅ Học được nền tảng Unity và C#
- ✅ Hiểu workflow game development
- ✅ Sẵn sàng cho thử thách tiếp theo

**Thành tựu:**
- 🎮 1 game hoàn chỉnh
- 📚 15+ khái niệm quan trọng
- 💻 Nhiều scripts C#
- 🎯 Workflow chuyên nghiệp

**Cảm ơn:**
- 🙏 Cảm ơn đã theo dõi
- 💬 Sẵn sàng trả lời câu hỏi
- 🤝 Chúc mọi người thành công

**Contact & Links:**
- 📧 Email: [your-email]
- 💻 GitHub: [your-github]
- 🎮 Itch.io: [your-itch]

**Q&A**
**Có câu hỏi nào không? 🙋‍♂️**

**Nội dung thuyết trình:**
- Cảm ơn mọi người đã theo dõi bài trình bày
- Obstacle Dodge là dự án nền tảng quan trọng
- Những kiến thức này sẽ được sử dụng trong tất cả dự án tiếp theo
- Hy vọng mọi người cảm thấy tự tin hơn với Unity
- Bây giờ tôi xin mở phần hỏi đáp

---

## SLIDE 31: Backup - Q&A Suggestions
**Tiêu đề:** CÂU HỎI THƯỜNG GẶP

**Nội dung Slide:**
**1. "Unity khó học không?"**
- Ban đầu có thể khó, nhưng với thực hành đều đặn sẽ dễ dần
- Community rất hỗ trợ, tài liệu phong phú

**2. "Cần học C# đến đâu trước khi học Unity?"**
- Cơ bản là đủ: variables, methods, conditions
- Học song song Unity và C# hiệu quả hơn

**3. "Mất bao lâu để làm game như thế này?"**
- Với kinh nghiệm: 2-3 giờ
- Người mới: 1-2 tuần (học + làm)

**4. "Asset nào cần cho dự án?"**
- Chỉ cần Unity Editor, không cần asset trả phí
- Cinemachine free từ Package Manager

**5. "Nên học 2D hay 3D trước?"**
- 3D có concepts nhiều hơn nhưng apply cho cả 2D
- Tùy sở thích, nhưng 3D foundation tốt hơn

**6. "Có thể kiếm tiền từ game này không?"**
- Game này là learning project
- Nhưng có thể polish và publish để học kinh nghiệm

---

## SLIDE 32: Backup - Code Examples
**Tiêu đề:** CODE THAM KHẢO - MOVER SCRIPT

**Nội dung Slide:**
```csharp
using UnityEngine;

public class Mover : MonoBehaviour
{
    [SerializeField] float moveSpeed = 10f;
    
    void Update()
    {
        MovePlayer();
    }
    
    void MovePlayer()
    {
        float xValue = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed;
        float zValue = Input.GetAxis("Vertical") * Time.deltaTime * moveSpeed;
        transform.Translate(xValue, 0f, zValue);
    }
}
```

---

## SLIDE 33: Backup - Code Examples 2
**Tiêu đề:** CODE THAM KHẢO - COLLISION HANDLER

**Nội dung Slide:**
```csharp
using UnityEngine;

public class ObjectHit : MonoBehaviour
{
    private MeshRenderer meshRenderer;
    private int hits = 0;

    void Start()
    {
        meshRenderer = GetComponent<MeshRenderer>();
    }

    void OnCollisionEnter(Collision collision)
    {
        if (collision.gameObject.tag == "Player")
        {
            hits++;
            meshRenderer.material.color = Color.red;
            Debug.Log("Hit count: " + hits);
        }
    }
}
```

---

## PHỤ LỤC: Hướng Dẫn Sử Dụng Kịch Bản

**Cách sử dụng kịch bản này:**

1. **Cho PowerPoint:**
   - Sao chép nội dung từng slide
   - Thêm hình ảnh, screenshots từ Unity
   - Thêm GIF hoặc video demo
   - Format cho đẹp mắt

2. **Thời gian trình bày:**
   - 30 slides × 1-2 phút/slide = 30-60 phút
   - Có thể rút gọn bằng cách bỏ backup slides
   - Tăng thời gian demo nếu có

3. **Tips trình bày:**
   - Thực hành trước
   - Chuẩn bị Unity project để demo
   - Dự phòng video nếu demo fail
   - Có backup slides cho Q&A

4. **Tùy chỉnh:**
   - Thêm/bớt slides theo thời gian
   - Điều chỉnh mức độ technical theo audience
   - Thêm humor và stories cá nhân
   - Include live coding nếu tự tin

---

**Chúc bạn trình bày thành công! 🚀**
