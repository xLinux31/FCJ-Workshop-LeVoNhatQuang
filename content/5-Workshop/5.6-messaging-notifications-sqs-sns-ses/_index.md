---
title: "5.6 Messaging & Notifications (SQS, SNS, SES)"
weight: 6
---

## Messaging & Notifications with SQS, SNS, SES

This section focuses on asynchronous processing and notifications in the IMS system,
using Amazon SQS, Amazon SNS, and Amazon SES.

## Messaging & notification diagrams

![SQS queue configuration for IMS background jobs](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20queue.png)
![SQS access policy for producers and consumers](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20policy.png)
![Queue details including DLQ configuration](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SQS%20config.png)

![SNS topic used to broadcast production alerts](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SNS.png)
![Email alert received from SNS notification](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SNS%20alert.png)

![SES configuration for sending OTP and notification emails](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/SES.png)

![CloudWatch alarm integrated with SNS for infrastructure alerts](/images/5-Workshop/5.6-messaging-notifications-sqs-sns-ses/cloudwatch-alarm.png)

These screenshots show how queues, topics, email sending, and alarms are configured to support asynchronous processing and alerting.

## Use Cases

- Queueing background jobs such as:
  - Recalculating production KPIs.
  - Generating daily/weekly production reports.
  - Processing delay or exception events.
- Fan-out notifications to multiple consumers (e.g., managers, monitoring tools).
- Sending OTP emails and system notifications (e.g., schedule changes, critical alerts).

## Amazon SQS – Background Processing

1. Create queues for background jobs (e.g., `ims-delay-events`, `ims-report-jobs`).
2. Configure dead-letter queues (DLQ) for failed messages.
3. In the backend, design services to:
   - Publish messages to SQS when certain events occur (e.g., delay detected).
   - Consume messages from SQS (via scheduled tasks, workers, or ECS services).
4. Use message attributes to include context (order ID, line, severity, etc.).

## Amazon SNS – Alerts & Fan-Out

1. Create SNS topics (e.g., `ims-critical-alerts`, `ims-status-updates`).
2. Subscribe SQS queues, email addresses, or other endpoints to these topics.
3. From backend services, publish high-level events to SNS when:
   - Critical production incidents occur.
   - Important threshold alarms are triggered.
4. Integrate SNS with CloudWatch alarms to receive infrastructure alerts.

## Amazon SES – Email OTP & Notifications

1. Verify domains and email addresses in **Amazon SES**.
2. Configure the backend to send emails using SES (for example using an HTML template
   for OTP or schedule notifications).
3. Typical flows:
   - Forgot password → backend generates OTP (and expiry) → send via SES → user submits
     OTP back to API → backend verifies OTP and allows password reset.
   - Manager creates new schedule → system emails line leaders with attached/linked
     documents or links to the schedule page.
4. Handle SES sandbox limitations (must verify both sender and recipient in sandbox).
5. Monitor SES metrics and bounces in CloudWatch / SNS.

By wiring SQS, SNS, and SES together, the IMS system can handle heavy workloads
asynchronously and keep users informed about important production events.
