---
type: atomic
tags: [coding/azure, devops, web, coding/security]
date: 2026-09-16
---

# Azure Front Door

## Idea
Front Door is the single public face of an Azure application — the thing users actually connect to, which then decides which of your backends deserves the request.

## Definition
Azure Front Door is a global edge service combining a CDN, a layer-7 load balancer, TLS termination, and a [[Web Application Firewall (WAF)|WAF]]. Its model is three nested pieces: **routes** match an incoming path pattern and point at an **origin group**, which contains one or more **origins** (your actual backends). Each origin group carries a [[Health Probe]] configuration, and each route can carry caching and rewrite rules. It comes in two tiers — Standard and Premium — and the difference is not cosmetic: managed WAF rule sets and Private Link to origins are Premium-only, which makes [[Tier-Gated Features]] a real deployment hazard. Because Front Door is the single entry point, backends must enforce [[Origin Verification]] to stop anyone reaching them directly.

## Source
Microsoft Azure; the current Standard/Premium generation shipped in 2021, replacing the classic Front Door SKU.

---

## Compass

**Roots** — *where this comes from*
It's the concrete Azure implementation of [[Single Origin Ingress]], and is typically declared in [[Bicep]] alongside the rest of the environment.

**Paths** — *where this leads*
Routing by path prefix forces each backend to do [[Path Base Stripping]]; origin groups need a [[Health Probe]] path; the public entry point is where [[Rate Limiting]] and WAF rules live.

**Neighbors** — *what lives nearby*
CloudFront and Cloudflare occupy the same position in their ecosystems; an API gateway does the same job one layer in.

**Clash** — *what pushes against this*
Every request now makes an extra hop, debugging gains a layer, and the Premium tier costs meaningfully more per month — a real trade-off, not a technicality.
