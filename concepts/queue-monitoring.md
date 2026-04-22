---
title: Queue Monitoring
tags: [observability, metrics, alerting, capacity-planning, sre]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queueing-theory.md]
layout: default
parent: Concepts
---

# Queue Monitoring

Observability and alerting for queueing systems. Monitoring queue health enables capacity planning, SLA compliance, and prevents cascading failures before they occur.

## Essential Metrics

See [Queue Metrics](queue-metrics.md) for detailed definitions. Summary:

1. **Queue Depth (L)**: Count of items waiting
2. **Age of Oldest Message**: How long the oldest item has been waiting
3. **Arrival Rate (λ)**: Items entering per time
4. **Departure Rate (μ)**: Items leaving per time
5. **Utilization (ρ)**: Fraction of capacity in use
6. **Latency Percentiles (P50, P95, P99)**: Distribution of processing time

## Why Monitor Queues?

**Leading indicator**: Queue depth (L) grows *before* downstream systems fail. By the time CPU or memory alerts fire, the queue may already be unmanageable.

**SLA compliance**: Many SLAs target latency (e.g., "P95 < 100ms"). Queue time dominates latency at high utilization ([M/M/1 trap](mm1-queue.md)).

**Capacity planning**: Historical queue metrics inform scaling decisions ([Erlang C](erlang-formulas.md) calculations).

## Alert Thresholds

### Queue Depth Alerts
- **Warning**: L > 2× typical (early signal)
- **Critical**: L > 10× typical or approaching capacity limit

**Example**: Normal L = 50, warning at L > 100, critical at L > 500.

### Age-Based Alerts
- **Warning**: Oldest message age > 50% of SLA
- **Critical**: Oldest message age > SLA

**Example**: SLA = 60s processing time, warning at age > 30s, critical at age > 60s.

### Utilization Alerts
- **Warning**: ρ > 80%
- **Critical**: ρ > 90%

**Rationale**: [M/M/1 queue](mm1-queue.md) shows nonlinear degradation above 80% utilization.

### Latency Alerts (P95/P99)
- **Warning**: P95 > 80% of SLA
- **Critical**: P95 > SLA

**Example**: SLA = P95 < 200ms, warning at P95 > 160ms, critical at P95 > 200ms.

### Consumer Lag (Kafka/Streaming)
- **Warning**: Lag > threshold (e.g., 10,000 messages) OR lag increasing for > 5 min
- **Critical**: Lag > critical threshold (e.g., 100,000) OR lag increasing for > 15 min

## Auto-Scaling Based on Metrics

### Scale on Queue Depth (Recommended)
**Mechanism**: Add consumers when L exceeds threshold.

**AWS SQS + Lambda**:
- Lambda polls SQS
- AWS auto-scales Lambda concurrency based on queue depth
- No configuration needed (built-in)

**Kubernetes HPA + KEDA**:
```yaml
apiVersion: keda.sh/v1alpha1
kind: ScaledObject
metadata:
  name: sqs-scaler
spec:
  scaleTargetRef:
    name: my-consumer-deployment
  triggers:
    - type: aws-sqs-queue
      metadata:
        queueURL: https://sqs...
        queueLength: "100"  # Target: 100 messages per pod
        awsRegion: "us-east-1"
```

**Result**: If queue depth = 1000 → scale to 10 pods (1000/100).

### Scale on Utilization (Lagging Indicator)
**Problem**: CPU/memory are lagging indicators. By the time they spike, queue may already be large.

**Better**: Use queue depth (leading indicator) + CPU/memory (confirmation).

### Predictive Scaling
- **Pattern-based**: Known traffic patterns (daily/weekly cycles)
- Pre-scale before expected spike
- **Example**: E-commerce site scales at 11:50am before lunch traffic

## Monitoring Stack

### Tools

**Message Queues**:
- **RabbitMQ**: Management UI, Prometheus exporter
- **Kafka**: JMX metrics, Prometheus exporter, Confluent Control Center
- **AWS SQS**: CloudWatch metrics (ApproximateNumberOfMessages, Age)
- **Redis**: INFO command, custom instrumentation

**Observability Platforms**:
- **Prometheus + Grafana**: Scrape metrics, visualize, alert
- **Datadog, New Relic, SignalFx**: Pre-built dashboards, anomaly detection
- **OpenTelemetry**: Instrument custom queues, export to any backend

### Custom Instrumentation (Example: Python)
```python
import time
from prometheus_client import Gauge, Counter, Histogram

queue_depth = Gauge('queue_depth', 'Current queue depth')
queue_age = Gauge('queue_oldest_message_age_seconds', 'Age of oldest message')
enqueue_total = Counter('queue_enqueue_total', 'Total items enqueued')
dequeue_total = Counter('queue_dequeue_total', 'Total items dequeued')
processing_time = Histogram('queue_processing_seconds', 'Processing time distribution')

# In producer:
def enqueue(item):
    queue.put(item)
    enqueue_total.inc()
    queue_depth.set(queue.qsize())

# In consumer:
def dequeue():
    start = time.time()
    item = queue.get()
    dequeue_total.inc()
    queue_depth.set(queue.qsize())

    process(item)

    processing_time.observe(time.time() - start)
    queue.task_done()
```

## Dashboards

### Essential Views

**1. Queue Health Overview**:
- Queue depth (L) over time (line chart)
- Arrival rate (λ) vs. departure rate (μ) (stacked area chart)
- Utilization (ρ) (gauge)

**2. Latency Distribution**:
- P50, P95, P99 latency (line chart)
- Latency histogram (heatmap)

**3. Consumer Performance**:
- Per-consumer throughput
- Error rate (%)
- [Dead Letter Queue](dead-letter-queues.md) depth

**4. Capacity Planning**:
- Historical utilization trends
- Peak load patterns (daily, weekly)
- Headroom (capacity - current load)

## Using Little's Law for Validation

[Little's Law](littles-law.md): **L = λW**

**Use case 1: Anomaly detection**
- Measured: L = 500, λ = 100/s
- Expected: W = L/λ = 5s
- If measured W = 10s → something is wrong (bottleneck, slow consumer)

**Use case 2: Capacity planning**
- SLA: W < 100ms
- Measured: λ = 1000/s
- Required: L < λW = 1000 × 0.1 = 100 items
- If L is currently 200 → either reduce L (add capacity) or relax SLA

## Common Failure Modes

### Growing Queue Depth
**Symptom**: L increases steadily over time.
**Diagnosis**: λ > μ (arrival rate exceeds processing rate).
**Action**: Scale consumers (increase μ) or throttle producers (reduce λ via [backpressure](backpressure.md)).

### Latency Spike
**Symptom**: P95/P99 latency suddenly increases.
**Diagnosis**: Utilization crossed nonlinear threshold ([M/M/1 trap](mm1-queue.md)), or downstream bottleneck.
**Action**: Investigate queue depth; scale if ρ > 80%.

### Oscillating Queue Depth
**Symptom**: L oscillates (sawtooth pattern).
**Diagnosis**: [Feedback loop](feedback-loops.md) delay. Auto-scaler lags behind load changes.
**Action**: Tune auto-scaler sensitivity, or pre-scale predictively.

### Dead Letter Queue Accumulation
**Symptom**: [DLQ](dead-letter-queues.md) depth increasing.
**Diagnosis**: Systemic processing failures (poison messages, downstream service down).
**Action**: Investigate DLQ messages, fix root cause, replay from DLQ.

## Cross-Framework Connections

### Reinertsen's Flow Economics
Monitoring queue depth (L) = monitoring [WIP](wip-limits.md). High WIP = long cycle time ([Cost of Delay](cost-of-delay.md)).

**Economic frame**: Queue depth is not just a metric; it's delayed economic value.

### Systems Thinking (Senge/Meadows)
Queue monitoring reveals [system dynamics](systems-thinking.md):
- Growing L = inflow > outflow (imbalance)
- Oscillating L = [feedback loop](feedback-loops.md) with delay
- **Balancing loop**: Alert → add capacity → L decreases

### Taleb's Antifragility
Tail latency (P99, P999) reveals [fragility](antifragility.md). If P99 is 100× median, system is fragile to load spikes.

**Monitoring tail latency** = measuring antifragility.

### Kahneman's Cognitive Biases
**WYSIATI**: Visible throughput (λ) obscures invisible queue depth (L). Always monitor **both**.

**Availability heuristic**: Recent smooth performance → assume queue is fine. Monitor L continuously to detect accumulation.

### Amazon Leadership Principles
**"Dive Deep"**: Metrics (L, W, ρ) reveal system behavior. Don't just monitor CPU; monitor queue depth.

**"Bias for Action"**: Alerts should trigger action (scale, investigate, throttle), not just noise.

### OKRs (Doerr/Grove)
**Key Result examples**:
- "P95 API latency < 100ms" → monitor queue latency
- "Queue depth < 50 at P95" → monitor L
- "Zero DLQ accumulation for > 1 hour" → monitor DLQ depth

Monitoring = measurement of Key Results.

## SRE Best Practices

**1. Monitor what matters**: Queue depth (L), not just CPU.
**2. Alert on trends**: L increasing for > 5 min, not just instantaneous spikes.
**3. Percentiles > Averages**: P95/P99 reveal user experience.
**4. Auto-scale on queue depth**: Leading indicator, faster than CPU.
**5. Dead Letter Queue = canary**: DLQ accumulation signals systemic failure.
**6. Runbooks**: Document response to each alert (scale, investigate, etc.).

## Key Takeaways

1. **Queue depth (L) is the leading indicator** — monitor it, alert on it, scale on it
2. **Utilization > 80% = danger zone** — nonlinear latency degradation ([M/M/1](mm1-queue.md))
3. **Percentiles reveal tail latency** — P95/P99 matter more than mean
4. **Little's Law for validation** — L = λW; use it to detect anomalies
5. **DLQ = smoke alarm** — accumulation signals systemic failure
6. **Auto-scale on queue depth** — faster response than CPU/memory

## Further Reading

- [Queue Metrics](queue-metrics.md) — detailed definitions of L, λ, W, ρ
- [Little's Law](littles-law.md) — L = λW for validation and capacity planning
- [M/M/1 Queue](mm1-queue.md) — why utilization > 80% is dangerous
- [Erlang Formulas](erlang-formulas.md) — capacity planning math
- [Dead Letter Queues](dead-letter-queues.md) — monitoring DLQs
- [Backpressure](backpressure.md) — what to do when queue depth grows

## See Also

- [Message Queues](message-queues.md) — implementations and monitoring tools
- [Flow Economics](flow-economics.md) — economic lens on queue metrics
- [Systems Thinking](systems-thinking.md) — queue dynamics and feedback loops
- [Cost of Delay](cost-of-delay.md) — economic cost of queue time
