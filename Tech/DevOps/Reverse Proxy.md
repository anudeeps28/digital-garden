---
type: atomic
tags: [devops, coding/networking, web]
date: 2026-10-04
---

# Reverse Proxy

## Idea
A reverse proxy is the single front door that receives all incoming traffic and forwards each request to the right service behind it.

## Definition
A forward proxy acts for clients going out; a reverse proxy acts for servers coming in. Clients only ever talk to the proxy, which then routes requests to internal services. Its everyday jobs are **TLS termination** (it holds certificates and speaks HTTPS so apps can speak plain HTTP on a private network), **host-based routing** (`app.example.com` to one container, `api.example.com` to another), path routing, compression, caching, rate limits and load balancing across several copies of a service. On a single server running many containers, a modern proxy can **discover routes automatically** from container labels and request certificates from Let's Encrypt on its own, so deploying a new app is just starting a container with the right labels. Because it sees every request, it is also the natural place for access logs, security headers and an allowlist. The trade-off is that it becomes a single point of failure and a place where misconfiguration (wrong forwarded headers, missing timeouts) causes confusing bugs.

## Tools
- **Traefik** — container-native, reads Docker labels, built-in Let's Encrypt.
- **Caddy** — automatic HTTPS by default with a short config file.
- **nginx** — the long-standing workhorse; HAProxy for high-performance load balancing.

## Source
Reverse proxying was common by the late 1990s (Squid accelerator mode, Apache mod_proxy). nginx (Igor Sysoev, public in 2004) made it standard; Traefik (2015) and Caddy (2015) brought automatic discovery and certificates.

---

## Compass

**Roots** — *where this comes from*
It is a [[Layer 7 Load Balancer]] in its simplest self-hosted form, and the same role an [[Edge Gateway]] plays in managed clouds.

**Paths** — *where this leads*
Routing decisions follow [[Path-Based vs Host-Based Routing]], and putting every app behind one entry point leads to [[Single Origin Ingress]] and simpler [[CORS]].

**Neighbors** — *what lives nearby*
[[Docker Compose]] usually runs it on a shared external network with the apps, and a [[Web Application Firewall (WAF)]] often sits in the same spot.

**Clash** — *what pushes against this*
Apps behind a proxy can mis-read the client IP or scheme unless forwarded headers are trusted correctly, and one proxy is one [[Blast Radius]] for every site on the box.
