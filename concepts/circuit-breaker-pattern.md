---
title: Circuit Breaker Pattern
tags: [distributed-systems, resilience, fault-tolerance, patterns, microservices]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queuing-theory-systems.md]
---

# Circuit Breaker Pattern

A fault-tolerance pattern that prevents cascading failures by failing fast when a downstream service is unhealthy. Monitors failure rate; opens circuit (rejects requests) when threshold exceeded; allows downstream to recover.

## The Problem

**Cascading failure in distributed systems.**

**Scenario**:
1. Service A calls Service B
2. Service B is slow/failing (overloaded, bug, network issue)
3. Service A waits for timeout (e.g., 30 seconds)
4. Requests to Service A queue up (waiting for B)
5. Service A exhausts threads/connections
6. Service A becomes slow/unresponsive
7. Service C (depends on A) now experiences same issue
8. **Cascading failure**: B → A → C → entire system down

**Without circuit breaker**:
- Retry storms (A keeps hammering failing B)
- Thread exhaustion (A blocked waiting for B)
- Slow propagation of failure (takes time for A to realize B is down)
- No recovery (A never stops calling B, preventing B from recovering)

## The Solution

**Circuit breaker monitors calls to downstream service. On repeated failures, opens circuit (fails fast). After timeout, allows probe requests. If successful, closes circuit (resume normal operation).**

## States

```
      ┌─── success ───┐
      │                │
   CLOSED ─ failure → OPEN ─ timeout → HALF-OPEN
      ↑                               │
      └───────── success ─────────────┘
```

### 1. Closed (Normal Operation)

- **Behavior**: All requests forwarded to downstream
- **Monitoring**: Track failure rate (e.g., failures / total requests in sliding window)
- **Transition**: If failure rate > threshold → OPEN

**Example**: 50% failure rate over last 100 requests → OPEN

### 2. Open (Failing Fast)

- **Behavior**: All requests **rejected immediately** (fail fast, no downstream call)
- **Return**: Error (503 Service Unavailable, or fallback response)
- **Duration**: Fixed timeout (e.g., 60 seconds)
- **Transition**: After timeout → HALF-OPEN

**Why**: Give downstream time to recover (stop hammering it with requests).

### 3. Half-Open (Testing Recovery)

- **Behavior**: Allow **limited probe requests** to downstream (e.g., 1-10 requests)
- **Success**: All probes succeed → CLOSED (resume normal operation)
- **Failure**: Any probe fails → OPEN (downstream not recovered yet)

**Why**: Test if downstream is healthy before fully resuming traffic.

## Benefits

**1. Fail fast**:
- Open circuit → immediate rejection (no waiting for timeout)
- Low latency failure (milliseconds, not 30 seconds)
- Threads not blocked

**2. Prevent cascading failure**:
- Upstream (A) doesn't exhaust resources waiting for downstream (B)
- Failure isolated to B; doesn't propagate to A, C, D

**3. Allow recovery**:
- Open circuit → stop sending requests → downstream (B) can recover (catch up on queue, restart, scale up)
- Without circuit breaker, retry storm prevents recovery

**4. Observability**:
- Circuit breaker state (open/closed) = clear signal of system health
- Alert on "circuit open" → downstream is unhealthy

## Relation to Queues

**Queue + Circuit Breaker = Graceful Degradation**

**Without circuit breaker**:
- Downstream slow → queue grows unbounded → upstream OOM

**With circuit breaker**:
- Downstream slow → queue grows → **circuit breaker monitors queue depth**
- Queue depth > threshold → **open circuit** (reject new requests)
- Stop adding to queue → queue drains → system stabilizes

**Pattern**: Use queue depth as circuit breaker signal
```
if queue_depth > THRESHOLD_CRITICAL:
    circuit_breaker.open()
    reject_request(503)  # Service Unavailable
```

**Relation to [Backpressure](backpressure.md)**:
- Circuit breaker is one form of backpressure
- Backpressure = signal to slow down
- Circuit breaker = extreme backpressure (stop completely)

## Implementation

**Libraries**:
- **Hystrix** (Netflix; deprecated but widely known)
- **Resilience4j** (Java; modern replacement for Hystrix)
- **Polly** (.NET)
- **pybreaker** (Python)
- **Akka Circuit Breaker** (Scala/Java)

**Example** (Python with pybreaker):
```python
from pybreaker import CircuitBreaker

breaker = CircuitBreaker(
    fail_max=5,       # Open after 5 failures
    timeout_duration=60  # Stay open for 60 seconds
)

@breaker
def call_downstream():
    response = requests.get('http://service-b/api')
    response.raise_for_status()
    return response.json()

try:
    data = call_downstream()
except CircuitBreakerError:
    # Circuit is open; fail fast
    return fallback_response()
```

**Configuration**:
- **fail_max**: Failure threshold (how many failures before opening?)
- **timeout_duration**: How long to stay open (recovery window)
- **Success threshold** (half-open): How many successes to close circuit?
- **Failure definition**: What counts as failure? (timeout, 5xx, exceptions)

## Monitoring

**Key metrics**:
- **Circuit state**: closed/open/half-open
- **Failure rate**: % of requests failing
- **Open duration**: How long circuit has been open
- **Rejected requests**: Count of fast-fail rejections

**Alerts**:
- Circuit opened → downstream unhealthy (page on-call)
- Circuit open > SLA duration → escalate (downstream not recovering)
- Frequent open/close → flapping (tuning needed)

**Dashboard**:
```
Service B Circuit Breaker
  State:         ⚠️  OPEN (last 5 minutes)
  Failure Rate:  🔴 75% (threshold: 50%)
  Rejected:      🚫 1.2k requests
  Last Success:  ⏱️  10 minutes ago
```

## Cross-Framework Connections

**[Backpressure](backpressure.md)**:
- Circuit breaker = extreme backpressure (stop sending requests)
- Complements queue-based backpressure (reject when queue full)

**[Queue-Based Load Leveling](queue-based-load-leveling.md)**:
- Circuit breaker + queue = complete pattern
  - Queue absorbs short spikes
  - Circuit breaker activates on sustained failure (queue doesn't drain)

**[Systems Thinking](systems-thinking.md) / [Feedback Loops](feedback-loops.md)**:
- Circuit breaker = **balancing loop** (negative feedback)
- Without it: **reinforcing loop** (A hammers B → B gets worse → A retries more → B collapses)
- **Limits to Growth archetype**: circuit breaker is the balancing intervention

**[Little's Law](littles-law.md)**:
- Open circuit → λ (arrival rate to downstream) = 0
- Queue depth L stops growing (no new arrivals)
- Allows queue to drain (W decreases)

**[Antifragility](antifragility.md) / [Taleb](../people/nassim-taleb.md)**:
- Circuit breaker = antifragile design (small failures prevent big ones)
- Open circuit = controlled burn (prevents catastrophic cascade)
- Fragile: no circuit breaker → one failure propagates system-wide

**[Westrum](../people/ron-westrum.md) / Culture**:
- **Generative culture**: Circuit breaker state monitored, acted on (investigate root cause)
- **Bureaucratic culture**: Circuit breaker exists but ignored (dashboards not watched)
- **Pathological culture**: Circuit breaker seen as problem (shooting the messenger)

**[Blameless Post-Mortems](westrum-cultural-typologies.md)**:
- Circuit breaker opening = blameless signal (system protected itself)
- Post-mortem: why did downstream fail? How to prevent?

**[Meadows](../people/donella-meadows.md) / [Leverage Points](leverage-points.md)**:
- Circuit breaker = Level 8 (strength of balancing loops)
- Tighter feedback (faster circuit opening) = higher leverage

**[Cost of Delay](cost-of-delay.md)**:
- Open circuit → rejected requests → opportunity cost
- But preventing cascade → saves total system downtime cost
- Economic tradeoff: (rejected request cost) vs. (cascading failure cost)

## Anti-Patterns

**No circuit breaker**:
- "We'll just retry with exponential backoff"
- Result: Retry storm, cascading failure
- Solution: Backoff helps but isn't sufficient; need circuit breaker

**Too-sensitive circuit breaker**:
- Opens on first failure (fail_max=1)
- Result: Flapping (open/close/open), unnecessary rejection
- Solution: Tune threshold (fail_max=5-10 is typical)

**Too-long timeout**:
- Circuit stays open for 10 minutes
- Result: Downstream recovered after 1 minute, but circuit still open (waste)
- Solution: Shorter timeout (30-60 seconds), use half-open probe

**Circuit breaker per instance**:
- Each instance has own circuit breaker state (not shared)
- Result: Inconsistent behavior (some instances open, others closed)
- Solution: Shared state (Redis, Consul) or accept per-instance (often fine)

**No fallback**:
- Circuit opens → return 503 → user sees error
- Result: Degraded UX
- Solution: Fallback response (cached data, default value, queue request)

**Circuit breaker instead of capacity planning**:
- "We're overloaded; let's add circuit breaker"
- Result: Circuit breaker opens frequently (rejecting valid requests)
- Solution: Circuit breaker handles transient failures, not sustained overload. If sustained, add capacity.

## Fallback Strategies

**When circuit opens, return**:

**1. Cached response**:
- Last successful response (with cache timestamp)
- Example: Product catalog (serve stale data)

**2. Default value**:
- Sensible default for this endpoint
- Example: Recommendations service → return empty list (or popular items)

**3. Queue for later**:
- Accept request, queue for processing when downstream recovers
- Example: Analytics event (queue to Kafka, process later)

**4. Degraded mode**:
- Partial functionality
- Example: Search with filters down → return unfiltered results

**5. Fail gracefully**:
- 503 Service Unavailable with clear message
- Better than 500 Internal Server Error (timeout)

## When to Use

**Use circuit breaker when**:
- Distributed system (microservices, service mesh)
- Calls to external services (third-party APIs)
- Calls to slow services (database, cache, ML model)
- Cascading failure risk (A → B → C dependencies)

**Don't use when**:
- Single-service monolith (no downstream)
- Synchronous in-process calls (function call, no network)
- Simple retry-with-backoff is sufficient (no cascade risk)

## References

- [Backpressure](backpressure.md) — circuit breaker as backpressure mechanism
- [Queue-Based Load Leveling](queue-based-load-leveling.md) — circuit breaker + queue pattern
- [Systems Thinking](systems-thinking.md) — circuit breaker as balancing loop
- [Feedback Loops](feedback-loops.md) — balancing loops prevent reinforcing cascade
- [Little's Law](littles-law.md) — stopping λ (arrivals) lets queue drain
- [Antifragility](antifragility.md) — circuit breaker as antifragile design
- [Leverage Points](leverage-points.md) — circuit breaker as high-leverage intervention
- [Westrum Cultural Typologies](westrum-cultural-typologies.md) — circuit breaker monitoring as cultural signal
