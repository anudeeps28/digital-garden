---
type: atomic
tags: [coding/security, security, coding/identity, coding/architecture]
date: 2026-10-01
---

# Zero Trust

## Idea
Being inside the network used to mean being trusted. Zero trust drops that assumption: where a request comes from earns it nothing, so every request has to prove itself, every time.

## Definition
Zero trust is a security model summed up as **"never trust, always verify"**. The older **castle-and-moat** model puts a strong wall (firewall, VPN) around the network and trusts anything inside it — so one stolen laptop or one phished password lets an attacker roam freely, because once they're over the moat nothing checks them again. A VPN fits that model: it brings you inside the wall and then gets out of the way. Zero trust removes the idea of a trusted inside. Each request is **authenticated** (who are you), **authorized** (are you allowed to do this specific thing) and **evaluated against context** — is the device managed and healthy, where is the sign-in coming from, does it look risky — and that check happens per request or per session, not once at the door. Two principles go with it: **least privilege**, so even a verified user gets access only to the specific apps and data they need, and **assume breach**, so you design as if an attacker is already inside: segment everything, encrypt internal traffic, log and inspect it all. It's a model rather than a product; in practice it's built from an identity provider, device management, a policy engine and an access proxy working together.

## Providers
- **Azure** — Microsoft Entra ID with Conditional Access as the policy engine, Intune for device health, and Global Secure Access (Internet Access and Private Access) for network paths.
- **AWS** — IAM with per-request signing for workloads, AWS Verified Access for user access to private apps.
- **Google Cloud** — BeyondCorp Enterprise (now Chrome Enterprise Premium) and Identity-Aware Proxy, descended from Google's internal BeyondCorp.
- **Others** — Zscaler, Cloudflare Zero Trust, Okta (identity and device-aware policy), and service meshes like Istio applying mutual TLS between services.

## Source
John Kindervag, Forrester Research — coined "zero trust" in *No More Chewy Centers* (2010). Google's BeyondCorp papers, starting with *BeyondCorp: A New Approach to Enterprise Security* (;login:, 2014). NIST SP 800-207, *Zero Trust Architecture* (2020).

---

## Compass

**Roots** — *where this comes from*
It grows out of [[Defence in Depth]] and moves the trust decision from the network to [[Authentication]] and [[Authorization]], usually via an [[Identity Provider (IdP)|identity provider]].

**Paths** — *where this leads*
[[Conditional Access]] is how the per-request policy gets written; [[Zero Trust Network Access (ZTNA)|ZTNA]] is how it replaces the VPN; [[Workload Identity]] and [[Machine-to-Machine Authentication]] apply it to services, not just people.

**Neighbors** — *what lives nearby*
[[Default-Deny Allowlisting]] is the network-level ancestor — allow only what's named — but it names addresses, where zero trust names identities. [[Security Control vs Security Boundary]] helps tell which pieces actually enforce anything.

**Clash** — *what pushes against this*
"Zero trust" is heavily marketed and often sold as a single product, which it isn't. Real adoption is slow and expensive — legacy apps that can't do modern authentication, devices you can't manage, and partners you can't enrol all end up as exceptions that quietly reintroduce trusted zones.
