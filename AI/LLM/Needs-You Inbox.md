---
type: atomic
tags: [ai/agents, frontend, mental-model]
date: 2026-10-04
---

# Needs-You Inbox

## Idea
When you supervise many agents at once, the interface's main job is to show what is waiting on you, not everything that is happening.

## Definition
A dashboard of running agents is tempting: progress bars, logs, token counts. But the human is the bottleneck, and the only question that matters at a glance is "who is blocked on me?". A **needs-you inbox** puts that first. Each session has a state, and the one that matters is "idle, waiting on you": a question, an approval, a proposal or a finished review. Everything else is quiet by default. A worked design: a control panel for parallel coding sessions uses a neutral palette everywhere and reserves its single accent colour for needs-you, so the eye goes straight to the sessions that need a decision. Its guiding phrase was "a control room, not a dashboard": a dashboard reports, a control room exists to prompt action.

## Source
The principle is management by exception, rooted in Frederick Taylor's "exception principle" from early scientific management and systematised by Lester Bittel's *Management by Exception* (1964): managers attend only to items that deviate from the plan.

---

## Compass

**Roots** — *where this comes from*
It is a guard against the [[Mere Urgency Effect]]: busy agent logs feel urgent, but only the blocked sessions are important.

**Paths** — *where this leads*
It is where [[Propose, Don't Execute]] proposals and [[Never Grade Your Own Homework]] escalations land, and it turns waiting work into the "urgent and important" quadrant of [[The Eisenhower Matrix]].

**Neighbors** — *what lives nearby*
[[Rank, Don't Filter]] suggests ordering the inbox by cost of delay rather than hiding items, and [[Slow Productivity]] argues for fewer things in flight at once.

**Clash** — *what pushes against this*
Hiding healthy sessions can hide slow failures too: an agent stuck in a loop is not "waiting on you" but still needs you, so a [[Silent Failure]] check belongs alongside the inbox.
