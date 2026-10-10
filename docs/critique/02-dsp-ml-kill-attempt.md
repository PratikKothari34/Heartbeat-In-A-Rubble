# 02 — DSP & ML Kill Attempt

Hostile review of the signal-processing and machine-learning content of `MASTER.md`
(§3.1, §6, §7, §11) and the inherited claims of `reference/Heartbeat_In_The_Rubble.md`.

**Posture:** the authors are competent. That is why the errors here are not arithmetic slips —
they are *consistent, self-reinforcing conceptual errors* that each individually look reasonable
and collectively make the system's two headline capabilities (classification and localization)
unreachable **as specified**.

Date **2026-10-06**. Labels: **MEASURED** (someone's instrument), **COMPUTED** (derived here from
raw inputs, arithmetic shown), **ASSERTED** (stated in the spec with no derivation).

Sibling document `00-my-own-arithmetic.md` §4/§6 reached the same *direction* on the timing term
by a rule-of-thumb and explicitly delegated the rigorous bound to this pass. This document
supplies that derivation and reaches a **harder** conclusion than the rule-of-thumb did.

---

## VERDICT

**The DSP chain is built on a category error in the first stage, and every downstream stage
inherits it.**

§3.1 lists the heartbeat as a *frequency* — "1.0–2.0 Hz (60–120 bpm)". It is not a frequency. It
is a **repetition rate of a broadband mechanical impulse**. The 0.5–4 Hz bandpass in §6 is
therefore matched to the *wrong quantity*: it keeps the rate and throws away the signal.

Everything the project is struggling with downstream — the unreachable accuracy table, the
unmeasurable detection range, the weak human/machine discriminator, the need for a neural network
to do a job a template would do — is a **downstream consequence of that one choice**, and several
of those problems dissolve when the band is widened.

The project is, additionally, **optimizing a term that does not matter** (clock sync) while the
term that dominates (arrival-time pick uncertainty) is not costed anywhere in `MASTER.md`.

### Ranked findings

| # | Severity | Finding |
|---|---|---|
| **F1** | **FATAL** | §6 stage 1: the 0.5–4 Hz band is matched to the beat *rate*, not the beat *signal*. Discards ~48 % of impulse energy at 100 ms pulse width, and keeps only **2 harmonics** at adult rates ≥100 bpm. Conceptual, not a parameter tweak. |
| **F2** | **FATAL** | §7 localization is **unreachable in the specified band at any plausible SNR**. CRLB pick error is **3,900–39,000× the clock-sync error** the project declared "largely answered". §7.2's table is off by 1–3 orders of magnitude. |
| **F3** | **FATAL** | §6 operating point: at a realistic prior the **PPV collapses to ~16 %** — five of every six map pins are phantom. The ">0.75, tuned for low false-negative rate" choice makes this *worse*, not better. |
| **F4** | **SERIOUS** | §6 HRV discriminator is **self-defeating below ~17 dB SNR**: pick jitter makes a zero-variance machine measure as 3.5–11 % "HRV" — indistinguishable from the human 5–10 % it is supposed to reject. |
| **F5** | **SERIOUS** | §6 FFT: "0.017 Hz ≈ 1 bpm" is arithmetically right and **operationally false**. HRV smears the peak over 6–12 bins. Effective resolution is **6–12 bpm, overstated 6–12×**. Directly contradicts F4's requirement. |
| **F6** | **SERIOUS** | §6 ICA: "N−1 sources with N nodes" is **not an ICA result** (it is the beamforming null theorem). Mixing is **convolutive**, not instantaneous; the problem is **underdetermined**; and permutation/scaling ambiguity breaks §7.1's amplitude-based depth. |
| **F7** | **SERIOUS** | §7.1 depth from `A = A₀e^(−αr)`: **two unknowns, zero equations**, and the model omits geometric spreading. Claimed ±0.5 m; a factor-of-2 ignorance of A₀ alone gives ±0.69–6.9 m. |
| **F8** | **SERIOUS** | §6 training data: **MIT-BIH is ECG — an electrical signal.** No forward model exists in the spec to convert it to ground acceleration. Training is circular: the model learns the authors' synthesis assumptions. |
| **F9** | **SLOPPY** | §6 LSTM is the wrong tool: **30,369 params, 177 MMAC/window**, and the naive `return_sequences` path needs **1.5 MiB** on a 64 KiB part. A matched filter beats it at ~1/1000 the compute. |
| **F10** | **SLOPPY** | §3.1/§6 "aftershocks removed by high-cut": a 4th-order Butterworth gives only **8.4 dB at 5 Hz**. Against a 10–1000 mg aftershock vs a 0.1–1 mg target you need 40–80 dB. |
| **F11** | **SLOPPY** | Reference doc: ">93 %/>87 % accuracy", "95 % of raw data is noise", and the §7.2 accuracy table are **reverse-engineered from the desired conclusion**. The accuracy table is internally impossible. |

---

## THE SINGLE MOST CONSEQUENTIAL ERROR

### F1 — The band is matched to the repetition rate, not to the signal

**ASSERTED**, `MASTER.md` §3.1: *"Heartbeat, adult | 1.0–2.0 Hz (60–120 bpm)"*
**ASSERTED**, §6 stage 1: *"4th-order Butterworth, 0.5–4 Hz"*
**ASSERTED**, reference §5: *"This eliminates: wind (<0.1 Hz), aftershocks (>5 Hz), machinery (>20 Hz). What remains: heartbeat band."*

**The error:** 60–120 bpm is how *often* the event repeats. It says nothing about the event's
spectral content. A cardiac contraction coupled into the ground is a **mechanical impulse** —
ventricular ejection with a rise time on the order of 50–150 ms. The spectrum of a periodic
impulse train is a **harmonic comb at multiples of the repetition rate, under an envelope set by
the pulse shape**:

```
x(t) = Σ p(t − n/f₀)   ⟹   X(f) = f₀ · P(f) · Σ δ(f − k·f₀)
                                      └───┬───┘
                            envelope = single-pulse transform
```

The repetition rate `f₀` sets the **comb spacing**. The pulse width `T_d` sets the **envelope
width**. The spec filtered on the comb spacing and ignored the envelope entirely.

#### COMPUTED — where the energy actually lives

Model: raised-cosine (Hann) pulse of total duration `T_d`, repeating at `f₀ = 1 Hz`.
Closed form `|P(f)| = (T_d/2)·sinc(f·T_d)/(1 − (f·T_d)²)`. Harmonic energy `E_k = |P(k f₀)|²`,
summed to 60 Hz.

| `T_d` | **energy in 0.5–4 Hz** | to 8 Hz | to 10 Hz | to 15 Hz | to 20 Hz | envelope −3 dB | −20 dB |
|---|---|---|---|---|---|---|---|
| 50 ms | **26.9 %** | 50.9 % | 61.2 % | 80.9 % | 92.4 % | 14.4 Hz | 33.0 Hz |
| **100 ms** | **52.0 %** | 84.6 % | 92.9 % | 99.6 % | 99.9 % | **7.2 Hz** | 16.5 Hz |
| 200 ms | 86.3 % | 99.9 % | 99.9 % | 100 % | 100 % | 3.6 Hz | 8.3 Hz |

**At the 100 ms figure the task posits, the spec's passband discards 48 % of the signal energy.
At 50 ms it discards 73 %.** The task's own estimate `1/(2·T_d) = 5 Hz` is a *lower* bound; the
true −3 dB point of the pulse envelope is **7.2 Hz** and the −20 dB point **16.5 Hz**.

#### COMPUTED — the harmonic-count problem is worse than the energy fraction

The energy table above uses `f₀ = 1 Hz` (60 bpm), the **most favourable case**. The comb spacing
*is* the heart rate, so a faster heart puts **fewer harmonics** in a fixed passband:

| Heart rate | `f₀` | Harmonics inside 0.5–4 Hz |
|---|---|---|
| 60 bpm | 1.00 Hz | 1, 2, 3, 4 Hz → **4 harmonics** |
| 100 bpm | 1.67 Hz | 1.67, 3.33 Hz → **2 harmonics** |
| 120 bpm (child, §5 ref) | 2.00 Hz | 2.00, 4.00 Hz → **2** (and k=2 sits *on* the cutoff, where the filter is −3 dB) |

A tachycardic survivor — which is the **physiologically expected state** for someone crushed,
frightened, hypovolaemic and hypoxic — presents the *fewest* harmonics and the *least* captured
energy. **The filter is least sensitive exactly for the patient most likely to be found alive.**

#### MEASURED — independent confirmation from the seismocardiography literature

Taebi & Mansy (2017), *Bioengineering* 4(2):32, measured the time–frequency distribution of
seismocardiographic signals — i.e. **the chest-wall mechanical signature of the heartbeat**, which
is the actual source this project is trying to detect through rubble:

> dominant spectral peaks at **f₁ = 9.20 ± 0.48 Hz, f₂ = 25.84 ± 0.77 Hz, f₃ = 50.71 ± 1.83 Hz**
> band-pass applied: **0.5–100 Hz**; sampling 320 Hz

**Every one of the three measured dominant peaks lies above the spec's 4 Hz ceiling.** The lowest
is 2.3× above it. The SCG literature routinely analyses 0.6–20 Hz for ejection events and >20 Hz
for heart sounds; the 1–25 Hz band is standard for the S1 complex.

> **This is the kill shot.** The spec's passband was chosen to match the number printed in the
> "Frequency" column of its own table, and that column contains a repetition rate. Measured
> cardiac-mechanical spectra put the dominant energy at 9–50 Hz. The spec filters it all out,
> then asks a neural network to recover a signal the filter already deleted.

#### Second-order consequence: the filter also fails at its *stated* job

**COMPUTED** — Butterworth magnitude `|H|² = 1/(1 + (f/f_c)^{2n})`, n = 4, f_c = 4 Hz:

| f | Attenuation |
|---|---|
| 5 Hz | **8.4 dB** |
| 8 Hz | 24.1 dB |
| 10 Hz | 31.8 dB |
| 20 Hz | 55.9 dB |
| 40 Hz | 80.0 dB |

§3.1 lists aftershocks at **10–1000 mg** against a **0.1–1 mg** target — a 20–80 dB gap. The
filter delivers **8.4 dB at 5 Hz**, where the aftershock band *starts*. The claim "high-cut
filter removes aftershocks" (reference §5) is false at the low edge of the band it claims to
remove. **F10.**

#### Is the right architecture a bandpass at all?

No. Because the signal is a **known-shape repeating transient in noise**, the optimal detector is
not a filter that isolates a frequency — it is a **matched filter / template correlator**, whose
output SNR is `2E/N₀` and depends only on **captured signal energy**, not on shape. This is the
Neyman–Pearson optimum under AWGN. Narrowing the band to 3.5 Hz throws away more than half the
energy `E`, so it **directly and irrecoverably degrades the optimal detector's performance** — and
the loss cannot be recovered by any downstream classifier, neural or otherwise. Data lost at
stage 1 is lost.

**Audit pass 2 (where F1 could be wrong):** the number that matters is the *coupled* pulse width
at the sensor, not at the chest. Rubble is dispersive and lossy, and high frequencies attenuate
faster than low ones — so propagation acts as a lowpass and the received pulse is **wider** than
the emitted one. If rubble attenuation is severe enough that nothing above ~5 Hz survives 2–3 m
of transit, the spec's band is accidentally correct. **This is a real possibility and I cannot
dismiss it without the §10.1 measurement.** But note what it costs: if nothing above 5 Hz
survives, then F2 applies in full force and **localization is dead regardless**, because timing
resolution scales with bandwidth. The spec cannot have it both ways: either the band is wide
(and §6 stage 1 is wrong) or it is narrow (and §7's accuracy table is unreachable). **§10.1 must
measure the received *spectrum*, not just an amplitude.** That is a change to the planned
experiment, and it is the single most valuable correction in this document.

---

## F2 — The project is optimizing the wrong timing term (CRLB)

**ASSERTED**, §10.4: time sync *"✅ LARGELY ANSWERED… <2 µs… negligible at every plausible velocity"*
**ASSERTED**, §7.2: *"the assumed 0.1 ms timestamp precision resolves to ±0.3 m"*

Both statements are true about the quantities they name, and **both are irrelevant**, because
neither is the dominant term. TDoA does not need a good *clock*; it needs a good **estimate of
when the beat arrived**. That estimate's variance is bounded by the Cramér–Rao bound for
time-delay estimation (Knapp & Carter 1976; Quazi 1981; Carter 1987).

**COMPUTED** — flat-band high-SNR CRLB, `σ_τ = (√3/2π)·1/(B√(BT))·1/√SNR`:

Band = 0.5–4 Hz ⟹ **B = 3.5 Hz**. Integration per pick `T = 1/B = 0.286 s`
(a narrow band cannot resolve a transient shorter than its own impulse response).

| SNR | σ_τ | position err @150 m/s | @1000 m/s | @3000 m/s |
|---|---|---|---|---|
| 0 dB | **78.7 ms** | 11.8 m | 78.7 m | 236 m |
| 10 dB | **24.9 ms** | 3.7 m | 24.9 m | 74.7 m |
| **20 dB** (the spec's own claim, §3.3) | **7.9 ms** | **1.18 m** | **7.9 m** | **23.6 m** |

### The comparison `MASTER.md` never makes

| Error term | Magnitude | Status in spec |
|---|---|---|
| Clock sync (LongShoT, §10.4) | **0.002 ms** | declared solved, celebrated |
| Timestamp quantisation (§7.2) | **0.1 ms** | identified as "the timing floor" |
| **Arrival-time pick, 0.5–4 Hz @ 20 dB** | **7.9 ms** | **not costed anywhere** |
| **Arrival-time pick, 0.5–4 Hz @ 0 dB** | **78.7 ms** | **not costed anywhere** |

**COMPUTED ratios:**
- pick/sync at 20 dB = 7.9 ms / 0.002 ms = **3,936×**
- pick/sync at 0 dB = 78.7 ms / 0.002 ms = **39,361×**
- pick/quantisation at 0 dB = **787×**

> §7.2 calls 0.1 ms "the timing floor" and §10.4 spent the project's effort — and a $24.95 GPS
> module — driving sync from "tens of µs" to 2 µs. **That is an improvement in a term 3,900×
> smaller than the one nobody measured.** Shaving the 0.002 ms term while the 7.9 ms term stands
> changes the total by 0.03 %. The GPS module is not wasted (it is needed for node position), but
> **§10.4's "downgrade" of time sync as a concern was based on an incomplete error budget.**

### What §7.2's table actually requires

**COMPUTED** — σ_τ needed for the claimed ±0.05 m (16-node row), and the SNR that implies in a
3.5 Hz band at T = 0.286 s:

| v | required σ_τ | required SNR |
|---|---|---|
| 150 m/s | 333 µs | **47.5 dB** |
| 1000 m/s | 50 µs | **63.9 dB** |
| 3000 m/s | 16.7 µs | **73.5 dB** |

The spec asserts >20 dB after filtering. **The table needs 47–74 dB — a shortfall of 27 to 53 dB,
i.e. a factor of 500 to 200,000 in power.** §7.2 already flagged the bottom two rows as below the
timestamp floor; it is worse than that. **Even the ±0.3–0.5 m (5-node) row is out of reach at
realistic velocity and SNR.**

### Bandwidth is the design variable — and it links F2 to F1

σ_τ scales as **B^(−3/2)** (one power from the phase slope, one half from the BT product).

**COMPUTED** — widening 0.5–4 Hz (B=3.5) to 0.5–25 Hz (B=24.5), equal SNR, equal T:

| | σ_τ @0 dB | σ_τ @10 dB | @20 dB |
|---|---|---|---|
| B = 3.5 Hz, T=0.2 s | 94.1 ms | 29.8 ms | 9.4 ms |
| B = 24.5 Hz, T=0.2 s | **5.1 ms** | **1.6 ms** | **0.51 ms** |
| improvement | **18.5×** | 18.5× | 18.5× |

`(24.5/3.5)^1.5 = 18.5` — exactly as predicted. At B = 24.5 Hz, T = 0.2 s, 10 dB SNR, the pick
error is **1.6 ms → 0.24 m at 150 m/s**. That is the first number in this analysis that is in the
same universe as the spec's ambition.

**MEASURED corroboration:** the microseismic picking literature reports improved STA/LTA
first-arrival errors of **~0.023 s at low SNR** on broadband seismic data — the same order as the
CRLB predicts for a wideband signal at modest SNR, and ~3× *better* than the spec's narrowband
0 dB figure despite being a cruder estimator. Consistent.

> **F1 and F2 are the same error seen from two directions.** Narrowing the band to isolate the
> beat *rate* is precisely what destroys the timing resolution needed to localize. **The §6 band
> choice and the §7 accuracy spec are in direct, unacknowledged conflict.**

**Audit pass 2 (where F2 could be wrong):** (a) coherent averaging over N beats buys √N — 60 beats
= 7.75×, taking the 20 dB narrowband figure from 7.9 ms to ~1.0 ms (0.15 m at 150 m/s). That
would rescue the lateral spec. **But it requires phase coherence across 60 s, which F4/F5 show
HRV destroys** (see the coherence calculation below). Incoherent envelope averaging is
HRV-immune but buys only ~N^(1/4) ≈ 2.8×. (b) The constant in the CRLB varies by a small factor
between formulations; I ran two (Quazi flat-band and an RMS-bandwidth phase-slope form) and they
differ by ~1.7× — immaterial against a 3,900× discrepancy. (c) If the real SNR is far above 20 dB
the picture improves — but §3.3 flags the detection-range assumption as the project's single
load-bearing unmeasured number, so 20 dB is itself ASSERTED.

**COMPUTED — the coherence limit, which closes the escape route:** HRV is a random walk in beat
phase. Accumulated timing jitter after n beats ≈ `σ_beat·√n`. Coherence is lost when that reaches
a half period (0.5 s):

| HRV | σ_beat | n to lose coherence |
|---|---|---|
| 5 % | 50 ms | (0.5/0.05)² = **100 beats = 100 s** |
| **10 %** | 100 ms | (0.5/0.10)² = **25 beats = 25 s** |

At 10 % HRV the coherent window is **25 s, not 60 s** — the spec's own window is *longer than the
signal stays coherent*. Coherent 60-beat averaging is not available at the upper end of the HRV
range the spec itself relies on.

---

## F3 — Base rate: the PPV collapses, and the threshold choice makes it worse

**ASSERTED**, §6: *"Accuracy — TARGET: > 93 % at > 1 m"*, *"Threshold > 0.75 = human confirmed;
tuned for low false-negative rate"*

Accuracy is the wrong metric for a rare-event detector, and "tuned for low false-negative rate"
means **trading specificity away** — which is exactly the parameter PPV is most sensitive to.

**COMPUTED** — decision unit = one node-minute (one 60 s window, one node). 9 nodes × 24 h =
**12,960 node-minutes/deployment**. Bayes: `PPV = sens·p / (sens·p + (1−spec)·(1−p))`.

**Scenario A — survivor present, heard by 3 of 9 nodes, 1 h out of 24** (prior p = 0.0139):

| sens | spec | **PPV** | TP/24 h | FP/24 h |
|---|---|---|---|---|
| 0.93 | 0.93 | **15.8 %** | 167 | **895** |
| 0.98 | 0.93 | **16.5 %** | 176 | **895** |
| 0.93 | 0.99 | 56.7 % | 167 | 128 |
| 0.93 | 0.999 | 92.9 % | 167 | 13 |

> **At the spec's own 93 % target, five of every six positive detections are false.** Raising
> sensitivity to 0.98 — literally what ">0.75, tuned for low false-negative rate" does — moves PPV
> from 15.8 % to 16.5 %. **The spec's tuning direction is the one that does not help.**

**Scenario B — empty rubble** (no survivor; the common case, since most of a search area is empty):

| spec | false alarms / 24 h | PPV |
|---|---|---|
| 0.93 | **907** | **0** |
| 0.99 | 130 | 0 |
| 0.999 | 13 | 0 |

**907 map pins per day, every one of them wrong.** Rescuers digging on a 72 h clock.

**COMPUTED — specificity actually required for PPV ≥ 90 %** (sens 0.95, prior 0.0139):
`(1−spec) ≤ 1.487×10⁻³` ⟹ **spec ≥ 99.85 %**, i.e. a false positive rate below **1 in 673
node-minutes**. The spec's 93 % implies **1 in 14**. **Shortfall: 48×.**

**COMPUTED — raw false-pin rate at 7 % FPR, one window/minute:**

| nodes | false pins/min | /hour | /day |
|---|---|---|---|
| 9 | 0.63 | 38 | **907** |
| 20 (reference doc's figure) | 1.40 | 84 | **2,016** |

### The mitigation the spec has but never quantifies — and why it is weaker than it looks

Requiring ≥3 nodes to concur (which §7.1 does require for TDoA) collapses the rate **if** false
positives are independent:

| concurrence | P(event) | false pins/day |
|---|---|---|
| ≥1 of 9 | 4.80×10⁻¹ | 691 |
| ≥2 of 9 | 1.27×10⁻¹ | 183 |
| **≥3 of 9** | **2.09×10⁻²** | **30** |
| ≥4 of 9 | 2.27×10⁻³ | 3.3 |

> **Independence is the load-bearing assumption and it is false.** The dominant noise sources —
> excavator, generator, aftershock, rescue crew, traffic — are **common-mode**: they hit every
> node in the array in the same minute. For correlated noise the joint FP rate stays near the
> marginal 7 %, not 7 %³. **The 3-node vote protects against the noise that was never the
> problem and not against the noise that is.** This is the single most important unexamined
> assumption in the detection chain, and it is nowhere in `MASTER.md`.

**Audit pass 2 (where F3 could be wrong):** the prior is mine, not the spec's — a real USAR
deployment targets a *specific* void where a survivor is suspected, which could raise the prior
to Scenario A's 1/3 case (PPV 87 %). I computed that case too; it is survivable. But (a) the
whole §8.1 pitch is **autonomous area search**, not confirmation of a known void, which forces
the low prior; and (b) **the empty-rubble scenario has no prior at all and 907 false pins/day
regardless** — and most of any search area is empty. The argument is not that the system can
never work; it is that **"93 % accuracy" is not a specification of anything operationally
meaningful**, and the spec currently has no false-alarm-rate requirement at all. That omission is
the finding.

---

## F4 — The HRV discriminator defeats itself at the SNR it must operate at

**ASSERTED**, §6: *"A human beat-to-beat interval varies ±5–10 %; a pump or motor at a nominal
1 Hz has effectively zero variance."*

Observed interval variance = true HRV variance **+ measurement variance**. Each interval is a
difference of two independent arrival-time picks, so it inherits `2σ_pick²`:

`σ_obs = √(σ_HRV² + 2σ_pick²)`

**COMPUTED** — σ_pick from the F2 CRLB (B = 3.5 Hz, T = 0.286 s); human HRV at 1 Hz: 5 % = 50 ms,
10 % = 100 ms:

| SNR | σ_pick | **zero-HRV machine *measures* as** | 5 % human measures as | 10 % human | verdict |
|---|---|---|---|---|---|
| 0 dB | 78.7 ms | **11.1 %** | 12.2 % | 15.0 % | **machine looks human** |
| 6 dB | 39.5 ms | **5.6 %** | 7.5 % | 11.5 % | **machine looks human** |
| 10 dB | 24.9 ms | **3.5 %** | 6.1 % | 10.6 % | **overlapping** |
| 20 dB | 7.9 ms | 1.1 % | 5.1 % | 10.1 % | separable |
| 30 dB | 2.5 ms | 0.4 % | 5.0 % | 10.0 % | clean |

> **At 6 dB SNR a perfectly rigid machine presents 5.6 % apparent HRV — inside the human band the
> spec uses to identify survivors.** The discriminator does not just degrade; it **inverts**,
> labelling machinery as human. And machinery is the loudest thing on the site (§3.1: >10 mg vs
> 0.1–1 mg), so it is present in a large fraction of windows.

**COMPUTED — SNR required** for pick jitter to stay under 1/3 of the 5 % HRV signal:
σ_pick ≤ 11.8 ms ⟹ **SNR ≥ 16.5 dB in a 3.5 Hz band.** The spec asserts >20 dB, so it *claims* to
clear this — but that 20 dB is the ASSERTED, unmeasured §3.3 number that §10.1 exists to test, and
the margin is only 3.5 dB.

**Observation-time question (as posed):** estimating a standard deviation from n samples has
relative standard error ≈ `1/√(2(n−1))`. **COMPUTED:** 25 % precision needs **9 beats (9 s)**;
10 % precision needs **51 beats (51 s)**. So the 60 s window *is* just barely adequate **for the
estimator's sampling error** — at 1 Hz. At 40 bpm (the hypothermic case §11 explicitly targets)
60 s yields only **40 beats**, and the window would need to grow. **The binding constraint is not
sample count, it is measurement jitter (above).** The spec worried about neither.

**Do real machines have zero variance?** No, and the spec's own reference doc half-admits it
(reference §9 Q1 concedes "a machine running at 1 Hz (rare but possible)"). Diesel engines under
varying load, hydraulic cycles, intermittent pneumatic tools, and generators responding to load
steps all exhibit cycle-to-cycle variation; reciprocating machinery under non-constant load is
routinely several percent. **The clean "±5–10 % vs 0 %" dichotomy is a false dichotomy from both
ends** — jitter inflates the machine's apparent HRV *and* real machines have genuine variance.

---

## F5 — The FFT resolution claim, and the HRV contradiction

**ASSERTED**, §6: *"60 s window at 100 Hz → 0.017 Hz resolution ≈ 1 bpm discrimination"*

**(a) The arithmetic is correct.** Δf = 1/T = 1/60 = **0.01667 Hz**. At any centre frequency,
converting to bpm: 0.01667 × 60 = **1.000 bpm**. **The spec's arithmetic passes.** (210 bins span
the 0.5–4 Hz band.) Note the sampling rate is irrelevant to resolution — only `T` matters — so
"60 s window at 100 Hz" names a quantity that does not affect the answer.

**(b) The claim is nonetheless operationally false,** because the peak is not a delta. HRV spreads
the instantaneous rate:

**COMPUTED** — mean interval 1.0 s, HRV = ±5 %: instantaneous rate ranges 1/1.05 to 1/0.95 =
0.9524–1.0526 Hz ⟹ spread **0.1003 Hz = 6.02 bpm = 6.0 bins.**
HRV = ±10 %: 0.9091–1.1111 Hz ⟹ spread **0.2020 Hz = 12.12 bpm = 12.1 bins.**

| HRV | fundamental smear | k=2 | k=3 | k=4 | **effective resolution** | overstatement |
|---|---|---|---|---|---|---|
| ±5 % | 6.0 bins | 12.0 | 18.1 | 24.1 | **6.0 bpm** | **6×** |
| ±10 % | 12.1 bins | 24.2 | 36.4 | 48.5 | **12.1 bpm** | **12×** |

Harmonics smear **proportionally to k**, so the higher harmonics — the ones carrying the energy
(F1) — are the most smeared. At ±10 % the 4th harmonic is spread over 48 bins.

**(c) Yes, it is self-contradictory — and here is the arithmetic.** §6 requires HRV **present**
(≥5 %, to reject machinery, F4) and **absent** (≤1 bpm ≈ 0.8 %, to achieve the claimed resolution).
These cannot both hold:

| requirement | needs HRV | source |
|---|---|---|
| "1 bpm discrimination" | **≤ 0.8 %** | §6 stage 2 |
| "human vs machine via HRV" | **≥ 5 %** | §6 discriminator |

**The two requirements are 6× apart and point in opposite directions.** The spec relies on both
in adjacent paragraphs.

**COMPUTED — the SNR cost nobody budgeted.** Smearing a peak over M bins divides its height by M:

| HRV | bins | **peak SNR loss** |
|---|---|---|
| 5 % | 6 | **−7.8 dB** |
| 10 % | 12 | **−10.8 dB** |

A **7.8–10.8 dB processing loss** appears nowhere in the §3.3 link budget. Against the 3.5 dB
margin computed in F4, this alone sinks the discriminator.

**(d) Is 60 s stationarity valid?** No. The coherence calculation in F2 gives **25 s at 10 % HRV**.
Real HRV also includes respiratory sinus arrhythmia (~0.2–0.4 Hz, the spec's own respiration band)
and slower Mayer-wave drift, both of which modulate rate *within* the window. **The 60 s FFT
integrates across a non-stationary signal, which is why the peak smears.**

**(e) What should it be instead?** **Autocorrelation or envelope autocorrelation, not a single
FFT.** Rationale:
- Autocorrelation of the **envelope** is insensitive to the carrier phase wander HRV causes, so it
  does not pay the 7.8–10.8 dB smearing loss.
- It naturally detects the **periodicity of a transient**, which is what this signal is, rather
  than assuming a sinusoid, which it is not (F1).
- Its peak lag directly estimates the beat interval; the **dispersion of successive peak lags is
  a far better HRV estimator** than spectral width, because it is a time-domain measurement of
  exactly the quantity §6 wants.
- A **spectrogram/STFT** (e.g. 10 s hops) would additionally expose rate *drift*, which is a
  stronger human signature than variance alone — a human's rate wanders; a machine's steps with
  load. The spec uses a single 60 s FFT and sees neither.

---

## F6 — ICA is invalid here, on four independent grounds

**ASSERTED**, §6: *"ICA separates up to N−1 sources with N nodes"*
**ASSERTED**, reference §9 Q2: *"same technique used in EEG brain signal separation"*

**(a) "N−1 sources with N nodes" is not an ICA result.** For linear instantaneous ICA the
standard condition is **#sensors ≥ #sources** — N sensors, at most **N** sources (the
determined/overdetermined case). There is no N−1. The N−1 figure is **the beamforming/adaptive
array theorem** (an N-element array can null N−1 interferers). Two different theorems from two
different literatures have been conflated. The EEG analogy in the reference doc is also where the
error likely entered: EEG *is* near-instantaneous mixing (volume conduction at essentially
infinite speed over 20 cm), which is exactly why ICA works there and **exactly why it does not
work here**.

**(b) The mixing is convolutive, not instantaneous.** Instantaneous mixing requires propagation
delay ≪ signal period. **COMPUTED** — delay as a fraction of a cycle at 4 Hz (top of the band):

| v | 5 m baseline | 10 m | 20 m |
|---|---|---|---|
| 150 m/s | 33.3 ms (0.133 cyc) | 66.7 ms (0.267 cyc) | **133 ms (0.533 cyc)** |
| 1000 m/s | 5.0 ms (0.020) | 10.0 ms (0.040) | 20.0 ms (0.080) |
| 3000 m/s | 1.7 ms (0.007) | 3.3 ms (0.013) | 6.7 ms (0.027) |

At the §10.5 **promoted** velocity bracket (150–1000 m/s) and realistic spacing, delays reach
**half a cycle** — a complete phase inversion. That is not a perturbation of an instantaneous
mixture; it is **frankly convolutive**. Worse, rubble is a multipath scattering medium: each
path also *filters* differently. The correct tool is **convolutive / frequency-domain BSS**, which
(i) needs far more data, (ii) solves an independent ICA per frequency bin, and (iii) therefore
inherits a **per-bin permutation problem** requiring a separate alignment algorithm. This is a
research problem, not a pipeline stage.

**(c) The problem is underdetermined.** **COMPUTED** source census for a live USAR site: survivor
×2, excavator engine, excavator hydraulics, generator, crew footsteps ×2, traffic, wind-driven
sway, aftershock microseismicity, pneumatic tool, drone downwash = **12 plausible independent
sources vs 9 nodes.** Underdetermined ⟹ plain ICA cannot separate, full stop. (The 3 axes per
node do **not** rescue this: three axes at one location sample one point of the wavefield and give
**polarisation**, not spatial diversity — they are not three independent mixtures.)

**(d) Permutation and scaling ambiguity break §7.1's depth estimate.** ICA output components are
unordered and of arbitrary scale — this is a *fundamental* indeterminacy, not an implementation
detail. Consequences the spec does not address:
- You do not know **which** separated component is survivor 1 vs survivor 2 **at each node**, so
  you cannot match the same source across nodes — and **TDoA requires exactly that correspondence**.
  Component k at node 1 and component k at node 2 may be different people.
- Scaling ambiguity means **the recovered amplitude is meaningless**, which destroys §7.1's
  `A = A₀e^(−αr)` depth estimate outright (see F7, which was already fatal for other reasons).

> §11 lists "> 5 overlapping survivors → ICA degrades" as the limit. The real limit is **≥1
> survivor plus the machinery that is always present**, and the failure is not graceful
> degradation — it is an invalid model assumption.

---

## F7 — Depth from amplitude: two unknowns, zero equations

**ASSERTED**, §7.1: *"Depth (Z): amplitude attenuation A = A₀·e^(−αr) solved for r … **±0.5 m***"

Solving `r = ln(A₀/A)/α` requires **both** `A₀` (source amplitude at the chest wall) and `α`
(rubble attenuation). Neither exists:
- **A₀** varies with body mass, posture, prone/supine, degree of crushing, coupling to debris,
  cardiac output, and blood volume. Unknown to **at least a factor of 10**.
- **α** is a property of the specific rubble pile, which is heterogeneous with air gaps. §10.5
  already concedes the project cannot even pin the *velocity* to better than 3–20×.

**COMPUTED** — depth error from A₀ ignorance alone, `Δr = ln(f)/α`:

| α | A₀ uncertain 2× | A₀ uncertain 10× |
|---|---|---|
| 0.1 /m | 6.93 m | 23.0 m |
| 0.5 /m | 1.39 m | **4.61 m** |
| **1.0 /m** | **0.69 m** | 2.30 m |
| 2.0 /m | 0.35 m | 1.15 m |

> **At a generous α = 1.0 /m, a mere factor-of-2 ignorance of A₀ already gives ±0.69 m — worse
> than the claimed ±0.5 m — before any uncertainty in α itself.** At a factor of 10 and α = 0.5,
> the error is **±4.6 m**, which spans the entire plausible burial range. The estimate carries
> **zero information**.

**The model is also structurally wrong.** For body waves the correct law includes geometric
spreading: `A = A₀·e^(−αr)/r`. The spec omits the `1/r`. **COMPUTED** — spreading alone gives
**6.0 dB** between 1 m and 2 m, comparable to the entire absorption term at short range. Fitting
the spec's equation to data that obeys the real one biases `α`, and therefore `r`, systematically.

### GDOP — depth is structurally ill-conditioned from a coplanar array

Even the *3D TDoA* alternative in §7.1 ("a 3D solve using the elevated drone as the out-of-plane
reference") fails, because all 9 nodes lie in one plane and the source is below it.

**COMPUTED** — DOP from the TDoA Jacobian, 3×3 grid at z = 0, source below centre:

| spacing | depth | HDOP_x | HDOP_y | **VDOP_z** | **VDOP/HDOP** |
|---|---|---|---|---|---|
| 4 m | 1.0 m | 0.42 | 0.43 | 1.38 | **3.2×** |
| 4 m | 2.0 m | 0.45 | 0.45 | 1.61 | **3.6×** |
| 4 m | 4.0 m | 0.57 | 0.54 | 2.40 | **4.2×** |
| 10 m | 2.0 m | 0.41 | 0.42 | 1.25 | 3.0× |
| 10 m | 4.0 m | 0.44 | 0.44 | 1.46 | 3.3× |

**Depth is 3–4× worse conditioned than lateral position**, structurally, for any coplanar array.
The physical reason: rays from a shallow source leave every node at a steep, nearly identical
angle, so the depth derivative is **nearly common-mode and cancels in the differences TDoA uses**.
This is the same result the microseismic literature reports — *surface arrays using only P-wave
arrivals have poor depth accuracy but good horizontal accuracy*.

§11 claims "**±0.5 m vs ±0.3 m**" for depth vs lateral — a ratio of **1.67×**. **The geometry
gives 3–4×, and that is before F2's pick error, which multiplies both.** The drone does not fix
this: it is an *emitter*-side reference, not a receiver below the plane, and it would have to
hover at a precisely known position while being the loudest object on site.

---

## F8 — Training on ECG to detect seismic impulses is a category error

**ASSERTED**, §6: *"Training data: PhysioNet MIT-BIH cardiac waveforms + USGS seismic noise
profiles + synthetic rubble noise from aftershock seismograms."*

**MIT-BIH is an ECG database.** 48 half-hour two-channel **ambulatory electrocardiogram**
recordings, 47 subjects, digitised at **360 Hz**, 11-bit over 10 mV, leads MLII and V1. It
measures the **electrical depolarisation** of cardiac muscle in millivolts at skin electrodes.

The project must detect **mechanical ground acceleration in milli-g**. These are different
physical quantities related by a chain the spec never writes down:

```
ECG (mV, electrical depolarisation)
  → electromechanical delay (~50 ms, varies with preload/afterload)
  → ventricular contraction & ejection (the mechanical event)
  → chest-wall motion  [this is SCG/BCG — the actual source]
  → coupling into debris (unknown, posture/contact dependent)
  → propagation through heterogeneous rubble (unknown α, unknown v)
  → ground acceleration at the node (mg)
```

**The forward model does not exist in the spec, and at least three of its links are flagged
elsewhere in `MASTER.md` as unmeasured** (§10.1 range, §10.5 velocity, coupling never mentioned).
An ECG R-peak tells you *when* a beat happened; it tells you essentially nothing about the
*waveform shape* of the resulting seismic impulse — and waveform shape is precisely what a matched
filter or an LSTM would need to learn.

**The sharpest form of the objection:** MIT-BIH's actual value here is as a source of **realistic
beat-interval sequences (RR intervals)** — i.e. real HRV statistics. That is genuinely useful and
is probably what the authors meant. But it means the model can only learn **rhythm**, not
**morphology** — and rhythm alone is a one-dimensional feature (interval variance) that needs no
LSTM and is better measured by autocorrelation (F5). **If MIT-BIH is being used for waveform
morphology, that is a category error. If it is being used for rhythm, it does not justify the
architecture.** Either way §6 does not survive.

### The circularity

If the signal is synthesised (from an assumed impulse shape, an assumed coupling, an assumed α)
and the noise is synthesised ("synthetic rubble noise"), then:

> **The model learns the authors' synthesis assumptions, and the test set validates the
> synthesiser, not the system.** A 93 % accuracy figure obtained this way measures only
> self-consistency. It would be equally achievable if the forward model were completely wrong.

This is not a hypothetical risk; it is the **mechanism by which the inherited >93 % number came to
exist** (F11). §12 step 2 ("Pipeline on synthetic data — filter, FFT, LSTM, against generated
signal + noise") **schedules this circularity into the build order**, before §12 step 1's
measurement has constrained the synthesiser. The order is right (step 1 first) but the spec must
state that **step 2 produces no accuracy claim** — it produces a sanity check on code.

**The honest position:** no accuracy number of any kind can be claimed until §10.1 produces
**real recorded ground acceleration from a real human through real attenuating material**. That
dataset does not exist and collecting it is the actual critical path of this project.

---

## F9 — The LSTM is the wrong tool, and probably untrainable

**ASSERTED**, §6: *"LSTM 64 (return sequences) → LSTM 32 → Dense 16 ReLU → sigmoid"*
**ASSERTED**, reference §5: *"Input | 60-second seismic window, 100 Hz sampling"*

**(a) COMPUTED — parameter count.** LSTM params = `4·(units·in_dim + units² + units)`:

| layer | arithmetic | params |
|---|---|---|
| LSTM(64, return_seq), in=3 (XYZ) | 4·(64·3 + 64·64 + 64) | 17,408 |
| LSTM(32), in=64 | 4·(32·64 + 32·32 + 32) | 12,416 |
| Dense(16) ReLU | 32·16 + 16 | 528 |
| Dense(1) sigmoid | 16·1 + 1 | 17 |
| **TOTAL** | | **30,369** |

(29,857 for a single-channel input.) 118.6 KiB as float32; 29.7 KiB int8.

**(b) COMPUTED — compute and memory.** Sequence length = 60 s × 100 Hz = **6,000 timesteps**. The
recurrence must be unrolled over all of them:

- MACs per timestep (both LSTM layers) = **29,440**
- **MACs per 60 s window = 29,440 × 6,000 = 176,640,000 ≈ 177 MMAC**

On the **Cortex-M4 @ 80 MHz** (the STM32WLE5 inside the RAK3172 that §9 already bought, and which
§10.3 contemplates for on-node inference):

| assumption | time per window |
|---|---|
| 1 MAC/cycle (CMSIS-DSP SIMD, optimistic) | **2.21 s** |
| 0.3 MAC/cycle (realistic with gating + activations) | **7.36 s** |

A window arrives every 60 s, so it *fits* on duty cycle — but at **2.2–7.4 s of full-power MCU
activity per minute**, i.e. a **3.7–12 % active duty cycle at ~10 mA against a 2 µA sleep
current**. Against §4.1's already-**CONTESTED** ~9 mA budget on a 225 mAh CR2032, this is not
free; it is comparable to the entire rest of the node's consumption.

**Memory — the harder problem.** `return_sequences=True` on layer 1 nominally materialises
**6,000 × 64 × 4 B = 1,500 KiB = 1.5 MiB**. The STM32WLE5 has **64 KiB of RAM total**.
**Over budget by ~24×.** A careful streaming implementation (feeding LSTM2 one timestep at a time
and never storing the sequence) reduces this to ~2 KiB of state — **but §6 does not say which is
intended**, and the difference is the difference between "fits" and "impossible". Specifying
`return_sequences` without specifying the execution strategy is how this error ships.

**(c) The architecture does not match the problem.** The signal is a **known-shape transient
repeating at an unknown but slowly-varying rate**. For that, the optimal detector under AWGN is
the **matched filter** (Neyman–Pearson optimal; output SNR = 2E/N₀, maximised by the Cauchy–Schwarz
equality condition), followed by periodicity estimation on the detection series. Compare:

| detector | ops per 60 s window | params to learn | training data needed |
|---|---|---|---|
| **LSTM as specified** | **177 MMAC** | **30,369** | ~10⁴–10⁵ labelled real windows (do not exist) |
| Matched filter + envelope autocorrelation | **~0.2 MMAC** (6,000-pt FFT ×2 + correlation) | **~0** (template + threshold) | **one** measured template |

**~1000× less compute, ~0 parameters, and it needs the measurement the project must take anyway.**

**(d) It is probably untrainable in practice.** 30,369 parameters need on the order of 10⁴–10⁵
independent labelled examples to fit without overfitting. The project has **zero** real labelled
examples (F8). Training on synthetic data produces a model that has learned the synthesiser (F8).
And §10.3 defers the MCU choice to "on-node inference needs the headroom" — committing hardware
budget to a model that should not exist.

**Audit pass 2 (where F9 could be wrong):** an LSTM *would* earn its place if the discriminating
feature were a **long-range temporal pattern that no hand-designed statistic captures** — e.g. a
subtle joint structure across HRV, respiration coupling (respiratory sinus arrhythmia *is* a real
human-specific signature, and §3.1 already lists respiration as "secondary confirmation"), and
amplitude envelope. That is a legitimate argument for a learned model, and I will not claim a
matched filter dominates in every regime. **But it cannot be made before a real dataset exists**,
and when it is made, the right comparison is against a tuned classical baseline — which §6 never
specifies, so there is nothing to beat. **Build the classical detector first; it is also the
thing that generates the labels the learned model would need.**

---

## F11 — Inherited claims that are reverse-engineered

**(a) ">93 % at >1 m, >87 % at 0.5 m."** Reference §5 sources these as *"based on analogous
medical MEMS studies"*. `MASTER.md` §6 is already honest — *"Inherited claim, no measurement
behind it"*. Three further problems it does not state:
- The figures are quoted **"at >1 m SNR"** and **"at 0.5 m SNR"** — *metres are not a unit of
  SNR*. The reference doc's own table header is dimensionally incoherent, which is the signature
  of a number copied without being understood.
- **Accuracy goes UP with distance** (93 % at >1 m vs 87 % at 0.5 m). That is backwards: signal
  amplitude falls with range, so performance must fall with range. Either the labels are
  inverted or the numbers were chosen for presentation. **Taken literally the table says the
  system works better the further away the survivor is.**
- "Analogous medical MEMS studies" means **sensors in direct contact with a chest, in a quiet
  room** — SNR tens of dB above a sensor on rubble 3 m away through concrete. The analogy
  transfers nothing.

**(b) "Raw rubble seismic data is ~95 % noise"** (`MASTER.md` §3.1; reference §5). **This is not a
measurable quantity as stated.** 95 % of *what* — time? energy? variance? bandwidth? If energy,
the true figure is far worse: a 0.1–1 mg target against 10–1000 mg machinery and aftershocks is
**80–140 dB down**, i.e. **99.99999 %+ noise by energy**, not 95 %. The "95 %" makes the problem
sound 5 orders of magnitude easier than it is. It should be deleted or replaced with a measured
SNR in dB.

**(c) The §7.2 accuracy-vs-node-count table is fabricated.** `MASTER.md` already flags two
constraints invalidating the lower rows. It is worse — the table is **internally impossible**:

| nodes | claimed accuracy | implied improvement |
|---|---|---|
| 3 | ±1–2 m | baseline |
| 5 | ±0.3–0.5 m | **4×** better for 1.67× the nodes |
| 9 | ±0.1–0.2 m | **2.5×** better for 1.8× the nodes |
| 16 | ±0.05 m | **3×** better for 1.78× the nodes |

Multilateration error scales roughly as **1/√N** from redundancy (plus a geometry term). Going
3 → 16 nodes gives √(16/3) = **2.3×**. **The table claims 1–2 m → 0.05 m = 20–40×.** It is
**10–17× steeper than estimation theory permits**, and it is monotone-smooth in a way real GDOP
never is. These are **numbers chosen to make a slide**, back-calculated from "±0.05 m sounds
impressive at 16 nodes". Combined with F2, the entire table should be struck, not patched —
`MASTER.md` §7.2 says "rebuilt once §10.1 gives a measured r"; it should say **deleted until
§10.1 and a pick-error budget exist**.

**(d) Reference §9 Q6's validation claims are uncheckable as written.** *"CERN researchers
published seismic cardiac monitoring through concrete in 2018"* and *"The US Army Research Lab
validated MEMS seismic survivor detection through 2–3 m rubble in 2020"* carry **no author, no
title, no venue, no DOI**. I could not verify either in this session (web search rate-limited —
see source table). **An unattributed claim of prior validation is the single most load-bearing
citation in the whole document** — it is the answer to "has this ever been shown to work?" — and
it is unsourced. **These two citations must be run down and produced in full, or the claim
withdrawn.** If the ARL result is real it would also supply the measured spectrum F1 needs.

**(e) Reference §9 Q3 is wrong on its own terms.** *"drone motors vibrate at 200–400 Hz — far
above our 0.5–4 Hz target band. The bandpass filter eliminates all of this. The drone could be
flying directly above the node with zero impact on readings."* Rotor **blade-pass tones** are at
200–400 Hz, but the **thrust-modulated downwash and airframe buffeting** load the ground with
broadband low-frequency energy well inside 0.5–4 Hz, and a 100 Hz sampler **aliases** any
unfiltered 200–400 Hz content back into the baseband unless there is an analogue anti-alias filter
— which §4 does not specify. "Zero impact" is asserted, not derived. (The ADXL355 does have a
configurable digital filter, which likely saves this in practice — but the spec does not say so.)

---

## THE PIPELINE I WOULD BUILD INSTEAD

Concrete, and ordered so that each stage produces the measurement the next one needs.

### Stage 0 — Measure the spectrum before designing the filter *(replaces §12 step 1)*

§10.1 as written measures *amplitude vs distance*. **That is insufficient and will produce a
filter as wrong as the current one.** Measure instead:

- **Power spectral density of the received signal, 5–200 Hz** (the ADR 0001 acquisition band), for a
  **tapping source** at 0.5/1/2/3 m through representative material. **[AMENDED 2026-10-11: was
  *"0.1–50 Hz … for a still human subject"* — a *cardiac* protocol over a band that would
  **structurally exclude** the 60–80 Hz region this measurement now exists to test. That is exactly
  the error this section warns about four paragraphs down, one octave up.]**
- The **time-domain impulse shape** of a single beat at the node (this is the matched-filter
  template and it does not exist today).
- The **ambient PSD of the same band** with no subject (this gives real SNR in dB, replacing the
  "95 % noise" and ">20 dB" assertions).
- **Deliverable: an SNR-vs-frequency curve.** Every band decision below follows from it
  mechanically, and it is the *only* way to settle F1 honestly.

Sample at **≥500 Hz** during this experiment, not 100 Hz. You cannot discover energy at 25 Hz with
a pipeline that has already decided it is not there. The ADXL355 supports it; the cost is storage
on a bench rig, which is free.

### Stage 1 — Filter: wide, and set by Stage 0

**Replace 4th-order Butterworth 0.5–4 Hz with a band set by the measured SNR curve**, with a
defensible prior of **20–80 Hz**, tagged `[ASSERTED — pending M2]` (ADR 0001, 2026-10-11), acquired
over **5–200 Hz**.

> **[AMENDED 2026-10-11.]** This originally read *"a defensible prior of **~1–25 Hz** (captures the
> measured SCG peak at 9.2 Hz …)"*. **The "set by the measured SNR curve" half is right and is the
> whole point; the numeric prior was cardiac** — justified by an **SCG** peak, i.e. derived for the
> premise this review helped kill. The B ≈ 24 Hz timing argument from F2 survives intact: any band
> wider than ~25 Hz delivers it, and 20–80 Hz (B = 60 Hz) delivers more.

- **Use a linear-phase FIR**, not Butterworth. A 4th-order IIR has **non-linear phase**, which
  introduces frequency-dependent group delay — **a systematic, uncorrected bias directly on the
  arrival time TDoA measures**. This is an error `MASTER.md` does not mention at all and it is
  free to fix. If IIR is required for MCU cost, use **zero-phase forward-backward filtering**
  (offline) or compensate the group delay explicitly.
- Keep a **separate narrow 0.15–0.6 Hz branch** for respiration (§3.1's "secondary confirmation"),
  which genuinely *is* a quasi-sinusoid and for which a narrow band is correct.
- Handle machinery with an **adaptive notch / spectral subtraction** keyed to the observed
  machinery lines, not a fixed high-cut (§11 already proposes this; it belongs here).

### Stage 2 — Detector: matched filter, not FFT

**Replace "FFT → LSTM" with template correlation → envelope → periodicity.**

1. **Matched filter** against the Stage 0 measured beat template (normalised cross-correlation).
   Optimal under AWGN; output SNR = 2E/N₀; ~0.1 MMAC per window via FFT-based correlation.
   Where the noise is strongly coloured (it is), use the **generalised cross-correlation with
   PHAT or ML weighting** (Knapp & Carter) — this is the *same* operator that Stage 4 needs, so
   it is implemented once.
2. **Envelope** (Hilbert or squared-and-smoothed) → a beat-detection series.
3. **Periodicity on the envelope autocorrelation**, not on the raw FFT. HRV-immune (F5), and the
   peak lag gives the beat interval directly.
4. **STA/LTA** as a cheap always-on trigger to gate the expensive stages — this is the standard
   seismological transient detector and it is what §10.2's event-only transmission needs anyway.

### Stage 3 — Classifier: start with no neural network

**Replace the LSTM with an explicit, auditable feature vector + logistic regression or a small
gradient-boosted tree:**

| feature | rejects |
|---|---|
| beat-interval dispersion (RMSSD/SDNN from autocorrelation peak lags) | rigid machinery — **with the F4 jitter correction applied** |
| template correlation peak value & shape | non-cardiac transients |
| harmonic structure ratio (energy at k·f₀ vs between) | broadband noise |
| respiration–cardiac coupling (RSA: is rate modulated at 0.2–0.4 Hz?) | **machinery cannot fake this** — the strongest human-specific feature available, and the spec already has the data |
| absolute amplitude | footsteps, machinery (§3.1's second axis) |
| cross-node coherence | common-mode noise — **directly attacks F3's correlated-FP problem** |

This is auditable (a rescuer can be told *why* a pin appeared), trains on hundreds not 10⁵
examples, runs in microseconds on the M4, and **establishes the baseline any future LSTM must
beat**. Revisit a learned model only when real labelled field data exists and the baseline is
measurably insufficient.

**Critically — specify the operating point as a false-alarm rate, not accuracy.** From F3: to
reach PPV ≥ 90 % at a realistic prior requires **FPR ≤ 1.5×10⁻³ per node-minute**. **That, not
"93 % accuracy", is the system requirement.** Set the threshold on the measured ROC at that FPR
and report the sensitivity that results.

### Stage 4 — Timing: GCC-PHAT on the wideband signal, not a threshold crossing

- Estimate arrival time by **generalised cross-correlation (GCC-PHAT)** between node pairs on the
  **wide-band** (Stage 1) signal, with **sub-sample parabolic interpolation** of the correlation
  peak.
- **Stack across beats**: correlate the *envelope* over many beats (incoherent, HRV-immune,
  gain ≈ N^¼) rather than assuming 60 s coherence that F2 shows does not exist at 10 % HRV.
- **Report a covariance, not a point.** Every pin on the §2 dashboard must carry an uncertainty
  ellipse derived from the actual pick variance. A map pin with no error bar is the mechanism by
  which F2 and F3 reach a rescuer with a shovel.
- **Expected honest performance** (COMPUTED, B = 24.5 Hz, T = 0.2 s, v = 150 m/s): **0.24 m at
  10 dB, 0.76 m at 0 dB** lateral, **×3–4 worse in depth** (F7 GDOP). Sub-metre lateral is
  achievable. **±0.05 m is not, ever.**

### Stage 5 — Multi-source: drop ICA

Replace with either:
- **Template-matched clustering of detections**: each detected beat gets (time, node, amplitude);
  cluster in TDoA space. Two survivors at different locations produce two distinct hyperbolic
  intersections *without any source separation at all* — exactly as reference §9 Q2's first
  sentence says, before it invokes ICA unnecessarily.
- Or, if genuinely overlapping, **convolutive/frequency-domain BSS** with explicit permutation
  alignment — but scope it as research, not a pipeline stage, and only after Stage 0.

**Delete the "N−1 sources with N nodes" claim.** It is not a real result.

### Summary of changed numbers

| quantity | spec | replacement |
|---|---|---|
| Band | 0.5–4 Hz Butterworth IIR | **Linear-phase FIR over a 5–200 Hz acquisition; detection band set by M2** — `20–80 Hz [ASSERTED]` where one figure is needed (ADR 0001). ~~~1–25 Hz~~ was an SCG prior |
| Sample rate (bench) | 100 Hz | **≥500 Hz** until the spectrum is known |
| Transform | 60 s FFT | **matched filter + envelope autocorrelation** (+ STFT for drift) |
| Classifier | LSTM 64/32 (30,369 params, 177 MMAC) | **feature vector + logistic regression (~10 params, ~0.2 MMAC)** |
| Operating point | ">0.75, accuracy >93 %" | **FPR ≤ 1.5×10⁻³ /node-minute**, sensitivity reported at that point |
| Timing | timestamp threshold, 0.1 ms | **GCC-PHAT + sub-sample interp, σ_τ reported** |
| Separation | ICA, "N−1 sources" | **TDoA-space clustering**; BSS only as research |
| Depth | `A=A₀e^(−αr)`, ±0.5 m | **report as unobservable** pending a non-coplanar node or S-wave arrival |

---

## SOURCE TABLE

Link status verified by **inspecting the response body**, per the project's own
`verify-links-by-body-not-status-code` rule. **Web search and fetch hit a session rate limit
partway through this review**; sources I could not re-verify in-session are marked
**UNVERIFIED-IN-SESSION** rather than claimed LIVE. That is a real gap in this deliverable and is
stated rather than papered over.

| # | Source | Used for | Status |
|---|---|---|---|
| 1 | Taebi A, Mansy HA. *Time-Frequency Distribution of Seismocardiographic Signals: A Comparative Study.* Bioengineering 2017;4(2):32. `pmc.ncbi.nlm.nih.gov/articles/PMC5590466/` | **F1** — measured SCG peaks 9.20±0.48, 25.84±0.77, 50.71±1.83 Hz; 0.5–100 Hz band; 320 Hz fs | **LIVE** — body read, numbers quoted directly |
| 2 | Quazi AH. *An overview on the time delay estimate in active and passive systems for target localization.* IEEE Trans ASSP 1981;29(3). DOI 10.1109/tassp.1981.1163618. `zenodo.org/records/1280942` | **F2** — flat-band TDE CRLB | **LIVE** — Zenodo record body read; PDF 759.4 kB present, 717 downloads |
| 3 | Knapp CH, Carter GC. *The Generalized Correlation Method for Estimation of Time Delay.* IEEE Trans ASSP 1976;24(4):320–327 | **F2, Stage 4** — ML delay estimator = prefilter + crosscorrelator; PHAT weighting | **LIVE (secondary)** — citation confirmed via search body; primary IEEE page not fetched |
| 4 | Carter GC. *Coherence and Time Delay Estimation.* Proc IEEE 1987;75(2) — PDF mirror `buzsakilab.nyumc.org/.../CarterIEEE1987.pdf` | **F2** — CRLB variance vs bandwidth/SNR | **UNVERIFIED-IN-SESSION** — URL surfaced in search; body not fetched |
| 5 | MIT-BIH Arrhythmia Database, PhysioNet. `physionet.org/content/mitdb/1.0.0/` | **F8** — 48×30 min, 2-channel **ECG**, 360 Hz, 11-bit/10 mV, leads MLII+V1, 47 subjects, ~110k annotations | **LIVE (secondary)** — specs confirmed from PhysioNet directory body via search; direct fetch blocked by rate limit |
| 6 | Van Trees HL. *Detection, Estimation, and Modulation Theory, Part I.* Wiley | **F2** — CRLB framework, RMS-bandwidth form | **UNVERIFIED-IN-SESSION** — canonical text, cited from standing knowledge |
| 7 | Kay SM. *Fundamentals of Statistical Signal Processing, Vol. I (Estimation) & II (Detection).* Prentice Hall | **F2, F9** — CRLB; matched filter / NP optimality | **UNVERIFIED-IN-SESSION** — canonical text |
| 8 | MIT OCW 6.011 ch.14, *Signal Detection* — `ocw.iti.hr/.../MIT6_011S10_chap14.pdf` | **F9, Stage 2** — matched filter maximises output SNR; 2E/N₀ | **LIVE (secondary)** — content confirmed via search body |
| 9 | TU Delft ET4386 *Neyman–Pearson detection* lecture notes — `cas.tudelft.nl/Education/courses/et4386/Slides/9-neyman-23.pdf` | **Stage 2** — NP optimality of matched filter | **LIVE (secondary)** — surfaced and summarised in search body |
| 10 | TU Graz, *Matched filter / detection* course notes — `www2.spsc.tugraz.at/www-archive/AdvancedSignalProcessing/WS04-DSPPrinciples/TertinekPaper.pdf` | **F9** — SNR depends on signal **energy**, not shape | **LIVE (secondary)** — content confirmed via search body |
| 11 | MathWorks Phased Array Toolbox, *Detection of Unknown Signals* | **F9** — energy detector as baseline when signal unknown; poor at low FAR | **LIVE (secondary)** — content confirmed via search body |
| 12 | Zhou Y et al. *A RobustICA Based Algorithm for Blind Separation of Convolutive Mixtures.* arXiv:1408.0193 | **F6** — convolutive mixing model; FD-ICA | **LIVE (secondary)** — arXiv listing + abstract read |
| 13 | Mazur R, Mertins A. *A sparsity-based criterion for solving the permutation ambiguity in convolutive BSS* (ICASSP 2011) — `isip.uni-luebeck.de/.../icassp2011-mazur.pdf` | **F6** — permutation + scaling ambiguity are intrinsic to FD-ICA | **LIVE (secondary)** — content confirmed via search body |
| 14 | *Convolutive Audio Source Separation using Robust ICA and an evolving permutation ambiguity solution.* arXiv:1708.03989 | **F6** — reverberant = multiple delays/amplitudes per path | **LIVE (secondary)** — abstract read |
| 15 | Hyvärinen A, Oja E. *Independent Component Analysis: Algorithms and Applications.* Neural Networks 2000;13(4–5):411–430 | **F6** — #sensors ≥ #sources; permutation/scaling indeterminacy | **UNVERIFIED-IN-SESSION** — canonical reference |
| 16 | Zhu W, Beroza GC. *PhaseNet: a deep-neural-network-based seismic arrival-time picking method.* arXiv:1803.03211 | **F2** — arrival-time picking as the limiting step | **LIVE (secondary)** — arXiv listing read |
| 17 | VMD + STA/LTA microseismic first-arrival study (*Applied Sciences*, via DOAJ `ba6898bc…`) | **F2** — measured picking error **<0.023 s at low SNR**; STA/LTA degrades at low SNR | **LIVE (secondary)** — numbers quoted in search body |
| 18 | MDPI *Sensors* two-stage STA/LTA + U-Net picking framework — `mdpi.com/1424-8220/26/5/1693` | **Stage 2** — STA/LTA as cheap first-stage trigger | **LIVE (secondary)** — surfaced in search body |
| 19 | Microseismic event-location accuracy modelling (US 9,945,970) + US 2009/0092005 A1 | **F7** — surface/P-only arrays have **poor depth, good horizontal** accuracy; error regions grow with source–array distance | **LIVE (secondary)** — content confirmed in search body |
| 20 | GDOP / dilution-of-precision reference | **F7** — geometry→precision error propagation | **LIVE (secondary)** — definition confirmed in search body |
| 21 | Base-rate fallacy / PPV references (metricgate.com base-rate-fallacy; omnicalculator false-positive paradox) | **F3** — PPV governed by prevalence; "99 % accurate on 99 % negatives is useless" | **LIVE (secondary)** — content confirmed in search body |
| 22 | Hochreiter S, Schmidhuber J. *Long Short-Term Memory.* Neural Computation 1997;9(8):1735–1780 | **F9** — LSTM gate structure → 4·(n·m + n² + n) param count | **UNVERIFIED-IN-SESSION** — canonical |
| 23 | ARM CMSIS-DSP / Cortex-M4 DSP throughput documentation | **F9** — ~1 MAC/cycle optimistic ceiling on M4 | **UNVERIFIED-IN-SESSION** — vendor docs; M4 is single-issue with single-cycle MAC |
| 24 | STMicroelectronics STM32WLE5 datasheet (64 KiB SRAM, Cortex-M4 @ 48–80 MHz) | **F9** — RAM budget vs 1.5 MiB requirement | **UNVERIFIED-IN-SESSION** — part already selected in `MASTER.md` §9 |
| 25 | Task Force of ESC/NASPE. *Heart rate variability: standards of measurement, physiological interpretation, and clinical use.* Circulation 1996;93:1043–1065 | **F4, F5** — HRV magnitudes, RSA, Mayer waves | **UNVERIFIED-IN-SESSION** — canonical HRV standard; **rate-limited before fetch** |
| 26 | `MASTER.md` §10.5's own cited brackets (PigV² 100–200 m/s; USGS SIR 2023-5061, 200–1000 m/s dry) | **F2, F6** — velocity bracket used in all position-error conversions | **In-repo** — inherited from the project's own prior pass, not re-verified here |

**Sources I failed to obtain and which matter:** the two validation claims in reference §9 Q6
(CERN 2018 concrete cardiac monitoring; ARL 2020 MEMS survivor detection through 2–3 m rubble).
Search was rate-limited before I could run them down. **These are the highest-value outstanding
citations in the project** (F11d) and should be the first thing retrieved next session — the ARL
work, if real, would directly answer F1's open question about the received spectrum.

---

## WHERE I COULD BE WRONG

Audited twice; this is the honest list, strongest objection first.

1. **F1's biggest vulnerability — rubble may be a lowpass.** My harmonic analysis is of the
   **emitted** pulse. Propagation through lossy, scattering debris attenuates high frequencies
   preferentially, so the **received** pulse is wider and the received band narrower. If nothing
   above ~5 Hz survives 2–3 m of rubble, the spec's band is accidentally right and F1 collapses to
   "right answer, wrong reasoning". **I cannot settle this without Stage 0.** What survives
   regardless: (a) the spec's *reasoning* is wrong either way — the band was chosen from a
   repetition rate, not from a measurement; (b) **if** the lowpass hypothesis is true, then B is
   genuinely small and **F2 kills localization outright**. The spec needs one of these to be
   false and cannot choose which.

2. **My pulse model is a guess.** I used a 100 ms Hann pulse because the task posited ~100 ms rise
   time. The real coupled waveform could be a damped oscillation (which would concentrate energy
   near its ringing frequency, not spread it) or substantially longer. At 200 ms the in-band
   fraction rises to 86 % and F1 weakens considerably. **I showed the 200 ms row precisely so the
   sensitivity is visible.** Note it still does not rescue the spec at high heart rates, where the
   harmonic-count problem (2 harmonics at 100–120 bpm) is independent of pulse width.

3. **The CRLB is a bound, not a prediction, and my constant is approximate.** Real estimators do
   worse than the CRLB; but the bound also assumes Gaussian noise and a known waveform, and below
   a threshold SNR the correlator suffers **cycle-ambiguity breakdown** where error jumps far
   *above* the bound. So the true error is likely worse than my table, not better — F2 is
   conservative. The two CRLB formulations I ran differ by ~1.7×; immaterial against 3,900×.

4. **F3's prior is mine.** A targeted deployment onto a suspected void has a much higher prior and
   PPV ~87 %. I computed and reported that case. The finding is not "the system cannot work" — it
   is "accuracy is the wrong spec and there is no false-alarm requirement". If the authors supply a
   concept of operations with a defensible prior, the numbers change; the **requirement to state
   one** does not.

5. **The 3-node concurrence vote may be stronger than I allow.** I argued common-mode noise
   defeats it. If per-node noise is substantially independent (different coupling, different
   contact, different local scatterers) the vote could deliver much of its nominal 30 false
   pins/day. **This is empirically testable at Stage 0 by recording two nodes simultaneously and
   measuring their noise cross-correlation** — a cheap experiment I would add. I may be too
   pessimistic here.

6. **F9 may be unfair to the LSTM.** If the true discriminator is a subtle multi-scale temporal
   pattern (HRV + RSA + envelope jointly), a learned model could genuinely beat my feature list.
   My claim is narrower than "never use an LSTM": it is that **you cannot know that before you
   have real data, the classical baseline must exist first, and the spec's particular 30k-param
   architecture is unjustified and memory-infeasible as literally written.**

7. **The `return_sequences` memory figure assumes a naive implementation.** A streaming
   implementation needs ~2 KiB. I flagged this in-line rather than claiming the 24× overrun as
   certain. The real criticism is that **§6 does not specify which**, and the gap between them is
   the gap between shipping and not.

8. **GDOP numbers depend on my assumed geometry.** I used a 3×3 square grid with the source near
   the centre. Real deployments are irregular, which sometimes *helps*. The 3–4× VDOP/HDOP ratio
   is robust across the spacings and depths I tested and matches the independent microseismic
   result, so I am confident in the direction if not the exact factor.

9. **Source-count for ICA is my estimate.** A quiet site at night with machinery stopped could
   have fewer sources than nodes, making ICA formally admissible. The **convolutive** objection
   (F6b) is the one that does not depend on counting, and it stands independently.

10. **I did not attack everything.** I did not analyse the ADXL355's own noise floor against the
    0.1–1 mg target (25 µg/√Hz over 24 Hz ≈ 122 µg RMS ⟹ ~0.12 mg — **marginal against a 0.1 mg
    target, and wideband makes it worse than the narrow band does**, which is a genuine cost of my
    recommendation and deserves its own pass), the 100 Hz anti-alias chain, or quantisation.
    **The sensor-noise-vs-bandwidth tradeoff is the strongest counter-argument to Stage 1 and I
    am flagging it against myself.** Widening the band raises the noise floor as √B: going 3.5 →
    24.5 Hz costs **√7 = 2.65× ≈ 8.5 dB** of noise. F2's timing gain is 18.5×, so the net is still
    strongly positive **for timing** (18.5/2.65 ≈ 7× net) — but **for detection** the matched
    filter only wins if the added band actually contains signal energy, which is exactly what
    Stage 0 must measure. This is the sharpest statement of why Stage 0 comes first.
