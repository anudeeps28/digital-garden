---
type: atomic
tags: [devops, coding/azure, coding/distributed-systems, iac]
date: 2026-09-16
---

# IP Address Space Registry

## Idea
Private IP ranges look infinite until two teams pick the same one. Then the networks can never be peered, and the fix is to rebuild one of them.

## Definition
An IP address space registry is a single authoritative record of which private network ranges are allocated to which system — a street-address book for the organization's networks. It exists because private address space is a shared finite resource with a brutal failure mode: overlapping ranges cannot be connected. Two systems that each quietly took the same subnet work perfectly in isolation and become impossible to peer, route between, or place behind shared infrastructure, and by the time anyone notices both are in production. So allocation is a claim you register before you build, typically as a reviewed change to a file in a shared repository, with ranges reserved per environment. The discipline worth keeping: verify the registry against what's actually deployed before trusting it, because a stale document is more dangerous than no document — it hands you a wrong answer with full confidence.

## Source
Long-standing network engineering practice (IP Address Management, IPAM), formalized in tools like Infoblox and NetBox and in cloud landing-zone reference architectures.

---

## Compass

**Roots** — *where this comes from*
The constraint comes from private address ranges defined in RFC 1918, and from the fact that routing cannot disambiguate identical subnets.

**Paths** — *where this leads*
An allocated range is a precondition for [[Private Endpoint|private endpoints]] and for any network peering, which makes it a gating dependency on infrastructure work.

**Neighbors** — *what lives nearby*
It's a specific case of [[Centralized Infrastructure Ownership]] — a shared resource that one team must arbitrate.

**Clash** — *what pushes against this*
Registration is a queue, and queues slow teams down. The temptation is always to grab a range and register it later, which is how collisions get created.
