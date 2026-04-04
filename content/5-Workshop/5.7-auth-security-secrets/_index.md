---
title: "5.7 Authentication, Security & Secrets"
weight: 7
---

## Authentication, Security & Secrets Management

This section describes how authentication, authorization, network security, and
secret management are handled in the IMS system.

## Security architecture diagrams

![IAM roles and permissions for ECS, CI/CD and SES](/images/5-Workshop/5.7-auth-security-secrets/IAM.png)

*Hình IAM cho phần IAM Roles & Permissions trong module 6.6.*

![Security group inbound rules for ALB](/images/5-Workshop/5.7-auth-security-secrets/sg-ALB-inbound.png)
![Security group outbound rules for ALB](/images/5-Workshop/5.7-auth-security-secrets/sg-ALB-outbound.png)

*Hai hình SG‑ALB dùng cho phần Network Security (ALB security group) của module 6.6.*

![Security group inbound rules for ECS tasks](/images/5-Workshop/5.7-auth-security-secrets/sg-ECS-inbound.png)
![Security group outbound rules for ECS tasks](/images/5-Workshop/5.7-auth-security-secrets/sg-ECS-outbound.png)

*Hai hình SG‑ECS dùng cho phần Network Security (ECS security group) của module 6.6.*

![Security group inbound rules for RDS](/images/5-Workshop/5.7-auth-security-secrets/sg-RDS-inbound.png)
![Security group outbound rules for RDS](/images/5-Workshop/5.7-auth-security-secrets/sg-RDS-outbound.png)

*Hai hình SG‑RDS dùng cho phần Network Security (RDS security group) của module 6.6.*

![Secrets Manager storing database and SMTP credentials](/images/5-Workshop/5.7-auth-security-secrets/secrete%20manager.png)
![KMS key protecting encrypted secrets](/images/5-Workshop/5.7-auth-security-secrets/KMS.png)

*Hai hình Secrets Manager và KMS cho phần Secrets Management & KMS trong module 6.6.*

![CloudWatch alarm as part of security and monitoring](/images/5-Workshop/5.7-auth-security-secrets/cloudwatch-alarm.png)

*Hình CloudWatch Alarm dùng chung cho phần Network Security/Monitoring của module 6.6 và liên kết với module 6.7 Observability & CI/CD.*

These diagrams show how IAM, security groups, Secrets Manager and KMS are configured to implement least-privilege access and protect sensitive data.

## Authentication & Authorization

- The backend uses **Spring Security** to protect APIs and enforce role-based access control.
- Main roles:
  - `ADMIN` – system administration features.
  - `MANAGER` – production planning and monitoring.
  - `LINE_LEADER` – shop-floor task execution.
- The frontend integrates with the auth APIs via `authService` and stores tokens client-side.

You can extend the current auth design by integrating **Amazon Cognito** as the identity provider:
- User Pool for user management and hosted login.
- JWT tokens issued by Cognito validated by Spring Boot.
- Fine-grained access via Cognito groups mapped to application roles.

### OTP and email verification

For password reset and account verification, the backend can expose endpoints like:
- `POST /auth/forgot-password` – generate a short-lived OTP, send via SES to the user email.
- `POST /auth/verify-otp` – validate the OTP and allow password change.

The OTP code and expiry timestamp should be stored server-side (for example in a database
table or cache such as Redis) and never embedded directly in JWTs.

## Network Security

- All services run inside a custom **VPC**.
- **Security Groups** restrict traffic:
  - ALB allows inbound HTTP/HTTPS from the internet.
  - ECS tasks accept traffic only from ALB.
  - RDS accepts traffic only from ECS tasks (and admin sources if needed).
- Private subnets are used for ECS and RDS, public subnets only for ALB and NAT gateways.

## IAM Roles & Permissions

IAM is used to give each component just enough access to AWS resources.

### ECS roles

- **ECS task execution role** (for example `ecsTaskExecutionRole-ims-prod`):
  - Used by the ECS agent, not by the application code.
  - Pulls container images from **ECR**.
  - Writes logs to **CloudWatch Logs**.
  - Typically attaches the managed policy `AmazonECSTaskExecutionRolePolicy`.

- **ECS task role** (for example `ecsTaskRole-ims-backend-prod`):
  - Used by the Spring Boot backend running inside the task.
  - Has least-privilege access to:
    - **S3** – read/write production documents in the dedicated bucket.
    - **SQS** – send and receive messages for background jobs and events.
    - **SNS** – publish alert and status messages.
    - **SES** – send emails if using the AWS SDK instead of SMTP.
    - **AWS Secrets Manager** – read application secrets at runtime.
    - **KMS** – decrypt secrets that are encrypted with a customer-managed key.

### CI/CD roles

- **CodeBuild / CodePipeline roles**:
  - Pull source from CodeCommit/GitHub via CodeConnections.
  - Build the backend JAR and Docker image.
  - Push images to **ECR**.
  - Update ECS task definitions and services during deployments.
  - Upload build artifacts (for example `imagedefinitions.json`, frontend bundles) to **S3**.

### IAM user for SES SMTP

For SMTP-based email sending, a dedicated IAM user is used only for SES:

- Example: `ims-ses-smtp-user`.
- Has permission to call `ses:SendEmail` / `ses:SendRawEmail`.
- SMTP credentials generated in the SES console are stored as secrets
  (not hard-coded) and injected into the application via configuration.

Follow the principle of **least privilege** and avoid using overly broad `*:*` policies in production.

## Secrets Management & KMS

Use **AWS Secrets Manager** to store sensitive information such as:
- Database credentials (RDS username, password).
- JWT signing keys or OAuth client secrets.
- SES SMTP / access keys and sender addresses.
- External AI API keys (if used).

Secrets are encrypted at rest using **AWS KMS** keys (AWS managed or a
customer-managed key such as `alias/ims-secrets-key`). The ECS task role
is allowed to call `secretsmanager:GetSecretValue` and `kms:Decrypt` so
that the backend can load secrets securely at startup.

In ECS Task Definitions, reference these secrets via:
- Environment variables sourced from Secrets Manager.
- Or AWS SDK calls within the application using the task role.

Never hard-code secrets in:
- Source code.
- Docker images.
- Frontend bundles.

By structuring authentication, OTP/email verification, IAM roles, network boundaries,
and KMS-encrypted secrets properly, the IMS system can satisfy common security
expectations for enterprise workloads.
