---
type: atomic
tags:
  - coding/architecture
date: 2026-03-24
---

# Clean Architecture

## Idea
Organize code into layers where each layer has one job, with dependencies pointing inward toward the domain.

## Definition
Clean Architecture is a software design pattern that separates code into distinct layers — Domain, Application, Infrastructure, API, and Presentation — so that each layer has a single responsibility. The Domain layer sits at the center with zero dependencies and contains entities and business rules. The Application layer holds business logic and use cases. Infrastructure handles external concerns like database connections, API clients, and third-party services. The Presentation layer (UI or API) is the outermost entry point. Each outer layer depends on inner layers, never the reverse, which makes the system testable, maintainable, and swappable.

## Source
Robert C. Martin, *Clean Architecture: A Craftsman's Guide to Software Structure and Design* (2017).

---

## Compass

**Neighbors** — *what lives nearby*
[[Hexagonal Architecture]], also known as Ports and Adapters, similarly isolates domain from infrastructure. [[Onion Architecture]] uses concentric layers with the domain at the center in much the same way. [[Separation of Concerns]] is the underlying principle that drives Clean Architecture — the idea that each module should handle one thing.

**Clash** — *what pushes against this*
[[Monolithic Architecture]] throws all code together without clear layer boundaries, ignoring structure entirely. [[Big Ball of Mud]] represents the opposite extreme — no discernible structure or separation at all.

**Roots** — *where this comes from*
Clean Architecture sits within the broader discipline of [[Software Architecture]], the practice of structuring systems for maintainability and extensibility. [[SOLID Principles]] are the design principles that Clean Architecture embodies and builds upon. The foundational question underneath all of this is: How do you decide which layer a piece of code belongs in?

**Paths** — *where this leads*
[[Dependency Injection]] is the mechanism that wires layers together without tight coupling, making the architecture work in practice. [[Unit Testing]] becomes straightforward because clean separation makes each layer independently testable. Clean Architecture is language-agnostic and can be applied across frameworks and platforms.
