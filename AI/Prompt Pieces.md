---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Prompt Pieces

## Idea
Prompt pieces are modular, versioned prompt fragments that get assembled at runtime instead of hardcoding one giant prompt.

## Definition
Rather than baking a single monolithic prompt into the code, the KBA project breaks the prompt into named, versioned fragments — base role, answer format, domain knowledge, synonyms, persona — stored in a PromptPieces table. At runtime the system assembles the relevant pieces into the final prompt sent to GPT-4o. Because the pieces live in data, not code, they can be edited and A/B tested without a redeploy, which is huge for tuning [[Prompt Engineering]] against real benefit questions. This modularity is what makes [[Persona-Based Synthesis]] and [[Response Enrichment]] clean to implement: you swap in a different persona piece or append an enrichment directive without touching the rest.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Prompt Engineering]] is the broader practice that prompt pieces operationalize in a modular way, and [[Response Enrichment]] naturally extends them by appending directives onto the assembled pieces.

**Clash** — *what pushes against this*
[[Selective LLM Usage]] takes the opposite approach — instead of shaping the LLM call with pieces, it's about deciding when to avoid calling the LLM altogether.

**Roots** — *where this comes from*
The assembled prompt ultimately gets sent to the GPT-4o deployment on [[Azure OpenAI]], which is the foundational service layer that makes this pattern possible.

**Paths** — *where this leads*
[[Persona-Based Synthesis]] builds on prompt pieces by swapping out the persona fragment to tailor the tone and voice for different audiences, extending modularity into output personalization.
