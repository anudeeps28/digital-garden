---
type: atomic
tags: [coding/testing, coding/dotnet]
date: 2026-03-24
---

# xUnit

## Idea
xUnit is the test framework for .NET — it discovers and runs your test methods and reports pass/fail results.

## Definition
xUnit.net is a free, open-source [[NuGet]] testing framework for [[.NET 8]]. It provides attributes like `[Fact]` (a single test case) and `[Theory]` (parameterized test with multiple inputs via `[InlineData]`) to mark test methods. When you run `dotnet test`, xUnit discovers all test methods, executes them, and reports which passed or failed. It integrates with [[Azure DevOps]] pipelines for automated test reporting. In the project, xUnit is used alongside [[Moq]] to write [[Unit Tests]] and [[Integration Tests]] for the Application and Infrastructure layers.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[NUnit]] and [[MSTest]] are other popular .NET test frameworks that solve the same problem, while [[Jest]] is the JavaScript equivalent testing framework that provides similar capabilities in a different ecosystem.

**Clash** — *what pushes against this*
[[Manual Testing]] represents the opposite approach—testing by hand without a framework—as does [[Console.WriteLine Debugging]], where you print output instead of writing proper tests.

**Roots** — *where this comes from*
xUnit is installed as a [[NuGet]] package and targets the [[.NET 8]] runtime, grounding it in the .NET ecosystem and package management model.

**Paths** — *where this leads*
xUnit executes both [[Unit Tests]] and [[Integration Tests]], and those tests run automatically in a [[CI-CD Pipeline]] for continuous validation.
