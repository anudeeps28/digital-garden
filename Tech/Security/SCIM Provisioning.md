---
type: atomic
tags: [coding/security, coding/identity, coding/web-api, api]
date: 2026-10-01
---

# SCIM Provisioning

## Idea
When someone joins or leaves a company, every app they use should find out automatically — SCIM is the standard way the identity system tells apps "create this user", "change this", "turn this one off".

## Definition
SCIM (System for Cross-domain Identity Management, pronounced "skim") is a standard [[REST API]] for managing users and groups across systems. RFC 7643 defines the data shape (a `User` and `Group` schema with `userName`, `emails`, `active`, `members`); RFC 7644 defines the protocol (`POST /Users`, `PATCH /Users/{id}`, `GET /Users?filter=userName eq "a@example.com"`, and the same for `/Groups`). It is a **push model**: the app exposes a SCIM endpoint and the [[Identity Provider (IdP)|identity provider]] calls it on a schedule or on change. Creating accounts saves admin time, but **deprovisioning** is the real value — when HR marks someone as gone, the IdP sends `active: false` and the leaver loses access in every connected app without anyone remembering to do it. The gotcha is that the caller is a *service*, not a person: no user signs in, so no MFA or [[Conditional Access]] applies. A SCIM endpoint can create and delete accounts, so it needs its own protection — a long random bearer token or OAuth client credentials, an allowlist limited to the IdP's published IP ranges, [[Rate Limiting]], and audit logging.

## Providers
- **Azure** — Microsoft Entra ID app provisioning pushes users and groups to any SCIM 2.0 endpoint.
- **AWS** — AWS IAM Identity Center accepts SCIM *inbound* from an external IdP to sync its own directory.
- **Google Cloud** — Google Workspace / Cloud Identity auto-provisions users into supported SaaS apps.
- **Others** — Okta and OneLogin provisioning; most SaaS apps publish a SCIM endpoint on enterprise plans.

## Source
IETF RFC 7643 (SCIM Core Schema) and RFC 7644 (SCIM Protocol), September 2015.

---

## Compass

**Roots** — *where this comes from*
It extends the [[Identity Provider (IdP)]] from "who can sign in" to "who has an account at all", using an ordinary [[REST API]].

**Paths** — *where this leads*
Because the IdP is the caller, securing it is a [[Machine-to-Machine Authentication]] problem — plus [[Default-Deny Allowlisting]] on the IdP's address ranges, often expressed as [[Service Tags]].

**Neighbors** — *what lives nearby*
Just-in-time provisioning creates the account on first sign-in instead, but it cannot remove anyone. [[Authorization]] uses the groups SCIM keeps in sync.

**Clash** — *what pushes against this*
Each IdP interprets the spec slightly differently (PATCH paths, filter support, group size), so "SCIM compliant" rarely means plug-and-play. And a misconfigured mapping can mass-deactivate real users in seconds.
