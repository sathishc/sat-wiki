---
title: "Westrum Cultural Typologies — Ron Westrum (2004, A Typology of Organisational Cultures)"
tags: [sources, westrum, culture, organisations, safety, devops, information-flow, psychological-safety]
---

# Source: Ron Westrum — Cultural Typologies and Organisational Safety

Ingested: 2026-04-17
Source type: Synthesised knowledge ingest (Jarvis session)

Primary sources:
- Ron Westrum, "A typology of organisational cultures" (BMJ Quality & Safety, 2004)
- Ron Westrum, "The study of information flow: A personal journey" (Safety Science, 2014)
- Nicole Forsgren, Jez Humble, Gene Kim, *Accelerate: The Science of Lean Software and DevOps* (2018) — operationalised Westrum's typology for software delivery research
- Gene Kim, *The Phoenix Project* (2013) and *The Unicorn Project* (2019) — fictional exploration of Westrum culture in tech

---

## Background

Ron Westrum is an American sociologist (born 1942) who studied how organisations handle information, particularly in safety-critical environments (aviation, healthcare, nuclear power, spaceflight). His research question: why do some organisations successfully process warning signals and avert disasters, while others fail to act on the same signals until catastrophe occurs?

His answer: it depends on the **culture of the organisation** — specifically, how it treats information, especially inconvenient or threatening information.

---

## The Westrum Typology: Three Organisational Cultures

Westrum identified three archetypal organisational cultures based on how they handle information:

### 1. Pathological (Power-Oriented)

**Core driver:** Power and personal survival.

**Information handling:**
- Messengers are shot (people who bring bad news are punished)
- Responsibilities are shirked (blame is shifted)
- Bridging is discouraged (information does not cross silos)
- Failure is covered up
- New ideas are actively crushed (threats to existing power)

**What this produces:** Information that threatens the powerful is suppressed. Problems fester until they cause catastrophe. Whistleblowers are destroyed. Cover-ups are rational individual choices.

**Examples:** Organisations where the Challenger disaster's warning signals were ignored; Enron; Wells Fargo fake accounts scandal — in all these cases, people *knew* there was a problem but the culture made surfacing it career-destroying.

**Characteristics:**
- Low cooperation
- Messengers shot
- Responsibilities shirked
- Bridging discouraged
- Failure → cover up
- New ideas → crushed

---

### 2. Bureaucratic (Rule-Oriented)

**Core driver:** Rules, procedures, and departmental turf.

**Information handling:**
- Messengers are tolerated (but ignored if inconvenient)
- Responsibilities are narrow (follow the procedure; it's not my problem)
- Bridging is allowed but not rewarded
- Failure → justice (find who violated which rule)
- New ideas → problems (they require changing the procedure)

**What this produces:** The organisation processes information within its established channels, but those channels are slow and siloed. Novel information that doesn't fit the existing procedure gets lost. The organisation is stable but not adaptive.

**Examples:** Large government agencies, legacy enterprises, heavily regulated industries before transformation — not actively hostile to information, but not good at using it.

**Characteristics:**
- Modest cooperation
- Messengers tolerated
- Narrow responsibilities
- Bridging tolerated
- Failure → justice (rule violation found)
- New ideas → problems (disrupt procedure)

---

### 3. Generative (Performance-Oriented)

**Core driver:** Mission and performance.

**Information handling:**
- Messengers are trained (people who surface problems are valued and developed)
- Risks are shared (problems are everyone's problem)
- Bridging is rewarded (information crosses silos actively)
- Failure → inquiry (what happened? what can we learn?)
- New ideas → welcomed (if they serve the mission)

**What this produces:** The organisation processes information effectively. Problems surface early. Near-misses are investigated. Failures produce learning. People speak up because it is safe and valued.

**Examples:** High-reliability organisations (HROs) in aviation and nuclear power that have exceptional safety records; DevOps teams with continuous deployment, blameless post-mortems, and psychological safety.

**Characteristics:**
- High cooperation
- Messengers trained
- Risks are shared
- Bridging rewarded
- Failure → inquiry
- New ideas → welcomed

---

## The Key Insight: Culture as Information Processing Architecture

Westrum's insight is not merely that "good culture is nice to have." It is structural:

**The culture of an organisation is its information processing system.**

In a pathological culture, information that threatens power is systematically suppressed. The organisation is flying blind on the issues that matter most. This is not a personal failing — it is the rational response of individuals to the incentive structure they face.

In a generative culture, information flows freely because the incentives are aligned: surfacing problems is rewarded, not punished. The organisation processes threatening information before it becomes catastrophic.

This maps directly onto [Meadows' Leverage Points](concepts/leverage-points.md) — specifically **Level 6: structure of information flows**. The organisational culture determines who gets what information. Changing the culture changes the information architecture, which changes decisions, which changes outcomes.

---

## Westrum in Software: Accelerate

Nicole Forsgren, Jez Humble, and Gene Kim's *Accelerate* (2018) operationalised Westrum's typology as a survey instrument and measured it against software delivery performance across thousands of organisations.

Their finding: **Westrum organisational culture is one of the strongest predictors of software delivery performance** (deployment frequency, lead time, change failure rate, time to restore) and organisational performance.

Specifically:
- Generative cultures have significantly higher deployment frequency
- Lower change failure rates
- Faster time to restore service after incidents
- Higher employee net promoter scores (people want to work there)

The cultural survey items used in Accelerate measure:
1. Information is actively sought
2. Messengers are not punished when they deliver bad news
3. Responsibilities are shared
4. Cross-functional collaboration is encouraged and rewarded
5. Failure causes inquiry
6. New ideas are welcomed

This gave Westrum's qualitative framework quantitative empirical backing in software — making it one of the most evidence-based frameworks in DevOps and engineering management.

---

## Blameless Post-Mortems

A key practice in generative cultures, popularised by Google's SRE (Site Reliability Engineering) culture and widely adopted in DevOps.

The premise: when a system fails, the first question should be "what happened in the system?" not "who made the mistake?"

**Why blameless matters:**
- If individuals fear punishment for failures, they will hide failures, work around broken systems, and not share what they know
- A blameless culture treats failures as system problems — the system allowed the error to occur; fix the system
- This is consistent with [Senge's](people/peter-senge.md) systems thinking: the structure produces the behaviour; change the structure

**The practice:**
- Detailed timeline reconstruction
- No attribution of blame to individuals
- Focus on systemic conditions that enabled the failure
- Concrete action items to change the system
- Published (transparency) — so the whole organisation learns

---

## Psychological Safety (Amy Edmondson)

Westrum's generative culture is closely related to Amy Edmondson's concept of **psychological safety** (Harvard Business School, 1999) — the belief that one will not be punished or humiliated for speaking up with ideas, questions, concerns, or mistakes.

Google's Project Aristotle (2012–2015) studied what made teams effective. The single strongest predictor of team effectiveness was psychological safety — consistent with Westrum's findings at the organisational level.

Psychological safety is the individual-level experience of what Westrum describes at the organisational level: an environment where information flows freely because speaking up is safe.

---

## Key Quotes

**Westrum:**
> "The culture of an organisation is its information processing system."
> "Organisational accidents are less about the actions of individuals and more about the culture and conditions that enabled those actions."
> "In generative organisations, the focus is on the mission. Everything else — including the egos of leaders — is subordinated to getting the mission done."

**Accelerate:**
> "Our research shows that the Westrum organisational culture measure is a strong predictor of software delivery performance."
> "Culture is not about ping-pong tables and free lunch. It is about how your organisation handles information."
