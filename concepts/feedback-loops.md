---
title: Feedback Loops
tags: [senge, meadows, systems-thinking, reinforcing, balancing, feedback, dynamics]
created: 2026-04-17
updated: 2026-04-17
sources: [sources/systems-thinking-senge-meadows.md]
layout: default
parent: Concepts
---

# Feedback Loops

The core structural element of systems thinking. A feedback loop exists when a change in a stock affects the flows that change that stock — creating circular causality rather than linear cause-and-effect.

Feedback loops are the reason systems behave in characteristic patterns — growth, oscillation, equilibrium, collapse. Understanding which loops are driving a system is the key to changing its behaviour.

---

## Reinforcing (Positive) Loops

A change in a stock amplifies further change in **the same direction**. Also called positive feedback (the signal is amplified) — though the effect may be positive or negative in value terms.

**The mechanism:** Stock increases → flow rate increases → stock increases faster.

**Behaviour produced:** Exponential growth (or exponential collapse if the loop runs in the negative direction). Does **not** self-correct. Runs until it hits a constraint or collapses.

**Examples:**
| Loop | Stock | Amplifying flow |
|---|---|---|
| Compound interest | Money | Interest added per period |
| Network effects | Users | Value → attracting more users |
| [Amazon flywheel](./amazon-growth-flywheel.md) | Customer experience | → traffic → sellers → selection → lower prices |
| Viral spread | Infected | → contacts → new infections |
| [Social proof](./social-proof.md) | Adopters | → visible use → more adopters |
| Panic | Fear | → selling → price drop → more fear |
| Skill/[compounding](./compounding.md) | Capability | → better work → more capability |

**The trap:** In the short term, reinforcing loops feel like success. The growth looks good. The danger is what happens when the constraint arrives — and you've been ignoring it because the loop was running so well.

---

## Balancing (Negative) Loops

A change in a stock triggers a response that **opposes** that change. Also called negative feedback (the signal is corrected) — though this is usually stabilising and desirable.

**The mechanism:** Stock moves away from goal → corrective action → stock moves back toward goal.

**Behaviour produced:** Stability, goal-seeking, oscillation (if delays are present).

**Examples:**
| Loop | Goal | Corrective flow |
|---|---|---|
| Thermostat | Target temperature | Heat on/off |
| Predator-prey | Population balance | Predation rate rises/falls |
| [WIP limits](./wip-limits.md) | WIP at target level | New work blocked when limit reached |
| Price mechanism | Market clearing price | Demand adjusts to price |
| [OKR review](./okrs.md) | Goal achievement | Corrective actions when behind |
| Body temperature | 37°C | Shivering, sweating |

---

## Delays

**The most important feature** of feedback loops in practice. When there is a delay between the action and the feedback signal:

1. Decision-makers keep acting **past** the point where their action has already taken effect (because the effect hasn't shown up yet)
2. The system **overshoots** the goal
3. A corrective response arrives and overshoots in the **opposite direction**
4. Result: **oscillation** — boom-bust cycles, overshoot and collapse

**The shower analogy:** You turn the hot water up. It's still cold (delay). You turn it up more. Finally hot water arrives — too hot. You turn it down. Still too hot. You turn it down more. Cold water arrives again. The delay produced oscillation.

**In organisations:**
- Hiring lags: you recruit for current demand; new staff arrive into a different market
- [Planning fallacy](./planning-fallacy.md): plans don't model the delays in implementation
- [Cost of Delay](./cost-of-delay.md): the cost accumulates during the delay; we keep acting as if it doesn't

**The fix:** Shorten the delay if possible (faster feedback → less overshoot). Or recognise the delay and act more conservatively. Reinertsen's small [batch sizes](./batch-size.md) and frequent releases are fundamentally delay-reduction mechanisms.

---

## Loop Dominance

In any complex system, **multiple loops run simultaneously** — some reinforcing, some balancing, operating at different time scales. The system's behaviour at any moment is determined by which loop is dominant.

As a system evolves, loop dominance can shift:
- Early growth: the reinforcing loop dominates (growth accelerates)
- Approaching constraint: a balancing loop grows in strength
- At constraint: balancing loop dominates; growth plateaus
- If the constraint is removed or the reinforcing loop weakens: behaviour shifts again

The "[Limits to Growth](./system-archetypes.md)" archetype is exactly this: a reinforcing loop dominated the early phase; a balancing constraint gradually became dominant; if the constraint is ignored and the reinforcing loop is pushed harder, the balancing loop strengthens faster and growth collapses.

---

## Cross-Framework Connections

### ↔ Amazon Growth Flywheel
The [Amazon flywheel](./amazon-growth-flywheel.md) is explicitly a reinforcing loop — Bezos drew it as a diagram. Customer experience → traffic → sellers → selection → lower costs → lower prices → customer experience. The power of the flywheel is the compounding of the reinforcing loop over time.

### ↔ Compounding
[Compounding](./compounding.md) is a reinforcing feedback loop applied to wealth, skill, and knowledge. The earlier you start the loop and the longer it runs without interruption, the more powerful it becomes. This is why Naval emphasises playing long-term games with long-term people — you're letting reinforcing loops compound.

### ↔ Cialdini (Social Proof / Commitment)
[Social proof](./social-proof.md) and [commitment & consistency](./commitment-and-consistency.md) are reinforcing loops in human social behaviour. More adopters → more visible adoption → more adopters. More commitment → stronger identity → more commitment. Cialdini describes the trigger; feedback loop analysis explains why they escalate.

### ↔ Taleb (Antifragility / Black Swan)
[Black Swans](./black-swan.md) are often the collapse of a reinforcing loop that has been running below visibility. Taleb's [antifragility](./antifragility.md) is a design approach for systems with positive feedback (reinforcing loops) that builds in convexity — so that volatility (the arrival of a constraint or a shock) amplifies gains rather than producing collapse.

### ↔ Reinertsen (Utilisation Trap)
The utilisation trap is a dangerous reinforcing loop: high utilisation → long queues → slower throughput → more WIP needed to maintain output → higher utilisation. The only way out is to deliberately break the loop — [WIP limits](./wip-limits.md) are a balancing loop imposed on the system.

---

## Related Pages

- [Systems Thinking](./systems-thinking.md)
- [System Archetypes](./system-archetypes.md)
- [Leverage Points](./leverage-points.md)
- [Peter Senge](../people/peter-senge.md)
- [Donella Meadows](../people/donella-meadows.md)
- [Amazon Growth Flywheel](./amazon-growth-flywheel.md)
- [Compounding](./compounding.md)
- [Antifragility](./antifragility.md)
- [Black Swan](./black-swan.md)
- [WIP Limits](./wip-limits.md)
- [Cost of Delay](./cost-of-delay.md)
- [Batch Size](./batch-size.md)
- [Social Proof](./social-proof.md)
- [Commitment and Consistency](./commitment-and-consistency.md)
- [Planning Fallacy](./planning-fallacy.md)

## Connections

- **[Peter Senge](../people/peter-senge.md)** — feedback loops as the core of systems thinking and the learning organisation
- **[Donella Meadows](../people/donella-meadows.md)** — formalised feedback loop types and their dynamics
- **[Systems Thinking](./systems-thinking.md)** — feedback loops are the structural foundation of systems thinking
- **[Amazon Growth Flywheel](./amazon-growth-flywheel.md)** — a deliberate reinforcing feedback loop designed for compounding growth
- **[WIP Limits](./wip-limits.md)** — WIP limits create a balancing feedback loop that controls queue growth
- **[Westrum Cultural Typologies](./westrum-cultural-typologies.md)** — culture quality determines the accuracy of organisational feedback loops

## Source

- [Systems Thinking Senge Meadows](../sources/systems-thinking-senge-meadows.md)
