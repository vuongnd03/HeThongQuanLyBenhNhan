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
ava 21

Spring Boot – Framework chính cho các microservice.

Spring Security + JWT – Xác thực và phân quyền.

gRPC + Protocol Buffers – Giao tiếp hiệu quả giữa các service.

Apache Kafka – Truyền sự kiện theo hướng publish-subscribe.

PostgreSQL – Cơ sở dữ liệu riêng biệt cho từng service.

Docker & Docker Compose – Đóng gói và triển khai hạ tầng.

JUnit + Testcontainers – Kiểm thử tích hợp (tích hợp Kafka, PostgreSQL...).
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
