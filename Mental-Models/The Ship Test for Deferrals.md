---
type: atomic
tags: [mental-model, coding/quality, coding/testing, workflow]
date: 2026-10-04
---

# The Ship Test for Deferrals

## Idea
Before calling something "deferred", ask one question: does the change I'm shipping behave wrongly for its real, configured inputs? If yes, it's a blocker, not a deferral.

## Definition
"Deferred" is a comfortable word, and it hides two different failures. The first is **mislabelling**: a real defect in the shipped behaviour gets filed as a later improvement because fixing it is inconvenient. The **ship test** catches this by grounding the question in the actual configuration rather than the theoretical one. If the feature is configured for three regions and breaks in one of them, that is not an edge case for later. The second failure is **evaporation**: a genuine deferral is mentioned in a pull request description, the PR merges, and the note is never seen again. The fix is to register every real deferral in the tracker, where it has an owner and a status, not in prose that scrolls away. One trap sits under both: "the tests pass" is not evidence, because test fixtures can encode the very defect being deferred. A fixture written to match current behaviour will happily approve a bug.

## Source
The underlying concept is Ward Cunningham's **technical debt** ("The WyCash Portfolio Management System", OOPSLA 1992), where a little debt speeds development only "so long as it is paid back promptly". The ship test is a practical gate for telling acceptable debt from a shipped defect; it is a synthesis rather than a named method.

---

## Compass

**Roots** — *where this comes from*
It is the companion of [[Record the Reason, Not Just the Blocker]]: that note makes deferrals legible, and this one makes sure the thing being deferred is legitimately deferrable. A clear [[Definition of Done]] is what the ship test checks against.

**Paths** — *where this leads*
Taking the test seriously pushes teams toward an independent [[Test Oracle]] and toward [[Mutation Testing]], which can reveal fixtures that would pass no matter what.

**Neighbors** — *what lives nearby*
[[Vacuous Test]] is the exact trap behind "tests pass", and [[The Merge Is What Gets Tested]] makes the same insistence on judging what actually ships.

**Clash** — *what pushes against this*
Strictly applied, every imperfection starts to look like a blocker and nothing ships. [[First Make It Work, Then Make It Better]] is the reminder that the test is about *wrong* behaviour, not merely unfinished behaviour.
