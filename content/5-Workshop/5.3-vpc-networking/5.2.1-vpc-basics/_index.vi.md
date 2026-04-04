---
title: "5.3.1 VPC cơ bản – CIDR & Subnet"
date: 2026-01-01
weight: 2
chapter: false
---

# 5.3.1 VPC cơ bản – CIDR & Subnet

Trong bước này, bạn tạo **VPC và các subnet** để chạy hệ thống Quản lý Sản xuất AI.

Đối với workshop, ta sử dụng một VPC tương tự môi trường thật của bạn:

- Tên VPC: `vpc-ims`
- CIDR block: `12.0.0.0/16`
- Availability Zone: `ap-southeast-1a` và `ap-southeast-1b`
- Subnet:
  - **Public-Subnet1** tại `ap-southeast-1a` – `12.0.1.0/24`
  - **Public-Subnet2** tại `ap-southeast-1b` – `12.0.2.0/24`
  - **Private-Subnet1** tại `ap-southeast-1a` – `12.0.3.0/24`
  - **Private-Subnet2** tại `ap-southeast-1a` – `12.0.4.0/24`
  - **Private-Subnet-5** tại `ap-southeast-1b` – `12.0.5.0/24`

#### Tại sao quan trọng?

- Public subnet chỉ dùng để expose **điểm vào (ALB / NAT Gateway)** ra Internet.
- Private subnet giúp **container ứng dụng và database** không bị truy cập trực tiếp từ Internet.
- Dùng hai AZ giúp tăng availability cho entry point frontend và backend services.

#### Sơ đồ: layout VPC IMS

![Sơ đồ VPC IMS với public và private subnet trên nhiều AZ](/images/5-Workshop/5.3-vpc-networking/VPC.png)

#### Bài tập workshop

- Tạo hoặc kiểm tra một VPC với CIDR `12.0.0.0/16` và các subnet như trên.
- Gắn tag subnet rõ ràng (ví dụ `ims-public-1a`, `ims-public-1b`, `ims-private-1a`, `ims-private-1a-extra`, `ims-private-1b`).
- Sau này gắn các private subnet này cho ECS cluster và RDS subnet group.
