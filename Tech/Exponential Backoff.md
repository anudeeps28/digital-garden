---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# Exponential Backoff

## Idea
Exponential backoff retries a failed call while waiting longer each time, so you don't hammer a struggling service.

## Definition
Exponential backoff is a retry strategy where the wait between attempts grows multiplicatively — 1s, 2s, 4s, 8s — usually with a little random jitter to avoid synchronized retry storms. In practice, it handles **transient** failures gracefully: a brief timeout, a temporary service hiccup, or an API call that returns [[HTTP Status Codes|429]]. When the response carries a `Retry-After` header, that value should be honored instead of a computed delay. The key is to distinguish transient faults (worth retrying) from permanent ones (fail immediately), and to give the downstream service room to recover. It's the client-side counterpart to the server-side [[Rate Limiting]] that produces 429 responses in the first place.

## Source
Industry standard, formalized in AWS SDK and RFC 7231 (HTTP protocol semantics). Exponential backoff with jitter is documented as a best practice in distributed systems literature; popularized by Amazon and Google's SRE practices.

---

## Compass

**Neighbors** — *what lives nearby*
Both [[Graceful Degradation]] and exponential backoff are resilience tactics for flaky dependencies. [[Rate Limiting]] connects directly here — backoff is the correct client response to a rate-limit 429.

**Clash** — *what pushes against this*
[[Fail Fast Fail Loudly]] stands as the opposite: fail-fast aborts immediately, while backoff deliberately keeps trying.

**Roots** — *where this comes from*
[[Async Await in CSharp]] is the substrate where backoff waits are implemented with async delays rather than blocking sleeps.

**Paths** — *where this leads*
[[HTTP Status Codes]] determine what backoff reacts to — 429 and 5xx responses — and the code honors `Retry-After` headers. Once retries are exhausted, the [[Result Pattern]] provides a clean way to return failure.
