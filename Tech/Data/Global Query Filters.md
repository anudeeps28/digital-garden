---
type: atomic
tags: [coding/database, coding/dotnet, coding/security, coding/patterns]
date: 2026-10-01
---

# Global Query Filters

## Idea
If every query for a table needs the same `WHERE tenant_id = ...`, somebody will eventually forget it. A global query filter writes that clause for you, every time.

## Definition
A global query filter is an ORM feature where you declare a condition once, on the entity, and the ORM silently adds it to every query that touches that entity — including queries reached through navigation properties and joins. The two classic uses are **tenant filtering** (`TenantId == currentTenant`) and **soft delete** (`!IsDeleted`). In [[EF Core]] you write `modelBuilder.Entity<Order>().HasQueryFilter(o => o.TenantId == _tenantId)`; the filter must read the tenant from a member of the `DbContext` instance (set by [[Tenant Resolution]]) so each request gets its own value — a captured constant would be baked into the cached model. Three gotchas matter. First, it's bypassable on purpose: `IgnoreQueryFilters()` turns it off for one query, so that call deserves code-review attention. Second, SQL that goes around the ORM — `ExecuteSql`, Dapper, a stored procedure — never sees the filter. Third, it lives in the application, so a bug in the app, a second app, or someone with a database login is not constrained by it. That's why it pairs with [[Row-Level Security]]: the ORM filter is the convenient first line, the database policy is the one that still holds when the app is wrong.

## Providers
- **.NET** — EF Core `HasQueryFilter` and `IgnoreQueryFilters()`.
- **Java** — Hibernate `@Filter` / `@FilterDef` (must be enabled per session), plus `@TenantId` for discriminator-column multi-tenancy.
- **Python** — Django custom managers overriding `get_queryset()`.
- **Ruby** — Rails `default_scope`, escaped with `unscoped`.
- **Database-side equivalent** — [[PostgreSQL]] `CREATE POLICY` and SQL Server / Azure SQL security policies, i.e. [[Row-Level Security]].

## Source
EF Core documentation ("Global Query Filters", introduced in EF Core 2.0); Hibernate ORM filter documentation; Rails and Django ORM documentation.

---

## Compass

**Roots** — *where this comes from*
It's a feature of ORMs like [[EF Core]], and it exists because application-only filtering is the weakest layer of [[Multi-Tenant Data Isolation]].

**Paths** — *where this leads*
The tenant value comes from [[Tenant Resolution]]; the database-side backstop is [[Row-Level Security]]; in pooled [[Tenancy Models]] the two together are what separates customers.

**Neighbors** — *what lives nearby*
[[Least-Privilege Database Roles]] limit which objects a connection can reach; [[Defence in Depth]] is why you keep both the ORM filter and the database policy.

**Clash** — *what pushes against this*
Invisible filters make queries harder to reason about — a missing row may be a filter, not a bug — and they can hide performance problems if the filtered column isn't indexed. Some teams prefer explicit filters in every query for readability, accepting the risk of forgetting one.
