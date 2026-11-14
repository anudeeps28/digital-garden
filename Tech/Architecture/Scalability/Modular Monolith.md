---
type: atomic
tags: [tech/architecture, tech/backend, tech/scalability]
date: 2026-11-14
---

# Modular Monolith

## Idea
Keep one deployable program with clean internal boundaries, and split it into services only when a specific pressure demands it, because clean boundaries make a later split easy, while splitting does not create clean boundaries.

## Definition
A backend usually goes through three stages.

1. **Monolith with server-side rendering:** page code calls data code in-process, with no network hop. This is right for one team and one front end.
2. **Modular monolith with an HTTP API:** a second client appears, such as a phone app that can only reach data through endpoints. You add a versioned API that reuses the *same service layer* the pages use. It is still one program and one deployment.
3. **Separate backend service:** the API becomes its own program and the website becomes just another client. Splitting further gives you microservices.

Move to stage 3 only for a concrete reason:

- several front ends already go through the API anyway
- separate teams need to release independently
- load is uneven, so you need many copies of the backend but not the front end
- each side needs a different language or tooling
- you are selling access to the API itself

Splitting before any of these apply is a known mistake: the team ends up spending its time on plumbing between services. A stage-3 benefit worth copying earlier: if the website must go through the API, the API can never fall behind the website. In stage 2 you get the same guarantee by sharing one service layer and putting contract tests on every endpoint.

## Source
Captured from a working session on taking a small-team web app to native mobile (November 2026).

The lineage: Martin Fowler's "MonolithFirst" (June 2015) argued that almost every successful microservices system started as a monolith that was later broken up. DHH defended the same position in "The Majestic Monolith" (2016). Shopify's Kirsten Westeinde described turning a large Rails monolith into a *modular* one with enforced component boundaries ("Deconstructing the Monolith", February 2019); the enforcement tool later became Packwerk. GitHub ran on a single large Rails app for years with the same approach.

---

## Compass

**Roots** — *where this comes from*
It is [[Separation of Concerns]] and [[Ports and Adapters]] enforced inside one process instead of across a network. The boundaries do the work; deployment is a separate decision. The trade-offs it weighs come from [[Scalability-and-Load-Parameters]].

**Paths** — *where this leads*
The stage-2 API habits are a written contract in [[Swagger and OpenAPI]], versioned [[REST API]] endpoints, a [[Bearer Token]] per device, and a [[Shared Contract Package]] so clients can't drift. When stage 3 does arrive, [[Stateless Services]] behind a [[Layer 7 Load Balancer]] is the usual next step.

**Neighbors** — *what lives nearby*
It sits beside [[Clean Architecture]], which draws the same inner boundaries, and [[Count the Copies of Each Screen]], which is the front-end counterpart of the same small-team budgeting.

**Clash** — *what pushes against this*
Boundaries inside a monolith are only enforced by discipline or tooling, and without them they erode into a big ball of mud that no one can split later. Organisations also tend to mirror their systems (Conway's law), so a company with many independent teams may need services earlier than the technical pressures alone would suggest.
