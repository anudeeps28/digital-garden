---
type: atomic
tags: [coding/security, coding/web-api]
date: 2026-10-04
---

# Path Traversal

## Idea
If a user can influence a file path, they can write `../../` or plant a symlink to climb out of the folder you meant and reach files you never intended to expose.

## Definition
**Path traversal** (directory traversal) happens when code joins untrusted input onto a base directory, `open(base + "/" + name)`, and `name` is `../../etc/passwd`, an absolute path, an encoded variant like `%2e%2e%2f`, or a symlink that points elsewhere. String checks such as "does it start with the base?" are easily fooled. The reliable fix is to **resolve the real path on both sides** (follow `..` and symlinks with `realpath`), then check that the resolved target sits inside one of the resolved allowed roots. Better still, never accept paths from clients at all: accept an id, look up the stored path. A worked example: a tool that launched agents in a user-chosen working folder resolved the requested folder and every allowed root to real paths before comparing, so a symlink could not get an agent started inside `~/.ssh`.

## Source
Catalogued by MITRE as CWE-22 ("Improper Limitation of a Pathname to a Restricted Directory"). A famous early case was the Microsoft IIS Unicode directory traversal flaw of 2000 (MS00-078). OWASP now files it under Broken Access Control.

---

## Compass

**Roots** — *where this comes from*
It feeds on the gap explained in [[Relative vs Absolute Paths]]: a relative path means nothing until it is resolved, and the attacker controls part of the resolution.

**Paths** — *where this leads*
When an allowed-roots check can't resolve something, it should [[Fail Closed]], and the safest design avoids client paths entirely, as in the stored-path rule for [[Pre-Signed URL|pre-signed URLs]].

**Neighbors** — *what lives nearby*
[[IDOR (Insecure Direct Object Reference)|IDOR]] is the same mistake with database ids instead of file paths: trusting a reference the client handed you.

**Clash** — *what pushes against this*
Realpath checks have a time-of-check to time-of-use gap, since a symlink can be swapped after the check, so high-risk code adds OS-level confinement like chroot, containers or `openat`-style APIs as [[Defence in Depth]].
