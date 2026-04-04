---
title: "5.4 Backend on ECS, ECR & RDS"
weight: 4
---

## Backend Service on ECS, ECR & RDS

In this section, you will focus on packaging and deploying the Spring Boot backend
from the `backend/backend` folder to **Amazon ECR** and **Amazon ECS (Fargate)**,
then connecting it to an **Amazon RDS** database.

## Backend Service Overview

The backend is a Spring Boot application that provides REST APIs for:
- Managing production orders and work orders.
- Defining production lines and capacities.
- Tracking production progress and delays.
- Exposing metrics for dashboards and AI analysis endpoints.
- Sending OTP emails and notifications via SES.

The project uses:
- Java 17
- Spring Boot
- Spring Security (role-based access)
- JPA/Hibernate with Flyway database migrations

## ECS architecture diagrams

![High-level ECS service architecture for the IMS backend](/images/5-Workshop/5.4-backend-ecs-rds/ecs1.png)

![ECS networking with private subnets, ALB and security groups](/images/5-Workshop/5.4-backend-ecs-rds/ecs7network.png)

These diagrams summarize how the backend service runs on Fargate tasks inside private subnets, connects to RDS, and is fronted by an ALB.

## Containerization & Amazon ECR

1. **Create an ECR repository** (for example `ims-production`) in the target AWS account/region.
2. Review the `Dockerfile` under `backend/backend/`.
3. Build the JAR using Maven (`./mvnw -DskipTests clean package`).
4. Log in to ECR using the AWS CLI (or let CodeBuild do it with `aws ecr get-login-password`).
5. Build the Docker image and tag it with your ECR repository URI, for example:
   - `638389534958.dkr.ecr.ap-southeast-1.amazonaws.com/ims-production:<git-sha>`
   - and optionally `:latest`.
6. Push the image to **Amazon ECR**.

In the workshop, this process is automated using **AWS CodeBuild** with the
`buildspec.yml` file at the repository root:
- CodeBuild logs in to ECR.
- Builds the Spring Boot JAR and Docker image.
- Tags the image with the short Git commit SHA and `latest`.
- Pushes both tags to the ECR repository.

## Deploying to ECS (Fargate)

![Creating ECS cluster and Fargate service](/images/5-Workshop/5.4-backend-ecs-rds/ecs2.png)
![Task definition with container image and CPU/memory](/images/5-Workshop/5.4-backend-ecs-rds/ecs3.png)
![Service configuration, desired count and deployment](/images/5-Workshop/5.4-backend-ecs-rds/ecs4.png)
![Load balancer integration for ECS service](/images/5-Workshop/5.4-backend-ecs-rds/ecs5.png)
![Auto scaling configuration for ECS service](/images/5-Workshop/5.4-backend-ecs-rds/ecs6.png)
![ALB listener and target group wired to ECS](/images/5-Workshop/5.4-backend-ecs-rds/ecs8alb.png)
![ECS service scaling policy based on CPU utilization](/images/5-Workshop/5.4-backend-ecs-rds/ecs9autoscale.png)

1. Create an **ECS Cluster** (Fargate type).
2. Define a **Task Definition**:
   - Container image **pulled from the ECR repository** above.
   - CPU/Memory limits (e.g., 0.5 vCPU / 1–2 GB RAM).
   - Container port (e.g., 8080).
   - Environment variables (database URL, username, password, etc.) – ideally from Secrets Manager.
3. Create an **Application Load Balancer (ALB)** and target group for the ECS service.
4. Configure health checks (e.g., `/actuator/health` if enabled).
5. Create an **ECS Service** using the task definition and attach it to the ALB target group.

## Connecting to Amazon RDS

![Amazon RDS PostgreSQL instance in private subnets](/images/5-Workshop/5.4-backend-ecs-rds/RDS.png)

1. Provision a **PostgreSQL** database in Amazon RDS inside your VPC private subnets.
2. Configure Security Groups so that only ECS tasks (and optionally bastion/administration hosts) can connect to RDS.
3. Store database credentials in **AWS Secrets Manager**.
4. Map secrets/environment variables into the ECS task definition:
   - `SPRING_DATASOURCE_URL`
   - `SPRING_DATASOURCE_USERNAME`
   - `SPRING_DATASOURCE_PASSWORD`
5. Verify that Flyway migrations under `src/main/resources/db/migration/` run successfully when the app starts.

## Traffic Flow & Logs

At runtime, requests follow this path:

`Client → Route 53 → ALB → ECS Service (Spring Boot) → RDS`

Logs from the container are sent to **CloudWatch Logs** (e.g., log group `/ecs/ims-backend`).
You can use these logs to troubleshoot errors and verify that the service is healthy after each deployment.
