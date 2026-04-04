---
title: "5.3 VPC & Networking cho hệ thống IMS"
weight: 3

---

VPC & Networking cho hệ thống Quản lý Sản xuất AI (IMS)

Trong module này, bạn sẽ thiết kế **nền tảng mạng** cho hệ thống Quản lý Sản xuất AI (IMS).

Bạn sẽ ánh xạ kiến trúc hệ thống vào một **VPC** duy nhất (ví dụ `vpc-ims`, CIDR `12.0.0.0/16`) với **hai public subnet và ba private subnet** trải trên các Availability Zone `ap-southeast-1a` và `ap-southeast-1b`, và xác định vị trí đặt **Application Load Balancer, các service ECS và RDS**.

#### Mục tiêu học tập

- Hiểu cách kiến trúc IMS được triển khai trong **AWS VPC** với public subnet và private subnet.
- Đặt **ALB, các ECS task và RDS** vào đúng subnet và Availability Zone.
- Chuẩn bị lớp mạng để các module sau (ECS, RDS, S3/CloudFront, messaging) có thể triển khai một cách an toàn.

#### Các phần trong module

1. [VPC cơ bản – CIDR & Subnet](5.2.1-vpc-basics/)
2. [Routing, Internet Gateway & NAT](5.2.2-routing-egress/)
3. [Biên giới bảo mật – Security Group, NACL & IAM](5.2.3-security-boundaries/)
4. [Kết nối dịch vụ – ECS, RDS, S3 & Messaging](5.2.4-service-connectivity/)
