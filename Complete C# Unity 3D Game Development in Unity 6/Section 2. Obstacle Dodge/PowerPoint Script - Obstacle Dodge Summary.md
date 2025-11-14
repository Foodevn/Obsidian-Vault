# Kịch Bản PowerPoint: Kiến Thức Cơ Bản Tạo Game Né Tránh Chướng Ngại Vật
## Unity 3D Game Development - Tóm Tắt Nền Tảng

---

## SLIDE 1: Trang Bìa
**Tiêu đề chính:** KIẾN THỨC CƠ BẢN
**Phụ đề:** Tạo Game Né Tránh Chướng Ngại Vật với Unity
**Thông tin:** Dự án Obstacle Dodge - Unity & C#

**Hình ảnh đề xuất:** Screenshot game Obstacle Dodge

	**Nội dung thuyết trình:**
	- Xin chào! Hôm nay tôi sẽ trình bày những kiến thức cơ bản để tạo một game né tránh chướng ngại vật sử dụng Unity và C#
	- Qua dự án Obstacle Dodge, chúng ta sẽ tìm hiểu các khái niệm nền tảng nhất của game development

---

## SLIDE 2: Tổng Quan Game và Mục Tiêu
**Tiêu đề:** DỰ ÁN OBSTACLE DODGE

**Nội dung Slide:**
**Game Description:**
- 🎮 Loại: Trò chơi tránh chướng ngại vật 3D
- 🎯 Mục tiêu: Di chuyển từ start đến finish, tránh vật cản
- 🕹️ Điều khiển: Phím WASD hoặc mũi tên

**Yếu Tố Game:**
- ✓ Nhân vật di chuyển 4 hướng
- ✓ Camera theo dõi tự động
- ✓ Chướng ngại vật: xoay, rơi, bay
- ✓ Hệ thống điểm số và va chạm

**Kiến Thức Học Được:**
- C# Programming: Variables, Methods, Conditions
- Unity Core: GameObjects, Components, Physics
- Game Dev: Input, Collisions, Prefabs

**Nội dung thuyết trình:**
- Obstacle Dodge là game đơn giản nhưng bao gồm tất cả yếu tố cơ bản của game development
- Người chơi điều khiển nhân vật tránh các chướng ngại vật để đến đích
- Qua dự án này, chúng ta sẽ nắm được nền tảng Unity và C#

---

## SLIDE 3: Thiết Lập Dự Án Unity
**Tiêu đề:** 1. THIẾT LẬP DỰ ÁN & SCENE

**Nội dung Slide:**
**Tạo Dự Án:**
```
Unity Hub → New Project
→ Universal 3D Template
→ Đặt tên: "Obstacle Dodge"
```

**Thiết Lập Scene Cơ Bản:**
```
Hierarchy → Create:
├── Plane (Ground) - Scale: 3.5, 3.5, 3.5
├── Cube (Player) - Tùy chỉnh scale
├── Cubes (Obstacles/Walls) - Bao quanh khu vực
└── Main Camera - Điều chỉnh góc nhìn
```

**Tổ Chức Assets:**
```
Project Folder:
├── 📁 Scripts/
├── 📁 Materials/
└── 📁 Prefabs/
```

**Materials (Vật liệu):**
- Tạo materials khác màu cho Ground, Player, Obstacles
- Giảm Smoothness = 0 để có bề mặt mờ

**Nội dung thuyết trình:**
- Bước đầu là thiết lập dự án với template Universal 3D
- Tạo các game objects cơ bản: mặt đất, nhân vật, chướng ngại vật
- Tổ chức thư mục ngăn nắp giúp quản lý dự án dễ dàng
- Materials giúp phân biệt các đối tượng bằng màu sắc

---

## SLIDE 4: Vòng Đời Script - Start() và Update()
**Tiêu đề:** 2. VÒNG ĐỜI SCRIPT UNITY

**Nội dung Slide:**
**Start() vs Update():**
```csharp
public class Mover : MonoBehaviour
{
    void Start()
    {
        // ✅ Chạy 1 LẦN khi game bắt đầu
        // Dùng cho: Khởi tạo, thiết lập ban đầu
        Debug.Log("Game Started!");
    }

    void Update()
    {
        // ✅ Chạy MỖI FRAME (60+ lần/giây)
        // Dùng cho: Di chuyển, Input, Logic liên tục
        transform.Translate(0.01f, 0f, 0f);
    }
}
```

**Tạo & Gắn Script:**
```
Project → Scripts → Create C# Script → "Mover"
Kéo script vào Player trong Hierarchy
Double-click để mở trong VS Code
```

**Kết quả:**
- Player di chuyển liên tục sang phải mỗi frame

**Nội dung thuyết trình:**
- Start() và Update() là hai hàm quan trọng nhất trong Unity
- Start() chạy một lần duy nhất khi game bắt đầu - dùng để khởi tạo
- Update() chạy liên tục mỗi frame - dùng cho logic game
- Transform.Translate() di chuyển object theo hướng chỉ định

---

## SLIDE 5: Variables - Biến trong C#
**Tiêu đề:** 3. VARIABLES - LƯU TRỮ DỮ LIỆU

**Nội dung Slide:**
**Khái niệm Biến:**
- 📦 "Hộp" chứa dữ liệu: tên, giá trị, kiểu dữ liệu
- 🔄 Có thể thay đổi giá trị trong code

**Các Kiểu Dữ Liệu Cơ Bản:**
```csharp
// Số thập phân (có dấu f)
float speed = 10.5f;
float xValue = 0.01f;

// Số nguyên
int score = 0;
int lives = 3;

// True/False
bool isAlive = true;
bool hasKey = false;

// Chuỗi ký tự
string playerName = "Dodgy";
```

**Sử Dụng Biến:**
```csharp
float xValue = 0.01f;

void Update()
{
    transform.Translate(xValue, 0f, 0f);
    // Dễ dàng thay đổi xValue thay vì 0.01f
}
```

**Nội dung thuyết trình:**
- Biến giúp lưu trữ và quản lý dữ liệu trong game
- Float dùng cho số thập phân, int cho số nguyên, bool cho true/false
- Sử dụng biến giúp code linh hoạt và dễ bảo trì hơn
- Thay vì hard-code giá trị, ta lưu vào biến và dễ dàng điều chỉnh

---

## SLIDE 6: SerializeField - Hiển Thị Trong Inspector
**Tiêu đề:** 4. SERIALIZEFIELD - ĐIỀU CHỈNH TRỰC TIẾP

**Nội dung Slide:**
**Vấn Đề:**
- Muốn thay đổi giá trị → phải sửa code → save → chạy lại
- Tốn thời gian khi thử nghiệm

**Giải Pháp - SerializeField:**
```csharp
[SerializeField] float xValue = 0f;
[SerializeField] float yValue = 0.05f;
[SerializeField] float zValue = 0f;

void Update()
{
    transform.Translate(xValue, yValue, zValue);
}
```

**Kết Quả:**
- ✅ Biến hiển thị trong Unity Inspector
- ✅ Thay đổi giá trị real-time khi Play
- ✅ Thử nghiệm nhanh mà không sửa code
- ⚠️ Thay đổi trong Play Mode không được lưu

**Demo:**
```
Chọn Player → Inspector → Mover Script
→ Thấy X Value, Y Value, Z Value
→ Có thể điều chỉnh bằng số hoặc slider
```

**Nội dung thuyết trình:**
- SerializeField là tính năng tuyệt vời của Unity
- Cho phép hiển thị biến private trong Inspector
- Có thể thử nghiệm nhiều giá trị nhanh chóng trong Play Mode
- Rất tiện khi cần điều chỉnh tốc độ, màu sắc, khoảng cách...
- Lưu ý: thay đổi trong Play Mode sẽ mất khi Stop

---

## SLIDE 7: Input System - Xử Lý Điều Khiển
**Tiêu đề:** 5. INPUT SYSTEM - ĐIỀU KHIỂN NGƯỜI CHƠI

**Nội dung Slide:**
**Input.GetAxis() - Đọc Phím Bấm:**
```csharp
void Update()
{
    // Trả về -1 đến 1
    float xValue = Input.GetAxis("Horizontal"); 
    // A/Left = -1, D/Right = 1, Không nhấn = 0
    
    float zValue = Input.GetAxis("Vertical");
    // W/Up = 1, S/Down = -1
    
    float yValue = 0f; // Không bay lên
    
    transform.Translate(xValue, yValue, zValue);
}
```

**Input Manager (Có sẵn):**
- "Horizontal": A/D, ← →
- "Vertical": W/S, ↑ ↓

**Vấn Đề:**
- ❌ Di chuyển quá nhanh
- ❌ Tốc độ khác nhau trên máy khác nhau
- ➡️ Giải quyết: Time.deltaTime

**Nội dung thuyết trình:**
- Input.GetAxis() đọc input từ bàn phím hoặc controller
- Giá trị trả về từ -1 đến 1, rất mượt mà cho di chuyển
- Horizontal cho trái/phải, Vertical cho lên/xuống
- Đặt yValue = 0 để nhân vật không bay lên
- Nhưng hiện tại di chuyển quá nhanh, cần chuẩn hóa

---

## SLIDE 8: Time.deltaTime - Chuẩn Hóa Tốc Độ
**Tiêu đề:** 6. TIME.DELTATIME - TỐC ĐỘ ĐỒNG NHẤT

**Nội dung Slide:**
**Vấn Đề Frame Rate:**
```
Máy nhanh: 120 FPS → Update chạy 120 lần/giây → nhanh
Máy chậm: 30 FPS  → Update chạy 30 lần/giây  → chậm
```

**Giải Pháp - Time.deltaTime:**
```csharp
[SerializeField] float moveSpeed = 10f;

void Update()
{
    float xValue = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed;
    float zValue = Input.GetAxis("Vertical") * Time.deltaTime * moveSpeed;
    
    transform.Translate(xValue, 0f, zValue);
}
```

**Time.deltaTime:**
- ⏱️ Thời gian (giây) để render 1 frame
- 🎯 Chuyển từ "mỗi frame" sang "mỗi giây"
- ✅ Tốc độ đồng nhất trên mọi máy

**Ví dụ:**
- moveSpeed = 10 → Di chuyển 10 đơn vị/giây
- Điều chỉnh moveSpeed trong Inspector

**Nội dung thuyết trình:**
- Time.deltaTime là giá trị cực kỳ quan trọng trong game dev
- Nó biểu thị thời gian để render một frame
- Nhân với Time.deltaTime chuyển đổi từ "per frame" sang "per second"
- Kết hợp với biến moveSpeed, ta kiểm soát tốc độ chính xác
- Giờ game chạy đồng nhất trên mọi máy tính

---

## SLIDE 9: Cinemachine - Camera Tự Động
**Tiêu đề:** 7. CINEMACHINE - CAMERA THEO DÕI

**Nội dung Slide:**
**Cài Đặt Cinemachine:**
```
Window → Package Manager
→ Unity Registry → Tìm "Cinemachine"
→ Install
```

**Thêm Virtual Camera:**
```
Hierarchy → Right-click
→ Cinemachine → Cinemachine Camera
```

**Cấu Hình Virtual Camera:**
```
Inspector:
├── Tracking Target: [Chọn Player]
├── Position Control → Follow
│   └── Follow Offset: (X: 10, Y: 8, Z: -10)
├── Rotation Control → Hard Look At
│   └── Look At Target: [Player]
└── Position Damping: (0.2, 0.2, 0.2)
```

**Kết Quả:**
- 🎥 Camera tự động theo Player
- 🎬 Góc nhìn đẹp và mượt mà
- ⚙️ Không cần viết code camera

**Nội dung thuyết trình:**
- Cinemachine là công cụ camera chuyên nghiệp của Unity, miễn phí
- Thay vì viết code phức tạp, chỉ cần cấu hình trong Inspector
- Virtual Camera tự động theo dõi Player với độ trễ mượt mà
- Follow Offset điều chỉnh vị trí camera so với Player
- Damping tạo độ trễ để camera không giật cục

---

## SLIDE 10: Physics - Va Chạm Cơ Bản
**Tiêu đề:** 8. COLLISION SYSTEM - VA CHẠM

**Nội dung Slide:**
**Components Cần Thiết:**

**1️⃣ Collider (Vùng va chạm):**
```
Mọi object cần va chạm phải có Collider:
- Box Collider (cho Cube)
- Sphere Collider (cho Sphere)
- Mesh Collider (cho model phức tạp)
```

**2️⃣ Rigidbody (Vật lý):**
```
Thêm vào Player:
Player → Add Component → Rigidbody

Cấu hình:
├── Use Gravity: ❌ Tắt (không rơi)
├── Freeze Position Y: ✅ Bật (không bay)
└── Freeze Rotation XYZ: ✅ Bật (không xoay)
```

**Phát Hiện Va Chạm:**
```csharp
void OnCollisionEnter(Collision collision)
{
    Debug.Log("Đã va chạm với: " + collision.gameObject.name);
}
```

**Kết Quả:**
- ✅ Player không đi xuyên tường
- ✅ Phát hiện khi va chạm
- ✅ Có thể xử lý logic khi chạm

**Nội dung thuyết trình:**
- Unity có hệ thống physics mạnh mẽ
- Collider xác định vùng va chạm của object
- Rigidbody thêm tính vật lý: trọng lực, khối lượng, lực
- Cần tắt gravity và đóng băng rotation/position Y để đúng gameplay
- OnCollisionEnter() tự động gọi khi có va chạm

---

## SLIDE 11: Methods và Code Organization
**Tiêu đề:** 9. METHODS - TỔ CHỨC CODE

**Nội dung Slide:**
**Methods (Phương thức):**
```csharp
// ❌ Code lộn xộn
void Update()
{
    float x = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed;
    float z = Input.GetAxis("Vertical") * Time.deltaTime * moveSpeed;
    transform.Translate(x, 0f, z);
    
    if (Input.GetKeyDown(KeyCode.Space))
    {
        Debug.Log("Jump!");
    }
}

// ✅ Code sạch sẽ với Methods
void Update()
{
    MovePlayer();
    HandleInput();
}

void MovePlayer()
{
    float x = Input.GetAxis("Horizontal") * Time.deltaTime * moveSpeed;
    float z = Input.GetAxis("Vertical") * Time.deltaTime * moveSpeed;
    transform.Translate(x, 0f, z);
}

void HandleInput()
{
    if (Input.GetKeyDown(KeyCode.Space))
    {
        Debug.Log("Jump!");
    }
}
```

**Lợi Ích:**
- ✅ Dễ đọc, dễ hiểu
- ✅ Tái sử dụng code
- ✅ Dễ debug và maintain

**Nội dung thuyết trình:**
- Methods giúp chia code thành các khối logic rõ ràng
- Mỗi method thực hiện một nhiệm vụ cụ thể
- Code dễ đọc hơn nhiều khi có tên methods mô tả đúng chức năng
- Dễ dàng tái sử dụng và bảo trì
- Đây là nguyên tắc cơ bản của clean code

---

## SLIDE 12: GetComponent và Caching
**Tiêu đề:** 10. GETCOMPONENT() - TRUY CẬP COMPONENT

**Nội dung Slide:**
**GetComponent() - Truy cập Components:**
```csharp
void OnCollisionEnter(Collision collision)
{
    // Lấy MeshRenderer component và đổi màu
    MeshRenderer renderer = GetComponent<MeshRenderer>();
    renderer.material.color = Color.red;
}
```

**Tối Ưu - Caching Reference:**
```csharp
// ❌ KHÔNG TỐT - Gọi mỗi frame
void Update()
{
    GetComponent<MeshRenderer>().material.color = Color.red;
}

// ✅ TỐT - Cache trong Start()
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

**Lý Do:**
- GetComponent() tốn hiệu suất
- Cache 1 lần → dùng nhiều lần
- Tăng performance đáng kể

**Nội dung thuyết trình:**
- GetComponent cho phép truy cập các component khác trên cùng GameObject
- Rất hữu ích để thao tác với MeshRenderer, Rigidbody, Collider...
- Nhưng GetComponent tốn hiệu suất nếu gọi nhiều lần
- Best practice: Cache reference trong Start(), dùng lại trong Update()
- Đây là kỹ thuật tối ưu cơ bản nhất trong Unity

---

## SLIDE 13: Tags và If Statements
**Tiêu đề:** 11. TAGS & CONDITIONS - LOGIC GAME

**Nội dung Slide:**
**Tags - Phân Loại Objects:**
```
Tạo Tag:
Inspector → Tag dropdown → Add Tag
→ Nhập "Obstacle", "Pickup", "Enemy"

Gán Tag:
Chọn object → Inspector → Tag → Chọn tag
```

**If Statements - Điều Kiện:**
```csharp
int score = 0;

void OnCollisionEnter(Collision collision)
{
    if (collision.gameObject.tag == "Obstacle")
    {
        Debug.Log("Hit obstacle!");
        GetComponent<MeshRenderer>().material.color = Color.red;
    }
    else if (collision.gameObject.tag == "Pickup")
    {
        Debug.Log("Collected pickup!");
        score++;
        Destroy(collision.gameObject);
    }
}
```

**Ứng Dụng:**
- Xử lý khác nhau cho từng loại object
- Tăng điểm khi nhặt vật phẩm
- Mất máu khi chạm kẻ thù
- Kích hoạt checkpoint

**Nội dung thuyết trình:**
- Tags giúp phân loại và nhận diện các loại objects khác nhau
- If statements cho phép code ra quyết định dựa trên điều kiện
- Kết hợp tags và conditions để xử lý logic phức tạp
- Ví dụ: va chạm với Obstacle thì đổi màu đỏ, va chạm Pickup thì tăng điểm
- Đây là nền tảng để tạo gameplay đa dạng

---

## SLIDE 14: Prefabs - Tái Sử Dụng Objects
**Tiêu đề:** 12. PREFABS - QUẢN LÝ & TÁI SỬ DỤNG

**Nội dung Slide:**
**Prefab là gì?**
- 📦 Template của GameObject
- 💾 Lưu dưới dạng file .prefab
- 🔄 Tạo nhiều instances giống nhau

**Workflow:**
```
1. Tạo Prefab:
   Kéo GameObject từ Hierarchy → Project/Prefabs/
   
2. Tạo Instance:
   Kéo Prefab từ Project → Scene
   
3. Sửa Prefab:
   Double-click Prefab (Isolation Mode)
   → Sửa → Save
   → Tất cả instances tự động cập nhật!
   
4. Override Instance:
   Sửa 1 instance riêng
   → Overrides trong Inspector
   → Apply All hoặc Revert
```

**Lợi Ích:**
- ✅ Cập nhật hàng loạt dễ dàng
- ✅ Consistency trong dự án
- ✅ Tiết kiệm thời gian development
- ✅ Dễ dàng quản lý nhiều objects

**Nội dung thuyết trình:**
- Prefabs là một trong những tính năng mạnh nhất của Unity
- Tạo template một lần, tái sử dụng vô số lần
- Khi sửa prefab gốc, tất cả instances tự động cập nhật
- Rất quan trọng cho các object lặp lại như chướng ngại vật, kẻ thù
- Giúp giữ consistency và giảm thiểu lỗi

---

## SLIDE 15: Tổng Kết và Demo
**Tiêu đề:** TỔ HỢP KIẾN THỨC - GAME HOÀN CHỈNH

**Nội dung Slide:**
**Kiến Thức Đã Học:**
```
✅ 1. Thiết lập Scene & Assets
✅ 2. Start() & Update() - Vòng đời script
✅ 3. Variables - Lưu trữ dữ liệu
✅ 4. SerializeField - Inspector editing
✅ 5. Input System - Điều khiển
✅ 6. Time.deltaTime - Chuẩn hóa tốc độ
✅ 7. Cinemachine - Camera tự động
✅ 8. Collisions - Va chạm vật lý
✅ 9. Methods - Tổ chức code
✅ 10. GetComponent() - Truy cập components
✅ 11. Tags & Conditions - Logic game
✅ 12. Prefabs - Tái sử dụng objects
```

**Game Features:**
- 🎮 Di chuyển 4 hướng mượt mà
- 🎥 Camera theo dõi chuyên nghiệp
- 💥 Va chạm với vật cản
- 🎯 Hệ thống điểm số
- 🔄 Chướng ngại vật đa dạng

**Next Steps:**
- 🚀 Thêm UI (score, timer, health bar)
- 🔊 Sound effects và music
- 💡 Particle effects
- 🏆 Multiple levels
- 📱 Build và publish

**Nội dung thuyết trình:**
- Chúng ta đã đi qua 12 kiến thức cơ bản nhất
- Tất cả kết hợp lại tạo thành một game hoàn chỉnh
- Đây là nền tảng cho mọi game Unity project
- Từ đây có thể mở rộng thêm nhiều tính năng
- Quan trọng là hiểu rõ từng khái niệm và biết khi nào áp dụng
- Thực hành nhiều là chìa khóa thành công!

---

## PHỤ LỤC: Code Tham Khảo Đầy Đủ

**Mover.cs - Script Di Chuyển Player:**
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

**ObjectHit.cs - Script Va Chạm:**
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
            Debug.Log("Hits: " + hits);
        }
    }
}
```

**Spinner.cs - Script Xoay Vật:**
```csharp
using UnityEngine;

public class Spinner : MonoBehaviour
{
    [SerializeField] float rotateSpeed = 100f;
    
    void Update()
    {
        transform.Rotate(0, rotateSpeed * Time.deltaTime, 0);
    }
}
```

---

## Hướng Dẫn Sử Dụng Kịch Bản

**Thời lượng:** 15-20 phút

**Cấu trúc:**
- Slide 1: Mở đầu (1 phút)
- Slides 2-3: Giới thiệu & setup (2 phút)
- Slides 4-14: Kiến thức cơ bản (10-15 phút)
- Slide 15: Tổng kết + Demo (2-3 phút)

**Tips:**
- ✅ Chuẩn bị Unity project để live demo
- ✅ Thêm screenshots/GIF vào mỗi slide
- ✅ Highlight code quan trọng
- ✅ Thực hành trước khi trình bày
- ✅ Có backup video nếu demo fail

**Tùy chỉnh theo audience:**
- Beginner: Chi tiết hơn slides 4-6
- Intermediate: Nhanh qua slides 4-8, focus vào 9-14
- Technical: Thêm performance tips, best practices

---

**Chúc bạn trình bày thành công! 🎮**
