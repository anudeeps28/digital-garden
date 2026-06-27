---
type: atomic
tags: [coding/testing]
date: 2026-06-26
---

# Jest

## Idea
The JavaScript test runner that guards the Angular front end the way xUnit guards the API.

## Definition
Jest is the JavaScript/TypeScript testing framework I use for the [[Angular]] UI's unit tests in the AI document ingestion project. It runs component and service specs fast, has assertions and mocking built in, and produces a coverage report that feeds the same [[Code Coverage Gate]] as the backend. Conceptually it's the front-end mirror of [[xUnit]] + [[Moq]]: isolate a unit, fake its dependencies, assert the result — same [[Arrange-Act-Assert]] rhythm, different language. Jest covers logic in isolation; the slower [[Playwright]] suite covers the app driven through a real browser.

## Source
AI document ingestion project

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
