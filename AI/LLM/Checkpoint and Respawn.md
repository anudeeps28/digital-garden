---
type: atomic
tags: [ai/agents, ai/llm, workflow]
date: 2026-10-04
---

# Checkpoint and Respawn

## Idea
Keep an agent's state on disk at all times, and when its context fills up, end the session at a clean point and start a fresh one from the files rather than letting it summarise itself.

## Definition
Long agent sessions degrade: as the context window fills, the model attends less reliably to what matters, and automatic compaction squashes hours of work into a lossy summary written by the same tired session. **Checkpoint and respawn** avoids both. The plan, progress and decisions live in files the whole time, updated as work happens. When the session reaches about 80% of its context, it finishes the current step, writes a final checkpoint, and ends. A new session starts with an empty window and reads the files. Because the state was always external, nothing depends on a self-summary. There is also a circuit breaker: if a task needs more than about two resumes, that is a signal the task is too big, and it escalates with "split it" instead of resuming again.

## Source
Checkpoint and restart is a long-standing technique in high-performance computing. For LLMs, Chroma's "Context Rot" report (2025) measured accuracy falling as input grows across 18 models, well before windows are full, and Anthropic's "Effective harnesses for long-running agents" (November 2025) describes fresh sessions that rebuild context from a progress file and git log.

---

## Compass

**Roots** — *where this comes from*
It exists because context is a budget of [[Tokens]] that loses quality as it fills, not just a hard limit you hit at the end.

**Paths** — *where this leads*
It depends on [[File-Based Handoffs]] for the state itself, and [[Agent Hooks]] can force a checkpoint before compaction. The [[Ralph Loop]] takes the idea to its extreme: respawn after every single task.

**Neighbors** — *what lives nearby*
[[The Exit Condition]] is the cousin of the resume cap, and [[Persist Facts, Derive State]] is the same discipline in application data.

**Clash** — *what pushes against this*
A fresh session loses tacit understanding that never made it into a file, and rereading state costs tokens on every start. If the checkpoint files are sloppy, respawning amplifies the mess.
