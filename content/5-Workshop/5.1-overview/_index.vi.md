---
title: "5.1 Tổng quan Workshop"
weight: 1
---

Phần này tóm tắt lại bài toán, vai trò người dùng và kịch bản demo cho
Hệ thống Quản lý Sản xuất Điện tử hỗ trợ AI (IMS).

## Bài toán

Các nhà máy điện tử vừa và nhỏ thường gặp:
- Lập kế hoạch sản xuất thủ công bằng Excel.
- Không có theo dõi tiến độ theo thời gian thực ở từng công đoạn (SMT, DIP, testing).
- Dữ liệu đơn hàng, lệnh sản xuất, báo cáo nằm rải rác nhiều file/hệ thống.
- Khó đánh giá năng lực line, thời gian chờ, nút thắt cổ chai.
- Hạ tầng on-prem khó mở rộng, thiếu giám sát tập trung.

## Đối tượng & Vai trò

Hệ thống được thiết kế cho 3 vai trò chính:

- **Admin** – quản lý tài khoản, phân quyền, cấu hình hệ thống.
- **Manager** – tạo/quản lý đơn hàng, lập kế hoạch sản xuất, theo dõi KPI & OEE.
- **Line Leader** – xem nhiệm vụ được giao, cập nhật tiến độ, nhận lịch và email thông báo.

## Kịch bản Demo

Trong workshop, ta dùng ví dụ một nhà máy điện tử với nhiều line (SMT, DIP, testing):

1. Manager tạo đơn hàng và kế hoạch sản xuất trên web.
2. Line leader nhận danh sách công việc trong ngày và cập nhật tiến độ.
3. Hệ thống tổng hợp dữ liệu thành dashboard, biểu đồ tiến độ và chỉ số OEE.
4. API AI cung cấp trả lời tự nhiên, ví dụ:
   - "Line nào đang gây trễ kế hoạch tuần này?"
   - "Hôm nay OEE của line SMT 1 là bao nhiêu?"
   - "Đơn hàng nào có nguy cơ trễ deadline?"

## Hành trình Workshop

Trong toàn bộ mục 5-Workshop, bạn sẽ:
- Hiểu kiến trúc end-to-end của IMS trên AWS.
- Đóng gói và triển khai backend Spring Boot lên ECS + RDS.
- Host frontend React trên S3 + CloudFront.
- Tích hợp SQS, SNS, SES cho xử lý nền và thông báo.
- Bảo mật secrets bằng Secrets Manager và cấu hình IAM cơ bản.
- Thiết lập CloudWatch logs, metrics, alarms và một pipeline CI/CD đơn giản.
