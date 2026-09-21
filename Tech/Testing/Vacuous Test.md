---
type: atomic
tags: [coding/testing, coding/quality, coding/patterns]
date: 2026-09-16
---

# Vacuous Test

## Idea
A test that passes over the exact mistake it was written to catch is worse than no test, because it spends your confidence without earning it.

## Definition
A vacuous test is one whose assertions cannot fail for the reason the test exists. The commonest form asserts *presence* rather than *correctness* — checking that a configuration property is set, that a rule exists, that a collection is non-empty — when the bug being guarded against is the property having the wrong value. A second form tests a conditional by exercising only one branch, so the other branch can be arbitrarily broken and the suite stays green. A third asserts on a mock's behaviour rather than the system's. The tell is structural: if you can't name a specific code change that would turn this test red, it isn't testing anything. The direct fix is to split each conditional and assert *both* branches explicitly, then confirm the result with [[Mutation Testing]] — deliberately break the code and require the test to notice.

## Source
Related to the "assertion-free test" and "happy path only" anti-patterns catalogued in the xUnit Test Patterns literature (Gerard Meszaros, 2007); the mutation-testing check is the standard empirical remedy.

---

## Compass

**Roots** — *where this comes from*
It arises from measuring test quality by [[Code Coverage Gate|coverage]], which counts lines executed and says nothing about lines *verified*.

**Paths** — *where this leads*
The only reliable detector is [[Mutation Testing]]; the design fix is one assertion per branch, in the [[Arrange-Act-Assert]] shape.

**Neighbors** — *what lives nearby*
[[Consensus Is Not Evidence]] is the same failure in a human setting — agreement mistaken for verification.

**Clash** — *what pushes against this*
Presence assertions are cheap, stable, and never flaky. Rigorous assertions are brittle by nature — they break when behaviour legitimately changes, which is both their cost and the entire point.
