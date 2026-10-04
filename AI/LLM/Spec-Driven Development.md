---
type: atomic
tags: [ai/agents, workflow, coding/architecture]
date: 2026-10-04
---

# Spec-Driven Development

## Idea
Write the spec until no decisions remain open, then let the coding agent implement it, because an agent fills every gap you leave with a guess.

## Definition
In **spec-driven development**, the specification is the primary artifact and code is generated from it. With coding agents this matters more than ever: a human developer asks when something is unclear, while an agent quietly improvises. A worked example uses four documents before any code: a **SPEC** (what and why), an **IMPLEMENTATION** plan (how, file by file), a **VERIFICATION** doc (how we will know it works) and an **OPERATIONS** doc (how it runs and fails in production). The gate to start coding is a single sentence that must be true: "no open decisions remain". The instructions to the agent then say plainly, "do not improvise mappings"; if a field mapping or edge case is not in the spec, stop and ask. The spec also gives a reviewer something concrete to check the output against.

## Tools
- **GitHub Spec Kit** — open-source CLI that adds a constitution, specify, plan, tasks and implement flow to existing coding agents.
- **Kiro** — an agentic IDE from AWS built around requirements, design and task documents.

## Source
GitHub released Spec Kit and its "spec-driven development with AI" post on 2 September 2025, and AWS had previewed Kiro that July; both popularised the term for agent workflows. The idea of executable specs is older, from design-by-contract to behaviour-driven development.

---

## Compass

**Roots** — *where this comes from*
It is [[Define Contract Before Implementation]] stretched to the whole feature, and it rests on [[Clarity In, Clarity Out]]: vague input to an agent produces confident, vague code.

**Paths** — *where this leads*
Before the spec is frozen, [[Grill the Plan]] hunts for the open decisions, and [[Explicit Non-Goals]] fence off what the agent should not touch.

**Neighbors** — *what lives nearby*
[[English Is the Programming Language]] is the bigger shift this belongs to, and [[Definition of Done]] is the VERIFICATION doc in miniature.

**Clash** — *what pushes against this*
Heavy specs can become waterfall in disguise, and they rot like any document through [[Documentation Drift]]. For small or exploratory changes, writing four documents costs more than the guesses it prevents.
