---
type: atomic
tags: [ai/llm, coding/testing, ai/vision]
date: 2026-10-04
---

# LLM-as-a-Judge

## Idea
When "good" cannot be checked by an exact rule, ask a capable model to score the output against a rubric and use that score as the gate.

## Definition
Many AI outputs (a summary, an image, a design) have no single right answer, so ordinary assertions cannot test them. **LLM-as-a-judge** hands the output and a rubric to a strong model and asks for a score plus a written critique. The critique is as useful as the number, because it tells the generator what to fix on the next attempt. A worked example: an image-critique tool sends each draft to a vision model, which returns a 0-100 score and specific feedback; a per-user threshold (90 by default) defines "done", and the loop keeps revising until the score clears it. The honest caveat is that the same image can score 86 on one run and 91 on the next, so the threshold is a fuzzy line, not a precise one. Good practice: use a different model from the generator, keep the rubric explicit, and spot-check judge scores against human ones.

## Source
Lianmin Zheng et al., "Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena" (NeurIPS 2023), found GPT-4 agreed with human preferences over 80% of the time, about as often as humans agree with each other. It also documented the judge's biases: position, verbosity and self-enhancement.

---

## Compass

**Roots** — *where this comes from*
It is a probabilistic [[Test Oracle]]: something has to decide pass or fail, and when no rule can, a model becomes the oracle.

**Paths** — *where this leads*
The score works like a [[Confidence Score]] that gates a loop, and the loop needs [[The Exit Condition]] so a judge that never says yes does not run forever.

**Neighbors** — *what lives nearby*
[[Never Grade Your Own Homework]] explains why the judge should be separate from the generator, and [[Report the Outcome, Not the Metric]] is a reminder that the score is a proxy.

**Clash** — *what pushes against this*
[[Sycophancy]] and self-preference bias pull judges toward approving whatever they are shown, and run-to-run variance means a fixed threshold can flip on noise. A judge also drifts when its model changes, which is why you [[Pin the Model Version]].
