---
type: atomic
tags: [coding/database, coding/security, coding/azure]
date: 2026-09-16
---

# Transparent Data Encryption

## Idea
Encryption at rest protects against someone walking off with the disk — not against someone with a valid login. Knowing which threat it actually covers is the whole point.

## Definition
Transparent Data Encryption (TDE) encrypts database files, log files, and backups on disk, decrypting pages transparently as they're read into memory. It's "transparent" because no application change is required — queries behave identically. That transparency is also its limit: an authenticated connection sees plaintext, so TDE does nothing against SQL injection, a leaked credential, or an over-privileged account. It defends the *stolen media* and *stolen backup file* threats, and it satisfies the encryption-at-rest line in most compliance frameworks. On Azure SQL it's on by default with a Microsoft-managed key; moving to [[Customer-Managed Keys (CMK)]] is what changes the trust story, because it means the platform operator alone can no longer decrypt.

## Source
Introduced in SQL Server 2008; enabled by default on Azure SQL Database since 2017. Equivalent features exist in Oracle, [[PostgreSQL]] (via filesystem or cloud-provider encryption), and all major cloud storage services.

---

## Compass

**Roots** — *where this comes from*
TDE is the bottom layer of [[Multi-Tenant Data Isolation]] — the one that assumes every layer above it has already been bypassed.

**Paths** — *where this leads*
The upgrade path is [[Customer-Managed Keys (CMK)]], which moves key custody from the platform to you.

**Neighbors** — *what lives nearby*
[[Managed Identity]] removes secrets from the wire and from config; TDE removes plaintext from the disk. Different surfaces, same instinct.

**Clash** — *what pushes against this*
Because it's on by default and invisible, TDE creates a false sense of completeness — a compliance checkbox that reads like "our data is encrypted" while the live attack paths run entirely through authenticated sessions.
