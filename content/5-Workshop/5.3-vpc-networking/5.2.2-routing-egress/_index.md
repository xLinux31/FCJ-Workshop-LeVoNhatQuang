---
title: "5.3.2 Routing, Internet Gateway & NAT"
date: 2026-01-01
weight: 2
chapter: false
---

Here you configure how traffic flows in and out of the VPC.

In the `vpc-ims` environment, routing is organized as:

- **Internet Gateway:** `igw-ims` attached to `vpc-ims`.
- **Public route table:** `rt-public` associated with the two public subnets and routing `0.0.0.0/0 → igw-ims`.
- **Private route table:** `rt-private` associated with the three private subnets and routing `0.0.0.0/0 → nat-ims`.
- **NAT gateway:** `nat-ims` in a public subnet for outbound Internet from private subnets.

#### Why this matters

- The Application Load Balancer and NAT gateway need Internet access through the IGW.
- ECS tasks in private subnets must reach external services (ECR image pulls, external APIs, SES/SNS/SQS) **without being publicly reachable**.

#### Workshop tasks

- Create or verify the **Internet Gateway** `igw-ims` and attach it to the VPC.
- Create/verify `rt-public` and `rt-private` and associate them with the right subnets.
- Ensure `rt-public` sends `0.0.0.0/0` to `igw-ims` and `rt-private` sends `0.0.0.0/0` to the `nat-ims` NAT gateway.
