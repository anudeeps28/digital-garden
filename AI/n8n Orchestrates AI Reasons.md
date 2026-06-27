---
type: atomic
tags: [ai/automation, mental-model, architecture]
date: 2026-02-23
---

# n8n Orchestrates, AI Reasons

## Idea
In AI automation, the orchestration tool handles all coordination while the AI handles only reasoning — never let the AI directly touch infrastructure.

## Definition
A separation-of-concerns principle: n8n (or any workflow orchestrator) owns routing, auth, validation, retries, logging, and approvals. The LLM owns reasoning, summarization, classification, and response drafting. AI never directly accesses databases or APIs — everything is routed through capability-constrained workflows.

## Source
KBA AI Automation Foundation Guide — [[Claude Code AI Automation Guide]]

---

## Compass

**Neighbors** — *what lives nearby*
The principle mirrors [[Separation of Concerns]] and the [[Single Responsibility Principle]], where each system owns a distinct domain and doesn't bleed into others' territory.

**Clash** — *what pushes against this*
This contrasts with Autonomous AI Agents, which operate under the assumption that AI can act directly without an orchestration layer, bypassing the gatekeeping and control structures.

**Roots** — *where this comes from*
This pattern roots in [[AI Automation Architecture]] and addresses a fundamental production question: How do you keep AI systems safe and auditable in production?

**Paths** — *where this leads*
Following this principle leads to [[Production-Ready Automation Checklist]] and the concept that [[CLAUDE.md is Guidance Hooks are Enforcement]] — every AI action is gated, logged, and reversible.
