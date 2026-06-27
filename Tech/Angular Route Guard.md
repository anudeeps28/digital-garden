---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# Angular Route Guard

## Idea
A route guard is a function that runs before navigation and decides whether the user is allowed onto a route — blocking access unless some condition holds.

## Definition
In modern Angular a guard is a `CanActivateFn` attached to a route. It returns `true` to allow navigation, `false` to block it, or a `UrlTree` to redirect elsewhere. Common conditions are "is the user authenticated?" or "does the user hold the required role?" In practice, a guard on a protected route checks whether the user is authenticated via an auth service (e.g., delegating to [[Entra ID]] or an OAuth provider) and redirects unauthenticated users to the login flow before they can reach the route — the client-side counterpart to [[Authorization]] checks the [[REST API]] enforces on the server. The guard handles "can you even see this page," while the [[HTTP Interceptor]] handles "is your token attached when you call the API."

## Source
Angular documentation on route guards; feature introduced in Angular 2+ (2016). The `CanActivateFn` functional API was modernized in Angular 14+ (2022) as part of the shift toward functional guards over class-based implementations.

---

## Compass

**Neighbors** — *what lives nearby*
[[Authorization]] and [[Authentication]] both gate access based on identity or role, though the guard sits on the UI side making the initial access decision, while [[Authentication]] checks whether the user is signed in at all.

**Clash** — *what pushes against this*
A public route with no guard sits on the opposite end of the spectrum — open to anyone, authenticated or not.

**Roots** — *where this comes from*
[[MSAL Authentication]] supplies the auth state that the guard inspects to make its decision.

**Paths** — *where this leads*
When a guard blocks access, the application redirects the user to the login flow, and at the request level the [[HTTP Interceptor]] serves as the complementary enforcement mechanism that ensures tokens are attached to API calls.
