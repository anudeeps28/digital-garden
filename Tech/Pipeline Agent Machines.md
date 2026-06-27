---
type: atomic
tags: [coding/devops, coding/cicd]
date: 2026-04-24
---

# Pipeline Agent Machines

## Idea
A pipeline agent is the actual machine — Windows server, Linux VM, container — where pipeline tasks execute; agents register with Azure DevOps, poll for jobs, and run them locally.

## Definition
Azure DevOps doesn't run pipeline tasks in some abstract cloud — every step runs on a specific machine that has the Azure DevOps **agent service** installed. Two flavors:

- **Microsoft-hosted agents** — disposable VMs that Microsoft provisions per job. Fresh OS each time, common toolchains preinstalled, no state carries over. Easy but slow to start, and they live on the public internet so they can't reach private resources.
- **Self-hosted agents** — machines you (or your ops team) own. Persistent state, custom toolchains, and — critically — they can sit *inside* your [[Virtual Networks (VNets)|VNet]] so they can deploy to resources with [[publicNetworkAccess Disabled]]. KBA's `SVDDCAPP01`-style hostnames are self-hosted agents grouped into [[Deployment Groups]].

The agent runs as a service, polls Azure DevOps over HTTPS for queued jobs, downloads the job's task definitions, executes them locally, and streams logs back. If the agent is offline, the pipeline waits.

## Source
CI/CD learning session — KBA's on-prem agent topology.

---

## Roots — *where this comes from*
The concept of where code actually builds and deploys from is often surprisingly unanswered — understanding [[Pipeline Agent Machines]] is foundational to knowing your [[CI/CD]] topology. Network placement of the agent is the critical lever that decides what resources your pipeline can reach.

## Paths — *where this leads*
[[Deployment Groups]] provide the organizational structure for managing multiple agents, while agent capabilities — the tools, SDKs, and OS versions advertised to the pipeline — determine what tasks can execute. Agent pools sit separately from Deployment Groups and handle organization on the build side.

## Neighbors — *what lives nearby*
The concept of agent grouping appears in [[Deployment Groups]], and [[Pipeline Agent Machines]] are the Azure DevOps equivalent of GitHub Actions self-hosted runners and the older Jenkins build slaves — all represent the persistent machines that actually execute CI/CD tasks.

## Clash — *what pushes against this*
Cloud-only hosted agents eliminate the infrastructure maintenance burden and avoid the need for persistent machines altogether, while serverless build systems like Cloud Build abandon the persistent machine concept entirely — trading flexibility and private network access for simplicity and zero operational overhead.
