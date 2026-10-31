---
type: atomic
tags: [coding/devops, deployment, coding/dotnet]
date: 2026-10-31
---

# Self-Contained Build

## Idea
Bundle the app *and* its runtime into one package, like a meal kit with everything in the box, so the target machine needs nothing installed first.

## Definition
A normal build produces code that expects the runtime to already be on the machine: a .NET DLL needs the .NET runtime, a Python script needs Python. A self-contained build ships the runtime inside the output. In .NET, `dotnet publish --self-contained -r linux-x64` copies the runtime next to your app, and `-p:PublishSingleFile=true` squeezes it into one executable; trimming and Native AOT shrink it further. **Go** and **Rust** go further by default: they compile to a single native binary with no runtime to install at all. The result is simple to deploy. You copy one file and run it, with no version clashes with whatever else is on the server. The limits are just as clear. It packages only *your app*, not the database or cache it talks to. It is built for one OS and CPU architecture. And you still need a server to run it on. It suits command-line tools, small services and agents that have to run on machines you don't control. It also pairs well with containers: a single static binary makes a tiny image built `FROM scratch` or from a distroless base.

## Source
Go (Google, 2009) made static single-binary deployment its default. .NET Core added self-contained deployment from 1.0 (2016) and single-file publishing in .NET Core 3.0 (2019).

---

## Compass

**Roots** — *where this comes from*
It is the lightest answer to [[It Works on My Machine]]: carry the runtime instead of hoping the server has the right one.

**Paths** — *where this leads*
Building for a different OS or chip than the one you're on is [[Cross-Compilation]], and a self-contained binary is the ideal last stage of a [[Multi-Stage Docker Build]].

**Neighbors** — *what lives nearby*
[[DotNet 8]] is the runtime it bundles in the .NET case; [[Containers Share the Host Kernel|containers]] carry the same idea up a level, packaging libraries and OS userland too.

**Clash** — *what pushes against this*
Every app carries its own copy of the runtime, so a security fix to the runtime means rebuilding and redeploying every app rather than patching the server once. It also does nothing for OS-level settings or the services the app depends on.
