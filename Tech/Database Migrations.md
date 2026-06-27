---
type: atomic
tags: [coding/database, coding/csharp]
date: 2026-03-24
---

# Database Migrations

## Idea
Migrations track changes to your database structure over time — like version control for your database schema.

## Definition
When you modify your [[CSharp]] entity classes (add a column, create a table, change a data type), [[EF Core]] can generate a migration — a C# file containing the `Up()` method (apply the change) and `Down()` method (undo it). Running `dotnet ef migrations add AddDocumentStatus` creates the migration, and `dotnet ef database update` applies it to [[Azure SQL]]. Migrations are stored as code files and committed to [[Git]], so every developer and the [[CI-CD Pipeline]] can reproduce the exact database schema. They're applied in order, each building on the previous one.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Git]] provides version control for code, just as migrations provide version control for database schema, and [[Flyway]] is a database migration tool for Java and other languages that serves the same purpose.

**Clash** — *what pushes against this*
[[Manual Schema Changes]] involve modifying the database by hand with no tracking, and [[Schema Drift]] occurs when the database and code disagree about the structure — both problems that migrations prevent.

**Roots** — *where this comes from*
[[EF Core]] provides migrations as a core feature for managing database schemas, and [[Azure SQL]] is the database whose schema migrations modify.

**Paths** — *where this leads*
Migrations run automatically during deployment through the [[CI-CD Pipeline]], and they create and modify [[Database Tables]] as the schema evolves.
