---
type: atomic
tags: [coding/devops, data]
date: 2026-10-31
---

# Docker Volume

## Idea
Containers are disposable: delete one and everything written inside it is gone. A volume is storage that lives outside the container, so the data survives when the container doesn't.

## Definition
A container's filesystem is a thin writable layer on top of its read-only [[Docker Image|image]]. Anything written there disappears when the container is removed, and it is slow for heavy writes. A **volume** is a directory managed by the container runtime and mounted into the container at a path, such as `/var/lib/postgresql/data` for a Postgres container. The database writes there, and when you replace the container with a newer image, the new one mounts the same volume and finds its data intact. **Named volumes** are managed by Docker and are the default for databases. **Bind mounts** map a host folder straight in, which suits local development when you want code edits to show up live. **tmpfs mounts** live only in memory. In [[Kubernetes]] the same idea becomes a PersistentVolume backed by a cloud disk or file share. The pattern is a strict split: the container is code and can be thrown away; the volume is state and must be backed up.

## Source
Docker documentation, "Volumes"; the split between disposable processes and attached storage echoes the Twelve-Factor App's "backing services" and "disposability" factors (Adam Wiggins, 2011).

---

## Compass

**Roots** — *where this comes from*
It follows from [[Containers Share the Host Kernel|containers being cheap to kill and restart]], which only works if [[Stateless Services|the process itself holds no state]] that matters.

**Paths** — *where this leads*
In [[Docker Compose]] a named volume keeps your local [[PostgreSQL]] data across `docker compose down` and `up`. Anything stored in a volume needs the same backups and [[Restore Drill|restore drills]] as any other database disk.

**Neighbors** — *what lives nearby*
[[Object Storage]] is the cloud-native alternative for files: instead of mounting a disk, the app talks to a storage API and stays fully stateless.

**Clash** — *what pushes against this*
A volume ties the container to wherever its storage lives, which fights the "run anywhere" promise. Running production databases in containers with volumes is possible, but most teams hand that to a [[Managed SQL Database]] instead.
