---
type: atomic
tags: [ai, ai/llm]
date: 2026-03-24
---

# Chunking

## Idea
Chunking is splitting a large document into smaller pieces so the AI can process and search through them effectively.

## Definition
LLMs have limited context windows ([[Tokens]]), so you can't feed an entire 100-page plan document into one prompt. Chunking breaks the document into smaller, manageable pieces — each chunk might be a page, a section, or a fixed number of characters. Each chunk is then embedded as a [[Vector Embedding]] and indexed in [[Azure AI Search]]. When a [[RAG (Retrieval-Augmented Generation)|RAG]] query comes in, only the most relevant chunks are retrieved, keeping the prompt focused and costs low. The [[Chunking Strategy]] (how you split) directly impacts search quality — splitting mid-sentence or mid-table produces poor results.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Pagination]] is the display-layer equivalent of chunking — splitting content into pages for user browsing — while [[Sharding]] takes the same principle to infrastructure, splitting data across database servers.

**Clash** — *what pushes against this*
The opposite approach is [[Full Document Processing]], which feeds the entire document at once into the system, or [[Single-Pass Extraction]], which processes without splitting at all.

**Roots** — *where this comes from*
Chunking is a critical step in the [[RAG (Retrieval-Augmented Generation)|RAG]] pipeline, where it enables the retrieval mechanism to work at all. The core question underneath is: what's the optimal chunk size for plan documents?

**Paths** — *where this leads*
Each chunk gets embedded as a [[Vector Embedding]] and indexed in [[Azure AI Search]] for fast retrieval, and the choice of [[Chunking Strategy]] — varying by document type — directly affects how well searches work. The size of chunks also directly impacts [[Tokens|token]] usage and overall cost.
