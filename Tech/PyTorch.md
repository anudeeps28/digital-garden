---
type: atomic
tags: [coding/python]
date: 2026-06-26
---

# PyTorch

## Idea
The deep-learning engine quietly doing the math under our embedding model — and installed lean to keep the image small.

## Definition
PyTorch is a deep-learning framework that provides tensors, automatic differentiation, and the neural-network runtime that models execute on. In the KBA AI Document Ingestion project, PyTorch is the engine beneath [[Sentence Transformers]]: when the embedding service runs all-MiniLM-L6-v2 to turn text into 384-dim [[Vector Embedding|vectors]], PyTorch is doing the actual forward pass. We install the CPU-only build (no CUDA/GPU stack) deliberately, because our [[Azure Container Apps]] deployment has no GPU and the CPU wheels make the [[Docker Image]] dramatically smaller and faster to pull. It's a transitive dependency we rarely call directly but always pay attention to at build time.

## Source
KBA AI Document Ingestion project

---

## Compass

**Roots** — *where this comes from*
PyTorch sits within the broader [[Python]] ecosystem and its deep-learning tooling stack.

**Paths** — *where this leads*
The CPU-only installation strategy directly reduces the size of the shipped [[Docker Image]], and PyTorch's computational output powers the [[Vector Embedding|vectors]] that downstream systems consume.

**Neighbors** — *what lives nearby*
[[Sentence Transformers]] is the higher-level library that sits directly on top of PyTorch and provides the embedding functionality we use in practice.

**Clash** — *what pushes against this*
[[Azure OpenAI]] represents the opposite approach — a hosted model API that hides the framework entirely, eliminating the need for self-hosting PyTorch and managing dependencies.
