---
type: atomic
tags: [coding/azure, devops]
date: 2026-06-26
---

# Scale-to-Zero

## Idea
Scale-to-zero means a service is allowed to shrink all the way down to no running replicas when nobody's using it — so an idle workload costs you nothing.

## Definition
Scale-to-zero is an autoscaling behavior where a service drops to zero replicas during idle periods and spins back up on the next request, trading a cold-start delay for the cost savings of paying only when work actually arrives. In practice, a containerized service might scale to zero between work batches, then wake up when new requests arrive. The tradeoff is a cold start — the first request after idle waits for a replica to start — which is acceptable for asynchronous or non-user-facing workloads. It's the same cost philosophy as [[SQL Serverless Auto-Pause]], applied to compute instead of the database.

## Source
Amazon Web Services (AWS), popularized through Lambda (2014). Scale-to-zero became a foundational pattern in serverless computing. Azure Container Apps brought this capability to container-based workloads as a built-in scaling feature.

---

## Neighbors — *what lives nearby*
[[SQL Serverless Auto-Pause]] applies the same pay-for-what-you-use philosophy to the database tier, while [[Azure Container Apps]] is the platform that provides scale-to-zero as a built-in feature for containerized services.

## Clash — *what pushes against this*
The real opposite is an always-on provisioned [[Connection String|service]] that bills continuously around the clock regardless of usage.

## Roots — *where this comes from*
Scale-to-zero emerged from the serverless computing movement as a way to fully align infrastructure costs with actual usage. It's now a standard feature across cloud platforms — [[Azure Container Apps]], AWS Fargate, Google Cloud Run — that enables the container-first equivalent of pay-per-invocation billing.

## Paths — *where this leads*
Queued messages in [[Azure Service Bus]] are what trigger a scaled-to-zero worker to spin back up and process work.
