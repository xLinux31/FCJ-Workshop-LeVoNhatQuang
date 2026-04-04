---
title: "Worklog Tuần 12"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 1.12 </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}

### Mục tiêu tuần 12:

* Rà soát và vẽ lại sơ đồ kiến trúc AWS cho khớp với hệ thống đang triển khai.
* Tối ưu hệ thống để giảm tài nguyên dư thừa và hạn chế phát sinh chi phí.
* Kiểm tra lại luồng hoạt động chính sau khi cập nhật sơ đồ và tinh chỉnh hệ thống.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Rà soát mức sử dụng tài nguyên ở frontend, backend và database <br> - Xác định các phần có thể cắt giảm hoặc gom lại để giảm chi phí                                             | 30/03/2026   | 30/03/2026      | Kiểm tra nội bộ |
| 3   | - Tinh chỉnh cấu hình CloudFront, ALB và ECS <br> - Điều chỉnh scaling, health check và runtime để tránh cấp phát quá mức                                                                                                     | 31/03/2026   | 31/03/2026      | AWS Docs        |
| 4   | - Rà soát query RDS, kết nối database và luồng đọc secret <br> - Điều chỉnh IAM theo nguyên tắc least privilege và loại bỏ các quyền không cần thiết                                                                                         | 01/04/2026   | 01/04/2026      | AWS Docs        |
| 5   | - Vẽ lại sơ đồ kiến trúc hệ thống theo trạng thái thực tế <br> - Xác nhận các luồng dịch vụ: CloudFront → S3, ALB → ECS, ECS → RDS, ECS → Secrets Manager                                                             | 02/04/2026   | 02/04/2026      | draw.io + AWS Docs |
| 6   | - Chạy smoke test sau tối ưu <br> - Ghi nhận log và so sánh trước/sau tinh chỉnh, nhất là các điểm liên quan đến chi phí <br> - Hoàn thiện ghi chú để đưa vào báo cáo                                                                                         | 03/04/2026   | 03/04/2026      | Kế hoạch test nội bộ |


### Kết quả đạt được tuần 12:

* Cải thiện độ ổn định hệ thống đồng thời giảm tài nguyên sử dụng không cần thiết.
* Tối ưu CloudFront, ALB, ECS và đường truy cập database theo hướng tiết kiệm chi phí.
* Vẽ lại sơ đồ kiến trúc AWS khớp với hệ thống đang triển khai.
* Xác nhận lại luồng hoạt động chính sau tối ưu:
  * User → Domain → CloudFront → S3 (FE)
  * API → ALB → ECS (BE + AI)
  * ECS → RDS và ECS → Secrets Manager
* Đã lưu log và ghi chú kiểm thử phục vụ báo cáo cuối kỳ.

