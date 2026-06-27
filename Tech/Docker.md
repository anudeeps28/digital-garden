---
type: atomic
tags: [coding/devops]
date: 2026-03-24
---

# Docker

## Idea
Docker packages your app and all its dependencies into a container that runs the same everywhere — your machine, a colleague's machine, or the cloud.

## Definition
Docker is a platform for building, shipping, and running applications in containers. A container is a lightweight, standalone package that includes your application code, runtime ([[.NET 8]]), libraries, and configuration — everything needed to run. You define the container in a `Dockerfile`, build it into a [[Docker Image]], and run it anywhere Docker is installed. This eliminates "works on my machine" problems. In the project, the [[REST API]] is containerized: the [[CI-CD Pipeline]] builds a Docker image, pushes it to [[Azure Container Registry]], and deploys it to [[Azure Container Apps]].

## Source
AI document ingestion project

---

## Compass

**Roots** — *where this comes from*
Docker is a cornerstone of modern [[DevOps]], enabling teams to manage application deployment at scale. The question of how a container differs from a [[Virtual Machines|virtual machine]] is fundamental to understanding containerization.

**Paths** — *where this leads*
Docker builds on the concept of a [[Docker Image]] as the blueprint for a container, which then gets deployed to [[Azure Container Apps]] or pushed to [[Azure Container Registry]] for storage. [[CI-CD Pipeline|CI-CD pipelines]] leverage Docker to automate the build and deployment process.

**Neighbors** — *what lives nearby*
[[Virtual Machines]] also isolate applications but are heavier with a full OS per VM, while [[Podman]] offers an alternative container runtime that maintains Docker compatibility.

**Clash** — *what pushes against this*
[[Bare Metal]] systems run directly on the host OS with no isolation, and [[Manual Installation]] requires installing dependencies by hand on each server — both approaches lack the consistency and portability Docker provides.
