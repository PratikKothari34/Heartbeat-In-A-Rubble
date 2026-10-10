# 05 — Verification Log (two audit passes per finding)

Per the standing instruction: *"Audit each finding 2 times to verify if you are not hallucinating."*

**Method.** Pass 1 = read the number out of the primary artefact on disk (datasheet/paper PDF
converted with markitdown, spec table read directly — never a search-result summary).
Pass 2 = independent confirmation from a different artefact, a live vendor page payload, or a
re-read of the primary with a different extraction. Anything that survives only one pass is tagged
**[UNVERIF]** wherever it appears, and is not used to support a conclusion.

---

## A. Specification claims

| # | Claim | Pass 1 | Pass 2 | Result |
|---|---|---|---|---|
| A1 | ADXL355 noise = **25 µg/√Hz** | ADI datasheet spec table, `extracts/adxl355.md` | Re-grepped the same table independently; also compared against MDPI *Sensors* 2025 (22.5) | ✅ **Confirmed 25.** Discrepancy D1 below |
| A2 | ADXL355 = **200 µA** meas / 160 µA LDO-off / 21 µA standby | ADI datasheet power table | Cross-read against EVAL-ADXL355-PMDZ user guide | ✅ Confirmed |
| A3 | ADXL355 = 20-bit, 3.9 µg/LSB, LCC 6×6×2.1 mm | ADI datasheet | Package drawing section, same PDF | ✅ Confirmed |
| A4 | Epson M-A352AD10 = **0.2 µG/√Hz @0.5–6 Hz** | Epson datasheet rev 2025-10-23 spec table | Re-read; **then a third time** against the M-A352 brief sheet (`Noise density +25 °C, Avg, f = 0.5 Hz to 6 Hz — 0.2 / 0.7 µG/√Hz rms`) and Epson's own lineup table | ✅ **Triple-confirmed** — and this qualifier is what makes it unique |
| A5 | Epson M-A352 = 48×24×16 mm, 25 g, 1,000 G shock | Epson datasheet | Lineup table + brief sheet agree | ✅ Confirmed |
| A5b | Epson M-A352 supply current | Lineup table: **13.2 mA @3.3 V** | Brief sheet: **20 mA typ at ODR 200 Hz** | ⚠️ **Mode-dependent — both true.** See D6 |
| A15 | **Epson M-A370AD10 = 0.02 µG/√Hz typ / 0.04 max @ 1–10 Hz** | Epson lineup table (`0.02 (1 to 10Hz)`) | Brief sheet spec table, downloaded independently: `Noise Density 25 °C, Average, f = 1 Hz ~ 10 Hz — 0.02 / 0.04 µG/√Hz, rms` | ✅ **Confirmed twice, two documents** |
| A16 | M-A370 = ±10 G / 170 dB, 0.06 µG/LSB, DC–210 Hz, ODR 50–1000 Hz, **36.3 mA**, 29 g, 500 G shock, GNSS 1 PPS | Brief sheet spec table | Lineup table agrees on size, weight, current, axis count, frequency response | ✅ Confirmed |
| A17 | M-A552AC10/AR10 = 0.5 µG/√Hz @0.5–6 Hz, IP67, 65×60×30 mm, 128 g, 35/40 mA @12 V, 9–32 V | Epson lineup table | Brief sheets downloaded (`Epson_M-A552A*_briefsheet.pdf`) | ✅ Confirmed |
| A6 | Colibrys SI1003 = **0.7 µg/√Hz typ**, 8 µg integrated **0.1–100 Hz** | SI1000-series datasheet, `extracts/Colibrys_SI1000.md` line 60–62 | Re-read full SI1003 parameter table (lines 50–110); SI1005 figures differ as expected (1.2 / 13 µg), which confirms the table is being read correctly | ✅ Confirmed |
| A7 | Colibrys SI1003 = **27 mA typ, 32 max** | SI1003 power table | SI1005 table shows identical 22/27/32 — consistent | ✅ Confirmed |
| A8 | MPU-6050 = **400 µg/√Hz @10 Hz** | TDK datasheet V3.4 | Re-extracted after the first download turned out to be HTML (see E1) and re-read | ✅ Confirmed |
| A9 | SM-24 = **28.8 V/m/s, fn 10 Hz, 375 Ω, 11 g, <0.1 % distortion** | Geospace brochure, `extracts/Geospace_SM-24_geophone_brochure.md` | Matches the SM-24 description quoted in the VitalMon paper | ✅ Confirmed |
| A10 | QuietSeis = **<15 ng/√Hz above 10 Hz; 1/f not characterized** | EGU2018 PDF, `extracts/EGU2018_...md` lines 40–130 | Consistent with Sercel's two other documents in `datasheets/` | ✅ Confirmed |
| ~~A11~~ | ST IIS2ICLX = 15 µg/√Hz, 2-axis, ±0.5–3 g | Search results + EDN article | — | ✅ **SUPERSEDED 2026-09-17 by A15–A17** — datasheet obtained. The search-sourced figure was **right but incomplete**: 15 is typ, and there is also a 30 µg/√Hz max. Package and operating current were both wrong |
| ~~A12~~ | Murata SCA3300 noise density | Not published anywhere found | — | ✅ **SUPERSEDED 2026-09-17 by A18** — datasheet obtained; **35/40 µg/√Hz Mode 3**. The gap was real: the figure appears in no web page, only in the PDF |
| A13 | TDK IIM-46234 = 70 µg/√Hz | Single search source | **No second pass, no datasheet** — re-attempted 2026-09-17, **TDK's entire site is unreachable** (E10) | ⚠️ **[UNVERIF] — still open, and not closable from here** |
| A14 | Kinemetrics ES-T = 0.06 µg/√Hz @1 Hz | Single source | No datasheet obtained | ⚠️ **[UNVERIF]** |
| **A15** | **IIS2ICLX = 15 µg/√Hz typ, 30 max** | `datasheets/ST_IIS2ICLX_datasheet.pdf` → markitdown → electrical table row *"An Zero-g noise density … 15 │ 30 µg/√Hz"* | Independently cross-read against the datasheet's own **Features** bullet on p.1, *"Ultralow noise performance: 15 µg/√Hz"* (typ only) | ✅ **Confirmed. 15 is typ; 30 is the guaranteed max** — the max was absent from the previous [UNVERIF] row and is materially worse than the ADXL355's typ |
| **A16** | **IIS2ICLX active current = 420 µA**, power-down 3 µA | Datasheet electrical table: `Idd … 420 µA`, `IddPD … 3 µA` | Features bullet p.1: *"Low power: 0.42 mA with 2 axes delivering full performance"* — two independent statements of the same figure | ✅ **Confirmed.** Corrects the earlier row, which listed only the 3 µA **power-down** figure and implied it was the operating current |
| **A17** | **IIS2ICLX package = CCLGA-16, 5 × 5 × 1.7 mm**, 2-axis, ±0.5/1/2/3 g, −40…+105 °C | Datasheet product-summary block | Re-read against the Features list and the ODR/bandwidth tables in the same PDF | ✅ Confirmed. **Corrects "LGA-16"** in the earlier row |
| **A18** | **SCA3300-D01 noise density = 44 / 68 / 35 / 35 µg/√Hz typ** (Modes 1–4) | `datasheets/Murata_SCA3300-D01_datasheet.pdf` (Doc.No. 3165 Rev. 3) → Table 2, *Performance Specifications for Accelerometer* | **Arithmetic cross-check against a second, independently specified table in the same document** — integrated noise (mg rms) predicted from density via 1st-order `ENBW = (π/2)·f−3dB`: 0.461 vs 0.5, 0.713 vs 0.7, 0.367 vs 0.4, 0.139 vs 0.15 | ✅ **Confirmed — all four modes agree within 8 %.** Two separately specified tables reproducing each other under the correct noise model is the **strongest internal validation in this folder**. Discrepancy D8 below concerns only the cover blurb |
| **A19** | **SCA3300-D01 −3 dB = 70 Hz** (Modes 1–3), 10 Hz (Mode 4), 1st-order | Table 2, *Amplitude response, −3dB frequency* | §4.3 *Operation modes*: *"mode 1: ± 3 g full-scale with 70 Hz 1st order low pass filter"* — confirms both the corner **and the filter order**, which the calculation in A18 depends on | ✅ Confirmed |
| **A20** | SCA3300-D01 = 1.2 mA, 3.0–3.6 V, ODR 2000 Hz, 8.6 × 7.6 × 3.3 mm, −40…+125 °C | Datasheet §2.2 / §2.3 / p.1 | Cross-read against the **Murata lineup page HTML** supplied by the user (*"3.0V…3.6V supply voltage with 1 mA current consumption"*) — an independent artefact | ✅ Confirmed. Datasheet's **1.2 mA** is the nominal figure and is used here; the web page rounds to 1 mA |

## B. Price claims — all captured 2026-09-17

| # | Claim | Pass 1 | Pass 2 | Result |
|---|---|---|---|---|
| B1 | **ADXL355 = $63.26 @1, $60.41 @30** | LCSC product page C468833 | **Re-pulled the raw `productPriceList` JSON** from the same page in a separate session: `"ladder":1,"usdPrice":63.2629` / `"ladder":30,"usdPrice":60.4114` | ✅ **Confirmed twice, exact to 4 dp** |
| B2 | ADXL355 LCSC stock = **3 pcs** (ADXL355BEZ), 8 (BEZ-RL) | LCSC page | `"stockNumber":3` / `"stockNumber":8` in the same JSON pull | ✅ Confirmed |
| B3 | **IIS2ICLX = $26.51 / $25.43 @5 / $24.35 @30, stock 421** | LCSC page C1857737 | Raw JSON: `63`→`26.5142`, `25.4324`, `24.3506`; `"stockNumber":421` | ✅ **Confirmed twice** |
| B4 | **SM-24 = $69.95 / $66.45 @25 / $62.96 @100** | SparkFun product page | Page's own Magento product payload: `"regularPrice":69.95`, `"tierPrices":[{"qty":25,"price":66.45},{"qty":100,"price":62.96}]`, SKU `SEN-11744` | ✅ **Confirmed twice** |
| B5 | ADXL355 DigiKey $70.93 | Search snippet | **DigiKey returns 403 to every automated request** | ⚠️ **[UNVERIF]** |
| B6 | ADXL355 ADI list ~$41.84 | Search snippet | analog.com timed out repeatedly | ⚠️ **[UNVERIF]** |
| B7 | ADXL354 ~$51.30 | LCSC search listing only | No product-page pull | ⚠️ **[UNVERIF]** |
| B8 | SCA3300 $38.98 | Search snippet | DigiKey 403 | ⚠️ **[UNVERIF]** |
| B9 | Epson M-A352 ~€999 | Single distributor snippet | Not reproduced | ⚠️ **[UNVERIF]** |
| B10 | MPU-6050 India modules ₹100–200 | General knowledge / snippets | Robu.in returns 403 | ⚠️ **[UNVERIF]** |
| B11 | Raspberry Shake ~$500+ | Snippet | Not reproduced | ⚠️ **[UNVERIF]** |

## C. Literature claims

| # | Claim | Pass 1 | Pass 2 | Result |
|---|---|---|---|---|
| C1 | PigV² detects heartbeats over **10–100 Hz** | Direct quote from the PDF | Re-located the passage in `extracts/pigv2.md`; the stated rationale ("sensitivity range of the sensors ≥10 Hz") is internally consistent | ✅ Confirmed |
| C2 | VitalMon's SM-24 has **fn = 10 Hz** and still gives 1.90 BPM mean error | Direct quotes from the PDF | Independently corroborated by the SM-24 brochure (A9) | ✅ **Confirmed by two independent documents** |
| C3 | Sercel: ambient-limited **above ~2 Hz** in an isolated lab | EGU2018 PDF | Consistent with the same deck's geophone-crossover slide | ✅ Confirmed |
| C4 | PigV² velocity **100–200 m/s** | PDF | Re-read in context | ✅ Confirmed as *their* medium — **not** established for rubble |
| C5 | Evans classes A $2–4k / B $500–1k / C $100–200 | SRL PDF | Re-read `extracts/evans.md`; B and C figures appear verbatim in the extract | ✅ Confirmed |
| C6 | Nof: **<US$150 DAQ**, Mw 2.7–5.1 at 5–106 km | Abstract of the PDF | Title/author/DOI block cross-read | ✅ Confirmed |

## D. Discrepancies — recorded, not resolved away

| # | Discrepancy | Handling |
|---|---|---|
| D1 | ADXL355 noise: MDPI *Sensors* 2025 says **22.5 µg/√Hz**, ADI datasheet says **25 µg/√Hz** | Datasheet takes precedence. 25 used throughout. The 11 % disagreement is small enough not to change any conclusion |
| D2 | Wave velocity: MASTER §7.1 **3000 m/s** vs PigV² **100–200 m/s** | **Unresolved and material.** Flagged in `01-requirements.md` §6 and `04-action-report.md` |
| D3 | Detection band: MASTER §6 **0.5–4 Hz** vs PigV²/VitalMon **10–100 Hz** | **Resolved against MASTER** — two independent working systems plus the 1/f argument |
| D4 | ADXL355 price: MASTER §9 **~$15** vs LCSC **$63.26** | **Resolved against MASTER** — live vendor payload, pulled twice |
| D5 | **My own error.** An earlier draft recorded M-A352 bandwidth as "−6 dB at **9**–460 Hz" | **Wrong.** Epson's lineup table and brief sheet both say **DC to 460 Hz (−6 dB)**. The "9" was most likely a filter-setting value misread as the response low end. **Corrected in `02-sensor-survey.md` A1b**, with the correction left visible rather than silently patched |
| D6 | M-A352 current: **13.2 mA @3.3 V** (lineup) vs **20 mA typ @ ODR 200 Hz** (brief sheet) | **Both true — mode-dependent.** `01-requirements.md` §7 requires ODR ≥250 Sps, so **~20 mA is the figure that applies here.** Both are quoted in A1b; the conclusion (disqualified on power) holds either way |
| D7 | `01-requirements.md` §2 claimed MEMS 1/f below 10 Hz is universally uncharacterised | **Overstated — corrected.** The **Epson M-A370AD10 specs 0.02 µG/√Hz over 1–10 Hz**, below the USGS NHNM. §2 now states the accurate version: the low band is *reachable*, at 36.3 mA and 29 g, which this node cannot afford. Conclusion unchanged, reasoning corrected |
| **D8** | **Murata contradicts itself.** SCA3300-D01 datasheet **p.1** advertises *"Ultra-low 37 µg/√Hz noise density"*; its **own Table 2** lists 44 / 68 / 35 / 35 µg/√Hz typ. **37 matches no mode** | **Unresolved — and resolved against the cover.** The spec table is the binding document: it is per-mode, has min/nom/max columns, and is corroborated by the integrated-noise table (A18). The cover figure is a marketing headline with no stated mode or condition. **35 µg/√Hz (Mode 3) is used throughout `02`.** Anyone quoting "37" is quoting the blurb, not the spec |
| **D9** | **IIS2ICLX bandwidth stated two ways.** Electrical table: *"Bw Bandwidth @ODR 833 Hz — 260 Hz"*. Figures 19–20: *"Frequency response — X-axis ODR = 833 Hz, **BW = ODR/2**"* (= 416 Hz) | **Both plausible, not reconciled.** 260 Hz is likely the default digital LPF setting; ODR/2 is the Nyquist limit of the plotted response. **Immaterial here** — the project's band ends at 100 Hz and *either* figure covers it with margin, at ODR ≥ 208 Hz. Recorded so the number is not quoted as settled |
| **D10** | **My own overstatement.** An interim note read Murata's lineup link text as *"Murata markets the SCA3300 for heartbeat detection"* | **Wrong, and caught on the second audit pass.** The page (`/en-global/products/sensor/library/apps/automotive/heartbeat`, ✅ live, fetched and read in full) is a generic **Sensors › Applications › Automotive** concept page about **in-car child-presence and anti-theft detection**. It **names no part number**, gives no specs, no measurements and no method, and says only that *"combining anti-theft system with accurate heart beat sensor"* improves reliability, with *"low cost two-axis sensors"* used for the anti-theft function. **It is not a source and was deliberately kept out of `03-literature.md`.** Its only legitimate weight: a major MEMS vendor treats accelerometer-based heartbeat detection as viable in a quiet, well-coupled seat — a far easier medium than rubble |

## E. Tooling failures and how they were handled

| # | Failure | Handling |
|---|---|---|
| E1 | First `TDK_MPU-6050_datasheet.pdf` was **an HTML page saved with a .pdf extension** | Detected because markitdown output was website chrome, not a spec table. Deleted, re-downloaded from a working mirror, re-extracted, re-verified (A8) |
| E2 | Two paper PDFs came back as **1.8 KB / 3.0 KB stubs** (MDPI, optomechanical geophone) | **Deleted.** A stub in `papers/` would be a fake citation. Recorded as a coverage gap in `03-literature.md` |
| E3 | analog.com timed out repeatedly | ADXL354/355 datasheet obtained from the `strawberry-linux.com` mirror; content verified as the genuine ADI document |
| E4 | DigiKey, Mouser, Robu, element14 IN, Epson, Safran all return 403 to automated requests | All prices from these marked **[UNVERIF]**. Nothing invented to fill the gap |
| E5 | Bulk `curl` download produced zero files | Replaced with PowerShell `Invoke-WebRequest` + browser UA + explicit timeout, reporting byte count per file |
| E6 | `Invoke-WebRequest` failed with *"PowerShell is in NonInteractive mode"* | Caused by the IE parsing engine's first-run prompt. Fixed with `-UseBasicParsing`; several "dead" URLs then returned 200 |
| E7 | Initial HEAD-request link check reported near-universal failure | **Misleading — HEAD is widely rejected.** Re-run as GET; most links were actually live. Original HEAD results discarded rather than reported |
| E8 | `global.epson.com/...` returned 403 and was cited with a ⚠️ | **Wrong host.** The user supplied the page source, which showed the site is served from **`www.epsondevice.com`**. That host returns 200, and the four brief sheets downloaded cleanly from it. Links corrected; the M-A370 and M-A552 parts were only found this way |
| **E9** | **A ✅ link in the first pass was actually dead.** `invensense.tdk.com/products/motion-tracking/6-axis/mpu-6050/` was recorded as verified-live. The user opened it in a browser and got **"Oops! Page Not Found."** | **The user was right and the method was wrong.** Re-checked: the URL returns **HTTP 200 while serving a not-found body** — a **soft 404**. E7 had already downgraded HEAD to GET; **GET alone is also insufficient, because a status code says nothing about the body.** Fixes applied: (1) the link is now tagged ❌ in `02` C1 with the correction stated in place; (2) **every other ✅ link in this folder was re-fetched and its body scanned** for `page not found` / `oops` / `<title>…404` — **all 10 others passed**, so the damage was contained to this one; (3) ✅ in the Conventions block now means *200 **and** body-inspected*. **The specs in C1 are unaffected** — they come from the PDF, not the page |
| **E10** | TDK's whole InvenSense namespace is unreachable | `invensense.tdk.com` **308-redirect-loops on every path including the bare domain**; `/en-us/products/motion-tracking/6-axis/{mpu-6050,iim-46234}` return soft 404s; `product.tdk.com` returns **403**. Not a local failure — the user reproduced it in a browser. **B5 (IIM-46234) cannot be closed from here**; it needs a distributor-hosted datasheet or TDK sales |

## F. Source provenance

**Datasheets** — ~~`datasheets/`~~ ⚠ **the directory no longer exists.** Every PDF was removed from the tree by `f73b73d` (2026-10-07; `*.pdf` is a gitignore carve-out — third-party datasheets and papers are not ours to redistribute). The **`extracts/*.md` conversions are now the only in-repo record**; the Origin column below is the retrieval path if a figure must be re-verified.

| File | Origin | Verified |
|---|---|---|
| `Epson_M-A352AD10_datasheet_rev20251023.pdf` | Epson (rev 2025-10-23) | 2.28 MB, spec tables parse |
| `Epson_M-A370AD10_briefsheet.pdf` | `epsondevice.com/sensing/en/pdf/briefsheet_a370_e_rev.1.0.pdf` | 335 KB |
| `Epson_M-A352AD10_briefsheet.pdf` | `epsondevice.com/sensing/en/pdf/briefsheet_a352_e_rev.1.0.pdf` | 353 KB |
| `Epson_M-A552AC10_briefsheet.pdf` | `epsondevice.com/sensing/en/pdf/m-a552ac1x_briefsheet_e_11.pdf` | 264 KB |
| `Epson_M-A552AR10_briefsheet.pdf` | `epsondevice.com/sensing/en/pdf/m-a552ar1x_briefsheet_e_11.pdf` | 266 KB |
| `ADI_ADXL354_ADXL355_datasheet.pdf` | strawberry-linux.com mirror (analog.com unreachable) | 1.56 MB, genuine ADI document |
| `ADI_ADXL355_PMOD_userguide.pdf` | Analog Devices, EVAL-ADXL355-PMDZ | 212 KB |
| **`ST_IIS2ICLX_datasheet.pdf`** | **Supplied by the user 2026-09-17** (st.com times out on every automated attempt) | **3.55 MB**, header `%PDF-1.3`, full electrical tables parse |
| **`Murata_SCA3300-D01_datasheet.pdf`** | `murata.com/-/media/webrenewal/products/sensor/pdf/datasheet/datasheet_sca3300-d01.ashx` — exact URL exposed by the page source the user supplied | **1.64 MB**, header `%PDF-`, **Doc.No. 3165 Rev. 3**, Table 2 parses |
| `Colibrys_SI1000_series.pdf` | Safran-Colibrys — **exact source URL not captured during the search pass**; content verified as a genuine SI1000-series datasheet | 1.42 MB |
| `Sercel_MEMS_3C_accelerometers_land_seismic.pdf` | Sercel | 254 KB |
| `Sercel_understanding_MEMS_digital_seismic_sensors.pdf` | Sercel | 7.76 MB |
| `Geospace_SM-24_geophone_brochure.pdf` | Geospace Technologies | 708 KB |
| `RaspberryShake_technical_specifications.pdf` | raspberryshake.org | 1.73 MB |
| `TDK_MPU-6050_datasheet.pdf` | cdiweb.com mirror, V3.4 (second attempt — see E1) | 1.49 MB |

**Papers** — ~~`papers/`~~ ⚠ **also removed by `f73b73d`** — see the note above.

| File | Origin |
|---|---|
| `SenSys2017_geophone_heartrate_shared_bed.pdf` | ACM SenSys '17, DOI 10.1145/3131672.3131679 |
| `PigV2_pig_vital_signs_ground_vibration.pdf` | arXiv 2212.03378 |
| `EGU2018_QuietSeis_ultralow_noise_MEMS_seismology.pdf` | EGU General Assembly 2018 |
| `Evans2014_performance_low_cost_accelerometers_SRL.pdf` | *Seismological Research Letters* |
| `Nof2019_MEMS_accelerometer_mini_array_MAMA.pdf` | *Earthquake Spectra* 35(1):21–38, DOI 10.1193/021218EQS036M |
| `USGS_OFR2005-1438_seismic_noise_PSD.pdf` | USGS Open-File Report 2005-1438 |

**Provenance note.** The two newest datasheets exist only because the user retrieved material by
hand: ST blocks automated access outright, and Murata publishes the datasheet URL only inside the
page source. **Both hand-offs also exposed errors in my own records** — A15/A16 corrected the
IIS2ICLX row, E9 corrected a link I had wrongly marked verified, and D10 caught an overstatement I
was about to write into the literature file.

All 21 files **were** confirmed as real PDFs by size and by successful text extraction, at the time this log was written.

⚠ **That relationship is now inverted (`f73b73d`, 2026-10-07).** The PDFs are gone from the tree; `extracts/` holds the markitdown conversions and they are **the sources of record**, not working files. The verification above stands as the provenance trail for each figure — it is why the extracts are trustworthy — but the PDFs are no longer here to re-check against. Re-retrieve from the Origin column if a figure is ever contested.

---

## G. Honest limits of this research

- **The `[CALC]` geophone noise figure in `01-requirements.md` §5 is my own arithmetic, not a
  measured or published number.** It models coil Johnson noise only. It has not been validated
  against a manufacturer noise curve, and real geophone channels are usually preamp-limited.
- **Nothing here was tested on rubble.** Every conclusion about the medium is extrapolated from
  beds and pig-pen floors. The extrapolation is explicitly unvalidated.
- **Six of eleven price points are [UNVERIF]** because the major distributors block automated
  access. The four that matter most (ADXL355, IIS2ICLX, SM-24 ×1) were each confirmed twice from
  the vendor's own price payload.
- **The ST IIS2ICLX row is entirely second-hand.** It is presented as the most interesting
  cost/noise candidate *and* as unverified. Both are true; do not act on it before the datasheet
  is in hand.

---

*Back to [README](README.md) · Prev: [04 — Action Report](04-action-report.md) · Next: [06 — Build vs Buy](06-build-vs-buy.md)*
