# 00b - Independent verification of the kill arithmetic

**Author:** primary agent (not a subagent). **Date:** 2026-10-07.
**Status:** computed from first principles, cross-checked against critics 01/02/03/06 after the fact.
**Purpose:** `00-my-own-arithmetic.md` checked the project's *stated* numbers. This document checks the
*critics' kill claims*, so the synthesis rests on arithmetic I ran, not on agreement between agents.

All figures from `scratchpad/verify.py` and `scratchpad/salvage.py` under `py -3.12`.

---

## A. The signal-level deficit is 48-69 dB, not ~20 dB

The only defensible anchor in the literature chain is a **measured footstep**: ~3 um/s particle
velocity at 19 Hz, 3 m range. Converting to acceleration (a = 2*pi*f*v):

```
a = 2*pi * 19 * 3e-6 = 3.581e-4 m/s2 = 0.0365 mg = 36.5 ug
```

Scaling to cardiac by force ratio - ground-reaction force ~700 N for a footstep, **1-4 N** for the
ballistocardiographic impulse transmitted into a substrate:

| Source | Force | Scaled amplitude @ 3 m |
|---|---|---|
| Footstep (anchor) | 700 N | 36.5 ug |
| Cardiac, optimistic | 4 N | **0.209 ug** |
| Cardiac, realistic | 1 N | **0.052 ug** |

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
| **5-40 Hz (corrected)** | **2.71 m** | **0.86 m** |
| 5-95 Hz (wide) | 1.05 m | 0.33 m |

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
f0 = (1/2pi)*sqrt(k/m), putting coupling resonance at **500 Hz - 67 kHz**, two to four orders above
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
- **The SM-24's 0.1 ug/rtHz is MASTER's own figure, not vendor-verified this session.** If it is
  optimistic by 10x, the tap cases drop to +3 to +21 dB - marginal for a knuckle, still fine for a
  rock strike. **This single number should be vendor-verified before committing to S1.**
- **Tap frequency content (60-80 Hz) is estimated, not measured.** It sets both the f-weighting gain
  and whether a 10 Hz-corner geophone is in-band. Both favour the tap, so this is the assumption most
  worth a bench check.
