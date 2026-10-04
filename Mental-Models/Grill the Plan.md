---
type: atomic
tags: [mental-model, framework, workflow, ai/agents]
date: 2026-10-04
---

# Grill the Plan

## Idea
Before building anything, have the plan questioned hard on every open design fork until each one has a decision and a stated tradeoff.

## Definition
A plan feels finished long before it is. The gaps hide in the forks nobody has looked at yet: which of two storage options, what happens on the empty state, who owns the retry. **Grilling the plan** means sitting through a deliberate interrogation, from a colleague or an AI, that walks the design tree one branch at a time and refuses to move on until the branch is resolved. The output is a small table with three columns (question, decision, key tradeoff), and each settled row is marked *locked, do not re-litigate*. That last part matters as much as the questions. Without it the same fork gets reopened in every later conversation, and the plan quietly dissolves back into options. A typical result: a plan that felt settled turns out to contain a dozen or more open forks, most of which had been silently assumed, and sometimes assumed differently in different parts of the draft.

## Source
The practice descends from Gary Klein's **premortem** ("Performing a Project Premortem", *Harvard Business Review*, September 2007), which imagines the project has already failed and asks why. It was popularised for AI-assisted coding by Matt Pocock's "grill me" agent skill, whose prompt is roughly "interview me relentlessly about every aspect of this plan until we reach a shared understanding", resolving each branch of the decision tree one question at a time.

---

## Compass

**Roots** — *where this comes from*
It grows out of [[Writing Is Thinking]]: a decision you cannot write down as a row with a tradeoff is a decision you have not really made yet. It also inverts the usual direction of prompting, the same move as [[Ask It to Ask You]], where the model interviews you instead of you instructing it.

**Paths** — *where this leads*
A locked decision table is the natural input to [[Spec-Driven Development]], and the tradeoff column is half of an [[Architecture Decision Records (ADR)|architecture decision record]] already written.

**Neighbors** — *what lives nearby*
[[Define Contract Before Implementation]] does the same thing for interfaces, settling shape before code. [[One-Way and Two-Way Doors]] helps decide which forks deserve a hard grilling and which can be answered quickly.

**Clash** — *what pushes against this*
Some forks only resolve by building, and [[Managing Ambiguity]] argues for moving forward without every answer. Grilling past the point of real information turns into speculation dressed as rigour.
