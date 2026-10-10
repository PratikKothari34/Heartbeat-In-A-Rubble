**RESEARCH PROPOSAL**

**Name:** [Faculty member's full name]

**Department:** [Department / School]

**E-mail ID:** [institutional e-mail]

**Address:** [Office address]

**Phone:** Home [ ] Office [ ] Fax [ ]

**Project Title:**

**Air-Deployed Seismic Sensor Mesh for Locating Responsive Survivors in Collapsed Structures: Array Extent, Coupling onto Debris, and the Limits of Cardiac Detection**

| **Item** | **Summary** |
| --- | --- |
| Duration requested | 12 months |
| Total amount requested | **Rs. 1,82,818** (detail on the Proposed Budget page) |
| Field of research | Near-surface seismic sensing, embedded sensor networks, disaster search-and-rescue technology |
| Nature of work | Experimental: bench measurement, a campus debris test pile, sensor-node hardware, drop and air-deployment trials, one field trial |
| Human participants | Yes, minimal risk. Adult volunteers tap on an instrumented plate and on the surface of a test pile. No one is ever placed under debris or load. Institutional ethics approval will be obtained before any participant test. |
| Drone | Borrowed from [lab / department]. No airframe purchase is requested. |

**Submitted by:** (Signature and printed name: Faculty Member)

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

[Printed name of faculty member] Date: [ ]

**PROPOSAL DESCRIPTION**

**ABSTRACT. *Please describe, in language appropriate for the educated lay person, what you propose to do and how it will contribute to knowledge or why it is important. (1 page)***

When a building collapses, rescuers find survivors mainly by calling out and listening. Roughly once an hour, all work on the site stops for a few minutes on a commanded signal, an "All Quiet", so that teams can listen for tapping or calling [2, 3]. In the 2010 Haiti response, most trapped people were found by bystanders or by rescuers using voice call-out [4].

The instruments that help them are listening devices: six to eight cabled sensors placed by hand on the debris, with a trained operator interpreting the output through headphones. India's National Disaster Response Force specifies exactly this type of instrument [5, 6]. These devices work, but a rescuer has to stand on an unstable pile to place each sensor and then move them from place to place. The array can also only be as wide as the cables and the operator allow. The closest published research system on real rubble names "the limited spatial extension of the sensor array" as one of its own limitations [1].

**We propose to drop many small, inexpensive vibration-sensing nodes from a drone.** The array can then be larger and denser than hand placement allows, and nobody has to climb the pile to lay it out. The nodes listen during each All Quiet and report to a ground station. The system then marks each 2–5 m cell of the site as **DETECTED**, **NO DETECTION** or **BLIND** (not covered). Because the nodes stay in place for days, the system can ask whether a signal comes back silence after silence. A trapped survivor stays put; a passing truck does not. A hand-carried instrument leaves with its operator, so it cannot use this repetition to reject false alarms.

This project began as an attempt to detect the **heartbeat** of an unconscious survivor, and training literature still suggests such sensors might pick up "even the vibration of a heartbeat" [21]. Our analysis, checked against heart forces measured in three independent studies [14–16], shows that this cannot work through rubble: the signal falls **38–60 dB short**, roughly 80 to 1,000 times too weak. No filter, averaging scheme or learning algorithm recovers that gap. We will publish this bound as a negative result so others stop designing toward it. The system therefore targets what rescue doctrine already asks survivors to do: **tap or call**.

The project will produce: the first measurements of how an air-dropped sensor couples to **collapsed debris** rather than soil; a measured comparison of location accuracy for a wide, air-deployed array against a compact, hand-placed one; a measured false-alarm rate for the repeated-silence rule; and the published cardiac bound. The work is ordered so that the two cheapest measurements, background vibration on site and the force of a real human tap, are made in the first two months. Either can stop the project before significant money is spent.

**1. *What are your objectives, or the specific questions/problem/hypothesis you will address? (1 page)***

**Overall aim**

To establish, by measurement, whether an air-deployed mesh of low-cost geophone nodes can locate a responsive survivor's tapping on collapsed debris to a 2–5 m cell, with a usable false-alarm rate. We also aim to publish the detection limits for both tapping and the heartbeat.

**What changed, and why**

An earlier design for this project aimed to detect heartbeats with MEMS accelerometers behind a 0.5–4 Hz filter. That filter matched the heart's **repetition rate** (60–120 beats per minute), not the **bandwidth** of each beat, which is a broadband impulse with a 50–150 ms rise. The filter kept the rate and discarded the signal. Correcting the error, and using source forces that have since been measured [14–16], put the cardiac signal 38–60 dB below the sensor floor. The same correction reverses the original sensor choice: a geophone (SM-24) is far quieter than the MEMS part in the band where the signal actually lives. Tapping clears that geophone's floor with a predicted margin of +23 to +41 dB.

**Research questions and hypotheses**

| **#** | **Research question** | **Hypothesis / success criterion** |
| --- | --- | --- |
| RQ1 | **Capability.** Does air deployment lift the array-extent limit that bounds existing microseismic survivor location [1], and by how much in localization accuracy? | Location error is bounded by node-position uncertainty, as standard geometric-dilution-of-precision (GDOP) analysis predicts; this is stated as an error-budget result, not a discovery. For the same node count, a wider air-placed array assigns a tap source on the test pile to the correct 2–5 m cell more often than a compact, hand-placed one. |
| RQ2 | **Coupling onto debris.** How does an air-dropped node couple to collapsed structural debris? Published air-deployment work characterises **soil** only [8, 9]; no characterisation on debris was found. | Measured contact resonances for geophones on soil fall at 100–500 Hz [13]. At the low end this is close enough to the tap band to distort amplitude **and phase**. We expect this to be worst for free-laid nodes on fractured debris, which is what air-dropping produces. Success: a measured transfer function for dropped, free-laid and planted nodes against a bolted reference, for each landing type. |
| RQ3 | **Bounds.** What is the true detection limit through rubble for a cardiac source and for a tap? | H3a: tap and voice from a responsive survivor exceed the geophone noise floor by +23 to +41 dB at relevant ranges [computed; depends on the tap force, which is measured first]. H3b: cardiac signal sits 38–60 dB below the same floor [computed from measured forces] and cannot be recovered. |
| RQ4 | **False alarms.** Does requiring a detection to persist across repeated All Quiet windows turn an unusable false-alarm rate into a usable one? | With illustrative per-look figures (93% sensitivity, 7% false-positive rate, 1.4% prior), a single look gives a positive predictive value near 16%. Requiring detection in at least 60% of available looks raises it to 70–98%. Target: no more than 1 false detection per node-hour on **empty** rubble, with machinery running. |

**Key unmeasured input.** Every tap margin above scales with the force and frequency content of a human tap. The working figures, 50–300 N with energy at 60–80 Hz, have no published source; the nearest published values come from destructive strikes and were rejected. They are therefore measured first (Activity 2).

**Prior art, cited and distinguished**

| **Work** | **What it establishes** | **How this project differs** |
| --- | --- | --- |
| Arosio et al. 2010 [1] | A hand-placed microseismic array on real rubble locates survivors; 3× faster than incumbent systems; rubble velocity 200–600 m/s. | Closest prior art. We address the array-extent limitation it names. |
| FEMA / UK NFCC doctrine [2, 3]; Delsar LD3, NDRF Type-I [5, 6] | Tapping and voice are the existing target: the "victim must create a recognizable sound pattern". | We do not claim the tap/voice target as new. |
| INACHUS, EU FP7 607522 [7] | Stated the goal of automated knock localization. | No peer-reviewed accuracy result was located. We claim neither novelty nor that it was achieved. |
| Stewart et al. 2016 [8]; SeismicDart [9] | Drone-landed and air-dropped geophones work in **soil** (correlation 0.81–0.98 with planted sensors). | Debris, not soil; mesh scale, not a few sensors per sortie. |
| HeartQuake, Park et al. 2020 [10] | Full ECG shape recovered through a mattress with an SM-24 geophone, the part we use. | Contact-coupled through bedding, not metres of rubble. Consistent with our bound, not a contradiction of it. |
| Sabatier & Ekimov 2008 [11] | A signal-equals-noise range bound for footsteps. | The direct methodological ancestor of our cardiac and tap bounds. |

**2. *Describe the methods of investigation and techniques of analysis you intend to use. (1 page)***

**A. Sensor and signal chain**

Each node carries a Geospace SM-24 geophone (10 Hz natural frequency, 28.8 V/(m/s), 375 Ω, 74 g) [20], a low-noise preamplifier, a 24-bit ADC, a microcontroller with an 865–867 MHz radio, and an 18650 cell. The element's own thermal noise, from Johnson-noise analysis (eₙ = √(4kTR), converted to acceleration through the sensitivity), is 0.003–0.005 µg/√Hz across 60–80 Hz. That is 23–30 times quieter than the 0.1 µg/√Hz assumed in the margin calculations. The geophone datasheet gives no noise figure, so the **preamplifier**, not the element, sets the system floor. At 4 nV/√Hz input noise the system sits 12–16× below the assumed floor; the margin is used up near 50 nV/√Hz. The preamplifier is specified and measured first. A microphone channel (200 Hz–3 kHz) covers voice.

**B. Analysis band set by measurement, not assumption**

Timing precision follows the Cramér–Rao bound, σₜ ≈ 1/(B·√SNR), where B is the RMS bandwidth [17, 18]. Narrowing the filter therefore makes location worse, which is the error that sank the original design. The detection band will be fixed from the **measured** tap spectrum (Activity 2). Current working estimates disagree: a 5–40 Hz design band against 60–80 Hz estimated tap energy. The NDRF Type-I specification, meanwhile, filters at 100–600 Hz [5]. Settling this is the first analytical deliverable.

**C. Amplitude prediction**

Received amplitude is predicted by **linear transfer-mobility scaling** (the FTA ground-borne vibration method [19]). Elastic wave propagation is linear, so response scales with source force. Scaling is anchored to measured footstep responses: no more than 3 µm/s at 3 m, with a peak near 17 Hz [11, 12]. Wave velocity is measured in place with a hammer source and compared with Arosio's 200–600 m/s for rubble [1].

**D. Detection and false-alarm control**

Nodes listen only during commanded All Quiet windows, which the incident commander already signals [2, 3]; this gives a duty cycle of roughly 5–13%. Detection uses a matched filter against the impulse shape and, where the survivor can be prompted, against a known tap pattern. Each node-cell detection is scored over repeated windows with a **fraction-of-looks** rule (at least 60% of available looks). A fixed count degrades as looks accumulate. Performance is reported as false detections per node-hour on empty rubble, not as accuracy.

**E. Localization**

Time-difference-of-arrival (TDoA) multilateration, with wave velocity solved as an unknown. GDOP is the stated framework for how array geometry amplifies error. A node's position is taken from the drone's logged release point plus its measured bounce; ground truth comes from a tape or total-station survey. The output is a cell, not a pin. Further spending on clock synchronisation is not justified: below about 2 µs, timing error is negligible against metre-scale node-position error.

**F. Coupling onto debris (RQ2)**

Node shells (rounded, spiked, weighted foot) are dropped onto the campus debris pile, first from a fixed release rig at measured heights, then from the drone. Each landed node is excited with a hammer source next to a bolted reference geophone. The resulting transfer function gives amplitude and phase error per landing type, including any contact resonance near the tap band [13].

**G. Cardiac bound (RQ3)**

The measured site noise floor and the published heart forces (3.7 N, n = 7 [14]; 4.06 ± 1.53 N, n = 26+ [15]; about 2 N peak-to-peak on a force plate [16]) are combined through the same transfer-mobility model. No human is ever placed under debris, and no new cardiac measurement on people is needed.

**3. *List the specific activities that you will undertake during the period of funding, noting the anticipated time frame for completion of each activity. Please also describe other activities in which you will participate during the award period that may be bear on your research, for example, summer teaching, conferences, administrative duties, and other comments. (1 page)***

Activities are ordered so that each risk that could stop the project is tested before the money that depends on it is spent. Months 1–4 use a **wired** array, which needs no radio approval and no drone and isolates the sensing problem from radio debugging.

| **Activity** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** | **10** | **11** | **12** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Ambient in-band noise survey (campus building, demolition site): **go/no-go** |  |  |  |  |  |  |  |  |  |  |  |  |
| Tap force and spectrum characterisation (volunteers, instrumented plate): **go/no-go** |  |  |  |  |  |  |  |  |  |  |  |  |
| Preamplifier design; ethics application; procurement |  |  |  |  |  |  |  |  |  |  |  |  |
| Build graded debris test pile on campus |  |  |  |  |  |  |  |  |  |  |  |  |
| Single-node wired signal chain; tap detection at 1 / 3 / 10 m |  |  |  |  |  |  |  |  |  |  |  |  |
| Cardiac bound: analysis against measured floor; manuscript draft |  |  |  |  |  |  |  |  |  |  |  |  |
| Coupling onto debris: free-laid vs planted vs dropped (RQ2) |  |  |  |  |  |  |  |  |  |  |  |  |
| Mesh: time sync, TDoA solver, persistence detector; false-alarm test with machinery running (RQ4) |  |  |  |  |  |  |  |  |  |  |  |  |
| Air deployment: drop mechanism, node survival, landing-position scatter |  |  |  |  |  |  |  |  |  |  |  |  |
| Field trial on a rubble pile: wide vs compact array, accuracy vs Arosio's benchmark (RQ1) |  |  |  |  |  |  |  |  |  |  |  |  |
| Analysis, dataset release, final report, manuscripts |  |  |  |  |  |  |  |  |  |  |  |  |

**Milestones and decision gates**

* **M2: go/no-go.** The measured in-band ambient floor and the measured tap force are compared with the predicted tap amplitude at 3 m. If the floor swamps the tap, or the tap force is far below 50 N, the project stops here, having spent mainly on two geophones and one node.
* **M4:** measured tap detection margin at 1 / 3 / 10 m against the computed +23 to +41 dB prediction; analysis band fixed.
* **M6:** coupling-onto-debris result (first publishable result) and cardiac-bound manuscript submitted.
* **M8:** false-alarm rate measured on empty rubble with machinery running; RQ4 answered.
* **M10:** node-position error budget closed from measured landing scatter.
* **M12:** field-trial accuracy (RQ1), open dataset, final report, follow-on proposal.

**Other activities during the award period**

[Teaching load for each semester, administrative duties, and any planned conferences. Suggested venue for results: Near Surface Geophysics / EAGE Near Surface meetings, or IEEE Sensors.]

Students: [number] undergraduate/postgraduate student(s) will work on node hardware, field recording and the detection software as part of their project work.

**4. *If this is a new line of inquiry for you, briefly explain why you decided to pursue it. (1/2 page)***

[Adapt to the faculty member's background.] It is a new line for this group. The case for it comes from a gap that the prior art names itself:

* Arosio et al. established microseismic survivor location on rubble and named **limited array extent** as a limitation [1]. Hand placement is what causes it; air deployment removes the cause. This is an argument about capability, which is stronger than an argument about cost.
* **Nobody has characterised sensor coupling onto collapsed debris.** All air-deployment work is parameterised by soil strength [8, 9]. This is a genuine, narrow, measurable gap.
* **The negative result is itself a contribution.** A bound on cardiac detection through rubble has not been published, while the belief that it might work persists in practitioner literature [21].
* **Indian context:** the NDRF Human Life Detector Type-I specification contains no automated-localization requirement at all [5]. That is a capability gap documented in the procuring agency's own words.

**5. *What products (i.e., publications, presentations, performances, outside funding, patents) would you anticipate from this project? (1/2 page)***

* **Journal article 1:** the cardiac seismic detection bound through rubble, a negative result publishable on its own.
* **Journal article 2:** air-deployed array extent and localization accuracy on rubble, with the false-alarm result.
* **Short measurement paper (possible):** coupling of free-laid and air-dropped geophone nodes onto collapsed debris.
* **Presentations:** near-surface geophysics and search-and-rescue technology venues; Arosio's line of work appears in *Near Surface Geophysics* and at EAGE meetings.
* **Open dataset and code:** debris noise recordings, tap-force and tap-spectrum measurements, coupling transfer functions, node firmware and the detection pipeline.
* **Outside funding:** measured coupling and accuracy results are the precondition for a credible NDRF/NDMA-facing or agency proposal. This project is scoped to produce that evidence.
* **Patents:** none claimed. Air deployment of seismic sensors is already published [8, 9].

**PREVIOUS RESEARCH AND SUPPORT**

*NOTE: You may omit this question and the next if they are not applicable. You may use additional paper to answer these questions if necessary.*

**1. *List any grants that you have received that relate in any way to the project you are proposing. (1 page)***

[None / or list: project title, source of support, period, amount awarded, products, and how it relates to this proposal.]

**2. *Please list any grants or awards for which you intend to apply or for which applications are pending that would bear in any way upon the project you are proposing in this application. (1/2 page)***

[None pending.] On successful completion we intend to apply for a follow-on project on field deployment with an operational partner (NDRF or a State Disaster Response Force) to [agency], for [period] and [amount]. It would build directly on the coupling, false-alarm and accuracy results established here.

**3. *Please list your five most recent scholarly products, e.g., books, journal articles, art exhibitions, performances, etc., with complete citations. (1/2 page)***

1. [Citation 1]
2. [Citation 2]
3. [Citation 3]
4. [Citation 4]
5. [Citation 5]

**PROPOSED BUDGET**

Please provide a brief description of each item requested in the space provided on this sheet. Use an attached sheet to provide a brief statement of justification for each item requested, including faculty salary.

| **Category** | **Amount** |
| --- | --- |
| 1. Consumables | Rs. 23,100 |
| 2. Equipment | Rs. 1,13,850 |
| 3. Services (PCB assembly, machining) | Rs. 9,240 |
| 4. Contingency (field work and research purposes only, 12% of direct costs) | Rs. 19,588 |
| 5. Supplies | Rs. 5,040 |
| 6. Other (specify): local travel to field sites | Rs. 12,000 |
| **TOTAL AMOUNT REQUESTED** | **Rs. 1,82,818** |

No faculty salary or honorarium is requested. No drone is purchased; air-deployment trials use a drone borrowed from [lab / department].

**Pricing basis.** Imported parts are converted at Rs. 84/USD (rate of 2026-10-07) with **+33% landed cost** added for basic customs duty, social welfare surcharge and IGST. The SM-24 geophone is priced at a current Indian distributor listing. Component prices on this project moved 8–16% in 19 days, so every line will be re-quoted before purchase.

**BUDGET JUSTIFICATION**

**Equipment: Rs. 1,13,850**

| **Item** | **Amount** |
| --- | --- |
| Sensor nodes × 8 (6 operating + 2 spares for drop losses) @ Rs. 10,021: SM-24 geophone Rs. 7,140 + node electronics Rs. 2,881 (radio/MCU module, antenna, 24-bit ADC and low-noise preamplifier, 18650 cell, case, PCB, passives; USD 25.79 + 33% landed) | Rs. 80,168 |
| Reference geophones (SM-24) × 2, bolted / planted, as ground truth for the coupling tests | Rs. 14,280 |
| Raspberry Pi 5 ground station | Rs. 8,938 |
| GNSS receiver with 1PPS output (timing reference for the mesh) | Rs. 2,788 |
| Cell charger, programming adaptors, small tools | Rs. 1,676 |
| Tap-force measurement plate: load cell, mounting plate and amplifier (est., to be quoted) | Rs. 6,000 |

**Consumables: Rs. 23,100**

PCB fabrication (two rounds), connectors, cabling, enclosures and potting compound, debris material for the campus test pile, and drop-test consumables, including spare propellers and a battery for the borrowed drone.

**Services: Rs. 9,240**

PCB assembly for the node boards; workshop machining of the drop-release mechanism and node feet/spikes.

**Supplies: Rs. 5,040**

Fasteners, adhesives, test targets, and safety consumables (gloves, helmets, boot covers) for work on debris.

**Other: local travel, Rs. 12,000**

About eight visits to demolition or debris sites for the ambient noise survey and the field trial.

**Contingency: Rs. 19,588**

12% of direct costs, held for nodes lost or damaged in drop tests, price movement on imported parts, and the field trial.

**Why the major items are needed**

* **Geophone nodes.** The geophone's low noise is the whole detection margin for tapping. Eight nodes give a six-node working array, enough to compare a wide layout against a compact one, plus two spares for drop losses.
* **Reference geophones.** A bolted reference is the only way to measure what a dropped node loses in coupling, which is research question RQ2.
* **Tap-force plate.** Every margin in the design scales with tap force, which has never been measured for this purpose. This is the cheapest item that can stop the project, and it is used first.

**Regulatory items (not requested in this budget)**

* **Drone.** Importing drones in built-up or kit (CBU/CKD/SKD) form has been prohibited since 9 Feb 2022 [22], so none is bought; the borrowed drone is operated on campus by its registered operator under the Drone Rules, 2021 [23].
* **Radio.** The 865–867 MHz band is licence-exempt only for type-approved equipment [24]. Months 1–4 use a wired array. Radio modules will be chosen from those holding WPC Equipment Type Approval; if none fits, approval will be sought through the institute before any over-the-air test.

**REFERENCES**

1. Arosio, D., Longoni, L., Papini, M., Scaioni, M., Zanzi, L., & Alba, M. (2010). A microseismic approach to locate survivors trapped under rubble. Near Surface Geophysics, 8(6), 623–633. doi:10.3997/1873-0604.2010051
2. FEMA National US&R Response System. Structural collapse training material, Module 3 Unit 3 [exact title to be confirmed]. fema.gov/pdf/emergency/usr/mod3\_u3.pdf
3. UK National Fire Chiefs Council. National Operational Guidance: Primary search – unstable or collapsed structure.
4. Macintyre, A. G., Barbera, J. A., & Petinaux, B. P. (2011). Survival interval in earthquake entrapments: research findings reinforced during the 2010 Haiti earthquake response. Disaster Medicine and Public Health Preparedness, 5(1), 13–22. doi:10.1001/dmp.2011.5
5. National Disaster Response Force. Specification: Human Life Detector Type-I (seismic/acoustic), and CSSR equipment schedule. www.ndrf.gov.in
6. Savox. Delsar LifeDetector LD3 datasheet (A02005#B).
7. INACHUS: Technological and methodological solutions for integrated wide area situation awareness and survivor localisation. EU FP7 grant agreement 607522.
8. Stewart, R. R., et al. (2016). Drone-deployed geophones. SEG Technical Program Expanded Abstracts 2016. [Exact title and DOI to be confirmed.]
9. Sudarshan, S., et al. A heterogeneous robotics team for large-scale seismic sensing (SeismicDart). NSF award IIS-1553063. [Venue to be confirmed.]
10. Park, J., Cho, H., Balan, R. K., & Ko, J. (2020). HeartQuake: accurate low-cost non-invasive ECG monitoring using bed-mounted geophones. Proc. ACM Interactive, Mobile, Wearable and Ubiquitous Technologies, 4(3). doi:10.1145/3411843
11. Sabatier, J. M., & Ekimov, A. E. (2008). Range limitation for seismic footstep detection. Proc. SPIE 6963, 69630V. doi:10.1117/12.785235
12. Ekimov, A., & Sabatier, J. M. (2006). Vibration and sound signatures of human footsteps in buildings. Journal of the Acoustical Society of America, 120(2), 762.
13. Krohn, C. E. (1984). Geophone ground coupling. Geophysics, 49(6), 722–731. doi:10.1190/1.1441700
14. Starr, I., Rawson, A. J., Schroeder, H. A., & Joseph, N. R. (1939). Studies on the estimation of cardiac output in man … the ballistocardiogram. American Journal of Physiology, 127(1), 1–28. doi:10.1152/ajplegacy.1939.127.1.1
15. Inan, O. T. (2009). Novel technologies for cardiovascular monitoring using ballistocardiography and electrocardiography. PhD dissertation, Stanford University.
16. Ashouri, H., Orlandic, L., & Inan, O. T. (2016). Unobtrusive estimation of cardiac contractility and stroke volume changes using ballistocardiogram measurements on a high bandwidth force plate. Sensors, 16(6), 787. doi:10.3390/s16060787
17. Van Trees, H. L. (1968). Detection, Estimation, and Modulation Theory, Part I. Wiley.
18. Quazi, A. H. (1981). An overview on the time delay estimate in active and passive systems for target localization. IEEE Trans. Acoustics, Speech, and Signal Processing, 29(3), 527–533.
19. Federal Transit Administration (2018). Transit Noise and Vibration Impact Assessment Manual (ground-borne vibration, transfer mobility method).
20. Geospace Technologies. SM-24 geophone element brochure.
21. Donnelly, [initials]. Building collapse: rescue operation's technical search capabilities. Fire Engineering.
22. Directorate General of Foreign Trade. Notification prohibiting import of drones in CBU/CKD/SKD form, 9 February 2022.
23. Ministry of Civil Aviation, Government of India. Drone Rules, 2021.
24. Department of Telecommunications. G.S.R. 564(E), 30 July 2008 (use of 865–867 MHz band).