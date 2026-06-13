[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-api-gateway.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-cognito-appsync.md)

# Step Functions

> **Pitch (1 line):** orchestrate Lambda functions and AWS services into **visual state machine workflows** — handles sequencing, branching, retries, and error handling without writing glue code.

## 🎯 When the exam picks this

- "orchestrate a multi-step workflow with Lambda / ECS / DynamoDB" → **Step Functions**
- "retry a failed step automatically" → **Step Functions** error handling
- "workflow that branches based on a condition" → **Step Functions Choice state**
- "run multiple tasks in parallel within a workflow" → **Step Functions Parallel state**

## 🧠 Core (non-obvious bits)

**Workflow types:**

| | Standard | Express |
|---|---|---|
| Duration | Up to **1 year** | Up to **5 minutes** |
| Execution model | At-least-once | At-least-once (async) / Exactly-once (sync) |
| Audit history | Full, in console | CloudWatch Logs only |
| Pricing | Per state transition | Per execution + duration |
| Use case | Long-running, auditable | High-volume, short, event processing |

**Key states:**
- **Task:** invoke a service (Lambda, ECS, SNS, DynamoDB, etc.)
- **Choice:** branch based on conditions (like if/else)
- **Parallel:** run multiple branches simultaneously
- **Map:** iterate over an array and run a state machine for each item
- **Wait:** pause for a duration or until a timestamp
- **Succeed / Fail / Pass:** terminal or pass-through states

**Error handling:**
- `Retry` block: retry the state N times with backoff.
- `Catch` block: catch specific errors and route to a fallback state.
- No extra code — all declared in the state machine definition (ASL JSON).

## ⚠️ Common traps

- Step Functions is an **orchestrator**, not a message queue — use SQS for buffering, Step Functions for workflow control.
- Standard workflows can run for up to 1 year — useful for human approval workflows (pause and wait for callback).
- "parallel steps" → use Parallel state inside Step Functions, not separate Step Functions executions.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./04-api-gateway.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./06-cognito-appsync.md)
