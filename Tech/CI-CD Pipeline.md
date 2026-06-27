---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# CI-CD Pipeline

## Idea
A CI/CD pipeline automatically builds, tests, and deploys your code when you push — removing manual steps and catching bugs early.

## Definition
CI/CD stands for **Continuous Integration** (automatically building and testing code on every commit) and **Continuous Deployment** (automatically deploying passing builds to production). In [[Azure DevOps]], a pipeline is defined in YAML and runs whenever code is pushed or a [[Pull Request]] is merged. A typical the project pipeline: (1) restore [[NuGet]] packages, (2) build the [[.NET 8]] solution, (3) run [[Unit Tests]] and [[Integration Tests]] with [[xUnit]], (4) build a [[Docker Image]], (5) push to [[Azure Container Registry]], (6) deploy to [[Azure Container Apps]], (7) run [[Database Migrations]]. If any step fails, the pipeline stops and the team is notified.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
[[GitHub Actions]] provides GitHub's equivalent CI/CD system, while [[Jenkins]] is an older self-hosted option, and [[GitLab CI]] offers GitLab's built-in alternative.

**Clash** — *what pushes against this*
[[Manual Deployment]] — building and deploying by hand — is error-prone and slow, and [[No Testing]] removes the safety net of automated verification before deployments.

**Roots** — *where this comes from*
Pipelines are hosted in [[Azure DevOps]] as the platform, and CI/CD is a core [[DevOps]] practice that enables continuous integration and deployment.

**Paths** — *where this leads*
The pipeline builds [[Docker Image]]s and pushes them to [[Azure Container Registry]], ultimately enabling deployment to [[Azure Container Apps]].
