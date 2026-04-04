---
title: "5.8 Lớp AI phân tích sản xuất"
weight: 1
---

## Lớp AI phân tích sản xuất

Phần này trình bày cách tích hợp AI vào hệ thống IMS để cung cấp
các insight và phân tích bằng ngôn ngữ tự nhiên trên dữ liệu sản xuất.

## Mục tiêu sử dụng AI trong IMS

Lớp AI giúp manager và kỹ sư:
- Nắm nhanh tình trạng sức khoẻ các line sản xuất.
- Phát hiện trễ và nút thắt cổ chai.
- Tóm tắt dashboard phức tạp thành báo cáo ngắn gọn cho lãnh đạo.
- Trả lời linh hoạt các câu hỏi về đơn hàng, lịch, OEE, trễ, v.v.

Ví dụ câu hỏi hệ thống có thể trả lời:
- "Công đoạn nào đang gây trễ kế hoạch tuần này?"
- "Hôm nay OEE của line SMT 1 là bao nhiêu?"
- "Những đơn hàng nào có nguy cơ trễ deadline?"

## Nguồn dữ liệu

Lớp AI sử dụng dữ liệu lưu trong **Amazon RDS**, bao gồm:
- Đơn hàng và lệnh sản xuất.
- Lịch sản xuất và log thực tế.
- Chỉ số hiệu suất line (OEE, throughput, downtime).
- Lịch sử trễ và sự cố.

Service backend sẽ tổng hợp dữ liệu này thành context có cấu trúc trước khi gửi
cho mô hình ngôn ngữ (LLM).

## Service AI phía backend

Trong backend Spring Boot, AI thường được hiện thực thông qua các service như:
- `AIProductionAnalysisService`
- `ProductionAnalysisService`

Các service này:
- Truy vấn dữ liệu sản xuất từ RDS.
- Xây dựng context cô đọng (dạng JSON hoặc bullet points).
- Gọi API AI bên ngoài (ví dụ OpenAI) với API key lưu trong **AWS Secrets Manager**.
- Xử lý lại kết quả trả về thành text thân thiện hoặc JSON cấu trúc cho frontend.

## Bảo mật & Chi phí

- **Secrets**: Không hard-code API key; luôn lấy từ Secrets Manager bằng quyền của ECS task.
- **Quyền riêng tư**: Hạn chế gửi dữ liệu cá nhân/nhạy cảm không cần thiết cho dịch vụ AI.
- **Chi phí**: Giới hạn tần suất request và kích thước context.
- **Timeout & Retry**: Cấu hình timeout/hành vi retry hợp lý để app không bị treo
  khi dịch vụ AI phản hồi chậm.

## Tích hợp frontend

Frontend React gọi các endpoint AI thông qua `aiService` và hiển thị:
- Tóm tắt ngôn ngữ tự nhiên (ví dụ "Production health summary for today").
- Highlight các rủi ro (đơn hàng trễ, line quá tải).
- Gợi ý hành động tiếp theo cho manager.

Khi kết hợp dữ liệu sản xuất (deterministic) với lớp AI tóm tắt, hệ thống IMS
mang lại cách nhìn trực quan hơn cho người dùng không chuyên kỹ thuật
khi theo dõi tình trạng nhà máy.
