---
type: atomic
tags: [coding/security, web, frontend]
date: 2026-10-04
---

# PKCE

## Idea
PKCE lets an app that cannot keep a secret, like a browser app or a mobile app, still use the OAuth authorization code flow safely. It proves that whoever swaps the code for a token is the same party that started the login.

## Definition
**Proof Key for Code Exchange** (said "pixy") adds a one-time secret to the authorization code flow. Before redirecting to the login page, the app generates a random **code verifier**, hashes it with SHA-256 to get a **code challenge**, and sends only the challenge. When the user comes back with `?code=...`, the app sends the code plus the original verifier to the token endpoint, which hashes the verifier and checks it matches. An attacker who intercepts the code (through a malicious app registered for the same redirect, browser history, or logs) cannot redeem it without the verifier. A worked example: a browser-only [[Single-Page Application (SPA)|SPA]] for a music-streaming API ran the whole flow client-side, keeping the verifier in `sessionStorage` for the round trip, stripping `?code=` from the address bar right after the exchange, and refreshing before the access token's roughly one-hour lifetime ran out. No client secret was ever shipped to the browser.

## Source
RFC 7636, "Proof Key for Code Exchange by OAuth Public Clients" (Sakimura, Bradley, Agarwal, IETF, September 2015), written for native apps. The OAuth 2.0 Security Best Current Practice (RFC 9700, 2025) and the OAuth 2.1 draft now recommend PKCE for all clients, including confidential ones.

---

## Compass

**Roots** — *where this comes from*
PKCE is a patch on the authorization code flow from [[OAuth 2.0 and OIDC]], needed because public clients cannot hold the client secret that the original flow relied on.

**Paths** — *where this leads*
What comes out the other end is a [[Bearer Token]], so the next problems are storage and expiry, and the token's [[Token Issuer and Audience|audience]] decides which APIs will accept it.

**Neighbors** — *what lives nearby*
Libraries such as [[MSAL Authentication|MSAL]] run PKCE for you in browser apps, and it is one of the reasons a pure [[Single-Page Application (SPA)]] no longer needs a backend just to log in.

**Clash** — *what pushes against this*
PKCE protects the code exchange, not the token afterwards; a token sitting in browser storage is still exposed to [[Cross-Site Scripting (XSS)]], which is why some teams prefer a backend-for-frontend that keeps tokens server-side.
