---
title: "Kiến trúc giải pháp & IaC"
weight: 1
---

## Kiến trúc giải pháp & Infrastructure-as-Code

Phần này giải thích kiến trúc tổng thể của hệ thống IMS trên AWS và cách
bạn có thể triển khai hạ tầng bằng Infrastructure-as-Code (IaC).

### Kiến trúc logic

Ở mức tổng quan, hệ thống có luồng như sau:

1. **Trình duyệt / Frontend** – Ứng dụng React SPA build từ thư mục `frontend/`.
2. **CDN & Static Hosting** – Artifact build của React được host trên **Amazon S3** và phân phối qua **Amazon CloudFront**.
3. **DNS & Routing** – Domain tuỳ chỉnh quản lý bởi **Amazon Route 53**, trỏ về CloudFront (frontend) và ALB (backend API).
4. **Backend API** – Ứng dụng Spring Boot trong `backend/backend` được đóng gói Docker và chạy trên **Amazon ECS (Fargate)** phía sau **Application Load Balancer**.
5. **Database** – **Amazon RDS (PostgreSQL)** lưu trữ đơn hàng, kế hoạch, trạng thái line, kết quả phân tích AI.
6. **Lưu trữ file** – Nhiều bucket **S3** cho:
   - Static assets của frontend.
   - Tài liệu sản xuất (POM/SOOP, form, file đính kèm).
   - Artifact triển khai và backup cấu hình.
7. **Messaging & Notifications** – **Amazon SQS** cho xử lý nền, **Amazon SNS** và **SES** cho cảnh báo và email.
8. **Bảo mật & Cấu hình** – **AWS Secrets Manager** cho mật khẩu và API key, IAM role cho ECS và CI/CD.
9. **Giám sát** – **Amazon CloudWatch** cho logs, metrics, alarms, dashboards.

### Mapping repo → kiến trúc

- `backend/backend` → Docker image → ECS Task Definition → ECS Service → ALB Target Group.
- `frontend/` → Vite build output → S3 website bucket → CloudFront distribution.
- Schema DB (các file migration tại `src/main/resources/db/migration/`) → Amazon RDS.
- Template email `otp-email.html` → luồng gửi OTP / thông báo sử dụng SES.

### Tuỳ chọn IaC

Bạn có thể hiện thực kiến trúc bằng nhiều cách:

- **Thiết lập thủ công trên console** để hiểu từng bước.
- **CloudFormation / AWS CDK** để định nghĩa VPC, ECS, RDS, S3, CloudFront, v.v.
- **Terraform** nếu bạn quen hạ tầng đa-cloud.

Trong workshop, bạn có thể bắt đầu với console + CLI để nắm rõ từng dịch vụ, sau đó
xem IaC như bước mở rộng nâng cao.

### So sánh với workshop serverless

So với ứng dụng serverless Travel Guide trong `5-Workshop` (Lambda + API Gateway + DynamoDB):

- Ở đây bạn chạy service container dài hạn trên **ECS Fargate** thay vì Lambda.
- Sử dụng cơ sở dữ liệu quan hệ (**RDS PostgreSQL**) thay vì DynamoDB.
- Bạn quản lý image Docker trong **ECR** và triển khai qua ECS/ALB.

Kiến trúc này gần với cách nhiều hệ thống Spring Boot + React trong doanh nghiệp được đưa lên AWS.
