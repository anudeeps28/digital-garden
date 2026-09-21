---
type: atomic
tags: [devops, coding/architecture, workflow, coding/security]
date: 2026-09-16
---

# Centralized Infrastructure Ownership

## Idea
Some infrastructure can't be owned by the team that needs it, because it's shared by everyone. Discovering which parts those are — late — is how projects get blocked.

## Definition
Centralized infrastructure ownership is the arrangement where a platform team holds the shared substrate — network address allocation, DNS zones, the reusable module library, subscription-level policy — and product teams consume it rather than recreate it. It's enforced through two mechanisms working together: a **shared module library** that product templates import, so everyone gets the same hardened building blocks instead of inventing their own; and **tenant-level policy** that outright blocks certain resource types from being created outside the central resource group, so the boundary isn't a convention anyone can bypass under deadline pressure. The practical consequence for a project team is that some work is simply not yours to do, however capable you are — and the only real mistake is finding that out during deployment rather than during planning.

## Source
The platform-team model described in Skelton and Pais's *Team Topologies* (2019); implemented in cloud landing-zone architectures (Azure Cloud Adoption Framework, AWS Control Tower).

---

## Compass

**Roots** — *where this comes from*
It exists because shared resources have organization-wide failure modes — the reason an [[IP Address Space Registry]] must be central at all.

**Paths** — *where this leads*
It turns some technical tasks into cross-team dependencies with their own lead time, which is what makes [[Record the Reason, Not Just the Blocker]] worth doing.

**Neighbors** — *what lives nearby*
[[Separation of Duties]] is the same boundary drawn for control rather than efficiency; [[Shared Module Library]] is the consumable half of the arrangement.

**Clash** — *what pushes against this*
Every centralized dependency is a queue in front of a delivery team, and platform teams are chronically the bottleneck. Autonomy argues the other way — and sometimes wins, at the cost of ten slightly different implementations of the same thing.
