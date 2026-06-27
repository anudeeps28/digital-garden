---
type: atomic
tags: [coding/csharp, coding/dotnet, api]
date: 2026-06-26
---

# Pagination

## Idea
Pagination returns a long list in bite-sized pages instead of dumping everything at once.

## Definition
Pagination splits a large result set into pages so the API never serializes thousands of rows in one go. In the AI document ingestion project, endpoints like query history take `pageNumber` and `pageSize` as [[FromQuery Attribute|[FromQuery]]] parameters and translate them into a `Skip(...).Take(...)` on the [[EF Core]] query (or `OFFSET/FETCH` when I drop to Dapper for read-heavy paths). The response wraps the page of [[DTOs (Data Transfer Objects)|DTOs]] alongside metadata — total count, current page, page size — so the client can render "page 3 of 12". This keeps payloads small, queries fast, and memory bounded, which matters when the underlying [[Database Tables]] grow over time.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Page parameters arrive via the query string using [[FromQuery Attribute]], just as [[Rate Limiting]] bounds the cost of a single request. Both are techniques for constraining API resource consumption.

**Clash** — *what pushes against this*
The [[N+1 Query Problem]] represents the opposite approach — naively loading everything at once or fetching one row per request instead of one bounded page.

**Roots** — *where this comes from*
Pagination is a standard [[REST API]] convention for collections, and it shapes both the [[Request and Response]] pattern where the response carries the page of data plus metadata about it.

**Paths** — *where this leads*
Each page item is shaped as a [[DTOs (Data Transfer Objects)|DTO]], and [[EF Core]] uses `Skip/Take` to generate the paged SQL queries that enforce the boundary.
