---
title: "5.2 Solution Architecture & IaC"
weight: 2
---

This section explains the overall architecture of the IMS system on AWS and how
you can provision it using Infrastructure-as-Code (IaC).

## Logical Architecture

At a high level, the system follows this flow:

1. **Browser / Frontend** – React SPA built from the `frontend/` folder.
2. **CDN & Static Hosting** – React build artifacts hosted on **Amazon S3** and served via **Amazon CloudFront**.
3. **DNS & Routing** – Custom domain managed in **Amazon Route 53**, pointing to CloudFront (frontend) and ALB (backend API).
4. **Backend API** – Spring Boot application from `backend/backend` packaged as a Docker image and run on **Amazon ECS (Fargate)** behind an **Application Load Balancer**.
5. **Database** – **Amazon RDS (PostgreSQL)** stores orders, production plans, line performance, and AI analysis results.
6. **File Storage** – Multiple **S3 buckets** for:
   - Frontend static assets.
   - Production documents (POM/SOOP, forms, attachments).
   - Deployment artifacts and backups.
7. **Messaging & Notifications** – **Amazon SQS** for background jobs, **Amazon SNS** and **SES** for alerts and emails.
8. **Security & Config** – **AWS Secrets Manager** for credentials and API keys, IAM roles for ECS tasks and CI/CD.
9. **Monitoring** – **Amazon CloudWatch** for logs, metrics, alarms, and dashboards.

## Mapping Repo to Architecture

- `backend/backend` → Docker image → ECS Task Definition → ECS Service → ALB Target Group.
- `frontend/` → Vite build output → S3 website bucket → CloudFront distribution.
- Database schema (Flyway migrations under `src/main/resources/db/migration/`) → Amazon RDS.
- Email template `otp-email.html` → SES-based OTP and notification flows.

## Infrastructure-as-Code Options

You can implement the above architecture in different ways:

- **Manual console setup** for learning step-by-step.
- **CloudFormation / AWS CDK** templates to define VPC, ECS, RDS, S3, CloudFront, etc.
- **Terraform** if you prefer a multi-cloud style IaC.

For this workshop, you can start with console + CLI to understand each component, then
optionally refactor into IaC templates as an extension.

## Difference from Serverless Workshop

Compared to the serverless Travel Guide app in `5-Workshop` (Lambda + API Gateway + DynamoDB):

- Here you run long-lived container services on **ECS Fargate** instead of short-lived Lambdas.
- You use a relational database (**RDS PostgreSQL**) instead of DynamoDB.
- You manage container images in **ECR** and deployments via ECS/ALB.

This architecture is closer to how many existing Spring Boot + React enterprise systems are migrated to AWS.
