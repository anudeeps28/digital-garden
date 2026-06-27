---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Confidence Score

## Idea
A confidence score is a 0-to-1 number the system attaches to an extraction or an answer, signaling how much it trusts the result.

## Definition
Every extracted field and every RAG answer carries a confidence score so the system knows when to act automatically versus when to escalate. A high score means proceed; a low one means flag for [[Field Verification]] by the cheap gpt-4.1-nano model or send it to a human. In the project this number is the gatekeeper across the pipeline: [[Self-Learning Templates]] only auto-deploy above an 85% confidence threshold, and low-confidence [[Template-Based Extraction]] outputs get double-checked. Treating confidence as a first-class signal is what lets the system lean on automation while keeping a safety net for the uncertain cases.

## Source
AI document ingestion project

---

## Neighbors — *what lives nearby*
[[Field Verification]] works in tandem with confidence scores, kicking in automatically when the score is too low to trust. [[Self-Learning Templates]] gates their auto-deployment on a confidence threshold, so the system only rolls out templates when it's sufficiently certain about the extraction.

## Clash — *what pushes against this*
[[Selective LLM Usage]] represents the opposite signal: high confidence means you can skip the LLM entirely and rely on simpler extraction methods, whereas confidence scoring is all about knowing when you *need* that expensive verification.

## Roots — *where this comes from*
Confidence scores are fundamentally about rating the reliability of [[Template-Based Extraction]]—the technique that powers the extractions that the score wraps around.

## Paths — *where this leads*
Low confidence routes [[Field Verification]] to double-check the extracted field, and it determines whether [[Self-Learning Templates]] can safely auto-deploy or whether escalation to a human is necessary.
