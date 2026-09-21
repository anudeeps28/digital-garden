---
type: atomic
tags: [coding/security, coding/database, coding/architecture, saas]
date: 2026-09-16
---

# Multi-Tenant Data Isolation

## Idea
When one system serves many customers out of one database, the only acceptable design is that no tenant can ever see another tenant's rows — and you don't trust a single mechanism to guarantee it.

## Definition
Multi-tenant data isolation is the set of controls that keep each customer's data reachable only by that customer in a shared platform. The strong version is defence in depth: several independent layers stacked so that a failure in one is caught by the next. A typical stack is (1) a least-privileged identity per application component, granted only the objects it needs; (2) [[Row-Level Security]] inside the database, filtering rows by a tenant key the application cannot forge; (3) per-tenant storage containers and, for higher tiers, a dedicated key store; and (4) [[Transparent Data Encryption|encryption at rest]] underneath all of it. Each layer is cheap; the combination is what makes a leak require several simultaneous mistakes rather than one. The alternative — filtering by tenant in application code alone — means every new query is a fresh opportunity to forget the `WHERE` clause.

## Source
Standard practice in SaaS architecture; the layered "silo / bridge / pool" tenancy models are documented in AWS and Microsoft multi-tenant SaaS reference architectures.

---

## Compass

**Roots** — *where this comes from*
Isolation only means something once you know who the caller is, which ties back to [[Authentication]] and [[Authorization]].

**Paths** — *where this leads*
The database-level layer is [[Row-Level Security]]; the identity layer is [[Least-Privilege Database Roles]]; the storage layer is [[Transparent Data Encryption]] and, at the top tier, [[Customer-Managed Keys (CMK)]].

**Neighbors** — *what lives nearby*
[[Defence in Depth]] is the general principle; [[Separation of Duties]] is the same instinct applied to people rather than data.

**Clash** — *what pushes against this*
Every layer costs latency, money, and operational complexity. [[Read-Only by Default]] argues for the strictest default; commercial pressure argues for the cheapest tier that technically works.
