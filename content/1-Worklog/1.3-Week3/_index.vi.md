---
title: "Worklog Tuần 3"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}}
⚠️ **Lưu ý:** Các thông tin dưới đây chỉ nhằm mục đích tham khảo, vui lòng **không sao chép nguyên văn** cho bài báo cáo của bạn kể cả warning này.
{{% /notice %}}


### Mục tiêu tuần 3:

* Bắt đầu tích hợp AI vào backend và xây dựng API phục vụ web.
* Container hóa backend + AI và chuẩn bị pipeline deploy.
* Triển khai dịch vụ lên ECS, kết nối qua ALB.
* Hoàn thiện nền tảng mạng VPC để workload private có thể truy cập internet an toàn.

### Các công việc cần triển khai trong tuần này:
| Ngày | Công việc | Trạng thái |
| --- | --- | --- |
| 19/01/2026 | Bắt đầu tích hợp AI vào backend; viết API để gọi AI từ web; test API local bằng Postman. | Hoàn thành |
| 20/01/2026 | Container hóa AI + backend bằng Docker; build image và chạy thử local; chuẩn bị deploy lên server. | Hoàn thành |
| 21/01/2026 | Tìm hiểu và push Docker image lên Amazon ECR; test pull image từ server. | Hoàn thành |
| 22/01/2026 | Setup ECS; deploy container backend + AI lên ECS; test chạy service lần đầu. | Hoàn thành |
| 23/01/2026 | Tạo ALB; kết nối ALB -> ECS; test truy cập backend qua ALB. | Hoàn thành |
| 24/01/2026 | Cấu hình VPC hoàn chỉnh: public subnet (ALB, NAT Gateway), private subnet (ECS, RDS); setup routing table. | Hoàn thành |
| 25/01/2026 | Setup IGW cho public subnet; setup NAT Gateway để ECS private gọi internet; test ECS gọi API ngoài (OpenAI/AI service). | Hoàn thành |


### Kết quả đạt được tuần 3:

* Hoàn thành tích hợp bước đầu AI vào backend và xác thực API local.
* Xây dựng được pipeline triển khai container: Docker -> ECR -> ECS.
* Triển khai thành công truy cập backend thông qua ALB.
* Hoàn thiện nền tảng mạng VPC public/private và luồng outbound internet cho ECS.




