---
type: atomic
tags: [coding/devops, deployment]
date: 2026-10-31
---

# Container Registry

## Idea
A container registry is where images live between being built and being run. It works like GitHub, but for packaged apps instead of source code.

## Definition
A registry is a server that stores [[Docker Image|container images]] and hands them out on request. An image is addressed as `registry/repository:tag`, for example `myregistry.azurecr.io/chat-api:1.4.2`. `docker push` uploads it and `docker pull` downloads it. Every image also has a **digest**, a content hash like `sha256:ab12…`. A tag such as `latest` or `1.4` can be moved to point at a different image, but a digest always means exactly the same bytes, so production deployments should pin digests. The registry is the handoff point in a [[CI-CD Pipeline]]: the pipeline builds and pushes once, and every environment pulls that same image. **Public** registries host official base images (Postgres, Redis, Nginx, .NET, Python). **Private** registries hold your company's images and are reached with a [[Workload Identity]] rather than a stored password. Most private registries also scan images for known vulnerabilities and can sign them.

## Providers
- **Azure** — Azure Container Registry (ACR), with geo-replication and built-in tasks for building images.
- **AWS** — Amazon ECR (Elastic Container Registry).
- **Google Cloud** — Artifact Registry.
- **Others** — Docker Hub (the default public registry), GitHub Container Registry, Quay, Harbor (self-hosted).

## Source
Docker Hub launched in 2014 as the public registry for Docker images. The registry protocol was later standardised as the OCI Distribution Specification.

---

## Compass

**Roots** — *where this comes from*
It is the storage half of [[Build Artifacts]]: the build produces a thing, and something has to keep it, version it and serve it.

**Paths** — *where this leads*
Pulling one immutable image into every stage is what makes [[Runtime Config (Build Once Deploy Everywhere)|build once, deploy everywhere]] work, and [[Code Signing]] lets the cluster refuse images nobody vouched for.

**Neighbors** — *what lives nearby*
[[NuGet]] feeds and npm registries do the same job for libraries; [[OCI (Open Container Initiative)|OCI]] defines the protocol, so any compliant tool can push to any registry.

**Clash** — *what pushes against this*
Mutable tags undo the whole promise: if `latest` quietly changes, two environments pulling "the same" image get different code. Public base images are also a supply-chain risk, since anything you pull without pinning or scanning runs with your app's privileges.
