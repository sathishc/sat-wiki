---
title: Little's Law
tags: [reinertsen, queueing-theory, flow, cycle-time, wip, mathematics]
created: 2026-04-16
updated: 2026-04-16
sources: [sources/reinertsen-flow.md]
---

# Little's Law

A theorem from queueing theory, proved by John Little (1961). The mathematical foundation underneath much of [Reinertsen](../people/donald-reinertsen.md)'s flow framework.

## The Formula

```
L = λW
```

Where:
- **L** = average number of items in the system (queue + being worked on) — i.e., WIP
- **λ** (lambda) = average throughput rate (items completed per unit time)
- **W** = average time an item spends in the system (cycle time)

Rearranged for product development:

```
Cycle Time = WIP / Throughput
```

or equivalently:

```
WIP = Throughput × Cycle Time
```

## What It Tells Us

The formula is remarkably robust — it holds regardless of queue discipline, arrival distribution, service distribution, or almost any other assumption. It is a near-universal law of systems that process items.

**For product development teams, the implications are direct:**

1. **To reduce cycle time**, reduce WIP or increase throughput
2. **If WIP grows unchecked**, cycle time grows proportionally
3. **You cannot reduce cycle time by adding more work** — adding WIP increases cycle time, not decreases it
4. **Throughput is not the same as starting more work** — throughput is *completing* work

## The Counterintuitive Implication

Most organisations try to go faster by **starting more work in parallel**. Little's Law says this is backwards: more parallel WIP means longer cycle time per item, not shorter. Starting more doesn't finish more. It just makes everything slower.

The correct lever: **finish work before starting new work**. "Stop starting, start finishing."

## Connection to [WIP Limits](./wip-limits.md)

WIP limits are the operational implementation of Little's Law. By capping L (WIP), you directly control W (cycle time), given roughly stable throughput. This is not a heuristic — it is mathematically guaranteed by Little's Law.

## Connection to [Compounding](./compounding.md)

Little's Law has a compounding-like quality: small reductions in WIP produce cycle time improvements that persist and multiply. A team that halves its WIP roughly halves its cycle time — which means faster feedback, fewer bugs, faster learning — which further improves throughput. The gains compound.

## Related Pages

- [Donald Reinertsen](../people/donald-reinertsen.md)
- [WIP Limits](./wip-limits.md)
- [Queues in Product Development](./queues-in-product-development.md)
- [Batch Size](./batch-size.md)
- [Flow Economics](./flow-economics.md)
