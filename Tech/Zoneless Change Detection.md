---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Zoneless Change Detection

## Idea
Zoneless change detection is an Angular 19 mode that drops Zone.js and instead refreshes the UI only when signals or explicit events tell it something changed.

## Definition
Historically Angular relied on Zone.js, which monkey-patches every async API (timers, promises, events) to know "something might have changed, re-check the whole component tree." That's convenient but coarse and costly. Zoneless mode removes Zone.js entirely; Angular only runs change detection when a [[Angular Signals|signal]] it depends on updates, when an event handler fires, or when an async pipe emits. In the AI document ingestion project, the `PlanDocumentRAG.Web` Angular 19 chat UI runs zoneless (`provideZonelessChangeDetection()`), which is why state is held in [[Angular Signals]] and template-driven reactivity rather than mutated fields — the signals are what tell Angular when to redraw the streaming chat answer.

## Source
AI document ingestion project

---

## Roots — *where this comes from*
Zoneless change detection is a performance-oriented mode of [[Angular]], built to replace the coarser Zone.js approach with fine-grained signal-based reactivity.

## Paths — *where this leads*
Adopting [[Angular Signals]] becomes the natural way to manage state in zoneless apps, and [[RxJS Observable|async pipe and observables]] still trigger detection cleanly, making it possible to layer both signal and observable patterns without overhead.

## Neighbors — *what lives nearby*
[[Angular Signals]] are the mechanism that drives updates in zoneless mode, making them essential for any zoneless change detection strategy. Like [[Percentile-Based-Performance-Metrics]], zoneless mode is ultimately about UI responsiveness and performance.

## Clash — *what pushes against this*
Zone.js change detection, the older default approach, re-checks the tree on any async activity, offering convenience at the cost of performance and coarser granularity.
