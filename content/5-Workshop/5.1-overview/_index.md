---
title: "5.1 IMS System & Workshop Overview"
weight: 1
---

In this section, we recap the business problem, user roles, and demo scenario for the
AI-Assisted Electronics Production Management System (IMS), and explain how the
hands-on workshop is organized around this system.

## Business Problem

Small and medium-sized electronics factories often:
- Plan production manually in Excel.
- Cannot track real-time progress per stage (SMT, DIP, testing).
- Store order and report data across many files and systems.
- Struggle to understand line capacity and bottlenecks.
- Rely on on-prem infrastructure that is hard to scale and monitor.

## Target Users & Roles

The system is designed for three main roles:

- **Admin** – manage user accounts, roles, and system configuration.
- **Manager** – create/manage production orders, build production plans, monitor KPIs and OEE.
- **Line Leader** – view assigned tasks, update execution status, receive schedules and notifications.

## Demo Scenario

In the workshop, we will use a sample electronics factory with multiple lines (SMT, DIP, testing):

1. A manager creates new customer orders and production plans in the web app.
2. Line leaders receive their daily tasks and update progress from the shop floor.
3. The system aggregates data into dashboards and OEE/throughput metrics.
4. AI endpoints provide natural-language summaries like:
   - "Which line is causing delays this week?"
   - "What is today’s OEE on SMT line 1?"
   - "Which orders are at risk of missing their deadline?"

## Workshop Journey

Throughout the 5-Workshop, you will:
- Understand the end-to-end architecture of the IMS system on AWS.
- Containerize and deploy the Spring Boot backend to ECS with RDS.
- Host the React frontend on S3 + CloudFront.
- Integrate SQS, SNS, SES for asynchronous processing and notifications.
- Secure secrets with Secrets Manager and configure basic IAM roles.
- Set up CloudWatch logs, metrics, alarms, and a simple CI/CD pipeline.

## How the Workshop Is Structured

The hands-on workshop is organized into modules that mirror the real system architecture:

- **Architecture & IaC** – map the React + Spring Boot system to AWS (CloudFront, S3, ALB, ECS, RDS, SQS/SNS/SES, Secrets Manager, CloudWatch).
- **VPC & Networking** – design the VPC, subnets, routing, and security groups that host the services.
- **Backend on ECS & RDS** – build and deploy the Spring Boot API as a container on ECS Fargate with PostgreSQL on RDS.
- **Frontend on S3 & CloudFront** – build and publish the React SPA.
- **Messaging & Notifications** – use SQS/SNS/SES for delays, incidents, and OTP emails.
- **Auth & Secrets** – configure IAM roles, an SES IAM user, Secrets Manager, and KMS.
- **Observability & CI/CD** – configure CloudWatch logs/metrics/alarms and the CodeBuild/CodePipeline → ECR → ECS deployment flow.
- **AI & Analytics** – connect production data to AI assistants and dashboards.

For full business requirements and detailed user stories, refer to the **2-Proposal** documents. The workshop focuses on how those requirements are realized using AWS services.
