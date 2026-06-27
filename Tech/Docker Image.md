---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# Docker Image

## Idea
A Docker image is the blueprint for a container — a read-only template containing your app, runtime, and dependencies, ready to be run.

## Definition
A [[Docker]] image is built from a `Dockerfile` — a text file with instructions like "start from the .NET 8 SDK image, copy my code, build it, and set the entry point." Each instruction creates a layer, and layers are cached for fast rebuilds. Images are tagged with versions (e.g., `kba-api:v1.2.3`) and stored in registries like [[Azure Container Registry]]. When you "run" an image, Docker creates a container from it. In the KBA project, the [[CI-CD Pipeline]] builds a Docker image of the [[REST API]], pushes it to ACR, and [[Azure Container Apps]] pulls and runs it.

## Source
KBA AI Document Ingestion project

---

## Compass

**Roots** — *where this comes from*
Docker images are at the core of [[Docker]]'s architecture, and they're stored and managed in registries like [[Azure Container Registry]].

**Paths** — *where this leads*
Docker images are deployed and run by [[Azure Container Apps]], and they're built and pushed automatically by the [[CI-CD Pipeline]].

**Neighbors** — *what lives nearby*
A [[VM Snapshot]] serves a similar purpose for virtual machines — a frozen state ready to be instantiated. [[NuGet Package|NuGet packages]] are also units of packaged code, though they target libraries rather than full applications.

**Clash** — *what pushes against this*
[[Source Code]] is the raw, uncompiled form that must be built before execution, whereas a Docker image is already prepared and ready to run. A [[Running Container]] is the live, mutable instance spawned from an image — the image itself is immutable.
