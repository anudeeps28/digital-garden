---
type: atomic
tags: [coding/testing, ai/llm, coding/quality]
date: 2026-10-04
---

# Test Oracle

## Idea
A test is only as good as whatever decides whether the output is correct, and some outputs have no such judge at all.

## Definition
A **test oracle** is the mechanism that tells you whether a program's output is right: an expected value in an assertion, a reference implementation, a property that must hold, or a human looking at it. Most of the time it is so obvious we forget it exists (`add(2, 2)` must be 4). The **oracle problem** is what happens when there is no cheap, reliable judge. AI outputs are the modern case: a summary, a rewrite or a generated image has no single correct answer, so `assertEqual` is meaningless. So are matters of visual taste, like whether a layout looks right. The options are to use **partial oracles** (properties that must hold: valid JSON, under N words, mentions the key facts), **graded evaluation** against a rubric by a model or a person, comparison against previous outputs, or **explicit human sign-off**. When three visual prototypes were judged, the oracle was simply opening them side by side and choosing by eye, and naming that step as the check made it a real gate rather than an afterthought.

## Source
The term comes from William Howden, "Theoretical and Empirical Studies of Program Testing" (1978); Elaine Weyuker's "On Testing Non-Testable Programs" (1982) framed the oracle problem. Surveyed by Barr, Harman et al. in "The Oracle Problem in Software Testing" (IEEE TSE, 2015).

---

## Compass

**Roots** — *where this comes from*
It underlies every assertion in [[Unit Tests]]; a test without a real oracle becomes a [[Vacuous Test]] that passes no matter what.

**Paths** — *where this leads*
For AI output the usual automated oracle is [[LLM-as-a-Judge]], with [[Never Grade Your Own Homework]] as the guard against a model approving itself. Every feature should name its oracle in the [[Definition of Done]].

**Neighbors** — *what lives nearby*
[[Field Verification]] checks extracted values against the source, a narrow but reliable oracle, and [[Mutation Testing]] tests whether your oracles catch anything.

**Clash** — *what pushes against this*
Human judgement does not scale and drifts with mood, while [[Taste Is Earned Conviction]] argues some calls should stay human anyway. Automated judges can be confidently wrong.
