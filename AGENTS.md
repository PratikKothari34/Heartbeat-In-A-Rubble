# AGENTS.md

Context for AI coding agents working in this repo. Read this before `docs/MASTER.md`.

**Project:** Heartbeat In The Rubble — drone-deployed seismic mesh for locating survivors in
collapsed structures. **Stage: pre-code.** No hardware acquired, no source code exists yet.

---

## 1. Read this first: the spec is superseded

`docs/MASTER.md` is the detailed spec. **Its core premise has been disproven and the document does
not say so.**

MASTER describes detecting a buried survivor's **heartbeat** with a MEMS accelerometer. A six-agent
adversarial review on 2026-10-07 established that this **cannot work**:

- The cardiac seismic signal is **38–60 dB below the ADXL355 floor** (25 µg/√Hz — the MEMS part
  MASTER §3.2 specifies, **not** the SM-24 that replaced it) at 3 m.
  (Was 47–69 dB. **Revised 2026-10-08** because the cardiac source force is now *measured*, not
  assumed: 3.7 N (Starr 1939, n=7), 4.06 N (Inan 2009, n=26+), 2 N_pp (Ashouri 2016). The worst
  single healthy subject in the literature, 10.95 N, costs **+8.75 dB**. Nothing recovers 38 dB, and
  the “what if the force is really 20–40 N” escape is now **closed by measurement**. A crush-injured
  survivor measures **weaker** — 0.94–1.05 N, ~12 dB below the healthy mean.)
- MASTER §3.3's central unmeasured assumption (0.1–1 mg at 2–3 m) is **wrong by 479–19,167×**.
- No filter, averaging scheme or ML model recovers this. Closing the gap would need 2.8 h–3.2 yr of
  phase-coherent integration, and the HRV feature needed to prove a signal is human **destroys the
  phase coherence averaging requires**.

> ⚠ **Which sensor the 38–60 dB is measured against — added 2026-10-11.** This file previously said
> *"the chosen sensor's own noise floor."* That was wrong, and in the most misleading possible
> direction: the **chosen** sensor is the **SM-24 geophone** (§4), and against the SM-24's *element*
> floor the cardiac signal is **positive**. 38–60 dB is an **ADXL355** figure —
> `docs/critique/00b-verification-arithmetic.md:26` derives it from the 47–69 dB ADXL355 deficit
> plus the 8.75 dB worst-healthy-subject correction, and `docs/critique/07-verdict.md:69` states the
> parent as *"47-69 dB below the ADXL355 floor."*
>
> **The premise still dies** — by ~31–53 dB after propagation
> (`00b-verification-arithmetic.md:73`) — but it dies **on the propagation path, not on sensor
> self-noise.** Getting this backwards is the single easiest way to publish a claim a reviewer can
> overturn with the datasheet. **Do not quote 38–60 dB against any sensor but the ADXL355**, and do
> not restate it as 31–53 dB either — that figure is frozen under `00b:85-95`.

**Do not design, plan or write code toward heartbeat detection.** It is settled, not open.

### What replaced it

Same hardware, different target. Retargeting to **tapping / voice from a responsive survivor**
clears the noise floor by **+23 to +41 dB** (conservative by ~6.5 dB since the 2026-10-08 anchor
correction — see the *Anchor correction* note in `docs/critique/00b-verification-arithmetic.md`;
deliberately not restated while tap force is unmeasured), and reuses the drone, LoRa mesh, TDoA solver, time sync
and dashboard almost unchanged.

Read in this order:

| File | Why |
|---|---|
| `docs/critique/README.md` | Index and bottom line |
| `docs/critique/07-verdict.md` | The verdict, findings register, rebuilt design |
| `docs/critique/08-amendment.md` | **Amends 07.** Read immediately after it |
| `docs/MASTER.md` | Spec. Numbers are mostly still good; the premise is not |

---

## 2. Precedence

Highest first:

1. **`docs/critique/07-verdict.md` + `08-amendment.md`** — current engineering position. **Read
   §9 of `07`**, the prior-art amendment.
2. **`docs/critique/prior-art/`** — literature sweep, 2026-10-08. **Amends everything above it**
   where they differ; start at its `README.md`. `docs/proposal/INPUT.md` is the proposal input pack
   built from all of it.
3. **`docs/decisions/`** — ADRs, binding where they exist. **Not in this repo** (kept local by the
   maintainer). If a decision seems to be missing, ask rather than assuming none exists.
4. **`docs/MASTER.md`** — consolidated numbers. Loses to the above; wins on raw figures. **It now
   carries a SUPERSEDED PREMISE banner at the top — read that before any section.**
5. `docs/research/` — working papers behind the numbers: `MEMS/` sensor selection, `BUDGET/` costing,
   `REDESIGN/` an earlier pass, consolidated to a single `README.md` on 2026-10-11 (it was never
   applied, and its premise, band and sensor are all superseded — one regulatory finding survives
   intact: the 500 mW Table-II envelope). `MEMS/extracts/` and `BUDGET/extracts/` hold the cited figures pulled
   out of source PDFs, since the PDFs themselves are not in the repo (see Conventions).
6. `docs/reference/` — the original hackathon-era doc. **Stale framing, kept for history only.**

Two things are gitignored and absent from your clone: **`docs/memory/`** (maintainer's project
memory) and **`docs/decisions/`**. The maintainer also has a local `CLAUDE.md` with
machine-specific setup that does not apply to you.

---

## 3. The one error that explains most others

**A repetition rate was mistaken for a signal bandwidth.**

60–120 bpm is how *often* a heartbeat repeats. The beat itself is a broadband impulse (~50–150 ms
rise). MASTER §6 bandpasses **0.5–4 Hz**, which matches the rate and **discards the signal**.

Consequences, all downstream of that single slip:

- Throws away ~48 % of impulse energy; keeps only 2 harmonics.
- **Destroys localization**, because timing precision scales as `σ_t ≈ 1/(B·√SNR)` — narrowing the
  filter makes TDoA *worse*. Correcting the band moves pick error from 8–27 m to 0.86–2.71 m.
- **Caused the wrong sensor choice.** §3.2 marks the ADXL355 **FIXED** and rejects the SM-24
  geophone because its 10 Hz corner sits "above the entire target band" — true only of the *wrong*
  band. The geophone's 48 dB noise-density advantage **is** the detection margin: every tap case is
  buried on the ADXL355 (−7 to −25 dB) and detected on the SM-24 (+23 to +41 dB).

**If you touch the signal chain: the sensor is the SM-24 and §3.2's "FIXED" marker is wrong.
The band is an open question — see below.**

> ⚠ **The tap band is NOT 5–40 Hz — decided 2026-10-11.** Earlier revisions of this file said it
> was. **Neither** circulating figure was ever derived from a tap: **5–40 Hz** comes from
> **seismocardiography** literature (`docs/critique/01-physics-kill-attempt.md:290`, *"centred near
> 15–20 Hz"*) — a *cardiac* band, for the premise that is dead — and **60–80 Hz** is
> *"NO DATA FOUND — and mildly suspect"* (`docs/critique/prior-art/C-propagation-modeling.md:241`).
> Committing to either publishes a tap band with no tap provenance — the same rate-vs-bandwidth
> category error one level up.
>
> **Decision: acquire 5–200 Hz; the detection band is an *output* of the M1/M2 bench measurement,
> not an input.** Where one figure is unavoidable, write `20–80 Hz [ASSERTED — pending M2]`. Any dB
> figure, margin or noise floor must **name the band it was computed in, inline**.
>
> Two things this does **not** change: **the SM-24 stays** (2nd-order high-pass, f0 = 10 Hz,
> ζ = 0.7 → −12.26 dB at 5 Hz but **−0.72 dB by 15 Hz** and ~0 above 30, so the corner penalty is
> confined below ~15 Hz and sensor selection does not re-open); and **the margin figures do not
> move on any band** — 38–60 dB and +23/+41 dB stay as written, frozen under
> `docs/critique/00b-verification-arithmetic.md:85-95`.
>
> What binds is **ambient, not self-noise**: Johnson noise is 0.00027–0.00439 µg/√Hz across
> 5–80 Hz — 23–365× of margin against the 0.1 µg/√Hz spec in *any* candidate band. But machinery
> (20–200 Hz) and aftershocks (5–50 Hz) sit inside the candidate bands
> (`01-physics-kill-attempt.md:300`), and that is site-dependent and unmeasured.
>
> Wide acquisition is also the cheap option: the incumbent this project is benchmarked against —
> the **Delsar LifeDetector LD3**, FEMA/UKSAR standard — runs **1 Hz–3 kHz**
> (`docs/critique/prior-art/A-cardiac-seismic.md:134`), ~37× wider than either candidate. A fielded
> tap/scratch/shout detector does not narrowband.
>
> Recorded as **ADR 0001**. That file (`docs/decisions/`) is kept local by the maintainer and is
> **not in your clone** — this block is the authoritative copy for collaborators.

---

## 4. Current design decisions

Locked (supersedes MASTER where they conflict):

| Parameter | Value |
|---|---|
| Sensor | **SM-24 geophone.** ~~vendor-verify its 0.1 µg/√Hz~~ **No vendor noise figure exists — the datasheet has none (verified by full re-extraction; regex `nois` = 0 matches). 0.1 µg/√Hz was never a vendor spec. Computed element thermal floor is 0.003–0.005 µg/√Hz, so the assumption is conservative by 23–30×. Specify the *preamplifier* instead — it sets the system floor (12–16× margin at 4 nV/√Hz; vanishes only near 50 nV/√Hz).** |
| Band | **Acquire 5–200 Hz** — tap detection band is an **output of the M1/M2 bench measurement**, not chosen now (ADR 0001, 2026-10-11; see §3). One figure where unavoidable: `20–80 Hz [ASSERTED — pending M2]`. ~~5–40 Hz~~ was a *cardiac* band. Voice **200 Hz–3 kHz** stands |
| Target | Tap / movement / voice. **Cardiac is a stretch goal only** |
| Operating mode | **Command-triggered during "All Quiet"**, not autonomous continuous |
| Duty cycle | **~5–8 %**, set by the incident commander, not by the design |
| Runtime requirement | **≥138–163 h** of presence (not 72 h) |
| Primary discriminator | **Persistence across silences, ≥60 % of available looks** — not an LSTM |
| Output | **DETECTED / NO DETECTION / BLIND per cell**, 2–5 m. Never a pin, never a clearance |
| Localization | **±3.5–5 m**, bounded by node position, not by clock error |
| Impact design | **~200 G** (15 mm crush cannot give 15–20 G) |
| Cost model | **Quadratic in 1/r** — halving detection range quadruples node count |
| Dropped | ICA, depth-from-amplitude, ECG-trained LSTM — invalid as specified |

Known-wrong numbers in MASTER, already corrected in the critique: node mass (15.52 g, not 8 g),
node position (±2–5 m, not ±0.05 m), impact (200 G at 15 mm), LoRa ToA (0.370688 s, not 0.3052 s),
packet size (needs 82–156 B, not 24 B), power (receive current budgeted at zero),
**STM32WLE5JC SRAM is 64 kB, not 100 kB — the planned input buffer alone is 70.3 kB (110 %)**.

### Two things that are not solved

1. **False alarms.** At a realistic prior, 93 % accuracy yields **~16 % positive predictive value** —
   five of six detections false; ~907 false pins/day on empty rubble. The persistence rule above is
   the proposed fix (→ 70–98 % PPV) but is **unmeasured**. Never present detection as confirmation.
   **Specify the false-alarm target per look or per All Quiet window, never per node-hour**: the architecture is command-triggered at ~1 window/hour, so a node-hour holds **~1 look**, and the ≤1-false-pin-per-node-hour figure still written in `07-verdict.md:200` and `08-amendment.md:199` is met **14× over before any persistence rule applies** (`09-pr3-citation-audit.md` §7). A gate that cannot fail is not a gate.
2. **Compliance and cost.** All-in capital is **$9,746, not $1,845**; the claimed 8× advantage over
   the $15,000 incumbent compresses to ~1.0–1.5×. As specified the build is **not legal in India**:
   DGFT prohibits importing a drone kit (buy components and assemble domestically) and the radio
   needs WPC type approval, budgeted at $0.

---

## 5. Conventions

- **Units and provenance matter.** This project has been burned repeatedly by unverified numbers.
  Label figures as measured, computed, or assumed, and say which. Don't assert a vendor price or
  stock status without a capture date — prices here drifted 8–16 % in 19 days.
- **Verify links by response body, not status code.** Vendor sites serve soft 404s (HTTP 200 with a
  "Page Not Found" body) and many block scripted access. Use `GET`, not `HEAD`.
- **State what you could be wrong about.** Every critique document ends with that section; match it.
- Markdown docs, LF endings (`.gitattributes` enforces it).
- **Don't commit PDFs.** `*.pdf` is gitignored globally — third-party datasheets and papers are not
  ours to redistribute. Convert to an `.md` extract with a provenance header naming the source URL,
  the DOI, and the figures the extract preserves, then delete the PDF.
- Never commit secrets, env files, or build output.
- **Extracts are now the only in-repo record of every source. There are no PDFs left in the tree.**
  All **33** source PDFs were converted to Markdown and deleted 2026-10-08; the directories that
  held them (`research/BUDGET/papers/`, `research/MEMS/papers/`, `research/MEMS/datasheets/`) are
  gone. Every `[DS]` and `[PAPER]` tag now resolves to a file in the sibling `extracts/` directory:

  | Directory | Extracts | Holds |
  |---|---|---|
  | `docs/research/MEMS/extracts/` | 18 | 15 datasheets + 6 papers (`adxl355`, `epson` and `evans` each cover several sources) |
  | `docs/research/BUDGET/extracts/` | 12 | LoRa sync/mesh, UAV deployment, velocity, BCG/victim-detection |
  | `docs/critique/prior-art/extracts/` | 3 | Arosio 2010, Ekimov & Sabatier 2006, Sabatier & Ekimov 2008 |

  **Before deleting an extract, check whether a figure cited elsewhere survives only there.** Two
  were removed as orphaned earlier on 2026-10-08 (`mpu6050`, `sensys`) and then **restored as full
  text**, because both are substantively cited — MPU-6050's **400 µg/√Hz** appears in three docs and
  SenSys'17 in five. `USGS_SIR2023-5061` was kept for the same reason: it holds the
  **200–1000 m/s** velocity bracket every position-error conversion in `02` depends on.

  **Two gotchas when reading an extract:**
  - **The PDF text layer drops the micro sign.** `TDK_MPU-6050_datasheet.md` renders its noise
    density as `400 g/√Hz`; the unit is **µg/√Hz**. Do not "correct" the docs to `g`.
  - **Two-column PDFs interleave columns.** A sentence can be split across the gutter, so a
    verbatim quote that greps to nothing may still be present. Flatten whitespace and re-search
    before concluding a figure is absent — that distinction is what separates a real
    mis-citation from a conversion artifact.

  An extract whose header says a row was **HELD but never read** means exactly that: the paper was
  retrieved as corroboration and no figure was taken from it. Do not cite a number out of one
  without reading it first.

---

## 6. Contributing

`main` is protected by a ruleset:

- **Pull request required**, 1 approving review.
- Stale approvals are dismissed when new commits land; review conversations must be resolved.
- **No force-push, no branch deletion, linear history required.**
- Signed commits are **not** required.
- Merge, squash and rebase are all allowed.
- The repository admin can bypass these; collaborators cannot.
- **GitHub forbids approving your own PR.** With a small team that means your PR needs the other
  party to review it — plan for that, don't assume you can self-merge.

So: branch, open a PR, get a review. Don't expect to push to `main`.

**Issues are used to delegate work — check open issues before starting, and reference the issue in
your PR.** The tracker is kept short on purpose: it holds only live work, and finished or superseded
items are **deleted**, not closed, with anything worth keeping written into `docs/` first.

**Current work is #7:** revise the research proposal `.docx` to merge-ready, verified in a PR. It
starts from tadiPro250's existing draft (already on `main`) and applies the fourteen fixes in
**`docs/critique/12-closed-work-archive.md`** — eight to the proposal, six to `main` — each with its
arithmetic in `docs/critique/09-pr3-citation-audit.md`. **Read that archive before touching the
proposal.**

### If you are an agent

- **Ask before acting on a contradiction.** MASTER disagreeing with the critique is expected and
  resolved in §2 above. A disagreement *within* the critique set, or anything touching a locked
  decision in §4, is worth raising rather than resolving silently.
- **Don't re-derive the kill arithmetic to check it.** It was computed independently twice and
  cross-checked by six agents. If you think it's wrong, say so with your own numbers — but read
  `docs/critique/00b-verification-arithmetic.md` first, which already lists the assumptions most
  likely to be wrong.
- **The cheapest open experiment is in `08-amendment.md` §6.** Measure the ambient in-band floor
  first: if it exceeds ~1 mg, the premise fails at any sensor price, because no filter removes
  in-band noise.

---

## 7. Prior-art amendment, 2026-10-08 — read before claiming novelty

A three-agent literature sweep (`docs/critique/prior-art/`) ran after the critique. **The kill stands
and is better evidenced** (see §1). What changed is **what counts as novel**.

**Already published. Do not claim any of these as a contribution:**

- **The tapping/voice retarget is existing doctrine.** FEMA US&R lists as a *disadvantage* of
  listening devices that the “**victim must create a recognizable sound pattern**,” and names the
  “audible call out/knocking method.” Delsar LD3, Leader SEARCH and the NDRF Type-I spec are all
  6–8-sensor, operator-interpreted systems. None claims heartbeat; none does automated localization.
- **Automated knock localization** was the stated goal of **INACHUS** (EU FP7 607522, 20 partners,
  2015–2018). No peer-reviewed accuracy result was located — so do **not** claim it as novel, and do
  **not** assert INACHUS achieved validated metre accuracy either. Both overstatements are wrong.
- **Drone deployment of seismic sensors.** Stewart et al., SEG 2016 (drone-*landed* geophones) and
  **SeismicDart** (air-*dropped* darts, ρ = 0.81–0.98 against planted geophones, all drops ≥20 m met
  the professional planting standard). Both characterise **soil**, not rubble.
- **A seismic array on rubble.** Arosio et al. 2010, *Near Surface Geophysics* 8(6):623–633,
  DOI 10.3997/1873-0604.2010051 — accuracy “within the limit of the seismic resolution,” 3× faster
  than incumbent systems.
- **“Node position dominates TDoA, not clock error.”** This is **textbook GDOP**. Written as an
  error-budget conclusion citing GDOP it adds rigour; written as a discovery, a reviewer marks it a
  basic-literature gap.

**What is defensibly novel, strongest first:**

1. **Array extent.** Arosio et al. name their own three limitations as debris inhomogeneity, the need
   for real-time response, and **“the limited spatial extension of the sensor array”** — confirmed in
   two independent sources. Hand placement is what causes that limit; air deployment lifts it. Prior
   art states the constraint; this project's mechanism removes it. A *capability* argument, which
   outranks the cost argument (whose prices are poorly verified).
2. **Coupling onto rubble rather than soil.** Unmeasured by anyone, and the same gap as the
   reinstated coupling risk below — so it is doubly worth measuring.
3. **The cardiac bound itself**, as a published negative result.
4. **Node count at mesh scale**, and the **NDRF Type-I** spec's complete absence of an
   automated-localization requirement — a capability gap in the procuring agency's own words.

**Three numbers in the critique were wrong:**

| Was | Is | Source |
|---|---|---|
| Coupling resonance 500 Hz – 67 kHz | **100–500 Hz** | Krohn 1984, DOI 10.1190/1.1441700 |
| Footstep anchor 19 Hz → 36.5 µg | **40 Hz → 76.9 µg** | Ekimov & Sabatier, *JASA* 120(2):762, **full text retrieved 2026-10-08**. The interim "17 Hz → 32.7 µg" was a **mis-citation** — that figure is not in the paper. Real text: *"maximum vibration response … was near 40 Hz"*, transfer function **20–90 Hz**. **+6.47 dB on every amplitude**, the only correction so far that favours the project |
| SM-24 “0.1 µg/√Hz, vendor-verify it” | **No vendor noise spec exists**; computed floor 0.003–0.005 µg/√Hz | SM-24 brochure, re-extracted |

The coupling correction **partially reinstates `01`'s struck condition C4**: our claimed *floor* was
the literature's *ceiling*, so a 100 Hz contact resonance sits only 1.25× above an 80 Hz tap — in
band, distorting amplitude **and phase**, so it degrades TDoA as well as detection. Margin is
**1.3–6×, not 6–800×**, worst for free-laid nodes on fractured debris — exactly what drone deployment
produces. **If you touch coupling, treat it as open, not settled.** §4's “lighter couples better” is
**Krohn's result, not this project's finding** — don't present it as ours.

**Terminology:** “force-ratio scaling” is not a standard term. It is **linear transfer-mobility
scaling** (FTA ground-borne vibration method; ASTM/FHWA impulse-response mobility spectrum).
Elastodynamics is LTI, so response amplitude is linear in source force — which is *why* it works.
Never scale by **energy** (a factor-2 dB error) and never invoke **seismic moment** (defined for
internal sources, not a body pressing on a surface).

**Citations that must appear in any write-up:** Arosio et al. 2010 (above); **Sabatier & Ekimov
2008**, Proc. SPIE 6963, 69630V, DOI 10.1117/12.785235, which is already a signal-equals-noise range
bound for footsteps — this project's method has a direct published ancestor; and **HeartQuake** (Park
et al. 2020, DOI 10.1145/3411843), which recovers full ECG morphology through a mattress **from an
SM-24 geophone element**, the same part §4 selects. HeartQuake must be cited *and distinguished*
(contact-coupled through bedding, not metres of rubble), because a reviewer who finds it unaided will
read it as contradicting the kill.

**Still unmeasured, now the highest-value bench work:** **tap force and tap spectrum.** The
50–300 N / 60–80 Hz figures every margin in `07` scales off have **no source** — the nearest
literature anchors are destructive (karate chop ~2,800 N) and were explicitly declined rather than
laundered as measured.

**Do not quote “~USD 15,000” for the incumbent Delsar.** Unconfirmed; observed reseller and auction
figures span USD 2,000–28,500, far too wide to support any cost-ratio claim.

**Do not state the 5–8 % duty cycle as doctrine.** Doctrine says “around once per hour for a few
minutes” with **no stated duration** — literally 5–13 %. At 10 min/hour it is ~17 %, a 2–3× power-budget
error. Mark it [ASSERTED].

~~**Four load-bearing citations are READ-ABSTRACT only**~~ — **three were retrieved and read in full
on 2026-10-08, and doing so overturned one of them.**

| Citation | State | Outcome |
|---|---|---|
| Arosio et al. 2010 | ✅ full text | **Confirmed.** *"the limited spatial extension of the sensor array"* verbatim — the novelty claim is now first-hand. Accuracy **≤2 m**; rubble velocity **200–600 m/s**; 20 m × 20 m in ~15 min |
| Sabatier & Ekimov 2008 | ✅ full text | **Confirmed verbatim**, and correctly used as an *upper* bound: *"did not exceed 3 x 10-6 m/s, even very close (3 meters)"* |
| Ekimov & Sabatier, *JASA* 120(2):762 | ✅ full text | **OVERTURNED.** No 17 Hz peak and no *"−85.7 dB re 1 g"* figure exist in this paper. Real peak **near 40 Hz**; transfer function **20–90 Hz**. Anchor → **76.9 µg, +6.47 dB** |
| **Krohn 1984** | ❌ **still abstract-only** | SEG paywall, USD 42. **Now the only unverified load-bearing figure.** The 100–500 Hz coupling window — which reinstates the coupling risk — rests on it |

**The lesson is worth keeping:** a verbatim-*looking* quote assembled from abstracts and search
snippets can be a quote of a paper that does not contain it. Two of the three figures attributed to
*JASA* 120(2):762 were not in it. Treat READ-ABSTRACT as unverified, not as weakly verified.
