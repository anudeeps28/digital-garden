---
type: atomic
tags: [ai, ai/llm, mental-model]
date: 2026-06-26
---

# Selective LLM Usage

## Idea
Selective LLM usage is the cost-discipline mindset of calling the LLM only where deterministic logic genuinely can't cope.

## Definition
LLM calls are powerful but expensive and slow, so the design principle is to reserve them for the hard cases and let cheap deterministic code handle the rest. In the KBA project this shows up as concrete budgets: the LLM touches only about 5% of extracted fields and 10-20% of queries, keeping spend near a ~$250/month target. The rest is handled by [[Template-Based Extraction]], [[Azure SQL]] lookups, and [[BM25 Scoring]]. This is really a mental model more than a feature — it drives [[Query Routing]] and [[Field Verification]], where the question is always "can something cheaper do this correctly first?" before reaching for GPT-4o on [[Azure OpenAI]].

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[Query Routing]] applies the same "cheapest capable path" logic to route requests efficiently, while [[Template-Based Extraction]] provides the deterministic alternative when you can avoid calling the LLM entirely.

**Clash** — *what pushes against this*
[[Response Enrichment]] deliberately adds more LLM calls rather than avoiding them, and [[Persona-Based Synthesis]] leans into LLM generation to craft specialized outputs.

**Roots** — *where this comes from*
This principle governs when to actually invoke an [[LLM (Large Language Model)]] — the deeper question is understanding what capabilities you truly need the model for versus what cheaper tools can handle.

**Paths** — *where this leads*
[[Field Verification]] builds on this approach by using a cheaper model only on the uncertain minority of fields, embodying the selective approach at a granular level.
