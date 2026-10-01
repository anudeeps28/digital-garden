---
type: atomic
tags: [coding/azure, coding/security, security, coding/identity]
date: 2026-10-01
---

# Role-Based Access Control (RBAC)

## Idea
Instead of granting each person a long list of individual permissions, you define a few job-shaped roles ("can read", "can deploy", "can manage everything") and hand out roles. Access becomes something you can read at a glance and take away in one step.

## Definition
Role-based access control is a way to do [[Authorization]] in which permissions are grouped into **roles**, and roles are assigned to identities: users, groups, or a [[Workload Identity]] that an app runs as. An assignment has three parts: who, which role, and at what **scope**. Scopes form a hierarchy (in Azure: management group, subscription, resource group, single resource, matching [[Deployment Scope]]), and an assignment is **inherited** by everything below it, so a role granted on a resource group applies to every resource in it. Good practice is **least privilege**: the smallest role at the narrowest scope that gets the job done, assigned to groups rather than individuals. Platforms ship **built-in roles** (Reader, Contributor, Owner) and let you write **custom roles** when none fits. The common gotcha is **control plane versus data plane**. Control-plane roles let you manage the resource itself (create it, change settings, delete it); data-plane roles let you read or write what is inside (the blobs, the secrets, the queue messages). Being Owner of a storage account does not by itself let you read its files through your identity. **ABAC** (attribute-based access control) goes further by also checking attributes, such as a tag on the resource or the user's department, at request time.

## Providers
- **Azure** — Azure RBAC; role definitions plus role assignments at a scope, with separate data-plane roles such as Storage Blob Data Reader and Key Vault Secrets User, and ABAC conditions on some assignments.
- **AWS** — AWS IAM is policy-based: JSON policies list allowed actions and resources and are attached to users, groups or roles. An IAM "role" means something different there: an identity that people, services or other accounts temporarily assume to get short-lived credentials, closer to a workload identity than to a permission bundle.
- **Google Cloud** — Cloud IAM; predefined and custom roles bound to principals on the organization, folder, project or resource hierarchy, with IAM Conditions for attribute checks.
- **Others** — Kubernetes RBAC: Roles and ClusterRoles bound to users or service accounts with RoleBindings, scoped to a namespace or the whole cluster.

## Source
Formalized by David Ferraiolo and Richard Kuhn at NIST (1992) and standardized as ANSI/INCITS 359-2004.

---

## Compass

**Roots** — *where this comes from*
It is the most common concrete form of [[Authorization]], applied once [[Authentication]] has established who is asking.

**Paths** — *where this leads*
Granting roles to a [[Workload Identity]] replaces stored credentials; inside a database the same idea shows up as [[Least-Privilege Database Roles]].

**Neighbors** — *what lives nearby*
[[Deployment Scope]] uses the same hierarchy to decide where resources are created; [[Separation of Duties]] is often enforced by making sure no single role covers two conflicting jobs.

**Clash** — *what pushes against this*
Roles multiply: every exception becomes a new custom role or a broad assignment "just to make it work", and inheritance means a grant made high up quietly reaches resources nobody was thinking about. Fine-grained, context-dependent rules are awkward to express as roles, which is why ABAC exists.
