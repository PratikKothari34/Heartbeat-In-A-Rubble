# A — Cardiac seismic source amplitude, competing modalities, survival-time evidence

Prior-art sweep for the funding proposal's problem statement. Scope: cardiac/vital-sign **source amplitude**, competing through-rubble modalities, USAR survival-time evidence. Propagation modelling, tap-source parameters and the SM-24 datasheet are covered by sibling document C; USAR doctrine and drone deployment by sibling document B.

Compiled 2026-10-07. Access states: **READ-FULL** / **READ-ABSTRACT** / **CITED-ONLY**.

---

## Bottom line for the proposal

- **The 1–4 N cardiac coupling assumption is MEASURED, PUBLISHED, AND CORRECT — it is not an estimate.** Starr et al. (1939) measured a mean ballistocardiographic I–J force amplitude of **3.7 N (±0.53 N)**; Inan (2009) independently replicated **4.06 N (±1.53 N)** across a healthy cohort, and Ashouri et al. (2016) report **~2 N peak-to-peak** on a calibrated high-bandwidth force plate. The proposal's central dB figure stands as written. The feared 20–40 N revision is not supported anywhere in the literature; the highest single-subject value found in any cohort is **10.95 N** (healthy maximum, Inan Table 6-1), and the entire *population* range is 0.63–10.95 N.
- **The bound is sound but it is not novel-as-a-negative-result, and no one has published it.** No paper was found that states or derives an infeasibility bound for seismic cardiac detection through rubble. The literature instead *silently concedes* the point: every through-rubble seismic system in service (Delsar LifeDetector, FEMA/INSARAG-fielded) targets **victim-generated tapping, scratching and voice**, never cardiac signal; and the one multi-sensor through-rubble study that enumerated modalities (Zhang et al., 2018) **did not attempt heartbeat at all**. Position the bound as *the first explicit quantification of a limit the field has only assumed*.
- **The retarget to tapping/voice is the doctrinally validated target, which strengthens rather than weakens the proposal.** Macintyre et al. (2011) report that in the 2010 Haiti response "[m]ost of the entrapped individuals were located by bystanders or by rescuers using voice callout search methods" — i.e. the responsive-survivor signal is already the operative one in the field. Use this to frame the retarget as *alignment with doctrine*, not retreat from ambition.

---

## The 1-4 N assumption: what the literature actually says

**Verdict: MEASURED. Multiple independent sources. The assumption is correct and defensible as written.**

This is the strongest result of the sweep. The force a human body couples into a substrate from cardiac activity has been measured since 1939 and re-measured repeatedly with modern instrumentation. It is reported as the **ballistocardiogram (BCG) I–J wave amplitude**, in newtons, at the body/substrate interface — which is exactly the quantity the analysis needs.

### Primary measured values

| Source | Quantity | Value | Method | Access |
|---|---|---|---|---|
| Starr et al. 1939 | BCG I–J force amplitude, mean (±σ), n=7 | **3.7 N (±0.53 N)** | Starr BCG table, calibration 28 g static force per mm of readout | CITED-ONLY (figure read in full from Inan 2009, which states the calibration conversion) |
| Inan 2009 (dissertation, §6.2.1) | BCG I–J amplitude, mean (±σ), healthy cohort | **4.06 N (±1.53 N)** | Modified commercial weighing scale, calibrated force transducer | READ-FULL |
| Inan 2009 (Table 6-1) | BCG I–J amplitude, **full population range** | **min 0.63 N / max 10.95 N** | same | READ-FULL |
| Inan 2009 (Table 6-1) | BCG J–K amplitude, mean (±σ) | 5.09 N (±1.90 N), range 1.27–13.25 N | same | READ-FULL |
| Inan 2009 (§6.2.3) | BCG I–J by sex | female **3.56 N (±1.06 N)**; male **5.56 N (±1.74 N)** | same | READ-FULL |
| Inan 2009 (Table 6-1) | BCG RMS power | **1.31 N_RMS (±0.48)**, range 0.55–3.59 N_RMS | same | READ-FULL |
| Ashouri et al. 2016 | BCG force, peak-to-peak, head-to-foot axis | **2 N_pp** | Kistler 9260AA6 high-bandwidth force plate (>200 Hz BW) | READ-FULL (Europe PMC full text) |
| Inan 2009 (§6.2.x, heart-failure subjects) | BCG I–J amplitude, pathological | **1.05 N** and **0.94 N** | same | READ-FULL |

Verbatim, Inan 2009 §6.2.1:

> "With the calibration factor (28 g static force per mm on the readout) given for converting millimeters on the readout to force in Newtons, the mean (±σ) BCG IJ-amplitude found by Starr, et al, was 3.7 N (±0.53 N), for seven subjects [9]. In this work, using the modified weighing scale, the BCG IJ-amplitude was found to be 4.06 N (±1.53 N), well within the expected range based on the Starr, et al. study."

Verbatim, Ashouri et al. 2016:

> "The force of the BCG signal is 2 N_pp and the sensitivity of the transducer in the weighing scale is 19.1 μV/N"

### Consequences for the proposal's central number

1. **No restatement is required.** 1–4 N brackets the healthy-population mean (3.7–4.06 N) from three independent instruments across 70 years. If anything the assumption is slightly *generous* to the heartbeat case at the low end: pathological subjects (the population of interest in a collapse — hypothermic, crush-injured, hypovolaemic) measure **0.94–1.05 N**, i.e. ~12 dB *below* the healthy mean. A trapped survivor's cardiac source is plausibly weaker than the assumption, not stronger.
2. **The 20–40 N scenario is excluded by measurement, not by argument.** The highest value recorded for any single healthy subject in a 26+ subject cohort is 10.95 N (I–J) / 13.25 N (J–K). To reach 20–40 N the proposal would need a subject outside every published distribution. The feared 14–20 dB erosion of the bound does not occur. The *defensible* worst case for the proposal is the healthy male maximum, ~11 N vs. the 4 N assumption — a **~8.7 dB** reduction in the bound, which leaves a 47–69 dB deficit at 38–60 dB. The conclusion is unchanged in kind.
3. **Caveat to state explicitly in the proposal.** These are **standing-subject, rigid-transducer, direct-contact** measurements — a human standing on a force plate or lying on an instrumented bed. They give the force the body *generates*, which is the right numerator. They do **not** characterise the body-to-rubble coupling efficiency of a supine, partially buried, debris-loaded torso, which is a separate (and almost certainly lossy) transfer function. The proposal should present 1–4 N as the measured **source force** and treat coupling loss as an additional, unquantified debit against the heartbeat case. This makes the bound conservative in the right direction.
4. **Use Starr 1939 as the primary citation and Inan/Ashouri as modern confirmation.** Starr is the canonical, most-cited source and the one a cardiology reviewer will recognise. Note that the 3.7 N figure is a *derived* conversion from Starr's millimetre readout using Starr's own stated calibration factor — the conversion is reported in Inan 2009, not asserted here. If a reviewer presses on provenance, Inan 2009's directly-calibrated 4.06 N is the cleaner citation.

### Also useful: the non-contact BCG/SCG literature confirms the regime, not the number

Target 1 anticipated mining the non-contact bed/chair sensor literature for absolute amplitudes. In practice **that literature almost never reports absolute N, m/s or m/s²** — it reports timing accuracy (ms error on R–J intervals), correlation against ECG, and heart-rate error percentages, because the applications are diagnostic rather than detection-limited. The absolute force numbers live in the *force-plate* subset (Starr, Inan, Ashouri, Yao), which is why those are the papers that matter here. Two incidental figures worth noting:

- Yao et al. 2020 measured the attenuation between a research force plate and a commercial weighing scale for the same subjects: the I, J, K waves "were attenuated by 0.18 N, 0.28 N, and 0.18 N" — i.e. instrument-dependent variability in BCG amplitude is of order 0.2 N, two orders below the 47–69 dB deficit. Instrumentation choice is not where this problem lives, which is the proposal's thesis.
- Peak-to-peak Central Aortic Force is reported at ~3.05 N at rest and ~5.77 N during exercise (Inan-group work). Exercise roughly doubles the cardiac force; a trapped survivor is not exercising.

---

## Novelty verdict

**PARTIALLY ANTICIPATED — with the specific novelty intact and worth funding.**

Justification, split by claim:

| Claim | Verdict | Why |
|---|---|---|
| "MEMS/geophone seismic sensing can detect a buried survivor's *heartbeat* through rubble" | **ALREADY REFUTED IN PRACTICE, NEVER PUBLISHED AS A BOUND** | No paper claims it. No fielded system attempts it. But no paper *states the bound either* — the field simply never tried. The negative result is unpublished. |
| "Seismic sensing detects *tapping/voice* from a responsive buried survivor" | **ALREADY PUBLISHED AND COMMERCIALLY FIELDED** | Delsar LifeDetector LD3 (Savox) is the FEMA/UKSAR-standard seismic/acoustic listening device doing exactly this. Up to 6 seismic sensors, 1 Hz–3000 Hz response. This is not novel as a detection concept. |
| "A geophone can recover cardiac signal at all" | **PUBLISHED AND WORKS — in direct contact** | HeartQuake (Park et al. 2020) recovers full ECG morphology from an **SM-24 geophone under a mattress** — the same sensor element this project uses. See Direct contradictions. |
| "First explicit, first-principles amplitude bound on seismic cardiac detection through rubble, derived from measured source force" | **NOVEL** | Nothing found states or derives this. |
| "Drone-deployed *distributed mesh* of MEMS seismic nodes, vs. hand-placed single sensors" | **LIKELY NOVEL — sibling B owns this** | Delsar is hand-emplaced by rescuers on the rubble surface. Autonomous aerial emplacement of a mesh is a different operational claim. Defer. |

**How to frame it in the proposal.** The novelty is *not* "we will detect survivors seismically" — that is a 30-year-old fielded capability. The novelty is (a) the **quantified bound** that explains why the heartbeat variant of the idea, which recurs constantly in student and startup proposals, cannot work, and (b) whatever sibling B establishes about drone-emplaced mesh geometry versus hand-emplaced point sensors. Claim (a) honestly as a negative result that the literature has assumed but never computed; it is a legitimate and citable contribution, and stating it up front inoculates the proposal against the obvious reviewer objection ("isn't this just a Delsar?").

---

## Papers found

| Full citation | DOI / URL | Access | Claim | Bearing on our argument |
|---|---|---|---|---|
| Starr, I., Rawson, A. J., Schroeder, H. A., & Joseph, N. R. (1939). Studies on the estimation of cardiac output in man, and of abnormalities in cardiac function, from the heart's recoil and the blood's impacts; the ballistocardiogram. *American Journal of Physiology–Legacy Content*, 127(1), 1–28. | 10.1152/ajplegacy.1939.127.1.1 | CITED-ONLY (DOI verified via Crossref; the 3.7 N figure read in full from Inan 2009's conversion of Starr's calibration) | Canonical first quantitative BCG; mean I–J force 3.7 N (±0.53), n=7 | **DECISIVE SUPPORT.** Primary measured source for the 1–4 N assumption. Cite as the anchor. |
| Inan, O. T. (2009). *Novel technologies for cardiovascular monitoring using ballistocardiography and electrocardiography* (Doctoral dissertation). Stanford University, Dept. of Electrical Engineering. | https://transducers.stanford.edu/uploads/PDFs/Dissertations/Dissertation_Inan.pdf | **READ-FULL** (203 pp. extracted locally) | I–J 4.06 N (±1.53), range 0.63–10.95 N; RMS 1.31 N_RMS; sex split 3.56/5.56 N; heart-failure subjects 0.94–1.05 N | **DECISIVE SUPPORT.** Independent modern replication of Starr, with full distribution and pathological cases. The single most useful document found. |
| Ashouri, H., Orlandic, L., & Inan, O. T. (2016). Unobtrusive estimation of cardiac contractility and stroke volume changes using ballistocardiogram measurements on a high bandwidth force plate. *Sensors*, 16(6), 787. | 10.3390/s16060787 | **READ-FULL** (Europe PMC XML; publisher site 403s) | BCG force 2 N_pp, head-to-foot; Kistler 9260AA6; n=17, 70.7 ± 11.3 kg | **SUPPORT.** Third independent instrument, calibrated force plate, same order. |
| Yao, Y., Ghasemi, Z., Shandhi, M. M. H., Ashouri, H., Xu, L., Mukkamala, R., Inan, O. T., & Hahn, J.-O. (2020). Mitigation of instrument-dependent variability in ballistocardiogram morphology: case study on force plate and customized weighing scale. *IEEE Journal of Biomedical and Health Informatics*, 24(1), 69–78. | 10.1109/JBHI.2019.2901635 (PMID 30802877, PMCID PMC6986214) | READ-ABSTRACT + partial full text (PDF extracted locally; Europe PMC XML returned 500) | I/J/K waves attenuated by 0.18 / 0.28 / 0.18 N between force plate and weighing scale; n=22 | **SUPPORT.** Instrument choice moves BCG amplitude by ~0.2 N — negligible against a 47–69 dB deficit. Reinforces "the deficit is in source, not instrumentation." |
| Kríz, J., & Seba, P. (2008). Force plate monitoring of human hemodynamics. *Nonlinear Biomedical Physics*, 2, 1. | 10.1186/1753-4631-2-1 (PMID 18294366, PMCID PMC2315646) | **READ-FULL** (Europe PMC XML) | Force plate resolution 0.1 N / 0.1 N·m, 1 kHz sampling. **Reports no absolute BCG force amplitudes.** | **NEUTRAL / useful negative.** Searched specifically for a fourth amplitude source; this paper does differential geometry on the waveform and never states amplitude. Documents that the non-contact BCG literature often omits absolute N. |
| Zhang, D., Sessa, S., Kasai, R., et al. (2018). Evaluation of a sensor system for detecting humans trapped under rubble: a pilot study. *Sensors*, 18(3), 852. | 10.3390/s18030852 (PMID 29534055, PMCID PMC5877370) | **READ-FULL** (Europe PMC XML) | CO₂, O₂, thermal, microphone tested in simulated collapse (8×24 m, Singapore Civil Defence Force). Detected casualty in 8/9 trials, ~1 h mean detection time. CO₂ sensitivity 75%, specificity 53.1%. Voice recognition 89.36%; human-related noise 93.85%; background rejection 100%. Thermal failed 2/9. **Heartbeat/cardiac signal was not attempted.** | **STRONG INDIRECT SUPPORT + the best "pre-empts" citation.** The one rigorous multi-modality through-rubble study enumerates four modalities and never considers cardiac. Cite as evidence the field treats heartbeat-through-rubble as out of scope. Its voice/noise detection rates also *support the retarget*. |
| Park, J., Cho, H., Balan, R. K., & Ko, J. (2020). HeartQuake: accurate low-cost non-invasive ECG monitoring using bed-mounted geophones. *Proceedings of the ACM on Interactive, Mobile, Wearable and Ubiquitous Technologies*, 4(3), Article 93, 1–28. | 10.1145/3411843 | READ-ABSTRACT (ACM DL 403s; abstract read in full from Yonsei Pure; DOI verified via Crossref) | **SM-24 geophone element** under a mattress recovers all five ECG peaks, 13 ms mean error; RR interval error 3 ms, QRS width 10 ms; n=21 + 15 | **THE KEY CONTRADICTION TO ADDRESS — and it resolves in our favour.** Same sensor element, cardiac signal, successfully recovered. Distinguished only by coupling path: mattress vs. metres of rubble. See Direct contradictions. |
| Yang, D., Zhu, Z., Zhang, J., & Liang, B. (2021). The overview of human localization and vital sign signal measurement using handheld IR-UWB through-wall radar. *Sensors*, 21(2), 402. | 10.3390/s21020402 (PMID 33430061) | **READ-FULL** (Europe PMC XML, first 100k chars of 283k) | Fielded IR-UWB systems: SJ6000+ penetrates 42 cm wall, 18 m stationary-human breathing detection, 27 m moving; RadarVision2000 >20 m through ~20 cm concrete; Xaver-400 20 m; Prism-200 15 m. Review is **predominantly respiration**, with minimal heartbeat-specific performance data. | **COMPETING MODALITY + supporting nuance.** Gives citable capability numbers for the context paragraph. Note for the proposal: even in radar — a far higher-SNR modality for this task — *respiration* is the workhorse and *heartbeat* is the hard case. The source-amplitude hierarchy is modality-independent. |
| Macintyre, A. G., Barbera, J. A., & Smith, E. R. (2006). Surviving collapsed structure entrapment after earthquakes: a "time-to-rescue" analysis. *Prehospital and Disaster Medicine*, 21(1), 4–17; discussion 18–19. | 10.1017/S1049023X00003253 (PMID 16602260) | READ-ABSTRACT (Europe PMC core record) | 1985–2004, 34 earthquake events, 48 medical articles with time-to-rescue data. Longest time to rescue "13–19 days"; longest *reliably reported* survival **14 days**. Mean maximum survival 6.8 days across 18 earthquakes. Multiple survivors beyond 48 h. | **VERIFIED — the user's known citation is real and correctly attributed.** Core motivation statistic. |
| Macintyre, A. G., Barbera, J. A., & Petinaux, B. P. (2011). Survival interval in earthquake entrapments: research findings reinforced during the 2010 Haiti earthquake response. *Disaster Medicine and Public Health Preparedness*, 5(1), 13–22. | 10.1001/dmp.2011.5 | **READ-FULL** (INSARAG-hosted published PDF, extracted locally) | Dismantles fixed-interval rules; majority of live rescues within first 5–6 days; US teams verified rescues on day 7; 22 individuals rescued by other US teams after day 5. **Most victims located by bystanders or voice callout.** | **BEST MOTIVATION CITATION + validates the retarget.** Note the third author differs from the 2006 paper (Petinaux, not Smith) — do not conflate them in the reference list. |

---

## Direct contradictions

Anything claiming seismic heartbeat detection works.

**One real contradiction exists, and it must be addressed head-on in the proposal because it uses the project's own sensor.**

### HeartQuake (Park et al. 2020) — SM-24 geophone, full ECG morphology recovered

| Attribute | HeartQuake | This project's heartbeat-through-rubble case |
|---|---|---|
| Sensor | SM-24 geophone element + amplifier + ADC | SM-24 / MEMS accelerometer |
| Coupling path | **One mattress. Direct body-to-substrate contact, standoff ≈ 0.2 m of foam.** | Metres of concrete, masonry, voids, soil |
| Noise environment | Quiet bedroom, stationary subject, controlled | Active disaster site; machinery, aftershocks, rescuers, traffic |
| Signal processing | Bi-LSTM deep model trained per-dataset, 21+15 subjects, clean paired ECG ground truth | No ground truth available at a collapse |
| Result | All five ECG peaks, 13 ms error | — |
| Stated degradation | "When additional noise factors are present (e.g., external vibration and various sleeping habits), the estimation error increases" — **in a bedroom** | — |

**How to handle it.** This paper does not contradict the bound; it *calibrates* it. HeartQuake proves the cardiac source is detectable when the coupling loss and the ambient noise are both near zero, which is precisely the regime the bound says is required. Its own authors report accuracy degrading from *household* vibration. Citing HeartQuake in the proposal is strongly advisable: it demonstrates the team knows the closest prior work, establishes that the 1–4 N source is real and recoverable in principle, and makes the 47–69 dB deficit a statement about *path and noise*, not about the sensor or the source. A reviewer who finds HeartQuake independently and sees it unaddressed will read the proposal as naive.

### Lower-grade claims seen but not substantiated

- An unattributed secondary claim surfaced in search that "the level of vibration produced by a beating heart is detectable by a geophone" at **< 30 cm from a person**, with "high auto-correlation levels." The ~30 cm standoff figure, if correct, is *itself a bound* and is consistent with ours — it implies a near-contact requirement. **Provenance is a US patent-family text, not a peer-reviewed measurement.** Do not cite without locating the primary source; see "Could not access."
- FINDER is repeatedly reported as detecting "heartbeats" through 30 ft of rubble. This is **microwave radar, not seismic** — a different physics with a different source term (chest-wall *displacement*, ~1 mm, reflecting an EM carrier) and no mechanical coupling into debris. It is not a contradiction of a seismic bound and should not be presented as one. See the modality table.

**No paper was found that claims seismic/accelerometric cardiac detection at any useful standoff through rubble, soil or debris.**

---

## Competing modalities through rubble

For the proposal's context paragraph — existence, capability, cost. Different physics; included only to position seismic.

| Modality | System | Capability | Cost if known | Citation / access |
|---|---|---|---|---|
| Microwave radar (vital signs) | **FINDER** (NASA JPL + DHS S&T) | Heartbeat beneath **30 ft (9 m)** crushed material; behind **20 ft (6 m)** solid concrete; **100 ft (30 m)** open space. NASA Spinoff reports **80% accuracy** commercially (65% for the JPL prototype). Four live rescues, 2015 Nepal earthquake. Also deployed 2017 Mexico earthquake. | **Not published.** Licensed to R4 Inc. (Edgewood, MD) and SpecOps Group Inc. Commercial units anticipated from spring 2014. Radar frequency not disclosed in public sources. | JPL news release 2013-09-17, https://www.jpl.nasa.gov/news/new-technology-can-detect-heartbeats-in-rubble/ — **READ-FULL**; NASA Spinoff 2018, https://spinoff.nasa.gov/Spinoff2018/ps_1.html — **READ-FULL**. Note: both are agency press/spinoff material, **not peer-reviewed**. Flag as such in the proposal. |
| IR-UWB radar (through-wall) | SJ6000+; RadarVision2000; Xaver-400; Prism-200 | SJ6000+: penetrates 42 cm wall; breathing of stationary human to **18 m**, moving human to **27 m**. RadarVision2000: >20 m through ~20 cm concrete. Xaver-400: 20 m. Prism-200: 15 m. PulseOn440: 1 cm accuracy open ground, <1 m indoors NLOS. **Respiration-dominant; heartbeat is the hard case even here.** | Not stated in the review | Yang et al. 2021, 10.3390/s21020402 — **READ-FULL** |
| CO₂ / O₂ gas sensing | Research prototype (Waseda / Singapore Civil Defence Force) | CO₂ sensitivity **75%**, specificity **53.1%**; 27 ppm threshold reduces the candidate search area to **44%** of total. Key limitation verbatim: "The gas sensor is difficult to use in open spaces due to stronger airflow affecting the CO₂ concentration." | Not stated | Zhang et al. 2018, 10.3390/s18030852 — **READ-FULL** |
| Thermal / IR vision | Same prototype | **Failed in 2 of 9 trials.** Confirms victim presence only where a line-of-sight gap through rubble exists. | Not stated | Zhang et al. 2018 — **READ-FULL** |
| Airborne acoustic (microphone + classifier) | Same prototype | Voice recognition **89.36%**; human-related suspect noise **93.85%**; background noise rejection **100%** | Not stated | Zhang et al. 2018 — **READ-FULL** |
| **Seismic / acoustic listening (the incumbent)** | **Delsar LifeDetector LD3** (Savox / Con-Space) | Up to **6 seismic sensors**, frequency response **1 Hz–3000 Hz**, shock resistance >1000 g, IP67, position-insensitive, 3.5″ dia × 2.6″ H, 16.5 oz. Turns the structure into a large microphone. **Targets victim-generated tapping, scratching, shouting — never cardiac.** Fielded by FEMA, UKSAR, SUSAR. | **Secondary-market observation only, uncaptured vendor pricing:** used LD3 unit listed ~**USD 3,490**; individual sensors ~**USD 333**. These are eBay/reseller listings seen in search result summaries — **treat as indicative, not citable.** No vendor list price retrieved. | Savox product page https://www.savox.com/products/search-and-rescue-kits/delsar — **CITED-ONLY** (specs read from search-result summaries, page body not directly fetched; see "Could not access"). **Per project environment rules, do not assert the price or stock without a captured date — and do not put either figure in the proposal without hand-verification.** |

**Positioning note for the proposal.** The honest comparison is not "seismic vs. radar for heartbeat" — radar wins that outright and FINDER is a fielded, publicly-credited success. The comparison that favours this project is **cost and coverage**: FINDER and Xaver-class radars are single-point, hand-operated, export-controlled, high-unit-cost instruments with no published price; a distributed low-cost MEMS mesh addresses *area search* rather than *point confirmation*. Make the argument on deployment economics and coverage geometry (sibling B's territory), not on sensitivity, where the bound this document supports says seismic loses for cardiac and ties-or-wins only for tapping/voice.

---

## Survival-time evidence for motivation

### Macintyre et al. 2006 — VERIFIED

PMID 16602260 confirmed real and correctly attributed. Macintyre AG, Barbera JA, Smith ER. *Prehospital and Disaster Medicine* 21(1):4–17, discussion 18–19. DOI 10.1017/S1049023X00003253.

- Method: Medline + Lexis-Nexis, 1985–2004. **34 earthquake events, 48 medical articles** with time-to-rescue data.
- Longest time to rescue: **"13–19 days"** post-event.
- Longest **reliably reported** survival: **14 days** after impact.
- **Mean maximum survival time 6.8 days** across 18 earthquakes.
- Multiple survivors documented beyond 48 h.

### Macintyre et al. 2011 (Haiti) — the stronger citation, and the one that settles "golden 72 hours"

Macintyre AG, Barbera JA, **Petinaux BP**. *Disaster Medicine and Public Health Preparedness* 5(1):13–22. DOI 10.1001/dmp.2011.5. READ-FULL.

**The "golden 72 hours" claim has a weak and partly mis-stated evidentiary basis.** Two findings a proposal can use directly:

1. **The original US doctrine was 48 hours, not 72.** Verbatim: *"Early teachings in the US response system emphasized only a 'golden 48 hours,' in which the chance of live finds is highest during the first 2 days. This approach was based on work related to a wide range of earthquake incidents which preceded the modern era of the sophisticated, integrated urban search and rescue capability."* The paper's own framing is that the fixed interval is a **teaching heuristic predating modern USAR**, not a derived survival curve. Other teams use an anecdotal "rule of fours" (4 min without air, 4 days without water, 4 weeks without food).
2. **The authors explicitly reject any single interval.** Verbatim from the abstract: *"The available medical and engineering data and media reports demonstrate a wide variety in survival 'time to rescue,' arguing against the acceptance of a single time interval applicable to all incidents."* And: *"Using these types of rigid, universal time frames to end search efforts may be grievously inaccurate."*

**Quantitative statistics available:**

- Majority of documented live rescues occur **within the first 5–6 days** — but the authors caution: *"The veracity and completeness of the data for this conclusion, however, are problematic."*
- 2010 Haiti: US teams **verified multiple rescues on day 7**; the final US-team rescues occurred on day 7 with 7 survivors extricated; other US teams rescued **22 individuals after day 5**.
- A documented Haiti case of extrication at **24 days** (media-reported, veracity flagged by the authors as doubtful for some late claims).
- Extrication itself is slow: one case required **5 h**, another **>10 h**; one required **amputation to extricate**.
- Hypothermia is common in extricated earthquake survivors, and the post-extrication period independently affects outcome.

**A caution the proposal should respect.** A recurring theme in both papers is that time-to-rescue data are **"perishable data [that] have never been captured in real time using objective and verifiable methods"**, with many rescues performed by untracked bystanders and media reports giving days rather than hours. Do not build a precise survival-vs-time curve or a quantitative "X% die per hour" claim from this literature — it does not support one, and a disaster-medicine reviewer will know that. The defensible motivation claims are: survival well past 72 h is documented and not rare; the longest reliable survival is 14 days; and the fixed-interval rules in common use are heuristics the primary authors explicitly disown. That is enough to motivate faster search without overclaiming.

### The finding that most helps the retarget

Verbatim from the 2011 paper's Haiti observations:

> "Most of the entrapped individuals were located by bystanders or by rescuers using voice callout search methods."

A survivor located by *voice callout* is by definition a **responsive survivor producing a deliberate signal**. The proposal's retarget to tapping/voice is therefore not a fallback — it targets the signal modality that actually locates people in real responses. This is the single best sentence in the sweep for the problem statement.

---

## Could not access — exact URLs/DOIs for hand-retrieval

Per project convention, these are named exactly. Several are **not** blocking — the needed figure was obtained by another route — and are flagged accordingly.

| Target | URL / DOI | Barrier | Still needed? |
|---|---|---|---|
| Starr et al. 1939, full text (to read the original calibration and amplitude tables first-hand) | DOI **10.1152/ajplegacy.1939.127.1.1** — https://journals.physiology.org/doi/10.1152/ajplegacy.1939.127.1.1 | Paywall (APS Legacy Content) | **YES — highest priority.** The 3.7 N figure is currently CITED-ONLY via Inan's conversion. For a faculty-signed proposal, read the original before citing it as the anchor number. |
| Park et al. 2020, HeartQuake, full text (for geophone mounting geometry, mattress thickness, signal amplitude, noise floor) | DOI **10.1145/3411843** — https://dl.acm.org/doi/10.1145/3411843 | HTTP 403 (ACM DL blocks scripted access) | **YES — high priority.** Needed to state the coupling path quantitatively when distinguishing it from the rubble case. Abstract and bibliographic data are confirmed; the amplitudes and standoff are not. |
| Yao et al. 2020, full text | DOI **10.1109/JBHI.2019.2901635** — PMCID **PMC6986214**; NSF public access copy https://par.nsf.gov/servlets/purl/10145592 | Europe PMC `fullTextXML` returned HTTP 500; PMC botwalled; NSF PDF extracted locally but tables not fully recovered | Low priority. The 0.18/0.28/0.18 N attenuation figure was recovered; nothing further is load-bearing. |
| Ashouri et al. 2016, publisher copy | DOI **10.3390/s16060787** — https://www.mdpi.com/1424-8220/16/6/787 | HTTP 403 (MDPI blocks scripted access) | No — full text read via Europe PMC XML (PMC4934213). Listed for completeness. |
| Delsar LifeDetector LD3 — official specification sheet and **current list price** | https://www.savox.com/products/search-and-rescue-kits/delsar and https://www.con-space.com/delsar/product/delsar-lifedetector-%e2%80%93-ld3/ | Page bodies not directly fetched; specs read only from search-result summaries. Prices seen are reseller/eBay listings. | **YES — medium priority.** The incumbent-system comparison is load-bearing for positioning. Capture specs and price **with a date stamp** per project convention; do not put the ~USD 3,490 / ~USD 333 figures in the proposal unverified. |
| FINDER / R4 Inc. unit price, and any peer-reviewed FINDER paper (as opposed to agency press) | Vendor: R4 Inc., Edgewood MD; SpecOps Group Inc. No DOI located. | No published price found; no peer-reviewed FINDER publication located in this sweep | **YES — medium priority.** The proposal would be stronger citing a peer-reviewed FINDER evaluation than a NASA Spinoff article. Worth one targeted search (try IEEE Xplore, "FINDER" + Lux/Jet Propulsion Laboratory). |
| Primary source for the "geophone detects heartbeat at <30 cm" claim | Appears in US patent-family text (likely among US 7,019,641 / US 7,417,536 "living being presence detection system", seen in search results but not fetched) | Not retrieved | Optional. Only if the proposal wants a second standoff bound. **Patent text is not a measurement — do not cite as one.** |
| Yang et al. 2021, remaining full text | DOI **10.3390/s21020402** | Read first 100,000 of 283,127 characters via Europe PMC; remainder unread (offset 100000) | Low priority. Capability table figures already extracted. Re-read only if a heartbeat-specific radar SNR figure is wanted. |

---

## What I could be wrong about

Stated plainly, because the proposal is faculty-signed.

1. **The Starr 3.7 N figure is a derived conversion I did not verify at the primary source.** It comes from Inan 2009 converting Starr's millimetre readout via Starr's stated 28 g-force-per-mm calibration. Inan's own directly-measured 4.06 N is independent and agrees, so the *conclusion* is robust to an error here — but the specific number 3.7 N should be read in the 1939 original before it anchors a proposal. If the conversion is wrong, Inan and Ashouri still bracket 2–4 N.
2. **All measured BCG forces are standing/supine direct-contact on rigid transducers.** They are the right numerator for a source-amplitude argument, but I found **no** measurement of cardiac force coupled from a *partially buried, debris-loaded, supine* body into rubble. That transfer function is unmeasured. I have assumed it is lossy (reducing the heartbeat case further); if some resonance or mass-loading effect in a confined void were to *amplify* coupling, the bound would need revisiting. I consider this unlikely but it is genuinely unmeasured and the proposal should not claim otherwise.
3. **The force-ratio scaling method itself is outside my lane and I did not validate it.** I verified the ~1–4 N cardiac numerator. Whether scaling a measured footstep *seismic amplitude* down by a cardiac/footstep *force* ratio is a legitimate operation depends on source-coupling, spectral content (footsteps 10–100 Hz with most energy 20–90 Hz; BCG/SCG below ~25 Hz, with Inan's BCG spectral peaks at 4.08 Hz and 5.99 Hz) and duration/impulse differences. **The two sources are not spectrally co-located**, which likely matters for both propagation and sensor response. Sibling C owns propagation; flag this to them. The dB figure could move on that basis even though the 1–4 N input is sound.
4. **The ~700 N footstep GRF comparator I did not independently verify.** It is physically reasonable (~1× body weight for walking, higher for running), but I searched for and did not retrieve a specific measured citation for it. It needs one.
5. **"No published infeasibility bound exists" is an absence-of-evidence claim.** I searched in English across PubMed/Europe PMC, Crossref, arXiv, MDPI, IEEE-indexed and Google-Scholar-style phrasings. A bound could exist in a defence/security-sensor venue (SPIE Defense + Security proceedings are a plausible home — "Range limitation for seismic footstep detection" surfaced there and I did not retrieve it), in a non-English literature, or in grey/agency literature I did not reach. Claim the novelty as "no published bound was located in a systematic search of X" rather than "none exists."
6. **FINDER's capability figures come entirely from NASA/JPL press and Spinoff material, not peer review.** The 30 ft / 20 ft concrete / 100 ft / 80% accuracy numbers are agency self-reported. They are fine for a context paragraph if attributed as such; they are not a peer-reviewed benchmark, and a reviewer may say so.
7. **Delsar pricing is unverified reseller data seen in search summaries.** I did not fetch the vendor pages directly. Per this project's own rule that BOM prices are perishable and stock claims need a capture date, these figures should not enter the proposal without hand-retrieval.
8. **HeartQuake is the contradiction most likely to be found by a reviewer, and my characterisation of it rests on its abstract plus bibliographic metadata, not its full text.** I could not read its methods section (ACM DL 403). My claim that it requires near-zero coupling loss follows from "penetrate through a bed mattress" and its own statement about degradation under external vibration — strongly implied, but I have not read the mounting geometry or the measured amplitudes. If its full text reports a larger standoff or a harsher noise environment than the abstract suggests, the way the proposal must distinguish it would change.
9. **I did not find absolute amplitudes (m/s, m/s², g) from the non-contact bed/chair sensor literature**, which search target 1 anticipated would be a rich source. My conclusion that this literature mostly reports timing/correlation rather than absolute magnitude is based on a sample of that literature, not an exhaustive read. A targeted search for SCG sternum acceleration in milli-g returned method descriptions and spectral ranges (SCG below ~25 Hz) but no peak-amplitude figures I could verify; those numbers may well exist and would give a fourth independent cross-check if found.
