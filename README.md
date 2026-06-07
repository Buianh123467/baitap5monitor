# baitap5monitor
họ và tên : bùi ngọc anh

lớp k58.ktp

mssv : k2225510201001

#bailam

Lý thuyết 

1. Docker là gì?
Docker là công cụ đóng gói ứng dụng cùng toàn bộ môi trường phụ thuộc vào một "hộp chứa" duy nhất gọi là Container.

2. Từ khóa trong docker-compose.yml
version: Phiên bản cú pháp Docker Compose (Ví dụ: version: '3.8').

services: Nhóm định nghĩa các container sẽ chạy (Ví dụ: mariadb, nodered).

image: Tên và bản sao môi trường tải từ mạng về (Ví dụ: image: mariadb:latest).

container_name: Đặt tên cố định cho container để dễ quản lý (Ví dụ: container_name: monitor_mariadb).

ports: Mở cổng kết nối giữa máy chủ và container (Ví dụ: ports: - "3000:3000").

environment: Khai báo biến cấu hình, mật khẩu (Ví dụ: MYSQL_ROOT_PASSWORD: root_password).

volumes: Gắn thư mục để lưu dữ liệu bền vững, không bị mất khi xóa container (Ví dụ: - mariadb_data:/var/lib/mysql).

networks: Tạo mạng ảo nội bộ để các container tự kết nối với nhau.

restart: always: Tự động chạy lại container nếu bị lỗi hoặc khi reset máy chủ.

3. Ưu điểm khi triển khai ứng dụng sử dụng Docker
Tính nhất quán (Consistency): Đảm bảo ứng dụng chạy y hệt nhau trên mọi môi trường (Laptop cá nhân, Staging, Server thật), loại bỏ hoàn toàn lỗi cấu hình khác biệt giữa các máy.

Tiết kiệm tài nguyên: Nhẹ hơn máy ảo (VM) rất nhiều do dùng chung nhân hệ điều hành máy chủ, giúp chạy được nhiều container cùng lúc mà không tốn tài nguyên cho OS ảo.

Triển khai siêu tốc (Speed & Scalability): Khởi động trong vài giây. Cài đặt cả hệ thống phức tạp (Node-RED, MariaDB, Nginx...) chỉ bằng một câu lệnh docker compose up -d.

Cách ly an toàn (Isolation): Mỗi container hoạt động hoàn toàn độc lập. Một dịch vụ bị lỗi hoặc sập không làm ảnh hưởng đến hệ điều hành gốc và các dịch vụ khác.

4. Các bước triển khai lên máy chủ thật KHÔNG CÓ INTERNET

Bước 1 (Trên Laptop có mạng): Xuất toàn bộ Docker Image đang dùng thành file nén

Bước 2 (Di chuyển dữ liệu): Dùng USB hoặc ổ cứng di động copy file app_images.tar và thư mục mã nguồn myapp/ (chứa file docker-compose.yml) sang máy chủ thật.

Bước 3 (Trên Máy chủ thật): Nạp lại các file Image vào hệ thống và kích hoạt ứng dụng.

II Thực hành 

cấu trúc dự án 
<img width="353" height="316" alt="Image" src="https://github.com/user-attachments/assets/759ac0f1-9b85-46b9-ae37-d4d4011f2a15" />

cấu hình APP.PY
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/1322c63a-e2ea-40a0-b4d8-a1d4ffd052d5" />

cấu hình dockerfile
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/05018fb3-a1d0-4a95-a3c8-377ef46fac44" />

cấu hình index.html
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/646b7b76-0c4e-4b42-b2ae-79f55b677401" />

cấu hình docker compose.yml
<img width="1366" height="768" alt="Image" src="https://github.com/user-attachments/assets/6f886016-6abd-416a-85e3-3aa1ec392016" />

chạy lệnh docker compose up -d khởi chạy hệ thống 
<img width="1160" height="640" alt="Image" src="https://github.com/user-attachments/assets/3d439249-07ce-4a51-8c68-a5e02bf76163" />

Vào trình duyệt để cấu hình Node-RED bằng giao diện kéo thả.

Cài đặt thư viện phụ trợ trong Node-RED:

Vào góc phải trên cùng -> Manage palette -> Thẻ Install -> Tìm và cài các nod

node-red-node-mysql (Kết nối MariaDB)

node-red-contrib-influxdb (Kết nối InfluxDB)

node-red-contrib-telegrambot (Gửi tin nhắn Telegram)

<img width="1327" height="614" alt="Image" src="https://github.com/user-attachments/assets/784c280b-7b3e-4149-95d5-2065e63e0260" />

cấu hình 
<img width="1332" height="616" alt="Image" src="https://github.com/user-attachments/assets/68067f63-59ee-491c-9b96-549a98143a5b" />

<img width="1357" height="671" alt="Image" src="https://github.com/user-attachments/assets/02d61b0b-4350-4852-80a8-615d18fc3f3d" />

truy cập  Grafana

vào mục Connections → Data Sources → Chọn InfluxDB.

<img width="1332" height="667" alt="Image" src="https://github.com/user-attachments/assets/9e4a6325-973b-4b58-90ea-7eedf1a871d0" />

Tạo một Group Telegram mới

<img width="1284" height="2552" alt="Image" src="https://github.com/user-attachments/assets/3f45b703-ab56-495e-bf8e-2bf5d907f230" />

Kéo thêm các Node sau từ đầu ra của Node Function.

Bước 1: Kéo và cấu hình Node switch

Bước 2: Cấu hình node switch

<img width="873" height="585" alt="Image" src="https://github.com/user-attachments/assets/a18b3e68-a629-44b8-94cd-6f10bf0687a0" />






