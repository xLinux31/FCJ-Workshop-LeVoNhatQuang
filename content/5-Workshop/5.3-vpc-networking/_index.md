---
title: "5.3 VPC & Networking for the IMS System"
date: 2026-01-01
weight: 3
chapter: false
---
VPC & Networking for the AI Production Management System

In this module, you design the **network foundation** for the AI Production Management System.

You will map the system architecture into a single **VPC** (for example `vpc-ims`, CIDR `12.0.0.0/16`) with **two public and three private subnets** spread across Availability Zones `ap-southeast-1a` and `ap-southeast-1b`, and see where the **Application Load Balancer, ECS services, and RDS** live.

#### Learning goals

- Understand how the IMS architecture fits into an **AWS VPC** with public and private subnets.
- Place **ALB, ECS tasks, and RDS** into appropriate subnets and Availability Zones.
- Prepare the network so that later modules (ECS, RDS, S3/CloudFront, messaging) can be deployed securely.

#### Sections

1. [VPC Basics – CIDR & Subnets](5.2.1-vpc-basics/)
2. [Routing, Internet Gateway & NAT](5.2.2-routing-egress/)
3. [Security Boundaries – Security Groups, NACLs & IAM](5.2.3-security-boundaries/)
4. [Service Connectivity – ECS, RDS, S3 & Messaging](5.2.4-service-connectivity/)
