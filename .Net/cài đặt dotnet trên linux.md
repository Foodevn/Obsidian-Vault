# 1.Thêm Microsoft package feed
wget https://packages.microsoft.com/config/ubuntu/24.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
rm packages-microsoft-prod.deb

# 2.Cập nhật gói và cài đặt .NET 8 SDK
sudo apt-get update
sudo apt-get install -y dotnet-sdk-8.0

# 3.Kiểm tra cài đặt
dotnet --version

# 4.Tạo dự án MVC
dotnet new mvc -n MyMvcApp
cd MyMvcApp

# 5.Chạy dự án
dotnet run


mở port 5030
https://5030-dot-yourprojectid.region.cloudshell.dev/

đổi port 
dotnet run --urls http://0.0.0.0:8080
