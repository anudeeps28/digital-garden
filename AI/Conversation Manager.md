---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Conversation Manager

## Idea
The conversation manager is the stateful piece that remembers recent turns in a session so follow-up questions have context.

## Definition
RAG itself is stateless — each query is answered fresh — but conversations are not. The conversation manager holds the recent query/answer turns for a session (with a 30-minute timeout that clears stale context) so later steps know what "it" and "that plan" mean. In the KBA project it feeds the [[Follow-Up Rewriter]], which uses the stored turns to perform [[Co-reference Resolution]] and produce a standalone query. It is deliberately lightweight: just enough short-term memory to make multi-turn chat coherent, without trying to persist a full history that would bloat the [[Retrieval Context (Top-K)]].

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
The [[Follow-Up Rewriter]] is the main consumer of the manager's stored turns, using them to contextualize follow-up questions. This stored context also enables [[Co-reference Resolution]], which relies on having recent conversation history to understand pronouns and references.

**Clash** — *what pushes against this*
A [[RAG Query]] operates as a stateless single-shot query with no memory, directly contrasting with the conversation manager's approach of maintaining context across multiple turns.

**Roots** — *where this comes from*
The conversation manager sits within [[RAG (Retrieval-Augmented Generation)]], adding a layer of conversational state on top of RAG's otherwise stateless retrieval model.

**Paths** — *where this leads*
The stored turns feed into the [[Follow-Up Rewriter]], which condenses the multi-turn context into a single standalone query that can be used for downstream retrieval steps.
