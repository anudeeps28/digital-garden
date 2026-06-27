---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Field Verification

## Idea
Field verification uses a cheap second model to double-check low-confidence extracted fields by comparing the template's answer against an independent read.

## Definition
When [[Template-Based Extraction]] produces a field with a low [[Confidence Score]], the system doesn't just trust it — it uses a small, inexpensive secondary model to independently read the source and produce its own value. If the two agree, confidence rises; if they disagree, the field is flagged for human review. In practice, this serves as the verification half of a pipeline's safety net and embodies [[Selective LLM Usage]]: a smaller model is deployed only on the uncertain minority of fields, not on every extraction. It's cross-checking, not regeneration — cheap insurance against silent extraction errors.

## Source
Industry practice in AI/ML data pipelines; formalized as part of validation and quality assurance patterns in document processing and information extraction systems.

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
