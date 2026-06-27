---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# HTTP Interceptor

## Idea
An HTTP interceptor is Angular middleware that sits in front of every outgoing request — the perfect place to automatically attach the auth token.

## Definition
An interceptor is a function (in modern Angular, a `HttpInterceptorFn`) registered globally that receives each outgoing request, can modify it, and passes it along the chain before it hits the network. It's the client-side mirror of backend [[Middleware]]: a single chokepoint every request flows through. In practice, an interceptor can silently acquire credentials and attach a [[Bearer Token]] `Authorization` header on calls to protected [[REST API]]s — so individual services never need to hand-roll auth headers themselves. Because requests are [[RxJS Observable|Observables]], the interceptor composes cleanly into that reactive pipeline.

## Source
Google Angular Team, introduced as a core feature in Angular 4.3 (2017). HTTP Interceptors formalized the middleware pattern for client-side HTTP request transformation; prior frameworks used similar middleware concepts, but Angular standardized it as an interceptor architecture.

---

## Compass

**Neighbors** — *what lives nearby*
The [[Middleware]] pattern is its backend equivalent — both are a pipeline every request passes through. The interceptor works hand-in-hand with [[MSAL Authentication]], which supplies the token that the interceptor attaches to each request.

**Clash** — *what pushes against this*
Manually setting the `Authorization` header on each individual HTTP call is the opposite approach — repetitive, error-prone, and spreads auth logic across the codebase.

**Roots** — *where this comes from*
The interceptor exists to enforce [[Authentication]] transparently, ensuring every protected API call carries valid credentials without requiring explicit auth logic in each service.

**Paths** — *where this leads*
The interceptor injects [[Bearer Token]]s into requests, and [[REST API]] endpoints receive these authenticated calls with valid authorization headers already in place.
