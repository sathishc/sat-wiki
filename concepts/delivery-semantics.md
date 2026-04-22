---
title: Delivery Semantics
tags: [distributed-systems, message-queues, reliability, consistency]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queuing-theory-systems.md]
---

# Delivery Semantics

Guarantees about how many times a message is delivered in a distributed queue system. The fundamental tradeoff between performance, simplicity, and correctness.

## Three Levels

### At-Most-Once

**Guarantee**: Message delivered **0 or 1 times** (never duplicates).

**Mechanism**:
- Fire-and-forget
- No retries on failure
- Ack before processing (or no ack at all)

**Pros**:
- Fast (no retry overhead)
- Simple (no deduplication logic)

**Cons**:
- **Message loss** possible (network failure, crash, etc.)

**Use when**:
- Loss is acceptable (metrics, logs, non-critical events)
- Performance > reliability
- Example: StatsD metrics, UDP protocols, Kafka with `acks=0`

### At-Least-Once

**Guarantee**: Message delivered **≥1 times** (possible duplicates).

**Mechanism**:
- Send message
- Wait for ack from consumer
- If no ack (timeout, crash, network failure), **retry**
- Consumer may receive duplicates (original + retries)

**Pros**:
- No message loss (reliable)
- Simpler than exactly-once

**Cons**:
- **Duplicates** possible
- Consumer must be **idempotent** or deduplicate

**Use when**:
- Loss is unacceptable, but duplicates can be handled
- Most common default (AWS SQS, RabbitMQ, Kafka with `acks=all`)

**Example**: Payment processing. Better to process twice (and deduplicate) than lose a payment.

### Exactly-Once

**Guarantee**: Message delivered **exactly 1 time** (no loss, no duplicates).

**Mechanism** (two approaches):

**1. Distributed Transaction (2PC, Saga)**:
- Producer writes message + consumer updates state in single atomic transaction
- Requires distributed transaction coordinator
- Expensive (latency, complexity, coordination overhead)

**2. At-Least-Once + Idempotency + Deduplication**:
- Deliver at-least-once (may have duplicates)
- Consumer is idempotent (applying twice = applying once)
- OR consumer deduplicates (checks unique ID, skips if already processed)
- **This is how most "exactly-once" systems work** (Kafka EOS, Google Pub/Sub, Flink)

**Pros**:
- No loss, no duplicate processing (correct)

**Cons**:
- High latency (distributed transaction or deduplication check)
- High complexity (idempotency constraints, unique ID generation, state management)
- Performance cost

**Use when**:
- Neither loss nor duplicates acceptable (financial transactions, inventory updates)
- Worth the complexity + latency cost

## Idempotency: The Key to Exactly-Once

**Definition**: Operation that can be applied multiple times with same result.

**Examples**:
- **Idempotent**: `SET x = 5` (applying twice → x=5)
- **Not idempotent**: `x += 5` (applying twice → x=10, not 5)

**How to design for idempotency**:

**1. Natural keys**:
- Use business key (order ID, user ID) as primary key
- `INSERT ... ON CONFLICT UPDATE` (upsert)
- Duplicate insert → update existing row (no duplicate data)

**2. Unique message IDs**:
- Producer assigns unique ID (UUID, timestamp+sequence)
- Consumer tracks processed IDs (in DB, cache, or bloom filter)
- On message arrival: check ID → if seen, skip; else process + record ID

**3. Check-before-write**:
- Before applying operation, check current state
- Example: "charge card $100" → check if already charged → if yes, skip; else charge

**4. Commutative operations**:
- Order doesn't matter: `x = max(x, 5)` is idempotent-ish (applying twice doesn't change result)
- CRDTs (Conflict-free Replicated Data Types) are designed for this

**Tradeoff**: Idempotency requires state (to remember what's been processed). State = complexity + latency.

## Kafka Exactly-Once Semantics (EOS)

Kafka provides exactly-once via:
1. **Idempotent producer**: Producer assigns sequence numbers; broker deduplicates
2. **Transactional writes**: Write to multiple partitions + commit atomically
3. **Idempotent consumer**: Consumer tracks offsets; replays from last commit

**Mechanism**:
- Producer writes message + offset atomically (transaction)
- Broker deduplicates (sequence number)
- Consumer reads transactionally (only sees committed messages)

**Tradeoff**: Higher latency (~2-3x), more complexity (transaction coordinator, state management).

**When to use**: Stream processing where duplicates break correctness (aggregations, joins).

## Real-World Defaults

| System | Default | Upgrade Path |
|---|---|---|
| AWS SQS | At-least-once | Make consumer idempotent |
| RabbitMQ | At-least-once | Make consumer idempotent |
| Kafka | At-least-once (`acks=all`) | Enable EOS (idempotent producer + transactional consumer) |
| Google Pub/Sub | At-least-once | Make consumer idempotent |
| Redis Streams | At-least-once | Make consumer idempotent |

**Pattern**: Start with at-least-once. Make consumer idempotent. Upgrade to exactly-once only if idempotency is impossible or too complex.

## Deduplication Strategies

**1. Database unique constraint**:
```sql
CREATE TABLE events (
  event_id UUID PRIMARY KEY,
  payload JSONB
);
INSERT INTO events VALUES (?, ?) ON CONFLICT DO NOTHING;
```
- Pros: Simple, atomic
- Cons: DB round-trip on every message

**2. In-memory cache (Redis)**:
```python
if redis.setnx(message_id, "1", ex=3600):  # Set if not exists
    process(message)
else:
    skip  # Already processed
```
- Pros: Fast
- Cons: Cache miss = reprocess (need TTL tuning)

**3. Bloom filter**:
- Probabilistic: "definitely not seen" or "probably seen"
- Pros: Memory-efficient
- Cons: False positives (may skip valid message)

**4. Application-level state**:
- Track "last processed ID" per partition/stream
- Only process IDs > last processed
- Pros: Simple for ordered streams
- Cons: Requires ordering

## Cross-Framework Connections

**[Message Queues](message-queues.md)**:
- All message queue systems must choose a delivery semantic
- At-least-once is the pragmatic default
- Exactly-once is the expensive upgrade

**[Systems Thinking](systems-thinking.md)**:
- At-least-once + idempotency = design pattern for resilience
- Exactly-once via transaction = tight coupling (synchronous coordination)
- At-least-once = loose coupling (async, retries)

**[Antifragility](antifragility.md) / [Taleb](../people/nassim-taleb.md)**:
- At-most-once = fragile (message loss)
- Exactly-once via 2PC = fragile (coordinator failure → system blocked)
- At-least-once + idempotency = antifragile (graceful degradation, no single point of failure)

**[Reinertsen](../people/donald-reinertsen.md) / [Cost of Delay](cost-of-delay.md)**:
- Exactly-once has latency cost (2PC, deduplication checks)
- At-least-once has rework cost (duplicate processing)
- Economic decision: which cost is lower?

**[Christensen](../people/clayton-christensen.md) / [100% Integrity](how-will-you-measure-your-life.md)**:
- Exactly-once = 100% correctness (no loss, no duplicates)
- At-least-once = 98% correctness (occasional duplicate)
- But 98% can collapse (if idempotency not enforced, duplicates corrupt data)
- **Lesson**: Choose exactly-once (idempotency) for domains where correctness matters (money, inventory, identity)

**[Kahneman](../people/daniel-kahneman.md) / [Planning Fallacy](planning-fallacy.md)**:
- Developers underestimate complexity of exactly-once
- "We'll just deduplicate" → requires state, unique IDs, edge case handling
- Planning fallacy → choose at-least-once + idempotency, discover idempotency is hard, ship with duplicates

**[Circuit Breaker Pattern](circuit-breaker-pattern.md)**:
- Circuit breaker + retry → at-least-once semantics
- Must combine with idempotency or deduplication

## Decision Tree

```
Can you tolerate message loss?
  ├─ Yes → At-Most-Once (UDP, metrics, logs)
  └─ No → Can you tolerate duplicates?
      ├─ Yes → At-Least-Once + Idempotent Consumer (most systems)
      └─ No → Is idempotency possible?
          ├─ Yes → At-Least-Once + Idempotent Consumer (still!)
          └─ No → Exactly-Once (Kafka EOS, 2PC, high complexity)
```

**Rule of thumb**: 95% of systems should use at-least-once + idempotent consumer. It's the sweet spot of reliability + simplicity.

## Anti-Patterns

**"We need exactly-once"** (without understanding cost):
- Most systems don't need it; idempotency is enough
- Exactly-once adds latency + complexity
- Solution: Default to at-least-once + idempotency; upgrade only if proven necessary

**Non-idempotent consumer with at-least-once**:
- Duplicates → data corruption (double-charge, double-inventory-decrement)
- Solution: Design for idempotency from day one

**Deduplication without TTL**:
- Deduplication cache grows unbounded
- Solution: TTL on deduplication state (how long to remember processed IDs?)

**Unique ID without entropy**:
- Sequential IDs → collisions on retry
- Solution: UUID, timestamp+node ID+sequence, or similar

## References

- [Message Queues](message-queues.md) — implementations and their delivery semantics
- [Backpressure](backpressure.md) — flow control complements delivery semantics
- [Dead Letter Queues](dead-letter-queues.md) — handling messages that fail delivery
- [Antifragility](antifragility.md) — at-least-once + idempotency as antifragile pattern
- [Systems Thinking](systems-thinking.md) — tight vs. loose coupling tradeoffs
- [Cost of Delay](cost-of-delay.md) — economic frame for semantic choice
