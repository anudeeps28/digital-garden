---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# TypeScript

## Idea
TypeScript is a strictly-typed superset of JavaScript that compiles down to plain JS — catching whole classes of bugs before the code ever runs.

## Definition
TypeScript adds static types, interfaces, generics, and compile-time checking on top of JavaScript; the browser never runs it directly — a compiler (`tsc`) strips the types and emits JS. Because every valid JS file is also valid TS, you can adopt it incrementally. In the KBA AI-Doc-Ingestion project, the entire `PlanDocumentRAG.Web` Angular 19 UI is TypeScript — typed models for API [[Request and Response]] payloads, a typed `AppConfig` interface for the [[Runtime Config (Build Once Deploy Everywhere)|config.json]] loaded at startup, and typed service classes for MSAL and HTTP. The strong typing here mirrors how the backend uses C# — both sides agree on shapes, so a renamed field surfaces as a compile error instead of a runtime surprise.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[CSharp]] and TypeScript are both statically typed languages that share the same "types catch bugs early" philosophy — the backend's C# and frontend's TS keep each other honest across the boundary. TypeScript also has the same [[Interfaces in CSharp|interface concept]] for describing shapes.

**Clash** — *what pushes against this*
Plain JavaScript offers dynamic typing without a compile-time safety net, trading the upfront effort of annotation for flexibility.

**Roots** — *where this comes from*
[[Angular]] is authored entirely in TypeScript, making it the foundation of the entire framework.

**Paths** — *where this leads*
Strong typing enables [[Angular Signals|Angular Signals]] — reactive values with full type safety — and makes it straightforward to map typed models cleanly onto [[JSON]] wire payloads.
