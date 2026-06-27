---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Co-reference Resolution

## Idea
Co-reference resolution rewrites a follow-up question so vague pronouns are replaced with the real things they refer to.

## Definition
In a conversation, people say "Does it cover physical therapy?" or "What about that plan?" — the meaning depends on earlier turns. Co-reference resolution swaps "it" and "that plan" for their concrete referents (e.g., "Does the Group 12345 plan cover physical therapy?") before anything is retrieved, because a vector or keyword search over a pronoun returns nothing useful. In practice, this is essential for multi-turn conversation: a rewriting step performs the resolution using context from prior turns, producing a standalone query that semantic search can actually match. Without it, every follow-up would silently lose its subject.

## Source
Jerry Hobbs, "Resolving Pronoun References" (1978); foundational work in computational linguistics on pronoun resolution. Modern approaches expanded across coreference resolution as a core NLP task throughout the 1980s onward.

---

## Compass

**Neighbors** — *what lives nearby*
[[Prompt Engineering]] techniques often implement co-reference resolution as a rewriting step, transforming vague references into explicit ones before passing queries downstream. [[Conversation Manager]] and similar context-tracking systems supply the prior turns needed to resolve references.

**Clash** — *what pushes against this*
A [[RAG Query]] is a single stateless query with no conversational context to resolve against, making it fundamentally different from the contextual approach co-reference resolution enables.

**Roots** — *where this comes from*
Resolution is a [[Prompt Engineering]]-driven rewrite step, grounded in the broader practice of shaping model behavior through prompting techniques.

**Paths** — *where this leads*
A resolved, standalone query can be retrieved accurately by [[Hybrid Search]], enabling the multi-turn conversation flow that co-reference resolution makes possible.
