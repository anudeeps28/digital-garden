---
type: atomic
tags: [coding/database]
date: 2026-03-24
---

# SQL

## Idea
SQL is the standard language for talking to relational databases — SELECT reads data, INSERT adds it, UPDATE changes it, DELETE removes it.

## Definition
SQL (Structured Query Language) is how you communicate with relational databases like [[Azure SQL]]. The four core operations (CRUD) map to SQL commands: `SELECT * FROM Plans WHERE GroupNumber = '123'` (read), `INSERT INTO Documents (Name, Type) VALUES ('plan.pdf', 'PDF')` (create), `UPDATE Plans SET Status = 'Active'` (update), `DELETE FROM Plans WHERE Id = 5` (delete). In the KBA project, while developers mostly interact with the database through [[EF Core]] (which generates SQL from [[CSharp]] code), understanding SQL is essential for debugging queries, writing [[Database Migrations|migrations]], and working directly with [[Azure SQL]] in tools like SSMS or Azure Data Studio.

## Source
KBA AI Document Ingestion project

---

## Compass

**Roots** — *where this comes from*
SQL is the language of [[Relational Database|relational databases]] and is used by database engines like [[Azure SQL]] to operate on [[Database Tables|tables]].

**Paths** — *where this leads*
SQL knowledge enables you to work with [[EF Core]], which generates SQL from [[CSharp]] code, and to write [[Database Migrations|schema changes as SQL]]. Understanding [[Primary Key|keys]] and how to use [[JOIN (SQL)|SQL's JOIN operations]] for combining tables is essential, and exploring [[PostgreSQL]] shows how open-source databases extend SQL with advanced features.

**Neighbors** — *what lives nearby*
[[LINQ]] is C#'s query language that [[EF Core]] translates to SQL, and [[NoSQL Query Languages]] serve a similar purpose for non-relational databases.

**Clash** — *what pushes against this*
[[NoSQL]] databases like MongoDB and Cosmos DB don't use SQL at all, instead using their own query languages, and [[File-Based Storage]] takes a fundamentally different approach by storing data in files rather than organized tables.
