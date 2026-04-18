---
title: Cost of Delay
tags: [reinertsen, flow, economics, prioritisation, product-development, wsjf]
created: 2026-04-16
updated: 2026-04-16
sources: [sources/reinertsen-flow.md]
layout: default
parent: Concepts
---

# Cost of Delay

The single most important economic concept in [Reinertsen](../people/donald-reinertsen.md)'s framework. Cost of Delay (CoD) is the **economic impact of time** — specifically, what it costs you when delivery is delayed by one unit of time.

> "Cost of Delay is the golden key that unlocks many doors. It has an astonishing power to transform the mindset of a development organisation."
> — Donald G. Reinertsen

## Formal Definition

Cost of Delay is the **partial derivative of total expected value with respect to time**. More practically: *what would it cost us if this was delayed by one month? What would it be worth to deliver it one month earlier?*

It combines two dimensions humans are notoriously poor at holding simultaneously:
- **Value** — how much is this feature/product worth?
- **Urgency** — how fast is that value decaying?

A feature worth $1M with no urgency has very different CoD than a feature worth $500K that loses 50% of its value each month it's late.

## Why It Matters

Most organisations prioritise by **size of value** alone — biggest business case wins. This is wrong. Without urgency (CoD), you might spend 6 months on a large project when a small fast one would have delivered more total value over the same period.

> "It is often far more valuable to get something even a week earlier than it is to make it slightly cheaper to develop."

## CD3 — Cost of Delay Divided by Duration

Also called **WSJF (Weighted Shortest Job First)**. The prioritisation formula that makes CoD actionable:

```
CD3 = Cost of Delay / Duration
```

Rank work items by this ratio — highest CD3 first. This maximises the economic value delivered in a given time period, given constrained capacity.

**Example:**

| Item | Cost of Delay ($/wk) | Duration (wks) | CD3 |
|---|---|---|---|
| A | $100k | 10 | $10k |
| B | $50k | 2 | $25k |
| C | $80k | 4 | $20k |

Correct order: B → C → A. Despite A having the highest raw CoD, B delivers far more value per unit of capacity consumed.

## CD3 Encourages Smaller Batches

Because duration is in the denominator, CD3 creates natural pressure to **break work into smaller pieces**. A 10-week project becomes more economically attractive if split into smaller deliverable chunks — which is aligned with all the other flow principles around [batch size](./batch-size.md).

## CoD Profiles

Not all work has the same urgency curve over time:

- **Fixed date** — value drops to zero after a deadline (e.g. seasonal feature, regulatory requirement)
- **Urgent standard** — high CoD now, stable after some point
- **Standard** — roughly linear decay; constant CoD per unit time
- **Intangible** — low CoD but cumulative (e.g. tech debt: doesn't hurt much week by week but compounds)

Understanding the profile changes prioritisation decisions dramatically.

## Cross-References

Cost of Delay is the economic articulation of what [Taleb](../people/nassim-taleb.md) calls asymmetric payoffs. Delaying optionality is expensive — you lose the ability to respond to a changing environment. [Naval's](../people/naval-ravikant.md) framing of [compounding](./compounding.md) is the positive mirror: the earlier you start, the longer your compound period.

## Related Pages

- [Donald Reinertsen](../people/donald-reinertsen.md)
- [Queues in Product Development](./queues-in-product-development.md)
- [WIP Limits](./wip-limits.md)
- [Batch Size](./batch-size.md)
- [Little's Law](./littles-law.md)
- [Flow Economics](./flow-economics.md)
- [Compounding](./compounding.md)
- [Shallow Work](./shallow-work.md) — the shallow work that delays high-CoD deep work
- [Seen vs Unseen](./seen-vs-unseen.md) — CoD makes the unseen cost of delay visible

## Connections

- **[Donald Reinertsen](../people/donald-reinertsen.md)** — developed Cost of Delay as the core economic metric in product development
- **[Queues in Product Development](./queues-in-product-development.md)** — CoD quantifies the cost of items sitting in queues
- **[WIP Limits](./wip-limits.md)** — WIP limits force prioritisation by CoD
- **[Seen vs Unseen](./seen-vs-unseen.md)** — CoD makes invisible delay costs visible and measurable
- **[Shallow Work](./shallow-work.md)** — shallow work displaces high-CoD deep work
- **[Compounding](./compounding.md)** — delayed value delivery loses compounding time
