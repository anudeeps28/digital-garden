---
type: atomic
tags: [coding/azure, coding/security, devops, coding/networking]
date: 2026-10-01
---

# Virtual Network

## Idea
A virtual network is your own private patch of the cloud: machines and services inside it can talk to each other on private addresses, and nothing outside can reach them unless you open a door on purpose.

## Definition
A virtual network is an isolated network that a cloud provider builds for you in software. You give it an **address range**, written in [[CIDR and Subnet Sizing|CIDR notation]] like `10.20.0.0/16`, and split that range into **subnets**, smaller blocks that group resources by role (web tier, data tier, build agents). Every resource placed in a subnet gets a **private IP** from that block. **Route tables** decide where traffic goes next, and **firewall rules** (security groups) attached to subnets or network interfaces allow or block traffic by address, port and protocol, ideally in a [[Default-Deny Allowlisting|default-deny]] style. Resources inside the network talk privately; managed services join it through a [[Private Endpoint]]. To reach other networks you connect them: **peering** joins two virtual networks so they route to each other directly, a **VPN gateway** links the cloud network to an office or data centre, and [[Zero Trust Network Access (ZTNA)|ZTNA]] gives individual users access to specific apps without putting them on the network at all. The gotcha is address planning: peered networks cannot have overlapping ranges, and changing a range later usually means rebuilding, so organizations track ranges in an [[IP Address Space Registry]].

## Providers
- **Azure** — Azure Virtual Network (VNet); regional, with subnets, network security groups, route tables and VNet peering.
- **AWS** — Amazon VPC; regional, with subnets pinned to one availability zone, security groups, network ACLs and VPC peering or Transit Gateway.
- **Google Cloud** — Google Cloud VPC; global, so one network spans every region and only its subnets are regional.

## Source
Amazon VPC (2009) introduced the idea of a private, customer-defined network inside a public cloud; Azure Virtual Network and Google Cloud VPC followed.

---

## Compass

**Roots** — *where this comes from*
It is the software version of a physical company network, sized with [[CIDR and Subnet Sizing|CIDR blocks]] and protected with [[Default-Deny Allowlisting|default-deny rules]].

**Paths** — *where this leads*
Many networks are usually joined in a [[Hub-and-Spoke Network]], with shared services in the hub. Self-hosted [[Pipeline Agent Machines]] sit inside the network so deployments can reach private resources.

**Neighbors** — *what lives nearby*
[[Private Endpoint]] pulls a managed service into the network; [[Service Tags]] let firewall rules name a provider's services instead of listing their IPs.

**Clash** — *what pushes against this*
A network boundary is not identity: once something is inside, flat networks let it reach far too much, which is the argument behind [[Zero Trust]]. Private networking also makes local development and debugging harder, and every new range has to be coordinated to avoid overlaps.
