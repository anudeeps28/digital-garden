---
type: atomic
tags: [ai/llm, ai/agents, framework]
date: 2026-10-04
---

# Model Tiering

## Idea
Give each step of an AI pipeline the cheapest model that can do it well, and save the strongest model for the steps where judgment is the actual product.

## Definition
Most LLM pipelines mix two kinds of work. **Mechanical** steps (fetching pages, reformatting JSON, extracting fields, rendering a template) have a clear right answer and a small model handles them fine. **Judgment** steps (deciding what matters, synthesising a point of view, ranking ideas) are where quality differences between models actually show. Model tiering assigns a tier per step instead of one model for the whole run. A weekly research digest is a good worked example: small, fast subagents fetch and clean sources in parallel, a mid-tier model renders the final document, and only the synthesis step that decides what the digest *says* runs on the top model, because synthesis needs taste. The result is most of the quality for a fraction of the cost and latency. The rule of thumb: if you could write a unit test that fully checks the output, the step probably does not need the best model.

## Source
Lingjiao Chen, Matei Zaharia and James Zou, "FrugalGPT" (Stanford, 2023), showed that cascading cheaper models before expensive ones could match the best model at a large cost reduction. Anthropic's "Building effective agents" (December 2024) describes the related **routing** workflow, sending easy requests to smaller models.

---

## Compass

**Roots** — *where this comes from*
It is a finer-grained version of [[Selective LLM Usage]]: that note asks whether a step needs an LLM at all, and tiering asks which one. Both come from treating [[Tokens]] as a real budget rather than a free resource.

**Paths** — *where this leads*
Tiering pairs naturally with the [[Orchestrator-Subagent Pattern]], where a strong orchestrator keeps the judgment and hands cheap, parallel chores to lighter subagents.

**Neighbors** — *what lives nearby*
[[Selective Intelligence]] makes the same argument about where to spend attention, and [[Open Weights vs Closed Models]] widens the menu, since a small local model can be the bottom tier.

**Clash** — *what pushes against this*
Every extra model is another version to pin and another failure mode to test, so [[Pin the Model Version]] gets harder. And a misjudged "mechanical" step can quietly degrade quality, which only shows up if something like [[LLM-as-a-Judge]] is checking the end result.
