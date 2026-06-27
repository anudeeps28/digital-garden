---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Chunk Classification

## Idea
Chunk classification tags each document chunk with what kind of content it holds, so retrieval can filter by structure, not just by words.

## Definition
When a health-plan document is split during [[Chunking]], each resulting chunk is labeled by content type — Benefit, TableRow, Exclusion, Definition, Eligibility, PlanAdmin, or Prose. Storing this label as metadata in [[Azure AI Search]] lets retrieval narrow the field before scoring: a question about what's excluded can restrict to Exclusion chunks, and a copay lookup can favor TableRow chunks. In the project this structural tagging makes [[Hybrid Search]] far more precise, because the system isn't searching the whole corpus blindly — it searches the slice that structurally matches the question's [[Query Intent Classification|intent]].

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Classification is a refinement layered on top of [[Chunking Strategy]], and both [[Query Intent Classification]] and chunk classification label things to enable smarter routing and filtering throughout the system.

**Clash** — *what pushes against this*
Plain [[Chunking]] with no type awareness stands in contrast to classification — splitting without structure misses the opportunity to tag content by its role, while classification adds the structure that chunking lacks.

**Roots** — *where this comes from*
This concept belongs to the broader theme of [[Hybrid Search]], where classification metadata makes the search space itself filterable rather than blindly scoring everything.

**Paths** — *where this leads*
Typed filtering yields a cleaner [[Retrieval Context (Top-K)]] set, where the system retrieves not just the most similar chunks but the most similar chunks *of the right type*.
