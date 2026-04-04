---
title: "5.9 Quan sát hệ thống & CI/CD"
weight: 1
---

# 5.9 Quan sát hệ thống & CI/CD Pipeline

Phần này trình bày cách giám sát hệ thống IMS bằng Amazon CloudWatch và
tự động hoá build/deploy với AWS CodeBuild, CodePipeline.

## CloudWatch Logs & Metrics

- **ECS Task**: gửi log ứng dụng lên CloudWatch Logs (ví dụ `/ecs/ims-backend`).
- **ALB**: (tuỳ chọn) ghi access log về S3 để phân tích HTTP chi tiết.
- **RDS**: các chỉ số CPU, số kết nối, IOPS đọc/ghi.
- **SQS/SNS/SES**: metrics vận hành cơ bản (độ dài hàng đợi, lỗi gửi, bounce...).

Bạn có thể tạo Dashboard đơn giản gồm:
- CPU & memory của ECS service.
- CPU & connections của RDS.
- Độ sâu queue SQS (số message chờ xử lý).
- Số lỗi 5XX của ALB và thời gian phản hồi trung bình.

## CloudWatch Alarm

Tạo alarm cho các tín hiệu quan trọng, ví dụ:

- **CPU ECS service** > 80% trong 5 phút → gửi thông báo qua SNS.
- **ALB HTTPCode_Target_5XX_Count** vượt ngưỡng → nghi ngờ lỗi ứng dụng.
- **RDS CPUUtilization** > 80% trong thời gian dài → cần tối ưu hiệu năng.
- **SQS ApproximateNumberOfMessagesVisible** quá cao → backlog job nền.

Alarm có thể gửi email (qua SNS/SES) và dùng làm trigger cho chính sách auto scaling
của ECS service.

## CI/CD với CodeBuild & CodePipeline

Repo đã có file `buildspec.yml` ở root để:
- Build backend Spring Boot.
- Build Docker image.
- Push image lên **Amazon ECR**.
- Tạo file `imagedefinitions.json` cho ECS deploy.

Một pipeline mẫu cho backend:

1. **Source Stage** – lấy mã nguồn từ GitHub/CodeCommit.
2. **Build Stage (CodeBuild)** – chạy `buildspec.yml` để build & push image.
3. **Deploy Stage** – dùng CodeDeploy hoặc ECS deploy action để cập nhật ECS service
   với `imagedefinitions.json` mới.

Bạn có thể tạo pipeline riêng cho frontend:
- Build React bằng `npm run build`.
- Đồng bộ artifact build lên S3 bucket frontend.
- Invalidate cache CloudFront.

## Vận hành & Rollback

Khi có sự cố:
- Xem log trong CloudWatch để tìm lỗi ứng dụng.
- Rollback về task definition hoặc image ECR phiên bản trước.
- Tạm thời scale-out ECS task nếu CPU hoặc latency tăng.

Khi có quan sát tốt và pipeline CI/CD, hệ thống IMS trở nên dễ vận hành,
dễ debug và nâng cấp an toàn hơn theo thời gian.
