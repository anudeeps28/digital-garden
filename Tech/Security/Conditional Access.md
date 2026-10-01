---
type: atomic
tags: [coding/security, coding/identity, security]
date: 2026-10-01
---

# Conditional Access

## Idea
A correct password is no longer enough on its own — the sign-in system also looks at who, from where, on what device and how risky it looks, and only then decides whether to let you in.

## Definition
Conditional access is a set of **if-then policies** the [[Identity Provider (IdP)|identity provider]] evaluates at sign-in, before it issues a token. The *if* side matches **signals**: user or group, target app, network location or country, device platform, device state, and a computed **sign-in risk** (impossible travel, leaked credentials, unfamiliar client). The *then* side is a decision: allow, **require MFA**, require a **compliant device**, require a password change, or block. A compliant device is one **enrolled** in the organization's mobile device management (MDM), so IT can vouch that it is patched, encrypted and locked; the IdP reads that state as a signal. Policies are usually stacked, and the strictest matching one wins. The gotcha is *where* the check runs: the IdP enforces the policy only when it mints a token. Anything that skips interactive sign-in — a long-lived refresh token already issued, an API key, a service calling another service, a legacy protocol that bypasses modern auth, a backend reachable directly — is not covered. So conditional access is only as strong as the set of paths that actually go through sign-in; close the others separately.

## Providers
- **Azure** — Microsoft Entra Conditional Access, with Intune supplying device-compliance state.
- **AWS** — AWS Verified Access policies evaluate identity and device posture per request to private apps.
- **Google Cloud** — Context-Aware Access (BeyondCorp Enterprise) with access levels built from device and network attributes.
- **Others** — Okta authentication policies (with Okta Verify device checks); Cloudflare Access policies.

## Source
Grew out of the [[Zero Trust]] model popularized by Forrester (2010) and Google's BeyondCorp papers (2014 onward); "Conditional Access" is Microsoft's product name for the pattern.

---

## Compass

**Roots** — *where this comes from*
It is the [[Identity Provider (IdP)]] applying [[Zero Trust]] — "never trust, always verify" — at the moment of [[Authentication]].

**Paths** — *where this leads*
[[Zero Trust Network Access (ZTNA)]] carries the same signals past sign-in to every connection. Paths that never touch sign-in need their own controls, which is the problem [[Machine-to-Machine Authentication]] and [[SCIM Provisioning]] endpoints face.

**Neighbors** — *what lives nearby*
[[Authorization]] decides what you may do once in; conditional access decides whether you get in at all. [[Defence in Depth]] explains why it is one layer, not the whole wall.

**Clash** — *what pushes against this*
It is a [[Security Control vs Security Boundary|control, not a boundary]]: it guards the token-issuing door, not the resource. Strict device rules also lock out contractors and partners on unmanaged laptops, pushing teams toward risky exceptions.
