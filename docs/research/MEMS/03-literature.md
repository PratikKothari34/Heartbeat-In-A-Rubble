# 03 — Annotated Literature

Six papers, all downloaded to `papers/` and read (text extracts in `extracts/`).
Ordered by how much they change the project.

---

## 1. VitalMon — heart rate through a bed, with a 10 Hz geophone ⭐ decisive

**Jia, Bonde, Li, Xu, Wang, Zhang, Howard, Zhang.** "Monitoring a Person's Heart Rate and
Respiratory Rate on a Shared Bed Using Geophones." *ACM SenSys '17*, Delft, 6–8 Nov 2017.
DOI [10.1145/3131672.3131679](https://doi.org/10.1145/3131672.3131679)
`papers/SenSys2017_geophone_heartrate_shared_bed.pdf`

Rutgers / CMU / Peking. Geophones under a bed sense **ballistic force** from the heartbeat.
Handles the hard case: **two people on one mattress**, free to move and change position.

**Why it matters here:**

> "The geophone we use, SM-24 Geophone Elements, is naturally a second-order high-pass filter
> and its natural frequency is **10 Hz**."

They measure heart rate to **1.90 BPM mean / 0.72 BPM median error** with a sensor that is
effectively deaf below 10 Hz. This is direct evidence that the detectable heartbeat signature lives
**above** 10 Hz, and that the 1–2 Hz rate is recovered from the *envelope*, not the raw band.

**Applies to this project:** ballistocardiographic coupling into a structure; the sensing principle
is identical, only the medium differs (mattress → rubble).
**Does not apply:** a mattress is a benign, low-loss, short-path, low-noise medium. Their SNR is
not ours.

---

## 2. PigV² — vital signs through a floor, and the propagation model ⭐ decisive

**Dong, Codling, Rohrer, Miles, Sharma, Brown-Brandl, Zhang, Noh.** "PigV²: Monitoring Pig Vital
Signs through Ground Vibrations Induced by Heartbeat and Respiration." 2022.
arXiv [2212.03378](https://arxiv.org/abs/2212.03378)
`papers/PigV2_pig_vital_signs_ground_vibration.pdf`

Stanford / Michigan / USDA-ARS / Nebraska. Geophone array under a pig pen floor, estimating heart
and respiratory rate of a live animal through the structure. **The closest published analogue to
this project**: a living body, an uncontrolled medium, a distributed sensor array, no contact with
the subject.

**Three findings this project must absorb:**

1. **Detection band.**
   > "The heartbeats are detected through peak picking over the sum of wavelet coefficients from
   > **10 to 100 Hz**... The range is chosen based on the typical heartbeat-induced vibration
   > frequency range (0-100 Hz) and the sensitivity range of the sensors (≥10 Hz)."

2. **Attenuation is frequency-dependent:** `S_loc2 = S_loc1 · e^(−α·f·d)`.
   Higher frequencies die faster with distance — the one real argument against a 10–100 Hz band,
   and it trades directly against the 1/f problem in `01-requirements.md` §2.

3. **Wave velocity 100–200 m/s** through the pen floor — against MASTER §7.1's 3000 m/s.
   See `01-requirements.md` §6.

**Method worth copying:** wavelet decomposition → sum coefficients in-band → peak-pick → rate.
Not FFT on a bandpassed signal.

---

## 3. Sercel QuietSeis — what MEMS noise specs actually mean ⭐ decisive

**Sercel / EGU General Assembly 2018.** "QuietSeis: ultra-low-noise MEMS for seismology."
`papers/EGU2018_QuietSeis_ultralow_noise_MEMS_seismology.pdf`
Supporting: `datasheets/Sercel_understanding_MEMS_digital_seismic_sensors.pdf`,
`datasheets/Sercel_MEMS_3C_accelerometers_land_seismic.pdf`

A manufacturer being unusually candid about the limits of their own technology.

> "MEMS accelerometers often perceived as too noisy at low frequency **because of 1/f noise** —
> True for most of the seismic MEMS on the market"

> "**<15 ng/sqrt(Hz) above 10Hz**" · "**1/f noise at low frequency not characterized**"

> "Noise limited by **ambient vibrations above ~2Hz**"

> "MEMS 1/f noise lower than: 10Hz-geophone noise below ~2Hz, 5Hz-geophone noise below ~0,1Hz,
> NHNM down to ~0,1Hz"

**Two consequences, both structural:**

- **Every noise-density number in `02-sensor-survey.md` is a white-region figure valid ≥10 Hz.**
  None of them describes behaviour at 1–2 Hz, where MASTER §6 currently operates.
- **Above ~2 Hz you are ambient-limited, not sensor-limited** — and that was measured in a
  soundproof chamber on an isolation platform. On rubble it is not close. This is the basis for
  `01-requirements.md` §3, which changes the sensor-selection rule from "lowest noise" to
  "cheap enough to deploy many."

The last quote also gives the honest crossover: MEMS beats a 10 Hz geophone **below ~2 Hz**, and
loses above it. Since the signal is above it, that favours the geophone — on noise alone.

---

## 4. Evans et al. — how low-cost accelerometers actually perform

**J. R. Evans, R. M. Allen, A. I. Chung, E. S. Cochran, R. Guy, M. Hellweg, J. F. Lawrence.**
"Performance of Several Low-Cost Accelerometers." *Seismological Research Letters*, 2014.
`papers/Evans2014_performance_low_cost_accelerometers_SRL.pdf`

Independent shake-table and box-flip testing of five triaxial low-cost sensors, by USGS/Berkeley/
Caltech people. The paper that defines the cost/performance tiers everyone else cites:

| Class | Sensor cost | Character |
|---|---|---|
| **A** | ~US$2,000–4,000 | Research-grade (e.g. force-balance EpiSensor) |
| **B** | ~US$500–1,000 | |
| **C** | ~US$100–200 | "the lowest performance level potentially usable by ANSS"; ~12–16 bit useful resolution, typically over ±2 g |

**Applies to this project:** it is the reality check on "cheap MEMS is fine." Class C is the floor
for a *seismic network*, and the ADXL355 at $63 sits below even that. It also documents the failure
modes that matter in the field — self-noise, clip level, and **cross-axis and tilt errors**, which
for a node dropped at random orientation is the relevant one.

**Caveat:** written for earthquake ground motion (strong motion, low frequency), not for
near-field biological micro-vibration. The tier costs are 2014 dollars.

---

## 5. Nof et al. — arrays of cheap MEMS beating one good sensor

**Ran N. Nof, Angela I. Chung, Horst Rademacher, Lori Dengler, Richard M. Allen.**
"MEMS Accelerometer Mini-Array (MAMA): A Low-Cost Implementation for Earthquake Early Warning
Enhancement." *Earthquake Spectra* **35**(1):21–38, Feb 2019.
DOI [10.1193/021218EQS036M](https://doi.org/10.1193/021218EQS036M)
`papers/Nof2019_MEMS_accelerometer_mini_array_MAMA.pdf`

Berkeley Seismology Lab + Geological Survey of Israel + Humboldt State. Two mini-arrays of low-cost
MEMS accelerometers, with a **<US$150 data acquisition unit**, solving **back-azimuth** for seven
events from **Mw 2.7 to 5.1 at 5–106 km**.

**Why it matters here — this is the architectural precedent.** It is the published demonstration
that *N cheap MEMS in a geometry* recovers directional information that a single better sensor
cannot, and it targets the same problem this project has: sparse coverage, poor location estimates.
It is the evidence behind `01-requirements.md` §3.3 — **spend on node count, not per-node noise.**

It also validates the array-processing half of the signal chain (MASTER §7 TDoA) with real field
data rather than simulation.

---

## 6. McNamara & Boaz — the tool for measuring site ambient

**D. E. McNamara and R. I. Boaz.** "Seismic Noise Analysis System Using Power Spectral Density
Probability Density Functions: A Stand-Alone Software Package." *USGS Open-File Report 2005-1438*.
`papers/USGS_OFR2005-1438_seismic_noise_PSD.pdf`

The PQLX methodology: compute PSDs over long records, bin them into **probability density
functions**, and read off the station's noise character against the Peterson **NLNM/NHNM** models
rather than a single averaged number.

**Why it is in this folder:** `01-requirements.md` §8.1 says the blocking measurement is *site
ambient PSD in 10–100 Hz on real rubble*. This report is the established method for making exactly
that measurement defensible — a PSD-PDF, not one spectrum. Use it when the Raspberry Shake
(`02-sensor-survey.md` R1) goes out.

**Caveat:** designed for permanent broadband stations over days-to-months. A rubble deployment
lasts hours. The PDF approach still applies; the statistics will be thinner.

---

## Coverage gaps

Searched for, not found in a form worth keeping:

- **Heartbeat detection through rubble/debris specifically.** Nothing published. The literature
  covers beds, floors, and chairs — benign media with short paths. **The rubble case is unproven,
  and that is this project's actual research contribution.**
- **MEMS 1/f noise characterisation below 10 Hz.** Sercel says it is not characterised; nobody
  else publishes it either. Confirmed as an industry-wide gap, not a search failure.
- **Two candidate papers were blocked** (MDPI *Sensors* 2025 MEMS shake-table comparison;
  an optomechanical 2.5 ng/√Hz geophone). PDF endpoints returned 403/stub files; the stubs were
  deleted rather than kept as fake sources. The MDPI paper's ADXL355 figure was read via the
  PMC HTML page and is recorded as a discrepancy in `05-verification-log.md`.

---

*Back to [README](README.md) · Prev: [02 — Sensor Survey](02-sensor-survey.md) · Next: [04 — Action Report](04-action-report.md)*
