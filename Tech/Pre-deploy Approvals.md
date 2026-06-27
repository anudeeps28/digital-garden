---
type: atomic
tags: [coding/devops, coding/cicd]
date: 2026-04-24
---

# Pre-deploy Approvals

## Idea
A pre-deploy approval is a manual or automated checkpoint that must pass before a release stage starts deploying — the human (or system) gate between "ready to ship" and "shipping."

## Definition
Pre-deploy approvals attach to a [[Release Stages|release stage]] and specify *who must approve* before the stage begins. Common patterns: a named individual or group must click "Approve" in the Azure DevOps UI; an automated check (HTTP probe, work-item state, ServiceNow ticket status) must return success; a time window (don't deploy on weekends) must be open. Until the approval clears, the stage sits in a "pending approval" state — the [[Build Artifacts|artifact]] is ready, the deploy hasn't started. Approvals exist for two reasons: **safety** (a human verifies the right thing is being deployed at the right time) and **compliance** ([[SOC 1 Audit|SOC 1]] and similar regimes require evidence that production deploys went through an approved gate, not just an automated push). The approval record itself becomes audit evidence — who approved, when, and any attached comments.

## Source
CI/CD learning session — Azure DevOps stage configuration.

---

## Neighbors — *what lives nearby*
The [[Pull Request]] is the source-control equivalent gate that serves a similar function earlier in the pipeline. A change-management ticket performs the same control function at the process level, and the two-person rule is its manual analogue in safety-critical operations.

## Clash — *what pushes against this*
Auto-deploy workflows eliminate the human-in-the-loop entirely, trusting automation to validate deployments. Post-deploy verification inverts the timing, running the gate after the change lands in production rather than before.

## Roots — *where this comes from*
[[Release Stages]] are the foundational concept that approvals gate between transitions, and [[Separation of Duties]] is the governance principle that approvals instantiate in CI/CD pipelines.

## Paths — *where this leads*
[[SOC 1 Audit|SOC 1]] regimes depend on approval logs as key audit evidence, and related concerns like approval timeouts and automated approval gates determine whether humans are strictly required in the process.
