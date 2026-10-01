---
type: atomic
tags: [coding/security, coding/identity, coding/web-api, api]
date: 2026-10-01
---

# Token Issuer and Audience

## Idea
A valid signature only proves a token is genuine — not that it came from someone you trust or that it was meant for you. Checking the issuer and the audience closes both gaps.

## Definition
Two registered JWT claims tell an API whether to believe a token. **`iss` (issuer)** says who minted it — a URL identifying the [[Identity Provider (IdP)|identity provider]] and often the tenant, such as `https://login.example.com/{tenant-id}/v2.0`. The API must accept only issuers on its trust list; in a multi-tenant app, the validated issuer is also the reliable answer to *which tenant* the caller belongs to. **`aud` (audience)** says who the token is *for* — the client ID or URI of the receiving API. An API must reject tokens whose audience is some other app; otherwise a token a user obtained for app A can be **replayed** against app B that trusts the same IdP. Validation runs in this order: verify the **signature** against the issuer's public keys, fetched from its OIDC metadata document (`/.well-known/openid-configuration`) and **JWKS** endpoint, then check `iss`, `aud`, and the time claims **`exp`** (expiry) and **`nbf`** (not before), allowing a few minutes of clock skew. Common mistakes: turning off audience validation to "make it work", or trusting any issuer that resolves to a valid key set — which in multi-tenant setups means trusting every tenant in the world.

## Providers
- **Azure** — Microsoft Entra ID: `iss` is `https://login.microsoftonline.com/{tenant-id}/v2.0`; `aud` is the API's application (client) ID or App ID URI.
- **AWS** — Amazon Cognito: `iss` is `https://cognito-idp.{region}.amazonaws.com/{user-pool-id}`; access tokens carry `client_id` rather than `aud`, so check that instead.
- **Google Cloud** — Google ID tokens: `iss` is `https://accounts.google.com`; `aud` is your OAuth client ID.
- **Others** — Auth0 / Okta: `iss` is your tenant or authorization-server URL; `aud` is the API identifier you register.

## Source
IETF RFC 7519 (JSON Web Token), May 2015; validation rules tightened in RFC 8725 (JWT Best Current Practices, 2020).

---

## Compass

**Roots** — *where this comes from*
These are claims inside the [[Bearer Token]] issued by an [[Identity Provider (IdP)]] during [[OAuth 2.0 and OIDC]] flows.

**Paths** — *where this leads*
The validated issuer drives [[Tenant Resolution]] and, downstream, [[Multi-Tenant Data Isolation]]. Checking both claims is the first step of [[Authentication]] in the API's [[Middleware]].

**Neighbors** — *what lives nearby*
[[Origin Verification]] asks "which route did this request take?"; issuer and audience ask "who vouched for this caller, and for whom?". [[Machine-to-Machine Authentication]] tokens need the same checks.

**Clash** — *what pushes against this*
Libraries validate these by default, which breeds complacency — a single `ValidateAudience = false` silently undoes it. Multi-tenant apps cannot pin one issuer, so they must build and maintain their own trusted-tenant list.
