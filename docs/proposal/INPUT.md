# Proposal input pack

**For:** `@tadiPro250`, drafting the faculty funding proposal.
**From:** the verified engineering record in `docs/critique/`.
**Date:** 2026-10-08. **Status of the underlying work:** pre-code, no hardware.

Mapped section-by-section onto `Research proposal format.docx`. Every figure here is tagged
**[MEASURED]** (someone measured it and published it), **[COMPUTED]** (derived here from measured
inputs, arithmetic independently reproduced twice), or **[ASSERTED]** (assumed, not yet verified —
**never state these as fact in the proposal**).

> **Read this first.** The project's original premise — detecting a buried survivor's **heartbeat** —
> is **disproven**. Do not write the proposal around it. The surviving project detects **tapping and
> voice from a responsive survivor**, and the dead premise becomes a *published negative result*,
> which is an asset in a research proposal rather than a loss. `docs/MASTER.md` still describes the
> old premise and carries a banner saying so; it is not the authority.

---

## Project title

Suggested: **"Air-deployed seismic sensor mesh for locating responsive survivors in collapsed
structures: array extent, coupling onto debris, and the limits of cardiac detection."**

Covers all three contributions: the capability claim (array extent), the measurement gap (coupling
onto rubble), and the negative result (cardiac bound).

---

## ABSTRACT (1 page, lay language)

Narrative, in plain English, in this order:

1. After a building collapses, rescuers find survivors mainly by **calling out and listening** — a
   procedure called "All Quiet," signalled site-wide by one long blast, run roughly once per hour.
   [MEASURED — FEMA US&R doctrine, read in full]
2. The instruments that help them are **6-to-8-sensor, cable-tethered listening devices whose output
   a trained operator interprets through headphones.** They work, but a human must sit on an unstable
   pile and move them from place to place — "an iterative move-and-listen procedure which is
   time-consuming" in the literature's own words. [MEASURED]
3. **What bounds their accuracy is how few sensors you can place and how far apart.** The closest
   published system names "the limited spatial extension of the sensor array" as one of its own three
   limitations. [MEASURED — Arosio et al. 2010]
4. **Our proposal:** drop many cheap sensor nodes from a drone, so the array can be larger and denser
   than hand placement allows, and locate taps automatically instead of by ear.
5. **We also settle a question the field has left open.** It is widely believed — including in fire
   service writing — that such sensors might pick up "even the vibration of a heartbeat." We show by
   measurement and calculation that this is **impossible by 38–60 dB**, and publish that bound so
   others stop designing toward it.

**Do not promise** survivor detection in unresponsive patients, heartbeat sensing, or a map pin on a
person. The honest output is **DETECTED / NO DETECTION / BLIND, per 2–5 m cell.**

---

## Q1 — Objectives, research questions, hypothesis (1 page)

### Research questions

- **RQ1 (capability).** Does air deployment lift the array-extent limit that bounds existing
  microseismic survivor location, and by how much in localization accuracy?
- **RQ2 (measurement gap).** How does an air-dropped sensor node couple to **collapsed structural
  debris**? All published air-deployment work characterises **soil**, parameterised by soil
  compression strength. Debris is not soil: it is voided, rebar-laced, non-penetrable in large
  fractions, dust-covered. **No characterisation on debris was located.**
- **RQ3 (bound).** What is the true detectability limit for a **cardiac** seismic source through
  rubble, and for a **tap**? Publish both as bounds.
- **RQ4 (the unsolved problem).** Does requiring a candidate to **persist across repeated All Quiet
  windows** convert an unusable false-alarm rate into a usable one?

### Hypotheses

- **H1.** Tap and voice from a responsive survivor exceed a geophone's noise floor by **+23 to
  +41 dB** at relevant ranges. [COMPUTED]
  > ⚠ **These margins are conservative by ~6.5 dB** after the 2026-10-08 anchor correction
  > (19 Hz → 40 Hz, full text of *JASA* 120(2):762). They are **deliberately not restated**, because
  > they also scale off a tap force that is still [ASSERTED] with no source. See the
  > *Anchor correction* note in `docs/critique/00b-verification-arithmetic.md`. **Quote the figures
  > as written here**; do not substitute the improved ones until the bench measurement lands.
- **H2.** Cardiac signal sits **38–60 dB below** the same floor and is unrecoverable by any filter,
  averaging scheme or learned model. [COMPUTED from MEASURED source forces]
- **H3.** Localization accuracy is bounded by **node position uncertainty**, not clock error.
  **Write this as an error-budget conclusion citing GDOP** — it is textbook, and presenting it as a
  discovery would read as a literature gap.
- **H4.** Persistence across silences raises positive predictive value from **~16 % to 70–98 %**.
  [COMPUTED, **unmeasured** — this is a proposal deliverable, not a result]

### Prior art to cite and distinguish *in this section*

The template has no literature-review section, so prior art belongs here and in Q4. **Concede these
explicitly** — a proposal that cites and distinguishes them is far stronger than one a reviewer
catches omitting them:

| Work | What it establishes | How we differ |
|---|---|---|
| **Arosio et al. 2010**, *Near Surface Geophysics* 8(6):623–633, DOI 10.3997/1873-0604.2010051 | Hand-placed microseismic array on real rubble locates survivors; accuracy "within the limit of the seismic resolution"; 3× faster than incumbents; rubble velocity 200–600 m/s measured | **Closest prior art.** We lift the array-extent limitation it names |
| **FEMA US&R doctrine** | Tapping/voice is the existing target: "Victim must create a recognizable sound pattern" | We do not claim the retarget as novel |
| **INACHUS** (EU FP7 607522, 20 partners) | Stated the automated-knock-localization goal | Goal published; **no peer-reviewed accuracy result located.** Do not claim novelty; do not assert they achieved it |
| **Stewart et al., SEG 2016**; **SeismicDart** (Sudarshan et al.) | Drone-landed and air-dropped geophones work in **soil** (ρ = 0.81–0.98 vs planted) | Rubble, not soil; mesh scale, not 4/sortie |
| **HeartQuake**, Park et al. 2020, DOI 10.1145/3411843 | Full ECG morphology through a mattress **from an SM-24 geophone element** — the part we select | **Must cite.** Contact-coupled through bedding, not metres of rubble. A reviewer who finds this unaided will read it as contradicting our bound |
| **Sabatier & Ekimov 2008**, Proc. SPIE 6963, 69630V, DOI 10.1117/12.785235 | Already a signal-equals-noise range bound for footsteps | Direct methodological ancestor of our bound |

---

## Q2 — Methods of investigation and techniques of analysis (1 page)

**Sensor.** SM-24 geophone, 10 Hz corner, 28.8 V/m/s, 375 Ω, 74 g. [MEASURED — datasheet]
**Band 5–40 Hz** for tap, 200 Hz–3 kHz for voice.

> **The one error worth explaining in the proposal**, because it motivates the method: the original
> design bandpassed **0.5–4 Hz**, reasoning that a heart beats 60–120 bpm. But that is the
> **repetition rate**, not the **signal bandwidth** — a beat is a broadband impulse with a
> ~50–150 ms rise. The filter kept the rate and discarded the signal. Correcting it also reverses the
> original sensor choice, because timing precision scales as **σ_t ≈ 1/(B·√SNR)**: narrowing the
> filter makes localization *worse*. This is a clean, teachable methodological point.

**Analysis techniques**, each named with its standard reference:

- **Linear transfer-mobility scaling** to predict amplitude from source force (FTA ground-borne
  vibration method; ASTM/FHWA impulse-response mobility spectrum). Elastodynamics is LTI, so response
  is linear in force. **Do not** scale by energy (factor-2 dB error) and **do not** invoke seismic
  moment (defined for internal sources, not a body pressing on a surface).
- **Cramér–Rao lower bound** for timing precision (Van Trees 1968; Quazi 1981, IEEE ASSP 29(3):527).
  The rigorous bandwidth term is **RMS bandwidth**, not the −3 dB width.
- **TDoA multilateration**, with **GDOP** as the stated framework for geometry-to-error amplification.
- **Johnson-noise analysis** of the geophone: e_n = √(4 k_B T R), v_n = e_n/S, a_n = 2πf·v_n.
- **Binomial persistence detection**, P(≥ k of n) looks, threshold as a *fraction* of available
  looks.

**Bench programme, in dependency order** (nothing here needs the drone):

1. **Measure the ambient in-band floor first.** If it exceeds ~1 mg, the premise fails at any sensor
   price, because no filter removes in-band noise. **Cheapest possible kill — run it first.**
2. **Measure tap force and tap spectrum.** Currently [ASSERTED] at 50–300 N / 60–80 Hz with **no
   source**; the nearest literature anchors are destructive (karate chop ~2,800 N) and were rejected
   rather than laundered as measured. **Every margin in the design scales off these two numbers.**
3. Tap detection at 1 / 3 / 10 m, then repeated **with an excavator running** — the false-alarm test.
4. **Coupling of a free-laid and air-dropped node onto fractured debris** (RQ2), including contact
   resonance. Krohn (1984), DOI 10.1190/1.1441700, measures coupling resonances at **100–500 Hz**; a
   100 Hz resonance sits only 1.25× above an 80 Hz tap, so it is **in band** and distorts amplitude
   *and phase* — which hits TDoA, not just detection.
5. Mesh time sync, then air deployment and node self-localization.

---

## Q3 — Specific activities and timeframe (1 page)

12 months, ordered so each kill-risk is tested before the money that depends on it is spent.

| Months | Activity | Gate |
|---|---|---|
| 1–2 | Ambient in-band floor survey; tap force/spectrum characterisation; preamplifier design | **Go/no-go.** Floor > ~1 mg or tap force far below assumption stops the project cheaply |
| 2–4 | Single-node signal chain: geophone + preamp + ADC; bench detection at 1/3/10 m | Detection margin confirmed against [COMPUTED] prediction |
| 4–6 | Coupling onto debris (RQ2); free-laid vs planted vs dropped | First publishable result |
| 5–8 | Mesh: time sync, TDoA solver, persistence detector; false-alarm test with machinery | PPV measured, H4 tested |
| 7–10 | Air deployment: drop mechanism, node survival, **landing-position scatter** | Node position error budget closed |
| 9–11 | Field trial on a rubble pile; accuracy vs Arosio's benchmark | RQ1 answered |
| 11–12 | Write-up: capability paper + the cardiac bound as a negative result | Deliverables |

**Sequencing note for the reviewer:** the two cheapest experiments can **falsify the project in
month 1**. That is deliberate.

---

## Q4 — If this is a new line of inquiry, why (½ page)

It is a new line for this group, and the justification is the **gap named by the prior art itself**:

- Arosio et al. 2010 established microseismic survivor location on rubble and named **limited array
  extent** as a limitation. Hand placement is what causes it. **We remove the cause.** Prior art
  states the constraint; our mechanism lifts it. This is a *capability* argument, which is stronger
  than a cost argument.
- **Nobody has characterised sensor coupling onto collapsed debris.** All air-deployment work is
  parameterised by soil strength. This is a genuine, narrow, measurable gap.
- **The negative result is itself a contribution.** The cardiac detection bound has never been
  published; the belief that it might work persists in practitioner literature. A rigorous bound
  saves other groups the same dead end.
- **Indian deployment context:** the NDRF "Human Life Detector Type-I" specification contains **no
  automated-localization requirement at all** — a documented capability gap in the procuring agency's
  own words.

---

## Q5 — Anticipated products (½ page)

- **Publications.** (i) Air-deployed array extent and localization accuracy on rubble. (ii) **The
  cardiac seismic detection bound** — a negative result, publishable on its own. (iii) Possibly
  coupling onto debris as a short measurement paper.
- **Presentations.** Near-surface geophysics and USAR technology venues; the Arosio line of work sits
  in *Near Surface Geophysics* and EAGE.
- **Outside funding.** A measured coupling-and-accuracy result is the precondition for any
  NDRF/NDMA-facing or agency proposal; this project is deliberately scoped as the evidence that makes
  that application credible.
- **Patents.** **Do not claim one.** Air deployment of seismic sensors is already published
  (SeismicDart, Stewart et al.); a patent claim would be read as a literature gap. Say so plainly.

---

## PROPOSED BUDGET

Rupees, five template categories, FX **₹84/USD** (state the rate and its date in the proposal).
Bottom-up from the per-node bill of materials. Prices captured **2026-10-07**; note that this
project's own prices **drifted 8–16 % in 19 days**, so re-verify before submission.

| # | Category | ₹ | What |
|---|---|---|---|
| 1 | Consumables | 23,100 | PCBs, connectors, cabling, enclosures/potting, drop-test consumables |
| 2 | Equipment | 1,48,240 | 6 nodes + 2 spares (**₹64,337**), drone/airframe + flight controller (**₹62,075**), ground station Pi 5 (6,720), GPS 1PPS (2,096), misc (1,260), 2 reference geophones for ground truth (11,752) |
| 3 | Services | 9,240 | PCB assembly, machining of the drop mechanism |
| 4 | Contingency | 22,274 | 12 % — field work on rubble, node loss on drops |
| 5 | Supplies | 5,040 | Fasteners, adhesives, test targets, safety consumables |
| | **TOTAL** | **₹2,07,894** | = USD 2,474.93 — **1.06× the sample award in the template** |

**Per-node cost [COMPUTED]:** ₹~8,042 (USD 95.74) = geophone 69.95 + radio module 5.99 + antenna
1.50 + **ADC and instrumentation amplifier 8.00** + **18650 cell 4.00** + case 2.50 + PCB 1.80 +
passives 2.00. The two bolded items are **new relative to the old design** and are the honest
consequence of switching sensors: the geophone is **analog** (so it needs its own front end) and
**74 g** (so it cannot run from a coin cell). +41 % per node versus the superseded MEMS design.

**Scaling levers, if the award is fixed:**

| Nodes | Total | vs sample award |
|---|---|---|
| 4 | ₹1,89,880 | **0.97× — fits** |
| 6 | ₹2,07,894 | 1.06× |
| 9 | ₹2,34,916 | 1.20× |
| 12 | ₹2,61,938 | 1.34× |
| **No drone** | **₹1,23,317** | 0.63× |

**The airframe and its consumables are ₹84,577 of the request.** If the budget must shrink, the
honest options are **4 nodes** (fits at 0.97×) or deferring air deployment — but **deferring the
drone deletes RQ1**, which is the strongest novelty axis. Prefer cutting node count.

---

## Do-not-claim list

Stating any of these gets the proposal marked down. Each is a real finding, not caution:

1. **No heartbeat detection.** 38–60 dB short. Settled, not open.
2. **No novelty for the tapping retarget** — FEMA doctrine.
3. **No novelty for drone-deployed seismic sensors** — Stewart et al.; SeismicDart.
4. **No novelty for "node position dominates TDoA"** — textbook GDOP.
5. **Do not claim INACHUS failed or that it succeeded at metre accuracy.** Neither is established.
6. **Do not quote "~USD 15,000" for the incumbent Delsar.** **Unconfirmed.** Observed reseller and
   auction figures span **USD 2,000–28,500**, far too wide to support any cost-ratio claim. If a cost
   comparison is needed, get an official quote first.
7. **Do not state 0.1 µg/√Hz as an SM-24 vendor specification.** The datasheet has **no noise
   spec**. Our computed element floor is 0.003–0.005 µg/√Hz. Describe it as computed.
8. **Do not claim "lighter sensors couple better" as our finding** — that is Krohn (1984).
9. **Do not promise ±0.05 m localization.** Realistic is **±3.5–5 m**, bounded by node position.
10. **Do not present detection as confirmation of life, or a cell as a clearance.** Output is
    DETECTED / NO DETECTION / **BLIND**.
11. **Do not state the 5–8 % duty cycle as doctrine.** Doctrine says "around once per hour for a few
    minutes" with **no stated duration**; literally that is 5–13 %. Mark [ASSERTED] and show the
    power budget's sensitivity — at 10 min/hour it is ~17 %, a 2–3× error.
12. **Do not state a tap count** ("tap three times") as doctrine — secondary sources only.
13. **Do not claim the build is import-ready.** As previously specified it is **not legal in India**:
    DGFT prohibits importing a drone kit (buy components, assemble domestically) and the radio needs
    **WPC type approval**, which was budgeted at zero. Address this in Q3 or the budget narrative.

---

## Before the faculty signature: four citations need full text

These are **READ-ABSTRACT only**. An abstract is enough to fix a number internally; it is not enough
to defend one in a funded proposal. Paywalled or bot-walled — they need hand retrieval:

| Priority | Citation | Why it matters | Access |
|---|---|---|---|
| ~~1~~ **DONE** | **Arosio et al. 2010**, DOI 10.3997/1873-0604.2010051 | **Retrieved and read 2026-10-08.** Confirms verbatim: *"the limited spatial extension of the sensor array"* as a stated limitation; accuracy **≤2 m**; rubble velocity **200–600 m/s**; 20 m × 20 m in ~15 min, 3× faster than incumbents | ✅ full text |
| ~~2~~ **DONE** | **Sabatier & Ekimov 2008**, DOI 10.1117/12.785235 | **Retrieved and read 2026-10-08.** Anchor confirmed verbatim: *"did not exceed 3 x 10-6 m/s, even very close (3 meters) to the walker"* — and correctly used as an **upper bound** | ✅ full text |
| **1 (now top)** | **Krohn 1984**, DOI 10.1190/1.1441700 | The 100–500 Hz coupling window that reinstates the coupling risk. **The only load-bearing citation still unverified** — everything else is now full text | SEG paywall, **USD 42**; try an institutional library login first |
| ~~4~~ **DONE — and it overturned a number** | **Ekimov & Sabatier**, *JASA* 120(2):762 | **Retrieved and read 2026-10-08.** The paper contains **no 17 Hz peak**; the real figure is *"near 40 Hz"*, transfer function **20–90 Hz**. Anchor corrected to **40 Hz → 76.9 µg, +6.47 dB**. The *"−85.7 dB re 1 g"* cross-check is **not in this paper** — do not cite it to this DOI | ✅ full text |
| 5 | **Delsar LD3 official specs and price** — `https://www.savox.com/products/search-and-rescue-kits/delsar` | The only way to make any cost comparison citable | Needs a vendor page capture or quote |

Also worth having: **Wiard et al. 2008**, DOI 10.1186/1753-4631-2-1 (open access, free), and
**Inan 2009** (Stanford dissertation, open) for the cardiac force figures.

---

## Where the numbers come from

| This pack says | Authority |
|---|---|
| The kill, the rebuilt design, the findings register | `docs/critique/07-verdict.md` (+ section 9 amendment) |
| Persistence/PPV and the compliance-cost finding | `docs/critique/08-amendment.md` |
| Arithmetic, reproduced twice | `docs/critique/00b-verification-arithmetic.md` |
| Cardiac force, measured | `docs/critique/prior-art/A-cardiac-seismic.md` |
| Doctrine, incumbents, drone prior art, NDRF | `docs/critique/prior-art/B-usar-systems.md` |
| Propagation and sensor-noise parameters, validated row by row | `docs/critique/prior-art/C-propagation-modeling.md` |
| Superseded original spec — **numbers only, premise dead** | `docs/MASTER.md` (carries a banner) |
