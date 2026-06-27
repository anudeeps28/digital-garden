---
type: atomic
tags: [coding/csharp, coding/dotnet]
date: 2026-06-26
---

# Cache Invalidation

## Idea
Cache invalidation is the hard problem of deciding when cached data has gone stale and must be thrown away.

## Definition
Cache invalidation answers the question every cache must face: when is this entry no longer trustworthy? In practice, **time-based absolute expiration** is a simple approach — each cached entry carries a TTL, and once it lapses the next read misses and refetches from the source. One way to avoid complexity is to skip manual eviction tied to writes when the data changes infrequently; instead, a short TTL bounds staleness to an acceptable window without the bug-prone bookkeeping of "remember to evict on every update." The trade-off is explicit: a longer TTL means fewer round-trips but a longer window where a consumer might see slightly old data. It's famously one of the two hard things in computer science.

## Source
Phil Karlton, attributed quote in systems design communities circa 1990s; foundational concept in caching theory formalized across distributed systems and database literature. Often cited alongside Donald Knuth's work on algorithm design and optimization. The problem became formalized in modern cache coherence protocols (e.g., MESI, MOESI) and HTTP cache specifications (RFC 7234, 2014).

---

## Neighbors — *what lives nearby*
[[In-Memory Caching]] is the policy half of caching where invalidation lives, and [[Rate Limiting]] shares similar reasoning in terms of time windows.

## Clash — *what pushes against this*
[[Fail Fast Fail Loudly]] insists on correctness now, whereas invalidation tolerates briefly-stale data on purpose.

## Roots — *where this comes from*
Invalidation only matters once you have a [[In-Memory Caching|cache]] in the first place. The deeper question is when a longer TTL's staleness becomes an acceptable trade for fewer DB/LLM calls.

## Paths — *where this leads*
[[Graceful Degradation]] occurs when an expired entry simply degrades to a fresh source read, and good caching plus smart invalidation reduces the [[N+1 Query Problem|pressure of repeat queries]].
