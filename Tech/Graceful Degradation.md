---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# Graceful Degradation

## Idea
Graceful degradation keeps the useful parts of a request working when a non-critical dependency fails, instead of failing the whole thing.

## Definition
Graceful degradation means a request still returns something useful even when an optional dependency is down. For example, if an [[In-Memory Caching|in-memory cache]] is empty, the system falls back to a slower persistent store; if a secondary enrichment call fails, the core response is returned without the extra metadata rather than erroring entirely. The principle is to separate *critical* dependencies (those without which the request cannot proceed) from *non-critical* ones (nice-to-have enhancements), and only hard-fail on the former. It pairs with [[Exponential Backoff]] (retry the transient stuff first) and the [[Result Pattern]] (model the degraded outcome explicitly), turning a brittle all-or-nothing flow into a resilient one.

## Source
Industry standard resilience pattern; foundational to distributed systems design and API resilience. Popularized through the "Resilient Web Design" movement by Jeremy Keith and expanded in practice through microservices and cloud-native architectures (Netflix, AWS documentation, 2010s onward).

---

## Neighbors — *what lives nearby*
Both [[Exponential Backoff]] and graceful degradation are resilience patterns for unreliable dependencies — the former retries the transient failures while the latter keeps serving when retries exhaust. The [[Result Pattern]] captures degradation expressively by modeling partial success as a handleable value rather than a thrown exception.

## Clash — *what pushes against this*
[[Fail Fast Fail Loudly]] takes the opposite stance: abort the whole request immediately when something goes wrong, making failures visible rather than silent. [[Rate Limiting]] also stands in contrast because it deliberately refuses requests to protect the system, whereas degradation deliberately keeps serving even when capacity is constrained.

## Roots — *where this comes from*
This pattern emerges from the broader question of how a [[REST API]] should behave when a downstream dependency becomes partially unavailable — do you fail the whole request or degrade gracefully?

## Paths — *where this leads*
Graceful degradation unlocks resilient caching: cache misses degrade to slower reads from a persistent store rather than hard failures. It also demands [[Structured Logging]] so degraded paths are visible in metrics — you need to see when and how often the system is falling back, otherwise silent degradation becomes a blind spot.
