---
title: "5.9 Observability & CI/CD"
weight: 9
---

# 5.9 Observability & CI/CD Pipeline

This section covers how to monitor the IMS system with Amazon CloudWatch and
how to automate builds and deployments with AWS CodeBuild and CodePipeline.

## CloudWatch Logs & Metrics

- **ECS Tasks**: send application logs to CloudWatch Logs (e.g., `/ecs/ims-backend`).
- **ALB**: optional access logs to S3 for deeper HTTP analysis.
- **RDS**: performance metrics such as CPU, connections, and read/write IOPS.
- **SQS/SNS/SES**: basic operational metrics (queue length, delivery failures, bounces).

You can build a simple CloudWatch Dashboard with widgets for:
- ECS service CPU & memory utilization.
- RDS CPU & connections.
- SQS queue depth (approximate number of messages).
- ALB 5XX error count and target response time.

## CloudWatch Alarms

Create alarms for key signals, for example:

- **ECS service CPU** > 80% for 5 minutes → send notification via SNS.
- **ALB HTTPCode_Target_5XX_Count** above a threshold → potential app errors.
- **RDS CPUUtilization** > 80% for sustained periods → performance investigation.
- **SQS ApproximateNumberOfMessagesVisible** too high → backlog in background jobs.

Alarms can notify you via email via an SNS topic (for example `ims-prod-alerts` with
an email subscription) and can also be wired as targets for ECS Service Auto Scaling
(target tracking on CPU or RequestCount).

### Example alarm setup

At minimum, the production environment should have:
- `ims-ecs-backend-cpu-high` – ECS service CPU alarm (SNS → email).
- `ims-alb-5xx-high` – ALB 5xx error alarm.
- `ims-rds-cpu-high` – RDS CPU alarm.

Each alarm:
1. Selects the metric (ECS, ALB, or RDS) for the production stack.
2. Uses a period such as 60–300 seconds and a static threshold (for example 80%).
3. Sends notifications to the SNS topic used by the ops team.

## CI/CD with CodeBuild & CodePipeline

The repository already includes a `buildspec.yml` at the root to:
- Build the Spring Boot backend.
- Build a Docker image.
- Push the image to **Amazon ECR**.
- Generate `imagedefinitions.json` for ECS deployment.

A typical pipeline for the backend might be:

1. **Source Stage** – pull from GitHub/CodeCommit.
2. **Build Stage (CodeBuild)** – run `buildspec.yml` to build & push the image.
3. **Deploy Stage** – use ECS deploy action to update the ECS service
   with the new `imagedefinitions.json`.

You can create a separate pipeline for the frontend:
- Build React with `npm run build`.
- Sync build artifacts to the S3 frontend bucket.
- Invalidate CloudFront cache.

## Operations & Rollback

In case of issues:
- Use CloudWatch Logs to inspect application errors.
- Roll back to the previous ECS task definition or ECR image tag.
- Scale out ECS tasks temporarily if CPU or latency is high.

With observability and CI/CD in place, the IMS system becomes much easier to operate,
troubleshoot, and evolve safely over time.
