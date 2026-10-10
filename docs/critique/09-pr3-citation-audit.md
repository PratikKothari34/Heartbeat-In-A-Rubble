# 09 - PR #3 audit: every inconsistency found

**Date:** 2026-10-09. **Status: OPEN REVIEW.** This audits an **unmerged** pull request against
`main` @ `f73b73d`. It is a review artifact, not a decision: nothing here binds until the PR is
resolved, and `docs/decisions/` outranks it. It changes nothing outside this file.
**Inputs:** four parallel subagents (physics/numbers, citations/prior-art, budget/regulatory,
logic/structure), plus base-provenance forensics on the `.docx` and the Gantt reconstructed from
`word/document.xml`.

---

**Document:** `docs/proposal/Research_Proposal_Air_Deployed_Seismic_Mesh.docx` (tadiPro250, PR #3, commit `4dac237`)
**Audited against:** `main` @ `f73b73d`
**Date:** 2026-10-09 · **Nothing has been edited.** Repo tree verified clean.

**Method:** four parallel subagents (physics/numbers, citations/prior-art, budget/regulatory, logic/structure)
plus my own base-provenance forensics. **Every finding below was re-derived by me before being written
down** — two agent claims were corrected downward in the process (§16, §22) and one was corrected upward (§4).

---

## 0. The headline

**Your instinct was right, and the evidence is stronger than a guess.** The proposal was authored against
**pre-`076e747`** repo state. But the audit found something more important: **the stale base accounts for
only 2 of the 10 blocking findings.** The rest are live defects — most of them inherited from `main`, which
means **fixing the proposal alone does not fix the project.**

| | Count |
|---|---|
| **BLOCKING** | **10** |
| SHOULD-FIX | 11 |
| MINOR / not-an-error | 9 |

**Attribution of the 10 blocking findings:**

| Source | Count | Items |
|---|---|---|
| Stale `f369eb0` base | **2** | §1, §2 |
| **Inherited from `main` — live right now** | **4** | §3, §5, §6, §7 |
| Author-introduced | **3** | §8, §9, §10 |
| Composition error | **1** | §4 |

**The single most useful sentence in this report:** the author did not mis-read the brief — **the brief moved
underneath them**, and four of the ten blocking defects are in `main` today.

---

# BLOCKING

## 1. The 17 Hz anchor — withdrawn figure, cited to two papers that both say 40 Hz
**Line 90** · stale base · *the only factually wrong number in the document*

> "Scaling is anchored to measured footstep responses: no more than 3 µm/s at 3 m, with a peak near **17 Hz** [11, 12]."

**The citation is wrong twice over.**

1. **17 Hz does not exist.** `C-propagation-modeling.md:227` marks it **WITHDRAWN 2026-10-08**: the full text
   of *JASA* 120(2):762 was retrieved and "contains no '17 Hz' figure." The paper says **"near 40 Hz"**.
   I grepped both retrieved extracts: ref [12] → **zero** matches for "17 Hz"; ref [11] → zero matches for
   "17 Hz" and **35+ for "40 Hz"**. **The proposal cites 17 Hz to two papers that both use 40.**
2. **The 3 µm/s anchor is not in ref [12] at all.** It belongs to **[11]** alone (Sabatier & Ekimov 2008,
   `extracts/SabatierEkimov2008...:39` — *"did not exceed 3 x 10⁻⁶ m/s, even very close (3 meters)"*).
   I grepped the ref-[12] extract for every form of the figure — **zero matches.** The joint cite claims
   support that does not exist.

**Recomputed:** 17 Hz → 32.68 µg; 19 Hz → 36.52 µg; **40 Hz → 76.88 µg** (`a = 2πf·3 µm/s`, linear chain).
**The error runs *against* the proposal** — it quotes a figure that makes its own case weaker.

> ⚠ **Which dB applies — corrected 2026-10-11 (C7).** The repo's **+6.47 dB** is the **19 → 40 Hz** step
> (`00b:20`, `07-verdict:313`), because 19 Hz was the figure the repo itself carried. **The proposal says
> 17 Hz**, and **17 → 40 Hz is +7.43 dB.** Both are right about different baselines; pairing "32.7 µg" with
> "+6.47 dB", as this section first did, mixes the two. The repo is internally consistent and records
> 17 Hz → 32.7 µg as a **superseded interim mis-citation** (`00b:65` strikes it; `07-verdict:313` names it
> *"the interim 17 Hz"*). **For the proposal's own correction, the figure is +7.43 dB.** Do not restate the
> frozen margins with either value — see §A1.

**Fix:** `"no more than 3 µm/s at 3 m [11], with the low-frequency vibration maximum near 40 Hz [12]."`
Change **only the anchor** — the derived margins are deliberately frozen (§A1).

---

## 2. SenSys'17 missing — a written obligation, unfulfilled. And there is a third such paper.
**Prior-art table, lines 69–76** · stale base + **upstream `INPUT.md` defect**

`extracts/SenSys2017_geophone_heartrate_shared_bed.md:14-19` carries an explicit instruction:

> "**Must be cited AND distinguished, for the same reason as HeartQuake.** This paper recovers a cardiac
> signal with the same class of sensor this project selects, so a reviewer who finds it unaided will read it
> as contradicting the kill."

There is no SenSys'17 row. HeartQuake **is** cited and distinguished (line 75) — so one of the two
obligations was discharged and the other missed.

**New, and worse — PigV2.** `docs/research/MEMS/extracts/pigv2.md` (41 KB, confirmed on disk): Dong et al.,
2022, **arXiv 2212.03378** — *"Monitoring Pig Vital Signs through Ground **Vibrations** Induced by **Heartbeat** and
Respiration."* Geophone cardiac detection **through the ground**, not through bedding. **That is closer to
this project's geometry than HeartQuake or SenSys'17**, and it is the strongest-looking apparent
counterexample in the entire repo. `MEMS/05-verification-log.md:62` confirms the project read it.

**Attribution — this one is mostly yours, not tadiPro's.** `OLD-INPUT.md`'s prior-art table omits both
papers, and **`INPUT.md` at HEAD still does.** The obligation lives only in the extract headers. An author
working from the input pack — which is what it is for — **could not have derived either.**

**Fix (one row):** *"Jia et al. 2017 (SenSys '17, DOI 10.1145/3131672.3131679); Dong et al. 2022 (PigV2,
arXiv 2212.03378) — cardiac/respiratory rate recovered with geophones, through a mattress and through barn
flooring. Centimetres of bedding or slab, not metres of fractured debris; the deficit is path loss, not
sensor capability."*

> ⚠ **Corrected 2026-10-11 (C6).** This row originally read *"Contact-coupled at centimetres"* for both
> papers and cited PigV2 as *"SenSys '22"*. Both were wrong. **PigV2 propagates through the ground**, so
> "contact-coupled" is the one ground that does *not* distinguish it — the distinction is **distance and
> medium**. And the repo cites it as **arXiv 2212.03378** (`MEMS/03-literature.md:38`); no conference venue
> was ever established. Issue #4 item 8 carries the original wording and has been corrected in a comment.

---

## 3. The cardiac deficit is attached to the WRONG SENSOR
**Line 62** · **inherited from `main`** · *worst finding in the document — no citation check needed to spot it*

Both halves of RQ3, in one table cell:

> H3a: tap and voice … exceed **the geophone noise floor** by +23 to +41 dB …
> H3b: cardiac signal sits 38–60 dB below **the same floor** …

"The same floor" is the geophone floor, named one clause earlier. But the 47–69 dB family is stated in
`00b:103-108` explicitly **"Against the ADXL355's own noise floor (25 µg/√Hz)"**, and `07-verdict.md:69`
finding #1 reads **"47-69 dB below the ADXL355 floor."**

**Recomputed at B = 35 Hz:**

| Reference floor | 1 N | 4 N | 10.95 N |
|---|---|---|---|
| ADXL355, 25 µg/√Hz | −69.1 dB | −57.0 dB | −49.2 dB |
| **SM-24 assumed, 0.1 µg/√Hz** | **−21.1 dB** | **−9.0 dB** | **−1.3 dB** |
| **SM-24 element, 0.0033 µg/√Hz** | **+8.5 dB** | **+20.6 dB** | **+28.4 dB** |

**Against the geophone the proposal actually specifies, the cardiac deficit is 1–21 dB, not 38–60 dB** —
and against the geophone's *element* floor the cardiac signal is **positive by 8.5–28.4 dB**. The 38–60 dB
figure is true only of the MEMS part line 54 says the project **abandoned in the same breath**.

**The internal contradiction a referee finds in one read.** Taking H3a and H3b at face value against one
floor implies a tap-to-cardiac ratio of **+61 to +101 dB**. The repo's own figure (`00b:177-183`) is
**+32 to +56 dB**, which I reproduced exactly (8.23/0.209 = +31.9 dB; 32.93/0.052 = +56.0 dB).
**The two hypotheses are mutually inconsistent by 29–45 dB.**

> ⚠ **Not the same as the staleness finding.** The *value* 38–60 dB is **correct by policy** (§A1). The
> defect is the **referent**. Fixing the sensor name does not require touching the number.

**Fix:** H3b must name the sensor — *"below the **MEMS (ADXL355)** floor the original design assumed"* —
and the salvage argument then needs the repo's **+32 to +56 dB** ratio. **`INPUT.md:73-81` carries the same
"the same floor" wording — fix upstream too.**

---

## 4. The noise floor is quoted in the band the same document rejects
**Line 82** · composition error · *highest-value single edit in the document*

> "The element's own thermal noise … is 0.003–0.005 µg/√Hz **across 60–80 Hz**."

Line 86 declares the design band **5–40 Hz**. Because `aₙ = 2πf·vₙ` is **linear in f**, the floor moves
**16× across the disputed range**:

| Band | Element floor | vs 0.1 µg/√Hz |
|---|---|---|
| 60–80 Hz (as written) | 0.00329–0.00439 | 23–30× |
| **5–40 Hz (the stated design band)** | **0.00027–0.00219** | **46–365×** |

The arithmetic is **exact** either way (Johnson noise `eₙ = √(4kTR)` = 2.464 nV/√Hz, R = 375 Ω, S = 28.8
V/(m/s) — verified). **The band is the defect.** The one sentence carrying the entire sensor-selection
argument is parameterised in a band the document rejects two paragraphs later, and the "23–30× quieter" and
"margin used up near 50 nV/√Hz" claims both inherit it. The 50 nV figure is right **only at 80 Hz**
(exactly 56.2 nV); over 5–40 Hz the margin survives to **112–899 nV/√Hz**, understating preamp headroom
by 2–16×.

> *Correction to my own earlier note:* I first logged this as MINOR because the error direction is
> conservative. **Direction is not the issue** — the figure is silently tied to one branch of an explicitly
> unresolved contradiction, and three dependent claims inherit it.

---

## 5. The tap margin integrates noise in one band and puts the signal in another
**Lines 54, 62, 129** · **inherited from `main`**

The **+23 to +41 dB** margin is quoted three times, including as acceptance criterion **M4**. I reproduced
it and it is **only** recoverable at **B = 35 Hz** — the 5–40 Hz integration bandwidth:

```
B=35: +22.87 / +34.90 / +40.94 dB   <- matches "+23 to +41" exactly
B=20: +25.30 / +37.33 / +43.37 dB   <- what a 60-80 Hz band would give
```

But `00b:160-166`'s **Freq** column places those three sources at **60 / 80 / 80 Hz**. So each margin
**integrates noise over 5–40 Hz while placing the signal at 60–80 Hz** — the source sits *outside* the band
whose noise is being integrated. Resolve it either way and the number changes: on a 60–80 Hz band it becomes
**+25 to +43 dB**.

**Compounding:** line 62 honestly tags H3a *"[computed; depends on the tap force, which is measured first]"*
— and line 129 then uses the same figure as a **fixed M4 acceptance target**. A gate cannot be stated to
±0.1 dB on a force the document calls unsourced (line 65) in a band it calls unresolved (line 86).

**The value is correct-per-repo and correctly frozen.** What is missing is the **band tag**.

---

## 6. The ambient go/no-go gate cannot fail — proved with the project's own cited paper
**`INPUT.md:132,152` + the proposal's M2** · **inherited from `main`**

The Activity-1 go/no-go is set at an ambient floor of **~1 mg**. Sabatier & Ekimov 2008 — reference **[11]**,
already held in full — publishes **measured** band-limited floors. Converted (`a = 2πfv/g`):

| Band | URBAN ave | URBAN peak | QUIET ave | QUIET peak |
|---|---|---|---|---|
| **10–40 Hz** | **40.0 µg** | 128.1 µg | 0.352 µg | 1.025 µg |
| 20–30 Hz | 14.4 µg | 38.4 µg | 0.240 µg | 0.833 µg |
| 30–40 Hz | 10.3 µg | 22.4 µg | 0.202 µg | 0.516 µg |

Against the weakest tap (**8.23 µg**, 50 N knuckle at 3 m):

- **URBAN** (ordinary occupied site): tap is **13.7 dB BELOW** the floor — **buried**.
- **QUIET**: tap is **+27.4 dB ABOVE** the floor — trivially detectable.
- **Both sites PASS a ~1 mg gate** — urban by 25×, quiet by 2,800×.

**A gate at 1 mg is 25× looser than the site that already defeats the system.** It cannot return "no-go" for
any realistic site, so Activity 1 cannot fail and the decision gate is decorative. The paper the proposal
itself cites says so in words: the 3 µm/s footstep *"is less than the typical level of the background
vibration noise floor."*

**Fix:** restate band-limited and ~2 orders tighter — go/no-go on the **10–40 Hz RMS floor at ~10 µg** —
and report a spectrum, not a single number. Cite Table 1 as the prior expectation (26–41 dB of site-to-site
spread) so a no-go is a legitimate, pre-registered outcome.

---

## 7. The RQ4 false-alarm gate cannot fail either
**Lines 63, 94** · **inherited from `main`** · *same class as §6*

> L63: "Target: **no more than 1 false detection per node-hour** on empty rubble."
> L94: "Nodes listen **only during commanded All Quiet windows**" — doctrine: **once per hour**.

So a node-hour contains **~1 look**, not thousands. Recomputed at the proposal's own 7% per-look FPR:

| Rule | False detections / node-hour | Slack vs target |
|---|---|---|
| single look, no persistence | 0.070 | **14× inside** |
| ≥3 of 6 looks | 9.7 × 10⁻⁴ | 1,028× inside |
| **≥4 of 6 looks (the stated rule)** | **5.4 × 10⁻⁵** | **18,692× inside** |

**The target is already met by 14× before any persistence rule is applied.**

**Root cause — a duty-cycle-vs-look-rate category error.** The ≤1/node-hour figure was set in
`07-verdict.md:200` for **continuous** operation, where a node-hour holds thousands of looks.
`08-amendment.md:20` changed the architecture to command-triggered (~5–13% duty), collapsing looks-per-hour
by ~3 orders of magnitude — **and the threshold was never rescaled.** This is a close cousin of the
project's signature rate-vs-bandwidth failure: **a per-hour *rate* carried across an architecture change
that redefined what an hour contains.**

**Fix:** state the target **per look** or per All Quiet window.

> **Three of the proposal's decision gates cannot fail** — §6 (ambient), §7 (false alarm), and RQ2's
> criterion-without-a-number (§17).

---

## 8. The 70–98% PPV range comes from a rule the same sentence forbids
**Line 63** · author-introduced (inherited trap)

> "a single look gives a PPV near 16%. Requiring detection in **at least 60% of available looks** raises it
> to **70–98%**."

Single-look PPV recomputes to **15.87%** — *"near 16%"* is **exact**. But:

| Rule | Fraction of looks | PPV |
|---|---|---|
| **≥3 of 6** | **50%** | **70.9%** ← the "70" endpoint |
| ≥4 of 6 | 67% | 97.8% ← the "98" endpoint |

**The 70% lower bound comes from a 50%-of-looks rule, which the ≥60% threshold in the same sentence
explicitly forbids.** Under a strict `k = ceil(0.6n)` rule the real range is **82–100% for n ≥ 5**:

```
n=4 k=3 (75%)  91.40%     n=6 k=4 (67%)  97.78%
n=5 k=3 (60%)  82.13%     n=8 k=5 (62%)  99.45%
```

The author took the **numbers** from the rows of `08-amendment.md:70-74` and the **rule** from that
section's conclusion at `:80-82`. Line 94 then states the very principle it violates: *"A fixed count
degrades as looks accumulate."*

**The honest fix makes the claim stronger.**

---

## 9. Volunteer testing is scheduled BEFORE ethics approval exists
**Line 23 vs the Gantt** · author-introduced · *cheapest fix in the document*

> L23: "Institutional ethics approval **will be obtained before any participant test**."

| Gantt row | Months |
|---|---|
| "Tap force and spectrum characterisation (**volunteers**, instrumented plate): go/no-go" | **1, 2** |
| "Preamplifier design; **ethics application**; procurement" | **1, 2, 3** |

**The volunteer measurement finishes in month 2. The ethics *application* — not the approval — runs to
month 3.** The human-subject work completes before the application does.

Compounding: this is the **M2 go/no-go** measurement and the tap force is *"measured first"*. **The single
most load-bearing measurement in the proposal is the one scheduled outside ethics cover.** An ethics
committee rejects this on sight — and it is **visible from the Gantt alone**, which is why §19 matters.

**Fix (free):** volunteer row → months 2–3; ethics application → month 1.

---

## 10. RQ1's effect is smaller than its own measurement quantum — and the comparison is confounded against it
**Line 60** · author-introduced · *this is the flagship experiment*

> "Location error is **bounded by node-position uncertainty**, as standard GDOP analysis predicts … For the
> same node count, a **wider** air-placed array assigns a tap source to the correct **2–5 m cell more often**
> than a compact, hand-placed one."

**Three independent reasons it cannot produce a result, each sufficient:**

1. **The halves defeat each other.** Widening an array improves only the GDOP multiplier on the *timing*
   term. If error is node-position-bounded — as half 1 concedes, **citing GDOP itself** — the term geometry
   acts on is already negligible. **Half 1 is the reason half 2 cannot be observed.**
2. **The whole effect is sub-cell.** Using the repo's own numbers (`00b:195` pick error 0.86 m at 20 dB;
   `00b:203-205` node position 3.5 m): wide (GDOP ×1) = **3.60 m**; compact (GDOP ×3) = **4.35 m**.
   **Entire swing 0.74 m against a declared 2–5 m cell.** Both arrays land in the same cell nearly always.
3. **The confound runs against the advocated arm.** Air-array node positions come from drone GPS + bounce —
   `00-my-own-arithmetic.md:75-83` gives **σ = 2.06–5.22 m**. The compact hand-placed array is surveyed by
   tape — centimetres. **As specified, RQ1 predicts air deployment will LOSE**, trading a 2–5 m handicap on
   the dominant term for 0.74 m of geometry.

**Why it matters most:** RQ1 is the self-declared **strongest novelty axis**, **Journal article 2**, and
milestone **M12**.

**Recommended reframing** (this matches §11 independently): make RQ1 about **coverage, BLIND-cell
elimination, and not putting rescuers on the pile** — not about beating a compact array on point accuracy.
**The array-extent argument survives that reframing; the accuracy-superiority framing does not.**

---

# SHOULD-FIX

## 11. Arosio's accuracy is now a hard number — and it beats the proposal's own target
**Line 71 vs lines 40/50/60/123** · partly stale base

The prior-art table states Arosio's result only in the old vague form. The full text now gives **accuracy
≤2 m** twice (`extracts/Arosio2010...:775-776, 894`). The proposal targets a **2–5 m cell**, and line 123
promises accuracy *"vs Arosio's benchmark"* **without ever stating the benchmark**.

**So the closest prior art already equals or beats the proposed system's stated goal**, and a reviewer who
opens [1] sees it. Worse for RQ1: the ≤2 m came from the **smaller spread** arrays — the *compact*
configuration — which is the arm RQ1 bets against.

Not fatal (Arosio's wide-array errors are attributed to amplitude variation under an *energy-focusing*
operator; this project proposes **TDoA**, a different estimator) — but the proposal must say so explicitly
instead of leaving the comparison implied. **See §10 for the recommended reframing.**

## 12. The 5–40 Hz branch puts a quarter of the band below the sensor's own corner
*(Finding stands; its conclusion is narrower than written — see the ADR 0001 note at §12's end.)*
**Line 82 vs line 86** · my own finding

All four SM-24 specs verified **exact** against the brochure (10 Hz / 28.8 V·s/m / 375 Ω / 74 g). But a
velocity geophone is a **2nd-order high-pass below its corner**. Computed (f₀ = 10 Hz, ζ = 0.7):

| f | 5 Hz | 7 Hz | 10 Hz | 20 Hz | 40–80 Hz |
|---|---|---|---|---|---|
| response | **−12.3 dB** | −7.1 dB | −2.9 dB | −0.2 dB | 0.0 dB |

**If the band resolves to 5–40 Hz, the chosen sensor is 12.3 dB down at the bottom of its own design band**
and loses most of its bottom octave. The proposal states "10 Hz natural frequency" as a bare spec and
**never connects it to the 5–40 Hz band**. `07-verdict.md:228` already lists this as an open question.

> **Narrowed 2026-10-11 (ADR 0001).** The −12.26 dB at 5 Hz is correct, but the penalty is **confined below ~15 Hz** — −2.92 dB at 10 Hz, −0.72 dB at 15, −0.22 at 20, ~0 above 30. So this does **not** re-open sensor selection, as the summary line originally implied: the SM-24 stays on any candidate band. It is an argument against *acquiring* below ~15 Hz, not against the sensor — and ADR 0001's 5–200 Hz acquisition band is chosen partly for that reason.

**Band choice and sensor choice are coupled.** The 60–80 Hz branch is flat for the SM-24; the 5–40 Hz branch
is not. Activity 2 should resolve **band and sensor-match together.**

## 13. The voice channel is a complete orphan
**Title, L62, L82 vs the whole budget and schedule** · largely inherited

| Promised | Delivered |
|---|---|
| L62 **H3a**: *"**tap and voice** … exceed the geophone noise floor by +23 to +41 dB"* | the figures are **tap-only** (`00b:164-166`) |
| L82: *"A **microphone channel (200 Hz–3 kHz)** covers voice."* | **no microphone in the BOM** |
| title / abstract *"tap or call"* | **no Gantt row, no milestone, no deliverable** |

Three defects: (1) **wrong transducer inside the hypothesis** — voice is handled by a mic in a different
band, and **no voice SNR has ever been computed anywhere in the repo**; (2) **unfunded** — line 204's BOM
lists nine items and no mic, and **line 82 enumerates the node contents and omits the mic in the same
paragraph that adds it**; (3) **untested** — zero occurrences in schedule or deliverables.

**The cleanest "scored hypothesis with no instrument" in the document.** `INPUT.md:73-74` welds voice to the
geophone margin — **fix upstream too.**

## 14. WPC radio type approval is budgeted at zero, and the radio goes on-air in month 5
**Line 241 vs the Gantt** · not base-attributable

`04-cost-kill-attempt.md:68-71`: ETA is *"a **per-device-model** approval requiring a test report from an
accredited lab"*, costed at `:81` as **₹1,50,000 [EST]** — **82% of the entire ₹1,82,818 request**; the
₹50,000 floor case is still 27%.

**"Months 1–4 are wired" is TRUE** — I verified from the Gantt shading that every wired row ends by month 4
and the first radio row starts month 5. **Credit where due.** But the project then needs an on-air radio for
**eight of twelve funded months**, with no line for the approval that enables it. The escape clause
(*"approval will be sought through the institute"*) transfers ₹1.5 lakh to a third party with no commitment
letter and no fallback. `04-cost-kill-attempt.md:775` logs the WPC source as **[SEARCH] — "URL identified,
not fetched"**, so even the claim that an ETA-holding module exists rests on an unverified source.

**Compounding:** it sits under a heading reading *"Regulatory items (**not requested in this budget**)"* —
accurate as a sentence, but it **frames a cost omission as a scope decision.**

## 15. 50% of the request is committed across the gate that is supposed to protect it
**Line 128 vs the Gantt** · not base-attributable · *fix is free*

> L110: "Activities are ordered so that each risk that could stop the project is tested **before the money
> that depends on it is spent**."
> L128 (**M2**): "the project stops here, **having spent mainly on two geophones and one node**" = ₹24,301.

But the Gantt row *"Preamplifier design; ethics application; **procurement**"* is shaded **months 1, 2 AND
3** — procurement **straddles and outlives** the month-2 gate.

| Reading | Pre-gate exposure | % of request |
|---|---|---|
| As claimed | ₹24,301 | 13.3% |
| Minimum honest (Activity 2 *is* the tap-force measurement → plate is pre-gate) | ₹30,301+ | 16.6%+ |
| **If the month-1–3 procurement row means what it says** | **₹91,894** | **50.3%** |

**Fix (editorial, free):** split into *"long-lead gate instruments (2 geophones, 1 node, force plate) —
month 1"* and *"array procurement — month 3, post-gate."* **As written, the budget's best feature is
refuted by its own schedule.**

## 16. Consumables retained after the drone was dropped — real, but ⅓ smaller than first reported
**Line 197** · not base-attributable · ⚠ *my correction to a subagent finding*

`INPUT.md:230` states *"The airframe and its consumables are **₹84,577** of the request"*, and the proposal
drops the drone while keeping the **full ₹23,100** consumables line — including *"spare propellers and a
battery for the borrowed drone."*

The reported decomposition was ₹84,577 − ₹62,075 = **₹22,502 = 97.4%** of consumables. The subtraction
reproduces — **but the decomposition is wrong.** `INPUT.md`'s contingency is **12% of direct cost** (verified:
direct 1,85,620 × 0.12 = 22,274 exactly). **So the airframe carries its own contingency:**

```
84,577 = 62,075 (airframe) + 7,449 (its 12% contingency) + 15,053 (drone consumables)
```

**Drone-attributable consumables are ₹15,053 = 65.2% of the line, not ₹22,502 = 97.4%.** The remaining
₹8,047 survives legitimately. **Net exposure ≈ ₹15,053 (8.2% of request), not ₹22,502 (12.3%).**

**A second defect falls out — and it is `INPUT.md`'s, not the proposal's.** INPUT derives *"No drone —
₹1,23,317"* by a **flat subtraction** `2,07,894 − 84,577`, leaving the 12% contingency computed on the
**with-drone** base. Done properly: airframe removed → **₹1,38,370**; airframe + its consumables removed →
**₹1,13,168**. Neither equals ₹1,23,317. **`INPUT.md:228`'s no-drone rung is arithmetically loose, and every
comparison drawn against it inherits that.**

## 17. Three more unfunded promises and an unfalsifiable criterion

- **Calibrated reference instruments** — `04-cost-kill-attempt.md:181-184` is categorical: *"A bare sensor
  measuring its own output is not a measurement; it is a tautology. The reference instrument **is** the
  measurement."* The proposal funds 1 of 7 test-equipment lines. **The month-1 ambient go/no-go gate has no
  funded instrument capable of deciding it** (needs a calibrated seismometer ~USD 400 + 24-bit DAQ ~USD 300).
- **International freight and clearance** — `04-cost-kill-attempt.md:127-128` prices three consignments +
  broker at **USD 225 ≈ ₹18,900**. Line 196's "Pricing basis" names only duty/SWS/IGST, implying it
  enumerated the full landed stack. **Duty is not the whole of landing a part in India.**
- **Tap-force plate spectrum** — ₹6,000 buys *static* force. The method needs force **and spectrum** to
  60–80 Hz. An HX711 samples at **10–80 SPS** — physically incapable of resolving a 60–80 Hz spectrum or a
  50–150 ms impulse. **The gate turns on the spectrum, and ₹6,000 cannot measure it.** (Shares an
  instrument with the unfunded hammer source for RQ2.)
- **RQ2's success criterion is unfalsifiable** — *"a measured transfer function … for each landing type"* is
  satisfied by **having taken the measurement, whatever it shows.** No threshold, no pass/fail. The
  preceding sentences make a real prediction that is simply not carried into the criterion.

## 18. Access-status drift, in BOTH directions

| Ref | Proposal says | Repo record | Direction |
|---|---|---|---|
| **[2]** FEMA | *"[exact title to be confirmed]"* | `B-usar-systems.md:141` **READ-FULL, 61,971 chars** | **too cautious** |
| **[14]** Starr 1939, 3.7 N | cited as if read | `A-cardiac-seismic.md:27` **CITED-ONLY** — read through Inan 2009 | **too confident** |
| **[13]** Krohn 1984 | cited flat, no hedge | `INPUT.md:273` *"**the only** load-bearing citation still unverified"* | **too confident** |

**[2] is the tell:** the proposal describes as unconfirmed a document the project holds in full and quotes at
line 72. **Drift against the author's own interest** — they were working from a stale copy while being
*more* cautious than the record required, not less. Also: **ρ = 0.81–0.98 is credited to [8] and [9]
jointly; it is SeismicDart's alone** (`B-usar-systems.md:113`) — and **`INPUT.md:99` makes the identical
conflation**, so fix that upstream.

## 18b. Two citations are presented as read when the repo says otherwise
**Lines 106, 61/102** · inherited from `main` · *from the citation agent, verified*

- **Starr 1939's 3.7 N is CITED-ONLY.** `A-cardiac-seismic.md:27` tags it
  *"figure read in full from Inan 2009, which states the calibration conversion"* — the number is a
  **derived conversion** from Starr's millimetre readout, reported by Inan, not asserted by the repo.
  `A:49` names Inan's directly-calibrated **4.06 N** as *"the cleaner citation"* if a reviewer presses.
  The proposal cites `[14]` as if read at the primary source, on the most canonical-looking number in
  the cardiac chain. Refs [15] and [16] are both READ-FULL and verbatim-clean.
  **Fix:** *"3.7 N (Starr 1939, as converted and reported in [15])"*, or lead with 4.06 N.
- **Krohn [13] is now the ONLY load-bearing citation still unverified.** `INPUT.md:273` promotes it to
  **"1 (now top)"** — *"The only load-bearing citation still unverified — everything else is now full
  text"* (SEG paywall, USD 42). `C-propagation-modeling.md:459-461` has it **READ-ABSTRACT**. It was #3
  of four unread at `f369eb0`; **the status change is in the delta the author missed.** The scoping is
  otherwise careful — "on soil" exactly matches the literature's *"firmness of the soil"* and preserves
  the RQ2 debris-vs-soil distinction. The defect is that the one unread citation reads identically in
  confidence to the three now-full-text ones.

## 19. markitdown silently DROPPED the Gantt chart
*methodological — affects any audit done from the `.md`*

The 11×12 activity table renders as **all-blank cells** in the markdown. The `.docx` encodes the schedule as
**cell shading**, not text: `word/document.xml` carries **31** cells at `w:fill="7F7F7F"`. I extracted it
from the XML directly.

**Ref [24] is also a conversion artifact, not a defect.** It looked truncated in the markdown; the
`.docx` carries it complete (*Department of Telecommunications, G.S.R. 564(E), 30 July 2008, 865–867 MHz*).
Same class as the Gantt — verified directly against the file.

**Any finding about the timeline drawn from the conversion alone is unsound** — and §9, §15 and the
over-committed terminal month are all visible *only* from the Gantt. **A reviewer reading the `.docx` sees
them; a reviewer reading the `.md` does not.** Belongs in the environment gotchas beside the two-column
interleave rule.

Reconstructed schedule:

| Activity | Months |
|---|---|
| Ambient in-band noise survey — **go/no-go** | 1, 2 |
| Tap force and spectrum (**volunteers**) — **go/no-go** | 1, 2 |
| **Preamp design; ethics application; procurement** | **1, 2, 3** |
| Build graded debris test pile | 2, 3 |
| Single-node wired chain; tap detection 1/3/10 m | 2, 3, 4 |
| Cardiac bound; manuscript **draft** | 4, 5, 6 |
| Coupling onto debris (RQ2) | 4, 5, 6 |
| **Mesh: time sync, TDoA, persistence (first radio work)** | **5, 6, 7, 8** |
| Air deployment: drop mechanism, survival, scatter | 7, 8, 9, 10 |
| Field trial: wide vs compact (RQ1) | 9, 10, 11 |
| Analysis, dataset release, final report | 11, 12 |

## 20. The SM-24 price: right number, unverifiable basis, own rule not applied
**Line 196** · ⚠ *downgraded from a subagent's BLOCKING*

₹7,140 / 84 = **USD 85.00 exactly — duty factor 1.000, no duty applied**, while the same +33% rule is
correctly applied to four other lines (Pi 5, GNSS, tools, node electronics — **all four reproduce to the
rupee**). **The author knew the rule and applied it everywhere except the largest line** (39% of the request).

And the stated basis cannot be checked: the **only** SM-24 price in the repo is **SparkFun USD 69.95**, a US
vendor. I grepped every Indian distributor named in the repo — **no SM-24 listing from any of them exists**,
and those vendors are recorded as 403-to-script, so the repo *could not* have priced one.

**Why I downgrade it — the exposure depends entirely on which price is real:**

| Basis | Landed/unit | Delta | ×10 units |
|---|---|---|---|
| Repo-verified USD 69.95 + 27.735% | ₹7,505 | +₹365 | **+₹3,655** |
| qty-25 break USD 66.45 + 27.735% | ₹7,130 | **−₹10** | −₹100 |
| The stated USD 85.00 + 27.735% | ₹9,120 | +₹1,980 | +₹19,803 |

The ₹19,803 figure assumes the unverifiable USD 85 is a real pre-duty price. **On the repo's own verified
figure the gap is ₹3,655, and at the qty-25 tier the proposal is right to within ₹10.** The number lands in
roughly the right place **by a wrong route** — harder to catch, and indefensible under challenge.

**Wider defect:** **the FX rate is the only date-stamped figure in the entire budget**, against
`02-vendor-register.md:119-121` (*"a BOM is a perishable artefact … needs a **pull date attached**"*). Line
196 converts a documented compliance rule into a future promise — precisely the move
`docs/memory/bom-prices-are-perishable.md` exists to prevent.

## 21. Six nodes is the bottom of the range the proposal criticises
**Lines 38, 40, 233**

> L38: incumbents use "six to eight cabled sensors placed by hand"
> L40: "drop **many** … larger **and denser** than hand placement allows"
> L233: "**Eight nodes give a six-node working array** … plus two spares"

**The funded working array is 6 — equal to the low end of the incumbent it criticises.** "Many" is not
funded. **"Denser" is untestable by construction:** RQ1 holds node count constant (*"For the same node
count"*), and density = count / area, so a fixed-count comparison varies only extent. **The density half of
the abstract's claim has no experiment anywhere.** Also 6 nodes → 5 TDoA equations against 4 unknowns
(x, y, z, v) = **redundancy 1**, zero margin for a node lost on the pile.

---

# MINOR

- **Donnelly [21] carries "[initials]"** — on the citation that justifies the whole negative result (sole
  support at line 147). **The repo cannot supply them**; needs an external lookup.
- **M6 promises "submitted"; the Gantt delivers "draft."** One-word fix either way.
- **M12 over-committed** — field trial ends month 11; analysis + dataset + final report + 2 manuscripts +
  a follow-on proposal all land in months 11–12. The follow-on proposal has **no Gantt row at all**.
- **Off-campus airspace unaddressed** — line 239 covers *campus* operation; the field trial (months 9–11)
  and "eight visits to demolition sites" are off-campus. `05-operational-kill-attempt.md:430-434` requires
  zone classification + Digital Sky UAOP **≥7 working days** ahead. No activity, milestone or budget line.
- **Duty cycle stated without its required hedge** — `INPUT.md:254-256` demands **[ASSERTED]** plus a power
  sensitivity (*"at 10 min/hour it is ~17%, a 2–3× error"*). The proposal takes 5–13% and drops both. **The
  only one of 13 do-not-claim items violated.**
- **"Matched filter" conflates two detectors** — impulse shape (ms, bandwidth domain) and tap pattern
  (seconds, rate domain) presented as one filter. The repo's architecture is explicitly **two-stage**. Mild,
  but it is the project's signature category error resurfacing.
- **Open-access APCs** — *Near Surface Geophysics* (Wiley) and *IEEE Sensors* named. **A single gold-OA APC
  exceeds the entire request.** Costs ₹0 to fix: elect subscription + green OA in one sentence.
- **Travel ₹1,500/visit** funds a solo day-trip, not a multi-day field trial moving 10 geophones, a ground
  station, a drone and a team.
- **Ref [12] has no DOI** while 10 other entries do. Cosmetic; consistent with the repo record.

---

# NOT AN ERROR — checked, and sound

## A1. "38–60 dB" and "+23 to +41 dB" are deliberately stale, and the proposal is RIGHT to use them

Post-correction values are ~31–53 dB and ~+29/+47 dB. **`00b:85-95` forbids substituting them:**

> "**The repo has deliberately NOT been bulk-edited to these new figures** … Re-deriving a margin from a
> corrected anchor and an unmeasured force would **manufacture false precision** … **Do not quote the 31–53 dB
> or +29/+47 dB figures as measured.**"

**Correct by policy.** This is the *stale-but-deliberate* distinction — and the author **independently
reproduced the policy without having been told**, because `INPUT.md`'s instruction block landed 18 minutes
after their document was created. Only residual exposure: a one-clause footnote (*"conservative by ~7.4 dB
after a 2026-10-08 anchor correction"*) would immunise it without restating anything. **~7.4 dB, not ~6.5:**
the proposal's baseline is 17 Hz, so its own correction is 17 → 40 Hz (+7.43 dB). The repo's +6.47 dB is the
19 → 40 Hz step from a baseline the proposal never used — see C7.

## A2. The blast radius of the stale base is bounded, and smaller than feared

Every pre-correction-only amplitude (36.5, 32.7, 0.187, 0.047, 0.511 µg) and every post-correction one
(76.9, 1.202, 0.439, 0.110): **zero occurrences.** The proposal quotes **no absolute amplitude from the
scaling chain at all** — only dB margins, which are deliberately frozen. **The stale base contaminated
exactly two things: the 17 Hz anchor (§1) and the Arosio framing (§11).**

## A3. Citation discipline is unusually good

- **No invented citations, no fabricated DOI, no figure without provenance.** All 24 refs trace to a repo
  record; every cross-checkable DOI matches exactly.
- **12 of 13 do-not-claim items compliant** (only the duty-cycle hedge missed) — including no `$15,000` cost
  ratio, no ±0.05 m, **BLIND** state present, 0.1 µg/√Hz correctly called *assumed*.
- **`−85.7 dB re 1 g` appears nowhere** — the un-asked trap the author was most likely to fall into, because
  `OLD-C-propagation-modeling.md:228` presented it as **SUPPORTED** at `f369eb0`. **They dropped it anyway.**
- **INACHUS [7]** — the sweep calls it *"the single most dangerous citation"*; the proposal matches the
  prescribed two-sided wording nearly clause for clause.
- **HeartQuake [10]** cited and distinguished exactly as mandated. **Sercel correctly NOT cited.**
- **Macintyre 2011 [4]** — correctly the Haiti paper, not the 2006 paper also in-repo. An easy confusion, avoided.

## A4. The physics that could have gone wrong, didn't

- **Terminology and scaling law fully clean** — "linear transfer-mobility scaling" with FTA cited; **zero**
  occurrences of "force-ratio scaling", "seismic moment", or energy-based scaling.
- **38–60 dB → "80 to 1,000 times" is correct as an amplitude ratio** (79.4× / 1000.0×). An energy reading
  would have given 6,310×–10⁶× — the factor-2-in-dB error the repo warns about. **Clean on exactly the point
  most likely to go wrong.**
- **Cramér–Rao** (2.71 m / 0.86 m at B = 35), **2 µs timing** (0.6 mm vs 3.5 m), **duty-cycle arithmetic**,
  **cardiac forces**, **ρ = 0.81–0.98**, **Krohn 100–500 Hz**, **all four SM-24 specs** — every one verified
  **exact**.
- **The rate-vs-bandwidth diagnosis (line 54) is textbook-correct** and correctly attributed as root cause.
  **The band disclosure at line 86 is better than `main`**, where `07-verdict.md:178` still lists 5–40 Hz
  under "Locked decisions" with no contested marker.
- **The circularity is broken by sequencing, not left circular** — force measured at Activity 2, prediction
  recomputed, *then* M4 compares. The proposal says so three times. **This is the model of disclosure.**
- **The cardiac bound is the soundest part of the document** — consistent in all five places, never upgraded
  to "measured", and the human-subjects logic is airtight.

---

# What I'd do next

**Send tadiPro only these, in this order** — all are cheap and all are theirs to fix:

1. **§1** line 90: `17 Hz` → `near 40 Hz`, split `[11, 12]`. *(one line)*
2. **§3** line 62: H3b must say **ADXL355**, not "the same floor". *(one phrase — biggest credibility win)*
3. **§9** Gantt: ethics to month 1, volunteers to months 2–3. *(free)*
4. **§15** Gantt: split the procurement row at the gate. *(free)*
5. **§4/§5** tag every dB figure with its band; fix line 82's 60–80 Hz. *(one sentence + tags)*
6. **§8** restate as 82–100% under the ≥60% rule — *the honest number is better*.
7. **§13** split H3a, or drop voice from the title until it is funded.
8. **§2** one prior-art row for SenSys'17 + PigV2.

**Fix in `main` yourself — these are ours, and four of them are blocking:**

- **§3** `INPUT.md:73-81` — the "the same floor" ambiguity that produced the worst finding.
- **§6** the `~1 mg` gate (`INPUT.md:132,152`) — **cannot return no-go for any real site**.
- **§7** `07-verdict.md:200` — the ≤1/node-hour target, never rescaled after the duty-cycle change.
- **§2** `INPUT.md`'s prior-art table — omits two papers carrying must-distinguish obligations.
- **§16** `INPUT.md:228`'s no-drone rung is arithmetically loose.
- **§18** `INPUT.md:99` conflates the SeismicDart fidelity figure across two sources.
- **§19** add the markitdown Gantt-dropping gotcha to `CLAUDE.md`.

**One decision only you can make:** the **tracked-`.docx` workflow**.

> ~~**Two decisions:** the tap band (5–40 vs 60–80 Hz — it moves the floor 16×, the margin, the
> preamp spec, *and* re-opens sensor selection via §12)~~ **— RESOLVED 2026-10-11, ADR 0001, and
> the framing was wrong.** The answer is **neither**: both figures lack tap provenance (5–40 Hz is
> a seismocardiography band, `01-physics-kill-attempt.md:290`; 60–80 Hz is *"NO DATA FOUND"*,
> `prior-art/C-propagation-modeling.md:241`). **Acquire 5–200 Hz; the detection band is an output
> of the M1/M2 bench measurement.**
>
> Two of this line's own premises were overstated and are withdrawn: the 16× floor swing is
> immaterial in absolute terms (Johnson noise is 0.00027–0.00439 µg/√Hz across 5–80 Hz —
> **23–365× of margin against the 0.1 µg/√Hz spec in either band**, so self-noise never binds),
> and **sensor selection does not re-open**: §12's −12.3 dB is real but confined below ~15 Hz
> (−0.72 dB by 15 Hz, ~0 above 30). What binds is **ambient**, which is unmeasured. §4/§5's fix
> stands and gets easier: **name the band inline on every dB figure** and tag the tap band
> `[ASSERTED — pending M2]`.

---

# Corrections made during this audit

**Every finding above was re-derived before being logged.** Four of those re-derivations changed a
result. They are recorded here because a finding's provenance is part of its weight — three of these
moved a number a reviewer would otherwise have quoted.

### C1. Consumables exposure — ₹22,502 → **₹15,053** (agent finding, corrected down)
The budget agent decomposed `INPUT.md:230`'s ₹84,577 as `84,577 − 62,075 = 22,502` consumables
(97.4 % of the line). The subtraction reproduces, **but it omits the airframe's own contingency.**
`INPUT.md`'s contingency is 12 % of direct cost (verified: `1,85,620 × 0.12 = 22,274` exactly), so:

```
84,577 = 62,075 (airframe) + 7,449 (its 12% contingency) + 15,053 (drone consumables)
```

Real exposure **₹15,053 (65.2 % of the line, 8.2 % of request)**, not ₹22,502 (97.4 %, 12.3 %).
**A second defect fell out of the correction** — `INPUT.md:228`'s "No drone — ₹1,23,317" is a flat
subtraction leaving contingency on the with-drone base; correct values are ₹1,38,370 or ₹1,13,168.
Neither matches. That one is `main`'s, not the PR's (§16).

### C2. SM-24 price exposure — ₹19,803 → **₹3,655** (agent finding, corrected down, severity downgraded)
Reported as BLOCKING on the assumption that the unverifiable USD 85 is a real pre-duty price. On the
repo's own verified USD 69.95 the gap is **₹3,655**, and at the qty-25 tier the proposal's number is
right to **within ₹10**. Downgraded BLOCKING → SHOULD-FIX (§20). The defect that survives is the
*route*, not the magnitude: the +33 % rule is applied to four other lines and not this one.

### C3. Tap:cardiac discrepancy — 5–29 dB → **29–45 dB** (agent finding, corrected **up**)
The physics agent reported the H3a/H3b internal contradiction as 5–29 dB. Recomputing against
`00b:177-183`'s +32 to +56 dB: `61−32` and `101−56` → **29–45 dB**. **This correction made the
finding worse, not better** (§3).

### C4. My own §4 — graded MINOR, corrected to **BLOCKING**
I first excused the 60–80 Hz noise-floor band because its error direction is conservative.
**Direction is not the issue.** The sentence carrying the entire sensor-selection argument is
parameterised in a band the document rejects two paragraphs later, and three dependent claims inherit
it. Re-graded.

### C5. Withdrawn — the FEMA/NFCC `[2, 3]` cite is **not** a misattribution
Mid-audit I logged proposal line 36's *"roughly once an hour … All Quiet [2, 3]"* as crediting FEMA
with a cadence only NFCC supplies, and queued it as a should-fix. **Reading line 36 directly, that was
wrong.** The sentence asserts two facts — the hourly cadence (NFCC, `B-usar-systems.md:155`) **and**
the commanded signal (FEMA, `B:145`) — so the joint cite is legitimate. It is **not** the same defect
as the ρ conflation at §18. Withdrawn, not logged. The citation agent caught this.

## C6. PigV2 cited to the wrong venue, and distinguished on the wrong ground — 2026-10-11

Found while reflecting this audit's obligations into `docs/research/`. Two errors in §2's suggested
prior-art row, both mine, both already published in issue #4 item 8:

| | Audit said | Verified |
|---|---|---|
| Venue | SenSys '22 | **arXiv 2212.03378** (`MEMS/03-literature.md:38`) |
| Distinguishing ground | "contact-coupled at centimetres" | **distance and medium** — PigV2 is *through the ground* |

The second is the substantive one. Lumping PigV2 with HeartQuake and Jia under "contact-coupled"
**concedes the distinction**: PigV2's whole contribution is that the path is structural, through a pen
floor. A referee who reads the row as written sees the one paper whose geometry matches ours waved off
on a ground that does not apply to it. The surviving grounds are centimetres-of-slab versus
metres-of-debris, and the 100–200 m/s velocity bracket this project already borrows from PigV2.

Recorded in `docs/critique/prior-art/README.md` alongside HeartQuake, where obligations belong — it
had been sitting only in an extract.

---

## C7. §1 paired the proposal's 17 Hz baseline with the repo's 19 Hz dB figure — 2026-10-11

Found while scoping the `main` fixes for handoff. `INPUT.md:76` says the anchor correction was
**"19 Hz → 40 Hz"**; this audit's §1 says **17 Hz**. Both are faithful to their sources — the proposal
says 17 Hz, the repo's withdrawal record (`C-propagation-modeling.md:227`) says 19 Hz — and the repo
is internally consistent: `00b:65` strikes 32.7 µg as superseded and `07-verdict:313` calls it
*"the interim 17 Hz"*.

**The defect was mine, and it was the dB figure, not the frequency.** §1 presented a 32.7 µg → 76.9 µg
step — a 17 Hz baseline — as worth **+6.47 dB**, which is the **19 → 40 Hz** step:

| Baseline | Amplitude @ 3 m | → 40 Hz |
|---|---|---|
| 17 Hz (the proposal's) | 32.68 µg | **+7.43 dB** |
| 19 Hz (the repo's) | 36.52 µg | **+6.47 dB** |
| 40 Hz (correct) | 76.88 µg | — |

Off by 0.97 dB for the document being reviewed. Corrected in §1 and in §A1's suggested footnote, which
had carried ~6.5 dB into advice aimed at the proposal. **No margin was restated on either value** — the
§A1 freeze holds, so nothing downstream moves.

---

**Net:** of four agent findings re-derived, three moved (two down, one up); of my own, one was
re-graded up, one withdrawn entirely, and two (C6, C7) corrected after publication.

---

*This audit modified no file it audits. The proposal, `INPUT.md` and `07-verdict.md` are untouched.*

*Exception, 2026-10-11: C6 corrected this file itself, and the obligations in §2 were reflected into
`docs/critique/prior-art/README.md` and `docs/research/MEMS/README.md`. Neither is a file this audit
reviews — the PR and the proposal remain untouched.*
