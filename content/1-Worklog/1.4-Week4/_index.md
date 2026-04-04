---
title: "Week 4 Worklog"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 4 Objectives:

* Deploy and validate database connectivity between ECS and RDS.
* Integrate AI data flow with RDS and verify real queries.
* Improve security by managing secrets with AWS Secrets Manager.
* Complete frontend delivery path with S3, CloudFront, and Route 53.

### Tasks to be carried out this week:
| Date | Task | Status |
| --- | --- | --- |
| 26/01/2026 | Created RDS PostgreSQL database; connected ECS to RDS; tested data write/read operations. | Done |
| 27/01/2026 | Integrated AI with database; enabled AI to read data from RDS; tested real query scenarios. | Done |
| 28/01/2026 | Set up AWS Secrets Manager; stored API keys and DB password; configured ECS to read secrets instead of hardcoding; fixed security issues. | Done |
| 29/01/2026 | Created S3 bucket for frontend; uploaded React/Vue static site; tested static web access. | Done |
| 30/01/2026 | Set up CloudFront; connected CloudFront to S3; tested faster web delivery. | Done |
| 31/01/2026 | Set up Route 53; pointed domain to CloudFront; tested domain availability (ims.mom). | Done |


### Week 4 Achievements:

* Completed end-to-end backend data layer with ECS to RDS integration.
* Enabled secure secret handling by replacing hardcoded credentials with AWS Secrets Manager.
* Delivered frontend hosting stack with S3 + CloudFront + Route 53 domain routing.
* Achieved a near-production web access flow from domain to CDN to static frontend.


