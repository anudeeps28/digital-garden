---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Query Routing

## Idea
Query routing is the decision of whether a user's question should be answered by a fast structured database lookup or by the slower, fuzzier Vector RAG path.

## Definition
Some questions have crisp, structured answers ("What is the deductible?") that a database query can return instantly and exactly. Others are open-ended ("What support is available?") and need [[RAG (Retrieval-Augmented Generation)|Vector RAG]] over embedded chunks. Query routing picks the right path so each question gets the cheapest capable handler. In practice, routing depends on [[Query Intent Classification]] to detect the question's intent — the system then directs it to the appropriate handler. Getting routing right is the core of [[Selective LLM Usage]]: don't invoke an LLM on something structured data can answer more efficiently.

## Source
Patrick Lewis et al., *Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks* (2020). The pattern of routing queries to different backends (structured vs. semantic search) is a foundational practice in hybrid retrieval systems that followed from RAG research and industry implementations of production RAG systems.

---

## Neighbors — *what lives nearby*
Routing acts on the intent that [[Query Intent Classification]] detects, so classification becomes the foundation that routing sits atop. Both are critical for directing questions to their optimal handlers.

## Clash — *what pushes against this*
[[Selective LLM Usage]] reveals the tension routing solves: the goal is to avoid using the LLM when structured data access can answer the question more cheaply and precisely. The tradeoff is that perfect routing requires accurate intent classification.

## Roots — *where this comes from*
[[RAG Query]] is the larger concept routing operates within — routing decides whether a question even becomes a RAG query or takes a different path.

## Paths — *where this leads*
Routing directs traffic to two destinations: structured database queries for precise, fact-based lookups, and [[RAG (Retrieval-Augmented Generation)]] for open-ended questions that need fuzzy semantic search. This branching enables cost-effective and accurate question-answering at scale.
