---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# TypeScript

## Idea
TypeScript is a strictly-typed superset of JavaScript that compiles down to plain JS — catching whole classes of bugs before the code ever runs.

## Definition
TypeScript adds static types, interfaces, generics, and compile-time checking on top of JavaScript; the browser never runs it directly — a compiler (`tsc`) strips the types and emits JS. Because every valid JS file is also valid TS, you can adopt it incrementally. In practice, typed models for API [[Request and Response]] payloads integrate seamlessly with typed interfaces for configuration objects loaded at startup. The strong typing across frontend and backend codebases means both sides agree on shapes, so a renamed field surfaces as a compile error instead of a runtime surprise.

## Source
Microsoft, led by Anders Hejlsberg; first released in 2012. Official language for Angular (Google, 2016+).

---

## Compass

**Neighbors** — *what lives nearby*
[[CSharp]] and TypeScript are both statically typed languages that share the same "types catch bugs early" philosophy. TypeScript also has the same [[Interfaces in CSharp|interface concept]] for describing shapes, making it natural to mirror backend type definitions on the frontend.

**Clash** — *what pushes against this*
Plain JavaScript offers dynamic typing without a compile-time safety net, trading the upfront effort of annotation for flexibility.

**Roots** — *where this comes from*
[[Angular]] is authored entirely in TypeScript, making it the foundation of the entire framework.

**Paths** — *where this leads*
Strong typing enables [[Angular Signals|Angular Signals]] — reactive values with full type safety — and makes it straightforward to map typed models cleanly onto [[JSON]] wire payloads.
