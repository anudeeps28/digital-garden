---
type: atomic
tags: [coding/embedded, ai/robotics]
date: 2026-10-04
---

# PID Controller

## Idea
A PID controller steers a system toward a target by looking at the error three ways: how big it is now, how long it has persisted, and how fast it is changing.

## Definition
The controller computes an output from the **error** e = setpoint − measurement:

```
u = Kp·e + Ki·∫e dt + Kd·de/dt
```

The **proportional** term reacts to the current error: bigger error, harder push. On its own it usually leaves a small **steady-state error**. The **integral** term adds up past error and keeps pushing until that residue is gone, but too much of it causes **overshoot** and **integral windup** when the actuator is saturated. The **derivative** term reacts to how fast the error is changing and acts as a brake, damping oscillation, though it amplifies sensor noise. **Tuning** the gains Kp, Ki and Kd trades speed against overshoot against steady-state error; methods range from hand tuning (raise Kp until it oscillates, back off, add Ki then Kd) to Ziegler–Nichols rules. In firmware it runs at a fixed rate in a timer loop, with clamped outputs and anti-windup. A common robotics use is path following: the error is the robot's sideways distance or heading offset from the planned path, and the output is the steering command.

## Source
Nicolas Minorsky published the first theoretical analysis in 1922, modelling how a helmsman steers by present error, accumulated error and rate of change while working on automatic steering for the US Navy (trials on USS New Mexico). Ziegler and Nichols published their tuning rules in 1942.

---

## Compass

**Roots** — *where this comes from*
It is the engineering form of a feedback loop, the same structure as [[The Flywheel Concept]], except here the loop is designed to settle rather than to grow.

**Paths** — *where this leads*
A path planner such as [[A-Star Search]] decides where to go, a [[Particle Filter]] estimates where the robot is, and the PID loop closes the gap between the two.

**Neighbors** — *what lives nearby*
Autoscalers and [[Backpressure]] mechanisms are proportional controllers in disguise, adjusting capacity from the error between load and target.

**Clash** — *what pushes against this*
PID knows nothing about the system it controls, so strongly nonlinear or delayed systems often need model-based control instead, and a badly tuned loop can be worse than none.
