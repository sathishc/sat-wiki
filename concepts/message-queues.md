---
title: Message Queues
tags: [distributed-systems, messaging, architecture, async, infrastructure]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queueing-theory.md]
layout: default
parent: Concepts
---

# Message Queues

**Message queues** are durable, distributed implementations of the theoretical queues described in queueing theory ([M/M/1](mm1-queue.md), [M/M/c](mmc-queue.md)). They decouple producers from consumers, enable asynchronous processing, and provide the infrastructure for scalable, resilient systems.

## Core Concept

**Producers** write messages to a queue. **Consumers** read and process messages from the queue. The queue acts as a buffer, decoupling the two: producers don't block waiting for consumers, and consumers process at their own rate.

**Benefits**:
1. **Asynchronous processing**: Producer returns immediately; consumer processes later
2. **Load leveling**: Queue absorbs traffic spikes; consumer processes at sustainable rate
3. **Decoupling**: Producer and consumer evolve independently
4. **Reliability**: Durable queues survive crashes; messages are not lost
5. **Scalability**: Add more consumers to increase throughput

## Popular Technologies

### RabbitMQ
- **Protocol**: AMQP (Advanced Message Queuing Protocol)
- **Features**: Flexible routing (exchanges, bindings), transactional, acknowledgments, priority queues
- **Use case**: Complex routing, reliable delivery, mature ecosystem
- **Durability**: Persists messages to disk
- **Model**: [M/M/c](mmc-queue.md) with c = number of consumers

### Apache Kafka
- **Architecture**: Distributed commit log (not a traditional queue)
- **Features**: High throughput, replay capability, partitioning, consumer groups
- **Use case**: Event streaming, real-time data pipelines, audit logs
- **Durability**: Append-only log, configurable retention
- **Model**: Partitions enable parallelism; each partition is a log, not a queue

### Amazon SQS (Simple Queue Service)
- **Type**: Managed queue service (fully managed by AWS)
- **Features**: At-least-once delivery, visibility timeout, dead-letter queues, FIFO queues
- **Use case**: Decoupling microservices, reliable task queues, serverless architectures
- **Durability**: Distributed, replicated storage
- **Model**: [M/M/c](mmc-queue.md) with auto-scaling consumers (Lambda integration)

### Redis Streams
- **Architecture**: In-memory data structure (append-only log)
- **Features**: Fast, consumer groups, message persistence (AOF/RDB)
- **Use case**: Real-time analytics, lightweight messaging, caching + messaging hybrid
- **Durability**: Configurable (in-memory with optional persistence)
- **Model**: Lightweight, lower latency than Kafka/RabbitMQ

### Google Cloud Pub/Sub
- **Type**: Managed pub-sub service
- **Features**: Global, auto-scaling, push/pull delivery, dead-letter topics
- **Use case**: Event-driven architectures, streaming analytics, multi-region systems
- **Durability**: Replicated across zones/regions
- **Model**: Pub-sub (one message → multiple subscribers)

### Azure Service Bus
- **Type**: Enterprise messaging service
- **Features**: Topics, queues, sessions, transactions, dead-letter queues
- **Use case**: Enterprise integration, reliable messaging, .NET ecosystems
- **Durability**: Multi-zone replication
- **Model**: Flexible (queues, topics, or hybrid)

## Design Patterns

### Queue-Based Load Leveling

**Pattern**: Insert a queue between frontend and backend to absorb traffic spikes.

**Mechanism**:
- Frontend writes to queue immediately (fast ack)
- Backend processes at sustainable rate
- Queue depth grows during spikes, drains during troughs

**Benefits**:
- Prevents backend overload
- Frontend remains responsive
- Backend can scale independently

**Trade-offs**:
- Latency increases (async processing)
- Queue becomes a durability requirement
- Monitoring queue depth is critical

**Example**: Web requests → SQS → Lambda workers processing at steady rate

**Queueing theory**: This is [M/M/c](mmc-queue.md) with c = backend capacity. Queue acts as buffer when λ (arrival rate) temporarily exceeds μ (service rate).

### Work Queues / Task Queues

**Pattern**: Distribute work across multiple consumers.

**Technologies**:
- **Celery** (Python): Distributed task queue, routing, retries, periodic tasks
- **Sidekiq** (Ruby): Redis-backed, multithreaded workers, job prioritization
- **Bull** (Node.js): Redis-based, job scheduling, delayed jobs, priorities

**Mechanism**:
- **Competing consumers**: Multiple workers pull from same queue ([M/M/c](mmc-queue.md) model)
- Each job processed exactly once (via acknowledgments)
- Failed jobs can be retried or moved to [Dead Letter Queue](dead-letter-queues.md)

**Use cases**:
- Background job processing (email sending, report generation)
- Data processing pipelines
- Long-running tasks decoupled from web requests

**Queueing theory**: c = number of workers. [Erlang C](erlang-formulas.md) predicts queue time given λ, μ, c.

### Priority Queues

**Pattern**: High-priority messages bypass low-priority messages.

**Implementations**:
- Multiple queues (one per priority level): consumers check high-priority queue first
- Heap-based (single queue with priority ordering): slower insert/extract
- Weighted round-robin: alternate between priority levels to prevent starvation

**Use cases**:
- SLA-based routing: premium customers get priority
- Critical alerts vs. routine tasks
- Real-time vs. batch processing

**Risk**: **Starvation** — low-priority jobs never execute if high-priority jobs keep arriving
- **Mitigation**: Priority aging (increase priority as job ages), or guaranteed minimum processing time for low-priority

### Fan-Out / Pub-Sub

**Pattern**: One message → copied to multiple queues or consumers.

**Pub-Sub model**:
- Producers publish to **topics**
- Consumers subscribe to topics of interest
- Message broker handles routing

**Use cases**:
- Event notification (order placed → email service, warehouse service, analytics service)
- Broadcasting updates (config change → all services)
- Multi-tenant systems (one message → all tenant-specific queues)

**Technologies**:
- **Kafka**: Topics with multiple consumer groups
- **RabbitMQ**: Exchanges with bindings (fanout exchange)
- **SNS + SQS**: AWS pub-sub pattern (SNS topic → multiple SQS queues)
- **NATS**: High-performance pub-sub

**Queueing theory**: Each subscriber has its own queue ([M/M/c](mmc-queue.md) per subscriber). Bottleneck = slowest subscriber.

## Pull vs Push

### Pull Model (Consumer-Driven)
- **Consumer polls queue** for messages
- Consumer requests N messages at a time
- **Backpressure-friendly**: Consumer only pulls when ready
- **Examples**: Kafka, SQS (long-polling), RabbitMQ (basic.get)

**Pros**:
- Consumer controls rate
- Natural [backpressure](backpressure.md)
- Easier to scale consumers dynamically

**Cons**:
- Higher latency (polling interval)
- Wasted polls if queue is empty (mitigated by long-polling)

### Push Model (Queue-Driven)
- **Queue pushes messages** to consumer
- Consumer receives messages as they arrive
- **Examples**: RabbitMQ (basic.consume), Google Pub/Sub (push subscriptions), webhooks

**Pros**:
- Lower latency (immediate delivery)
- No polling overhead

**Cons**:
- Risk of overwhelming consumer (requires [backpressure](backpressure.md) mechanism)
- Consumer must be online to receive

**Hybrid**: Many systems support both (e.g., Google Pub/Sub has push and pull subscriptions).

## Ordering Guarantees

### FIFO (First-In-First-Out)
- Messages processed in arrival order
- **Strict FIFO**: Total ordering across all messages
- **Per-partition FIFO**: Ordering within a partition/shard, not globally
- **Examples**: SQS FIFO queues, Kafka (per-partition)

**Trade-off**: Strict FIFO limits parallelism (can't process out of order).

### Unordered
- No ordering guarantee
- **Fastest**: Maximum parallelism
- **Examples**: SQS standard queues, RabbitMQ (default)

**Use case**: When order doesn't matter (idempotent operations, independent tasks)

### Partial Ordering
- Ordering within a key/shard, not globally
- **Examples**: Kafka (per-partition), Kinesis (per-shard)
- **Mechanism**: Hash message key to partition; all messages with same key → same partition → FIFO within partition

**Use case**: User actions (all events for user X in order), but different users can be processed in parallel.

## Visibility Timeout

**Concept** (SQS, Azure Service Bus):
- When consumer receives message, it becomes **invisible** to other consumers
- If consumer doesn't delete message within visibility timeout, message becomes visible again (automatic retry)
- Prevents duplicate processing

**Example** (SQS):
1. Consumer polls, receives message, visibility timeout = 30s
2. Consumer processes message (takes 20s), deletes message → success
3. If consumer crashes, message becomes visible after 30s → another consumer retries

**Queueing theory**: Visibility timeout prevents message from being counted in queue depth (L) while being processed.

## Durability and Persistence

### In-Memory (Volatile)
- **Fast**: No disk I/O
- **Risk**: Messages lost on crash
- **Examples**: Redis (without persistence), in-memory queues
- **Use case**: High-throughput, loss-tolerant (metrics, logs)

### Durable (Persistent)
- **Reliable**: Messages survive crashes
- **Slower**: Disk I/O overhead
- **Examples**: RabbitMQ (durable queues), Kafka, SQS
- **Use case**: Financial transactions, critical tasks

**Replication**: Distributed queues (Kafka, SQS) replicate across nodes/zones for fault tolerance.

## Cross-Framework Connections

### Queueing Theory (M/M/1, M/M/c)
Message queues are **distributed implementations** of theoretical queueing models:
- **Queue** = L (messages waiting)
- **Producers** = λ (arrival rate)
- **Consumers** = c servers with rate μ each
- [Little's Law](littles-law.md): L = λW applies
- [Erlang C](erlang-formulas.md): Predict wait time given λ, μ, c

**Monitoring**: [Queue depth](queue-metrics.md) (L), [consumer lag](queue-monitoring.md) (Lq), throughput (λ, μ).

### Reinertsen's Flow Economics
Message queues enable [queue-based load leveling](queues-in-product-development.md):
- Queue absorbs variance in λ (arrivals)
- Consumers operate at steady μ (service rate)
- [WIP Limits](wip-limits.md) = queue depth limits

[Cost of Delay](cost-of-delay.md): High queue depth (L) → long wait time (W) → delayed value delivery.

### Systems Thinking (Senge/Meadows)
Message queues are **stocks** (L):
- **Inflow**: Producers (λ)
- **Outflow**: Consumers (μ)
- **Balancing loop**: High L → alert → add consumers → L decreases

**Delays**: Capacity changes (adding consumers) take time; L reacts immediately to λ spikes. [Leverage Points](leverage-points.md): reducing λ (prevent unnecessary work) beats adding capacity.

### Taleb's Antifragility
Unbounded queues are **fragile**: they can grow without limit if λ > μ.

**Robustness mechanisms**:
- **Bounded queues**: Reject new messages when full (fail-fast)
- **[Backpressure](backpressure.md)**: Throttle producers when queue is deep
- **[Dead Letter Queues](dead-letter-queues.md)**: Isolate poison messages

**Barbell strategy**: Overprovision consumers (ρ < 80%) for robustness, not efficiency.

### Amazon Leadership Principles
**"Customer Obsession"**: SQS, Kinesis, EventBridge are Amazon-scale message queues enabling reliable, low-latency services.

**"Bias for Action"**: Async processing via queues decouples decision-making (produce) from execution (consume), enabling fast iteration.

### OKRs (Doerr/Grove)
**Key Result examples**:
- "P95 queue processing latency < 100ms"
- "Queue depth < 50 at P95"
- "Consumer lag < 1000 messages sustained"

Message queue metrics = Key Results. [Queue monitoring](queue-monitoring.md) = measurement.

## Common Failure Modes

### Poison Messages
- **Problem**: Message causes consumer to crash repeatedly
- **Impact**: Consumer enters retry loop, queue blocks
- **Solution**: [Dead Letter Queue](dead-letter-queues.md) after N retries

### Consumer Lag / Backlog
- **Problem**: λ > μ (producers faster than consumers)
- **Impact**: Queue grows unbounded, latency increases
- **Solution**: Scale consumers, optimize processing, or throttle producers ([backpressure](backpressure.md))

### Message Duplication
- **Problem**: At-least-once delivery ([delivery semantics](delivery-semantics.md)) causes duplicates
- **Impact**: Duplicate processing (double-charge, double-email)
- **Solution**: Idempotent consumers (detect and skip duplicates)

### Hot Partitions
- **Problem** (Kafka, Kinesis): Uneven key distribution → one partition overloaded
- **Impact**: One partition's consumer lags, others idle
- **Solution**: Better key distribution, more partitions, or custom partitioner

## Key Takeaways

1. **Message queues implement queueing theory** — [M/M/c](mmc-queue.md), [Little's Law](littles-law.md), [Erlang C](erlang-formulas.md) all apply
2. **Asynchronous processing** — decouple producers from consumers, enable scalability
3. **Durability vs. speed** — in-memory (fast, volatile) vs. disk (slow, durable)
4. **Pull vs. push** — pull = backpressure-friendly, push = lower latency
5. **Ordering** — FIFO (strict or per-partition) vs. unordered (maximum parallelism)
6. **Monitor queue depth and lag** — leading indicators of congestion

## Further Reading

- [M/M/c Queue](mmc-queue.md) — theoretical model behind message queues
- [Queue Metrics](queue-metrics.md) — monitoring L, λ, W, ρ
- [Backpressure](backpressure.md) — preventing unbounded queue growth
- [Dead Letter Queues](dead-letter-queues.md) — isolating poison messages
- [Delivery Semantics](delivery-semantics.md) — at-most-once, at-least-once, exactly-once

## See Also

- [Jackson Networks](jackson-networks.md) — multi-stage message processing pipelines
- [Little's Law](littles-law.md) — L = λW applies to all queues
- [Flow Economics](flow-economics.md) — economic lens on queue-based systems
- [Queue Monitoring](queue-monitoring.md) — observability and alerting
