# Doc sweep — action report

**Date:** 2026-10-11
**Scope:** every `.md` under `docs/`, plus `AGENTS.md`
**Commits:** `4b4ba27` (critique + `AGENTS.md`), `9dd4faa` (research + prior-art) — both pushed
**End state:** stale info gone; issues reduced to the live set; one unowned defect filed as #6

---

## 1. What was wrong, in one line

**The project's stated detection band was never derived from its target.** Both candidates were
inherited from the dead heartbeat premise or from nothing at all, and the docs asserted them as
settled in fourteen places. A second, independent error ran alongside it: the headline dB deficit
named the wrong sensor as its noise referent, which inverted the sign of the margin against the
sensor actually selected.

---

## 2. The band — ADR 0001 (2026-10-11)

| Candidate | Where it came from | Verdict |
|---|---|---|
| **5–40 Hz** | `01-physics-kill-attempt.md:290` §3.3 — **seismocardiography** literature, *"centred near 15–20 Hz"* | Real measured data — **for heartbeats.** A cardiac band for a premise that is dead. |
| **60–80 Hz** | `prior-art/C-propagation-modeling.md:241` | ***"NO DATA FOUND — and mildly suspect."*** `07-verdict:369`: the figures *"have no source."* |

`07-verdict.md:178` had logged `5-40 Hz (tap)` as a **locked decision** — the correct repair of the
earlier 0.5–4 Hz rate-vs-bandwidth error, but it kept a cardiac bandwidth and appended `(tap)`.
Picking either number publishes the same category error one level up.

**Decision.** Acquire **5–200 Hz**, unnarrowed in hardware. **The tap detection band is an output of
the M1/M2 bench measurement, not an input.** Where one figure is unavoidable:
`20–80 Hz [ASSERTED — pending M2]`.

ADR 0001 lives at `docs/decisions/0001-tap-acquisition-band.md`, which is a **gitignored carve-out**
— it does not survive a clone. Its full substance was therefore copied into **`AGENTS.md:91`**, the
authoritative copy for collaborators, and mirrored to `docs/memory/`.

### Two constraints that sound decisive and are not

Both were overstated when the band question was first put to the assignees; both were recomputed.

- **The SM-24 corner is nearly a non-issue.** 2nd-order high-pass, f0 = 10 Hz, ζ = 0.7:

  | 5 Hz | 10 Hz | 15 Hz | 20 Hz | 30 Hz | ≥40 Hz |
  |---|---|---|---|---|---|
  | −12.26 dB | −2.92 dB | **−0.72 dB** | −0.22 dB | −0.03 dB | ~0.00 dB |

  The penalty is confined below ~15 Hz. **Sensor selection does not re-open — the SM-24 stays.**
  It is an argument against *acquiring* below ~15 Hz, not against the sensor.

- **Johnson noise never binds.** `eₙ = √(4kTR)` = **2.4640 nV/√Hz** (R = 375 Ω, T = 293.15 K);
  `aₙ = 2πf·eₙ/S` at S = 28.8 V/(m/s) → **1.096 ng/√Hz @ 20 Hz, 3.289 @ 60, 4.385 @ 80.** Against a
  0.1 µg/√Hz working spec that is **23–365× of margin anywhere in 5–200 Hz.** Do not write gates or
  margins against sensor self-noise.

**What does bind is ambient.** `01-physics-kill-attempt.md:300` — machinery at 20–200 Hz,
aftershocks at 5–50 Hz. Any candidate band sits inside the noise the filter was relied on to remove.
Site-dependent, unmeasured. **That is M1, and it is the cheapest possible kill — run it first.**

**Width sanity check.** The only fielded empirical anchor is the incumbent: **Delsar LifeDetector
LD3** (Savox), FEMA/UKSAR standard, **1 Hz–3 kHz** (`prior-art/A-cardiac-seismic.md:134`) — ~37×
wider than either candidate. A fielded tap/scratch/shout detector does not narrowband.

---

## 3. The floor misattribution

**38–60 dB, and its parent 47–69 dB, is an ADXL355 figure** (25 µg/√Hz) — not the selected SM-24's.
Four documents stated or implied otherwise, including `07-verdict.md:17`, the verdict's own headline,
while `:69` of the same file had the referent right.

Recomputed: integrated ADXL355 floor over B = 3.5 Hz = **46.771 µg**; 0.209 µg → **−47.00 dB**. So
**47 is correct** and the `00b:47` heading reading 48 was the typo, not `README:19`'s figure.

**Why it matters:** against the SM-24 *element* floor the cardiac signal is **positive**. The premise
still dies — by ~31–53 dB after propagation — but **on the path, not on sensor self-noise.** Quoting
the figure without its referent reads as "the sensor we chose cannot hear it," which is false.

**The frozen margins did not move.** `00b-verification-arithmetic.md:85-95` holds: 38–60 dB and
+23/+41 dB stay as written on any band. 31–53 dB and +29/+47 dB were **not** substituted.

---

## 4. Everything else corrected

| # | Defect | Where | Action |
|---|---|---|---|
| 1 | Radio band **865–867 MHz** — the superseded 2005 RFID allocation | `MASTER.md:124`/`:159`, `04-cost:68`/`:691` | → **865–868 MHz** per G.S.R. 853(E) rule 1, primary-source verified (`06:171`). Also added: Table-II is **500 mW e.r.p.** (not EIRP), occupied bandwidth **≤200 kHz** — LoRa BW125 complies, **BW250/BW500 do not**, closing the "go wider to cut airtime" escape. "Licence-free" corrected: ETA is a per-model approval, ~$1,786. |
| 2 | **Node-hour category error** — ≤1 false pin/node-hour | `07-verdict.md:200` | The target was set for *continuous* operation; `08-amendment.md:20` moved to command-triggered (~1 All Quiet window/hour), so a node-hour holds **~1 look**. The target is met **14× over** at the design's own 7% per-look FPR. Restated **per look**. |
| 3 | **PigV² cited as "SenSys '22"** and distinguished as "contact-coupled" | `MEMS/03`, `BUDGET/01`, `REDESIGN` (now `README`), `A-cardiac` | → **arXiv 2212.03378**. It propagates **through the ground** (pig-pen floor), so the coupling argument fails: the grounds are **distance and medium**. Obligation had been recorded only at `prior-art/README:92-102`. |
| 4 | **Jia et al. 2017** recorded as a bare "SenSys'17" row | `BUDGET/01`, `A-cardiac` | → full citation, **DOI 10.1145/3131672.3131679**. Same obligation as HeartQuake: cite and distinguish. |
| 5 | **"LCSC stock is 3 pieces"** supply argument | `02-sensor-survey.md:216` | Dead since **2026-10-06** — stock is **486 + 1192**. The 3-piece figure was captured 2026-09-17. Marked superseded, capture dates stated. |
| 6 | Verification logs pointed at **`papers/`** and **`datasheets/`** and called `extracts/` *"working files, not sources"* | `MEMS/05:101`/`:121`/`:138-139`, `BUDGET/04:76` | `f73b73d` deleted **every PDF** (`*.pdf` is a gitignore carve-out — third-party datasheets and papers are not ours to redistribute). The relationship is **inverted**: the extracts are the sources of record. The provenance trail stands as the reason they are trustworthy. |
| 7 | `C-prop:228` kept the old **36.5 µg** anchor one line below the corrected **76.9 µg** | `C-propagation-modeling.md:228` | Struck through, pointed at row 2. |
| 8 | **`MEMS/06-build-vs-buy.md` had no marker at all** while §7 answered *"Develop a geophone node? No"* | file-level | Marker inserted after the H1 — the verdict is **reversed**. Preserved as now **load-bearing open problems**: the ±10° tilt vs ±30° landing conflict, coupling-vs-self-righting, and the mass/power/cost arithmetic. |
| 9 | **`C-propagation-modeling.md` had no marker at all** while carrying ready-to-paste proposal text baking in 60–80 Hz | `:333`, `:443`, `:634` | File-level marker plus three sited ones. `:634` dismissed a sub-10 Hz roll-off as irrelevant *"for the 60–80 Hz tap band"* — now **live and unresolved**, since acquisition is 5–200 Hz. |
| 10 | `prior-art/README:115` *"Hand-retrieve those four"* vs `:111` *"three of the four are now full text"* | `:115` | → **one remaining paper (Krohn 1984)**. |
| 11 | `MEMS/README` extracts breakdown: **15 datasheets, Epson ×5, ADI ×2** | `MEMS/README.md` | → **12, Epson ×3, ADI ×1**. Also the ADXL355 shortlist row marked ⛔ REJECTED with dated prices ($63.26 @2026-09-17, $55.1592 @2026-10-06) and stock resolved. |
| 12 | Three research READMEs carried markers dated **2026-10-08** covering premise and sensor — **three days before** ADR 0001, so none covered the band | `MEMS/`, `BUDGET/`, `REDESIGN/` READMEs | Band marker appended to all three, closing four separate findings in one stroke. |

---

## 5. What was deliberately left alone

Stale-looking is not stale. The following are **historical record** and were not touched:

- **`01` and `02` kill-attempt derivations** and **`00b` Section A computations** — these are the
  arithmetic that *produced* the corrections. Rewriting them would destroy the audit trail.
- **`05-operational`** and **`docs/reference/`** (already marked ⛔ HISTORICAL).
- **`04-cost:794`** — records a DoT document's *title* containing "865-867 MHz". It is a citation,
  not an assertion.
- **`09:516`** — records what the `.docx` says, not what is true.
- **`BUDGET/04:66`, `MEMS/05:89`** — narrate PDF stubs that were deleted at the time. Past tense,
  correct as written.
- **The superseded-instrument rows in `REDESIGN/`** — they identify the 2005/2007 instruments *as*
  superseded. That is the point of the rows. (Carried into
  `research/REDESIGN/README.md` by the 2026-10-11 consolidation — see §below.)
- **`INPUT.md:80`/`:108`/`:134`** — issue #5's assigned scope. Not edited; filed as **#6** instead.

---

## 6. Issues

**Purge:** nothing to purge. No unanswered older issues exist.

| # | State | Disposition |
|---|---|---|
| #1 | **CLOSED** | Proposal-drafting instruction, discharged by PR #3. Its footstep anchor was withdrawn — do not work from its figures. |
| #2 | **CLOSED** | Same: superseded by PR #3. |
| #4 | **OPEN** → tadiPro250 | Live. PR #3 review, 8 items. Band question unblocked; item 4 reshaped from "pick one and recompute" to "name the band inline." |
| #5 | **OPEN** → Maverick01-code | Live. Six `main` fixes. Band question unblocked; item 2's gate is to be written **band-parametric**. |
| **#6** | **OPEN, new** | **`INPUT.md:107` asserts 5–40 Hz as settled while `:134` admits the tap spectrum is unsourced.** Both #4 and #5 correctly deferred it, and between them nobody held it. Now owned. |

#4 and #5 each received a comment cross-referencing #6 and listing the three sweep results that
bear on their items.

---

## 7. Residual sweep — what remains open

Not defects in the docs; **measurements the docs correctly say are missing.**

1. **M1 — ambient in-band floor.** The binding constraint. Site-dependent, unmeasured. Cheapest kill.
2. **M2 — tap force and tap spectrum.** 50–300 N and the detection band both wait on this. **Every
   margin in the design scales off these two numbers.**
3. **A13 (TDK IIM-46234, 70 µg/√Hz) and A14 (Kinemetrics ES-T)** — `[UNVERIF]`, not closable from
   here. TDK's site is unreachable (`MEMS/05` E10).
4. **Krohn 1984** — the one prior-art paper still needing hand-retrieval before a faculty signature.
5. **ADR 0001 does not survive a clone.** `docs/decisions/` is gitignored. `AGENTS.md:91` is the
   only copy that travels. **Any future band decision must be reflected there too.**

---

## 8. Consolidation — `docs/research/REDESIGN/`, 2026-10-11

Five files → one. `01-literature.md`, `02-vendor-register.md`, `03-proposals.md`,
`04-verification-log.md` and the old README are now a single `docs/research/REDESIGN/README.md`
(1,015 lines → 141).

**Why this folder and no other.** It is the only part of the tree where the documents outlived
their content. Its own header said *"nothing in this folder was ever applied"*, and all three of
its premises are now dead: the heartbeat target, the 10–100 Hz band (which was **PigV²'s heartbeat
band**, not a tap band — ADR 0001) and the MEMS-over-geophone conclusion (**reversed**; the SM-24
is selected). Five files implied five live work-streams. There was one finding.

**Preserved in full, because none of it depends on the dead premise:**

- **R1** — the Table-II regulatory finding. **500 mW e.r.p. / ≤2.5% / APC / ≤200 kHz**, and the
  Gazette's own note naming *"Emergency detection of buried victims"*. **+13 dB** = 4.47× range
  (n=2), 2.35× (n=3.5), 2.5× airtime. A matter of law, so nothing in the retarget touches it.
- **R3** — the CR2032 **pulse-current** diagnosis (aged 30 Ω → 1.20 V droop → 1.80 V brownout at
  40 mA) and both fixes: supercap ≈ 10:1, or LiMnO₂. Neither abandons the coin cell.
- **R2, R4, R5** — recorded with their dispositions (absorbed / superseded / live FTO warning),
  since `06-prior-research-audit.md` cites them by designator.
- The **38-URL audit record** (30 LIVE / 4 BOTWALL / 3 DEAD / 1 UNREACHABLE), the **E17** lesson
  that the link classifier was itself wrong first, and the one citation unique to the pass
  (`10.3929/ETHZ-B-000281405`).

**Dangling references patched, same discipline as the deleted issues:**
`06-prior-research-audit.md` rows 16–19 name the four deleted files. They are **left as written** —
they record what was read at audit time, which is provenance, not a live path — with a `†` footnote
stating where the content went. Every designator those rows cite still resolves.

**Considered and rejected:**

| Candidate | Why it stays |
|---|---|
| `extracts/` — 33 files, **42,324 lines, 76% of the tree** | The PDFs were deleted (`f73b73d`). These **are** the sources of record, and every one is DOI-cited from `BUDGET/01` or `REDESIGN`. The bloat is load-bearing. |
| `00-my-own-arithmetic.md` + `00b-verification-arithmetic.md` | `00` checks the project's **stated** numbers before any critic reported; `00b` checks the **critics' kill claims**. Merging destroys an independent cross-check. |
| `07-verdict.md` + `08-amendment.md` | `08` is cited **by line number** from four files, and `07`§4.2 is explicitly superseded by `08`§5. **The two-document structure is the supersession record.** |
| `docs/reference/` (474 lines, ⛔ stale) | It is the **primary source the critique critiques** — cited as such by `01`, `02`, `05`, `07`. Deleting it orphans four kill-attempt documents. |
| `docs/decisions/0001` + `docs/memory/ADR-0001` (identical) | The mirror is mandated: `docs/decisions/` is gitignored, so the duplicate is the recovery copy. |
