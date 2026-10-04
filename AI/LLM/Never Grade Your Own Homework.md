---
type: atomic
tags: [ai/agents, mental-model, coding/quality]
date: 2026-10-04
---

# Never Grade Your Own Homework

## Idea
The agent that wrote the work should not be the one that approves it; review needs a separate reviewer with a fresh context.

## Definition
An agent reviewing its own output carries all the assumptions that produced it, and models measurably prefer their own text. The fix is a **separate reviewer**: a fresh session that sees the plan and the diff but not the author's reasoning, and that only *reports* findings rather than editing code. Findings are graded, and only **BLOCK** findings fail the review; the rest are suggestions. Rework loops back to the author, capped at three rounds, after which the task escalates to a human instead of grinding on. A worked example of trimming: one workflow started with five role-based sessions (planner, architect, coder, tester, reviewer). Each cold start cost roughly five times the tokens with no visible gain in quality, so it collapsed to two, a builder and an independent reviewer. The only separation worth paying for was the one between making and judging.

## Source
Separation of duties is an old control principle in accounting and security. For models specifically, Zheng et al. (2023) documented self-enhancement bias in LLM judges, and Panickssery, Bowman and Feng, "LLM Evaluators Recognize and Favor Their Own Generations" (NeurIPS 2024), showed models score their own outputs higher than equally good ones from others.

---

## Compass

**Roots** — *where this comes from*
It is [[Separation of Duties]] applied to agents, and it guards against [[Sycophancy]] turned inward, where a model is too agreeable with itself.

**Paths** — *where this leads*
The reviewer's verdict usually lands on a [[Pull Request]], and when the reviewer is a model, [[LLM-as-a-Judge]] supplies the method and its known biases.

**Neighbors** — *what lives nearby*
[[A Draft, Not a Verdict]] treats the author's output as provisional, and [[The Exit Condition]] is why rework is capped rather than open-ended.

**Clash** — *what pushes against this*
Independence costs cold starts and tokens, so splitting into many roles quickly costs more than it catches. Two models from the same family may share blind spots, so "separate" is not always "independent".
