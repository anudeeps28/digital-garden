---
type: atomic
tags: [coding/testing, coding/quality]
date: 2026-09-16
---

# Mutation Testing

## Idea
Coverage tells you the test ran the code. Mutation testing tells you the test would have *noticed* if the code were wrong — which is the thing you actually wanted to know.

## Definition
Mutation testing deliberately introduces small faults into the source — flipping a comparison, inverting a conditional, changing a constant, removing a call — and re-runs the suite against each mutated version. A mutant that makes some test fail is **killed**; one that leaves the suite green **survives**, and every survivor is a precise, located gap in your assertions. The score is killed over total. Done with a tool (Stryker, PIT) it's automated across the whole codebase; done by hand it's just as useful for a single risky change — break the condition you just wrote, confirm a test goes red, put it back. That thirty-second loop is the only direct evidence a test is real rather than a [[Vacuous Test]], and it's the difference between believing your safety net works and knowing it does.

## Source
Proposed by Richard Lipton in 1971 and developed by DeMillo, Lipton, and Sayward (1978); made practical by modern tooling such as PIT (Java) and Stryker (.NET, JavaScript).

---

## Compass

**Roots** — *where this comes from*
It exists because [[Code Coverage Gate|coverage]] measures execution, not verification — a number that rises without the suite getting stronger.

**Paths** — *where this leads*
Surviving mutants map one-to-one onto missing assertions, which is what makes the technique the standard cure for a [[Vacuous Test]].

**Neighbors** — *what lives nearby*
[[Fail Fast Fail Loudly]] is the production-side version: engineer the system so wrongness announces itself. Mutation testing engineers the *test suite* to do the same.

**Clash** — *what pushes against this*
A full run is expensive — the suite executes once per mutant — and equivalent mutants (changes that genuinely don't alter behaviour) generate noise that has to be triaged by hand.
