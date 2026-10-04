---
type: atomic
tags: [devops, workflow, learning, framework]
date: 2026-10-04
---

# Postmortem

## Idea
After something goes wrong (or a piece of work finishes), write down what happened and change the system so it cannot happen the same way again, without blaming people.

## Definition
A postmortem is a short written review after an incident: a timeline, the impact, the contributing causes, and concrete follow-up actions with owners. The **blameless** part is essential. It assumes people acted reasonably given what they knew, and asks why the system let a reasonable action cause harm, because punishing individuals just teaches everyone to hide mistakes. The output that matters is not the document but the changes: alerts added, defaults changed, a check automated. The same habit works at the end of any project as a quick **finalize ritual**: what surprised you, what would you change next time, and which lessons should become rules. A strong version proposes **writebacks** to the team's standards files (checklists, templates, coding rules) as concrete diffs that someone must approve, so lessons land in the place people will actually see them next time rather than in a forgotten report.

## Source
Popularised in software by John Allspaw's "Blameless PostMortems and a Just Culture" (Etsy, 2012) and the Google SRE book (Beyer et al., 2016, chapter "Postmortem Culture"). The roots lie in aviation and healthcare safety work on just culture (Sidney Dekker).

---

## Compass

**Roots** — *where this comes from*
It rests on [[Errare Humanum Est]]: mistakes are inevitable, so the system should absorb them. It is [[Kaizen]] applied to failures.

**Paths** — *where this leads*
The point is to [[Codify Lessons Into Defaults]], turning each finding into a check, template or rule, and recording the big decisions as [[Architecture Decision Records (ADR)]].

**Neighbors** — *what lives nearby*
[[Silent Failure]] is a common root cause it uncovers, and [[Blast Radius]] is a common question it asks.

**Clash** — *what pushes against this*
Postmortems that produce documents but no changes become ritual, and lessons kept only in prose suffer [[Documentation Drift]]. Blamelessness is also hard to keep when the incident was costly.
