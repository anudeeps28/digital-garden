---
type: atomic
tags: [coding/csharp, coding/database]
date: 2026-03-24
---

# EF Core

## Idea
Entity Framework Core is an ORM that lets you write C# code instead of raw SQL — it translates your C# queries into SQL automatically.

## Definition
EF Core (Entity Framework Core) is an Object-Relational Mapper (ORM) for [[.NET 8]]. Instead of writing [[SQL]] strings manually, you define [[CSharp]] entity classes that map to [[Database Tables]], and use LINQ queries that EF translates to SQL behind the scenes. For example, `context.Plans.Where(p => p.GroupNumber == "123")` becomes `SELECT * FROM Plans WHERE GroupNumber = '123'`. EF Core also handles [[Database Migrations]] — when you change your entity classes, EF generates migration scripts to update the [[Azure SQL]] schema. It manages [[Foreign Key|foreign key]] relationships through navigation properties and supports async operations with methods like `SaveChangesAsync()`.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Dapper]] is a lightweight alternative ORM that stays closer to raw SQL, and [[Hibernate]] is Java's equivalent to EF Core for object-relational mapping.

**Clash** — *what pushes against this*
[[Raw SQL]] queries written manually as strings offer more control but less abstraction, and [[Stored Procedures]] push SQL logic into the database itself rather than letting the ORM handle it.

**Roots** — *where this comes from*
EF Core is a core library in [[.NET 8]] and is distributed through [[NuGet]], which is how most .NET dependencies are installed and managed.

**Paths** — *where this leads*
EF Core generates and tracks [[Database Migrations]] as your entity classes evolve, uses a [[Connection String]] to reach your database, and provides async methods like those in [[Async Await in CSharp]] for all operations.
