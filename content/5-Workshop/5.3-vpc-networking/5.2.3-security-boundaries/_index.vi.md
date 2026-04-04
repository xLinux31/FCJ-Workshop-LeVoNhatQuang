---
title: "5.3.3 Biên giới bảo mật – Security Group, NACL & IAM"
date: 2026-01-01
weight: 2
chapter: false
---

Phần này mô tả cách cho phép/giới hạn traffic giữa các thành phần, và cách lớp bảo mật mạng liên quan đến IAM và secrets.

#### Bạn cấu hình gì?

- **Security group** cho:
  - Application Load Balancer: cho phép HTTP/HTTPS từ Internet.
  - ECS service: chỉ cho phép traffic đến từ security group của ALB.
  - RDS PostgreSQL: chỉ cho phép traffic đến từ security group của ECS service.
- **Network ACL (NACL)** (tuỳ chọn) – giữ cấu hình đơn giản, dùng default allow rules cho workshop.
- Mối quan hệ giữa **network boundary** và **identity boundary**:
  - Security group / NACL: kiểm soát ai có thể nói chuyện ở **tầng mạng**.
  - IAM role & policy: kiểm soát **AWS API** nào ECS task được phép gọi (ECR, S3, SQS, SNS, SES, Secrets Manager, CloudWatch).
  - **Secrets Manager + KMS**: lưu và mã hoá credential DB, secret SMTP/SES và các cấu hình nhạy cảm khác.

#### Bài tập workshop

- Tạo security group cho ALB, ECS service và RDS, cấu hình cho phép đúng luồng traffic.
- Kiểm tra đảm bảo database chỉ truy cập được từ ECS task, không truy cập trực tiếp từ Internet.
- Liên kết sang cấu hình IAM và secrets chi tiết hơn ở module `6.6-auth-security-secrets`.
