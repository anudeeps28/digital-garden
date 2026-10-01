---
aliases: [tech/deployment-scope]
type: atomic
tags: [coding/azure, iac, devops]
date: 2026-06-26
---

# Deployment Scope

## Idea
Deployment scope is the "where does this apply" of a Bicep deployment — the whole subscription, or just one resource group.

## Definition
Scope determines the level at which an Azure deployment operates: a subscription-scoped deployment can create resource groups and networking foundations, while a resource-group-scoped deployment stamps application resources inside an existing group. In practice, bootstrap-style infrastructure — resource groups and [[Virtual Network|Virtual Networks (VNets)]] — is often created at subscription scope, then app resources like [[Serverless Functions|Azure Functions]], [[Serverless Containers|Azure Container Apps]], and [[Managed SQL Database|Azure SQL]] are deployed at resource-group scope. Picking the right scope in [[Bicep]] (via the `targetScope` declaration) is what lets different infrastructure layers stay cleanly separated. [[Bicep Module]]s can also declare their own scope, so a single deployment can touch more than one level.

## Providers
- **Azure** — tenant, management group, subscription and resource-group scopes.
- **AWS** — organization, account and region (StackSets for multi-account).
- **Google Cloud** — organization, folder and project.

## Source
Microsoft, Azure Resource Manager (introduced 2014); Bicep (Microsoft, 2021) as the domain-specific language for ARM templates.

---

## Compass

**Neighbors** — *what lives nearby*
Both [[Role-Based Access Control (RBAC)|RBAC in Azure]] and deployment scope define a boundary; RBAC scopes permissions, while deployment scope scopes resource creation.

**Clash** — *what pushes against this*
[[Bicep Parameter File]]s vary *values* across environments, whereas scope varies the *target level* of a deployment.

**Roots** — *where this comes from*
Scope is set by the `targetScope` keyword in a [[Bicep]] template.

**Paths** — *where this leads*
[[Bicep Module]]s let a single deployment span multiple scopes, and understanding scope is a core [[IaC]] concept for organizing what gets provisioned where.
