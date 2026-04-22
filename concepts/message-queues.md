---
title: Message Queues
tags: [distributed-systems, architecture, async, messaging, middleware]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queuing-theory-systems.md]
---

# Message Queues

Asynchronous communication middleware for distributed systems. Senders publish messages to a queue; receivers consume messages later. The foundational pattern for decoupled, scalable, resilient system architecture.

## Core Guarantees

**Decoupling**: Sender and receiver don't need to be online simultaneously. Fire-and-forget from sender perspective.

**Durability**: Messages persist (usually to disk) until consumed. Survives receiver crashes, network partitions, restarts.

**Ordering**: Varies by implementation
- Strong ordering (RabbitMQ, Kafka per-partition, SQS FIFO)
- Weak ordering (SQS standard, unordered pub-sub)
- Per-key ordering (Kafka partitions)

**Delivery semantics**: See [Delivery Semantics](delivery-semantics.md)
- At-most-once (fire-and-forget, possible loss)
- At-least-once (retries, possible duplicates)
- Exactly-once (expensive, rare)

## Common Implementations

### RabbitMQ
**Model**: AMQP-based, exchanges + bindings + queues

**Strengths**:
- Rich routing (topic, fanout, headers exchanges)
- Strong ordering per queue
- Reliable (persistent messages, publisher confirms)
- Management UI, monitoring

**Weaknesses**:
- Medium throughput (~10k-50k msg/sec per node)
- Scales vertically more than horizontally

**Use when**: Need complex routing, strong ordering, transactional guarantees.

### Apache Kafka
**Model**: Distributed commit log, partitioned topics, consumer groups

**Strengths**:
- High throughput (100k-1M+ msg/sec)
- Replayable (consumers can rewind to any offset)
- Horizontal scale (add brokers, add partitions)
- Per-partition ordering (strong within partition, weak across)
- Long retention (days/weeks/forever)

**Weaknesses**:
- Operational complexity (Zookeeper/KRaft, partition management)
- Not a queue (it's a log; all consumers see all messages unless consumer groups)
- Per-message overhead higher than simple queues

**Use when**: High throughput, event sourcing, stream processing, need replay.

### AWS SQS
**Model**: Managed queue service, standard (unordered, at-least-once) or FIFO

**Strengths**:
- Fully managed (no ops)
- Scales automatically (no capacity planning)
- Integrates with AWS ecosystem (Lambda, SNS, CloudWatch)

**Weaknesses**:
- Weak ordering (standard queues are unordered)
- FIFO queues limited throughput (300 tps, or 3000 with batching)
- Message size limit (256 KB)
- Higher per-message cost than self-hosted

**Use when**: AWS shop, want managed service, don't need strong ordering or high throughput.

### Redis Streams
**Model**: In-memory log, consumer groups, pub-sub

**Strengths**:
- Fast (in-memory, microsecond latency)
- Consumer groups (Kafka-like semantics)
- Simple ops (Redis is easy to run)

**Weaknesses**:
- Less durable (in-memory; persistence is async)
- Limited retention (memory-bound)
- Single-threaded per shard (scales via sharding)

**Use when**: Need low latency, can tolerate rare message loss, moderate throughput.

### Google Cloud Pub/Sub
**Model**: Managed pub-sub, push and pull delivery

**Strengths**:
- Fully managed, global
- Auto-scales
- Push (webhooks) and pull (polling) models
- At-least-once delivery

**Weaknesses**:
- Weak ordering (no FIFO guarantee)
- Can't replay (once ack'd, message is gone)
- Cost scales with throughput

**Use when**: GCP shop, want managed service, fan-out to many subscribers.

### Azure Service Bus
**Model**: Enterprise messaging, queues and topics, sessions for ordering

**Strengths**:
- FIFO sessions (ordered processing per session key)
- Advanced features (scheduled messages, dead-lettering, duplicate detection)
- Integrates with Azure ecosystem

**Weaknesses**:
- Azure-specific
- Moderate throughput (similar to RabbitMQ)

**Use when**: Azure shop, need enterprise messaging patterns.

## When to Use Message Queues

**Decouple producers and consumers**:
- Producer doesn't wait for consumer (async)
- Producer doesn't know who consumers are (loose coupling)
- Example: Web app publishes "order placed" event; multiple services (inventory, shipping, email) consume independently

**Smooth spiky traffic** (see [Queue-Based Load Leveling](queue-based-load-leveling.md)):
- Queue absorbs traffic spikes
- Backend consumes at sustainable rate
- Example: Black Friday traffic → payment processing queue

**Asynchronous workflows**:
- Long-running tasks (video transcode, report generation)
- Background jobs (send email, resize image)
- Scheduled tasks (nightly batch job)

**Fan-out / pub-sub**:
- One event, many consumers
- Each consumer gets copy of message
- Example: User signup → welcome email + analytics + CRM update

**Retry and [Dead Letter Queue](dead-letter-queues.md) patterns**:
- Failed messages automatically retry
- Poison messages moved to DLQ after N retries
- Observability into failure modes

## Architecture Patterns

**Work Queue**:
- One producer → one queue → many workers
- Each message consumed exactly once (single consumer per message)
- Workers are fungible (any worker can process any message)
- Example: Image processing job queue

**Pub-Sub (Publish-Subscribe)**:
- One producer → topic → many subscribers
- Each subscriber gets own copy of message
- Subscribers are independent (different consumer groups in Kafka, different queues in RabbitMQ)
- Example: Event notification system

**Request-Reply** (anti-pattern):
- Don't use message queue for synchronous RPC
- High latency (two queue hops + polling)
- Use HTTP/gRPC for synchronous, queue for async

**Saga Pattern**:
- Distributed transaction across services
- Each step publishes event to queue
- Compensating actions on failure
- Example: E-commerce order (inventory → payment → shipping → email)

## Operational Considerations

**Monitoring**:
- Queue depth (L in [Little's Law](littles-law.md))
- Age of oldest message
- Enqueue rate (λ)
- Dequeue rate (μ)
- Dead letter queue depth (sign of systemic failure)

**Scaling**:
- Scale consumers (add workers) when queue depth grows
- Scale producers if enqueue rate is bottleneck (rare)
- See [Queue Depth Monitoring](#monitoring) for auto-scaling triggers

**Backpressure**:
- Bounded queues + flow control (see [Backpressure](backpressure.md))
- Circuit breaker when queue depth exceeds threshold
- Reject new messages (fail fast) vs. block producer

**Idempotency**:
- At-least-once delivery → duplicates → need idempotent consumers
- Design for idempotency: unique IDs, check-before-write, natural keys
- See [Delivery Semantics](delivery-semantics.md)

## Cross-Framework Connections

**[Kendall Notation](kendall-notation.md)**:
- Message queue with workers = M/M/c (random arrivals, multiple consumers)
- Kafka partition = M/M/1 (single consumer per partition)
- Bounded queue = M/M/c/K (K = max queue depth)

**[Little's Law](littles-law.md)**:
- L (queue depth) = λW (arrival rate × latency)
- Monitor L to predict consumer lag
- If L grows, either increase μ (add workers) or decrease λ (backpressure)

**[Erlang Formulas](erlang-formulas.md)**:
- Use Erlang-C to size worker pool: given λ and μ, solve for c (workers) to hit latency SLA

**[Reinertsen](../people/donald-reinertsen.md) / [Flow Economics](flow-economics.md)**:
- Queue = visible WIP (work in progress)
- [Cost of Delay](cost-of-delay.md) = economic value of reducing queue depth
- Message queue latency = opportunity cost

**[Systems Thinking](systems-thinking.md)**:
- Queue = stock, enqueue = inflow, dequeue = outflow
- Unbounded queue = missing balancing loop ([Backpressure](backpressure.md))
- DLQ = safety valve (limits to growth archetype)

**[Queueing Networks](queueing-networks.md)**:
- Microservices architecture = queueing network
- Each service has input queue (message queue or load balancer)
- Bottleneck analysis → which service to scale

**[Westrum](../people/ron-westrum.md) / Culture**:
- Generative culture → fast queue drain (low latency)
- Pathological culture → messages ignored, queue grows unbounded
- DLQ monitoring = cultural signal (ignored errors vs. rapid response)

## Anti-Patterns

**Queue as database**:
- Queues are not databases; limited query, weak consistency
- Store in DB, send pointer to queue

**Unbounded queues without backpressure**:
- Queue grows without limit → OOM
- Solution: bounded queue + backpressure

**Too many queues**:
- Operational complexity (monitoring each queue)
- Solution: consolidate, use topic routing

**No DLQ / retry logic**:
- Poison messages block queue forever
- Solution: DLQ, max retries, exponential backoff

## Comparison Table

| Feature | RabbitMQ | Kafka | SQS | Redis | Pub/Sub |
|---|---|---|---|---|---|
| **Throughput** | Medium | Very High | Medium | High | High |
| **Ordering** | Strong | Per-partition | Weak (FIFO opt) | Strong | Weak |
| **Durability** | High | High | High | Medium | High |
| **Replay** | No | Yes | No | Limited | No |
| **Ops complexity** | Medium | High | Low (managed) | Low | Low (managed) |
| **Cost** | Self-hosted | Self-hosted | Pay-per-msg | Self-hosted | Pay-per-msg |

## References

- [Kendall Notation](kendall-notation.md) — M/M/c models for message queues
- [Little's Law](littles-law.md) — queue depth = arrival rate × latency
- [Erlang Formulas](erlang-formulas.md) — capacity planning (worker pool sizing)
- [Delivery Semantics](delivery-semantics.md) — at-least-once vs exactly-once
- [Backpressure](backpressure.md) — flow control mechanisms
- [Queue-Based Load Leveling](queue-based-load-leveling.md) — smoothing traffic spikes
- [Dead Letter Queues](dead-letter-queues.md) — handling poison messages
- [Priority Queues](priority-queues.md) — SLA differentiation
