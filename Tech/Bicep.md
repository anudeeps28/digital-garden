---
type: atomic
tags: [coding/azure, iac, devops]
date: 2026-06-26
---

# Bicep

## Idea
Bicep is a clean, declarative language that lets you describe Azure infrastructure the way you'd describe it to a colleague — then compiles down to the verbose ARM JSON Azure actually understands.

## Definition
Bicep is a domain-specific language (DSL) that transpiles to Azure Resource Manager (ARM) templates, giving you readable, type-safe [[IaC]] for [[Azure]]. In practice, every cloud resource is defined in Bicep — a `main.bicep` orchestrates the deployment and pulls in environment values from a `.bicepparam` file so test and production environments stay separate but share one source of truth. The resources Bicep can provision include [[Azure Functions]] apps, [[Azure Container Apps]] containers, [[Azure SQL]], [[Azure Key Vault]], [[Azure OpenAI]], and [[Azure AI Search]], all wired to a [[Managed Identity]] so no secrets live in the templates. Because Bicep is declarative, re-running it converges the environment to the desired state rather than issuing imperative commands.

## Source
Microsoft, introduced as a domain-specific language for Azure infrastructure-as-code in 2020; now a core part of Azure's resource definition tooling alongside ARM templates.

---

## Compass

**Roots** — *where this comes from*
Bicep exists specifically to provision [[Azure]] resources, grounded in the cloud platform's resource management needs.

**Paths** — *where this leads*
Bicep templates are parameterized per environment via [[Bicep Parameter File|parameter files]], and every Bicep deployment runs against a chosen [[Deployment Scope]].

**Neighbors** — *what lives nearby*
Bicep is the concrete language we use to practice [[IaC]], and it's composed of reusable [[Bicep Module|modules]] that make infrastructure definitions more modular and composable.

**Clash** — *what pushes against this*
[[Connection String|Connection strings]] represent the old, secret-bearing way of wiring resources that Bicep combined with managed identity replaces.
