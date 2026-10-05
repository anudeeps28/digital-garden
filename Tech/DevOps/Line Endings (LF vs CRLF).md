---
type: atomic
tags: [coding/devops, coding/testing, dev-tools]
date: 2026-10-05
---

# Line Endings (LF vs CRLF)

## Idea
Every time you press Enter, the file stores an invisible "new line starts here" marker, and Windows uses a different marker from Linux and Mac. Files that look identical can still differ character by character.

## Definition
You never see it, but the end of every line in a text file holds a hidden character. There are two common versions:

| Name | Written in code as | Used by |
|---|---|---|
| **LF** (Line Feed) | `\n` ("backslash n") | Linux, macOS, and most tools and servers |
| **CRLF** (Carriage Return + Line Feed) | `\r\n` | Windows |

So "LF" and `\n` are two names for the same thing: the one-character "go to the next line" marker. CRLF is the same marker with an extra `\r` in front of it.

Most of the time this doesn't matter, because editors read both happily. It matters when a program compares files **exactly**, character by character. A golden-file (snapshot) test is the classic case: the test saves a known-good output file and checks every later run against it. To a human the two files look the same. To the computer, one has an extra hidden `\r` on every line, so the test fails with a diff that seems to show no differences. Other common symptoms:
- [[Git]] shows every line of a file as changed when only one was edited.
- A shell script written on Windows fails on Linux with `/bin/bash^M: bad interpreter`. The `^M` is the stray `\r`.

**An analogy:** two people write the same letter. One ends each line with a period, the other with a period plus a tiny invisible dot. Read side by side, they're the same letter. A machine checking dot by dot says they don't match.

**Where the names come from:** typewriters. *Carriage Return* slid the paper holder back to the left edge, and *Line Feed* rolled the paper up one line. Windows kept both steps, while Unix (and later macOS) kept only the line feed. Classic Mac OS, before OS X, used a lone CR.

**The fix:** pick one ending for the repository and let Git enforce it, rather than relying on everyone's editor settings. A `.gitattributes` file at the repo root does this:
```
* text=auto eol=lf
*.bat text eol=crlf
```
Git then stores LF in the repository and checks files out with the ending each type needs. Editors can also be told via `.editorconfig` (`end_of_line = lf`). For tests, either store golden files with a fixed ending or normalise both sides (replace `\r\n` with `\n`) before comparing.

**Not to be confused with LFN.** *Long File Names* is an old Windows feature, from Windows 95, that let file names be longer than the MS-DOS limit of 8 characters plus a 3-character extension. It has nothing to do with line endings. In conversations about Git or test files, "LF" almost always means the line ending.

## Source
The CR and LF control characters are defined in ASCII (ANSI X3.4, 1963) and come from teletype and typewriter mechanics. Git documentation, `gitattributes` ("End-of-line conversion") and `git config core.autocrlf`.

---

## Compass

**Roots** — *where this comes from*
It's a leftover from typewriters and teletypes, carried into the ASCII character set and then into operating systems that made different choices. Cross-platform teams inherit the split the moment Windows and Linux machines touch the same [[Git]] repository.

**Paths** — *where this leads*
Settling line endings with `.gitattributes` is one of the first things a repo shared across operating systems needs, especially when a [[CI-CD Pipeline]] runs on Linux agents while developers work on Windows. It also makes exact-match tests such as golden-file checks in [[Unit Tests]] reliable.

**Neighbors** — *what lives nearby*
Character encoding (UTF-8 vs UTF-16, or a hidden byte-order mark at the start of a file) causes the same "looks identical, compares different" problem. Trailing whitespace is a quieter cousin that shows up as noise in [[Pull Request]] diffs.

**Clash** — *what pushes against this*
Git's own `core.autocrlf` setting tries to convert endings automatically, but it lives on each developer's machine, so two people with different settings keep flipping the same files back and forth. A committed `.gitattributes` beats per-machine settings for that reason. And for most day-to-day editing the difference is invisible, which is exactly why it surprises people when it finally matters.
