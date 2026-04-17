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
