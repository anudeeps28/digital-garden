---
type: atomic
tags: [coding/csharp, coding/dotnet]
date: 2026-06-26
---

# Keyed Service (DI)

## Idea
A keyed service lets you register several implementations of one interface under string keys and ask for the exact one you want.

## Definition
Keyed services (added in .NET 8) solve the "which implementation?" problem when a single interface has multiple concrete versions. You register each under a string key and resolve it with `[FromKeyedServices("key")]` or `GetRequiredKeyedService<T>("key")`. In the KBA AI Document Ingestion project I register two OpenAI chat clients against the same interface: `"chat"` for the heavyweight **GPT-4o** (deep RAG answers) and `"chat-fast"` for the cheap **nano** model (quick classification, title generation). The service that needs an answer just asks for the key that fits the job, keeping the cost/quality trade-off explicit at the call site instead of buried in a factory. It's an extension of ordinary [[Dependency Injection]], and the keys themselves are often driven by the [[IOptions Pattern|IOptions]] config.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Keyed services are a flavor of standard [[Dependency Injection]] registration, centralizing the "how do I get the right instance" question much like an [[Entity Factory Method]] does.

**Clash** — *what pushes against this*
A [[Connection String]] approach picks a resource by raw config string rather than through typed key resolution.

**Roots** — *where this comes from*
Keyed DI is a [[DotNet 8]] feature that lets [[Interfaces in CSharp|interfaces]] have multiple implementations hanging off them.

**Paths** — *where this leads*
The [[IOptions Pattern]] often decides which key to resolve, and you can implement [[Graceful Degradation]] by falling back from the `"chat"` key to `"chat-fast"` under pressure.
