---
type: atomic
tags: [coding/devops, standards]
date: 2026-10-31
---

# OCI (Open Container Initiative)

## Idea
Docker is the tool; OCI is the standard. Images built with Docker follow an open format that any runtime can run, so in production Docker itself often isn't running at all, but Docker-built images are.

## Definition
The Open Container Initiative is a Linux Foundation project that turned Docker's image and runtime formats into vendor-neutral specifications. There are three. The **Image Spec** defines how an image's layers and metadata are laid out. The **Runtime Spec** defines how to unpack an image and run it as an isolated process; `runc` is the reference implementation. The **Distribution Spec** defines the HTTP API a [[Container Registry]] speaks. Because of these specs the container world split into interchangeable parts. You can build with Docker, Podman or Buildah, store in any registry, and run with containerd or CRI-O, which is what [[Kubernetes]] nodes typically use. "Docker" in everyday speech usually means "OCI containers", and learning Docker teaches you the format everything else uses.

## Source
Formed in June 2015 by Docker, CoreOS and others under the Linux Foundation (briefly called the Open Container Project); Runtime and Image Spec v1.0 released July 19, 2017 ([linuxfoundation.org](https://www.linuxfoundation.org/press/press-release/open-container-initiative-oci-releases-v1-0-of-container-standards)).

---

## Compass

**Roots** — *where this comes from*
It standardises what [[Docker]] invented, after rival formats (CoreOS's appc and rkt) threatened to split the ecosystem.

**Paths** — *where this leads*
Because the [[Docker Image]] format is shared, the same image runs on any cloud's [[Serverless Containers]] platform or Kubernetes service, which is the main reason containers make moving between clouds realistic.

**Neighbors** — *what lives nearby*
[[Swagger and OpenAPI|OpenAPI]] plays the same role for HTTP APIs: a neutral contract that let many tools work together where there had been one vendor's format.

**Clash** — *what pushes against this*
The standard covers packaging and running, not everything around it. Compose files, build features and orchestration still differ between tools, so "OCI-compatible" doesn't mean "drop-in replacement".
