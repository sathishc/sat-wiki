---
title: Product Development — Map of Content
tags: [moc, product-development, flow, execution, teams, delivery, devops]
created: 2026-04-17
updated: 2026-04-17
layout: default
parent: Maps of Content
---

# Product Development

A navigational map of the product development and engineering execution content in this wiki. These frameworks answer: *how do you build software products reliably, quickly, and at high quality?*

---

## The Core Problem

Knowledge work — especially software development — is fundamentally different from manufacturing. Variability is high, demand is unpredictable, and the work is largely invisible until something ships or breaks. Most traditional management practices (utilisation targets, annual planning, headcount scaling) are designed for manufacturing contexts and are actively harmful in product development.

[Reinertsen](../people/donald-reinertsen.md) made the economic case. [Westrum](../people/ron-westrum.md) made the cultural case. [Newport](../people/cal-newport.md) made the individual case. They converge: **optimise for flow, not utilisation; for learning, not coverage; for psychological safety, not heroics.**

---

## Framework Map

### Flow Economics (Reinertsen)

The economic foundation. Start here to understand *why* the other practices matter.

| Framework | Core insight |
|---|---|
| [Flow Economics](../concepts/flow-economics.md) | Optimise for economic value of delivery, not resource utilisation |
| [Cost of Delay](../concepts/cost-of-delay.md) | Time is the most important variable; delay has compounding economic cost |
| [Queues in Product Development](../concepts/queues-in-product-development.md) | Queues are the root cause of slow delivery; the utilisation trap |
| [Little's Law](../concepts/littles-law.md) | Cycle Time = WIP ÷ Throughput; the mathematics of flow |
| [WIP Limits](../concepts/wip-limits.md) | Constrain work in progress to control queues and restore flow |
| [Batch Size](../concepts/batch-size.md) | Smaller batches = faster feedback, lower risk, better flow |

### Culture (Westrum)

Culture is not a "soft" concern — it directly drives technical delivery performance (Accelerate).

| Framework | Core insight |
|---|---|
| [Westrum Cultural Typologies](../concepts/westrum-cultural-typologies.md) | Pathological / Bureaucratic / Generative; culture = information processing architecture |
| [Psychological Safety](../concepts/psychological-safety.md) | Teams cannot learn or perform without safety to speak up |

### Individual Focus (Newport)

| Framework | Core insight |
|---|---|
| [Deep Work](../concepts/deep-work.md) | Cognitively demanding work requires distraction-free concentration; four rules |
| [Shallow Work](../concepts/shallow-work.md) | Email, meetings, logistics expand to fill time; drain deliberately |

### Goals & Alignment (Doerr)

| Framework | Core insight |
|---|---|
| [OKRs](../concepts/okrs.md) | Qualitative objective + quantitative key results; focus, alignment, tracking, stretch |

---

## The Utilisation Trap

The most important concept for product managers and engineering leaders:

> **High utilisation → long queues → slow throughput → poor quality → more rework → higher WIP → higher utilisation.**

This is a **reinforcing feedback loop** ([Systems Thinking](../concepts/systems-thinking.md)) that is self-amplifying. Teams running at 100% capacity feel productive; they are actually in a destructive spiral.

The fix is counterintuitive: **deliberately run below full utilisation**. Slack capacity is not waste — it is the buffer that absorbs variability, enables fast response, and prevents queue explosion.

See: [Queues in Product Development](../concepts/queues-in-product-development.md), [WIP Limits](../concepts/wip-limits.md), [Flow Economics](../concepts/flow-economics.md).

---

## The DORA Metrics

The *Accelerate* research (Forsgren, Humble, Kim) identified four metrics that reliably distinguish high-performing from low-performing engineering organisations:

| Metric | What it measures | Elite benchmark |
|---|---|---|
| **Deployment frequency** | How often code ships to production | Multiple times per day |
| **Lead time for changes** | Commit to production | < 1 hour |
| **Change failure rate** | % of changes that cause incidents | 0–15% |
| **Time to restore service** | How fast you recover from incidents | < 1 hour |

These metrics are lead indicators of [Westrum culture](../concepts/westrum-cultural-typologies.md) and lagging indicators of [flow economics](../concepts/flow-economics.md) practices. Improving them requires both:
- Technical practices: CI/CD, test automation, feature flags, small batch size
- Cultural practices: psychological safety, blameless post-mortems, shared ownership

---

## The Blameless Post-Mortem

The single most important cultural practice for a generative engineering team. When something breaks:

1. **Timeline reconstruction** — what happened, in sequence, without blame attribution
2. **System analysis** — what conditions allowed this error to occur?
3. **Action items** — what changes to the *system* will prevent recurrence?
4. **Publication** — share the findings; the whole organisation learns

**Why blameless:** If individuals fear punishment for failures, they hide failures, work around broken systems, and the organisation cannot learn. The system caused the failure; fix the system. (See [System Archetypes — Shifting the Burden](../concepts/system-archetypes.md): blaming individuals is the quick fix that prevents addressing the real structural cause.)

---

## Practical Sequencing

If you're trying to improve product delivery, this is roughly the order that matters:

1. **Measure what matters** — DORA metrics; [Cost of Delay](../concepts/cost-of-delay.md) for priority decisions
2. **Reduce batch size** — smaller stories, shorter sprints, more frequent releases
3. **Implement WIP limits** — stop starting, start finishing; surface the real constraints
4. **Build psychological safety** — blameless post-mortems; make it safe to surface problems
5. **Align on goals** — [OKRs](../concepts/okrs.md) that connect individual work to product and company outcomes
6. **Protect deep work time** — [Deep Work](../concepts/deep-work.md) blocks; reduce meeting load; async-first communication

---

## Cross-Framework Connections

**Systems Thinking:** The utilisation trap is a [reinforcing feedback loop](../concepts/feedback-loops.md). WIP limits are a [balancing loop](../concepts/feedback-loops.md) imposed on the system. Shortening batch size is a [delay reduction](../concepts/leverage-points.md) (Level 9 leverage). Blameless post-mortems change the [information flow structure](../concepts/leverage-points.md) (Level 6).

**Cialdini:** [Commitment & Consistency](../concepts/commitment-and-consistency.md) explains why teams defend broken processes — having committed to "the way we do things", inconsistency is psychologically costly. Changing the practice requires providing cover: a new commitment device (OKRs, a retro, a post-mortem action item) that makes the new behaviour the consistent choice.

**OKRs + Flow:** OKRs tell you *what* matters. [Cost of Delay](../concepts/cost-of-delay.md) tells you *how urgent* each item is. Together they provide the priority signal that flow economics needs to make the right sequencing decisions.

---

## Related Maps

- [Strategy Frameworks](strategy-frameworks.md)
- [Systems Thinking Primer](systems-thinking-primer.md)
- [Mental Models for Decision-Making](decision-making.md)
- [Personal Development Frameworks](personal-development.md)
- [Startup & Founder Playbook](startup-founder-playbook.md)
