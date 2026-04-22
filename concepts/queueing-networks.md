---
title: Queueing Networks
tags: [queueing-theory, systems, bottlenecks, jackson-networks, capacity-planning]
created: 2026-04-22
updated: 2026-04-22
sources: [sources/queuing-theory-systems.md]
---

# Queueing Networks

Multiple queues connected in a network, where items move between queues according to routing rules. Foundation for analyzing complex systems like manufacturing lines, computer networks, distributed systems, and workflow pipelines.

## Jackson Networks

Developed by James R. Jackson (1957). The most important class of queueing networks.

**Properties**:
- Multiple queues, each is an M/M/c queue
- Items route between queues with specified probabilities
- Network has **product-form solution**: joint steady-state distribution = product of individual queue distributions
- This is remarkable: complex network behavior can be decomposed into independent single-queue analyses

**Types**:

**Open networks**:
- Items arrive from outside, are processed through multiple queues, eventually leave
- Example: web requests → load balancer → app servers → database → response

**Closed networks**:
- Fixed population (N items) circulates through queues forever
- Example: N users, N requests always in flight (as soon as one completes, another is issued)
- Common in performance testing ("closed workload generator")

**Tandem queues**:
- Output of queue i is input of queue i+1 (serial pipeline)
- Example: CI/CD pipeline stages (build → test → deploy)

**Feedback loops**:
- Items can revisit queues (cycles in routing graph)
- Example: code review → fix → re-review

## Bottleneck Analysis

In a queueing network, the **bottleneck** is the queue with highest utilization (ρ = λ/μ).

**Key insight**: Bottleneck limits system throughput. No matter how much you optimize non-bottleneck queues, overall throughput cannot exceed bottleneck capacity.

**Example**: Pipeline with 3 stages:
1. Build: μ₁ = 10/hour
2. Test: μ₂ = 5/hour (bottleneck)
3. Deploy: μ₃ = 20/hour

System throughput ≤ 5/hour (limited by test stage), regardless of build/deploy speed.

**Practical implication**: Optimize the bottleneck first. Improving non-bottleneck queues has zero throughput impact until you shift the bottleneck.

## Routing and Load Balancing

Items move between queues according to **routing probabilities**.

**Example**: Load balancer distributes requests to c servers
- p = 1/c probability to each server (uniform distribution)
- If servers are heterogeneous (different μ), route more to faster servers

**Optimal load balancing**: Route to minimize maximum utilization (balance load).

**Join-Shortest-Queue (JSQ)**: Route to queue with fewest items. Provably optimal for homogeneous servers (minimizes average latency).

**Power-of-Two-Choices**: Route to less-loaded of 2 randomly sampled queues. Nearly as good as JSQ, much simpler to implement. Used in production load balancers.

## Capacity Planning

Queueing networks let you answer:
1. **Given**: Arrival rates, service rates, routing probabilities
2. **Find**: Queue depths, utilizations, end-to-end latency
3. **Solve for**: How many servers (c) at each stage to meet SLA?

**Method**:
1. Model system as queueing network (draw diagram)
2. Compute arrival rate λᵢ at each queue (account for routing)
3. Check stability: ρᵢ = λᵢ/(cᵢμᵢ) < 1 for all i
4. Use [Kendall notation](kendall-notation.md) formulas for each queue
5. Sum or max latencies (depending on series/parallel topology)

**Tool support**: Simulation (discrete-event simulation), analytical solvers (for Jackson networks), queueing theory libraries.

## Real-World Examples

**Microservices architecture**:
- Each service = queue (or multiple queues if service has multiple endpoints)
- Requests route between services (API calls)
- Bottleneck analysis → which service to scale first

**Manufacturing line**:
- Each station = queue
- Products move down the line
- Bottleneck = slowest station (Theory of Constraints)

**CI/CD pipeline**:
- Build, test, deploy stages = queues
- Commits route through stages
- Bottleneck = longest stage (often test or deploy)

**Hospital / healthcare**:
- Triage, exam rooms, imaging, labs = queues
- Patients route through system
- Bottleneck analysis → where to add capacity

## Cross-Framework Connections

**[Systems Thinking](systems-thinking.md) / [Meadows](../people/donella-meadows.md)**:
- Queueing network = stock-flow diagram
- Each queue is a stock, routing is flow between stocks
- Bottleneck = constraint on system flow
- Feedback loops in routing = reinforcing/balancing loops

**[Reinertsen](../people/donald-reinertsen.md) / [Flow Economics](flow-economics.md)**:
- Product development is a queueing network (requirements → design → code → test → deploy)
- [Cost of Delay](cost-of-delay.md) = economic value of latency through the network
- [WIP Limits](wip-limits.md) = cap on N (closed network population)
- Bottleneck optimization = where to add capacity first

**[Theory of Constraints](https://en.wikipedia.org/wiki/Theory_of_constraints)** (Goldratt):
- TOC = applied bottleneck analysis for manufacturing
- "The Goal" is a queueing network story
- Same math, different framing

**[Message Queues](message-queues.md) / Distributed Systems**:
- Microservices = queueing network
- Each service has input queue (message queue or HTTP load balancer)
- Bottleneck → where to scale (add workers/servers)
- [Backpressure](backpressure.md) propagates upstream through network

**[Little's Law](littles-law.md)**:
- Applies to each queue in the network AND to the network as a whole
- End-to-end latency W = sum of per-queue W (if serial) or max (if parallel)
- End-to-end WIP L = sum of per-queue L

**[Kendall Notation](kendall-notation.md)**:
- Each queue in network has its own A/S/c classification
- Network analysis decomposes into per-queue analysis (Jackson networks)

## When to Use Queueing Networks

**Use when**:
- System has multiple stages (not single queue)
- Items route between stages
- Want to understand bottlenecks, capacity needs, end-to-end latency

**Don't use when**:
- Single queue (use simple [Kendall notation](kendall-notation.md) model)
- Routing is too complex (use simulation instead)
- Service times are correlated across queues (violates Jackson network assumptions)

## References

- [Kendall Notation](kendall-notation.md) — classifying individual queues in the network
- [Little's Law](littles-law.md) — applies to networks and individual queues
- [Systems Thinking](systems-thinking.md) — stock-flow diagrams = queueing networks
- [Flow Economics](flow-economics.md) — economic frame for queueing networks
- [Message Queues](message-queues.md) — distributed systems as queueing networks
- [Queues in Product Development](queues-in-product-development.md) — Reinertsen's application
