---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---


# Hệ Thống Quản Lý Sản Xuất Điện Tử Hỗ Trợ AI
## (Nền tảng hợp nhất trên AWS cho lập kế hoạch & giám sát sản xuất)

### 1. Tóm tắt điều hành
Hệ thống Quản lý Sản xuất hỗ trợ AI được thiết kế cho các doanh nghiệp sản xuất điện tử vừa và nhỏ (SME) nhằm nâng cao quản lý đơn hàng, lập kế hoạch và giám sát sản xuất.
Hệ thống hỗ trợ nhiều dây chuyền (SMT, DIP, kiểm tra) với khả năng mở rộng khi số lượng đơn hàng và dây chuyền tăng. Nền tảng cho phép quản lý dữ liệu sản xuất tập trung, trực quan hóa tiến độ và phát hiện sớm các chậm trễ trên từng công đoạn.
Giải pháp tận dụng các dịch vụ AWS như ECS, ECR, RDS, S3, CloudFront, Route 53, CloudWatch, Secrets Manager, SNS, SQS, SES để đảm bảo hệ thống ổn định, bảo mật, dễ mở rộng và tối ưu chi phí.

Ngoài ra, hệ thống tích hợp thành phần AI để hỗ trợ người dùng tra cứu nhanh thông tin liên quan đến đơn hàng, lịch sản xuất (schedule), các chỉ số OEE, biểu đồ Gantt và các tình huống chậm trễ đơn giản. Người dùng có thể đặt các câu hỏi tự nhiên như "đơn hàng X đang ở công đoạn nào?", "dây chuyền SMT 1 hôm nay OEE bao nhiêu?", "công đoạn nào đang gây trễ cho kế hoạch tuần này?" và nhận được câu trả lời dựa trên dữ liệu sản xuất đã được thu thập và tổng hợp.

### 2. Tuyên bố vấn đề
#### Vấn đề đặt ra
Trong các doanh nghiệp sản xuất điện tử SME, bài toán hiện tại thường gặp:
- Lập kế hoạch sản xuất thủ công bằng Excel, khó tối ưu dây chuyền và công suất.
- Không có khả năng theo dõi tiến độ sản xuất theo thời gian thực trên từng công đoạn.
- Dữ liệu đơn hàng, lệnh sản xuất và báo cáo phân tán ở nhiều file, nhiều hệ thống.
- Khó đánh giá năng lực dây chuyền, thời gian chờ và các điểm nghẽn trong quy trình.
- Hệ thống nội bộ khó mở rộng, phụ thuộc vào hạ tầng on-premise, thiếu cơ chế giám sát tập trung.

#### Giải pháp
Hệ thống cung cấp nền tảng web tập trung để quản lý và thống kê sản xuất:
- Backend xử lý logic nghiệp vụ (đơn hàng, lệnh sản xuất, kế hoạch, báo cáo) chạy dưới dạng container trên ECS.
- Giao diện web cho phép quản lý, theo dõi tiến độ, xem dashboard tình trạng dây chuyền.
- Dữ liệu nghiệp vụ được lưu trữ trên RDS với mô hình quan hệ, hỗ trợ truy vấn báo cáo.
- Các file tài liệu sản xuất (POM/SOOP, biểu mẫu) và artifact triển khai được lưu tách biệt trên 3 bucket S3.
- Tác vụ nền (ví dụ gửi thông báo, xử lý batch) sử dụng SQS để tách khỏi luồng chính.
- SNS và SES hỗ trợ gửi cảnh báo, thông báo email cho quản lý/kỹ thuật khi có sự cố.
- CloudWatch và Secrets Manager giúp giám sát, bảo mật thông tin kết nối và cấu hình hệ thống.
- Thành phần AI được tích hợp để truy vấn dữ liệu sản xuất theo ngôn ngữ tự nhiên, hỗ trợ người dùng xem nhanh tình trạng đơn hàng, lịch sản xuất, OEE, biểu đồ Gantt, điểm nghẽn và các chậm trễ đơn giản mà không cần tự lọc nhiều màn hình/báo cáo.

#### Lợi ích và hoàn vốn đầu tư
- Giảm thao tác thủ công trong quản lý và tổng hợp số liệu sản xuất.
- Cải thiện khả năng theo dõi tiến độ và phát hiện sớm chậm trễ trên dây chuyền.
- Tạo nguồn dữ liệu tập trung, phục vụ phân tích, báo cáo và áp dụng AI trong tương lai.
- Sử dụng hạ tầng AWS giúp giảm chi phí đầu tư ban đầu, trả theo mức sử dụng, dễ mở rộng khi quy mô nhà máy tăng.

### 3. Kiến trúc giải pháp
Hệ thống sử dụng kiến trúc cloud triển khai trên AWS.
Người dùng truy cập qua giao diện web được host trên Amazon S3 và phân phối qua CloudFront. Các request được định tuyến qua Amazon Route 53 đến backend chạy trên ECS. Backend xử lý dữ liệu và lưu trữ vào cơ sở dữ liệu quan hệ trên Amazon RDS.

Các file POM/SOOP và tài liệu liên quan được lưu trên một S3 bucket chuyên biệt; frontend được build và deploy lên một S3 bucket riêng; artifact và gói triển khai ứng dụng được lưu trên một S3 bucket khác để phục vụ quy trình deploy. Các tác vụ nền và xử lý bất đồng bộ sử dụng Amazon SQS, trong khi thông báo và cảnh báo sử dụng Amazon SNS và Amazon SES.

Thông tin nhạy cảm như thông tin đăng nhập database, API key, cấu hình email được quản lý an toàn bằng AWS Secrets Manager. Toàn bộ log, metric, cảnh báo được giám sát tập trung qua Amazon CloudWatch.

<img height="500" src="/images/2-Proposal/architecture.jpg" width="500" alt="Proposal Image"/>

#### Dịch vụ AWS sử dụng
- Amazon ECS: chạy backend quản lý sản xuất
- Amazon ECR: lưu trữ Docker image của các service backend
- Amazon RDS (PostgreSQL/MySQL): lưu dữ liệu sản xuất (đơn hàng, lệnh, kế hoạch, tiến độ)
- Amazon S3 (Bucket 1): lưu trữ file POM/SOOP và tài liệu sản xuất
- Amazon S3 (Bucket 2): host frontend (React app)
- Amazon S3 (Bucket 3): lưu artifact và gói triển khai ứng dụng
- Amazon CloudFront: phân phối frontend qua CDN
- Amazon Route 53: quản lý domain và định tuyến tên miền
- Amazon SES: gửi email (thông báo, cảnh báo, báo cáo định kỳ)
- Amazon SQS: hàng đợi cho tác vụ nền, xử lý batch, retry
- Amazon SNS: gửi thông báo/cảnh báo đến quản lý, tích hợp với kênh khác
- Amazon CloudWatch: giám sát log, metric, thiết lập alarm
- AWS Secrets Manager: lưu trữ thông tin nhạy cảm (DB password, API key)

#### Thiết kế thành phần
**Frontend**
- Host trên S3
- Phân phối qua CloudFront
- Cung cấp dashboard và giao diện quản lý sản xuất (đơn hàng, kế hoạch, dây chuyền)

**Backend**
- Chạy trên ECS dưới dạng container
- Xử lý logic nghiệp vụ: đơn hàng, lệnh sản xuất, lập lịch, báo cáo, API cho frontend
- Gửi/nhận message với SQS/SNS để xử lý tác vụ nền

**Database**
- RDS lưu đơn hàng, kế hoạch sản xuất, tiến độ, lịch sử sản xuất, báo cáo

**Lưu trữ file**
- S3 bucket POM/SOOP lưu tài liệu quy trình, hướng dẫn sản xuất
- S3 bucket frontend lưu mã build của ứng dụng web
- S3 bucket artifact lưu các gói triển khai, backup cấu hình

**Bảo mật & Giám sát**
- Secrets Manager lưu cấu hình nhạy cảm
- CloudWatch thu thập log, metric và gửi cảnh báo qua SNS/SES

### 4. Triển khai kỹ thuật
**Các giai đoạn triển khai**
Dự án phát triển qua 4 giai đoạn:
- Phân tích yêu cầu và thiết kế kiến trúc theo stack thực tế.
- Xây dựng backend container, push image lên ECR và triển khai ECS.
- Triển khai frontend lên S3 + CloudFront, cấu hình domain qua Route 53.
- Tích hợp RDS, SQS, SNS, SES, Secrets Manager và CloudWatch; kiểm thử tổng thể.

**Yêu cầu kỹ thuật**
**Yêu cầu hệ thống**
- Ứng dụng web cho người dùng cuối.
- Hỗ trợ lưu trữ nội dung hành trình và tài liệu đính kèm.
- Có cơ chế giám sát, cảnh báo và gửi email thông báo.

**Công nghệ sử dụng**
- Backend: Spring Boot (container hóa).
- Frontend: React.
- Database: Amazon RDS (PostgreSQL/MySQL).
- Cloud: AWS (S3, CloudFront, ECS, ECR, Route 53, CloudWatch, Secrets Manager, SNS, SQS, SES).

### 5. Lộ trình & Mốc triển khai
- Trước phát triển: Làm rõ phạm vi chức năng, thiết kế kiến trúc và chuẩn naming cho 3 bucket S3.
- Giai đoạn phát triển: Hoàn thiện backend trên ECS/ECR, tích hợp RDS, SQS, SNS, SES.
- Giai đoạn triển khai: Deploy frontend qua S3/CloudFront, kết nối domain Route 53.
- Sau triển khai: Theo dõi CloudWatch, tối ưu chi phí và hiệu năng theo dữ liệu thực tế.

### 6. Ước tính ngân sách
**Chi phí hạ tầng**
Hệ thống triển khai trên AWS với chi phí theo mức sử dụng thực tế cho quy mô nhỏ.
1. Compute (Amazon ECS)
    - Chạy backend container service.
    - Chi phí: ~ $6.00 / tháng
2. Container Registry (Amazon ECR)
    - Lưu trữ image và version deploy.
    - Chi phí: ~ $1.00 / tháng
3. Database (Amazon RDS)
    - Lưu dữ liệu nghiệp vụ ứng dụng.
    - Chi phí: ~ $12.00 / tháng
4. Storage (Amazon S3 - 3 buckets)
    - Bucket POM/SOOP, bucket frontend, bucket artifact/deploy.
    - Chi phí: ~ $2.00 / tháng
5. CDN (Amazon CloudFront)
    - Phân phối frontend và cache nội dung.
    - Chi phí: ~ $1.50 / tháng
6. DNS (Amazon Route 53)
    - Quản lý domain và định tuyến truy cập.
    - Chi phí: ~ $0.50 / tháng
7. Queue & Notification (Amazon SQS + SNS)
    - Xử lý tác vụ nền và cảnh báo sự kiện.
    - Chi phí: ~ $2.00 / tháng
8. Email Service (Amazon SES)
    - Gửi email thông báo/xác minh.
    - Chi phí: ~ $0.50 / tháng
9. AWS Secrets Manager
    - Lưu thông tin đăng nhập DB và secret ứng dụng.
    - Chi phí: ~ $0.80 / tháng
10. Monitoring (Amazon CloudWatch)
    - Log, metric, dashboard, alarm.
    - Chi phí: ~ $2.50 / tháng

**Tổng chi phí ước tính**
| Dịch vụ | Chi phí/tháng |
|---|---|
| ECS | $6.00 |
| ECR | $1.00 |
| RDS | $12.00 |
| S3 (3 buckets) | $2.00 |
| CloudFront | $1.50 |
| Route 53 | $0.50 |
| SQS + SNS | $2.00 |
| SES | $0.50 |
| Secrets Manager | $0.80 |
| CloudWatch | $2.50 |
| **Tổng** | **28.80** |

**Chi phí năm**
~ $345.6 / năm

**Chi phí phát triển**
- Không cần đầu tư máy chủ vật lý.
- Tận dụng mô hình cloud trả theo mức dùng.
- Dễ điều chỉnh ngân sách theo lưu lượng thực tế.

### 7. Đánh giá rủi ro
**Rủi ro**
- Tăng chi phí khi traffic tăng nhanh hoặc truy vấn RDS chưa tối ưu.
- Tồn đọng hàng đợi SQS trong giờ cao điểm.
- Lỗi cấu hình secret gây gián đoạn kết nối dịch vụ.

**Chiến lược giảm thiểu**
- Thiết lập CloudWatch alarm cho ECS, RDS, SQS, SES.
- Tối ưu truy vấn và index trên RDS.
- Áp dụng nguyên tắc phân quyền tối thiểu và quản lý secret tập trung.
- Cấu hình retry và theo dõi thông điệp lỗi trên hàng đợi.

**Kế hoạch dự phòng**
- Snapshot dữ liệu RDS định kỳ và kiểm thử restore.
- Duy trì version image ổn định trên ECR để rollback nhanh.
- Gửi cảnh báo tức thời qua SNS/email khi hệ thống vượt ngưỡng.

### 8. Kết quả kỳ vọng
**Cải tiến kỹ thuật**
- Hệ thống vận hành ổn định, tách lớp rõ ràng frontend/backend/data.
- Tăng khả năng mở rộng và tính sẵn sàng nhờ kiến trúc AWS container.
- Cải thiện khả năng quan sát và xử lý sự cố với CloudWatch + SNS + SES.
- Bổ sung lớp AI hỗ trợ hỏi đáp về đơn hàng, schedule, OEE, Gantt, chậm trễ đơn giản; giúp người dùng truy cập thông tin nhanh hơn và giảm phụ thuộc vào chuyên gia phân tích.

**Giá trị dài hạn**
- Tạo nền tảng kỹ thuật vững chắc cho việc mở rộng tính năng hệ thống quản lý và thống kê sản xuất, bao gồm cả các mô hình AI nâng cao trong tương lai (dự báo tải chuyền, tối ưu lịch, phân tích nguyên nhân chậm trễ).
- Chuẩn hóa quy trình deploy và vận hành cho các phiên bản tiếp theo.
- Tối ưu hiệu quả chi phí theo mức tăng trưởng người dùng.
