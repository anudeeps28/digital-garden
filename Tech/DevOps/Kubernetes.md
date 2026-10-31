---
type: atomic
tags: [coding/devops, coding/distributed-systems, infrastructure]
date: 2026-10-31
---

# Kubernetes

## Idea
Kubernetes is a fleet manager for containers. You tell it what should be running, and it keeps making that true across many machines: restarting crashes, spreading load and rolling out new versions.

## Definition
Kubernetes (K8s) runs containers across a **cluster** of machines called **nodes**. You don't tell it *how* to run things; you **declare** the state you want in YAML: "three copies of this [[Docker Image|image]], reachable on this port, with this much CPU." A **control loop** keeps comparing reality to that declaration and closes the gap. If a container crashes it is restarted. If a node dies its workloads move elsewhere. If you change the image tag, it does a **rolling update**, replacing copies one by one so there is no downtime. The core objects are the **Pod** (one or more containers scheduled together), the **Deployment** (keeps N copies of a Pod running and handles rollouts), the **Service** (a stable address in front of changing Pods) and **Ingress** (routes outside HTTP traffic in). A [[Health Probe]] tells it when a Pod is ready or broken. Nodes run containers through a runtime such as containerd; Docker itself is usually not installed.

## Providers
- **Azure** — AKS (Azure Kubernetes Service); Azure Container Apps hides a managed Kubernetes under a simpler surface.
- **AWS** — EKS (Elastic Kubernetes Service).
- **Google Cloud** — GKE (Google Kubernetes Engine), including Autopilot mode.
- **Others** — k3s, kind and minikube for local or edge clusters; Red Hat OpenShift.

## Source
Created at Google by Joe Beda, Brendan Burns and Craig McLuckie, drawing on Google's internal Borg cluster manager. First commit June 6, 2014, announced at DockerCon 2014. Version 1.0 shipped July 21, 2015, when Google donated it to the newly formed Cloud Native Computing Foundation ([kubernetes.io](https://kubernetes.io/blog/2024/06/06/10-Years-of-Kubernetes/)).

---

## Compass

**Roots** — *where this comes from*
It exists because [[Containers Share the Host Kernel|containers are cheap to start and kill]], so a scheduler can treat them as interchangeable cattle rather than [[Snowflake Servers|pets]].

**Paths** — *where this leads*
Its declarative model leads naturally to [[Pull-Based Deployment|pull-based (GitOps) deployment]], where an agent in the cluster syncs to a Git repository instead of a pipeline pushing changes.

**Neighbors** — *what lives nearby*
[[Serverless Containers]] give you most of the benefit, with Kubernetes running out of sight underneath. [[Docker Compose]] is the single-machine, development-time cousin.

**Clash** — *what pushes against this*
The power comes with a lot of moving parts: networking, storage classes, RBAC, upgrades. Small teams often adopt it before they need it, and [[First Make It Work, Then Make It Better]] argues for starting on PaaS or serverless containers and moving up only when you feel real pain.
