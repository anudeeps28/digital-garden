---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# Uvicorn

## Idea
The lightweight ASGI server that lets a single FastAPI process handle many concurrent embedding requests.

## Definition
Uvicorn is an ASGI (Asynchronous Server Gateway Interface) server for Python — the production process that actually receives HTTP connections and hands them to an async app. It runs [[FastAPI]] applications inside [[Docker]] containers, serving HTTP endpoints with high concurrency so many requests can be in flight while the application processes them. It's the runtime bridge between the container's exposed port and the Python application code, commonly deployed on cloud platforms like [[Azure Container Apps]].

## Source
Tom Christie, first released 2016; now the industry-standard ASGI server for Python async applications.

---

## Compass

**Neighbors** — *what lives nearby*
[[FastAPI]] is the app that Uvicorn serves; the two are almost always paired in production Python async applications.

**Clash** — *what pushes against this*
[[Azure Container Apps]] sits above Uvicorn as a managed platform layer, handling orchestration and scaling rather than focusing on the per-request serving that Uvicorn provides.

**Roots** — *where this comes from*
Uvicorn belongs to the [[Python]] ecosystem as an ASGI server implementation.

**Paths** — *where this leads*
[[Docker]] relies on Uvicorn as the process its entrypoint launches to run the containerized service, and it exposes the HTTP surface that becomes a [[REST API]] for clients to call.
