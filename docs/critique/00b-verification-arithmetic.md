# 00b - Independent verification of the kill arithmetic

**Author:** primary agent (not a subagent). **Date:** 2026-10-07.
**Status:** computed from first principles, cross-checked against critics 01/02/03/06 after the fact.
**Purpose:** `00-my-own-arithmetic.md` checked the project's *stated* numbers. This document checks the
*critics' kill claims*, so the synthesis rests on arithmetic I ran, not on agreement between agents.

All figures from `scratchpad/verify.py` and `scratchpad/salvage.py` under `py -3.12`.

---

> ## AMENDED 2026-10-08 by the prior-art sweep (`prior-art/`)
>
> Three numbers below are superseded by measured literature. **The original figures are left in
> place** because this document's value is that it was computed before the critics reported; the
> corrections are stated here rather than silently patched in.
>
> | Below | Corrected | Source | Effect |
> |---|---|---|---|
> | anchor **19 Hz** -> 36.5 ug | **40 Hz** -> **76.9 ug** | Ekimov & Sabatier, *JASA* 120(2):762 (2006), **full text retrieved 2026-10-08**: *"The maximum vibration response for the footstep in the low-frequency range (below 500 Hz) was near 40 Hz for the regular walking style"* | **+6.5 dB.** Anti-conservative direction, but does not rescue the premise. **Supersedes the 17 Hz figure**, which was a mis-citation. |
> | coupling resonance **500 Hz - 67 kHz** | **100-500 Hz** | Krohn (1984), *Geophysics* 49(6):722, DOI 10.1190/1.1441700 | **Our floor was the literature's ceiling.** See below. |
> | SM-24 **0.1 ug/rtHz** "MASTER's own figure" | not a vendor figure at all - **the datasheet has no noise spec** | SM-24 brochure re-extracted, regex `nois` = 0 matches | Element thermal floor computed at **0.003-0.005 ug/rtHz** - our figure is **conservative by 23-30x, not optimistic**. |
>
> **Section G's load-bearing worry is resolved in the project's favour.** The 1-4 N cardiac force is
> **measured**: 3.7 N (Starr 1939), 4.06 N (Inan 2009, n=26+), 2 N_pp (Ashouri 2016). Worst single
> healthy subject 10.95 N = **+8.75 dB**, moving the deficit from 47-69 dB to **38-60 dB**. Unchanged
> in kind. Pathological hearts measure **0.94-1.05 N**, ~12 dB *below* healthy mean - a crush-injured
> hypothermic survivor is plausibly *weaker* than assumed.
>
> **Section E needs partial walk-back.** C4 was struck on the strength of the 500 Hz-67 kHz window.
> With measured resonances at 100-500 Hz, a 100 Hz coupling resonance is only **1.25x** above an
> 80 Hz tap - in-band, distorting amplitude *and phase*, which hits TDoA as well as detection. The
> direction of E's argument (lighter couples better, f0 proportional to 1/sqrt(m)) is **established**
> - Krohn (1984) - but it is not a project finding and the margin is 1.3-6x, not 6-800x. **C4
> deserves partial reinstatement for free-laid nodes on fractured debris**, which is the worst-coupling
> regime and the one drone deployment actually produces.
>
> Also: the anchor **3 um/s at 3 m is now citable** - Sabatier & Ekimov, Proc. SPIE 6963, 69630V
> (2008), DOI 10.1117/12.785235, verbatim "did not exceed 3 x 10^-6 m/s, even very close (3 metres)".
> That paper is also a **signal-equals-noise range bound for footsteps**, i.e. this document's method
> has a direct published ancestor that must be cited.

---

---

## A. The signal-level deficit is 47-69 dB, not ~20 dB

The only defensible anchor in the literature chain is a **measured footstep**: ~3 um/s particle
velocity at 19 Hz, 3 m range. Converting to acceleration (a = 2*pi*f*v):

```
a = 2*pi * 19 * 3e-6 = 3.581e-4 m/s2 = 0.0365 mg = 36.5 ug
   [AMENDED 2026-10-08, full text: measured peak is 40 Hz, not 17 or 19
    -> 2*pi*40*3e-6 = 7.540e-4 m/s2 = 76.9 ug. The site transfer function
    peaks over 20-90 Hz; the 1-4 Hz figure in the literature is the FORCE of
    MULTIPLE footsteps, not the per-footstep vibration response.]
```

Scaling to cardiac by force ratio - ground-reaction force ~700 N for a footstep, **1-4 N** for the
ballistocardiographic impulse transmitted into a substrate:

| Source | Force | Scaled amplitude @ 3 m | ~~AMENDED (17 Hz)~~ | **AMENDED (40 Hz, full text)** |
|---|---|---|---|---|
| Footstep (anchor) | 700 N | 36.5 ug | ~~32.7 ug~~ | **76.9 ug** |
| Cardiac, optimistic | 4 N | **0.209 ug** | ~~0.187 ug~~ | **0.439 ug** |
| Cardiac, realistic | 1 N | **0.052 ug** | ~~0.047 ug~~ | **0.110 ug** |
| Cardiac, worst healthy subject (measured) | **10.95 N** | - | ~~0.511 ug~~ | **1.202 ug** |

*The whole column scales linearly off the anchor, so the 40 Hz correction moves every row by the
same **+6.47 dB** (relative to 19 Hz) or **+7.43 dB** (relative to the withdrawn 17 Hz figure).
**This is the one correction so far that moves against the kill, and it is not enough:** the
deficit goes from 38-60 dB to roughly **31-53 dB**, so the heartbeat premise stays dead by a wide
margin. It does, however, *improve* every tap/voice margin by the same 6.5 dB.

> ### Anchor correction 2026-10-08 — effect on the headline numbers
>
> The **+6.47 dB** anchor correction (19 Hz → 40 Hz, full text) raises **every amplitude in the
> chain by the same factor**, because the scaling is linear. Consequences:
>
> | Claim as written elsewhere | After the correction | Changes the conclusion? |
> |---|---|---|
> | Cardiac deficit **38–60 dB** | **~31–53 dB** | **No.** Nothing recovers 31 dB. |
> | Tap margin **+23 to +41 dB** (SM-24) | **~+29 to +47 dB** | **No** — improves it. |
> | Tap on ADXL355 **−7 to −25 dB** | **~−1 to −19 dB** | **No** — still buried. |
>
> **The repo has deliberately NOT been bulk-edited to these new figures**, for one reason: the tap
> margins scale off **tap force and tap spectrum, which are still [ASSERTED] with no source**
> (50–300 N / 60–80 Hz). Re-deriving a margin from a corrected anchor and an unmeasured force would
> manufacture false precision. **The anchor correction is settled; the margins stay as they are
> until the bench measurement lands**, at which point every margin gets recomputed once, from
> measured inputs, in a single pass.
>
> Direction is what matters for the proposal: the correction is **favourable and the kill is
> unaffected.** Do not quote the 31–53 dB or +29/+47 dB figures as measured — they are this note's
> arithmetic on an unmeasured force.
 The added row is Inan (2009)'s maximum single healthy subject - the most
favourable case the measured literature permits, included so the bound cannot be accused of
using a convenient average. Method: linear transfer-mobility scaling (see `07` section 9 on the
naming). Against the ADXL355 at B = 35 Hz the cardiac SNR is **-70.0 / -58.0 / -49.2 dB** at
1 / 4 / 10.95 N respectively.*

Against the ADXL355's own noise floor (25 ug/rtHz):

| Band | Sensor noise (rms) | SNR @ 0.209 ug | SNR @ 0.052 ug |
|---|---|---|---|
| 0.5-4 Hz (B=3.5) | 46.8 ug | **-47.0 dB** | **-58.9 dB** |
| 5-40 Hz (B=35) | 147.9 ug | **-57.0 dB** | **-68.9 dB** |

This is *before* any propagation loss beyond 3 m, before rubble scattering, before ambient.

### A.1 This retroactively determines section 3.3's open measurement

MASTER 3.3 assumes **0.1-1 mg at 2-3 m** and flags it as unmeasured. The calibration chain gives
0.00005-0.0002 mg.

```
claimed 0.1 mg / computed 0.209 ug  =   479x
claimed 1.0 mg / computed 0.052 ug  = 19167x
```

**The premise is wrong by 2.7 to 4.3 orders of magnitude.** The "one unmade ~$2 measurement" was
never going to return favourably; arithmetic settles it today. This agrees with critic 01's
independent route (PREMISE DEAD) and vindicates 01's instruction: **do not run section 12 step 1 as
specified.**

## B. Coherent averaging cannot close it

Coherent gain is sqrt(N), so closing a deficit of D dB needs N = 10^(D/10) beats:

| Deficit | Beats required | Continuous integration time |
|---|---|---|
| 20 dB | 100 | 1.7 min |
| 40 dB | 10,000 | **2.8 h** |
| 60 dB | 1,000,000 | **278 h (11.6 days)** |
| 80 dB | 100,000,000 | **27,778 h (3.2 years)** |

The real deficit (47-69 dB) sits in the 2.8 h -> 278 h range **and requires phase coherence across
the whole interval** - which HRV destroys by construction (finding 6 of `00`). The two requirements
are mutually exclusive, so even the unphysical integration time is unavailable.

**Net: no amount of DSP recovers this.** 02's FATAL findings are correct in kind and, if anything,
understated in degree.

---

## C. The decisive result: the SM-24 reversal is load-bearing

MASTER 3.2 marks the ADXL355 choice **FIXED** and rejects the SM-24 geophone because its 10 Hz
corner sits "above the entire target band." That rejection is **downstream of the section 6 band
error** - it is only true for the wrong band.

Noise-density ratio:

```
ADXL355 25 ug/rtHz  /  SM-24 0.1 ug/rtHz  =  250x  =  +48.0 dB
```

Applied to the tapping source of salvage S1 (calibrated off the same footstep anchor, including the
a = 2*pi*f*v weighting that favours the higher-frequency tap):

| Tap source | Force | Freq | Amplitude @ 3 m | ADXL355 | SM-24 |
|---|---|---|---|---|---|
| Knuckle on slab | 50 N | 60 Hz | 8.23 ug | -25.1 dB **BURIED** | **+22.9 dB DETECT** |
| Rock/rebar on slab | 150 N | 80 Hz | 32.9 ug | -13.0 dB **BURIED** | **+34.9 dB DETECT** |
| Hard tool strike | 300 N | 80 Hz | 65.9 ug | -7.0 dB **BURIED** | **+40.9 dB DETECT** |

**Every tap case fails on the ADXL355 and succeeds on the SM-24.** The 48 dB density advantage *is*
the entire detection margin.

So the SM-24 decision is not a line-item optimisation to "revisit" - **reversing section 3.2 is a
precondition for the only surviving architecture.** This is a stronger claim than 01 made.

### C.1 Why tapping works where cardiac cannot

```
tap  8.23 ug / cardiac 0.209 ug =   39x = +31.9 dB
tap  8.23 ug / cardiac 0.052 ug =  158x = +44.0 dB
tap 32.93 ug / cardiac 0.209 ug =  158x = +44.0 dB
tap 32.93 ug / cardiac 0.052 ug =  631x = +56.0 dB
```

**+32 to +56 dB** - which is precisely the deficit identified in section A. The salvage is not a
consolation prize; it is the same system pointed at a source that is physically present.

---

## D. Localization: the binding constraint moves to node position

With sigma_t ~ 1/(B*sqrt(SNR)) and 300 m/s:

| Band | SNR 10 dB | SNR 20 dB |
|---|---|---|
| 0.5-4 Hz (as written) | 27.11 m | 8.57 m |
| **5-40 Hz** ~~(corrected)~~ **[WITHDRAWN - ADR 0001]** | **2.71 m** | **0.86 m** |
| 5-95 Hz (wide) | 1.05 m | 0.33 m |

> **[ADR 0001, 2026-10-11]** The 5-40 Hz row is retained for its arithmetic only. That band was
> **seismocardiography**-derived (`01-physics-kill-attempt.md:290`) and was never derived from a tap;
> it is withdrawn as the project's band. Acquisition is **5-200 Hz** and the detection band is an
> **output of the M1/M2 bench measurement**. **The conclusion of this section is unaffected and in
> fact strengthens:** at any band wider than ~25 Hz the pick error is sub-metre, so **node position
> dominates the error budget** - which is the finding that sets the +/-3.5-5 m localization spec. The
> `5-95 Hz (wide)` row is the closer analogue to the decided acquisition band.

Combined in quadrature with honest node-position uncertainty (+/-3.5 m mid-range, from drone GPS CEP
plus post-impact bounce - finding 3 of `00`):

| Pick error | + node position 3.50 m | Total | Dominant term |
|---|---|---|---|
| 0.33 m | 3.50 m | **3.52 m** | node position |
| 1.11 m | 3.50 m | **3.67 m** | node position |
| 3.30 m | 3.50 m | **4.81 m** | node position |

**Node position dominates in every case.** Two consequences:

1. The band correction is still mandatory - it moves pick error from 8-27 m (useless) to sub-metre
   (negligible). It buys the *right* to be limited by node position.
2. **Past that point, every further dollar spent on timing is wasted.** Clock sync at 2 us
   (= 0.0006 m) is over-engineered by ~10^4. The honest spec is **+/-3.5-5 m**, and the only way to
   improve it is better node position (RTK, acoustic self-survey, or surveyed anchors) - not better
   timing.

This supersedes MASTER 8.5's +/-0.05-0.1 m claim by ~30-70x.

---

## E. Resolving the 01-vs-03 coupling conflict

01's condition C4 calls favourable coupling "luck, not design." 03 computes k = 4Ga/(1-nu) and
f0 = (1/2pi)*sqrt(k/m), putting coupling resonance at **500 Hz - 67 kHz** [**AMENDED: CONTRADICTED. Krohn (1984) measures
100-500 Hz; 67 kHz has no support and must not be quoted**], two to four orders above
the band, so transmissibility -> 1.

**03 is right and 01's C4 should be struck.** The resonance calculation is explicit, uses standard
rigid-disc-on-elastic-half-space theory, and the margin is so large that no plausible parameter
error closes it. 01 was importing the "surface-laid sensors decouple" intuition from 10-100 Hz
survey work, where it is true because survey geophones are heavy and the band is near resonance.

Corollary worth keeping, because it inverts the usual instinct: **f0 proportional to 1/sqrt(m) means
a lighter sensor couples better.** The mass budget overrun (15.52 g vs 8 g claimed, finding 2 of
`00`) is a drone-endurance and impact problem - **not** a coupling problem.

Note this does *not* rescue cardiac detection: coupling being fine means the 47-69 dB deficit is
a genuine source-amplitude deficit, with no coupling loss left to blame or fix. **Good coupling
makes the kill more certain, not less.**

---

## F. What this adds to the register

| # | Finding | Severity | Cross-check |
|---|---|---|---|
| V1 | Cardiac deficit is 47-69 dB, not ~20 | FATAL to cardiac | 01, 02 independently |
| V2 | Section 3.3's 0.1-1 mg premise wrong by 479-19167x | FATAL; closes the open measurement | 01 |
| V3 | Averaging needs 2.8 h-3.2 yr **and** phase coherence HRV forbids | FATAL | 02, `00` #6 |
| V4 | **SM-24 reversal is load-bearing, not optional** | ENABLING | extends 01 |
| V5 | Corrected band moves pick error 8-27 m -> 0.86-2.71 m | ENABLING | `00` #4 |
| V6 | Node position dominates all timing terms; honest spec +/-3.5-5 m | HIGH | `00` #3 |
| V7 | 01's C4 struck; coupling is fine; light sensor couples better | CORRECTION | 03 |

**Through-line:** the project's arithmetic was never wrong where it was checked. Every fatal result
here comes from a quantity nobody computed - source amplitude from a measured anchor, the deficit in
dB, and which error term actually dominates localization.

---

## G. What I could be wrong about

- **The 700 N / 1-4 N force ratio is the load-bearing assumption.** If the cardiac impulse couples
  into a substrate at 20-40 N rather than 1-4 N, the deficit shrinks by 14-20 dB. It would still be
  fatal (-27 to -49 dB), so the conclusion is robust, but the exact figure is not.
- **Linear force scaling of a near-field seismic source is approximate.** Source-coupling efficiency
  depends on contact area and substrate impedance, which differ between a shoe and a torso. The
  direction of that error is unknown; the magnitude is plausibly a few dB, not tens.
- **The SM-24's 0.1 ug/rtHz is MASTER's own figure, not vendor-verified this session.**
  [**AMENDED: the datasheet carries NO noise spec at all. Computed element floor is
  0.003-0.005 ug/rtHz, so 0.1 is conservative by 23-30x. Relabel as a system-level
  (element+preamp) assumption, never as a vendor figure.**] If it is
  optimistic by 10x, the tap cases drop to +3 to +21 dB - marginal for a knuckle, still fine for a
  rock strike. **This single number should be vendor-verified before committing to S1.**
- **Tap frequency content (60-80 Hz) is estimated, not measured.** It sets both the f-weighting gain
  and whether a 10 Hz-corner geophone is in-band. Both favour the tap, so this is the assumption most
  worth a bench check.
