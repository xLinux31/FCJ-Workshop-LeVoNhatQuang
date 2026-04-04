---
title: "Week 3 Worklog"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 3 Objectives:

* Integrate AI into backend services and expose AI APIs.
* Containerize backend + AI stack and prepare deployment pipeline.
* Deploy services on AWS ECS with ALB and VPC network components.
* Validate internet connectivity and routing for private workloads.

### Tasks to be carried out this week:
| Date | Task | Status |
| --- | --- | --- |
| 19/01/2026 | Started integrating AI into backend; wrote APIs for web-to-AI calls; tested APIs locally with Postman. | Done |
| 20/01/2026 | Containerized AI + backend with Docker; built image and tested locally; prepared deployment to server. | Done |
| 21/01/2026 | Learned and pushed Docker images to Amazon ECR; tested pulling images from server. | Done |
| 22/01/2026 | Set up ECS; deployed backend + AI containers to ECS; tested first service run. | Done |
| 23/01/2026 | Created ALB; connected ALB -> ECS; tested backend access via ALB. | Done |
| 24/01/2026 | Completed VPC setup: public subnet (ALB, NAT), private subnet (ECS, RDS); configured route tables. | Done |
| 25/01/2026 | Set up Internet Gateway for public subnet; set up NAT Gateway for private ECS outbound traffic; tested ECS external API access (OpenAI/AI service). | Done |


### Week 3 Achievements:

* Delivered initial AI-backend integration and validated API flow locally.
* Established container deployment pipeline (Docker -> ECR -> ECS).
* Completed first production-style service exposure through ALB.
* Implemented VPC networking baseline for public/private workloads and outbound internet access from ECS.


