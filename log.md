# Log

Append-only chronological record of all wiki operations.

---

## [2026-04-16] setup | Wiki initialised

Wiki scaffolded via git-wiki skill. Empty structure created: pages/, people/, concepts/, sources/, index.md, log.md.

## [2026-04-16] ingest | Almanack of Naval Ravikant

Source: https://www.navalmanack.com/almanack-of-naval-ravikant/table-of-contents

Fetched 15 chapters from navalmanack.com. Created:
- sources/naval-almanack.md (raw source, 48k chars)
- people/naval-ravikant.md (comprehensive person page)
- concepts/specific-knowledge.md
- concepts/leverage.md
- concepts/happiness.md
- concepts/rational-buddhism.md
- concepts/compounding.md
- index.md (updated with all new entries)

Key themes: wealth creation, specific knowledge, permissionless leverage (code/media), happiness as a subtractive practice, rational Buddhism, compounding across domains.

## [2026-04-16] ingest | Antifragile — Nassim Nicholas Taleb

Sources:
- https://fs.blog/antifragile-a-definition/
- https://fourminutebooks.com/antifragile-summary/
- https://sive.rs/book/Antifragile (Derek Sivers' notes — direct Taleb quotes)

Created:
- sources/antifragile.md (raw source, 15k chars)
- people/nassim-taleb.md (person page with Incerto series overview)
- concepts/antifragility.md (core concept; fragile/robust/antifragile distinction)
- concepts/barbell-strategy.md (bimodal risk approach)
- concepts/black-swan.md (rare high-impact events; Turkey problem)
- concepts/lindy-effect.md (survival as signal of future longevity)
- concepts/skin-in-the-game.md (accountability + via negativa)
- index.md updated with all new entries

Cross-references added: Taleb ↔ Naval Ravikant on accountability, compounding, leverage. Skin in the Game ↔ Naval's accountability framework. Lindy Effect ↔ compounding. Barbell Strategy ↔ permissionless leverage asymmetry.

## [2026-04-16] ingest | Principles: Life & Work — Ray Dalio

Sources:
- https://www.principles.com/principles/
- https://fourminutebooks.com/principles-summary/
- https://sive.rs/book/Principles (Derek Sivers — direct quotes)
- https://www.nateliason.com/notes/principles-ray-dalio

Created:
- sources/dalio-principles.md (raw source, 20k chars)
- people/ray-dalio.md (person page; Bridgewater, 5-step process, contrast with Naval + Taleb)
- concepts/radical-transparency.md
- concepts/idea-meritocracy.md
- concepts/five-step-process.md
- concepts/mental-models.md (cross-source: Naval + Dalio + Taleb models catalogued)
- index.md updated

Cross-references added: Dalio ↔ Naval ↔ Taleb three-way contrast on failure, knowledge, uncertainty, accountability. Mental Models page synthesises all three. Idea Meritocracy ↔ Specific Knowledge. Five-Step Process ↔ Compounding. Radical Transparency ↔ Skin in the Game.

## [2026-04-16] ingest | Principles of Product Development Flow — Donald G. Reinertsen

Sources:
- https://blackswanfarming.com/cost-of-delay/ (Black Swan Farming)
- https://blackswanfarming.com/cost-of-delay-divided-by-duration/ (CD3/WSJF)
- https://en.wikipedia.org/wiki/Cost_of_delay
- https://en.wikipedia.org/wiki/Little%27s_law
- https://en.wikipedia.org/wiki/Kanban_(development)
- https://martinfowler.com/articles/products-over-projects.html
- https://www.goodreads.com/book/show/6278270 (book description + reviews)

Created:
- sources/reinertsen-flow.md (raw source, 37k chars)
- people/donald-reinertsen.md (person page; 8 domains; 4-way contrast table)
- concepts/cost-of-delay.md (CoD, CD3/WSJF, urgency profiles)
- concepts/queues-in-product-development.md (utilisation trap, queue costs)
- concepts/littles-law.md (L = λW; implications for WIP and cycle time)
- concepts/wip-limits.md (mechanism, setting limits, forced prioritisation)
- concepts/batch-size.md (economics of small batches; transaction vs holding cost)
- concepts/flow-economics.md (synthesis: economic frame across all 8 domains)
- index.md updated

Cross-references: Flow Economics ↔ Antifragility (reserve capacity = slack against Black Swans). Batch Size ↔ Barbell Strategy. Cost of Delay ↔ Compounding. WIP Limits ↔ Antifragility. Little's Law ↔ Compounding. Decentralised Control ↔ Skin in the Game. Flow Economics ↔ Leverage.

## [2026-04-16] ingest | Amazon Leadership Principles & Growth Flywheel

Sources:
- https://www.aboutamazon.com/about-us/leadership-principles (official)
- https://www.amazon.jobs/content/en/our-workplace/leadership-principles (official)
- https://en.wikipedia.org/wiki/Amazon_(company)
- https://fourweekmba.com/amazon-flywheel/

Created:
- sources/amazon-lp-flywheel.md (raw source, 20k chars)
- people/jeff-bezos.md (person page; Day 1, Type 1/2 decisions, Working Backwards, 5-way contrast table)
- concepts/amazon-leadership-principles.md (all 16 principles; underlying patterns; cross-references)
- concepts/amazon-growth-flywheel.md (flywheel loop, AWS fuel, Prime anchor, strategic implications)
- index.md updated

Cross-references: LP Ownership ↔ Skin in the Game. LP Customer Obsession ↔ Cost of Delay. LP Disagree & Commit ↔ Idea Meritocracy + Radical Transparency. Flywheel ↔ Compounding. Flywheel ↔ Leverage (AWS). Type 1/2 decisions ↔ Batch Size. Working Backwards ↔ Flow Economics.

## [2026-04-16] ingest | Economics in One Lesson — Henry Hazlitt

Sources:
- https://en.wikipedia.org/wiki/Economics_in_One_Lesson
- https://en.wikipedia.org/wiki/Parable_of_the_broken_window
- https://en.wikipedia.org/wiki/Fr%C3%A9d%C3%A9ric_Bastiat
- https://mises.org/library/book/economics-one-lesson
- https://fee.org/people/henry-hazlitt/
- https://www.goodreads.com/book/show/3028.Economics_in_One_Lesson

Created:
- sources/hazlitt-economics-one-lesson.md (raw, 22k chars)
- people/henry-hazlitt.md (person page; the one lesson; 24 fallacies; contrast table)
- people/frederic-bastiat.md (person page; seen vs unseen; The Law; opportunity cost)
- concepts/seen-vs-unseen.md (master framework; cross-domain applications)
- concepts/broken-window-fallacy.md (the parable; modern applications; cross-refs)
- concepts/unintended-consequences.md (structure; cross-domain parallels)
- index.md updated

Cross-references: Seen/Unseen ↔ Black Swans (Taleb). Seen/Unseen ↔ Hidden Queues (Reinertsen). Broken Window ↔ Naive Intervention (Taleb). Unintended Consequences ↔ Antifragility ↔ Five-Step Process ↔ Type 1/2 decisions (Bezos). Cost of Delay = quantifying the unseen.

## [2026-04-16] ingest | Thinking, Fast and Slow — Daniel Kahneman

Sources:
- https://en.wikipedia.org/wiki/Thinking,_Fast_and_Slow
- https://sive.rs/book/ThinkingFastAndSlow (Derek Sivers — direct quotes)
- https://fourminutebooks.com/thinking-fast-and-slow-summary/
- https://www.goodreads.com/book/show/11468377-thinking-fast-and-slow
- https://en.wikipedia.org/wiki/Prospect_theory
- https://en.wikipedia.org/wiki/Anchoring_effect
- https://en.wikipedia.org/wiki/Availability_heuristic
- https://en.wikipedia.org/wiki/Planning_fallacy

Created:
- sources/kahneman-thinking-fast-slow.md (raw, 33k chars)
- people/daniel-kahneman.md (person page; WYSIATI; experiencing/remembering self; 5-way contrast)
- concepts/system-1-and-2.md (dual-process; when each is reliable; System 2 disciplines)
- concepts/loss-aversion.md (prospect theory; framing; endowment effect; cross-refs)
- concepts/planning-fallacy.md (inside vs outside view; reference class forecasting; pre-mortem)
- concepts/cognitive-biases-kahneman.md (WYSIATI, anchoring, availability, substitution, halo effect, overconfidence, narrative fallacy, regression to mean)
- index.md updated

Cross-references: WYSIATI ↔ Broken Window (Hazlitt). Availability heuristic ↔ Black Swans (Taleb). Planning Fallacy ↔ Cost of Delay + Batch Size (Reinertsen). Loss Aversion ↔ Barbell Strategy (Taleb). Biases ↔ Idea Meritocracy (Dalio). System 1/2 ↔ Principles as System 2 backup (Dalio). Planning Fallacy ↔ Black Swan fat tails (Taleb).

## [2026-04-17] ingest | Competing for the Future — C.K. Prahalad & Gary Hamel

Sources:
- https://en.wikipedia.org/wiki/C._K._Prahalad
- https://en.wikipedia.org/wiki/Core_competency
- https://en.wikipedia.org/wiki/Bottom_of_the_pyramid
- https://en.wikipedia.org/wiki/Gary_Hamel
- https://hbr.org/1994/07/competing-for-the-future

Created:
- sources/prahalad-competing-for-future.md (raw, 20k chars)
- people/ck-prahalad.md (person page; 5 major works; contrast table; Tamil Nadu note)
- concepts/core-competency.md (tree analogy; core vs end products; comparison with specific knowledge)
- concepts/competing-for-the-future.md (present vs future competition; industry foresight; white space; strategic architecture)
- concepts/strategic-intent.md (3 attributes; stretch goal; classic examples)
- concepts/bottom-of-the-pyramid.md (BOP market; poverty penalty; innovation lab; debate)
- index.md updated

Cross-references: Core Competency ↔ Specific Knowledge (Naval). Strategic Intent ↔ Five-Step Process (Dalio). Competing for Future ↔ Day 1 (Bezos) ↔ Antifragility (Taleb) ↔ Cost of Delay (Reinertsen). BOP ↔ Leverage + Batch Size. BOP ↔ Seen vs Unseen (Hazlitt).

## [2026-04-17] ingest | Clayton Christensen — Innovator's Trilogy + How Will You Measure Your Life?

Ingested Clayton Christensen's three core works: *The Innovator's Dilemma* (1997), *The Innovator's Solution* (2003, with Michael Raynor), and *How Will You Measure Your Life?* (2012, with Allworth & Dillon). Source synthesised from Jarvis ingest session.

Files created:
- sources/christensen-innovators-trilogy.md (raw source notes; immutable)
- people/clayton-christensen.md (person page; bio, three works, cross-thinker contrast table, quotes)
- concepts/innovators-dilemma.md (disruptive innovation; sustaining vs disruptive; three failure mechanisms; overshooting trajectory; classic examples)
- concepts/jobs-to-be-done.md (JTBD; McDonald's milkshake study; three dimensions; demographics vs jobs)
- concepts/innovators-solution.md (RPM framework; non-consumption; integration/modularisation; emergent strategy; hiring for experiences)
- concepts/how-will-you-measure-your-life.md (Herzberg two-factor theory; marginal cost trap; 100% integrity rule; JTBD in relationships; school of experience; life metric)
- index.md updated (People section + Disruption & Innovation section + Sources)

Cross-references: Disruptive Innovation ↔ Competing for Future (Prahalad) ↔ Core Competency. RPM ↔ Dalio culture/process. JTBD ↔ non-consumption ↔ Bottom of Pyramid (Prahalad). Marginal cost trap ↔ WYSIATI (Kahneman). 100% integrity ↔ Radical Transparency (Dalio). Day 1 (Bezos) ↔ Disruption Defence.

## [2026-04-17] ingest | Geoffrey Moore — Crossing the Chasm

Ingested Geoffrey Moore's *Crossing the Chasm* (1991/1999/2014), including post-chasm extensions (Tornado, Main Street) from *Inside the Tornado* (1995). Source synthesised from Jarvis ingest session.

Files created:
- sources/moore-crossing-the-chasm.md (raw source; immutable)
- people/geoffrey-moore.md (person page; bio, core contribution, contrast table vs. Christensen/Prahalad/Bezos/Taleb, quotes)
- concepts/crossing-the-chasm.md (full framework: TALC segments, why the chasm exists, D-Day beachhead strategy, Whole Product, Tornado/Main Street, extensive cross-framework analysis section)
- index.md updated (People + Go-to-Market section + Sources)

Cross-references built:
- Christensen (Disruptive Innovation): complementary lenses — Moore = entrant view, Christensen = incumbent view. Same phenomenon, different vantage points.
- Christensen (JTBD): visionary vs. pragmatist as hiring for different jobs; explains why early adopter references fail with pragmatists.
- Christensen (Innovator's Solution): non-consumption targeting = beachhead targeting; RPM = why incumbents can't respond to the entrant crossing.
- Prahalad (Competing for Future / Strategic Intent): strategic intent = macro beachhead; competing for future = post-tornado expansion playbook.
- Prahalad (BOP): non-consumers at BOP as a canonical chasm beachhead (under-served, accessible, adjacent).
- Reinertsen (WIP Limits / Cost of Delay): beachhead discipline = WIP limit applied to GTM; spreading thin across segments = unlimited WIP = delayed flow everywhere.
- Taleb (Black Swan): the chasm as structurally predictable but cognitively invisible; WYSIATI and availability heuristic explain why founders miss it.
- Kahneman (Cognitive Biases): WYSIATI — early traction constructs a complete story that excludes the chasm.
- Bezos (Amazon Flywheel): books as canonical beachhead; flywheel as the mechanism of post-beachhead expansion.

## [2026-04-17] lint | Index restructure — fix orphaned concepts under Sources

The Amazon/Bezos, Economics, Psychology, and Strategy concept groups had drifted under the Sources section heading during previous ingests. Moved all concept groups to the Concepts section. Sources section now contains only raw source file links. No page content changed; index.md only.

## [2026-04-17] ingest | Mihaly Csikszentmihalyi — Flow: The Psychology of Optimal Experience

Ingested Csikszentmihalyi's *Flow* (1990). Source synthesised from Jarvis ingest session.

Files created:
- sources/csikszentmihalyi-flow.md (raw source; immutable)
- people/mihaly-csikszentmihalyi.md (person page; bio, core contribution, contrast table vs. Kahneman/Naval/Christensen/Reinertsen, quotes)
- concepts/flow-optimal-experience.md (full framework: 8 characteristics, challenge/skill matrix, pleasure vs. enjoyment, psychic entropy/negentropy, autotelic experience, work paradox, conditions for flow, cross-framework connections)
- index.md updated (People + Philosophy & Happiness section + Sources)

Cross-references built:
- Kahneman (Experiencing vs. Remembering Self): the Work Paradox explained — remembering self biases toward anticipated leisure over experienced engagement; flow lives in the experiencing self.
- Naval (Specific Knowledge): autotelic skill-building = the path to specific knowledge; flow is the phenomenology of that engagement.
- Christensen / HWYMYL (Herzberg): Herzberg's motivators/hygiene = organisational encoding of autotelic/exotelic distinction. Same structure, different vocabulary.
- Reinertsen (Flow Economics): system-level flow and psychological flow share the same enabling conditions — clear goals, immediate feedback, challenge/skill match, reduced interruption. Reinertsen WIP limits prevent the anxiety zone; Csikszentmihalyi challenge/skill balance prevents boredom and anxiety. They reinforce each other.
- Naval (Happiness): eudaimonic engagement vs. subtractive contentment — complementary paths to the same goal.
- Rational Buddhism: meditation and flow as parallel attention-ordering practices (external challenge vs. internal practice).
- Note: "Flow Economics" (Reinertsen) and "Flow (Optimal Experience)" (Csikszentmihalyi) now both exist in the wiki and are explicitly cross-linked to clarify the distinction and the convergence.

## [2026-04-17] ingest | Robert Cialdini — Influence: The Psychology of Persuasion

Ingested Cialdini's *Influence* (1984, expanded 2021 with Unity). Source synthesised from Jarvis ingest session.

Files created:
- sources/cialdini-influence.md (raw source; immutable)
- people/robert-cialdini.md (person page; bio, seven principles summary table, contrast vs. Kahneman/Taleb/Dalio/Christensen, quotes)
- concepts/principles-of-influence.md (full framework: all seven principles with mechanism/examples/defence; unified structure table; ethical use section; cross-framework connections)
- index.md updated (People + Psychology & Cognitive Biases section + Sources)

Cross-references built:
- Kahneman (System 1/2 + Cognitive Biases): Cialdini's principles are the exploitation manual for System 1. Mapped each principle to its Kahneman mechanism — Social Proof=WYSIATI/availability, Authority=halo effect, Scarcity=loss aversion, Commitment=anchoring+consistency, Liking=affect heuristic.
- Taleb (Skin in the Game): structural antidote to authority/social proof abuse. If an authority bears consequences of advice, the signal is informative. If not, it's noise.
- Dalio (Radical Transparency + Idea Meritocracy): institutional design that neutralises authority bias, liking bias, and commitment bias — Bridgewater as a Cialdini-defence architecture.
- Christensen (100% integrity / marginal cost trap): Commitment & Consistency mechanically explains why 98% commitment collapses. Each exception is consistent with the prior exception; self-image updates toward "someone who makes exceptions."
- Moore (Crossing the Chasm): Social Proof is the psychological engine of pragmatist herd behaviour. Moore's beachhead strategy is deliberate social proof construction.

## [2026-04-17] ingest | Cialdini — Individual concept pages for all 7 principles

The original Cialdini ingest created only a single umbrella page (principles-of-influence.md). This pass creates individual concept pages for each of the seven principles, matching the pattern of Kahneman's individual concept pages.

Files created:
- concepts/reciprocity.md
- concepts/commitment-and-consistency.md
- concepts/social-proof.md
- concepts/authority-bias.md
- concepts/liking.md
- concepts/scarcity.md
- concepts/unity.md

index.md updated: Psychology & Cognitive Biases section now lists all 7 individual principle pages plus the umbrella principles-of-influence.md.

Each page contains: mechanism, techniques/examples, defence, and targeted cross-references to existing wiki pages.

## [2026-04-17] ingest | Cal Newport — Deep Work: Rules for Focused Success in a Distracted World

Ingested Newport's *Deep Work* (2016). Source synthesised from Jarvis ingest session.

Files created:
- sources/newport-deep-work.md (raw source; immutable)
- people/cal-newport.md (person page; bio, core contribution, contrast table vs. Csikszentmihalyi/Naval/Reinertsen/Kahneman, quotes)
- concepts/deep-work.md (full framework: three arguments, four philosophies, four rules, busyness proxy, cross-framework connections)
- concepts/shallow-work.md (counterpart concept: definition, structural causes, busyness trap, management strategies, cross-refs)
- index.md updated (People + new Productivity & Focus section + Sources)

Cross-references built:
- Csikszentmihalyi (Flow): Deep work is flow applied as career strategy. Newport's four rules engineer Csikszentmihalyi's conditions. Deep Work = practical operationalisation of flow theory for professional context.
- Naval (Specific Knowledge): "career capital" = specific knowledge. Deep work is the mechanism that accumulates it. Both argue: genuine depth compounds into irreplaceable capability.
- Reinertsen (WIP Limits / Flow Economics / Cost of Delay): Individual-level and system-level frameworks converge. Context-switching = interrupt queues. Fixed-schedule productivity = WIP limit applied to the day. Shallow work opportunity cost = Cost of Delay.
- Kahneman (Substitution heuristic): Busyness as proxy for productivity = substitution heuristic applied to work self-assessment. Shallow work is visible; deep work value is unseen until it produces output.
- Cialdini (Commitment & Consistency): Newport's rituals and scoreboards leverage commitment devices to make deep work the default behaviour.
- Hazlitt/Bastiat (Seen vs Unseen): Shallow work is the seen output; deep work value is the unseen opportunity cost. Same failure mode as the broken window fallacy in organisations.
- Csikszentmihalyi (Psychic Entropy): Shallow work maintains low-grade distraction that prevents both deep focus and genuine rest — it is psychic entropy, not productivity.

## [2026-04-17] lint | Broken links, orphaned sources, index drift

Ran full lint pass. Issues found and fixed:

Broken relative links (5 fixed):
- people/ck-prahalad.md: three links used ./foo.md (people-relative) instead of ../concepts/foo.md — fixed specific-knowledge, cost-of-delay, leverage
- people/daniel-kahneman.md: one link used ./specific-knowledge.md instead of ../concepts/specific-knowledge.md — fixed
- concepts/radical-transparency.md: referenced ./radical-truth.md which does not exist — replaced with inline reference to ray-dalio.md (radical truth is covered there; no standalone page exists)

Sources on disk not in index (4 added):
- sources/amazon-lp-flywheel.md (ingested 2026-04-16; missing from index)
- sources/kahneman-thinking-fast-slow.md (ingested 2026-04-16; missing from index)
- sources/hazlitt-economics-one-lesson.md (ingested 2026-04-16; missing from index)
- sources/prahalad-competing-for-future.md (ingested 2026-04-16; missing from index)

Post-lint state: 0 broken links, 0 orphaned sources, people 14/14, concepts 49/49 fully in sync.

## [2026-04-17] lint | Cross-reference audit batch 1 (A–M concepts)

Updated cross-references in: amazon-growth-flywheel, antifragility, barbell-strategy, black-swan, bottom-of-the-pyramid, broken-window-fallacy, cognitive-biases-kahneman, competing-for-the-future, compounding, cost-of-delay, deep-work, five-step-process, flow-economics, flow-optimal-experience, happiness, how-will-you-measure-your-life, idea-meritocracy, innovators-dilemma, innovators-solution.

Added 29 links, fixed 0 path issues.

Key connections added:
- amazon-growth-flywheel → crossing-the-chasm (books beachhead)
- antifragility related pages already complete (barbell-strategy, black-swan, skin-in-the-game, lindy-effect all present)
- barbell-strategy → loss-aversion, skin-in-the-game
- black-swan → cognitive-biases-kahneman, crossing-the-chasm, social-proof
- bottom-of-the-pyramid → crossing-the-chasm
- broken-window-fallacy → cognitive-biases-kahneman
- cognitive-biases-kahneman → principles-of-influence, social-proof, authority-bias, scarcity
- competing-for-the-future → crossing-the-chasm, innovators-dilemma
- compounding → lindy-effect, deep-work, amazon-growth-flywheel, flow-economics
- cost-of-delay → shallow-work, seen-vs-unseen
- deep-work → seen-vs-unseen
- five-step-process → strategic-intent
- flow-economics → flow-optimal-experience, deep-work
- flow-optimal-experience → deep-work, shallow-work
- happiness → flow-optimal-experience, how-will-you-measure-your-life
- how-will-you-measure-your-life → flow-optimal-experience, commitment-and-consistency
- idea-meritocracy → social-proof, authority-bias
- innovators-dilemma → crossing-the-chasm
- innovators-solution → crossing-the-chasm

Post-audit state: 0 broken links.

## [2026-04-17] lint | Cross-reference audit batch 2 (J–Z concepts)
Updated cross-references in: jobs-to-be-done, leverage, liking, lindy-effect, loss-aversion, mental-models, planning-fallacy, principles-of-influence, queues-in-product-development, radical-transparency, rational-buddhism, scarcity, seen-vs-unseen, skin-in-the-game, social-proof, specific-knowledge, system-1-and-2, wip-limits. Added 29 links, fixed 7 broken path issues (../concepts/ → ./ in principles-of-influence body; wrong ../people/ link for commitment-and-consistency).

## [2026-04-17] ingest | John Doerr — Measure What Matters (OKRs)

Ingested Doerr's *Measure What Matters* (2018), covering OKRs as developed by Andy Grove at Intel and popularised by Doerr at Google. Source synthesised from Jarvis ingest session.

Files created:
- sources/doerr-measure-what-matters.md (raw source; immutable)
- people/john-doerr.md (person page; bio, Grove origin, contrast table vs. Dalio/Reinertsen/Newport/Christensen, key convergences)
- concepts/okrs.md (full framework: Objectives, Key Results, four superpowers, CFRs, OKRs vs KPIs, failure modes, cross-framework connections)
- index.md updated (People + new Goals & Execution section + Sources)

Cross-references built:
- Dalio (Five-Step Process): parallel personal operating system; Step 1=Objective, KRs=Step 4 plan, review cadence=Step 2/3.
- Reinertsen (Cost of Delay / WIP Limits / Flow Economics): CoD = cost of misaligned/untracked OKRs; WIP limits = operational expression of OKR focus.
- Newport (Deep Work / 4DX): 4DX is individual-level OKRs — same four-discipline structure at personal scale.
- Christensen (Emergent vs Deliberate Strategy): OKR cycle design should match strategy maturity — more aspirational/short-cycle when exploring, more committed/quarterly when executing.
- Cialdini (Commitment & Consistency): public OKRs are commitment devices — transparency increases accountability through social commitment pressure.
- Prahalad (Strategic Intent): strategic intent = long-horizon company Objective; OKRs are the quarterly execution cadence beneath it.

## [2026-04-17] ingest | Systems Thinking — Peter Senge & Donella Meadows

Ingested Peter Senge's *The Fifth Discipline* (1990) and Donella Meadows' *Thinking in Systems* (2008). Source synthesised from Jarvis ingest session.

Files created:
- sources/systems-thinking-senge-meadows.md (raw source; immutable)
- people/peter-senge.md (person page; five disciplines, seven learning disabilities, contrast table)
- people/donella-meadows.md (person page; stocks/flows, leverage points, contrast table)
- concepts/systems-thinking.md (full framework: stocks/flows, two loop types, delays, leverage points, archetypes, cross-framework connections)
- concepts/feedback-loops.md (reinforcing vs balancing loops, delays, oscillation, loop dominance)
- concepts/system-archetypes.md (six archetypes: limits to growth, shifting the burden, tragedy of the commons, escalation, success to the successful, eroding goals)
- concepts/leverage-points.md (Meadows' 12-level hierarchy from numbers to paradigm transcendence)
- concepts/learning-organisation.md (Senge's five disciplines, seven learning disabilities, dialogue vs discussion)
- index.md updated (2 new People, new Systems Thinking section with 5 concepts, Sources)

Cross-references built:
- Reinertsen (Flow/WIP/Queues): Reinertsen's product flow is applied systems dynamics. WIP=stock, throughput=flow, utilisation trap=reinforcing loop. Little's Law = stock-flow relationship in queues.
- Taleb (Black Swan/Antifragility): Black Swan = collapse of a silently accumulating reinforcing loop. Antifragility = design response to system complexity. Barbell = response to delay+reinforcing loop dynamics.
- Kahneman (Cognitive Biases): Learning disabilities map to cognitive biases. WYSIATI = mental models resisting update. Planning fallacy = failure to model feedback loops and delays.
- Christensen (Innovators Dilemma): The Dilemma is the "Success to the Successful" archetype. RPM = leverage point analysis (values = Level 2 paradigm; processes = Level 5 rules).
- Dalio (Radical Transparency): Addresses learning disability #7 (myth of management team) = Level 6 leverage point (information flow structure).
- Cialdini (Social Proof/Commitment): These are reinforcing feedback loops in human social systems. Escalation archetype = reciprocity + commitment in a reinforcing loop without balancing constraint.
- Amazon Flywheel: Explicitly a reinforcing loop. Cross-linked to feedback-loops.md and system-archetypes.md (Success to the Successful).
- Newport/Deep Work: Personal mastery requires deep work. Tragedy of the Commons archetype = shared attention pool degraded by open offices and constant interruption.
- OKRs (Doerr): OKRs are Level 5/3 leverage (rules + goals). Review cadence = balancing loop to correct trajectory.
- Seen vs Unseen (Hazlitt): Making unseen costs visible = Level 6 leverage point (information flow structure).

## [2026-04-17] ingest | Ron Westrum — Cultural Typologies (Pathological / Bureaucratic / Generative)

Ingested Westrum's cultural typology framework (BMJ 2004) and related empirical work from Accelerate (Forsgren, Humble, Kim 2018) and psychological safety (Edmondson 1999 / Google Project Aristotle). Source synthesised from Jarvis ingest session.

Files created:
- sources/westrum-cultural-typologies.md (raw source; immutable)
- people/ron-westrum.md (person page; bio, core contribution, contrast table, cross-thinker convergences)
- concepts/westrum-cultural-typologies.md (full framework: three types, comparison table, Accelerate empirical validation, blameless post-mortems, psychological safety, cross-framework connections)
- concepts/psychological-safety.md (Edmondson, Google Project Aristotle, safety vs comfort distinction, cross-references)
- index.md updated (People + new Organisational Culture section + Sources)

Cross-references built:
- Dalio (Radical Transparency): RT is the operational implementation of Westrum generative culture. "Don't shoot the messenger" enforced as norm.
- Meadows (Leverage Points): Westrum typology = leverage point analysis. Pathological = wrong paradigm (Level 2). Generative = Level 6 (information flow) + Level 3 (mission goal).
- Senge (Learning Organisation): Generative culture = learning organisation. Westrum's 6 generative behaviours directly counter Senge's 7 learning disabilities.
- Reinertsen (Flow/Queues): Generative culture enables fast, honest feedback loops that flow economics requires. Pathological culture systematically corrupts the feedback signals Reinertsen's framework depends on.
- Cialdini (Authority/Social Proof): Authority bias suppresses information in pathological cultures. Social proof amplifies pathology (pluralistic silence). In generative cultures, social proof amplifies psychological safety.
- OKRs (Doerr): Moonshot OKRs only function in psychologically safe environments. Sandbagging = bureaucratic culture behaviour.
- Newport (Deep Work): Psychological safety is prerequisite for deep collaborative work; self-monitoring in unsafe environments consumes attentional bandwidth.
