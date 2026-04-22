---
title: M/M/1 Queue
tags: [queueing-theory, markov, poisson, performance, mathematics]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queueing-theory.md]
layout: default
parent: Concepts
---

# M/M/1 Queue

The **M/M/1 queue** is the simplest and most-studied queueing model. It describes a system with:
- **M**: Markov (Poisson) arrival process
- **M**: Markov (exponential) service time distribution
- **1**: Single server

It's the "spherical cow" of queueing theory — unrealistic but analytically tractable, providing foundational intuition for all queueing systems.

## Assumptions

1. **Arrivals**: Poisson process with rate λ (arrivals per unit time)
   - Inter-arrival times are exponentially distributed
   - Memoryless: past arrivals don't affect future arrivals

2. **Service**: Exponential service time with rate μ (completions per unit time)
   - Average service time = 1/μ
   - Memoryless: time already spent doesn't affect remaining time

3. **One server**: Jobs are served one at a time, FIFO discipline

4. **Infinite capacity**: Queue can grow unbounded (K = ∞)

5. **Infinite population**: Arrivals are independent of queue length (N = ∞)

## Key Parameter: Utilization (ρ)

**ρ = λ/μ**

- ρ = fraction of time the server is busy
- ρ < 1: system is **stable** (queue doesn't grow forever)
- ρ ≥ 1: system is **unstable** (queue grows without bound)

Example: λ = 9 arrivals/hour, μ = 10 completions/hour → ρ = 0.9 (90% utilization)

## Performance Formulas

All formulas assume ρ < 1 (stable system).

### Average Number in System
**L = ρ/(1-ρ)**

- Total customers in system (queue + service)
- At ρ = 0.5: L = 1
- At ρ = 0.9: L = 9
- At ρ = 0.95: L = 19
- At ρ = 0.99: L = 99

**Nonlinear explosion**: As utilization approaches 100%, queue length explodes.

### Average Number in Queue
**Lq = ρ²/(1-ρ) = λ²/(μ(μ-λ))**

- Customers waiting (not including the one being served)
- Lq = L - ρ (subtract the customer in service)

### Average Time in System
**W = 1/(μ-λ) = (1/μ)/(1-ρ)**

- Total time from arrival to departure (wait + service)
- W = 1/μ + Wq (service time + wait time)

### Average Time in Queue
**Wq = ρ/(μ-λ) = λ/(μ(μ-λ))**

- Time spent waiting before service begins
- Wq = W - 1/μ

### Verification via Little's Law

All formulas are consistent with [Little's Law](littles-law.md):
- L = λW ✓
- Lq = λWq ✓
- L = Lq + ρ ✓ (queue + customer in service)

## The Utilization Trap

The most important insight from M/M/1: **queue time is nonlinear in utilization**.

| Utilization (ρ) | L (avg in system) | W (avg time) |
|-----------------|-------------------|--------------|
| 50%             | 1.0               | 2.0/μ        |
| 70%             | 2.3               | 3.3/μ        |
| 80%             | 4.0               | 5.0/μ        |
| 90%             | 9.0               | 10.0/μ       |
| 95%             | 19.0              | 20.0/μ       |
| 99%             | 99.0              | 100.0/μ      |

**Implication**: Running a server at 95% utilization to "maximize efficiency" results in 19x the queue length and 20x the latency compared to 50% utilization.

This is why [Reinertsen's Flow Economics](flow-economics.md) emphasizes keeping utilization below 80%, and why [WIP Limits](wip-limits.md) are essential.

## When M/M/1 Applies

### Good fit:
- Internet-scale request arrivals (Poisson is a good approximation)
- Simple, independent tasks with high variability
- Single-threaded server or serialized processing

### Poor fit:
- Bursty, correlated arrivals (not Poisson)
- Service time is constant or low-variance (use M/D/1 or M/G/1)
- Multiple parallel servers (use [M/M/c](mmc-queue.md))
- Arrivals depend on queue length (finite population models)

## Practical Examples

### Web server with single worker thread
- Requests arrive randomly (λ)
- Each request takes variable time (μ)
- If ρ = 90%, expect 9 requests in system on average
- High latency during traffic spikes

### Database connection pool (size 1)
- Queries arrive at rate λ
- Each query takes 1/μ time on average
- High utilization → long wait times
- Solution: increase pool size ([M/M/c](mmc-queue.md)) or reduce query time (increase μ)

### Single-threaded task processor
- Jobs arrive from queue (λ)
- Processing time is exponential (μ)
- Keep ρ < 80% to avoid queue explosion

## Comparison with Other Models

| Model | Service Time | Result |
|-------|--------------|--------|
| M/M/1 | Exponential (high variance) | Baseline |
| M/D/1 | Deterministic (zero variance) | Lq is **half** of M/M/1 |
| M/G/1 | General distribution | Depends on variance (see [Pollaczek-Khinchin](queue-metrics.md)) |

**Lesson**: **Variance kills queues.** Predictable service time (M/D/1) drastically reduces queueing compared to variable service time (M/M/1), even if the mean is the same.

This is why [Batch Size](batch-size.md) reduction improves flow — smaller batches have lower variance.

## Cross-Framework Connections

### Reinertsen's Flow Economics
The [utilization trap](queues-in-product-development.md) Reinertsen describes is M/M/1 behavior. His recommendation to keep utilization below 80% comes directly from M/M/1 analysis.

**Cost of Delay**: As ρ → 1, W → ∞, so [Cost of Delay](cost-of-delay.md) explodes. High utilization has hidden cost in delayed value delivery.

### Little's Law
M/M/1 formulas are *derived* from [Little's Law](littles-law.md) combined with Markov chain steady-state analysis. Little's Law is the universal constraint; M/M/1 provides the specific solution.

### Systems Thinking (Senge/Meadows)
M/M/1 describes a **stock-flow system**:
- Queue = stock (L)
- Arrivals = inflow (λ)
- Completions = outflow (μ)
- Stock grows when inflow > outflow (ρ > 1)

The **reinforcing loop**: High utilization → slow service → longer queue → even higher utilization (if arrival rate responds to queue length in some systems).

### Taleb's Antifragility
M/M/1 is **fragile**: as ρ → 1, the system becomes extremely sensitive to small variations in λ or μ. A 1% increase in arrival rate can double queue length at high utilization.

**Barbell strategy**: Keep ρ low (50-70%) for robustness, not 95% for "efficiency." The hidden cost of high utilization is tail risk.

### Kahneman's Cognitive Biases
**WYSIATI** (What You See Is All There Is): Visible utilization (ρ) obscures invisible queue length (L). A 95%-utilized server looks efficient but hides a queue 19x larger than at 50%.

**Planning fallacy**: Estimating delivery time using just service time (1/μ) ignores queue time (Wq), which dominates at high utilization.

### Newport's Deep Work
Context switching creates a mental M/M/1 queue. Each interruption is an arrival (λ). Each task requires focus time (1/μ). High "mental utilization" → long queue of half-finished thoughts → no [Deep Work](deep-work.md).

### Allen's GTD
The [GTD inbox](gtd-workflow.md) is an M/M/1 queue. **Clarify** is the service process (μ). If items arrive faster than you clarify them, the inbox explodes. The [Two-Minute Rule](two-minute-rule.md) increases μ for trivial items, reducing Lq.

## Limitations of M/M/1

1. **Service time is rarely exponential**: Most real systems have lower variance (M/G/1 or M/D/1 is more realistic).
2. **Single server is rare**: Most systems have parallelism ([M/M/c](mmc-queue.md)).
3. **Arrivals aren't always Poisson**: Bursty traffic violates the memoryless assumption.
4. **Finite capacity**: Real queues have limits (M/M/1/K model).

But M/M/1 is the **starting point**. It provides closed-form solutions and intuition. More complex models build on M/M/1.

## Key Takeaways

1. **Utilization trap**: Queue length is nonlinear in ρ. 90% → 9x, 95% → 19x, 99% → 99x.
2. **Variance matters**: Exponential service time (high variance) creates long queues. Reducing variance (M/D/1) cuts queue length in half.
3. **Little's Law always applies**: L = λW holds for M/M/1 and every other queueing system.
4. **Keep ρ < 80%**: Trade "efficiency" for predictable latency.
5. **Math matches reality**: The formulas are not abstract—they describe every queue in every system.

## Further Reading

- [Kendall Notation](kendall-notation.md) — M/M/1 in the context of other queue models
- [M/M/c Queue](mmc-queue.md) — multiple servers serving a common queue
- [Queue Metrics](queue-metrics.md) — throughput, latency, utilization, tail latency
- [Little's Law](littles-law.md) — universal relationship L = λW
- [Queues in Product Development](queues-in-product-development.md) — Reinertsen's applied queueing theory

## See Also

- [Flow Economics](flow-economics.md) — optimizing for economic value of flow, not utilization
- [WIP Limits](wip-limits.md) — constraining L to control W
- [Cost of Delay](cost-of-delay.md) — economic cost of time in queue
- [Batch Size](batch-size.md) — smaller batches reduce variance, improving flow
