---
type: atomic
tags: [coding/architecture, coding/database, coding/distributed-systems, saas]
date: 2026-10-01
---

# Tenancy Models

## Idea
When one product serves many customers, you have to decide how much each customer shares with the others: everything, nothing, or something in between. That choice sets your cost, your risk, and how much one customer's bad day can spill onto everyone else.

## Definition
Tenancy models are the spectrum of ways to separate customers (**tenants**) in a shared system. At one end is **pool**: every tenant shares the same compute and the same database, and each row carries a tenant ID that every query must filter on. At the other end is **silo**: each tenant gets its own compute and its own database, so nothing is shared. **Bridge** is the middle: some layers shared, others separated — typically shared compute with a separate schema or a separate database per tenant. A very common real-world pick is pooled compute with database-per-tenant, which makes the database the thing that actually keeps tenants apart. The trade-offs move together. Pool is cheapest and simplest to run, but one heavy tenant slows everyone (**noisy neighbour**) and one missed filter can leak everything (large **blast radius**). Silo contains damage and lets you back up, restore, or move one tenant on its own, but costs more and turns every schema change into a migration run across N databases, where some will fail halfway. Most platforms mix models by tier — pool for small customers, silo for the ones paying for it.

## Providers
- **Azure** — Azure SQL elastic pools share capacity across many per-tenant databases; the Azure Architecture Center's multitenant guidance and SaaS database tenancy patterns describe the options.
- **AWS** — the silo / bridge / pool terms come from AWS SaaS Factory and the Well-Architected SaaS Lens.
- **Google Cloud** — GKE multi-tenancy guidance (namespace-per-tenant vs cluster-per-tenant) and Cloud SQL or Spanner for shared or per-tenant databases.
- **Others** — PostgreSQL schema-per-tenant; Citus distributes tenants across nodes by tenant ID or by schema; Kubernetes namespaces as the compute-side equivalent.

## Source
AWS SaaS Factory and the AWS Well-Architected SaaS Lens (origin of the silo / bridge / pool vocabulary); Microsoft's multitenant SaaS database tenancy patterns documentation.

---

## Compass

**Roots** — *where this comes from*
The model you pick decides which layers of [[Multi-Tenant Data Isolation]] carry the load — in pool it's [[Row-Level Security]] and [[Global Query Filters]]; in silo it's the database boundary itself.

**Paths** — *where this leads*
Anything except pure pool needs [[Tenant Resolution]] to pick the right [[Connection String]], and per-tenant databases make [[Database Migrations]] and [[Restore Drill|restore drills]] an N-times problem.

**Neighbors** — *what lives nearby*
[[Customer-Managed Keys (CMK)]] are often the silo-tier upgrade; [[Security Control vs Security Boundary]] is the habit of asking which layer really separates tenants.

**Clash** — *what pushes against this*
Silo sounds safest but multiplies operational work — thousands of databases to patch, migrate, and monitor. Many teams find a well-defended pool is cheaper *and* less error-prone than a fleet they can't keep consistent.
