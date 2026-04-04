---
title: "5.3.4 Kết nối dịch vụ – ECS, RDS, S3 & Messaging"
date: 2026-01-01
weight: 2
chapter: false
---

# 5.3.4 Kết nối dịch vụ – ECS, RDS, S3 & Messaging

Ở bước cuối, bạn kết nối các dịch vụ AWS với VPC để ứng dụng có thể hoạt động end‑to‑end.

#### Bạn kết nối những gì?

- **ECS Fargate service** trong private subnet, phía trước là ALB nằm ở public subnet.
- **RDS PostgreSQL** trong private subnet, chỉ nhận kết nối từ security group của ECS.
- Kết nối từ ECS task tới:
  - **Amazon ECR** để pull container image.
  - **Amazon S3** để lưu file.
  - **Amazon SQS/SNS** cho job nền và thông báo.
  - **Amazon SES** để gửi email OTP và email hệ thống.
  - **AWS Secrets Manager** để lấy credential DB và secret SMTP/SES.

#### ALB và Target Group

![ALB ở public subnet routing tới ECS](/images/5-Workshop/5.3-vpc-networking/ALB.png)

![Target Group cho ECS service phía sau ALB](/images/5-Workshop/5.3-vpc-networking/TG.png)

Hai hình này minh hoạ ALB lắng nghe ở public subnet và chỉ forward traffic tới các ECS task healthy trong private subnet thông qua target group.

#### Mẫu kết nối mạng

- Bắt đầu với việc cho phép truy cập ra ngoài thông qua **NAT gateway** tới các endpoint public của AWS.
- Tuỳ chọn: thảo luận về **VPC endpoint** (S3, SQS, SNS, Secrets Manager, CloudWatch Logs) như một bước hardening cho môi trường production.

#### Bài tập workshop

- Gắn private subnet vào ECS cluster và RDS subnet group.
- Kiểm tra ECS task có thể truy cập ECR, S3, SQS/SNS/SES và Secrets Manager từ private subnet.
- Đối chiếu lại cách lớp mạng này hỗ trợ các module sau: backend ECS/RDS, messaging & notifications, security và observability.
