---
type: atomic
tags: [coding/database, coding/azure, devops]
date: 2026-10-01
---

# Managed SQL Database

## Idea
A managed SQL database is a [[Relational Database|relational database]] where the cloud provider does the server chores (patching, backups, failover) so you only look after your data and how you use it.

## Definition
A managed SQL database is a database engine (SQL Server, [[PostgreSQL]], MySQL) that the provider installs, runs and maintains for you. You get a connection endpoint, not a machine. The provider handles **patching** and version upgrades, takes automatic **backups** with **point-in-time restore** (rewind the database to any second within a retention window), keeps replicas for **high availability** so a hardware failure becomes a brief failover rather than an outage, and lets you change **service tiers** to scale compute and storage up or down. What stays yours: the schema, the [[SQL]] queries, the indexes, who can connect and with what rights, and whether a restore actually works when you need it. The gotchas are practical. Tiers decide more than size: features like longer backup retention, zone redundancy or [[Geo-Redundant Backup|geo-redundant backups]] are often only available on higher tiers ([[Tier-Gated Features]]). Each tier caps concurrent connections and workers, so a connection leak shows up as a hard limit. And because the provider moves your database during patching and failover, apps see short **transient failures** (dropped connections that succeed on retry), which is why [[Connection Resiliency]] isn't optional.

## Providers
- **Azure** — Azure SQL Database (single database or elastic pool), Azure SQL Managed Instance for near-full SQL Server compatibility, and Azure Database for PostgreSQL / MySQL.
- **AWS** — Amazon RDS (PostgreSQL, MySQL, SQL Server, Oracle and others) and Amazon Aurora, AWS's cloud-native MySQL/PostgreSQL-compatible engine.
- **Google Cloud** — Cloud SQL (PostgreSQL, MySQL, SQL Server) and AlloyDB for PostgreSQL.
- **Others** — Neon and Supabase (hosted PostgreSQL with developer-focused extras).

## Source
Amazon RDS (2009) and SQL Azure (2010, now Azure SQL Database) established the model of the database as a managed service rather than a server you run.

---

## Compass

**Roots** — *where this comes from*
It's a [[Relational Database]] with the operations work moved to the provider; the engine underneath is still [[SQL]] Server, [[PostgreSQL]] or MySQL.

**Paths** — *where this leads*
Serverless tiers add [[Database Auto-Pause]], and the provider's backups only count once you've proven them with a [[Restore Drill]].

**Neighbors** — *what lives nearby*
[[Connection Resiliency]] handles the transient failures it produces; [[Tier-Gated Features]] decides which safety features you actually have; [[Least-Privilege Database Roles]] covers the access part you still own.

**Clash** — *what pushes against this*
You give up control: no OS access, limited engine settings, maintenance on the provider's schedule, and a price that climbs quickly with tier. At steady high load, a self-run database on reserved hardware can be much cheaper.
