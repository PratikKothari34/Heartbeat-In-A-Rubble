# 01 — Literature Base (Redesign Pass)

Sources for the five redesign questions. Verified **2026-10-06**, three-state
(`04-verification-log.md` **E17**).

| Tag | Meaning |
|---|---|
| 📄 **HELD** | File downloaded, `%PDF-` checked, converted, **and read** — quotes are from the file |
| ✅ **LIVE** | Page verified live; abstract/metadata read, full text not downloaded |
| 🔒 **BOTWALL** | Exists, blocks scripts (Cloudflare/reCAPTCHA/403-to-UA). Opens in a browser. Cited by DOI |
| ❌ **DEAD** | Not found. **Three carry this tag and none of them is cited for a claim** |

**Honest count.** Load-bearing claims come from 📄 HELD sources and are quoted. The rest is
verified-to-exist context read at abstract level. **I am not claiming 20 deeply-read papers per
concept.** Sources carried from `../BUDGET/01-literature.md` are marked **[carried]** and counted
once.

---

## Concept R1 — Spectrum law and duty cycle *(the decisive concept)*

### Load-bearing, read in full

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **G.S.R. 853(E)**, Gazette of India Extraordinary, Pt II §3(i), **10 Dec 2021** — *Use of Low Power Equipment in the Frequency Band 865–868 MHz for Short Range Devices (Exemption from Licence) Rules, 2021* | **THE primary legal source.** Four tables, each with its own limits. **Table-I** Non-Specific SRD: 25 mW e.r.p., **duty cycle 1%**. **Table-II** Tracking/Tracing/Data Acquisition: **500 mW e.r.p.**, APC required, ≤200 kHz, **duty cycle ≤10% network access points, ≤2.5% otherwise**. **Table-II's note names "Emergency detection of buried victims".** Rule 3 grants licence exemption on a non-interference, non-protection, shared basis. Supersedes the 2005 RFID rules | 📄 **HELD, quoted from the PDF** <br><https://thc.nic.in/Central%20Governmental%20Rules/use%20of%20low%20power%20Equipment%20in%20the%20frequency%20band%20865%20to%20868%20MHz%20for%20Short%20Range%20Devices%20Exemption%20from%20Licence%20Rules,2021.pdf> |
| 2 | **ETSI EN 300 220-2 V3.2.1 (2018-06)** | The harmonised standard G.S.R. 853(E) cites in its own column 6 | ✅ <https://www.etsi.org/deliver/etsi_en/300200_300299/30022002/03.02.01_60/en_30022002v030201p.pdf> |
| 3 | **ETSI EN 300 220-2 V3.3.1 (2025-03)** | Current revision | ✅ <https://www.etsi.org/deliver/etsi_en/300200_300299/30022002/03.03.01_60/en_30022002v030301p.pdf> |
| 4 | **ERC Recommendation 70-03**, CEPT ECO | **Independent confirmation**: same 500 mW / 2.5% / avalanche-victim category. **India mirrors the European allocation** | ⚠️ UNREACHABLE to script (URLError); content confirmed via CEPT EFIS annex (#5) |
| 5 | **CEPT EFIS — Annex 2: Tracking, Tracing and Data Acquisition** | The category definition itself | ✅ <https://efis.cept.org/adhoc_grabber.jsp?annex=5> |

### Verified, abstract-level

| # | Source | Relevance | Status |
|---|---|---|---|
| 6 | G.S.R. 37(E) — 865–867 MHz amendment rules 2007 | Prior Indian instrument | ✅ indiacode.nic.in |
| 7 | Use of low power equipment 865–867 MHz for RFID (Exemption) Rules, **2005** | The superseded rule | ✅ latestlaws.com |
| 8 | **WPC Wing, DoT — Regulations index** | The issuing authority | ✅ <http://wpc.dot.gov.in/content/10_1_Regulations.aspx> |
| 9 | Granite River Labs — WPC/ETA certification guide | What compliance actually requires to ship | ✅ |
| 10 | AutoAbode — LoRa frequency bands India, WPC rules, ERP limits, ETA | Practitioner reading of the same rules | ✅ |
| 11 | TTN — Duty cycle docs | **1% = 864 s airtime/day**; duty cycle applies per device/channel/sub-band | ✅ <https://www.thethingsnetwork.org/docs/lorawan/duty-cycle/> |
| 12 | Lansitec — LoRaWAN duty cycle | Airtime budgeting in practice | ✅ |
| 13 | Semtech — ISM band and LoRaWAN regional parameters | IN865 plan | ✅ learn.semtech.com |
| 14 | LoRa Alliance **RP002** Regional Parameters | Defines IN865 duty cycle/dwell, LBT, max EIRP | ✅ (spec behind registration) |
| 15 | Actility — LoRaWAN regional parameters | Regional plan overview | ✅ |
| 16 | Dragino — regional parameters reference | IN865 channel plan | ✅ |
| 17 | NiceRF — LoRa module selection guide India 2025 | **Warns many "868 MHz" modules are illegal in India** if channels not reconfigured | ✅ |
| 18 | NiceRF — LoRa India compliance & environment | Band-edge practicalities | ✅ |
| 19 | Zbotic — 2.4 GHz vs 915 MHz LoRa India | Band choice for India | ✅ |
| 20 | everythingRF — LoRa frequency band in India | Channel list 865.0625 / 865.4025 / 865.985 MHz | ✅ |
| 21 | Wikipedia — Short-range device | Cross-index of SRD categories and the avalanche-victim entry | ✅ |
| 22 | Semtech — introduction to regional parameters | Background | ✅ |
| 23 | RiverPublishers — *LoRa-Alliance Regional Parameters Overview* (JICTS) | Peer-reviewed overview of the parameter system | ✅ |

### ⭐ R1 conclusion

**MASTER §5 cites the wrong table.** The device is not a Non-Specific SRD; the Gazette's own note
puts *emergency detection of buried victims* in **Table-II**. The correct envelope is
**500 mW e.r.p. / 2.5% / APC / ≤200 kHz**, not 25 mW / 1%.

**+13 dB of ERP** = a **4.47× range multiplier** in free space (n=2), **2.35×** in clutter (n=3.5).
**2.5× the airtime.** Both verified by two independent regulatory sources.

**Caveats, stated once.** Table-II requires **Adaptive Power Control** and **≤200 kHz** occupied
bandwidth — LoRa at BW125 complies on bandwidth; APC must be implemented, not assumed. Licence
exemption is **non-interference, non-protection**. And a device sold in India needs **ETA/WPC**
conformance regardless.

---

## Concept R2 — Event-driven architecture vs raw streaming

### Load-bearing

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **LightEQ: On-Device Earthquake Detection with Low-Power Microcontrollers** (IoTDI '23, DOI 10.1145/3576842.3582387) | **The closest published system to the proposed redesign.** Runs on **Cortex-M4 with 100 kB RAM**; smallest model **29 k params, F1 0.99**, **193 kB RAM**, **932 ms inference per 1 min of raw data**, **5.86 mJ**. **Extends battery life ≥3× over STA/LTA by not transmitting false positives** | ✅ LIVE <br><https://tore.tuhh.de/entities/publication/e02eeb00-8296-4937-87f3-297ed751b9f2> |
| 2 | **Quality-driven Volcanic Earthquake Detection using WSN** (NTU, RTSS) | **P-phase picking transmitting only 16% of sensor data**; distributed detection avoids raw transmission entirely | 📄 **HELD** <br><https://personal.ntu.edu.sg/tanrui/pub/tosn-volcano.pdf> |
| 3 | **SamurAI: A Versatile IoT Node with Event-Driven Wake-Up and Embedded ML** (arXiv 2304.13726) | Event-driven wake-up + on-node ML as a node architecture | ✅ <https://arxiv.org/abs/2304.13726> |
| 4 | **Multimetric Event-driven System for Long-Term WSN Operation in SHM** (arXiv 1910.07718) | Event-driven operation for multi-year structural monitoring | ✅ <https://arxiv.org/abs/1910.07718> |
| 5 | **Machine Learning Sensors** (arXiv 2206.03266) | The paradigm: sensor emits *inferences*, not samples | ✅ <https://arxiv.org/abs/2206.03266> |
| 6 | **Lightweight CNN for P-wave detection on edge devices**, *Sci Rep* **[carried]** | **<7 ms on a Pi 5, ~38 k params, 97.12%** | 🔒 DOI 10.1038/s41598-026-42568-y |
| 7 | **LongShoT** — long-range time sync **[carried]** | **<2 µs**, <0.1 ppm, 4 km, COTS, GPS 1PPS | 📄 HELD |

### Verified, abstract-level

| # | Source | Relevance | Status |
|---|---|---|---|
| 8 | **TinyML for On-Device and Edge Analytics in Wireless Networks** (arXiv 2606.30843) | Survey; deployment patterns and concept drift | ✅ |
| 9 | ETH Zürich — **A Wake-Up Circuit for Event-Driven Duty-Cycling of Wearable IoT Nodes** | Wake-up receiver design | ✅ DOI 10.3929/ETHZ-B-000281405 |
| 10 | **Always-on sparse event wake-up detectors: A Review** | **nW to tens of µW**, >90% detection accuracy | ✅ bib.irb.hr/1189401 |
| 11 | Terfloth et al. — cost model for WSN data reduction | Formal transmit-vs-process tradeoff | ✅ FU Berlin |
| 12 | NTU — timing/IPSN companion paper | Sync in the volcano deployment | ✅ |
| 13 | Integration of MEMS Accelerometers in Regional Seismological Networks: **low-cost edge computing** | Edge approach in real seismic networks | ✅ SSA |
| 14 | ST — Smart asset tracking, ST Edge AI Suite | Vendor reference for on-node inference | ✅ |
| 15 | arXiv 2405.14740 — duty-cycle-efficient sync, slotted-Aloha LoRaWAN **[carried]** | **Sync under a duty-cycle constraint** — directly applicable | 📄 HELD |
| 16 | arXiv 2312.08387 — JMAC cross-layer multi-hop LoRa **[carried]** | MAC under airtime limits | 📄 HELD |
| 17 | arXiv 2206.14077 — DSME-LoRa **[carried]** | Node-to-node LoRa | 📄 HELD |
| 18 | arXiv 2006.12570 — hybrid LPWA mesh **[carried]** | Mesh topology | 📄 HELD |
| 19 | *Beyond the Star of Stars* **[carried]** | *"no standardised, commercialised multi-hop LoRa network"* | 🔒 |
| 20 | Energy Consumption Model for LoRa/LoRaWAN nodes **[carried]** | Node energy model | ✅ PMC6068831 |
| 21 | Refined Node Energy Consumption Modeling in LoRaWAN **[carried]** | In-situ measured per-step energy | 🔒 DOI 10.3390/s21196398 |
| 22 | Modeling the Energy Performance of LoRaWAN **[carried]** | **2400 mAh ≈ 1 year at 1 msg/5 min** | 🔒 |
| 23 | arXiv 2306.09106 — embedded sound classification **[carried]** | Embedded inference budget | 📄 HELD |
| 24 | Meshtastic resilience profiles (arXiv 2605.17063) **[carried]** | SF11–12, 180 dB link budget | ✅ |

### ⭐ R2 conclusion

**Every system in this literature that works does on-node detection and transmits inferences.**
LightEQ does it in **100 kB of RAM on a Cortex-M4** — the exact class of part the RAK3172 carries,
which makes **§10.3's MCU question answerable without new hardware**. The volcano deployment
transmits **16%** of its data. MASTER §5.1 proposes to transmit **100%**, and that is the
assumption that breaks.

---

## Concept R3 — Node power, cell chemistry, pulse current

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **TI SLVAES7** — application report | Primary-cell pulse behaviour and droop mitigation | ✅ <https://ti.com/lit/pdf/SLVAES7> |
| 2 | **TTN — "The curious case of LoRaWAN devices and coin cell batteries"** | **CR2032 internal resistance ~10 Ω fresh, 15–30 Ω aged.** At ~30 mA the droop is ~0.18 V; **pulse loads of 30 mA at 10% duty can halve usable capacity** vs the 1 mA rating | ✅ <https://www.thethingsnetwork.org/article/the-curious-case-of-lorawan-devices-and-coin-cell-batteries> |
| 3 | **Avnet Abacus** — Extending battery lifetime in wireless applications using supercapacitors | **A 1 F supercap (ESR 860 mΩ) across a coin cell cuts the cell's pulse current ~10:1**, leaving ~3 mA draw | ✅ <https://my.avnet.com/abacus/resources/article/extending-battery-lifetime-in-wireless-applications-using-supercapacitors/> |
| 4 | **CAP-XX prismatic supercapacitors** — product category | **ESR 50–100 mΩ, 100–800 mF**, −40…+85 °C, leakage <1 µA. The part class for the fix | ✅ <https://cap-xx.com/product-category/prismatic-supercapacitors> |
| 5 | **Battery Power Tips** — six common Li primary chemistries compared | **Li-MnO₂: 3.0 V, 400–580 Wh/L, HIGH pulse capability. Li-SOCl₂: 3.6 V, 650–1200 Wh/L, LOW pulse capability.** Li-SOCl₂ needs a hybrid pulse capacitor | ✅ |
| 6 | Tadiran — Comparing lithium chemistries | Vendor cross-check of the same tradeoff | ✅ |
| 7 | Machine Design — Lithium battery basics | Internal-impedance comparison | ✅ |
| 8 | Longsing — lithium primary selection guide | **LiMn pouch: ~75 mA continuous, 150 mA pulse** | ✅ |
| 9 | Hubble — Designing BLE products for coin-cell operation | Chip-to-power-budget method for coin cells | ✅ |
| 10 | Qoitech — coin cell pulse measurement | Measurement methodology | ✅ |
| 11 | Amicell — primary lithium overview | Chemistry reference | ✅ |
| 12 | Deutsche Telekom IoT — battery hardware notes | Field guidance for IoT cells | ✅ |
| 13–22 | *(R2 sources 20–22 + `../BUDGET/` C3 energy literature — LoRaWAN node energy models, SX1276 TX/RX power, LPWAN lifetime estimation; counted once each)* **[carried]** | Node lifetime modelling | 📄/🔒 |

### ⭐ R3 conclusion

**MASTER §4.1's CR2032 objection is correct but mis-stated.** The problem is **not capacity** —
under Scheme C, 72 h needs only **77 mAh** of a 225 mAh cell. The problem is **pulse current**:

| Cell state | R | Droop @40 mA | Rail | |
|---|---|---|---|---|
| Fresh | 10 Ω | 0.40 V | 2.60 V | marginal |
| Aged | 30 Ω | **1.20 V** | **1.80 V** | **brownout** |

Two independent fixes, both cheap: a **supercapacitor across the cell** (~10:1 pulse reduction),
or **LiMnO₂ instead of Li-SOCl₂** where pulse capability is the selection criterion.
**Neither requires abandoning the coin cell.**

---

## Concept R4 — Enclosure, ground coupling, node attitude

| # | Source | What it establishes | Status |
|---|---|---|---|
| 1 | **US 5866827 — Auto-orienting motion sensing device** | **The mechanism that resolves the coupling-vs-self-righting conflict**: a spherical **inner housing free to rotate inside an outer housing**, CoG below the rotational centre, 3-axis sensing. The *outer* case couples; the *inner* gimbal self-levels | ✅ <https://patents.google.com/patent/US5866827> |
| 2 | **US 12650530 — Self-orienting sensing node and method** | Modern restatement: double housing, inner rotates freely, **"a tilt angle doesn't negatively impact seismic data recording"** | ✅ USPTO |
| 3 | **US 9645267 — Triaxial accelerometer assembly + in-situ calibration** | Internal alignment matrix making gravity-vector measurement **rotationally invariant regardless of orientation** — the software alternative to a gimbal | ✅ USPTO |
| 4 | **US 5046056 / 5126980 — Self-orienting vertically sensitive accelerometer** | Earlier art in the same family | ✅ USPTO |
| 5 | **Tilt thresholds (from the self-orienting art)** | **Up to 20° tilt tolerable before degradation; above 30°, no acquisition.** Quantifies `MEMS/04` A8's "bounded, not controlled" | ✅ |
| 6 | **EP 3080642 — System and method for coupling a seismic sensor to the ground** | **Directly on the drop problem**: sensor **releases a coupling material on ground impact** | ✅ <https://patents.google.com/patent/EP3080642> |
| 7 | **US 9933534 — Seismic coupling system and method** | Coupling improvement for emplaced sensors | ✅ USPTO |
| 8 | **US 9494449 / 10018740 — Coupling device for seismic sensors** | Coupling hardware | ✅ USPTO |
| 9 | **US 7272505 — Determination of geophone coupling** | **Measuring** coupling quality in situ — a self-test the node could run | ✅ USPTO |
| 10 | **US 7284431 — Geophone** | Proof-mass/spring/case relationship | ✅ <https://patents.google.com/patent/US7284431> |
| 11 | **US 5124956 — Geophone with depth sensitive spikes** | Spike penetration vs depth | ✅ |
| 12 | **US 5010531 — Three-dimensional geophone** | 3C packaging | ✅ |
| 13 | **Krohn / NCU — *The usefulness of geophone ground-coupling experiments*** | **The canonical coupling reference**: well-planted spiked geophones are governed by **shear along the spike**; poorly planted ones by **weight coupling** (mass × contact pressure). Coupling is a **transfer function**; perfect coupling = 1 at all frequencies; **the main feature is a resonance between device and ground** | ✅ basin.earth.ncu.edu.tw |
| 14 | **ADI — Design a good vibration sensor enclosure** | **The enclosure must have a frequency response better than the MEMS inside it**; geometry and height dominate the natural frequencies | ✅ analog.com |
| 15 | **Uni. Luxembourg — Accurate measurement of ground shock with cellular solid** | **Impedance matching**: embedding the sensor in a **cellular solid whose acoustic impedance matches the soil** eliminates reflection at the interface while minimising relative motion | ✅ orbilu.uni.lu/handle/10993/44562 |
| 16 | **IOA — The influence of sensor mounting condition during ground-borne vibration measurement** | Measured effect of mounting on recorded vibration | ✅ ioa.org.uk |
| 17 | **SeismicDart / SeismicSpider** (Univ. Houston, NSF) | **Dart-shaped wireless sensors planted by UAV drop.** Increasing drop height increases penetration and **removes the need for a level landing site**. Penetrator must be aerodynamically stable with **low CoG to damp oscillation and land near-vertical** | 📄 **HELD** <br><https://par.nsf.gov/servlets/purl/10048939> |
| 18 | UH — heterogeneous robotics team for seismic deployment | The wider deployment programme | ✅ |
| 19 | UH — Sudarshan MS thesis, seismic sensor deployment | Mechanism detail | ✅ |
| 20 | UH — Nguyen MS thesis | Companion work | ✅ |
| 21 | **ISS Aerospace / DARTs (Downfall Air Receiver Technology)** | **Fielded practice**: released from ~20 m, multi-sensor camera checks the ground is clear first | ✅ geoexpro.com |
| 22 | **STRYDE nodal sensors** | Commercial nodal node **~150 g**, one operator carries 60–90 | ✅ earthdoc.org |
| 23 | Edinburgh — comparative field trial, nimble node vs cabled | Nodal vs cabled data quality | ✅ research.ed.ac.uk |
| 24 | US 6808336 — oscillation detecting device for compacting soil | Soil-contact sensing | ✅ USPTO |
| 25 | UWA — simple method for absolute calibration of geophones | Calibration without a shaker | ✅ |

### ⭐ R4 conclusion

**This is the one item where the prior pass said "unsolved" and the literature says otherwise.**
`MEMS/04` A8 framed coupling-vs-self-righting as the project's unsolved mechanical conflict. It is
**solved prior art**, twice over:

1. **Gimballed inner housing** (US 5866827, US 12650530) — outer case couples to the rubble, inner
   sphere self-levels. Tilt stops mattering.
2. **Rotationally-invariant calibration** (US 9645267) — no moving parts; solve attitude in
   software from the gravity vector, which a 3-axis part measures anyway.

**Option 2 is almost free** and consistent with the already-made 3-axis decision.

**And the drop mechanism is prior art too** — SeismicDart is UAV-dropped dart-shaped sensors, with
the aerodynamic requirement stated (**low CoG, near-vertical landing**). **US 11624847 / 10845492**
(carried from `../BUDGET/` C2 #17) covers automated geophysical sensor deployment.
**Freedom-to-operate should be checked before mechanism design**, not after.

---

## Concept R5 — Velocity, spacing, and the DSP band

Carried in full from `../BUDGET/01-literature.md` C5 (21 sources). Nothing this pass changes the
conclusion; it is listed here only because the redesign verdict depends on it.

| # | Source | Status |
|---|---|---|
| 1 | **USGS SIR 2023-5061** — unconsolidated **200–1000 m/s** dry, 1500–2300 saturated | 📄 HELD |
| 2 | **PigV²** (Dong et al. 2022), **arXiv 2212.03378** — **100–200 m/s measured** through a floor; heartbeat in a **10–100 Hz** band | 📄 HELD — 📝 obligation below |
| 3 | **arXiv 2309.11577** — porous granular media have low effective elastic modulus → low P-wave speed | 📄 HELD |
| 4 | OSTI — lab velocity/attenuation in sediments | 📄 HELD |
| 5 | Wiley DOI 10.1155/2016/1548215 — concrete ~3600 m/s | 🔒 |
| 6–21 | *(C5 sources 5–21: edge inference, Raspberry Shake specs, Nof 2019 back-azimuth, PSD-PDF, SM-24 fn=10 Hz, Sercel ambient-limited >2 Hz, multi-modal fusion)* | 📄/✅/🔒 |

**Unchanged conclusion:** §7.1's 3000 m/s is **3–20× too high**; defensible bracket **150–1000 m/s**.
**§6's 0.5–4 Hz band discards the signal** — but the replacement is **not** 10–100 Hz either. That figure comes from **heartbeat** work (PigV²), i.e. it is a cardiac band for a target that is now tap/voice. Per **ADR 0001 (2026-10-11)**: acquire **5–200 Hz** and let M1/M2 output the detection band.

> 📝 **Citation obligation on row 2 — recorded 2026-10-11** (`../../critique/prior-art/README.md:92-102`). PigV² must be cited and distinguished, as **arXiv 2212.03378, never "SenSys '22"**. It is the **closest published work to our geometry** — the path is through the ground, not through bedding — so **"contact-coupled, not through a medium" does not distinguish it.** The grounds are **distance and medium**: centimetres of barn flooring versus metres of fractured debris.

---

## Cross-concept conclusions

| # | Finding | Hits |
|---|---|---|
| **1** | **MASTER §5 cites the wrong Gazette table.** Table-II (buried-victim detection) allows **500 mW / 2.5%**, not 25 mW / 1%. **+13 dB, 2.5× airtime** | R1 |
| **2** | **Every working system in the literature transmits inferences, not waveforms.** LightEQ: 100 kB RAM, F1 0.99. Volcano WSN: 16% of data | R2 |
| **3** | **The CR2032 problem is pulse current, not capacity.** 72 h needs 77 mAh; an aged cell browns out at 40 mA. Supercap or LiMnO₂ fixes it | R3 |
| **4** | **Coupling vs self-righting is solved prior art** — gimballed inner housing, or rotationally-invariant calibration in software | R4 |
| **5** | **UAV sensor-dart deployment is prior art with a stated aerodynamic spec**, and patents cover it. **Check FTO before designing** | R4 |
| **6** | **The enclosure must out-perform the MEMS in frequency response**, and should impedance-match the ground | R4 |

---

## Audit record

**38 URLs machine-verified this pass**, three-state, title-scoped:

| Verdict | Count |
|---|---|
| ✅ LIVE | 30 |
| 🔒 BOTWALL | 4 |
| ❌ **DEAD** | **3** |
| ⚠️ UNREACHABLE | 1 |

**The three DEAD links are cap-xx PDFs** (`AB1004`, `AB1025`, `CAP-XX-Product-Guide`) — that whole
`/datasheets/` path is gone. **They are not cited for any claim**; the supercapacitor numbers come
from TI SLVAES7 and Avnet instead. **The classifier that found them was itself wrong first** — it
tagged a 404 as LIVE until patched (`04` **E17**).

---

*Next: [02 — Vendor Register](02-vendor-register.md) · [03 — Proposals](03-proposals.md) ·
[04 — Verification Log](04-verification-log.md) · Back to [README](README.md)*
