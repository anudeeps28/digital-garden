---
type: atomic
tags: [coding/azure, iac, devops]
date: 2026-06-26
---

# Bicep Module

## Idea
A Bicep module is a self-contained chunk of infrastructure you can name, reuse, and snap together — like a function for cloud resources.

## Definition
A Bicep module is a separate `.bicep` file that encapsulates the definition of one logical piece of infrastructure (say, a container app or monitoring service) and exposes parameters and outputs so it can be composed by a top-level template. In practice, a parent `main.bicep` calls into modules rather than defining every resource inline, with each module owning a coherent slice such as compute or observability. This keeps [[Bicep]] readable and lets the same module be reused across environments with different inputs. Outputs from one module (like a resource ID or principal identifier) feed into the next, so dependencies wire themselves up cleanly.

## Source
Microsoft Azure Bicep documentation; modules introduced as a core composition feature in Bicep (first released 2021 as an alternative to ARM templates).

---

## Compass

**Neighbors** — *what lives nearby*
Modules are a core composition feature of [[Bicep]] itself — a module is just a Bicep file consumed by another Bicep file. They're also fundamental to how [[IaC]] stays DRY and maintainable, letting you avoid repetition and keep your infrastructure code organized.

**Clash** — *what pushes against this*
While modules carry the *structure* of infrastructure, [[Bicep Parameter File|parameter files]] carry the *values* — they're complementary concerns that separate concerns differently.

**Roots** — *where this comes from*
Modules are a composition feature of the [[Bicep]] language itself, allowing you to build larger infrastructure definitions from smaller, reusable pieces.

**Paths** — *where this leads*
Understanding [[Deployment Scope]] matters because modules can target a different scope than the parent template, enabling flexible composition across organizational hierarchies.
