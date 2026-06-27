---
type: atomic
tags: [coding/csharp, coding/dotnet, coding/database]
date: 2026-06-26
---

# N+1 Query Problem

## Idea
The N+1 problem is when loading a list then looping to fetch each item's related data fires one query per row — N+1 round-trips where one would do.

## Definition
The N+1 query problem is a classic ORM performance trap: you run 1 query to get N parent rows, then accidentally run N more queries (one per row) to load each parent's related data. In the KBA AI Document Ingestion project this would bite when listing documents and then lazily touching each document's processing records — suddenly 50 documents means 51 trips to [[Azure SQL]]. The fix in [[EF Core]] is eager loading with `Include()` (or a projection) so the related data comes back in the same query; when I drop to Dapper for hot read paths I just write a single [[JOIN (SQL)]]. Either way the cure is "fewer, fatter queries," and [[Pagination]] keeps even the fat query bounded.

## Source
KBA AI Document Ingestion project

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
