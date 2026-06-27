---
type: atomic
tags: [coding/distributed-systems, mental-model, framework, ddia]
date: 2026-03-30
---

# Maintainability — Operability, Simplicity, Evolvability

## Idea
Most of a system's cost is incurred *after* it's built — maintainability is about designing so the ongoing cost of operating, understanding, and changing the system stays low.

## Definition
Maintainability has three sub-properties:

**Operability** — easy to keep the system healthy day-to-day
- Good monitoring, metrics, logs, distributed tracing
- Health checks and automated alerting
- Easy deployment and rollback (CI/CD pipelines)
- Infrastructure as code (Terraform, Ansible) to avoid configuration drift
- No single-person dependencies — anyone on the team can operate it
- Good documentation and runbooks

**Simplicity** — managing complexity so the system is understandable
- Target is *accidental complexity* — complexity that crept in via workarounds, hacks, tangled dependencies — not inherent complexity of the problem
- Core tool: **abstraction** — clean interfaces that hide messy internals
- Loosely coupled, cohesive modules
- Domain model aligned with the business domain
- Covered further in Ch 4 (Encoding) — clean data interfaces between systems

**Evolvability** — easy to change the system as requirements shift
- **Schema evolution** and backward/forward compatibility — old and new code coexist during rolling deployments (covered deeply in Ch 4)
- Loose coupling between services — microservices and message queues let you change one part without redeploying everything
- Feature flags — ship code dark, enable incrementally
- Agile practices — short feedback loops, iterative delivery, TDD
- Covered further in Ch 4 (Encoding & Evolution), Ch 8 & 9 (distributed system evolution without downtime)

## Source
[[Designing Data-Intensive Applications]] — Martin Kleppmann, Chapter 1

---

## Compass

**Neighbors** — *what lives nearby*
Maintainability is the third pillar alongside [[Reliability, Scalability, Maintainability]], and [[Agile Software Development]] operationalizes evolvability at the process level through iterative delivery and continuous feedback.

**Clash** — *what pushes against this*
Poor maintainability produces [[Accidental Complexity]], while [[Big Bang Releases]] represent the opposite of evolvability—changing everything at once rather than evolving incrementally.

**Roots** — *where this comes from*
This concept emerges from the deeper question of [[Software Design Principles]]—what fundamentally makes a system easy to live with long-term? There's a fundamental tension to resolve: how do you balance simplicity (fewer abstractions) with evolvability (more layers)?

**Paths** — *where this leads*
[[Encoding and Evolution]] provides the data-layer mechanism for achieving evolvability, relying on [[Backward and Forward Compatibility]] to allow old and new versions of code to coexist. At the architectural level, [[Microservices Architecture]] represents a pattern that deliberately trades simplicity for greater evolvability.
