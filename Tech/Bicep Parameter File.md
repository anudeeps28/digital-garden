---
type: atomic
tags: [coding/azure, iac, devops]
date: 2026-06-26
---

# Bicep Parameter File

## Idea
A Bicep parameter file is the one knob-board per environment — same template, different settings — so Test and Prod never drift in structure but stay distinct in values.

## Definition
A `.bicepparam` file supplies environment-specific values to a single shared Bicep template, letting one `main.bicep` deploy differently to each environment. On the AI document ingestion project, `main.test.bicepparam` and `main.prod.bicepparam` feed the same `main.bicep` — they set things like SKU sizes, resource names, and which [[Azure OpenAI]] or [[Azure AI Search]] endpoint to target, while the template's logic stays identical. This is the mechanism that keeps Test and Prod as separate-but-mirrored environments. Sensitive values aren't hardcoded here either; secrets stay in [[Azure Key Vault]] and services reach them via [[Managed Identity]], so a param file holds configuration, not credentials.

## Source
AI document ingestion project

---

## Compass

**Neighbors** — *what lives nearby*
Both [[Bicep Module|Bicep modules]] and parameter files are pieces of a Bicep deployment; modules give structure while param files give values. Parameter files carry configuration much like [[Connection String|connection strings]] do, but parameter files keep secrets *out* and defer them to [[Azure Key Vault]] instead.

**Clash** — *what pushes against this*
[[Bicep]] itself is the environment-agnostic logic, while the parameter file is the environment-specific data — they're opposite sides of the same deployment coin.

**Roots** — *where this comes from*
[[IaC|Infrastructure as Code]] uses parameterization as its core mechanism for serving multiple environments from a single definition.

**Paths** — *where this leads*
The chosen parameter file pairs with a [[Deployment Scope]] at deploy time, determining how and where infrastructure lands.
