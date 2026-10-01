---
type: atomic
tags: [coding/security, security, coding/networking, coding/identity]
date: 2026-10-01
---

# Zero Trust Network Access (ZTNA)

## Idea
A VPN puts you on the whole network. ZTNA connects you to one specific app, only after checking who you are and what device you're on — and the private network never has to open a door to the internet.

## Definition
ZTNA is the replacement for the VPN built on [[Zero Trust]] principles. It has three parts. A **client agent** runs on an enrolled, managed device. A **cloud service** run by the provider sits in the middle and makes the access decision. And a lightweight **connector** is installed inside the private network and **dials out** to that cloud service, holding the connection open — so traffic flows back in over a connection the connector started, and you never open an inbound port or expose a public address. When a user tries to reach a private app, the cloud service checks their identity, their device's health and any [[Conditional Access]] policy, and only then stitches the user's session to that one app through the connector. They get the app, not the network: no scanning, no reaching neighbouring servers. The private app can have internal-only DNS and no public IP at all. The limit is built into the design: it only works for users whose devices can be enrolled in your organization's identity tenant. External partners and machine-to-machine callers can't install your agent or pass your device checks, so they need a different, deliberately public path — typically an edge gateway with authentication, allowlisting and origin checks.

## Providers
- **Azure** — Microsoft Entra Private Access (part of Global Secure Access), using the Global Secure Access client and Microsoft Entra private network connectors.
- **AWS** — AWS Verified Access, which evaluates identity and device signals per request in front of private apps (agentless for web apps).
- **Google Cloud** — Identity-Aware Proxy and BeyondCorp Enterprise (now Chrome Enterprise Premium), with app connectors for apps outside Google Cloud.
- **Others** — Cloudflare Access with Cloudflare Tunnel (`cloudflared` as the outbound connector), Zscaler Private Access (App Connectors), and Tailscale, which builds a peer-to-peer WireGuard mesh with identity-based access rules and uses subnet routers in place of connectors.

## Source
The ZTNA category name comes from Gartner's market research; the architecture follows NIST SP 800-207 (2020) and Google's BeyondCorp work (from 2014).

---

## Compass

**Roots** — *where this comes from*
It's [[Zero Trust]] applied to the specific problem of remote access, using an [[Identity Provider (IdP)|identity provider]] and [[Conditional Access]] as the gate.

**Paths** — *where this leads*
Callers it can't serve — partners, other systems — go through a public path guarded by an [[Edge Gateway]], [[Machine-to-Machine Authentication]], [[Default-Deny Allowlisting]] and [[Origin Verification]].

**Neighbors** — *what lives nearby*
Connectors usually live in the hub of a [[Hub-and-Spoke Network]] so one set reaches every spoke; a [[Private Endpoint]] does the same "no public address" job for services rather than people.

**Clash** — *what pushes against this*
It moves the trust to the provider's cloud and the connector: if either is down, nobody gets in, and a compromised connector sits inside the network. Unmanaged devices, contractors and legacy protocols often don't fit, so many organizations end up running ZTNA and a VPN side by side for years.
