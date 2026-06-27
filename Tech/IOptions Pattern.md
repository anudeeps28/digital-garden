---
type: atomic
tags: [coding/csharp, coding/dotnet]
date: 2026-06-26
---

# IOptions Pattern

## Idea
The IOptions pattern binds a chunk of appsettings to a strongly-typed C# class and injects it where you need it.

## Definition
The IOptions pattern is the .NET-idiomatic way to read configuration: instead of reaching into `IConfiguration` with magic string keys, I define a plain POCO (e.g. `OpenAiOptions`, `RateLimitOptions`), bind a section of `appsettings.json` to it at startup, and inject `IOptions<T>` via [[Dependency Injection]]. In the AI document ingestion project this keeps settings like OpenAI endpoints, cache TTLs, and rate-limit windows type-safe and discoverable — a typo becomes a compile-time or bind-time problem instead of a silent null at runtime. It naturally complements [[Fail Fast Fail Loudly]]: validate the bound options on startup so a misconfigured environment refuses to boot rather than failing on the first request.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Dependency Injection]] is the mechanism that delivers `IOptions<T>` to where it's needed, while [[DTOs (Data Transfer Objects)]] share a similar structure as simple typed objects that shape data.

**Clash** — *what pushes against this*
A [[Connection String]] represents the loosely-typed approach of reading raw strings directly, which is exactly the problem that IOptions improves on.

**Roots** — *where this comes from*
[[DotNet 8]] includes IOptions as part of the core .NET configuration system, establishing the framework foundation for this pattern.

**Paths** — *where this leads*
IOptions enables typed options to configure which [[Keyed Service (DI)|keyed implementation]] to wire up, and it naturally supports [[Fail Fast Fail Loudly]] by validating options at startup so bad config fails immediately rather than at runtime.
