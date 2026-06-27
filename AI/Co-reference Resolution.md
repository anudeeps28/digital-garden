---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Co-reference Resolution

## Idea
Co-reference resolution rewrites a follow-up question so vague pronouns are replaced with the real things they refer to.

## Definition
In a conversation, people say "Does it cover physical therapy?" or "What about that plan?" — the meaning depends on earlier turns. Co-reference resolution swaps "it" and "that plan" for their concrete referents ("Does the Group 12345 plan cover physical therapy?") before anything is retrieved, because a vector or keyword search over a pronoun returns nothing useful. In the KBA project this is what makes multi-turn conversation work: the [[Follow-Up Rewriter]] performs the resolution using context from the [[Conversation Manager]], producing a standalone query that [[Hybrid Search]] can actually match. Without it, every follow-up would silently lose its subject.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
The [[Follow-Up Rewriter]] is the component that actually performs co-reference resolution, while the [[Conversation Manager]] supplies the prior turns needed to resolve references.

**Clash** — *what pushes against this*
A [[RAG Query]] is a single stateless query with no conversational context to resolve against, making it fundamentally different from the contextual approach co-reference resolution enables.

**Roots** — *where this comes from*
Resolution is a [[Prompt Engineering]]-driven rewrite step, grounded in the broader practice of shaping model behavior through prompting techniques.

**Paths** — *where this leads*
A resolved, standalone query can be retrieved accurately by [[Hybrid Search]], enabling the multi-turn conversation flow that co-reference resolution makes possible.
