---
title: "5.8 AI Production Analytics"
weight: 8
---

## AI Production Analytics Layer

This section highlights how AI is integrated into the IMS system to provide
natural-language insights and analytics on top of production data.

## Purpose of AI in IMS

The AI layer helps managers and engineers:
- Quickly understand the health of production lines.
- Identify delays and bottlenecks.
- Summarize complex dashboards into executive-level narratives.
- Answer ad-hoc questions about orders, schedules, OEE, and delays.

Example questions the system may answer:
- "Which stage is causing delays for this week’s plan?"
- "What is today’s OEE on SMT line 1?"
- "List orders at risk of missing their deadline."

## Data Sources

The AI services rely on data stored in **Amazon RDS**, including:
- Orders and work orders.
- Production schedules and actual execution logs.
- Line performance metrics (OEE, throughput, downtime).
- Historical delays and incident records.

Backend services aggregate this data into structured prompts before sending it to
an LLM/AI API.

## Backend AI Services

In the backend (Spring Boot), AI support is typically implemented via services such as:
- `AIProductionAnalysisService`
- `ProductionAnalysisService`

These services:
- Query production data from RDS.
- Build a compact, structured context (e.g., JSON or bullet points).
- Call an external AI API (e.g., OpenAI) using a secret API key stored in **AWS Secrets Manager**.
- Post-process the AI response into user-friendly text or structured JSON for the frontend.

## Security & Cost Considerations

- **Secrets**: Never hard-code AI API keys; always fetch them from Secrets Manager
  using the ECS task role.
- **Privacy**: Avoid sending unnecessary personal or sensitive data to AI APIs.
- **Cost**: Add limits on request frequency and maximum context size.
- **Timeouts & Retries**: Implement reasonable timeouts and error handling so the
  app remains responsive even when the AI provider is slow.

## Frontend Integration

The React frontend calls AI-related endpoints via `aiService` and displays:
- Natural-language summaries (e.g., "Production health summary for today").
- Highlighted risks (late orders, overloaded lines).
- Suggestions or next actions for managers.

By combining deterministic production data with an AI summarization layer, the IMS
system provides a more intuitive way for non-technical users to understand
complex factory status at a glance.
