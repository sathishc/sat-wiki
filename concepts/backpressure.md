---
title: Backpressure
tags: [distributed-systems, flow-control, resilience, systems]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queuing-theory-systems.md]
---

# Backpressure

Signals from consumer to producer to slow down when the consumer is overwhelmed. The essential feedback loop that prevents unbounded queue growth, cascading failures, and system collapse.

## The Problem

**Fast producer + slow consumer → unbounded queue growth → OOM or message loss.**

Without backpressure:
- Queue grows without limit
- Memory exhausted → crash or swap thrashing
- Or messages dropped (if queue is bounded but drops on overflow)
- Or downstream overwhelmed (if queue is unbounded in-memory but propagates all)

**Analogy**: Water flowing into a bucket faster than it drains. Without overflow mechanism (backpressure), bucket overflows.

## Mechanisms

### 1. Bounded Queues + Blocking

**How**: Queue has max capacity (K in [Kendall notation](kendall-notation.md)). When full, producer blocks until space available.

**Example**: Java `BlockingQueue.put()` blocks if queue full.

**Pros**:
- Simple to implement
- Natural backpressure (producer can't outrun consumer)

**Cons**:
- Producer blocked → can't do other work
- Deadlock risk if not carefully designed (e.g., producer and consumer both block waiting on each other)

**When to use**: Single-process systems, tight coupling acceptable.

### 2. Rate Limiting

**How**: Limit messages/sec from producer (fixed rate or adaptive).

**Example**: Token bucket, leaky bucket, sliding window rate limiter.

**Pros**:
- Simple, coarse-grained control
- Prevents runaway producer

**Cons**:
- Static limit doesn't adapt to consumer capacity
- Wastes producer capacity if consumer could handle more

**When to use**: Known max safe rate, or as secondary defense layer.

### 3. Flow Control Protocols

**How**: Receiver advertises capacity; sender respects it.

**Examples**:

**TCP flow control**:
- Receiver advertises window size (buffer space available)
- Sender sends ≤ window size
- Automatic, built into protocol

**RabbitMQ credit-based flow**:
- Consumer prefetch limit (max un-acked messages)
- Producer blocks when limit reached
- Consumer acks → credits replenished

**gRPC / HTTP/2 flow control**:
- Per-stream window size
- Receiver sends WINDOW_UPDATE frames
- Sender respects stream and connection windows

**Pros**:
- Dynamic adaptation to receiver capacity
- Efficient (no wasted bandwidth)

**Cons**:
- Protocol complexity
- Requires bidirectional communication

**When to use**: Network protocols, high-throughput systems.

### 4. Consumer Lag Monitoring + Circuit Breaker

**How**: Monitor queue depth or consumer lag. If exceeds threshold, open circuit breaker (reject new messages, fail fast).

**Example**:
- Kafka consumer lag > 1M messages → circuit open
- Reject new publishes (503 Service Unavailable)
- Allows consumer to catch up

**Pros**:
- Prevents cascading failure
- Fast failure (don't queue doomed requests)

**Cons**:
- Messages rejected (shifted to client retry logic)
- Requires monitoring + alerting infrastructure

**When to use**: Distributed systems, microservices, when prevention is better than cure.

### 5. Reactive Streams / Backpressure Propagation

**How**: Demand-driven. Consumer requests N items; producer sends ≤ N; consumer requests more when ready.

**Examples**:
- Java Flow API (JDK 9+)
- Project Reactor (Spring WebFlux)
- RxJava
- Akka Streams

**Mechanism**:
```
Consumer → request(N) → Producer
Producer → send(M≤N) → Consumer
Consumer → request(N') → Producer
...
```

**Pros**:
- Precise control (consumer pulls what it can handle)
- Composes across multiple stages (backpressure propagates end-to-end)

**Cons**:
- Implementation complexity
- Paradigm shift (pull vs. push)

**When to use**: Streaming data pipelines, reactive systems, fine-grained flow control needed.

## Propagation: End-to-End Backpressure

**Key insight**: Backpressure must propagate through entire system. A queue without backpressure is just a buffer before the failure point.

**Example**: 3-tier system (API → Queue → Worker → Database)

**Without propagation**:
- Database slow → Worker slow → Queue grows → Queue full → Worker blocks → BUT API keeps accepting requests → API queue grows → OOM

**With propagation**:
- Database slow → Worker slow → Queue depth grows → Circuit breaker opens → API rejects requests (503) → Client retries with backoff → System stabilizes

**Pattern**: Monitor each queue depth; if any exceeds threshold, apply backpressure upstream (reject, block, or rate-limit).

## Tradeoffs

| Mechanism | Latency | Throughput | Complexity | Message Loss Risk |
|---|---|---|---|---|
| Blocking | High (blocked) | Low | Low | None |
| Rate Limiting | Low | Limited | Low | None (but rejects) |
| Flow Control | Low | High | High | None |
| Circuit Breaker | Low (fast fail) | Adaptive | Medium | Rejections (not loss) |
| Reactive Streams | Low | High | Very High | None |

**Rule of thumb**: Start simple (rate limiting + circuit breaker). Add flow control if throughput matters. Reactive streams only if building streaming infrastructure.

## Anti-Patterns

**Unbounded queues**:
- "We'll just make the queue bigger"
- Postpones problem; doesn't solve it
- Eventually hits limit (memory, disk, network)

**Infinite retries**:
- Producer retries forever on failure
- Amplifies load during outage (retry storm)
- Solution: exponential backoff + jitter + max retries

**Dropping silently**:
- Queue full → drop message silently
- No feedback to producer → keeps sending
- Solution: reject with error (fail fast)

**Backpressure on wrong metric**:
- Monitor CPU, not queue depth
- CPU lags behind (only spikes after queue already overflowing)
- Solution: monitor queue depth directly

## Cross-Framework Connections

**[Systems Thinking](systems-thinking.md) / [Feedback Loops](feedback-loops.md)**:
- Backpressure = **balancing loop** (negative feedback)
- Without it, system has only **reinforcing loop** (queue grows unbounded)
- Meadows' [Leverage Points](leverage-points.md): backpressure is Level 5 (information flow) and Level 8 (balancing loop strength)

**[Little's Law](littles-law.md)**:
- L = λW (queue depth = arrival rate × latency)
- Backpressure reduces λ (arrival rate) to cap L (queue depth)
- Tradeoff: capping L increases W for rejected requests (they must retry)

**[Kendall Notation](kendall-notation.md)**:
- Backpressure changes model from M/M/c (infinite queue) to M/M/c/K (finite queue capacity K)
- Bounded queue → some requests rejected (blocking probability)

**[Reinertsen](../people/donald-reinertsen.md) / [WIP Limits](wip-limits.md)**:
- Backpressure = operational mechanism to enforce WIP limit
- Bounded queue = hard WIP limit (K in Kendall notation)
- [Cost of Delay](cost-of-delay.md): rejecting requests has cost, but so does queueing them (choose lower cost)

**[Message Queues](message-queues.md)**:
- All production message queue systems need backpressure
- RabbitMQ: prefetch limit
- Kafka: consumer lag monitoring + circuit breaker
- SQS: bounded queue + DLQ for poison messages

**[Antifragility](antifragility.md) / [Taleb](../people/nassim-taleb.md)**:
- Backpressure = antifragile design (graceful degradation vs. collapse)
- Unbounded queue = fragile (catastrophic failure when limit hit)
- Circuit breaker = stress testing (small failures prevent big ones)

**[Circuit Breaker Pattern](circuit-breaker-pattern.md)**:
- Circuit breaker is one form of backpressure
- Monitors failure rate or queue depth → opens on threshold
- Backpressure propagates as 503s (Service Unavailable)

## Practical Implementation

**In code** (Python example):
```python
from queue import Queue, Full

# Bounded queue
q = Queue(maxsize=100)

def producer():
    try:
        q.put(item, block=True, timeout=1.0)  # Block with timeout
    except Full:
        # Backpressure signal: queue full
        return 503  # Service Unavailable

def consumer():
    item = q.get()
    process(item)
    q.task_done()
```

**In infrastructure**:
- Monitor: Queue depth, consumer lag
- Alert: Depth > threshold
- Auto-scale: Add consumers
- Circuit breaker: If depth > critical, reject new requests

**In protocols**:
- TCP: window size
- RabbitMQ: prefetch limit
- gRPC: flow control windows
- Reactive: `request(N)` demand signaling

## References

- [Little's Law](littles-law.md) — queue depth = arrival rate × latency
- [Kendall Notation](kendall-notation.md) — M/M/c/K (bounded queue)
- [Systems Thinking](systems-thinking.md) — backpressure as balancing loop
- [Feedback Loops](feedback-loops.md) — balancing loops prevent unbounded growth
- [Message Queues](message-queues.md) — queue implementations and backpressure
- [WIP Limits](wip-limits.md) — backpressure in product development
- [Circuit Breaker Pattern](circuit-breaker-pattern.md) — backpressure via fail-fast
- [Antifragility](antifragility.md) — backpressure as antifragile design
