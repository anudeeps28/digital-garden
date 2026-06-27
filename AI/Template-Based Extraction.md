---
type: atomic
tags: [ai/llm]
date: 2026-03-24
---

# Template-Based Extraction

## Idea
Template-based extraction uses a fixed JSON template plus an AI model to pull structured data from unstructured documents automatically.

## Definition
Template-based extraction gives the [[LLM (Large Language Model)|LLM]] a JSON schema (the template) that defines which fields to extract. The model reads source documents and fills in the template with the correct values. The template acts as both the instruction and the output format, sent to the model as part of the [[Prompt Engineering|prompt]]. This approach converts unstructured text into structured [[JSON]] data automatically, replacing manual transcription work.

## Source
Emerged as a common pattern in [[Prompt Engineering|prompt engineering]] circa 2022–2023 with the rise of large language models (GPT-3.5, GPT-4) and structured output capabilities. Combines JSON Schema (formalized as a standard by the JSON Schema collaborative) with LLM instruction-following to extract data into predefined templates.

---

## Neighbors — *what lives nearby*

[[Named Entity Recognition]] is the traditional NLP approach to extracting structured data, while [[Form Recognition]] services like Azure's handle extracting data from forms and invoices similarly.

## Clash — *what pushes against this*

[[Manual Data Entry]] represents the opposite workflow where humans read documents and type values manually, and [[Free-Form Q&A]] contrasts with extracting specific fields by asking unstructured questions instead.

## Roots — *where this comes from*

[[RAG (Retrieval-Augmented Generation)]] uses similar retrieval mechanisms but applies them to extraction rather than Q&A, and the [[LLM (Large Language Model)]] itself is the AI model that performs the extraction.

## Paths — *where this leads*

The extracted data is output as structured [[JSON]], which can be stored in databases, piped into downstream processing, or integrated into larger systems. Template-based extraction unlocks automation wherever structured data needs to be pulled from unstructured sources.
