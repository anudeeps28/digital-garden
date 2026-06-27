---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# Python

## Idea
A high-level, dynamically typed language that earns its place in the KBA stack precisely where its ML ecosystem is unbeatable.

## Definition
Python is a high-level, dynamic, interpreted language known for readable syntax and a massive scientific/ML ecosystem. In the KBA AI Document Ingestion project, the main system is [[DotNet 8]], and Python shows up in exactly one place: the self-hosted embedding microservice (`services/embedding-service`). We chose Python there because the ML libraries — [[Sentence Transformers]] and [[PyTorch]] — are strongest and most mature in this ecosystem, with no comparable .NET equivalent. That single service is a [[FastAPI]] app running the all-MiniLM-L6-v2 model to produce 384-dim [[Vector Embedding|vectors]], served by [[Uvicorn]] and packaged in [[Docker]]. Python is used surgically, not everywhere.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[DotNet 8]] is the other language runtime in the project, and Python complements rather than replaces it. [[FastAPI]] is the Python web framework that we built on top of this language for our service.

**Clash** — *what pushes against this*
[[DotNet 8]] is statically typed and serves as the default for the rest of the system, contrasting sharply with Python's dynamic typing.

**Roots** — *where this comes from*
[[RAG (Retrieval-Augmented Generation)]] is the broader pipeline that this Python service feeds into, anchoring its role in the larger system.

**Paths** — *where this leads*
[[Sentence Transformers]] is the ML library that justifies bringing Python in at all, and [[PyTorch]] is the deep-learning runtime underneath the embedding model that powers the service.
