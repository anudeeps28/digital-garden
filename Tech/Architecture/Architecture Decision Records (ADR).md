---
type: atomic
tags: [coding/architecture, coding/patterns, devops]
date: 2026-10-01
---

# Architecture Decision Records (ADR)

## Idea
Code shows *what* was built, never *why*. An ADR is a short note written when a decision is made, so the next person can see the reasons before undoing it.

## Definition
An **Architecture Decision Record** is a short document, often one page, that captures one significant decision. It has four parts. **Context** covers the forces and constraints at the time. **Decision** states what was chosen, in plain words. **Status** is proposed, accepted, deprecated or superseded. **Consequences** lists what gets easier, what gets harder and what is now ruled out. ADRs are numbered in order and stored as Markdown in the repository next to the code they describe (commonly `docs/adr/`), so they're reviewed in pull requests and versioned with everything else. The key rule: once accepted, an ADR is **immutable**. If the decision changes, you don't edit the old record. You write a new one that **supersedes** it and mark the old one's status, so the history of reasoning survives. That's the point. A future teammate who finds an odd choice can learn whether it was deliberate, what it traded away and whether its assumptions still hold, rather than guessing or "fixing" something that was intentional. The common failure is writing them after the fact or not at all, leaving a folder that covers three decisions out of thirty.

## Providers
- **Formats** — Nygard's original template, MADR (Markdown Architectural Decision Records) and Y-statements.
- **Tooling** — adr-tools (shell scripts to create, number and supersede records) and Log4brains (publishes ADRs as a browsable site).
- **Platforms** — the Backstage ADR plugin surfaces records in a developer portal. GitHub and Azure DevOps repos and wikis host them alongside code.
- **Cloud guidance** — the AWS Prescriptive Guidance, Azure Well-Architected Framework and Google Cloud Architecture Center all recommend keeping ADRs.

## Source
Michael Nygard, "Documenting Architecture Decisions" (Cognitect blog, 2011). Later popularised by the ThoughtWorks Technology Radar.

---

## Compass

**Roots** — *where this comes from*
It's [[Record the Reason, Not Just the Blocker]] applied to design: a decision without its reason looks identical to an accident.

**Paths** — *where this leads*
Kept in the repo, ADRs become the [[Single Source of Truth]] for why the system is shaped the way it is, and they get reviewed through the same [[Pull Request]] flow as code.

**Neighbors** — *what lives nearby*
[[Optimize for Future Teammates Reading Your History]] is the same instinct applied to commits. [[Writing Is Thinking]] explains why drafting the record often changes the decision. [[Define Contract Before Implementation]] is another way of settling things in writing first.

**Clash** — *what pushes against this*
They cost time when time feels scarce, and they decay into ceremony if every small choice gets one. An ADR that nobody updates when reality drifts becomes a confidently wrong record. See [[A Stale Source Is Confidently Wrong]].
