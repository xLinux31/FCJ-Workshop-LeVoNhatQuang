---
title: "Week 11 Worklog"
date: 2026-01-01
weight: 2
chapter: false
pre: " <b> 1.11. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 11 Objectives:

* Finalize the optimized system architecture and documentation.
* Continue refining system performance and stability.
* Re-test the full service flow after the final adjustments.

### Tasks to be carried out this week:
| Day | Task                                                                                                                                                                                                   | Start Date | Completion Date | Reference Material                        |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------- | --------------- | ----------------------------------------- |
| 2   | - Review final architecture against the current implementation <br> - Check all service links and optimize any remaining weak points                                                                     | 23/03/2026 | 23/03/2026      | Internal review |
| 3   | - Re-tune CloudFront, ALB, ECS, and RDS settings where needed <br> - Verify secret access and runtime permissions                                                                                     | 24/03/2026 | 24/03/2026      | AWS Docs        |
| 4   | - Redraw the final system architecture diagram <br> - Update documentation to match the optimized deployment                                                                                           | 25/03/2026 | 25/03/2026      | draw.io + AWS Docs |
| 5   | - Run a final smoke test across frontend, backend, AI, and database layers <br> - Check logs and stability after tuning                                                                                | 26/03/2026 | 26/03/2026      | Internal test plan |
| 6   | - Summarize optimization results and architecture changes <br> - Prepare the final handover notes                                                                                                      | 27/03/2026 | 27/03/2026      | Internal report   |


### Week 11 Achievements:

* Finalized the system architecture and aligned it with the actual deployment.
* Completed the last round of performance and stability tuning.
* Confirmed service paths after final updates:
  * User → Domain → CloudFront → S3 (FE)
  * API → ALB → ECS (BE + AI)
  * ECS → RDS and ECS → Secrets Manager
* Verified logs, runtime behavior, and deployment stability after optimization.
* Prepared the final handover summary for the project.


