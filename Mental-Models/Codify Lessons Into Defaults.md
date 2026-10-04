---
type: atomic
tags: [mental-model, workflow, ai/agents, learning]
date: 2026-10-04
---

# Codify Lessons Into Defaults

## Idea
A lesson is only learned once it lives in the system's defaults; a log of lessons should shrink over time, not grow.

## Definition
Most lessons-learned documents become graveyards: long, unread, and full of advice nobody applies. The fix is to treat each lesson as a temporary resident. Keep an **append-only, dated log** that is read at the start of every working session, by you or by an agent. Then, whenever a lesson is turned into code (a check, a template default, a lint rule, a test), mark the entry `CODIFIED: <where it now lives>` and retire it from the active list. The log becomes a queue of things the system hasn't absorbed yet, and its length is a rough measure of how much the system still depends on memory. The pattern has a recognisable shape: the first five or so iterations of any new workflow produce a burst of lessons, then the rate drops sharply as most of them move into defaults, and the active log settles to a short list of genuinely judgement-based notes.

## Source
The habit of capturing lessons after every event comes from the US Army's After Action Review, developed in the 1970s and institutionalised at the National Training Center in the early 1980s. Toyota's practice of building learning into standard work, so the next person cannot repeat the mistake, supplies the "into defaults" half.

---

## Compass

**Roots** — *where this comes from*
It is [[Kaizen]] with a ratchet: small improvements that are made permanent instead of re-learned. A [[Postmortem]] is where many of these lessons are first written down.

**Paths** — *where this leads*
Codified lessons become [[Self-Learning Templates]], hooks, and tests, and the ones that keep recurring are candidates for [[Fitness Functions]] that check them automatically.

**Neighbors** — *what lives nearby*
[[Turn Repeated Work Into a Skill]] codifies procedures the same way this codifies mistakes, and [[Optimize for Future Teammates Reading Your History]] is the same respect for whoever comes next.

**Clash** — *what pushes against this*
Not every lesson is codifiable; some are judgement, and forcing them into rules produces brittle checks. Over-codifying also risks [[Documentation Drift]] in reverse, where defaults outlive the reason they were added.
