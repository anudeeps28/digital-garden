---
type: atomic
tags: [ai/llm]
date: 2026-03-24
---

# LLM (Large Language Model)

## Idea
An LLM is an AI model trained on massive text data that can read, understand, and generate human language — like GPT-4o.

## Definition
A Large Language Model is a neural network with billions of parameters trained on enormous text datasets. It processes input text as [[Tokens]], understands context and meaning, and generates coherent responses. LLMs can summarize, translate, answer questions, extract structured data, and more. In practice, LLMs are applied through [[RAG (Retrieval-Augmented Generation)|RAG]] to answer questions about documents grounded in real data, and through [[Template-Based Extraction]] to extract structured information from text. The model doesn't "know" your documents — it needs them provided as context through [[Prompt Engineering|prompts]].

## Source
OpenAI, *Language Models are Unsupervised Multitask Learners* (2019, GPT-2); Alec Radford et al. Foundational work building on transformer architecture; GPT-3 (Brown et al., 2020) demonstrated few-shot learning at scale, and GPT-4 (OpenAI, 2023) extended capabilities further.

---

## Compass

**Neighbors** — *what lives nearby*
[[Traditional NLP]] represents the older rule-based and statistical approach to language processing, while [[Search Engines]] also process text queries but return links instead of generating answers directly.

**Clash** — *what pushes against this*
[[Rule-Based Systems]] follow explicit programmed rules instead of learned patterns, and [[Deterministic Algorithms]] always produce the same output for the same input, in stark contrast to the probabilistic nature of LLMs.

**Roots** — *where this comes from*
[[Artificial Intelligence]] is the broader field that encompasses LLMs as one of its most significant subsets, and the central question driving their development is: how do you prevent LLMs from hallucinating (making up facts)?

**Paths** — *where this leads*
[[RAG (Retrieval-Augmented Generation)]] grounds LLMs in real documents to prevent hallucination, [[Prompt Engineering]] crafts the instructions that guide the LLM's behavior, and [[Tokens]] define how LLMs measure and process text.
