---
title: "5.6 Messaging & Notifications (SQS, SNS, SES)"
weight: 1
---

## Messaging & Notifications với SQS, SNS, SES

Phần này tập trung vào xử lý bất đồng bộ và thông báo trong hệ thống IMS
sử dụng Amazon SQS, Amazon SNS và Amazon SES.

## Sơ đồ messaging & notification

![Cấu hình SQS queue cho job nền IMS](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20queue.png)
![Policy truy cập SQS cho producer/consumer](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20policy.png)
![Chi tiết queue bao gồm cấu hình DLQ](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20config.png)

![SNS topic phát tán cảnh báo sản xuất](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SNS.png)
![Email alert nhận được từ SNS notification](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SNS%20alert.png)

![Cấu hình SES để gửi email OTP và thông báo](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SES.png)

![CloudWatch alarm tích hợp SNS cho cảnh báo hạ tầng](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/cloudwatch-alarm.png)

## Use case chính

- Đưa các tác vụ nặng vào hàng đợi, ví dụ:
  - Tính lại KPI sản xuất.
  - Tạo báo cáo sản xuất ngày/tuần.
  - Xử lý sự kiện trễ hoặc lỗi.
- Phát tán (fan-out) thông báo tới nhiều consumer (manager, công cụ giám sát...).
- Gửi email OTP và thông báo hệ thống (thay đổi lịch, cảnh báo quan trọng).

## Amazon SQS – Xử lý nền

1. Tạo các queue cho job nền (ví dụ `ims-delay-events`, `ims-report-jobs`).
2. Cấu hình dead-letter queue (DLQ) cho message lỗi.
3. Trong backend, thiết kế service để:
   - Gửi message lên SQS khi có sự kiện (ví dụ phát hiện trễ).
   - Tiêu thụ message từ SQS (qua cron, worker, hoặc ECS service riêng).
4. Sử dụng message attribute để truyền thêm context (mã đơn hàng, line, mức độ nghiêm trọng...).

## Amazon SNS – Cảnh báo & Fan-Out

1. Tạo SNS topic (ví dụ `ims-critical-alerts`, `ims-status-updates`).
2. Subcribe queue SQS, email hoặc endpoint khác vào topic.
3. Từ backend, publish event mức cao lên SNS khi:
   - Có sự cố sản xuất nghiêm trọng.
   - Có ngưỡng cảnh báo được kích hoạt.
4. Tích hợp SNS với CloudWatch alarm để nhận cảnh báo hạ tầng.

## Amazon SES – Email OTP & Thông báo

1. Verify domain và địa chỉ email trong **Amazon SES**.
2. Cấu hình backend gửi email qua SES (sử dụng template `otp-email.html`).
3. Các luồng thường gặp:
   - Quên mật khẩu → tạo OTP → gửi qua SES → người dùng nhập OTP để xác nhận.
   - Manager tạo lịch sản xuất mới → hệ thống gửi email kèm link/tài liệu cho line leader.
4. Lưu ý môi trường sandbox của SES (phải verify cả người gửi và người nhận).

Bằng cách kết hợp SQS, SNS và SES, hệ thống IMS có thể xử lý tải lớn theo kiểu bất đồng bộ
và gửi cảnh báo kịp thời tới các bên liên quan.
