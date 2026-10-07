# 07 - Verdict: the bulletproof idea

**Date:** 2026-10-07. **Inputs:** `00`, `00b` (primary agent), `01`, `02`, `03`, `06` (critics);
`04` cost and `05` operations pending at time of writing - see section 8.
**Scope:** this document supersedes the individual critiques where they conflict. It changes nothing
outside `docs/critique/`. `MASTER.md`, `docs/research/` and `docs/reference/` are untouched.

---

## 1. The verdict in one page

**The stated premise is dead. The system is not.**

Those are separable claims, and keeping them separate is the whole point of this document.

**Dead:** detecting an unconscious victim's *heartbeat* through rubble with a MEMS accelerometer.
Not "hard", not "needs better DSP" - **short by 47 to 69 dB** against the chosen sensor's own noise
floor, confirmed by two independent routes (`01` via propagation, `00b` via footstep calibration).
Closing even the optimistic end needs 2.8 hours of phase-coherent integration; closing the
realistic end needs 278 hours. HRV - the feature required to prove the signal is human - destroys
the phase coherence that averaging requires. **There is no parameter choice that recovers this.**

**Alive, and more valuable than it looks:** everything else. Drone deployment, the LoRa mesh, TDoA
triangulation, LongShoT time sync, node mechanics, the dashboard, the cost argument, and the actual
novel contribution. Pointed at a **tapping / conscious-victim** signature instead, the same hardware
clears its noise floor by **+23 to +41 dB** - and the measured gain over cardiac, **+32 to +56 dB**,
is precisely the deficit that killed the original premise.

**One component swap makes this work, and it is a decision the spec already made backwards.**

> MASTER 3.2 marks the ADXL355 **FIXED** and rejects the SM-24 geophone because its 10 Hz corner is
> "above the entire target band." That is only true of the *wrong* band. Against the corrected band,
> every tapping case is **BURIED on the ADXL355 (-7 to -25 dB)** and **DETECTED on the SM-24 (+23 to
> +41 dB)**. The geophone's 48 dB noise-density advantage is not an optimisation - **it is the entire
> detection margin.**

So the headline is not "the project failed." It is: **the project was one filter and one sensor
choice away from a defensible system, and both errors trace to the same root cause.**

### The root cause, stated once

**A rate was mistaken for a bandwidth.** 60-120 bpm is how *often* the beat repeats; the beat itself
is a broadband impulse with a ~50-150 ms rise. MASTER 6's 0.5-4 Hz bandpass is matched to the
repetition rate and **discards the signal**. Everything below is downstream of that single error:

- it throws away ~48% of impulse energy and keeps 2 harmonics (`02` F1);
- it destroys TDoA timing, because `sigma_t ~ 1/(B*sqrt(SNR))` - **narrowing the filter degrades
  localization**, turning 0.86 m into 8.57-27 m (`00b` D);
- it made the aftershock high-cut ineffective;
- and it caused the geophone rejection, the single highest-value correction available.

**Why three rigorous prior passes missed it:** they verified *arithmetic* and *link liveness*, never
*whether the right quantity was being computed*. `06` demonstrates this concretely - the prior ToA
is **0.370688 s, not 0.3052 s**, and no combination of CR/header/CRC/LDRO/preamble reproduces the
old figure, so four "16/16 verified" downstream numbers all inherit one wrong constant. The numbers
reproduced perfectly. They reproduced from a wrong premise.

---

## 2. What is fatal, what is fixable, what survives

Deduplicated across all six sources, severity-ranked. "x2" marks findings two agents reached
independently - the strongest evidence in the set.

### FATAL to the stated premise

| # | Finding | Source |
|---|---|---|
| 1 | Cardiac signal is **47-69 dB below the ADXL355 floor** at 3 m, before propagation loss | `00b` A, `01` x2 |
| 2 | MASTER 3.3's **0.1-1 mg premise is wrong by 479-19167x**. The "unmade $2 measurement" is already decided | `00b` A.1 |
| 3 | Closing the deficit needs **2.8 h - 3.2 yr** of coherent integration, and **HRV forbids the coherence** | `00b` B, `02` F4, `00` #6 |
| 4 | **0.5-4 Hz band is matched to the rate, not the signal** - the root cause | `02` F1, `01` x2 |

### FATAL to the operational claim, and NOT fixed by the tapping pivot

| # | Finding | Source |
|---|---|---|
| 5 | **PPV ~16% at a realistic prior** - five of six pins false. Needs spec >= 99.85%, has 93%: **48x short**. Empty rubble yields **907 false pins/day**. "Tuned for low false-negative rate" moves PPV 15.8% -> 16.5%: **the tuning direction does not help** | `02` F3 |
| 6 | The 3-of-9 concurrence vote assumes **independent** false positives. Real noise - excavator, generator, aftershock, crew - is **common-mode**. The vote defends against the noise that was never the problem | `02` F3 |

**This is the most important thing in this document after the verdict.** The tapping pivot fixes
amplitude. It does **not** fix false alarms, and a 93%-accuracy target is not a specification of
anything operationally meaningful. **Item 5-6 is the binding risk on the rebuilt system.**

### Fixable - real errors, known fixes

| # | Finding | Fix | Source |
|---|---|---|---|
| 7 | **Node position +/-2-5 m**, not +/-0.05-0.1 m (GPS CEP + post-impact bounce): **30-70x gap** | Spec honestly; it is the dominant error term | `00` #3, `03` x2 |
| 8 | **STM32WLE5JC has 64 kB SRAM**, not 100 kB. The 60 s x 100 Hz x 3-axis buffer alone is **70.3 kB = 110% of RAM**. Section 10.3 **reopened**, BOM part disqualified | Stream/decimate, or change MCU | `06` |
| 9 | Scheme C's 24 B holds **2.0-2.13 bits/beat**; needs **82 B** (1 ms) to **156 B** (2 us): short **5.5-6.5x** | Resize packet | `00` #5, `06` x2 |
| 10 | Power budget has **zero receive current**. "A node that never listens is a beacon, not a mesh node." 1.07 mA/211 h -> **0.73-1.93 mA / 116-307 h** | Re-budget with RX | `06` |
| 11 | Channel occupancy **32.3% @11 nodes, 83.2% @20** with ALOHA + ACK + relay, vs 5.59% claimed | Re-plan airtime | `06` |
| 12 | Impact is **200 G at 15 mm crush** (1000 G at 3 mm); 15-20 G needs **150-200 mm**. Node is 15 mm tall | Redesign for ~200 G, or add crush | `00` #1, `03` x2 |
| 13 | Node mass **15.52 g vs 8 g** claimed (1.94x) | Re-budget endurance | `00` #2, `03` x2 |
| 14 | ToA **0.370688 s, not 0.3052 s**; duty **0.618% / 6.80%** | Arithmetic correction | `06` |
| 15 | **+13 dB is a legal ceiling, not a reachable gain.** BOM radio caps at +22 dBm -> **<=8 dB, 1.69x range**; no PA budgeted. Rule 5 makes **type approval mandatory regardless** | Re-scope link budget | `06` |
| 16 | Orderable KEMET supercap at **25 Ohm ESR drops 1.00 V at 40 mA** - recreates the brownout it was bought to fix. Only <=100 mOhm CAP-XX class works | Change part | `06` |
| 17 | **Cost scales as 1/r^2**: 400 m2 costs $1,506 at r=3 m, **$13,550 at r=1 m, $54,200 at r=0.5 m** | Model cost as quadratic | `00` #7 |
| 18 | Coverage table ignores its own `d = r*sqrt(2)` spacing rule - node counts understated up to **3.1x** | Recompute | `00` #7 |
| 19 | ICA invalid here (convolutive, not instantaneous mixing); "N-1 sources with N sensors" is the **beamforming null theorem, not an ICA result** | Drop ICA | `02` F6 |
| 20 | Depth-from-amplitude: **two unknowns, zero equations** | Drop or add constraint | `02` F7 |
| 21 | Training on ECG to detect seismic impulses is a **category error**; LSTM likely untrainable at this data scale | Redesign detector | `02` F8-F9 |
| 22 | Pixhawk 6C Mini $49 saving verified on **PWM count only** - UART, IMU redundancy, CAN, flash never compared | Verify or revert | `06` |
| 23 | Self-righting "solved, ~$0" **conflates orientation with mechanical coupling**. The MEMS pass's own 6.1 calls the spike/anchor interface *"unsolved... the dominant term... this project's actual contribution"* | Reopen | `06` |

### Survives scrutiny - do not re-litigate

| Claim | Status |
|---|---|
| G.S.R. 853(E) **Table-II exists** with the buried-victims note; 865-868 MHz band; MASTER cites the superseded 2005 instrument | **CONFIRMED** - Gazette PDF pulled independently, verbatim |
| Supercap **recharge timing**: 5*tau = 11-33 s vs 60 s budget, leakage <=1.9% | **CONFIRMED** (principle sound; part wrong - item 16) |
| F450 airframe **25 min with 9 nodes** | **CONFIRMED** - `03` attacked it and withdrew |
| **LongShoT <2 us** sync | **CONFIRMED** - and now over-engineered by ~10^4 (section 3) |
| E17 link-checker bug | **CONFIRMED** - a real, honestly self-reported catch |
| **Coupling is fine in-band** | **AMENDED 2026-10-08 - PARTLY OVERTURNED.** Krohn (1984) *measures* coupling resonances at **100-500 Hz** (DOI 10.1190/1.1441700); our claimed floor was the literature's ceiling and 67 kHz has no support. At a 100 Hz resonance an 80 Hz tap sits only 1.25x below it: in-band, distorting amplitude **and phase**, so it hits TDoA too. Margin 1.3-6x, not 6-800x. `01`'s C4 deserves **partial reinstatement for free-laid nodes on fractured debris** - the regime drone deployment actually produces. Direction (lighter couples better) is right, and is Krohn's result, not ours. |

---

## 3. Two inter-critic conflicts, adjudicated

**(a) Coupling: `01` C4 ("luck, not design") vs `03` (computed, fine).**
**`03` wins; `01`'s C4 is struck.** `03` computes `k = 4Ga/(1-nu)`, `f0 = (1/2pi)*sqrt(k/m)` and puts
coupling resonance **two to four orders above the band**, so transmissibility -> 1. The margin is too
large for parameter error to close. `01` imported the "surface-laid sensors decouple" intuition from
10-100 Hz survey work, where it holds because survey geophones are heavy and the band sits near
resonance. Neither condition applies here.

Keep the corollary, which inverts the usual instinct: **`f0 ~ 1/sqrt(m)`, so a lighter sensor couples
better.** The mass overrun (item 13) is an endurance and impact problem, **not** a coupling problem.

**This makes the cardiac kill *more* certain, not less.** Good coupling means the 47-69 dB deficit is
a genuine source-amplitude shortfall with no coupling loss left to blame - or to fix.

**(b) Clock sync: "largely answered" vs 3,900-39,000x off.**
Both are right about different things, and the resolution reorders the roadmap. LongShoT's <2 us is
real and excellent. At 300 m/s it is **0.0006 m** - against a **3.5 m** node-position uncertainty.
Combining in quadrature, node position dominates **in every case**:

| Pick error | + node position 3.50 m | Total |
|---|---|---|
| 0.33 m | 3.50 m | **3.52 m** |
| 1.11 m | 3.50 m | **3.67 m** |
| 3.30 m | 3.50 m | **4.81 m** |

**Timing is a solved problem that was never the bottleneck.** The band correction is still mandatory
- it moves pick error from 8-27 m (useless) to sub-metre (negligible), buying the *right* to be
limited by node position. **Past that point, every further dollar spent on timing is wasted.** The
next dollar belongs to node position: RTK, acoustic self-survey, or surveyed anchors.

---

## 4. The rebuilt idea

**Drone-deployed seismic-acoustic mesh for locating responsive survivors by tap or voice.**

Not a heartbeat detector. The change is narrow - one sensor, one filter, one claim - and it converts
an impossible system into a buildable one that keeps the novelty intact.

### 4.1 The contribution, stated honestly

Delsar (the $15,000 incumbent) is **hand-placed, one point at a time, by an operator standing on
unstable rubble**, and yields a **single bearing**. This system is **drone-deployed, simultaneous,
multi-point, and automatically triangulated**, with time sync already solved.

**The $1,845 vs $15,000 comparison becomes honest, because it now compares like with like.** Under
the cardiac premise it compared a working product against a system that could not detect its target.
That is the real reason this pivot strengthens rather than weakens the project.

What is given up: the unconscious-victim claim - which section 2 shows was never deliverable. **The
pivot surrenders nothing that existed.**

### 4.2 Locked decisions

| Parameter | Value | Why |
|---|---|---|
| **Sensor** | **SM-24 geophone** (vendor-verify noise first) | 48 dB density advantage **is** the margin. Reverses 3.2 |
| **Band** | **5-40 Hz** (tap), 200 Hz-3 kHz (voice, S4) | Matches the signal, not the rate |
| **Target** | Tap / movement / voice | +32 to +56 dB over cardiac |
| **Cardiac** | **Stretch goal only**, contact-range confirmer (`01` S3) | Not load-bearing |
| **Localization spec** | **+/-3.5-5 m**, node-position-bound | Honest; supersedes 8.5 by 30-70x |
| **Timing** | LongShoT as-is, **no further investment** | Over-engineered 10^4 |
| **Impact** | Design to **~200 G** | 15 mm crush cannot give 15-20 G |
| **Cost model** | **Quadratic in 1/r**, stated explicitly | $1.5k -> $54k as r: 3 m -> 0.5 m |
| **Drop ICA, depth-from-amplitude, ECG-trained LSTM** | - | Invalid as specified (19-21) |
| **DSP** | Matched filter / impulse detector | Correct tool for a broadband impulse |

**Architecture: adopt `01`'s S4** (geophone + microphone + CO2/VOC, cardiac demoted) - "the most
project value for the least physics risk," and it matches real multi-modal USAR workflow. S1 is the
minimum viable subset if budget forces one channel.

### 4.3 The one unsolved problem - own it, don't bury it

**False alarms (items 5-6) are the binding risk, and the tapping pivot does not fix them.** A taught
tap pattern helps where a heartbeat could not - it is a *cooperative, structured* signal, so it
admits matched filtering and pattern gating that raw energy detection cannot achieve. That is a real
advantage of S1 over the original premise. But it must be **specified and measured**, not assumed:

- **Replace "93% accuracy" with a false-alarm-rate requirement.** Accuracy is the wrong metric for a
  rare-event detector. Target **<= 1 false pin per node-hour**, measured on **empty** rubble.
- **Measure common-mode rejection explicitly** with an excavator or generator running. Do not credit
  the 3-of-N vote until independence is tested - `02` shows it is the single most load-bearing
  unexamined assumption in the chain, and it is nowhere in MASTER.
- **Exploit the cooperative signal**: a prompted "tap 3 times on command" gives a known pattern,
  turning detection into template matching against a deterministic sequence. This is the strongest
  available false-alarm defence and it exists only because the victim is responsive.

### 4.4 Cheapest next steps, in order

From `01`, with my arithmetic attached. Note what comes first: **nothing here requires buying
anything.**

1. **Delete the 0.5-4 Hz filter.** Wrong regardless of path. Free.
2. **Re-run the 3.2 sensor trade against 5-40 Hz.** The geophone rejection is wrong and the
   correction is free. ~~**Vendor-verify the SM-24's 0.1 ug/rtHz**~~ **AMENDED 2026-10-08: there is
   nothing to vendor-verify.** The SM-24 brochure was re-extracted and contains **no noise
   specification at all** (regex `nois` over the full text: zero matches). 0.1 ug/rtHz was never a
   vendor figure. Computing the element's thermal floor from the brochure's own 375 ohm / 28.8 V/m/s
   gives **0.003-0.005 ug/rtHz across 60-80 Hz**, i.e. the assumed figure is **conservative by
   23-30x, not optimistic**. The +23/+41 dB tap margin therefore holds, and the knuckle-tap risk
   above is withdrawn. **The real number the architecture rests on is now the preamplifier**, since
   it, not the element, sets the system floor: at 4 nV/rtHz input noise the margin is still 12-16x;
   only at ~50 nV/rtHz does it vanish. Specify the preamp, don't re-chase the element.**
3. **Do NOT run MASTER 12 step 1 as written.** Its outcome is already determined; it would cost weeks
   to confirm what arithmetic gives today.
4. **Bench-test a TAPPING source at 1 / 3 / 10 m** on specified hardware. Measures real detection
   range and **validates the 60-80 Hz tap-spectrum assumption** - the estimate most worth checking,
   since it sets both the f-weighting gain and whether a 10 Hz-corner geophone is in-band.
5. **Run step 4 again with an excavator or generator active** - the false-alarm and common-mode test.
   Cheap, and it attacks the only unsolved problem.
6. **Decide S1 vs S4 before spending the deferrable $739 airframe** (MASTER 9 already flags it).

---

## 5. Honest statement of residual risk

What could still sink the rebuilt system, in order:

1. **False alarms (4.3).** Unsolved. Mitigable via cooperative patterns, but unproven. **The one that
   should worry you.**
2. **SM-24 noise figure.** MASTER's own number, not vendor-verified. 10x optimism makes knuckle taps
   marginal.
3. **Tap spectrum.** 60-80 Hz estimated, not measured. Both effects favour the tap, so error is
   likely small - but it is an assumption.
4. **Responsive-victim-only.** A genuine capability reduction. Honest, and it is what physics allows.
5. **Node position** caps localization at +/-3.5-5 m. Adequate for directing a dig; not the
   centimetre claim.

**What is NOT at risk:** the band correction, the coupling conclusion, the cardiac kill, the cost
scaling, and the regulatory finding. Those are arithmetic or verified documents.

---

## 6. The methodological lesson, recorded

Three prior passes certified wrong conclusions while being internally rigorous, because **they
audited the arithmetic they chose to do and never asked whether the right quantity was being
computed.** The projects's numbers reproduced - from a wrong ToA constant, a wrong band, and an
unmeasured source amplitude off by three orders of magnitude.

**Guard adopted going forward:** before verifying a number, state what physical quantity it is and
what it would have to be for the design to fail. `00b` was written before reading any critic's
output for exactly this reason - so agreement between my arithmetic and theirs is evidence rather
than an echo. It held: `03` independently reproduced 200 G, 15.5 g and ~4 m; `06` independently
reproduced the packet failure under a *stricter* assumption (156 B vs my 82 B).

---

## 7. One-paragraph answer

The heartbeat premise is unrecoverable - 47 to 69 dB short, and the unmeasured assumption it rested
on was already wrong by three orders of magnitude. But the error that killed it was a single
conceptual slip (a repetition rate mistaken for a signal bandwidth), and correcting that slip hands
back a better project than the one being defended: swap the ADXL355 for the SM-24 geophone that the
same error caused to be rejected, retarget from heartbeat to tap or voice, and the identical drone,
mesh, TDoA solver and sync stack clear their noise floor by 23 to 41 dB instead of failing by 47 to
69. The novelty survives completely - no one else drone-deploys a self-triangulating seismic mesh -
and the cost argument becomes honest for the first time, because it finally compares against the
incumbent on the same task. **One unsolved problem remains, and it is not physics: false alarms, at
roughly 16% positive predictive value and a concurrence vote that assumes an independence real
rubble does not provide. That is where the next effort belongs - not on another sensor spec, and not
on the timing problem, which was solved four orders of magnitude past where it mattered.**

---

## 8. Status of pending inputs

`04-cost-kill-attempt.md` and `05-operational-kill-attempt.md` were still running when this was
written. They attack **economics and deployment of an architecture these findings already
determine** - they can refine section 4's numbers (BOM under the geophone swap, 1/r^2 fleet cost,
INSARAG fit, operator workflow) but cannot reverse section 1, which rests on sensor noise floors,
source amplitudes and the CRLB. **If either contradicts a locked decision in 4.2, this document gets
amended rather than defended** - the same standard applied to `01`'s C4 in section 3.

---

## 9. Prior-art amendment, 2026-10-08

Three agents swept the literature after this verdict was written (`prior-art/A`, `B`, `C`).
What changes:

**The kill stands and gets stronger evidence.** The 1-4 N cardiac source force is no longer an
assumption - it is **measured** three times over 70 years with three instruments: 3.7 N (Starr
1939, n=7), 4.06 N +-1.53 (Inan 2009, Stanford, n=26+), 2 N_pp (Ashouri 2016, Kistler force
plate). Worst single healthy subject 10.95 N = **+8.75 dB**, so the deficit becomes **38-60 dB**
instead of 47-69. Unchanged in kind: nothing recovers 38 dB. And the feared "what if it's
20-40 N" escape is now **closed by measurement**, not argument. Pathological hearts measure
**0.94-1.05 N**, ~12 dB *below* the healthy mean - a crush-injured hypothermic survivor is
plausibly weaker than this verdict assumed, not stronger.

**Two numbers in this document are wrong** - see the amended register row above (coupling
100-500 Hz) and `00b`'s amendment header (anchor 17 Hz -> 32.7 ug, not 19 Hz -> 36.5 ug;
Ekimov & Sabatier, *JASA* 120(2):762).

**"Force-ratio scaling" must be renamed.** The method is sound but the name is not standard.
It is **linear transfer-mobility scaling** (FTA ground-borne vibration method; ASTM/FHWA
impulse-response mobility spectrum). Elastodynamics is LTI, so amplitude is linear in source
force - this is why the method works. Two errors to keep avoiding: scaling by *energy* instead
of force (a factor-2 dB error) and invoking *seismic moment* (defined for internal sources, not
a body pressing on a surface).

**The novelty claim has moved, and this is the biggest change for the proposal.** The
tapping retarget is **not novel** - it is FEMA doctrine, verbatim: listening devices require
that the "victim must create a recognizable sound pattern," and the "audible call out/knocking
method" is named doctrine. Delsar LD3, Leader SEARCH and the NDRF Type-I spec are all
6-8-sensor operator-interpreted systems. Nor is drone deployment of seismic sensors novel
(Stewart et al., SEG 2016, drone-landed geophones; SeismicDart, air-dropped darts, rho =
0.81-0.98 against planted geophones). Nor is a seismic array on rubble (Arosio et al. 2010).
Nor is "node position dominates TDoA" - that is **textbook GDOP** and must be written as an
error-budget conclusion, never as a finding.

**What survives as defensible, strongest first:**

1. **Array extent.** Arosio et al. 2010 names its own three limitations as debris
   inhomogeneity, real-time response, and **"the limited spatial extension of the sensor
   array"** - verified in two independent sources. Hand placement is what bounds array extent;
   air deployment lifts it. Prior art states the constraint, the proposal's mechanism removes
   it. A capability argument, which outranks the cost argument.
2. **Rubble, not soil.** Every air-deployment result is parameterised by *soil* compression
   strength. **No characterisation of air-dropped node coupling onto collapsed debris was
   located.** Genuine measurement gap, natural deliverable - and it is the same gap as the
   reinstated C4 coupling worry above, which makes it doubly worth measuring.
3. **The cardiac bound itself.** Nobody has published the negative result this critique
   derived. It is publishable as a bound.
4. **Node count / cost at mesh scale**, and **NDRF context** - the Type-I spec contains no
   automated-localization requirement, a documented capability gap in the procuring agency's
   own words.

**Must be conceded in writing, or a reviewer will catch it:** tapping is doctrine's existing
target; INACHUS (FP7 607522) stated the automated-knock-localization goal; air-dropped
geophones exist. Equally, do **not** assert INACHUS *achieved* validated metre accuracy - no
peer-reviewed result was located either way.

**Two citations that must appear and currently do not:** Arosio et al. 2010, *Near Surface
Geophysics* 8(6):623-633, DOI 10.3997/1873-0604.2010051 (the closest prior art; accuracy
"within the limit of the seismic resolution", 3x faster than incumbent systems); and Sabatier &
Ekimov 2008, Proc. SPIE 6963, 69630V, DOI 10.1117/12.785235, which is **already a
signal-equals-noise range bound for footsteps** - this document's method has a direct published
ancestor. Also HeartQuake (Park et al. 2020, DOI 10.1145/3411843), which recovers full ECG
morphology through a mattress **from an SM-24 geophone element** - the same part this verdict
selects. It must be cited and distinguished (contact-coupled through bedding, not metres of
rubble), because a reviewer who finds it unaided will read it as contradicting the kill.

**Still unmeasured, and now the highest-value bench work:** tap force and tap spectrum. The
50-300 N / 60-80 Hz figures this verdict uses have **no source** - the nearest literature
anchors are destructive (karate-chop, ~1,900-2,800 N) and were explicitly declined rather than
laundered as measured. Everything in section 2's margin table scales off them.
