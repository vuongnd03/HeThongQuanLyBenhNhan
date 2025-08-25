"# HeThongQuanLyBenhNhan" 
Java Spring Microservices - Hệ thống quản lý phòng khám
Dự án này trình bày kiến ​​trúc vi dịch vụ thực tế sử dụng Java và Spring Boot . Hệ thống được mô phỏng theo một phòng khám chăm sóc sức khỏe, bao gồm các chức năng chính như quản lý bệnh nhân, thanh toán, xác thực, phân tích và thông báo.

Tổng quan
Dự án dựa trên dịch vụ vi mô này bao gồm:

API Gateway – Điểm vào duy nhất cho tất cả các dịch vụ
Authentication Service – Đăng ký/đăng nhập người dùng bằng mã thông báo JWT
Patient Service – Xử lý hồ sơ bệnh nhân và xuất bản sự kiện
Billing Service – Giao tiếp với dịch vụ bệnh nhân thông qua gRPC
Analytics Service – Sử dụng các sự kiện Kafka để thực hiện phân tích
Dịch vụ thông báo – Lắng nghe các sự kiện Kafka và gửi cảnh báo
Kiểm thử tích hợp – Kiểm thử cho các tình huống đầu cuối
Cơ sở hạ tầng – Thiết lập dựa trên Docker với Kafka, PostgreSQL, v.v.
Công nghệ Stack
Java 21
spring boot
spring security + JWT
gRPC – Giao tiếp giữa các dịch vụ
Kafka – Phát trực tuyến sự kiện
PostgreSQL – Cơ sở dữ liệu cho từng dịch vụ
Docker & Docker Compose – Điều phối container
Protocol Buffers– Dành cho tin nhắn gRPC
JUnit/Testcontainers – Kiểm thử tích hợp
🧱 Kiến trúc
                       +------------------------+
                       |     API Gateway        |
                       +-----------+------------+
                                   |
      +----------------------------+-----------------------------+
      |                            |                             |
+-----v-----+            +---------v--------+           +--------v--------+
|  Auth     |            |   Patient        |           |    Billing       |
|  Service  |            |   Service        |<--gRPC--->|    Service       |
+-----------+            +--------+---------+           +-----------------+
                                  |
                             Kafka Event
                                  v
                    +---------------------------+
                    |  Notification Service     |
                    +---------------------------+
                                  |
                    +---------------------------+
                    |  Analytics Service        |
                    +---------------------------+
