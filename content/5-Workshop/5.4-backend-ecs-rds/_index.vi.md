---
title: "Backend trên ECS & RDS"
weight: 1
---

## Triển khai Backend trên ECS, ECR & RDS

Phần này tập trung vào việc đóng gói và triển khai backend Spring Boot
(từ thư mục `backend/backend`) lên Amazon ECS (Fargate) và kết nối tới
cơ sở dữ liệu Amazon RDS.

## Tổng quan backend

Backend là ứng dụng Spring Boot cung cấp REST API cho:
- Quản lý đơn hàng và lệnh sản xuất.
- Khai báo line sản xuất và năng lực.
- Theo dõi tiến độ, trễ và hiệu suất.
- Cung cấp dữ liệu cho dashboard và các endpoint phân tích AI.
- Gửi email OTP và thông báo qua SES.

Dự án sử dụng:
- Java 17
- Spring Boot
- Spring Security (phân quyền theo vai trò)
- JPA/Hibernate với Flyway migration cho database

## Đóng gói container

1. Xem lại file `Dockerfile` trong `backend/backend/`.
2. Build JAR bằng Maven (`./mvnw -DskipTests clean package`).
3. Build Docker image và tag với URI của repository ECR.
4. Push image lên **Amazon ECR**.

Trong workshop, quy trình này có thể được tự động hoá bằng **AWS CodeBuild** với
file `buildspec.yml` ở thư mục gốc repo.

## Triển khai lên ECS (Fargate)

![Tạo ECS cluster và Fargate service](/images/5-Workshop/5.4-backend-ecs-rds/ecs2.png)
![Task definition với container image và CPU/memory](/images/5-Workshop/5.4-backend-ecs-rds/ecs3.png)
![Cấu hình service, desired count và deployment](/images/5-Workshop/5.4-backend-ecs-rds/ecs4.png)
![Tích hợp load balancer cho ECS service](/images/5-Workshop/5.4-backend-ecs-rds/ecs5.png)
![Cấu hình auto scaling cho ECS service](/images/5-Workshop/5.4-backend-ecs-rds/ecs6.png)
![ALB listener và target group gắn với ECS](/images/5-Workshop/5.4-backend-ecs-rds/ecs8alb.png)
![Chính sách scale ECS service theo CPU](/images/5-Workshop/5.4-backend-ecs-rds/ecs9autoscale.png)

1. Tạo **ECS Cluster** (kiểu Fargate).
2. Định nghĩa **Task Definition**:
   - Image container lấy từ ECR.
   - CPU/Memory (ví dụ 0.5 vCPU / 1–2 GB RAM).
   - Cổng container (ví dụ 8080).
   - Biến môi trường (URL DB, username, password, v.v.) – ưu tiên lấy từ Secrets Manager.
3. Tạo **Application Load Balancer (ALB)** và target group cho ECS service.
4. Cấu hình health check (ví dụ `/actuator/health` nếu bật).
5. Tạo **ECS Service** dùng task definition và gắn với target group của ALB.

## Kết nối Amazon RDS

![Instance Amazon RDS PostgreSQL trong private subnet](/images/5-Workshop/5.4-backend-ecs-rds/RDS.png)

1. Khởi tạo database **PostgreSQL** trên Amazon RDS trong private subnet của VPC.
2. Cấu hình Security Group để chỉ ECS (và máy quản trị cần thiết) có thể truy cập DB.
3. Lưu thông tin đăng nhập DB trong **AWS Secrets Manager**.
4. Map secrets / biến môi trường vào task definition của ECS:
   - `SPRING_DATASOURCE_URL`
   - `SPRING_DATASOURCE_USERNAME`
   - `SPRING_DATASOURCE_PASSWORD`
5. Kiểm tra Flyway migration (trong `src/main/resources/db/migration/`) chạy ok khi app khởi động.

## Luồng truy cập & log

Khi chạy thực tế, request đi theo luồng:

`Client → Route 53 → ALB → ECS Service (Spring Boot) → RDS`

Log từ container được gửi về **CloudWatch Logs** (ví dụ log group `/ecs/ims-backend`).
Bạn có thể dựa vào log để debug lỗi và xác nhận service hoạt động ổn định sau mỗi lần deploy.
