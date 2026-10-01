---
type: atomic
tags: [coding/security, coding/identity, coding/web-api, coding/architecture]
date: 2026-10-01
---

# Tenant Resolution

## Idea
Before a multi-tenant app does anything, it has to answer "which customer is this request for?" — and if the caller can choose that answer, the caller can choose someone else's data.

## Definition
Tenant resolution is the step, usually early in the [[Middleware]] pipeline, that works out which tenant a request belongs to and attaches that to the request for everything downstream. The resolved tenant then does real work: it selects the [[Connection String]] or database (in per-tenant [[Tenancy Models]]), sets the tenant ID used by [[Global Query Filters]], and feeds the session value that [[Row-Level Security]] checks. The rule is that the final answer must come from something the caller **cannot forge** — the **validated token**: its issuer, or a **tenant claim** signed by the identity provider (see [[Token Issuer and Audience]]). A header like `X-Tenant-Id`, a subdomain like `acme.example.com`, or a `?tenant=` query string are fine as *hints* — for routing or showing the right login page — but on their own they are just text the caller typed. The failure mode is simple and severe: resolve from an untrusted input and a logged-in user of tenant A changes one value and is served tenant B's data with a perfectly valid token. If you do use a hint, cross-check it against the token and reject the request when they disagree.

## Providers
- **Azure** — Microsoft Entra ID multi-tenant apps put the customer's directory ID in the `tid` claim (and in the v2 issuer URL); the app maps `tid` to its own tenant record.
- **AWS** — Amazon Cognito: a user pool per tenant (the issuer identifies the tenant) or a custom tenant attribute added to tokens, e.g. via a pre-token-generation trigger.
- **Google Cloud** — Identity Platform multi-tenancy issues tokens carrying the tenant ID in the `firebase.tenant` claim.
- **Others** — Auth0 Organizations (`org_id` claim); Finbuckle.MultiTenant for ASP.NET Core, which offers host, route, header, and claim strategies and hands the resolved tenant (including its connection string) to the rest of the app.

## Source
Standard practice in multi-tenant SaaS design; documented in Microsoft Entra multi-tenant app guidance, AWS SaaS Factory identity guidance, and the Finbuckle.MultiTenant documentation.

---

## Compass

**Roots** — *where this comes from*
It rests on [[Authentication]] and [[Bearer Token]] validation — the tenant is only trustworthy once the token is, which is why the [[Identity Provider (IdP)]] is the real source of the answer.

**Paths** — *where this leads*
The resolved tenant drives [[Global Query Filters]], [[Row-Level Security]], and the database choice in [[Tenancy Models]] — all layers of [[Multi-Tenant Data Isolation]].

**Neighbors** — *what lives nearby*
[[Authorization]] decides what a user may do *within* a tenant; tenant resolution decides *which* tenant they're in. [[Origin Verification]] makes the same "don't trust what the caller says about itself" argument for routes.

**Clash** — *what pushes against this*
Users who belong to several tenants break "one token, one tenant" — you end up with a tenant switcher, re-issued tokens, or a header that must be checked against a membership list, each adding complexity and new ways to get it wrong.
