---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Query Routing

## Idea
Query routing is the decision of whether a user's question should be answered by a fast structured database lookup or by the slower, fuzzier Vector RAG path.

## Definition
Some benefit questions have crisp, structured answers ("What is the Group 12345 deductible?") that an [[Azure SQL]] query can return instantly and exactly. Others are open-ended ("What mental health support is available?") and need [[RAG (Retrieval-Augmented Generation)|Vector RAG]] over embedded chunks. Query routing picks the right path so each question gets the cheapest capable handler. In the KBA project this lives in the IntentParser, which depends on [[Query Intent Classification]] to make the call — though today it is hard-routed straight to RAG, with the SQL path planned. Getting routing right is the core of [[Selective LLM Usage]]: don't burn an LLM call on something a SQL row answers better.

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*
Routing acts on the intent that [[Query Intent Classification]] detects, making classification the foundation that routing sits atop.

## Clash — *what pushes against this*
[[Selective LLM Usage]] reveals the tension routing solves: the goal is to avoid using the LLM when [[Azure SQL]] can answer the question more cheaply and precisely.

## Roots — *where this comes from*
[[RAG Query]] is the larger concept routing operates within — routing decides whether a question even becomes a RAG query or takes a different path.

## Paths — *where this leads*
Routing directs traffic to two destinations: [[Azure SQL]] for structured lookups that need exact answers, and [[RAG (Retrieval-Augmented Generation)]] for open-ended questions that need fuzzy semantic search.
