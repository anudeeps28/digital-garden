---
type: atomic
tags: [ai/llm]
date: 2026-03-24
---

# Prompt Engineering

## Idea
Prompt engineering is the art of crafting instructions for an AI model — the system prompt sets behavior, and the user prompt asks the question.

## Definition
A prompt is the text input you send to an [[LLM (Large Language Model)|LLM]]. It typically has two parts: the **system prompt** (persistent instructions that define behavior, tone, and constraints — like "You are a health benefits assistant. Only answer from provided context.") and the **user prompt** (the actual question or task). In [[RAG (Retrieval-Augmented Generation)|RAG]], the prompt includes retrieved document chunks as context. In [[Template-Based Extraction]], the prompt includes a JSON schema and tells the model to extract matching fields. Good prompts are specific, provide examples, and set clear boundaries. Small changes in wording can dramatically affect output quality.

## Source
Emerged as a discipline with the rise of large language models (OpenAI GPT-2, 2019 onwards). Formalized through industry practice and research papers including "Prompting as a Programming Language" (Liang et al., 2023) and foundational work on prompt design techniques like Few-Shot Learning and Chain-of-Thought (Wei et al., 2022).

---

## Compass

**Neighbors** — *what lives nearby*
[[Few-Shot Learning]] works by including examples in the prompt to teach the model, while [[Chain-of-Thought]] asks the model to reason step by step — both are core techniques for improving prompt effectiveness.

**Clash** — *what pushes against this*
[[Zero Configuration]] systems work without any instructions, and [[Hardcoded Logic]] programs behavior directly in code instead of through natural language, representing opposing approaches to instruction delivery.

**Roots** — *where this comes from*
[[LLM (Large Language Model)]] are the foundation for prompt engineering since prompts are the primary interface to these models. A key open question is: how do you test and iterate on prompts systematically?

**Paths** — *where this leads*
Prompt engineering feeds directly into [[RAG (Retrieval-Augmented Generation)]], where retrieved chunks are injected into prompts, and into [[Template-Based Extraction]], where prompts instruct the model what to extract. It also has cost implications through [[Tokens]], since prompt length directly affects cost.
