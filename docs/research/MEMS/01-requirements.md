# 01 — Sensor Requirement, Derived From Physics and Literature

> Research date: 2026-09-17. Every number below is tagged:
> **[DS]** = read out of a datasheet PDF in `datasheets/` · **[PAPER]** = quoted from a PDF in `papers/`
> **[CALC]** = my arithmetic from tagged inputs · **[UNVERIF]** = single-source, not confirmed.
> See `05-verification-log.md` for the two audit passes behind each.

---

## 1. What the signal actually is

The project spec (`docs/MASTER.md` §3.1) assumes the heartbeat is a **1.0–2.0 Hz tone at 0.1–1 mg**,
and §6 bandpasses **0.5–4 Hz** to catch it. The two published systems that have actually recovered
heartbeats through a solid structure both contradict this.

**PigV² (arXiv 2212.03378)** — pig vital signs through a pen floor, geophone array: **[PAPER]**

> "The heartbeats are detected through peak picking over the sum of wavelet coefficients from
> **10 to 100 Hz**... The range is chosen based on the typical heartbeat-induced vibration frequency
> range (0-100 Hz) and the sensitivity range of the sensors (≥10 Hz)."

**VitalMon (ACM SenSys 2017)** — heart rate of two people in a shared bed, geophone: **[PAPER]**

> "The geophone we use, SM-24 Geophone Elements, is naturally a second-order high-pass filter and
> its natural frequency is **10 Hz**."

VitalMon still achieves **1.90 BPM mean error, 0.72 BPM median** with a sensor that is
near-blind below 10 Hz.

### The correction

A heartbeat coupled into a structure is not a sinusoid. It is an **impulse train**:

- **Energy** — each beat is a broadband mechanical transient, 0–100 Hz, usefully detectable **≥10 Hz**.
- **Rate** — 1–2 Hz is the *repetition rate of the impulses*, not a frequency present in the raw
  acceleration at useful amplitude.

You recover the rate by detecting impulses in the **10–100 Hz** band, building an **envelope**, and
finding periodicity in the envelope. You do **not** recover it by bandpassing the raw signal to
0.5–4 Hz — that filter throws away the energy and keeps the band where MEMS sensors are worst (§2).

**→ MASTER §6 (0.5–4 Hz Butterworth) discards the signal. This is the single highest-impact
finding in this research.**

---

## 2. Why 1–2 Hz is the worst possible band for a MEMS part

MEMS accelerometer noise-density specs are quoted in the **flat (white) region, above ~10 Hz**.
Below that, **1/f flicker noise** dominates and manufacturers generally do not characterise it.

Sercel, presenting their QuietSeis MEMS at **EGU 2018**: **[PAPER]**

> "MEMS accelerometers often perceived as too noisy at low frequency **because of 1/f noise** —
> True for most of the seismic MEMS on the market"

and, for their own best-in-class part:

> "**<15 ng/sqrt(Hz) above 10Hz**" · "**1/f noise at low frequency not characterized**"

So for essentially every part in `02-sensor-survey.md`, the headline noise number **is not valid at
1–2 Hz**, and the true figure there is unpublished and worse — possibly by an order of magnitude or
more. Designing the detection band at 1–2 Hz means designing into a region where you cannot even
predict your own noise floor.

Detecting ≥10 Hz is not a compromise forced by the sensors. It is where the signal energy is *and*
where the sensors are characterised. Both arguments point the same way.

### The exceptions — and what they cost

Three parts *do* characterise the low band, which means the 1–2 Hz design is not physically
impossible. It is unaffordable **in this node's power envelope**:

| Part | Low-band noise spec | Price of that spec |
|---|---|---|
| **Epson M-A370AD10** | **0.02 µG/√Hz @ 1–10 Hz**, "surpassing USGS NHNM" | **36.3 mA**, 29 g |
| Epson M-A352AD10 | 0.2 µG/√Hz @ 0.5–6 Hz | 13.2–20 mA, 25 g |
| Safran-Colibrys SI1003 | 8 µg rms **integrated 0.1–100 Hz** | 27 mA, analog |

Against a **~9 mA total node budget and an 8 g node** (MASTER §4.1), the cheapest of these draws
**1.5× the whole node's current** and the best draws **4×**.

**So the honest statement is not "1–2 Hz is impossible."** It is: *1–2 Hz requires a class of sensor
that this node cannot power or carry, and every sensor it can power is uncharacterised there.*
That holds the conclusion — design at 10–100 Hz — while being accurate about why.

It also sets a hard test: if a future node can afford 36 mA and 29 g, the M-A370 reopens the low
band. Nothing else in this survey does.

---

## 3. The ambient-noise ceiling — the finding that reframes sensor selection

Same Sercel EGU 2018 presentation, describing their own low-frequency lab measurement: **[PAPER]**

> "Noise limited by **ambient vibrations above ~2Hz**"

That measurement was taken in a **soundproof chamber, on a vibration-isolation platform, in a
peri-urban basement**. Even there, above ~2 Hz what they measured was the building and the world,
not the sensor.

**Implication for this project.** A rubble field has heavy machinery, generators, rescue crews,
wind loading on debris, and aftershocks. Site ambient in 10–100 Hz will be *orders of magnitude*
above any of these sensors' self-noise.

**Therefore sensor self-noise is almost certainly not the binding constraint, and buying a
lower-noise part buys nothing.** The binding constraints are:

1. **Ambient rejection** — array coherence, template/matched filtering, adaptive cancellation.
2. **Coupling** — how well the node mechanically mates to the rubble. Dominates sensitivity.
3. **Sensor count** — N nodes gives ~√N coherent gain against incoherent ambient; this is the
   cheapest real sensitivity available, and it is bought with *cost per node*, not noise per node.

This flips the selection rule from *"lowest noise density"* to *"self-noise comfortably under site
ambient in 10–100 Hz, at minimum cost/power/size — then spend the savings on more nodes."*

---

## 4. Noise budget **[CALC]**

In-band RMS noise from a flat noise density: `a_rms = ND × √B`

Detection band **B = 10–100 Hz → 90 Hz**, `√90 = 9.487`.

| Part | ND (10–100 Hz) | a_rms over 90 Hz | Source of ND |
|---|---|---|---|
| TDK MPU-6050 | 400 µg/√Hz | **3795 µg** (3.8 mg) | [DS] |
| ADI ADXL355 | 25 µg/√Hz | **237 µg** | [DS] |
| ST IIS2ICLX | 15 µg/√Hz | **142 µg** | [UNVERIF] |
| Safran-Colibrys SI1003 | 0.7 µg/√Hz | **6.6 µg** | [DS] |
| Epson M-A352AD10 | 0.2 µG/√Hz | **1.9 µg** | [DS] |
| Geospace SM-24 (geophone) | see §5 | **~0.032 µg** | [CALC] |

*Epson M-A370AD10 is omitted from this table on purpose:* its noise is specified over **1–10 Hz**
and its response ends at **210 Hz**, so extrapolating 0.02 µG/√Hz across 10–100 Hz would be
inventing a number. In **its own** band it gives `0.02 × √9 = 0.06 µg rms` over 1–10 Hz **[CALC]** —
which is why it is the only part that could serve the original low-band design.

Against the project's own assumed signal of **0.1–1 mg (100–1000 µg)**: the ADXL355 sits at
237 µg rms broadband — i.e. **below a 1 mg impulse but comparable to a 0.1 mg one.** That is before
any ambient noise, and before the caveat that 25 µg/√Hz is *not* the figure at 1–2 Hz.

### FFT processing gain

`G = 10·log10(B_analysis / B_bin)`. For a 60 s record: `B_bin = 1/60 = 0.0167 Hz`.
Over 90 Hz of analysis: `G = 10·log10(90 / 0.0167) = 10·log10(5400) = 37.3 dB` **[CALC]**

This gain applies to a **coherent tone**. A heartbeat impulse train is not one, so the realised gain
is lower and depends on the envelope-detection chain. Treat 37.3 dB as a ceiling, not a budget line.
MASTER §6's implied gain over 0.5–4 Hz is `10·log10(3.5/0.0167) = 23.2 dB` **[CALC]** — 14 dB worse,
in a band with no signal energy.

---

## 5. The geophone comparison **[CALC]** — the uncomfortable result

MASTER §3.2 rejects the Geospace SM-24 because of its 10 Hz corner. Given §1, that corner is no
longer a defect. So it is worth pricing its actual noise.

SM-24, from the manufacturer brochure **[DS]**: sensitivity **28.8 V/m/s**, coil resistance
**375 Ω**, `f_n` **10 Hz**, moving mass 11 g, distortion <0.1%.

Coil Johnson noise (the dominant self-noise term above resonance), T = 293 K:

```
e_n = sqrt(4kTR) = sqrt(4 · 1.381e-23 · 293 · 375) = 2.46 nV/sqrt(Hz)
```

Referred to velocity: `2.46e-9 / 28.8 = 85.5 pm/s/√Hz`
Referred to acceleration at frequency f: `a = 2πf · v`

| f | equivalent acceleration noise |
|---|---|
| 10 Hz | 0.55 ng/√Hz |
| 20 Hz | 1.10 ng/√Hz |
| 100 Hz | 5.5 ng/√Hz |

Integrated 10–100 Hz (noise rises linearly with f): **≈ 32 ng rms**.

**A US$70 passive geophone is roughly 7,400× (77 dB) quieter in-band than a US$63 ADXL355.**

**Caveats, stated honestly:**

- This is coil-resistance Johnson noise only; it ignores suspension thermal noise and is therefore
  a floor, not a measured figure.
- It is only achievable if the **preamp** is quieter than ~2.5 nV/√Hz. A worse preamp dominates.
  Real geophone channels are usually preamp-limited, not coil-limited.
- Below `f_n` = 10 Hz the response rolls off second-order, so referred-to-input noise rises steeply.
  Under §1 that band is not needed — but if §1 is ever overturned, the geophone dies with it.
- It is **1-axis** and has **11 g of moving mass**, a real problem for a drone-dropped node
  (orientation-dependent, and the mass *is* the sensor).
- Per §3, none of this matters if site ambient is above 32 ng — which it certainly is. The geophone's
  advantage is real but probably **unusable**, which loops back to: stop optimising noise.

---

## 6. Propagation — an open conflict

MASTER §7.1 uses **~3000 m/s** (P-wave in concrete) for TDoA.
PigV² measured through a pig-pen floor: **100–200 m/s** **[PAPER]**.

A 15–30× velocity error is a 15–30× error in the distance implied by every time difference. TDoA
geometry, node spacing, and required timing sync all depend on this.

Rubble is not monolithic concrete — it is fractured, unconsolidated, air-gapped debris, closer in
character to the loose medium PigV² measured than to a poured slab. **The 3000 m/s figure is
probably wrong for the actual medium**, and is currently unsupported by any source in this folder.

PigV² also gives the attenuation model **[PAPER]**: `S_loc2 = S_loc1 · e^(−α·f·d)` — attenuation is
**frequency-dependent**, so the 10–100 Hz band attenuates faster with distance than a low band would.
This is the one genuine argument *for* low-frequency operation, and it trades directly against §2.
Resolving that trade needs a measurement, not more reading.

---

## 7. Derived requirement

| Parameter | Requirement | Rationale |
|---|---|---|
| Detection band | **10–100 Hz** | §1 — both working systems; sensor specs valid here |
| Rate extraction | envelope periodicity, 0.8–3 Hz | §1 — repetition rate, not carrier |
| Self-noise, 10–100 Hz | **< 50 µg rms** is sufficient | §3 — ambient-limited; below this is wasted |
| Axes | 3-axis preferred | drop orientation is uncontrolled |
| ODR | ≥ 250 Sps | Nyquist for 100 Hz + filter margin |
| Supply current | ≤ 2 mA sensor budget | MASTER §4.1: ~9 mA total for 25 h |
| Mass / size | ≤ 3 g, ≤ 10 mm | MASTER: ~8 g node |
| Interface | SPI or I²C, digital | avoids an analog front-end per node |
| Cost | **≤ US$10/node** | §3 — spend on node count, not per-node noise |
| Temp | −20…+70 °C min | field deployment |

**Nothing in `02-sensor-survey.md` meets all of these.** The parts that meet the noise spec fail
power/size/cost by 10–100×; the parts that meet power/size/cost have noise 5–150× over. That gap is
the real finding, and it is only resolvable by measuring site ambient — because if ambient is where
§3 says it is, the cheap parts are fine and the requirement above is over-specified.

---

## 8. What must be measured before any part is fixed

1. **Site ambient PSD in 10–100 Hz on real rubble.** Everything above is downstream of this.
   Until it exists, no sensor choice is defensible.
2. **Coupling loss, node-to-rubble.** Likely larger than every sensor difference in this folder.
3. **Wave velocity in rubble** (§6). 3000 vs 150 m/s is not a detail.
4. **Actual heartbeat impulse amplitude at 1 m, 3 m, 5 m through debris.** MASTER §10.1 already flags
   detection range as the blocking unknown; this research confirms it and does not resolve it.

---

*Back to [README](README.md) · Next: [02 — Sensor Survey](02-sensor-survey.md)*
