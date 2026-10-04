---
type: atomic
tags: [coding/architecture, coding/patterns, coding/database]
date: 2026-10-04
---

# Repository Pattern

## Idea
Hide where and how data is stored behind an object that looks like a simple collection: get this, find those, save that. Business code asks the repository and never touches the database, file or API directly.

## Definition
A **repository** mediates between the domain and the storage layer. It exposes collection-like operations in domain terms, such as `get_by_id`, `find_overdue`, `add`, `save`, and hides queries, serialisation and storage technology behind them. Business logic depends on the repository's interface, so the storage can change, and tests can swap in an in-memory version. A good repository also owns **defensive decoding**: storage is external input and may be old, partial or corrupt. A settings repository for a small app, for example, reads its stored JSON, validates each field, and falls back to defaults for anything missing or malformed instead of crashing. After an upgrade adds a new setting, old stored data still loads; after a bad write, the app still starts. That logic lives in exactly one place instead of being repeated wherever settings are read. A useful discipline is to return domain objects, not raw rows or dictionaries, so callers never learn the storage shape.

## Source
Described in Martin Fowler's *Patterns of Enterprise Application Architecture* (Addison-Wesley, 2002), where the Repository pattern was contributed by Edward Hieatt and Rob Mee, and made central to domain modelling in Eric Evans' *Domain-Driven Design* (2003).

---

## Compass

**Roots** — *where this comes from*
It is a driven port in [[Ports and Adapters]] and a fixture of [[Clean Architecture]], keeping persistence at the outer edge.

**Paths** — *where this leads*
Defensive decoding pairs naturally with [[Runtime Schema Validation]] or [[Pydantic]] models, and an in-memory repository makes [[Unit Tests]] fast without a database.

**Neighbors** — *what lives nearby*
In .NET, [[EF Core]]'s `DbContext` already behaves like a unit of work with repository-like sets. [[Dependency Injection]] wires the real or fake repository in, and the [[Strategy Pattern]] has the same "swap the implementation" shape.

**Clash** — *what pushes against this*
Wrapping a full ORM in a thin repository often just re-exposes it with less power and creates the [[N+1 Query Problem]] behind innocent-looking methods. Many teams now skip the extra layer and use the ORM directly unless they genuinely need to swap storage.
