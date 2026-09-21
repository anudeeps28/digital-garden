---
type: atomic
tags: [devops, coding/distributed-systems, coding/architecture]
date: 2026-09-16
---

# Health Probe

## Idea
A load balancer that can't tell a healthy backend from a dead one will keep confidently sending traffic to the dead one.

## Definition
A health probe is a periodic request a load balancer, edge service, or orchestrator sends to each backend to decide whether it should still receive traffic. The probe targets a dedicated lightweight endpoint — conventionally `/health` — that returns a success status only if the instance can actually serve. Two distinctions matter. A *liveness* probe asks "is this process wedged and in need of a restart?"; a *readiness* probe asks "can it take traffic right now?" — and a freshly started instance is alive long before it's ready. The other trap is a probe with no configured path: the balancer falls back to probing `/`, which on an API returns 404 and marks every healthy instance unhealthy, or returns 200 from a static page and marks a broken instance healthy. An unconfigured probe is worse than an obvious outage, because it fails quietly.

## Source
Standard in load balancer and orchestrator design; formalized as liveness/readiness/startup probes in Kubernetes, and as health endpoints in ASP.NET Core Health Checks and Spring Boot Actuator.

---

## Compass

**Roots** — *where this comes from*
Probes exist because distributed systems partially fail — the same premise as [[Fault-vs-Failure]].

**Paths** — *where this leads*
A probe result drives removal from an origin group in [[Azure Front Door]], which is what makes [[Graceful Degradation]] automatic rather than manual.

**Neighbors** — *what lives nearby*
[[Structured Logging]] and [[Percentile-Based-Performance-Metrics]] tell you *how* a service is doing; a probe answers the cruder binary question of whether to route to it at all.

**Clash** — *what pushes against this*
A probe that checks too little declares a broken instance healthy; one that checks its whole dependency chain turns a downstream blip into a cascading removal of every instance at once.
