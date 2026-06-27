---
type: atomic
tags: [coding/csharp, coding/architecture]
date: 2026-03-24
---

# Dependency Injection

## Idea
Dependency Injection (DI) is a pattern where classes receive the tools they need from the outside rather than creating them internally.

## Definition
Instead of a class saying `new BlobStorageClient()` inside itself, DI means the class declares "I need an `IBlobStorageClient`" in its constructor, and the framework automatically provides one at runtime. In [[.NET 8]], DI is built into the framework — you register services in `Program.cs` and the runtime resolves them everywhere. This keeps classes focused on their job, makes them testable (you can inject [[Moq]] fakes), and supports [[Clean Architecture]] by letting the Application layer depend on [[Interfaces in CSharp]] without knowing about Infrastructure details.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
The [[Service Locator Pattern]] is another way to resolve dependencies but is considered an anti-pattern, whereas the [[Factory Pattern]] creates objects but leaves the wiring to developers instead of automating it like DI does.

**Clash** — *what pushes against this*
[[Tight Coupling]] represents the opposite approach — when classes create their own dependencies directly with `new` — while [[Static Methods]] are globally accessible and require no injection but are notoriously hard to test.

**Roots** — *where this comes from*
DI is the mechanism that enables [[Clean Architecture]] by wiring layers together, and it's a core realization of the [[SOLID Principles]] through the Dependency Inversion Principle, with [[.NET 8]] providing built-in support through its DI container.

**Paths** — *where this leads*
DI maps [[Interfaces in CSharp]] to their concrete implementations, makes code testable through [[Unit Tests]] by allowing mock injection, and provides services to [[Middleware]] in the request pipeline.
