---
aliases: ["tech/cloud/managed-identity"]
type: atomic
tags: [coding/azure, coding/security, devops, iac]
date: 2026-09-16
---

# Workload Identity

## Idea
The most reliable way to stop leaking a secret is to not have one. A workload identity lets a service prove who it is without ever holding a credential.

## Definition
A workload identity is an identity the cloud platform creates and maintains for a running service, which the service uses to authenticate to other services without any password, key, or [[Connection String|connection string]] in configuration. The platform issues short-lived tokens to the workload at runtime and rotates the underlying credential itself, so there is nothing to store, nothing to check into a repository, and nothing to rotate on a calendar. Access is then granted the other direction — the target resource grants a role to that identity — which makes permissions auditable and revocable in one place. On Azure, where it's called a *managed identity*, two flavours exist: **system-assigned**, tied to a single resource and deleted with it, and **user-assigned**, a standalone identity shared by several resources, which is what you want when multiple components need the same grants.

## Providers
- **Azure** — managed identities (system- or user-assigned), plus workload identity federation for workloads running outside Azure.
- **AWS** — IAM roles attached to the compute (instance profiles, Lambda execution roles, IAM Roles for Service Accounts on EKS).
- **Google Cloud** — service accounts attached to the resource, and Workload Identity Federation.
- **Others** — Kubernetes service account tokens; SPIFFE/SPIRE as the open standard.

## Source
Azure Managed Identities for Azure resources (Microsoft, 2017); AWS IAM roles and Google Cloud service accounts fill the same role.

---

## Compass

**Roots** — *where this comes from*
It's the practical form of the principle behind [[Least-Privilege Database Roles]] — identity-based access rather than shared secrets.

**Paths** — *where this leads*
It's the prerequisite for secretless data access, for [[Customer-Managed Keys (CMK)]] where the service is granted key *use*, and for [[Bicep]] templates that contain no secrets at all.

**Neighbors** — *what lives nearby*
[[OAuth 2.0 and OIDC]] is the same token-based model for human users; a workload identity is the machine equivalent, and the strongest form of [[Machine-to-Machine Authentication]].

**Clash** — *what pushes against this*
It only works inside the cloud platform. Local development, on-premises components, and third-party systems still need a fallback credential path — which is where the secrets quietly come back.
