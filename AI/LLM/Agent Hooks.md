---
type: atomic
tags: [ai/agents, coding/security, devops]
date: 2026-10-04
---

# Agent Hooks

## Idea
Hooks are small deterministic scripts that run at fixed points in an agent's loop, so a rule is enforced every time instead of whenever the model remembers it.

## Definition
An instruction in a prompt is a request; a hook is code. Agent tools expose lifecycle events such as **PreToolUse** (before a command or edit runs, and able to block it), **PostToolUse** (after it runs), **PreCompact** (before the context is summarised) and **SessionEnd**. A worked example of a hook set: a PreToolUse script blocks destructive git commands (force push, hard reset) and destructive database statements, and rejects edits that contain what look like hardcoded secrets; a PreCompact hook writes the current task state to disk before context is squashed; a SessionEnd hook appends a log of what happened. The important caveat: a regex denylist is an **oversight gate**, not a sandbox. Base64-encoded commands, a variable holding the dangerous string, or a heredoc piped to a shell all slip past pattern matching. Hooks catch honest mistakes; containment needs real isolation.

```bash
# PreToolUse: exit code 2 blocks the call
echo "$CMD" | grep -Eq 'git push .*--force|reset --hard' && exit 2
```

## Tools
- **Claude Code** — hooks on PreToolUse, PostToolUse, PreCompact, SessionEnd and other events, configured in settings files.
- **Git hooks** — the older model of the same idea (pre-commit, pre-push).

## Source
Claude Code introduced hooks in June 2025 with a handful of events, growing to more than a dozen by early 2026. The pattern descends from git hooks and CI policy checks.

---

## Compass

**Roots** — *where this comes from*
Hooks are the enforcement layer of an [[Agent Harness]], turning soft guidance into hard checks.

**Paths** — *where this leads*
Saving state on PreCompact is what makes [[Checkpoint and Respawn]] safe, and blocking the riskiest commands shrinks the [[Blast Radius]] of a bad decision.

**Neighbors** — *what lives nearby*
[[Default-Deny Allowlisting]] is the stronger alternative to a denylist, and [[Defence in Depth]] explains why hooks are one layer among several.

**Clash** — *what pushes against this*
[[Security Control vs Security Boundary]] is the hard limit: a hook a determined process can route around is a control, not a boundary, so never rely on it alone for untrusted code.
