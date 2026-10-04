---
type: atomic
tags: [coding/embedded, coding/architecture]
date: 2026-10-04
---

# Device Driver

## Idea
A device driver turns a datasheet into an API. It hides the timing diagrams, register sequences and protocol quirks of one piece of hardware behind a few clean functions the rest of the program can trust.

## Definition
A **driver** sits between application code and a specific device. Below it is a **hardware abstraction layer (HAL)** that exposes generic operations such as "set pin", "read SPI byte" or "wait microseconds"; above it is an interface like `sensor_init()`, `sensor_read_temperature()`. The driver's job is to implement the device's protocol exactly as the datasheet describes: power-up delays, command bytes, the order of chip-select and clock edges, how long a conversion takes. Two habits make drivers robust. First, treat the datasheet as the **contract**: encode its timing values as named constants and write the sequence step by step, so a reviewer can check the code against the spec line by line. Second, put a **timeout on every wait**: never loop forever on "busy bit cleared" or "line went high", because hardware that is unplugged, broken or simply slow will hang the whole system. Return an error instead and let the caller decide whether to retry. A worked example from a classroom-style exercise: a driver for a one-wire style sensor written in [[CPP|C++]] as a small class over a GPIO HAL became testable on a laptop once the HAL was an interface that a fake could implement.

## Source
The concept is as old as operating systems; Unix (1970s) made it a defining structure by exposing drivers as files under `/dev`. *Linux Device Drivers* (Rubini, 1998; later Corbet, Rubini and Kroah-Hartman) is the classic reference for the OS side.

---

## Compass

**Roots** — *where this comes from*
Every driver is built from [[Memory-Mapped IO]] register access, and reading the datasheet first is [[Define Contract Before Implementation]] applied to hardware.

**Paths** — *where this leads*
Protocol sequences are cleanest as a [[Finite State Machine]], and retries after a timeout should follow [[Exponential Backoff]] rather than hammering a device that is still busy.

**Neighbors** — *what lives nearby*
A HAL is [[Ports and Adapters]] for hardware, and depending on it through an interface is the same [[Dependency Injection]] that makes server code testable.

**Clash** — *what pushes against this*
Layers cost cycles and bytes, so on tiny parts or timing-critical paths, engineers often bypass the HAL and write registers directly, accepting less portability for exact control.
