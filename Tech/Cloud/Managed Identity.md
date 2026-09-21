---
type: atomic
tags: [coding/azure, coding/security, devops, iac]
date: 2026-09-16
---

# Managed Identity

## Idea
The most reliable way to stop leaking a secret is to not have one. A managed identity lets a service prove who it is without ever holding a credential.

## Definition
A managed identity is an identity the cloud platform creates and maintains for a running service, which the service uses to authenticate to other services without any password, key, or [[Connection String|connection string]] in configuration. The platform issues short-lived tokens to the workload at runtime and rotates the underlying credential itself, so there is nothing to store, nothing to check into a repository, and nothing to rotate on a calendar. Access is then granted the other direction — the target resource grants a role to that identity — which makes permissions auditable and revocable in one place. Two flavours exist: **system-assigned**, tied to a single resource and deleted with it, and **user-assigned**, a standalone identity shared by several resources, which is what you want when multiple components need the same grants.

## Source
Azure Managed Identities for Azure resources (Microsoft, 2017); AWS IAM roles for service accounts and Google Cloud service account impersonation fill the same role.

---

## Compass

**Roots** — *where this comes from*
It's the practical form of the principle behind [[Least-Privilege Database Roles]] — identity-based access rather than shared secrets.

**Paths** — *where this leads*
It's the prerequisite for secretless data access, for [[Customer-Managed Keys (CMK)]] where the service is granted key *use*, and for [[Bicep]] templates that contain no secrets at all.

**Neighbors** — *what lives nearby*
[[OAuth 2.0 and OIDC]] is the same token-based model for human users; a managed identity is the machine equivalent.

**Clash** — *what pushes against this*
It only works inside the cloud platform. Local development, on-premises components, and third-party systems still need a fallback credential path — which is where the secrets quietly come back.
