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
| Human participants | Yes, minimal risk. Adult volunteers tap on an instrumented plate and on the surface of a test pile. No one is ever placed under debris or load. The ethics application is filed in month 1, and no participant test takes place until institutional ethics approval has been granted (month 2 at the earliest). |
| Drone | Borrowed from [lab / department]. No airframe purchase is requested. |

**Submitted by:** (Signature and printed name: Faculty Member)

\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_

[Printed name of faculty member] Date: [ ]

**PROPOSAL DESCRIPTION**

**ABSTRACT. *Please describe, in language appropriate for the educated lay person, what you propose to do and how it will contribute to knowledge or why it is important. (1 page)***

When a building collapses, rescuers find survivors mainly by calling out and listening. Roughly once an hour, all work on the site stops for a few minutes on a commanded signal, an "All Quiet", so that teams can listen for tapping or calling [2, 3]. In the 2010 Haiti response, most trapped people were found by bystanders or by rescuers using voice call-out [4].

The instruments that help them are listening devices: six to eight cabled sensors placed by hand on the debris, with a trained operator interpreting the output through headphones. India's National Disaster Response Force specifies exactly this type of instrument [5, 6]. These devices work, but a rescuer has to stand on an unstable pile to place each sensor and then move them from place to place. The array can also only be as wide as the cables and the operator allow. The closest published research system on real rubble names "the limited spatial extension of the sensor array" as one of its own limitations [1].

**We propose to drop many small, inexpensive vibration-sensing nodes from a drone.** The array can then be larger and denser than hand placement allows, and nobody has to climb the pile to lay it out. The nodes listen during each All Quiet and report to a ground station. The system then marks each 2–5 m cell of the site as **DETECTED**, **NO DETECTION** or **BLIND** (not covered). Because the nodes stay in place for days, the system can ask whether a signal comes back silence after silence. A trapped survivor stays put; a passing truck does not. A hand-carried instrument leaves with its operator, so it cannot use this repetition to reject false alarms.

This project began as an attempt to detect the **heartbeat** of an unconscious survivor, and training literature still suggests such sensors might pick up "even the vibration of a heartbeat" [21]. Our analysis, checked against heart forces measured in three independent studies [14–16], shows that this cannot work through rubble: against the MEMS accelerometer the original design specified, the signal falls **38–60 dB short**, roughly 80 to 1,000 times too weak. No filter, averaging scheme or learning algorithm recovers that gap. We will publish this bound, computed against measured site noise, as a negative result so others stop designing toward it. The system therefore targets what rescue doctrine already asks survivors to do: **tap**. Calling out is the other half of that doctrine; a voice channel (200 Hz–3 kHz) needs a microphone this award neither funds nor schedules, so it is left to later work.

The project will produce: the first measurements of how an air-dropped sensor couples to **collapsed debris** rather than soil; a measured comparison of how much of a debris pile an air-deployed array covers, and how many cells it leaves BLIND, against a compact hand-placed array, with nobody on the pile; a measured false-alarm rate for the repeated-silence rule; and the published cardiac bound. The work is ordered so that the two cheapest measurements, background vibration on site and the force of a real human tap, are made in the first three months, the tap measurement only after ethics approval. Either can stop the project before significant money is spent: until then only the instruments those two measurements need are bought.

**1. *What are your objectives, or the specific questions/problem/hypothesis you will address? (1 page)***

**Overall aim**

To establish, by measurement, whether an air-deployed mesh of low-cost geophone nodes can locate a responsive survivor's tapping on collapsed debris to a 2–5 m cell, with a usable false-alarm rate. We also aim to publish the detection limits for both tapping and the heartbeat.

**What changed, and why.** An earlier design targeted heartbeats with MEMS accelerometers behind a 0.5–4 Hz filter — the heart’s **repetition rate**, not the **bandwidth** of each beat, a broadband impulse with a 50–150 ms rise. The filter kept the rate and discarded the signal. Corrected, and with source forces since measured [14–16], the cardiac signal sits 38–60 dB below that MEMS floor (ADXL355, 25 µg/√Hz). The same correction reverses the sensor choice to an SM-24 geophone, far quieter in the band where the signal lives (margins under RQ3).

**Research questions and hypotheses**

| **#** | **Research question** | **Hypothesis / success criterion** |
| --- | --- | --- |
| RQ1 | **Capability.** Does air deployment lift the array-extent limit that bounds existing microseismic survivor location [1]: more of the pile covered, fewer BLIND cells, and no rescuer on the debris? | With the same six nodes, an air-deployed layout leaves fewer of a test area's 2–5 m cells BLIND than a compact, hand-placed layout, and puts nobody on the debris; deployment time is recorded for both. A cell counts as covered when a reference tap at its centre is detected by at least five nodes, the minimum for a TDoA fix with wave velocity unknown. Point accuracy is reported for both layouts but is not the claim (section E). |
| RQ2 | **Coupling onto debris.** How does an air-dropped node couple to collapsed structural debris? Published air-deployment work characterises **soil** only [8, 9]; no characterisation on debris was found. | Measured contact resonances for geophones on soil fall at 100–500 Hz [13; abstract read, full text not yet retrieved]. At the low end this is close enough to the tap band to distort amplitude **and phase**. We expect this to be worst for free-laid nodes on fractured debris, which is what air-dropping produces. Success: a measured transfer function for dropped, free-laid and planted nodes against a bolted reference, for each landing type. |
| RQ3 | **Bounds.** What is the true detection limit through rubble for a cardiac source and for a tap? | H3a: a tap from a responsive survivor exceeds the geophone's assumed 0.1 µg/√Hz floor by +23 to +41 dB at 3 m [computed: noise integrated over a 35 Hz bandwidth (5–40 Hz), tap energy assumed at 60–80 Hz; scales with the tap force and spectrum, both measured first].[[1]](#footnote-1) H3b: the cardiac signal sits 38–60 dB below the **MEMS (ADXL355)** floor the original design assumed [computed from measured forces, same bandwidth] and cannot be recovered. A tap and a heartbeat differ by +32 to +56 dB at the same range [computed], which is why retargeting to tapping works. |
| RQ4 | **False alarms.** Does requiring a detection to persist across repeated All Quiet windows turn an unusable false-alarm rate into a usable one? | With illustrative per-look figures (93% sensitivity, 7% false-positive rate, 1.4% prior), a single look gives a positive predictive value near 16%. Requiring detection in at least 60% of available looks raises it to 82% at five looks, 98% at six and above 99% from seven [computed; assumes independent looks, which the test checks]. Target: on **empty** rubble with machinery running, a per-look false-positive rate no higher than the 7% assumed, and no correlation between successive windows. |

**Key unmeasured input.** Every tap margin above scales with the force and frequency content of a human tap. The working figures, 50–300 N with energy at 60–80 Hz, have no published source: the nearest published values come from destructive strikes and were rejected. Both are measured first (Activity 3), after ethics approval.

**2. *Describe the methods of investigation and techniques of analysis you intend to use. (1 page)***

**A. Sensor and signal chain**

Each node carries a Geospace SM-24 geophone (10 Hz natural frequency, 28.8 V/(m/s), 375 Ω, 74 g) [20], a low-noise preamplifier, a 24-bit ADC, a microcontroller with an 865–868 MHz radio, and an 18650 cell. The element's own thermal noise, from Johnson-noise analysis (eₙ = √(4kTR), converted to acceleration through the sensitivity), rises linearly with frequency: 0.0003–0.0044 µg/√Hz across 5–80 Hz, 23 to 365 times quieter than the 0.1 µg/√Hz assumed in the margin calculations. The geophone datasheet gives no noise figure, so the **preamplifier**, not the element, sets the system floor. At 4 nV/√Hz input noise the system sits 12–16× below the assumed floor across 60–80 Hz, and further below it at lower frequencies; at 80 Hz the margin is used up near 56 nV/√Hz. The preamplifier is therefore specified and measured first. In no candidate band does sensor self-noise set the limit; site background vibration does, which is why it is measured first (Activity 2).

**B. Analysis band set by measurement, not assumption**

Timing precision follows the Cramér–Rao bound, σₜ ≈ 1/(B·√SNR), where B is the RMS bandwidth [17, 18]. Narrowing the filter therefore makes location worse, which is the error that sank the original design. Nodes acquire **5–200 Hz**, and the tap detection band is an **output** of the measured tap spectrum (Activity 3), not an input. Where one working figure is unavoidable it is 20–80 Hz [assumed, pending measurement]. Two earlier figures are withdrawn: 5–40 Hz came from seismocardiography, a cardiac band, and 60–80 Hz for tap energy has no published source. The SM-24's 10 Hz corner costs 12 dB at 5 Hz but under 1 dB above 15 Hz, so the sensor choice holds in every candidate band. For comparison, the Delsar LD3 covers 1 Hz–3 kHz [6] and the NDRF Type-I specification filters at 100–600 Hz [5]. Every dB figure in this proposal names the band it was computed in.

**C. Amplitude prediction**

Received amplitude is predicted by **linear transfer-mobility scaling** (the FTA ground-borne vibration method [19]). Elastic wave propagation is linear, so response scales with source force. Scaling is anchored to measured footstep responses: no more than 3 µm/s at 3 m [11], with the low-frequency vibration maximum near 40 Hz [12]. Wave velocity is measured in place with a hammer source and compared with Arosio's 200–600 m/s for rubble [1].

**D. Detection and false-alarm control**

Nodes listen only during commanded All Quiet windows, which the incident commander already signals [2, 3]; this gives a duty cycle of roughly 5–13% [assumed: doctrine states the cadence, about once an hour, but not the duration]. Detection runs in two stages: a matched filter against the impulse shape, then, where the survivor can be prompted, a test for a known tap pattern over several seconds. Each node-cell detection is scored over repeated windows with a **fraction-of-looks** rule (at least 60% of available looks). A fixed count degrades as looks accumulate. Performance is reported as false detections per look on empty rubble, not as accuracy.

**E. Localization**

Time-difference-of-arrival (TDoA) multilateration, with wave velocity solved as an unknown. GDOP is the stated framework for how array geometry amplifies error. A node's position is taken from the drone's logged release point plus its measured bounce; ground truth comes from a tape or total-station survey. The output is a cell, not a pin. Air-placed node positions are uncertain by 2–5 m, against centimetres for a surveyed hand-placed array, which is why RQ1 is framed around coverage rather than point accuracy. Further spending on clock synchronisation is not justified: below about 2 µs, timing error is negligible against metre-scale node-position error.

**F. Coupling onto debris (RQ2)**

Node shells (rounded, spiked, weighted foot) are dropped onto the campus debris pile, first from a fixed release rig at measured heights, then from the drone. Each landed node is excited with a hammer source next to a bolted reference geophone. The resulting transfer function gives amplitude and phase error per landing type, including any contact resonance near the tap band [13; abstract only].

**G. Cardiac bound (RQ3).** The measured site noise floor and the published heart forces (4.06 ± 1.53 N, n = 26+ [15]; 3.7 N, n = 7, from Starr et al. [14] as converted and reported in [15]; about 2 N peak-to-peak on a force plate [16]) are combined through the same transfer-mobility model. No human is ever placed under debris, and no new cardiac measurement on people is needed.

**3. *List the specific activities that you will undertake during the period of funding, noting the anticipated time frame for completion of each activity. Please also describe other activities in which you will participate during the award period that may be bear on your research, for example, summer teaching, conferences, administrative duties, and other comments. (1 page)***

Activities are ordered so that each risk that could stop the project is tested before the money that depends on it is spent: only the gate instruments are bought before the month-3 go/no-go, and the rest of the array after it. Months 1–4 use a **wired** array, which needs no radio approval and no drone and isolates the sensing problem from radio debugging.

| **Activity** | **1** | **2** | **3** | **4** | **5** | **6** | **7** | **8** | **9** | **10** | **11** | **12** |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Ethics application; buy gate instruments only: 2 reference geophones, 1 node, tap-force plate |  |  |  |  |  |  |  |  |  |  |  |  |
| Ambient in-band noise survey (campus building, demolition site): **go/no-go** |  |  |  |  |  |  |  |  |  |  |  |  |
| Tap force and spectrum characterisation (volunteers, after ethics approval; instrumented plate): **go/no-go** |  |  |  |  |  |  |  |  |  |  |  |  |
| Preamplifier design; single-node wired signal chain; tap detection at 1 / 3 / 10 m on a floor slab |  |  |  |  |  |  |  |  |  |  |  |  |
| Array procurement after the gate: 7 nodes, ground station, GNSS receiver |  |  |  |  |  |  |  |  |  |  |  |  |
| Build graded debris test pile on campus |  |  |  |  |  |  |  |  |  |  |  |  |
| Cardiac bound: analysis against measured floor; manuscript |  |  |  |  |  |  |  |  |  |  |  |  |
| Coupling onto debris: free-laid vs planted vs dropped (RQ2) |  |  |  |  |  |  |  |  |  |  |  |  |
| Mesh: time sync, TDoA solver, persistence detector; false-alarm test with machinery running (RQ4) |  |  |  |  |  |  |  |  |  |  |  |  |
| Air deployment: drop mechanism, node survival, landing-position scatter |  |  |  |  |  |  |  |  |  |  |  |  |
| Field trial on a rubble pile: coverage and BLIND cells, air-deployed vs hand-placed layout, nobody on the pile (RQ1) |  |  |  |  |  |  |  |  |  |  |  |  |
| Analysis, dataset release, final report, manuscripts |  |  |  |  |  |  |  |  |  |  |  |  |

**Milestones and decision gates**

* **M3: go/no-go.** The measured in-band ambient floor and the measured tap force and spectrum are compared with the predicted tap amplitude at 3 m, in the band the measured tap spectrum indicates. If the floor swamps the tap, or the tap force is far below 50 N, the project stops here, having spent Rs. 30,301 (16.6% of the request) on two reference geophones, one node and the tap-force plate, plus local travel for the survey.
* **M4:** measured tap detection margin at 1 / 3 / 10 m on a floor slab, against the prediction recomputed from the measured tap force and spectrum (the +23 to +41 dB in RQ3 is the pre-measurement estimate); detection band fixed.
* **M6:** cardiac-bound manuscript submitted.
* **M7:** coupling-onto-debris result (first publishable measurement).
* **M8:** per-look false-positive rate measured on empty rubble with machinery running; RQ4 answered.
* **M10:** node-position error budget closed from measured landing scatter.
* **M12:** field-trial coverage result (RQ1), open dataset, final report, follow-on proposal.

**Other activities during the award period**

[Teaching load for each semester, administrative duties, and any planned conferences. Suggested venue for results: Near Surface Geophysics / EAGE Near Surface meetings, or IEEE Sensors.] Students: [number] undergraduate/postgraduate student(s) will work on node hardware, field recording and the detection software as part of their project work.

**4. *If this is a new line of inquiry for you, briefly explain why you decided to pursue it. (1/2 page)***

[Adapt to the faculty member's background.] It is a new line for this group. The case for it comes from a gap that the prior art names itself:

* Arosio et al. 2010 established microseismic survivor location on rubble — within 2 m, 3× faster than incumbent systems, velocity 200–600 m/s — and named limited array extent as a limitation [1]. Hand placement is what causes it; air deployment removes the cause. Because that ≤2 m accuracy already meets our 2–5 m cell, we claim no gain in point accuracy, only the extent. This is an argument about capability, which is stronger than an argument about cost. Tapping and voice are already the target in doctrine and fielded kit [2, 3, 5, 6], and INACHUS [7] stated the automated-knock-localization goal without a located peer-reviewed accuracy result; we claim neither as new.
* Nobody has characterised sensor coupling onto collapsed debris. All air-deployment work is parameterised by soil strength: drone-landed [8] and air-dropped [9] geophones work in soil, the darts correlating 0.81–0.98 with planted sensors [9]. This project addresses fractured debris at mesh scale instead — a genuine, narrow, measurable gap.
* The negative result is itself a contribution. A bound on cardiac detection through rubble has not been published, while the belief that it might work persists in practitioner literature [21]. Contact-coupled work (HeartQuake [10] with the same SM-24; Jia et al. 2017 [25]; PigV² [26]) recovers ECG or heart rate through centimetres of bedding or slab, not metres of debris, so it is consistent with our bound rather than counter to it: the deficit is path loss, not sensor capability. Sabatier & Ekimov 2008 [11] supplies the signal-equals-noise range bound that is its methodological ancestor.
* **Indian context:** the NDRF Human Life Detector Type-I specification contains no automated-localization requirement at all [5]. That is a capability gap documented in the procuring agency's own words.

**5. *What products (i.e., publications, presentations, performances, outside funding, patents) would you anticipate from this project? (1/2 page)***

* **Journal article 1:** the cardiac seismic detection bound through rubble, a negative result publishable on its own.
* **Journal article 2:** air-deployed array extent on rubble: coverage and BLIND-cell reduction with nobody on the pile, with the false-alarm result.
* **Short measurement paper (possible):** coupling of free-laid and air-dropped geophone nodes onto collapsed debris.
* **Presentations:** near-surface geophysics and search-and-rescue technology venues; Arosio's line of work appears in *Near Surface Geophysics* and at EAGE meetings.
* **Open dataset and code:** debris noise recordings, tap-force and tap-spectrum measurements, coupling transfer functions, node firmware and the detection pipeline.
* **Outside funding:** measured coupling and coverage results are the precondition for a credible NDRF/NDMA-facing or agency proposal. This project is scoped to produce that evidence.
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

**Pricing basis.** Imported parts are converted at Rs. 84/USD (rate of 2026-10-07) with **+33% landed cost** added for basic customs duty, social welfare surcharge and IGST; international freight is not yet included. Prices checked on 2026-10-11: the SM-24 lists at USD 69.95 each from SparkFun (USD 66.45 from 25 units), about Rs. 7,815 landed, 9% above the Rs. 7,140 budgeted; the Indian distributor listing that matched Rs. 7,140 now shows Rs. 11,616. At the direct-import price the shortfall for ten units is about Rs. 6,750, which contingency covers. The tap-force plate is an estimate, not a quote. Every line will be re-quoted, with its date, before purchase.

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

**Regulatory items, including one unfunded cost**

* **Drone.** Importing drones in built-up or kit (CBU/CKD/SKD) form has been prohibited since 9 Feb 2022 [22], so none is bought; the borrowed drone is operated on campus by its registered operator under the Drone Rules, 2021 [23].
* **Radio.** The 865–868 MHz band is licence-exempt only for type-approved equipment [24]. Months 1–4 use a wired array; from month 5 the mesh needs an on-air radio. **WPC Equipment Type Approval is not in this budget.** If the chosen radio module does not already hold it, approval for our own module is estimated at Rs. 1,50,000 (application plus an accredited test-lab report; an estimate, not a quote), 82% of this request. Before purchase, the module's approval is checked against the WPC register. If no approved module fits and the institute has not committed approval funding in writing by month 4, nodes do not transmit: they record locally with timestamps and are read out after each trial. Coverage (RQ1), coupling (RQ2) and false-alarm (RQ4) results are then computed offline; live reporting is not demonstrated, and clock offsets for localization are recovered from a hammer shot at a surveyed point, a method the project would first have to validate.

**REFERENCES**

1. Arosio, D., Longoni, L., Papini, M., Scaioni, M., Zanzi, L., & Alba, M. (2010). A microseismic approach to locate survivors trapped under rubble. Near Surface Geophysics, 8(6), 623–633. doi:10.3997/1873-0604.2010051
2. Federal Emergency Management Agency. US&R Incident Support Team Training Student Manual, Module 3, Unit III: Operations Functional Training. fema.gov/pdf/emergency/usr/mod3\_u3.pdf
3. UK National Fire Chiefs Council. National Operational Guidance: Primary search – unstable or collapsed structure.
4. Macintyre, A. G., Barbera, J. A., & Petinaux, B. P. (2011). Survival interval in earthquake entrapments: research findings reinforced during the 2010 Haiti earthquake response. Disaster Medicine and Public Health Preparedness, 5(1), 13–22. doi:10.1001/dmp.2011.5
5. National Disaster Response Force. Specification: Human Life Detector Type-I (seismic/acoustic), and CSSR equipment schedule. www.ndrf.gov.in
6. Savox. Delsar LifeDetector LD3 datasheet (A02005#B).
7. INACHUS: Technological and methodological solutions for integrated wide area situation awareness and survivor localisation. EU FP7 grant agreement 607522.
8. Stewart, R. R., Chang, L., Sudarshan, S. K. V., Becker, A. T., & Huang, L. (2016). An unmanned aerial vehicle with vibration sensing ability (seismic drone). SEG Technical Program Expanded Abstracts 2016, 225–229. doi:10.1190/segam2016-13973407.1
9. Sudarshan, S. K., Montano, V., Nguyen, A., McClimans, M., Chang, L., Stewart, R. R., & Becker, A. T. (2017). A heterogeneous robotics team for large-scale seismic sensing (SeismicDart). IEEE Robotics and Automation Letters, 2(3), 1328–1335. doi:10.1109/LRA.2017.2666300
10. Park, J., Cho, H., Balan, R. K., & Ko, J. (2020). HeartQuake: accurate low-cost non-invasive ECG monitoring using bed-mounted geophones. Proc. ACM Interactive, Mobile, Wearable and Ubiquitous Technologies, 4(3). doi:10.1145/3411843
11. Sabatier, J. M., & Ekimov, A. E. (2008). Range limitation for seismic footstep detection. Proc. SPIE 6963, 69630V. doi:10.1117/12.785235
12. Ekimov, A., & Sabatier, J. M. (2006). Vibration and sound signatures of human footsteps in buildings. Journal of the Acoustical Society of America, 120(2), 762–768. doi:10.1121/1.2217371
13. Krohn, C. E. (1984). Geophone ground coupling. Geophysics, 49(6), 722–731. doi:10.1190/1.1441700 (Abstract read; full text not yet retrieved.)
14. Starr, I., Rawson, A. J., Schroeder, H. A., & Joseph, N. R. (1939). Studies on the estimation of cardiac output in man … the ballistocardiogram. American Journal of Physiology, 127(1), 1–28. doi:10.1152/ajplegacy.1939.127.1.1
15. Inan, O. T. (2009). Novel technologies for cardiovascular monitoring using ballistocardiography and electrocardiography. PhD dissertation, Stanford University.
16. Ashouri, H., Orlandic, L., & Inan, O. T. (2016). Unobtrusive estimation of cardiac contractility and stroke volume changes using ballistocardiogram measurements on a high bandwidth force plate. Sensors, 16(6), 787. doi:10.3390/s16060787
17. Van Trees, H. L. (1968). Detection, Estimation, and Modulation Theory, Part I. Wiley.
18. Quazi, A. H. (1981). An overview on the time delay estimate in active and passive systems for target localization. IEEE Trans. Acoustics, Speech, and Signal Processing, 29(3), 527–533.
19. Federal Transit Administration (2018). Transit Noise and Vibration Impact Assessment Manual (ground-borne vibration, transfer mobility method).
20. Geospace Technologies. SM-24 geophone element brochure.
21. Donnelly, T. (2010, October 1). Building collapse: rescue operation's technical search capabilities. Fire Engineering.
22. Directorate General of Foreign Trade. Notification prohibiting import of drones in CBU/CKD/SKD form, 9 February 2022.
23. Ministry of Civil Aviation, Government of India. Drone Rules, 2021.
24. Department of Telecommunications (WPC Wing). G.S.R. 853(E), 10 December 2021. Use of Low Power Equipment in the Frequency Band 865–868 MHz for Short Range Devices (Exemption from Licence) Rules, 2021.
25. Jia, Z., Bonde, A., Li, S., Xu, C., Wang, J., Zhang, Y., Howard, R. E., & Zhang, P. (2017). Monitoring a person's heart rate and respiratory rate on a shared bed using geophones. Proc. 15th ACM Conference on Embedded Network Sensor Systems (SenSys '17). doi:10.1145/3131672.3131679
26. Dong, Y., Codling, J. R., Rohrer, G., Miles, J., Sharma, S., Brown-Brandl, T., Zhang, P., & Noh, H. Y. (2022). PigV²: Monitoring pig vital signs through ground vibrations induced by heartbeat and respiration. arXiv:2212.03378

1. Both margins were computed from a footstep anchor read before a 2026-10-08 correction (Section 2C). The corrected anchor raises every computed amplitude by about 6.5 dB, so the tap margins are conservative by that amount and the cardiac deficit is overstated by it; neither conclusion changes. The figures are deliberately left unrevised: they also scale with a tap force that has not been measured, and are recomputed once, from measured inputs, at M4. [↑](#footnote-ref-1)