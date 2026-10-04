---
type: atomic
tags: [coding/architecture, coding/distributed-systems, devops]
date: 2026-10-04
---

# Thundering Herd

## Idea
When many clients wake up and hit the same resource at the same instant, the spike can knock it over even though average load is low. Spreading the timing out is often the whole fix.

## Definition
A **thundering herd** is synchronised demand. The original case was in the Unix kernel: many processes blocked on `accept()` were all woken for one incoming connection, only one could win, and the rest burned CPU going back to sleep. The modern versions are everywhere. Humans schedule jobs at round times, so the whole internet's cron jobs fire at `:00`. A nightly job set for exactly 21:00 kept failing with CDN errors, because it arrived in the same second as everyone else's; moving it to an odd minute fixed it. Retries cause herds too: if a service blips and every client retries after exactly one second, they all come back together. A **cache stampede** is the data-layer flavour: a hot cache key expires and hundreds of requests miss at once and all hit the database to rebuild it. Remedies are about de-synchronising: add **jitter** (random delay) to schedules and retries, pick odd minutes, let only one request rebuild a cache entry while others wait or serve stale data, and stagger expiry times.

## Source
The term comes from Unix kernel and network-server work in the 1980s and 1990s, documented in W. Richard Stevens' *Unix Network Programming*. The cache version is treated in "Scaling Memcache at Facebook" (Nishtala et al., NSDI 2013), which used **leases** to stop herds on hot keys.

---

## Compass

**Roots** — *where this comes from*
[[Cron]] makes it easy to pick round times, and that is exactly how many independent schedulers end up synchronised without anyone intending it.

**Paths** — *where this leads*
The standard fix for retries is [[Exponential Backoff]] with jitter, and on the server side [[Rate Limiting]] turns a herd into an orderly queue rather than an outage.

**Neighbors** — *what lives nearby*
A stampede is a [[Cache Invalidation]] problem in disguise, since the moment of invalidation is the moment of the herd. [[Backpressure]] is the general mechanism for a resource to say "slow down" to a crowd.

**Clash** — *what pushes against this*
Jitter trades predictability for safety, so "the report lands at 9:00 sharp" becomes "somewhere around 9:07". [[Scalability-and-Load-Parameters]] reminds you that sometimes the honest answer is that peak load is the real requirement and you must provision for it.
