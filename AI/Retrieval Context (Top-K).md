---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Retrieval Context (Top-K)

## Idea
Retrieval context is the set of top ~15 most relevant chunks that get injected into the LLM prompt as the grounding for its answer.

## Definition
RAG works by giving the LLM only the most relevant slices of the corpus instead of the whole document set. The "top-K" is that selected set — in the project, roughly the top 15 chunks surviving [[Hybrid Search]] and [[Semantic Re-ranking]] — placed into the GPT-4o prompt so the model synthesizes its answer from real source text rather than memory. Choosing K is a balance: too few chunks and the answer misses context; too many and you waste [[Tokens]] and dilute focus. This context is the literal grounding of [[RAG (Retrieval-Augmented Generation)|RAG]], and everything upstream — chunking, search, re-ranking — exists to make these final chunks the right ones.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
[[Semantic Re-ranking]] produces the ordered chunks that become the top-K, while [[Hybrid Search]] is the retrieval operation that the top-K is drawn from.

## Clash — *what pushes against this*
[[Selective LLM Usage]] is about minimizing what the LLM sees, whereas top-K retrieval is about deciding how much context to feed it — a tension between constraint and information.

## Roots — *where this comes from*
The top-K is the grounding step of [[RAG (Retrieval-Augmented Generation)|RAG]], the foundational mechanism that anchors the entire retrieval-augmented pipeline.

## Paths — *where this leads*
[[Response Enrichment]] appends directives around this context before synthesis, while [[Tokens]] are directly driven by K, affecting the prompt token cost of each request.
