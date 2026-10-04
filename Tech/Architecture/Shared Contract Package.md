---
type: atomic
tags: [coding/architecture, coding/web-api, frontend]
date: 2026-10-04
---

# Shared Contract Package

## Idea
Put the message types, validators and enums that client and server both depend on into one package that both import. If the contract changes, both sides change together or the build fails.

## Definition
When a client and a server each define their own copy of a message shape, the copies drift: a field is renamed on one side, an enum gains a value on the other, and the mismatch shows up at runtime as a silently ignored field or a broken screen. A **shared contract package** removes the second copy. In a monorepo it is typically a small workspace package (for example `packages/shared`) containing the **types** of every message, the **validators** that check them at runtime, and the **enums and constants** both sides switch on. The client and the server import from it, so a renamed field becomes a compile error in both. This kills an entire class of silent-drift bugs for very little cost. It's also worth knowing where to stop. A full rewrite of every type into a schema-first library, so types are generated from schemas, was considered in one project and rejected: the existing hand-written types plus validators already prevented the drift, and the rewrite would have touched every file for a marginal gain. Shared contracts work best for things that genuinely cross the boundary; internal types on each side should stay private.

## Tools
- **TypeScript workspaces** — npm, pnpm or Yarn workspaces for an internal shared package.
- **Zod / Valibot** — runtime validators that also produce static types.
- **Protocol Buffers / OpenAPI** — language-neutral contracts with generated code for each side.

## Source
No single coiner for the package itself. It draws on Bertrand Meyer's "Design by Contract" (Eiffel, 1986), Ian Robinson's "Consumer-Driven Contracts: A Service Evolution Pattern" (martinfowler.com, 2006), and end-to-end typed stacks in TypeScript monorepos such as tRPC (2020).

---

## Compass

**Roots** — *where this comes from*
It is [[Define Contract Before Implementation]] turned into code, and the TypeScript cousin of a [[Shared Module Library]] that several projects consume.

**Paths** — *where this leads*
Types only protect at compile time, so the package usually ships [[Runtime Schema Validation]] for messages arriving over the wire, which matters for [[Server-Authoritative State]] where every intent is untrusted.

**Neighbors** — *what lives nearby*
A [[Ubiquitous Language]] shares vocabulary between people; the contract package shares it between programs. [[DTOs (Data Transfer Objects)]] are the shapes it typically holds.

**Clash** — *what pushes against this*
Shared packages couple release cycles, so they work in a monorepo but hurt across independently deployed teams, where consumer-driven contract tests are gentler. And [[Read Payloads Are Not Write Payloads]] warns against sharing one type for every direction just because it is convenient.
