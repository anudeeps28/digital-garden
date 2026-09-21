---
type: atomic
tags: [coding/security, security, coding/architecture]
date: 2026-09-16
---

# Defence in Depth

## Idea
One lock is a single point of failure. Three independent locks mean an attacker has to be right three times and you only have to be right once.

## Definition
Defence in depth is the practice of layering independent controls so that the compromise or misconfiguration of any one of them does not, by itself, cause a breach. The word doing the work is *independent*: three checks that all read the same header, or all trust the same token, are one control wearing three hats. Real depth means the layers fail for different reasons — a network boundary, an identity boundary, a data-level predicate, and encryption at rest each break under different conditions. The practical test is to ask, for each layer, "if this one silently stopped working, would anything else stop the request?" If the answer is no, you have a chain, not a stack.

## Source
Originates in military fortification doctrine; adopted into information security by NSA guidance in the 1990s and now standard in NIST and ISO security frameworks.

---

## Compass

**Roots** — *where this comes from*
The idea assumes failure is normal — the same premise behind [[Fault-vs-Failure]] and [[Errare Humanum Est]].

**Paths** — *where this leads*
Applied to tenant data it becomes [[Multi-Tenant Data Isolation]]; applied at the network edge it becomes [[Origin Verification]] plus [[Web Application Firewall (WAF)]] plus [[Rate Limiting]].

**Neighbors** — *what lives nearby*
[[Separation of Duties]] and [[The Four Gatekeepers]] are the same logic applied to decisions rather than packets.

**Clash** — *what pushes against this*
[[Maintainability-Operability-Simplicity-Evolvability|Simplicity]] pushes back: every layer is another thing to operate, another thing that can wrongly deny a legitimate request, and another place to look when something breaks.
