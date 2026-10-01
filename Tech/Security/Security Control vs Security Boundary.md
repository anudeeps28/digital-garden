---
type: atomic
tags: [coding/security, coding/architecture, security]
date: 2026-10-01
---

# Security Control vs Security Boundary

## Idea
Not every security measure stops every threat. Being exact about *which* measure actually stops *which* threat keeps you from feeling safe for the wrong reason.

## Definition
A **security boundary** is the thing whose failure means the bad outcome happens — the wall that, if breached, lets the attacker in. A **security control** is anything that lowers the chance or the cost of a threat; useful, but if it fails the boundary still has to hold. The same measure can be a boundary for one threat and only a control for another, so the honest question is always "for *this* threat, what's the boundary?" Example: making a staff admin site reachable only from a private network is a strong **credential-theft control** — a stolen password is useless from outside the network. But it is *not* the tenant-isolation boundary, because a legitimate user already on the network is still separated from other tenants' data only by identity and data-layer checks. Counting the network as isolation gives false confidence. A short threat → boundary mapping makes this concrete: *stolen staff password* → network restriction plus MFA; *user of tenant A reads tenant B* → [[Tenant Resolution]] from a validated token, plus [[Row-Level Security]] and [[Global Query Filters]]; *compromised app reads everything* → [[Least-Privilege Database Roles]] and database-side policies; *stolen disk or backup* → encryption at rest. If a box in that map is empty, no amount of controls elsewhere fills it.

## Providers
- **Microsoft** — the Security Servicing Criteria for Windows explicitly list which mechanisms are "security boundaries" (and get security fixes) versus "defense-in-depth features" that don't.
- **NIST** — SP 800-53 organises controls into families (e.g. AC access control, SC system and communications protection, with SC-7 "Boundary Protection"), which forces you to say which control addresses which risk.
- **Threat modeling** — STRIDE and the Microsoft Threat Modeling Tool or OWASP Threat Dragon draw explicit **trust boundaries** on a data-flow diagram and attach threats to each crossing.

## Source
Microsoft Security Servicing Criteria for Windows ("security boundaries"); NIST SP 800-53; STRIDE threat modeling, developed at Microsoft.

---

## Compass

**Roots** — *where this comes from*
It sharpens [[Defence in Depth]]: layering only works if you know which layer is the one that must not fail for each threat.

**Paths** — *where this leads*
Applied to SaaS, it says the boundary for tenant separation lives in identity and data — [[Multi-Tenant Data Isolation]] and the choice of [[Tenancy Models]] — not in the network.

**Neighbors** — *what lives nearby*
[[Zero Trust Network Access (ZTNA)]] and [[Private Endpoint|private endpoints]] are excellent controls that are easy to over-credit; [[Zero Trust]] makes the same point by refusing to treat "inside the network" as a boundary at all.

**Clash** — *what pushes against this*
The line isn't always crisp — enough strong controls stacked together can behave like a boundary in practice, and arguing over labels can stall decisions. The value is in the mapping, not the vocabulary.
