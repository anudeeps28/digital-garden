---
type: atomic
tags: [coding/security]
date: 2026-03-24
---

# Authentication

## Idea
Authentication is proving who you are — verifying your identity before granting access to the system.

## Definition
Authentication (authn) answers the question "Who are you?" In the KBA project, when a client calls the [[REST API]], it must include a [[Bearer Token]] (a [[JWT]] issued by [[Entra ID]]). The API's [[Middleware]] validates this token — checking its signature, expiration, and issuer — before allowing the request to reach the [[Controller]]. If the token is missing or invalid, the API returns a `401 Unauthorized` [[HTTP Status Codes|status code]]. Authentication is distinct from [[Authorization]] — authentication proves identity, authorization checks permissions.

## Source
KBA AI Document Ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Authentication is fundamentally what [[OAuth 2.0]] enables — the authorization framework that Entra ID implements to prove identity. Similarly, [[Single Sign-On (SSO)]] extends authentication so you only need to prove yourself once to access multiple services.

**Clash** — *what pushes against this*
[[Anonymous Access]] represents the opposite approach — it requires no identity verification at all. It's also crucial to distinguish authentication from [[Authorization]], where authentication answers "who are you?" while authorization answers "what are you allowed to do?"

**Roots** — *where this comes from*
Authentication sits as a foundational concept within [[Security Concepts]], the larger domain of security practices. [[Entra ID]] is the concrete implementation — the identity provider that handles the actual authentication work in modern systems.

**Paths** — *where this leads*
Authentication directly enables the use of [[Bearer Token|bearer tokens]] as proof of identity, which are typically implemented as [[JWT|JWTs]]. Once authenticated, the next step is [[Authorization]] to determine what permissions the user has, and the [[Middleware]] layer validates tokens on every request to enforce authentication.
