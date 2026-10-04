---
type: atomic
tags: [coding/architecture, coding/distributed-systems, coding/patterns]
date: 2026-10-04
---

# Backpressure

## Idea
When work arrives faster than you can do it, push back on the producer instead of letting an unbounded pile build up. A bounded system that says "not now" stays alive; an unbounded one eventually falls over.

## Definition
**Backpressure** is any mechanism by which a slow consumer limits a fast producer. Without it, excess work goes into a queue, memory or thread pool that grows until latency explodes or the process runs out of resources. The basic tools are simple. A **concurrency cap**, such as a semaphore, allows at most N tasks in flight and makes the rest wait. A **bounded queue** holds at most M waiting items. When both are full, you **reject** new work with a clear error (or tell the caller to retry later) rather than accepting it and failing slowly. An agent runner that spawns worker processes might cap concurrent spawns with a semaphore and refuse new jobs once its queue is full. Sometimes the right cap is one. Running five `git fetch` commands at once in the same repository caused lock contention that broke a run; serialising worktree creation behind a single lock fixed it, at almost no cost in total time. The point is that the limit is chosen deliberately by the system, not discovered by it during an outage.

## Source
The term is borrowed from fluid dynamics (resistance against flow in a pipe). In software it is as old as TCP flow control (the receive window, RFC 793, 1981), and it was formalised for asynchronous libraries by the Reactive Streams initiative (2013, engineers from Netflix, Pivotal, Lightbend, Twitter and others), which made non-blocking backpressure part of its specification, later adopted as Java 9's `Flow` API.

---

## Compass

**Roots** — *where this comes from*
It comes from the questions in [[Scalability-and-Load-Parameters]]: once you know the load your system can actually handle, backpressure is how you enforce that number.

**Paths** — *where this leads*
Rejected work should be retried politely, which is the job of [[Exponential Backoff]], and shedding low-priority load under pressure is a form of [[Graceful Degradation]].

**Neighbors** — *what lives nearby*
[[Rate Limiting]] is backpressure applied per client over time, and a [[Thundering Herd]] is the burst that backpressure has to absorb. Separate pools per workload also shrink the [[Blast Radius]].

**Clash** — *what pushes against this*
Rejecting work feels like failure, so teams quietly raise limits until they are effectively unbounded again. And for some producers, such as sensor data or live video, pushing back isn't possible, so you must drop or sample instead.
