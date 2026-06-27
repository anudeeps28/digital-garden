---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# CI-CD Pipeline

## Idea
A CI/CD pipeline automatically builds, tests, and deploys your code when you push — removing manual steps and catching bugs early.

## Definition
CI/CD stands for **Continuous Integration** (automatically building and testing code on every commit) and **Continuous Deployment** (automatically deploying passing builds to production). Pipelines are configured in version control (typically YAML) and run whenever code is pushed or a [[Pull Request]] is merged. A typical pipeline includes stages such as: (1) restoring dependencies, (2) building the application, (3) running [[Unit Tests]] and [[Integration Tests]], (4) building a [[Docker Image]], (5) pushing artifacts to a registry, (6) deploying to a target environment, and (7) running [[Database Migrations]]. If any step fails, the pipeline stops and the team is notified.

## Source
Industry standard practice; foundational concepts from the DevOps movement. "Continuous Integration" was popularized by Martin Fowler (2000s). Continuous Deployment evolved as an extension of CI practices.

---

## Compass

**Neighbors** — *what lives nearby*
[[GitHub Actions]] provides GitHub's equivalent CI/CD system, while [[Jenkins]] is an older self-hosted option, and [[GitLab CI]] offers GitLab's built-in alternative.

**Clash** — *what pushes against this*
[[Manual Deployment]] — building and deploying by hand — is error-prone and slow, and [[No Testing]] removes the safety net of automated verification before deployments.

**Roots** — *where this comes from*
CI/CD is a foundational [[DevOps]] practice born from the need to automate and accelerate software delivery, enabling faster feedback and reducing human error in deployment workflows.

**Paths** — *where this leads*
Successful pipelines enable rapid, reliable deployments and serve as the backbone of modern [[DevOps]] practices, supporting practices like [[Blue-Green Deployment]] and [[Canary Release]]s.
