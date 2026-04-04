---
title: "5.3.1 VPC Basics – CIDR & Subnets"
date: 2026-01-01
weight: 1
chapter: false
---

5.3.1 VPC Basics – CIDR & Subnets

In this step, you create the **VPC and subnets** that host the AI Production Management System.

For this workshop, we use a VPC similar to your real environment:

- VPC name: `vpc-ims`
- CIDR block: `12.0.0.0/16`
- Availability Zones: `ap-southeast-1a` and `ap-southeast-1b`
- Subnets:
  - **Public-Subnet1** in `ap-southeast-1a` – `12.0.1.0/24`
  - **Public-Subnet2** in `ap-southeast-1b` – `12.0.2.0/24`
  - **Private-Subnet1** in `ap-southeast-1a` – `12.0.3.0/24`
  - **Private-Subnet2** in `ap-southeast-1a` – `12.0.4.0/24`
  - **Private-Subnet-5** in `ap-southeast-1b` – `12.0.5.0/24`

#### Why this matters

- Public subnets expose only the **entry point (ALB / NAT Gateway)** to the Internet.
- Private subnets keep **application containers and database** isolated from direct public access.
- Using two AZs improves availability of the frontend entry point and backend services.

#### Diagram: IMS VPC layout

![IMS VPC with public and private subnets across AZs](/images/5-Workshop/5.3-vpc-networking/VPC.png)

#### Workshop tasks

- Recreate or verify a VPC with CIDR `12.0.0.0/16` and the subnets above.
- Tag subnets clearly (e.g., `ims-public-1a`, `ims-public-1b`, `ims-private-1a`, `ims-private-1a-extra`, `ims-private-1b`).
- Attach the private subnets later to the ECS cluster and RDS subnet group.
