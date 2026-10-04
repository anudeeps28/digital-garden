---
type: atomic
tags: [coding/testing, coding/architecture, coding/quality]
date: 2026-10-04
---

# Fitness Functions

## Idea
Turn an architectural rule into an automated test, so the build fails the moment the codebase drifts away from the design.

## Definition
An **architectural fitness function** is any objective, automated check that measures whether the system still has a property you care about. Unlike a unit test, which checks behaviour, a fitness function usually checks **structure or qualities**: the domain layer must not import the database package; no component may hard-code a colour outside the token file; every API route must have an auth guard; bundle size stays under a limit; response time stays under a threshold. Many are just tests that **read the source code** (or the dependency graph) and fail with a clear message when a rule is broken. The motivation is that a written contract decays: a rule in a README is followed until a deadline, then quietly ignored, and nobody notices for months. A failing check makes the rule self-enforcing and keeps the reason next to it. Keep them few, fast and focused on rules that actually matter, and include the "why" in the failure message.

## Tools
- **ArchUnit** (Java), **NetArchTest** (.NET), **dependency-cruiser** (JS/TS), **import-linter** (Python) for dependency rules.
- Plain test files that grep or parse the source work for everything else.

## Source
Borrowed from evolutionary computing by Neal Ford, Rebecca Parsons and Patrick Kua in "Building Evolutionary Architectures" (O'Reilly, 2017; second edition 2022 with Pramod Sadalage).

---

## Compass

**Roots** — *where this comes from*
It is the cure for [[Documentation Drift]]: a rule that lives in a test cannot silently go stale. [[Clean Architecture]] and [[Ports and Adapters]] supply many of the rules worth enforcing.

**Paths** — *where this leads*
It is the strongest form of [[Codify Lessons Into Defaults]], and it runs in the [[CI-CD Pipeline]] alongside a [[Code Coverage Gate]].

**Neighbors** — *what lives nearby*
[[Design Tokens]] rules and [[Architecture Decision Records (ADR)]] are typical sources of checks, and [[Mutation Testing]] is another test that tests the code base rather than a feature.

**Clash** — *what pushes against this*
Too many rigid checks make the architecture hard to change on purpose, and checks that are noisy get disabled. Some qualities (readability, good naming) resist being measured at all.
