---
type: atomic
tags: [ai/agents, workflow]
date: 2026-10-04
---

# Ralph Loop

## Idea
Run a coding agent headless in a loop against the same fixed prompt and a progress file, one task per iteration, with a fresh context every time.

## Definition
The **Ralph loop** is almost embarrassingly simple: a shell loop that feeds the same instructions to an agent over and over. Each iteration starts with an empty context, reads the requirements document (PRD or specs) and a progress or TODO file, picks the single most important unfinished item, does it, runs the tests, updates the progress file, commits, and exits. Then the loop starts it again. Because every iteration rebuilds its context from the same files, behaviour stays consistent even though the model is not deterministic. Practical versions add an **iteration cap** and a completion signal so the loop stops, and back pressure from tests, type checkers and linters so bad work fails fast instead of piling up.

```bash
for i in $(seq 1 30); do cat PROMPT.md | agent -p || break; done
```

## Source
Geoffrey Huntley, "Ralph Wiggum as a 'software engineer'" (blog post, July 2025), with the original form `while :; do cat PROMPT.md | claude-code ; done`. Named after the Simpsons character: naive, persistent and with no memory of the last scene.

---

## Compass

**Roots** — *where this comes from*
It is [[Checkpoint and Respawn]] taken to the limit, respawning after every task, and it needs [[File-Based Handoffs]] because the files are the only memory.

**Paths** — *where this leads*
Without [[The Exit Condition]] it burns money forever, and a sharp [[Spec-Driven Development]] document is what keeps each iteration pointed the same way.

**Neighbors** — *what lives nearby*
[[Fitness Functions]] and a [[Code Coverage Gate]] are the kind of back pressure that keeps the loop honest.

**Clash** — *what pushes against this*
It removes the human from every step, which clashes with [[Propose, Don't Execute]] and works poorly where judgment or taste matters. Each iteration also rereads everything, so costs add up fast on large repos.
