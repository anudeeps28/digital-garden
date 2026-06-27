---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Semantic Re-ranking

## Idea
Semantic re-ranking is a second-pass ML model that re-orders already-retrieved chunks by how well they actually answer the question, not just how well they word-match.

## Definition
After [[Hybrid Search]] returns its top candidates, semantic re-ranking takes roughly the top 50 chunks and runs them through a deep language model in [[Azure AI Search]] that scores each one against the true intent of the query. This catches cases where a chunk scored high on [[BM25 Scoring]] or [[Vector Search]] but isn't really relevant, and promotes chunks that are a better fit. In the project this sharpens the [[Retrieval Context (Top-K)]] handed to GPT-4o, so the answer is grounded in the genuinely best passages rather than the ones that merely overlapped on words or vectors. It's a cheap relevance boost that doesn't require re-embedding anything.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Hybrid Search]] is what semantic re-ranking refines—it takes the candidates that hybrid search retrieves and applies a second layer of relevance filtering. Similarly, [[BM25 Scoring]] is both a relevance-scoring step like re-ranking, just operating at an earlier stage of the retrieval pipeline.

**Clash** — *what pushes against this*
[[Vector Search]] represents raw similarity scoring that semantic re-ranking deliberately overrides—it's the initial pass that re-ranking can correct when the vector similarity was misleading.

**Roots** — *where this comes from*
Semantic re-ranking improves the retrieval quality that [[RAG (Retrieval-Augmented Generation)]] depends on, addressing a core challenge in the RAG pipeline of surfacing truly relevant context.

**Paths** — *where this leads*
The re-ranked top chunks become the grounding for [[Retrieval Context (Top-K)]], ensuring that the LLM receives the genuinely best passages rather than ones that merely overlapped on words or vectors.
