---
type: atomic
tags: [ai/llm, kba]
date: 2026-03-24
---

# Template-Based Extraction

## Idea
Template-based extraction uses a fixed JSON template plus an AI model to pull structured data from unstructured documents automatically.

## Definition
Instead of manually reading a plan document and typing out benefit details, template-based extraction gives the [[LLM (Large Language Model)|LLM]] a JSON schema (the template) that defines which fields to extract — like deductible amounts, copays, coinsurance percentages, and coverage limits. The model reads the document chunks and fills in the template with the correct values. In the project, this powers automated benefit extraction: a plan document goes in, and structured [[JSON]] data comes out. The template acts as both the instruction and the output format, sent to [[Azure OpenAI]] as part of the [[Prompt Engineering|prompt]]. This replaces hours of manual data entry.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*

[[Named Entity Recognition]] is the traditional NLP approach to extracting structured data, while [[Form Recognition]] services like Azure's handle extracting data from forms and invoices similarly.

## Clash — *what pushes against this*

[[Manual Data Entry]] represents the opposite workflow where humans read documents and type values manually, and [[Free-Form Q&A]] contrasts with extracting specific fields by asking unstructured questions instead.

## Roots — *where this comes from*

[[RAG (Retrieval-Augmented Generation)]] uses similar retrieval mechanisms but applies them to extraction rather than Q&A, and the [[LLM (Large Language Model)]] itself is the AI model that performs the extraction.

## Paths — *where this leads*

The extracted data is output as structured [[JSON]], sourced from [[Plan Document|plan documents]], capturing specific [[Benefits]] fields like deductible and copay amounts that become [[Metadata]] stored in [[Azure SQL]].
