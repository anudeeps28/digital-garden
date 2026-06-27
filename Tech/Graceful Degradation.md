---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# Graceful Degradation

## Idea
Graceful degradation keeps the useful parts of a request working when a non-critical dependency fails, instead of failing the whole thing.

## Definition
Graceful degradation means a request still returns something useful even when an optional dependency is down. In the AI document ingestion project, if the [[In-Memory Caching|in-memory cache]] of templates is empty I just fall back to the database; if a secondary enrichment LLM call fails I return the core RAG answer without the extra metadata rather than 500-ing the user. The principle is to separate *critical* dependencies (the primary [[Azure SQL]] read — without it there's no answer) from *non-critical* ones (a nice-to-have lookup), and only hard-fail on the former. It pairs with [[Exponential Backoff]] (retry the transient stuff first) and the [[Result Pattern]] (model the degraded outcome explicitly), turning a brittle all-or-nothing flow into a resilient one.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
Both [[Exponential Backoff]] and graceful degradation are resilience patterns for unreliable dependencies — the former retries the transient failures while the latter keeps serving when retries exhaust. The [[Result Pattern]] captures degradation expressively by modeling partial success as a handleable value rather than a thrown exception.

## Clash — *what pushes against this*
[[Fail Fast Fail Loudly]] takes the opposite stance: abort the whole request immediately when something goes wrong, making failures visible rather than silent. [[Rate Limiting]] also stands in contrast because it deliberately refuses requests to protect the system, whereas degradation deliberately keeps serving even when capacity is constrained.

## Roots — *where this comes from*
This pattern emerges from the broader question of how a [[REST API]] should behave when a downstream dependency becomes partially unavailable — do you fail the whole request or degrade gracefully?

## Paths — *where this leads*
Graceful degradation unlocks resilient caching: an [[In-Memory Caching|in-memory cache]] miss degrades to a slower database read rather than a failure. It also demands [[Structured Logging]] so degraded paths are visible in metrics — you need to see when and how often you're falling back, otherwise silent degradation becomes a blind spot.
