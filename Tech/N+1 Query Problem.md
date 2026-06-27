---
type: atomic
tags: [coding/csharp, coding/dotnet, coding/database]
date: 2026-06-26
---

# N+1 Query Problem

## Idea
The N+1 problem is when loading a list then looping to fetch each item's related data fires one query per row — N+1 round-trips where one would do.

## Definition
The N+1 query problem is a classic ORM performance trap: you run 1 query to get N parent rows, then accidentally run N more queries (one per row) to load each parent's related data. For example, listing 50 parent records then lazily loading each one's related data means 51 database round-trips instead of 1. The fix in [[EF Core]] is eager loading with `Include()` (or a projection) so the related data comes back in the same query; writing a single [[JOIN (SQL)]] achieves the same effect at the SQL level. Either way the cure is "fewer, fatter queries," and [[Pagination]] keeps even the fat query bounded.

## Source
Industry standard concept in ORM and relational database optimization; formalized and widely discussed in ORM documentation (e.g., Hibernate, Entity Framework, SQLAlchemy) and in classical database design literature since the early 2000s.

---

## Compass

**Neighbors** — *what lives nearby*
A single [[JOIN (SQL)]] is the manual fix for N+1, collapsing multiple queries into one combined result. Both this problem and [[Pagination]] are about keeping query volume and result size under control.

**Clash** — *what pushes against this*
[[In-Memory Caching]] avoids the queries entirely rather than trying to batch or optimize them, trading memory for fewer database round-trips.

**Roots** — *where this comes from*
[[EF Core]]'s lazy loading is where N+1 silently creeps in, and the fundamental issue stems from [[Relational Database|relational databases]], where the round-trip cost of multiple queries is what makes N+1 expensive in the first place.

**Paths** — *where this leads*
You can collapse N+1 into a single joined query using [[JOIN (SQL)]], and [[Pagination]] helps you bound the result set so even the fixed query stays cheap and performant.
