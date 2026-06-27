---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Persona-Based Synthesis

## Idea
Persona-based synthesis shapes the answer's format and tone to fit who is asking — a terse table for a CSR, plain language for a member.

## Definition
The same benefit fact needs to be delivered differently depending on the audience. A customer service rep wants a dense markdown table they can scan fast; a plan member wants a warm, plain-language explanation. Persona-based synthesis selects the right answer style based on the asker's role, then asks GPT-4o on [[Azure OpenAI]] to synthesize in that voice. In the KBA project this is wired through [[Prompt Pieces]] — a swappable persona fragment is assembled into the prompt at runtime — so the underlying [[Retrieval Context (Top-K)]] stays the same while the presentation changes. It's the last-mile step that makes one RAG engine serve very different users.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Prompt Pieces]] form the modular building blocks for persona-based approaches, with persona as one of the swappable fragments. [[Response Enrichment]] also shapes the final output by adjusting the synthesis prompt, making them natural cousins in the quest to tailor synthesis to context.

**Clash** — *what pushes against this*
[[Template-Based Extraction]] represents the opposite extreme — a rigid, one-size-fits-all output format that doesn't bend to the audience, whereas persona-based synthesis is all about shaping the answer to fit who's asking.

**Roots** — *where this comes from*
[[Prompt Engineering]] is the broader theme that persona selection belongs to; persona is fundamentally a prompt-design decision, one piece of the larger craft of guiding language models to produce the right output.

**Paths** — *where this leads*
[[Azure OpenAI]] and GPT-4o are where the persona-shaped prompt is executed; the synthesized answer in the chosen voice is the final, user-facing result of this pattern.
