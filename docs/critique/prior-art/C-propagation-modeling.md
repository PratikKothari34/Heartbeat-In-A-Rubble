# C — Propagation & Modeling: Parameter Validation Against Published Measurement

**Date:** 2026-10-07 · **Task:** validate the feasibility-bound parameter chain against measured
literature for a faculty-signed funding proposal (India). **Not** a critique of the study.

**Access-state convention, used on every item:**
**READ-FULL** = primary document retrieved and text extracted here ·
**READ-ABSTRACT** = abstract or indexed extract read, full text not retrieved ·
**CITED-ONLY** = exists and is cited by a source I read, but I did not read it myself.

Nothing in this file is a number I did not see. Where I computed something, it is labelled
**[COMPUTED HERE]** with the inputs shown.

---

## Bottom line for the proposal

- **Force-ratio scaling is defensible and is standard practice** — but it must be renamed. The
  defensible version is a **linear transfer-mobility / force-density argument** (the US FTA's own
  ground-borne vibration method, and the ASTM impulse-response method for concrete, both scale
  response linearly per unit input force). Elastodynamics is linear for small strain, so response
  amplitude scales with **source force**, not source energy. State it that way, cite the mobility
  literature, and add the one genuine caveat: linearity holds for the *propagation path*, but the
  **source-coupling efficiency** (contact area, impedance, contact duration) is not shared between a
  shoe and a torso. That caveat is worth a few dB, not tens — it does not re-derive the bound.
- **A human-seismic feasibility bound already exists and must be cited: Arosio et al. 2010, *Near
  Surface Geophysics*, DOI 10.3997/1873-0604.2010051** — a microseismic survivor-location system
  tested on real rubble piles of concrete beams. It is the proposal's closest prior art and its best
  friend: **it measured 200–600 m/s in rubble**, bracketing our 300 m/s. For a proposal this is a
  cited foundation, not a threat, and failing to cite it would be the bigger problem.
- **Two parameters are wrong and one is not a vendor number.** (i) The SM-24 datasheet contains **no
  noise specification whatsoever** — verified by extracting the primary PDF and finding zero
  occurrences of "nois"; the 0.1 µg/√Hz figure cannot be attributed to the manufacturer. My own
  thermal-noise computation says the *element* is ~0.001–0.005 µg/√Hz, i.e. our figure is
  **conservative by 20–100×, not optimistic** — so the tap margin is safe, but for the opposite
  reason than assumed. (ii) The coupling-resonance window **500 Hz – 67 kHz is contradicted**:
  measured geophone coupling resonances are **100–500 Hz**. The conclusion (resonance above band,
  transmissibility → 1) survives for a 60–80 Hz tap band, but with far less margin than claimed.

---

## Is force-ratio scaling defensible? (KEY METHODOLOGICAL SECTION)

**Verdict: YES as physics, but the proposal is using the wrong vocabulary for it, and should adopt
the established name and citations.**

### Why it is defensible

The governing fact is linearity. Seismology's standard statement, from source theory:

> "Over the time scales of seismic wave propagation the Earth is a linear invariant system; the
> Green's function (impulse response) is the motion induced by an impulse force, and the motion
> produced by an arbitrary force can be obtained from the Green's function by convolution."
> — Madariaga, *Seismic Source Theory*, Treatise on Geophysics 4.02 (READ-ABSTRACT)

If the medium is linear and time-invariant, then for the *same source position, same contact
geometry, same receiver, same frequency*, doubling the applied force doubles the particle velocity.
That is exactly what force-ratio scaling asserts. It is not an approximation in the propagation
term; it is the definition of a linear system.

### The literature does this, under a different name

Two independent engineering communities scale near-field sources by linear force ratio as routine
practice:

1. **Ground-borne vibration prediction (FTA / railway).** The standard method factorises the
   prediction into **force density** (the source, per unit length or per unit force) and **transfer
   mobility** (the path, in velocity per unit force). Response is obtained by multiplying them.
   Explicitly: *"Force density is defined as the difference between the vibration velocity level at
   one or more receivers in the free field and the line source transfer mobility measured at the same
   receiver(s)"* — i.e. the path is characterised **per unit force** and the source is swapped in
   and out linearly. Assumptions are stated as *"decoupling of source and receiver, assuming linear
   elastic constitutive behaviour of the track and the soil."* (READ-ABSTRACT; see citation table.)
   **This is force-ratio scaling, institutionalised in a transport-agency guideline.**

2. **Impulse-response / mobility testing of concrete slabs.** *"The impact force is measured by a
   load cell, and the velocity is measured by the geophone… The ratio of the measured velocity
   response to the impact force in the frequency domain is called the mobility spectrum."* — FHWA
   Impulse Response method / NIST impact-echo overview (READ-ABSTRACT). Mobility is **velocity per
   newton**. Dividing out the force is the method. **This is force-ratio scaling applied to
   concrete, which is our medium.**

So the answer to "does the literature scale near-field sources this way?" is: **yes, and it is the
dominant method in both the soil-vibration and the concrete-NDT communities.**

### What the alternatives would say, and why they do not apply

- **Energy scaling.** Wrong for this use. Energy goes as amplitude *squared*, so scaling by an
  energy ratio when you mean a force ratio costs a factor-of-two error in dB (a 20 dB force deficit
  becomes a 10 dB energy deficit, or vice versa, depending which way it is misapplied). Seismic
  energy is indeed proportional to the square of particle velocity — which is *why* amplitude, not
  energy, is the linear-in-force quantity. The project's chain works in amplitude throughout and is
  therefore self-consistent. **Do not switch to energy.**
- **Seismic moment.** Not applicable. Moment is defined for *internal* sources — a dipole or a
  double couple — and *"the seismic moment of a linear dipole source equals the force multiplied by
  the separation distance"* (GFZ *Seismic Sources and Source Parameters*, READ-ABSTRACT). A footstep
  and a tap are **single forces applied at a free surface**, not internal moment tensors. The correct
  representation is a **point force on a half-space**, whose Green's function is linear in that
  force. Moment would be the right frame only if the cardiac source were modelled as an internal
  source inside the body — which is arguably true, and is the one place a moment framing is defensible
  (see caveat 2 below).
- **Contact area / impedance matching.** This is **not** an alternative to force scaling — it is the
  correction term that sits *on top* of it, and it is where the real uncertainty lives. See below.

### The two caveats that are genuine, and must be stated in the proposal

1. **Linearity is a property of the path, not of the coupling.** The force-ratio argument validly
   transfers the *propagation* from footstep to tap or cardiac. It does **not** establish that the
   same fraction of source force enters the ground. A shoe is a stiff, high-impedance, large-area,
   normal-incidence contact; a torso is soft, low-impedance, and air-gapped. The project's own
   `01-physics-kill-attempt.md` §2.5 already quantifies one tissue-air interface at **−29.6 dB** —
   and that term is *additional to*, not instead of, the force ratio. **For cardiac the coupling
   correction makes the bound worse, so the force-ratio bound is conservative (an upper bound on
   signal) — which is exactly what a feasibility bound should be.** State this explicitly; it is a
   methodological strength, not a weakness.
2. **For a tap, coupling is favourable and the force-ratio step is close to exact** (hand or boot on
   concrete is the same rigid-normal-contact class as a shoe on ground), so the **+23 to +41 dB tap
   margin rests on the strongest version of the method**. For cardiac the method is a bound, not an
   estimate. This asymmetry is worth one sentence in the proposal because it is precisely why the
   surviving architecture is the tap architecture.
3. **Granular media are nonlinear at high amplitude.** Measured in Quillen et al. 2022 (READ-FULL):
   pulse speed depends on pulse pressure as `v_P ∝ P_pk^(1/6)` until `P_pk ≲ P_0`, at which point
   *"the pulse propagation speed undergoes a transition from a nonlinear and shock-like propagation
   regime… to a linear propagation regime where the propagation speed depends on the ambient or
   confinement pressure."* **Our amplitudes (µg) are deep in the linear regime**, many orders below
   confining pressure, so this nonlinearity does not bite. Worth one line, because a reviewer who
   knows granular physics will ask.

### Recommended wording for the proposal

> We bound the cardiac and tap source amplitudes from a measured footstep anchor by **linear
> transfer-mobility scaling**: for a linear-elastic path, particle velocity at a fixed receiver is
> proportional to the applied source force (FTA force-density / transfer-mobility formalism; ASTM
> impulse-response mobility for concrete). We apply the force ratio to the propagation term only,
> and treat source-coupling efficiency as a separate, strictly non-positive correction for the
> cardiac case, making our cardiac figure an **upper bound** on signal.

That is defensible, citable, and does not require re-deriving the bound.

---

## Does a human-seismic feasibility bound already exist? (cite it)

**Yes — three things exist, and all three must be cited. None is fatal to a proposal; two are
actively helpful.**

### 1. The closest prior art — a fielded microseismic survivor-location system

**Arosio, D., Longoni, L., Papini, M., Scaioni, M., Zanzi, L., Alba, M. (2010). "A microseismic
approach to locate survivors trapped under rubble." *Near Surface Geophysics*, 8(6), 623–633. DOI:
10.3997/1873-0604.2010051.** — **READ-ABSTRACT** (Wiley full text 403-blocked; substantive content
from the indexed abstract and the publisher record)

What it did and why it matters to us:

- Built *"a system capable of semi-automatic detection and location of microseismic emissions
  generated by survivors trapped under debris"* — i.e. **this is a human-seismic detection and
  localisation system, and it is 16 years old.**
- **Measured elastic-wave velocity in actual rubble**: *"a hammer directly connected to the
  recording unit was used to generate triggered records that were analyzed to calculate the velocity
  range of elastic signals within the rubble, with velocity values generally falling between
  200–600 m/s."*
- Test medium was real: *"a linear spread was deployed in five positions both on grassy areas and on
  rubble piles consisting of concrete beams."*
- Method: traveltime (TDoA) vs energy analysis, concluding **traveltime is more reliable** — which
  independently validates the project's TDoA choice over amplitude-based localisation.
- Claimed result: localisation *"within the limit of seismic resolution (accuracy ≤2 m)"* and a
  *"factor of three"* reduction in investigation time vs incumbent seismic SAR systems.

**Implication for the proposal.** This is the paper the proposal's contribution must be positioned
*against*, and it is good news on three counts: it validates the velocity parameter, it validates
TDoA over energy, and its own stated limitations — *"the inhomogeneity of the debris pile, the need
of a real-time response, and the limited extension of the sensor array"* — are **exactly** what a
drone-deployed mesh addresses. The honest novelty claim becomes: *Arosio et al. established the
microseismic survivor-location principle with a hand-placed array of limited extent; we address the
array-extent and deployment-time limitations they identify, by drone-deploying the array.*

### 2. The follow-on from the same group — still active

**Villacci, V., Hojat, A., Zanzi, L. "Developing and Testing a Software for Search and Rescue in
Rubble Piles Based on Microseismic Signals." EAGE, DOI 10.3997/2214-4609.202177069** —
**READ-ABSTRACT** (EarthDoc 403-blocked). States the operational problem precisely: *"Passive
microseismics is used in Search and Rescue operations to localize people under piles of rubble. An
operator can evaluate the approximate position of the survivor using an array of geophones by an
iterative move-and-listen procedure which is time-consuming."* **The "move-and-listen is
time-consuming" framing is the proposal's motivation, stated by the incumbent researchers
themselves.** Cite it for that.

### 3. The footstep detection-range bound — the direct methodological ancestor

**Sabatier, J.M., Ekimov, A.E. (2008). "Range limitation for seismic footstep detection." Proc. SPIE
6963, *Unattended Ground, Sea, and Air Sensor Technologies and Applications X*, 69630V (16 Apr
2008). DOI: 10.1117/12.785235.** — **READ-ABSTRACT** (SPIE Digital Library returned empty
body/botwall)

This **is** a noise-floor-limited detection-range bound for human activity, and it is the source of
our anchor. From the indexed content:

- *"The peak magnitudes of seismic vibrations from human footsteps did not exceed 3 × 10⁻⁶ m/s, even
  very close (3 meters) to the walker."* — **this is our anchor, verbatim, and it is confirmed.**
- *"The typical background RMS vibration noise corresponds to 8 × 10⁻⁶ m/s or 50 dB re: 10⁻⁶
  inches/sec."*
- The bound's logic: *"The maximum distance at which sound waves can be detected is determined by
  the amplitude at which the sound signal level equals the background sound noise level"* — a
  signal-equals-noise range equation, i.e. structurally the same bound the proposal is building.
- Its conclusion is a **negative feasibility result**: footstep amplitude *"is less than the typical
  level of the background vibration noise floor and indicates a possible inability to apply the
  seismic method for footstep detection in urban areas."*

**Implication.** The proposal is not inventing the noise-floor-limited human-seismic range bound —
Sabatier & Ekimov published it for footsteps in 2008. The proposal's extension is (a) applying it to
*cardiac and tap* sources rather than footsteps, (b) applying it in *rubble* rather than soil, and
(c) using it as a **design-space bound for a sensor mesh** rather than a single-sensor range figure.
That is a real and defensible increment, but it must be framed as an increment.

**Also worth citing for completeness:** "Evaluation of a Sensor System for Detecting Humans Trapped
under Rubble: A Pilot Study" (PMC5877370) — surfaced in search, **NOT ACCESSED** (PMC URL 404'd on
both the legacy and current host). Listed under hand-retrieval.

---

## Parameter validation table

| # | Our value | Literature value | Full citation | Access | Verdict |
|---|---|---|---|---|---|
| 1 | Footstep anchor: **3 µm/s at 3 m** | *"did not exceed 3 × 10⁻⁶ m/s, even very close (3 metres) to the walker"* | Sabatier & Ekimov, Proc. SPIE 6963, 69630V (2008), DOI 10.1117/12.785235 | READ-ABSTRACT | **SUPPORTED** — exact match. Note it is an *upper bound* ("did not exceed"), used correctly as such. |
| 2 | Anchor frequency **19 Hz** | *"maxima of the ground vibration responses for the Z component of acceleration to footsteps are in the frequency band **near 17 Hz** for all walking styles"*; separately *"most of the energy is in the band from 10 to 100 Hz"* | Ekimov & Sabatier, "Vibration and sound signatures of human footsteps in buildings," *JASA* 120(2):762 (2006); + "Broad frequency acoustic response of ground/floor to human footsteps," Proc. SPIE 6241 (2006), DOI 10.1117/12.663978 | READ-ABSTRACT | **SUPPORTED, minor correction.** Measured peak is **17 Hz**, not 19. Using 19 Hz *overstates* a = 2πfv by 12 % (+0.9 dB). Recommend restating the anchor at 17 Hz: a = 2π·17·3e-6 = **32.0 µg**, not 36.5 µg. Direction: makes the bound slightly more conservative. |
| 3 | **a = 2πf·v** (36.5 µg) | Standard harmonic relation; independent cross-check from the same authors: regular walking **−85.7 dB re 1 g @ 17 Hz at 1 m** ⇒ 5.2e-5 g = **52 µg at 1 m** | Ekimov & Sabatier, *JASA* 120(2):762 (2006); dB reference confirmed as *"Magnitude dB re 1g"* in the UGS literature (ADA584491) | READ-ABSTRACT | **SUPPORTED.** [COMPUTED HERE] 52 µg at 1 m, geometrically spread as 1/r to 3 m, gives **17 µg** — same order as our 32–36.5 µg, within the spread of walking style and soil. Two independent routes from the same measurement family agree to a factor of ~2. |
| 4 | Cardiac impulse **1–4 N** | BCG is measured in newtons on force plates with *"a precision of 0.1 N"*; J-peak amplitude reported in N | Inan et al., "Ballistocardiography and Seismocardiography: A Review of Recent Advances," *IEEE JBHI* 19(4):1414 (2015); Wiard et al., "Force plate monitoring of human hemodynamics," *Nonlinear Biomed. Phys.* 2:1 (2008), DOI 10.1186/1753-4631-2-1 | READ-ABSTRACT | **NO SPECIFIC VALUE CONFIRMED.** The N-unit framing and force-plate method are confirmed; I did **not** retrieve a numeric peak-force figure to validate 1–4 N. Flag as the weakest-sourced input in the chain. The project's own independent momentum-conservation route (1 mm/s body recoil) is the better support and does not depend on a literature N value. |
| 5 | Footstep GRF **~700 N** | Not separately verified here; whole-body-weight normal impulse is uncontroversial (70 kg × 9.81 = 687 N static) | — | CITED-ONLY | **SUPPORTED by inspection** (bodyweight), though peak GRF in walking is typically 1.0–1.2× bodyweight, i.e. **690–840 N**. Using 700 N is central and fine. |
| 6 | ADXL355 **25 µg/√Hz** | 25 µg/√Hz stated in the ADI datasheet, held in-project and independently cited in `03-hardware-kill-attempt.md` as PDF-fetched and text-extracted | Analog Devices, ADXL354/ADXL355 datasheet Rev. A, Table 5 | CITED-ONLY (this pass) / READ-FULL in prior project pass | **SUPPORTED.** Caveat already in-project: it is a white-noise-region figure, not valid at 1 Hz. |
| 7 | SM-24 **0.1 µg/√Hz** | **The datasheet contains no noise specification of any kind.** [COMPUTED HERE] from verified datasheet specs: Johnson noise of the 375 Ω coil = **2.46 nV/√Hz** ⇒ velocity noise 8.55e-11 (m/s)/√Hz ⇒ acceleration noise **0.0005 µg/√Hz @10 Hz, 0.0033 µg/√Hz @60 Hz, 0.0044 µg/√Hz @80 Hz**. Suspension thermal noise (m=11 g, f0=10 Hz, ζ=0.6) = **0.0011 µg/√Hz**. | Geospace/I-O Sensor Nederland, *SM-24 Geophone Element* brochure, ©2006 Input/Output Inc., P/N 1004117 | **READ-FULL** (primary PDF fetched from cdn.sparkfun.com and text-extracted locally; regex for "nois" returned **zero matches**) | **CONTRADICTED AS A CITATION, but conservative as a number.** See dedicated section. Our 0.1 µg/√Hz is ~20–100× *worse* than the element's thermal floor. It is not a vendor figure and must not be cited as one; it is, however, a safe stand-in for an element+preamp system floor. |
| 8 | Rubble velocity **~300 m/s** | *"velocity values generally falling between **200–600 m/s**"* — measured by hammer source on rubble piles of concrete beams | Arosio et al. (2010), *Near Surface Geophysics* 8(6):623, DOI 10.3997/1873-0604.2010051 | READ-ABSTRACT | **SUPPORTED — and this is the single best parameter validation in the chain.** 300 m/s sits in the lower-middle of a directly measured rubble range, from the one group that measured rubble specifically. Cite this and stop treating 300 m/s as an assumption. |
| 9 | Geometric spreading **1/r** | Measured in dry granular media: *"The power law forms for pulse peak pressure, velocity and seismic energy depend on distance from impact to a power of **−2.5**"* | Quillen, A.C. et al. (2022), "Propagation and attenuation of pulses driven by low velocity normal impacts in granular media," *Icarus* (arXiv:2201.01225v4) | **READ-FULL** (PDF fetched, pdfminer-extracted) | **CONTRADICTED for loose granular media; NOT APPLICABLE to our medium as stated.** r^−2.5 is far faster decay than 1/r. **But**: that experiment is unconsolidated sand/millet in a 42 L tub at low confining pressure, with measured pulse speed **55 m/s** — an order below Arosio's 200–600 m/s rubble. Our medium (concrete beams, partially intact slabs) is Arosio's, not Quillen's. **Verdict: treat r^−2.5 as a sensitivity-analysis bound, not the nominal.** See rubble section. |
| 10 | Intrinsic attenuation negligible at 3 m | Granular media at kHz attenuate strongly; at our f and r the project's own Q-based computation (0.9 dB over 3 m at Q=3) stands | Quillen et al. (2022) + project `01` §2.3 | READ-FULL | **SUPPORTED** at our frequency/range. Scattering, not intrinsic Q, is the live risk. |
| 11 | σ_t ~ **1/(B·√SNR)** | CRLB `var(τ̂−τ) ≥ N₀/(2ζ²E_s)` with ζ² the mean-squared bandwidth; *"the higher the SNR or the larger the signal bandwidth, the lower the CRB"* | See Cramér-Rao section | READ-ABSTRACT | **SUPPORTED in form.** The 1/(B√SNR) scaling is the correct functional dependence of the CRLB. Exact constants depend on pulse shape via ζ². |
| 12 | Coupling stiffness **k = 4Ga/(1−ν)** | Standard rigid-disc-on-elastic-half-space vertical static stiffness; the specific expression was not retrieved in this pass's searches | Foundation-dynamics texts (e.g. Richart, Hall & Woods; Gazetas) | CITED-ONLY | **NO DATA FOUND this pass** for the exact closed form. The formula is standard and I have no reason to doubt it, but I did not verify it against a source I read. Flag for hand-retrieval. |
| 13 | Coupling resonance **500 Hz – 67 kHz** | *"coupling resonant frequencies range from **100 to 500 Hz** at different locations depending on the firmness of the soil"*; *"The coupling resonant frequency can be increased by burial of the geophones or by the use of longer spikes"* | Krohn, C.E. (1984), "Geophone ground coupling," *Geophysics* 49(6):722–731, DOI 10.1190/1.1441700; + Krohn (1985) | READ-ABSTRACT | **CONTRADICTED at the lower bound.** Measured coupling resonances are 100–500 Hz, i.e. our claimed *floor* of 500 Hz is the literature's *ceiling*. The downstream conclusion (resonance ≫ 60–80 Hz tap band, transmissibility → 1) **still holds**, but the margin is ~1.3–6×, not 6–800×. Do not quote 67 kHz in the proposal. |
| 14 | *f₀ ∝ 1/√m* ⇒ **lighter couples better** | *"Adding mass reduces the frequency of resonance"* | Krohn (1984), *Geophysics* 49:722, DOI 10.1190/1.1441700, and the coupling literature citing it | READ-ABSTRACT | **SUPPORTED** — and it is established, not novel. See coupling section for the important qualification. |
| 15 | Tap force **50–300 N** | **No measured knock-on-concrete force found.** Nearest anchors are far above our range and are destructive, not tapping: karate chop *"up to 2,800 newtons"*, *"splitting a typical concrete slab 1½ inches thick takes about 1,900 newtons"* | Popular-science/physics-education sources only | READ-ABSTRACT | **NO DATA FOUND.** 50–300 N is plausible for a knuckle/boot tap by analogy to bodyweight-fraction impulses, but it is **unmeasured and remains an estimate.** Highest-value bench measurement in the whole chain. |
| 16 | Tap frequency **60–80 Hz** | **No measured knocking spectrum on concrete found.** Impulse-response/impact-echo practice puts *useful* slab response in the 0–1 kHz (IR) and ~5–15 kHz (impact-echo) ranges; the force spectrum is set by contact time, *"with a larger contact time reducing bandwidth"* | FHWA Impulse Response (InfoTechnology); Carino, N.J., "The Impact-Echo Method: An Overview," NIST (READ-ABSTRACT) | READ-ABSTRACT | **NO DATA FOUND — and mildly suspect.** A soft-tissue knuckle has a long contact time ⇒ low bandwidth, so 60–80 Hz is not unreasonable; but a boot or a rock on concrete would push far higher, and the slab's own modes, not the contact, may dominate. **Measure it.** |

---

## SM-24 actual manufacturer specification (HIGH VALUE)

**This was the highest-value item in the brief and the finding is clean.**

**Source, READ-FULL:** *SM-24 Geophone Element — Where Quality Data Starts*, SENSOR Nederland b.v.
(an I/O subsidiary), ©2006 Input/Output, Inc., ordering P/N 1004117 (SM-24/U-B 10 Hz 375 Ohm).
Retrieved as PDF from `https://cdn.sparkfun.com/datasheets/Sensors/Accelerometers/SM-24%20Brochure.pdf`
and text-extracted locally with pdfminer under `py -3.12`. This is the same document already held at
`docs/research/MEMS/extracts/Geospace_SM-24_geophone_brochure.md`; **I re-extracted it independently
and the project's extract is faithful.**

### What the datasheet actually says

| Specification | Value |
|---|---|
| Natural frequency | **10 Hz**, tolerance ±2.5 % |
| Max tilt for specified Fn | 10° |
| Typical spurious frequency | **>240 Hz** |
| **Sensitivity** | **28.8 V/m/s** (0.73 V/in/s), tolerance ±2.5 % |
| **Coil resistance** | **375 Ω** standard, ±2.5 % |
| Open-circuit damping | **0.25** typical |
| Damping w/ calibration shunt (1339 Ω) | 0.6 (+5 %, −0 %) |
| Moving mass | **11 g** |
| Max coil excursion p-p | 2 mm |
| Distortion (coil-to-case, 17.78 mm/s p-p @12 Hz) | <0.1 % |
| Total weight | **74 g** |
| Dimensions | 25.4 mm dia × 32 mm high |
| Operating temperature | −40 °C to +100 °C |

### The finding

> **The SM-24 datasheet contains no noise specification of any kind.** A case-insensitive regex for
> `nois\w*` over the full extracted text (3,508 characters) returns **zero matches**. There is no
> noise density, no noise floor, no self-noise, no equivalent input noise.

**Consequence for the proposal: `0.1 µg/√Hz` cannot be attributed to the manufacturer.** It is not
in the datasheet. Any proposal text implying a vendor noise spec for the SM-24 is unsupportable, and
a reviewer who pulls the one-page brochure will find nothing. This must be fixed before submission.

### What the noise floor actually is — [COMPUTED HERE]

A moving-coil geophone's intrinsic floor has two dominant terms, both computable from the verified
specs above:

```
Johnson noise of the coil:   e_n = sqrt(4 k_B T R),  R = 375 Ω, T = 293 K
                             e_n = 2.463e-9 V/√Hz  = 2.46 nV/√Hz
Equivalent velocity noise:   v_n = e_n / S,  S = 28.8 V/(m/s)
                             v_n = 8.553e-11 (m/s)/√Hz
Equivalent acceleration:     a_n = 2πf · v_n
```

| Frequency | Johnson-limited acceleration noise |
|---|---|
| 10 Hz | **0.0005 µg/√Hz** |
| 19 Hz | 0.0010 µg/√Hz |
| 40 Hz | 0.0022 µg/√Hz |
| **60 Hz** (tap band) | **0.0033 µg/√Hz** |
| **80 Hz** (tap band) | **0.0044 µg/√Hz** |
| 100 Hz | 0.0055 µg/√Hz |

Suspension (mechanical-damping) thermal noise, `a_n = sqrt(4 k_B T c)/m` with `c = 2ζmω₀`,
m = 11 g, f₀ = 10 Hz:

| Damping ζ | Acceleration noise |
|---|---|
| 0.25 (open circuit) | 0.0007 µg/√Hz |
| 0.6 (shunt-damped, the normal operating case) | **0.0011 µg/√Hz** |

**So the SM-24 element's own thermal floor across the 60–80 Hz tap band is roughly
0.003–0.005 µg/√Hz — about 20–30× BELOW our assumed 0.1 µg/√Hz.**

### What this does to the tap margin — the answer to the brief's worry

The brief's concern was: *"If optimistic by 10× the tap margin drops to +3 to +21 dB."*

**That concern is resolved in the project's favour.** Our 0.1 µg/√Hz is not optimistic by 10× — it
is **pessimistic** by 20–100× relative to the sensor element. The +23 to +41 dB tap margin is
therefore **not at risk from the sensor element**, and if anything is understated.

**The real caveat is different, and the proposal should state it.** A geophone system's floor is set
by whichever is larger: the element's thermal noise, or the **preamplifier and ADC** behind it. The
element is so quiet that the electronics will dominate — which is exactly what the one published
SM-24 noise figure I found shows: Dean et al. (2018) plot *"noise levels of the combination of an
SM-24 geophone (natural frequency = 10 Hz, sensitivity = 28.8 V/m/s) and a measured, but scaled,
instrument noise level"* against the Peterson (1993) NLNM/NHNM — i.e. the published treatment is
explicitly **geophone + digitiser**, never the geophone alone.

**Recommended proposal wording:** *"We adopt 0.1 µg/√Hz as a conservative system noise-density
figure for an SM-24-class geophone with its preamplifier. The SM-24 datasheet specifies no noise
figure; the element's own thermal floor, computed from its specified 375 Ω coil resistance and
28.8 V/m/s sensitivity, is 0.003–0.005 µg/√Hz across 60–80 Hz, so our figure carries 20–30 dB of
margin for front-end electronics."* That is both honest and stronger than the current text.

**Also note for the BOM**: the datasheet's 74 g total weight and 11 g moving mass are the real
numbers; a 4.5 Hz variant at the same 375 Ω / 28.8 V/m/s exists from third-party suppliers
(seismicgeophone.com, READ-ABSTRACT) — relevant if a lower corner is ever wanted, but that is not an
I/O part and should not be cited as an SM-24 spec.

---

## Rubble propagation: velocity and attenuation

### Velocity — SUPPORTED, from the one group that measured rubble

| Medium | Measured velocity | Source | Access |
|---|---|---|---|
| **Rubble piles of concrete beams** | **200–600 m/s** (hammer source, triggered records) | Arosio et al. (2010), *NSG* 8(6):623, DOI 10.3997/1873-0604.2010051 | READ-ABSTRACT |
| Unconsolidated material (dry) | 200–1000 m/s | project MASTER §10.5 | in-project |
| Dry quartz sand, impact pulse | **53 m/s** (Matsue et al. 2020); **55 m/s** (this study, sand and millet) | Quillen et al. (2022), arXiv:2201.01225 | READ-FULL |
| 200 µm glass beads | **109 m/s** (Yasui et al. 2015) | cited in Quillen et al. (2022) | CITED-ONLY |
| Gently-held granular aggregate (rubble asteroid) | as low as **~20 m/s** | Quillen et al. (2022) | READ-FULL |

**Verdict: 300 m/s is defensible and should be cited to Arosio et al. (2010), not asserted.** It
sits in the lower-middle of a directly measured 200–600 m/s range in the correct medium — collapsed
concrete, not soil and not sand.

**The important distinction to make explicitly in the proposal.** Loose granular media are an order
of magnitude slower (53–110 m/s) than collapsed-concrete rubble (200–600 m/s), because rubble
retains stiff, load-bearing members (beams, slabs, rebar) that carry fast paths. **Our medium is
Arosio's.** If the proposal ever needs a worst case, the honest low end is **200 m/s** (Arosio's own
floor), not 55 m/s — invoking the sand number would be using the wrong medium.

### Attenuation — the genuine open risk, and it is not intrinsic Q

**No dB/m or Q value for collapsed concrete was found.** That is a real gap, and the proposal should
say so rather than paper over it.

What the literature does establish:

- **In loose granular media, decay is measured as r^−2.5** for pulse peak pressure, peak velocity
  and seismic energy (Quillen et al. 2022, READ-FULL — *"The power law forms for pulse peak
  pressure, velocity and seismic energy depend on distance from impact to a power of −2.5 and this
  rapid decay is approximately consistent with our experimental measurements"*). The authors frame
  this as supporting a **"seismic jolt"** model — rapid attenuation — *over* a reverberation model.
- **Propagation is not spherically symmetric**: *"Peak amplitudes are about twice as large for the
  pulse propagating downward than at 45 degrees from vertical."* A factor-of-2 (6 dB) directional
  asymmetry is directly relevant to a mesh that assumes isotropic spreading for TDoA.
- **Arosio et al. identify debris inhomogeneity as their primary obstacle**, which is a scattering
  statement, not an absorption statement.

**Sensitivity analysis the proposal should carry.** Over our 3 m path, relative to 1/r:

| Decay law | Loss 0.1 m → 3 m | Penalty vs 1/r |
|---|---|---|
| r^−1 (our nominal) | −29.5 dB | — |
| r^−1.5 | −44.3 dB | −14.8 dB |
| r^−2.5 (granular, measured) | −73.8 dB | **−44.3 dB** |

[COMPUTED HERE, 20·log₁₀(r_ratio^n), r_ratio = 30.]

**This is the largest single unquantified risk in the propagation model.** It does not change the
cardiac verdict (already −47 to −69 dB; r^−2.5 only makes it deader). But it **could erase the tap
margin**: +23 to +41 dB minus up to 44 dB of excess spreading loss goes negative. The honest
position for the proposal is: *nominal 1/r, justified by rubble's load-bearing stiff members and
Arosio's successful 200–600 m/s traveltime picks at operational ranges; with r^−1.5 to r^−2.5 as a
stated sensitivity case, and a measurement of the actual decay exponent in instrumented rubble as an
explicit work package.* **Making that measurement a deliverable turns the weakest parameter into a
contribution.**

---

## Tap/impact as a seismic source: measured values

**Verdict: NO DATA FOUND for either of the two load-bearing figures. Both remain estimates.**

| Our figure | What I looked for | What I found |
|---|---|---|
| **50–300 N** tap force | measured peak force of a human knock/tap on concrete | Nothing in this range from a measurement source. Only destructive-impact anchors, far above: karate chop *"up to 2,800 newtons"*; *"splitting a typical concrete slab 1½ inches thick takes about 1,900 newtons"*; *"when a karate expert's hand reached a speed of 11 m/s, it exerted a force of 3,000 Newtons on concrete."* All READ-ABSTRACT, popular-science grade. **Not citable in a funding proposal.** |
| **60–80 Hz** tap spectrum | measured spectrum of knocking/tapping on a concrete slab | Nothing directly. The method literature gives the governing principle but no knock spectrum. |

### What the impact/NDT literature does give us, and it is useful

- **The mobility formalism** (directly supports the force-ratio method): *"The impact force is
  measured by a load cell, and the velocity is measured by the geophone… the ratio of the measured
  velocity response to the impact force in the frequency domain is called the mobility spectrum."*
  — FHWA Impulse Response, READ-ABSTRACT.
- **Contact time sets bandwidth**: *"The hammer size, length, material, and impact velocity determine
  the amplitude and frequency content of the force impulse. While a hammer strike cannot achieve an
  infinitely small duration, its contact time directly influences the frequency content of the
  force, with a larger contact time reducing bandwidth."* — modal-testing practice, READ-ABSTRACT.
  **This is the physical argument that makes 60–80 Hz plausible for a soft knuckle** (long contact
  time ⇒ low bandwidth) — and simultaneously the argument that a **boot or rock strike would be much
  broader-band and higher**. The project should not assume one number covers both.
- **Impulse-response (IR) testing of slabs operates in the low-hundreds of Hz**, distinct from
  impact-echo at 5–15 kHz (*"higher peak frequencies (typically near 12–15 kHz) correspond to regions
  of sound concrete… whereas lower frequencies around 5 kHz consistently mark defect-prone areas"* —
  arXiv:2511.21080 / NIST overview, READ-ABSTRACT). **So 60–80 Hz sits below the standard IR band**,
  which is a mild warning: the slab's own modes may dominate over the contact spectrum, and those are
  geometry-dependent.
- **A calibrated, standardised tapping source exists and is worth knowing about**: the building-
  acoustics **tapping machine**, which *"creates 10 impacts per second"* with known force and
  frequency (ISO 10140 / ISO 16283 family, READ-ABSTRACT). If the project needs a *repeatable*
  laboratory tap source for the bench test, this is the standardised instrument, and citing it would
  strengthen the methodology section.

### Recommendation

Treat 50–300 N and 60–80 Hz as **explicitly flagged estimates** in the proposal, and make their
measurement a named early work package — an instrumented-hammer / load-cell measurement of knuckle,
boot and rock taps on a concrete slab, reported as a mobility spectrum. This is cheap, uses standard
equipment, and **it is the measurement that determines whether the surviving architecture closes.**
A proposal that identifies its own weakest parameter and budgets to measure it reads as competent;
one that asserts 60–80 Hz does not.

---

## Coupling: is "lighter couples better" established?

**Verdict: SUPPORTED — the mass dependence is established and not novel. But the project's numeric
resonance window is CONTRADICTED, and the practical claim needs an important qualification.**

### The mass dependence is established

**Krohn, C.E. (1984). "Geophone ground coupling." *Geophysics*, 49(6), 722–731. DOI:
10.1190/1.1441700.** — READ-ABSTRACT (SEG Library; abstract and extensive secondary citation read,
full text not retrieved). This is **the** canonical citation; use it.

- Krohn modelled coupling as a **two-degree-of-freedom system**: the geophone's own
  spring-mass-damper plus a geophone–ground coupling resonance.
- Mass dependence, stated directly in the coupling literature: *"Adding mass reduces the frequency
  of resonance"* — which is `f₀ = (1/2π)√(k/m)`, i.e. **f₀ ∝ 1/√m**, exactly as the project has it.
- Supporting mechanisms: *"The coupling resonant frequency can be increased by burial of the
  geophones or by the use of longer spikes"*, and *"as coupling improves, the coupling-induced
  resonance frequency clearly increases."*
- Contact geometry: *"with the decline of coupling medium's diameter, the resonant frequency of the
  'ground-coupling system' increases"* (geophone–seabed coupling literature citing Krohn,
  READ-ABSTRACT).
- Transmissibility: *"For frequencies much lower than the coupling resonant frequency, the geophone
  accurately follows the ground motion, but for higher frequencies the coupling can alter both the
  amplitude and phase of the seismic signal."* **This is the transmissibility → 1 argument, and it
  is correct.**
- Krohn also found *"the influence of coupling resonance was reduced when the damping was
  increased."*

So the project's framing is right and so is its direction of inference. **It is established prior
art, so cite Krohn rather than presenting "lighter couples better" as a project finding.**

### But the numeric window is CONTRADICTED — state this plainly

> Project value: coupling resonance **500 Hz – 67 kHz**.
> Measured literature: *"coupling resonant frequencies range from **100 to 500 Hz** at different
> locations depending on the firmness of the soil."*

**Our claimed lower bound (500 Hz) is the literature's upper bound.** The 67 kHz figure has no
support in anything I read and should not appear in a funding proposal — it is a factor of ~10²
above any measured coupling resonance.

**Does the conclusion survive?** For the tap band, yes, but with much less margin:

| Coupling f₀ | Ratio to 80 Hz tap | Transmissibility error |
|---|---|---|
| 100 Hz (literature low) | 1.25× | **Severe — in-band, resonant** |
| 500 Hz (literature high) | 6.25× | ~2.6 % — negligible |
| 67 kHz (our claim) | 840× | negligible, but unsupported |

[COMPUTED HERE, |1/(1−(f/f₀)²)| for the undamped single-DOF case.]

**At the literature's low end, a 100 Hz coupling resonance is only 1.25× above an 80 Hz tap — that
is in-band and would distort both amplitude and phase**, which matters for TDoA as well as
detection. The project's conclusion ("far above band, transmissibility → 1") holds for firm contact
but **fails for soft/loose contact**, which is exactly what drone-dropped nodes on debris will often
get.

### The qualification that matters most

Krohn's literature measures **spiked or buried survey geophones in soil**. Our case is a
**free-laid, drone-dropped puck on fractured debris with air gaps** — the regime where coupling is
*worst* and where `k` (ground stiffness at the contact) is smallest and least predictable. Since
`f₀ ∝ √k`, a poor contact lowers f₀ toward and into the band. Note that the project's own
`06-prior-research-audit.md` §6 already found that the prior pass **conflated orientation with
coupling**, and quoted the earlier MEMS pass calling the spike/anchor interface *"unsolved… the
dominant term… this project's actual contribution."*

**So the honest proposal position is:** *lighter is better for coupling resonance (Krohn 1984,
f₀ ∝ 1/√m), and this usefully inverts the intuition that heavier sensors couple better. But measured
coupling resonances are 100–500 Hz, not 500 Hz–67 kHz, and the low end of that range is close enough
to a 60–80 Hz tap band that contact stiffness must be measured, not assumed.* Replace 67 kHz with
the measured range and keep the direction of the argument.

---

## Cramér-Rao / TOA bound: canonical citation

**Verdict: SUPPORTED in functional form.**

### Canonical citations

1. **Van Trees, H.L. (1968). *Detection, Estimation, and Modulation Theory, Part I*. Wiley.** —
   CITED-ONLY. The standard textbook origin of the time-delay CRLB and the mean-squared-bandwidth
   formulation. This is the citation a reviewer expects.
2. **Kay, S.M. (1993). *Fundamentals of Statistical Signal Processing: Estimation Theory*.
   Prentice Hall.** — CITED-ONLY. The standard modern textbook reference for the CRLB generally.
3. **Quazi, A.H. (1981). "An overview on the time delay estimate in active and passive systems for
   target localization." *IEEE Trans. ASSP* 29(3):527–533.** — CITED-ONLY. The canonical
   *application* paper for TDoA localisation.
4. For a retrievable, citable modern statement: **"Cramér-Rao bound for time-delay estimation in the
   frequency domain," Proc. EUSIPCO 2009** — READ-ABSTRACT, open PDF at
   `eurasip.org/Proceedings/Eusipco/Eusipco2009/contents/papers/1569192158.pdf`.
5. **Dardari, D. et al., "Cramér-Rao bounds in the estimation of time of arrival in fading
   channels," *EURASIP J. Adv. Signal Process.* 2018:15, DOI 10.1186/s13634-018-0540-1** —
   READ-ABSTRACT, open access.

### What the bound actually says

The CRLB for time-delay estimation, as read:

```
var(τ̂ − τ)  ≥  N₀ / (2 ζ² E_s)
```

where `N₀` is noise PSD, `ζ²` the **mean-squared bandwidth** of the signal, and `E_s` the signal
energy. Since `E_s/N₀` is the SNR:

```
σ_τ  ≥  1 / (ζ · √(2·SNR))     ⇒     σ_τ  ∝  1/(B·√SNR)
```

Confirmed qualitatively in the sources read: *"The theoretical lower bound is dependent on the SNR
and the waveform characteristics… the higher the SNR or the larger the signal bandwidth, the lower
the CRB"* and *"A larger bandwidth and a higher central frequency result in a larger Fisher
information measure and a lower CRB."*

**Our form `σ_t ~ 1/(B√SNR)` is the correct functional dependence.** The one precision point worth
making in the proposal: the bandwidth in the bound is the **RMS (mean-squared) bandwidth ζ**, which
is a pulse-shape-weighted quantity, **not** the −3 dB filter bandwidth. For a flat spectrum over
bandwidth B, ζ relates to B by an O(1) constant (for a rectangular band, ζ = 2πB/√12 ≈ 1.81B in rad/s).
So using B directly is right to within a small constant — **state it as a scaling law, not an
equality**, and the bound is unimpeachable.

---

## Could not access — exact URLs/DOIs for hand-retrieval

Ordered by value to the proposal. All confirmed to **exist** (indexed, with resolvable DOIs); the
listed failure is the access state I observed, not a judgement on the paper.

| Priority | Item | Exact URL / DOI | Observed failure |
|---|---|---|---|
| **1** | **Arosio, D. et al. (2010), "A microseismic approach to locate survivors trapped under rubble," *Near Surface Geophysics* 8(6):623–633** — the single most important citation in this report (rubble velocity 200–600 m/s; prior-art bound) | DOI **10.3997/1873-0604.2010051** · `https://onlinelibrary.wiley.com/doi/10.3997/1873-0604.2010051` · RG mirror: `researchgate.net/publication/275942059` | Wiley **HTTP 403** |
| **2** | **Sabatier & Ekimov (2008), "Range limitation for seismic footstep detection," Proc. SPIE 6963, 69630V** — our anchor's primary source | DOI **10.1117/12.785235** · `https://www.spiedigitallibrary.org/conference-proceedings-of-spie/6963/69630V/Range-limitation-for-seismic-footstep-detection/10.1117/12.785235.short` · RG mirror: `researchgate.net/publication/252566889` | SPIE returned **empty body** (botwall); WebFetch got no content |
| **3** | **Krohn, C.E. (1984), "Geophone ground coupling," *Geophysics* 49(6):722–731** — the coupling citation; needed to replace the 500 Hz–67 kHz window with measured values | DOI **10.1190/1.1441700** · `https://library.seg.org/doi/10.1190/1.1441700` | SEG paywall (abstract only) |
| **4** | **Ekimov & Sabatier (2006), "Vibration and sound signatures of human footsteps in buildings," *JASA* 120(2):762** — the −85.7 dB re 1 g @17 Hz figure and the 17 Hz peak | `https://pubs.aip.org/asa/jasa/article-abstract/120/2/762/893348` | AIP paywall |
| **5** | **Ekimov & Sabatier (2006), "Broad frequency acoustic response of ground/floor to human footsteps," Proc. SPIE 6241** | DOI **10.1117/12.663978** · `https://www.spiedigitallibrary.org/proceedings/Download?fullDOI=10.1117/12.663978` | SPIE returned **empty body** |
| **6** | **DTIC ADA584491, "Robust Personnel Detection using PIR and Seismic Sensors"** — US Army, likely contains measured footstep amplitudes in dB re 1 g at stated ranges | `https://apps.dtic.mil/sti/tr/pdf/ADA584491.pdf` | **HTTP 403** via WebFetch; curl with browser UA returned **HTTP 200 but an HTML page, not a PDF** — a textbook soft-200. Hand-retrieve in a browser. |
| **7** | **DTIC ADA562080, "Target Detection and Classification Using Seismic and PIR Sensors"** (ARL-TR, the "footsteps reliably detected at ranges up to 30 m" and "7.5 dB / 12.5 dB walking style" figures) | `https://apps.dtic.mil/sti/pdfs/ADA562080.pdf` | **HTTP 403** |
| **8** | **Dean, T., Shem, ?, Al Hasani, ? (2018), "Methods for reducing unwanted noise (and increasing signal) in passive seismic surveys," ASEG Extended Abstracts** — contains **the only published SM-24 noise-level figure I located** (Fig. 4: SM-24 + instrument noise vs Peterson NLNM). **High value for the SM-24 section.** | DOI **10.1071/ASEG2018abW8_2A** · `https://www.earthdoc.org/content/journals/10.1071/ASEG2018abW8_2A` · PDF: `https://www.tandfonline.com/doi/pdf/10.1071/ASEG2018abW8_2A` | Taylor & Francis **HTTP 403** |
| **9** | **Villacci, V., Hojat, A., Zanzi, L., "Developing and Testing a Software for Search and Rescue in Rubble Piles Based on Microseismic Signals," EAGE** | DOI **10.3997/2214-4609.202177069** · `https://www.earthdoc.org/content/papers/10.3997/2214-4609.202177069` | EarthDoc **HTTP 403** |
| **10** | **"Evaluation of a Sensor System for Detecting Humans Trapped under Rubble: A Pilot Study"** (PMC5877370) | `https://pmc.ncbi.nlm.nih.gov/articles/PMC5877370/` (note: the `/pmc/articles/` path **404s**; try `/articles/`) | 301 → **404** on both hosts tried |
| **11** | **Rigid-disc-on-elastic-half-space vertical stiffness `k = 4Ga/(1−ν)`** — needed to close parameter #12 | Standard texts: Richart, Hall & Woods, *Vibrations of Soils and Foundations* (1970); Gazetas, G. (1991), "Formulas and charts for impedances of surface and embedded foundations," *J. Geotech. Eng.* 117(9):1363, DOI 10.1061/(ASCE)0733-9410(1991)117:9(1363) | Not attempted in full; formula not located in any source I read |
| **12** | **A numeric BCG peak force in newtons** — to close parameter #4 (the 1–4 N figure) | Wiard et al. (2008), *Nonlinear Biomed. Phys.* 2:1, DOI 10.1186/1753-4631-2-1 (open access, `nonlinearbiomedphys.biomedcentral.com/articles/10.1186/1753-4631-2-1`); Inan et al. (2015), *IEEE JBHI* 19(4):1414, DOI 10.1109/JBHI.2014.2361732 | Not retrieved; the open-access BMC one is the cheapest win here |

**Environment notes confirmed during this pass**, for whoever hand-retrieves:
DTIC returns **HTTP 200 with an HTML body instead of the PDF** when scripted — the project's
"HTTP 200 does not mean a page exists" rule held exactly. SPIE returns **200 with an empty body**.
Wiley / Taylor & Francis / EarthDoc / AIP return clean **403**s. PMC's legacy `/pmc/articles/` path
301s to a **404**.

---

## What I could be wrong about

Worst first.

1. **Four of my most load-bearing citations are READ-ABSTRACT, not READ-FULL** — Arosio (200–600 m/s),
   Sabatier & Ekimov (the 3 µm/s anchor), Krohn (100–500 Hz coupling), and the Ekimov 17 Hz / −85.7 dB
   figures. The numbers came through indexed abstracts and search extracts, which is one remove from
   the primary document. **Every one of them should be hand-retrieved before the proposal is
   signed.** I have quoted them verbatim and marked them, but a verbatim quote of an abstract is not
   a reading of a methods section — in particular I cannot confirm *how* Arosio's 200–600 m/s was
   measured beyond "hammer source, triggered records," nor at what ranges.
2. **The 100–500 Hz coupling-resonance range is for spiked/buried geophones in soil, and I am
   applying it to a free-laid puck on debris.** That extrapolation could go either way: debris
   contact might be *stiffer* than soil (concrete-on-concrete point contact, high local `k` ⇒ higher
   f₀, helping us) or far softer and intermittent (lower `k` ⇒ lower f₀, hurting us). **I flagged
   the window as CONTRADICTED on the strength of the measured numbers, but I cannot tell you which
   direction our actual case sits.** The contradiction of the *67 kHz* figure is solid regardless;
   the practical risk assessment is not.
3. **The r^−2.5 finding may not transfer to our medium at all, and I may be over-weighting it.**
   Quillen et al. is unconsolidated sand/millet in a 42 L tub, impact-driven, at 55 m/s pulse speed
   — a medium whose velocity is 4–10× below measured rubble. I presented it as a sensitivity bound
   rather than a nominal for exactly this reason, but a reviewer could fairly say it is the wrong
   analogy and should not appear. **I kept it because no measured attenuation exponent for collapsed
   concrete exists, and an unquantified risk is worse than a loosely-bounded one.**
4. **My SM-24 noise computation is an element-only thermal floor and is not a system figure.** I
   computed Johnson noise of the coil and suspension thermal noise from verified datasheet specs.
   I did **not** model preamp voltage/current noise, ADC quantisation, or the geophone's response
   roll-off below 10 Hz (which, for the 60–80 Hz tap band, is irrelevant — but would matter a great
   deal for any lower band). **The claim "0.1 µg/√Hz is conservative" is therefore a claim about the
   sensor element, not about a built system.** The Dean et al. figure (hand-retrieval item 8) is the
   thing that would settle it, and I could not read it.
5. **I did not find the BCG 1–4 N figure, and I did not find any measured tap force or tap
   spectrum.** Three of the chain's inputs are therefore still estimates after this pass. I resisted
   substituting the karate-chop numbers (1,900–3,000 N) as "measured tap forces" because they are
   destructive impacts from popular-science sources and would be a bad citation in a funded proposal.
   **"NO DATA FOUND" here is an honest result, not a failed search** — but a more specialised search
   (ISO tapping-machine force calibration, forensic biomechanics, or the Delsar vendor literature)
   might find them.
6. **I may be too generous to force-ratio scaling.** I concluded it is defensible because
   elastodynamics is linear and because two engineering communities do exactly this. The strongest
   counter-argument I can construct against myself: the FTA/mobility method characterises the path
   **per unit force at a fixed, well-defined contact**, and then swaps *sources of the same
   contact class* (different trains on the same track). Swapping a **shoe for a torso** changes the
   contact class, not just the force magnitude — so the method's validity for the cardiac case rests
   entirely on the coupling-correction term being treated separately and honestly. I believe the
   proposal's use is sound **because it yields an upper bound**, but a reviewer hostile to the method
   would attack precisely there, and "it's linear" is not a complete answer to them.
7. **I found no evidence either way on whether anyone has published a *cardiac* seismic bound
   through rubble.** My search for an existing feasibility bound returned footstep bounds
   (Sabatier & Ekimov) and survivor-localisation systems (Arosio) but nothing cardiac-specific. That
   is consistent with the project's earlier finding that nobody has done this, but **absence of
   evidence from one pass of searching is not evidence of absence**, and the proposal should not
   claim world-first on the strength of it without a dedicated systematic search.
8. **The 17 Hz vs 19 Hz correction is small and I may be over-stating its cleanliness.** The
   "near 17 Hz" figure is for the Z-component ground response in Ekimov & Sabatier's building/ground
   measurements; the 19 Hz the project uses may come from a different measurement in the same family
   with a different soil. Both are within the plausible spread. **I recommended 17 Hz because it is
   the figure I could quote verbatim, not because I proved 19 Hz wrong.**
