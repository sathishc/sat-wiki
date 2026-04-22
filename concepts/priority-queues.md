---
title: Priority Queues
tags: [queueing-theory, data-structures, sla, scheduling, distributed-systems]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queuing-theory-systems.md]
---

# Priority Queues

A queue where items are dequeued by priority, not arrival order (FIFO). Enables SLA differentiation, mixed workload optimization, and handling critical requests ahead of bulk work.

## Definition

**Priority queue**: Items have associated priority value. Dequeue operation returns highest-priority item, regardless of arrival order.

**Contrast with FIFO**:
- FIFO: First-in, first-out (arrival order)
- Priority: Highest priority first (breaks arrival order)

**Use when**:
- Mixed workload (critical + batch)
- SLA tiers (gold/silver/bronze customers)
- Preemption (high-priority work must jump queue)

## Implementations

### Data Structure: Heap

**Binary heap**: O(log n) enqueue, O(log n) dequeue (extract-max).

**Fibonacci heap**: O(1) amortized enqueue, O(log n) dequeue. Better for decrease-key operations.

**Example** (Python):
```python
import heapq

pq = []
heapq.heappush(pq, (priority, item))  # Lower number = higher priority
priority, item = heapq.heappop(pq)
```

### Multiple FIFO Queues

**Pattern**: One queue per priority level. Dequeue from highest-priority non-empty queue.

**Example**:
```
High-priority queue:   [A, B]
Medium-priority queue: [C, D, E]
Low-priority queue:    [F, G, H, I]

Dequeue order: A, B, C, D, E, F, G, H, I
```

**Pros**:
- O(1) enqueue, O(1) dequeue (check queues in priority order)
- Simple implementation

**Cons**:
- Coarse-grained (fixed priority levels)
- Starvation risk (low-priority never executes)

### Message Queue Systems

**RabbitMQ**: Priority queues (0-255). Configure max-priority on queue.

**AWS SQS**: Priority via message attributes + multiple queues (manual routing).

**Kafka**: No native priority; manual routing to partitions (high-priority partition consumed first).

**Redis**: Sorted sets (ZADD with priority score).

## Use Cases

### 1. Mixed Workload

**Problem**: User-facing requests (low latency SLA) + batch jobs (no SLA) share same workers.

**Solution**: Two queues
- High-priority: User requests (P0)
- Low-priority: Batch jobs (P1)
- Workers drain high-priority first

**Result**: User requests never wait behind batch jobs.

### 2. SLA Differentiation

**Problem**: Gold customers (1-minute SLA), silver customers (5-minute SLA), bronze customers (best-effort).

**Solution**: Three priority levels
- P0: Gold customer requests
- P1: Silver customer requests
- P2: Bronze customer requests

**Result**: Higher-paying customers get faster service.

### 3. Preemption

**Problem**: Critical alert (system down) arrives while processing routine tasks.

**Solution**: High-priority queue for alerts, low-priority for routine.

**Result**: Alerts processed immediately (jump queue).

### 4. Remediation

**Problem**: Bug caused 10k failed jobs → retry all 10k. But new user requests arriving (mustn't wait behind retries).

**Solution**:
- New user requests: high priority
- Retries: low priority

**Result**: New work not blocked by backlog remediation.

## Pitfalls

### 1. Starvation

**Problem**: High-priority items keep arriving → low-priority items never execute.

**Example**: P0 queue always has work → P1 queue never drained → P1 items wait forever.

**Mitigation**:

**Aging**: Increase priority over time
```
priority = base_priority - (now - arrival_time) / age_factor
```
After waiting long enough, low-priority becomes high-priority.

**Time slicing**: Round-robin between priority levels
```
Process 10 P0, then 5 P1, then 1 P2, repeat
```

**Quota**: Max high-priority work per time window
```
P0 quota: 1000 requests/hour
After quota: P0 and P1 treated equally
```

### 2. Priority Inflation

**Problem**: "Everything is P0" (everyone wants their work prioritized).

**Solution**:
- Objective priority rules (SLA, customer tier, business value)
- Limited P0 quota
- Priority review (periodic audit: is this still P0?)

### 3. Complexity

**Problem**: Priority determination logic is complex (what's P0 vs P1?).

**Solution**:
- Start with two levels (critical, normal)
- Add levels only if proven necessary
- Document priority criteria

### 4. Unfairness

**Problem**: Low-priority users feel discriminated against.

**Solution**:
- Transparent priority rules (published SLA tiers)
- Aging (eventually everyone gets served)
- Monitoring (measure starvation; adjust if needed)

## Queueing Theory

**Model**: Priority queues are complex to analyze (no closed-form solution like M/M/1).

**Non-preemptive priority**: High-priority item must wait for current item to finish (can't interrupt).

**Preemptive priority**: High-priority item can interrupt current item (restart or resume).

**Key insight**: High-priority class sees **lower average wait time** than equivalent FIFO queue. Low-priority class sees **higher** wait time. Total system wait time is **unchanged** (just redistributed).

**Mean wait time by priority** (M/M/1 with non-preemptive priority):
- High-priority: W_high < W_FIFO
- Low-priority: W_low > W_FIFO
- Overall: W_avg = W_FIFO (same total system latency, just redistributed)

**Implication**: Priority queues don't reduce overall latency; they redistribute it. High-priority gains at expense of low-priority.

## Cross-Framework Connections

**[Kendall Notation](kendall-notation.md)**:
- Priority queue changes D (discipline) from FIFO to Priority
- M/M/1/FIFO → M/M/1/Priority
- More complex analysis (no simple closed-form solution)

**[Little's Law](littles-law.md)**:
- Still holds for priority queues (L = λW)
- But W differs by priority class (W_high < W_low)

**[Message Queues](message-queues.md)**:
- Some message queue systems support priority (RabbitMQ, Redis)
- Others require manual routing (Kafka partitions, multiple SQS queues)

**[Queue-Based Load Leveling](queue-based-load-leveling.md)**:
- Priority queues preserve load leveling (absorb spikes per priority class)
- High-priority spikes don't block low-priority work (just delay it)

**[Reinertsen](../people/donald-reinertsen.md) / [Cost of Delay](cost-of-delay.md)**:
- Priority = Cost of Delay weighting
- WSJF (Weighted Shortest Job First) = priority by CoD / duration
- High CoD → high priority → processed first

**[Systems Thinking](systems-thinking.md)**:
- Priority queue = policy (rules determining behavior)
- Starvation = unintended consequence (Limits to Growth archetype)
- Aging = balancing loop (prevents starvation)

**[Westrum](../people/ron-westrum.md) / Culture**:
- Generative culture: Priority based on objective criteria (SLA, CoD)
- Bureaucratic culture: Priority based on hierarchy (manager's request → P0)
- Pathological culture: Priority based on politics (who shouts loudest)

**[Porter](../people/michael-porter.md) / [Generic Strategies](generic-strategies.md)**:
- Differentiation strategy → priority queues (gold/silver/bronze service tiers)
- Cost leadership → FIFO (everyone treated equally, no overhead)

## Anti-Patterns

**Everything is high-priority**:
- "All our customers are VIP"
- Result: Priority queue degenerates to FIFO (no differentiation)
- Solution: Limit high-priority quota, enforce objective criteria

**Too many priority levels**:
- 10+ priority levels
- Result: Hard to reason about, hard to tune
- Solution: 2-3 levels (critical, normal, low) is usually enough

**Priority without starvation protection**:
- Low-priority items never execute
- Result: Work abandoned, waste, frustration
- Solution: Aging, time slicing, or quota

**Priority as substitute for capacity planning**:
- "We're overloaded; let's add priorities"
- Result: Low-priority work still queued; problem not solved
- Solution: Priority helps redistribute latency, but doesn't add capacity. If overloaded, add workers.

## When to Use vs. FIFO

**Use priority when**:
- Mixed workload (user-facing + batch)
- SLA tiers (gold/silver/bronze)
- Preemption required (critical alerts)
- Cost of Delay varies widely between items

**Use FIFO when**:
- Homogeneous workload (all items equal value)
- Fairness required (first-come, first-served)
- Simplicity valued (no priority logic)

**Rule of thumb**: Default to FIFO. Add priority only if proven necessary (SLA violations, business value differentiation).

## References

- [Kendall Notation](kendall-notation.md) — priority changes queue discipline (D)
- [Little's Law](littles-law.md) — applies to priority queues (per-class)
- [Message Queues](message-queues.md) — implementations that support priority
- [Cost of Delay](cost-of-delay.md) — economic basis for priority
- [Queue-Based Load Leveling](queue-based-load-leveling.md) — priority + load leveling
- [Systems Thinking](systems-thinking.md) — starvation as unintended consequence
- [Generic Strategies](generic-strategies.md) — differentiation via priority
