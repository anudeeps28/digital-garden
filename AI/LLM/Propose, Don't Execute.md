---
type: atomic
tags: [ai/agents, mental-model, workflow]
date: 2026-10-04
---

# Propose, Don't Execute

## Idea
When an agent's analysis says an action outside its brief is needed, it should write the action down as a proposal for a human, not carry it out.

## Definition
Agents reason their way to conclusions, and a confident conclusion feels like permission. **Propose, don't execute** separates the two: inside its brief an agent acts; outside it, especially where the brief explicitly says no, it emits a clearly labelled **PROPOSED ACTION** with the reasoning and stops. A worked example: several agent sessions ran in parallel, and one was told plainly "DO NOT move files in this folder". Its analysis concluded a file was misplaced, so it moved it anyway. The move turned out to be correct, which is exactly why the lesson is easy to miss. The problem was not the outcome but the precedent: an agent that overrides an explicit instruction whenever its reasoning disagrees is one that cannot be trusted with any instruction. The fix had two parts: the proposal convention for agents, and an orchestrator that snapshots the file tree before and after each session and diffs it, so any unrequested change is visible.

## Source
The idea maps to the levels of automation of Sheridan and Verplank (1978), where a system that "executes the suggestion if the human approves" sits below one that acts and merely informs. Anthropic's "Building effective agents" (2024) likewise recommends human checkpoints before consequential actions.

---

## Compass

**Roots** — *where this comes from*
It extends [[Read-Only by Default]] from data to authority: the narrowest permission is the default, and widening it is a human decision. [[Separation of Duties]] is why the proposer should not also be the approver.

**Paths** — *where this leads*
Proposals need somewhere to wait, which is the [[Needs-You Inbox]], and the before-and-after diff is a simple [[Write Ledger]] for agent sessions.

**Neighbors** — *what lives nearby*
[[A Draft, Not a Verdict]] treats AI output as something to review, and [[One-Way and Two-Way Doors]] says which actions most need a proposal: the ones you cannot undo.

**Clash** — *what pushes against this*
It slows autonomy and pushes work back to the human, which is the opposite of the [[Ralph Loop]]. Too many trivial proposals train people to approve without reading.
