---
title: Little's Law
tags: [reinertsen, queueing-theory, flow, cycle-time, wip, mathematics]
created: 2026-04-16
updated: 2026-04-22
sources: [sources/reinertsen-flow.md, sources/queuing-theory-systems.md]
layout: default
parent: Concepts
---

# Little's Law

A theorem from queueing theory, proved by John Little (1961). The mathematical foundation underneath much of [Reinertsen](../people/donald-reinertsen.md)'s flow framework. **The most important law in queueing theory** — it works for ANY stable queueing system regardless of arrival distribution, service distribution, or queue discipline.

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

## Universality: Why Little's Law Always Works

The formula is remarkably robust — it holds **regardless of**:
- **Arrival distribution** (Poisson, bursty, scheduled, correlated)
- **Service distribution** (exponential, fixed, variable)
- **Queue discipline** (FIFO, LIFO, priority, random)
- **Number of servers** (single server, multiple servers)
- **Network topology** (single queue, [queueing networks](queueing-networks.md))

**Only requirement**: The system must be **stable** (average arrival rate = average departure rate over long term).

This is why Little's Law is the bridge between different queueing models. Whether you're analyzing an M/M/1 queue (see [Kendall notation](kendall-notation.md)) or a complex distributed system, L = λW always holds.

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

## Applications Across Domains

**Product development** ([Reinertsen](../people/donald-reinertsen.md)):
- L = features in progress (WIP)
- λ = features shipped per week (throughput)
- W = time from start to done (cycle time)

**Message queues** (see [Message Queues](message-queues.md)):
- L = queue depth (messages waiting + being processed)
- λ = message processing rate (msgs/sec)
- W = end-to-end latency (enqueue to ack)

**Call centers** (see [Erlang Formulas](erlang-formulas.md)):
- L = callers in system (on hold + being served)
- λ = call arrival rate (calls/hour)
- W = average time in system (wait + talk time)

**Microservices**:
- L = requests in flight (HTTP connections, gRPC streams)
- λ = throughput (requests/sec)
- W = end-to-end latency (client perspective)

**CI/CD pipelines**:
- L = jobs in pipeline (build + test + deploy queues)
- λ = deployments per day
- W = commit-to-production time

## Derivation-Free Proof

**Intuition**: In steady state, items entering = items leaving. Tag a single item and track it from arrival to departure. Its time in system (W) must equal the average number of items in system (L) divided by the rate items flow through (λ).

**Why it's distribution-free**: The proof doesn't depend on HOW items arrive or HOW long they take to serve. It's a conservation law — what goes in must come out.

## Connection to [Compounding](./compounding.md)

Little's Law has a compounding-like quality: small reductions in WIP produce cycle time improvements that persist and multiply. A team that halves its WIP roughly halves its cycle time — which means faster feedback, fewer bugs, faster learning — which further improves throughput. The gains compound.

## Relation to Other Queueing Models

**[M/M/1 Queue](kendall-notation.md#mm1)**:
- Gives specific formulas for L, W given λ and μ (service rate)
- Little's Law relates them: L = λW
- M/M/1 tells you WHAT L and W are; Little's Law relates them

**[Erlang-C](erlang-formulas.md)**:
- Gives W (wait time) for M/M/c queues
- Apply Little's Law: L = λW to get queue depth

**[Queueing Networks](queueing-networks.md)**:
- Little's Law applies to EACH queue AND to the network as a whole
- End-to-end L = sum of per-queue L
- End-to-end W = sum (serial) or max (parallel) of per-queue W

## Connection to [Backpressure](backpressure.md)

**Backpressure mechanisms control λ (arrival rate) to cap L (queue depth).**

From Little's Law:
- If L is bounded (max queue depth = K)
- And W is roughly constant (predictable service time)
- Then λ must be capped: λ ≤ K/W

This is why [bounded queues](message-queues.md) implement backpressure — they enforce the L constraint, which mathematically requires capping λ.

## Related Pages

### Queueing Theory Foundations
- [Kendall Notation](kendall-notation.md) — M/M/1, M/M/c models where Little's Law applies
- [Erlang Formulas](erlang-formulas.md) — capacity planning with Little's Law
- [Queueing Networks](queueing-networks.md) — Little's Law in multi-stage systems

### Systems Architecture
- [Message Queues](message-queues.md) — L = queue depth, monitoring with Little's Law
- [Backpressure](backpressure.md) — controlling λ to cap L
- [Queue-Based Load Leveling](queue-based-load-leveling.md) — λ spikes → L grows → W increases

### Product Development
- [Donald Reinertsen](../people/donald-reinertsen.md)
- [WIP Limits](./wip-limits.md) — operational implementation of Little's Law
- [Queues in Product Development](./queues-in-product-development.md)
- [Batch Size](./batch-size.md)
- [Flow Economics](./flow-economics.md)
