---
title: "Week 9 Worklog"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

* Draw the architecture of AWS services used in the project.
* Review and optimize the current system for performance, stability, and cost.
* Validate optimized end-to-end user flow and document deployment notes.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ------------------ |
| 2   | - Inventory all AWS services currently in use <br> - Define logical layers (Edge, Frontend, App, Data, Security, Observability) <br> - Draft architecture version 1                                                                                 | 09/03/2026 | 09/03/2026      | AWS Docs           |
| 3   | - Draw final architecture diagram for workshop stack <br> - Validate request/response paths: CloudFront → S3 and ALB → ECS <br> - Verify data/security paths: ECS → RDS and ECS → Secrets Manager                                                   | 10/03/2026 | 10/03/2026      | draw.io + AWS Docs |
| 4   | - Optimize frontend delivery: CloudFront cache policy, compression, error fallback <br> - Optimize ALB and ECS health checks/startup grace period <br> - Tune ECS task CPU/memory and deployment settings                                           | 11/03/2026 | 11/03/2026      | AWS Docs           |
| 5   | - Optimize DB path: connection management, query/index review, timeout settings <br> - Review IAM least privilege for ECS task role and secret access <br> - Add or adjust monitoring/alerts (CloudWatch metrics + logs)                            | 12/03/2026 | 12/03/2026      | AWS Docs           |
| 6   | - Execute load & functional smoke tests after optimization <br> - Compare before/after metrics (latency, error rate, response time) <br> - Finalize architecture and optimization summary for report                                                   | 13/03/2026 | 13/03/2026      | Internal test plan |


### Week 9 Achievements:

* Completed AWS architecture diagram of the implemented system.
* Documented service interactions across edge, application, database, and secrets layers.
* Applied key optimizations:
	* CloudFront caching and compression for static frontend delivery.
	* ALB and ECS health-check tuning to reduce false unhealthy states.
	* ECS task resource tuning and safer rolling deployment configuration.
	* RDS access-path and query/index review for stable response time.
	* IAM + Secrets Manager policy review for least-privilege secret access.
* Completed validation after optimization:
	* User → Domain → CloudFront → S3 (FE)
	* API calls → ALB → ECS (BE + AI)
	* ECS → RDS and ECS → Secrets Manager
* Observed improvements in page/API response stability and reduced deployment interruption.

