---
type: atomic
tags: [coding/devops, deployment]
date: 2026-10-31
---

# It Works on My Machine

## Idea
An app never runs alone. It runs on top of an environment, and when the environment changes the app breaks. Most deployment tooling is a different answer to one question: how do we make the app run the same everywhere?

## Definition
"It works on my machine" is the failure where code runs on the developer's laptop and breaks everywhere else. The code is the same; what changed is everything around it. That includes the operating system, the runtime version (.NET 8 vs .NET 6, Python 3.12 vs 3.10), the installed libraries, environment variables and config files, file paths, and the other services it expects to find, such as a database or an API key. A developer's laptop builds up the right mix over months, often by accident, and nobody writes it down. A new machine has none of it, so one version mismatch is enough to break the app. Every way of shipping software attacks this gap from a different side. You can script the server's setup ([[Infrastructure as Code]]), let a platform own the environment ([[Managed Web Hosting (PaaS)]], [[Serverless Functions]]), bundle the runtime into the app ([[Self-Contained Build]]), clone the whole machine ([[Virtual Machines|VM images]]), or ship the app together with its environment as a [[Docker]] container.

## Source
The phrase is old programmer folklore and nobody knows who said it first. Joseph Cooney's joke "Works on My Machine" certification, written up by Jeff Atwood on Coding Horror (2007), made it famous ([codinghorror.com](https://blog.codinghorror.com/the-works-on-my-machine-certification-program)). Docker's 2013 launch pitch was built around getting rid of it.

---

## Compass

**Roots** — *where this comes from*
It is what happens when no file describes the environment, so every machine becomes a [[Snowflake Servers|snowflake]] whose setup lives only in someone's memory.

**Paths** — *where this leads*
The fix is to build one artifact and promote those exact bytes from dev to staging to production, which is what [[Runtime Config (Build Once Deploy Everywhere)|build once, deploy everywhere]] and a [[CI-CD Pipeline]] enforce.

**Neighbors** — *what lives nearby*
[[Docker Compose]] applies the same cure to local development: every teammate gets the same database and cache versions from one file instead of hand-installing them.

**Clash** — *what pushes against this*
Even a perfectly packaged app can still behave differently because of what it can't carry with it: real data volumes, network latency, secrets and production traffic. A [[Containers Share the Host Kernel|container still shares the host's kernel]], too, so identical images aren't fully identical environments.
