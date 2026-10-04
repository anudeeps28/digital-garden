---
type: atomic
tags: [ai/agents, ai/llm, coding/architecture]
date: 2026-10-04
---

# Orchestrator-Subagent Pattern

## Idea
One lead agent plans the work, fans out narrow tasks to subagents with fresh context, and keeps the synthesis for itself.

## Definition
In the **orchestrator-subagent** pattern, a single orchestrator holds the goal and the plan. It breaks the job into pieces that do not need each other's context, spawns **subagents** to do them (often in parallel), receives only their compact results, and does the final reasoning itself. Subagents start clean, so a noisy fetch or a long file read never pollutes the orchestrator's context. A worked example: a weekly digest runs in six phases. For each reader it fans out three parallel fetch subagents (one per source type), deduplicates what comes back, synthesises the digest itself, then hands rendering to another subagent. The team considered a classic script calling an API on a cron schedule, but running it inside a flat-rate coding agent made the marginal cost close to zero and kept a human in the loop to glance at the output before it went out.

## Source
Anthropic, "Building effective agents" (Erik Schluntz and Barry Zhang, December 2024), names it the **orchestrator-workers** workflow: a central LLM dynamically breaks down a task, delegates to worker LLMs and synthesises their results. The shape echoes the much older manager-worker pattern in distributed computing.

---

## Compass

**Roots** — *where this comes from*
It is [[n8n Orchestrates AI Reasons]] moved one level up: the coordinating role becomes an agent itself, while workers stay narrow and replaceable.

**Paths** — *where this leads*
Once workers are separate, [[Model Tiering]] lets them run on cheaper models, and [[File-Based Handoffs]] let their results survive outside any one context window.

**Neighbors** — *what lives nearby*
[[Persona-Based Synthesis]] is a natural fit for the final step, since the orchestrator is the one place that sees every result at once. [[Separation of Concerns]] is the same instinct in ordinary code.

**Clash** — *what pushes against this*
Fan-out multiplies [[Tokens]] spent and adds coordination bugs, so for a task one agent can finish in a single pass, the orchestration is overhead. Subagents also lose nuance the orchestrator never wrote down in their brief.
