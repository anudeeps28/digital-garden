---
type: atomic
tags: [ai, ai/llm]
date: 2026-03-24
---

# Hybrid Search

## Idea
Hybrid search combines keyword search and vector search to get the best of both — exact word matching plus meaning-based similarity.

## Definition
Hybrid search runs both a traditional keyword search and a [[Vector Search]] in parallel, then merges and re-ranks the results. This overcomes the weaknesses of each approach alone: keyword search misses synonyms and paraphrases, while vector search can sometimes miss exact terms (like specific plan numbers or dollar amounts). By combining both, you get results that match on meaning AND on specific terms. In the KBA project, [[Azure AI Search]] performs hybrid search when answering [[RAG (Retrieval-Augmented Generation)|RAG]] queries, ensuring that both conceptual questions ("What mental health benefits are covered?") and specific lookups ("What is the Group 12345 deductible?") return the right chunks.

## Source
KBA AI Document Ingestion project

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
