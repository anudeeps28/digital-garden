---
type: atomic
tags: [coding/csharp]
date: 2026-03-24
---

# Interfaces in CSharp

## Idea
An interface is a contract that says "any class doing this job must have these methods" — it defines *what* something does without specifying *how*.

## Definition
In [[CSharp]], an interface (prefixed with `I`, e.g., `IDocumentService`) declares method signatures, properties, and events that implementing classes must provide. Interfaces are the backbone of [[Dependency Injection]] and [[Clean Architecture]] — the Application layer defines interfaces, and the Infrastructure layer provides the concrete implementations. This means you can swap out implementations without changing any business logic, for example by replacing a real external service client with a test double in [[Unit Tests]].

## Source
Microsoft documentation and C# language specification; interfaces are a core object-oriented programming feature standardized as part of the C# language since its introduction in 2000. The pattern of using interfaces for [[Dependency Inversion]] was formalized by Robert C. Martin in *Clean Architecture: A Craftsman's Guide to Software Structure and Design* (2017).

---

## Roots — *where this comes from*
Interfaces are fundamental to [[CSharp]] as the language that provides them, and they serve as the bedrock for implementing [[SOLID Principles]], particularly the Dependency Inversion Principle. [[Clean Architecture]] relies on interfaces to define clear boundaries between layers and enforce abstraction.

## Paths — *where this leads*
Interfaces enable [[Dependency Injection]] by allowing DI containers to wire up interface-to-implementation mappings at startup, and they make it straightforward to write testable code through [[Unit Tests]] where you can easily mock dependencies with tools like [[Moq]]. They're also commonly used alongside [[DTOs (Data Transfer Objects)]] to define data contracts.

## Neighbors — *what lives nearby*
[[Abstract Classes]] also define contracts and serve a similar purpose, but they can include shared implementation whereas interfaces cannot. [[Protocols]] are the equivalent concept in Python and Swift, providing the same abstraction mechanism across different languages.

## Clash — *what pushes against this*
[[Concrete Classes]] implement behavior directly without requiring a contract abstraction, and [[Tight Coupling]] occurs when code depends on specific implementations rather than relying on the abstraction that an interface provides.
