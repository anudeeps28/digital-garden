---
type: atomic
tags: [coding/security, coding/architecture]
date: 2026-10-04
---

# Permission Inheritance

## Idea
In a tree of folders or pages, access granted at a parent flows down to its children. Grant at the right level and moves and new children just work; grant too low and things break when they move.

## Definition
**Permission inheritance** means a child resource takes its access rules from its ancestors unless it overrides them. File systems with ACLs, cloud resource hierarchies (organisation, project, resource) and workspace tools with nested pages all work this way. It makes administration scale, because you grant once on a container instead of on every item, but it also means a resource's effective access depends on where it lives. A worked example: an API integration that had been shared with individual databases suddenly got 404 Not Found errors after someone moved those databases under a new parent page, because the grants travelled with the old location. Sharing the integration with the parent page fixed it, and every future child inherited access automatically. A 404 rather than a 403 is common here, since many systems hide resources you can't see.

## Source
ACL inheritance was popularised by Windows NT's NTFS permissions, with automatic propagation to children arriving in Windows 2000; cloud IAM hierarchies (for example Google Cloud's organisation, folder and project model) and workspace tools such as Notion apply the same rule to modern resources.

---

## Compass

**Roots** — *where this comes from*
It is how [[Role-Based Access Control (RBAC)]] scales to large trees: assign a role on a container and [[Authorization]] decisions for everything inside follow from it.

**Paths** — *where this leads*
It shapes [[Multi-Tenant Data Isolation]] too, since putting each tenant's data under one parent makes "everything under here belongs to tenant X" a single, auditable grant.

**Neighbors** — *what lives nearby*
[[Tenancy Models]] decide what the top of the tree looks like, and [[Centralized Infrastructure Ownership]] relies on inheritance to apply policy from one place.

**Clash** — *what pushes against this*
Granting high in the tree over-grants: the integration that now sees the parent sees every sibling as well, which cuts against least privilege and widens the [[Blast Radius]] of a leaked credential.
