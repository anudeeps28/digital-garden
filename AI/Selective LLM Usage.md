---
type: atomic
tags: [ai, ai/llm, mental-model]
date: 2026-06-26
---

# Selective LLM Usage

## Idea
Selective LLM usage is the cost-discipline mindset of calling the LLM only where deterministic logic genuinely can't cope.

## Definition
LLM calls are powerful but expensive and slow, so the design principle is to reserve them for the hard cases and let cheap deterministic code handle the rest. In practice, this shows up as concrete budgets: the LLM is applied selectively, touching only a small fraction of workload volume while deterministic alternatives handle the majority through [[Template-Based Extraction]], fuzzy matching, and simple scoring heuristics. This is really a mental model more than a feature — it drives [[Query Routing]] and [[Field Verification]], where the question is always "can something cheaper do this correctly first?" before invoking a capable LLM.

## Source
Industry best practice; crystallized from production AI systems (2023–2024) as LLM API costs scaled. Core principle: use cheaper deterministic methods first, escalate to LLM only when needed. No single inventor; emerged organically from practitioners optimizing cost/latency tradeoffs in hybrid AI systems.

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
