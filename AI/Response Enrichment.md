---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Response Enrichment

## Idea
Response enrichment injects extra directives into the synthesis prompt so the LLM's answer comes out clearer and more complete.

## Definition
Before GPT-4o synthesizes an answer, response enrichment appends helpful context and instructions to the prompt — for example a source inventory listing which documents the chunks came from, or a cost-share summary that pre-organizes deductible and copay figures. These directives steer the model toward a clearer, better-structured answer without changing the retrieved chunks themselves. In the project this is layered on via [[Prompt Pieces]], appended after the [[Retrieval Context (Top-K)]] is assembled, and it complements [[Persona-Based Synthesis]]: enrichment improves substance and clarity, persona handles tone and format. Together they make the raw retrieval read like a polished answer.

## Source
AI document ingestion project

---

## Roots — *where this comes from*
Response enrichment is a targeted [[Prompt Engineering]] technique that addresses the need to structure and clarify synthesis from large amounts of retrieved data.

## Paths — *where this leads*
The enriched prompt drives clearer [[Azure OpenAI]] synthesis, making the final output more polished and useful to the end user.

## Neighbors — *what lives nearby*
[[Persona-Based Synthesis]] and response enrichment both refine the final synthesis step, while [[Prompt Pieces]] are the building blocks that enrichment directives are assembled from — enrichment uses these fragments to construct more sophisticated prompts.

## Clash — *what pushes against this*
[[Selective LLM Usage]] takes the opposite approach, avoiding LLM calls altogether where possible, whereas enrichment actively adds to the LLM call to improve its output.
