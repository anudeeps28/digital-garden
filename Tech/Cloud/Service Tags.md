---
type: atomic
tags: [coding/azure, coding/security, coding/networking, devops]
date: 2026-10-01
---

# Service Tags

## Idea
A service tag lets you write "allow the cloud provider's gateway service" instead of a list of IP addresses that changes every week. But "the gateway service" means everyone's gateway, not just yours.

## Definition
A service tag is a named group of IP ranges that a cloud provider owns and keeps up to date — for example "the edge gateway's backend range" or "the storage service in this region". You put the name in a firewall or network rule instead of hard-coding addresses, and the provider updates what the name covers as its infrastructure changes, so your rules don't silently break. The key insight is what the name actually covers: **every customer of that service**, not just you. If you allow the edge gateway's tag, then any other tenant who sets up their own instance of that same gateway can send traffic to your backend through it — their requests leave from exactly the same addresses as yours. A shared tag therefore proves "this came through that service", never "this came through *my* configuration of it". To close the gap you add a second check, usually a header the service stamps with your instance's unique id ([[Origin Verification]]). The alternative, where the service supports it, is to route traffic from a **dedicated subnet you own**, so the allowed range contains only your resources and the IP rule alone is meaningful.

## Providers
- **Azure** — service tags (e.g. `AzureFrontDoor.Backend`, `Storage.WestEurope`) usable in NSGs, Azure Firewall and App Service access restrictions; the full list is also published as a downloadable JSON file.
- **AWS** — AWS-managed prefix lists (e.g. the CloudFront origin-facing list) usable in security groups and route tables; the full set of AWS ranges is published as `ip-ranges.json`.
- **Google Cloud** — publishes its ranges as JSON files (`goog.json`, `cloud.json`) and documents fixed ranges for things like load balancer health checks; there's no direct equivalent of a named, auto-updating tag in basic VPC firewall rules, so you script updates or use firewall policy address groups.
- **Others** — Cloudflare, GitHub (the `/meta` API) and most SaaS platforms publish their egress ranges for the same purpose.

## Source
Provider documentation: Azure virtual network service tags (Microsoft), AWS-managed prefix lists (Amazon), and Google Cloud's published IP range files.

---

## Compass

**Roots** — *where this comes from*
It's a convenience layer on [[Default-Deny Allowlisting]]: the one allow rule names a provider's range instead of a raw list of addresses.

**Paths** — *where this leads*
Because a tag is shared by all tenants, it almost always needs [[Origin Verification]] stacked on top — a small, concrete case of [[Defence in Depth]].

**Neighbors** — *what lives nearby*
An [[Edge Gateway]] is the most common thing people allow by tag; a [[Private Endpoint]] avoids the question entirely by taking the service off the public internet.

**Clash** — *what pushes against this*
The convenience hides how broad the rule is: it reads like "allow my gateway" but means "allow anyone's", and because the provider changes the contents, you no longer know exactly which addresses your rule trusts on a given day.
