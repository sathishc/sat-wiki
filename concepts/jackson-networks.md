---
title: Jackson Networks
tags: [queueing-theory, networks, pipelines, distributed-systems, mathematics]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queueing-theory.md]
layout: default
parent: Concepts
---

# Jackson Networks

**Jackson networks** (James R. Jackson, 1957) extend single-queue models ([M/M/1](mm1-queue.md), [M/M/c](mmc-queue.md)) to **networks of queues**. They model multi-stage systems where jobs visit multiple queues in sequence or in complex routing patterns.

Jackson networks are foundational for analyzing build pipelines, multi-stage manufacturing, distributed systems, and any workflow where items pass through multiple processing stages.

## Key Idea

Instead of modeling a single queue in isolation, model the **entire system** as a network of interconnected queues. Jobs arrive from outside, visit one or more queues (in sequence or probabilistically), then exit.

**Product-form solution**: The steady-state distribution of the entire network is the **product** of each queue's individual steady-state distribution. This makes analysis tractable.

## Open Jackson Network

**Definition**:
- External arrivals enter from outside
- Jobs visit multiple queues
- Jobs eventually leave the system
- Each queue is M/M/c with its own service rate

**Model**:
- N queues (stations)
- External arrival rate γ_i to queue i
- Service rate μ_i at queue i (with c_i servers)
- Routing: After service at queue i, job goes to queue j with probability p_ij, or exits with probability p_i0

**Effective arrival rate** (λ_i) at queue i:
- λ_i = γ_i + Σ_j λ_j · p_ji (external arrivals + arrivals from other queues)
- System of linear equations; solve for λ_i

**Stability condition**: Each queue must have ρ_i < 1
- ρ_i = λ_i / (c_i · μ_i)
- If any ρ_i ≥ 1, that queue is unstable → entire network is unstable

**Product-form solution** (Jackson's theorem):
- Steady-state joint distribution: **P(n_1, n_2, ..., n_N) = P_1(n_1) · P_2(n_2) · ... · P_N(n_N)**
- Where P_i(n_i) is the steady-state distribution of queue i in isolation
- **Implication**: Each queue behaves as if it were independent, even though jobs flow between them

**Burke's theorem** (1956): Departures from an M/M/1 (or M/M/c) queue in steady state are **Poisson** with the same rate as arrivals. This explains why Jackson networks have product-form solutions—the output of one queue is valid Poisson input for the next.

## Closed Jackson Network

**Definition**:
- **Fixed number of jobs (K)** circulating in the network
- No external arrivals or departures
- Jobs visit queues repeatedly in a loop

**Use cases**:
- Batch processing systems
- Token-based concurrency limits
- Machine repair models (K machines, 1 repair queue)

**Analysis**:
- More complex than open networks
- **Mean Value Analysis (MVA)** algorithm provides exact solutions
- Normalizing constant must be computed (computationally expensive for large K, N)

**Stability**: Always stable (K is fixed, no unbounded growth)

## Practical Examples

### Build Pipeline (Open Jackson Network)

**Stages**: compile → test → package → deploy
- Queue 1 (compile): μ_1 = 20 builds/hour, c_1 = 2 workers
- Queue 2 (test): μ_2 = 10 tests/hour, c_2 = 3 workers
- Queue 3 (package): μ_3 = 30 packages/hour, c_3 = 1 worker
- Queue 4 (deploy): μ_4 = 15 deploys/hour, c_4 = 1 worker

**External arrivals**: γ = 8 commits/hour enter at compile stage
**Routing**: Deterministic (linear pipeline, p_12 = 1, p_23 = 1, p_34 = 1, p_40 = 1)

**Effective arrival rates**:
- λ_1 = 8 (external)
- λ_2 = 8 (from stage 1)
- λ_3 = 8 (from stage 2)
- λ_4 = 8 (from stage 3)

**Utilization**:
- ρ_1 = 8 / (2 · 20) = 0.2 (20%)
- ρ_2 = 8 / (3 · 10) = 0.27 (27%)
- ρ_3 = 8 / (1 · 30) = 0.27 (27%)
- ρ_4 = 8 / (1 · 15) = 0.53 (53%)

**Bottleneck**: Stage 4 (deploy) has highest utilization (53%). This stage will dominate cycle time if load increases.

**Total cycle time**: W = W_1 + W_2 + W_3 + W_4 (sum of individual queue times)

### Microservices Architecture (Open Jackson Network)

**Services**: Frontend → Auth → Database → Cache → Frontend (response)
- Auth handles authentication requests
- Database queries data
- Cache reduces database load
- Probabilistic routing: 80% cache hit → skip database; 20% cache miss → query database

**Model**:
- External arrivals: γ = 1000 req/s at Frontend
- Routing: p(Frontend→Auth) = 1, p(Auth→Cache) = 1, p(Cache→Database) = 0.2, p(Cache→Frontend) = 0.8, etc.
- Effective arrival rates computed from routing probabilities

**Bottleneck identification**: Compute ρ_i for each service. Highest ρ_i is the bottleneck.

### Data Processing Pipeline (Open Jackson Network)

**Stages**: Ingest → Parse → Transform → Enrich → Store
- Each stage is a queue with its own throughput
- Jobs may skip stages (e.g., already-parsed data enters at Transform)
- Failures route to retry queue (probabilistic routing)

**Analysis**: Solve for λ_i at each stage, compute ρ_i, identify bottleneck.

### Batch Job System (Closed Jackson Network)

**Model**: K jobs circulate between "waiting" and "processing" queues
- Jobs arrive at waiting queue → processed → return to waiting queue (loop)
- K = concurrency limit (e.g., K = 100 concurrent jobs)
- μ_processing = job processing rate

**Result**: Fixed K means no unbounded growth, but high K may still cause long queue times. Use MVA to compute average queue length and cycle time.

## Bottleneck Analysis

**Definition**: The bottleneck is the queue with the **highest utilization** (ρ_i).

**Impact**:
- Bottleneck limits system throughput: X_max = μ_bottleneck
- As load increases, bottleneck queue grows → dominates total cycle time
- Other queues may be idle while bottleneck is saturated

**Optimization**:
1. Identify bottleneck (highest ρ_i)
2. Increase μ_i (optimize processing) or add servers (increase c_i) at bottleneck
3. Re-compute λ_i, ρ_i → new bottleneck may emerge
4. Iterate until system meets throughput/latency targets

**Theory of Constraints** (Goldratt): "Optimizing a non-bottleneck doesn't improve throughput." This is Jackson network analysis in practice.

## Relationship to Little's Law

[Little's Law](littles-law.md) applies to each queue individually **and** to the entire network:

**Per queue**: L_i = λ_i · W_i

**Entire network**: L = λ · W
- L = total jobs in the network
- λ = external arrival rate
- W = average total time in the network

**Implication**: Reducing W (cycle time) requires reducing L (total WIP) or increasing λ (throughput). [WIP Limits](wip-limits.md) enforce this.

## Cross-Framework Connections

### Reinertsen's Flow Economics

Jackson networks mathematically describe [product development flow](queues-in-product-development.md).

**Multi-stage development**: Requirements → Design → Implementation → Test → Deploy
- Each stage is a queue
- [Batch Size](batch-size.md) affects μ_i (processing rate)
- [WIP Limits](wip-limits.md) constrain L_i (queue depth)

**Bottleneck identification**: Reinertsen's "identify the bottleneck, elevate the bottleneck" is Jackson network optimization.

[Cost of Delay](cost-of-delay.md) accumulates across all queues: CD = Σ W_i · value. Optimizing the slowest stage has highest impact.

### Systems Thinking (Senge/Meadows)

Jackson networks are **stock-flow systems**:
- Each queue is a stock (L_i)
- Arrivals are inflow (λ_i)
- Completions are outflow (μ_i)

**Feedback loops**:
- **Balancing loop**: High queue depth at bottleneck → add capacity → queue drains
- **Reinforcing loop** (if arrivals depend on completions): Fast processing → more output → more demand

**Delays**: Capacity changes take time; queues react immediately. [Leverage Points](leverage-points.md) analysis: structural changes (reduce variability, improve routing) beat adding capacity.

### Taleb's Antifragility

Jackson networks are **fragile** to bottlenecks. The bottleneck queue has ρ → 1, so a small increase in λ or decrease in μ causes queue explosion.

**Via negativa**: Remove unnecessary stages (fewer queues) rather than add capacity to bottlenecks.

**Barbell strategy**: Overprovision capacity at the bottleneck (ρ < 70%) to absorb variability.

### Amazon Growth Flywheel

The [Amazon Flywheel](amazon-growth-flywheel.md) is a **closed Jackson network**:
- Customer experience → traffic → sellers → selection → lower cost → lower prices → customer experience (loop)
- Each stage is a queue
- Faster processing at any stage accelerates the entire loop (reinforcing loop)

### OKRs (Doerr/Grove)

**Key Result examples**:
- "Reduce deploy stage cycle time from 4h to 1h" → optimize μ_4 in build pipeline
- "Increase end-to-end pipeline throughput to 50 builds/hour" → balance all stages, eliminate bottleneck

Jackson networks provide the **math** to validate OKR feasibility and measure progress.

### Newport's Deep Work / GTD

**GTD workflow** is a Jackson network:
- Inbox → Clarify → Organize → Do → Complete
- Each stage is a queue
- [Two-Minute Rule](two-minute-rule.md) increases μ_clarify for trivial items

**Bottleneck**: If clarify stage is slow, inbox queue grows. Jackson network analysis: optimize μ_clarify (faster decision-making) or add capacity (batch-clarify sessions).

## Limitations

1. **Assumes exponential service**: M/M/c at each queue (high variance). Real systems often have lower variance (use approximations or simulation).

2. **Assumes Poisson arrivals**: External arrivals and routing are memoryless. Bursty arrivals violate this.

3. **Product-form only for specific topologies**: Jackson's theorem requires specific routing rules (open networks with probabilistic routing, or closed networks). Non-Jackson networks (e.g., priority queues, blocking) require simulation.

4. **Ignores correlation**: Jobs are independent. Real systems have batch arrivals, correlated failures, etc.

But Jackson networks provide **baseline intuition**. More complex models build on Jackson as the starting point.

## Extensions

**BCMP networks** (Baskett, Chandy, Muntz, Palacios, 1975):
- Generalize Jackson to allow different customer classes, different service disciplines, processor sharing
- Still have product-form solutions under certain conditions

**Non-product-form networks**:
- Priority queues, finite buffers, blocking, synchronization
- Require numerical methods or simulation
- Tools: QNAP, SHARPE, SimPy (Python)

## Key Takeaways

1. **Jackson networks model multi-stage systems**: Build pipelines, microservices, manufacturing, workflows
2. **Product-form solution**: Each queue behaves independently → analyze separately, then combine
3. **Burke's theorem**: M/M/1 output is Poisson → chaining queues works
4. **Bottleneck analysis**: Highest ρ_i limits system throughput
5. **Little's Law applies per-queue and network-wide**: L = λW at every level
6. **Optimize the bottleneck**: Adding capacity elsewhere doesn't help

## Further Reading

- [M/M/1 Queue](mm1-queue.md) — single queue, foundation of Jackson networks
- [M/M/c Queue](mmc-queue.md) — each node in Jackson network is M/M/c
- [Little's Law](littles-law.md) — applies to each queue and entire network
- [Kendall Notation](kendall-notation.md) — M/M/c nodes in Jackson networks

## See Also

- [Queues in Product Development](queues-in-product-development.md) — Reinertsen's applied Jackson networks
- [Flow Economics](flow-economics.md) — economic lens on multi-stage flow
- [WIP Limits](wip-limits.md) — constraining L in Jackson networks
- [Cost of Delay](cost-of-delay.md) — economic cost of W across stages
- [Systems Thinking](systems-thinking.md) — stock-flow analysis of queue networks
