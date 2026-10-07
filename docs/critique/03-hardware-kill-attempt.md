# 03 — Hardware Kill Attempt

Hostile mechanical/electrical review of the node as specified in `MASTER.md` §4, §4.1, §8.3–§8.6
and the reference doc. Date **2026-10-06**.

**Convention:** MEASURED (lab/field data from a cited source) · COMPUTED (derived here, arithmetic
shown) · ASSERTED (claimed in the spec or a source with no derivation).
Price provenance: LIVE (read off the vendor page in this pass) · SEARCH (search snippet) · EST.

> **⚠️ Evidence bar NOT met — read §12 before trusting the vendor tables.**
> The brief required ≥20 referred sources and ≥15 distinct vendors/datasheets with live prices.
> I reached **~14 sources and 6 priced parts** before the session's web-tool quota was exhausted.
> The *physics* findings below are complete and self-contained — every one is arithmetic over
> inputs already in the spec, and the two decisive datasheet facts were read from primary
> sources. **The redesign BOM is under-sourced and is costed to ±30%.** It is a direction, not a
> purchase order. §12 lists exactly what is missing.

---

## 1. Verdict

**The node as specified cannot be built, and if it could be built it would not work.**

Three independent failures, each sufficient on its own. None is a tuning problem; all three are
dimensional or arithmetic, provable without buying anything.

| # | Finding | Severity |
|---|---|---|
| F1 | §8.3's impact figure is wrong by **10–100×**. Real impact is 200–2000 G, not 15–20 G. The foam is sized for the wrong load by two orders of magnitude. | **FATAL** |
| F2 | The **8 g mass is impossible**. Cell + ballast alone are 6 g. Honest build is **17 g**. | **SERIOUS** |
| F3 | **CR2032 cannot source 9 mA.** Panasonic rates it at 0.2 mA; max continuous is 3 mA. Real runtime is **4–11 h, not 25 h**, and the radio browns out on TX. | **FATAL** |
| F4 | **The foam is required to be two contradictory things** — an impact isolator and a rigid coupling path. *(But see §5: the frequency separation is real, and this is the one attack in my brief that FAILS.)* | **SLOPPY, not fatal** |
| F5 | Node position is known to **±4 m**; §7.2 claims ±0.1 m localization. **43× gap.** | **FATAL (geometric)** |
| F6 | ADXL355 is rated **5,000 g, not 10,000 g**. Survives — but the **solder joints and cell holder are the failure point**, not the die. | **SERIOUS** |
| F7 | Dropping hard objects onto a live collapse is an **operational-safety non-starter** no incident commander signs off. | **SERIOUS** |
| F8 | Reference doc's **$29/node, 48–72 h, 15–20 G, ±0.05 m** are all reverse-engineered from desired answers. | **SLOPPY** |

**One correction to my own brief up front, recorded because it cuts against me:** I was told to
attack the F450's "25 min with 9 nodes" as fantasy. **It is not fantasy.** See §8 — the claim
substantially survives. Attacking it would have been wrong.

---

## 2. The single hardest physical problem

**It is not the drop, and it is not the battery. Both of those are solvable with money and volume.**

> ### Coupling an 8 g puck to rubble at 1–4 Hz is the problem with no clean solution.
> ### And the reason is the opposite of what the brief assumed.

My brief predicted the node is "10× too light" and would decouple because the coupling resonance
falls into the 1–4 Hz band. **I computed it and that is wrong.** Using the standard rigid-disc-on-
elastic-half-space stiffness `k = 4Ga/(1−ν)` (Lamer/Krohn lineage):

| Ground | Contact | k (N/m) | f₀, 8 g node | f₀, SM-24 (75 g) |
|---|---|---|---|---|
| Loose dry rubble, G=10 MPa | full face, a=20 mm | 1.19e6 | **1944 Hz** | 635 Hz |
| Compact debris, G=50 MPa | full face | 5.97e6 | **4348 Hz** | 1420 Hz |
| Concrete slab, G=12 GPa | full face | 1.43e9 | **67 kHz** | 22 kHz |
| Loose rubble | **3 point contacts, a=0.5 mm** | 8.96e4 | **533 Hz** | 107 Hz |

**COMPUTED.** The coupling resonance is **500 Hz – 67 kHz — two to four orders of magnitude above
the 1–4 Hz target band.** Below resonance, transmissibility → 1. **A light sensor couples *better*
than a heavy one** (f₀ ∝ 1/√m), which is the exact inverse of the brief's premise.

**So why do geophones get spiked and buried?** Because the SM-24 has a **10 Hz natural frequency of
its own moving element** and is used at 10–100+ Hz where soil damping, tilt and shear coupling
actually bite — and because a 75 g cylinder on a 25 mm base has far lower f₀ than a 4 cm puck.
Krohn 1984 and Drijkoningen 2000 are about the **spike-shear vs weight-coupling** distinction at
*seismic-survey* frequencies. **Transplanting "surface-laid sensors decouple" to 1–4 Hz is a
category error.** I was briefed to make it; I am not making it.

**The real coupling problem is not resonance. It is these four, and they are worse:**

1. **Tilt, not decoupling.** On a 30–45° rubble slope the sensing axis is 30–45° off vertical.
   `cos(45°) = 0.707` → **3 dB of signal lost** before anything else. A 3-axis sensor plus a
   gravity-vector rotation genuinely does fix this in software, for ~$0. **This part of the spec
   is right** and the "~$0 software fix" claim in the research pass holds.
2. **Voids.** A node that lands in a cavity, or bridges two blocks touching neither, couples to
   nothing at any frequency. **No sensor design fixes this.** It is a placement-statistics
   problem, and it argues for *more, cheaper nodes* — which cuts against the $55 ADXL355.
3. **A loose rock that rings.** A node resting on a detached fragment measures **the fragment's**
   resonance, not the ground's. A 0.5 kg slab fragment on a compliant contact has f₀ in the tens
   of Hz with a high Q — out of band, but it will ring at every aftershock and raise the noise
   floor in-band through intermodulation.
4. **Rocking.** A puck on 3 point contacts has a *rocking* mode far softer than the vertical one,
   and rocking couples horizontal ground motion into the vertical axis. This is in-band and is
   the one genuine low-frequency coupling risk. The spec never mentions it.

> **Verdict on coupling:** the node is **not** too light, and mass is **not** the fix. The fixes
> are **a conformal contact** (so you get face contact, not 3 points), **a low, wide stance** (to
> stiffen the rocking mode), and **accepting that void landings are a yield loss** — plan on
> 20–40% of nodes returning nothing and deploy enough to survive that.
>
> **This is unsolvable in the sense that matters: you cannot guarantee from the air that a given
> node lands on load-bearing material.** That is a deployment-statistics reality, not a bug.

---

## 3. F1 — The drop arithmetic (FATAL)

### 3.1 Independent verification

**§8.3 asserts:** 3–4 m → ~7.7 m/s → `F = m·v²/(2·compression)` ≈ **15–20 G**, "inside foam tolerance."

Step 1, velocity. `v = √(2gh)`, g = 9.80665:

| h | v |
|---|---|
| 3 m | **7.671 m/s** |
| 4 m | 8.857 m/s |

**COMPUTED. The 7.7 m/s is correct.** It is the only correct number in §8.3.

Step 2, deceleration. `a = v²/(2d)`, d = stopping distance, h = 3 m:

| d | a | G |
|---|---|---|
| **150 mm** | 196 m/s² | **20 G** ← what §8.3's answer implies |
| **15 mm** (entire node height, crushed to nothing) | 1961 m/s² | **200 G** |
| 10 mm | 2942 m/s² | 300 G |
| 5 mm (realistic foam crush) | 5884 m/s² | **600 G** |
| 3 mm | 9807 m/s² | 1000 G |
| 2 mm (onto concrete rubble) | 14710 m/s² | **1500 G** |
| 1 mm (onto a rock point) | 29420 m/s² | 3000 G |

Inverted — stopping distance required to achieve a given G at h = 3 m:

| Target | Required d |
|---|---|
| 15 G | **200 mm** |
| 20 G | **150 mm** |
| 200 G | 15 mm |
| 1000 G | 3 mm |

> **To hit 15–20 G you need 150–200 mm of crush. The node is 15 mm tall.**
> **§8.3 is not optimistic. It is dimensionally impossible for its own stated geometry** — off by
> **10× in the best case (full crush) and 30–100× realistically.**

**Audit #1:** the error is a missing `d`. §8.3 writes `F = m·v²/(2·compression)` — correct in form
— then supplies an answer consistent with d ≈ 150 mm. Nobody checked d against the node height on
the line above. **Reproduced independently; matches `00-my-own-arithmetic.md` §1 exactly.**

**Audit #2:** is the spec perhaps quoting 15–20 G as the *post-foam* load at the die, with the foam
absorbing the rest? Even granting that reading, a 15 mm node cannot contain a 150 mm stroke, and
§4's wording — *"foam shell absorbs 15–20 G"* — describes the **total impact**, not a residual.
Either reading fails.

### 3.2 Energy and force (h = 3 m, m = 8 g) — COMPUTED

KE = ½mv² = **235 mJ**; momentum = 61.4 g·m/s.

| Crush | G | Peak force |
|---|---|---|
| 15 mm | 200 G | 15.7 N |
| 5 mm | 600 G | 47.1 N |
| 2 mm | 1500 G | 118 N |
| 1 mm | 3000 G | 235 N |

Contact stress at 1000 G over 3 asperities of 1 mm² each: **26 MPa**. Over the full 4 cm face:
**0.06 MPa**. **Three orders of magnitude difference** — which is the whole argument for a
conformal contact rather than a rigid shell.

### 3.3 Is the node dead on landing? — part by part

**ADXL355 die: SURVIVES.** Primary datasheet, read directly (Rev. A, p.8, Table 5):

> **Acceleration (Any Axis, 0.1 ms), Unpowered: 5,000 g**

**MEASURED/datasheet. Note my brief guessed 10,000 g — that is the ADXL375/ADXL335 figure. The
ADXL355 is 5,000 g, half.** Still above a 600–1500 G impact, so the **die is not the problem** —
margin is ~3–8×. But the rating is for a **0.1 ms** pulse and is an *absolute maximum* (a stress
rating, explicitly "functional operation... is not implied"), not a fatigue spec. **Repeated** 1000 G
events are outside what that number certifies.

**Solder joints: THE ACTUAL FAILURE POINT.** The ADXL355 is a **14-terminal 6×6×2.1 mm LCC** —
leadless. Leadless packages have no compliant lead to absorb board flex. The literature is
unambiguous and specifically about this package class:

> FEM analysis of a **MEMS board-level LCC package** shows "the solder joints are one of the key
> weakness points"; max effective stress at "the outer corner in the outermost solder point."
> Drop-test failure modes: **pad cratering** (most common) and **solder cracking near the
> intermetallic layer**. — PHM Society, *Study on MEMS board-level package reliability under
> high-G impact*

**This is the finding that kills the node, not the die rating.** A rigid PCB with a leadless MEMS
part, taking 600–1500 G repeatedly, fails at the joints. And the failure is **insidious**: a
cracked joint often still conducts, so the node reports data that is wrong rather than reporting
nothing. **A silently-wrong survivor sensor is worse than a dead one.**

**CR2032 + holder: PROBABLE FAILURE.** A 3.0 g cell at 600 G exerts **17.7 N** on the retaining
spring (`F = ma = 0.003 × 600 × 9.81`). Standard retainers are specified for retention under
"shock and vibration" in the IEC sense — not for 600–1500 G. Momentary contact break = brownout =
reboot = lost time sync. **The cell holder is the single most likely part to end the mission**, and
it is exactly the part the BOM prices at **$0.60 [EST]**.

**Verdict:** the die survives; **the assembly does not.** The spec protects the wrong component.

---

## 4. F2 — The 8 g mass budget is impossible (SERIOUS)

**§4 asserts:** ~4 cm dia × 1.5 cm, **~8 g assembled**, including a **3 g tungsten base**.

Honest build, component by component — COMPUTED, masses EST from package geometry except where noted:

| Item | Mass | Basis |
|---|---|---|
| CR2032 cell | 3.00 g | datasheet typical |
| CR2032 SMD holder | 1.20 g | EST |
| ADXL355, 14-term LCC 6×6×2.1 mm | 0.20 g | COMPUTED from package volume |
| RAK3172 module | 0.70 g | EST |
| PCB, 35 mm dia, 1.6 mm, 4-layer FR4 | 2.60 g | COMPUTED: V=1.54 cm³ × 1850 kg/m³ = **2.85 g** |
| Antenna, u.FL whip + pigtail | 1.50 g | EST |
| Passives + connector | 0.30 g | EST |
| PLA shell, 40×15 mm | 3.50 g | EST |
| EVA foam | 1.00 g | EST |
| **Tungsten ballast (as specified)** | **3.00 g** | §4 |
| **TOTAL** | **17.0 g** | |
| *(without tungsten)* | *14.0 g* | |

> **The cell and the ballast alone are 6.0 g of an 8 g budget**, leaving 2 g for PCB, sensor,
> radio, antenna, holder, case and foam. **The 8 g figure is impossible** — the honest number is
> **~2.1× the spec.** This matches the independent estimate in `00-my-own-arithmetic.md` (15.5 g);
> the gap between 15.5 and 17.0 is PCB diameter and antenna assumptions, not a disagreement.

**The 3 g tungsten ballast does not do what §4 claims.** Tungsten is 19 250 kg/m³, so 3 g is
**0.156 cm³** — as a 36 mm disc that is a **0.15 mm foil**. For shuttlecock self-righting you need
the CG well below the centre of pressure; a 0.15 mm foil against a 14 g airframe moves the CG
barely at all. **Meaningful ballast is 10–50 g** (0.5–2.6 mm of tungsten disc), which *doubles to
quadruples* node mass — and, per §2, that is **fine for coupling** and **bad for impact** (energy
scales with m).

**Self-righting, attacked properly:**

- **(a)** The mass budget does not add up, above.
- **(b)** **Shuttlecock righting works in a fluid, during flight.** It orients the node *in the
  air*. It does nothing after first contact. At 7.7 m/s onto irregular rubble the node **bounces,
  rolls, and settles in an arbitrary attitude** — or wedges in a crevice sensor-up. The spec
  conflates "arrives oriented" with "rests oriented." **A 3–4 m fall gives ~0.8 s of flight —
  enough to orient, and enough to reach 7.7 m/s, which is what then un-orients it.**
- **(c)** On a 30–45° slope "sensor-down" ≠ "level." **The 3-axis + gravity-vector fix is real and
  does work** — the ADXL355 is DC-coupled, so the static gravity vector gives absolute tilt, and
  rotating into the vertical frame is a few lines of firmware. **Cost genuinely ~$0.** This is one
  of the few claims in the spec that survives contact.

---

## 5. F4 — Foam as isolator vs foam as coupler (the attack that FAILS)

My brief told me these are "DIRECTLY CONTRADICTORY" and to attack head-on. **I computed the
transmissibility and the contradiction largely dissolves. Recording that honestly.**

Single-DOF transmissibility `|T| = 1/|1−(f/f₀)²|`, foam pad A = 1257 mm², t = 5 mm, m = 8 g,
`k = EA/t` — COMPUTED:

| Foam | k (N/m) | f₀ | T @ 1 Hz | T @ 4 Hz | T @ 1 kHz |
|---|---|---|---|---|---|
| Soft EVA, E=1 MPa | 2.51e5 | **892 Hz** | 1.0000 | 1.0000 | 3.90 (+11.8 dB) |
| EVA, E=5 MPa | 1.26e6 | 1995 Hz | 1.0000 | 1.0000 | 1.34 |
| Stiff EVA, E=20 MPa | 5.03e6 | 3989 Hz | 1.0000 | 1.0000 | 1.07 |
| PLA, E=3.5 GPa | 8.80e8 | 52.8 kHz | 1.0000 | 1.0000 | 1.0004 |

> **At 1–4 Hz, transmissibility is 1.0000 to four decimal places for every foam considered.**
> The signal band sits **200–4000× below** the foam's resonance. The foam is acoustically
> invisible in-band.

**So there IS a frequency separation, and it is enormous.** Impact is a ~kHz-scale event
(a 1 ms pulse has energy to ~1 kHz); the signal is 1–4 Hz. **Three orders of magnitude of
separation.** One structure *can* do both jobs. The brief's premise is wrong.

**What survives of the attack — two real caveats:**

1. **The soft EVA row shows T = 3.9 at 1 kHz — amplification, not isolation.** A foam with
   f₀ = 892 Hz *amplifies* impact content near 892 Hz by ~12 dB. **Soft foam chosen for impact
   can make the impact worse** at the frequency that cracks solder. Foam must be chosen stiff
   (f₀ well above impact content) or genuinely crushable (energy-absorbing, not spring-like).
2. **Crushable ≠ elastic.** The table models foam as a *linear spring*, valid for the µg-level
   signal. For impact the foam must **crush plastically** — and a crushed foam is a *different,
   denser* material afterward. **The node's coupling after impact is not the coupling you
   designed.** This is real, and the spec never mentions it.

**Verdict: SLOPPY, not fatal.** The two requirements are compatible. The spec is still wrong to
have never *stated* the assumption, and the soft-foam amplification trap is live. **A two-stage
design (sacrificial crush nose + rigid sensor path) is the right answer** — not because the
frequencies conflict, but because **plastic crush and repeatable coupling conflict.**

---

## 6. F3 — Power (FATAL)

### 6.1 The spec's own arithmetic is internally consistent — and built on a false premise

§4.1: 200 µA + 800 µA + 8 mA = **9.0 mA**; 225 ÷ 9 = **25.0 h**. **COMPUTED: both check out.**
The LoRa average: 40 mA × (100 ms / 500 ms) = **8.0 mA**, i.e. a **20% duty cycle** — which §5 says
must be ~1%. **20× over.** (Already flagged in MASTER; confirmed here.)

### 6.2 (a) Is 225 mAh even right?

**Nominally yes, meaninglessly so.** Panasonic/Maxell rate CR2032 at **220–235 mAh** — but
**at 0.2 mA, into a 3 kΩ load** (Energizer: 0.19 mA). **ASSERTED in spec as if rate-independent.**
**The rating current is 45× below the spec's operating current.**

### 6.3 (b) Derated capacity — the number that matters

| Condition | Capacity | Runtime at 9 mA |
|---|---|---|
| Rated, 0.19–0.2 mA | 225 mAh | *(25.0 h — the spec's claim)* |
| Energizer 2 s pulse spec, 6.8 mA | **100 mAh** | **11.1 h** |
| Est. 9 mA continuous | **~60 mAh** | **6.7 h** |
| Est. 9 mA at 0 °C | **~40 mAh** | **4.4 h** |

**COMPUTED from MEASURED derating data.** Independent corroboration — a measured 9 mA load
(ATtiny85 + OLED) dropped a CR2032 **from 3.0 V to below 2.5 V in 30 minutes**, 1.5 V at 12 h.

> **Real runtime is 4–11 h, not 25 h. The spec overstates by 2.3–5.6×.**
> **And the reference doc's "48–72 hours" overstates by 4–18×.** The 72 h survival window — the
> entire premise of the project — is **not reachable on a CR2032 by a factor of ten.**

**Manufacturer limits, SEARCH:** Panasonic continuous drain **0.2 mA**; Duracell max continuous
**6 mA**, max 1 s pulse **20 mA**; Energizer 2 s pulse **6.8 mA**. **9 mA continuous exceeds every
manufacturer's continuous rating.** The spec operates the cell outside its datasheet.

### 6.4 (c) Pulse droop — when does the radio brown out?

`V_droop = I × R_int` — COMPUTED. A fresh CR2032 is ~10–30 Ω, rising to 100 Ω+ as it depletes and
when cold. SX1276 at +14 dBm draws ~40 mA; at +20 dBm, ~120 mA.

| R_int | 40 mA TX | 120 mA TX |
|---|---|---|
| 10 Ω | 3.0 → **2.60 V** | 3.0 → **1.80 V** |
| 15 Ω | 3.0 → 2.40 V | 3.0 → **1.20 V** |
| **30 Ω** | 3.0 → **1.80 V** | 3.0 → **−0.60 V** (i.e. collapse) |
| 50 Ω | 3.0 → 1.00 V | collapse |
| 100 Ω (depleted/cold) | 3.0 → **−1.00 V** (collapse) | collapse |

SX1276 minimum supply is **1.8 V**; ESP32 needs 2.3 V, STM32WLE5 1.8 V.

> **At 30 Ω — an ordinary mid-life CR2032 — a 40 mA TX pulse lands exactly on the 1.8 V floor
> with zero margin. At +20 dBm it collapses outright.** The node browns out **on its first
> transmission at high power**, and progressively earlier as the cell ages.
>
> **This is unfixable by firmware.** It needs a **bulk capacitor** (≥100 µF, ideally a
> supercapacitor) across the cell to source the pulse — a part the BOM does not contain.

### 6.5 (d) Temperature

Panasonic CR2032 operating range **−30 to +85 °C**; Maxell **−20 to +85 °C**; some vendors spec
**−10 °C** as the practical floor. Internal resistance rises sharply below 0 °C — commonly 2–4×.

> At 0 °C, R_int ≈ 30–60 Ω → **40 mA TX droops 1.2–2.4 V → brownout.**
> At −10 °C it is worse. **Earthquakes happen in winter** (Kahramanmaraş, Feb 2023, sub-zero
> nights; Nepal, Turkey, Afghanistan). **The node fails in exactly the conditions where buried
> survivors most need a fast find** — cold also depresses heart rate into the 0.67 Hz band the
> spec widens its filter for. **The two cold-weather requirements collide.**

### 6.6 (e) What cell should it be, in an 18.85 cm³ envelope?

Envelope: π × (2 cm)² × 1.5 cm = **18.85 cm³** — COMPUTED. Enormous for a coin cell. The CR2032
(1.0 cm³) uses **5%** of it. **The envelope was never the constraint; nobody checked.**

**The right cell is a LiSOCl₂ 1/2AA**, e.g. **ER14250 / LS14250**:
**3.6 V, 1200 mAh, 14.65 × 24.8 mm, 8.9 g**, max continuous **35 mA**, max pulse **200 mA (1 s)**.

| | CR2032 | ER14250 |
|---|---|---|
| Rated capacity | 225 mAh @ 0.2 mA | **1200 mAh @ ~2 mA** |
| Usable at 9 mA | ~60 mAh | **~1100 mAh** |
| Max continuous | 0.2–6 mA | **35 mA** |
| Max pulse | 20 mA | **200 mA** |
| Runtime at 9 mA | **6.7 h** | **~122 h** |
| Mass | 3.0 g | 8.9 g |

**COMPUTED: 1100 mAh ÷ 9 mA = 122 h — comfortably past the 72 h window**, with the pulse headroom
to transmit without browning out. Costs **+5.9 g** and needs a 24.8 mm length (fits a 1.5 cm-tall
puck only if the node grows to ~2.8 cm tall, or the cell lies on its side across the 4 cm diameter
— **it fits laid flat**).

**Caveat, stated because it matters:** LiSOCl₂ cells **passivate** when stored, and the first pulse
after long storage sees elevated impedance. They also dislike being pulsed hard from cold without a
parallel capacitor. **The bulk cap from §6.4 is required either way.**

---

## 7. F5 — Localization collapses on node-position uncertainty (FATAL, geometric)

**§8.5:** node position = drone GPS at release + drift correction. **§7.2:** ±0.1–0.2 m at 9 nodes.

**TDoA solves for a target from *known* sensor positions. It cannot know the target better than it
knows the sensors.** Error budget, RSS — COMPUTED:

| Term | σ |
|---|---|
| Consumer GPS CEP, open sky | 2.50 m |
| Multipath near rubble/standing structures (additional) | 3.00 m |
| Release transient at 3 m/s | 0.50 m |
| Lateral drift over a 3–4 m fall (wind) | 0.70 m |
| **Bounce + roll after impact** | **1.50 m** |
| **RSS total σ_p** | **4.27 m** |

Target error ≥ σ_p × GDOP:

| GDOP | Target error |
|---|---|
| 1.0 (best case) | 4.27 m |
| 1.5 | **6.41 m** |
| 2.0 | 8.54 m |
| 3.0 | 12.81 m |

> **Claimed ±0.15 m vs achievable ~6.4 m: the spec is off by ~43×.**

**And the timing work is irrelevant to this.** At LongShoT's 2 µs: **0.3 mm** at 150 m/s, **6 mm**
at 3000 m/s — COMPUTED. §10.4 optimized a term that was already **1000× smaller** than the term
nobody budgeted. **The bounce-and-roll term is not in §8.5 at all**, and it is the one term no
amount of GPS quality removes.

**Does the whole localization claim collapse? Yes, as written.** Two honest outs:

1. **Restate the spec in metres.** 4–6 m still beats "somewhere in this 500 m² pile" and is
   genuinely useful for directing a search. **This is the intellectually honest fix and costs $0.**
2. **UWB inter-node ranging.** TDoA needs only *relative* geometry, so ranging nodes to each other
   recovers sub-decimetre *relative* positions regardless of GPS.

**UWB fallback, fully costed — the line the spec never adds:**

| Item | Figure |
|---|---|
| DW1000/DW3000-class BOM adder | **$12–25/node** [EST] |
| 9 nodes | **$108–225** |
| 11 nodes (with spares) | **$132–275** |
| Power | **31–160 mA** active TX/RX — **4–18× the entire node budget** |
| Complexity | own ranging schedule, scheduler, ≥3 anchors at known positions |

> **The power line is the killer, not the money.** $108–275 is affordable; **drawing 31–160 mA on
> a node whose total budget is 9 mA is not.** UWB must be duty-cycled to a brief survey *once*
> after deployment, then shut down permanently — which works (positions don't change after
> landing) but must be designed in deliberately. **Nobody has written that down.**

---

## 8. F-none — Deployment claims that SURVIVE (recording where my brief was wrong)

**(a) "25 min with 9 nodes on an F450" — SUBSTANTIALLY SURVIVES.** My brief called this fantasy
and predicted 10–18 min. Field reports: an F450 on **4S 5200 mAh reaches 20–25 min**; 25 min is
achieved "in ideal conditions"; a 1200 g F450 on 3S 5000 mAh managed 18 min. **~25 min is at the
optimistic end of a real range, not fabricated.** And the payload claim is sound: **72 g on an
800 g airframe is ~9%** — §8.4's "+8–10% battery drain" is proportionate and honest.

**Two caveats that do bite:** (i) at the corrected **17 g/node**, 9 nodes = **153 g**, not 72 g —
**2.1× the payload**, pushing drain to ~17–19% and flight time toward **18–20 min**; (ii) this is
hover-and-cruise, not **precision station-keeping at 4 m in thermals**, which costs more.

**(b) Hovering at 4–5 m over a fire with updrafts — the PID claim is a non-sequitur.** "PID at
400–1000 Hz" is **ASSERTED as if loop rate were the limiting factor. It is not.** Every modern
flight controller runs there; it is the default, not a mitigation. The actual limits are **thrust
margin and control authority**, and a fire updraft can exceed the airframe's descent authority
regardless of loop rate. **GPS multipath beside standing structures** also degrades position hold
exactly where the rubble is. **Optical flow at 4 m over self-similar grey rubble is a weak
reference** — low texture contrast is its known failure mode. **SLOPPY**: the stated mitigation
does not address the stated threat.

**(d) Operational safety — SERIOUS, and the one most likely to end the project in the real world.**

- **Dropping 17 g objects at 7.7 m/s onto a live collapse.** Energy is only ~0.24 J — genuinely
  low, comparable to a dropped coin. **Direct trauma risk to a survivor in a void is small.**
- **But the trigger risk is not about energy.** Debris piles sit in **metastable equilibrium**;
  the hazard is disturbance at a critical contact, and USAR doctrine treats *any* unnecessary
  loading of an unshored pile as unacceptable during live rescue.
- **The drone is the bigger hazard than the node.** A 1 kg quad losing authority in an updraft
  and striking the pile is a far larger disturbance than the payload — plus rotor downwash on
  loose dust and debris at 4 m.
- **Regulatory:** this is **flight over people** (rescuers on and beside the pile) and the
  deliberate **release of an object from a UA** — in most jurisdictions that needs specific
  authorization, and in a disaster zone the airspace is typically under TFR with manned
  rotary-wing medevac operating low.

> **Would an incident commander permit it? Not during live rescue on an unshored pile, and not
> into airspace shared with medevac.** The credible concept of operations is **hand-placement at
> the pile margin, or drone placement during an assessment phase before crews are committed** —
> not "fly the grid while the search is running." **This does not kill the sensor; it kills the
> drone-deployment premise that §8.1 uses to justify the whole architecture.** §8.1's argument
> ("manual placement puts rescuers on unstable rubble") is real — but the answer may be a
> **thrown or placed** node, not a dropped one, which **removes the entire impact problem (F1)**.

---

## 9. F8 — The reference doc, audited for reverse-engineered numbers

| Claim | Status |
|---|---|
| **"$29/node"** | **Reverse-engineered.** MASTER already rebuilt it at **$67.75** (2.3×). The ADXL355 alone is **$55.16**. The old figure summed "~$15 + ~$4 + ~$5 + ~$2 + ~$3" = $29 — **retail guesses with no PCB, no spares, no assembly.** |
| **"48–72 hours"** | **Reverse-engineered from the 72 h survival window, not from the cell.** MASTER caught the double-count and said 25 h. **Both are wrong: the real number is 4–11 h** (§6). The figure was chosen to match the pitch. |
| **"~8 g"** | **Impossible** (§4). Honest ~17 g. |
| **"15–20 G"** | **Dimensionally impossible** (§3). Honest 200–2000 G. |
| **"±0.05 m at 16 nodes"** | **Below the system's own timing floor AND 85× below its position floor** (§7). |
| **"Terminal velocity in 3m fall ≈ 7.7 m/s"** | **Right number, wrong term.** 7.67 m/s is *impact* velocity; terminal velocity is where drag balances weight and is irrelevant in a 3 m fall. Sloppy physics vocabulary masking a correct value. |
| **"SM-24 … 10 Hz minimum"** → rejected | **Correct reasoning, and it quietly indicts the project.** A 10 Hz corner is indeed unusable at 1–2 Hz. But the doc never asks the follow-up: **the entire professional seismic industry works above 10 Hz because that is where ground coupling and SNR are tractable.** Choosing 1–2 Hz opts out of all of it. |
| **"Weeks on coin battery in duty-cycle mode"** (§4 table) | Contradicts the doc's **own** Q7 answer of 25 h, three pages later. **Internally inconsistent.** |
| **"CERN 2018 / US Army Research Lab 2020 / DARPA"** (Q6) | **UNVERIFIED — I could not check these in this pass** (quota). Q6 asserts "this is not theoretical" on three citations given without title, author or DOI. **Given this doc's demonstrated numeric reliability, treat all three as unconfirmed until someone pulls the actual papers.** Flagged in §12. |

---

## 10. The node I would build instead

**Design rules, derived from the findings above:**

1. **Don't drop it.** F1 and F7 both dissolve if the node is **placed or lowered**, not dropped.
   A drone hovering at 1 m and releasing at <1.5 m/s cuts impact to ~25 G at 5 mm crush —
   **inside real foam tolerance** — and removes the secondary-collapse objection.
   *If it must be dropped from 3–4 m, it needs a crushable nose of ≥30 mm stroke* (→ 100 G).
2. **Mass is not the enemy** (§2). Spend it on a real cell and a conformal base.
3. **Protect the joints, not the die** (§3.3). Underfill or pot the sensor; strain-relieve the PCB.
4. **Hold the cell mechanically**, not with a spring retainer.
5. **A bulk capacitor is mandatory** (§6.4), whatever the cell.

### 10.1 Mass budget that adds up

| Item | Mass |
|---|---|
| ER14250 LiSOCl₂ 1/2AA, laid flat | 8.9 g |
| Cell: soldered tabs + retention clamp (no spring holder) | 1.0 g |
| ADXL355 | 0.2 g |
| RAK3172 | 0.7 g |
| PCB 35 mm, 4-layer | 2.6 g |
| 220 µF bulk cap + passives | 0.8 g |
| Antenna | 1.5 g |
| Shell: TPU conformal base + crushable EVA nose | 6.0 g |
| Potting/underfill | 1.5 g |
| **Ballast (tungsten, for righting authority)** | **12.0 g** |
| **TOTAL** | **35.2 g** |

**COMPUTED. ~35 g, not 8 g.** Nine nodes = **317 g** — still only ~40% of an 800 g F450's airframe
mass and well inside its lift, costing maybe 5–7 min of flight time. **Envelope grows to ~4 cm ×
2.8 cm** (6.0 cm³ of 18.85 cm³ available — still roomy).

**Why 12 g of ballast, not 3 g:** 12 g of tungsten = 0.62 cm³ = a **0.61 mm disc at 36 mm dia** —
thin enough to sit under the PCB, heavy enough (34% of node mass at the very bottom) to give real
CG authority. And per §2, **added mass does not hurt coupling** — f₀ at 35 g on loose rubble is
still **~930 Hz**, three orders above the band.

### 10.2 Parts, prices, links

| Role | Part | Spec | Price | Vendor | Status |
|---|---|---|---|---|---|
| **Cell** | **Jauch ER14250J-T** | 3.6 V, 1200 mAh LiSOCl₂, 35 mA cont, 200 mA pulse, 8.9 g | **$2.96** @1 / $2.46 @10 / $2.04 @100 | DigiKey | **SEARCH** (price from snippet; product page **BOTWALL** — `azcus.digikey.com` did not resolve) |
| Cell (alt) | SAFT LS14250AX | same form, axial tabs — **tabs preferred: no holder** | — | DigiKey | **BOTWALL** |
| Cell (alt) | Dantona ER14250 | 1200 mAh | $8.73 @1 | Newark | SEARCH |
| **Sensor** | **ADXL355BEZ** | 25 µg/√Hz, ±2 g, 14-term LCC 6×6×2.1, **5000 g unpowered**, −40/+125 °C | $55.16 | LCSC (per MASTER §9) | **[LIVE] in MASTER's pass, not re-verified here** |
| **MCU+radio** | **RAK3172** | STM32WLE5, Cortex-M4 + SX126x | $5.99 | RAKwireless (per MASTER §9) | **[LIVE] in MASTER's pass, not re-verified here** |
| **Reference** | **SM-24 geophone w/ insulating disc** | 28.8 V/m/s, 74 g, 10 Hz, 25.4×32 mm | **$69.95** | SparkFun, SEN-11744, **in stock** | **LIVE** ✅ |
| Buck/LDO | Adafruit LM3671 breakout | 3.3 V, 600 mA | **$4.95** | Adafruit PID 2745 | **LIVE** ✅ *(breakout — for bench bring-up only, not the node BOM)* |
| Bulk cap | 220 µF low-ESR tantalum/ceramic + 1 F supercap | sources 120 mA TX pulse | ~$1.50 | — | **EST — NOT SOURCED** |
| Conformal base | TPU 95A, printed | shore-A, conforms to asperities | ~$0.50 | — | **EST — NOT SOURCED** |
| Ballast | Tungsten disc 36 mm × 0.6 mm | 19 250 kg/m³ | ~$4–8 | — | **EST — NOT SOURCED** |
| UWB (optional) | DW3000-class module | §7 fallback | $12–25 | — | **EST — NOT SOURCED** |

**Revised per-node cost:** $55.16 + $5.99 + $2.96 + ~$1.50 + ~$0.50 + ~$6 + PCB $1.80 + antenna
$1.50 + passives $1.50 ≈ **$77** [EST, ±30%] — up ~$9 from MASTER's $67.75, almost entirely cell
and ballast. **The headline $1,845 system cost moves by roughly $100. The Delsar
order-of-magnitude argument is unaffected.**

> **The cheapest change on this page is not a part. It is lowering the node instead of dropping
> it** — that is firmware and flight profile, costs $0, and removes a FATAL finding and a SERIOUS
> one at once.

---

## 11. Where I could be wrong

**On the coupling finding (§2) — most likely to be challenged.** I used a **rigid disc on an
elastic half-space**, which assumes a continuum. **Rubble is a discrete granular medium** and a
continuum shear modulus may not describe it; if effective local stiffness at a 3-point contact is
far lower than G = 10 MPa implies, f₀ drops. **It would have to drop by 100× to reach the band**
(f₀ ∝ √k, so k would need to fall 10 000×). I judge that implausible but not impossible. **The
rocking mode is the real exposure** — I did not compute it, and it is softer than the vertical
mode by the ratio of contact spacing to CG height. **If one finding here gets overturned, it is
this one, and I'd want a shake-table test before betting on it.**

**On the impact G (§3).** If a **deliberately crushable nose with ≥30 mm stroke** were added, G
drops to ~100 G and much of F1 recedes. The spec describes no such thing (15 mm total height), so
I judged it against what is written. Also, my `a = v²/2d` assumes **constant deceleration**; a real
crush pulse is peaked, so **peak G is typically 1.5–2× my figure** — my numbers are *optimistic*,
and the finding strengthens rather than weakens.

**On capacity derating (§6.3).** The 60 mAh and 40 mAh figures are **EST by extrapolation** from
the measured 100 mAh @ 6.8 mA, not read off a 9 mA discharge curve — I could not open the
Panasonic PDF (quota). They could be off by ±40%. **The conclusion is robust to that**: even
100 mAh gives 11 h, still 2.3× short of the claim and 6.5× short of 72 h.

**On flight time (§8a).** I used forum field reports, not a controlled test. They skew optimistic
(pilots report best flights). Real mission-profile endurance with precision hover is likely
**below** my 18–20 min.

**On operational safety (§8d).** This is a **judgment about doctrine and regulation, not physics.**
I did not verify against a specific jurisdiction's rules or INSARAG guidance — the search quota
ran out. A USAR practitioner could reasonably say drone placement during an assessment phase is
routine. **I'd want that reviewed by someone who has run a pile.**

**On the solder-joint finding (§3.3).** The cited FEM work is on *a* MEMS LCC package, not on the
ADXL355 specifically, and I did not find ADXL355 drop-test data. The package class and failure
physics transfer; the exact G at which *this* part fails is unknown. **Testable cheaply: drop 10
nodes and read the noise floor before and after.**

**On §5, where I contradicted my own brief.** The transmissibility model is linear single-DOF.
Foam under impact is **non-linear and rate-dependent**, so the 1 kHz column is indicative only.
The **1–4 Hz columns are robust** — three orders below resonance, any plausible model gives T ≈ 1.

---

## 12. Source register — and what is missing

**Honest accounting against the brief's bar of ≥20 sources / ≥15 vendors with live prices:**
**reached ~14 sources, 6 vendor/datasheet references, 3 verified-live prices.** The session's
web-tool quota was exhausted mid-pass. **The physics stands; the sourcing does not.**

| # | Source | Used for | Access |
|---|---|---|---|
| 1 | **Analog Devices ADXL354/ADXL355 datasheet Rev. A**, p.8 Table 5 — `analog.com/media/en/technical-documentation/data-sheets/adxl354_adxl355.pdf` | **5,000 g unpowered**; 25 µg/√Hz; LCC 6×6×2.1; −40/+125 °C | **LIVE** (PDF fetched + text-extracted directly) ✅ |
| 2 | Same, spec tables | noise density, filter passbands, scale factor | **LIVE** ✅ |
| 3 | **Drijkoningen 2000, *Geophysics* 65(6):1780–1787**, "Usefulness of geophone ground-coupling experiments" | spike-shear vs **weight coupling**; Krohn 1984 context | **LIVE** (PDF extracted) ✅ |
| 4 | Krohn 1984, *Geophysics* 49:722–731 (via #3) | coupling canon | **secondary — not read directly** |
| 5 | PHM Society, *Study on MEMS board-level package reliability under high-G impact* | **LCC solder joints are the weak point**; pad cratering | SEARCH |
| 6 | embeddedcomputing.com, "CR2032 Maximum Current Capacity: Datasheet, Reality, and Alternatives" | **measured 9 mA → <2.5 V in 30 min**; Panasonic 0.2 mA, Duracell 6 mA/20 mA, Energizer 0.19 mA/6.8 mA | **LIVE** ✅ |
| 7 | Panasonic CR2032 datasheet | 220–235 mAh @ 3 kΩ; −30/+85 °C | **BOTWALL/quota — NOT READ.** Figures via #6 and search |
| 8 | Maxell CR2032 datasheet | 220 mAh; −20/+85 °C | SEARCH |
| 9 | SAFT/Jauch LS14250/ER14250 specs (baltrade listing) | 1200 mAh, 35 mA cont, 200 mA pulse, 8.9 g, 14.65×24.8 | SEARCH |
| 10 | DigiKey ER14250J-T, `azcus.digikey.com/.../25651443` | $2.96/$2.46/$2.04, 921 in stock | **DEAD** (`ENOTFOUND azcus.digikey.com`) — price is SEARCH only |
| 11 | **SparkFun SEN-11744 SM-24 geophone** — `sparkfun.com/geophone-sm-24-with-insulating-disc.html` | **$69.95**, in stock, 28.8 V/m/s | **LIVE** ✅ |
| 12 | Core Electronics / Little Bird SM-24 listings | **74 g**, 10 Hz, 11 g moving mass, 25.4×32 mm | SEARCH |
| 13 | **Adafruit PID 2745 LM3671** — `adafruit.com/product/2745` | **$4.95** | **LIVE** ✅ |
| 14 | ArduPilot discuss threads (multiple) | F450 **20–25 min on 4S 5200**; 18 min at 1200 g on 3S | SEARCH |
| 15 | Harwin HT027xx coin-cell holder environmental testing | shock/vib retention data | **DEAD** (301 → 404) |
| 16 | SparkFun DEV-21265 | *(URL guessed, returned MyoWare sensor — discarded, not used)* | LIVE but irrelevant |

**Explicitly NOT obtained, and needed before this BOM is actionable:**

1. **Panasonic/Energizer CR2032 discharge curves at 9 mA** — §6.3's 60/40 mAh are extrapolations.
2. **A live, readable DigiKey/Mouser page for ER14250** with price and stock (all DigiKey hosts
   BOTWALL/DEAD this pass).
3. **Vendor sources for: bulk capacitor, TPU filament, tungsten disc, DW3000 module, cell retention
   clamp** — all EST, none priced from a vendor. **These are 5 of the ~15 vendors the brief wanted.**
4. **Harwin/Keystone/Renata coin-holder shock-retention numbers** — §3.3's holder-failure claim is
   reasoned from force, not from a retention spec.
5. **The reference doc's Q6 citations** (CERN 2018, ARL 2020, DARPA) — **unverified**; §9 flags them.
6. **ADXL355-specific drop-test data** — none found; §3.3 reasons from package class.

---

## 13. What to do next, in order

1. **Stop specifying a drop.** Change §8.3 to a **low-altitude lowered release (<1.5 m, <1.5 m/s)**.
   Costs $0, removes F1 and most of F7. *If the drop must stay, the node needs a ≥30 mm crush nose
   and the 15 mm height goes.*
2. **Change the cell to ER14250 + bulk cap.** Removes F3. +$2.40, +6 g.
3. **Correct §4 to ~35 g** and re-derive payload. Removes F2.
4. **Restate §7.2 in metres**, or add the UWB line with its **31–160 mA** power cost. Removes F5.
5. **Underfill the ADXL355 and clamp the cell.** Addresses F6 — the joints, not the die.
6. **Before any of it: §10.1's bench measurement still gates everything.** If the ADXL355 cannot
   resolve a heartbeat at 0.5 m, none of the above matters.

**One thing worth saying plainly:** the sensing premise is not disproven by anything here. Every
finding above is about **packaging, power and deployment** — all fixable with mass, volume and a
different release profile, none of which the project is short of. **The hardware is wrong. The
idea is not yet wrong.**
