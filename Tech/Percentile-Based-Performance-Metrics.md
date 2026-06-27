---
type: atomic
tags: [#coding/distributed-systems, #mental-model]
date: 2026-03-30
---

# Percentile-Based Performance Metrics (TP99, TP95)

## Idea
Response time is a distribution, not a number — percentiles reveal the tail experience that averages hide, and it's the tail that defines SLAs and user pain.

## Definition
Response time varies on every request due to queuing, network jitter, GC pauses, etc. Measuring the *average* hides the worst experiences.

**Percentiles** give a truer picture:
- **TP50 (median)**: 50% of requests are faster than this. The "typical" user experience.
- **TP95**: 95% of requests are faster than this. 5% are slower.
- **TP99**: 99% of requests are faster than this. The slowest 1% — often your heaviest, most valuable users (they have the most data).
- **TP999**: The worst 0.1% — relevant at Amazon/Google scale where millions of users means thousands having terrible experiences.

**Why the tail matters:**
- SLAs (Service Level Agreements) are defined in percentiles: *"p99 response time < 200ms"*
- The 1% slowest users are often your most active customers — they have more data, more history, more to load
- **Tail latency amplification**: if one request fans out to 100 backend calls and waits for all of them, your response time = the slowest of those 100. With 100 calls each having a 1% chance of being slow, you're almost guaranteed to hit one slow call every request

## Source
[[Designing Data-Intensive Applications]] — Martin Kleppmann, Chapter 1

---

## Compass

**Neighbors** — *what lives nearby*
[[Scalability and Load Parameters]] measures the performance side of load, and [[SLA and SLO|SLA and SLOs]] are contractually defined in percentiles, making this metric the actual currency of service agreements.

**Clash** — *what pushes against this*
[[Average Response Time]] is a misleading metric that hides tail latency, obscuring exactly the information percentiles are designed to reveal.

**Roots** — *where this comes from*
This concept belongs to [[Observability and Monitoring]], which tackles the larger question of how you measure and surface percentile data in production, and connects to the deeper challenge of setting the right SLA targets without over- or under-committing.

**Paths** — *where this leads*
Understanding percentiles directly informs [[Fan-out and Tail Latency Amplification]], which explains why distributed calls make tail latency worse, and also guides [[Scalability and Load Parameters|scaling decisions]] by ensuring you're measuring performance correctly in the first place.
