# Ghi chú học tập: JSON Web Token (JWT) - Khái niệm và Ứng dụng

## Mục tiêu bài học
- Hiểu khái niệm và cấu trúc của **JSON Web Token (JWT)**.
- Nắm được lý do sử dụng JWT trong **authorization (ủy quyền)**.
- Biết cách triển khai JWT trong ứng dụng web với các thao tác tạo, xác thực, và làm mới token.
- Xây dựng ứng dụng demo sử dụng **Node.js** và **Express** để thực hiện các chức năng liên quan đến JWT.

---

## Khái niệm JSON Web Token (JWT)

### Định nghĩa
- **JSON Web Token (JWT)**: Là một chuẩn mở để truyền dữ liệu an toàn giữa các bên dưới dạng đối tượng JSON.
- **Tính an toàn**: JWT được ký bằng chữ ký số, đảm bảo dữ liệu không bị giả mạo.
- **Ứng dụng chính**: Được sử dụng cho **authorization (ủy quyền)**, không phải **authentication (xác thực)**.

### Phân biệt Authentication và Authorization
- **Authentication (xác thực)**:
  - Là quá trình kiểm tra danh tính người dùng (ví dụ: kiểm tra username và password).
  - Đây là bước đầu tiên trong quy trình bảo mật.
  - Ví dụ: Xác minh thông tin đăng nhập có hợp lệ hay không.
- **Authorization (ủy quyền)**:
  - Là quá trình cấp quyền cho người dùng để truy cập tài nguyên hoặc chức năng cụ thể.
  - Thực hiện sau bước xác thực.
  - Ví dụ: Quyết định người dùng có quyền gọi API hay truy cập dữ liệu hay không.
  - JWT đảm bảo rằng người gửi request đã đăng nhập thành công và có quyền truy cập.

### Cấu trúc của JWT
JWT bao gồm 3 phần, nối với nhau bằng dấu chấm (`.`):
1. **Header**:
   - Chứa thông tin về thuật toán mã hóa (mặc định: **HS256**) và loại token (**JWT**).
   - Ví dụ: `{"alg": "HS256", "typ": "JWT"}`.
2. **Payload**:
   - Chứa thông tin người dùng (không bao gồm thông tin nhạy cảm như password).
   - Ví dụ: `{"sub": "123456", "name": "user", "iat": 1631234567}`.
   - Các trường phổ biến:
     - `sub`: ID người dùng.
     - `name`: Tên người dùng.
     - `iat`: Thời gian tạo token (issued at).
3. **Signature**:
   - Được tạo bằng cách mã hóa Base64 của **Header** và **Payload**, sau đó sử dụng **secret key** để ký.
   - Công thức: `HMAC-SHA256(base64(Header) + "." + base64(Payload), secret)`.
   - **Secret key**: Phải được bảo mật tuyệt đối trên server.

---

## Lý do sử dụng JWT

### Vấn đề với Session-based Authorization
- **Session-based Authorization**:
  - Server lưu trữ **session ID** sau khi người dùng đăng nhập thành công.
  - Client lưu trữ **session ID** (thường trong cookie) và gửi kèm trong các request tiếp theo.
  - Server kiểm tra **session ID** trong cơ sở dữ liệu để xác minh người dùng.
- **Hạn chế**:
  - Phù hợp với kiến trúc **monolith** (một server duy nhất).
  - Trong kiến trúc **microservices**, nhiều server không chia sẻ chung cơ sở dữ liệu session, dẫn đến vấn đề khi request được chuyển đến server khác.

### Lợi ích của JWT
- **Lưu trữ thông tin trên client**:
  - JWT chứa thông tin người dùng và chữ ký số, không cần lưu trữ session trên server.
  - Server chỉ cần xác thực chữ ký của JWT để đảm bảo tính hợp lệ.
- **Hỗ trợ microservices**:
  - Tất cả các server có thể chia sẻ **secret key** để xác thực JWT.
  - Không phụ thuộc vào cơ sở dữ liệu session, giảm tải server.
- **Tính linh hoạt**:
  - JWT có thể được gửi qua header (Authorization), body, hoặc query string.

---

## Ứng dụng Demo: Tạo, Xác thực và Làm mới JWT

### Cài đặt môi trường
- **Khởi tạo dự án**:
  ```bash:disable-run
  npm init -y
  ```
- **Cài đặt các thư viện**:
  ```bash
  npm install dotenv express jsonwebtoken nodemon
  ```
  - `dotenv`: Lưu trữ biến môi trường.
  - `express`: Framework để xây dựng server.
  - `jsonwebtoken`: Xử lý JWT.
  - `nodemon`: Tự động khởi động lại server khi có thay đổi.

- **Cấu hình `package.json`**:
  ```json
  "scripts": {
    "start": "nodemon server.js",
    "start-server": "nodemon server.js"
  }
  ```

- **Tạo file `.env`**:
  ```env
  PORT=5000
  ACCESS_TOKEN_SECRET=your_access_token_secret
  REFRESH_TOKEN_SECRET=your_refresh_token_secret
  ```

### Cấu hình Server
- **Tạo file `server.js`**:
  ```javascript
  import express from 'express';
  import dotenv from 'dotenv';
  import jwt from 'jsonwebtoken';

  dotenv.config();
  const app = express();
  const PORT = process.env.PORT || 5000;

  app.use(express.json()); // Middleware để parse JSON từ client

  app.listen(PORT, () => {
    console.log(`Server is running on port ${PORT}`);
  });
  ```

- **Dữ liệu mẫu**:
  ```javascript
  const books = [
    { id: 1, title: "Chí Phèo", author: "ABC" },
    { id: 2, title: "Chiến tranh và Hòa bình", author: "XYZ" }
  ];
  ```

### Xây dựng API

#### 1. API Login (Tạo Access Token và Refresh Token)
- **Đường dẫn**: `POST /login`
- **Chức năng**: Tạo **access token** và **refresh token** khi người dùng đăng nhập.
- **Mã nguồn**:
  ```javascript
  app.post('/login', (req, res) => {
    const { username } = req.body;
    const accessToken = jwt.sign(
      { username },
      process.env.ACCESS_TOKEN_SECRET,
      { expiresIn: '30s' } // Access token hết hạn sau 30 giây
    );
    const refreshToken = jwt.sign(
      { username },
      process.env.REFRESH_TOKEN_SECRET
    );
    refreshTokens.push(refreshToken); // Lưu refresh token (lưu ý: nên lưu vào database)
    res.json({ accessToken, refreshToken });
  });
  ```

#### 2. API Refresh Token
- **Đường dẫn**: `POST /refresh-token`
- **Chức năng**: Tạo **access token** mới dựa trên **refresh token**.
- **Mã nguồn**:
  ```javascript
  let refreshTokens = []; // Lưu trữ tạm thời (nên dùng database trong thực tế)

  app.post('/refresh-token', (req, res) => {
    const { token } = req.body;
    if (!token) return res.status(401).json({ error: 'Unauthorized' });
    if (!refreshTokens.includes(token)) return res.status(403).json({ error: 'Forbidden' });

    try {
      const data = jwt.verify(token, process.env.REFRESH_TOKEN_SECRET);
      const accessToken = jwt.sign(
        { username: data.username },
        process.env.ACCESS_TOKEN_SECRET,
        { expiresIn: '30s' }
      );
      res.json({ accessToken });
    } catch (error) {
      res.status(403).json({ error: 'Forbidden' });
    }
  });
  ```

#### 3. API Logout
- **Đường dẫn**: `POST /logout`
- **Chức năng**: Xóa **refresh token** khi người dùng đăng xuất.
- **Mã nguồn**:
  ```javascript
  app.post('/logout', (req, res) => {
    const { token } = req.body;
    refreshTokens = refreshTokens.filter(t => t !== token);
    res.status(200).json({ message: 'OK' });
  });
  ```

#### 4. API Books (Yêu cầu Authorization)
- **Đường dẫn**: `GET /books`
- **Chức năng**: Trả về danh sách sách nếu **access token** hợp lệ.
- **Middleware xác thực token**:
  ```javascript
  const authenticateToken = (req, res, next) => {
    const authHeader = req.headers['authorization'];
    const token = authHeader && authHeader.split(' ')[1];
    if (!token) return res.status(401).json({ error: 'Unauthorized' });

    try {
      const data = jwt.verify(token, process.env.ACCESS_TOKEN_SECRET);
      console.log('Token data:', data);
      next();
    } catch (error) {
      res.status(403).json({ error: 'Forbidden' });
    }
  };

  app.get('/books', authenticateToken, (req, res) => {
    res.json({ status: 'success', data: books });
  });
  ```

### Kiểm tra API với Rest Client
- **Cài đặt Rest Client**:
  - Sử dụng extension **Rest Client** trong Visual Studio Code để gửi request.
- **File `jwt.rest`**:
  ```rest
  ### Login
  POST http://localhost:5000/login
  Content-Type: application/json

  {
    "username": "Hutech"
  }

  ### Get Books
  GET http://localhost:5000/books
  Authorization: Bearer <access_token>

  ### Refresh Token
  POST http://localhost:5000/refresh-token
  Content-Type: application/json

  {
    "token": "<refresh_token>"
  }

  ### Logout
  POST http://localhost:5000/logout
  Content-Type: application/json

  {
    "token": "<refresh_token>"
  }
  ```

### Triển khai mô hình Microservices
- **Tách server**:
  - **Server 1** (`auth-server.js`): Xử lý đăng nhập, đăng xuất, làm mới token (chạy trên port 5500).
  - **Server 2** (`server.js`): Xử lý API dữ liệu (ví dụ: `/books`).
- **Chia sẻ secret key**:
  - Cả hai server sử dụng cùng **ACCESS_TOKEN_SECRET** và **REFRESH_TOKEN_SECRET** trong file `.env`.
- **Kiểm tra**:
  - Đăng nhập trên server 1 để lấy **access token** và **refresh token**.
  - Sử dụng **access token** để gọi API `/books` trên server 2.
  - Khi **access token** hết hạn, gọi API `/refresh-token` trên server 1 để lấy token mới.

---

## Ghi chú thêm
- **Bảo mật**:
  - **Secret key** phải được bảo mật tuyệt đối, không để lộ.
  - **Refresh token** nên được lưu trong cơ sở dữ liệu (không nên lưu trong biến tạm như trong demo).
- **Hạn chế**:
  - JWT không phù hợp để lưu trữ thông tin nhạy cảm (ví dụ: password) trong payload.
  - Cần cơ chế làm mới token để tránh việc token hết hạn gây gián đoạn.
- **Liên kết nội bộ**:
  - [[Authentication]].
  - [[Authorization]].
  - [[Microservices]].

---

## Tổng kết
- JWT là công cụ mạnh mẽ để thực hiện **authorization** trong ứng dụng web, đặc biệt trong kiến trúc **microservices**.
- Việc triển khai JWT cần chú ý đến bảo mật và quản lý **refresh token**.
- Ứng dụng demo sử dụng **Node.js** và **Express** minh họa cách tạo, xác thực, và làm mới JWT.

--- 

**Nguồn tham khảo**: Video hướng dẫn về JWT (không tham chiếu nguồn web bên ngoài).
```