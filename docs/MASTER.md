# MASTER — Heartbeat In The Rubble

Detailed spec of the current project. Consolidated read, **not an authority**: loses to
`docs/decisions/`, wins on numbers. Every number in the project lives here.

Status markers — **FIXED** settled · **PENDING** needs a measurement or a decision before
anything downstream is trustworthy · **TARGET** design goal, not yet met.

Last revised: **2026-10-06** · Stage: pre-code, no hardware acquired.

> **Budget rehauled 2026-10-06** — §9 replaced, §2/§8 contradiction found, §4.1 and §10.4
> challenged. Full working: **`docs/research/BUDGET/`**. Sensor selection: **`docs/research/MEMS/`**.

---

## 1. What it is

Drone-deployed MEMS seismic mesh that locates buried survivors by their heartbeat.

A heartbeat is a mechanical event — each contraction couples a pressure wave into the
body, the ground, and surrounding material. A sensitive accelerometer reads that wave
through concrete whether or not the survivor is conscious, visible, or making noise. That
is the gap: thermal is surface-only (10–15 cm of concrete blocks it), acoustic needs a
conscious victim who can knock or shout, manual search covers 50–100 m²/h against a 72 h
survival window.

**Signal chain:** MEMS node → LoRa mesh → drone gateway → bandpass + FFT → LSTM classifier
→ TDoA solve → map pin.

## 2. System architecture

| Layer | Element | Role |
| --- | --- | --- |
| Sense | ADXL355 + MCU node, dropped in a grid | capture ground vibration continuously |
| Link | SX1276 LoRa mesh, drone as elevated gateway | relay node data out of the rubble |
| Compute | Raspberry Pi 4 ground station | filter, classify, triangulate |
| Deploy | ~~DJI Mini 3 class drone, servo release~~ **⛔ INVALID — see §8.6.** F450 + Pixhawk 6C | place nodes without putting people on rubble |
| Present | Flask + Leaflet + WebSocket dashboard | live map pin per detected survivor |

Mesh is self-healing (Meshtastic or custom AODV): a destroyed node reroutes, no single
point of failure. The drone's elevation is what makes the gateway link work.

## 3. Sensing

### 3.1 Target band

| Source | Frequency | Amplitude | Action |
| --- | --- | --- | --- |
| Heartbeat, adult | 1.0–2.0 Hz (60–120 bpm) | 0.1–1 mg | **target** |
| Heartbeat, hypothermic/injured | 0.67–1.0 Hz (40–60 bpm) | lower | target; filter low end drops to 0.3 Hz |
| Respiration | 0.2–0.5 Hz | 0.05–0.5 mg | secondary confirmation |
| Wind | < 0.1 Hz | variable | low-cut |
| Footsteps | 1–3 Hz | 5–50 mg | in-band — rejected on amplitude |
| Aftershock | 5–50 Hz | 10–1000 mg | high-cut |
| Machinery | 20–200 Hz | high | high-cut |

Raw rubble seismic data is ~95% noise. Everything downstream exists to pull out the 5%.

### 3.2 Sensor — FIXED

**ADXL355**, 3-axis, 25 µg/√Hz noise floor, ±2 g, ~$15.

Rejected: MPU-6050 (400 µg/√Hz — 16× noisier, $3); SM-24 geophone (0.1 µg/√Hz but a 10 Hz
corner frequency, which sits above the entire target band — unusable here regardless of
its noise spec).

### 3.3 Detection range — PENDING

Working assumption: **0.1–1 mg at 2–3 m through concrete**, > 20 dB SNR after filtering.

This is the load-bearing number of the whole project. Node spacing, node count, coverage,
deploy time and total cost are all derived from it. It is inherited from the reference doc
and has not been measured. See §10.1.

## 4. Node

| Property | Value |
| --- | --- |
| Form factor | ~4 cm dia × 1.5 cm, ~8 g assembled |
| Sensor | ADXL355 |
| MCU | ESP32 or STM32 — **PENDING**, see §10.3 |
| Radio | SX1276, 865–867 MHz |
| Power | CR2032, 225 mAh |
| Orientation | 3 g tungsten base at sensor end + aerodynamic fin → lands sensor-down |
| Impact tolerance | foam shell absorbs 15–20 G |
| Sampling | 100 Hz, 60 s analysis window |
| Wake | free-fall then impact detected → sensing starts after landing |

### 4.1 Power budget — FIXED at 25 h

| Draw | Current |
| --- | --- |
| ADXL355, full operation | 200 µA |
| ESP32, light sleep | 800 µA |
| SX1276, 40 mA for 100 ms every 500 ms | 8 mA average |
| **Total** | **~9 mA** |

225 mAh ÷ 9 mA = **25 h continuous**.

> ⚠️ **CONTESTED 2026-10-06 — this budget contradicts §5 and needs rebuilding, not repricing.**
> The 8 mA LoRa average assumes **40 mA for 100 ms every 500 ms = a 20 % duty cycle**.
> **§5 states the band limit is ~1 %** — this breaches it by **20×**. Independently, a 225 mAh
> CR2032 has too high an internal resistance to source 40 mA TX pulses without severe voltage
> droop, and the LoRaWAN energy literature puts a 2400 mAh node at ~1 year for **one message per
> 5 minutes** against the ~2/s assumed here.
> **25 h is not a trustworthy number.** See `research/BUDGET/01-literature.md` C4 and `04` D15.

The 48–72 h figure in the reference doc double-counts duty-cycling — the 8 mA LoRa average
already assumes it. **25 h is the number.** Reaching the 72 h survival window needs a
larger cell, event-only transmission, or a deeper sleep schedule; that choice is coupled to
the radio budget in §10.2.

## 5. Radio

| Parameter | Value |
| --- | --- |
| Band | 865–867 MHz (India, licence-free) |
| Module | SX1276 |
| Modulation | Chirp Spread Spectrum |
| Range, line of sight | 2–15 km |
| Range, through rubble | 200–500 m |
| Rate | 250 bps (SF12) – 50 kbps (SF7) |
| Draw | 10–40 mA TX, 1–2 mA RX |
| Duty-cycle limit | ~1% |

**Packet, 15 B:** node ID 2 B · timestamp 4 B · accel X/Y/Z 2 B each · RSSI 1 B · CRC 2 B.

### 5.1 Throughput — PENDING

Continuous raw streaming does not fit. 15 B × 2 packets/s × 20 nodes = 600 B/s =
**4800 bps**: ~19× over SF12, at SF7's ceiling, and in breach of the 1% duty-cycle limit.

The architecture must change, not the arithmetic. See §10.2.

## 6. Signal processing

| Stage | Spec |
| --- | --- |
| 1. Bandpass | 4th-order Butterworth, 0.5–4 Hz (0.3 Hz low end for hypothermic) |
| 2. FFT | 60 s window at 100 Hz → 0.017 Hz resolution ≈ 1 bpm discrimination |
| 3. Classify | LSTM 64 (return sequences) → LSTM 32 → Dense 16 ReLU → sigmoid |
| 4. Threshold | > 0.75 = human confirmed; tuned for low false-negative rate |
| 5. Separate | ICA for overlapping sources |

**Human vs machine discriminator:** heart-rate variability. A human beat-to-beat interval
varies ±5–10%; a pump or motor at a nominal 1 Hz has effectively zero variance. Amplitude
is the second axis — machinery runs > 10 mg against a 0.1–1 mg heartbeat.

**Multi-survivor:** ICA separates up to N−1 sources with N nodes; separation degrades past
roughly 5 overlapping survivors.

**Training data:** PhysioNet MIT-BIH cardiac waveforms + USGS seismic noise profiles +
synthetic rubble noise from aftershock seismograms.

**Accuracy — TARGET:** > 93% at > 1 m, > 87% at 0.5 m. Inherited claim, no measurement
behind it. Treat as the goal to beat, not a property of the system.

## 7. Localization

### 7.1 Method

TDoA across 3+ nodes that independently confirm a human signal.

1. Δt₁₂ = t₁ − t₂ for each node pair.
2. Δd₁₂ = v · Δt₁₂.
3. Each pair defines one hyperbola: √((x−x₁)²+(y−y₁)²) − √((x−x₂)²+(y−y₂)²) = Δd₁₂.
4. Solve the system for (x, y).

**Wave velocity:** ~3000 m/s P-wave in solid concrete; ~1500 m/s water-saturated debris —
the solver takes velocity as a calibrated parameter, not a constant. Real rubble is
heterogeneous with air gaps, so propagation is slower and scattered; this is the dominant
physical error term and is not yet modelled.

**Depth (Z):** amplitude attenuation A = A₀·e^(−αr) solved for r, or a 3D solve using the
elevated drone as the out-of-plane reference. **±0.5 m** — enough to brief a drill
direction, not to place one.

### 7.2 Accuracy — PENDING

Reference table, at 10 m spacing:

| Nodes | Accuracy | Coverage | Deploy time |
| --- | --- | --- | --- |
| 3 | ±1–2 m | ~75 m² | ~2 min |
| 5 | ±0.3–0.5 m | ~150 m² | ~3 min |
| 9 | ±0.1–0.2 m | ~400 m² | ~5 min |
| 16 | ±0.05 m | ~900 m² | ~8 min |

Two constraints invalidate the lower rows as written:

- **Timing floor.** At 3000 m/s, the assumed 0.1 ms timestamp precision resolves to
  0.1 ms × 3000 m/s = **±0.3 m**. The ±0.1 m and ±0.05 m rows are below the system's own
  time resolution. ±0.1 m requires ~33 µs sync across independent battery-powered nodes.
- **Spacing vs range.** Spacing comes from d = √(2·r²) = r·√2. At the assumed r = 3 m that
  is **4.2 m**, not the 10–15 m used to compute the coverage column. At 10 m spacing a
  survivor can sit outside every node's range, and TDoA needs three nodes to hear them.

The table is rebuilt once §10.1 gives a measured r and §10.4 gives a sync mechanism.

## 8. Deployment

### 8.1 Why drone

Manual placement puts rescuers on unstable rubble, one sensor at a time, 45–60 min for an
area the drone covers in 5. It also reaches collapsed multi-storey and fire zones people
cannot enter, and gives an aerial view for placement in real time.

### 8.2 Flight

- Snake-pattern grid, 4–5 m altitude, 3 m/s, servo release every 10–15 m (**PENDING** on
  §10.1 — likely tightens to ~4 m).
- PID pitch/roll at 400–1000 Hz to counter micro wind tunnels and fire updrafts.
- Barometer + IMU fusion for altitude hold; bottom-facing optical flow for GPS-denied hover.

### 8.3 Drop mechanics

Drop height 3–4 m → ~7.7 m/s at impact → F = m·v²/(2·compression) ≈ **15–20 G**, inside
foam tolerance. Low centre of gravity plus fin gives shuttlecock-style self-righting.

### 8.4 Payload

| Parameter | No payload | 9 nodes (72 g) |
| --- | --- | --- |
| Weight | ~800 g | ~872 g |
| Hover thrust | ~8 N | ~8.7 N |
| Flight time | ~28 min | ~25 min |
| Battery drain | baseline | +8–10% |
| Motor RPM | baseline | +3–4% |

72 g is negligible for a mid-range airframe. No heavy-lift drone required.

### 8.6 ⛔ The specified airframe cannot perform §8.2 — NEW 2026-10-06

§2 specifies a **DJI Mini 3 class drone with servo release**; §8.2 specifies an **autonomous
snake-grid with servo release every 10–15 m**. **These are mutually exclusive.**

From **DJI's own Product SDK Compatibility table** (verified live, read directly):

> **DJI Mini 3 / Mini 3 Pro — Mobile SDK: Yes · Payload SDK: — · Onboard SDK: —**

**Payload SDK exists only on Enterprise airframes** (Matrice 350/400/4-series, FlyCart). The Mini 3
exposes **no PWM output and no payload-control path**. Third-party drop kits work by hijacking the
**landing-light channel** or carrying their **own RC receiver** — meaning **a human triggers every
single release**. Autonomous grid deployment is not achievable on this airframe at any price.

| Path | Build | Cost | Autonomous drop? |
|---|---|---|---|
| A | DJI Mini 3 + STARTRC drop kit | $657.99 | ❌ **No** |
| **B** | **F450 kit + Pixhawk 6C + servo** | **$738.99** | ✅ **Yes** (AUX PWM via MAVLink) |
| C | DJI Matrice (Payload SDK) | $10,000–20,000 | ✅ Yes — out of scope |

**→ Path B.** 8 % over §9's old ceiling, and the only option that delivers what §8.2 already
specifies. Full costing: `research/BUDGET/03-budget.md` §3.

### 8.5 Node position

Node position = drone GPS at moment of release + drift correction from barometer and
ground speed. GPS-denied fallback is UWB inter-node ranging — TDoA needs only relative
coordinates, not absolute fixes.

## 9. Bill of materials — REBUILT 2026-10-06

All prices pulled from vendor payloads **2026-10-06**. Working and provenance:
`research/BUDGET/02-vendor-register.md` and `03-budget.md`.
**[LIVE]** = vendor's own price field · **[EST]** = my estimate · **[UNVERIF]** = single-source.

**Per node — $67.75** (was claimed $29; **understated 2.3×**)

| Item | Part | Cost | Src |
| --- | --- | --- | --- |
| Sensor | ADXL355 (LCSC) | **$55.1592** | [LIVE] |
| **MCU + radio** | **RAK3172 — STM32WLE5 = Cortex-M4 + SX126x in one module** | **$5.99** | [LIVE] |
| Antenna | u.FL 868 MHz whip | $1.50 | [EST] |
| Cell | CR2032 225 mAh + holder — **see §4.1 warning** | $0.60 | [EST] |
| Case | PLA print + EVA foam | $1.20 | [EST] |
| PCB | JLCPCB 4-layer, qty 10, amortised | $1.80 | [EST] |
| Passives / connector | | $1.50 | [EST] |

**The RAK3172 replaces two line items with one cheaper part**, saving $3.01/node and removing the
MCU↔radio SPI link — one fewer joint to survive a 15–20 G impact.

**System — $1,845** (was claimed $641–1141; **understated 2.2–2.3×**)

| Item | Cost |
| --- | --- |
| 9 nodes | $609.74 |
| **+2 spare nodes (20 % drop attrition)** | **$135.50** |
| Ground station — Pi 5 8 GB $80.00 + **GPS FeatherWing $24.95** + misc $15 | $119.95 |
| Drone — **Path B: F450 + Pixhawk 6C** (§8.6) | $738.99 |
| Dashboard — Flask + Leaflet | $0 |
| **Subtotal** | **$1,604.18** |
| Contingency 15 % | $240.63 |
| **TOTAL** | **$1,844.81 ≈ ₹1,55,000** |

**What the old §9 missed** — four whole categories, not four bad numbers:
**(1)** spares, for sensors *thrown onto rubble*; **(2)** the **GPS 1PPS time reference** §10.4
requires; **(3)** a **PCB** to mount the parts on; **(4)** an airframe that can actually perform
§8.2.

**The Delsar argument survives intact.** Incumbent ~$15,000, hand-placed one point at a time, blind
to unconscious victims. **At $1,845 the order-of-magnitude advantage holds with 10× margin** — the
old conclusion was right even though its arithmetic was not.

**Cheapest real saving:** switch the sensor to **Murata SCA3300-D01** (−$145.61 across 9 nodes),
**gated on the §10.1 ambient measurement** and on confirming its price ([UNVERIF] — DigiKey 403s).
**Do not buy the drone first:** build order §12 steps 1–5 need no airframe, so **$739 is deferrable**
past the measurement that may change the architecture.

## 10. Unresolved

Blocking, in order. Nothing here is decided; no ADRs written yet.

**10.1 Detection range.** Does an ADXL355 resolve a heartbeat through rubble at 3 m, or at
0.5 m? Spacing, node count, coverage, deploy time and cost all derive from it. Bench-
answerable before any drone exists: sensor, still subject, concrete slab, FFT, vary
distance and slab thickness. **Everything else waits on this.**

**10.2 Radio budget.** 4800 bps does not fit the link. Candidate directions: on-node
detection with event-only transmission (cheap on radio and power, but removes the raw
waveforms TDoA needs — likely forces on-node timestamping of detected beats instead);
lower packet rate; or a different link layer. Couples directly to §4.1 power.

**10.3 MCU.** ESP32 or STM32 — unpicked. Decided by the §10.2 outcome: on-node inference
needs the headroom, dumb relay does not.

**10.4 Time sync.** ~~Hardest open problem here.~~ **✅ LARGELY ANSWERED 2026-10-06 — downgrade.**
**LongShoT** (CMU/NSF, PDF read) achieves **<2 µs average sync error**, <0.1 ppm drift, across
devices **within 4 km**, on **COTS hardware** against a GPS 1PPS reference — ~10× better than the
"tens of µs" this section asks for. Position error from 2 µs is **0.3 mm at 150 m/s** and **6 mm at
3000 m/s**: **negligible at every plausible velocity.**
**Cost: one GPS module ($24.95), now a line in §9.** Caveat: LoRa's timestamp quantum is 1 µs, so
2 µs is near the hardware floor; sub-µs needs oversampling or the 2.4 GHz SX1280 path.
**The binding constraint on localization is §10.5 (velocity), not clock error.**
See `research/BUDGET/01-literature.md` C3.

**10.5 Propagation model.** 3000 m/s is solid concrete. Rubble is not. The solver needs a
velocity model or an in-field calibration procedure.
**↑ PROMOTED 2026-10-06 — this is now the binding unknown for localization**, having overtaken
§10.4. Published brackets: PigV² measured **100–200 m/s** through a floor; **USGS SIR 2023-5061**
gives unconsolidated material **200–1000 m/s** dry / 1500–2300 m/s saturated; intact concrete
~3600 m/s. Rubble is porous granular material — low effective elastic modulus, hence low P-wave
speed. **Defensible bracket 150–1000 m/s, so §7.1's 3000 m/s is likely 3–20× too high**, which
propagates into §8.2 node spacing and every TDoA distance.
Resolvable by a hammer travel-time test across a known baseline on debris.

## 11. Known limits

| Limit | Mitigation |
| --- | --- |
| Burial > 4 m | more nodes, geophone-grade sensor, or pair with VOC detection |
| Machinery running nearby | adaptive threshold + notch filter at machine frequency |
| > 5 overlapping survivors | ICA degrades; more nodes |
| GPS-denied dense rubble | UWB relative positioning |
| Waterlogged debris | recalibrate velocity to ~1500 m/s |
| Core temp < 35 °C | heart rate to 40 bpm; filter low end to 0.3 Hz |
| Depth vs lateral accuracy | ±0.5 m vs ±0.3 m; Z used for drill direction only |

## 12. Build order

1. **Bench detection** — ADXL355 + dev board, Python capture, bandpass + FFT. Answer §10.1.
2. **Pipeline on synthetic data** — filter, FFT, LSTM, against generated signal + noise.
3. **Two-node TDoA** — with a real sync mechanism. Answer §10.4.
4. **Mesh** — n-node link with the §10.2 architecture settled.
5. **Node hardware** — case, drop-test, power validation.
6. **Drone integration** — release mechanism, grid autonomy, GPS tagging.
7. **Dashboard** — live map, end to end.
