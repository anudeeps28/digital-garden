---
type: atomic
tags: [coding/architecture, coding/database, coding/patterns]
date: 2026-10-04
---

# Persist Facts, Derive State

## Idea
Store only what can't be recomputed: identifiers, user choices, things that happened. Compute everything else fresh when you read it, so it can never go stale.

## Definition
A **fact** is something that, once lost, is gone: which item a user picked, when they pressed start, the id of a record in another system. **Derived state** is anything you can work out from facts plus current sources: a status, a count, a "time remaining", whether something is overdue. Storing derived values creates a second copy that must be kept in sync, and it will drift the moment one update path forgets. The rule is to persist the facts and recompute the rest on each read. A tracking app might store only the external ids it is following and the user's own notes, then ask the live source for current status every time it renders, so a status can't be days out of date. A shared countdown timer is a neat case: instead of a server broadcasting "59, 58, 57..." every second, it stores and sends `startedAt` and `durationRemaining` once, and each client computes the countdown locally from its own clock. That is less traffic, no drift between clients, and a reconnecting client is instantly correct. Cache derived values only when recomputing is measurably too slow, and then treat the cache as disposable.

## Source
The idea runs through Martin Fowler's "Event Sourcing" (2005), where current state is derived from a log of events, and Rich Hickey's talk "The Value of Values" (2012) on facts as immutable. The React team's guidance "You Probably Don't Need Derived State" (2018) states the front-end version. The exact phrase used here is a descriptive summary, not a coined name.

---

## Compass

**Roots** — *where this comes from*
It is [[Single Source of Truth]] taken seriously: a stored derived value is a second source that can disagree with the first, and [[A Stale Source Is Confidently Wrong]].

**Paths** — *where this leads*
It removes most [[Cache Invalidation]] problems by not caching in the first place, and it pairs with [[Store UTC, Display Local]], where the fact is a UTC instant and the display is derived per viewer.

**Neighbors** — *what lives nearby*
[[Server-Authoritative State]] uses it to avoid broadcasting every timer tick, and the [[Reducer Pattern]] treats state itself as derived from a sequence of actions.

**Clash** — *what pushes against this*
Recomputing on every read costs latency and load on the live source, and if that source is down you have nothing to show. [[Graceful Degradation]] sometimes justifies keeping a last-known value, clearly labelled as such.
