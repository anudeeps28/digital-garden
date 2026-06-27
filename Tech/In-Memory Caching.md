---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# In-Memory Caching

## Idea
In-memory caching keeps hot data in the running process so you skip repeat database or LLM calls.

## Definition
In-memory caching stores frequently-read data right in the app's process memory, keyed by a lookup, so the next request hits RAM instead of a slow source. In .NET applications, `IMemoryCache` (injected via [[Dependency Injection]]) can cache expensive reads — such as frequently accessed templates or computed results — so an identical lookup doesn't re-execute a slow database query or computation. Each entry gets a TTL (absolute expiration), and on a miss the code falls back to the real source — a clean case of [[Graceful Degradation]]. Because it lives in-process it's blazing fast but per-instance (not shared across servers) and bounded by memory, which is exactly why a deliberate [[Cache Invalidation]] policy matters.

## Source
Microsoft, introduced in ASP.NET Core (2016) as part of Microsoft.Extensions.Caching.Memory; foundational caching concept in computer science with roots in early memory management systems.

---

## Roots — *where this comes from*
[[DotNet 8]] provides `IMemoryCache` as part of the core framework, making in-memory caching a native pattern in modern C# applications. [[Cache Invalidation]] is the fundamental question that every cache must answer — deciding when cached entries go stale.

## Paths — *where this leads*
TTLs are how cached entries expire and refresh from the source, making [[Cache Invalidation]] a critical design decision. In practice, caching frequently-read data avoids expensive round-trips through data access layers, which directly improves application responsiveness and reduces load on backing services.

## Neighbors — *what lives nearby*
[[Graceful Degradation]] applies naturally to caching — a cache miss degrades elegantly to the slower source rather than failing. [[Keyed Service (DI)]] shares the same lookup-by-key pattern that in-memory caching uses to retrieve values.

## Clash — *what pushes against this*
The [[N+1 Query Problem]] — repeatedly hitting the database — is exactly what caching exists to avoid, making them opposing approaches to the same performance challenge.
