---
type: atomic
tags: [coding/cloud, infrastructure]
date: 2026-10-31
---

# Virtual Machines

## Idea
A virtual machine is a pretend computer running inside a real one, with its own full operating system. When you "rent a server" in the cloud, you are almost always renting a VM.

## Definition
A **hypervisor** is software that slices one powerful physical machine into several isolated virtual machines. It hands each VM a share of the CPU, memory, disk and network, and each VM boots its own complete operating system, kernel included, believing it owns the hardware. A **VM image** is a snapshot of a fully set-up machine: OS, runtime, the app and every setting. You build it once, often with a tool like HashiCorp Packer (a "golden image"), and launch identical copies from it. That kills drift between servers and gives very strong isolation, because VMs share nothing above the hypervisor. The cost is weight. Images are gigabytes because each one carries a whole OS, boot takes minutes, and ten VMs means ten operating systems to run and patch. Cloud VMs (Azure Virtual Machines, AWS EC2, Google Compute Engine) are the base layer that PaaS, serverless and managed Kubernetes are all built on.

## Providers
- **Azure** — Virtual Machines and VM Scale Sets; Azure Compute Gallery for images.
- **AWS** — EC2 with AMIs (Amazon Machine Images) and Auto Scaling groups.
- **Google Cloud** — Compute Engine with custom images and managed instance groups.
- **Others** — VMware vSphere/ESXi, Hyper-V, KVM, Proxmox for on-premises.

## Source
IBM's CP-40 and CP-67 (late 1960s) were the first virtual machine systems. Popek and Goldberg's 1974 paper set out the formal requirements for virtualisation, and VMware (1998) brought it to x86 servers. Packer was released by HashiCorp in 2013.

---

## Compass

**Roots** — *where this comes from*
VM images answer [[It Works on My Machine]] by cloning the whole machine, which also ends the hand-built [[Snowflake Servers|snowflake server]].

**Paths** — *where this leads*
[[Containers Share the Host Kernel|Containers share the host's kernel]] instead of bringing their own, which is why they took over most of the work VMs used to do. VMs still sit underneath, as the nodes [[Kubernetes]] schedules containers onto.

**Neighbors** — *what lives nearby*
A VM sits inside a [[Virtual Network]] and is usually described in [[Infrastructure as Code]] rather than clicked together in a portal.

**Clash** — *what pushes against this*
Every VM is an OS you must patch, and that ops burden is exactly what [[Managed Web Hosting (PaaS)]] and [[Serverless Functions]] exist to remove. Paying for an always-on VM that mostly sits idle is the waste [[Scale-to-Zero]] targets.
