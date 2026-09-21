---
type: atomic
tags: [coding/database, coding/dotnet, coding/distributed-systems, coding/patterns]
date: 2026-09-16
---

# Connection Resiliency

## Idea
A cloud database will drop your connection for reasons that have nothing to do with you. The question isn't whether it happens, it's whether the application notices.

## Definition
Connection resiliency is the client-side policy that retries transient database failures automatically instead of surfacing them as errors. Managed databases fail over, throttle, and get reconfigured underneath you, producing short-lived errors that succeed on the next attempt. The policy has three knobs worth tuning together: a **retry count** (five is a common ceiling), a **maximum delay** between attempts so [[Exponential Backoff]] doesn't stretch to minutes, and a **command timeout** that bounds any single attempt. The critical constraint is that retries must only fire on error codes known to be transient — retrying a constraint violation or a syntax error just burns time — and any retried operation must be idempotent, because a timeout means "I don't know if it committed", not "it didn't".

## Source
Implemented as execution strategies in [[EF Core]] (`EnableRetryOnFailure`), and as the general Retry pattern in Microsoft's Cloud Design Patterns and libraries such as Polly.

---

## Compass

**Roots** — *where this comes from*
It's the concrete application of [[Exponential Backoff]] to the database connection, driven by the reality behind [[Fault-vs-Failure]].

**Paths** — *where this leads*
Retries only work when operations are safe to repeat, which pushes design toward idempotent commands and away from "read, decide, write" sequences.

**Neighbors** — *what lives nearby*
[[Graceful Degradation]] handles failures you couldn't retry away; [[Rate Limiting]] is the same conversation from the server's side.

**Clash** — *what pushes against this*
Aggressive retries against an already-overloaded database make the overload worse — the retry storm. And silent retries hide a degrading dependency until it fails outright.
