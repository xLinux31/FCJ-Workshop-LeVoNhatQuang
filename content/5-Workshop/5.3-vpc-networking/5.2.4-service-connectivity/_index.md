---
title: "5.3.4 Service Connectivity – ECS, RDS, S3 & Messaging"
date: 2026-01-01
weight: 4
chapter: false
---

Finally, you connect AWS services to the VPC so that the application can work end‑to‑end.

#### What you connect

- **ECS Fargate service** in private subnets, fronted by the ALB in public subnets.
- **RDS PostgreSQL** in private subnets, reachable only from the ECS security group.
- Access from ECS tasks to:
  - **Amazon ECR** to pull container images.
  - **Amazon S3** for file storage.
  - **Amazon SQS/SNS** for background jobs and notifications.
  - **Amazon SES** for sending OTP and system emails.
  - **AWS Secrets Manager** to fetch DB credentials and SMTP/SES secrets.

#### ALB and Target Group

![Application Load Balancer in public subnets routing traffic to ECS](/images/5-Workshop/5.3-vpc-networking/ALB.png)

![Target Group for ECS service behind ALB](/images/5-Workshop/5.3-vpc-networking/TG.png)

These diagrams show how the ALB listens on public subnets and forwards traffic only to healthy ECS tasks in private subnets via the target group.

#### Network patterns

- Start with access via the **NAT gateway** to public AWS endpoints.
- Optionally, discuss **VPC endpoints** (S3, SQS, SNS, Secrets Manager, CloudWatch Logs) as a production-hardening step.

#### Workshop tasks

- Attach private subnets to the ECS cluster and RDS subnet group.
- Verify that ECS tasks can reach ECR, S3, SQS/SNS/SES, and Secrets Manager from private subnets.
- Cross-check how this networking layer supports later modules: backend on ECS/RDS, messaging & notifications, security, and observability.
