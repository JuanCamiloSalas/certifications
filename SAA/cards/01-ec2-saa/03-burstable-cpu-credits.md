[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-instance-lifecycle.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-hibernation.md)

# Burstable Instances (T family) & CPU Credits

> **Pitch (1 line):** **T** instances (T2/T3/T3a/T4g) are cheap and deliver a **baseline** performance with the ability to **burst** above it using **CPU credits** — ideal for workloads with occasional spikes.

## 🎯 When the exam picks this

- "spiky/bursty workload, low average CPU, cost-sensitive" → **T family (burstable)**
- "must sustain bursts even when credits run out" → **T Unlimited mode**
- "high, sustained CPU" → ⚠️ NOT T → **Compute Optimized (C family)**

## 🧠 Core (non-obvious bits)

- Each T instance has a CPU **baseline** (a fixed %). Below baseline it **earns** credits; bursting above baseline **spends** credits.
- **Standard mode:** when the credit balance hits 0 → the instance is **throttled to baseline** (the app slows down).
- **Unlimited mode:** can keep bursting even with no credits, but you're **charged extra** if average usage exceeds the baseline.
- Key defaults: **T2 = Standard** by default; **T3/T3a/T4g = Unlimited** by default.
- Typical use cases: web servers, dev/test, microservices, small DBs — anything with **low average CPU and occasional spikes**.

## 🔢 Numbers to memorize

- CloudWatch metric to watch: **`CPUCreditBalance`** (trending to 0 under load → you're out of credits).
- Baseline depends on size (e.g. `t3.micro` ≈ 10% × 2 vCPU). Don't memorize the %; memorize the **baseline/burst concept**.

## ⚠️ Common traps

- "the T2/T3 app slows down under sustained load" → it **ran out of CPU credits** → enable **Unlimited** or move to **C** (compute optimized).
- "cheapest option for a constant CPU-intensive workload" → ❌ not T; throttling or the Unlimited surcharge makes it costly. T is for spikes, not flat high load.

## 🖼️ Diagram

```mermaid
flowchart LR
    A["CPU &lt; baseline"] -->|earns credits| B[("CPU credit<br/>balance")]
    C["Spike: CPU &gt; baseline"] -->|spends credits| B
    B -->|balance = 0| D{Mode}
    D -->|Standard| E["Throttle to baseline"]
    D -->|Unlimited| F["Keep bursting<br/>+ extra charge"]
```

## 🔄 Easily confused with

- → [Instance families / types (CCP)](../../../CCP/3_EC2/README.md) — General Purpose vs Compute Optimized vs Memory/Storage.

---

[![](https://img.shields.io/badge/<_Prev-FF4859?style=for-the-badge)](./02-instance-lifecycle.md)
[![](https://img.shields.io/badge/Block-175074?style=for-the-badge)](./README.md)
[![](https://img.shields.io/badge/Next_>-FF4859?style=for-the-badge)](./04-hibernation.md)
