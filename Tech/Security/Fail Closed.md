---
type: atomic
tags: [coding/security, mental-model, coding/architecture]
date: 2026-10-04
---

# Fail Closed

## Idea
When a security check can't reach a decision, the answer is no. Errors, timeouts and missing config should leave the door locked, not open.

## Definition
A system **fails closed** (fail-secure) when any failure in a protective check results in denial rather than access. The everyday bug it prevents looks like `try { allowed = check() } catch { allowed = true }`, or a filter that treats an empty allowlist as "allow everything". Failing closed means the default branch of every decision is deny, and access has to be positively granted. Worked examples: a permission broker that asks a human to approve an agent's actions resolved to deny when its queue overflowed or the request was aborted, rather than auto-approving; a path gate that limited tools to allowed folders denied everything when its list of roots was empty or couldn't be resolved, instead of skipping the check. The point is that a broken guard should be noticed as an outage, not discovered later as a breach.

## Source
Saltzer and Schroeder named it "fail-safe defaults" in "The Protection of Information in Computer Systems" (Proceedings of the IEEE, 1975): base access decisions on permission rather than exclusion. "Fail closed" and "fail open" come from physical security and electrical engineering.

---

## Compass

**Roots** — *where this comes from*
It is the runtime form of [[Default-Deny Allowlisting]]: if access must be explicitly granted, then a failure to evaluate the grant can only mean no access.

**Paths** — *where this leads*
Paired with [[Fail Fast Fail Loudly]], a denial should also raise an alert, otherwise a fail-closed guard turns into a [[Silent Failure]] where users are blocked and nobody knows why.

**Neighbors** — *what lives nearby*
[[Read-Only by Default]] applies the same instinct to mutability, and [[Propose, Don't Execute]] applies it to agents: when in doubt, the action does not happen.

**Clash** — *what pushes against this*
Availability pulls the other way: fire doors, medical devices and some [[Graceful Degradation]] designs must fail open because a locked door is the greater harm, so the choice depends on which failure costs more.
