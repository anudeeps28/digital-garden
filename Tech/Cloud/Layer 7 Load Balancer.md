---
type: atomic
tags: [coding/azure, coding/security, devops, coding/networking, web]
date: 2026-10-01
---

# Layer 7 Load Balancer

## Idea
A load balancer that reads the HTTP request (hostname, path, headers) before deciding where to send it. Because it understands the request, it can route, terminate TLS and filter attacks, not just spread connections around.

## Definition
A Layer 7 load balancer is a regional reverse proxy that understands HTTP. Traffic enters on **frontend IPs**, which can be public, private or both. A private-only frontend with no public DNS record can be reached only from inside the network. A **listener** is the thing that answers: an IP, a port and a hostname, plus a protocol and, for HTTPS, a TLS certificate. **Routing rules** connect each listener to a **backend pool** (VMs, containers, app services), either directly or through a path map. **Health probes** remove failing backends, and an optional [[Web Application Firewall (WAF)|WAF]] inspects requests on the way in. A Layer 4 load balancer, by contrast, forwards TCP/UDP connections by IP and port and never reads the HTTP inside, so it is faster but cannot route by host or path. A global [[Edge Gateway]] does Layer 7 work too, but at the internet edge across many regions, while this sits inside one region, often behind the edge. The key insight is about where traffic comes from. Whichever frontend or listener a request arrives on, all gateway instances reach the backends from the same subnet, so the backend cannot tell by source IP which listener the request came through. If public and private listeners must be treated differently, identity has to carry that distinction: tokens, headers or [[Origin Verification|origin checks]].

## Providers
- **Azure** — Application Gateway v2: frontend IPs, listeners, rules, backend pools, probes and an integrated WAF, deployed into its own subnet.
- **AWS** — Application Load Balancer: listeners with rules routing to target groups, with AWS WAF attached.
- **Google Cloud** — external and internal Application Load Balancers, using forwarding rules, URL maps and backend services.
- **Others** — NGINX, Envoy, HAProxy and Traefik, often as a Kubernetes ingress controller.

## Source
The OSI model (ISO 7498, 1984) gives the "Layer 7" name; the pattern grew from reverse proxies such as NGINX (2004) and HAProxy (2001).

---

## Compass

**Roots** — *where this comes from*
It's a reverse proxy with scaling and [[Health Probe|health probes]] built in, the regional form of [[Single Origin Ingress]].

**Paths** — *where this leads*
Its routing choices are spelled out in [[Path-Based vs Host-Based Routing]], and a path map often needs [[Path Base Stripping]] on the backend. It works best in front of [[Stateless Services]] that any instance can serve.

**Neighbors** — *what lives nearby*
An [[Edge Gateway]] handles the global edge; [[Managed Web Hosting (PaaS)]] and [[Serverless Functions]] are typical backends. [[Default-Deny Allowlisting]] on the backend subnet keeps traffic flowing only through the gateway.

**Clash** — *what pushes against this*
Being in the request path means it adds latency, cost and one more thing to scale and patch. Because it hides the client's real address behind its own subnet, network rules on the backend can no longer distinguish callers; you have to trust forwarded headers or rely on identity.
