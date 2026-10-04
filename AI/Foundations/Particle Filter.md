---
type: atomic
tags: [ai/robotics, ai]
date: 2026-10-04
---

# Particle Filter

## Idea
When you do not know where a robot is, keep many guesses at once, move them all as the robot moves, and keep the ones that best explain what the sensors see. The cloud of surviving guesses is the robot's belief about its position.

## Definition
A **particle filter** represents a probability distribution with a set of samples, called **particles**, each a hypothesis with a **weight**. In **Monte Carlo Localization (MCL)** each particle is a candidate pose (x, y, heading) on a known map, and every cycle has three steps. **Predict**: move every particle according to the wheel odometry, adding noise to reflect how unreliable odometry is. **Weight**: compare what each particle *would* see from its pose (expected laser ranges against the map) with what the sensor actually measured, and give closer matches higher weight. **Resample**: draw a new set of particles in proportion to weight, so good hypotheses multiply and bad ones die out. Started with particles spread over the whole map, the cloud collapses onto the true pose after the robot has moved and seen distinctive features. **AMCL** (adaptive MCL) varies the number of particles using KLD sampling: many while uncertain, few once the cloud is tight. Unlike a Kalman filter, a particle filter can represent several separate hypotheses at once, such as two identical corridors.

## Source
Gordon, Salmond and Smith introduced the bootstrap particle filter in 1993. Dellaert, Fox, Burgard and Thrun applied it to robot localisation as Monte Carlo Localization (ICRA 1999); Fox's KLD-sampling (2001) is the "adaptive" part of AMCL. Thrun, Burgard and Fox's *Probabilistic Robotics* (2005) is the standard text.

---

## Compass

**Roots** — *where this comes from*
It is Bayesian reasoning done by sampling, the same idea of weighting hypotheses by evidence that sits behind a [[Confidence Score]].

**Paths** — *where this leads*
A localised pose is the starting point that [[A-Star Search]] plans from and that a [[PID Controller]] uses to measure its error from the path.

**Neighbors** — *what lives nearby*
Resampling weighted candidates resembles [[Semantic Re-ranking]], where many rough guesses are scored again by a better judge and only the best are kept.

**Clash** — *what pushes against this*
Cost grows with the number of particles and, badly, with the number of dimensions, and if every particle drifts away from the truth the filter cannot recover without deliberately injecting random particles.
