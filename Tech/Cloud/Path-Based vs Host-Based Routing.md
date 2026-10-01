---
type: atomic
tags: [coding/azure, devops, coding/networking, web, api]
date: 2026-10-01
---

# Path-Based vs Host-Based Routing

## Idea
A gateway can decide where a request goes by looking at the hostname (which site was asked for) or at the path (which part of the site). The hostname is the better place to set separate rules for different audiences; the path is the better way to keep everything under one address.

## Definition
**Host-based routing** sends requests to a backend according to the hostname in the request. In practice that means one listener per hostname: `a.example.com` goes to one set of rules and `b.example.com` to another. **Path-based routing** splits traffic within a single host by URL path, so `/api/*` goes to the API, `/auth/*` to the identity service, and everything else to the frontend. The rules live in a **path map** (Azure) or **URL map** (Google), which is checked in order with a default backend for anything unmatched. The two are usually combined: many hostnames, each with its own listener, all pointing at one shared path map, so every site has the same `/api` and `/auth` layout. The trade-off is where policy can attach. Policy such as WAF rules, rate limits, certificates and allowed callers hangs off the listener, so host-based routing lets you give each customer or audience its own settings. Path-based routing gives a **single origin**: the browser sees one domain, which removes CORS and cookie-scope problems. The cost is that every path under that host shares one policy, and backends must cope with being mounted under a prefix.

## Providers
- **Azure** — Application Gateway (multi-site listeners plus URL path maps); Front Door routes match on domain and path patterns.
- **AWS** — Application Load Balancer listener rules with `host-header` and `path-pattern` conditions; CloudFront cache behaviours by path.
- **Google Cloud** — URL maps with host rules and path matchers on the Application Load Balancer.
- **Others** — Kubernetes Ingress (`host` and `path` fields), NGINX `server_name` and `location` blocks, Traefik `Host()` and `PathPrefix()` rules.

## Source
Host-based routing became possible with the HTTP/1.1 `Host` header (RFC 2616, 1999) and, for HTTPS, TLS Server Name Indication (RFC 3546, 2003). Path routing is standard reverse-proxy behaviour.

---

## Compass

**Roots** — *where this comes from*
Both are features of a [[Layer 7 Load Balancer]] or [[Edge Gateway]], which can read the hostname and path because they understand HTTP.

**Paths** — *where this leads*
Path-based routing is how you build [[Single Origin Ingress]], and it usually forces [[Path Base Stripping]] so an app mounted at `/api` still sees its own routes.

**Neighbors** — *what lives nearby*
[[CORS]] is the problem path-based routing makes disappear; [[Web Application Firewall (WAF)|WAF]] and [[Rate Limiting]] policies are what host-based routing lets you vary per audience.

**Clash** — *what pushes against this*
Host-based routing multiplies certificates, DNS records and listeners, and gateways have hard limits on how many you can have. Path-based routing leaks routing into the app: hard-coded absolute URLs, redirects and cookie paths break when a prefix is added or changed.
