---
type: atomic
tags: [coding/azure, coding/database, devops, coding/security]
date: 2026-10-01
---

# Object Storage

## Idea
Object storage is where cloud apps put files: you hand it some bytes and a name, and it keeps them safely and cheaply at almost any scale. It looks like a file system but it isn't one, and that difference matters.

## Definition
Object storage keeps data as **objects**, each made of the bytes, some **metadata** (content type, custom tags) and a **key** (its name). Objects sit in a flat **bucket** or **container**, and you read and write them over HTTP (`PUT`, `GET`, `DELETE`). It is not a file system. The slashes in `invoices/2026/a.pdf` are just characters in the key, so there are no real folders, "rename" means copy then delete, and you replace an object whole rather than editing it in place. In return you get storage that is cheap, practically unlimited and very durable, because the provider keeps several copies, optionally in another region ([[Geo-Redundant Backup|geo-redundant]]). **Access tiers** (hot, cool, archive) trade storage price against retrieval cost and delay; archived data can take hours to bring back. **Versioning** keeps old copies when something is overwritten, and **immutability** policies (write once, read many) stop anyone deleting data before a retention date, which helps against ransomware and for compliance. Access works best through identity ([[Workload Identity]]), or with a [[Pre-Signed URL]] when a browser needs one object for a short time. The classic mistake is making a whole bucket public. Add a [[Private Endpoint]] for private network access and [[Customer-Managed Keys (CMK)]] when you must control the encryption keys yourself.

## Providers
- **Azure** — Azure Blob Storage (containers inside a storage account; hot, cool, cold and archive tiers).
- **AWS** — Amazon S3 (buckets; Standard, Infrequent Access and Glacier storage classes).
- **Google Cloud** — Cloud Storage (Standard, Nearline, Coldline and Archive classes).
- **Others** — Cloudflare R2 (S3-compatible, no egress fees); MinIO (self-hosted, S3-compatible).

## Source
Amazon S3 (2006) defined the model, and its API became the de facto standard that most other object stores copy.

---

## Compass

**Roots** — *where this comes from*
It came from the need to store huge amounts of unstructured data (uploads, backups, logs) more cheaply than a [[Relational Database]] or a shared file server could.

**Paths** — *where this leads*
Handing files straight to browsers leads to [[Pre-Signed URL|pre-signed URLs]]; locking them down leads to [[Private Endpoint|private endpoints]] and [[Customer-Managed Keys (CMK)]].

**Neighbors** — *what lives nearby*
[[Geo-Redundant Backup]] relies on the same replication options; a [[Managed SQL Database]] usually stores an object's key rather than the file itself.

**Clash** — *what pushes against this*
Anything that needs file-system behaviour (appending, locking, renaming folders, many small random writes) is slow or awkward here. Egress fees can also make reading data back out cost more than storing it.
