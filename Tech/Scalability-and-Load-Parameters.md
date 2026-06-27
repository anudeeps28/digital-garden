---
type: atomic
tags: [#coding/distributed-systems, #mental-model, #ddia]
date: 2026-03-30
---

# Scalability and Load Parameters

## Idea
Scalability is meaningless until you define *what* is growing — load parameters are the specific numbers that describe your system's load, and the right ones differ per system.

## Definition
Scalability is a system's ability to cope with increased load. But "load" is not generic — you must define it precisely using **load parameters** relevant to your system:

- **Requests per second** — volume of API/service calls
- **Read/write ratio** — mostly reading or writing? Drives storage strategy entirely
- **Number of concurrent users** — active simultaneously, not total registered
- **Cache hit rate** — what % served from cache vs hitting the database
- **Fan-out** — for each user action, how many downstream records/services are touched
- **Dataset size** — how large is the data being queried
- **Message queue backlog** — how many unprocessed jobs are waiting

**Twitter's fan-out problem** is the classic example:
- A celebrity with 30M followers posts a tweet
- Option A (write fan-out): push the tweet to all 30M follower timelines immediately — O(followers) writes per tweet
- Option B (read fan-out): merge on read — every timeline load fetches tweets from all followed accounts — O(followed accounts) reads per load
- Twitter uses a **hybrid**: pre-computed timelines for most users, but celebrities' tweets are fetched and merged at read time, because writing to 30M caches per tweet is too expensive

The load parameter that mattered was fan-out ratio, not raw requests/second.

## Source
[[Designing Data-Intensive Applications]] — Martin Kleppmann, Chapter 1

---

## Compass

**Neighbors** — *what lives nearby*
Scalability is one of the three pillars alongside [[Reliability, Scalability, Maintainability]], and [[Partitioning]] is the primary mechanism for scaling write throughput across nodes.

**Clash** — *what pushes against this*
[[Vertical Scaling]] stands opposite to the distributed approach — adding power to a single machine instead of distributing load.

**Roots** — *where this comes from*
[[Distributed Systems Design]] asks the broader question of how you design a system that scales gracefully, and understanding load parameters becomes critical as your product grows and your chosen metrics shift.

**Paths** — *where this leads*
Once load is defined, [[Replication]] enables scaling of read throughput by adding read replicas, while [[Partitioning]] scales by splitting data across nodes, and [[Percentile-Based Performance Metrics]] ensures that performance is measured correctly rather than through misleading averages.
