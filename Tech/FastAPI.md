---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# FastAPI

## Idea
A modern async Python framework that turns type hints into a documented HTTP API almost for free.

## Definition
FastAPI is a modern, async-first Python web framework that builds a [[REST API]] from ordinary type-annotated functions and generates interactive OpenAPI docs automatically. In practice, FastAPI serves as the web layer for microservices: it exposes endpoints that accept [[JSON]] input and return structured responses, leveraging [[Pydantic]] for request/response validation and running via [[Uvicorn]] inside [[Docker]] containers. The framework is commonly used for lightweight, self-hosted API services because of its minimal overhead and automatic schema generation.

## Source
Sebastián Ramírez, FastAPI framework (first released 2018); https://fastapi.tiangolo.com/

---

## Compass

**Neighbors** — *what lives nearby*
[[Uvicorn]] is the ASGI server that actually runs the FastAPI app, while [[REST API]] is the interface style that FastAPI implements.

**Clash** — *what pushes against this*
Managed cloud APIs like [[Azure OpenAI]] provide embeddings as a service but incur per-call costs; self-hosting lightweight services avoids these costs at the expense of operational complexity.

**Roots** — *where this comes from*
[[Python]] is the language and ecosystem that FastAPI lives in.

**Paths** — *where this leads*
[[Pydantic]] serves as the validation layer FastAPI uses to enforce request/response schemas, while the endpoints connect to downstream services or data processing layers that consume the structured responses.
