---
type: atomic
tags: [coding/devops, infrastructure]
date: 2026-10-31
---

# Containers Share the Host Kernel

## Idea
A virtual machine brings its own operating system; a container borrows the host's kernel and only packages what sits above it. That one difference is why containers are megabytes instead of gigabytes and start in seconds instead of minutes.

## Definition
A container is an ordinary process that the Linux kernel isolates. **Namespaces** give it a private view of the system: its own process list, network interfaces, hostname and filesystem root, so it can't see other containers. **Control groups (cgroups)** cap how much CPU and memory it may use. The [[Docker Image|image]] holds only the app, its runtime and its libraries; the kernel underneath is the host's. Compare that with [[Virtual Machines]], where a hypervisor emulates hardware and every VM boots a full OS. Ten VMs are ten restaurants, each with its own building and plumbing. Ten containers are ten food trucks in one lot, sharing the lot's power hookup.

| | Virtual machine | Container |
|---|---|---|
| Size | Gigabytes | Megabytes |
| Startup | Minutes | Seconds or less |
| Per server | A handful | Dozens to hundreds |
| Isolation | Very strong | Strong, slightly weaker |

Two consequences follow. A Linux container needs a Linux kernel, which is why Docker Desktop on a Mac or Windows quietly runs a small Linux VM. And a kernel bug can be a way out of every container on the host, so the isolation is good but not VM-grade.

## Source
The building blocks predate Docker: `chroot` (Unix V7, 1979), FreeBSD jails (2000), Solaris Zones (2004), Linux cgroups (contributed by Google engineers, merged in 2008) and LXC (2008). Docker (Solomon Hykes, 2013) made them easy to use.

---

## Compass

**Roots** — *where this comes from*
It is the lighter answer to [[It Works on My Machine]]: ship the environment with the app, but leave the kernel out.

**Paths** — *where this leads*
Because containers are cheap to start and kill, you can run hundreds per machine and let [[Kubernetes]] reschedule them freely. That only works if they are [[Stateless Services|stateless]] and keep data in a [[Docker Volume]].

**Neighbors** — *what lives nearby*
[[Docker]] is the tooling that made this usable, and [[OCI (Open Container Initiative)|OCI]] is the standard that lets other runtimes run the same images.

**Clash** — *what pushes against this*
A shared kernel is a weaker [[Security Control vs Security Boundary|security boundary]] than a hypervisor. For hostile multi-tenant workloads, platforms add microVMs (Firecracker, Kata Containers) or gVisor to get VM-style isolation back.
