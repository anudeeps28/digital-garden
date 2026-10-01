---
type: atomic
tags: [coding/azure, devops, coding/distributed-systems, coding/architecture]
date: 2026-10-01
---

# Serverless Functions

## Idea
You write one small piece of code, say what should start it (an HTTP call, a message on a queue, a timer), and the platform runs it only when that happens. You stop paying for a server that mostly sits idle, but in return you can't keep anything in memory between runs.

## Definition
A serverless function is code that a platform runs on demand when a **trigger** fires. The trigger can be an HTTP request, a message arriving on a queue, a file landing in storage, or a timer schedule. The platform starts an instance, passes in the event, runs your handler and may then throw the instance away. Functions are deployed in a container that Azure calls the **function app**: one deployable unit holding several functions that share configuration, runtime version, identity and scaling. Deploying, scaling or restarting the app affects every function inside it. On a **consumption plan** you pay per execution, and the platform scales out to many instances and back down to none, which means the first request after an idle period pays a **cold start** while the runtime loads. **Premium or dedicated plans** keep warm instances ready and remove most of that delay, but you pay for those instances even when nothing runs. Functions must be [[Stateless Services|stateless]]: any instance can handle any event, and an instance can vanish between two calls. So counters, sessions and caches belong in a database, cache or queue, not in local variables or local disk.

## Providers
- **Azure** — Azure Functions; the function app is the unit of deployment and scaling, with Consumption, Flex Consumption, Premium and Dedicated (App Service) plans.
- **AWS** — AWS Lambda; each function scales on its own, and provisioned concurrency keeps instances warm.
- **Google Cloud** — Cloud Run functions (formerly Cloud Functions), which now run on the Cloud Run platform.
- **Others** — Cloudflare Workers run in lightweight isolates at the edge, which nearly eliminates cold starts; Knative and OpenFaaS bring the same model to Kubernetes.

## Source
AWS Lambda (2014) made the model mainstream; Azure Functions and Google Cloud Functions followed in 2016.

---

## Compass

**Roots** — *where this comes from*
It is [[Scale-to-Zero]] taken all the way down to a single handler. It only works because the code is a [[Stateless Services|stateless service]].

**Paths** — *where this leads*
HTTP-triggered functions often sit behind a [[Layer 7 Load Balancer]] or an [[Edge Gateway]], and they reach other cloud resources with a [[Workload Identity]] rather than stored secrets.

**Neighbors** — *what lives nearby*
[[Managed Web Hosting (PaaS)]] is the always-on sibling: same "the platform runs it" deal, but billed for a running app rather than per execution. [[Docker]] containers are the other common packaging.

**Clash** — *what pushes against this*
Cold starts, execution time limits and per-call billing make functions a poor fit for steady high traffic or long-running work. Spreading logic across many small triggers also makes the whole flow harder to trace and debug than one service would be.
