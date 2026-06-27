---
type: atomic
tags: [mental-model, security, governance]
date: 2026-04-24
---

# Separation of Duties

## Idea
No single person should be able to both *make* a sensitive change and *approve* it — split the authority across roles so no individual can act unilaterally.

## Definition
Separation of Duties (SoD) is the principle that critical actions require multiple people in distinct roles. In a regulated codebase: developers can write code but can't merge their own [[Pull Request|PRs]]; pipelines can deploy but only after a [[Pre-deploy Approvals|pre-deploy approval]] from someone in operations; engineers can request infrastructure changes but the platform team executes them. SoD is the structural defense against both honest mistakes (a tired dev pushes a bad migration on a Friday) and malicious action (a single insider can't both create and authorize a fraudulent change). It's the *why* behind the friction: "I can't just `az webapp config set`" feels like bureaucracy until you remember that auditing every production action by attribution-of-author-vs-approver is what makes a [[SOC 1 Audit]] passable. The trade-off — every SoD boundary is a wait state, and over-applied SoD becomes a productivity killer that drives people to invent workarounds.

## Source
CI/CD learning session — the structural reason developers don't have direct production access.

---

## Compass

**Roots** — *where this comes from*
SoD emerges from the broader landscape of [[Compliance and Governance|compliance and governance]] — what makes audit-passable systems work. It sits at the intersection of [[Trust vs Structural Safety|trust versus structural safety]], asking the hard question: is this person trustworthy enough that we don't need the gate, or should we always have the structural control regardless?

**Paths** — *where this leads*
SoD is what [[SOC 1 Audit]] requires to pass and why [[Pre-deploy Approvals]] exist as a gate in pipelines. It's also why [[Pull Request|pull requests]] are the SoD mechanism in source control. But pushing SoD too tight creates [[Workaround Risk|workaround risk]] — when the friction is too high, people route around the controls entirely.

**Neighbors** — *what lives nearby*
[[Read-Only by Default]] applies the same restraint principle but to code defaults rather than governance. The two-person rule in military and banking systems is analogous — requiring multiple parties to authorize critical actions. [[Principle of Least Privilege]] overlaps conceptually but isn't identical; SoD is about separation of roles, while least privilege is about minimizing access per role.

**Clash** — *what pushes against this*
"Just give the dev prod access" is the expedient counter-argument — fast but audit-failing. A single root account everywhere is the anti-pattern that SoD directly opposes. Both reject the structural control that SoD demands.
