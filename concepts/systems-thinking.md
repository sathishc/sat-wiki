---
title: Systems Thinking
tags: [senge, meadows, systems, feedback, complexity, mental-models, organisations, dynamics]
created: 2026-04-17
updated: 2026-04-17
sources: [sources/systems-thinking-senge-meadows.md]
layout: default
parent: Concepts
---

# Systems Thinking

A way of understanding reality that emphasises **relationships, feedback, and emergence** over linear cause-and-effect. Rather than asking "what caused this?" systems thinking asks "what feedback structures are producing this behaviour?"

The core premise: **most problems that resist solution are not caused by isolated events or bad actors — they are produced by the structure of the system itself.** Changing the actors without changing the structure produces the same behaviour.

> "Structure influences behaviour. Different people in the same structure tend to produce qualitatively similar results." — Peter Senge
> "Today's problems come from yesterday's solutions." — Peter Senge

---

## The Three Components of a System

Every system has three fundamental components:

### Stocks
Elements you can see, feel, count, or measure at a given moment. The state variables of the system.
- Water in a bathtub; money in an account; trust in a relationship; population; WIP in a product development pipeline; inventory

Stocks change slowly — they are the memory of a system. They provide inertia and continuity.

### Flows
The rates that change stocks over time. Inflows add to stocks; outflows subtract.
- Births and deaths (population); income and spending (money); building and eroding trust; arrivals and completions (WIP)

You can only change a stock by changing its flows. You cannot instantly change a stock — it accumulates over time.

### Feedback Loops
The mechanism by which a change in a stock affects the flows that change that stock. Feedback loops are what give systems their characteristic behaviour.

See [Feedback Loops](./feedback-loops.md) for full detail.

---

## The Two Fundamental Loop Types

### Reinforcing (Positive) Feedback Loops
A change in a stock amplifies further change in the same direction. These are "virtuous cycles" or "vicious cycles" depending on direction. They produce exponential growth or collapse — they do not self-correct.

- Interest on savings: money → interest → more money
- Network effects: users → value → more users
- [Amazon flywheel](./amazon-growth-flywheel.md): selection → traffic → sellers → lower costs → prices → traffic
- Panic: fear → selling → price drops → more fear
- [Innovator's Dilemma](./innovators-dilemma.md): incumbent serves best customers → best customers get more investment → weaker customers are underserved → disruptors gain foothold

### Balancing (Negative) Feedback Loops
A change in a stock triggers a response that opposes that change. These loops seek a goal or equilibrium. They produce stability, oscillation, and goal-seeking behaviour.

- Thermostat: temperature below target → heat on → temperature rises → heat off
- Inventory: stock too low → order → stock rises → stop ordering
- [WIP limits](./wip-limits.md): WIP too high → new work blocked → WIP falls → work allowed in
- Price mechanism: price rises → demand falls → price falls
- [OKR review cadence](./okrs.md): goal off-track → corrective action → goal approached → action reduces

---

## Delays

Delays in feedback loops are the primary cause of oscillation, overshoot, and collapse in systems.

When the feedback signal is delayed relative to the action that produced it:
- Decision-makers keep acting after the desired effect has already been produced (but hasn't shown up yet)
- The system overshoots the goal
- A corrective response arrives too late and overshoots in the other direction
- The result: oscillation (boom-bust cycles)

**Examples:**
- **Construction lag:** New housing demand rises → builders start construction → 2–3 years later, supply floods a market that may have already cooled
- **Policy delays:** Government stimulus takes 18 months to affect employment; decisions are made with outdated feedback
- **Boiled frog (Senge):** Temperature rises slowly; frog doesn't perceive the threat until it's too late
- **[Cost of Delay](./cost-of-delay.md):** Decisions are made without accounting for the compounding cost of delay between problem recognition and solution delivery

**Managing delays:** Meadows argues that shortening feedback delays is one of the highest-leverage interventions available (Level 9 in her hierarchy). Reinertsen's insistence on short [batch sizes](./batch-size.md) and frequent releases is essentially a delay-reduction strategy.

---

## Leverage Points

Meadows' most influential contribution: a hierarchy of **places to intervene in a system**, ranked from least to most effective:

| Rank | Intervention type | Examples | Effectiveness |
|---|---|---|---|
| 12 | Numbers / parameters | Tax rates, speed limits, subsidy amounts | Least — rarely changes behaviour |
| 11 | Buffer sizes | Reservoir capacity, emergency stockpiles | Low — often physically fixed |
| 10 | Stock-flow structures | Physical layout, infrastructure | Low — expensive to change |
| 9 | Delays | Feedback lag, reporting frequency, release cadence | Medium-high |
| 8 | Balancing loop strength | Strength of regulatory feedback, price elasticity | Medium-high |
| 7 | Reinforcing loop gain | Growth rate of a positive loop | High — slow a runaway loop |
| 6 | Information flow structure | Who gets what data, when, how | Very high |
| 5 | Rules | Laws, incentives, constraints | Very high |
| 4 | Power to change rules | Who governs the system | Very high |
| 3 | System goals | What the system is optimising for | Highest — but very difficult |
| 2 | Paradigm / worldview | The shared assumptions behind the system | Highest — very hard to change |
| 1 | Power to change paradigms | Transcending paradigms entirely | Highest of all |

**The political paradox:** The highest-leverage interventions (goals, paradigms, information flows) are also the most politically and institutionally resisted. Most policy focuses on Level 12 (numbers) because they are the easiest to agree on — even though they rarely change system behaviour.

**Application:**
- [Radical Transparency](./radical-transparency.md) (Dalio) = Level 6: changing information flow structure
- [OKRs](./okrs.md) = Level 5/3: changing rules + clarifying system goals
- [Idea Meritocracy](./idea-meritocracy.md) = Level 4: changing who has power to change rules
- Cultural change = Level 2: changing paradigm

---

## System Archetypes

Recurring system structures that produce recognisable behaviour patterns. See [System Archetypes](./system-archetypes.md) for full detail.

| Archetype | Structure | Classic example |
|---|---|---|
| **Limits to Growth** | Reinforcing loop hits a balancing constraint | Sales growth slows as service quality degrades |
| **Shifting the Burden** | Quick fix relieves symptom; fundamental solution atrophies | Hiring consultants instead of building internal capability |
| **Tragedy of the Commons** | Shared resource; individual rational action degrades it for all | Overfishing, overloaded shared services |
| **Escalation** | Two competing balancing loops: each response triggers a counter-response | Price wars, arms races, ad spend competition |
| **Success to the Successful** | Two competing activities; resources flow to the winner | [Innovator's Dilemma](./innovators-dilemma.md); the rich get richer |
| **Eroding Goals** | When achieving the goal is hard, the goal is lowered instead | Quality standards drift under delivery pressure |

---

## Cross-Framework Connections

### ↔ Reinertsen (Flow / Queues / WIP)
Reinertsen's [product development flow](./flow-economics.md) framework is applied systems dynamics. WIP is a stock; arrivals and completions are flows; the utilisation trap is a reinforcing loop (high utilisation → long queues → slow feedback → worse decisions → more rework → higher WIP). [Little's Law](./littles-law.md) is the mathematical relationship between stocks and flows in a queue system.

### ↔ Taleb (Antifragility / Black Swan)
Taleb's [Black Swan](./black-swan.md) is a system dynamics event: a reinforcing loop accumulating invisibly until a discontinuous collapse. His [antifragility](./antifragility.md) is a design response to system complexity — instead of trying to predict or prevent tail events, build systems that gain from them. His [barbell strategy](./barbell-strategy.md) is a response to delay + reinforcing loop dynamics: hold two extremes, avoid the fragile middle where feedback signals are corrupted.

### ↔ Unintended Consequences / Seen vs Unseen
[Unintended consequences](./unintended-consequences.md) are almost always the result of acting on symptoms (visible, Level 12 interventions) while ignoring feedback structure. The [seen vs. unseen](./seen-vs-unseen.md) framework (Hazlitt/Bastiat) is systems thinking applied to economics: you see the immediate first-order effect; you miss the second and third-order effects that the feedback structure produces.

### ↔ Kahneman (Cognitive Biases)
[System 1](./system-1-and-2.md) is incapable of perceiving feedback structures — it sees events, not loops. WYSIATI builds a story from the visible symptoms without modelling the invisible structure producing them. The [availability heuristic](./cognitive-biases-kahneman.md) makes recent dramatic events salient while gradual structural accumulation goes unnoticed. Systems thinking is a System 2 discipline: slow, deliberate, structural.

### ↔ Christensen (Disruption / RPM)
The [Innovator's Dilemma](./innovators-dilemma.md) is the "Success to the Successful" archetype. The disruptor's reinforcing loop (cheap + good enough → new customers → investment → improvement) runs simultaneously with the incumbent's reinforcing loop (best customers → best investment → best performance for best customers). The incumbent's loop is larger and more profitable — which is exactly why it wins every quarterly resource allocation fight while losing the structural battle.

Christensen's RPM framework is a leverage point analysis: changing **values** (Level 2–3) and **processes** (Level 5) in the disruptive unit is the structural intervention, not just changing the people.

### ↔ Cialdini (Influence Principles)
[Reciprocity](./reciprocity.md), [commitment](./commitment-and-consistency.md), and [social proof](./social-proof.md) are reinforcing feedback loops in human social systems. Cialdini describes the triggers; systems thinking provides the structural framework for why they self-amplify and persist. Escalation (the archetype) is exactly what happens when reciprocity loops run without a balancing constraint.

---

## Connections

- [Peter Senge](../people/peter-senge.md)
- [Donella Meadows](../people/donella-meadows.md)
- [Feedback Loops](./feedback-loops.md)
- [System Archetypes](./system-archetypes.md)
- [Leverage Points](./leverage-points.md)
- [Learning Organisation](./learning-organisation.md)
- [Unintended Consequences](./unintended-consequences.md)
- [Seen vs Unseen](./seen-vs-unseen.md)
- [Flow Economics](./flow-economics.md)
- [Queues in Product Development](./queues-in-product-development.md)
- [Black Swan](./black-swan.md)
- [Antifragility](./antifragility.md)
- [Innovators Dilemma](./innovators-dilemma.md)
- [Amazon Growth Flywheel](./amazon-growth-flywheel.md)
- [OKRs](./okrs.md)
- [Cognitive Biases (Kahneman)](./cognitive-biases-kahneman.md)
- [Mental Models](./mental-models.md)
