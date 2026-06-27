---
type: atomic
tags: [coding/distributed-systems, mental-model, ddia]
date: 2026-03-30
---

# Fault vs Failure

## Idea
A fault is one component deviating from spec; a failure is the entire system stopping — and only one of them is designable against.

## Definition
- **Fault**: A single component behaving unexpectedly — a disk crashes, a process returns bad data, a human misconfigures a setting. Faults are inevitable.
- **Failure**: The entire system stops providing service to users. This is what users actually experience.
- The goal of resilience engineering is to build **fault-tolerant** systems: assume faults *will* happen and prevent them from cascading into full failures.
- We can design fault-tolerant systems. We cannot design failure-proof systems.
- Netflix's **Chaos Monkey** embodies this: it deliberately injects faults in production to verify the system handles them gracefully.

## Source
[[Designing Data-Intensive Applications]] — Martin Kleppmann, Chapter 1

---

## Compass

**Neighbors** — *what lives nearby*
Fault tolerance is what [[Reliability, Scalability, Maintainability]] is built on, and understanding faults is crucial for resilience. In [[Partial Failures in Distributed Systems]], faults become especially tricky because they're partial and non-deterministic — you can't always tell if a component failed or just got slow.

**Clash** — *what pushes against this*
A [[Single Point of Failure]] is a design that allows one fault to become a full failure — the opposite of what fault-tolerant architecture should do.

**Roots** — *where this comes from*
This concept belongs to the broader question of [[Distributed Systems Design]]: how do we build systems that keep working when parts break? The fundamental tension is whether you can ever fully eliminate faults, or whether you can only contain and isolate them.

**Paths** — *where this leads*
Understanding faults drives us toward [[Replication]] — keeping copies of data so one node's fault doesn't cause data loss — and mechanisms like [[Fencing Tokens]] to prevent a faulty node from corrupting shared state. [[Quorum-Based Systems]] take this further, making decisions even when some nodes are faulty.
