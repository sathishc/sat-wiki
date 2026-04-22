---
title: M/M/c Queue
tags: [queueing-theory, parallelism, capacity-planning, erlang, mathematics]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queueing-theory.md]
layout: default
parent: Concepts
---

# M/M/c Queue

The **M/M/c queue** extends the [M/M/1](mm1-queue.md) model to **c parallel servers** serving a common queue. It's the foundational model for capacity planning in systems with parallelism: call centers, thread pools, worker fleets, and database connection pools.

## Model Description

In [Kendall Notation](kendall-notation.md): **M/M/c**

- **M**: Poisson arrival process (rate λ)
- **M**: Exponential service time (rate μ per server)
- **c**: Number of parallel servers

All c servers draw from a single shared queue (FIFO). An arriving customer enters service immediately if any server is idle; otherwise, they wait in the queue.

## Key Parameters

- **λ**: Arrival rate (customers per unit time)
- **μ**: Service rate per server (customers per unit time per server)
- **c**: Number of servers
- **ρ**: System utilization = **λ/(cμ)**
  - ρ < 1 required for stability
  - Note: ρ is system utilization, not per-server utilization
  - Each server has utilization λ/(cμ) on average

**Offered load**: **a = λ/μ** (measured in Erlangs)
- a is the "amount of work" arriving per time unit
- If a = 5 and c = 5, then ρ = 100% → unstable
- If a = 5 and c = 10, then ρ = 50% → stable, low queueing

## Erlang C Formula

**Erlang C** (C(c,a)) is the probability that an arriving customer must wait (all servers are busy).

**Formula** (complex, usually computed numerically):

C(c,a) = [a^c / c!] · [c/(c - a)] / [Σ(k=0 to c-1) a^k/k! + (a^c/c!) · c/(c-a)]

Where a = λ/μ (offered load in Erlangs).

**Interpretation**:
- C(c,a) = 0: No queueing (low load or many servers)
- C(c,a) = 1: All arrivals queue (high load or few servers)

**Use case**: Given λ, μ, and target P(wait), solve for required c.

Example: Call center with λ = 100 calls/hour, μ = 10 calls/hour (6-minute average call), target P(wait) < 20% → use Erlang C to find required agents (c).

## Performance Metrics

### Probability of Queueing
**P(wait > 0) = C(c,a)**

### Average Time in Queue (for those who wait)
**Wq = C(c,a) / (cμ - λ)**

### Average Time in System
**W = Wq + 1/μ**

### Average Number in Queue
**Lq = λ · Wq** (via [Little's Law](littles-law.md))

### Average Number in System
**L = λ · W** (via Little's Law)

## Diminishing Returns of Adding Servers

**Key insight**: The first server eliminates all queueing at low load. The second server helps, but less. By the 10th server, marginal benefit is tiny.

| Servers (c) | Utilization (ρ) | P(wait) | Avg Wait Time |
|-------------|-----------------|---------|---------------|
| 1           | 90%             | 90%     | Very high     |
| 2           | 45%             | ~20%    | Moderate      |
| 5           | 18%             | ~2%     | Low           |
| 10          | 9%              | ~0.1%   | Negligible    |

(Assuming a = 0.9 Erlangs)

**Implication**: Adding capacity has **diminishing returns**. Structural changes (reduce λ, increase μ, change service distribution) often beat adding more servers.

This is why [Reinertsen's Flow Economics](flow-economics.md) emphasizes reducing batch size and variability over just adding capacity.

## M/M/c vs M/M/1

Compare M/M/c (c servers, shared queue) with **c separate M/M/1 queues** (c servers, each with dedicated queue, random routing).

**Result**: M/M/c (shared queue) has **lower average wait time** than c × M/M/1.

**Reason**: Load balancing. In M/M/1, a customer might wait while another queue is idle. In M/M/c, idle servers always serve waiting customers immediately.

**Practical implication**: Thread pools, worker pools, and connection pools should use **shared queues**, not dedicated per-worker queues.

## Practical Examples

### Call Center
- Incoming calls (λ = Poisson)
- c agents (parallel servers)
- Call duration exponential (μ)
- Goal: P(wait > 0) < 20% → use Erlang C to size agent pool

### Database Connection Pool
- Query arrivals (λ)
- Pool size c (max concurrent queries)
- Query execution time (μ)
- If ρ > 90%, queries queue → increase c or optimize queries (increase μ)

### Thread Pool / Worker Fleet
- Tasks arrive at rate λ
- c worker threads/processes
- Each task takes 1/μ time
- Keep ρ < 80% to avoid queueing delay

### Web Server (Nginx, Apache)
- HTTP requests arrive (λ)
- c worker processes/threads
- Request handling time (μ)
- Auto-scaling: add workers (increase c) when ρ > threshold

### Kubernetes Pods
- Incoming load (λ)
- Pod replicas (c)
- Request processing time (μ)
- HorizontalPodAutoscaler adds pods when utilization crosses threshold

## When to Use M/M/c

**Good fit**:
- Multiple parallel workers serving a shared queue
- Independent tasks (no dependencies)
- Roughly exponential service times (or use M/G/c approximations)

**Poor fit**:
- Service time is deterministic (use M/D/c approximations)
- Low variance service time (M/G/c)
- Arrivals are bursty or correlated
- Tasks have dependencies (use [Jackson Networks](jackson-networks.md))

## Erlang B vs Erlang C

**Erlang B** (M/M/c/c model):
- **No queue**: blocked customers are lost (rejected)
- System capacity = c (K = c in Kendall notation)
- Use case: Trunked phone lines, connection-oriented systems

**Erlang C** (M/M/c model):
- **Infinite queue**: customers always wait
- Use case: Most software systems (task queues, call centers)

**Which to use?**
- If overflow is rejected → Erlang B
- If overflow waits → Erlang C

Most modern systems use Erlang C (infinite or very large queue capacity).

## Capacity Planning with M/M/c

**Problem**: Given λ, μ, and SLA target (e.g., P95 latency < X), find required c.

**Steps**:
1. Measure or estimate λ (arrival rate)
2. Measure or estimate μ (service rate per worker)
3. Choose target ρ (e.g., 70% for safety margin)
4. Calculate a = λ/μ (offered load)
5. Solve c ≥ a/ρ (e.g., if a=7 and ρ=0.7, then c ≥ 10)
6. Validate using Erlang C: does P(wait) meet SLA?
7. Add buffer for variability, growth, failures (e.g., +20%)

**Pro tip**: Don't target ρ > 90%. The M/M/c formulas show that queue time explodes as ρ → 1, just like [M/M/1](mm1-queue.md).

## Cross-Framework Connections

### Reinertsen's Flow Economics
M/M/c underpins [capacity planning in product development](queues-in-product-development.md). Teams are servers (c), work items are arrivals (λ). [WIP Limits](wip-limits.md) enforce ρ < 1.

**Insight**: Adding headcount (increasing c) has diminishing returns. Better: reduce batch size (reduce λ per item) or improve capability (increase μ).

### Little's Law
All M/M/c metrics are consistent with [Little's Law](littles-law.md): L = λW, Lq = λWq. Little's Law applies regardless of c.

### Systems Thinking (Senge/Meadows)
M/M/c is a **stock-flow system** with parallel outflows:
- Queue = stock (L)
- Arrivals = inflow (λ)
- Completions = c parallel outflows (μ each)
- System is stable when total outflow (cμ) > inflow (λ)

**Leverage point**: Increasing c (servers) is a Level 9 intervention (low leverage). Reducing λ or increasing μ (structural changes) are higher leverage.

### Taleb's Barbell Strategy
M/M/c at high ρ is **fragile**. A small increase in λ or decrease in μ (due to server failure) causes queue explosion.

**Barbell approach**: Overprovision capacity (ρ = 50-70%) for robustness, not efficiency. The "waste" is insurance against tail risk.

### Amazon Leadership Principles
**"Customer Obsession" + "Frugality"**: Balance low latency (low ρ) with cost efficiency (high ρ). Erlang C provides the math to navigate this trade-off.

**Auto-scaling**: AWS Lambda, ECS, EKS all use M/M/c-like models to scale c dynamically based on λ.

### OKRs (Doerr/Grove)
**Key Result example**: "P95 API latency < 100ms"
- Requires ρ < threshold for M/M/c
- Monitoring: track λ, μ, c, ρ, Wq
- Action: scale c or optimize μ when ρ crosses threshold

## Advanced Topics

### M/G/c (General Service Distribution)
M/M/c assumes exponential service time (high variance). Most real systems have lower variance. **M/G/c** uses the **Pollaczek-Khinchin** extension but has no closed-form solution—numerical methods or simulation required.

**Rule of thumb**: If service time variance is low, M/M/c overpredicts queue length. Actual performance will be better than M/M/c predicts.

### M/M/c/K (Finite Capacity)
If queue has maximum size K, arriving customers are rejected when system is full. This is **M/M/c/K**, intermediate between Erlang C (infinite queue) and Erlang B (zero queue).

### Impatient Customers
If customers leave the queue after waiting too long (balking/reneging), the model becomes **M/M/c with impatience**. More complex, usually requires simulation.

## Key Takeaways

1. **Shared queue beats dedicated queues**: M/M/c has lower average wait time than c separate M/M/1 queues.
2. **Diminishing returns**: Adding servers helps less and less as c increases.
3. **Erlang C**: The standard formula for P(wait > 0) in M/M/c systems.
4. **Keep ρ < 80%**: High utilization causes queueing, just like M/M/1.
5. **Capacity planning**: Use M/M/c + Erlang C to size worker pools, thread pools, and service fleets.

## Further Reading

- [M/M/1 Queue](mm1-queue.md) — single-server baseline
- [Kendall Notation](kendall-notation.md) — M/M/c in the taxonomy of queueing models
- [Erlang Formulas](erlang-formulas.md) — Erlang B, Erlang C, and capacity planning
- [Queue Metrics](queue-metrics.md) — throughput, latency, utilization, tail latency
- [Little's Law](littles-law.md) — L = λW applies to M/M/c

## See Also

- [Message Queues](message-queues.md) — distributed implementations of M/M/c
- [Backpressure](backpressure.md) — preventing unbounded queue growth
- [Flow Economics](flow-economics.md) — economic lens on capacity planning
- [WIP Limits](wip-limits.md) — enforcing ρ < 1 in product development
