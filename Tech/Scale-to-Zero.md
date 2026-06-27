---
type: atomic
tags: [coding/azure, devops]
date: 2026-06-26
---

# Scale-to-Zero

## Idea
Scale-to-zero means a service is allowed to shrink all the way down to no running replicas when nobody's using it — so an idle workload costs you nothing.

## Definition
Scale-to-zero is an autoscaling behavior where a service drops to zero replicas during idle periods and spins back up on the next request, trading a cold-start delay for the cost savings of paying only when work actually arrives. On the KBA AI Document Ingestion project, the embedding [[Azure Container Apps|Container App]] is configured this way: between document batches it scales to zero, then wakes up when the [[Azure Service Bus]] queue (via [[Azure Functions]]) drives new work its way. The tradeoff is a cold start — the first request after idle waits for a replica to start — which is acceptable here because embedding happens asynchronously, not on a user-facing hot path. It's the same cost philosophy as [[SQL Serverless Auto-Pause]], applied to compute instead of the database.

## Source
KBA AI Document Ingestion project

---

## Neighbors — *what lives nearby*
[[SQL Serverless Auto-Pause]] applies the same pay-for-what-you-use philosophy to the database tier, while [[Azure Container Apps]] is the platform that provides scale-to-zero as a built-in feature for containerized services.

## Clash — *what pushes against this*
The real opposite is an always-on provisioned [[Connection String|service]] that bills continuously around the clock regardless of usage.

## Roots — *where this comes from*
Scale-to-zero is a built-in scaling feature of the [[Azure Container Apps]] hosting model, which enables this cost-optimization pattern natively.

## Paths — *where this leads*
Queued messages in [[Azure Service Bus]] are what trigger a scaled-to-zero worker to spin back up and process work.
