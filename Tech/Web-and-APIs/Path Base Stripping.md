---
type: atomic
tags: [coding/dotnet, coding/web-api, web, coding/architecture]
date: 2026-09-16
---

# Path Base Stripping

## Idea
When an edge router puts your service behind a path prefix, the service still thinks it lives at the root — so something has to peel the prefix off before routing looks at the URL.

## Definition
Path base stripping is the step that removes a mounting prefix from the incoming request path and records it separately, so an application written for `/orders` still works when it's published at `/api/shop/orders`. In ASP.NET Core this is `app.UsePathBase("/api/shop")`, which moves the matched segment from `Request.Path` into `Request.PathBase`, keeping generated links correct. The sharp edge is ordering: if you don't call `UseRouting()` explicitly after `UsePathBase`, the framework auto-inserts routing at the very start of the pipeline, routing runs against the unstripped path, and the strip silently never applies. This is the general hazard of [[Middleware]] — the pipeline is order-dependent, and a wrong order produces no error, just wrong behaviour.

## Source
ASP.NET Core middleware documentation (Microsoft); equivalent concepts are `ProxyPass`/`X-Forwarded-Prefix` in nginx and `root_path` in [[FastAPI]].

---

## Compass

**Roots** — *where this comes from*
The need arises the moment you adopt [[Single Origin Ingress]] and route several services under one hostname.

**Paths** — *where this leads*
Get it wrong and every route 404s or every generated URL is malformed — the class of bug that [[Integration Tests]] catch and unit tests never will.

**Neighbors** — *what lives nearby*
It's one entry in the [[Middleware]] pipeline, sitting near [[Origin Verification]] and forwarded-header handling at the front.

**Clash** — *what pushes against this*
An alternative is to make the service prefix-aware in its own route definitions — simpler to trace, but it hard-codes deployment topology into application code.
