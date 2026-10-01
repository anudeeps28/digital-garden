---
type: atomic
tags: [coding/azure, coding/networking, devops, coding/architecture]
date: 2026-10-01
---

# Hub-and-Spoke Network

## Idea
Instead of every project building its own firewall, VPN and DNS, you build them once in a central network and plug every project's network into it. The catch is that plugging two spokes into the same hub does not connect them to each other.

## Definition
A hub-and-spoke network is a layout where one central **hub** virtual network holds the shared services — the firewall, the VPN gateway or ZTNA connectors, DNS resolvers, sometimes a bastion host — and each workload lives in its own **spoke** network that is peered to the hub. Think of an airport hub: every regional flight connects to it, so nobody needs a direct route to everywhere. Organizations use it to pay for, secure and audit the expensive shared pieces once, to give each team its own isolated spoke, and to force traffic through one inspection point. The detail that trips people up is that **peering is non-transitive**: if spoke A is peered to the hub and spoke B is peered to the hub, A still cannot reach B. Traffic only crosses between spokes if you deliberately route it through something in the hub — usually the firewall, using route tables that send spoke traffic there — which is exactly what makes it a control point rather than an accident. The other hard constraint is that peered networks cannot have overlapping address ranges, so the whole design depends on a central record of who owns which range.

## Providers
- **Azure** — VNet peering with user-defined routes pointing at Azure Firewall or a network virtual appliance in the hub; Azure Virtual WAN is the managed version where Microsoft runs the hub and its routing.
- **AWS** — Transit Gateway acts as the hub router, with its route tables deciding which attachments can talk to which; plain VPC peering is non-transitive, like Azure's.
- **Google Cloud** — VPC Network Peering (non-transitive) for the simple case; Network Connectivity Center for a managed hub with VPC and hybrid spokes. Shared VPC is a related pattern where projects share one network instead of peering.
- **Others** — on-premises this is the classic data-centre core/distribution design; SD-WAN products apply the same shape to branch offices.

## Source
Long-standing network topology, formalized for the cloud in the providers' landing-zone reference architectures (Microsoft Cloud Adoption Framework, AWS multi-account guidance, Google Cloud enterprise foundations blueprint).

---

## Compass

**Roots** — *where this comes from*
It's [[Centralized Infrastructure Ownership]] applied to the network: a platform team owns the hub, product teams own their spokes.

**Paths** — *where this leads*
Every spoke needs a range that doesn't collide with any other, which is why an [[IP Address Space Registry]] and careful [[CIDR and Subnet Sizing]] come first. Shared private DNS zones for each [[Private Endpoint]] usually live in, or are linked from, the hub.

**Neighbors** — *what lives nearby*
[[Zero Trust Network Access (ZTNA)|ZTNA]] connectors and VPN gateways sit in the hub so remote users reach spokes through one controlled path; [[Default-Deny Allowlisting]] decides what is allowed once traffic arrives.

**Clash** — *what pushes against this*
The hub is a shared dependency and a bottleneck: a bad firewall rule or route change there breaks every spoke at once, and routing all spoke-to-spoke traffic through a central firewall adds latency and per-gigabyte processing cost.
