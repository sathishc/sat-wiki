---
title: Erlang Formulas
tags: [queueing-theory, erlang, capacity-planning, telecommunications, mathematics]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queueing-theory.md]
layout: default
parent: Concepts
---

# Erlang Formulas

The **Erlang formulas** are foundational equations in queueing theory for capacity planning and performance analysis. Developed by Danish mathematician **Agner Krarup Erlang** (1878–1929) for the Copenhagen Telephone Company, they remain the gold standard for sizing systems with random arrivals and finite resources.

## Historical Context

**Agner Krarup Erlang** (1909) pioneered queueing theory while solving a practical problem: how many telephone lines does a telephone exchange need?

- **Problem**: Calls arrive randomly; if all lines are busy, the call is blocked
- **Goal**: Size the system so blocking probability is acceptably low
- **Result**: Erlang B formula (1917) and later Erlang C formula

Erlang's work predated formal queueing theory and remains the most-used capacity planning tool in telecommunications, call centers, and systems engineering.

**Unit of measurement**: The **Erlang** is named after him. 1 Erlang = continuous use of 1 server.

## Offered Load (Erlangs)

**Offered load (a)** = λ/μ (dimensionless, measured in Erlangs)

- λ = arrival rate (calls, requests, jobs per unit time)
- μ = service rate (completions per unit time per server)
- a = "amount of work" arriving per time unit

**Interpretation**:
- a = 1 Erlang: enough work to keep 1 server continuously busy
- a = 5 Erlangs: enough work to keep 5 servers continuously busy
- a = 0.5 Erlangs: enough work to keep 1 server busy 50% of the time

**Example**: λ = 100 calls/hour, average call duration = 6 minutes (μ = 10 calls/hour)
- a = 100/10 = 10 Erlangs
- Need at least 10 agents to keep up (and more to handle queueing)

## Erlang B Formula

**Model**: M/M/c/c in [Kendall Notation](kendall-notation.md)
- Poisson arrivals (rate λ)
- Exponential service (rate μ per server)
- c servers
- **No queue**: blocked calls are lost (system capacity = c)

**Erlang B (E_B(c,a))** = Probability that an arriving call is blocked

**Formula**:

E_B(c,a) = (a^c / c!) / Σ(k=0 to c) (a^k / k!)

Where:
- a = offered load (Erlangs)
- c = number of servers

**Use case**: Systems where overflow is **rejected**, not queued
- Trunked telephone lines
- Connection-oriented systems with limited capacity
- Circuit-switched networks

**Capacity planning**:
- Given a (offered load) and target blocking probability (e.g., 1%), solve for c
- Example: a = 10 Erlangs, target P(blocking) < 1% → c = 16 lines (from Erlang B table)

### Erlang B Table (Sample)

| Offered Load (a) | c (servers) for P(block) < 1% | c for P(block) < 5% |
|------------------|-------------------------------|---------------------|
| 1                | 5                             | 3                   |
| 5                | 11                            | 8                   |
| 10               | 17                            | 14                  |
| 20               | 29                            | 25                  |
| 50               | 62                            | 56                  |

**Observation**: To achieve low blocking, you need c significantly > a. Pure utilization-based sizing (c = a) results in unacceptable blocking.

## Erlang C Formula

**Model**: M/M/c in [Kendall Notation](kendall-notation.md)
- Poisson arrivals (rate λ)
- Exponential service (rate μ per server)
- c servers
- **Infinite queue**: customers wait if all servers are busy

**Erlang C (C(c,a))** = Probability that an arriving customer must wait

**Formula** (complex, usually computed numerically):

C(c,a) = [a^c / c!] · [c/(c - a)] / [Σ(k=0 to c-1) a^k/k! + (a^c/c!) · c/(c-a)]

Where:
- a = offered load (Erlangs)
- c = number of servers
- Requires: a < c (otherwise system is unstable)

**Use case**: Systems where overflow **waits in queue**
- Call centers
- Help desks
- Task queues
- API servers
- Database connection pools

**Derived metrics** (given C(c,a)):

1. **Average time in queue** (for customers who wait):
   - **Wq = C(c,a) / (cμ - λ)**

2. **Average time in system**:
   - **W = Wq + 1/μ**

3. **Probability customer waits > t seconds**:
   - **P(W > t) = C(c,a) · e^(-(cμ-λ)t)**

**Capacity planning**:
- Given a, target P(wait) or target average wait time → solve for c
- Example: a = 10 Erlangs, target P(wait) < 20% → c = 13 agents (from Erlang C calculator)

### Erlang C Table (Sample)

| Offered Load (a) | c for P(wait) < 10% | c for P(wait) < 20% |
|------------------|---------------------|---------------------|
| 1                | 2                   | 2                   |
| 5                | 7                   | 6                   |
| 10               | 14                  | 13                  |
| 20               | 26                  | 24                  |
| 50               | 59                  | 57                  |

**Observation**: Erlang C requires c > a (utilization < 100%) for stability. The margin above a determines queueing probability and wait time.

## Erlang B vs Erlang C

| Aspect          | Erlang B (M/M/c/c)                  | Erlang C (M/M/c)                   |
|-----------------|-------------------------------------|------------------------------------|
| **Queue**       | No queue (blocked calls lost)       | Infinite queue (customers wait)    |
| **Overflow**    | Rejected                            | Queued                             |
| **Metric**      | P(blocking)                         | P(wait > 0), average wait time     |
| **Use case**    | Circuit-switched, connection pools  | Call centers, task queues, APIs    |
| **Stability**   | Always stable (fixed capacity)      | Requires a < c (ρ < 1)             |
| **Formula**     | Simpler (no denominator complexity) | More complex (c/(c-a) term)        |

**Which to use?**
- **Erlang B**: If system **rejects** overflow (connection refused, busy signal)
- **Erlang C**: If system **queues** overflow (caller waits, task waits)

Most modern software systems use **Erlang C** (queue, don't reject).

## Practical Examples

### Call Center (Erlang C)
- **Given**: λ = 100 calls/hour, average call = 6 minutes (μ = 10 calls/hour), target P(wait) < 20%
- **Offered load**: a = λ/μ = 100/10 = 10 Erlangs
- **Erlang C**: c = 13 agents for P(wait) < 20%
- **Result**: 13 agents, 77% utilization (10/13), 20% of callers wait

### Database Connection Pool (Erlang C or Erlang B)
- **Given**: λ = 500 queries/sec, average query = 10ms (μ = 100 queries/sec), target P(wait) < 5%
- **Offered load**: a = 500/100 = 5 Erlangs
- **Erlang C**: c = 7 connections for P(wait) < 5%
- **Erlang B**: If overflow is rejected (connection refused), use Erlang B → c = 8 for P(block) < 5%

### Web Server Workers (Erlang C)
- **Given**: λ = 1000 req/s, average processing = 50ms (μ = 20 req/s), target P(wait) < 10%
- **Offered load**: a = 1000/20 = 50 Erlangs
- **Erlang C**: c = 59 workers for P(wait) < 10%
- **Result**: 59 workers, 85% utilization, 10% of requests wait

### Telephone Lines (Erlang B)
- **Given**: λ = 50 calls/hour, average call = 3 minutes (μ = 20 calls/hour), target P(block) < 1%
- **Offered load**: a = 50/20 = 2.5 Erlangs
- **Erlang B**: c = 7 lines for P(block) < 1%
- **Result**: 7 lines, 36% utilization (2.5/7)

## Limitations and Extensions

### Assumptions of Erlang B/C
1. **Poisson arrivals**: Random, memoryless (M/M/c assumption)
2. **Exponential service**: High variance (often unrealistic)
3. **Independent customers**: No bulk arrivals, no retrials
4. **Infinite patience** (Erlang C): Customers never abandon queue

**Real systems violate these assumptions**, but Erlang formulas are still useful approximations.

### Extensions

**Customer abandonment** (Erlang A):
- Customers leave queue after waiting too long
- More realistic than infinite patience (Erlang C)
- More complex formulas; usually requires simulation

**Non-exponential service** (M/G/c):
- General service distribution (not just exponential)
- **Pollaczek-Khinchin approximation** for M/G/1
- M/G/c requires numerical methods or simulation

**Bursty arrivals** (non-Poisson):
- Batch arrivals, correlated arrivals
- Use **peaked Erlang** or simulation

**Retrials**:
- Blocked customers retry after delay
- More complex models (retrial queues)

## Online Calculators

- **supositorio.com/queueing**: Interactive Erlang B/C calculator
- **erlang.com/calculator**: Classic Erlang calculator
- **R package `queueing`**: Programmatic access to Erlang formulas
- **Python `erlang` library**: Calculate Erlang B/C in Python

## Cross-Framework Connections

### M/M/c Queue
The [M/M/c Queue](mmc-queue.md) is the theoretical model behind Erlang C. Erlang C is the closed-form solution for P(wait > 0) in M/M/c.

### Little's Law
[Little's Law](littles-law.md) (L = λW) is model-agnostic. Erlang C provides the formulas for W (average wait time) given c, λ, μ. Then L = λW.

**Combined use**: Erlang C gives W, Little's Law gives L. Together, they fully describe system performance.

### Reinertsen's Flow Economics
Erlang formulas quantify the [utilization trap](queues-in-product-development.md). High utilization (a → c) → long queue times.

[Capacity planning in product development](flow-economics.md): Teams are servers (c), work items are arrivals (λ). Erlang C predicts queue time.

### Systems Thinking (Senge/Meadows)
Capacity (c) is a **stock**. Adding capacity is a **balancing loop** triggered by high queue depth or wait time.

But [delays](feedback-loops.md) in capacity changes mean you must **pre-scale** using Erlang formulas, not react after queues explode.

### Taleb's Barbell Strategy
Erlang formulas show the **fragility** of high utilization. At a/c = 0.95, a 5% increase in λ causes queue explosion.

**Barbell approach**: Overprovision capacity (a/c = 0.6-0.7) for robustness. The "waste" is insurance against tail risk.

### Amazon Leadership Principles
**"Customer Obsession"**: SLAs (e.g., P95 latency < 100ms) require capacity planning. Erlang C enables science-based sizing, not guesswork.

**"Frugality"**: Don't overprovision (wasteful) or underprovision (bad experience). Erlang C finds the optimum.

### OKRs (Doerr/Grove)
**Key Result example**: "P95 call center wait time < 30 seconds"
- Use Erlang C to size agent pool (c) given λ, μ, target wait time
- Monitor actual P95, adjust c as needed

## Key Takeaways

1. **Erlang B**: For systems where overflow is **rejected** (blocking systems)
2. **Erlang C**: For systems where overflow **queues** (most software systems)
3. **Offered load (a = λ/μ)**: Measured in Erlangs; the "amount of work"
4. **Capacity planning**: Given a and target P(block) or P(wait), solve for c
5. **High utilization is fragile**: a/c = 0.95 → long queues; keep a/c ≤ 0.8
6. **Erlang formulas are approximations**: Real systems violate assumptions, but formulas provide useful bounds

## Further Reading

- [M/M/c Queue](mmc-queue.md) — the theoretical model behind Erlang C
- [Kendall Notation](kendall-notation.md) — M/M/c/c (Erlang B) vs M/M/c (Erlang C)
- [Queue Metrics](queue-metrics.md) — using Erlang formulas to predict L, W, ρ
- [Little's Law](littles-law.md) — universal L = λW relationship

## See Also

- [Queues in Product Development](queues-in-product-development.md) — applying Erlang logic to teams
- [Flow Economics](flow-economics.md) — economic lens on capacity planning
- [WIP Limits](wip-limits.md) — constraining a to prevent queue explosion
- [Message Queues](message-queues.md) — distributed systems where Erlang C applies
