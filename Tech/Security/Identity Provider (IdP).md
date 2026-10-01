---
type: atomic
tags: [coding/security, coding/identity, security]
date: 2026-10-01
---

# Identity Provider (IdP)

## Idea
Instead of every app keeping its own list of usernames and passwords, apps hand the whole job of "who is this person?" to one trusted system — and believe whatever it signs.

## Definition
An identity provider is the system that holds user accounts, checks sign-in (password, MFA, passkey), and issues signed tokens that applications trust. An app **delegates login** to it: it redirects the user to the IdP, the IdP verifies them, and the app receives a token via [[OAuth 2.0 and OIDC]] or SAML — the app never sees the password. Accounts live in a **tenant** (also called a directory): one isolated container per organization, with its own users, groups, policies and signing settings. A **multi-tenant** app accepts sign-ins from many directories, so a token can come from any customer's tenant, and the app must decide which tenants it trusts. The gotcha: an external partner's staff live in *their own* tenant, not yours — you don't own their accounts, their MFA, or their leavers process; you only choose whether to accept their tokens (or invite them as guests). IdPs also split by audience: **workforce identity** (employees, managed by IT, tied to HR) versus **customer identity** (CIAM: public self-sign-up, social logins, millions of accounts, branding). Same protocols, very different scale and risk.

## Providers
- **Azure** — Microsoft Entra ID for workforce tenants; Microsoft Entra External ID for customer and partner identities.
- **AWS** — AWS IAM Identity Center for workforce sign-in to AWS accounts and apps; Amazon Cognito user pools for customer identity.
- **Google Cloud** — Google Cloud Identity (the directory behind Google Workspace); Identity Platform for customer sign-in.
- **Others** — Okta (workforce) and Auth0 by Okta (customer identity); Keycloak as the open-source, self-hosted option.

## Source
The pattern formalized with federated identity standards: SAML 2.0 (OASIS, 2005) and OpenID Connect Core 1.0 (OpenID Foundation, 2014).

---

## Compass

**Roots** — *where this comes from*
It is [[Authentication]] pulled out of the app and centralized, speaking [[OAuth 2.0 and OIDC]] to every app that trusts it.

**Paths** — *where this leads*
The IdP is where [[Conditional Access]] policies run, where [[SCIM Provisioning]] pushes users from, and whose identity the API checks via [[Token Issuer and Audience]]. In a multi-tenant app, the issuing tenant feeds [[Tenant Resolution]].

**Neighbors** — *what lives nearby*
[[MSAL Authentication]] is one client library for talking to an IdP; the [[Bearer Token]] is what it hands back. [[Machine-to-Machine Authentication]] uses the same IdP for services instead of people.

**Clash** — *what pushes against this*
Centralizing identity makes the IdP a single point of failure and a prize target: if it goes down nobody signs in, and if it is compromised every app that trusts it is compromised too.
