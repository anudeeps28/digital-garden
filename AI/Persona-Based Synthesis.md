---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Persona-Based Synthesis

## Idea
Persona-based synthesis shapes the answer's format and tone to fit who is asking — a terse table for a CSR, plain language for a member.

## Definition
The same information needs to be delivered differently depending on the audience. A technical user wants a dense, structured format they can parse quickly; a non-technical user wants a warm, plain-language explanation. Persona-based synthesis selects the right answer style based on the asker's role, then synthesizes the response in that voice. This is typically wired through modular prompt components — a swappable persona fragment is assembled into the prompt at runtime — so the underlying [[Retrieval Context (Top-K)]] stays the same while the presentation changes. It's an effective pattern for making a single information source serve diverse audiences.

## Source
Foundational prompt engineering pattern; popularized by OpenAI and the broader generative AI community through empirical work on role-playing and persona injection in prompts (early 2020s). Formalized in prompt engineering best practices and documented across community resources like OpenAI's prompt engineering guides and academic work on controlled text generation.

---

## Compass

**Neighbors** — *what lives nearby*
Modular prompt components form the building blocks for persona-based approaches, with persona as one of the swappable fragments. [[Response Enrichment]] also shapes the final output by adjusting the synthesis prompt, making them natural cousins in the quest to tailor synthesis to context.

**Clash** — *what pushes against this*
[[Template-Based Extraction]] represents the opposite extreme — a rigid, one-size-fits-all output format that doesn't bend to the audience, whereas persona-based synthesis is all about shaping the answer to fit who's asking.

**Roots** — *where this comes from*
[[Prompt Engineering]] is the broader theme that persona selection belongs to; persona is fundamentally a prompt-design decision, one piece of the larger craft of guiding language models to produce the right output.

**Paths** — *where this leads*
Large language models execute the persona-shaped prompt; the synthesized answer in the chosen voice is the final, user-facing result of this pattern.
