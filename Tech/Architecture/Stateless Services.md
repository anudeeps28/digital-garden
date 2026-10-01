---
type: atomic
tags: [coding/architecture, coding/distributed-systems, coding/web-api, api]
date: 2026-10-01
---

# Stateless Services

## Idea
If a server forgets every caller the moment it finishes answering, any copy of that server can answer the next request. That forgetting is what lets you add more copies when load grows.

## Definition
A stateless service keeps no per-client memory between requests. Everything it needs either arrives with the request (a [[Bearer Token]] that says who the caller is, IDs in the URL or body) or is read from a **shared store** such as a database, a distributed cache or a queue that every instance can reach. Because no instance holds anything the others lack, a load balancer can send each request to whichever instance is free, and you can add, remove, restart or replace instances without losing anyone's session. That is what makes **horizontal scaling** (more machines rather than a bigger machine) work in practice. The state does not go away; it moves. Login sessions become signed tokens or entries in a shared cache, uploaded files go to object storage, and work in progress goes on a queue. The anti-pattern is **sticky sessions** (session affinity): the load balancer pins each client to the instance that holds its in-memory session. It looks like it works, but load spreads unevenly, a single instance restart logs users out, and scaling in or deploying means draining connections. Being stateless is a property of the process, not of the system: the system still has state, but it lives in places built to share it.

## Providers
- **Azure** — App Service and Container Apps both have an "ARR affinity" / session-affinity toggle; turning it off is the stateless default.
- **AWS** — Application Load Balancer stickiness is opt-in per target group; ElastiCache is the usual shared session store.
- **Google Cloud** — Cloud Run assumes stateless containers and offers session affinity only as best-effort.
- **Others** — Kubernetes Deployments assume interchangeable pods (StatefulSets exist for the exceptions); Redis is the common shared store; the [[REST API|REST]] style requires statelessness between client and server.

## Source
Statelessness is one of the REST constraints in Roy Fielding's doctoral dissertation (2000); the "processes are stateless and share-nothing" rule is factor VI of the Twelve-Factor App (Heroku, 2011).

---

## Compass

**Roots** — *where this comes from*
It's the server-side constraint behind [[REST API|REST]], and the precondition for the horizontal scaling described in [[Scalability-and-Load-Parameters]].

**Paths** — *where this leads*
Once instances are interchangeable you can run them as [[Serverless Functions]] or let them [[Scale-to-Zero]], because nothing is lost when an instance disappears.

**Neighbors** — *what lives nearby*
[[In-Memory Caching]] is the tempting exception: fine for data that is the same for everyone, dangerous for per-user data that another instance won't see. A [[Layer 7 Load Balancer]] is what spreads requests across the stateless copies.

**Clash** — *what pushes against this*
Every request now pays a round trip to the shared store, and that store becomes the new bottleneck and single point of failure. Some workloads, such as WebSockets, game servers and long-lived streams, are naturally stateful, and forcing them into this shape costs more than it saves.
