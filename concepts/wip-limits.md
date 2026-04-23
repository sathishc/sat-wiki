---
title: WIP Limits
tags: [reinertsen, kanban, flow, wip, cycle-time, product-development]
created: 2026-04-16
updated: 2026-04-16
sources: [sources/reinertsen-flow.md]
layout: default
parent: Concepts
---

# WIP Limits

Work-In-Progress limits — constraints on how many items can be actively in a given stage of work at any time. The primary operational mechanism for controlling [queues](./queues-in-product-development.md) and reducing cycle time, derived directly from [Little's Law](./littles-law.md).

> "Stop starting. Start finishing."

## Why WIP Limits Work

From [Little's Law](./littles-law.md): `Cycle Time = WIP / Throughput`. Holding throughput roughly constant, reducing WIP directly reduces cycle time. WIP limits enforce this reduction by preventing new work from entering a stage until existing work exits.

The mechanism:
1. WIP limit is reached → new work cannot start
2. Team is forced to finish something before pulling new work in
3. Queues shrink → items flow through faster
4. Faster flow → shorter feedback loops → fewer defects accumulate → quality improves

## The Counter-Intuitive Truth

WIP limits feel like slowing down. You have to *stop* people from starting work. This feels wrong — idle people look unproductive. But [Reinertsen](../people/donald-reinertsen.md) (and queueing theory) are clear: **idle people with short queues outperform busy people with long queues**, because the busy team's cycle time is 3x longer and their feedback loops are too slow to catch problems early.

This is [Taleb](../people/nassim-taleb.md)'s [antifragility](./antifragility.md) applied operationally: reserve capacity is not waste; it is the system's ability to absorb variability without collapsing into a long queue.

## Setting WIP Limits

No universal rule, but common starting points:
- **Per stage:** number of team members working on that stage (or n+1 as a starting point)
- **Total system WIP:** 1–2x team size
- **The test:** if your team never hits the limit, it's too high; if work is constantly blocked, it may be too low

WIP limits should be slightly constraining — they should force occasional hard decisions about priority.

## WIP Limits Force Prioritisation

When the WIP limit is hit, the team cannot simply add work — they must choose what to pull next. This forces explicit prioritisation by [Cost of Delay](./cost-of-delay.md) rather than "whatever someone asked for most recently."

WIP limits make the economic trade-off visible and unavoidable.

## Relationship to Batch Size

WIP limits and [batch size](./batch-size.md) are complementary. Smaller batches mean items spend less time in each stage → WIP naturally stays lower → cycle time falls further. Combining both is multiplicative: smaller batches + WIP limits produces dramatically faster flow than either alone.

## Connections

- [Donald Reinertsen](../people/donald-reinertsen.md)
- [Little's Law](./littles-law.md)
- [Queues in Product Development](./queues-in-product-development.md)
- [Batch Size](./batch-size.md)
- [Cost of Delay](./cost-of-delay.md)
- [Deep Work](./deep-work.md) — WIP limits for knowledge work mirror Newport's prescription: finish one deep work block before starting another; context switching is cognitive WIP
- [Crossing the Chasm](./crossing-the-chasm.md) — beachhead focus is strategic WIP limiting: do one segment completely before opening the next
- [Flow Economics](./flow-economics.md)
- [Antifragility](./antifragility.md)

## Source

- [Reinertsen Flow](../sources/reinertsen-flow.md)
