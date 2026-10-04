---
type: atomic
tags: [ai/agents, workflow, framework]
date: 2026-10-04
---

# Agent Harness

## Idea
An agent is a model plus a harness; the harness is everything you build around the model so it behaves the same way every time.

## Definition
The **harness** is the scaffolding around a coding agent: instructions and rules files, reusable **skills**, **subagents** for narrow jobs, **hooks** that run deterministic scripts at fixed moments, templates for plans and reports, and the workflow that strings them together. A worked example of a personal harness runs every task through the same stages: understand, plan, execute, evaluate, then open a pull request, with a human approval gate after the plan and before the merge. Its own description sums it up: "not an autonomous agent, a supervised one". The model provides the intelligence, but the harness provides the consistency: it decides what context the model sees, which actions are allowed, where work is written down, and when a person must look. Improving the harness after each mistake is how the same model gets steadily more reliable on your work.

## Source
"Agent harness" (also "agent scaffolding") circulated among practitioners through 2025, summed up as *agent = model + harness*. The phrase "harness engineering" spread in early 2026, with attribution contested between a Mitchell Hashimoto blog post and LangChain's "Anatomy of an Agent Harness"; Anthropic's "Effective harnesses for long-running agents" (November 2025) is a widely cited reference.

---

## Compass

**Roots** — *where this comes from*
It grows out of [[Turn Repeated Work Into a Skill]]: each repeated instruction becomes a reusable part of the harness instead of a prompt you retype.

**Paths** — *where this leads*
Its enforcement layer is [[Agent Hooks]], its memory is [[File-Based Handoffs]], and its review stage applies [[Never Grade Your Own Homework]].

**Neighbors** — *what lives nearby*
[[Codify Lessons Into Defaults]] is the habit that keeps a harness improving, and [[Pre-deploy Approvals]] are the CI-world version of its human gates.

**Clash** — *what pushes against this*
A harness can grow into its own unmaintained codebase, and heavy process slows small tasks. Model upgrades can also make yesterday's careful workarounds unnecessary, so parts of the harness need pruning, not just adding.
