---
type: atomic
tags: [coding/csharp, coding/dotnet]
date: 2026-06-26
---

# Result Pattern

## Idea
The Result pattern returns an explicit Success/Failure object for expected problems instead of throwing exceptions for them.

## Definition
The Result pattern models the outcome of an operation as a value — a `Result<T>` carrying either a success payload or a failure with an error code/message — rather than signalling failure by throwing. In practice, this is used for *expected* failures: a resource not found, a validation conflict, a query that returned no results. A service returns `Result.Failure("...")`, the [[Controller]] maps that to the right [[HTTP Status Codes|status code]] (404, 409, 422), and exceptions stay reserved for the genuinely exceptional — a dropped [[Connection String|DB connection]], an out-of-memory. This keeps the happy path readable, makes failure modes part of the method signature, and avoids using costly exceptions for ordinary control flow.

## Source
Scott Wlaschin, "Railway-Oriented Programming" (2014); also formalized as the Result/Either monad in functional programming (Haskell, F#, Rust). Popularized in .NET through libraries like `CSharp.Unions` and now widely adopted in modern exception handling strategies.

---

## Compass

**Neighbors** — *what lives nearby*
Like [[Guard Clauses]], Results surface failure early and explicitly, making the error cases part of the flow. They're also similar to [[DTOs (Data Transfer Objects)]] — a Result is simply a small object shaping an outcome.

**Clash** — *what pushes against this*
The Result pattern contrasts with [[Fail Fast Fail Loudly]], which crashes loudly on failure; Results instead swallow expected failures into values rather than crashing, keeping them handleable.

**Roots** — *where this comes from*
Results belong to the theme of [[Graceful Degradation]], where partial or expected failure becomes a first-class, handleable outcome rather than an exceptional condition.

**Paths** — *where this leads*
This pattern directly enables the use of [[HTTP Status Codes]], where the controller maps a failure Result to the right status code, and [[Controller]]s can then translate Results cleanly into HTTP responses.
