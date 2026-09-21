---
type: atomic
tags: [iac, devops, coding/architecture, coding/azure]
date: 2026-09-16
---

# Shared Module Library

## Idea
Ten teams each writing their own storage account template produces ten subtly different security postures. One reviewed module produces one.

## Definition
A shared module library is a central repository of reusable [[Infrastructure as Code]] components — a storage module, a key vault module, a networking module — that every project imports instead of writing its own. The value is that a hardening decision or a compliance fix is made once and propagates, rather than being reimplemented nine times with nine near-misses. Two mechanical details decide whether it works in practice. The first is **how it's referenced**: importing by relative sibling path means the library must be cloned *beside* the consuming repository rather than inside it, an unwritten layout rule that breaks a new machine's first build. Pinning by version tag or registry reference avoids that but adds an upgrade step. The second is **freshness**: a local clone that's months behind produces confident, wrong answers about what the library offers — so pull before you reason about it.

## Source
Common practice in Terraform (module registries), [[Bicep]] (template specs and module paths), and Helm (chart repositories).

---

## Compass

**Roots** — *where this comes from*
It's the consumable half of [[Centralized Infrastructure Ownership]] — the carrot next to the policy stick.

**Paths** — *where this leads*
Version pinning becomes an upgrade obligation: a security fix in the library only helps consumers who bump.

**Neighbors** — *what lives nearby*
[[NuGet]] packages solve the same reuse problem for application code, with far better tooling for versioning than most IaC ecosystems have.

**Clash** — *what pushes against this*
A shared module is a shared constraint. When a project needs something the module doesn't expose, the options are a parameter nobody else wants, a fork, or a wait — and all three are worse than the copy-paste would have been.
