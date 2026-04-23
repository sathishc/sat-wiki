---
title: Flow Economics
tags: [reinertsen, flow, economics, product-development, system-thinking]
created: 2026-04-16
updated: 2026-04-16
sources: [sources/reinertsen-flow.md]
layout: default
parent: Concepts
---

# Flow Economics

The overarching framework in [Reinertsen](../people/donald-reinertsen.md)'s work: treating **every product development decision as an economic decision**, with time as the primary variable. Most organisations optimise for cost; Reinertsen argues they should optimise for **economic flow** — the rate at which value moves through the system.

## The Wrong Optimisation Target

Standard management doctrine optimises for:
- **Resource utilisation** — keep everyone busy, eliminate "idle" time
- **Cost efficiency** — minimise spend per feature
- **Schedule adherence** — hit the date that was planned

Reinertsen's argument: all three are proxies, and all three create perverse incentives that slow the system down.

- High utilisation → queues → slower flow
- Cost optimisation → large batches → slower feedback → more rework
- Schedule adherence → scope negotiation → wrong things built on time

## The Right Optimisation Target

Optimise for the **economic value of flow**: how much value are we delivering per unit time? This reframes every decision:

| Old Question | New Question |
|---|---|
| Can we afford to reduce utilisation? | What does a long queue cost us in [Cost of Delay](./cost-of-delay.md)? |
| Can we afford smaller batches? | What does the current [batch size](./batch-size.md) cost in delayed feedback? |
| Should we add more people? | Would more capacity reduce queue time enough to justify the cost? |
| Should we release now? | What is the Cost of Delay of waiting for the next release window? |

## The Eight Principles in Economic Terms

Reinertsen's eight domains each translate into economic levers:

1. **Economics** — quantify [Cost of Delay](./cost-of-delay.md); every decision has an economic value
2. **Queues** — invisible queues are hidden costs; making them visible makes them manageable
3. **Variability** — variability in arrival and service rates drives queue growth; manage asymmetrically
4. **[Batch Size](./batch-size.md)** — large batches have high holding costs; reduce to improve economics
5. **[WIP Constraints](./wip-limits.md)** — cap WIP to keep queues short; idle capacity is cheaper than queue growth
6. **Flow Control** — manage arrival rate to match capacity; prevent demand spikes from creating queues
7. **Fast Feedback** — feedback is information; delayed feedback is wasted decision-making capacity
8. **Decentralised Control** — decisions should be made where information is freshest; centralisation creates information queues

## Connection to Other Frameworks

### Dalio's [Five-Step Process](./five-step-process.md)
Both Reinertsen and [Dalio](../people/ray-dalio.md) insist on explicit, economic reasoning over gut feel. Dalio's "diagnose root causes" maps directly to Reinertsen's queue diagnosis. Both create [Feedback Loops](./feedback-loops.md) that encode learning into the system.

### Taleb's [Antifragility](./antifragility.md)
Reserve capacity (Reinertsen) = slack against [Black Swans](./black-swan.md) (Taleb). Both argue that over-optimised, high-utilisation systems are fragile. The flow economics insight — that idle capacity has real economic value — is the operational version of antifragility.

### Naval's [Leverage](./leverage.md)
Improving flow economics is a form of leverage: the same people, with better flow, produce more output. Reducing cycle time through queue management is multiplying output without multiplying headcount.

## Related Pages

- [Donald Reinertsen](../people/donald-reinertsen.md)
- [Cost of Delay](./cost-of-delay.md)
- [Queues in Product Development](./queues-in-product-development.md)
- [WIP Limits](./wip-limits.md)
- [Batch Size](./batch-size.md)
- [Little's Law](./littles-law.md)
- [Antifragility](./antifragility.md)
- [Five-Step Process](./five-step-process.md)
- [Leverage](./leverage.md)
- [Flow (Optimal Experience)](./flow-optimal-experience.md) — individual psychological parallel to system-level flow
- [Deep Work](./deep-work.md) — individual-level implementation of the same throughput logic

## Source

- [Reinertsen Flow](../sources/reinertsen-flow.md)
