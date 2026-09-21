---
type: atomic
tags: [coding/architecture, coding/security, devops, web]
date: 2026-09-16
---

# Single Origin Ingress

## Idea
If every service has its own public address, you have as many front doors as services — and you will secure some of them better than others.

## Definition
Single origin ingress means all external traffic enters the system through exactly one public hostname, which then routes internally to the right backend by path. A single edge service — a CDN or reverse proxy such as [[Azure Front Door]], CloudFront, or an ingress controller — owns TLS, [[Web Application Firewall (WAF)|WAF]] rules, [[Rate Limiting]], and routing, and the backends stop being directly reachable. The payoff is that hardening is written once and cannot drift between services, and [[CORS]] largely disappears because the browser only ever sees one origin. The cost is that each backend now receives requests under a path prefix it wasn't written for, so it needs a path-base step to strip the prefix before routing — see [[Path Base Stripping]].

## Source
A standard pattern in edge and API-gateway architecture; described as the API Gateway pattern in Chris Richardson's *Microservices Patterns* (2018) and in CDN reference architectures.

---

## Compass

**Roots** — *where this comes from*
It's the consolidation step that makes [[Defence in Depth]] affordable at the edge — one place to apply every control.

**Paths** — *where this leads*
Once traffic is consolidated you must prove it actually came through the door: [[Origin Verification]]. Routing behind the prefix requires [[Path Base Stripping]], and each backend pool needs a [[Health Probe]].

**Neighbors** — *what lives nearby*
[[Middleware]] is the same idea inside a single process — one pipeline that every request passes through.

**Clash** — *what pushes against this*
One front door is also one blast radius. A misconfiguration at the edge takes everything down at once, where separate per-service endpoints would have failed independently.
