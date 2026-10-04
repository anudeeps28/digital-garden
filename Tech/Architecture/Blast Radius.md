---
type: atomic
tags: [coding/architecture, coding/distributed-systems, devops]
date: 2026-10-04
---

# Blast Radius

## Idea
Blast radius is how much else breaks when one thing breaks. Good design keeps it small, so a single bad dependency costs one feature, not the whole system.

## Definition
Every component will fail eventually; the design question is what fails *with* it. Coupling hides in mundane places. One example: two independent pipelines were scheduled as a single cron line, `run_a && run_b`. When the first hit an error, the second silently never ran, so a problem in one area stalled an unrelated one. Another: a task that wrote to several destinations stopped entirely when one destination misbehaved, even though the others were fine. The fixes share a principle called **bulkheads**, after the watertight compartments of a ship's hull: give each independent unit its own schedule, its own error handling, its own pool of threads or connections, so a breach floods one compartment. At larger scale the same idea shows up as **cell-based architecture** (split users across identical, isolated stacks), **canary releases** (expose a new version to a small slice first), and per-tenant resource limits. A quick test for any design: list the failures you expect, and for each one ask "who else notices?"

## Source
"Blast radius" is borrowed from explosives and military usage. The software countermeasure, the **Bulkhead** pattern, was introduced by Michael Nygard in *Release It!* (Pragmatic Bookshelf, 2007). AWS's Well-Architected guidance popularised cell-based architecture as a way to limit blast radius.

---

## Compass

**Roots** — *where this comes from*
It starts from the distinction in [[Fault-vs-Failure]]: faults are inevitable, and the goal is to stop a local fault from becoming a system-wide failure.

**Paths** — *where this leads*
Small blast radius is what makes [[Graceful Degradation]] possible, since the healthy parts keep serving while the broken one is switched off. A per-destination [[Write Ledger]] is a bulkhead for data.

**Neighbors** — *what lives nearby*
[[Defence in Depth]] limits how far an attacker gets the way bulkheads limit how far a failure spreads. [[Backpressure]] protects a component from being flooded by its neighbours, and [[Separation of Concerns]] gives you the seams where bulkheads can go.

**Clash** — *what pushes against this*
Isolation costs resources and complexity: separate pools sit idle, separate schedules multiply. For a job where partial output is worse than none, an [[All-or-Nothing Run]] deliberately couples the steps.
