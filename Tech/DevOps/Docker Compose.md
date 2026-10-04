---
type: atomic
tags: [devops, coding/architecture]
date: 2026-10-04
---

# Docker Compose

## Idea
Docker Compose describes a whole multi-container app in one YAML file, so the entire stack starts, stops and rebuilds with one command.

## Definition
A `compose.yaml` file lists **services** (each an image or a build), their ports, environment, volumes and networks. `docker compose up -d` creates or updates everything to match the file, and `docker compose down` tears it down. On a single server the useful settings are few: `restart: always` (or `unless-stopped`) so containers come back after a crash or reboot, `env_file` to load secrets from a file kept out of git, and an **external network** shared with a [[Reverse Proxy]] so the proxy can reach each app by name without publishing ports. The biggest payoff is disaster recovery. If the host is **stateless** (all durable data lives in a managed database or object storage), rebuilding a dead server is: provision a machine, clone the repo, copy the env file, run `docker compose up`. The compose file becomes runnable documentation of how the system is wired. It is not an orchestrator: there is no multi-host scheduling or self-healing beyond restarts.

```yaml
services:
  app:
    build: .
    restart: always
    env_file: .env
    networks: [proxy]
networks:
  proxy:
    external: true
```

## Source
Began as Fig, written in 2014 by Aanand Prasad and Ben Firshman at Orchard Laboratories; Docker acquired Orchard in July 2014 and renamed Fig to Docker Compose. Compose v2 (2021-2022) moved it into the `docker compose` CLI plugin.

---

## Compass

**Roots** — *where this comes from*
It orchestrates [[Docker]] containers on one machine and is a light form of [[Infrastructure as Code]] for that host.

**Paths** — *where this leads*
Clone-and-up recovery only works with [[Stateless Services]], and it sets your real [[RTO and RPO]] once you time it in a [[Restore Drill]].

**Neighbors** — *what lives nearby*
[[Multi-Stage Docker Build]] produces the images it runs, and [[Pull-Based Deployment]] can simply `git pull` and re-run `up` on a schedule.

**Clash** — *what pushes against this*
It stops at one host, so high availability means Kubernetes or [[Serverless Containers]]. Secrets in an `.env` file on disk are also weaker than proper [[Secrets and Key Management]].
