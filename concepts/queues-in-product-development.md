---
title: Queues in Product Development
tags: [reinertsen, flow, queues, cycle-time, utilisation, product-development]
created: 2026-04-16
updated: 2026-04-16
sources: [sources/reinertsen-flow.md]
---

# Queues in Product Development

The central villain in [Reinertsen](../people/donald-reinertsen.md)'s framework. Queues — work waiting to be worked on — are the **root cause of slow delivery, poor quality, and unpredictability** in product development. The problem: they are almost entirely **invisible**.

> "Queues are the single most important factor in determining the speed of product development."

## What a Queue Is

In product development, a queue is any work item waiting for attention:
- Features waiting for prioritisation
- Code waiting for code review
- Specs waiting for design
- Designs waiting for engineering
- Builds waiting for QA
- PRs waiting to be merged

Unlike physical queues (you can see the pile of boxes), knowledge work queues are invisible — they live in Jira backlogs, inboxes, and "in progress" columns nobody looks at.

## Why Queues Form: The Utilisation Trap

The counterintuitive root cause: **trying to keep everyone busy**.

> "Utilisation has a nonlinear effect on cycle time. As utilisation approaches 100%, cycle time approaches infinity."

This is not opinion — it is queueing theory. [Little's Law](./littles-law.md) and the M/M/1 queue model both predict it mathematically. The relationship looks like a hockey stick: at 80% utilisation, cycle time is manageable; at 90% it doubles; at 95% it doubles again; at 99% it's catastrophic.

**The utilisation trap:**
1. Management wants high resource utilisation (everyone busy = efficient)
2. High utilisation → long queues → long cycle times
3. Long cycle times → large [batch sizes](./batch-size.md) (you batch work to justify the wait)
4. Large batches → more variability → longer queues
5. Repeat

The "efficient" organisation is actually systematically inefficient.

## The Cost of Invisible Queues

Queues exact costs that most organisations never measure:

- **Longer cycle time** — the queue is waiting time added to every item's journey
- **Risk accumulation** — the longer something sits, the more the world changes around it
- **Feedback delay** — you don't discover problems until much later
- **Context switching** — people work on many things in parallel, each with its own queue
- **Morale** — work disappears into a backlog and never seems to ship

## How to Attack Queues

Reinertsen's prescription:

1. **Make queues visible** — put WIP on a board; measure queue length and wait time
2. **Limit WIP** — use [WIP limits](./wip-limits.md) to constrain how much enters the system
3. **Reduce [batch size](./batch-size.md)** — smaller batches move through faster and create less queue buildup
4. **Manage by [Cost of Delay](./cost-of-delay.md)** — don't treat all queued items equally; prioritise by economic urgency
5. **Reserve capacity** — don't run at 100% utilisation; slack is not waste, it's queue control

## Reserves Are Not Waste

One of Reinertsen's most counter-cultural points: **idle capacity is the price of fast response**. An organisation running at 100% utilisation cannot respond to anything unexpected without creating a massive queue. Slack is not inefficiency — it is the mechanism that keeps queues short.

This directly echoes [Taleb](../people/nassim-taleb.md): over-optimised systems are fragile. Reserve capacity is [antifragility](./antifragility.md) at the operational level.

## Related Pages

- [Donald Reinertsen](../people/donald-reinertsen.md)
- [WIP Limits](./wip-limits.md)
- [Little's Law](./littles-law.md)
- [Batch Size](./batch-size.md)
- [Cost of Delay](./cost-of-delay.md)
- [Flow Economics](./flow-economics.md)
- [Antifragility](./antifragility.md) — over-optimisation = fragility
