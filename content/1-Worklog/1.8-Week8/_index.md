---
title: "Week 8 Worklog"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.8. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 8 Objectives:

* Fix network issues between ECS services and the internet.
* Finalize target architecture:
	* CloudFront → S3 (Frontend)
	* ALB → ECS (Backend + AI service)
	* ECS → RDS
	* ECS → Secrets Manager
* Validate full end-to-end flow:
	* User → domain → web → AI → DB

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                 | Start Date | Completion Date | Reference Material |
| --- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | --------------- | ------------------ |
| 2   | - Investigate and reproduce ECS outbound internet issue <br> - Verify route table, NAT Gateway/Internet Gateway, NACL, and Security Group                                                         | 02/03/2026 | 02/03/2026      | AWS Docs           |
| 3   | - Apply network fixes for ECS private subnet <br> - Re-test outbound calls and service health checks                                                                                                | 03/03/2026 | 03/03/2026      | AWS Docs           |
| 4   | - Finalize frontend path CloudFront → S3 <br> - Verify domain and HTTPS behavior                                                                                                                    | 04/03/2026 | 04/03/2026      | AWS Docs           |
| 5   | - Finalize backend path ALB → ECS (BE + AI) <br> - Validate ECS connectivity to RDS                                                                                                                 | 05/03/2026 | 05/03/2026      | AWS Docs           |
| 6   | - Validate ECS secret access via Secrets Manager <br> - Execute full flow test: User → domain → web → AI → DB                                                                                     | 06/03/2026 | 06/03/2026      | Internal test plan |


### Week 8 Achievements:

* Fixed ECS outbound internet issue by correcting subnet route path and security configuration.
* Confirmed stable network path for ECS tasks to access required external services.
* Completed frontend deployment flow with CloudFront distributing static content from S3.
* Completed backend routing with ALB forwarding requests to ECS services (Backend + AI).
* Verified secure runtime secret retrieval from Secrets Manager in ECS tasks.
* Verified ECS to RDS connectivity for read/write operations.
* Successfully tested full application flow:
	* User → domain → web → AI → DB
* Collected logs and monitoring snapshots for deployment validation and handover.



