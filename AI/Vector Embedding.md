---
type: atomic
tags: [ai/llm, ai]
date: 2026-03-24
---

# Vector Embedding

## Idea
A vector embedding turns text into a list of numbers so that similar meanings end up close together mathematically.

## Definition
An embedding is a numerical representation of text — a list (vector) of hundreds or thousands of floating-point numbers. An embedding model (like Ada from [[Azure OpenAI]]) converts a sentence or paragraph into this vector. The key insight: texts with similar meanings produce vectors that are close together in this high-dimensional space. "What is the copay?" and "How much do I pay per visit?" would have similar vectors even though the words differ. In the KBA project, every document chunk gets embedded and stored in [[Azure AI Search]], enabling [[Vector Search]] — finding relevant chunks by meaning rather than exact keyword match.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Word2Vec]] is an earlier word embedding technique that pioneered this approach, and [[TF-IDF]] represents an older method for representing text as numbers, though it's frequency-based rather than meaning-based like modern embeddings.

**Clash** — *what pushes against this*
[[Keyword Matching]] searches by exact word matches rather than meaning, and [[Plain Text]] exists without any numerical representation at all, making both fundamentally opposed to the vector embedding approach.

**Roots** — *where this comes from*
[[LLM (Large Language Model)]] and embedding models are related neural networks that work with similar underlying principles, and [[Azure OpenAI]] provides the embedding model that powers this approach in practice.

**Paths** — *where this leads*
[[Vector Search]] enables searching by vector similarity, which can be combined with [[Keyword Matching]] in [[Hybrid Search]] for more robust results. The vectors are stored and indexed in [[Azure AI Search]], and the process requires [[Chunking]] to prepare text before embedding.
