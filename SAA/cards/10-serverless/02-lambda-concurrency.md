[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-lambda-fundamentals.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-lambda-vpc.md)

# Lambda Concurrency, Cold Starts, Destinations & Layers

<img src="../../assets/icons/lambda.png" width="64">

> **Pitch (1 line):** concurrency governs how many Lambda instances run simultaneously — reserved limits neighbors, provisioned eliminates cold starts; layers share code across functions.

## 🎯 When the exam picks this

- "ensure Lambda doesn't consume all account concurrency" → **Reserved Concurrency**
- "eliminate cold start latency" → **Provisioned Concurrency**
- "route success/failure of async Lambda to different targets" → **Lambda Destinations**
- "share common libraries across Lambda functions" → **Lambda Layers**

## 🧠 Core (non-obvious bits)

**Concurrency:**
- **Account limit:** 1,000 concurrent executions per region (soft limit, can request increase).
- **Reserved Concurrency:** guarantee a maximum for one function AND prevent it from consuming others' concurrency. Sets a ceiling, not a floor.
- **Provisioned Concurrency:** pre-initialize a set of function instances — they're always warm, no cold start. Costs money even when idle.

**Cold Start:**
- First invocation (or scale-up) requires: init the execution environment → download code → run init code outside handler.
- Duration: 100ms–1s+ depending on runtime and code size. Java and .NET have the worst cold starts.
- Solutions: Provisioned Concurrency, Lambda SnapStart (Java), or keep-warm pings (anti-pattern, use SnapStart).

**Lambda Destinations (async invocations only):**
- On **success** → forward event to SQS, SNS, EventBridge, or another Lambda.
- On **failure** (after retries exhausted) → forward to SQS DLQ, SNS, EventBridge, or another Lambda.
- Destinations are preferred over function-level DLQs (more flexible, more information in the event).

**Lambda Layers:**
- A zip of libraries/dependencies shared across multiple functions.
- Up to **5 layers** per function.
- Max total unzipped size (function + layers): **250 MB**.
- Use cases: shared SDK, custom runtimes, large ML model files.

## 🔢 Numbers to memorize

- Account default concurrency: **1,000** per region
- Max layers per function: **5**
- Async retries before destination/DLQ: **2 retries** (3 total attempts)

## ⚠️ Common traps

- Reserved concurrency sets a ceiling (throttles above it), not a guaranteed floor. To guarantee available capacity, use Provisioned Concurrency.
- "Lambda timeout" ≠ cold start — timeout is the max execution time; cold start is initialization before execution.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./01-lambda-fundamentals.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./03-lambda-vpc.md)
