---
title: Queues in Product Development
tags: [reinertsen, flow, queues, cycle-time, utilisation, product-development]
created: 2026-04-16
updated: 2026-04-22
sources: [sources/reinertsen-flow.md, sources/queuing-theory-systems.md]
layout: default
parent: Concepts
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

This is not opinion — it is queueing theory. [Little's Law](./littles-law.md) and the **M/M/1 queue model** (see [Kendall notation](kendall-notation.md)) both predict it mathematically.

### The Math: M/M/1 Queue

For a single-server queue with exponential arrivals and service:
- **ρ = λ/μ** (utilization = arrival rate / service rate)
- **W = 1/(μ - λ)** (average wait time)
- As ρ → 1, W → ∞

**Concrete numbers** (assuming μ = 1 item/day):

| Utilization (ρ) | Avg Wait Time (W) | Multiple of Service Time |
|---|---|---|
| 50% | 1 day | 1× |
| 70% | 1.7 days | 1.7× |
| 80% | 2.5 days | 2.5× |
| 90% | 5 days | 5× |
| 95% | 10 days | 10× |
| 99% | 50 days | 50× |

The relationship is **nonlinear** (exponential). This is the hockey stick: at 80% utilization, cycle time is manageable; at 90% it doubles; at 95% it doubles again; at 99% it's catastrophic.

**Real product development is WORSE than M/M/1** because:
1. Service times have high variance (some features take 1 day, some take 10)
2. M/G/1 model (general service distribution) shows: higher variance → longer queues
3. Product dev is closer to 95th percentile service time, not average

**The utilisation trap:**
1. Management wants high resource utilisation (everyone busy = efficient)
2. High utilisation → long queues → long cycle times
3. Long cycle times → large [batch sizes](./batch-size.md) (you batch work to justify the wait)
4. Large batches → more variability (M/G/1) → even longer queues
5. Repeat (reinforcing feedback loop)

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

**From queueing theory**: To keep average wait time W below 2× service time, utilization must stay below 70%. To keep it below 3×, utilization < 80%.

**Practical target**: Operate at **70-80% utilization**. The remaining 20-30% is not "waste" — it's the capacity that allows you to respond to urgent work, handle variability, and prevent queue explosion.

This directly echoes [Taleb](../people/nassim-taleb.md): over-optimised systems are fragile. Reserve capacity is [antifragility](./antifragility.md) at the operational level. [Erlang formulas](erlang-formulas.md) quantify this: to hit service-level targets, you must overprovision beyond average load.

## Connection to Message Queues and Distributed Systems

Product development queues are **invisible** (Jira backlogs, PR queues). Message queues in distributed systems are **visible** (queue depth metrics).

But the math is identical:
- Product dev team = server pool processing features
- [Message queue](message-queues.md) workers = server pool processing messages
- Both follow M/M/c model (multiple servers)
- Both hit utilization trap at ρ → 1

**Systems lessons that apply to product dev**:
- Monitor queue depth (make WIP visible)
- [Backpressure](backpressure.md) (WIP limits, say no to new work)
- [Dead Letter Queue](dead-letter-queues.md) (parking lot for blocked work)
- [Priority queues](priority-queues.md) (expedite by [Cost of Delay](cost-of-delay.md))
- [Queue-based load leveling](queue-based-load-leveling.md) (absorb demand spikes)

The infrastructure patterns ARE the product development patterns. Same math, different vocabulary.

## Connections

### Queueing Theory Foundations
- [Little's Law](./littles-law.md) — L = λW (WIP = throughput × cycle time)
- [Kendall Notation](kendall-notation.md) — M/M/1, M/G/1 models of product dev queues
- [Erlang Formulas](erlang-formulas.md) — capacity planning (team sizing)
- [Queueing Networks](queueing-networks.md) — multi-stage pipelines (design → code → test → deploy)

### Systems Architecture Patterns
- [Message Queues](message-queues.md) — same patterns, different domain
- [Backpressure](backpressure.md) — WIP limits as backpressure
- [Queue-Based Load Leveling](queue-based-load-leveling.md) — absorbing demand spikes
- [Dead Letter Queues](dead-letter-queues.md) — parking lot for blocked work
- [Priority Queues](priority-queues.md) — expedite by CoD

### Product Development
- [Donald Reinertsen](../people/donald-reinertsen.md)
- [WIP Limits](./wip-limits.md)
- [Batch Size](./batch-size.md)
- [Cost of Delay](./cost-of-delay.md)
- [Flow Economics](./flow-economics.md)

### Cross-Framework
- [Shallow Work](./shallow-work.md) — shallow work obligations create cognitive queues; Newport's shutdown ritual is the cognitive equivalent of queue clearing
- [Antifragility](./antifragility.md) — over-optimisation = fragility; reserve capacity = robustness
- [Systems Thinking](systems-thinking.md) — queue = stock; utilization trap = reinforcing loop
