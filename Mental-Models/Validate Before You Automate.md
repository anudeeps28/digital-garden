---
type: atomic
tags: [mental-model, workflow, devops]
date: 2026-10-04
---

# Validate Before You Automate

## Idea
Keep a new workflow on a manual trigger until it has proved it is useful; automating something before you know it's worth doing is premature.

## Definition
Scheduling a job feels like progress, but it locks in a guess. Once a workflow runs by itself, nobody looks at whether its output is read, acted on, or even correct, and its cost becomes invisible background noise. **Validating first** means running the thing by hand, on purpose, a handful of times. Each manual run is a small experiment that answers questions automation hides: did I actually use the result, what did I have to fix by hand, how often did I genuinely need it? Only when the answers are stable does it earn a schedule. For example, a daily digest designed to run every morning can be kept on a button instead; if after two weeks it has only been pressed a few times, the right cadence is weekly, and a month of unread daily output has been avoided.

## Source
The time side of the tradeoff is captured by Randall Munroe's xkcd #1205, "Is It Worth the Time?" (April 2013), a table of how long you can spend automating a task before it costs more than it saves. The usefulness side echoes a line widely attributed to Bill Gates: automation applied to an inefficient operation magnifies the inefficiency.

---

## Compass

**Roots** — *where this comes from*
This is [[First Make It Work, Then Make It Better]] with a step inserted in the middle: make it work, then make sure it matters, then make it automatic.

**Paths** — *where this leads*
A workflow that survives manual validation is a strong candidate to [[Turn Repeated Work Into a Skill]] or put on a [[Cron]] schedule, because by then its inputs and its failure modes are known.

**Neighbors** — *what lives nearby*
[[Not Blocked Is Not Start Now]] is the same caution applied to triggers: something able to run is not a reason for it to run. [[Approve the Foundation Before Polish]] makes the same bet that early effort should go into checking direction, not adding finish.

**Clash** — *what pushes against this*
Manual steps get skipped, and some value only appears once something runs reliably without you, which is the whole point of [[Environment Design]]. Validation that never ends is just procrastination with a checklist.
