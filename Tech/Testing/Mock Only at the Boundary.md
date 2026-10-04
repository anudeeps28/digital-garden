---
type: atomic
tags: [coding/testing, coding/patterns, coding/architecture]
date: 2026-10-04
---

# Mock Only at the Boundary

## Idea
Replace only the things at the edge of your system (network, database, filesystem, clock, heavy models) with fakes, and let your own code run for real in tests.

## Definition
A mock stands in for a dependency so a test can run fast and deterministically. The question is *which* dependencies. Mocking at the **boundary** means faking the slow, flaky or external things: HTTP calls to other services, the database (or using a real throwaway one), the filesystem, the system clock, and heavy machine-learning models that take seconds to load. Your **internal classes are not mocked**; the test exercises them together. Mocking internals produces tests that mirror the implementation line by line, so they break on every refactor while still passing when the real behaviour is wrong. Boundary mocks, by contrast, survive refactoring because the boundary rarely changes. A refinement from the mock-objects pioneers: **don't mock types you don't own**. Instead of mocking a third-party SDK directly, wrap it in a thin adapter you own, mock that adapter in unit tests, and cover the adapter itself with a few integration tests against the real service.

## Source
Steve Freeman, Nat Pryce, Tim Mackinnon and Joe Walnes, "Mock Roles, not Objects" (OOPSLA 2004), and Freeman and Pryce's "Growing Object-Oriented Software, Guided by Tests" (2009), which states "only mock types that you own". Echoed by Vladimir Khorikov's "Unit Testing Principles" (2020) on mocking only unmanaged out-of-process dependencies.

---

## Compass

**Roots** — *where this comes from*
It follows from [[Ports and Adapters]]: the ports are exactly the boundary, so adapters are the natural thing to fake. [[Dependency Injection]] is what lets you swap them.

**Paths** — *where this leads*
It pushes logic into a [[Functional Core, Imperative Shell]] where the core needs no mocks at all, and leaves the real wiring to [[Integration Tests]].

**Neighbors** — *what lives nearby*
[[Moq]] and `vi.mock` in [[Vitest]] are the tools, and the [[Repository Pattern]] is the classic seam for faking the database.

**Clash** — *what pushes against this*
The London school of TDD mocks collaborators freely to drive design, and some boundaries (complex databases) are better tested for real than faked, since a fake that disagrees with reality hides bugs.
