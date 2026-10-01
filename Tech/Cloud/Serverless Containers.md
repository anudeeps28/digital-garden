---
type: atomic
tags: [coding/azure, devops, coding/distributed-systems, coding/architecture]
date: 2026-10-01
---

# Serverless Containers

## Idea
You hand the platform a container image and it runs it for you: no virtual machines to patch, no Kubernetes cluster to babysit. It adds copies when traffic arrives and removes them, all the way to none, when traffic stops.

## Definition
A serverless container platform runs a [[Docker Image|container image]] you supply and takes care of the servers, networking and scaling underneath it. You describe the app (image, CPU and memory, environment variables, which port it listens on) and the platform decides how many **instances** to run. Scaling is driven by rules: concurrent HTTP requests, or events such as queue length, measured by an **event-driven autoscaler** in the style of KEDA. When nothing is happening it can [[Scale-to-Zero|scale to zero]], so you pay nothing while idle, at the price of a cold start on the next request. Each deployment creates an immutable **revision**, and **traffic splitting** lets you send, say, 10% of requests to the new revision before switching everyone over, or roll back instantly. Compared with [[Serverless Functions]], you bring a whole container rather than one handler: any language, any framework, your own web server, and much longer runs. Compared with running Kubernetes yourself, you give up control over nodes, networking add-ons and cluster-level tuning in exchange for far less operations work. The app should still be [[Stateless Services|stateless]], because instances come and go.

## Providers
- **Azure** — Azure Container Apps; built on Kubernetes and KEDA underneath, with revisions, traffic splitting and scale-to-zero.
- **AWS** — AWS Fargate runs containers for ECS (or EKS) without managing servers but does not scale to zero on its own; AWS App Runner is the simpler "give it an image, get a URL" option.
- **Google Cloud** — Cloud Run; request-driven, scales to zero, with revisions and traffic splitting.
- **Others** — Knative, the open-source layer that adds this model on top of any Kubernetes cluster (Cloud Run implements the Knative API).

## Source
Google Cloud Run (2019) and Knative (Google and partners, 2018) defined the request-driven model; AWS Fargate arrived in 2017 and Azure Container Apps in 2022.

---

## Compass

**Roots** — *where this comes from*
It packages software as [[Docker]] containers and borrows [[Scale-to-Zero]] from the serverless world.

**Paths** — *where this leads*
Instances usually reach databases and secrets through a [[Workload Identity]], and the environment can be placed inside a [[Virtual Network]] so internal services stay private.

**Neighbors** — *what lives nearby*
[[Serverless Functions]] is the smaller-grained sibling, and [[Managed Web Hosting (PaaS)]] is the always-on option for a single web app. A [[Health Probe]] tells the platform when a new instance is ready to take traffic.

**Clash** — *what pushes against this*
Cold starts hurt latency-sensitive apps unless you keep a minimum instance warm, which removes the zero-cost benefit. You also live inside the platform's limits (no host access, restricted networking options, fixed scaling knobs), and once you need more than that you end up on full Kubernetes anyway.
