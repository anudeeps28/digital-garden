---
type: atomic
tags: [coding/database]
date: 2026-05-06
---

# PostgreSQL

## Idea
PostgreSQL (Postgres) is an open-source relational database management system — it's actual software you install that *uses* [[SQL]] as its query language, plus its own powerful extensions.

## Definition
While [[SQL]] is a standardized language for querying relational data, PostgreSQL is a specific database engine that implements that language and adds features on top. Think of it like chess: SQL is the rules, Postgres is a specific chess engine that follows those rules and adds house rules of its own. Postgres originated at UC Berkeley in the late 1980s and is consistently ranked as developers' most-loved database. What it adds beyond standard SQL: advanced data types (JSON/JSONB, arrays, UUID, hstore, geometric types), full-text search, extensibility (custom functions, extensions like PostGIS), strong [[ACID Properties]] compliance, and proprietary syntax like `RETURNING` and `ON CONFLICT DO UPDATE` (upsert).

## Source
Conversation with Claude — SQL vs Postgres differences

---

## Compass

**Neighbors** — *what lives nearby*
[[MySQL]] and [[Azure SQL]] (Microsoft's cloud relational database that uses T-SQL dialect) are other popular relational database systems, while [[SQLite]] offers a lightweight, file-based alternative for similar use cases.

**Clash** — *what pushes against this*
[[SQL]] is the language specification itself rather than a database engine, and [[NoSQL]] databases like MongoDB and Redis operate on entirely different principles by rejecting the relational model.

**Roots** — *where this comes from*
Postgres is an implementation of the [[Relational Database]] model and organizes its data in [[Database Tables]], which form the foundational structure for how it stores and retrieves information.

**Paths** — *where this leads*
Postgres's native support for [[JSON]] via JSONB blurs the boundaries between relational and document databases, and frameworks like [[EF Core]] can use Postgres as a backing database through the Npgsql provider.
