---
type: atomic
tags: [coding/azure, coding/security, coding/networking, devops]
date: 2026-10-01
---

# Default-Deny Allowlisting

## Idea
Start with every door locked and unlock only the ones you can name a reason for. The strength of the rule then depends on how precisely you can name who is allowed in.

## Definition
Default-deny allowlisting is an access-rule style where everything is blocked unless a rule explicitly allows it. The cleanest form is **default deny, one allow**: a backend that only accepts traffic from its gateway's subnet, and refuses everything else. How strong that one allow is depends on who else can stand inside the allowed range. Allowing a **subnet you control** is strong — only your own resources live there. Allowing a **shared range**, such as a cloud service's published IP block, is weaker, because every other customer of that service sends traffic from the same addresses; there you need a second factor such as a header check that proves the request came through *your* instance. The same idea covers inbound callers outside your network: when a partner publishes the IP ranges their systems call from, you allowlist exactly those. The gotcha is that one application often has several separate front doors, each with its **own rule list** — a web app's public site and its deployment/management site, for example — and locking down one leaves the other wide open. Also check what "default" really means on your platform: some rule systems ship with built-in allows (such as all traffic within the virtual network) sitting above your deny.

## Providers
- **Azure** — Network Security Groups (NSGs) on subnets and network interfaces; App Service access restrictions, which keep separate rule lists for the main site and the deployment (SCM/Kudu) site. Note that NSGs include default rules allowing virtual-network and load-balancer traffic.
- **AWS** — security groups deny all inbound by default, are allow-only and stateful, and can name another security group as the source (a precise "only from my own resources" rule); network ACLs are stateless, numbered, and support explicit denies at the subnet level.
- **Google Cloud** — VPC firewall rules and firewall policies with an implied deny-all ingress; rules can target instances by network tag or service account rather than by IP.
- **Others** — Kubernetes NetworkPolicy (a default-deny policy plus specific allows); host firewalls like iptables/nftables; Cloudflare and other edge platforms offer IP access rules.

## Source
The "deny by default" principle traces to Saltzer and Schroeder's "fail-safe defaults" in *The Protection of Information in Computer Systems* (1975); it is standard firewall practice and appears in NIST firewall guidance (SP 800-41).

---

## Compass

**Roots** — *where this comes from*
It's [[Read-Only by Default]] applied to the network: start at the most restrictive setting and open up only with a concrete reason. It's one layer of [[Defence in Depth]].

**Paths** — *where this leads*
When the allowed source is a shared provider range, you reach for [[Service Tags]] to name it and [[Origin Verification]] to tell your traffic apart from everyone else's.

**Neighbors** — *what lives nearby*
Sizing and grouping subnets carefully ([[CIDR and Subnet Sizing]]) matters because a subnet allow trusts everything placed in that subnet. [[Zero Trust]] pushes the same "allow only what's named" idea from IP addresses up to identities.

**Clash** — *what pushes against this*
IP-based rules say where a request came from, not who sent it; addresses get shared, reassigned and spoofed behind proxies, and long allowlists rot as partners change their ranges without telling you.
