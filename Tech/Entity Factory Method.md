---
type: atomic
tags: [coding/csharp, coding/dotnet]
date: 2026-06-26
---

# Entity Factory Method

## Idea
An entity factory method creates a domain object through a named static `Create()` instead of a raw constructor, so an entity can never be born in an invalid state.

## Definition
The entity factory method pattern keeps a domain entity's invariants in one place: instead of a public constructor that callers fill in field by field, the entity exposes a static `Create(...)` that validates inputs and returns a valid instance, and the constructor is made private. Once created, the entity is mutated only through **intent-named state methods** — in the AI document ingestion project a `Document` moves forward via `MarkProcessed()` or `MarkFailed(reason)` rather than letting outside code poke `Status = "..."` directly. This bakes [[Guard Clauses]] into creation and every transition, so illegal states (a "Processed" document with no result) simply can't be expressed. The [[EF Core]] entities follow this so persistence and domain rules don't fight each other.

## Source
AI document ingestion project

---

## Compass

**Roots** — *where this comes from*
Private constructors plus static factories are a core [[CSharp]] idiom, and this pattern emerges from the deeper question of how domain invariants can coexist with an ORM's entities like [[EF Core]].

**Paths** — *where this leads*
Invalid state is rejected at creation time, embodying the principle of [[Fail Fast Fail Loudly]], and the `Create()` method can return a [[Result Pattern]] when validation fails instead of throwing an exception.

**Neighbors** — *what lives nearby*
[[Guard Clauses]] are the mechanism the factory uses to reject invalid creation, and [[Keyed Service (DI)]] shares the same goal of centralizing "how a correct instance is produced" in a single location.

**Clash** — *what pushes against this*
[[DTOs (Data Transfer Objects)]] represent the opposite philosophy — they are anemic open bags of data, whereas entities guard their own invariants and encapsulate their state.
