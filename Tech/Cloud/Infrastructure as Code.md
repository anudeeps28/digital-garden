---
type: atomic
aliases: [iac]
tags: [iac, devops, coding/azure, coding/cicd]
date: 2026-09-16
---

# Infrastructure as Code

## Idea
Clicking buttons in a cloud portal produces an environment nobody can reproduce. Writing it down produces one that rebuilds identically, and a diff you can review.

## Definition
Infrastructure as Code (IaC) is the practice of describing every cloud resource in version-controlled files and letting a tool create them, rather than provisioning by hand. The properties that make it worth the effort are: **reproducibility** — the same files produce the same environment every time; **reviewability** — an infrastructure change arrives as a pull request a colleague can read; and **convergence** — re-running against an existing environment brings it back to the described state rather than duplicating it. What it actually prevents is *drift*: the slow divergence where dev works and production doesn't and nobody can say what differs, because the difference was made by someone clicking something eighteen months ago. The discipline only holds if the portal becomes read-only in practice — one manual change and the files are no longer the truth.

## Source
Term popularized by the DevOps movement in the early 2010s; Kief Morris's *Infrastructure as Code* (O'Reilly, 2016) is the canonical treatment. Tooling includes Terraform, [[Bicep]]/ARM, CloudFormation, and Pulumi.

---

## Compass

**Roots** — *where this comes from*
It applies the logic of source control and code review to a domain that historically had neither — the same instinct as [[Database Migrations]] for schemas.

**Paths** — *where this leads*
On Azure the language is [[Bicep]], organized into [[Bicep Module|modules]] and varied per environment by [[Bicep Parameter File|parameter files]] and [[Deployment Scope]].

**Neighbors** — *what lives nearby*
[[CI-CD Pipeline|CI/CD]] does for application deployment what IaC does for the environment underneath it; together they make [[Branch-based Deployments]] possible.

**Clash** — *what pushes against this*
It is genuinely slower for a one-off change, and the feedback loop is brutal: many errors only appear at deploy time against real cloud APIs, so a template that compiles cleanly can still be rejected — see [[Tier-Gated Features]].
