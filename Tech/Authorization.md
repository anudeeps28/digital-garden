---
type: atomic
tags: [coding/security]
date: 2026-03-24
---

# Authorization

## Idea
Authorization is checking what you're allowed to do — after proving your identity, the system verifies your permissions.

## Definition
Authorization (authz) answers the question "What are you allowed to do?" After [[Authentication]] confirms who you are, authorization checks whether you have permission to perform the requested action. In practice, systems like [[Entra ID]] include roles and claims in the [[Bearer Token|JWT token]] — the API can check if a user has the "Admin" role before allowing restricted actions, or limit certain [[API Endpoints|endpoints]] to specific groups. Authorization is commonly enforced using attributes or decorators on controller methods or through policy-based authorization in frameworks like [[.NET 8]].

## Source
Foundational concept in information security; formalized in academic security literature including Graham and Denning's work on access control (1972). Widely standardized in frameworks like the OWASP Top 10 and implemented natively in modern identity platforms like Microsoft Entra ID.

---

## Neighbors — *what lives nearby*
[[Role-Based Access Control (RBAC)]] assigns permissions based on roles, while [[Claims-Based Authorization]] checks specific claims in a token — both are concrete patterns for determining what users can do.

## Clash — *what pushes against this*
[[Authentication]] focuses on proving identity (who you are), whereas authorization determines what you can do — they're complementary but distinct concerns. [[Open Access]] represents the opposite extreme, where there are no permission checks at all.

## Roots — *where this comes from*
[[Security Concepts]] treat authorization as a core principle for protecting systems, and identity platforms like [[Entra ID]] manage roles and permissions at scale across enterprise applications.

## Paths — *where this leads*
[[Bearer Token|Tokens]] carry role and permission claims that enable authorization decisions, [[Controller]] methods use `[Authorize]` attributes to enforce authorization checks, and [[Middleware]] can intercept requests to validate permissions before they reach the application logic.
