---
type: atomic
tags: [coding/testing]
date: 2026-06-26
---

# Jest

## Idea
The JavaScript test runner that guards the Angular front end the way xUnit guards the API.

## Definition
Jest is a JavaScript/TypeScript testing framework that runs component and service specs fast, has assertions and mocking built in, and produces coverage reports. Conceptually it's analogous to [[xUnit]] + [[Moq]]: isolate a unit, fake its dependencies, assert the result — same [[Arrange-Act-Assert]] rhythm, different language. Jest covers logic in isolation; integration and end-to-end testing is handled by tools like [[Playwright]] that exercise the app through a real browser.

## Source
Facebook (now Meta), released as open-source in 2014; maintained as a core JavaScript testing tool and part of the Jest project.

---

## Compass

**Neighbors** — *what lives nearby*
[[xUnit]] plays the same role on the backend .NET side, and [[Unit Tests]] is how the Angular layer writes them.

**Clash** — *what pushes against this*
[[Playwright]] operates at the browser level for end-to-end testing, whereas Jest focuses on isolated unit testing.

**Roots** — *where this comes from*
[[Angular]] is the front end whose code Jest exercises and tests.

**Paths** — *where this leads*
Jest's coverage numbers feed into the [[Code Coverage Gate]], which enforces the pipeline threshold.
