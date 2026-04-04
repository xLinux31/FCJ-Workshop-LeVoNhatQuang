---
title: "5.3.3 Security Boundaries – Security Groups, NACLs & IAM"
date: 2026-01-01
weight: 3
chapter: false
---

This section defines how traffic is allowed between components, and how networking security relates to IAM and secrets.

#### What you configure

- **Security groups** for:
  - Application Load Balancer: allow HTTP/HTTPS from the Internet.
  - ECS service: allow traffic only from the ALB security group.
  - RDS PostgreSQL: allow traffic only from the ECS service security group.
- Optional **network ACLs** (NACLs) – keep them simple, using default allow rules for the workshop.
- The relationship between **network boundaries** and **identity boundaries**:
  - Security groups / NACLs: control who can talk at the **network level**.
  - IAM roles & policies: control which **AWS APIs** ECS tasks can call (ECR, S3, SQS, SNS, SES, Secrets Manager, CloudWatch).
  - **Secrets Manager + KMS**: store and encrypt DB credentials, SMTP/SES secrets, and other sensitive configuration.

#### Workshop tasks

- Create security groups for ALB, ECS service, and RDS and wire them together.
- Verify that the database is only reachable from ECS tasks, not from the Internet.
- Link forward to the detailed IAM and secrets configuration in module `6.6-auth-security-secrets`.
