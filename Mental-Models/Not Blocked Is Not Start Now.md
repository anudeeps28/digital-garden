---
type: atomic
tags: [mental-model, workflow, ai/agents]
date: 2026-10-04
---

# Not Blocked Is Not Start Now

## Idea
A precondition being met is not a trigger. "Nothing stops this from running" is a different statement from "this should run now."

## Definition
Systems that start work automatically usually check whether a task *can* run: its dependencies are done, nothing is locked, the inputs exist. It is easy to let that check stand in for whether the task *should* run, and the two come apart badly at scale. A worked example: an autopilot designed to pick up ready work was switched on for the first time against a backlog of more than twenty items. Every item was technically unblocked, so it launched a builder for all of them at once, burning budget and producing a pile of half-wanted changes nobody had asked for yet. The fix was not a smarter readiness check. It was removing the "runs by itself" behaviour entirely and acting only on an **explicit human queue**: work starts when someone puts it in the queue, and the readiness check only decides whether queued work can proceed. Separating the *precondition* (can it?) from the *trigger* (has someone said go?) keeps automation from inventing its own priorities.

## Source
The idea mirrors the **pull system** at the heart of the Toyota Production System (Taiichi Ohno, 1950s to 1970s), where work is started by a downstream signal rather than by capacity being free, and its software form in David J. Anderson's *Kanban* (2010), where WIP limits stop teams from starting everything that is merely ready.

---

## Compass

**Roots** — *where this comes from*
It comes straight from [[Kanban]], where "pull, don't push" exists precisely because available work is not the same as wanted work.

**Paths** — *where this leads*
It leads to designs like the [[Needs-You Inbox]] and [[Propose, Don't Execute]], where an agent may prepare work but a human signal starts it, and to [[Backpressure]] as the system-level guard against starting too much.

**Neighbors** — *what lives nearby*
[[The Exit Condition]] is its twin at the other end of a task: knowing when to stop matters as much as knowing when to start. [[Validate Before You Automate]] makes the same point about schedules.

**Clash** — *what pushes against this*
Requiring a human to start everything recreates the bottleneck automation was meant to remove, and [[Delay Is Capacity Catching Up]] reminds that some waiting is just queueing, not judgement.
