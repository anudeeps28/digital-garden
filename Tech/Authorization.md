---
type: atomic
tags: [coding/security]
date: 2026-03-24
---

# Authorization

## Idea
Authorization is checking what you're allowed to do — after proving your identity, the system verifies your permissions.

## Definition
Authorization (authz) answers the question "What are you allowed to do?" After [[Authentication]] confirms who you are, authorization checks whether you have permission to perform the requested action. In the KBA project, [[Entra ID]] includes roles and claims in the [[Bearer Token|JWT token]] — the API can check if a user has the "Admin" role before allowing them to delete documents, or restrict certain [[API Endpoints|endpoints]] to specific groups. Authorization is enforced using `[Authorize]` attributes on [[Controller]] methods or through policy-based authorization in [[.NET 8]].

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*
[[Role-Based Access Control (RBAC)]] assigns permissions based on roles, while [[Claims-Based Authorization]] checks specific claims in a token — both are concrete patterns for determining what users can do.

## Clash — *what pushes against this*
[[Authentication]] focuses on proving identity (who you are), whereas authorization determines what you can do — they're complementary but distinct concerns. [[Open Access]] represents the opposite extreme, where there are no permission checks at all.

## Roots — *where this comes from*
[[Security Concepts]] treat authorization as a core principle for protecting systems, and [[Entra ID]] is the specific service that manages roles and permissions in the KBA project.

## Paths — *where this leads*
[[Bearer Token|Tokens]] carry role and permission claims that enable authorization decisions, [[Controller]] methods use `[Authorize]` attributes to enforce authorization checks, and [[Middleware]] can intercept requests to validate permissions before they reach the application logic.
