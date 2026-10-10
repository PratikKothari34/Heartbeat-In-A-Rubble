# docs/critique/ - adversarial review, 2026-10-07

Ruthless critique of the pipeline, components and costing as specified in `docs/MASTER.md`, plus an
audit of the prior research passes. Six parallel kill attempts, each briefed to **destroy** its
assigned area, then adjudicated into a single verdict.

**Read `07-verdict.md` first.** It supersedes the individual critiques where they conflict.

**Nothing outside this folder was created or modified.** `MASTER.md`, `docs/research/` and
`docs/reference/` are untouched by design.

> **UPDATE 2026-10-08.** A three-agent prior-art sweep now sits in **`prior-art/`** and amends this
> folder. The kill is **confirmed and better evidenced** (the cardiac force is now *measured*), but
> **the novelty claim has moved** and three numbers here were wrong. Read **`prior-art/README.md`**
> after `08`. `MASTER.md` has since been given a superseded banner; it is no longer untouched.

## The bottom line

The **heartbeat premise is dead** - the cardiac signal sits **38-60 dB below the ADXL355 floor**
(25 ug/rtHz - the MEMS part MASTER 3.2 specifies, **not** the SM-24 that replaced it; derivation
`00b-verification-arithmetic.md:26`), and MASTER 3.3's unmeasured 0.1-1 mg assumption is **wrong by
479-19167x**.

> **Corrected 2026-10-11.** This line previously read *"47-69 dB below the chosen sensor's own noise
> floor."* Both halves were wrong. **47-69 dB** is the pre-amendment figure, superseded by **38-60 dB**
> once the cardiac source force was measured (`00b:26`). And **"the chosen sensor"** now reads as the
> **SM-24**, against whose *element* floor the cardiac signal is **positive** - the deficit is an
> **ADXL355** number only. The premise still dies, by ~31-53 dB after propagation (`00b:73`), but it
> dies **on the propagation path, not on sensor self-noise.** Do not quote 38-60 dB against any sensor
> but the ADXL355, and do not restate it as 31-53 dB - that figure is frozen under `00b:85-95`.

The **system survives**, because the error that killed the premise was one conceptual slip: MASTER 6
filters 0.5-4 Hz, which is the heartbeat's **repetition rate**, not its **signal bandwidth**.
Correcting it reverses 3.2's rejection of the SM-24 geophone - and with that one swap, the same
drone, mesh, TDoA solver and time sync detect **taps and voice at +23 to +41 dB** instead of failing
at -47.

**One problem remains unsolved, and it is not physics:** false alarms (~16% PPV, and a concurrence
vote that assumes independence real rubble does not provide).

## Files

| File | What it is |
|---|---|
| **`07-verdict.md`** | **The synthesis: verdict, deduplicated findings register, conflicts adjudicated, rebuilt design, residual risk** |
| `00-my-own-arithmetic.md` | My 7 findings on MASTER's *stated* numbers, derived **before** any critic reported |
| `00b-verification-arithmetic.md` | My independent check of the critics' *kill claims* - the 47-69 dB deficit, the tapping salvage, the geophone reversal |
| `01-physics-kill-attempt.md` | Propagation, source amplitude, coupling. **Verdict: PREMISE DEAD.** Salvage paths S1-S4 |
| `02-dsp-ml-kill-attempt.md` | 11 findings, 3 FATAL: the band error, the CRLB, and the base-rate/PPV collapse |
| `03-hardware-kill-attempt.md` | Node, impact, mass, power. Self-corrected twice - see below |
| `06-prior-research-audit.md` | Prior claims re-verified: CONFIRMED / WEAKENED / OVERTURNED |
| `04-cost-kill-attempt.md` | Procurement audit. **$9,746 capital (5.3x), and the build is illegal as specified** - DGFT prohibits drone kit import |
| `05-operational-kill-attempt.md` | CONOPS audit. **Sensitive listening happens inside a commanded hourly "All Quiet" (~5-8% duty)** |
| **`08-amendment.md`** | **Amends 07 for 04 and 05. Read after 07.** Persistence fixes the PPV problem; compliance breaks the cost claim |
| **`09-pr3-citation-audit.md`** | **OPEN REVIEW of unmerged PR #3, 2026-10-09.** Audits the proposal .docx against `f73b73d`: 10 blocking, 12 should-fix. Four of the blocking defects are in `main`, not the PR |
| **`10-doc-sweep-action-report.md`** | **Action report, 2026-10-11.** Full `docs/` sweep: what was stale, what was corrected, what was deliberately left as historical record, and what is still open. Start here for the state of the band decision and the floor referent |
| **`11-closed-issue-archive.md`** | **Archive of issues #1 and #2, 2026-10-11**, written immediately before they were deleted from GitHub. Holds the anchor correction, three methodological lessons that each caught a real error, and the record of Krohn 1984 as the last unheld citation. `#4`/`#5` still say "do not work from #1's figures" — this is where #1 went |
| **`prior-art/`** | **Literature sweep, 2026-10-08. Amends everything above.** `A` cardiac force (now measured), `B` USAR systems + drone prior art + doctrine, `C` propagation parameters validated row by row |

## Why this is trustworthy

- **`00` and `00b` were written before reading the critics' outputs**, so agreement is corroboration,
  not an echo chamber. It held: `03` independently reproduced 200 G, 15.5 g and ~4 m node position;
  `06` independently reproduced the packet failure under a *stricter* assumption than mine.
- **The critics corrected themselves against their own briefs**, which is recorded because it cuts
  against the critique: `03` found the F450 flight-time claim **survives** and that its brief's
  coupling premise was **inverted** (a light sensor couples *better*); `01` found its own premise #5
  wrong in acceleration.
- **Conflicts were adjudicated, not averaged.** `01`'s coupling condition C4 is **struck** in favour
  of `03`'s explicit calculation - see `07` section 3.
- **Each document states what it could be wrong about.** `00b` section G names the SM-24 noise figure
  and tap spectrum as the two assumptions the rebuilt architecture actually rests on.
- **What survives is recorded too:** the Table-II regulatory finding, the supercap recharge
  principle, the F450 endurance claim, LongShoT's <2 us sync, and the in-band coupling result.

## Cheapest next steps

Nothing here requires buying anything:

1. **Delete the 0.5-4 Hz filter.** Wrong on every path. Free.
2. **Re-run the 3.2 sensor trade.** ~~Vendor-verify the SM-24 noise density~~ -
   **there is no vendor noise figure; the datasheet has none.** The computed element floor is
   23-30x *better* than assumed, so the margin holds and this is no longer the critical number.
   **Specify the preamplifier instead** - it sets the system floor (12-16x margin at 4 nV/rtHz).
3. **Do NOT run MASTER 12 step 1 as written** - arithmetic already determines its outcome.
4. **Bench-test a tapping source at 1/3/10 m**, then **repeat it with an excavator running** - the
   false-alarm test, which attacks the only unsolved problem. **Measure tap force and tap spectrum
   while you are there**: the 50-300 N / 60-80 Hz figures have no source, and every margin in `07`
   scales off them. This is now the highest-value measurement in the project. **[ADR 0001, 2026-10-11: the spectrum measurement *sets* the tap detection band rather than checking one - neither 60-80 Hz nor 5-40 Hz was ever derived from a tap. Acquire 5-200 Hz; where one figure is unavoidable write `20-80 Hz [ASSERTED - pending M2]`.]**
5. **Decide S1 vs S4 before the deferrable $739 airframe.**
