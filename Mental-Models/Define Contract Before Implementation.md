---
type: atomic
tags: [mental-model, coding/patterns, architecture]
date: 2026-02-23
---

# Define Contract Before Implementation

## Idea
Decide what something produces — its output shape and guarantees — before writing how it produces it.

## Definition
Before writing a class, method, or system, define the contract: what does it return? What does it accept? What does it promise? The implementation is secondary — the contract is what other things depend on. In C#, this means defining your `record` output types and `interface` signatures before writing the logic. In TDD, it means writing the test (what you expect) before the code. The compiler enforces this: it needs to know a type exists before it can compile code that returns it.

*Analogy: design the box before packing it.*

## Source
C# coding session — defining `DocumentFingerprint` record before `DocumentFingerprintExtractor`, interface-first design

---

## Compass

**Neighbors** — *what lives nearby*
Interface-first design, [[Test-Driven Development]] (write the test/contract first), and API-first design (define the API spec before building) all follow the same principle. [[n8n Orchestrates AI Reasons]] exemplifies this by defining what each layer's responsibility is before building it.

**Clash** — *what pushes against this*
Emergent design takes the opposite approach — write code and figure out the shape as you go. The temptation to defer cleanup ("I'll clean up the interfaces later") pulls against the discipline of contracts-first thinking.

**Roots** — *where this comes from*
This concept connects to [[One Method One Responsibility]] and the broader question of how you design systems that are easy to change.

**Paths** — *where this leads*
Cleaner separation between what a thing does and how it does it; [[Read-Only by Default]] extends this by having contracts define what callers can and cannot do; and easier testing — if the contract is clear, writing tests is straightforward.
