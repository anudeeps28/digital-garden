---
type: atomic
tags: [mental-model, productivity, workflow, decision-making]
date: 2026-09-16
---

# Record the Reason, Not Just the Blocker

## Idea
"Not done" is indistinguishable from "forgotten" three weeks later. "Not done because it needs a permission I don't have" is a thing that comes back on its own.

## Definition
When work stops short of finished, the item itself carries almost no information — a list of incomplete things looks identical whether each one was deliberately deferred or simply dropped. What makes deferral legitimate rather than negligent is recording *why*, specifically enough that the reason can be checked later: a permission only someone else holds, a cost decision that isn't yours to make, a dependency that doesn't exist yet, a rehearsal you can't run against a system that isn't deployed. A reason of that shape has an implicit trigger built into it — when the permission is granted, when the budget is decided, when the dependency ships — so the item resurfaces by itself instead of relying on someone remembering. It also converts an uncomfortable conversation about incomplete work into a factual one, because the alternative to a recorded reason isn't fewer blockers, it's the same blockers with no explanation attached.

## Source
A convergence of engineering practice: the rationale field in architecture decision records, the "known limitations" discipline in release notes, and blocker-with-cause tracking in Kanban systems.

---

## Compass

**Roots** — *where this comes from*
It follows from [[The Dichotomy of Control]] — separating what you could have done from what was never yours to do.

**Paths** — *where this leads*
It makes [[Centralized Infrastructure Ownership|cross-team dependencies]] legible as lead time rather than as apparent slowness, and turns a backlog into a set of self-triggering items.

**Neighbors** — *what lives nearby*
[[Optimize for Future Teammates Reading Your History]] is the same instinct applied to commits; [[The Exit Condition]] is the same instinct applied to when to stop.

**Clash** — *what pushes against this*
Written reasons are also written excuses, and a well-documented blocker can become a comfortable place to stop. [[Managing Ambiguity]] argues for pushing further before declaring something blocked.
