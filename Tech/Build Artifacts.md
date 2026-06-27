---
type: atomic
tags: [coding/devops, coding/cicd]
date: 2026-04-24
---

# Build Artifacts

## Idea
A build artifact is the packaged output of a build pipeline — the immutable, versioned thing that downstream release pipelines deploy.

## Definition
At the end of a successful build, the [[CI-CD Pipeline]] produces an artifact: typically a zip of compiled binaries, a [[Docker Image]], a NuGet package, or a published .NET output folder. The artifact is uploaded to artifact storage (Azure DevOps Artifacts, a container registry, a file feed) and tagged with the build number. From there, [[Release Stages|release pipelines]] download the artifact and deploy it. **The contract:** an artifact is built *once* and deployed *many times* — same bytes promoted from dev → test → prod. This is what makes "[[Runtime Config (Build Once Deploy Everywhere)|build once, deploy everywhere]]" possible. It also means a redeploy doesn't rebuild — the release pipeline can grab an old artifact and ship it to fix a regression. If you're tempted to "rebuild prod," you're probably skipping the artifact step and creating drift between what was tested and what shipped.

## Source
CI/CD learning session.

---

## Compass

**Neighbors** — *what lives nearby*
A [[Docker Image]] is a specific kind of artifact, and the concept extends to NuGet packages and Maven JARs / Python wheels across other ecosystems — they're all the same idea in different packaging.

**Clash** — *what pushes against this*
"Build on every deploy" defeats the immutability guarantee, as does the practice of manual file copy, which skips versioned artifacts altogether.

**Roots** — *where this comes from*
The [[Build Pipeline vs Release Pipeline]] distinction centers on the artifact as the handoff between them, and artifacts are fundamentally the work product of the [[CI-CD Pipeline]].

**Paths** — *where this leads*
[[Artifact Filters]] are release-pipeline conditions that watch for new artifacts, while [[Release Stages]] define the environments an artifact flows through, and artifact retention policies govern how long old versions are kept.
