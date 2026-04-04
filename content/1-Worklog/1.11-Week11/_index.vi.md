---
title: "Worklog Tuần 11"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 11:

* Hoàn thiện sơ đồ kiến trúc hệ thống sau tối ưu.
* Tiếp tục tinh chỉnh hiệu năng và độ ổn định của hệ thống.
* Kiểm tra lại full flow sau các thay đổi cuối cùng.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                   | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Rà soát lại kiến trúc hiện tại so với bản triển khai thực tế <br> - Kiểm tra các kết nối dịch vụ và tối ưu các điểm còn yếu                                                                                             | 23/03/2026   | 23/03/2026      | Kiểm tra nội bộ |
| 3   | - Tinh chỉnh lại CloudFront, ALB, ECS và RDS nếu cần <br> - Xác nhận quyền truy cập secret và quyền runtime                                                                                                             | 24/03/2026   | 24/03/2026      | AWS Docs        |
| 4   | - Vẽ lại sơ đồ kiến trúc hệ thống cuối cùng <br> - Cập nhật tài liệu cho khớp với hệ thống đã tối ưu                                                                                                                     | 25/03/2026   | 25/03/2026      | draw.io + AWS Docs |
| 5   | - Chạy test smoke cuối cùng cho frontend, backend, AI và database <br> - Kiểm tra log và độ ổn định sau tối ưu                                                                                                          | 26/03/2026   | 26/03/2026      | Kế hoạch test nội bộ |
| 6   | - Tổng hợp kết quả tối ưu và thay đổi kiến trúc <br> - Chuẩn bị ghi chú bàn giao cuối cùng                                                                                                                                | 27/03/2026   | 27/03/2026      | Báo cáo nội bộ   |


### Kết quả đạt được tuần 11:

* Hoàn thiện sơ đồ kiến trúc và đồng bộ với hệ thống triển khai thực tế.
* Hoàn thành đợt tinh chỉnh cuối cùng về hiệu năng và độ ổn định.
* Xác nhận lại các luồng chính sau cập nhật:
  * User → Domain → CloudFront → S3 (FE)
  * API → ALB → ECS (BE + AI)
  * ECS → RDS và ECS → Secrets Manager
* Kiểm tra log, hành vi runtime và độ ổn định sau tối ưu.
* Chuẩn bị xong phần ghi chú bàn giao cuối dự án.





