# MASTER — Consolidated Spec

Consolidated read. **Not an authority.** Loses to `docs/decisions/`, wins on numbers.
Source: `docs/reference/Heartbeat_In_The_Rubble.md` (old doc). Numbers below are carried
forward or corrected; every correction is marked.

Legend — `[DOC]` as written in the source · `[CALC]` derived here · `[CONFLICT]` source
contradicts itself or physics · `[UNVERIFIED]` claimed without a checkable source.

---

## 1. Concept

Heartbeat is a mechanical event. Each contraction couples a pressure wave into the body,
the ground, and surrounding material. A sensitive enough accelerometer reads it through
concrete regardless of consciousness, visibility, or noise — which is exactly where
thermal (surface-only), acoustic (needs a conscious victim), and manual search (too slow)
all fail.

Chain: **MEMS node → LoRa mesh → drone gateway → bandpass + FFT → LSTM → TDoA → map pin.**

## 2. Signal budget

| Quantity | Value | Note |
| --- | --- | --- |
| Heartbeat band | 1.0–2.0 Hz (60–120 bpm) | `[DOC]` |
| Hypothermic / injured | 0.67–1.0 Hz (40–60 bpm) | extend filter low end to 0.3 Hz |
| Heartbeat amplitude | 0.1–1 mg at 2–3 m through concrete | `[DOC]` — **the load-bearing assumption** |
| Respiration | 0.2–0.5 Hz, 0.05–0.5 mg | secondary confirm |
| Aftershock | 5–50 Hz, 10–1000 mg | high-cut rejects |
| Machinery | 20–200 Hz, high | high-cut rejects |
| Footsteps | 1–3 Hz, 5–50 mg | in-band; amplitude threshold rejects |
| Wind | < 0.1 Hz | low-cut rejects |

## 3. Sensor

| Part | Noise floor | Range | Cost | Verdict |
| --- | --- | --- | --- | --- |
| **ADXL355** | 25 µg/√Hz | ±2 g | $15 | selected |
| MPU-6050 | 400 µg/√Hz | ±2 g | $3 | 16× noisier — rejected |
| SM-24 geophone | < 0.1 µg/√Hz | 10 Hz+ | $25 | **unusable**: 10 Hz corner sits above the 1–2 Hz target band |

Claimed SNR: > 20 dB for a 0.1 mg signal at 2 m through concrete after filtering `[DOC]`.

## 4. Node

- Form: ~4 cm dia × 1.5 cm, ~8 g with casing and cell.
- Orientation: 3 g tungsten base at the sensor end + aerodynamic fin → lands sensor-down.
- Impact: foam shell absorbs 15–20 G.
- BOM/node `[DOC]`: ADXL355 $15 + ESP32/STM32 $4 + SX1276 $5 + cell $2 + printed case $3 = **$29**.
- Current budget `[DOC]`: ADXL355 200 µA + ESP32 light-sleep 800 µA + SX1276 8 mA avg = **~9 mA**.
- Life `[CALC]`: CR2032 225 mAh ÷ 9 mA = **25 h**.
  `[CONFLICT]` Source claims 48–72 h "with duty-cycling" — but the 8 mA LoRa figure
  already assumes duty-cycling (40 mA for 100 ms every 500 ms). Double-counted.
  **25 h is the defensible number.** 72 h needs a larger cell or a real sleep schedule.

## 5. Radio

| Parameter | Value |
| --- | --- |
| Band (India) | 865–867 MHz, licence-free |
| Module | SX1276 |
| Range, line of sight | 2–15 km |
| Range, through rubble | 200–500 m |
| Rate | 250 bps (SF12) – 50 kbps (SF7) |
| Draw | 10–40 mA TX, 1–2 mA RX |

Packet, 15 B total: node ID 2 B, timestamp 4 B, accel X/Y/Z 2 B each, RSSI 1 B, CRC 2 B.

`[CONFLICT]` Source: 15 B × 2/s × 20 nodes = 600 B/s, "well within LoRa bandwidth at any
spreading factor." **False.** 600 B/s = **4800 bps** — ~19× over SF12's 250 bps, and near
SF7's ceiling. The 865–867 MHz band also carries a ~1% duty-cycle limit that continuous
2 Hz transmission violates. Unresolved; see Open Questions.

Mesh: Meshtastic or custom AODV, self-healing, drone as elevated gateway. No single point
of failure — losing a node reroutes.

## 6. Processing

1. **Bandpass** — 4th-order Butterworth, 0.5–4 Hz.
2. **FFT** — 60 s window at 100 Hz sampling → 0.017 Hz resolution ≈ 1 bpm discrimination.
3. **LSTM** — 64 units (return sequences) → 32 → Dense 16 ReLU → sigmoid. Threshold **0.75**.
4. **Discriminator** — HRV. Humans vary ±5–10% beat to beat; machines have zero variance.
   Amplitude separates too: machinery > 10 mg vs heartbeat 0.1–1 mg.
5. **Multi-survivor** — ICA, up to N−1 sources with N nodes; degrades past ~5 survivors.

Training: PhysioNet MIT-BIH + USGS seismic noise + synthetic rubble noise.
`[UNVERIFIED]` Claimed > 93% accuracy at > 1 m, > 87% at 0.5 m — no measurement behind it.

## 7. Localization

- P-wave velocity: **~3000 m/s** in solid concrete; ~1500 m/s water-saturated.
  Real rubble is heterogeneous with air gaps — velocity is lower and scattered. TDoA
  assumes a homogeneous medium; this is a larger error source than the source doc admits.
- Method: Δt between node pairs → Δd = v·Δt → one hyperbola per pair → solve for (x, y).
- Depth: amplitude attenuation A = A₀·e^(−αr), or 3D solve using the elevated drone. ±0.5 m.

| Nodes | Claimed accuracy | Coverage @ 10 m spacing | Deploy time |
| --- | --- | --- | --- |
| 3 | ±1–2 m | ~75 m² | ~2 min |
| 5 | ±0.3–0.5 m | ~150 m² | ~3 min |
| 9 | ±0.1–0.2 m | ~400 m² | ~5 min |
| 16 | ±0.05 m | ~900 m² | ~8 min |

`[CONFLICT]` **Timing floor.** At 3000 m/s the stated 0.1 ms timestamp precision gives
0.1 ms × 3000 m/s = **±0.3 m**. The ±0.1 m and ±0.05 m rows sit below the hardware's own
resolution. ±0.1 m needs ~33 µs sync across independent battery nodes — not addressed
anywhere in the source, and the hardest open problem in the design.

`[CONFLICT]` **Spacing vs range.** Sensing is specified at 2–3 m. Spacing is specified at
10–15 m from `d = √(2·r²)`, which is r·√2 — for r = 3 m that yields **4.2 m**, not 10–15 m.
At 10 m spacing a survivor sits outside every node's stated range, and TDoA needs three
nodes to hear them, not one. Either range is much larger than 3 m, or the grid tightens to
~4 m — which multiplies node count, cost, and deploy time.

## 8. Drone

| Parameter | No payload | 9 nodes (72 g) |
| --- | --- | --- |
| Weight | ~800 g (DJI Mini class) | ~872 g |
| Hover thrust | ~8 N | ~8.7 N |
| Flight time | ~28 min | ~25 min |
| Battery drain | baseline | +8–10% |

- Drop from 3–4 m; ~7.7 m/s terminal; 15–20 G impact — inside foam tolerance.
- Snake grid at 4–5 m altitude, 3 m/s, servo release every 10–15 m.
- Stability: PID at 400–1000 Hz, baro + IMU fusion, optical flow for GPS-denied hover.
- Node position = drone GPS at drop + drift correction. UWB inter-node ranging is the
  GPS-denied fallback — TDoA only needs relative coordinates.

## 9. Cost

| Item | Cost |
| --- | --- |
| 9 nodes @ $29 | $261 |
| Ground station (Pi 4 + LoRa hat) | $80 |
| Drone (DJI Mini 3 / Pixhawk F450) | $300–800 |
| **Total** `[CALC]` | **$641–1141** |

`[CONFLICT]` Source states both "~$550" and "$300–500 total hardware cost". Neither adds
up. Incumbent Delsar Life Detector is ~$15,000 `[UNVERIFIED]`, so the order-of-magnitude
advantage survives even at $1141.

## 10. Known limits

| Limit | Mitigation |
| --- | --- |
| Burial > 4 m | more nodes, geophone-grade sensor, or pair with VOC detection |
| Running machinery nearby | adaptive threshold + notch at machine frequency |
| > 5 overlapping survivors | ICA separation degrades; more nodes |
| GPS-denied rubble | UWB relative positioning |
| Waterlogged debris | recalibrate TDoA velocity to ~1500 m/s |
| Core temp < 35 °C | extend filter low end to 0.3 Hz |
| Depth accuracy | ±0.5 m vs ±0.1 m lateral; used for drill direction only |

## 11. Open questions

Blocking, in order. None resolved — no ADRs written yet.

1. **Real detection range.** Does an ADXL355 read a heartbeat through rubble at 3 m, or at
   0.5 m? Every downstream number — spacing, node count, coverage, cost — rides on this.
   Answerable on a bench: sensor, a still person, a concrete slab, an FFT.
2. **Radio budget.** 4800 bps does not fit. Options: on-node detection with event-only
   transmission (kills raw-data TDoA), a lower packet rate, or a different link.
3. **Time sync.** What gets nodes within tens of µs of each other? Without it, accuracy is
   ±0.3 m at best regardless of node count.
4. **Power.** 25 h measured against a 72 h survival window.
