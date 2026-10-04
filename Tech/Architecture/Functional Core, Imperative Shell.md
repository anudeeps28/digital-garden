---
type: atomic
tags: [coding/architecture, coding/patterns, coding/testing]
date: 2026-10-04
---

# Functional Core, Imperative Shell

## Idea
Put all the decisions in pure functions that take values and return values, and wrap them in a thin outer layer that does the messy I/O. The core gets exhaustive tests; the shell stays too simple to need many.

## Definition
The **functional core** holds the logic: rules, calculations, transformations. It has no clock, no disk, no network, no UI; everything it needs comes in as arguments and everything it decides goes out as return values. The **imperative shell** reads the clock, loads data, calls the core, then writes files, updates the screen or sends messages based on what the core returned. Dependencies point inward: the shell knows the core, never the reverse. A small timer app shows the payoff. All the time maths (how many minutes remain in this session, when the next break starts, what happens if the device slept for an hour) lives in one pure module that takes "now" as a parameter. It can be covered by dozens of unit tests that run in milliseconds and include the edge cases you would never reproduce by hand. Around it, separate shells handle the UI, local storage and a home-screen widget, each one just "get inputs, call core, render output". When a bug appears it is almost always in the core, where it is easy to pin with a test.

## Source
Named by Gary Bernhardt in the Destroy All Software screencast "Functional Core, Imperative Shell" (July 2012) and his talk "Boundaries" (SCNA 2012), which argues for using simple values as the boundaries between components.

---

## Compass

**Roots** — *where this comes from*
It is built from [[Pure Functions]] and is a lightweight cousin of [[Clean Architecture]], where the domain sits in the middle and frameworks stay at the edge.

**Paths** — *where this leads*
Most of the code becomes testable with plain [[Unit Tests]] and no mocks, which leaves [[Mock Only at the Boundary]] as the natural rule for the little that remains.

**Neighbors** — *what lives nearby*
[[Ports and Adapters]] draws the same line but focuses on swappable outside systems. The [[Reducer Pattern]] is a functional core for state changes, and [[Separation of Concerns]] is the general principle underneath.

**Clash** — *what pushes against this*
Some logic is inherently interleaved with I/O, like streaming or step-by-step negotiations, and forcing it into "compute then act" can produce awkward code. In I/O-heavy glue scripts there may simply be very little core to extract.
