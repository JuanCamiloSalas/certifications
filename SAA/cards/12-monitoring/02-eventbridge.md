[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-cloudwatch.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-cloudtrail.md)

# EventBridge — Event-Driven Automation

> **Pitch (1 line):** serverless event bus that routes events from AWS services, custom apps, and SaaS partners to targets like Lambda, SQS, SNS, Step Functions — the backbone of event-driven architectures.

## 🎯 When the exam picks this

- "trigger Lambda when an EC2 instance is stopped" → **EventBridge rule (state change event)**
- "run a Lambda on a schedule (cron)" → **EventBridge scheduled rule**
- "react to an AWS API call (like S3 object creation, IAM policy change)" → **EventBridge + CloudTrail integration**
- "route SaaS events (Zendesk, Datadog) to AWS targets" → **EventBridge partner event bus**

## 🧠 Core (non-obvious bits)

**Buses:**
- **Default event bus:** receives all AWS service events automatically.
- **Custom event bus:** for your own application events (`PutEvents` API).
- **Partner event bus:** for SaaS integrations (Zendesk, PagerDuty, Stripe, etc.).

**Rules:**
- **Event pattern rule:** filter events by content (service, event type, specific field values). Matched events are sent to the target.
- **Scheduled rule:** cron expression or rate expression (e.g., `rate(5 minutes)`). Replaces the old CloudWatch Events scheduled jobs.

**Targets (what receives the event):**
Lambda, Step Functions, SQS, SNS, Kinesis Data Streams, API Gateway, EC2 actions, ECS tasks, and more. Up to 5 targets per rule.

**Schema Registry:**
- EventBridge can infer and store event schemas. You can generate code bindings from schemas (Java, Python, TypeScript).

**Archive & Replay:**
- Archive events and replay them later (useful for debugging or reprocessing after a bug fix).

**Cross-account / cross-region:**
- Event buses can receive events from other accounts/regions — enables centralized event processing.

## ⚠️ Common traps

- EventBridge ≠ SNS: EventBridge does content-based filtering and routing; SNS does fan-out to multiple subscribers.
- EventBridge replaced **CloudWatch Events** — same service, new name and more features. "CloudWatch Events scheduled rule" in old docs = EventBridge scheduled rule now.
- EventBridge can receive CloudTrail events for API call reactions, but needs CloudTrail enabled first.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-cloudwatch.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-cloudtrail.md)
