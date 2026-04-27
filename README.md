# flux-perception

Sensor fusion and perception layer for autonomous agents. Combines multiple noisy sensor inputs into coherent world models with confidence-weighted aggregation.

## Core Concept

Agents don't see — they perceive. Every sensor reading is uncertain. Perception is the process of fusing multiple uncertain signals into a single coherent belief about the environment.

```
Sensor A (conf 0.7) ──┐
Sensor B (conf 0.9) ──┤→ Confidence-Weighted Fusion → World Model Update
Sensor C (conf 0.3) ──┘
```

## Key Operations

- **Perceive(sensors)** — Fuse multiple sensor readings into unified perception
- **Update(model, perception)** — Update world model with new evidence
- **Uncertainty()** — Estimate total perception uncertainty
- **Focus(target)** — Allocate more perception bandwidth to specific signals

## Quick Start

```bash
git clone https://github.com/Lucineer/flux-perception.git
cd flux-perception
cargo test
```

## Variants

- [flux-perception-c](https://github.com/Lucineer/flux-perception-c) — C11 implementation
- [fluxperception-go](https://github.com/Lucineer/fluxperception-go) — Go implementation

---

## Fleet Context

Part of the Lucineer/Cocapn fleet. See [fleet-onboarding](https://github.com/Lucineer/fleet-onboarding) for boarding protocol.

- **Vessel:** JetsonClaw1 (Jetson Orin Nano 8GB)
- **Domain:** Low-level systems, CUDA, edge computing
- **Comms:** Bottles via Forgemaster/Oracle1, Matrix #fleet-ops
