---
type: atomic
tags: [coding/azure, coding/security, devops, coding/distributed-systems]
date: 2026-09-16
---

# Private Endpoint

## Idea
A private endpoint pulls a public cloud service onto your private network. It's two things that must both exist — a network interface and a DNS record — and only one of them tells you when it's missing.

## Definition
A private endpoint gives a managed service (a database, a key vault, a config store) a private IP address inside your virtual network, so traffic never traverses the public internet. It has two halves. The first is the endpoint resource itself: a network interface in your subnet, mapped to the service. The second is a **private DNS zone** — a zone like `privatelink.<service>.<domain>` linked to every virtual network that needs to resolve it — which overrides the service's public hostname to return the private IP. Miss the DNS half and the failure mode is nasty: the endpoint is created successfully, the deployment reports success, and every client silently resolves the public address instead. Nothing errors. You just don't have the isolation you think you have — a textbook case of the argument in [[Fail Fast Fail Loudly]].

## Source
Azure Private Link (Microsoft, 2019); AWS PrivateLink and Google Private Service Connect are the equivalents.

---

## Compass

**Roots** — *where this comes from*
It's the network layer of [[Defence in Depth]], removing public reachability rather than just guarding it.

**Paths** — *where this leads*
Because private DNS zones are usually shared across an organization, creating one is often a [[Centralized Infrastructure Ownership|centrally owned]] operation rather than something a project team can do for itself.

**Neighbors** — *what lives nearby*
[[Origin Verification]] closes the bypass path for inbound traffic; a private endpoint closes it for service-to-service traffic.

**Clash** — *what pushes against this*
It makes local development harder — a developer outside the network can no longer reach the resource at all — and the DNS dependency turns a name-resolution problem into a total outage.
