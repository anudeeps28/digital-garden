---
type: atomic
tags: [coding/embedded, devops]
date: 2026-10-04
---

# Cross-Compilation

## Idea
You build the program on one machine (the host) for a different machine (the target), because the target is too small, too slow or simply a different CPU. Every firmware image for a microcontroller is built this way.

## Definition
A **cross-compiler** runs on the host, say an x86 or Apple Silicon laptop, and emits machine code for the target, say an ARM Cortex-M chip. The toolchain is named after the target triple, for example `arm-none-eabi-gcc`: ARM architecture, no operating system ("bare metal"), embedded ABI. A typical build has three parts. A **Makefile** or CMake file drives the compiler with target flags (`-mcpu=cortex-m4 -mthumb`). A **linker script** describes the chip's memory map and tells the linker where to place things: code and constants into flash, initialised data copied from flash to RAM at startup, zeroed `.bss` and the stack in RAM. A **startup file** sets up the vector table and runs that copy before `main`. The output is an ELF file for debugging and a raw `.bin` or `.hex` image that a programmer writes into flash. Because the host cannot run the result natively, testing leans on emulators, hardware-in-the-loop rigs, or compiling the hardware-independent logic a second time for the host so it can be unit tested there.

## Tools
- **GNU Arm Embedded Toolchain** — `arm-none-eabi-gcc`, the common free choice for Cortex-M.
- **Clang/LLVM** — one compiler binary that targets many architectures via `--target`.
- **Vendor IDEs** — bundle a cross-toolchain, linker scripts and flashing tools for their chips.

## Source
The term comes from compiler practice; GCC formalised the build/host/target triple in its configure system (late 1980s onward). I could not find a single originator of cross-compilation itself, which predates GCC.

---

## Compass

**Roots** — *where this comes from*
The linker script is where [[Memory-Mapped IO]] meets the build: the same memory map that places peripherals also decides where your code lives.

**Paths** — *where this leads*
The flashed image is a [[Build Artifacts|build artifact]] like any other and belongs in a [[CI-CD Pipeline]], built once and versioned.

**Neighbors** — *what lives nearby*
A multi-architecture [[Docker Image]] build is the same problem in the server world: compile on one CPU, run on another.

**Clash** — *what pushes against this*
Code that passed tests on the host can still fail on the target because of [[Endianness]], word size, alignment or timing, so host tests reduce but never replace on-device testing.
