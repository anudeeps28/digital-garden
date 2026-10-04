---
type: atomic
tags: [coding/security, coding/networking, web]
date: 2026-10-04
---

# DNS Rebinding

## Idea
An attacker's domain first points at their server, then quickly re-points at 127.0.0.1. The browser still thinks it's talking to the same site, so the attacker's page can now read your local services.

## Definition
**DNS rebinding** defeats the browser's same-origin policy by changing what a hostname resolves to after the page loads. The victim visits `evil.example`, which serves JavaScript and a DNS record with a tiny TTL. The attacker then answers the next lookup with `127.0.0.1` or a private LAN address. Scripts on the page keep making requests to `evil.example`, which the browser treats as same-origin, but they now land on a router admin page, a local dev server or an IoT device that assumed "only things on this machine can reach me". The key defence on the server is to **validate the `Host` header**: a local service should only answer requests whose Host is `localhost` or `127.0.0.1` (plus its port), because a rebound request still carries `Host: evil.example`. A worked example: a local tool rejected non-loopback Host headers before serving the page that embedded its session token, so a rebound page could never fetch that token.

## Source
The underlying flaw was described by Dean, Felten and Wallach in 1996 against Java applets. The term and modern analysis come from Jackson, Barth, Bortz, Shao and Boneh, "Protecting Browsers from DNS Rebinding Attacks" (ACM CCS, October 2007).

---

## Compass

**Roots** — *where this comes from*
It attacks the assumption that network location equals trust, the same assumption [[Zero Trust]] rejects: "it's on localhost" is not a credential.

**Paths** — *where this leads*
Host-header checks are a form of [[Origin Verification]], and any local server that also speaks [[WebSocket]] needs the handshake checks from [[Cross-Site WebSocket Hijacking]] as well.

**Neighbors** — *what lives nearby*
Browsers' Private Network Access work and resolver-level filtering of private IPs are layered mitigations, a textbook case of [[Defence in Depth]], since no single layer stops every variant.

**Clash** — *what pushes against this*
Strict Host checks break legitimate setups such as custom local hostnames or access through a [[Reverse Proxy]], so the allowlist has to be configurable rather than hardcoded to one value.
