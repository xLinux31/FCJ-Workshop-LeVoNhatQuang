---
title: "Workshop"
date: 2026-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "

---

## AI Production Management System on AWS – Workshop

This workshop walks through the end‑to‑end design and deployment of an **AI‑Assisted Electronics Production Management System** on AWS.

The system is a real project combining:
- **Backend:** Spring Boot (containerized) running on Amazon ECS Fargate
- **Frontend:** React (Vite) hosted on Amazon S3 and served via Amazon CloudFront
- **Database:** Amazon RDS (PostgreSQL)
- **Infrastructure & Security:** VPC, subnets, security groups, IAM, AWS Secrets Manager, AWS KMS
- **Messaging & Notifications:** Amazon SQS, Amazon SNS, Amazon SES (OTP & alerts)
- **Observability:** Amazon CloudWatch Logs, Metrics, Dashboards, and Alarms

You will see how the architecture from the proposal and architecture diagrams is implemented in practice, from networking and containers to monitoring and alerting.

#### What You Will Learn

By the end of this workshop, you will be able to:

- Design a **VPC‑based architecture** with public/private subnets, ALB, ECS services, and RDS.
- Build and package the Spring Boot backend as a Docker image and push it to **Amazon ECR**.
- Deploy the backend to **Amazon ECS Fargate** behind an **Application Load Balancer**.
- Build the React frontend and deploy it to **Amazon S3 + CloudFront + Route 53** with HTTPS.
- Use **Amazon SQS** and **Amazon SNS** to decouple background tasks and alerts.
- Integrate **Amazon SES** to send OTP emails and production alerts.
- Apply security best practices with **IAM roles**, an IAM user for SES, **Secrets Manager**, and **KMS** encryption.
- Configure **CloudWatch Logs**, **metrics**, **dashboards**, and **alarms** (e.g., ECS CPU > 80%) to monitor the system.

#### Target Audience

- Students and engineers who want a concrete example of a production‑style web system on AWS.
- Developers familiar with basic AWS concepts (EC2/ECS, S3, IAM) and web development (Java/Spring, React).

#### Workshop Modules

This workshop is organized into the following sections (see subfolders under `5-Workshop/`):

1. **[System & Workshop Overview](5.1-overview/)** – business context of the IMS system and how the hands‑on lab is organized.
2. **[Solution Architecture & IaC](5.2-architecture-iac/)** – overall IMS architecture on AWS and (optional) infrastructure‑as‑code.
3. **[VPC & Networking](5.3-vpc-networking/)** – VPC, subnets, routing, Internet/NAT gateways, security groups, and connectivity to AWS services.
4. **[Backend on ECS & RDS](5.4-backend-ecs-rds/)** – Spring Boot containers, ECR repository, ECS task definitions/services, and PostgreSQL schema.
5. **[Frontend on S3 & CloudFront](5.5-frontend-s3-cloudfront/)** – React build pipeline, S3 static hosting, CloudFront distribution, and domain configuration.
6. **[Messaging & Notifications (SQS/SNS/SES)](5.6-messaging-notifications-sqs-sns-ses/)** – SQS queues, SNS topics, and SES email/OTP flows.
7. **[Auth & Secrets](5.7-auth-security-secrets/)** – IAM roles, SES IAM user, Secrets Manager, KMS, and application security patterns.
8. **[AI & Production Analytics](5.8-ai-production-analytics/)** – how production data (orders, lines, delays, OEE) feeds into AI assistants and reporting.
9. **[Observability & CI/CD](5.9-observability-ci-cd/)** – CloudWatch logs/metrics/alarms, dashboards, and the buildspec/CodeBuild–ECR–ECS deployment pipeline.

Each section connects directly to the running code in this repository (`backend/` and `frontend/`) and to the AWS resources described in **Idea for AWS project** and **2‑Proposal**.
