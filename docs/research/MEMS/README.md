# MEMS Sensor Research — Heartbeat In The Rubble


> ## ⛔ SUPERSEDED PREMISE — 2026-10-08
>
> **This pass selected a sensor for detecting a buried survivor's heartbeat. That target is
> disproven.** The cardiac signal sits **38–60 dB below the ADXL355 floor** (25 µg/√Hz) this pass
> selected — **not** below the SM-24 floor the next paragraph reverses to; see the note below — at
> 3 m, and the source force is now *measured* (3.7 N Starr 1939; 4.06 N Inan 2009; 2 N_pp Ashouri
> 2016), so no filter, averaging scheme or model recovers it.
>
> **The sensor conclusion is also reversed.** This pass marked the **ADXL355** FIXED and rejected the
> **SM-24 geophone** because its 10 Hz corner sits above the target band — true only of the *wrong*
> band. The band error (0.5–4 Hz, a *repetition rate*, not a *signal bandwidth*) caused the sensor
> error. The SM-24 is the selected sensor and the ADXL355 cannot do the
> job: every tap case is buried on the ADXL355 (−7 to −25 dB) and detected on the SM-24 (+23 to
> +41 dB).
>
> **What is still good here:** the noise-density survey, the vendor register, the requirements
> arithmetic, and the extracts — which are the only in-repo record of figures whose PDFs are
> gitignored. Read the numbers; ignore the conclusion.
>
> **Which floor the 38–60 dB is measured against — added 2026-10-11.** That figure is an
> **ADXL355** number: `00b-verification-arithmetic.md:26` derives it from the 47–69 dB ADXL355
> deficit plus the 8.75 dB worst-healthy-subject force correction, and `07-verdict.md:69` states
> the parent figure as *"47-69 dB below the ADXL355 floor."* **It is not a geophone figure.**
> Against the SM-24 selected below, the deficit is far smaller, and against the SM-24's *element*
> floor the cardiac signal is **positive**. The heartbeat premise still dies — by ~31–53 dB after
> propagation (`00b:73`) — but it dies on the propagation path, **not** on geophone self-noise.
> Do not quote 38–60 dB against any sensor but the ADXL355.
>
 ⚠ **The band is superseded too — ADR 0001, 2026-10-11.** This marker was written 2026-10-08, three
> days before the band was settled, so it reverses the premise and the sensor but **not the band**.
> **None of 0.5–4 Hz, 10–100 Hz, 5–40 Hz or 60–80 Hz is the project's position:** 5–40 Hz came from
> **seismocardiography** literature (a cardiac band, for the dead premise) and 60–80 Hz is *"NO DATA
> FOUND"*. **Acquire 5–200 Hz; the detection band is an output of the M1/M2 bench measurement.**
> Where one figure is unavoidable: `20–80 Hz [ASSERTED — pending M2]`. The margin figures do not move
> on any band (`00b-verification-arithmetic.md:85-95`).
>
> Authority: `docs/critique/07-verdict.md` → `08-amendment.md` → `docs/critique/prior-art/`.

Research pass completed **2026-09-17**. Scope: what sensor this project actually needs, what exists
that meets it, what it costs and where to buy it, and what the literature says about detecting a
heartbeat through a structure.

> ⏱️ **Prices in this folder were captured 2026-09-17 and have since moved 8–16 %.** The current
> figures live in **[../BUDGET/](../BUDGET/)** (re-pulled 2026-10-06). Specs and physics here are
> unaffected; **only the money is stale.**

**21 primary sources downloaded** (15 datasheets, 6 papers), all read, every number audited twice.

---

## Read this first — three findings that change the project

### 1. The detection band is wrong ⛔

MASTER §6 bandpasses **0.5–4 Hz**. The two published systems that have actually recovered heartbeats
through a solid structure both work at **10–100 Hz**:

- **PigV²** — *"heartbeats are detected through peak picking over the sum of wavelet coefficients
  from 10 to 100 Hz... the typical heartbeat-induced vibration frequency range (0-100 Hz) and the
  sensitivity range of the sensors (≥10 Hz)."*
- **VitalMon** — heart rate to **1.90 BPM mean error** using a geophone that is *"naturally a
  second-order high-pass filter... natural frequency is 10 Hz."*

A heartbeat in a structure is an **impulse train**, not a tone. The energy is ≥10 Hz; 1–2 Hz is the
repetition rate, recovered from the **envelope**. The current filter discards the signal.

Independently: MEMS noise specs are white-region figures. Sercel, on their own part —
*"<15 ng/sqrt(Hz) above 10Hz"*, *"1/f noise at low frequency not characterized."*

**With one exception.** The **Epson M-A370AD10** specs **0.02 µG/√Hz over 1–10 Hz**, *"surpassing
the USGS New High Noise Model."* So the low band is reachable — at **36.3 mA and 29 g**, against a
9 mA / 8 g node. The accurate statement is not *"1–2 Hz is impossible"* but *"1–2 Hz needs a sensor
this node cannot power or carry, and every sensor it can carry is uncharacterised there."*

→ `01-requirements.md` §1–2 · `04-action-report.md` A1

### 2. The ADXL355 costs far more than $15 ⛔

MASTER §9 prices it at ~$15. On 2026-09-17 it was **$63.26 @1**; **re-pulled 2026-10-06 it is
$55.1592 @1** (−12.8 % in 19 days). Either way **MASTER §9 is wrong by 3.7–4.2× on this line.**

> ⚠️ **Updated 2026-10-06.** The stock claim that was here — *"LCSC stock is 3 units, you cannot
> buy them"* — **is no longer true**: stock is now **486 + 1192**. **The price error stands; the
> supply problem has resolved.** Current BOM: **[../BUDGET/03-budget.md](../BUDGET/03-budget.md)**.

→ `02-sensor-survey.md` B1 · `04-action-report.md` A2 · `../BUDGET/04-verification-log.md` D11

### 3. Sensor noise is probably not the binding constraint at all ⚠️

Sercel measured their MEMS as **ambient-limited above ~2 Hz** — in a soundproof chamber, on an
isolation platform. A rubble field has machinery, generators, crews and wind. Site ambient in
10–100 Hz will swamp every sensor self-noise figure in this folder.

If that holds, the ADXL355's 25 µg/√Hz buys nothing over a **$2 MPU-6050**, and the right lever is
**node count** (~√N gain against incoherent noise), bought with cost per node. Nof et al. is the
precedent: mini-arrays of low-cost MEMS with a <US$150 DAQ, solving back-azimuth for real
earthquakes.

**The cheapest decisive test in the project: a ~$2 MPU-6050 module and one evening recording
ambient on a demolition site.** It either justifies the $63 part or eliminates it.

→ `01-requirements.md` §3 · `04-action-report.md` A4

---

## Index

| Doc | Contents |
|---|---|
| **[01 — Requirements](01-requirements.md)** | What the signal is, the 1/f problem, the ambient ceiling, noise-budget math, the geophone comparison, propagation conflict, derived spec, what must be measured |
| **[02 — Sensor Survey](02-sensor-survey.md)** | 15 parts across 4 tiers. Full specs, **prices, vendor links, per-row verification status** |
| **[03 — Literature](03-literature.md)** | 6 papers, annotated: what each proves, what applies here, what does not |
| **[04 — Action Report](04-action-report.md)** | A1–A7 ranked changes to MASTER.md + recommended sequence |
| **[05 — Verification Log](05-verification-log.md)** | Two audit passes per finding, discrepancies, tooling failures, source provenance, honest limits |
| **[06 — Build vs Buy](06-build-vs-buy.md)** | Should we develop our own sensor? Three levels, why all three lose to ambient, the hybrid tiered array costed, **and what to build instead** |

## Folders

| Path | Contents |
|---|---|
| `extracts/` | **18 full-text Markdown extracts** — **12** manufacturer datasheets (Epson ×3, ADI, Colibrys, Sercel ×2, Geospace, Raspberry Shake, TDK, **ST**, **Murata**) plus **6 research papers**. **The source PDFs were converted and deleted 2026-10-08** (`*.pdf` is gitignored project-wide), so these extracts are the **only in-repo record** of their figures |
| | plus 6 research papers — SenSys'17, PigV², EGU2018, Evans 2014 SRL, Nof 2019, USGS OFR 2005-1438. **The source PDFs were converted and deleted 2026-10-08** (`*.pdf` is gitignored project-wide; third-party material is not ours to redistribute). The extracts are the only in-repo record. |

---

## The shortlist

| Part | Noise (10–100 Hz) | Price @1 | Verdict |
|---|---|---|---|
| ~~**ADI ADXL355**~~ | 237 µg rms | $63.26 *(captured 2026-09-17; **$55.1592 on 2026-10-06**, −12.8 %)* | ⛔ **REJECTED** — MASTER's *former* pick. Power/size excellent, but 38–60 dB short on the cardiac premise. ~~stock 3~~ **stock resolved to 486 + 1192 on 2026-10-06** (`../BUDGET/04` A22) |
| ~~**ST IIS2ICLX**~~ | 142 µg rms typ / 285 max | $26.51 ✅ live | ⛔ **ELIMINATED — 2-axis.** Specs verified and excellent; the slant-ray geometry costs it −7 to −10 dB at the far nodes. `04` A8 |
| **Murata SCA3300-D01** | 332 µg rms (Mode 3) | $38.98 ⚠️ | ✅ **Noise density finally published: 35 µg/√Hz.** Noisiest buyable part — but 3-axis, mechanically over-damped, and **the only candidate with an India supply path** |
| **TDK MPU-6050** | 3795 µg rms | ~$2 module | 16× too noisy on paper — **and the right instrument for the ambient test** (vendor link dead, specs unaffected) |
| **Geospace SM-24** | ~0.032 µg rms | **$69.95** ✅ live | Quietest by ~77 dB. 1-axis, 11 g moving mass, needs a preamp |
| **Epson M-A370AD10** | 0.06 µg rms **@1–10 Hz** | quote only | **Specs 0.02 µG/√Hz at 1–10 Hz, below the USGS NHNM.** 36.3 mA and 29 g — 4× the node's whole budget |
| **Epson M-A352AD10** | 1.9 µg rms | ~€999 ⚠️ | Specced down to 0.5 Hz. 13.2–20 mA and 25 g — unusable in this node |
| **Colibrys SI1003** | 6.6 µg rms | quote only | 8 µg integrated 0.1–100 Hz — rare honest low-f spec. 27 mA kills it |

Full specs, vendor links and per-number verification status: **[02 — Sensor Survey](02-sensor-survey.md)**.

---

## What this research does **not** establish

- **No paper exists on heartbeat detection through rubble.** The literature covers beds, floors and
  chairs — benign, short-path, low-noise media. Extrapolating to fractured debris is unvalidated,
  and that gap is this project's actual contribution.
- **MASTER §10.1 (detection range) is not closed.** It cannot be closed by reading.
- **Six of eleven price points are single-source** because DigiKey, Mouser, Robu, element14 IN,
  Epson and Safran all block automated access. They are tagged ⚠️ **[UNVERIF]** throughout and
  nothing was invented to fill the gaps.
- **The geophone noise figure is my own calculation**, not a published or measured number.

All limits stated explicitly in **[05 — Verification Log](05-verification-log.md)** §G.

---

## Conventions

**[DS]** datasheet extract in `extracts/` · **[PAPER]** paper extract in `extracts/` ·
**[CALC]** my arithmetic from tagged inputs · **[LIVE]** pulled from the vendor page's own price
payload today · **[UNVERIF]** single-source, do not trust ·
✅ link returned HTTP 200 **and its body was inspected for soft-404 markers** today ·
⚠️ bot-blocked, canonical URL unconfirmed · ❌ confirmed dead

> **A note on ✅.** In the first pass ✅ meant *status code 200 only*. That was not sufficient —
> one link (TDK MPU-6050) returned 200 while serving a "Page Not Found" page. As of 2026-09-17
> every ✅ in this folder has had its **response body** checked for soft-404 markers. See
> `05-verification-log.md` **E9**.
