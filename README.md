# C++midterm
# Orbital Starfield — A Gravitational Particle System

> 100 twinkling polygon stars orbiting an interactive gravity well. Drag the attractor with sliders, watch the orbits warp.

A 3D particle system built in **openFrameworks (C++)** for *Nature of Code — Chapter 6: Particle Systems* (Spring 2026).
---

## 📖 About

The sketch simulates a tiny solar system. A single `Attractor` sits at the center of the world, pulling on every particle through an inverse-square gravitational law (F = G · m₁ · m₂ / d²). 100 particles — a mix of `CircleParticle`s and `OctagonParticle`s — are emitted along polar orbits, each starting at its own radius and angle.

Every particle twinkles on its own rhythm: a per-particle `twinkleSpeed` and `twinklePhase` modulate its brightness so the field breathes rather than blinks. The background never fully clears — instead, a translucent black rectangle is drawn every frame, leaving a short trail that traces each star's path through space.

The attractor isn't fixed. Two GUI sliders (`Move X`, `Move Y`) push its target position, and the attractor *eases* toward that target, so when you slide, the whole orbital field bends and follows like it's being tugged by an unseen hand.

---

## 🛠️ Built With

- **Language:** C++23
- **Framework:** openFrameworks v0.12.1
- **Addons:** `ofxGui`, `ofxOpenCv`
- **Platform:** macOS 11.5+ (Xcode project included)

---

## ▶️ How to Run

1. Install openFrameworks v0.12.1 for macOS.
2. Clone this repo into `of_v0.12.1_osx_release/apps/myApps/`.
3. Open `S26_NOC_06_ParticleSystems_P2.xcodeproj` in Xcode.
4. Build & Run (⌘R).

---

## 🎮 Controls

| Input                 | Action                                |
| --------------------- | ------------------------------------- |
| `SPACE`               | Reset all particles                   |
| `R`                   | Reset camera                          |
| `F`                   | Toggle fullscreen                     |
| `H`                   | Hide / show GUI                       |
| Mouse drag            | Orbit the 3D camera                   |
| **Background Alpha**  | Trail length (low = long, high = crisp) |
| **Particle Mass**     | Heavier particles → stronger pull     |
| **Move X / Move Y**   | Drag the attractor across the field   |

---

## 🧠 How It Works

**Polar positioning.** Each particle stores its position in polar coordinates (radius `r`, angle `θ`) and converts to Cartesian each frame. This makes spawning along clean orbits trivial.

**Gravitational pull.** `Attractor::attract()` returns a 3D force pointing from the particle toward the attractor, scaled by `G · m_attractor · m_particle / d²`. Distance is clamped between 5 and 25 units so particles near the center don't get flung infinitely fast.

**Smooth following.** Instead of teleporting the attractor when sliders change, `Attractor::updatePosition()` adds an easing-scaled force toward the target — the attractor accelerates, drifts, decelerates. The whole field inherits that smoothness.

**Trails by alpha.** `ofSetBackgroundAuto(false)` keeps the framebuffer between frames. A semi-transparent black rectangle every frame creates motion blur / trails.

---

## 💡 What I Learned

- **Polar vs. Cartesian** — choosing the right coordinate system. Circular motion is trivial in polar coords.
- **Inverse-square forces** with distance clamping to avoid numerical explosions near singularities.
- **Easing** as a way to make UI feel alive — sliders that pull rather than teleport.
- **Trails through framebuffer persistence** rather than storing past positions.
- **Inheritance for shape variation** — one `Particle` base, multiple polygon subclasses, parallel vectors per type.

---

## 🙏 Credits

Starter scaffold (`Particle`, `Emitter`, `Attractor` skeleton) provided by **Luisa Pinzon** for *Nature of Code S26*. Visual design, GUI integration, 3D camera, twinkle behavior, and trail handling are mine.

---

*Built by Aeon · Spring 2026*
