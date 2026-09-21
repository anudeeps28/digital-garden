---
type: atomic
tags: [coding/security, devops, web, api]
date: 2026-09-16
---

# Origin Verification

## Idea
Putting a guarded front door on a building is pointless if the back windows are still open — so the building itself has to refuse anyone who didn't come through the door.

## Definition
Origin verification is the backend's check that a request genuinely arrived via the intended edge service rather than directly at the origin's own address. Edge platforms inject a secret or identifier into every forwarded request — Azure Front Door sends an `X-Azure-FDID` header carrying the profile's unique id, Cloudflare uses authenticated origin pull certificates, CloudFront supports a custom origin header — and the backend rejects anything without the expected value. Without it, an attacker who discovers the origin hostname simply walks around [[Web Application Firewall (WAF)|WAF]], [[Rate Limiting]], and every other edge control. The check must run early in the [[Middleware]] pipeline, before any real work happens, and it pairs with forwarded-header handling restricted to the edge's known IP ranges — otherwise a client can spoof its own `X-Forwarded-For` and poison whatever you keyed off the caller's address.

## Source
Documented as required practice by Azure Front Door, AWS CloudFront (custom origin headers), and Cloudflare (authenticated origin pulls).

---

## Compass

**Roots** — *where this comes from*
It's the missing half of [[Single Origin Ingress]] — consolidating the entrance only helps if the alternatives are closed.

**Paths** — *where this leads*
Once the origin is trusted, forwarded headers can be trusted, which is what makes per-caller [[Rate Limiting]] and accurate [[Structured Logging]] possible.

**Neighbors** — *what lives nearby*
[[Bearer Token]] verification answers "who is this caller"; origin verification answers "which route did they take". Both are gates in the same [[Middleware]] pipeline.

**Clash** — *what pushes against this*
It couples the backend to one edge provider, and the shared identifier is a static secret — real but shallow protection compared with mutual TLS.
