---
title: Kendall Notation
tags: [queueing-theory, notation, classification, mathematics]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queueing-theory.md]
layout: default
parent: Concepts
---

# Kendall Notation

Kendall notation (developed by David George Kendall, 1953) is the standard classification system for queueing models. It describes a queue's characteristics using a compact symbolic form: **A/B/c/K/N/D**.

## The Six Elements

1. **A** — Arrival process distribution
   - M = Markov (memoryless, exponential inter-arrival times, Poisson process)
   - D = Deterministic (fixed inter-arrival times)
   - G = General (arbitrary distribution)
   - E_k = Erlang-k distribution
   - H = Hyperexponential distribution

2. **B** — Service time distribution
   - Same notation as A
   - M = exponential service times
   - D = constant service times
   - G = arbitrary service time distribution

3. **c** — Number of servers
   - 1, 2, 3, ... (parallel servers serving a common queue)
   - c = 1: single-server queue
   - c > 1: multi-server queue

4. **K** — System capacity (optional, default = ∞)
   - Maximum number of customers in system (queue + service)
   - K = ∞: unbounded queue
   - K = c: no queue, only service slots (Erlang B model)

5. **N** — Population size (optional, default = ∞)
   - N = ∞: infinite source (open system)
   - N < ∞: finite source (closed system, machine repair models)

6. **D** — Service discipline (optional, default = FIFO)
   - FIFO: First-In-First-Out
   - LIFO: Last-In-First-Out
   - SIRO: Service In Random Order
   - Priority: preemptive or non-preemptive priorities
   - PS: Processor Sharing (all customers served simultaneously)

## Common Shorthand

When K = ∞, N = ∞, and D = FIFO (the most common case), the notation simplifies to **A/B/c**.

Examples:
- **M/M/1** = Poisson arrivals, exponential service, single server, infinite capacity, infinite population, FIFO
- **M/M/c** = Poisson arrivals, exponential service, c servers
- **M/G/1** = Poisson arrivals, general service distribution, single server
- **M/D/1** = Poisson arrivals, deterministic service, single server

## Standard Models

### M/M/1
The simplest and most-studied queue. Analytically tractable, closed-form solutions for all metrics. See [M/M/1 Queue](mm1-queue.md).

**Key property**: Memoryless arrival and service processes → Markov chain analysis applies.

### M/M/c
Multiple parallel servers serving a common queue. See [M/M/c Queue](mmc-queue.md).

**Use case**: Call centers, thread pools, parallel workers.

### M/G/1
Poisson arrivals, but **arbitrary** service time distribution. More realistic than M/M/1 for systems where service time variance matters.

**Key insight**: The [Pollaczek-Khinchin formula](queue-metrics.md) shows that service time *variance* directly affects queue length. High variance = longer queues, even if mean service time is unchanged.

### M/D/1
Poisson arrivals, **deterministic** service time (constant). Special case of M/G/1 where variance = 0.

**Result**: Queue length is *half* that of M/M/1 with the same mean service time. Predictability reduces queueing.

### G/G/1
General arrival process, general service process, single server. Most realistic, but hard to analyze.

**Kingman's approximation** (1961) provides bounds, but no closed-form solution. Simulation is often necessary.

## Why Kendall Notation Matters

1. **Communication**: "M/M/c" instantly conveys arrival/service assumptions and server count to anyone familiar with queueing theory.

2. **Model selection**: Choosing the right model depends on your system's characteristics. Is arrival rate truly memoryless? Is service time constant or variable?

3. **Analysis tractability**: M/M/* models have closed-form solutions. M/G/1 has the PK formula. G/G/1 requires simulation. Kendall notation signals which tools apply.

4. **Mismatch detection**: If you model a system as M/M/1 but service times have high variance, predictions will be wrong. Kendall notation forces you to articulate assumptions.

## Choosing the Right Model

| System Characteristic | Arrival (A) | Service (B) | Notes |
|----------------------|-------------|-------------|-------|
| Independent random arrivals at constant average rate | M | - | Poisson process; memoryless |
| Fixed arrival schedule | D | - | Deterministic; no randomness |
| Bursty arrivals with memory | G | - | Use general distribution or simulation |
| Service time is exponential (highly variable) | - | M | Simple but often unrealistic |
| Service time is constant | - | D | Assembly lines, fixed-duration tasks |
| Service time is variable but not exponential | - | G | Most real systems; use M/G/1 formula |

**Rule of thumb**: Start with M/M/1 for simplicity. If predictions don't match reality, upgrade to M/G/1 (if service variance is the issue) or M/M/c (if parallelism matters).

## Cross-Framework Connections

### Reinertsen's Flow Economics
Reinertsen's work is applied queueing theory without always naming it. His [Queues in Product Development](queues-in-product-development.md) implicitly uses M/M/1 or M/G/1 models. The **utilization trap** he describes is M/M/1 behavior.

### Systems Thinking (Senge/Meadows)
Kendall notation describes the *structure* of a queue. [Systems Thinking](systems-thinking.md) analyzes the *dynamics* — how queues interact with feedback loops, delays, and policy changes. Kendall notation = static structure; systems thinking = dynamic behavior.

### Little's Law
Kendall notation describes *which* queue model; [Little's Law](littles-law.md) (L = λW) applies *regardless* of the model. It's model-agnostic, while Kendall notation is model-specific.

## Historical Note

David George Kendall (1918–2007) was a British mathematician. He introduced this notation in 1953, formalizing what had been ad-hoc descriptions. It became the universal standard for queueing theory.

Before Kendall, researchers would write paragraphs describing arrival processes, service distributions, and server configurations. Kendall notation compressed this into a 5-6 character code.

## Further Reading

- [M/M/1 Queue](mm1-queue.md) — simplest Markov queue
- [M/M/c Queue](mmc-queue.md) — multi-server extension
- [Queue Metrics](queue-metrics.md) — throughput, latency, utilization, queue depth
- [Little's Law](littles-law.md) — universal relationship between L, λ, W
- [Jackson Networks](jackson-networks.md) — networks of M/M/c queues

## See Also

- [Queues in Product Development](queues-in-product-development.md) — Reinertsen's applied queueing theory
- [Systems Thinking](systems-thinking.md) — queue dynamics in feedback loops
- [WIP Limits](wip-limits.md) — constraining L to control W (Little's Law)
