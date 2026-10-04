---
type: atomic
tags: [coding/architecture, coding/quality, workflow]
date: 2026-10-04
---

# Documentation Drift

## Idea
Documentation drift is when docs slowly stop describing the system they claim to describe. Drifted docs are worse than missing ones, because they still look authoritative.

## Definition
Code changes in one place and docs live in another, so every change that skips the docs widens the gap a little. Nobody decides to let docs rot; they just stop being updated in the same motion as the code. The dangerous form is **contradiction**: two documents disagree, and a reader (human or AI agent) picks whichever they read first. A concrete case: two planning docs named different models for the same job. Nobody noticed until work started, and resolving it took a proper decision record. The lasting fix wasn't more care but **automation**. A pre-commit style hook now checks docs against the recorded technology choices and **blocks** a change that contradicts them, so drift is caught at the moment it is introduced rather than months later. More general defences: keep docs in the same repository as the code and update them in the same pull request ("docs as code"), generate reference docs from the code where possible, keep one canonical home for each fact and link to it instead of restating it, and mark every doc with what it is (a decision at a point in time, or a description of now).

## Tools
- **Docs-as-code toolchains** — Markdown in the repo, reviewed in pull requests, built in CI.
- **OpenAPI generators** — produce API reference straight from the code so it can't drift.
- **Doc linters and drift checkers** — CI checks that flag docs whose anchored code changed.

## Source
No single coiner; the problem is long known as "documentation rot". The **docs-as-code** movement, popularised by the Write the Docs community in the 2010s and Anne Gentle's *Docs Like Code* (2017), is the main structural response.

---

## Compass

**Roots** — *where this comes from*
It is what happens when there is no [[Single Source of Truth]] for a fact, and [[A Stale Source Is Confidently Wrong]] explains why it misleads rather than merely annoys.

**Paths** — *where this leads*
Checking docs automatically against recorded choices is a [[Fitness Functions|fitness function]] for documentation, and AI tools can enforce it at commit time through [[Agent Hooks]].

**Neighbors** — *what lives nearby*
[[Architecture Decision Records (ADR)]] resist drift by being dated and immutable, while a [[Ubiquitous Language]] glossary must be kept current. [[Swagger and OpenAPI]] avoids the problem by generating docs from code.

**Clash** — *what pushes against this*
Strict checks make doc changes a gate on every commit, and teams under pressure may respond by writing less documentation rather than keeping it accurate. Not every doc deserves that rigour; dated notes can be allowed to age honestly.
