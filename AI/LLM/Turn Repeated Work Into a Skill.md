---
type: atomic
tags: [ai/llm, framework, systems]
date: 2026-10-03
---

# Turn Repeated Work Into a Skill

## Idea
Any piece of work you do repeatedly can be written down once as a reusable unit that gets a little better every time you run it.

## Definition
Most AI use is one-off: you re-explain the task, get a decent result, and throw the scaffolding away. A skill is the opposite — the weekly report, the pull-request review, the meal plan captured as explicit instructions the model loads each time. The first version is mediocre. The gain comes from the edit after each run: a missed edge case added, a bad default removed. Because the unit persists, improvements accumulate instead of evaporating, which makes it one of the few genuinely compounding assets in day-to-day AI use. The work stops being redone and starts being refined.

## Source
Captured from my own reel on AI concepts most people miss (September 2026), describing Projects and Skills as the two features that change AI from a search box into something that knows your situation.

The packaging is recent — Anthropic shipped Skills for Claude in 2025 — but the idea is old and well-evidenced: the standard operating procedure, and Atul Gawande's case in *The Checklist Manifesto* that writing down what experts already know measurably reduces failure. What is new is that the written-down procedure is now executable by the thing reading it.

---

## Compass

**Roots** — *where this comes from*
This is [[Kaizen]] applied to your own tooling — each run is a small improvement your brain can't resist making, and the artifact is what makes the improvement stick. Mechanically it is the general case of [[Self-Learning Templates]], where a system refines its own extraction rules instead of waiting for a human rewrite.

**Paths** — *where this leads*
The compounding is the point, and it behaves like [[The Flywheel Concept]]: the first few runs are all push, after which the thing starts carrying itself. Sustained, it is the tooling expression of [[Consistency Over Intensity]].

**Neighbors** — *what lives nearby*
It shares its architecture with [[Prompt Pieces]] — modular, versioned fragments assembled at runtime rather than one monolithic prompt — and with [[Template-Based Extraction]], where a fixed, reusable shape does the work a fresh instruction would otherwise have to.

**Clash** — *what pushes against this*
Encoding a procedure too early freezes a version you have not finished figuring out, which is why [[First Make It Work, Then Make It Better]] insists on shipping the rough thing before standardising it. There is also a real cost to maintaining skills nobody runs — the pursuit of total coverage is where [[85% Rule]] applies, since a few well-worn skills beat a library of stale ones.
