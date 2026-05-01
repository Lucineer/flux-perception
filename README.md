# flux-perception 👁️

**Sensor fusion engine for autonomous agents.** Confidence-weighted blending of multiple noisy sensor streams into coherent world models.

```rust
use flux_perception::Engine;

let mut e = Engine::new(0.3);  // minimum confidence threshold
e.add_sensor(1, 0.5, 0.0);    // id=1, weight=0.5, bias=0.0
e.add_sensor(2, 0.3, 0.0);

e.update(1, 48.5, 0.95, now);   // high confidence reading
e.update(2, 52.0, 0.60, now);   // lower confidence

let fused = e.read();
println!("Fused: {:.2} (conf: {:.2}, var: {:.2}, sources: {})",
         fused.value, fused.confidence, fused.variance, fused.source_count);
```

## API

```rust
let mut e = Engine::new(0.2);  // lower threshold = more sensors accepted

// Register sensors
e.add_sensor(1, 0.5, 0.0);   // id, blend weight, calibration bias

// Feed readings
e.update(1, 48.5, 0.95, now);

// Read fused perception
let fs: FusedSignal = e.read();
// fs.value          — weighted blend
// fs.confidence     — agreement-weighted certainty
// fs.variance       — disagreement signal
// fs.source_count   — active sensors contributing

// History
let last_10 = e.history(10);

// Sensor management
let s = e.find_sensor(1);
e.deactivate(1);
e.calibrate(1, 0.5);   // adjust bias

// Agreement
println!("Sensor agreement: {:.2}", e.agreement());
```

### Fusion Algorithm

1. Filter sensors below confidence threshold
2. Weight each by `weight × confidence`, bias-correct
3. Fused value = normalized weighted sum
4. Fused confidence = mean × agreement ratio
5. Variance = RMS disagreement (high = conflicting)

## Cargo.toml

```toml
[dependencies]
flux-perception = { git = "https://github.com/Lucineer/flux-perception" }
```

## Fleet Context

Part of the Lucineer/Cocapn fleet. Pairs with [flux-confidence](https://github.com/Lucineer/flux-confidence) (belief calibration). Also available in [C11](https://github.com/Lucineer/flux-perception-c) and [Go](https://github.com/Lucineer/fluxperception-go).
