---
type: atomic
tags: [coding/azure, coding/networking, devops, iac]
date: 2026-10-01
---

# CIDR and Subnet Sizing

## Idea
A subnet's size is decided once, at the start, and is painful to change later. So you size it for the biggest the thing inside it will ever get, not for what it needs today.

## Definition
**CIDR notation** (Classless Inter-Domain Routing) writes a range of IP addresses as a starting address and a slash number, like `10.0.1.0/24`. An IPv4 address has 32 bits; the slash number says how many of them are fixed, and the rest are free to vary. So `/24` fixes 24 bits and leaves 8 free — 2⁸ = 256 addresses. Every step up halves the range: `/25` is 128, `/26` is 64, `/27` is 32, `/28` is 16. A smaller slash number means a *bigger* network. Two practical details shrink what you actually get. First, clouds **reserve addresses in every subnet** for the network address, the default gateway, DNS and broadcast — Azure and AWS each take 5, so a `/28` gives you 11 usable addresses, not 16. Second, some managed services demand a **dedicated subnet** that nothing else may share, and each instance they scale out to takes an address; you must size that subnet for the service's *maximum* scale-out plus upgrade headroom, because during an upgrade the old and new instances can exist side by side. Getting it wrong is expensive: most clouds won't let you resize a subnet that has anything in it, so the fix is usually to build a new subnet and migrate.

## Providers
- **Azure** — reserves 5 addresses per subnet (first four and last); smallest subnet is `/29`. Application Gateway v2, Azure Firewall (`AzureFirewallSubnet`), VPN gateways (`GatewaySubnet`) and Azure Bastion each require their own dedicated subnet with a minimum size. A subnet can only be resized when it's empty.
- **AWS** — reserves 5 addresses per subnet (first four and last); subnets range from `/16` to `/28`. A subnet can't be resized, but you can add secondary CIDR blocks to a VPC and create new subnets in them. Transit Gateway attachments are commonly given small dedicated subnets.
- **Google Cloud** — reserves 4 addresses in each subnet's primary range. Unusually, you can *expand* a subnet's primary range in place (never shrink it), which makes undersizing more forgiving.
- **Others** — Kubernetes clusters with per-pod IP addressing (e.g. Azure CNI, AWS VPC CNI) consume subnet addresses very quickly and are the most common cause of exhausted subnets.

## Source
CIDR was defined by the IETF in RFC 1518 and RFC 1519 (1993), updated by RFC 4632 (2006). Private ranges come from RFC 1918 (1996). Reserved-address counts and dedicated-subnet rules are from each provider's virtual network documentation.

---

## Compass

**Roots** — *where this comes from*
Address space is a finite shared resource, which is why ranges are claimed in an [[IP Address Space Registry]] before anything is built.

**Paths** — *where this leads*
Sizing decisions add up across a [[Hub-and-Spoke Network]], where every spoke's range must fit and none may overlap.

**Neighbors** — *what lives nearby*
Subnets are also security units: [[Default-Deny Allowlisting]] often allows traffic from a whole subnet, so what you put in a subnet decides who shares its permissions.

**Clash** — *what pushes against this*
Sizing for maximum scale wastes address space in an organization where ranges are already scarce, and generous `/24`s for every small service exhaust a private range surprisingly fast — the tension is between headroom now and room for everyone else later.
