---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-27
---

# Prompt Pieces

## Idea
Prompt pieces are modular, versioned prompt fragments that get assembled at runtime instead of hardcoding one giant prompt.

## Definition
Rather than baking a single monolithic prompt into the code, you break the prompt into named, versioned fragments — base role, answer format, domain knowledge, synonyms, persona — and store them in a table or database. At runtime the system assembles the relevant pieces into the final prompt sent to the LLM. Because the pieces live in data, not code, they can be edited and A/B tested without a redeploy, which is essential for tuning [[Prompt Engineering]] against real use cases. This modularity makes [[Persona-Based Synthesis]] and [[Response Enrichment]] clean to implement: you swap in a different persona piece or append an enrichment directive without touching the rest.

## Source
Emergent pattern in AI/LLM applications; formalized by practitioners building systems with large language models (e.g., prompt templating frameworks like Langchain, Anthropic prompt caching patterns, late 2022–2024).

---

## Compass

**Neighbors** — *what lives nearby*
[[Prompt Engineering]] is the broader practice that prompt pieces operationalize in a modular way, and [[Response Enrichment]] naturally extends them by appending directives onto the assembled pieces.

**Clash** — *what pushes against this*
[[Selective LLM Usage]] takes the opposite approach — instead of shaping the LLM call with pieces, it's about deciding when to avoid calling the LLM altogether.

**Roots** — *where this comes from*
This pattern builds on foundational software modularity and composition patterns, applied specifically to prompt management as LLM systems became more sophisticated and the need for prompt tuning and versioning increased.

**Paths** — *where this leads*
[[Persona-Based Synthesis]] builds on prompt pieces by swapping out the persona fragment to tailor the tone and voice for different audiences, extending modularity into output personalization.
