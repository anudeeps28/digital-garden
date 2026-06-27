---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Query Intent Classification

## Idea
Query intent classification is reading a question to figure out what kind of answer it wants, so the system can pick the right handler.

## Definition
Before answering, the system parses the user's question to detect its shape: is it asking for one specific field, a comparison across options, or an exploratory overview? Each shape maps to a different, cost-appropriate handler. In practice, a specific-field question can be routed to efficient structured queries, while an exploratory one requires semantic understanding. Classifying intent first is what makes [[Selective LLM Usage]] possible: you only spend expensive model tokens on the questions that genuinely need synthesis.

## Source
Foundational concept in NLP and information retrieval; formalized in the context of dialogue systems and question-answering systems. The systematic classification of user queries into intent categories is a core technique in conversational AI, popularized through work on dialogue state tracking and question-answering systems (e.g., Amazon Alexa, Google Assistant, and research systems like Stanford's Question-Answering Infra (QANET) and Microsoft's semantic parsing work).

---

## Neighbors — *what lives nearby*
Classification is the input that [[Query Routing]] acts on — it sits upstream, filtering which handler gets invoked. Both [[Query Intent Classification]] and [[Prompt Engineering]] shape how a question is interpreted, just at different stages.

## Clash — *what pushes against this*
The opposite approach is [[RAG Query|treating every question identically as a retrieval query]], with no classification step to distinguish between easy lookups and questions that need synthesis.

## Roots — *where this comes from*
This concept belongs to [[Selective LLM Usage]], which rests on the insight that classification enables choosing the cheapest capable path instead of reaching for a powerful model for every question.

## Paths — *where this leads*
Once intent is clear, [[Co-reference Resolution]] can rewrite follow-up questions appropriately for retrieval, using the context that classification provided.
