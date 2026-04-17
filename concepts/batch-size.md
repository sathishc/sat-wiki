---
title: Batch Size
tags: [reinertsen, flow, lean, batch-size, feedback, cycle-time]
created: 2026-04-16
updated: 2026-04-16
sources: [sources/reinertsen-flow.md]
layout: default
parent: Concepts
---

# Batch Size

The size of a unit of work processed at one time. One of Reinertsen's most powerful levers: **reducing batch size almost always improves flow**, often dramatically and across multiple dimensions simultaneously.

## Why Batch Size Matters

Large batches cause problems across every stage of the development system:

| Problem | Mechanism |
|---|---|
| Long cycle time | Large batches take longer to move through each stage |
| Delayed feedback | You don't find out what's wrong until the whole batch is done |
| Risk accumulation | More can go wrong while a large batch is in progress |
| Long queues | Large batches occupy capacity longer, creating queues for everything behind them |
| Integration problems | Large batches mean large merges → more conflicts → more bugs |
| Harder to prioritise | Big batches bundle many things; harder to sequence by [Cost of Delay](./cost-of-delay.md) |

## The Economics of Small Batches

Small batches have compounding benefits:

1. **Faster feedback** — you learn what works sooner
2. **Reduced risk** — less can go wrong; easier to diagnose when it does
3. **Lower WIP** — smaller in-flight items → lower [Little's Law](./littles-law.md) cycle time
4. **Better prioritisation** — granular items can be ordered by economic priority
5. **Faster release cadence** — more frequent delivery; value reaches users sooner

The catch: there is a **transaction cost** to each batch (setup time, context switch, release overhead). The optimal batch size minimises total cost = holding cost (cost of being slow) + transaction cost (cost per batch). Reinertsen shows that in most knowledge work, organisations are far to the right — batches are too large, and the holding cost dominates.

## Applying This

**In software development:**
- Small commits over large PRs
- Feature flags over big-bang releases
- Thin vertical slices over horizontal layers
- Continuous delivery over scheduled releases
- Daily deployments over monthly release trains

**In product planning:**
- One-week sprints over quarterly planning
- Hypothesis-driven experiments over large roadmap bets
- Incremental specs over complete-before-build documents

## Connection to [Barbell Strategy](./barbell-strategy.md)

[Taleb](../people/nassim-taleb.md)'s barbell and Reinertsen's small batches share a structural logic: small, fast, cheap bets (with limited downside) allow you to gather information and exercise optionality. Large bets are exposed to [Black Swans](./black-swan.md) that appear mid-execution.

## Related Pages

- [Donald Reinertsen](../people/donald-reinertsen.md)
- [WIP Limits](./wip-limits.md)
- [Little's Law](./littles-law.md)
- [Queues in Product Development](./queues-in-product-development.md)
- [Cost of Delay](./cost-of-delay.md)
- [Flow Economics](./flow-economics.md)
- [Barbell Strategy](./barbell-strategy.md) — Taleb parallel
