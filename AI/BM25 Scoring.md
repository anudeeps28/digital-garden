---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# BM25 Scoring

## Idea
BM25 is the classic keyword-relevance formula that scores how well a document matches a search query based on word overlap.

## Definition
BM25 (Best Match 25) ranks documents by combining term frequency (how often a query word appears in a chunk) with inverse document frequency (how rare that word is across the whole corpus), plus a length-normalization factor so long chunks don't win unfairly. It is purely lexical — it matches exact words and stems, with no understanding of meaning. In the project, BM25 powers the keyword half of [[Hybrid Search]] inside [[Azure AI Search]]: it reliably catches specific terms like plan numbers and dollar amounts that [[Vector Search]] might gloss over, while the vector half handles paraphrase and synonyms. The two scores are fused before [[Semantic Re-ranking]] takes a final pass.

## Source
AI document ingestion project

---

## Roots — *where this comes from*
[[Hybrid Search]] uses BM25 as the keyword half of its strategy, grounding the approach in proven lexical matching techniques.

## Paths — *where this leads*
BM25 results get re-ordered by [[Semantic Re-ranking]], a smarter model that refines the initial keyword matches with deeper semantic understanding.

## Neighbors — *what lives nearby*
[[Vector Search]] serves as the meaning-based counterpart that BM25 is fused with, and BM25 itself operates over [[Tokens]], the fundamental units it scores.

## Clash — *what pushes against this*
[[Vector Embedding]] represents meaning rather than literal word matches, embodying an opposite scoring philosophy that captures paraphrase and synonyms where BM25 sees only exact terms.
