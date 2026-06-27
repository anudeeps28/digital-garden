---
type: atomic
tags: [coding/devops, coding/cicd]
date: 2026-04-24
---

# Release Stages

## Idea
Release stages are the ordered environments a build flows through on its way to production — typically Dev → Test → Prod — each with its own deploy steps, gates, and approvals.

## Definition
A release pipeline is structured as a chain of stages, each representing an environment. A new [[Build Artifacts|artifact]] enters the first stage, deploys to that environment, runs whatever validation lives there, and — if everything passes the [[Pre-deploy Approvals|gates]] for the next stage — promotes forward. KBA's typical chain: **Dev** (auto-deploy on every successful build to a sandbox), **Test** (auto-deploy when the build comes from `master`, run integration tests), **Prod** (manual approval, possibly a deployment window). Each stage can be configured with its own variables, connections, and approval rules. The promotion model is what makes [[Build Artifacts|the artifact]] meaningful — the same bytes go through the same steps in each stage, so production gets the version that survived dev and test.

## Source
CI/CD learning session — Azure DevOps release pipeline structure.

---

## Roots — *where this comes from*
Release stages answer fundamental questions about environment management. The concept connects to [[Build Pipeline vs Release Pipeline]], which distinguishes where stages live (in the release pipeline), and environment parity is a persistent question about how closely test environments should mirror production.

## Paths — *where this leads*
Release stages enable downstream infrastructure concerns like [[Pre-deploy Approvals]], which define gates between stages, and [[Artifact Filters]], which control what artifacts a stage will accept. They also necessitate environment-specific configuration — connection strings, feature flags, and deployment parameters tailored to each stage.

## Neighbors — *what lives nearby*
[[Deployment Slots]] achieve a similar goal of staging-to-prod swaps, though they operate inside a single App Service rather than across logical environments. Blue-green deployment is another form of environment-promotion at runtime, and trunk-based dev is a related branching philosophy that shapes how code flows into these stages.

## Clash — *what pushes against this*
The opposite approach is to deploy straight to prod without any staging environment to catch regressions, which trades safety for speed. On the extreme end, single environment setups where dev equals prod are fine only for hobby projects and trivialize the entire concept of stages.
