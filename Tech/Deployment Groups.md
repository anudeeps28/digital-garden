---
type: atomic
tags: [coding/devops, coding/cicd]
date: 2026-04-24
---

# Deployment Groups

## Idea
A Deployment Group is a logical pool of physical or virtual machines — typically on-prem or inside a [[Virtual Networks (VNets)|VNet]] — that an Azure DevOps release pipeline can target as deployment destinations.

## Definition
When the deployment target is a managed PaaS service like [[Azure App Service]], the pipeline talks to Azure APIs and you're done. But when the target is a real Windows machine running [[IIS]], a self-hosted [[SQL Server]], or any on-prem box, you need an **agent** running on that machine that can pull deployment instructions and execute them locally. A Deployment Group is the collection of those agents grouped under a name, with tags like `role:web`, `env:prod`. The release pipeline says "deploy to all machines in deployment group `KBA-Test` tagged `web`" and Azure DevOps fans the deployment out. KBA's `SVDDCAPP01` and similar machine names are members of a Deployment Group — they run an Azure DevOps agent service that polls for jobs and runs them on the local box. This is also how you deploy *into* a network that has [[publicNetworkAccess Disabled]] on its targets — the agent is already inside the network, so it can reach the resources the cloud pipeline can't.

## Source
CI/CD learning session — KBA on-prem deployment targets.

---

## Neighbors — *what lives nearby*
[[Pipeline Agent Machines]] are the individual machines inside a Deployment Group, running the agent service that receives deployment instructions. The broader concept of self-hosted agents extends beyond just release deployments to build agents as well, and this pattern is similar to what [[Ansible]] does with its inventory — maintaining a named collection of target machines grouped with metadata.

## Clash — *what pushes against this*
Microsoft-hosted agents provide the opposite approach — disposable cloud VMs that don't persist between runs and are managed entirely by Azure DevOps. A PaaS-only deployment strategy eliminates the need for machine lists altogether, since you're deploying directly to managed cloud services.

## Roots — *where this comes from*
Deployment Groups exist because hybrid deployment scenarios still matter — when on-prem infrastructure remains critical to an organization. The underlying challenge is [[Network reachability]] — getting deploys into locked-down networks where the cloud pipeline can't reach directly, but an agent already inside can.

## Paths — *where this leads*
Understanding individual [[Pipeline Agent Machines]] and how they function within a group is essential for managing deployments. Agent versioning becomes critical as you scale across multiple machines, ensuring consistency in how deployments execute. Health checks detect offline agents before a release tries to use them, preventing failed deployments to unavailable targets.
