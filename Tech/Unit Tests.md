---
type: atomic
tags: [coding/testing]
date: 2026-03-24
---

# Unit Tests

## Idea
Unit tests check one small piece of code in isolation — verifying that a single method or class works correctly without depending on external systems.

## Definition
A unit test is a small, fast, automated test that exercises a single unit of code (usually a method) with known inputs and verifies expected outputs. The key word is *isolation* — you don't call real databases, APIs, or file systems. Instead, you use [[Moq]] to create fake versions of dependencies (like mocking `IBlobStorageClient`). This is possible because of [[Interfaces in CSharp]] and [[Dependency Injection]] — you inject mocks instead of real services. In the project, unit tests verify business logic in the Application layer without touching [[Azure SQL]], [[Azure Blob Storage]], or [[Azure OpenAI]]. Tests are written with [[xUnit]] and follow the Arrange-Act-Assert pattern.

## Source
AI document ingestion project

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
