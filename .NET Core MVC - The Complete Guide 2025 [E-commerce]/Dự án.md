- Đa ngôn ngữ: tiếng Anh, tiếng Việt
- Xem trang chủmàn hình chính: gồm có các thông tin vềtài khoản của người dùng, thông tin các bệnh viện, thông tin các bác sĩ, thông tin các chuyên khoa khám bệnh. 
- Xem chi tiết thông tin bệnh viện
- Xem chi tiết thông tin bác sĩ
- Xem chi tiết thông tin chuyên khoa khám bệnh
- Xem lịch sử khám bệnh: bệnh nhân có thểxem lại lịch sửkhám bệnh của mình cũng như xem lại đơn thuốc đã được lên đơn.
- Đăng nhập và phân quyền: mỗi người dùng có một quyền nhất định. Tài khoản quản trị viên sẽ có tất cả các quyền. 
	- Tài khoản của bác sĩ thì không thể thực hiện xóa, sửa, thêm tài khoản, được quyền thêm những ca chính bác sĩ ấy trống đểchữa bệnh và quản lý bệnh nhân, lên đơn thuốc khám bệnh. 
	- Tài khoản bệnh nhân thì chỉ xem được các thông tin bác sĩ, bệnh viện, chuyên khoa khám bệnh, lịch sửkhám bệnh và thông tin cá nhân của mình. 
- Đăng ký tài khoản: mặc định đăng ký tài khoản thành công thì sẽ trao cho tài khoản đăng ký là bệnh nhân. 
- Quên mật khẩu: bệnh nhân có thểlấy lại mật khẩu của mình qua email dưới đường link xác nhận token 
- Cập nhật thông tin người người: bệnh nhân có thể cập nhật thông tin hồsơ của mình
- Quản lý bệnh nhân: bác sĩ có thể xem thông tin các bệnh nhân đặt lịch, tạo đơn thuốc, gửi qua email cho bệnh nhân.
- Quản lý thời gian trống để bệnh nhân đặt lịch: bác sĩ
- Chọn ngày trong hệ thống sau đó chọn ca mà bác sĩ rãnh có thể khám bệnh để bệnh nhân biết và đặt lịch khám bệnh cho chính mình
- Quản lý tài khoản: Quản trịviên có thể xem thông tin của tất cảtài khoản trong hệthống(bác sĩ, bệnh nhân)
- Quản lý kế hoạch khám bệnh của bác sĩ: Quản trị viên có thể thêm, cập nhật ca làm việc của bác sĩ
- Quản lý thông tin phòng khám: Quản trị viên có thể thêm, cập nhật, xóa thông tin phòng khám
- Quản lý chuyên khoa: Quản trịviên có thểthêm, cập nhật, xóa chuyên khoa khám bệnh
- Quản lý thuốc: Quản trịviên có thểthêm, cập nhật, xóa các loại thuốc-Thống kê top 3 bác sĩ có doanh thu cao nhất trong năm theo từng tháng (biểu đồ)
- Thống kê top 4 bệnh nhân vip
- Thống kê doanh thu các chuyên khoa theo tháng
- Lên đơn thuốc và gửi về email bệnh nhân
- Thống kê tổng số bác sĩ
- Thống kê tổng số lịch hẹn khám bệnh đã hoàn thành trong hệ thống
- Thống kê các user mới trong ngày
- Thống kê doanh thu của hệ thống hàng tuần


## **1. Các chức năng cần làm trước (cốt lõi)**

### **A. Liên quan đến người dùng**

- **Đăng ký tài khoản (mặc định là bệnh nhân)**  
    → Cần để người dùng có thể tham gia hệ thống.
    
- **Đăng nhập & phân quyền cơ bản** (Bệnh nhân, Bác sĩ, Quản trị viên)  
    → Xác định được quyền để kiểm soát truy cập.
    
- **Quên mật khẩu (reset bằng email)**  
    → Giúp người dùng khôi phục tài khoản.
    
- **Cập nhật thông tin người dùng** (bệnh nhân)  
    → Cho phép người dùng chỉnh sửa hồ sơ cá nhân.
    

### **B. Chức năng khám bệnh và đặt lịch**

- **Quản lý thời gian trống của bác sĩ** (bác sĩ chọn ca làm việc rảnh)
    
- **Đặt lịch khám bệnh (bệnh nhân)**
    
- **Quản lý bệnh nhân (dành cho bác sĩ)**: xem danh sách bệnh nhân đã đặt lịch.
    
- **Xem lịch sử khám bệnh & đơn thuốc** (bệnh nhân)
    
- **Lên đơn thuốc & gửi qua email (bác sĩ)**  
    → Đây là luồng nghiệp vụ chính của hệ thống.
    

### **C. Quản lý thông tin cơ bản**

- **Trang chủ hiển thị thông tin cơ bản** (tài khoản, bệnh viện, bác sĩ, chuyên khoa)
    
- **Xem chi tiết thông tin bệnh viện, bác sĩ, chuyên khoa**
    
- **Quản lý phòng khám (quản trị viên)**: thêm/cập nhật/xóa
    
- **Quản lý chuyên khoa (quản trị viên)**
    

---

## **2. Các chức năng nâng cao (làm sau)**

- **Đa ngôn ngữ (tiếng Anh & tiếng Việt)** (nâng cấp trải nghiệm)
    
- **Quản lý thuốc (quản trị viên)**
    
- **Thống kê**:
    
    - Top 3 bác sĩ doanh thu cao nhất theo tháng
        
    - Top 4 bệnh nhân VIP
        
    - Doanh thu chuyên khoa theo tháng
        
    - Tổng số bác sĩ
        
    - Tổng số lịch hẹn hoàn thành
        
    - User mới trong ngày
        
    - Doanh thu hàng tuần của hệ thống
        
- **Quản lý tài khoản toàn hệ thống (quản trị viên)**
    
- **Quản lý kế hoạch khám bệnh của bác sĩ (quản trị viên)**
    

---

## **3. Lộ trình gợi ý**

1. **Sprint 1 (Chức năng cơ bản hệ thống & người dùng)**
    
    - Đăng ký, đăng nhập, phân quyền cơ bản
        
    - Trang chủ và hiển thị thông tin cơ bản (bệnh viện, bác sĩ, chuyên khoa)
        
    - Cập nhật hồ sơ cá nhân
        
    - Quên mật khẩu
        
2. **Sprint 2 (Quy trình đặt lịch khám)**
    
    - Bác sĩ quản lý thời gian trống
        
    - Bệnh nhân đặt lịch khám
        
    - Bác sĩ xem danh sách bệnh nhân & lên đơn thuốc gửi email
        
    - Bệnh nhân xem lịch sử khám & đơn thuốc
        
3. **Sprint 3 (Quản trị & nâng cao)**
    
    - Quản lý phòng khám, chuyên khoa
        
    - Quản lý tài khoản (quản trị viên)
        
    - Quản lý thuốc
        
    - Thống kê cơ bản (tổng bác sĩ, tổng lịch hẹn, user mới)
        
4. **Sprint 4 (Nâng cao & mở rộng)**
    
    - Đa ngôn ngữ
        
    - Thống kê doanh thu & top bác sĩ, bệnh nhân
        
    - Báo cáo chuyên sâu