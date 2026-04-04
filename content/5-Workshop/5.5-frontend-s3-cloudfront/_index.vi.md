---
title: "Frontend với S3 & CloudFront"
weight: 1
---

## Triển khai Frontend với S3 & CloudFront

Phần này hướng dẫn bạn build và deploy frontend React trong thư mục `frontend/`
sử dụng Amazon S3 và Amazon CloudFront.

## Chức năng frontend

Ứng dụng React cung cấp các màn hình:
- Đăng nhập và điều hướng theo vai trò (Admin / Manager / Line Leader).
- Quản lý đơn hàng và xem chi tiết đơn hàng.
- Xem kế hoạch sản xuất, lịch line và một số dashboard cơ bản.
- Truy cập trang AI insights (qua `aiService`) để xem tóm tắt, phân tích tình trạng sản xuất.

## Sơ đồ kiến trúc frontend

![Bucket S3 host website frontend IMS](/images/5-Workshop/5.5-frontend-s3-cloudfront/s3.png)

![CloudFront đứng trước S3 làm CDN](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront.png)
![Cấu hình behavior và cache của CloudFront](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront1.png)
![Chi tiết distribution CloudFront và domain name](/images/5-Workshop/5.5-frontend-s3-cloudfront/CloudFront2.png)

## Build frontend

1. Cài đặt dependency:
   - `npm install`
2. Cấu hình API base URL (ví dụ bằng biến môi trường `VITE_API_BASE_URL`).
3. Build bản production:
   - `npm run build`
4. Kiểm tra thư mục `dist/` (hoặc tương đương) chứa các file static.

## Host trên Amazon S3

1. Tạo S3 bucket dành riêng cho frontend (ví dụ `ims-frontend-prod`).
2. Bật static website hosting (hoặc cấu hình origin access control nếu muốn private bucket).
3. Upload toàn bộ nội dung thư mục `dist/` lên S3 bucket.
4. Cấu hình `index document` (ví dụ `index.html`) và `error document` để hỗ trợ SPA routing.

## Phân phối qua CloudFront

1. Tạo **CloudFront distribution** với origin là S3 bucket chứa frontend.
2. Thiết lập default root object là `index.html`.
3. Cấu hình cache và (tuỳ chọn) custom error để SPA luôn trả `index.html` khi 404.
4. Gắn **ACM certificate** và domain riêng (qua Route 53) nếu cần HTTPS.

## Tích hợp API & CORS

- Đảm bảo frontend gọi backend API với đúng base URL (ALB DNS hoặc domain tuỳ chỉnh).
- Cấu hình CORS ở backend (và/hoặc ALB) cho phép domain CloudFront truy cập.
- Ở môi trường production, tránh hard-code URL; dùng biến môi trường build.

Kết thúc phần này, frontend React sẽ truy cập được qua URL CloudFront hoặc domain tuỳ chỉnh,
đóng vai trò cổng vào chính của hệ thống IMS.
