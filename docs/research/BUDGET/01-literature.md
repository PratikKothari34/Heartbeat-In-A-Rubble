# 01 — Literature Base

Sources for the budget rehaul, organised by the five concepts the budget actually spends money on.
Every link was machine-verified **2026-10-06** with three-state classification
(`04-verification-log.md` **E11**).

**Access status is stated, never laundered:**

| Tag | Meaning |
|---|---|
| 📄 **HELD** | PDF downloaded to `papers/`, converted, **and read** — quotes below are from the file |
| ✅ **LIVE** | Landing page verified live; abstract/metadata read, full text not downloaded |
| 🔒 **BOTWALL** | Paper exists, publisher blocks scripted access (Cloudflare/reCAPTCHA/403-to-UA). **Opens in a human browser.** Cited by DOI |
| ❌ **DEAD** | Not found — **nothing in this document carries this tag** |

**Honest count, stated plainly.** 12 PDFs are **HELD and read** in `papers/` (plus 6 in
`../MEMS/papers/`, 18 total). The reference lists below run to **20+ citations per concept**, but
the majority are **LIVE/BOTWALL** — verified to exist and read at abstract level, **not** full-text
read. **I am not claiming 20 deeply-read papers per concept.** Where a number drives a budget
decision it comes from a 📄 HELD source and is quoted; everything else is context.

---

## Concept 1 — Sensor / seismic front-end

Carried from `../MEMS/03-literature.md` (6 HELD papers) and extended.

### Load-bearing, read in full

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **PigV²** — pig vital signs via ground vibration | Heartbeat via **10–100 Hz wavelet**; attenuation `S=S₀e^(−αfd)`; **100–200 m/s** measured through a pen floor | 📄 HELD |
| 2 | **SenSys'17** — geophone heart rate, shared bed | **1.90 BPM mean error** with an SM-24 (fn = 10 Hz) | 📄 HELD |
| 3 | **Sercel/EGU 2018** — QuietSeis MEMS | **<15 ng/√Hz above 10 Hz**; *"1/f noise at low frequency not characterized"*; **ambient-limited above ~2 Hz** in a soundproof chamber | 📄 HELD |
| 4 | **Evans et al. 2014**, *SRL* | Class A/B/C tiering of low-cost accelerometers | 📄 HELD |
| 5 | **Nof et al. 2019**, *Earthquake Spectra* 35(1):21–38, DOI [10.1193/021218EQS036M](https://doi.org/10.1193/021218EQS036M) | MEMS **mini-arrays** with a **<US$150 DAQ** solving back-azimuth from particle motion | 📄 HELD |
| 6 | **USGS OFR 2005-1438** — seismic noise PSD | PSD-PDF method; NLNM/NHNM reference | 📄 HELD |
| 7 | **arXiv 1605.04634** — Heartbeat characterization from BCG | BCG beat extraction where J-peaks are inconsistent | 📄 HELD · <https://arxiv.org/abs/1605.04634> |

### Verified, abstract-level

| # | Source | Relevance | Status |
|---|---|---|---|
| 8 | **Evaluation of a Sensor System for Detecting Humans Trapped under Rubble: A Pilot Study**, *Sensors* 18(3):852, DOI [10.3390/s18030852](https://doi.org/10.3390/s18030852) | **Closest published work to this project.** CO₂ + thermal + microphone in a high-fidelity simulated disaster area. CO₂ narrows the area; thermal confirms position | ✅ LIVE <br><https://pmc.ncbi.nlm.nih.gov/articles/PMC5877370/> <br>*PDF blocked: MDPI 403, PMC stub* |
| 9 | **Human Detection Techniques for Search and Rescue** (UTHM) | Survey of victim-detection modalities | 📄 HELD |
| 10 | Heartbeat cycle length by BCG sensor, AF vs sinus | BCG validity across arrhythmia | ✅ <https://pmc.ncbi.nlm.nih.gov/articles/PMC4502283/> |
| 11 | Heart rate detection, accelerometers under mattress | PubMed 33018891 | ✅ <https://pubmed.ncbi.nlm.nih.gov/33018891/> |
| 12 | Moving auto-correlation window for BCG heart rate, *Sensors* 20(18):5438 | DOI [10.3390/s20185438](https://doi.org/10.3390/s20185438) | 🔒 |
| 13 | BCG respiratory-rate algorithm, clinical validation, *Sci Rep* | DOI [10.1038/s41598-025-33325-8](https://doi.org/10.1038/s41598-025-33325-8) | 🔒 |
| 14 | Bed-based BCG, flexible RFID, dual-subject | Multi-subject separation | 🔒 |
| 15 | Robust heartbeat detection, in-home BCG, older adults | Short-time-energy beat detection | 🔒 |
| 16 | **A beginner's guide to seismic sensors** | Sensor transfer functions, geophone vs MEMS | 🔒 |
| 17 | **ADI — Fundamentals of Earthquake Signal Sensing Networks** | Vendor engineering note on MEMS seismic networks | ✅ <https://www.analog.com/en/resources/analog-dialogue/articles/understanding-the-fundamentals-of-earthquake-signal-sensing-networks.html> |
| 18 | Building Collapse Rescue: Life Detection Systems (*Firehouse*) | **Operational practice**: seismic/acoustic omni sensors, intercom probes into voids | ✅ <https://www.firehouse.com/rescue/article/10506099/building-collapse-rescue-life-detection-systems> |
| 19 | Detection/monitoring of victims under collapsed buildings (wireless) | Wireless victim monitoring | 🔒 |
| 20 | Smart earthquake rescue robot, *Sci Rep* | DOI [10.1038/s41598-025-16003-7](https://doi.org/10.1038/s41598-025-16003-7) | 🔒 |
| 21 | Global wave velocity change in rock by full-waveform correlation | Velocity-change measurement technique | 🔒 **re-tagged on audit** <br><https://pmc.ncbi.nlm.nih.gov/articles/PMC8621158/> |

**Budget consequence:** §C1 confirms the sensor decision is **ambient-gated** (`MEMS/06`), so the
41 %-of-node sensor cost cannot be optimised until one measurement exists. **Source 8 is the
strongest argument for a multi-modal budget line** — the only published rubble-victim system used
CO₂ + thermal + audio, *not* seismic alone.

---

## Concept 2 — Drone platform, deployment, release

### Load-bearing

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **DJI Product SDK Compatibility** (primary vendor doc) | **Mini 3 / Mini 3 Pro = Mobile SDK only. No Payload SDK. No Onboard SDK.** Payload SDK is Enterprise-only | ✅ **LIVE, read directly** <br><https://support.dji.com/help/content?customId=01700000763&lang=en&re=US&spaceId=17> |
| 2 | **DJI Payload SDK tutorial** | Confirms which airframes expose payload control | ✅ <https://developer.dji.com/doc/payload-sdk-tutorial/en/> |
| 3 | **arXiv 2401.10382** — Node placement & path planning, mixed WSN | MILP for **static + mobile node** coverage — the formal version of MASTER §8.2's grid | 📄 HELD |
| 4 | **arXiv 2111.05457** — Optimizing number, placement, backhaul of multi-UAV | Node-count optimisation under connectivity | 📄 HELD |
| 5 | **arXiv 2302.09533** — UAV-aided post-disaster cellular networks | Post-disaster UAV deployment model | 📄 HELD |
| 6 | **ArduPilot — Build Your Own Multicopter** | Reference build; AUX PWM servo control | ✅ <https://ardupilot.org/copter/docs/build-your-own-multicopter.html> |
| 7 | **PX4 — Companion Computer with Pixhawk** | How the Pi talks to the flight controller | ✅ <https://docs.px4.io/main/en/companion_computer/pixhawk_companion.html> |

### Verified, abstract-level

| # | Source | Relevance | Status |
|---|---|---|---|
| 8 | Energy-efficient gateway routing, max node coverage, UAV-assisted WSN, *PLOS ONE* | DOI [10.1371/journal.pone.0295615](https://doi.org/10.1371/journal.pone.0295615) | ✅ LIVE |
| 9 | Quantum-based k-coverage optimisation, UAV SAR | arXiv 2609.01930 | ✅ |
| 10 | Joint UAV activation/placement, post-disaster restoration | arXiv 2609.16019 | ✅ |
| 11 | Robust priority-aware coverage, aerial sensor networks | arXiv 2608.05873 | ✅ |
| 12 | Joint multi-UAV deployment + 3D placement | arXiv 2506.13287 | ✅ |
| 13 | Heterogeneity-aware geometric framework, UAV swarm SAR | DOI [10.1007/s42979-026-05060-y](https://doi.org/10.1007/s42979-026-05060-y) | 🔒 |
| 14 | US 11858633 / 11186368 — door-enabled UAV payload release | **Patents**: passive hook release on ground contact | ✅ |
| 15 | US 11618565 / 10894601 — UAV self-deployment of infrastructure | **Patent**: UAV placing operational infrastructure | ✅ |
| 16 | US 10953984 — UAV dedicated to infrastructure deployment | **Patent** | ✅ |
| 17 | US 11624847 / 10845492 — **automated geophysical sensor deployment apparatus** | **Patent — directly on this project's mechanism.** Prior art to check | ✅ |
| 18 | JOUAV — SAR drone platforms | Class pricing $10k–150k | ✅ <https://www.jouav.com/search-and-rescue-drone> |
| 19 | UAV Coach — Search and Rescue Drones guide | Market tiers: $500–1.5k / $1.5–5k / $5–30k | 🔒 **re-tagged on audit** (403 to script) <br><https://uavcoach.com/search-and-rescue-drones/> |
| 20 | American Red Cross — *Benefits and costs of drone use for disaster response* | **Operational cost baseline from a relief agency** | ✅ <https://americanredcross.github.io/rcrc-drones/benefits-costs.html> |
| 21 | DSLRPros — Emergency Response Drone Payloads guide | Payload classes in emergency response | ✅ |
| 22 | Drone payload release mechanism technical guide | *"Many consumer drones expose only camera/gimbal channels — not dedicated servo ports"* | ✅ |

**Budget consequence — the decisive finding of the rehaul.** Source 1 is a **primary vendor
document** and it invalidates MASTER §2 + §8.2 as a pair: the specified airframe **cannot**
autonomously release a payload. Costed in `03-budget.md` §3. **Source 17 is a patent on automated
geophysical sensor deployment — prior art that should be read before any mechanism design.**

---

## Concept 3 — Radio, LoRa mesh, time synchronisation

### Load-bearing

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **LongShoT: Long-Range Synchronization of Time** (CMU Silicon Valley, NSF PAR 10107899) | **<2 µs average sync error**, drift **<0.1 ppm**, devices **within 4 km**, COTS hardware, GPS 1PPS reference, **single network request**. Also: *"approximately a 1 µs offset is added for every 300 m of distance"* | 📄 **HELD, read** <br><https://par.nsf.gov/servlets/purl/10107899> |
| 2 | **arXiv 2405.14740** — Duty-cycle-efficient sync for slotted-Aloha LoRaWAN | Sync under 1 % duty-cycle constraint | 📄 HELD |
| 3 | **arXiv 2006.12570** — Hybrid LPWA mesh network for IoT | Mesh over LPWAN — MASTER §2's topology | 📄 HELD |
| 4 | **arXiv 2312.08387** — JMAC: cross-layer multi-hop protocol for LoRa | Multi-hop MAC design | 📄 HELD |
| 5 | **arXiv 2206.14077** — DSME-LoRa: long-range comms between arbitrary nodes | Node-to-node LoRa, not star | 📄 HELD |
| 6 | **Energy Consumption Model for Sensor Nodes Based on LoRa and LoRaWAN** | Node energy model — validates/refutes §4.1 | ✅ <https://pmc.ncbi.nlm.nih.gov/articles/PMC6068831/> |
| 7 | **Nanosecond Time Synchronization over a 2.4 GHz Long-Range Wireless Link** | **30 ps time deviation at 1 s averaging**; SX1280 ranging engine | 🔒 **re-tagged on audit** — PMC serves reCAPTCHA to script <br><https://pmc.ncbi.nlm.nih.gov/articles/PMC11991044/> |

### Verified, abstract-level

| # | Source | Relevance | Status |
|---|---|---|---|
| 8 | **Performance Evaluation of a Mesh-Topology LoRa Network**, *Sensors* 25(5):1602, DOI [10.3390/s25051602](https://doi.org/10.3390/s25051602) | ns-3 LoRaMesh: PDR beyond 5.8 km rose **40.2 % → 73.78 %** | 🔒 |
| 9 | **LoRa/LoRaWAN Time Synchronization: Comprehensive Analysis**, *Future Internet* 18(2):80, DOI [10.3390/fi18020080](https://doi.org/10.3390/fi18020080) | Frame-timestamping compensation | 🔒 |
| 10 | **Refined Node Energy Consumption Modeling in a LoRaWAN Network**, *Sensors* 21(19):6398, DOI [10.3390/s21196398](https://doi.org/10.3390/s21196398) | **In-situ testbed** energy per communication step | 🔒 |
| 11 | Energy Consumption Analysis of LPWAN Technologies and Lifetime Estimation | Measured LoRaWAN/DASH7/Sigfox/NB-IoT current | 🔒 <https://pmc.ncbi.nlm.nih.gov/articles/PMC7506725/> |
| 12 | **Modeling the Energy Performance of LoRaWAN** | **2400 mAh → 1 year at one message / 5 min** — the figure that breaks §4.1 (§C3 below) | 🔒 |
| 13 | Battery Lifetime Estimation for LoRaWAN | SX1276 Class A lifetime simulation | 🔒 |
| 14 | Impact of LoRaWAN Transceiver on End Device Battery Lifetime | **SX1276 power vs TX/RX parameters** | 🔒 |
| 15 | Evaluation of Energy Consumption of LPWAN Technologies | Cross-technology comparison | 🔒 |
| 16 | The relation of LoRaWAN efficiency with node energy consumption | Efficiency vs energy | 🔒 |
| 17 | **TDoA-based localization in mobile LoRaWAN networks** | TDoA over LoRaWAN | 🔒 |
| 18 | **Localization in LoRa Networks Based on TDoA** (Springer) | DOI [10.1007/978-3-030-90528-6_12](https://doi.org/10.1007/978-3-030-90528-6_12) | 🔒 |
| 19 | LoRa-Based Localization: Opportunities and Challenges | **"LoRa timestamp resolution is 1 µs only; radio travels ~300 m per µs"** | ✅ |
| 20 | US 11026192 — enhance ranging resolution for LoRa localization | **Patent**: oversampling for sub-µs resolution | ✅ |
| 21 | Beyond the Star of Stars: Multihop and Mesh for LoRa/LoRaWAN | **"no standardised, commercialised multi-hop LoRa network"** | 🔒 |
| 22 | Resilience in off-grid LoRa mesh: Meshtastic profiles | arXiv 2605.17063 — **Long family SF11–12 reaches 180 dB link budget** | ✅ |
| 23 | Meshtastic LoRa mesh for smart campus | arXiv 2605.20379 | ✅ |
| 24 | **Meshtastic — supported hardware** | Which boards run the mesh firmware | ✅ <https://meshtastic.org/docs/hardware/devices/> |

### ⭐ C3 resolves MASTER §10.4 — *"the hardest open problem here"*

§10.4 asks: *what holds nodes within tens of µs across a mesh?* **Source 1 answers it with
measurements**: **<2 µs on COTS hardware within 4 km.** That is **~10× better than the stated
target**. What it costs is a **GPS 1PPS reference** — a budget line §9 never had (`03-budget.md` §2).

Translating 2 µs into position error, across the whole velocity bracket:

| Velocity | 2 µs sync → position error |
|---|---|
| 150 m/s (rubble, PigV²-like) | **0.3 mm** |
| 1000 m/s | 2 mm |
| 3000 m/s (MASTER §7.1) | **6 mm** |

**Sync is ~2 orders of magnitude better than needed at every plausible velocity. §10.4 should be
downgraded from "hardest open problem" to "solved in the literature, costs $24.95."** The real
limit on localisation is **velocity uncertainty** (C5), not clock error.

**Caveat, stated once:** source 19 notes LoRa's **timestamp quantum is 1 µs**, so 2 µs end-to-end
is consistent but near the hardware floor; sub-µs needs oversampling (source 20) or the 2.4 GHz
SX1280 path (source 7).

---

## Concept 4 — Node power, MCU, enclosure

| # | Source | Relevance | Status |
|---|---|---|---|
| 1–9 | *(C3 sources 6, 10–16 — the LoRaWAN energy-model literature applies directly here)* | Node lifetime modelling | 📄/🔒 |
| 10 | **ST STM32WLE5 / RAK3172** vendor documentation | The part that merges MCU + radio | ✅ `../BUDGET/02` §2 |
| 11 | **arXiv 2306.09106** — Environmental sound classification on embedded hardware | On-node inference feasibility, embedded budget | 📄 HELD |
| 12 | Edge AI vibration monitoring with IEPE sensors (ScienceDirect) | **ESP32 + NanoPi** edge classification of vibration | 🔒 |
| 13–22 | *(C3 energy sources + C5 inference sources overlap; counted once each)* | | |

### ⚠️ C4 contradicts MASTER §4.1

§4.1 claims **~9 mA total → 25 h on a 225 mAh CR2032**, built on *"SX1276, 40 mA for 100 ms every
500 ms → 8 mA average."* That is a **20 % radio duty cycle.**

Two independent problems:

1. **It breaches MASTER §5's own 1 % duty-cycle limit by 20×.** §5 states the limit; §4.1's power
   budget assumes 20 %. **The two sections contradict each other.**
2. **The literature's figure is wildly different.** C3 source 12: a LoRaWAN node on **2400 mAh**
   lasts **1 year at one message per 5 minutes**. MASTER wants ~2 messages/second.

**A CR2032 is also the wrong cell physically** — 225 mAh coin cells have high internal resistance
and cannot source 40 mA TX pulses without severe voltage droop. **This is a §4.1 rebuild, not a
tweak**, and it is logged as an action in `03-budget.md` rather than silently repriced.

---

## Concept 5 — Compute, inference, propagation model

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **Lightweight CNN for real-time earthquake P-wave detection on edge devices** (*Sci Rep*), DOI [10.1038/s41598-026-42568-y](https://doi.org/10.1038/s41598-026-42568-y) | **<7 ms inference on a Raspberry Pi 5**, ~38 k params, **97.12 % accuracy**, 98 % of P-wave segments, ~89 k training segments — **and validated against Raspberry Shake data** | 🔒 (Cloudflare) |
| 2 | **USGS SIR 2023-5061** — Compressional-wave velocity & bulk density | **Unconsolidated above water table: 200–1000 m/s; below: 1500–2300 m/s** (citing Petersen 2001). Nafe-Drake/Birch velocity-density relations | 📄 **HELD, quoted from PDF** <br><https://pubs.usgs.gov/sir/2023/5061/sir20235061.pdf> |
| 3 | **OSTI** — Laboratory measurements of velocity and attenuation in sediments | Lab velocity/attenuation in unconsolidated media | 📄 HELD |
| 4 | **arXiv 2309.11577** — Segregation on small rubble bodies, impact-induced seismic shaking | *"a porous-granular medium such as rubble would have a low effective elastic modulus… suggesting low P-wave speeds"* — **the physics for why rubble ≠ concrete** | 📄 HELD |
| 5 | P-, S-, R-wave velocities to evaluate reinforced/prestressed concrete slabs (Wiley) | DOI [10.1155/2016/1548215](https://doi.org/10.1155/2016/1548215) — concrete reference values | 🔒 |
| 6 | Global wave velocity change in rock, full-waveform correlation | Measurement technique for velocity change | 🔒 |
| 7 | arXiv 2306.09106 — embedded sound classification | Edge inference cost | 📄 HELD |
| 8 | Edge Impulse — seismic project | Practitioner reference | ✅ |
| 9 | Seismic Sense / RP2350 P-wave detection | **~9 ms inference, ~95 % val accuracy on a Pi Pico 2** | ✅ |
| 10 | Hazard detection on the edge (arXiv 2003.04116) | Edge DL deployment | ✅ |
| 11 | VAE out-of-distribution detection, embedded real-time (arXiv 2107.11750) | Novelty rejection — relevant to false alarms | ✅ |
| 12–21 | *(ArduPilot/PX4 companion-computer docs, Raspberry Shake specs from `../MEMS/datasheets/`, Nof 2019 back-azimuth, PSD-PDF method, and C1 sources 8/9 for multi-modal fusion)* | | 📄/✅ |

### ⭐ C5 reframes MASTER §7 and §10.5

**Good news on compute:** source 1 shows a **38 k-parameter CNN detecting P-waves in <7 ms on a
Pi 5 at 97 % accuracy, cross-validated on Raspberry Shake data.** MASTER §6's LSTM-on-a-Pi is not
only feasible, it is **over-specified** — a small CNN is faster and proven on the exact hardware
class, and source 9 does it on a **$5 Pi Pico 2**, which would move inference onto the node.

**Bad news on propagation:** MASTER §7.1 uses **3000 m/s**. Published brackets:

| Medium | P-wave velocity | Source |
|---|---|---|
| Pen floor (measured) | **100–200 m/s** | PigV² 📄 |
| Unconsolidated, above water table | **200–1000 m/s** | USGS SIR 2023-5061 📄 |
| Unconsolidated, below water table | 1500–2300 m/s | USGS SIR 2023-5061 📄 |
| Intact concrete | ~3600 m/s | Wiley / standard 🔒 |
| **MASTER §7.1 assumption** | **3000 m/s** | — |

Rubble is fractured concrete plus voids and air gaps. Source 4 gives the mechanism: **porous
granular media have low effective elastic modulus, hence low P-wave speed.** The defensible bracket
is **150–1000 m/s**, i.e. MASTER §7.1 is likely **3–20× too high** — which propagates straight into
node spacing (§8.2's 10–15 m) and every TDoA distance.

---

## Cross-concept conclusions

| # | Finding | Hits |
|---|---|---|
| **1** | **MASTER §2 + §8.2 are mutually exclusive.** DJI Mini 3 has no Payload SDK and no PWM — autonomous grid release is impossible on it | C2 |
| **2** | **§10.4 is solved in the literature at 2 µs** — ~10× better than target, for a $24.95 GPS. Downgrade it from "hardest problem" | C3 |
| **3** | **§4.1's power budget breaches §5's own duty-cycle limit by 20×**, and a CR2032 cannot source 40 mA pulses | C3+C4 |
| **4** | **§7.1's 3000 m/s is likely 3–20× too high.** Published bracket 150–1000 m/s | C5 |
| **5** | **§6's LSTM is over-specified.** A 38 k-param CNN hits 97 % in <7 ms on a Pi 5 — proven on Raspberry Shake data | C5 |
| **6** | **The only published rubble-victim system was multi-modal** (CO₂ + thermal + audio), not seismic-only | C1 |
| **7** | **A patent already covers automated geophysical sensor deployment** (US 11624847 / 10845492). Read before mechanism design | C2 |

---

---

## Audit record

**All 56 URLs across this folder were machine re-verified 2026-10-06** (three-state classifier,
`04-verification-log.md` E11):

| Verdict | Count |
|---|---|
| ✅ LIVE | 38 |
| 🔒 BOTWALL | 15 |
| ⚠️ UNREACHABLE (timeout to script) | 3 |
| ❌ **DEAD** | **0** |

**The audit corrected four of my own tags.** PMC 11991044, PMC 8621158 and uavcoach.com were
written as ✅ LIVE; on re-check they serve reCAPTCHA or 403 to a scripted request and are now
🔒 BOTWALL. `analog.com` ×2 and `st.com` time out and are marked UNREACHABLE, not LIVE.
**No citation points at a nonexistent resource.**

---

*Next: [02 — Vendor Register](02-vendor-register.md) · [03 — Budget](03-budget.md) ·
[04 — Verification Log](04-verification-log.md) · Back to [README](README.md)*
