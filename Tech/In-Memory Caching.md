---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# In-Memory Caching

## Idea
In-memory caching keeps hot data in the running process so you skip repeat database or LLM calls.

## Definition
In-memory caching stores frequently-read data right in the app's process memory, keyed by a lookup, so the next request hits RAM instead of a slow source. In the AI document ingestion project I use `IMemoryCache` (injected via [[Dependency Injection]]) to cache two expensive things: document **templates** read from [[Azure SQL]], and **RAG answers** so an identical question doesn't re-run an LLM call. Each entry gets a TTL (absolute expiration), and on a miss the code falls back to the real source — a clean case of [[Graceful Degradation]]. Because it lives in-process it's blazing fast but per-instance (not shared across servers) and bounded by memory, which is exactly why a deliberate [[Cache Invalidation]] policy matters.

## Source
AI document ingestion project

---

## Roots — *where this comes from*
[[DotNet 8]] provides `IMemoryCache` as part of the core framework, making it a native pattern in modern C# applications. [[Cache Invalidation]] is the fundamental question that every cache must answer — deciding when cached entries go stale.

## Paths — *where this leads*
TTLs are how cached entries expire and refresh from the source, making [[Cache Invalidation]] a critical design decision. Caching template reads avoids expensive round-trips through [[EF Core]] to [[Azure SQL]], which directly improves application responsiveness.

## Neighbors — *what lives nearby*
[[Graceful Degradation]] applies naturally to caching — a cache miss degrades elegantly to the slower source rather than failing. [[Keyed Service (DI)]] shares the same lookup-by-key pattern that in-memory caching uses to retrieve values.

## Clash — *what pushes against this*
The [[N+1 Query Problem]] — repeatedly hitting the database — is exactly what caching exists to avoid, making them opposing approaches to the same performance challenge.
