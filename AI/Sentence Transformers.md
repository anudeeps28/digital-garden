---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Sentence Transformers

## Idea
A library of pretrained models that map a sentence to a single dense vector — the heart of our cost-saving, self-hosted embedding service.

## Definition
Sentence Transformers is a Python library offering pretrained models that turn whole sentences or passages into dense [[Vector Embedding|embeddings]], where semantic similarity becomes geometric closeness. In the AI document ingestion project, this is the core of the embedding microservice: we self-host the `all-MiniLM-L6-v2` model, which produces 384-dimensional vectors, instead of paying for [[Azure OpenAI]] embeddings — a deliberate cost-cutting choice for a system that embeds large volumes of document [[Chunking|chunks]]. The model runs on [[PyTorch]] (CPU-only), is wrapped by a [[FastAPI]] app, served by [[Uvicorn]], and deployed in [[Docker]] on [[Azure Container Apps]]. Those embeddings then power [[Vector Search]] and [[Hybrid Search]] in our [[RAG (Retrieval-Augmented Generation)]] pipeline.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
[[Vector Embedding]] is exactly what this library produces, turning text into dense vectors. [[Azure OpenAI]] is an alternative embeddings provider — the commercial option we chose against in favor of self-hosting Sentence Transformers for cost reasons.

## Clash — *what pushes against this*
[[Tokens]] are the discrete sub-word units that text is broken into, whereas Sentence Transformers collapses an entire sentence or passage into a single continuous vector representation.

## Roots — *where this comes from*
This library serves as the foundation for [[RAG (Retrieval-Augmented Generation)]], the broader pipeline that combines retrieval and generation to augment LLM responses with grounded context.

## Paths — *where this leads*
The embeddings produced here enable [[Vector Search]], which performs nearest-neighbor retrieval to find semantically similar chunks, and can be combined with [[Hybrid Search]] to merge vector-based and keyword-based ranking. Upstream, [[Chunking]] determines which portions of text get embedded in the first place.
