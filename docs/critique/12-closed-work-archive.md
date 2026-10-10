# Closed work archive — issues #4/#5/#6 and PR #3

**Archived 2026-10-11, immediately before the issues and the PR were purged from GitHub.**

The tracker is now **empty by decision**. Issues **#4** (PR #3 review, 8 fixes), **#5** (six `main`
doc fixes), **#6** (the `INPUT.md` band contradiction) and **PR #3** (the faculty proposal `.docx`)
were deleted, following #1 and #2 (`11-closed-issue-archive.md`).

**Why the tracker is empty rather than assigned.** The collaborators work only on items assigned to
them, and every open item was blocked on one of two bench measurements — **M1** (ambient in-band
floor) and **M2** (tap force and spectrum) — that nobody but the maintainer can run. A tracker of
items waiting on an unscheduled measurement tracks nothing. The work itself is **not cancelled**:
it is below, and it is the same work.

> **The audit is the surviving artifact.** Every blocking finding from #4 and #5, with its
> arithmetic, is in **`09-pr3-citation-audit.md`** — which was already the issues' own cited source
> of truth. #6's content is **ADR 0001** (`docs/decisions/0001-tap-acquisition-band.md`, gitignored;
> the travelling copy is `AGENTS.md:91`). This file records only what existed **nowhere else.**

---

## 1. The proposal `.docx` — recovered, and it was the only copy

**PR #3 added `docs/proposal/Research_Proposal_Air_Deployed_Seismic_Mesh.docx` and never merged.**
The file existed **only** on branch `proposal/air-deployed-seismic-mesh` (`4dac237`) — not on
`main`. Deleting the PR and its branch would have destroyed a collaborator's 9-page deliverable.

**It was pulled down before the purge and committed to `main`**, alongside a Markdown conversion so
the content is greppable and diffable:

- `docs/proposal/Research_Proposal_Air_Deployed_Seismic_Mesh.docx` — tadiPro250's original, byte-identical (26,910 B)
- `docs/proposal/Research_Proposal_Air_Deployed_Seismic_Mesh.md` — markitdown conversion, 266 lines

**One thing the conversion loses:** the Gantt chart is encoded as **cell shading**
(`w:fill="7F7F7F"`) in `word/document.xml`, which markitdown renders as blank cells. The ethics
scheduling defect (§9 of the audit) is **invisible in the `.md`** and visible in the `.docx`. Read
the `.docx` for anything schedule-related.

**The document is stale against `main`** and needs a rebuild before any signature — it predates
`076e747` and `f73b73d`, still carries the pre-correction footstep anchor, and still has `[...]`
placeholders for faculty details, five publications and the drone-lending lab. The 8 fixes in §3
below are that rebuild's checklist.

---

## 2. tadiPro250's budget rebuild — the reasoning existed only in a PR comment

`INPUT.md` prices the drone as an imported F450 kit at **₹2,07,894**. The author rebuilt it to
**₹1,82,818** and the rebuild is sound: **importing drones in CBU/CKD/SKD form has been
DGFT-prohibited since 9 Feb 2022** (which this project's own `08-amendment.md` notes), and
`INPUT.md` also omitted the **~33% landed cost** (BCD + SWS + IGST) the amendment says to add.

| Scenario | Total |
|---|---|
| Drone built domestically from components | ~₹2,80,000 — **over** the ₹1,95,749 sample award |
| **Drone borrowed (chosen)** | **₹1,82,818** — 0.93× the sample award |

| Category | Amount |
|---|---|
| Equipment | ₹1,13,850 |
| ↳ 8 nodes @ ₹10,021 (SM-24 ₹7,140 + electronics $25.79 × 1.33 × 84) | ₹80,168 |
| ↳ 2 reference SM-24s (bolted ground truth for RQ2) | ₹14,280 |
| ↳ Raspberry Pi 5 ground station | ₹8,938 |
| ↳ GNSS with 1PPS | ₹2,788 |
| ↳ Charger, adaptors, tools | ₹1,676 |
| ↳ Tap-force plate (**estimate, unquoted**) | ₹6,000 |
| Consumables | ₹23,100 |
| Services (PCB assembly, machining) | ₹9,240 |
| Supplies | ₹5,040 |
| Local travel (~8 site visits) | ₹12,000 |
| Contingency (12% of direct) | ₹19,588 |
| **Total** | **₹1,82,818** |

Basis: **₹84/USD (2026-10-07)**, +33% landed on imported parts, SM-24 at ₹7,140 from an Indian
distributor listing `[ASSERTED]`. **Prices on this project drift 8–16% in 19 days** — every line
needs a fresh quote, and the author said so unprompted.

**Two items carry no money by design:** the drone is borrowed and flown by its registered operator
under the Drone Rules 2021; the radio array is wired for months 1–4, with type-approved modules
chosen later. **WPC ETA type approval is still budgeted at zero** while the radio goes on-air in
month 5 — `04-cost-kill-attempt.md:81` costs it at **₹1,50,000**. That is a budget decision, not a
doc defect, and it is unresolved.

---

## 3. The eight proposal fixes — the rebuild checklist

Full arithmetic per item: **`09-pr3-citation-audit.md`**. Two were blocking; six are one-line.

| # | Fix | Audit § |
|---|---|---|
| 1 | **The 17 Hz anchor, wrong twice.** 17 Hz is **WITHDRAWN** — *JASA* 120(2):762 says **"near 40 Hz"**, and both cited refs use 40. The 3 µm/s anchor is **[11] alone**, not the joint cite. → `"no more than 3 µm/s at 3 m [11], with the low-frequency vibration maximum near 40 Hz [12]"` | §1 |
| 2 | **H3b names the wrong sensor.** 38–60 dB is an **ADXL355** figure, not the geophone named one clause earlier. At one floor H3a and H3b imply +61 to +101 dB tap:cardiac against the repo's +32 to +56 — **inconsistent by 29–45 dB.** → *"below the **MEMS (ADXL355)** floor the original design assumed."* **Keep the number.** | §2 |
| 3 | **Ethics approval scheduled after the volunteer test.** Volunteers finish month 2; the ethics *application* runs to month 3. This is the **M2 go/no-go**. → volunteers to months 2–3, ethics application to month 1. **Invisible in the `.md` — see §1.** | §9 |
| 4 | **Noise floor quoted in the rejected band.** `aₙ = 2πf·eₙ/S` is linear in f, so the floor moves 16× across the candidates. Post-ADR 0001 the fix is **not** "pick a band" — it is **name the band inline on every dB figure** and mark the tap band pending M2. | §4 |
| 5 | **The 70–98% PPV range uses a rule the same sentence forbids.** The 70% endpoint is a **≥3-of-6 (50%)** rule; the stated threshold is **≥60%**. Under `k = ceil(0.6n)` the real range is **82–100% for n ≥ 5** (n=5 → 82.13%, n=6 → 97.78%, n=8 → 99.45%). Single-look **15.87%** — *"near 16%"* is exact. **The honest number is stronger than the one quoted.** | §8 |
| 6 | **The voice channel is unfunded and untested.** H3a scores *"tap and voice"* on **tap-only** figures; no voice SNR exists anywhere in the repo; the BOM has no microphone; zero Gantt rows mention voice. → split H3a, or drop voice from the title until funded. | §12 |
| 7 | **Two citations presented as read.** **Starr 1939 (3.7 N)** is CITED-ONLY, a derived conversion — cite as *"as converted and reported in [15]"*, or lead with Inan's **4.06 N**. **Krohn 1984** is the project's last unverified load-bearing citation — flag the access status. Also: **[2] FEMA** is READ-FULL in-repo, so its *"[exact title to be confirmed]"* is over-cautious, and **[21] Donnelly** still has a literal `[initials]` placeholder. | §12 |
| 8 | **One prior-art row, two papers.** *"Jia et al. 2017 (SenSys '17, DOI 10.1145/3131672.3131679); Dong et al. 2022 (PigV², arXiv 2212.03378) — cardiac/respiratory rate recovered with geophones, through a mattress and through barn flooring. Centimetres of bedding or slab, not metres of fractured debris; the deficit is path loss, not sensor capability."* | §2 |

**Two traps on item 8, both corrected mid-issue as C6:** cite PigV² as **arXiv 2212.03378**, never
"SenSys '22" — no venue was ever established here. And **do not** distinguish it as
*"contact-coupled"*: it propagates **through a pen floor**, so that is the one ground that does not
apply. The grounds are **distance and medium**.

**Two items flagged for awareness, not fixes:** **RQ1 as specified predicts air deployment will
lose** (air node σ = 2.06–5.22 m vs tape-surveyed centimetres, against a 0.74 m geometry effect
inside a 2–5 m cell), and the ETA gap in §2 above.

---

## 4. The six `main` doc fixes

All six are in-repo markdown. **No hardware, no measurement, no new research.**

| # | File | Fix | Audit § |
|---|---|---|---|
| 1 | `proposal/INPUT.md:80` | **H2 attaches the cardiac deficit to the wrong sensor** — same defect as proposal item 2. *"the same floor"* resolves to *a geophone's*; 38–60 dB is **ADXL355**. Also in **`MASTER.md:10`** and **`reference/…:7`**. Precedent wording: `research/MEMS/README.md` (`3e74e5d`) | §2 |
| 2 | `proposal/INPUT.md:132`, `:152` | **The ambient go/no-go gate cannot return no-go.** The ~1 mg threshold is ~25× looser than the URBAN floor that already buries the weakest tap by **13.7 dB**. **Write it band-parametric** — a formula or per-band pair, referenced to a named tap case, noting the band is pending M2 | §6 |
| 3 | `critique/07-verdict.md:200` | **The false-alarm target is met 14× over before any persistence rule.** ≤1 false pin/node-hour was set for **continuous** operation; `08-amendment.md` cut it to ~1 look/hour, so at 7% per-look a node-hour yields **0.070**. A duty-cycle-vs-look-rate category error — same shape as the rate-vs-bandwidth error that killed the original band. → **restate per look** | §7 |
| 4 | `proposal/INPUT.md:99` | **ρ = 0.81–0.98 is SeismicDart's alone** (`prior-art/B-usar-systems.md:113`), not Stewart's. Keep Stewart in the row for drone-landed geophones in soil | §18 |
| 5 | `proposal/INPUT.md:228` | **The no-drone figure keeps contingency sized for the with-drone build.** Contingency is 12% of direct (`1,85,620 × 0.12 = 22,274` exactly — that identity is how the decomposition was unwound). → recompute as `(direct − airframe − airframe consumables) × 1.12` | §13 |
| 6 | `proposal/INPUT.md` prior-art table | **The two missing papers** — same row and same two traps as proposal item 8 | §2 |

---

## 5. Still true, and still the constraint on all of it

**The tracker emptied; the measurements did not happen.** Both gates below are unchanged and
unscheduled, and every deleted item was waiting on one of them.

- **M1 — ambient in-band floor.** **The binding constraint and the cheapest kill.** Johnson noise
  never binds: `aₙ = 2πf·eₙ/S` with `eₙ = √(4kTR)` = 2.464 nV/√Hz gives 1.1 ng/√Hz at 20 Hz, 4.4 at
  80 — **23–365× of margin anywhere in 5–200 Hz.** What binds is ambient:
  `01-physics-kill-attempt.md:300` — machinery 20–200 Hz, aftershocks 5–50 Hz, i.e. the band sits
  inside the noise the filter was relied on to remove. Site-dependent, unmeasured.
  **Never write a gate or a margin against sensor self-noise.**
- **M2 — tap force and tap spectrum.** 50–300 N is `[ASSERTED]`. **Every margin in the design scales
  off these two numbers**, and ADR 0001 makes the detection band an *output* of this measurement.
- **A13 (TDK IIM-46234, 70 µg/√Hz) and A14 (Kinemetrics ES-T)** — `[UNVERIF]`. TDK's site is
  unreachable to scripts (`MEMS/05` E10); needs hand-retrieval.
- **Krohn 1984**, DOI `10.1190/1.1441700` — SEG paywall, USD 42. The 100–500 Hz geophone coupling
  window rests entirely on it. Highest-value single retrieval if institutional access exists.

**The frozen margins do not move.** `00b-verification-arithmetic.md:85-95`: **38–60 dB and
+23/+41 dB stay as written, on any band.** Do not substitute 31–53 dB or +29/+47 dB. Re-deriving a
margin from a corrected anchor and an unmeasured force was explicitly rejected.

**The SM-24 stays.** 2nd-order high-pass, f0 = 10 Hz, ζ = 0.7: −12.26 dB at 5 Hz, −2.92 at 10,
**−0.72 at 15**, −0.22 at 20, ~0 above 30. The penalty is confined below ~15 Hz, so **sensor
selection does not re-open** — a constraint that was overstated when the band question was first
put to the collaborators.

---

## 6. One loose number, recorded because it has no home

**The "+8.75 dB" worst-healthy-subject correction matches neither reference force.** For 10.95 N it
is **8.6 dB against 4.06 N** and **9.4 dB against 3.7 N**. Found by tadiPro250 in the PR notes;
**it does not change any conclusion**, and 8.75 dB is what `00b:26` uses to take the deficit from
47–69 dB to 38–60 dB. Left as-is under the frozen-margin policy — recorded here so the discrepancy
is not rediscovered as a defect.
