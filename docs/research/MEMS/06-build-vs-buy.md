# 06 — Build vs Buy: should we develop our own sensor?

Written 2026-09-17, in answer to a direct question. Short version: **no — and the reason is not
that it's hard, it's that it optimises the wrong variable.** The thing worth building is the
**coupling interface**, not the transducer.

---

## 1. Three things "develop our own sensor" could mean

They are not variations of one project. They are three different projects with three different
verdicts.

| Level | What it means | Verdict |
|---|---|---|
| **L1** | Design and fabricate a MEMS die | ⛔ **Dead.** Wrong by 2–3 orders of magnitude and 3–5 years |
| **L2** | Custom readout electronics around a bare MEMS die | ⛔ **Dead.** Re-implements trimmed silicon, worse |
| **L3** | Custom non-MEMS transducer chain — **geophone + low-noise AFE** | ⚠️ **Real, and genuinely tempting. Wrong for *this node*, right for a *listening post*** |

---

## 2. L1 — fabricating a MEMS die ⛔

| | Reality |
|---|---|
| Route | Multi-project wafer run: MEMSCAP PolyMUMPs, X-FAB, Silex, Teledyne DALSA |
| Cost | ~$10–20k **per iteration** |
| Turnaround | 12–16 weeks **per iteration**, and first silicon is never right |
| What you get | **Unpackaged dies.** Vacuum packaging sets Q, hence thermomechanical noise — it is a separate, harder problem |
| Readout | Needs a trimmed capacitive-to-voltage ASIC. This is what ST/ADI/Murata do at wafer level |
| Realistic first-silicon noise | **mg/√Hz range — 100–1000× worse than a $26 IIS2ICLX** |

A commercial MEMS accelerometer is decades of process development and wafer-level trim sold for
$26. **This is a doctoral research programme, not a project subsystem.** It is out of scope by a
margin that no amount of effort closes.

## 3. L2 — custom readout around a bare die ⛔

Same objection, smaller. You would re-implement the capacitance-to-voltage converter that the
manufacturer already trims per-die at wafer level — but on a PCB, with worse parasitics, worse
matching and no trim. **There is no version of this that beats the integrated part.**

---

## 4. L3 — geophone + custom low-noise front end ⚠️

**This is the one that deserves a real answer, because the evidence points at it.**

### Why it is tempting

- **Both working heartbeat-through-structure systems in `extracts/` used geophones, not MEMS.**
  VitalMon achieved **1.90 BPM mean error with an SM-24** — the exact part already surveyed in
  `02` G1. PigV² used the same class.
- **~0.001 µg/√Hz**, ≈32 ng rms integrated over 10–100 Hz [CALC] — **~77 dB below the ADXL355.**
- The transducer is passive and costs **zero power**.
- MASTER §3.2 rejected geophones on the 10 Hz corner, and **`04` A3 already showed that rejection
  is invalid** — 10 Hz is the *edge* of the real band, not above it.

So the literature, the noise physics and this folder's own corrections all point the same way.
Then you budget it.

### Why it breaks this node

| | Custom 3-axis geophone node | SCA3300 node | Over by |
|---|---|---|---|
| **Mass** | ~260 g — 3 × SM-24 at **74 g each** [DS] + AFE + shielding | ~8 g | **32×** |
| **Current** | ~19–31 mA — 3 preamp channels + 24-bit ADC | ~1.2 mA | **2–3.4×** |
| **Cost** | **~$259/node → $2,330 for 9** | $52.98 → $477 | **4.9×** |

Preamp options, all of which must beat the SM-24's own **2.46 nV/√Hz** Johnson noise [CALC] or
they throw the geophone's advantage away:

| Part | Noise | Current | 3 channels |
|---|---|---|---|
| LT1028 | 0.85 nV/√Hz | 7.6 mA/ch | 22.8 mA |
| AD8429 | 1.0 nV/√Hz | 6.7 mA/ch | 20.1 mA |
| OPA1612 | 1.1 nV/√Hz | 3.6 mA/ch | 10.8 mA |

Plus a 24-bit Σ-Δ ADC (ADS1256 class), ~8 mA. **Against a 9 mA whole-node budget.**

### And the datasheet ends the argument for a *dropped* node

> **SM-24: "Maximum tilt angle for specified Fn — 10°"** [DS]

A geophone is a **gravity-referenced spring-mass**. Outside ±10° of vertical it no longer meets its
own natural-frequency spec — the restoring force is wrong. This is categorically different from a
MEMS part, which merely loses a **projection** when tilted and remains a calibrated instrument.

**The stated usable landing range is ±30°. That is 3× outside what the transducer tolerates.**
A drone-dropped geophone is not a degraded geophone; it is an uncalibrated one.

---

## 5. The argument that settles all three

**You cannot beat ambient noise by building a sensor.**

Sercel measured their own MEMS as **ambient-limited above ~2 Hz** — in a soundproof chamber, on an
isolation platform, in a basement (`03` §3). A rubble field has machinery, generators, crews and
wind. Site ambient in 10–100 Hz will exceed **every self-noise figure in this folder, the
geophone's included.**

If the site is ambient-limited, a 0.001 µg/√Hz transducer and a 35 µg/√Hz one **record the same
thing.** The 77 dB is invisible.

**Developing a sensor means spending the hardest engineering in the project on a variable that
`04` A4 says is probably not binding — before the ~$2 measurement that would settle whether it is
binding at all.** That is the whole argument, and it applies to L1, L2 and L3 equally.

### The two regimes, and why only one of them is fixable by an array

| Regime | Binding constraint | The lever | Does a geophone help? |
|---|---|---|---|
| **Ambient-limited** (likely) | Site noise | **Node count (√N) + coupling** | **No — it buys nothing** |
| **Self-noise-limited** (unlikely) | Sensor floor | Sensor quality | **Yes, and nothing else does** |

Coherent stacking against incoherent ambient gives √N amplitude gain:

| N nodes | Gain |
|---|---|
| 4 | 6.0 dB |
| 9 | 9.5 dB |
| 12 | 10.8 dB |
| 16 | 12.0 dB |
| 25 | 14.0 dB |

**To match the geophone's 77 dB by node count alone you would need N ≈ 5 × 10⁷ nodes** [CALC].
So the two regimes are genuinely exclusive: **if self-noise is binding, no affordable array
substitutes for a better sensor; if ambient is binding, no better sensor substitutes for more
nodes.** One measurement tells you which world you are in. Nothing else does.

---

## 6. What is actually worth building

### 6.1 The coupling interface — **this is the real project** ⭐

Per `04` A7, **coupling loss is likely larger than every sensor difference in this folder.** A
drone-droppable anchor that genuinely mates a node to fractured, air-gapped debris is:

- **unsolved** — no paper was found on heartbeat detection through rubble at all,
- **the dominant term** in the link budget,
- **this project's actual contribution.**

**And it collides head-on with the attitude requirement.** Good coupling wants a spike or a flat
mated face pressed into debris. Self-righting wants a rounded, weighted, tumbler base — which
gives rocking point contact, the worst possible coupling. **That conflict is the design problem
worth solving, and it is why the 3-axis sensor is the right call:** it lets the node land in
whatever shape couples best, and recovers attitude afterwards from the DC gravity vector instead
of demanding a shape that rights itself.

### 6.2 The hybrid tiered array — the right answer *if* sensitivity turns out to matter

If the ambient measurement says self-noise **is** binding, the answer is still not a custom
transducer. It is to put the geophone where its constraints are free:

- **Perimeter listening posts** — hand-planted at the rubble edge where a person can safely reach.
  Planted means **vertical**, so the ±10° spec is met. No mass limit, no drop shock, and mains or a
  large battery, so the 20–30 mA AFE is free.
- **Interior nodes** — many cheap drone-dropped MEMS units across the field, where only node count
  and coupling matter.

This matches the **Evans Class A/B/C tiering** already in `extracts/evans.md`, and it is how real seismic
arrays are actually built.

**Costed** (interior node = SCA3300 at $52.98; non-node system cost $380–880 from `04` A2):

| Post type | Build | Cost each |
|---|---|---|
| **1-C** (vertical only) | SM-24 $69.95 + preamp $5 + 24-bit ADC $18 + MCU/LoRa $14 + enclosure/spike/battery $15 | **$121.95** |
| **3-C** (full vector, back-azimuth capable) | 3 × SM-24 $209.85 + 3-ch preamp $15 + ADC $18 + $14 + $15 | **$271.85** |

| Config | Composition | Hardware | System total |
|---|---|---|---|
| **A** | 9 MEMS nodes *(current plan)* | $477 | **$857–1,357** |
| **B** | 4 × 1-C post + 9 nodes | $965 | $1,345–1,845 |
| **C** | 4 × 3-C post + 9 nodes | $1,564 | $1,944–2,444 |
| **D** | 3 × 1-C post + 12 nodes | $1,002 | $1,382–1,882 |
| **E** | 2 × 3-C post + 12 nodes | $1,179 | $1,559–2,059 |

**B and D are the interesting ones.** Both roughly double hardware cost and both keep the Delsar
comparison (~$15,000) intact by a wide margin. **D is probably the better buy:** it spends the
extra money on *more interior nodes* as well as posts, hedging both regimes at once — √N gain if
ambient-limited, geophone sensitivity if not.

**None of these should be bought before the ambient measurement.**

### 6.3 The one narrow "build our own" that survives

**A custom low-noise AFE for a geophone listening post** — preamp <2.5 nV/√Hz plus a 24-bit
Σ-Δ ADC. It is:

- bounded, well-understood analog design, not research,
- built on a part already surveyed and priced (`02` G1),
- free of every constraint that killed it as a node — **no mass limit, no power limit, no drop
  shock, and planted vertical so the 10° tilt spec is met.**

**That is the build worth doing — conditional on the ambient measurement saying sensitivity is
binding.** It is L3 applied where L3 works.

---

## 7. Decision

| | |
|---|---|
| **Develop a MEMS sensor (L1/L2)?** | **No.** Wrong by orders of magnitude; not recoverable with effort |
| **Develop a geophone node (L3)?** | **No.** 32× mass, 2–3.4× power, 4.9× cost, and **3× outside its own tilt spec** when dropped |
| **Develop a geophone *listening post*?** | **Conditionally yes** — if and only if the ambient measurement says self-noise is binding |
| **Develop the coupling interface?** | **Yes. This is the highest-value engineering in the project** and nobody has published it |
| **Buy the node sensor?** | **Yes** — 3-axis, per `04` A4, gated on the same measurement |

**Everything routes through the same ~$2 measurement.** That remains the cheapest decisive test in
the project, and this document does not change it — it widens what the measurement decides.

**No ADR proposed.** Per `CLAUDE.md`, ADRs are for irreversible, cross-cutting or contested
decisions. L1/L2 are not contested — they fail on arithmetic. L3-as-listening-post is deferred, not
decided. **If the hybrid array is adopted after the ambient measurement, that is an ADR** — it is
cross-cutting (cost, deployment method, DSP, mesh topology, and it changes what the drone is for).

---

*Back to [README](README.md) · Prev: [05 — Verification Log](05-verification-log.md)*
