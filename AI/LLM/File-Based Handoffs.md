---
type: atomic
tags: [ai/agents, workflow, coding/architecture]
date: 2026-10-04
---

# File-Based Handoffs

## Idea
Agent phases and parallel sessions should pass work to each other by writing files, not by relying on what is in a chat context.

## Definition
A **file-based handoff** means each phase ends by writing an artifact the next phase reads: a brief, a plan, a state file, an evaluation report. The context window is treated as scratch space; the files are the record. This does three things. It survives restarts and compaction, so a fresh session can pick up exactly where the last one stopped. It prevents **goal drift**, because each phase reads the original brief rather than a chain of paraphrases. And it makes evaluation possible: a reviewer can compare what was built against the plan file instead of against the builder's own account. Parallel sessions work the same way: they never message each other; one writes a file, another reads it. A short, fixed set of artifact names (BRIEF, PLAN, STATE, EVAL) makes the flow easy to follow and easy to automate.

## Source
The shared-workspace idea goes back to the **blackboard architecture** of the Hearsay-II speech system (1970s), where independent modules cooperated only through a common data store. Anthropic's "Effective harnesses for long-running agents" (November 2025) applies it with a progress file, a feature list and git history that each new session reads.

---

## Compass

**Roots** — *where this comes from*
It applies [[Single Source of Truth]] to agent work: the plan file, not anyone's memory of the conversation, is what counts.

**Paths** — *where this leads*
It is the foundation of [[Checkpoint and Respawn]] and the [[Ralph Loop]], and it gives [[Never Grade Your Own Homework]] reviewers a plan to check against.

**Neighbors** — *what lives nearby*
[[Git Worktree per Task]] gives each parallel session its own files to write, and [[Writing Is Thinking]] explains why being forced to write a plan improves it.

**Clash** — *what pushes against this*
Files go stale like any documentation, so [[Documentation Drift]] can leave a respawned agent following an outdated plan. Writing and rereading artifacts also costs tokens and time on small tasks that would fit in one session.
