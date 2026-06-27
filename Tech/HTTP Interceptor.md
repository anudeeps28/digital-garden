---
type: atomic
tags: [coding/angular, frontend]
date: 2026-06-26
---

# HTTP Interceptor

## Idea
An HTTP interceptor is Angular middleware that sits in front of every outgoing request — the perfect place to automatically attach the auth token.

## Definition
An interceptor is a function (in modern Angular, a `HttpInterceptorFn`) registered globally that receives each outgoing request, can modify it, and passes it along the chain before it hits the network. It's the client-side mirror of backend [[Middleware]]: a single chokepoint every request flows through. In the AI document ingestion project, the `PlanDocumentRAG.Web` Angular 19 app uses MSAL's interceptor to silently acquire an access token from [[Entra ID]] and attach it as a [[Bearer Token]] `Authorization` header on calls to the protected [[REST API]] — so individual services never hand-roll auth headers. Because requests are [[RxJS Observable|Observables]], the interceptor composes cleanly into that pipeline.

## Source
AI document ingestion project

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
