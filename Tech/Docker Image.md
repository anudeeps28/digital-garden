---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# Docker Image

## Idea
A Docker image is the blueprint for a container — a read-only template containing your app, runtime, and dependencies, ready to be run.

## Definition
A [[Docker]] image is built from a `Dockerfile` — a text file with instructions like "start from the base OS image, copy code, install dependencies, and set the entry point." Each instruction creates a layer, and layers are cached for fast rebuilds. Images are tagged with versions and stored in registries like [[Docker Hub]] or container registries. When you "run" an image, Docker creates a container from it — a live, executable instance of that blueprint.

## Source
Solomon Hykes, dotCloud (now Docker, Inc.), first released 2013. Docker revolutionized containerization by making it accessible and practical for developers.

---

## Compass

**Roots** — *where this comes from*
Docker images are at the core of [[Docker]]'s architecture. The concept of immutable, layered images builds on decades of containerization research and makes the practice of packaging and distributing applications reproducibly feasible.

**Paths** — *where this leads*
Docker images are deployed and run on container orchestration platforms like [[Docker]] Engine, Kubernetes, or managed container services, and they're typically built and pushed automatically by CI/CD pipelines.

**Neighbors** — *what lives nearby*
A [[VM Snapshot]] serves a similar purpose for virtual machines — a frozen state ready to be instantiated. [[NuGet Package|NuGet packages]] and [[JAR Files|JAR files]] are also units of packaged code, though they target language-specific libraries rather than full containerized applications.

**Clash** — *what pushes against this*
[[Source Code]] is the raw, uncompiled form that must be built before execution, whereas a Docker image is already prepared and ready to run. A [[Running Container]] is the live, mutable instance spawned from an image — the image itself is immutable.
