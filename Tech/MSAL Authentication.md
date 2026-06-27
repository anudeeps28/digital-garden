---
type: atomic
tags: [coding/angular, frontend, auth]
date: 2026-06-26
---

# MSAL Authentication

## Idea
MSAL (Microsoft Authentication Library) is the library the Angular app uses to log users in through Entra ID and obtain access tokens for calling the API.

## Definition
MSAL handles the messy parts of the [[OAuth 2.0 and OIDC]] flow for you — redirecting to Microsoft's login page, caching tokens, and silently refreshing them. The Angular flavour (`@azure/msal-angular`) plugs into the framework with a guard, an interceptor, and providers. In practice, MSAL can be used to sign users in against [[Entra ID]], then acquire an access token scoped to a backend [[REST API]]. That token rides along as a [[Bearer Token]] via the [[HTTP Interceptor]], while an [[Angular Route Guard]] keeps unauthenticated users off protected routes. The MSAL config (client ID, authority, [[SPA Redirect URIs]], API scope) is typically loaded from runtime configuration so the same build works across environments.

## Source
Microsoft, introduced in the Azure ecosystem; formalized as the Microsoft Authentication Library (MSAL) for various platforms including web, mobile, and desktop (first release for .NET, 2016; JavaScript support added 2018).

---

## Neighbors — *what lives nearby*
MSAL is a client implementation of [[OAuth 2.0 and OIDC]], and it authenticates against [[Entra ID]], the identity provider that actually validates credentials.

## Clash — *what pushes against this*
MSAL delegates identity management to a trusted provider, as opposed to a hand-rolled username/password login form where you store credentials yourself.

## Roots — *where this comes from*
[[Authentication]] is the foundational concern here — MSAL is how this app proves who the user is.

## Paths — *where this leads*
MSAL acquires an [[Bearer Token]] that gets attached to requests via the [[HTTP Interceptor]], and the [[SPA Redirect URIs]] must be registered in Entra ID for the redirect flow to work.
