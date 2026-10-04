---
type: atomic
tags: [coding/embedded, coding/cpp]
date: 2026-10-04
---

# Memory-Mapped IO

## Idea
On a microcontroller, talking to hardware is just reading and writing memory. Each peripheral exposes its control and status registers at fixed addresses, and the CPU drives the hardware with ordinary loads and stores.

## Definition
In **memory-mapped IO**, the address space is shared between RAM, flash and peripherals. A timer, a UART or a GPIO port appears as a block of registers at a documented base address, and each bit or field in those registers means something physical: "enable this clock", "drive this pin high", "a byte has arrived". On an ARM Cortex-M part, for example, enabling a GPIO port means setting one bit in the clock-control (RCC) block and then writing mode bits into the GPIO block, both found in the reference manual's memory map. In C or [[CPP|C++]] you reach a register through a pointer to a fixed address marked **`volatile`**:

```c
#define GPIOA_ODR (*(volatile uint32_t *)0x40020014u)
GPIOA_ODR |= (1u << 5);   /* drive pin PA5 high */
```

`volatile` tells the compiler that this location can change on its own and that every access has side effects, so it must not cache the value in a register, merge two writes or delete a "useless" read. Setting and clearing single bits is everyday [[Bit Manipulation]]. The older alternative, **port-mapped IO**, uses a separate address space and special instructions (x86 `in`/`out`).

## Source
The approach was popularised by DEC's PDP-11 (1970), whose Unibus put device registers in the top of the normal address space so any instruction could operate on them. Today it is the standard model on ARM and most microcontrollers, documented per chip in vendor reference manuals; the semantics of `volatile` come from the C standard (C89).

---

## Compass

**Roots** — *where this comes from*
It falls out of treating the CPU as something that only knows how to move bytes around, which is why [[Endianness]] and register widths matter as soon as you touch it.

**Paths** — *where this leads*
Configuring pins through registers is the first step toward [[GPIO and Open-Drain Outputs]], and wrapping raw register pokes in named functions is how a [[Device Driver]] begins.

**Neighbors** — *what lives nearby*
Registers that hardware changes behind your back are the same reason variables shared with an [[Interrupt Service Routine]] must be `volatile`.

**Clash** — *what pushes against this*
Raw address pokes are invisible to type checkers and easy to get wrong, so most teams hide them behind a hardware abstraction layer, trading a little directness for code that reads like [[Define Contract Before Implementation|a contract]] rather than magic numbers.
