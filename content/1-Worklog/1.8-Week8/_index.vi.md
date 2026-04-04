---
title: "Worklog Tuần 8"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---


### Mục tiêu tuần 7:

* Fix lỗi network giữa ECS và internet.
* Hoàn thiện kiến trúc mục tiêu:
	* CloudFront → S3 (Frontend)
	* ALB → ECS (Backend + AI)
	* ECS → RDS
	* ECS → Secrets Manager
* Test full flow end-to-end:
	* User → domain → web → AI → DB

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                                                | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu       |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | -------------------- |
| 2   | - Điều tra và reproduce lỗi ECS không ra internet <br> - Kiểm tra route table, NAT Gateway/Internet Gateway, NACL, Security Group                                                                    | 02/03/2026   | 02/03/2026      | AWS Docs             |
| 3   | - Áp dụng fix network cho ECS private subnet <br> - Test lại outbound call và health check                                                                                                             | 03/03/2026   | 03/03/2026      | AWS Docs             |
| 4   | - Hoàn thiện luồng frontend CloudFront → S3 <br> - Kiểm tra domain và HTTPS                                                                                                                            | 04/03/2026   | 04/03/2026      | AWS Docs             |
| 5   | - Hoàn thiện luồng backend ALB → ECS (BE + AI) <br> - Xác nhận kết nối ECS tới RDS                                                                                                                     | 05/03/2026   | 05/03/2026      | AWS Docs             |
| 6   | - Kiểm tra ECS đọc secret từ Secrets Manager <br> - Chạy test full flow: User → domain → web → AI → DB                                                                                                | 06/03/2026   | 06/03/2026      | Kế hoạch test nội bộ |


### Kết quả đạt được tuần 7:

* Đã fix lỗi ECS không outbound internet bằng cách hiệu chỉnh route và security phù hợp.
* Xác nhận luồng network ổn định để ECS truy cập các dịch vụ bên ngoài khi runtime.
* Hoàn thiện frontend deployment với CloudFront phân phối nội dung tĩnh từ S3.
* Hoàn thiện backend routing với ALB điều hướng request vào ECS (BE + AI).
* Kết nối ECS ↔ RDS hoạt động ổn định cho thao tác đọc/ghi dữ liệu.
* ECS lấy secret runtime từ Secrets Manager đúng quyền và đúng giá trị.
* Test end-to-end thành công theo luồng:
	* User → domain → web → AI → DB
* Đã lưu log và bằng chứng test phục vụ nghiệm thu, bàn giao.


