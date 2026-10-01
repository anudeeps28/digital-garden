---
type: atomic
tags: [coding/security, coding/identity, coding/web-api, api]
date: 2026-10-01
---

# Machine-to-Machine Authentication

## Idea
When one service calls another with no human present, there is nobody to type a password or approve an MFA prompt — so the service needs its own identity, and the protections that normally lean on a person have to be replaced by something else.

## Definition
Machine-to-machine (M2M) authentication is how a service, script or job proves who it is to another service. The standard route is the **OAuth 2.0 client credentials grant**: the service presents its client ID plus a secret or signed certificate to the [[Identity Provider (IdP)|identity provider]] and gets back an access token for a named API — no user, no redirect. Better still is **workload identity**: the platform itself vouches for the running code (a VM, function, container or pod), so there is no secret to store or leak. **Mutual TLS** has both sides present certificates during the connection handshake. **API keys** — a static shared string in a header — are the weakest: they rarely expire, carry no identity beyond "someone who has the key", and get pasted into config files. The gotcha is that M2M calls never pass through interactive sign-in, so MFA, device checks and [[Conditional Access]] do not apply. Compensating controls take their place: **narrow scopes** (application permissions for exactly one job), **short-lived tokens**, IP restriction to the caller's known ranges, [[Rate Limiting]], and validating [[Token Issuer and Audience|issuer and audience]] on every call.

## Providers
- **Azure** — Microsoft Entra app registrations (client credentials with secret or certificate) and managed identities for secretless workload identity.
- **AWS** — IAM roles assumed by compute (EC2, Lambda, EKS) for AWS APIs; Amazon Cognito client credentials for your own APIs.
- **Google Cloud** — Service accounts, with Workload Identity Federation to avoid exported keys.
- **Others** — Auth0 machine-to-machine applications; Kubernetes service account tokens; SPIFFE/SPIRE for workload certificates.

## Source
Client credentials grant defined in IETF RFC 6749 (OAuth 2.0), section 4.4, 2012; certificate-bound tokens with mutual TLS in RFC 8705 (2020).

---

## Compass

**Roots** — *where this comes from*
It is the no-human branch of [[OAuth 2.0 and OIDC]]; the result is still a [[Bearer Token]] checked like any other.

**Paths** — *where this leads*
[[Workload Identity]] removes the stored secret altogether. [[SCIM Provisioning]] is a concrete M2M caller that needs exactly these compensating controls.

**Neighbors** — *what lives nearby*
[[Default-Deny Allowlisting]] and [[Rate Limiting]] stand in for the checks a human sign-in would have provided. [[Pre-Signed URL|Pre-signed URLs]] are another way to grant access without a user present.

**Clash** — *what pushes against this*
Service identities tend to be over-permissioned and never reviewed, and a leaked client secret works from anywhere until someone notices — the convenience of "it just runs" is exactly what makes it dangerous.
