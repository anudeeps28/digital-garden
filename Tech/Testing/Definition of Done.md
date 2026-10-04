---
type: atomic
tags: [coding/testing, workflow, framework]
date: 2026-10-04
---

# Definition of Done

## Idea
"Done" is a shared, explicit checklist that work must pass before it counts as finished, not a feeling that the code seems to work.

## Definition
The Definition of Done is the quality bar every piece of work must meet before it is called complete. Without one, "done" means different things to different people: written, or tested, or deployed, or verified by a user. A useful version is short and checkable. **Done means the goal is met**, not just that the tasks were completed. The **acceptance criteria are the end-to-end gate**: each one is stated up front, and each has a chosen way to be verified (an automated test, a field check, a screenshot comparison, or a named human sign-off). That last part matters most for features with no easy [[Test Oracle]], like AI output or visual design. The rule is that **no-oracle features are still gated, never skipped**: if no test can judge them, a person must explicitly approve them, and that approval is part of done. Agreeing the verification method before building also sharpens the criteria themselves, because a criterion nobody can check is usually a vague one.

## Source
From Scrum: early Scrum training around 2003-2005 introduced "definition of done" exercises, following Bill Wake's 2002 writing on what "done" means; it is a formal commitment for the Increment in the Scrum Guide (Ken Schwaber and Jeff Sutherland, made explicit in the 2020 edition).

---

## Compass

**Roots** — *where this comes from*
It comes from Scrum and agile practice, close to [[Define Contract Before Implementation]]: decide what success looks like before building.

**Paths** — *where this leads*
Each criterion needs a [[Test Oracle]], automated through [[Playwright]] or [[Field Verification]] where possible, and [[Spec-Driven Development]] writes these criteria down before code.

**Neighbors** — *what lives nearby*
[[The Exit Condition]] asks the same question of any task, and [[Explicit Non-Goals]] says what done deliberately excludes.

**Clash** — *what pushes against this*
A long checklist becomes box-ticking, and under deadline pressure teams quietly redefine done, which is why a [[Code Coverage Gate]] or similar automated gate is harder to fudge than a document.
