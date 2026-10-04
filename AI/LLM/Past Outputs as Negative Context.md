---
type: atomic
tags: [ai/llm, framework]
date: 2026-10-04
---

# Past Outputs as Negative Context

## Idea
To stop a model repeating itself across runs, paste in what it produced recently and tell it not to produce those again.

## Definition
A recurring generator (weekly ideas, daily headlines, newsletter hooks) has no memory between runs, so it drifts back to the same favourite phrasings. **Negative context** fixes this by putting recent outputs into the prompt as a list of things to avoid. A worked example: an ideas generator passes the last four weeks of hooks it produced, roughly a thousand [[Tokens]], with the instruction "do not repeat or closely paraphrase any of these". That is far cheaper and simpler than building an embedding index and filtering near-duplicates after generation. A second design choice mattered just as much: all topics stay in one call rather than one call per topic, because seeing everything at once is what lets the model connect ideas across topics. The serendipity is a feature of shared context.

## Source
There is no single coined origin; it is a practitioner prompting technique. The goal it serves, balancing relevance against novelty, goes back to Maximal Marginal Relevance (Carbonell and Goldstein, 1998), which reranked results to penalise similarity to what had already been chosen.

---

## Compass

**Roots** — *where this comes from*
It is a lightweight substitute for [[Vector Embedding]] deduplication: instead of measuring similarity after the fact, the model is shown the near-misses up front.

**Paths** — *where this leads*
The same window idea governs [[Retrieval Context (Top-K)]], where you decide how much history is worth its token cost, and [[Structured Output Validation]] can back it up with an exact-match check for repeats.

**Neighbors** — *what lives nearby*
[[Prompt Engineering]] is the broader craft, and [[Self-Learning Templates]] also feed past results back into future prompts, though to copy rather than avoid them.

**Clash** — *what pushes against this*
The window does not scale: after months of history the avoid-list crowds the prompt and real embedding dedup becomes worth it. Telling a model what not to do can also prime it toward exactly those phrases.
