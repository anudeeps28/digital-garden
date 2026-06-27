---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Follow-Up Rewriter

## Idea
The follow-up rewriter is an LLM step that folds a multi-turn exchange down into a single standalone question ready for retrieval.

## Definition
Retrieval works best on one self-contained query, but real conversations are spread across turns and full of context that lives in earlier messages. The follow-up rewriter takes the recent dialogue and condenses it into one clear question — doing [[Co-reference Resolution]] along the way to swap out pronouns. In the KBA project it pulls recent turns from the [[Conversation Manager]] and emits a query that [[Hybrid Search]] can match precisely, so "and the deductible?" becomes "What is the in-network deductible for the Group 12345 plan?" This rewrite is the bridge between a natural chat experience and the system's need for a crisp [[RAG Query]].

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*
The rewriter performs [[Co-reference Resolution]], swapping pronouns for clear references, and works directly with the [[Conversation Manager]] which provides the turn history it condenses.

## Clash — *what pushes against this*
A [[RAG Query]] without rewriting is just a raw user query with no normalization, standing in contrast to the polished, disambiguated output the rewriter produces.

## Roots — *where this comes from*
This concept grows out of [[Prompt Engineering]] itself — the rewriter is fundamentally a carefully crafted LLM call designed to extract and clarify meaning from dialogue.

## Paths — *where this leads*
The standalone, rewritten query feeds directly into [[Hybrid Search]], enabling accurate and precise retrieval that wouldn't be possible with raw multi-turn context.
