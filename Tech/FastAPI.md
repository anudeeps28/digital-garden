---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# FastAPI

## Idea
A modern async Python framework that turns type hints into a documented HTTP API almost for free.

## Definition
FastAPI is a modern, async-first Python web framework that builds a [[REST API]] from ordinary type-annotated functions and generates interactive OpenAPI docs automatically. In the AI document ingestion project, FastAPI is the web layer of the embedding microservice (`services/embedding-service`): it exposes the `/embed` and `/embed/batch` endpoints that accept [[JSON]] text and return 384-dim [[Vector Embedding|vectors]] from the all-MiniLM-L6-v2 model. It leans on [[Pydantic]] for request/response validation and is run by [[Uvicorn]] inside the [[Docker]] container. Choosing this lightweight self-hosted service let us avoid paying [[Azure OpenAI]] for embeddings.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Uvicorn]] is the ASGI server that actually runs the FastAPI app, while [[REST API]] is the interface style that FastAPI implements.

**Clash** — *what pushes against this*
[[Azure OpenAI]] represents the managed embeddings API we chose not to call, opting instead for self-hosting this service.

**Roots** — *where this comes from*
[[Python]] is the language and ecosystem that FastAPI lives in.

**Paths** — *where this leads*
[[Pydantic]] serves as the validation layer FastAPI uses to enforce schemas, while [[Vector Embedding]] is what the endpoints ultimately produce.
