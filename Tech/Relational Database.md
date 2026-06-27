---
type: atomic
tags: [coding/database]
date: 2026-05-06
---

# Relational Database

## Idea
A relational database solves one core problem: instead of repeating data, store each thing once and use ID numbers to point between tables.

## Definition
A relational database organizes data into [[Database Tables|tables]] (rows and columns) and defines relationships between them using [[Primary Key|primary keys]] and [[Foreign Key|foreign keys]]. The name comes from the mathematical concept of a *relation* (a set of tuples), invented by Edgar Codd at IBM in 1970. The key insight is eliminating **data redundancy** — if Alice's phone number appears in 50 order records and she changes it, you'd have to update all 50 rows. In a relational database, Alice's phone is stored once in a `users` table, and orders just *point* to her via a foreign key. The database guarantees consistency through [[ACID Properties]] (Atomicity, Consistency, Isolation, Durability). You query relational databases using [[SQL]]. Examples include [[PostgreSQL]], [[Azure SQL]], MySQL, and SQLite.

## Source
Conversation with Claude — relational databases from first principles

---

## Compass

**Neighbors** — *what lives nearby*
[[Database Tables]] are the building blocks that make a relational database work. Relational databases have a similar visual concept to [[Spreadsheets]], though spreadsheets lack the enforced relationships that give databases their power.

**Clash** — *what pushes against this*
[[NoSQL]] databases reject the relational model entirely, opting instead for documents, key-value pairs, or graph structures. [[Denormalized Data]] deliberately duplicates information across tables to chase performance gains, sacrificing the consistency guarantees that make relational databases trustworthy.

**Roots** — *where this comes from*
[[SQL]] is the language built to query relational databases and express their core question: why do we split data across multiple tables instead of keeping one big table?

**Paths** — *where this leads*
[[Database Relationships]] like one-to-many and many-to-many show how tables connect to one another. [[JOIN (SQL)]] is the mechanism that combines split tables back together when you need the full picture. [[ACID Properties]] provide the guarantees that make relational databases trustworthy for critical applications. [[EF Core]] is an ORM that maps C# objects to relational tables, bridging the object-oriented and relational worlds.
