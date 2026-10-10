# 04 — Action Report

What this research changes in `docs/MASTER.md`, ranked by impact.
Nothing here has been written into MASTER — these are proposed changes awaiting a decision.

---

## A1 — MASTER §6 filters out the signal ⛔ blocking

**Current:** 4th-order Butterworth **0.5–4 Hz**, 60 s FFT @ 100 Hz.
**Finding:** the detectable heartbeat signature through a structure is an **impulse train with
energy in 10–100 Hz**. 1–2 Hz is the *repetition rate*, present in the envelope, not in the raw
acceleration at useful amplitude.

**Evidence** (`01-requirements.md` §1, `03-literature.md` §1–2):

- PigV² detects heartbeats over **10–100 Hz** wavelet coefficients, explicitly because the
  heartbeat vibration band is 0–100 Hz and sensors are useful ≥10 Hz.
- VitalMon achieves **1.90 BPM mean error** with a geophone that is a second-order high-pass at
  **10 Hz** — i.e. with the 0.5–4 Hz band already removed by the sensor itself.
- Sercel: MEMS noise specs are white-region figures; **1/f below ~10 Hz is not characterised**,
  so 1–2 Hz is also the band where the noise floor is *unknowable* from any datasheet.

**Proposed change:**

| | From | To |
|---|---|---|
| Acquisition band | 0.5–4 Hz | **5–200 Hz** — ~~10–100 Hz~~; the **detection** band is an **output of M1/M2**, not proposed here (ADR 0001) |
| Method | bandpass → FFT → LSTM | **bandpass → wavelet/envelope → peak-pick rate → LSTM** |
| Rate band | (the signal band) | **envelope periodicity, 0.8–3 Hz** |

**Knock-on:** §3.1's "aftershock 5–50 Hz — high-cut" and "machinery 20–200 Hz — high-cut" now
**overlap the signal band**. Those interferers can no longer be rejected by frequency. They must be
rejected on **character** — impulse-train periodicity, amplitude, and cross-node coherence. This is
a real increase in DSP difficulty and it should be stated in MASTER rather than discovered later.

**Counter-argument, stated once:** PigV²'s own attenuation model `S = S₀·e^(−α·f·d)` means 10–100 Hz
attenuates faster with distance than 1–2 Hz would. If rubble is lossy enough, the low band could
win on range despite having less energy. **This is measurable and unmeasured.**

It still does not rescue the current design. The 0.5–4 Hz band assumes a noise floor the chosen part
does not document. **One part does document it** — the Epson **M-A370AD10**, 0.02 µG/√Hz over
1–10 Hz, below the USGS NHNM — at **36.3 mA and 29 g**, i.e. 4× the node's entire current budget and
3.6× its mass. So the low-band design is coherent only with a sensor this node cannot carry.
**If the node ever grows a 36 mA / 30 g budget, A1 is worth reopening.** Until then it stands.

---

## A2 — MASTER §9 BOM is wrong by 4× on the sensor ⛔ blocking

**Current:** ADXL355 at **~$15**, node $29, 9 nodes $261, system $641–1141.
**Finding:** ADXL355 is **$63.26 @1 / $60.41 @30** (LCSC C468833, confirmed twice today from the
page's own price payload — `05-verification-log.md` B1).

**Corrected BOM [CALC]:**

| | Current | Corrected |
|---|---|---|
| Sensor | $15 | **$63.26** |
| **Per node** | $29 | **$77.26** |
| 9 nodes | $261 | **$695** |
| **System** | $641–1141 | **$1,075–1,575** |

The Delsar-comparison argument in §9 still holds at $1,575 — the order-of-magnitude advantage over
~$15,000 survives. **But the numbers in §9 are wrong and must be restated.**

**Worse than the price: supply.** LCSC shows **3 units** of ADXL355BEZ in stock (plus 8 of the
reel variant). **You cannot currently buy the 9 parts §9 assumes.** India availability is
unconfirmed — element14 IN and Robu both block automated checks.

> ⚠️ **SUPERSEDED 2026-10-06 — this supply argument is dead.** Re-pulled: ADXL355 stock is now
> **486 + 1192 units**, and the price has fallen to **$55.1592 @1** (−12.8 %). **You can buy the
> 9 parts.** The price correction stands; the scarcity claim does not. See
> `../BUDGET/04-verification-log.md` **D11**, and `../BUDGET/03-budget.md` for the rebuilt BOM at
> current prices. **Lesson: an inventory claim is perishable and must carry a date.**

**✅ Updated 2026-09-17 — there is now a fully verified way out of both problems.** The ST
**IIS2ICLX** datasheet is in `extracts/ST_IIS2ICLX_datasheet.md` and its specs are first-hand (`02` B3): **15 µg/√Hz typ,
420 µA, $26.51, 421 in stock.** Non-sensor node cost is **$14.00** [CALC], so:

| Sensor | Per node | 9 nodes | System |
|---|---|---|---|
| ADXL355 (current pick) | $77.26 | $695 | **$1,075–1,575** |
| **IIS2ICLX** | **$40.51** | **$365** | **$745–1,245** |
| Murata SCA3300-D01 | $52.98 | $477 | $857–1,357 |

**Switching to the IIS2ICLX removes $330 from the node BOM and replaces a stock of 3 with a stock of
421.** The cost of doing so is the **Z axis** — see A4. That trade, not the price, is the decision.

---

## A3 — MASTER §3.2 rejects the SM-24 for a reason that no longer holds ⚠️ high

**Current:** *"SM-24 geophone (0.1 µg/√Hz but a 10 Hz corner frequency, which sits above the entire
target band — unusable here regardless of its noise spec)."*

Two problems:

1. **The premise died with A1.** If the target band is 10–100 Hz, a 10 Hz corner is not above it —
   it is at the edge of it. **The SM-24 is the exact part VitalMon used to measure heart rate, and
   the same class PigV² used.** Two of the three working systems in `03-literature.md` used a
   geophone.
2. **The noise figure is understated by ~100×.** MASTER says 0.1 µg/√Hz. **[CONFIRMED 2026-10-08 by independent re-extraction of the brochure: it contains NO noise specification — regex `nois` returns zero matches over the full text. So 0.1 µg/√Hz is not a vendor figure and never was. This report's computed value is the right one; treat 0.1 as a conservative system-level (element + preamp) assumption, never as a datasheet number.]** Coil Johnson noise from
   the brochure's own 375 Ω / 28.8 V/m/s gives **~1 ng/√Hz at 20 Hz** — about **0.001 µg/√Hz**
   (`01-requirements.md` §5, my calculation, caveats stated there).

**Proposed change:** rewrite the rejection. The SM-24 may still be the wrong node sensor, but for
the *real* reasons: **1-axis**, **11 g moving mass** in an 8 g node, **$69.95 each**, and it needs a
**<2.5 nV/√Hz preamp + ADC per node**. Rejecting it on the 10 Hz corner is rejecting it on the one
property that the literature says is fine.

---

## A4 — Sensor selection is optimising the wrong variable ⚠️ high

Sercel measured their own MEMS as **ambient-limited above ~2 Hz** — in a soundproof chamber, on an
isolation platform, in a basement (`03-literature.md` §3). On a rubble field, with machinery,
generators, crews and wind, site ambient in 10–100 Hz will exceed every sensor self-noise figure in
`02-sensor-survey.md` by orders of magnitude.

**If that holds, the ADXL355's 25 µg/√Hz buys nothing over a $2 MPU-6050, and the project is paying
$48/node extra for margin below the noise floor of the environment.**

The lever that actually works against incoherent ambient noise is **node count** (~√N coherent
gain) — which is bought with cost per node. Nof et al. is the published precedent: mini-arrays of
low-cost MEMS with a **<US$150 DAQ** solving back-azimuth for real earthquakes.

**Proposed change:** add to §3.2 that the sensor is **PENDING on a site-ambient measurement**, not
FIXED. Selection rule becomes *"self-noise comfortably below site ambient in 10–100 Hz, at minimum
cost/power/size"* — not *"lowest noise density."*

**This is the cheapest test in the project.** A ~$2 MPU-6050 module plus an evening of recording on
any rubble/demolition site answers it. If ambient exceeds 3.8 mg rms in 10–100 Hz, the MPU-6050 is
sufficient and A2 evaporates. If ambient is below ~200 µg rms, the ADXL355 is justified and its
price has to be accepted.

**✅ Updated 2026-09-17 — the Murata SCA3300-D01 sharpens this argument considerably.** Its noise
density was the missing number that got it rejected; it is now published and verified at
**35 µg/√Hz (Mode 3)** — making it **the noisiest of the three buyable candidates**
(IIS2ICLX 15, ADXL355 25). On a pure noise ranking it loses. But it is the only candidate that is
**3-axis, rated −40…+125 °C, mechanically over-damped, and published with an India distributor
path.** On a rubble field — machinery, falling debris, drone-drop impact, uncontrolled node
attitude, and a team sourcing in India — **every one of those beats a 20 µg/√Hz noise advantage
that sits far below site ambient anyway.**

**This is now a three-way decision that the ambient measurement settles:**

| If site ambient in 10–100 Hz is… | Then the right part is… | Because |
|---|---|---|
| **≫ 400 µg rms** (likely) | **SCA3300-D01**, or an MPU-6050 | Self-noise is irrelevant; buy 3 axes, shock tolerance and supply |
| **~150–400 µg rms** | **IIS2ICLX** | Cheapest part still below ambient — if the Z-axis loss is survivable |
| **≪ 150 µg rms** (unlikely) | ADXL355 or better | Only then does noise density buy range |

**Not one of these three rows can be chosen by reading.** That is the finding.

---

## A5 — MASTER §7.1 wave velocity is probably wrong ⚠️ high

**Current:** ~3000 m/s (P-wave in concrete).
**Finding:** PigV² measured **100–200 m/s** through a pen floor. Rubble — fractured,
unconsolidated, air-gapped — is far closer to that than to a poured slab.

A 15–30× velocity error is a 15–30× error in every distance TDoA infers from a time difference. It
changes node spacing, array aperture, and the timing-sync precision the LoRa mesh must deliver.

**Proposed change:** mark §7.1 velocity **PENDING**, with 150 m/s and 3000 m/s as the bracket until
measured. A hammer-source travel-time test across a known baseline on debris resolves it in an hour.

---

## A6 — MASTER §4.1 power budget disqualifies the good sensors ℹ️ note

The budget is ~**9 mA total** for 25 h. Against that:

| Part | Sensor current alone |
|---|---|
| ADXL355 | 200 µA ✔ (2 % of budget) |
| Epson M-A352AD10 | **13.2 mA** ✘ (146 % of the *whole node*) |
| Colibrys SI1003 | **27 mA** ✘ (300 %) |

The only two parts in this survey whose noise specs are valid in-band **cannot be powered by this
node**, and the Epson is additionally 25 g in a 48 mm case against an 8 g node.

No change proposed — this is confirmation that the power budget, not noise, is what eliminates the
seismic-grade tier. It is worth recording in §3.2 so the tier is not re-investigated later.

---

## A7 — MASTER §10.1 remains the blocking unknown ℹ️ confirmed

§10.1 asks: *does an ADXL355 resolve a heartbeat through rubble at 3 m, or at 0.5 m?*

**This research does not answer it, and confirms nothing published does.** The literature covers
beds, floors and chairs — benign, short-path, low-noise media. **No paper was found on heartbeat
detection through rubble or debris.** That gap is this project's actual contribution, and it means
§10.1 can only be closed by measurement.

The four measurements, in dependency order (`01-requirements.md` §8):

1. **Site ambient PSD, 10–100 Hz, on real rubble** — gates A4 and therefore the sensor choice.
   Method: `03-literature.md` §6 (PSD-PDF, McNamara & Boaz). Instrument: Raspberry Shake, or an
   MPU-6050 module for a first cut.
2. **Coupling loss, node-to-rubble** — likely larger than every sensor difference in this folder.
3. **Wave velocity in rubble** — gates A5.
4. **Heartbeat impulse amplitude at 1 / 3 / 5 m through debris** — closes §10.1.

---

## A8 — Node attitude is bounded, not controlled → the sensor must be 3-axis ⛔ resolved

**Input (user, 2026-09-17):** a drone drop **cannot guarantee attitude**, but a **usable range**
can be set.

**Tilt alone would have been survivable** — *provided* the sensor is mounted with its blind axis
**horizontal**. (Mounted blind-axis-vertical, a perfectly flat landing captures **nothing**.)

| Node tilt | Worst-case capture | Loss |
|---|---|---|
| ±15° | 0.966 | −0.3 dB |
| ±30° | 0.866 | −1.3 dB |
| ±45° | 0.707 | −3.0 dB |

At ±30° that is ~1 dB — **not worth $330.** But tilt is not the binding term.

**The source geometry is.** The signal arrives along a **slant ray** from a buried source, not
vertically. The node's azimuth is random on landing and **the source azimuth is the unknown being
solved for**, so the sensitive plane cannot be pre-oriented. With `d` = horizontal offset and
`h` = depth [CALC]:

| d/h | Incidence | Worst case | Azimuth-averaged |
|---|---|---|---|
| 0.5 | 27° | −1.0 dB | −0.5 dB |
| 1.0 | 45° | −3.0 dB | −1.3 dB |
| 2.0 | 63° | **−7.0 dB** | −2.2 dB |
| 3.0 | 72° | **−10.0 dB** | −2.6 dB |

**The loss is worst at the far nodes — which are already weakest from attenuation, and which TDoA
needs most.** A 2-axis part degrades precisely the arrival picks that set the localisation aperture.

**Two further findings:**

1. **Self-righting fights coupling.** The mechanical fix for attitude is a weighted tumbler base —
   i.e. a **rounded bottom**, giving rocking point contact on rubble. Per A7, coupling loss is
   likely larger than every sensor difference in this folder. **Solving attitude that way worsens
   the bigger problem.** Expanded in `06-build-vs-buy.md` §6.1.
2. **3 axes buy a capability 2 cannot.** With attitude recoverable from the DC gravity vector, each
   node can rotate into the world frame and yield **per-node back-azimuth from particle-motion
   polarisation** — an independent constraint on position alongside TDoA. **Nof et al.
   (`extracts/`) do exactly this with low-cost MEMS mini-arrays.**

**Decision: 3-axis. The ST IIS2ICLX is eliminated** — not on noise or price, on geometry. The $330
saving in A2 was buying a constraint that fights coupling.

**This leaves SCA3300-D01 ($52.98/node) vs ADXL355 ($77.26/node), still gated on A4's ambient
measurement.** No ADR: this eliminates a candidate, it does not fix the sensor. The ADR remains the
post-ambient sensor decision, with this as an input to it.

> ⚠ **SUPERSEDED 2026-10-11 — the sensor is no longer gated on an ambient measurement.** The **SM-24
> geophone is selected** and the **ADXL355 is rejected** (`docs/critique/07-verdict.md` §4.2; ADR 0001).
> The SCA3300/ADXL355 shortlist above, and the three-way table in A4, are closed — neither names the
> part that won. **The 3-axis geometry argument still stands on its own terms** and was one of the
> reasons; so does the point that a 2-axis part buys a constraint that fights coupling.

---

## Recommended sequence

| # | Action | Cost | Unblocks |
|---|---|---|---|
| 1 | Restate §6 band as 10–100 Hz + envelope method | $0 | A1 — the signal chain is currently wrong |
| 2 | Correct §9 BOM to $77.26/node, $1,075–1,575 system | $0 | A2 — honest numbers |
| 3 | Rewrite the §3.2 SM-24 rejection; downgrade sensor from FIXED to PENDING | $0 | A3, A4 |
| 4 | Buy an MPU-6050 module (~$2); record ambient on a demolition site | ~$2 | **A4 — the highest value per rupee in the project** |
| 5 | Hammer travel-time test on debris | $0 | A5 |
| ~~6~~ | ~~Download the ST IIS2ICLX datasheet~~ ✅ **DONE 2026-09-17** — B3 is now fully [DS], and the Murata SCA3300 noise density was obtained with it | $0 | — |
| 7 | Price a Raspberry Shake; decide if calibrated ground truth is worth it | — | rigorous version of 4 |
| ~~8~~ | ~~Decide whether a drone-dropped node can guarantee attitude~~ ✅ **ANSWERED 2026-09-17: it cannot, but a usable range (±~30°) can be set.** → **3-axis required, IIS2ICLX eliminated** (A8) | $0 | — |
| 10 | **Design the coupling interface** — spike/anchor that mates a dropped node to fractured debris, *without* a self-righting round base | — | **the dominant term in the link budget** (`06` §6.1) |
| 9 | Re-check the SCA3300 price on a live page, and get an India distributor quote via Murata's `en-in` stock-check path | $0 | the only verified India supply route in the survey |

~~**No ADR is proposed.**~~ **[SUPERSEDED 2026-10-11: two ADR-worthy decisions have since been taken.]**
Per `CLAUDE.md`, ADRs are for irreversible, cross-cutting or contested decisions. A1–A3 are corrections
to numbers and a band — MASTER is live and takes them directly. If the sensor is re-fixed *after* the
ambient measurement, **that** is an ADR: it is cross-cutting (cost, power, DSP, node count) and it is
contested by this document.

> **What actually happened.** The sensor *was* re-fixed — to the **SM-24**, not to either part this
> document shortlists, and without waiting on the ambient measurement (`07-verdict.md` §4.2). And the
> band became **ADR 0001** (`docs/decisions/0001-tap-acquisition-band.md`, 2026-10-11), because it was
> contested exactly as this paragraph predicts. **A1's band row is superseded by that ADR** and is no
> longer "a plain doc edit": the detection band is now an output of measurement, which is the one
> thing a live doc edit cannot express. A2/A3 remain plain numeric corrections.
>
> Note `docs/decisions/` is **gitignored** — the ADR does not survive a clone. `AGENTS.md` carries its
> full substance for collaborators.

---

*Back to [README](README.md) · Prev: [03 — Literature](03-literature.md) · Next: [05 — Verification Log](05-verification-log.md)*
