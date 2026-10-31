---
type: atomic
tags: [coding/cloud, performance, coding/distributed-systems]
date: 2026-10-31
---

# Cold Start

## Idea
When a platform has scaled your code down to nothing, the first request has to wait while it finds a machine, loads your code and starts the runtime. That wait is the price of not paying for idle time.

## Definition
A cold start is the extra latency on a request that arrives when no warm instance of your code exists. The platform must allocate compute, pull the package or [[Docker Image|image]], start the runtime (the JVM, the .NET CLR, Python), run your startup code (dependency injection, config loading, opening connections), and only then handle the request. A **warm start** reuses an instance that is already running and skips all of that. Cold starts range from tens of milliseconds for lightweight runtimes to several seconds for big images or heavy frameworks. Ways to shrink them: keep the package small, do less at startup, use a runtime that starts fast (Go, Native AOT, or snapshot features like AWS Lambda SnapStart), or keep a minimum number of instances warm, either through provisioned concurrency or a "min replicas = 1" setting.

## Source
The term spread with AWS Lambda (2014) and serverless computing; it is now a standard concern for every [[Scale-to-Zero]] platform.

---

## Compass

**Roots** — *where this comes from*
It is the direct trade-off of [[Scale-to-Zero]]: no idle bill means no idle instance ready to answer.

**Paths** — *where this leads*
It is the main reason [[Serverless Functions]] and [[Serverless Containers]] get a "min instances" setting. Startup time shows up in tail latency, so watch it with [[Percentile-Based-Performance-Metrics|p99 latency]], not averages.

**Neighbors** — *what lives nearby*
A [[Health Probe]] decides when a freshly started instance may take traffic. A [[Thundering Herd]] is what happens when a burst of requests forces many cold starts at once.

**Clash** — *what pushes against this*
Keeping instances warm removes the delay but also removes the zero-cost benefit, which pushes steady-traffic apps back toward always-on [[Managed Web Hosting (PaaS)]] or containers.
