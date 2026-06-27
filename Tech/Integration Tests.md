---
type: atomic
tags: [coding/testing]
date: 2026-03-24
---

# Integration Tests

## Idea
Integration tests check multiple pieces working together — verifying that components actually connect and communicate correctly.

## Definition
While [[Unit Tests]] verify individual methods in isolation, integration tests verify that components work correctly when combined — that the API controller actually calls the service, which actually talks to the database, which actually returns the right data. Integration tests are slower and more complex (they may need a real database or test server), but they catch problems that unit tests can't — like incorrect [[EF Core]] queries, misconfigured [[Dependency Injection]], or broken [[Middleware]] pipelines. In practice, integration tests might spin up a test server, call an [[API Endpoints|endpoint]], and verify the full request-response cycle.

## Source
Kent Beck, *xUnit Test Patterns: Refactoring Test Code* (2007); foundational concept in test-driven development and continuous integration practices that emerged in the 1990s XP (Extreme Programming) movement.

---

## Neighbors — *what lives nearby*
[[Unit Tests]] provide a narrower scope for testing in isolation, while [[End-to-End Tests]] cast an even broader net by testing the full user journey.

## Clash — *what pushes against this*
[[Unit Tests]] focus on isolated components that are fast and use [[Moq|mocks]], whereas [[Manual Testing]] verifies behavior by hand without automated checks.

## Roots — *where this comes from*
Integration tests are powered by [[xUnit]], the framework that orchestrates these tests, and they naturally arise from [[Clean Architecture]] principles that emphasize verifying how layers connect properly.

## Paths — *where this leads*
Integration tests are essential checkpoints in the [[CI-CD Pipeline]], running before deployment to catch regressions, and they often leverage [[Docker]] containers to spin up isolated test environments with real dependencies.
