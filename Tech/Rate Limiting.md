---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# Rate Limiting

## Idea
Rate limiting caps how many requests one user can fire in a time window, protecting the API from abuse and runaway costs.

## Definition
Rate limiting throttles request volume so a single caller can't overwhelm the service or rack up huge LLM bills. In the the project AI Document Ingestion API, I wire up ASP.NET Core's built-in `RateLimiter` [[Middleware]] using a **fixed-window** limiter partitioned per authenticated user — the partition key comes off the user's identity from the [[Bearer Token]]. When a user exceeds their window, the API short-circuits with [[HTTP Status Codes|429 Too Many Requests]] and emits standard rate-limit headers (including `Retry-After`) so clients know when to come back. Because LLM calls are expensive and slow, this is as much a cost guardrail as a security one. It pairs naturally with [[Exponential Backoff]] on the client side.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Both [[Authorization]] and rate limiting decide whether a request is allowed to proceed, and rate limiting runs as a [[Middleware]] in the request pipeline alongside other cross-cutting concerns.

**Clash** — *what pushes against this*
[[Graceful Degradation]] keeps serving when downstream fails; rate limiting deliberately refuses excess load to protect the system.

**Roots** — *where this comes from*
Rate limiting is a cross-cutting concern of a public [[REST API]], and partitioning per user requires knowing who the caller is, which ties back to [[Authentication]].

**Paths** — *where this leads*
Exhausting the limit returns [[HTTP Status Codes|429 Too Many Requests]] with `Retry-After`, and clients should employ [[Exponential Backoff]] when they hit the limit to respect the server's constraints.
