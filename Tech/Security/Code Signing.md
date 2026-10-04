---
type: atomic
tags: [coding/security, devops, coding/kotlin]
date: 2026-10-04
---

# Code Signing

## Idea
Signing a build with a private key proves who made it and that nobody changed it. On mobile, that key is also your app's identity, so losing it can mean you can never ship an update again.

## Definition
**Code signing** attaches a cryptographic signature to an executable or package using the publisher's private key; the operating system or store checks it with the matching public key or certificate before installing or running. It answers two questions: who published this, and has it been tampered with since. On Android the signing key goes further: an update only installs over an existing app if it is signed with the **same key**, so the keystore is effectively the app's identity. A worked example: a hobby Android app kept its release keystore out of git (ignored, never committed), with a backup stored separately along with its passwords, because a lost keystore would have stranded every installed user on the old version. Store-managed signing, where the store holds the real signing key and you only keep a resettable upload key, removes that single point of failure.

## Tools
- **Android** — `apksigner` and Play App Signing (store holds the app signing key, developer holds an upload key).
- **Apple** — codesign with Developer ID certificates and notarization.
- **Windows** — Authenticode via `signtool`.
- **Open source** — Sigstore (cosign) for keyless signing of containers and packages.

## Source
Microsoft introduced Authenticode in 1996 to sign downloadable code; Java signed JARs followed. Android has required signed APKs since launch (2008), and Google introduced Play App Signing in 2017 so a lost upload key is recoverable.

---

## Compass

**Roots** — *where this comes from*
It is applied public-key cryptography, and the private key is among the most valuable items in [[Secrets and Key Management]] because, unlike a password, it often can't be rotated without breaking existing installs.

**Paths** — *where this leads*
Signing usually moves into the [[CI-CD Pipeline]] so that only the pipeline touches the key, and it is the base for supply-chain checks on [[Build Artifacts]].

**Neighbors** — *what lives nearby*
[[Customer-Managed Keys (CMK)]] raise the same "you hold the key, you can lose the key" trade-off for encrypted data, and [[Workload Identity]] is how pipelines reach a signing service without storing the key.

**Clash** — *what pushes against this*
A signature proves origin, not safety: signed malware from a stolen key still installs, and handing your key to the store trades the risk of losing it for trusting someone else with it.
