---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# Pydantic

## Idea
A Python library that turns type hints into runtime guardrails for API data.

## Definition
Pydantic is a data-validation library that uses Python type hints to define schemas and then validates and parses incoming data against them at runtime. In practice, Pydantic models define the request and response shapes for [[FastAPI]] services — enforcing constraints like maximum text length and batch sizes so that malformed or oversized [[JSON]] payloads are rejected before reaching downstream processors. This keeps services safe and predictable while enabling [[FastAPI]] to auto-generate accurate OpenAPI documentation.

## Source
Samuel Colvin, first released 2018. Pydantic is the standard Python data validation library.

---

## Compass

**Neighbors** — *what lives nearby*
[[FastAPI]] uses Pydantic models directly as endpoint schemas, treating them as the single source of truth for API contracts.

**Clash** — *what pushes against this*
[[JSON]] is the raw, unvalidated wire format that Pydantic exists to tame — it represents the chaotic input before validation rules are applied.

**Roots** — *where this comes from*
[[Python]] provides the type-hint system that Pydantic builds upon, allowing declarative schema definition through modern Python syntax.

**Paths** — *where this leads*
Pydantic enables well-defined request/response contracts in [[REST API]]s and auto-generated documentation, while length limits directly support model constraints like how much text a model can handle in [[Tokens]].
