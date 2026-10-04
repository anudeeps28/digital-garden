---
type: atomic
tags: [frontend, web, coding/patterns]
date: 2026-10-04
---

# Optimistic UI

## Idea
Show the result of an action immediately, assuming the server will agree, and quietly roll it back if it does not.

## Definition
In an optimistic UI the client applies a change locally the instant the user acts (the task ticks off, the like count goes up) and sends the request in the background. If the server confirms, nothing visible happens; if it fails, the UI **reverts** and tells the user. The goal is feedback in under about 100 ms, the threshold where an action feels instant. It works best for actions that almost always succeed and are cheap to undo. The companion discipline is **honesty about freshness**: a live app should say whether what you see is *Live*, *Stale* or *Reconnecting* rather than pretending. Loading states follow the same logic. Use **skeletons** (grey placeholders in the shape of the content) when content is loading, and reserve spinners for short local actions; a spinner where content should be starts to read as "broken" after about two seconds. Never be optimistic about things that are expensive to undo, like payments or sends, where a clear pending state is kinder.

## Source
Popularised as "latency compensation" by the Meteor framework (2012), which later called it optimistic UI; written up widely after Denys Mishunov's "True Lies of Optimistic User Interfaces" (Smashing Magazine, 2016). The response-time thresholds trace to Robert B. Miller (1968) and Jakob Nielsen (1993). Games have long done the same thing as client-side prediction.

---

## Compass

**Roots** — *where this comes from*
It is the client-side answer to network latency, and it only works cleanly when there is [[Server-Authoritative State]] to reconcile against afterwards.

**Paths** — *where this leads*
Reverting cleanly is much easier with the [[Reducer Pattern]], where a failed action can simply be replayed out, and retried requests must be safe through [[Idempotency]].

**Neighbors** — *what lives nearby*
[[Graceful Degradation]] shares the instinct of staying useful when the backend is slow, and [[Service Worker]] caches let an offline [[Progressive Web App]] keep behaving optimistically.

**Clash** — *what pushes against this*
Optimism is a lie told on credit: if failures are common, users see things appear and vanish, which is worse than waiting. Silently dropping a failed change is a [[Silent Failure]].
