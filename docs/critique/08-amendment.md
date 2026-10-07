# 08 - Amendment to the verdict: the two late critics

**Date:** 2026-10-07. **Amends:** `07-verdict.md`, per its own section 8 commitment to amend rather
than defend if `04` or `05` contradicted a locked decision. **Both did.**

`07` was written while `04-cost-kill-attempt.md` and `05-operational-kill-attempt.md` were still
running. Neither reverses section 1 of `07` (the cardiac kill, which rests on sensor noise floors and
the CRLB). **Both change what the rebuilt system in section 4 should be.**

Verification scripts: `scratchpad/ops.py`, `scratchpad/cost2.py` under `py -3.12`.

---

## 1. Summary of the amendment

| `07` said | Amendment |
|---|---|
| False alarms are "the one unsolved problem", no mechanism offered | **A mechanism now exists**: persistence across hourly All Quiet windows. **PPV 16% -> 70-98%** |
| Cost model: state it as quadratic in 1/r | Still true, but **the base is wrong**: $1,845 -> **$9,746 capital**. Add a **compliance axis that no engineering choice removes** |
| "Continuous monitoring" implicitly assumed | **False.** Sensitive listening happens inside a commanded site-wide "All Quiet", ~5-8% duty. The system **does not control its own listening schedule** |
| Runtime: 25 h contested vs 116-307 h | **Requirement is 138-163 h**, not 72 h (Macintyre). Fails continuous; **passes easily duty-limited** |
| Localization +/-3.5-5 m, TDoA retained | **TDoA may be the wrong output entirely** - Delsar operators don't trilaterate, they hill-climb by repositioning |

**Net effect: the rebuilt system gets *better*, and its cost claim gets *worse*.** Those are
independent, and both must be said.

---

## 2. `05` - The CONOPS finding, and why it is the best news in the whole set

### 2.1 The fact

**Sensitive listening in USAR happens inside a commanded, signalled, site-wide "All Quiet"** -
roughly once per hour, for a few minutes. Four independent source classes agree (UK NFCC doctrine
verbatim, FEMA US&R "All Quiet / Cease Ops = 1 Long Blast", Fire Engineering practitioner
literature, AP reporting from Adana 2023 and Colombia 2026).

**[VERIFIED]** duty-cycle arithmetic:

| Silence length | Duty | 7-day op: wall clock | **Actual sensing** |
|---|---|---|---|
| 3 min/h | 5.0% | 168 h | **8.4 h** |
| 5 min/h | 8.3% | 168 h | **14.0 h** |
| 8 min/h | 13.3% | 168 h | **22.4 h** |

### 2.2 Why this reverses two "crises"

MASTER 4.1's power agony and 10.2's radio crisis **are both artifacts of a CONOPS nobody wrote.**

- A 7-day deployment needs **8.4-14 h of sensing**, not 168 h. **MASTER's own contested 25 h budget
  covers it with margin.**
- Runtime requirement is **138-163 h** of *presence* (Macintyre: avg max 6.8 d, median 5.75 d - so
  MASTER's 72 h framing is wrong in the direction that hurts, by 1.9-2.3x). Continuous sensing fails
  this by 6.5x. **Duty-limited at 0.73 mA: 307 h. Passes.**
- Channel occupancy (`06`: 32.3% at 11 nodes) was computed for continuous operation. Under
  command-triggered bursts the airtime problem **largely dissolves**.

**The correct architecture is command-triggered, not autonomous.** The incident commander already
signals the All Quiet; the node can be *told* when to listen rather than inferring it. That is the
cheapest sensor-fusion input available and it **deletes section 11's adaptive-threshold hand-wave.**

### 2.3 Persistence: the first real answer to the PPV problem

`07` section 4.3 named false alarms as the binding unsolved risk and offered no mechanism. `05`
proposes one: **20-100 independent looks at the same cell across successive silences.** A survivor is
persistently present; noise is not.

I computed what `05` asserted but did not quantify (per-look FPR 7%, sensitivity 93%, prior 0.0139):

| Looks | Threshold | **PPV** |
|---|---|---|
| 6 | >=2 of 6 | 18.8% |
| 6 | **>=3 of 6** | **70.7%** |
| 6 | **>=4 of 6** | **97.8%** |
| 12 | >=4 of 12 | 65.2% |
| 20 | >=4 of 20 | 23.0% |

**Two conclusions `05` did not draw:**

1. **The threshold must be a *fraction* of looks, not a fixed count.** A fixed ">=4" degrades as looks
   accumulate (97.8% at 6 looks -> 23.0% at 20) because false positives keep accruing. Roughly
   **>=60% of available looks** is the right rule.
2. **The independence assumption is far more defensible here than in `02` F3.** `02` correctly killed
   the 3-of-9 *across-nodes* vote, because an excavator hits every node within the same minute
   (common-mode). But **across hours, the machine moves, the crew rotates, the site changes.**
   Temporal independence is a much weaker assumption than spatial independence. **This is the real
   advance.**

And it is **immune to the HRV-vs-coherence conflict** (`00` #6, `02` F4), because it correlates
*detections*, not waveform phase. A hand-carried Delsar **structurally cannot do this** - it leaves
with the operator. **Persistence is a capability the incumbent cannot have, and it is the strongest
contribution identified anywhere in this critique set.**

### 2.4 Corrections against `05`

- **RX current: `05` says 1-2 mA. SX126x datasheet RX is ~4.6-5.5 mA** (DC-DC, BW125). `05` is low by
  ~3x, so **the mesh contradiction is worse than it reported**: at 100% RX duty a CR2032 (225 mAh)
  lasts **41-49 h**, not days. The conclusion stands and strengthens; the number was wrong.
- **TDoA vs hill-climbing is a genuine design question, not a settled one.** `05` is right that Delsar
  operators reposition sensors to close in, and that fixed dropped nodes remove that freedom. But
  amplitude-ratio localization needs a known source amplitude and attenuation model - and `02` F7
  already killed depth-from-amplitude for *exactly* that reason (two unknowns, zero equations).
  **Amplitude-ratio area localization inherits the same weakness.** Verdict: keep TDoA for the
  corrected 5-40 Hz band (where `00b` D shows pick error is sub-metre), **but output a cell, not a
  pin** - which is `05`'s real point and is correct.

---

## 3. `04` - The compliance finding, and one overstatement corrected

### 3.1 What reproduces exactly

**[VERIFIED to the cent]**

| Claim | `04` | My recomputation |
|---|---|---|
| India landed-cost stack, duty + tax | $348.12 (33.0%) | **$348.12 (33.0%)** |
| Same, floor case all at 7.5% band | $292 | **$292.49** |
| Regulatory block total | $2,758 | **$2,758** |

The cumulative stack `BCD -> SWS = 10% of BCD -> IGST on (CIF+BCD+SWS)` is correct, and **§9 quotes
US vendor prices for an Indian build with no tax, freight or brokerage line at all.** That alone
understates by ~1/3 before any other error.

### 3.2 The two regulatory walls

- **DGFT prohibits drone import in CBU/CKD/SKD form (9 Feb 2022).** §8.6's *recommended* Path B is an
  F450 **kit** - a complete disassembled airframe, the textbook CKD definition. Components are
  explicitly free to import; the frame kit is not. §8.6 did the DJI SDK homework correctly and then
  recommended a part that **cannot lawfully enter the country**. Domestic assembly from
  separately-sourced components: $1,035 at Indian retail vs §8.6's $738.99.
- **WPC ETA is per-device-model and requires an accredited-lab test report.** §9 budgets **$0**.

### 3.3 Overstatement corrected: the advantage compresses, it does not vanish

`04`'s verdict says the cost advantage "does not survive" and that the project is "more expensive
than the incumbent." **On capital that is too strong.** Recomputed against Delsar's $15,000:

| Basis | Total | vs Delsar |
|---|---|---|
| MASTER §9 as written | $1,845 | 8.13x cheaper |
| **`04` capital, all-in** | **$9,746** | **1.54x cheaper** |
| `04` honest node count (r = 3 m) | $10,957 | 1.37x cheaper |
| **`04` with junior-engineer labour** | **$14,145** | **1.06x cheaper** |
| **`04` if §10.1 returns r = 1 m** | **$26,270** | **1.75x MORE EXPENSIVE** |

**Honest statement: the 8x advantage collapses to ~1.0-1.5x, and inverts only conditionally on
detection range.** It does not unconditionally invert.

**This is still fatal to the headline claim**, because a 1.06x edge over a delivered, certified,
trained, warranted instrument is no edge at all - and `04`'s central point is exactly right: **§9
compared this project's bare component prices against a competitor's delivered kit price.** But the
defensible sentence is "the advantage compresses to nothing," not "the project is more expensive."

### 3.4 `04`'s softest number, as it flagged

The **WPC ETA lab cost at INR 150,000 is [EST]** and is **65% of the entire regulatory block**:

| ETA assumption | Regulatory block |
|---|---|
| `04`'s EST (INR 150k) | $2,758 |
| `04`'s own low case (INR 50k) | $1,568 |
| Bench-only R&D waiver, no TX | $973 |

`04` was right to flag this as its weakest input. **Even at the floor the omitted line is ~$1,000**,
so the finding survives its own uncertainty - but the headline $2,758 should be quoted as a range.

---

## 4. Do the two late critics overlap? No - and that matters

**They attack orthogonal axes, so neither cancels the other:**

- `05` (CONOPS) attacks **power, BOM, runtime, mesh RX**. Its fix - duty-cycled, command-triggered
  sensing - genuinely relieves all four.
- `04` (compliance) attacks **import legality, type approval, duty/tax, labour**. **The regulatory
  block is independent of duty cycle, and the DGFT import ban is independent of every technical
  choice in the project.**

So `05`'s good news does not pay for `04`'s bad news. **The rebuilt system is more buildable than
`07` thought and less cheap than MASTER thought, simultaneously.**

---

## 5. Amended locked decisions (supersedes `07` section 4.2)

Unchanged: SM-24 geophone, 5-40 Hz band, tap/voice target, cardiac as stretch only, ~200 G impact
design, drop ICA / depth-from-amplitude / ECG-LSTM.

**Changed or added:**

| Parameter | Amended value | Source |
|---|---|---|
| **Operating mode** | **Command-triggered during All Quiet**, not autonomous continuous | `05` |
| **Duty cycle** | **~5-8%**, set by the incident commander, not by the design | `05` |
| **Runtime requirement** | **>=138-163 h presence** (not 72 h); met duty-limited | `05` + Macintyre |
| **Primary discriminator** | **Persistence across silences, >=60% of available looks** - not the LSTM | `05`, quantified here |
| **Output** | **DETECTED / NO DETECTION / BLIND per cell**, 2-5 m. **Never a pin. Never a clearance** | `05` |
| **False-alarm spec** | Replace "93% accuracy" with **<=1 false pin per node-hour on empty rubble** | `02` F3 + `05` |
| **TDoA** | **Keep** for 5-40 Hz (sub-metre picks), but **output a cell**; do not invest further in timing | `00b` D, adjudicated vs `05` |
| **Airframe** | **Assemble domestically from components.** Do NOT buy an F450 kit - import prohibited | `04` |
| **Compliance budget** | **$973-2,758**, non-optional, non-engineerable. ETA dominates and is [EST] | `04` |
| **Landed cost** | Apply **+33%** to every US/Chinese vendor price | `04` |
| **Honest cost claim** | **"~1.0-1.5x the incumbent, inverting if r < 1 m"** - NOT "10x cheaper" | `04`, corrected |
| **Operator** | Credentialed agency (NDRF/SDRF) under its own airspace authority | `04`, `05` |

---

## 6. Amended next steps

`05`'s minimum viable experiment is **cheaper and more decisive** than `07` section 4.4 and replaces
items 1-4 there. Decision rules are written down **before** measuring.

**Step 0 - free, tonight.** Smartphone accelerometer, person lying still at 0.5 / 1 m. Can only
return good news or no news.

**Step 1 - one ADXL355, ~INR 1,500-3,000, four measurements, each able to stop the next:**

1. **Ambient in-band floor in a normal, un-silenced building.** If > ~1 mg, the premise is dead at
   any sensor price - no filter removes in-band noise. **Run this first.**
2. **Coupling loss through a slab at 0.5 / 1 / 2 / 3 m.** Returns r, which **sets cost as 1/r^2** and
   decides whether `04`'s $26,270 inversion case is live.
3. **Repeat (1) with an angle grinder running 5-10 m away.** `05` calls this the measurement nobody
   proposed, and it **decides the CONOPS** - if SNR is usable at 20-30 m from running machinery,
   continuous monitoring returns as a real advantage and `05`'s lead finding weakens substantially.
4. **Persistence: 20 present / 20 absent windows, scored as detections.** Tests the one surviving
   advantage, and calibrates the >=60%-of-looks threshold computed in section 2.3.

**Then, before any spend:** ~~confirm the SM-24's 0.1 ug/rtHz with the vendor~~ **AMENDED 2026-10-08:
impossible - the SM-24 datasheet carries no noise specification at all, so 0.1 ug/rtHz was never a
vendor figure. The computed element floor is 0.003-0.005 ug/rtHz, making the assumption conservative
by 23-30x. Specify the preamplifier instead; it sets the system floor. See `prior-art/C`.** The
superseded text read: confirm the SM-24's 0.1 ug/rtHz with the vendor (`00b` G - the one number
the architecture rests on), and get a written ETA quote from an accredited lab to replace `04`'s
[EST].

**Still binding from `07`:** do **not** run MASTER §12 step 1 as written; delete the 0.5-4 Hz filter;
decide S1 vs S4 before the deferrable airframe spend - which is now **also** blocked on the import
finding, so the airframe decision is deferred twice over.

---

## 7. What the full six-critic set did not break

Recorded so it is not re-litigated: the Table-II regulatory finding (Gazette verbatim), the supercap
recharge *principle*, the F450 **flight-time** claim (`03` attacked and withdrew), LongShoT's <2 us
sync, the in-band coupling result (`03`'s calculation, `01`'s C4 struck), and the E17 link-checker
catch.

**And the contribution itself survives all six attacks, in amended form:** a drone-deployed,
command-triggered, persistently-listening seismic-acoustic mesh that tells a search planner **which
cells deserve the next breach**. Its edge is **coverage and persistence** - not accuracy, and no
longer cost. **No incumbent can do persistence, because every incumbent leaves with its operator.**
