---
type: atomic
tags: [mental-model, decision-making, coding/git, learning]
date: 2026-09-16
---

# A Stale Source Is Confidently Wrong

## Idea
An out-of-date source doesn't tell you it's out of date. It answers your question fluently, completely, and wrong — and you have no signal that anything happened.

## Definition
The failure mode worth naming is not *missing* information but *stale* information, because the two feel completely different from the inside. Missing information announces itself: you look, find nothing, and know to go elsewhere. Stale information hands you a confident answer with no marker of age attached — a local clone months behind its remote, a document written before the reorganization, a memory of how a system used to work. You then reason correctly from a false premise and arrive somewhere wrong with full conviction, which is worse than not knowing, because certainty stops you checking. The countermeasure is procedural rather than analytical: refresh before you reason. Pull first, check the date, confirm against the live system. Not because you suspect the source, but precisely because you can't.

## Source
A recurring lesson in engineering practice; related to the "confidently incorrect" failure mode discussed in knowledge management and in evaluations of language models, where fluency is uncorrelated with accuracy.

---

## Compass

**Roots** — *where this comes from*
It's a specific case of the problem [[Critical Thinking Skills]] addresses — the premise, not the reasoning, is where the error entered.

**Paths** — *where this leads*
In practice it becomes a habit: `git pull` before reading a dependency's source, verify a registry against live state before trusting it — see [[IP Address Space Registry]] and [[Shared Module Library]].

**Neighbors** — *what lives nearby*
[[Consensus Is Not Evidence]] is the social version: many people repeating something is not a check on whether it's still true.

**Clash** — *what pushes against this*
Verifying everything is paralysis. Most sources are fine most of the time, and the cost of universal suspicion exceeds the cost of occasional staleness — so the judgement is *which* sources move fast enough to matter.
