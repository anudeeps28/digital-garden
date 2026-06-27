---
type: atomic
tags: [coding/security, coding/auth]
date: 2026-04-24
---

# OAuth 2.0 and OIDC

## Idea
OAuth 2.0 is a delegated *authorization* protocol — "let app A act on my behalf at service B" — and OpenID Connect (OIDC) is a thin identity layer on top that adds *authentication* — "and tell A who I am."

## Definition
OAuth 2.0 defines flows where a **client** (your app) asks an **authorization server** ([[Entra ID]], Auth0, Okta) for an **access token** that lets it call a **resource server** (an API) on behalf of a **resource owner** (the user). The most common flow today is **Authorization Code with PKCE** — the user logs in at the auth server's hosted page, the auth server redirects back to the app with a one-time code, the app trades the code for an access token. The access token (often a [[Bearer Token|JWT]]) is what the app sends to the API.

OIDC extends OAuth: in addition to the access token, the auth server returns an **ID token** that contains claims about the user (subject ID, email, name). The ID token is for the *app* (proves who logged in); the access token is for the *API* (proves what you're allowed to do). Mixing them up is a classic security bug — never use an ID token as an API credential.

## Source
CI/CD learning session — the protocol underneath every Entra ID interaction.

---

## Compass

**Neighbors** — *what lives nearby*
[[Authentication]] is what OIDC adds to the authorization layer, and [[Authorization]] is what OAuth grants through delegation. SAML 2.0 is an older, XML-based equivalent that serves enterprise SSO with similar goals.

**Clash** — *what pushes against this*
Basic Auth sends credentials in every request without delegation, Cookie-session auth relies on server-side state rather than token exchange, and API keys provide no user identity at all — stripping away the identity and authorization separation that OAuth and OIDC provide.

**Roots** — *where this comes from*
[[Entra ID]] acts as the auth server in modern enterprise stacks, and the broader question of Token-based vs session-based auth informs how OAuth's token model fits into authentication architecture.

**Paths** — *where this leads*
[[Bearer Token]] is the access token's most common form, and [[SPA Redirect URIs]] determine where the auth code lands in browser applications. Refresh tokens extend the credential's lifetime by minting new access tokens, while Scopes and consent define the user-granted permission boundaries that gate what the app can actually do.
