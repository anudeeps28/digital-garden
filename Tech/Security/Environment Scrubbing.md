---
type: atomic
tags: [coding/security, ai/agents, devops]
date: 2026-10-04
---

# Environment Scrubbing

## Idea
A child process inherits every environment variable its parent has, including API keys. Give spawned processes only the variables they need.

## Definition
By default, `fork`/`exec`, Python's `subprocess`, and Node's `child_process` pass the parent's whole environment to the child. If the parent holds `OPENAI_API_KEY`, `AWS_SECRET_ACCESS_KEY` or a database URL, so does every script, plugin or agent it launches, and anything that child runs can read or log them. **Environment scrubbing** means building the child's environment from an explicit **allowlist** (`PATH`, `HOME`, `LANG`, plus the specific variables that tool needs) instead of copying everything. A worked example: a tool that launched coding agents as subprocesses passed each one a minimal allowlisted environment, so an agent that ran arbitrary shell commands could not echo the parent's keys. It is cheap to do and closes a leak that is otherwise invisible until a crash dump or debug log prints `env`.

## Source
MITRE CWE-526 ("Exposure of Sensitive Information Through Environmental Variables") catalogues the weakness. `sudo` has long reset the environment by default (`env_reset`) for the same reason, and the Twelve-Factor App's advice to keep config in environment variables (2011) made the problem common.

---

## Compass

**Roots** — *where this comes from*
It is least privilege applied to configuration, and a practical corner of [[Secrets and Key Management]]: a secret is only as safe as the widest set of processes that can read it.

**Paths** — *where this leads*
It matters most inside an [[Agent Harness]], where the child is a model running commands you didn't write, and it shrinks the [[Blast Radius]] of any one compromised tool.

**Neighbors** — *what lives nearby*
[[Workload Identity]] goes further by removing long-lived keys from the environment altogether, and [[Default-Deny Allowlisting]] is the same allowlist-first shape applied to networks.

**Clash** — *what pushes against this*
Allowlists break tools that quietly depend on some variable you forgot (a proxy setting, a locale, a cert path), so scrubbing trades a little debugging friction for safety.
