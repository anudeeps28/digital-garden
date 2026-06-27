---
type: atomic
tags: [ai, ai/llm]
date: 2026-06-26
---

# Confidence Score

## Idea
A confidence score is a 0-to-1 number the system attaches to an extraction or an answer, signaling how much it trusts the result.

## Definition
Every extracted field and every answer carries a confidence score so the system knows when to act automatically versus when to escalate. A high score means proceed; a low one means flag for [[Field Verification]] or send it to a human. In practice, confidence acts as a gatekeeper across the pipeline: automation only proceeds above a confidence threshold (e.g., 85%), and low-confidence outputs get routed to verification or human review. Treating confidence as a first-class signal lets the system lean on automation while keeping a safety net for the uncertain cases.

## Source
Uncertainty quantification in machine learning; formalized through work on model calibration (Guo et al., "On Calibration of Modern Neural Networks," ICML 2017) and Bayesian inference. Industry practice for quality gates in production AI systems.

---

## Neighbors — *what lives nearby*
[[Field Verification]] works in tandem with confidence scores, triggering automatically when the score falls below a trusted threshold. [[Self-Learning Templates]] gates deployment on confidence thresholds, ensuring that extractions only proceed automatically when uncertainty is acceptably low.

## Clash — *what pushes against this*
[[Selective LLM Usage]] represents the opposite signal: high confidence means you can skip the LLM entirely and rely on simpler extraction methods, whereas confidence scoring is all about knowing when you *need* that expensive verification.

## Roots — *where this comes from*
Confidence scores grow out of uncertainty quantification, rooted in Bayesian inference and extended through modern deep learning calibration research. They measure how much a model trusts its own output.

## Paths — *where this leads*
Low confidence routes uncertain results to verification or human review, while high confidence unlocks automation. This creates a quality gate that balances speed (high-confidence auto-processing) with safety (low-confidence escalation).
