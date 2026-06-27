---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Self-Learning Templates

## Idea
Self-learning templates let the system teach itself how to extract from a brand-new document type by generating, testing, and auto-deploying its own extraction rules.

## Definition
When a document arrives that doesn't match any known template, an LLM generates a candidate set of extraction rules for it, then self-tests those rules against the source document to see how well they pull the right fields. If the result clears an 85% [[Confidence Score]] threshold, the template is auto-deployed; below that, it's held for human review. In the project this is what lets [[Template-Based Extraction]] scale to new health-plan formats without an engineer hand-writing rules each time. It's a tight, self-correcting loop — generate, verify, gate — and a step toward more [[Agentic RAG Evolution|agentic]] behavior where the system improves its own tooling.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
[[Template-Based Extraction]] generates the rules that self-learning templates produce as their output, creating a direct dependency between the two. Both [[Template-Based Extraction]] and self-learning templates rely on [[Field Verification]] as a gating mechanism to ensure quality before committing to results.

## Clash — *what pushes against this*
[[Selective LLM Usage]] represents the opposite approach—it conserves LLM effort by minimizing use, whereas self-learning templates spend LLM effort upfront to avoid the manual work of rule-writing.

## Roots — *where this comes from*
The [[Confidence Score]] framework underpins the deployment decision; the 85% threshold is what determines whether a self-learned template gets automatically deployed or held for human review.

## Paths — *where this leads*
Self-learning templates are a concrete step toward [[Agentic RAG Evolution]], where systems don't just answer questions but actively improve their own extraction tooling and capabilities.
