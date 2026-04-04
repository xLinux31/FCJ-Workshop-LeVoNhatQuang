---
title: "Worklog Tuần 4"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 4:

* Triển khai cơ sở dữ liệu RDS và xác thực kết nối ECS -> RDS.
* Tích hợp AI với dữ liệu trong RDS và kiểm thử query thực tế.
* Tăng cường bảo mật bằng AWS Secrets Manager.
* Hoàn thiện luồng frontend với S3, CloudFront và Route 53.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc | Trạng thái |
| --- | --- | --- |
| 26/01/2026 | Tạo database RDS (PostgreSQL); kết nối ECS -> RDS; test lưu và đọc dữ liệu. | Hoàn thành |
| 27/01/2026 | Tích hợp AI với database; AI có thể đọc dữ liệu từ RDS; test query thực tế. | Hoàn thành |
| 28/01/2026 | Setup AWS Secrets Manager; lưu API key (AI, DB password); ECS đọc secret thay vì hardcode; fix lỗi security. | Hoàn thành |
| 29/01/2026 | Tạo S3 (Frontend); upload web frontend (React/Vue); test truy cập static web. | Hoàn thành |
| 30/01/2026 | Setup CloudFront; kết nối CloudFront -> S3; test load web nhanh hơn. | Hoàn thành |
| 31/01/2026 | Setup Route 53; trỏ domain về CloudFront; test domain hoạt động (ims.mom). | Hoàn thành |


### Kết quả đạt được tuần 4:

* Hoàn thiện lớp dữ liệu backend với kết nối ECS -> RDS ổn định.
* Nâng mức bảo mật bằng cách chuyển thông tin nhạy cảm sang Secrets Manager.
* Hoàn tất tuyến phân phối frontend: S3 + CloudFront + Route 53.
* Đạt luồng truy cập gần production từ domain đến CDN và frontend tĩnh.




