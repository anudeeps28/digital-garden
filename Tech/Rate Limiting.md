---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# Rate Limiting

## Idea
Rate limiting caps how many requests one user can fire in a time window, protecting the API from abuse and runaway costs.

## Definition
Rate limiting throttles request volume so a single caller can't overwhelm the service or rack up huge costs. In practice, you wire up a rate-limiting [[Middleware]] using a **fixed-window** limiter partitioned per authenticated user — the partition key comes off the user's identity. When a user exceeds their window, the API short-circuits with [[HTTP Status Codes|429 Too Many Requests]] and emits standard rate-limit headers (including `Retry-After`) so clients know when to come back. Because API calls can be expensive and slow, this is as much a cost guardrail as a security one. It pairs naturally with [[Exponential Backoff]] on the client side.

## Source
Foundational concept in API design; formalized in HTTP specifications including RFC 6585 (2011, defining 429 status code) and RFC 7231 (2014, defining `Retry-After` header). Widely implemented in frameworks like ASP.NET Core, Express, and Django.

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
