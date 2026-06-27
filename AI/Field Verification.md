---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Field Verification

## Idea
Field verification uses a cheap second model to double-check low-confidence extracted fields by comparing the template's answer against an independent read.

## Definition
When [[Template-Based Extraction]] produces a field with a low [[Confidence Score]], the system doesn't just trust it — it asks the small, inexpensive gpt-4.1-nano model on [[Azure OpenAI]] to independently read the source and produce its own value. If the two agree, confidence rises; if they disagree, the field is flagged for human review. In the project this is the verification half of the pipeline's safety net, and it embodies [[Selective LLM Usage]]: a small model is spent only on the uncertain minority of fields, not on every extraction. It's cross-checking, not regeneration — cheap insurance against silent extraction errors.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
The [[Confidence Score]] is the trigger that decides which fields get verified, while [[Self-Learning Templates]] also employs a similar self-test/verify gate before trusting its output.

**Clash** — *what pushes against this*
[[Template-Based Extraction]] is the deterministic extraction process that verification audits and challenges.

**Roots** — *where this comes from*
This practice emerges from [[Selective LLM Usage]], the principle of spending the model only where confidence is low rather than on every field indiscriminately.

**Paths** — *where this leads*
The cheap nano model performing the independent read is an instance of [[LLM (Large Language Model)]] being deployed strategically for verification purposes.
