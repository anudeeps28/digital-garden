---
type: atomic
tags: [coding/database]
date: 2026-05-06
---

# Database Relationships

## Idea
There are really only two fundamental relationship patterns: "put a foreign key in one table" (one-to-many) and "create a middle table" (many-to-many) — every database relationship is one of these.

## Definition
When [[Database Tables|tables]] in a [[Relational Database]] need to connect, the relationship falls into one of three categories (which reduce to two patterns):

**One-to-Many** — The most common (~80% of relationships). One record in table A relates to many records in table B. Example: one user has many orders. Solution: put a [[Foreign Key]] (`user_id`) directly in the "many" side table (orders). No extra table needed.

**Many-to-Many** — Both sides can have multiple connections. Example: students take many courses, and courses have many students. Solution: create a [[Join Table]] (e.g., `enrollments`) that holds two foreign keys. The join table can also carry data about the relationship itself (like a grade).

**One-to-One** — Each record in table A relates to exactly one record in table B. Example: user and passport. Solution: put a foreign key in either table. Rare in practice.

To figure out which type you have, ask the question in both directions: "Can one A have many Bs?" and "Can one B have many As?" If both answers are yes → many-to-many. If only one is yes → one-to-many. If neither → one-to-one.

## Source
Conversation with Claude — database relationships from first principles

---

## Compass

**Neighbors** — *what lives nearby*
The [[Foreign Key]] is the mechanism that implements relationships, while the [[Join Table]] serves as the middle table needed for many-to-many connections.

**Clash** — *what pushes against this*
[[Denormalized Data]] flattens relationships by duplicating data instead of connecting tables, and [[Unlinked Tables]] exist without any relationships between them at all.

**Roots** — *where this comes from*
Relationships are what make a [[Relational Database]] truly "relational," and they exist to connect [[Database Tables]] to each other in meaningful ways.

**Paths** — *where this leads*
Understanding relationships enables you to write [[JOIN (SQL)]] queries across related tables, and relationships can become complex through patterns like [[Self-Referential Relationship|self-referential relationships]] where a table relates to itself. Frameworks like [[EF Core]] express relationships through navigation properties in C#.
