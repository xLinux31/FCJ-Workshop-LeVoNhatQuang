---
title: "Week 12 Worklog"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 1.12. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}

### Week 12 Objectives:

* Redraw and refine the AWS architecture diagram to match the current deployment.
* Optimize the system to reduce unnecessary resource usage and lower operating cost.
* Re-validate the main traffic flow after the diagram and tuning updates.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Review current resource usage across frontend, backend, and database layers <br> - Identify areas that can be reduced or consolidated to cut cost                                             | 30/03/2026 | 30/03/2026      | Internal review |
| 3   | - Tune CloudFront, ALB, and ECS configuration <br> - Adjust scaling, health checks, and runtime settings to avoid over-provisioning                                                                                                     | 31/03/2026 | 31/03/2026      | AWS Docs        |
| 4   | - Review RDS queries, connection behavior, and secret access flow <br> - Apply IAM least-privilege adjustments and remove unused access paths if needed                                                                                         | 01/04/2026 | 01/04/2026      | AWS Docs        |
| 5   | - Redraw the updated system architecture diagram <br> - Verify service connections: CloudFront → S3, ALB → ECS, ECS → RDS, ECS → Secrets Manager                                                             | 02/04/2026 | 02/04/2026      | draw.io + AWS Docs |
| 6   | - Run smoke tests after optimization <br> - Compare logs and billing-related behavior before/after tuning <br> - Finalize notes for the report                                                                         | 03/04/2026 | 03/04/2026      | Internal test plan |


### Week 12 Achievements:

* Improved system stability while reducing unnecessary resource consumption.
* Applied cost-focused optimization to CloudFront, ALB, ECS, and database access paths.
* Reviewed and updated the AWS architecture diagram to match the actual implementation.
* Confirmed the main service flow after tuning:
  * User → Domain → CloudFront → S3 (FE)
  * API → ALB → ECS (BE + AI)
  * ECS → RDS and ECS → Secrets Manager
* Collected logs and tuning notes for the final report.




