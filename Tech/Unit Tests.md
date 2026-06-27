---
type: atomic
tags: [coding/testing]
date: 2026-03-24
---

# Unit Tests

## Idea
Unit tests check one small piece of code in isolation — verifying that a single method or class works correctly without depending on external systems.

## Definition
A unit test is a small, fast, automated test that exercises a single unit of code (usually a method) with known inputs and verifies expected outputs. The key word is *isolation* — you don't call real databases, APIs, or file systems. Instead, you use mocking libraries to create fake versions of dependencies. This is possible because of [[Interfaces in CSharp]] and [[Dependency Injection]] — you inject mocks instead of real services. In practice, unit tests verify core business logic without touching external systems like databases or third-party APIs. Tests are typically written with frameworks like [[xUnit]] and follow the Arrange-Act-Assert pattern.

## Source
Foundational concept in software engineering; formalized by Kent Beck with the creation of [[SUnit]] (Smalltalk Unit testing framework) in the 1990s, and popularized in Java as JUnit. Standardized practice across modern software development; core principle in Robert C. Martin's *Clean Architecture: A Craftsman's Guide to Software Structure and Design* (2017).

---

## Compass

**Neighbors** — *what lives nearby*
[[Integration Tests]] check multiple pieces working together at a wider scope than unit tests, while [[Snapshot Tests]] compare output against a saved baseline to verify behavior.

**Clash** — *what pushes against this*
[[Manual Testing]] means running the app and clicking through it yourself rather than automating verification, and [[No Tests]] represents shipping code without any automated verification at all.

**Roots** — *where this comes from*
[[Clean Architecture]] makes unit testing possible through separation of layers, and [[Dependency Injection]] enables injecting mocks for isolation.

**Paths** — *where this leads*
[[xUnit]] is the framework that runs unit tests, [[Moq]] is the library that creates mock objects, and [[CI-CD Pipeline]] means unit tests run automatically on every push.
