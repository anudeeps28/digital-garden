---
aliases: ["tech/cloud/azure-front-door"]
type: atomic
tags: [coding/azure, devops, web, coding/security, coding/networking]
date: 2026-09-16
---

# Edge Gateway

## Idea
An edge gateway is the single public face of an application — the thing users actually connect to, sitting at the internet's edge close to them, which then decides which of your backends deserves the request.

## Definition
An edge gateway is a globally distributed service combining a CDN, a layer-7 load balancer, TLS termination, and a [[Web Application Firewall (WAF)|WAF]]. Users connect to the nearest point of presence, and the gateway forwards their request over the provider's backbone to your backend. Its model is three nested pieces: **routes** match an incoming hostname and path pattern and point at an **origin group**, which contains one or more **origins** (your actual backends). Each origin group carries a [[Health Probe]] configuration, and each route can carry caching and rewrite rules. Feature tiers matter: managed WAF rule sets and private connections to origins are often reserved for the premium tier, which makes [[Tier-Gated Features]] a real deployment hazard. Because the gateway is the single entry point, backends must enforce [[Origin Verification]] to stop anyone reaching them directly. It differs from a regional [[Layer 7 Load Balancer]], which lives inside one region's network and can also serve private, internal-only traffic.

## Providers
- **Azure** — Azure Front Door (Standard/Premium, 2021, replacing the classic SKU); origins identify it by the `X-Azure-FDID` header.
- **AWS** — Amazon CloudFront, with AWS WAF and custom origin headers.
- **Google Cloud** — Cloud CDN behind the global external Application Load Balancer, with Cloud Armor.
- **Others** — Cloudflare, Akamai, Fastly.

## Source
The CDN-plus-proxy pattern that grew out of content delivery networks (Akamai, 1998) and became the standard internet entry point for cloud applications.

---

## Compass

**Roots** — *where this comes from*
It's the concrete implementation of [[Single Origin Ingress]], and is typically declared in [[Bicep]] or another [[Infrastructure as Code]] tool alongside the rest of the environment.

**Paths** — *where this leads*
Routing by path prefix forces each backend to do [[Path Base Stripping]]; origin groups need a [[Health Probe]] path; the public entry point is where [[Rate Limiting]] and WAF rules live.

**Neighbors** — *what lives nearby*
A [[Layer 7 Load Balancer]] does the same job one layer in, within a region; [[Path-Based vs Host-Based Routing]] is how both decide where a request goes.

**Clash** — *what pushes against this*
Every request now makes an extra hop, debugging gains a layer, and the premium tier costs meaningfully more per month — a real trade-off, not a technicality.
