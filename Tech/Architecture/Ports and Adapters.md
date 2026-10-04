---
type: atomic
tags: [coding/architecture, coding/patterns]
date: 2026-10-04
---

# Ports and Adapters

## Idea
The core of an application talks to the outside world only through a few small interfaces it defines itself (ports). Each concrete outside system plugs in through its own translator (an adapter), so the core never knows which one it is using.

## Definition
A **port** is an interface owned by the application, describing what it needs in its own terms: "list open tasks", "mark task done", "save a note". An **adapter** implements that port for one specific technology. The core depends only on the port; adapters depend on both the port and their external system. Swapping or adding a technology means writing a new adapter, with **zero changes to the core**. A tool that pulls work items from issue trackers is a clean example. The core defines a tiny contract, for instance three operations with fixed input and output shapes, and each tracker gets its own small adapter script. Supporting a new tracker is a new file, not a new branch of `if tracker == ...` logic scattered through the codebase. Ports come in two directions: **driving** ports, through which users, tests or schedulers call the app, and **driven** ports, through which the app calls databases, APIs and queues. Tests use the same seam, plugging in a fake adapter in place of the real one.

## Source
Alistair Cockburn, "Hexagonal Architecture" (also called "Ports and Adapters"), first sketched on his wiki in 2005 and published as an article on 4 September 2005. The hexagon shape just gave room to draw several ports; it has no special meaning.

---

## Compass

**Roots** — *where this comes from*
In C# a port is literally one of the [[Interfaces in CSharp]], and [[Dependency Injection]] is how the right adapter gets plugged in at startup.

**Paths** — *where this leads*
It grew into [[Clean Architecture]] and onion architecture, which add more concentric layers around the same inward-pointing rule, and it makes [[Mock Only at the Boundary]] easy because every boundary is already a named interface.

**Neighbors** — *what lives nearby*
The [[Repository Pattern]] is a driven port for persistence, and the [[Strategy Pattern]] is the same plug-in idea at the scale of a single algorithm. [[Functional Core, Imperative Shell]] draws a similar line between logic and I/O.

**Clash** — *what pushes against this*
A port with exactly one adapter forever is just indirection, and the [[Rule of Three]] suggests waiting for a second real implementation before abstracting. Ports also tend to flatten external systems to a lowest common denominator, hiding features that only one of them has.
