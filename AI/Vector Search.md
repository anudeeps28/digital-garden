---
type: atomic
tags: [ai, ai/llm]
date: 2026-03-24
---

# Vector Search

## Idea
Vector search finds documents whose meaning is similar to your query by comparing vector embeddings — it searches by concept, not just keywords.

## Definition
Vector search (also called semantic search) compares the [[Vector Embedding]] of a query against the embeddings of stored document chunks. If two vectors are "close" in the embedding space (measured by cosine similarity), the texts have similar meaning. For example, a search for "annual maximum out-of-pocket" can find a chunk that says "yearly OOP limit" even though no words match. Vector search is operationalized in modern platforms like [[Azure AI Search]], Pinecone, and Weaviate to power [[RAG (Retrieval-Augmented Generation)|RAG]] systems that retrieve the most relevant passages for a given query.

## Source
Modern vector search emerged from information retrieval research and word embedding techniques. Tomas Mikolov et al. introduced Word2Vec in 2013, enabling dense vector representations of words. The application of dense embeddings to document retrieval and semantic search was popularized in the late 2010s through tools like Elasticsearch with dense_vector support, Weaviate, Pinecone, and integration into major platforms like OpenAI's API and Azure AI Search, enabling practical semantic search at scale.

---

## Compass

**Neighbors** — *what lives nearby*
[[Keyword Search]] is the traditional approach that matches exact words, while [[Fuzzy Search]] accounts for typos but still doesn't grasp meaning the way vector search does.

**Clash** — *what pushes against this*
[[Keyword Search]] prioritizes exact word matches over semantic meaning, and [[Exact Match]] requires identical strings — both miss the conceptual similarities that vector search captures.

**Roots** — *where this comes from*
[[Vector Embedding]] is the foundation that makes vector search possible, and [[Azure AI Search]] is the service that operationalizes vector search in practice.

**Paths** — *where this leads*
[[Hybrid Search]] combines vector search with keyword search to get the best of both worlds, and [[RAG (Retrieval-Augmented Generation)|RAG]] relies on vector search to power its retrieval step.
