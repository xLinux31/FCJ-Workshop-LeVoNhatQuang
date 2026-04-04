---
title: "Workshop"
date: 2025-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# Workshop: Triển khai Hệ thống Quản lý Sản Xuất Điện Tử hỗ trợ AI trên AWS

#### Tổng quan

Workshop này hướng dẫn bạn triển khai **Hệ thống Quản lý Sản xuất Điện tử hỗ trợ AI (IMS)** lên AWS.
Bạn sẽ sử dụng chính **Spring Boot backend** và **React frontend** trong repository này, sau đó triển khai
chúng lên môi trường gần với production sử dụng các dịch vụ managed của AWS.

Hệ thống giúp nhà máy quản lý đơn hàng, kế hoạch sản xuất, hiệu suất line và các báo cáo/phân tích bằng AI.

**Công nghệ chính:**
- **Backend:** Spring Boot, JPA/Hibernate, REST API, Java 17
- **Frontend:** React (Vite), routing theo vai trò (Admin / Manager / Line Leader)
- **Database:** Amazon RDS (PostgreSQL)
- **Compute & Containers:** Amazon ECS (Fargate), Amazon ECR, Application Load Balancer (ALB)
- **Storage & CDN:** Amazon S3 (frontend + tài liệu), Amazon CloudFront
- **Messaging & Notifications:** Amazon SQS, Amazon SNS, Amazon SES (gửi OTP & thông báo)
- **Bảo mật & Cấu hình:** AWS Secrets Manager, IAM, AWS KMS, security group
- **Giám sát & CI/CD:** Amazon CloudWatch, AWS CodeBuild, AWS CodePipeline

#### Bạn sẽ học được gì?

Sau khi hoàn thành workshop, bạn sẽ:

- Thiết kế kiến trúc **VPC với public/private subnets**, ALB, ECS services và RDS.
- Build và đóng gói backend Spring Boot thành Docker image và push lên **Amazon ECR**.
- Triển khai backend lên **Amazon ECS Fargate** phía sau **Application Load Balancer**.
- Build frontend React và deploy lên **Amazon S3 + CloudFront + Route 53** với HTTPS.
- Sử dụng **Amazon SQS** và **Amazon SNS** để tách rời các tác vụ nền và cảnh báo.
- Tích hợp **Amazon SES** để gửi email OTP và thông báo sản xuất.
- Áp dụng best practice bảo mật với **IAM roles**, IAM user cho SES, **Secrets Manager** và mã hóa bằng **KMS**.
- Cấu hình **CloudWatch Logs**, **metrics**, **dashboards** và **alarms** (ví dụ ECS CPU > 80%) để giám sát hệ thống.

#### Đối tượng phù hợp

- Sinh viên và kỹ sư muốn xem một ví dụ cụ thể về hệ thống web gần production trên AWS.
- Developer đã nắm cơ bản về AWS (EC2/ECS, S3, IAM) và web (Java/Spring, React).

#### Các phần trong workshop

Workshop được chia thành các phần sau (ứng với các thư mục con trong `5-Workshop/`):

1. **[Tổng quan hệ thống & kịch bản demo](5.1-overview/)** – bối cảnh nghiệp vụ IMS và cách tổ chức các bước hands-on.
2. **[Kiến trúc giải pháp & Infrastructure-as-Code](5.2-architecture-iac/)** – kiến trúc tổng thể IMS trên AWS và (tuỳ chọn) triển khai bằng IaC.
3. **[VPC & Networking](5.3-vpc-networking/)** – VPC, subnets, routing, Internet/NAT Gateway, security group và kết nối tới các dịch vụ AWS.
4. **[Triển khai Backend trên ECS & RDS](5.4-backend-ecs-rds/)** – container Spring Boot, ECR repository, ECS task/service và schema PostgreSQL.
5. **[Triển khai Frontend với S3 & CloudFront](5.5-frontend-s3-cloudfront/)** – build React, host tĩnh trên S3, CloudFront distribution và cấu hình domain.
6. **[Messaging & Notifications với SQS, SNS, SES](5.6-messaging-notifications-sqs-sns-ses/)** – SQS queue, SNS topic và luồng gửi email/OTP với SES.
7. **[Xác thực, bảo mật & quản lý secrets](5.7-auth-security-secrets/)** – IAM roles, IAM user cho SES, Secrets Manager, KMS và các pattern bảo mật trong ứng dụng.
8. **[Lớp AI phân tích sản xuất](5.8-ai-production-analytics/)** – cách dữ liệu sản xuất (đơn hàng, line, delay, OEE) được dùng cho AI assistant và báo cáo.
9. **[Quan sát hệ thống & CI/CD Pipeline](5.9-observability-ci-cd/)** – CloudWatch logs/metrics/alarms, dashboard và pipeline buildspec–CodeBuild–ECR–ECS.

Mỗi phần đều gắn trực tiếp với code trong repo (`backend/` và `frontend/`) và các tài nguyên AWS đã mô tả trong **Idea for AWS project** và **2‑Proposal**.
