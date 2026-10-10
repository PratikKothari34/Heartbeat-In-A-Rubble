# 01 — Physics Kill Attempt

**Role:** hostile peer review. Mandate: kill the core physics premise if it is killable.
**Date:** 2026-10-06 · **Target:** `docs/MASTER.md` §3, §6, §7, §10.1, §10.5, §11 and
`docs/reference/Heartbeat_In_The_Rubble.md` (whole).
**Evidence convention:** **[M]** measured by someone · **[C]** computed here from stated inputs ·
**[A]** asserted without support.

---

## VERDICT: PREMISE DEAD

**Cardiac detection through 2–3 m of rubble with a $15 MEMS accelerometer is not a pending
measurement. It is excluded by arithmetic that can be done today, and the project has been
sequencing its entire build order behind a bench test (§12 step 1) whose outcome is already
determined.**

The claimed signal of 0.1–1 mg at 2–3 m is **too high by a factor of ~14× at the most generous
end and ~19,000× at the realistic end**, by two fully independent derivations that agree with
each other. Below is the summary; the arithmetic is in §2.

| Route | Independent? | Predicted accel at 3 m | vs claimed 0.1 mg | vs claimed 1 mg |
|---|---|---|---|---|
| Energy budget, 10 % of body recoil radiated (absurdly generous) | yes | 7.3e-3 mg | **14× too high** | 137× |
| Energy budget, 1 % radiated | yes | 2.3e-3 mg | 43× | 435× |
| Footstep calibration, 4 N cardiac force | yes | 2.1e-4 mg | 470× | 4,699× |
| Footstep calibration, 1 N cardiac force | yes | 5.3e-5 mg | **1,880×** | 18,797× |

Three further findings are each independently fatal or near-fatal:

1. **The 0.5–4 Hz bandpass (§6 stage 1) is in the wrong place.** It filters out the heartbeat.
   This is a textbook rate-vs-bandwidth confusion, and it is the single clearest technical
   error in the spec (§3 below).
2. **The system is sensor-limited before it is ever ambient-limited.** §10.1's framing — "is it
   ambient-limited?" — is the wrong question. Even in a perfectly silent vacuum chamber the
   ADXL355's own Johnson noise swamps the signal (§2.4).
3. **Nobody has ever done this.** Every incumbent the project benchmarks against solves a
   different and much easier problem (§4).

**This verdict does not require the ambient-noise measurement in §10.1.** Ambient noise makes a
dead premise deader. The premise dies on the sensor floor alone.

---

## 1. The strongest single argument

**A footstep is barely detectable at 3 m. A heartbeat is ~1,000× weaker than a footstep. The
project proposes to detect the heartbeat at the same range, through worse coupling, with a
sensor 100× noisier than the geophone that struggles with the footstep.**

The chain, with each link sourced:

**[M]** Measured peak seismic ground velocity from a human footstep does not exceed
**3 × 10⁻⁶ m/s even at 3 m from the walker**, with dominant ground response **near 19 Hz**
(Succi et al., footstep characterization; corroborated in the footstep-ID literature, S8/S9).

**[C]** Convert to acceleration: `a = 2πf·v = 2π × 19 × 3e-6 = 3.58e-4 m/s² = 0.037 mg = 37 µg`.

That is the **whole body weight** — a ~700–1000 N impulse — delivered through a rigid shoe in
direct normal contact with the ground. It produces **37 µg at 3 m**.

**[C]** Now the force ratio. Cardiac body recoil is a **1–4 N** peak force (BCG literature, S10;
the whole-body recoil velocity is ~1 mm/s, §2.2 below). Against a ~700 N footstep that is a ratio
of **1.4e-3 to 5.8e-3**. Linear scaling of the same propagation path gives:

```
4 N cardiac:  37 µg × 5.8e-3  = 0.21 µg at 3 m
1 N cardiac:  37 µg × 1.4e-3  = 0.053 µg at 3 m
```

**[C]** The ADXL355's in-band RMS noise floor over the spec's own 0.5–4 Hz band is
`25 µg/√Hz × √3.5 Hz = 46.8 µg`.

**The predicted signal is 0.05–0.2 µg. The sensor's own noise is 46.8 µg. That is a deficit of
47 to 59 dB — a factor of 220 to 880 in amplitude — before a single disaster-site noise source
is switched on.**

And this is the *generous* framing: it credits the heartbeat with the footstep's coupling
efficiency. In reality a footstep is a rigid-to-rigid normal impulse, while a heartbeat must
cross soft tissue → skin → a loose, air-gapped contact with debris (§2.5). A single tissue-air
interface costs **−29.6 dB** on its own **[C]**.

### The averaging escape route is closed

The obvious rebuttal is coherent averaging over many beats. It does not survive contact with the
numbers **[C]**:

| Estimate | Deficit | Beats needed for +10 dB | Observation time @ 72 bpm |
|---|---|---|---|
| Energy budget, 10 % radiated | 16.2 dB | 4.1e2 | **5.7 minutes** |
| Energy budget, 1 % radiated | 26.2 dB | 4.1e3 | **57 minutes** |
| Footstep scaling, 4 N | 46.8 dB | 4.8e5 | **112 hours** |
| Footstep scaling, 1 N | 58.9 dB | 7.7e6 | **1,790 hours** |

The two lower rows exceed the 72-hour survival window the project is built around — by 1.5× and
25× respectively. And the whole table assumes **perfect phase coherence** across the entire
averaging interval. §6 of MASTER simultaneously claims **±5–10 % beat-to-beat HRV** as the
project's primary human-vs-machine discriminator. **These two claims are mutually destructive:
the HRV that identifies the target as human is exactly what destroys the phase coherence needed
to dig it out of the noise.** You cannot have both. The spec currently assumes both.

---

## 2. Attack 1 — the 0.1–1 mg at 2–3 m assumption (§3.3)

### 2.1 Where the number came from

**[A]** It is inherited verbatim from the reference doc's "KEY PHYSICS" box: *"A heartbeat at
1–2 Hz creates a ground vibration of 0.1–1 mg acceleration at 2–3 m distance through solid
concrete."* No citation, no derivation, no measurement. MASTER §3.3 honestly flags it PENDING and
calls it "the load-bearing number of the whole project." It is load-bearing and it is wrong.

### 2.2 First-principles energy budget **[C]**

**Step 1 — mechanical work per beat.** `W = P × SV = (100 mmHg × 133.322 Pa/mmHg) × 70 mL
= 13,332 Pa × 7.0e-5 m³ = 0.93 J`. The brief's ~1 J/beat is **correct**. That is the only part of
the premise that survives.

**Step 2 — how much of that 1 J can possibly leave the body as an elastic wave?** Almost none.
Stroke work goes into blood kinetic energy, aortic wall elastic storage, and viscous dissipation
in tissue. The *upper bound* on what can couple out is whole-body recoil, which is bounded by
momentum conservation:

```
blood momentum   p = m·v = 0.07 kg × 1.0 m/s = 0.07 kg·m/s
body recoil vel  v = p/M = 0.07/70         = 1.0e-3 m/s   (1 mm/s)
body recoil KE   E = ½Mv² = ½ × 70 × (1e-3)² = 3.5e-5 J
```

**This is 0.0038 % of the 1 J stroke work.** The brief's framing — "almost all of it into blood,
not into the ground" — is right, and understates it: the bulk-recoil channel is ~4 parts in
100,000, and only a fraction of *that* radiates.

**Step 3 — radiate it into rubble.** Hemispherical spreading, pulse duration τ = 100 ms, rubble
ρ = 1600 kg/m³, v = 300 m/s (mid-range of MASTER §10.5's own defensible 150–1000 m/s bracket).
Intensity `I = E/(2πr²τ)`, particle velocity `u = √(I/ρv)`, acceleration `a = 2πf·u` at 10 Hz:

| Radiated fraction of recoil KE | r = 1 m | r = 2 m | r = 3 m |
|---|---|---|---|
| 10 % (absurdly generous) | 21.8 µg | 10.9 µg | **7.3 µg** |
| 1 % (still generous) | 6.9 µg | 3.5 µg | **2.3 µg** |

**Against a claim of 100–1000 µg. Short by 14× to 435×.**

### 2.3 Where the brief's attack premise is WRONG — intrinsic Q is not the killer

The brief instructed me to attack via low Q in granular media. **I ran it and it does not work,
and I will not manufacture a result to agree with my own brief.**

**[C]** `α = πf/(Qv)` [Np/m]. Even at the hostile end — f = 10 Hz, v = 300 m/s, **Q = 3** (the
lowest measured value in the literature, S7) — `α = π×10/(3×300) = 0.0349 Np/m`, giving a skin
depth `1/α = 28.6 m`. Over the 3 m path the intrinsic absorption factor is `exp(-0.0349×3)
= 0.90` — **a loss of 0.9 dB. Negligible.**

Intrinsic attenuation is irrelevant at these distances and frequencies because the wavelength
(λ = v/f = 30 m at 10 Hz and 300 m/s) is **ten times the propagation path**. At 3 m the sensor is
in the near field. The real losses are:

1. **Geometric spreading** — 1/r for body waves. From r₀ = 0.1 m to r = 3 m is a factor of 30,
   **−29.5 dB**.
2. **Coupling** — §2.5 below. Dominant.
3. **Scattering at air gaps** — not an exponential-Q effect at λ >> gap size, but a severe
   mode-conversion and path-randomization effect that destroys the coherent arrival TDoA needs.

**Correction to the brief: the "low Q kills it" argument is false. The premise dies on source
strength and coupling, not on absorption.** This matters practically — it means thinner rubble
does not rescue the project.

### 2.4 The sensor-limited finding — §10.1 is asking the wrong question **[C]**

MASTER §10.1 and the brief both frame the open question as "is the system ambient-limited?" The
arithmetic says that question never arises.

```
ADXL355 floor, 0.5–4 Hz:   25 µg/√Hz × √3.5 Hz = 46.8 µg RMS
Claimed signal, low end:                          100 µg
SNR  =  20·log10(100/46.8)  =  +6.6 dB
```

**MASTER §3.3 and the reference doc's "RECOMMENDATION" box both assert ">20 dB SNR after
filtering" at 0.1 mg. [C] That is arithmetically false on their own numbers.** To reach 20 dB
against this sensor in this band you need `10 × 46.8 µg = 468 µg = 0.47 mg` — **4.7× more than
the low end of the project's own claimed signal range.** The spec's own two numbers contradict
each other, and nobody has checked.

Compare the ambient contribution **[C]**, using Peterson (1993) NLNM coefficients (S5, S6),
`dB = A + B·log₁₀(T)`, PSD in dB rel. 1 (m/s²)²/Hz:

| Freq | NLNM dB | ASD (µg/√Hz) |
|---|---|---|
| 0.5 Hz | −152.80 | 0.0023 |
| 1.0 Hz | −166.40 | 0.0005 |
| 2.0 Hz | −167.50 | 0.0004 |
| 4.0 Hz | −166.70 | 0.0005 |

**The quietest sites on Earth sit at ~0.0005 µg/√Hz. The ADXL355 sits at 25 µg/√Hz — 50,000×
noisier, i.e. +94 dB.** Even Hamburg-class urban cultural noise, measured at **20–40 dB above
baseline across 0.5–30 Hz** (S4, S11), does not close a 94 dB gap.

**Conclusion, and it is the opposite of what the project assumes: this system is
sensor-limited by an enormous margin, everywhere, including on a busy disaster site.** The
practical implication is that **the §10.1 bench test as specified cannot produce the answer the
project wants even if it is run perfectly in a quiet lab.** That result is already known.

A secondary point the spec misses entirely: **25 µg/√Hz is the flat-band figure and is not valid
at 1 Hz. [C]** MEMS accelerometers have 1/f noise below a corner typically in the 1–10 Hz region.
If the corner sits at 5 Hz, the real floor is **56 µg/√Hz at 1 Hz and 125 µg/√Hz at 0.2 Hz** —
2.2× to 5× worse than the number used. **Every SNR figure in MASTER is optimistic for this reason
alone**, and it hurts the respiration band (§5) worst.

### 2.5 Coupling — the loss the spec never accounts for **[C]**

Transmission at a normal-incidence interface: `T = 4Z₁Z₂/(Z₁+Z₂)²`.

- Soft tissue (Z ≈ 1.5e6 Rayl) → concrete (ρ 2400 × v 3400 = 8.16e6 Rayl):
  `T = 0.525 = −2.8 dB`. Tolerable — **but this assumes a bonded, continuous contact.**
- Soft tissue → **air gap** (Z = 415 Rayl): `T = 1.11e-3 = −29.6 dB`.

A body in rubble is not bonded to it. It lies on broken, irregular, dusty material with
intermittent point contacts and air gaps. **One tissue-air interface costs 30 dB; the rubble pile
offers many.** The reference doc's §3 "KEY PHYSICS" box models the body as if rigidly cast into
concrete. **No real burial geometry resembles that**, and the spec contains no coupling term at
all — not in §3.3, not in §7's attenuation model `A = A₀e^(−αr)`, which has only an absorption
term and no interface term.

### 2.6 Audit pass 2 — where §2 could be wrong

- **The footstep anchor comes from one measurement family.** 3e-6 m/s at 3 m is a single
  reported peak; soil type, shoe, and gait all move it. If the true figure were 10× higher the
  deficit drops from 47–59 dB to 27–39 dB. **Still fatal, but less so.**
- **Linear force scaling footstep→heartbeat is crude.** It assumes the same source-coupling
  efficiency and radiation pattern for a 700 N normal impulse and a 1–4 N internal recoil. The
  heartbeat's coupling is realistically *worse*, so this is conservative in the project's favour.
- **The τ = 100 ms pulse duration** in §2.2 step 3 is taken from the brief. A shorter rise time
  concentrates the same energy into higher intensity; a 10 ms pulse would raise the predicted
  acceleration by √10 ≈ 3.2×. **This is my single largest soft assumption.** It does not change
  the verdict: 3.2× against a 14–435× deficit.
- **Hemispherical spreading is optimistic for the project.** Real rubble scatters into a diffuse
  field; the coherent first arrival that TDoA needs decays faster than 1/r.
- **I did not model resonance.** If a slab happens to resonate at the cardiac spectral peak and
  the body happens to be coupled to it, local amplification of 10–20 dB is conceivable. This is
  the one physical mechanism that could partially rescue the amplitude — see §7 condition C4. It
  is uncontrolled, unrepeatable, and cannot be designed around.

---

## 3. Attack 3 — the band is wrong, and this is the clearest error in the spec

**This one does not need any new measurement. It is a definitional error, and it is decisive.**

### 3.1 The error

MASTER §3.1 lists "Heartbeat, adult — **1.0–2.0 Hz** (60–120 bpm)" and §6 stage 1 specifies a
**4th-order Butterworth bandpass at 0.5–4 Hz**. The parenthetical gives the game away: *60–120
bpm* is the **repetition rate**, not the signal's spectral content.

A seismic sensor does not observe "a 1.2 Hz sinusoid." It observes a **train of impulses repeating
at 1.2 Hz**. The spectrum of that train is a comb of harmonics at multiples of 1.2 Hz, whose
**envelope is set by the shape and rise time of the individual impulse** — not by the repetition
rate. Filtering 0.5–4 Hz keeps the first three comb lines and discards the envelope that contains
essentially all the energy.

This is the same error as trying to record speech through a 0.5–4 Hz filter because people
produce about 3 syllables per second.

### 3.2 What the measurement says **[M]**

Taebi & Mansy (S1), 8 healthy subjects, PCB Piezotronics accelerometer at the left sternal border,
4th intercostal space, digitized at 3200 Hz. **Table IV, dominant SCG frequency by subject (STFT
column):**

| Subject | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 |
|---|---|---|---|---|---|---|---|---|
| **Dominant freq (Hz)** | 6.25 | 30.00 | 11.25 | 17.50 | 28.75 | 7.50 | 20.00 | 33.75 |

**Not one of the eight falls inside the spec's 0.5–4 Hz passband. The minimum is 6.25 Hz —
above the 4 Hz ceiling. The median is ~18.75 Hz, more than 4× the ceiling.**

The same paper localizes the two cardiac events SCG1 and SCG2 at **18.75 Hz and 37.50 Hz**, and
reports instantaneous frequency sweeping from 21 Hz down below 10 Hz within a single cycle. The
broader SCG literature (S2, S3) puts energy **below 30 Hz but concentrated well above 4 Hz**,
with the standard analysis band **0.5–100 Hz** or split as (0.05–1 Hz) for respiration and
**(1–40 Hz) for the mechanical SCG waves**, and attributes **energy above 18 Hz to valve closure**
and lower frequencies to muscle contraction.

### 3.3 So which band is right? **[C]**

**The 10–100 Hz proposal from the separate research pass is substantially closer to correct than
the 0.5–4 Hz in §6. MASTER §6 is wrong.** The best-supported band from the measured data is
roughly **5–40 Hz**, centred near 15–20 Hz.

But correcting the band **does not rescue the project — it makes the noise worse**, because
widening to 5–40 Hz costs √(35/3.5) = 3.2× more integrated sensor noise **[C]**:

```
0.5–4 Hz  (BW 3.5 Hz):  floor = 46.8 µg
5–40 Hz   (BW 35 Hz):   floor = 148 µg
```

And §3.1's own table puts **machinery at 20–200 Hz** and **aftershocks at 5–50 Hz** — i.e. the
corrected cardiac band **sits directly inside both of the noise sources the spec was relying on
the filter to remove.** The 0.5–4 Hz choice was quietly doing the project a favour by excluding
disaster-site noise; it was excluding the signal along with it.

**This is a genuine fork and both tines are bad:** keep 0.5–4 Hz and filter out the heartbeat, or
move to 5–40 Hz and admit the noise the architecture was designed to reject.

### 3.4 Audit pass 2 — where §3 could be wrong

- SCG is measured **on the sternum**, directly on the body. Propagation through rubble is
  **low-pass**: scattering and intrinsic absorption both rise with frequency, so the spectrum
  arriving at a node will be shifted down from the 6–34 Hz source range. **This is the strongest
  counter-argument to my §3 and it is real.** But §2.3 shows intrinsic absorption at 3 m is only
  ~1 dB, so the shift is modest — and it cannot move 18 Hz into a 0.5–4 Hz window without
  destroying the signal in the process. A low-pass severe enough to put the energy below 4 Hz
  has by definition removed almost all of it.
- The ±5–10 % HRV sidebands do spread each comb line, but they spread it by ±0.1 Hz, not by 15 Hz.
- 8 subjects is a small sample, all healthy. A crush-injured, hypothermic survivor's SCG spectrum
  is unmeasured. **This is a real gap in my evidence** — but there is no mechanism by which injury
  moves valve-closure transients from 18 Hz to 2 Hz.

---

## 4. Attack 4 — the incumbents solve a different, easier problem

**Has anyone ever detected a human heartbeat seismically through rubble? I found no evidence that
anyone has.** Not one source in this review describes a fielded or published seismic (mechanical
contact) cardiac detection through debris.

### 4.1 FINDER (NASA JPL / DHS) — **radar, not seismic** **[M]**

FINDER uses **reflected microwave radar**, beaming signals into debris and analyzing returns
(S12, S13). Claimed performance: **individuals as deep as 30 ft (9 m) in crushed material, behind
20 ft (6 m) of solid concrete, 100 ft (30 m) in open space**, with **80 % accuracy** through 30 ft
of dense rubble.

**This is not a counterexample to my verdict — it is an illustration of why the project's modality
is the wrong one.** FINDER detects **chest-wall displacement** via phase change in a reflected EM
wave. It never couples mechanically into the rubble. Its signal travels through **air gaps and
voids as an electromagnetic wave**, which is why it reaches 9 m. Radar measures **displacement**
directly, where a MEMS accelerometer measures **acceleration** and must fight f² weighting at low
frequency.

Note also what FINDER actually leans on: *"to pick out multiple victims, the device had to be able
to recognize the rhythms of distinct pairs of heart and breathing rates"* — it uses **both**, and
the heart-breathing coupling, rather than cardiac alone.

### 4.2 Delsar LifeDetector — **detects tapping, not heartbeat** **[M]**

The incumbent MASTER §9 benchmarks against. Vendor and operator documentation (S14, S15, S16):
seismic sensors with a **1 Hz – 3000 Hz** range that must be **in physical contact with the
structure**, converting the collapsed structure into a sensitive microphone to transmit
**"noises from entombed victims"** — sensitive enough to detect **"vibrations from trapped victims
moving or tapping in the rubble."**

**Delsar detects a conscious victim deliberately striking a slab. That is a signal many orders of
magnitude above a heartbeat — a hand or boot against concrete is a footstep-class impulse, not a
1–4 N internal recoil.**

### 4.3 What this does to the project's central value claim

MASTER §9 states: *"The Delsar argument survives intact. Incumbent ~$15,000, hand-placed one point
at a time, blind to unconscious victims. At $1,845 the order-of-magnitude advantage holds with 10×
margin."*

**This claim is invalid, and not because of the price.** The comparison is:

| | Delsar | This project |
|---|---|---|
| Detects | deliberate tapping/movement by a conscious victim | cardiac recoil of an unconscious victim |
| Source amplitude | footstep-class, ~10²–10³ N impulse | ~1–4 N |
| Demonstrated | yes, fielded by FEMA/UKSAR for decades | **never, by anyone** |

**"We beat a $15,000 incumbent at $1,845" is not a cost argument when the incumbent solves a
problem ~1,000× easier in amplitude and this project's problem has no demonstrated solution at any
price.** The honest framing is: the project is attempting an unprecedented world-first, and the
$15,000 device is cheap for what it reliably does.

### 4.4 The reference doc's Q6 "validation" claims are unsupported

Reference doc §9 Q6 answers *"Has seismic heartbeat detection been validated in real conditions?"*
with **"Yes. This is not theoretical."** and three specific claims. I attempted to verify each:

| Claim (reference doc Q6) | Status |
|---|---|
| "CERN researchers published seismic cardiac monitoring through concrete in 2018" | **NOT FOUND.** Targeted searching returned no such publication. CERN results that surface are neutron shielding and particle physics. **[A]** |
| "The US Army Research Lab validated MEMS seismic survivor detection through 2–3 m rubble in 2020" | **NOT FOUND.** Multiple search strategies across ARL/DEVCOM/DTIC surfaced nothing matching. ARL seismic work that does surface is footstep/vehicle target classification and infrasonic arrays — not cardiac. **[A]** |
| "Medical MEMS seismic beds (heartbeat through mattress) are commercial products" | **TRUE but irrelevant.** BCG/SCG bed sensors are real. They work through **~10 cm of foam in direct body contact**, not 3 m of rubble. **[M], but does not support the inference.** |

**This is the most serious integrity problem in the reference doc.** The one question that asks
directly whether the core premise has ever been validated is answered "Yes" on the strength of two
claims I cannot find any trace of and one that is a category error. **The project's physics premise
has been carried forward for its entire life on a citation that appears not to exist.**

I cannot prove a negative — see §8. But the burden is on the claim, and it has not been met.

---

## 5. Attack 5 — respiration vs heartbeat: **the brief's own premise is wrong**

The brief asserts respiration is "10–100× larger mechanically" and asks whether it should be the
primary target. **I ran it and the answer is more interesting than the brief expects. I am
reporting against my own instructions here.**

**In displacement, yes [C]:** tidal breathing moves the chest wall ~5 mm; cardiac SCG moves it
~0.1–0.5 mm. Ratio ≈ **17×**, consistent with the brief.

**In acceleration, the ranking reverses [C].** A MEMS accelerometer measures acceleration, and
`a = (2πf)²·d` — **frequency enters squared**:

```
Respiration:   d = 5 mm,   f = 0.25 Hz  →  a = (2π×0.25)² × 5e-3  = 1.23e-2 m/s² = 1.26 mg
Cardiac (SCG): d = 0.3 mm, f = 15 Hz    →  a = (2π×15)²   × 3e-4  = 2.66 m/s²    = 272 mg
```

**Cardiac is ~216× LARGER than respiration in acceleration**, because it is 60× faster and f²
beats the 17× displacement advantage by a wide margin.

**So the target selection in §3.1 is NOT backwards, and this is the one design judgement in the
spec that is defensible.** Respiration is worse for a MEMS accelerometer, and worse specifically:

1. 0.2–0.5 Hz is where **MEMS 1/f noise is worst** — 2.2× to 5× above the datasheet figure (§2.4).
2. 0.2–0.5 Hz **overlaps the secondary microseism peak at ~0.14 Hz** and its shoulder — the one
   band where the Earth itself is loudest. The NLNM at 0.5 Hz is **−152.8 dB, 13.6 dB worse than
   at 1 Hz [C]** — the quietest-possible-site floor is already degrading as you move down.
3. Wind loading on rubble is a <0.1 Hz phenomenon whose tail sits directly in the respiration band;
   §3.1's "low-cut" assumes a clean separation that does not exist.

**Correct conclusion: respiration is the better target for a different sensor class (tilt,
pressure, radar, laser vibrometry — anything that measures displacement rather than
acceleration), and a worse target for the ADXL355.** If the project pivots to respiration it must
also pivot away from MEMS accelerometers. See salvage §8.

---

## 6. Attack 6 — the reference doc's inherited claims

| Claim | Status | Finding |
|---|---|---|
| **">93 % accuracy at >1 m, >87 % at 0.5 m"** | **[A]** | Reference doc sources this to "analogous medical MEMS studies." Medical SCG is measured **on the sternum in direct contact**. Transferring an accuracy figure across a ~50 dB SNR gap is not an analogy, it is a non-sequitur. MASTER §6 already demotes it to TARGET — correct, but it should be **deleted**, not retargeted: an accuracy number is meaningless when §2 shows SNR is negative. |
| **"48–72 h runtime"** | **[A], already killed** | MASTER §4.1 correctly identifies the double-count and the CR2032 internal-resistance problem. I add: a **CR2032 cannot source 40 mA pulses at all** without catastrophic droop — typical CR2032 pulse capability is single-digit mA. The 25 h figure is also optimistic. Nothing further needed; §4.1's CONTESTED banner is right. |
| **"$29/node"** | **[A], already killed** | MASTER §9 rebuilt it at $67.75. Confirmed as a reference-doc error. |
| **"Raw rubble seismic data is ~95 % noise"** | **[A]** | Unsourced and, worse, **wildly optimistic in a way that inverts the design problem**. §2 computes SNR of −16 to −59 dB. At −20 dB the data is **99.0 % noise**; at −47 dB it is **99.998 % noise**. "95 % noise" implies 5 % signal — an SNR of about −13 dB — which is **better than any estimate in this document**. The figure sounds humble and is in fact the most optimistic number in the reference doc. |
| **"ICA separates up to N−1 sources with N nodes"** | **[A], and invalid** | See §6.1. |

### 6.1 ICA is not applicable here — three independent violations **[C]**

The standard ICA model is `x(t) = A·s(t)`: observations are an **instantaneous linear mixture** of
statistically independent sources, with **A a constant scalar matrix**.

**Violation 1 — the mixing is convolutive, not instantaneous.** This is fatal and it is fatal *by
the project's own design*. Seismic propagation applies a **different travel time** to each
source-sensor pair — that delay is the entire basis of §7's TDoA localization. The real model is
`x_i(t) = Σ_j h_ij(t) * s_j(t)` — a convolution with a propagation impulse response, including
delay, dispersion, and multipath from every air gap. **Plain ICA cannot invert this.** The project
cannot escape by denying the delays, because **§7 requires them to exist and to be measurable**.
MASTER §6 and §7 are therefore in direct contradiction: §6 assumes instantaneous mixing, §7 assumes
differential delay. Frequency-domain or convolutive ICA exists but introduces permutation and
scaling ambiguity across frequency bins — a substantially harder problem, not a citation.

**Violation 2 — the N−1 claim is wrong even in the ideal model.** Standard ICA requires **at least
as many sensors as sources** (N sensors → at most **N** sources, and practically N−1 after
removing a reference). The reference doc's Q2 states "theoretically separate up to N-1 sources
with N nodes," which is roughly the right *form* — but §11/§6 then claim degradation "past roughly
5 overlapping survivors" **while specifying 9 nodes**, which is not what the N−1 rule predicts
(that would be 8). The number is asserted, not derived. Minor, but symptomatic.

**Violation 3 — independence is questionable and moot.** Multiple survivors' hearts are plausibly
independent. But ICA also requires **non-Gaussianity**, and more importantly: **ICA operating on
channels whose SNR is −47 dB separates noise from noise.** Source separation cannot recover a
signal that was never above the floor. This violation is downstream of §2 and is the least
interesting of the three.

**Verdict: §6 stage 5 should be struck.** Not deferred — struck.

### 6.2 One more inherited error worth flagging **[C]**

§3.1 lists **"Footsteps 1–3 Hz, 5–50 mg"** and relies on amplitude thresholding to reject them.
The measured figure is **~0.037 mg at 3 m** (§1). **The spec overstates footstep amplitude by
137× to 1,369×.** This matters: the rejection strategy "machinery runs >10 mg against a 0.1–1 mg
heartbeat" (§6) is built on noise amplitudes that are themselves unsourced and, where checkable,
wrong by three orders of magnitude. **The amplitude-discrimination axis in §6 is not trustworthy.**

---

## 7. What would have to be true for this to work

The premise survives **only** inside the following regime. These conditions are conjunctive — all
of them, simultaneously. I state them precisely so the project can test the cheapest one first.

**C1 — Range collapses from 3 m to contact or near-contact.**
Signal falls as ~1/r (plus coupling). Closing from 3 m to 0.3 m buys **20 dB**. Closing to direct
body contact buys the whole coupling term back. **The viable regime is 0–0.5 m, not 2–3 m.**
Consequence: this is no longer a mesh that localizes a survivor; it is a proximity confirmer that
must already be on top of them. **It does not survive as a search tool.**

**C2 — The band moves to 5–40 Hz and the spec admits the noise that comes with it.**
Non-negotiable from §3. §6's 0.5–4 Hz filter must be deleted. Accept that the corrected band
overlaps machinery (20–200 Hz) and aftershocks (5–50 Hz) and that §3.1's filter-based rejection
strategy no longer works.

**C3 — The sensor changes class.**
The ADXL355 at 25 µg/√Hz is 50,000× noisier than the Earth's own floor and cannot see the signal
at any plausible range beyond contact. Required: a sub-µg/√Hz instrument. **Note the SM-24
geophone's 10 Hz corner — rejected in §3.2 as "above the entire target band" — is only a problem
for the WRONG band. Against the corrected 5–40 Hz band of C2, a 10 Hz-corner geophone is nearly
ideal.** §3.2's rejection of the geophone was a consequence of the §6 band error and should be
revisited. This is the single highest-value correction in this document.

**C4 — Favourable coupling, which cannot be engineered or relied upon.**
The victim must be in firm, continuous mechanical contact with a stiff continuous member (an
intact slab), not resting on loose debris with air gaps. Per §2.5, a single tissue-air interface
costs 30 dB. If a slab resonance happens to coincide with the cardiac spectral peak, 10–20 dB of
amplification is conceivable. **This is luck, not design.** No deployment protocol can guarantee
it, and nothing in §8's drop-grid influences it.

**C5 — A quiet site, which a disaster site is not.**
Needed only if C1–C4 are met. Given the sensor-limited finding (§2.4) this is the *least* binding
condition, which is itself the surprise of this review.

**C6 — Long, phase-coherent integration, which HRV forbids.**
Per §1, even the generous estimate needs 5.7 minutes of perfectly coherent averaging and the
realistic one needs 112–1,790 hours. Beat-to-beat variability of ±5–10 % destroys coherence long
before that. **Mitigable only by beat-domain (envelope/ensemble) averaging triggered by a detected
beat — which requires detecting a beat first. Circular.** Genuine escape: ensemble-average on an
independent trigger (see salvage §8).

**If all six held, the surviving system is:** a contact or near-contact (≤0.5 m) geophone-class
sensor, in the 5–40 Hz band, on a victim firmly coupled to intact structure, with ensemble
averaging on an external trigger. **That is not the project in MASTER.md. It is roughly a
Delsar — which already exists, costs $15,000, and is already deployed.**

---

## 8. Salvage — what nearby project is alive

The premise as stated is dead. **Several adjacent projects are alive, and some of the existing
work transfers directly.** This is the only constructive section, as instructed.

### S1 — Tapping-assisted / conscious-victim seismic mesh **(strongest salvage)**

**Keep:** the drone deployment, the LoRa mesh, the TDoA solver, the dashboard, §10.4's LongShoT
time sync (genuinely good work, <2 µs), the node mechanics, nearly all of §4, §5, §7, §8, §9, §12.
**Drop:** cardiac detection only.

**Target a tapping or movement signature instead of a heartbeat.** That is footstep-class
amplitude — **~10²–10³× above cardiac** — which is **+40 to +60 dB**, precisely the deficit §1
identified. The physics works, demonstrably: Delsar does it today.

**The novel contribution survives fully intact and is genuinely valuable:** Delsar is
**hand-placed, one point at a time, by an operator standing on unstable rubble**, giving a single
bearing. This project offers **drone-deployed, simultaneous, multi-point, automatically
triangulated** detection of the same signal — with a real time-sync solution already researched.
**That is a defensible and unprecedented contribution, and the $1,845-vs-$15,000 argument becomes
honest** because it now compares like with like.

Cost: gives up the unconscious-victim claim, which was the premise's headline — and which §2
shows was never deliverable.

### S2 — Respiration via a different sensor class

Per §5, respiration is the wrong target for a MEMS accelerometer but the right target for
**displacement-sensing** modalities. If the unconscious-victim capability is the non-negotiable
requirement, the modality must change to radar (the FINDER path, S12), laser Doppler vibrometry,
or a pressure/tilt sensor — **not an accelerometer**. This is a different project with a different
BOM, and it competes with a mature, fielded, government-funded incumbent.

### S3 — Contact/near-contact cardiac confirmer (narrow but real)

Under conditions C1–C4, a **geophone-class** sensor placed within ~0.5 m of a located victim could
plausibly confirm cardiac activity. Workflow: use another method to localize, then this to confirm
life before committing a dig. Modest, but the one place cardiac seismic detection might honestly
survive. **Requires C3 — sensor class change — and specifically revisiting the SM-24 rejection.**

### S4 — Multi-modal node, cardiac demoted

Keep the mesh and the drone; make each node carry **geophone (tapping) + microphone (voice,
200 Hz–3 kHz, per Delsar's own acoustic channel) + CO₂/VOC**. Cardiac detection becomes a stretch
goal, not a load-bearing assumption. **This retains the most project value for the least physics
risk**, and matches the real USAR workflow, which is multi-modal for exactly these reasons.

### Immediate, cheap next step

**Do not run §12 step 1 as specified** — its outcome is already determined by §2.4, and running it
will cost weeks to confirm what arithmetic gives today. Instead:

1. **Delete the 0.5–4 Hz filter** (§6 stage 1). It is wrong regardless of which salvage path wins.
2. ~~**Re-run §3.2's sensor trade against the corrected 5–40 Hz band.**~~ The geophone rejection is
   wrong and the correction is free — **this was done; the SM-24 is the selected sensor**
   (`07-verdict.md` §4.2). **[AMENDED 2026-10-11, ADR 0001: "the corrected 5–40 Hz band" is
   withdrawn. The band derived in §3.3 above is a **seismocardiography** band — correct for the
   *cardiac* question §3.3 was answering, and never derived from a tap. Acquire **5–200 Hz**; the tap
   detection band is an **output of the M1/M2 bench measurement**. The sensor trade does not re-open
   either way: the SM-24 corner costs −0.72 dB by 15 Hz and ~0 dB above 30.]**
3. **Run the §12 step 1 bench test on a TAPPING source instead**, at 1, 3 and 10 m. That measures
   the S1 salvage path's real detection range and uses hardware already specified.
4. **Decide S1 vs S4 before spending the $739 on the airframe** — MASTER §9 already correctly
   identifies that cost as deferrable.

---

## 9. Source table

Access verified by **inspecting response bodies**, not status codes. **LIVE** = content retrieved
and read · **BOTWALL** = reachable but blocked (CAPTCHA/403/redirect loop) · **DEAD** = not found.

| # | Source | Type | Used for | Access |
|---|---|---|---|---|
| S1 | Taebi & Mansy, *Analysis of Seismocardiographic Signals Using Polynomial Chirplet Transform and SPWVD*, Univ. Central Florida — arxiv.org/pdf/1711.11138 | peer-reviewed conf. | **[M]** SCG dominant freqs 6.25–33.75 Hz, Table IV; SCG1/SCG2 at 18.75/37.50 Hz; PCB Piezotronics accel, 3200 Hz | **LIVE** (PDF extracted locally; WebFetch could not parse, `pdftotext` could) |
| S2 | *Time-Frequency Distribution of Seismocardiographic Signals: A Comparative Study*, Bioengineering 4(2):32 — doi.org/10.3390/bioengineering4020032 | peer-reviewed | **[M]** dominant freqs ~9.20, 25.84, 50.71 Hz; >18 Hz = valve closure | **BOTWALL** (PMC mirror = reCAPTCHA; MDPI = 403; content via search abstract) |
| S3 | SCG/BCG review literature (SCG band 0–100 Hz, energy <30 Hz; dual bands 0.05–1 Hz and 1–40 Hz; analysis band 0.5–100 Hz) | peer-reviewed | **[M]** SCG bandwidth convention | **LIVE** (via search result text) |
| S4 | *Low frequency cultural noise*, Geophys. Res. Lett., 10.1029/2009GL039625 | peer-reviewed | **[M]** cultural noise 1–10 Hz dominance | **BOTWALL** (AGU PDF = 403; content via search) |
| S5 | Peterson (1993) NLNM, via `seizmo/noise/nlnm.m` coefficient table (github.com/g2e/seizmo) | reference impl. of USGS model | **[M]** NLNM coefficients A, B; `dB = A + B·log₁₀(T)` | **LIVE** |
| S6 | USGS Open-File Report 2005-1438, *Seismic Noise Analysis System Using PSD* — pubs.usgs.gov/of/2005/1438 | gov't agency | NLNM/NHNM framework, units (m/s²)²/Hz | **BOTWALL** (PDF is scanned/OCR-corrupt; unreadable) |
| S7 | *Shear wave velocity versus quality factor: results from seismic noise recordings*, Geophys. J. Int. 210(2):660 | peer-reviewed | **[M]** Qs30 **down to 3** (Bishkek, gravel), many sites <10; Berlin sand 32–70 | **LIVE** |
| S8 | *Person Identification using Seismic Signals generated from Footfalls* — arxiv.org/pdf/1809.08783 | preprint | footstep seismic characterization, geophone 2.88 V/mm/s | **BOTWALL** (rate-limited before full read; content via search) |
| S9 | Footstep seismic characterization literature (Succi et al. family; *Range limitation for seismic footstep detection*; *Vibration signature of human footsteps*) | peer-reviewed | **[M]** **peak ≤3×10⁻⁶ m/s at 3 m**; dominant ~19 Hz; geophone range 2.5 m indoor / 25 m outdoor | **LIVE** (via search result text) |
| S10 | *Ballistocardiogram: Mechanism and Potential for Unobtrusive Cardiovascular Health Monitoring*, Sci. Rep. 6:31297 | peer-reviewed | BCG forces in Newtons; body recoil from cardiac ejection | **BOTWALL** (nature.com → idp.nature.com auth redirect) |
| S11 | *Chapter 4: Seismic Signals and Noise* (GFZ / IASPEI New Manual of Seismological Observatory Practice) | standard reference | **[M]** Hamburg urban noise **20–40 dB above baseline, 0.5–30 Hz**; NLNM Table 4.1 | **BOTWALL** (GFZ 403; content via search) |
| S12 | NASA Spinoff 2018, *Radar Device Detects Heartbeats Trapped under Wreckage* — spinoff.nasa.gov/Spinoff2018/ps_1.html | gov't agency | **[M]** FINDER = **reflected microwave radar**; 30 ft rubble / 100 ft open, 80 % accuracy; uses heart+breathing rate pairs | **LIVE** |
| S13 | NASA JPL FINDER releases (Nepal 2015, Mexico, Türkiye 2023) — jpl.nasa.gov | gov't agency | **[M]** FINDER 30 ft crushed material, 20 ft solid concrete, 100 ft open | **LIVE** (via search) |
| S14 | Savox/Delsar LifeDetector LD3 product documentation — savox.com | vendor | **[M]** seismic 1 Hz–3000 Hz, acoustic 200 Hz–3000 Hz; requires physical contact | **LIVE** (via search) |
| S15 | Delsar LD3 Operation & Maintenance Manual (manualzz mirror) | vendor manual | **[M]** detects victims **"moving or tapping"**; sensor placement | **LIVE** (via search) |
| S16 | Delsar LD3 overviews (OTB Products, AllSafe, FireProductSearch) | vendor/distributor | **[M]** FEMA/UKSAR/SUSAR usage; 2/4/6 sensor configs | **LIVE** (via search) |
| S17 | Analog Devices ADXL355 datasheet | mfr. datasheet | **[M]** 25 µg/√Hz noise density, ±2 g | **LIVE** (figure as quoted in both project docs; not independently re-fetched — see §10) |
| S18 | *Estimates of Shear-Wave Q for Unconsolidated and Semiconsolidated Sediments in Eastern North America* | peer-reviewed | **[M]** Qp 100–160, Qs 50–80 Mississippi Embayment | **LIVE** (via search) |
| S19 | SEG Wiki, *Seismic attenuation*; Bulk Sediment Qp/Qs (USGS, Mooney) | reference / gov't | scattering vs intrinsic attenuation; Qi ≥ 2×Qs | **LIVE** (via search) |
| S20 | Acoustic impedance references (Routledge *Acoustical Properties of Biological Tissue*; TI *Physics of Ultrasound*) | textbook / technical | **[M]** soft tissue Z = 1.5–1.7 MRayl; `T = 4Z₁Z₂/(Z₁+Z₂)²` | **LIVE** (via search) |
| S21 | *Review — Microwave Radar Sensing Systems for Search and Rescue Purposes*, Sensors | peer-reviewed | radar as the established through-rubble vital-sign modality | **LIVE** (via search) |
| S22 | *An ultra-wideband high-dynamic range GPR for detecting buried people after collapse of buildings* | peer-reviewed | UWB radar for buried-person detection | **LIVE** (via search) |
| S23 | *Finding Earthquake Victims by Voice Detection Techniques*, MDPI Eng. Proc. 10(1):69 | peer-reviewed | acoustic/voice detection as the fielded alternative | **LIVE** (via search) |
| S24 | *MEMS Accelerometer Mini-Array (MAMA)*, Nof et al. 2019 (Berkeley) — rallen.berkeley.edu | peer-reviewed | MEMS accel real-world seismic performance envelope | **LIVE** (via search) |
| S25 | *Small Local Earthquake Detection Using Low-Cost MEMS Accelerometers*, Seismic Record 1(1):20 | peer-reviewed | MEMS accel detection thresholds in practice | **LIVE** (via search) |
| S26 | CERN 2018 "seismic cardiac monitoring through concrete" (reference doc Q6) | — | **claim verification** | **DEAD — not found.** No such publication surfaced. |
| S27 | US Army Research Lab 2020 "MEMS seismic survivor detection through 2–3 m rubble" (reference doc Q6) | — | **claim verification** | **DEAD — not found.** ARL/DEVCOM/DTIC searches surfaced only footstep/vehicle classification and infrasonic arrays. |

**Access-status honesty note:** several sources are marked LIVE "via search" — meaning the
substantive quoted content came through search-result extracts rather than a full page fetch. Two
WebFetch calls hit a session rate limit mid-review, and PMC/AGU/GFZ/Nature/MDPI were variously
CAPTCHA-walled, 403'd, or auth-redirected. **S1 and S5 — the two sources carrying the most
decisive findings (the SCG band and the NLNM floor) — were both read in full from primary
material**, which is where it matters most. The footstep anchor (S9) is the weakest-sourced
load-bearing number; see §10.

---

## 10. Where I could be wrong

Stated plainly, worst first.

1. **The footstep anchor (S9) is my weakest-sourced load-bearing input.** "3×10⁻⁶ m/s at 3 m" came
   through a search extract, not a full primary read, and I was rate-limited before I could
   confirm it against the original. **If that number is wrong by 10×, my strongest argument (§1)
   weakens from a 47–59 dB deficit to 27–39 dB.** Still fatal, but the rhetorical force drops.
   **This is the first thing a defender of the project should attack, and the first thing I would
   re-verify.** Note that the independent energy-budget route (§2.2) does not depend on it and
   still gives a 14–435× deficit.

2. **The pulse-duration assumption τ = 100 ms.** Taken from the brief. If the true cardiac impulse
   rise time is 10 ms, predicted acceleration rises by ~3.2×. Combined with a favourable reading
   of every other parameter this is my largest single source of optimism-for-the-project that I
   did not fully explore.

3. **I did not model resonance or waveguiding.** Rubble containing intact slabs and rebar could
   behave as a waveguide or resonator, with amplification at specific frequencies in specific
   geometries. 10–20 dB is conceivable. **It is the one mechanism that could materially move my
   numbers** — but it is uncontrolled, site-specific, unrepeatable, and cannot be designed into a
   deployment protocol. It also cuts both ways: resonance that amplifies the signal amplifies
   ambient noise in the same band.

4. **The low-pass argument against my §3 is real.** Propagation through rubble shifts the spectrum
   down from the measured 6–34 Hz source range. I argued (§3.4) that §2.3's ~1 dB intrinsic loss
   at 3 m makes this modest, but **scattering attenuation — which I did not quantify — is strongly
   frequency-dependent and I may be underestimating it.** If the shift is severe, the correct band
   is lower than my 5–40 Hz. It cannot plausibly reach 0.5–4 Hz with signal intact, so §6 is still
   wrong, but my proposed replacement band could be off.

5. **SCG amplitudes are measured on healthy, supine, uninjured subjects.** A crush-injured,
   hypothermic, hypotensive survivor — the actual target population — has lower stroke volume,
   lower blood pressure, and therefore a weaker signal than every number I used. **My estimates
   are biased in the project's favour on this axis.**

6. **"Not found" is not "does not exist" (§4.4).** The CERN and ARL claims may exist in venues my
   searching did not reach — DTIC restricted holdings, CERN internal notes, paywalled
   proceedings. I searched multiple phrasings and found nothing. **The burden is on the claim, and
   the project should either produce the citations or strike them.**

7. **I never independently re-fetched the ADXL355 datasheet (S17).** I took 25 µg/√Hz from the two
   project documents. It matches my recollection of the part and both docs agree, but it is the
   one spec I accepted on the project's own authority. **If anything, the real in-band figure is
   worse** (§2.4, 1/f), so this favours the project.

8. **My 1/f corner frequency for the ADXL355 is assumed, not sourced.** I presented 1 Hz and 5 Hz
   as scenarios rather than facts, and labelled them as such. The true corner should be read off
   the datasheet noise plot before anyone cites my numbers.

9. **I am reviewing hostilely by instruction.** I have tried to flag every place the evidence cut
   against my brief — most substantially in §2.3 (the low-Q attack **fails**; intrinsic
   attenuation is negligible at 3 m) and §5 (respiration is **not** the better target for an
   accelerometer; the brief's premise is wrong because of f² weighting). **A reader should weigh
   those two sections as evidence that the rest was not simply reverse-engineered toward a kill.**
