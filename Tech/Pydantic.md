---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# Pydantic

## Idea
A Python library that turns type hints into runtime guardrails for API data.

## Definition
Pydantic is a data-validation library that uses Python type hints to define schemas and then validates and parses incoming data against them at runtime. In the AI document ingestion project, Pydantic models define the request and response shapes for the [[FastAPI]] embedding service — for example enforcing a maximum text length and a maximum batch size on the `/embed/batch` endpoint, so a malformed or oversized [[JSON]] payload is rejected before it ever reaches the all-MiniLM-L6-v2 model. This keeps the self-hosted service safe and predictable and is what lets [[FastAPI]] auto-generate accurate OpenAPI docs.

## Source
AI document ingestion project

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
