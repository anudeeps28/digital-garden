---
type: atomic
tags: [coding/database, coding/security, sql, saas]
date: 2026-09-16
---

# Row-Level Security

## Idea
Instead of trusting every query to remember its `WHERE tenant_id = ...`, you push the filter into the database itself, where it cannot be forgotten.

## Definition
Row-Level Security (RLS) is a database feature that attaches a predicate function to a table so reads and writes are automatically constrained to the rows the current session is allowed to touch. In SQL Server it has two parts: a **FILTER predicate**, which silently removes invisible rows from `SELECT`, `UPDATE`, and `DELETE`, and a **BLOCK predicate**, which raises an error when someone tries to insert or move a row outside their slice. The predicate function is normally declared `WITH SCHEMABINDING` so the underlying columns can't be altered out from under it, and it reads the tenant key from `SESSION_CONTEXT` — a per-connection key/value store set by a connection interceptor when the connection opens, not passed as a query parameter the application could get wrong. The effect is that a query for the wrong tenant returns nothing rather than returning something it shouldn't.

## Source
SQL Server 2016 and Azure SQL Database; equivalent features exist in [[PostgreSQL]] (`CREATE POLICY`, since 9.5) and Oracle (Virtual Private Database).

---

## Compass

**Roots** — *where this comes from*
RLS is one layer of [[Multi-Tenant Data Isolation]], and it relies on the tenant identity resolved during [[Authentication]].

**Paths** — *where this leads*
Because the predicate runs on every access, it shapes query plans — and can amplify cost the way the [[N+1 Query Problem]] does if the tenant column isn't indexed.

**Neighbors** — *what lives nearby*
[[Least-Privilege Database Roles]] limit *which objects* a connection can touch; RLS limits *which rows* inside them.

**Clash** — *what pushes against this*
Application-level filtering is simpler to read and debug, but it fails open — a forgotten clause returns everything. RLS fails closed, at the cost of a filter that isn't visible in the query text.
