# 02 — Sensor Survey: Specs, Price, Vendors

> **All prices captured 2026-09-17.** Semiconductor pricing moves; re-check before any PO.
> Tags: **[DS]** from the datasheet extract in `extracts/` · **[LIVE]** pulled from the vendor page's
> own price payload today · **[UNVERIF]** single-source or search-snippet only, **do not trust**.
> **Link check:** ✅ = returned HTTP 200 today. ⚠️ = bot-blocked (403/timeout) from this machine;
> the URL is the canonical one but I could not confirm it live — verify in a browser.
> Audit trail: `05-verification-log.md`.

---

## Summary table

| # | Part | ND @≥10 Hz | Axes | Current | Size | Price @1 | Verdict |
|---|---|---|---|---|---|---|---|
| A1a | **Epson M-A370AD10** | **0.02 µG/√Hz @1–10 Hz** [DS] | 3 | 36.3 mA | 48×24×16 mm, 29 g | quote only | **Beats the USGS NHNM.** Power ✘✘✘ |
| A1b | Epson M-A352AD10 | **0.2 µG/√Hz @0.5–6 Hz** [DS] | 3 | 13.2–20 mA | 48×24×16 mm, 25 g | ~€999 [UNVERIF] | Noise ✔, everything else ✘ |
| A1c | Epson M-A552AC10/AR10 | 0.5 µG/√Hz @0.5–6 Hz [DS] | 3 | 35–40 mA @12 V | 65×60×30 mm, 128 g | quote only | IP67 field unit. Far too big |
| A2 | Safran-Colibrys SI1003 | **0.7 µg/√Hz** [DS] | 1 | 27 mA | LCC20 | no public price | Noise ✔, power ✘✘ |
| A3 | Sercel QuietSeis | **<15 ng/√Hz** [PAPER] | 3 | 85 mW | OEM module | not sold as a component | Unobtainable |
| A4 | Kinemetrics EpiSensor ES-T | 0.06 µg/√Hz @1 Hz [UNVERIF] | 3 | — | instrument | Class A, $2–4k [PAPER] | Reference tier only |
| B1 | **ADI ADXL355** | 25 µg/√Hz [DS] | 3 | 200 µA | 6×6×2.1 mm | **$63.26** [LIVE] | MASTER's pick — **4× the assumed price** |
| B2 | ADI ADXL354 | 20 µg/√Hz [DS] | 3 | — | same family | ~$51.30 [UNVERIF] | Analog out; needs an ADC |
| B3 | ST IIS2ICLX | **15 typ / 30 max µg/√Hz** [DS] | **2 (X/Y)** | **420 µA** | CCLGA-16 5×5×1.7 | **$26.51** [LIVE] | Best noise/$ — but 2-axis |
| B4 | Murata SCA3300-D01 | **35 typ / 40 max µg/√Hz** (Mode 3) [DS] | 3 | 1.2 mA | 8.6×7.6×3.3 mm | $38.98 [UNVERIF] | Noisiest buyable part — but 3-axis, over-damped, **sourceable in India** |
| B5 | TDK IIM-46234 | 70 µg/√Hz [UNVERIF] | 6-axis | 0.3 mA | 23×23×8.5 mm | not found | Single-source spec |
| C1 | TDK MPU-6050 | **400 µg/√Hz** [DS] | 6-axis | ~3.9 mA | module | ~$2 (module, IN) | 16× too noisy — but see §C |
| G1 | **Geospace SM-24** | ~1 ng/√Hz @20 Hz [CALC] | 1 | passive | Ø25.4 mm, 11 g | **$69.95** [LIVE] | Quietest by 77 dB; 1-axis, heavy |
| R1 | Raspberry Shake RS1D | instrument | 1 | mains/USB | boxed | ~$500+ [UNVERIF] | **Buy one as ground truth** |

---

## Tier A — Seismic-grade MEMS

These are the only parts whose noise spec would survive contact with the original 1–2 Hz design.
Every one of them fails this project's power, size, or cost envelope by 10–100×.

### A1a. Epson M-A370AD10 — the part that proves the low band is *possible*

**The single most important part in this survey**, not because it is buyable but because of what it
demonstrates. Epson's own headline claim:

> "Ultra-low noise, **surpassing USGS New High Noise Model** — **0.02 µG/√Hz typ. (1 Hz ~ 10 Hz)**"
> *(citing Peterson, J., "Observations and Modeling of Seismic Background Noise", USGS OFR 93-322, 1993)*

| Spec | Value | Src |
|---|---|---|
| **Noise density** | **0.02 µG/√Hz typ, 0.04 max @ 1–10 Hz** | [DS] brief sheet |
| Range / dynamic range | ±10 G, **170 dB** | [DS] |
| Resolution | 2⁻²⁴ G/LSB = **0.06 µG/LSB** | [DS] |
| Frequency response | **DC to 210 Hz** | [DS] |
| Output data rate | 50–1000 Hz, user selectable | [DS] |
| Amplitude / phase response | ±0.4 dB / ±0.1° | [DS] |
| Bias temp error | ±0.5 mG max (−30…+85 °C) | [DS] |
| Bias repeatability | ±0.1 mG typ / year | [DS] |
| **Time sync** | **GNSS 1 PPS input** | [DS] |
| **Supply current** | **36.3 mA @ 3.3 V** | [DS] |
| Package | Aluminium die-cast **48 × 24 × 16 mm, 29 g**, SPI/UART | [DS] |
| Shock | 500 G (vs 1,000 G for M-A352/M-A552) | [DS] |
| Temp | −30…+85 °C | [DS] |
| Part code | `X2F000091000000` | [DS] |

**Why this matters to `01-requirements.md` §2.** My argument against the 1–2 Hz band is that MEMS 1/f
noise there is *uncharacterised*. **This part characterises it** — 0.02 µG/√Hz across 1–10 Hz, below
the USGS NHNM. So the low band is not physically impossible. It costs **36.3 mA and 29 g** to get
there, against a 9 mA / 8 g node. The band is unreachable *for this project*, not in principle.
That is a materially more honest framing and it is now in §2.

**Price:** no public listing. Quote only.
**Vendors:** see A1b below — same distributor network.

**Verdict — the most capable seismic MEMS found, and 4× over the entire node power budget.**
Recommended application list is literally *"seismic measurement, resource exploration, SHM."*
Right domain, wrong power envelope.

### A1b. Epson M-A352AD10

| Spec | Value | Src |
|---|---|---|
| Noise density | **0.2 µG/√Hz typ, 0.7 max @ 0.5–6 Hz** | [DS] |
| Range | ±15 G, 3-axis (+ tilt, ±1.047 rad / ±60°) | [DS] |
| Resolution | 0.06 µG/LSB | [DS] |
| **Frequency response** | **DC to 460 Hz (−6 dB)** | [DS] |
| Output rate | 50–1000 Sps | [DS] |
| Supply current | **13.2 mA @ 3.3 V** (lineup table); **20 mA typ at ODR 200 Hz** (brief sheet); sleep 1.3 mA | [DS] |
| Supply | 3.15–3.45 V | [DS] |
| Package | Aluminium die-cast **48 × 24 × 16 mm, 25 g**, SPI/UART | [DS] |
| Shock | 1,000 G | [DS] |
| Bias temp error / repeatability | ±2 mG (−30…+85 °C) / 3 mG typ per year | [DS] |
| Temp | −30…+85 °C | [DS] |
| MTBF | 87,600 h | [DS] |

> **Correction to an earlier draft of this survey:** I had recorded the bandwidth as "−6 dB at
> **9**–460 Hz". Both Epson's lineup table and the M-A352 brief sheet say **DC to 460 Hz (−6 dB)**.
> The low end is DC, not 9 Hz. Logged as D5 in `05-verification-log.md`.

> **Power is mode-dependent.** 13.2 mA is the lineup figure; the brief sheet quotes **20 mA typ at
> ODR 200 Hz**. Since `01-requirements.md` §7 needs ODR ≥ 250 Sps, **~20 mA is the number that
> applies here** — which makes the disqualification below stronger, not weaker.

**Price:** ~**€999** — ⚠️ **[UNVERIF], single source.** Treat as order-of-magnitude only.

**Vendors** (corrected — `global.epson.com` 403s; the live host is `epsondevice.com`):
- Manufacturer lineup: <https://www.epsondevice.com/sensing/en/products/accelerometer/feature/> ✅
- Authorised distributors: <https://www.epsondevice.com/sensing/en/contact/distributor/> ✅
  - **Americas** — Digi-Key (accelerometers + eval tools), Mouser, Dove
  - **Europe/EMEA** — Texim Europe, Amcoris
  - **Asia / India — none listed.** ⚠️ Procurement would go through Epson global sales or an EMEA
    distributor. This is a real obstacle, independent of price.
- Brief sheets converted to `docs/research/MEMS/extracts/epson.md` and `Epson_M-A352AD10_briefsheet.md` / `Epson_M-A370AD10_briefsheet.md` (source PDFs deleted 2026-10-08; `*.pdf` is gitignored)

**Verdict — disqualified on three counts:**
- **13.2–20 mA** against a **~9 mA whole-node budget** (MASTER §4.1). The sensor alone exceeds the node.
- **25 g in a 48 mm case** against an **~8 g node**. The sensor is 3× the node.
- **~€999** against a **$29 node**. ~35× the entire BOM.

Keep it in mind as a **calibration reference**, not a node part.

### A1c. Epson M-A552AC10 / M-A552AR10

An M-A352 in an **IP67 waterproof/dustproof housing** — the ruggedised field variant.
0.5 µG/√Hz @0.5–6 Hz, ±15 G, DC–460 Hz, **65 × 60 × 30 mm, 128 g**, 9–32 V at **35 mA (CANopen)** /
**40 mA (RS422)**, −30…+70 °C, M12 connector. [DS]

**Relevant only as a design reference.** A rubble field is exactly the harsh, wet, dusty environment
IP67 exists for — so the *enclosure* requirement is real and MASTER's "3D-printed PLA + foam" case
(§9) deserves a second look. The part itself is 16× the node's mass budget.

### A2. Safran-Colibrys SI1000 series (SI1003 / SI1005)

| Spec | SI1003 | SI1005 | Src |
|---|---|---|---|
| Range | ±3 g | ±5 g | [DS] |
| White noise | **0.7 µg/√Hz typ, 0.9 max** | 1.2 typ, 1.5 max | [DS] |
| Noise integrated **0.1–100 Hz** | **8 µg** | 13 µg | [DS] |
| Dynamic range (100 Hz BW) | 108.5 dB | 108.5 dB | [DS] |
| Frequency response (+3 dB) | 450–550 Hz | — | [DS] |
| Resonant frequency | 1.0 kHz | — | [DS] |
| Scale factor | 900 mV/g | — | [DS] |
| Supply | 3.2–3.4 V | same | [DS] |
| **Supply current** | **27 mA typ, 32 max** | same | [DS] |
| Package | LCC20 hermetic, non-magnetic, RoHS | same | [DS] |
| Output | **analog differential** (OUTP−OUTN) | same | [DS] |

Note the rare and valuable **"integrated over 0.1 Hz to 100 Hz = 8 µg"** spec — unlike almost
everything else here, this part's low-frequency behaviour is actually characterised.

**Price:** no public distributor listing found. Quote-only.
**Vendors:** Safran Colibrys product pages ⚠️ (403 from this machine). Sold through Safran directly.

**Verdict — disqualified on power.** 27 mA is 3× the whole node budget. Also 1-axis and analog,
so each node would need a low-noise ADC + reference chain. Excellent part, wrong application.

### A3. Sercel QuietSeis

| Spec | Value | Src |
|---|---|---|
| Noise | **<15 ng/√Hz above 10 Hz** | [PAPER] |
| Low-frequency 1/f | **not characterized** | [PAPER] |
| Bandwidth | DC–800 Hz | [PAPER] |
| Power | 85 mW | [PAPER] |
| Axes | 3C | [PAPER] |

**Not purchasable as a component.** Sercel sells it inside land-seismic acquisition systems.
Its value here is as **evidence** (see `01-requirements.md` §2–3), not as a part.

### A4. Kinemetrics EpiSensor ES-T

Force-balance, **not MEMS**. 0.06 µg/√Hz @1 Hz, ±0.25–4 g, ~155 dB DR [UNVERIF].
Sits in the **Class A ($2,000–4,000)** tier of Evans et al. 2014 [PAPER]. Reference instrument.

---

## Tier B — Industrial / instrumentation MEMS (actually buyable)

### B1. ADI ADXL355 — *MASTER §3.2's fixed choice*

| Spec | Value | Src |
|---|---|---|
| Noise density | **25 µg/√Hz** (all three axes, ±2 g range) | [DS] |
| Range | ±2 / ±4 / ±8 g, 3-axis | [DS] |
| Resolution | 20-bit, **3.9 µg/LSB** @±2 g | [DS] |
| Digital LPF | 1–1000 Hz | [DS] |
| Digital HPF | 0.0095–10 Hz | [DS] |
| ODR | 3.9 Hz – 4 kHz | [DS] |
| Supply current | **200 µA** measurement (internal LDO on) / 160 µA (LDO bypassed) / 21 µA standby | [DS] |
| Supply | 2.25–3.6 V | [DS] |
| Package | 14-terminal LCC, **6 × 6 × 2.1 mm** | [DS] |
| Temp | −40…+125 °C | [DS] |
| Interface | SPI / I²C | [DS] |

**Price — this is the problem.**

| Source | Qty 1 | Break | Stock | Status |
|---|---|---|---|---|
| **LCSC** (C468833, ADXL355BEZ) | **$63.26** | $60.41 @30 | **3 pcs** (+8 of BEZ-RL) | ✅ **[LIVE]** |
| DigiKey | $70.93 | — | — | ⚠️ [UNVERIF] |
| ADI list | ~$41.84 | — | — | ⚠️ [UNVERIF] |

**Vendors:**
- LCSC (verified live, exact price above): <https://www.lcsc.com/product-detail/C468833.html> ✅
- Manufacturer: <https://www.analog.com/en/products/adxl355.html> ⚠️
- Mouser search: <https://www.mouser.com/c/?q=ADXL355> ✅
- DigiKey search: <https://www.digikey.com/en/products/result?keywords=ADXL355> ⚠️
- India — element14: <https://in.element14.com/search?st=ADXL355> ⚠️ · Robu: <https://robu.in/?s=ADXL355> ⚠️
  (both bot-blocked from here; India stock **unconfirmed**)

**Also available:** EVAL-ADXL355-PMDZ Pmod breakout — user guide in
`docs/research/MEMS/extracts/adxl355.md`. This is the sane way to get first data without
laying out a board.

**Verdict:**
- ✔ Power (200 µA), size (6 mm), 3-axis, digital, temp range — all excellent.
- ✘ **MASTER §9 prices this at ~$15. It is $63.26.** That is **+$48/node**; the $29 node BOM and
  the $641–1141 system figure are both invalid. See `04-action-report.md`.
- ✘ **LCSC stock is 3 pieces.** Not a supply base for a multi-node array.
- ⚠ 25 µg/√Hz is a **white-region** number. Per `01-requirements.md` §2 it does **not** hold at
  1–2 Hz, which is exactly where MASTER §6 operates.

> **Discrepancy found and recorded:** MDPI *Sensors* 2025 quotes ADXL355 noise as 22.5 µg/√Hz.
> The ADI datasheet says **25 µg/√Hz**. Datasheet wins; the disagreement is logged, not hidden.

### B2. ADI ADXL354

Analog-output sibling of the ADXL355. **20 µg/√Hz @±2 g** [DS], ±2/4/8 g.
Quieter on paper, but needs an external ADC + reference per node — added cost, power and noise
that will erase the 5 µg/√Hz advantage. ~$51.30 ⚠️ [UNVERIF].
Datasheet is the same file: `docs/research/MEMS/extracts/adxl355.md`.

### B3. ST IIS2ICLX — **datasheet obtained, specs now first-hand** ✅

`docs/research/MEMS/extracts/ST_IIS2ICLX_datasheet.md` (3.5 MB, supplied by the user 2026-09-17 — st.com blocks
automated access). Every row below is now **[DS]**; the whole table was previously [UNVERIF].

| Spec | Value | Src |
|---|---|---|
| **Noise density** | **15 µg/√Hz typ, 30 µg/√Hz max** | [DS] "An Zero-g noise density" |
| Range | ±0.5 / 1 / 2 / 3 g | [DS] |
| **Axes** | **2 (X and Y only)** | [DS] — confirmed |
| Sensitivity | 0.015 mg/LSB @±0.5 g → 0.122 @±3 g (16-bit) | [DS] |
| Zero-g offset | ±8 mg; ±0.075 mg/°C | [DS] |
| **Active current** | **420 µA** (2 axes, full performance) | [DS] |
| Power-down current | 3 µA | [DS] |
| Supply | 1.71–3.6 V | [DS] |
| **Package** | **CCLGA-16, 5 × 5 × 1.7 mm** | [DS] |
| Temp range | −40 … +105 °C | [DS] |
| ODR | 12.5 / 26 / 52 / 104 / 208 / 416 / 833 Hz | [DS] |
| Bandwidth | 260 Hz @ ODR 833 Hz | [DS] — see `05` D9 |
| Non-linearity | 0.1 % FS | [DS] |
| Extras | **machine learning core + finite state machine**, programmable HP/LP filters, 3 KB FIFO | [DS] |
| Order code | IIS2ICLXTR | [DS] |

**Corrections to the previous [UNVERIF] row:** package was recorded as "LGA-16" — it is
**CCLGA-16, 5 × 5 × 1.7 mm**. Current was recorded only as "3 µA standby", which is the
**power-down** figure; the **active** current is **420 µA**. Noise was recorded as a bare
"15 µg/√Hz" — that is the **typ**; there is also a **30 µg/√Hz max**.

**In-band noise, 10–100 Hz [CALC]** (`a_rms = ND × √90`):

| | Density | 10–100 Hz rms |
|---|---|---|
| IIS2ICLX **typ** | 15 µg/√Hz | **142 µg rms** |
| IIS2ICLX **max** | 30 µg/√Hz | **285 µg rms** |
| ADXL355 typ | 25 µg/√Hz | 237 µg rms |

**This is the one finding that weakens the part.** At its **guaranteed max**, the IIS2ICLX is
*worse* than the ADXL355's typ. The "better noise than the ADXL355" claim holds **typ-vs-typ only**.
It is not a defeat — **ADI publishes no max noise density for the ADXL355 at all**, so the honest
comparison is 15 vs 25 typ (IIS2ICLX wins) or 30 max vs *unknown* max (undecidable). Stated here so
the shortlist is not read as stronger than it is.

**Power:** 420 µA is **2.1× the ADXL355's 200 µA**, and still only **4.7 % of the 9 mA node
budget** (MASTER §4.1). Not a constraint.

**Price — LCSC (C1857737, IIS2ICLXTR), pulled live today ✅ [LIVE]:**
**$26.51 @1 · $25.43 @5 · $24.35 @30 · stock 421 pcs**

**Vendors:**
- LCSC: <https://www.lcsc.com/product-detail/C1857737.html> ✅
- Manufacturer: <https://www.st.com/en/mems-and-sensors/iis2iclx.html> ⚠️ (st.com times out on
  every automated attempt; the datasheet was retrieved by hand)

> ⛔ **ELIMINATED 2026-09-17 on node attitude, after this section was written.** A drone drop
> cannot guarantee attitude; the slant-ray geometry then costs a 2-axis part up to −7 to −10 dB
> **at the far nodes, which TDoA needs most**. See `04` **A8**. The specs below stand and are
> verified — **the part is excluded on geometry, not on merit.** Retained in full because the
> elimination is reversible if the deployment method changes.

**Verdict — the strongest Tier-B candidate on paper, now on verified specs, with one fatal
limitation:**
- ✔ **15 µg/√Hz typ at $26.51 with 421 in stock** — better typ noise than the ADXL355, 42 % of
  the price, 140× the availability. A2's supply problem does not apply to it.
- ✔ 420 µA, 5 × 5 × 1.7 mm, and an **on-chip ML core** that could do node-side event triage
  before the LoRa hop — directly relevant to MASTER §5's bandwidth budget.
- ✔ ST lists **structural health monitoring** among its own applications for the part.
- ✘ **Two-axis.** For a drone-dropped node at unknown, uncontrolled orientation, the missing Z axis
  is the real objection — an arbitrary node attitude projects vertical ground motion onto a plane
  the sensor may barely see. This is now the *only* open objection to the part.
- ✘ Its **max** noise spec is worse than the ADXL355's typ (above).

### B4. Murata SCA3300-D01 — **noise density finally published** ✅

`docs/research/MEMS/extracts/Murata_SCA3300-D01_datasheet.md` (Doc.No. 3165 Rev. 3, 1.6 MB, downloaded from the
exact URL exposed by the user's page source 2026-09-17). **This closes the gap that previously
disqualified the part.**

| Spec | Value | Src |
|---|---|---|
| Axes | 3 (XYZ) | [DS] |
| Supply | 3.0–3.6 V, **1.2 mA** nom | [DS] |
| Interface | SPI | [DS] |
| ODR | 2000 Hz | [DS] |
| Size | 8.6 × 7.6 × 3.3 mm, DFL plastic | [DS] |
| Temp range | −40 … +125 °C | [DS] |
| Offset temp. dependency | ±15 mg (−40…+125 °C) | [DS] |
| Cross-axis sensitivity | ±1 % | [DS] |

**The four operation modes — this is the whole story of the part [DS]:**

| Mode | Range | −3 dB | Sensitivity | **Noise density** | Integrated noise |
|---|---|---|---|---|---|
| **1** (default) | ±3 g | 70 Hz | 2700 LSB/g | **44 typ / 49 max µg/√Hz** | 0.5 / 0.7 mg rms |
| **2** | ±6 g | 70 Hz | 1350 LSB/g | **68 / 76 µg/√Hz** | 0.7 / 1.0 mg rms |
| **3** | ±1.5 g | 70 Hz | 5400 LSB/g | **35 / 40 µg/√Hz** | 0.4 / 0.6 mg rms |
| **4** | ±1.5 g | **10 Hz** | 5400 LSB/g | **35 / 40 µg/√Hz** | 0.15 / 0.2 mg rms |

The low-pass is **1st-order**. Mode 3 is the only mode worth considering here.

**Audit cross-check [CALC] — the two tables agree.** For a 1st-order filter the equivalent noise
bandwidth is `ENBW = (π/2)·f−3dB`. Predicting integrated noise from the density column:

| Mode | `ND × √(1.571 × f−3dB)` | Datasheet | Δ |
|---|---|---|---|
| 1 | 0.461 mg | 0.5 mg | −8 % |
| 2 | 0.713 mg | 0.7 mg | +2 % |
| 3 | 0.367 mg | 0.4 mg | −8 % |
| 4 | 0.139 mg | 0.15 mg | −8 % |

All four consistent. **Two independently specified tables reproduce each other under the correct
noise model — the strongest internal validation of any number in this folder.**

**⚠️ Discrepancy D8 — the front page contradicts the spec table.** Page 1 advertises
*"Ultra-low 37 µg/√Hz noise density."* **37 matches no mode** (44 / 68 / 35 / 35 typ). The value
used throughout this survey is the **spec table's 35 µg/√Hz (Mode 3)**, not the cover figure.
Logged in `05-verification-log.md` D8.

**In-band noise, 10–100 Hz [CALC]:** Mode 3 gives **332 µg rms typ / 380 µg rms max** —
**the noisiest of the three buyable candidates** (IIS2ICLX 142, ADXL355 237).

**The 70 Hz band edge — quantified, and *not* the disqualifier it looks like.** Our band runs to
100 Hz; a 1st-order 70 Hz pole is **−4.8 dB at 100 Hz**. But it attenuates signal and sensor noise
*together*, so analog SNR across the band is preserved and the tilt is recoverable by equalisation —
bounded below by the digital floor. That floor is not binding: Mode 3's 1 LSB = 185 µg, so
quantisation noise is 53.5 µg rms over the 1000 Hz Nyquist span = **1.69 µg/√Hz, ~21× below the
35 µg/√Hz analog noise** [CALC]. **The real cost of the 70 Hz pole is phase distortion across
10–100 Hz, which matters for TDoA (MASTER §7) far more than for detection.**

**Price:** $38.98 DigiKey ⚠️ [UNVERIF — still not re-checked on a live page].

**Vendors and documents** (all ✅ live today, body-inspected for soft 404s):
- Lineup: <https://www.murata.com/en-global/products/sensor/accel/overview/lineup/sca3300> ✅
- Part page: <https://www.murata.com/en-global/products/sensor/overview/item/sca3300-d01> ✅
- **India locale: <https://www.murata.com/en-in/products/sensor/accel/overview/lineup/sca3300>** ✅
- Eval board `SCA3300-D01-PCB`: `/en-global/products/sensor/design-development/sca3300_pcb`
- Distributor inventory: `/en-global/products/sensor/accel/support` · Stock check: `/en-global/support/stock`

**Procurement note — the one place this part beats everything else in the survey.** Murata publishes
an **India locale** (`en-in`, alongside en-us/en-eu/en-sg/zh-cn/ko-kr/ja-jp) with its own distributor
and stock-check path. **Epson publishes no Asia/India distributor at all**, and the ADXL355's India
availability is unconfirmed. For a project sourcing in India this is a real advantage, and it is
orthogonal to the noise numbers.

**Verdict — no longer rejected, but it loses on the merits.** The missing spec is now in hand and it
is unflattering: **35 µg/√Hz is worse than both the ADXL355 (25) and the IIS2ICLX (15), at $38.98 —
more expensive than the IIS2ICLX.** What it genuinely offers, and neither rival does:
- **3 axes** (the IIS2ICLX's one hard limitation),
- **−40…+125 °C** and **mechanical over-damping** — Murata's own stated differentiator, and on a
  rubble field with machinery and falling debris **shock robustness is a real requirement, not a
  brochure line**,
- **an India supply path**.

Per `01-requirements.md` §3, if site ambient dominates in 10–100 Hz then 35 vs 15 µg/√Hz is a
distinction without a difference, and **over-damping plus 3 axes plus buyability in India would make
this the correct choice.** It is the strongest argument yet that A4's ambient measurement is the
decision that matters. **Keep it on the shortlist, gated on that measurement.**

### B5. TDK IIM-46234 — **unverifiable: the vendor's own site is broken**

70 µg/√Hz, 6-axis, 0.3 mA, 23×23×8.5 mm ⚠️ **[UNVERIF — single source, no datasheet obtained]**.
No price found. **Not a candidate until documented.**

**Re-attempted 2026-09-17 and it is not a retrieval failure on this end.** Every path under
`invensense.tdk.com` either returns **HTTP 308 in a redirect loop** (including the bare domain
`https://www.invensense.tdk.com/`) or **HTTP 200 carrying a "Page Not Found" body**. Paths probed:
`/products/iim-46234/`, `/smartindustrial/iim-46234/`,
`/en-us/products/motion-tracking/6-axis/iim-46234`. `product.tdk.com` returns **403**.
The user independently hit the same "Oops! Page Not Found." in a normal browser.

**Conclusion: TDK's InvenSense product namespace appears to be mid-migration and is currently
unreachable by any method available here.** This part cannot be closed from this end; it needs a
datasheet obtained through a distributor (Mouser/DigiKey host their own copies) or a direct TDK
sales contact.

---

## Tier C — Commodity MEMS

### C1. TDK InvenSense MPU-6050

| Spec | Value | Src |
|---|---|---|
| Noise density | **400 µg/√Hz @10 Hz** (AFS_SEL=0, ODR 1 kHz) | [DS] |
| Range | ±2 / 4 / 8 / 16 g | [DS] |
| DLPF | 5–260 Hz | [DS] |
| ODR | 4–1000 Hz | [DS] |
| Supply | 2.375–3.46 V, I²C | [DS] |

**Price:** LCSC bare IC ~$15.58 ⚠️ [UNVERIF]. **GY-521 modules in India: roughly ₹100–200
(~$1–2)** ⚠️ [UNVERIF — not price-checked on a live page; verify at Robu/element14].
**Manufacturer:** ~~`https://invensense.tdk.com/products/motion-tracking/6-axis/mpu-6050/`~~
❌ **DEAD — corrected 2026-09-17.** This was previously tagged ✅ in error. The URL returns
**HTTP 200 with a "Page Not Found" body** (a *soft 404*), which defeated the status-code-only link
check used in the first pass. See `05-verification-log.md` **E9**. The datasheet in
`docs/research/MEMS/extracts/TDK_MPU-6050_datasheet.md` is unaffected — it was obtained earlier and every [DS] row
above still reads from it. **Only the link is wrong, not the specs.**

**Verdict — 16× too noisy for the `01-requirements.md` §7 target of <50 µg rms** (it gives 3.8 mg rms
over 10–100 Hz). **But** it is the only part here that fits the cost model, and per §3 the real
ceiling is site ambient, not sensor noise. **Its correct role is as the throwaway instrument that
measures site ambient** — if ambient in 10–100 Hz turns out to exceed 3.8 mg rms, the MPU-6050 *is*
the answer and this entire survey is moot. That measurement costs ~$2 and settles the argument.

---

## Non-MEMS alternative

### G1. Geospace SM-24 geophone element

| Spec | Value | Src |
|---|---|---|
| Sensitivity | **28.8 V/m/s** | [DS] |
| Natural frequency | **10 Hz** | [DS] |
| Coil resistance | 375 Ω | [DS] |
| Moving mass | 11 g | [DS] |
| Distortion | <0.1 % | [DS] |
| Frequency range | 10 Hz → 240 Hz | [DS] |
| Diameter | Ø25.4 mm | [DS] |
| Power | **passive — zero** | [DS] |
| Computed self-noise, 10–100 Hz | **~32 ng rms** | [CALC] |

**Price — SparkFun SEN-11744, pulled live from the page's own product JSON today ✅ [LIVE]:**
**$69.95 @1 · $66.45 @25 · $62.96 @100**

**Vendors:**
- SparkFun: <https://www.sparkfun.com/geophone-sm-24-with-insulating-disc.html> ✅
- Manufacturer: <https://www.geospace.com/> ✅ (root confirmed; the `/sensors/sm-24/` path 404s —
  navigate from the homepage)

**Verdict — MASTER §3.2 rejects this part for the wrong reason.** The rejection is "10 Hz corner,
unusable here," which is only true under the 0.5–4 Hz assumption that `01-requirements.md` §1
overturns. **This is the exact sensor VitalMon used to measure heart rate through a mattress, and
the exact class PigV² used through a floor.** Two of the three published successes in this folder
used a geophone.

Real objections that remain: **1-axis**, **11 g moving mass** (orientation-sensitive, and heavy for
an 8 g node), **passive output needs a <2.5 nV/√Hz preamp + ADC per node**, and **$70 each**.
It is not obviously the right node sensor — but the stated reason for rejecting it is wrong, and
that needs correcting in MASTER.

### R1. Raspberry Shake RS1D / RS4D

A packaged geophone + 24-bit digitiser + Pi seismograph. Specs in
`docs/research/MEMS/extracts/RaspberryShake_technical_specifications.md`. Pricing not confirmed ⚠️ (~$500+ [UNVERIF]).
**Vendor:** <https://raspberryshake.org/> ✅

**Recommended purchase — not as a node, as the instrument that answers
`01-requirements.md` §8.1.** It gives calibrated ground-motion PSD on a real site, which is the
measurement every remaining decision depends on.

---

## What this survey did not resolve

| Gap | Why it matters | How to close it |
|---|---|---|
| ~~ST IIS2ICLX datasheet~~ | ✅ **RESOLVED 2026-09-17** — supplied by the user; B3 is now fully [DS] | — |
| ~~Murata SCA3300 noise density~~ | ✅ **RESOLVED 2026-09-17** — 35/40 µg/√Hz Mode 3, from Doc.No. 3165 Rev. 3 | — |
| TDK IIM-46234 | Vendor site 308-loops or soft-404s on every path | Get the datasheet via Mouser/DigiKey or TDK sales |
| TDK IIM-46234 | Single-source spec, no price | Datasheet + distributor quote |
| Epson M-A352 / M-A370 real price | €999 is one source; M-A370 has none | Quote via Digi-Key/Mouser (Americas) or Texim/Amcoris (EMEA) — **no India distributor exists** |
| ADXL355 India availability | Affects the whole procurement plan | Browser check at element14 IN / Robu |
| Colibrys SI1003 price | Quote-only | Safran sales enquiry |
| Raspberry Shake pricing | It is the recommended buy | raspberryshake.org store |

---

*Back to [README](README.md) · Prev: [01 — Requirements](01-requirements.md) · Next: [03 — Literature](03-literature.md)*
