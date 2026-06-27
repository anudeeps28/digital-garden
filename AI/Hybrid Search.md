---
type: atomic
tags: [ai, ai/llm]
date: 2026-03-24
---

# Hybrid Search

## Idea
Hybrid search combines keyword search and vector search to get the best of both — exact word matching plus meaning-based similarity.

## Definition
Hybrid search runs both a traditional keyword search and a [[Vector Search]] in parallel, then merges and re-ranks the results. This overcomes the weaknesses of each approach alone: keyword search misses synonyms and paraphrases, while vector search can sometimes miss exact terms or rare entities. By combining both, you get results that match on meaning AND on specific terms. In practice, retrieval systems use hybrid search to ensure that both conceptual queries and specific lookups return relevant documents, making it particularly effective for [[RAG (Retrieval-Augmented Generation)|RAG]] systems where precision and recall both matter.

## Source
Foundational concept emerging from information retrieval research in the late 1990s–2000s; formalized as search systems gained vector-based retrieval capabilities. Major implementations include Elasticsearch (2010+), Weaviate, Pinecone, and Azure AI Search (2019+), which offer hybrid search as a core feature combining BM25 or TF-IDF keyword scoring with semantic vector similarity.

---

## Compass

**Neighbors** — *what lives nearby*
[[Vector Search]] handles the meaning-based half of hybrid search, while [[Keyword Search]] handles the word-matching half, and together they overcome what each approach alone cannot do.

**Clash** — *what pushes against this*
[[Single-Mode Search]] uses only keywords or only vectors rather than both, and [[No Search]] feeds entire documents to the LLM without retrieval, bypassing the need for any search strategy at all.

**Roots** — *where this comes from*
[[Azure AI Search]] is the service that implements hybrid search, and [[RAG (Retrieval-Augmented Generation)]] relies on hybrid search to power its retrieval step.

**Paths** — *where this leads*
Better retrieval through [[RAG (Retrieval-Augmented Generation)]] yields better AI answers, and [[Chunking|chunk quality]] directly affects how well search results perform.
