[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)

# 📊 Comparisons (`comparativas/`)

> Side-by-side tables for services that the exam keeps confusing on purpose. Open these when a card mentions "easily confused with...".

## How this folder works

- **Not in the card flow.** Cards link here when relevant; you don't walk through this folder linearly.
- **One topic per file.** A comparison stays focused on a single decision.
- **Table-first.** Open with the decision table; details after.
- **Built after each block**, not in advance. Real Dojo confusion drives what gets written.

## File naming

`<topic-or-services>.md`, lowercase, dash-separated. Examples:

- `sqs-vs-sns-vs-kinesis.md`
- `sqs-standard-vs-fifo.md`
- `ecs-vs-eks-vs-fargate.md`
- `cloudfront-vs-global-accelerator.md`
- `security-group-vs-nacl.md`
- `dr-strategies.md`

## Suggested skeleton for a comparison file

```markdown
# X vs Y vs Z

> One-line summary of when each wins.

## Decision table

| | X | Y | Z |
|---|---|---|---|
| Model | ... | ... | ... |
| Throughput | ... | ... | ... |
| Use case | ... | ... | ... |
| Limits | ... | ... | ... |

## When the exam picks each
- **X:** trigger phrases
- **Y:** trigger phrases
- **Z:** trigger phrases

## Common traps
- ...

## Linked cards
- [X card](../cards/NN-block/...)
- [Y card](../cards/NN-block/...)
```

## Index of comparisons

| File | Topic | Block |
|---|---|---|
| [cluster-spread-partition.md](./cluster-spread-partition.md) | EC2 Placement Groups: Cluster vs Spread vs Partition | 01 – EC2 |
| [sqs-vs-sns-vs-kinesis.md](./sqs-vs-sns-vs-kinesis.md) | SQS vs SNS vs Kinesis vs Amazon MQ | 08 – Decoupling |

---

[![](https://img.shields.io/badge/<_SAA-FF4859?style=for-the-badge)](../README.md)
