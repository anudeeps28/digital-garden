---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# Exponential Backoff

## Idea
Exponential backoff retries a failed call while waiting longer each time, so you don't hammer a struggling service.

## Definition
Exponential backoff is a retry strategy where the wait between attempts grows multiplicatively — 1s, 2s, 4s, 8s — usually with a little random jitter to avoid synchronized retry storms. In the AI document ingestion project I lean on it for **transient** Azure failures: a brief [[Azure SQL]] timeout, an [[Azure Blob Storage]] hiccup, or an OpenAI call that returns [[HTTP Status Codes|429]]. When the response carries a `Retry-After`, I honor that value instead of my own delay. The point is to distinguish transient faults (worth retrying) from permanent ones (don't bother), and to give the downstream room to recover. It's the client-side counterpart to the server-side [[Rate Limiting]] that produced the 429 in the first place.

## Source
AI document ingestion project

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
