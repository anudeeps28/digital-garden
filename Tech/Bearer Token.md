---
type: atomic
tags: [coding/security]
date: 2026-03-24
---

# Bearer Token

## Idea
A bearer token (JWT) is a signed token the client sends with every request to prove its identity — whoever "bears" the token is authenticated.

## Definition
A Bearer Token is a security token included in the `Authorization` header of HTTP requests: `Authorization: Bearer eyJhbG...`. These are often JWTs (JSON Web Tokens) — compact, signed [[JSON]] objects containing claims like user ID, email, roles, and expiration time. An identity provider issues the token after login, and the client includes it in every [[REST API]] request. The API's [[Middleware]] validates the token's signature (proving it wasn't tampered with), checks it hasn't expired, and extracts the user's identity and roles for [[Authorization]]. The token is "bearer" style — anyone holding a valid token is authenticated, so tokens must be kept secret.

## Source
RFC 6750 (OAuth 2.0 Bearer Token Usage), Internet Engineering Task Force, October 2012. Bearer tokens became a standard part of OAuth 2.0 for API authentication and are widely used with JSON Web Tokens (JWTs) as defined in RFC 7519 (2015).

---

## Compass

**Neighbors** — *what lives nearby*
[[API Key]] is a simpler authentication mechanism that's less secure and has no expiration by default, while [[Session Cookie]] handles web browser authentication using server-side state.

**Clash** — *what pushes against this*
[[Basic Auth]] requires sending username and password with every request, which is far less secure than bearer tokens, whereas [[No Authentication]] foregoes any token requirement entirely.

**Roots** — *where this comes from*
Bearer tokens serve the fundamental purpose of [[Authentication]] to prove identity, and in this system [[Entra ID]] is responsible for issuing and signing the tokens.

**Paths** — *where this leads*
The tokens carry role claims that enable [[Authorization]] for permission checks, and [[Middleware]] in the API pipeline validates these tokens during request processing. Proper key management is critical for maintaining the security of token signatures.
