---
title: "Worklog Tuần 10"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 10:

* Tiếp tục tối ưu hệ thống để tăng hiệu năng và độ ổn định.
* Rà soát và vẽ lại sơ đồ kiến trúc hệ thống AWS.
* Kiểm tra lại luồng hoạt động chính sau khi tối ưu.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Rà soát các điểm nghẽn hiệu năng ở frontend, backend và database <br> - Xác định các hạng mục cần tối ưu như cache, routing và tài nguyên dịch vụ                                             | 16/03/2026   | 16/03/2026      | Kiểm tra nội bộ |
| 3   | - Tinh chỉnh cấu hình CloudFront, ALB và ECS <br> - Điều chỉnh health check, timeout và triển khai service                                                                                                     | 17/03/2026   | 17/03/2026      | AWS Docs        |
| 4   | - Rà soát query RDS, kết nối database và luồng đọc secret <br> - Điều chỉnh IAM theo nguyên tắc least privilege nếu cần                                                                                         | 18/03/2026   | 18/03/2026      | AWS Docs        |
| 5   | - Vẽ lại sơ đồ kiến trúc hệ thống theo trạng thái thực tế <br> - Xác nhận các luồng dịch vụ: CloudFront → S3, ALB → ECS, ECS → RDS, ECS → Secrets Manager                                                             | 19/03/2026   | 19/03/2026      | draw.io + AWS Docs |
| 6   | - Chạy smoke test sau tối ưu <br> - Ghi nhận log và so sánh trước/sau tối ưu <br> - Hoàn thiện ghi chú để đưa vào báo cáo                                                                                         | 20/03/2026   | 20/03/2026      | Kế hoạch test nội bộ |


### Kết quả đạt được tuần 10:

* Tăng độ ổn định hệ thống nhờ tinh chỉnh các thành phần chính của kiến trúc.
* Tối ưu CloudFront, ALB, ECS và đường truy cập database.
* Vẽ lại sơ đồ kiến trúc AWS khớp với hệ thống đang triển khai.
* Xác nhận lại luồng hoạt động chính sau tối ưu:
  * User → Domain → CloudFront → S3 (FE)
  * API → ALB → ECS (BE + AI)
  * ECS → RDS và ECS → Secrets Manager
* Đã lưu log và ghi chú kiểm thử phục vụ báo cáo cuối kỳ.




