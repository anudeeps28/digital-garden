---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Angular Signals

## Idea
A signal is Angular's reactive primitive — a container holding a value that automatically notifies anyone reading it whenever that value changes.

## Definition
You create a signal with `signal(initialValue)`, read it by calling it like a function (`count()`), and update it with `.set()` or `.update()`. Derived values use `computed()`, and side effects use `effect()`. Because reads are tracked, Angular knows exactly which parts of the UI depend on which signals — so it can refresh only those parts. In practice, signals hold component state (messages, loading flags, selected items), and signal updates trigger [[Zoneless Change Detection]] directly — the update is the signal that tells Angular to re-render, with no Zone.js needed. Signals complement [[RxJS Observable|Observables]]: observables model async streams from HTTP, signals model synchronous current state.

## Source
Angular team (Google), introduced in Angular 16 (May 2023); see [Angular docs on signals](https://angular.io/guide/signals).

---

## Compass

**Neighbors** — *what lives nearby*
Both [[RxJS Observable|Observables]] and signals are reactive primitives that track changes and notify dependents, though signals excel at modeling state while observables handle async streams. [[TypeScript]] pairs naturally with signals since both emphasize strong typing to prevent errors.

**Clash** — *what pushes against this*
Plain mutable component fields change silently with nothing tracking what depends on them — the opposite of signals' transparent dependency graph.

**Roots** — *where this comes from*
[[Zoneless Change Detection]] represents the modern reactive direction that signals enable, where change detection is triggered directly by state updates rather than by async event batching.

**Paths** — *where this leads*
Signals unlock [[Zoneless Change Detection]] for efficient, targeted UI updates and embody the modern reactive style that defines contemporary [[Angular]].
