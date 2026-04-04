---
title: "Week 10 Worklog"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 1.10. </b> "
---


### Week 10 Objectives:

* Continue optimizing the system for performance and stability.
* Review and redraw the updated AWS system architecture.
* Re-validate the main traffic flow after optimization changes.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Review current performance bottlenecks across frontend, backend, and database layers <br> - Identify optimization points for caching, routing, and service resources                                             | 16/03/2026 | 16/03/2026      | Internal review |
| 3   | - Tune CloudFront, ALB, and ECS configuration <br> - Adjust health checks, timeouts, and deployment settings                                                                                                     | 17/03/2026 | 17/03/2026      | AWS Docs        |
| 4   | - Review RDS queries, connection behavior, and secret access flow <br> - Apply IAM least-privilege adjustments if needed                                                                                         | 18/03/2026 | 18/03/2026      | AWS Docs        |
| 5   | - Redraw the updated system architecture diagram <br> - Verify service connections: CloudFront → S3, ALB → ECS, ECS → RDS, ECS → Secrets Manager                                                             | 19/03/2026 | 19/03/2026      | draw.io |
| 6   | - Run smoke tests after optimization <br> - Collect logs and compare behavior before/after tuning <br> - Finalize notes for the report                                                                         | 20/03/2026 | 20/03/2026      | Internal test plan |


### Week 10 Achievements:

* Improved system stability by tuning core layers of the application stack.
* Applied optimization to CloudFront, ALB, ECS, and database access paths.
* Reviewed and updated the AWS architecture diagram to match the actual implementation.
* Confirmed the main service flow after tuning:
  * User → Domain → CloudFront → S3 (FE)
  * API → ALB → ECS (BE + AI)
  * ECS → RDS and ECS → Secrets Manager
* Collected logs and testing notes for the final report.

