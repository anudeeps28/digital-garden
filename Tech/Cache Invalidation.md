---
type: atomic
tags: [coding/csharp, coding/dotnet]
date: 2026-06-26
---

# Cache Invalidation

## Idea
Cache invalidation is the hard problem of deciding when cached data has gone stale and must be thrown away.

## Definition
Cache invalidation answers the question every cache must face: when is this entry no longer trustworthy? In the AI document ingestion project I keep it simple and use **time-based absolute expiration** — each [[In-Memory Caching|IMemoryCache]] entry (templates, RAG answers) carries a TTL, and once it lapses the next read misses and refetches from [[Azure SQL]] or the LLM. I deliberately avoid manual eviction tied to writes, because the data changes rarely and a short TTL bounds staleness to an acceptable window without the bug-prone bookkeeping of "remember to evict on every update." The trade-off is explicit: a longer TTL means fewer round-trips but a longer window where a user might see slightly old data. It's famously one of the two hard things in computer science.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
[[In-Memory Caching]] is the policy half of caching where invalidation lives, and [[Rate Limiting]] shares similar reasoning in terms of time windows.

## Clash — *what pushes against this*
[[Fail Fast Fail Loudly]] insists on correctness now, whereas invalidation tolerates briefly-stale data on purpose.

## Roots — *where this comes from*
Invalidation only matters once you have a [[In-Memory Caching|cache]] in the first place. The deeper question is when a longer TTL's staleness becomes an acceptable trade for fewer DB/LLM calls.

## Paths — *where this leads*
[[Graceful Degradation]] occurs when an expired entry simply degrades to a fresh source read, and good caching plus smart invalidation reduces the [[N+1 Query Problem|pressure of repeat queries]].
