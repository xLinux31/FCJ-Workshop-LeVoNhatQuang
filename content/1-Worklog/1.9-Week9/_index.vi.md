---
title: "Worklog Tuần 9"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 9:

* Vẽ architecture tổng thể các dịch vụ AWS đã sử dụng trong dự án.
* Rà soát và tối ưu hệ thống theo các tiêu chí hiệu năng, ổn định, chi phí.
* Kiểm thử lại full flow sau tối ưu và hoàn thiện tài liệu kỹ thuật.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                                                                          | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu       |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | --------------- | -------------------- |
| 2   | - Thống kê toàn bộ dịch vụ AWS đang dùng <br> - Gom nhóm theo layer: Edge, Frontend, Application, Data, Security, Monitoring <br> - Phác thảo architecture version 1                                                                                                 | 09/03/2026   | 09/03/2026      | AWS Docs             |
| 3   | - Vẽ architecture chính thức cho workshop stack <br> - Xác nhận luồng truy cập CloudFront → S3 và ALB → ECS <br> - Xác nhận luồng dữ liệu/bảo mật ECS → RDS, ECS → Secrets Manager                                                                                | 10/03/2026   | 10/03/2026      | draw.io + AWS Docs   |
| 4   | - Tối ưu frontend delivery: CloudFront cache policy, compression, fallback trang lỗi <br> - Tối ưu health check ALB/ECS và startup grace period <br> - Điều chỉnh CPU/memory task ECS và cấu hình rolling deployment                                             | 11/03/2026   | 11/03/2026      | AWS Docs             |
| 5   | - Tối ưu đường DB: connection management, rà soát query/index, timeout <br> - Rà soát IAM least privilege cho ECS task role và quyền đọc secret <br> - Bổ sung/chỉnh cảnh báo giám sát bằng CloudWatch metrics + logs                                              | 12/03/2026   | 12/03/2026      | AWS Docs             |
| 6   | - Chạy test tải nhẹ + test chức năng sau tối ưu <br> - So sánh chỉ số trước/sau (latency, error rate, response time) <br> - Hoàn thiện báo cáo architecture và kết quả tối ưu                                                                                       | 13/03/2026   | 13/03/2026      | Kế hoạch test nội bộ |


### Kết quả đạt được tuần 9:

* Đã hoàn thiện sơ đồ architecture AWS của hệ thống đang triển khai.
* Mô tả rõ luồng dịch vụ giữa lớp edge, app, data và lớp quản lý secret.
* Đã áp dụng các tối ưu quan trọng:
	* Tối ưu cache + nén CloudFront cho frontend tĩnh.
	* Tinh chỉnh health check ALB/ECS để giảm false alarm.
	* Cân chỉnh tài nguyên task ECS và cấu hình rolling deploy an toàn hơn.
	* Rà soát truy cập RDS, query/index và timeout cho độ ổn định tốt hơn.
	* Siết quyền IAM và truy cập Secrets Manager theo nguyên tắc least privilege.
* Đã kiểm thử full flow sau tối ưu:
	* User → Domain → CloudFront → S3 (FE)
	* API → ALB → ECS (BE + AI)
	* ECS → RDS và ECS → Secrets Manager
* Kết quả thực tế: hệ thống phản hồi ổn định hơn, giảm gián đoạn khi deploy.



