---
type: atomic
tags: [ai/llm, devops, coding/quality]
date: 2026-10-04
---

# Pin the Model Version

## Idea
Name the exact, dated model you depend on in one config value, the way you pin a library version, so its behaviour cannot change underneath you.

## Definition
Providers expose friendly **aliases** ("latest", a family name) that silently move to new models, and dated **snapshot IDs** that stay fixed until retired. Pinning means your code and docs refer to one exact snapshot ID, held in a single config value that an environment variable can override for experiments. A worked example: a project's documents had drifted between two variants of a model, some pages naming a preview build and others the generally available one, so nobody could say which model the evaluations were run against. The fix was to choose the exact GA model ID, put it in one setting, and record the choice in a decision record; any later change to the model writes a new record that supersedes the old one. Upgrading becomes a deliberate act with its own re-test, not a surprise.

## Source
Lingjiao Chen, Matei Zaharia and James Zou, "How is ChatGPT's behavior changing over time?" (2023), showed that the "same" GPT-4 service dropped from 84% to 51% on one task between March and June 2023. Major providers publish dated snapshot IDs alongside moving aliases for exactly this reason.

---

## Compass

**Roots** — *where this comes from*
It is dependency pinning applied to models, held in place by [[Runtime Config (Build Once Deploy Everywhere)]] so one setting controls every environment.

**Paths** — *where this leads*
Each pin and each change becomes an entry in [[Architecture Decision Records (ADR)]], and a pinned model is what makes [[LLM-as-a-Judge]] scores comparable across weeks.

**Neighbors** — *what lives nearby*
[[Judging AI on a Version That Is Gone]] is the reader-side version of the same problem, and [[Documentation Drift]] is how two model names ended up in the docs in the first place.

**Clash** — *what pushes against this*
Snapshots get deprecated, so a pin is a promise to revisit, not a way to stop thinking. Pinning also means you miss free improvements until you choose to upgrade.
