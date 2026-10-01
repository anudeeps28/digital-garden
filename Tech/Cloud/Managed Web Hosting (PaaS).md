---
type: atomic
tags: [coding/azure, coding/security, devops, web]
date: 2026-10-01
---

# Managed Web Hosting (PaaS)

## Idea
You hand the platform your code or a container and it keeps the server running for you: the operating system, the patches, the certificates and the scaling. You give up control of the machine so you can stop looking after it.

## Definition
Managed web hosting is a platform-as-a-service where the provider runs your web app on infrastructure it operates. You deploy a code package or a container image; the platform provides the OS, the web server or runtime, security patching, TLS certificates, a default hostname, scale-out rules and a [[Health Probe]] that replaces unhealthy instances. **Deployment slots** give you a second live copy of the app (staging) on its own hostname; you deploy there, warm it up and then swap it into production with no downtime, and swap back if it goes wrong. Most platforms also run a **companion management site** next to your app. On Azure this is the Kudu or SCM site at `<app>.scm.azurewebsites.net`, which accepts deployments and exposes logs, environment variables and a debug console. The gotcha is that this site has its **own access restrictions**, separate from the main site's. Locking the app down to a private network or a single edge gateway does not lock down the deploy endpoint unless you also restrict the SCM site (or tell it to reuse the main site's rules). Otherwise the most powerful URL on the app is the one left open.

## Providers
- **Azure** — Azure App Service (Web Apps), with deployment slots and the Kudu/SCM site; can host on Windows ([[IIS]]) or Linux, and run code or containers.
- **AWS** — Elastic Beanstalk (manages EC2 instances for you, with environment swaps) and App Runner (container or source to a running HTTPS service).
- **Google Cloud** — App Engine (the original PaaS, with traffic splitting between versions) and Cloud Run (containers, with revisions).
- **Others** — Heroku, Render, Fly.io and Railway offer the same "push code, get a URL" model.

## Source
Google App Engine (2008) and Heroku (2007) popularised the model; Azure Websites launched in 2012 and became App Service in 2015.

---

## Compass

**Roots** — *where this comes from*
It packages what used to be a hand-run [[IIS]] or Linux server into a service, and increasingly takes a [[Docker]] image as the unit you deploy.

**Paths** — *where this leads*
Apps that need to scale out freely must be [[Stateless Services|stateless]]. Production setups usually put a [[Layer 7 Load Balancer]] or [[Edge Gateway]] in front and use [[Origin Verification]] so the default hostname can't be used to bypass it.

**Neighbors** — *what lives nearby*
[[Serverless Functions]] are the pay-per-execution sibling; [[Private Endpoint|private endpoints]] are how the app reaches its database without the public internet.

**Clash** — *what pushes against this*
You live inside the platform's choices: supported runtimes, file system limits, restart schedules and pricing tiers ([[Tier-Gated Features]]). Each hidden companion endpoint, such as the deploy site, is one more surface you have to know exists before you can secure it.
