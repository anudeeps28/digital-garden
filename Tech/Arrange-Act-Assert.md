---
type: atomic
tags: [coding/testing]
date: 2026-06-26
---

# Arrange-Act-Assert

## Idea
A clean test reads in three beats: set the stage, do the thing, then check what happened.

## Definition
Arrange-Act-Assert (AAA) is the standard layout for writing clear, readable tests. **Arrange** wires up the inputs and mocks, **Act** invokes the single method under test, and **Assert** verifies the outcome. Keeping those three phases visually separate makes each test state its intent at a glance and quietly enforces one-behaviour-per-test. The same rhythm scales to any test framework—whether [[xUnit]] [[Unit Tests|unit tests]] with [[Moq]] and [[FluentAssertions]], or [[Integration Tests]] that arrange a request, act by sending it, and assert on the response.

## Source
Bill Wake, *Extreme Programming Explored* (2002); popularized as a foundational testing pattern in test-driven development and xUnit frameworks. Also documented in Robert C. Martin's *Clean Code: A Handbook of Agile Software Craftsmanship* (2008).

---

## Compass

**Neighbors** — *what lives nearby*
AAA is the canonical shape of a good [[Unit Tests|unit test]], and like [[Define Contract Before Implementation]], it pushes you to decide the expected behaviour up front before writing the code.

**Clash** — *what pushes against this*
[[Structured Logging]] represents the opposite approach — observing behaviour in production rather than asserting it in a controlled test environment.

**Roots** — *where this comes from*
[[xUnit]] is the framework that these AAA tests are written in, providing the foundation for this testing pattern.

**Paths** — *where this leads*
[[FluentAssertions]] is the tooling that makes the final "Assert" beat readable and expressive in practice.
