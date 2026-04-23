---
title: Cognitive Biases (Kahneman)
tags: [kahneman, cognitive-bias, heuristics, anchoring, availability, psychology]
created: 2026-04-16
updated: 2026-04-16
sources: [sources/kahneman-thinking-fast-slow.md]
layout: default
parent: Concepts
---

# Cognitive Biases (Kahneman)

A catalogue of systematic errors in judgment identified by [Kahneman](../people/daniel-kahneman.md), Tversky, and colleagues. These are not random mistakes — they are predictable, consistent patterns that arise from [System 1](./system-1-and-2.md)'s architecture.

> "The confidence people have in their beliefs is not a measure of the quality of evidence; it is a measure of the coherence of the story that System 1 has managed to construct."

## WYSIATI — What You See Is All There Is

The most fundamental bias. System 1 builds the most coherent story it can from *available* information — and then acts as if that story is complete. It does not flag what is missing.

**Consequences:**
- Overconfidence: confidence tracks story coherence, not evidence quality
- Jumping to conclusions on limited data
- Ignoring base rates (the specific story crowds out the statistical reference class)
- Confirmation bias: new information is assimilated into the existing story

**Cross-reference:** WYSIATI explains why [Hazlitt](../people/henry-hazlitt.md)'s [Broken Window Fallacy](./broken-window-fallacy.md) persists. The glazier's payment is in the story; the cobbler's forgone sale is not. System 1 builds its narrative from what it sees.

---

## Anchoring

**The bias:** Initial information (an anchor) exerts a disproportionate influence on subsequent estimates, even when the anchor is arbitrary or irrelevant.

**Classic experiment:** Spin a wheel (rigged to stop at 10 or 65). Then ask: what percentage of African countries are in the UN? Groups anchored at 65 guessed ~45%; groups anchored at 10 guessed ~25%.

**Applications:**
- Negotiation: whoever names a number first anchors the discussion
- Salary negotiations: first offer anchors subsequent counter-offers
- Project estimates: the first timeline mentioned dominates
- Court sentencing: prosecutors' initial sentence requests anchor judge decisions

**Cross-reference:** [Amazon LP #12 "Dive Deep"](./amazon-leadership-principles.md) — leaders must be sceptical of the first number they hear. [Dalio](../people/ray-dalio.md)'s back-testing is a mechanism for replacing anchored intuitions with data.

---

## Availability Heuristic

**The bias:** People estimate frequency or probability by how easily examples come to mind. What is memorable or recent is judged as common; what is hard to recall is judged as rare.

**Examples:**
- Plane crashes (rare but memorable) are perceived as more dangerous than car crashes (common but routine)
- Shark attacks vs bee stings: people fear the former, die from the latter
- After vivid news stories about crime, people overestimate local crime rates
- Words with R as first letter vs third letter: most people say first — but third is actually more common

**Consequences for organisations:**
- Recency bias: last quarter's results dominate risk models
- Availability cascades: media coverage of risks inflates perceived probability
- Underestimation of slow, diffuse risks (like [invisible queues](./queues-in-product-development.md))

**Cross-reference:** The availability heuristic explains why [Black Swans](./black-swan.md) (Taleb) are systematically underestimated — by definition, unprecedented events are hard to recall.

---

## Substitution

**The bias:** When confronted with a hard question, System 1 quietly replaces it with an easier related question and answers that instead — without flagging the substitution.

- "How happy are you with your life?" → becomes → "How am I feeling right now?"
- "How dangerous is nuclear power?" → becomes → "How much do I fear nuclear accidents?"
- "What is this company worth?" → becomes → "Do I like this company?"

This explains why people are so confident in answers to questions they didn't actually answer.

---

## Halo Effect

**The bias:** A positive impression in one dimension spills over to other dimensions. If you find someone attractive, you also tend to rate them as more intelligent and trustworthy.

**In organisations:** A team's last success inflates all subsequent evaluations of their work. An articulate presenter is assumed to have better ideas. A charismatic leader is assumed to have better strategy.

**Cross-reference:** [Dalio](../people/ray-dalio.md)'s [idea meritocracy](./idea-meritocracy.md) is explicitly designed to counteract the halo effect — weight ideas by track record on the specific question, not by overall impressiveness.

---

## Overconfidence

**The finding:** People are systematically overconfident in their own knowledge and predictions. When asked questions and then asked "how confident are you?", calibration is poor — people saying 90% confident are right far less than 90% of the time.

**Particularly bad in:**
- Long-range forecasting (political, economic, business)
- Domains with irregular feedback
- Experts who have learned a coherent framework (illusion of understanding)

> "Those with the most knowledge are often less reliable. The reason is that the person who acquires more knowledge develops an enhanced illusion of her skill."

**Cross-reference:** [Taleb](../people/nassim-taleb.md)'s critique of forecasters. [Dalio](../people/ray-dalio.md)'s instruction to "seek disconfirmation." [Amazon LP #4](./amazon-leadership-principles.md): "work to disconfirm their beliefs."

---

## Narrative Fallacy

**The bias:** Humans construct causal stories about sequences of events, even when the events are random. The story feels explanatory and inevitable in hindsight.

**Consequences:**
- Hindsight bias: "I knew it all along"
- Overlearning from anecdotes (one vivid story vs thousands of data points)
- False certainty about the past → false confidence about the future

**Cross-reference:** [Taleb](../people/nassim-taleb.md)'s [Black Swan](./black-swan.md) is partly an attack on the narrative fallacy — the post-hoc story that makes Black Swans seem predictable.

---

## Regression to the Mean

**The insight:** Extreme outcomes are partly luck. The next outcome will regress toward the average. This produces a persistent illusion:
- Praised for exceptional performance → next time is ordinary → "praise doesn't help"
- Punished for terrible performance → next time is better → "punishment works"

The intervention (praise/punishment) gets credit/blame for what was actually statistical regression.

**Cross-reference:** [Reinertsen](../people/donald-reinertsen.md)'s focus on system-level metrics rather than individual performance is partly a defence against regression-to-mean misattribution.

## Related Pages

- [Daniel Kahneman](../people/daniel-kahneman.md)
- [System 1 and System 2](./system-1-and-2.md)
- [Loss Aversion](./loss-aversion.md)
- [Planning Fallacy](./planning-fallacy.md)
- [Seen vs Unseen](./seen-vs-unseen.md)
- [Broken Window Fallacy](./broken-window-fallacy.md)
- [Black Swan](./black-swan.md)
- [Mental Models](./mental-models.md)
- [Idea Meritocracy](./idea-meritocracy.md)
- [Principles of Influence](./principles-of-influence.md) — Cialdini's exploitation of the same biases
- [Social Proof](./social-proof.md) — heuristic rooted in availability and WYSIATI
- [Authority Bias](./authority-bias.md) — halo effect as the mechanism
- [Scarcity](./scarcity.md) — scarcity heuristic driven by availability and loss aversion

## Connections

- **[Daniel Kahneman](../people/daniel-kahneman.md)** — primary researcher behind the documented biases
- **[System 1 and System 2](./system-1-and-2.md)** — the cognitive architecture that produces these biases
- **[Loss Aversion](./loss-aversion.md)** — one of the most consequential individual biases
- **[Planning Fallacy](./planning-fallacy.md)** — inside-view optimism bias in action
- **[Principles of Influence](./principles-of-influence.md)** — Cialdini's exploitation manual for these biases
- **[Seen vs Unseen](./seen-vs-unseen.md)** — WYSIATI explains the persistence of economic fallacies
- **[Mental Models](./mental-models.md)** — good mental models are the System 2 antidote to cognitive biases

## Source

- [Kahneman Thinking Fast Slow](../sources/kahneman-thinking-fast-slow.md)
