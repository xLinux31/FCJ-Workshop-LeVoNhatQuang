---
title: "Week 5 Worklog"
date: 2026-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---
{{% notice warning %}} 
⚠️ **Note:** The following information is for reference purposes only. Please **do not copy verbatim** for your own report, including this warning.
{{% /notice %}}


### Week 5 Objectives:

* Stabilize the full system by fixing cross-component bugs.
* Harden network access controls with security group rules.
* Enforce least-access traffic paths between ALB, ECS, and RDS.
* Validate security behavior after rule updates.

### Tasks to be carried out this week:
| Date range | Task | Status |
| --- | --- | --- |
| 01/02/2026 - 03/02/2026 | Fixed overall system bugs across services. | Done |
| 04/02/2026 - 06/02/2026 | Configured Security Groups: opened ALB ports 80/443; allowed ECS inbound traffic only from ALB; allowed RDS inbound traffic only from ECS; performed security testing. | Done |


### Week 5 Achievements:

* Resolved key system-level bugs to improve overall service stability.
* Implemented security group segmentation aligned with architecture boundaries.
* Confirmed secure traffic flow model: ALB -> ECS -> RDS.
* Completed validation tests for ingress restrictions and runtime access behavior.


