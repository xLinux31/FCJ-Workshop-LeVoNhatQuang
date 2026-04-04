---
title: "Worklog Tuần 5"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 5:

* Khắc phục lỗi tổng thể để ổn định hệ thống.
* Củng cố bảo mật mạng bằng cấu hình Security Group theo đúng vai trò dịch vụ.
* Đảm bảo luồng truy cập giới hạn đúng kiến trúc: ALB -> ECS -> RDS.
* Kiểm thử lại các rule bảo mật sau khi cập nhật.

### Các công việc cần triển khai trong tuần này:
| Giai đoạn | Công việc | Trạng thái |
| --- | --- | --- |
| 01/02/2026 - 03/02/2026 | Fix bug hệ thống tổng thể. | Hoàn thành |
| 04/02/2026 - 06/02/2026 | Cấu hình Security Group: ALB mở port 80/443; ECS chỉ nhận từ ALB; RDS chỉ nhận từ ECS; test bảo mật. | Hoàn thành |


### Kết quả đạt được tuần 5:

* Khắc phục các lỗi chính giúp hệ thống vận hành ổn định hơn.
* Thiết lập phân tách truy cập mạng theo đúng vai trò từng tầng dịch vụ.
* Đảm bảo luồng truy cập bảo mật: ALB -> ECS -> RDS.
* Hoàn tất kiểm thử rule ingress và xác thực chính sách bảo mật đang hoạt động đúng.




