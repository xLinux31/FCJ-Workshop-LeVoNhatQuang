---
title: "5.3.2 Routing, Internet Gateway & NAT"
date: 2026-01-01
weight: 2
chapter: false
---

Trong bước này, bạn cấu hình cách traffic đi vào và ra khỏi VPC.

Trong môi trường `vpc-ims`, routing được tổ chức như sau:

- **Internet Gateway:** `igw-ims` gắn với `vpc-ims`.
- **Public route table:** `rt-public` gắn với hai public subnet và route `0.0.0.0/0 → igw-ims`.
- **Private route table:** `rt-private` gắn với ba private subnet và route `0.0.0.0/0 → nat-ims`.
- **NAT gateway:** `nat-ims` nằm trong một public subnet, dùng cho outbound Internet từ private subnet.

#### Tại sao quan trọng?

- Application Load Balancer và NAT gateway cần Internet access thông qua IGW.
- ECS task trong private subnet phải truy cập được các dịch vụ bên ngoài (ECR, API ngoài, SES/SNS/SQS) **mà không bị public**.

#### Bài tập workshop

- Tạo/kiểm tra **Internet Gateway** `igw-ims` và gắn với VPC.
- Tạo/kiểm tra `rt-public` và `rt-private`, gắn đúng với các subnet.
- Đảm bảo `rt-public` route `0.0.0.0/0` tới `igw-ims` và `rt-private` route `0.0.0.0/0` tới NAT gateway `nat-ims`.
