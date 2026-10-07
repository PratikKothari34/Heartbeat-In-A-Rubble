# 04 — Verification Log (Budget Rehaul)

Two audit passes per finding, per the standing constraint. Pass 1 = the original capture.
Pass 2 = an **independent** re-read, re-pull, or recomputation from raw inputs.

Numbering continues from `../MEMS/05-verification-log.md` (which ends at A20 / D10 / E10).

---

## A. Price and spec claims — all captured 2026-10-06

| # | Claim | Pass 1 | Pass 2 | Result |
|---|---|---|---|---|
| **A21** | **ADXL355BEZ = $55.1592 @1** | LCSC C468833 page | **Raw JSON re-pull in a separate request:** `{"ladder":1,...,"usdPrice":55.1592,...}` | ✅ **Confirmed, exact to 4 dp** |
| **A22** | **ADXL355 stock = 486 / 1192** | Same page | `"stockNumber":486`, `"stockNumber":1192` | ✅ Confirmed. **Supersedes `MEMS/05` B2 (stock 3)** — see D11 |
| **A23** | **IIS2ICLXTR = $22.7341 @1 · $21.6483 @5 · $20.5642 @30** | LCSC C1857737 | Raw JSON ladder re-pull | ✅ Confirmed |
| **A24** | **RAK3172 = $5.99** | RAKwireless page | Shopify payload `"price":599` (cents) **and** `og:price:amount = 5.99` — two independent fields | ✅ **Double-confirmed** |
| **A25** | **Pixhawk 6C = $199.00** | Holybro page | `"price":19900` cents; variant ladder to 25299 | ✅ Confirmed. **Initially mis-flagged — see E12** |
| **A26** | **STARTRC drop system = $39.99** | NewBeeDrone | `"price":3999` **and** `og:price:amount=39.99` | ✅ Double-confirmed |
| **A27** | **Raspberry Pi 5 8 GB = $80.00 (Adafruit) / $89.95 (SparkFun)** | Both pages | Independent parse per vendor, same minute | ✅ Confirmed. **$9.95 spread on an identical part** |
| **A28** | **SM-24 = $69.95 / $66.45 @25 / $62.96 @100** | SparkFun payload | `"regularPrice":69.95`, tiers `[[25,66.45],[100,62.96]]` | ✅ Confirmed **and unchanged vs 2026-09-17** — see D12 |
| **A29** | **Wio-E5 bulk module = $8.80** | OpenELab | Shopify cents `880` | ✅ Confirmed |
| **A30** | **DJI Mini 3 has no Payload SDK / no Onboard SDK** | DJI compatibility table | **Raw text extracted from the fetched HTML and read in context**: `DJI Mini 3 DJI Mini 3 Pro Yes \ [CHECK] \` — Mobile SDK only; Payload SDK column populated only for Matrice/FlyCart | ✅ **Confirmed from the primary vendor document** |
| **A31** | **LongShoT = <2 µs avg sync error, <0.1 ppm drift, 4 km** | Search summary | **PDF downloaded, markitdown-converted, quoted from the file**: *"achieves an average synchronization error of less than 2μs and compensates oscillator drift to less than 0.1ppm with devices distributed within 4km of a gateway"* | ✅ **Confirmed in primary text** |
| **A32** | **Unconsolidated P-wave above water table = 200–1000 m/s** | Search snippet | **USGS SIR 2023-5061 PDF downloaded and quoted**: *"materials above the water table have the lowest velocities (on the order of 0.2–1.0 km/s) and those below have the highest (on the order of 1.5–2.3 km/s)"* (citing Petersen, 2001) | ✅ **Confirmed in primary text** |
| **A33** | All budget arithmetic | Computed when written | **Every published figure recomputed from raw vendor inputs in an independent script** — 22 checks: node subtotals, ×9, ×12, system totals, spares, contingency, INR conversion, all deltas | ✅ **All 22 reproduce. `ALL ARITHMETIC CONSISTENT`** |

---

## B. Link verification — the whole folder

**56 unique URLs, machine-verified 2026-10-06**, three-state classifier:

| Verdict | Count |
|---|---|
| ✅ LIVE | 38 |
| 🔒 BOTWALL | 15 |
| ⚠️ UNREACHABLE | 3 |
| ❌ **DEAD** | **0** |

**The audit corrected four of my own tags** (see D13). Nothing cited is nonexistent.

---

## C. Discrepancies

| # | Discrepancy | Resolution |
|---|---|---|
| **D11** | **`MEMS/04` A2 says ADXL355 stock = 3 units and calls the §9 BOM unbuyable.** Today: **486 + 1192** | **The A2 supply argument is dead.** Market condition, not an error — but the doc asserted it as fact, so `MEMS/04` and `MEMS/README` have been corrected. **Lesson: inventory claims need a date stamp and expire fast** |
| **D12** | **Both MEMS parts repriced 8–16 % in 19 days; the SM-24 did not move at all** | **Both verified twice.** The SM-24 holding flat is the **control** that proves the drift is real repricing, not an extractor bug. **A BOM is perishable — re-pull before any purchase** |
| **D13** | **My own over-claiming.** I tagged PMC 11991044, PMC 8621158 and uavcoach.com as ✅ LIVE | **Wrong — caught on audit pass 2.** All three serve reCAPTCHA or 403 to a scripted request. **Re-tagged 🔒 BOTWALL** in `01-literature.md`. analog.com ×2 and st.com re-tagged ⚠️ UNREACHABLE. The papers are real; **my access claim was not** |
| **D14** | **ADXL355 ladder is non-monotonic**: `@10 = $53.33` is cheaper than `@30 = $55.61` | **Not a transcription error.** LCSC interleaves ladders for BEZ vs BEZ-RL package variants. **Quote the variant, not just the quantity** — flagged in `02` §1 |
| **D15** | **MASTER §4.1 contradicts MASTER §5.** §4.1 assumes SX1276 at 40 mA for 100 ms every 500 ms = a **20 % duty cycle**; §5 states the band limit is **~1 %** | **Unresolved and material — §4.1 needs rebuilding, not repricing.** §4.1 breaches §5 by **20×**. Independently, a 225 mAh CR2032 cannot source 40 mA pulses without severe droop. Logged in `01` C4 and `03` §5 |
| **D16** | **MASTER §7.1 (3000 m/s) vs published brackets** (PigV² 100–200; USGS 200–1000 dry / 1500–2300 saturated; concrete ~3600) | **Resolved against MASTER.** Rubble is porous granular material — arXiv 2309.11577 gives the mechanism (low effective elastic modulus → low P-wave speed). Defensible bracket **150–1000 m/s**, so §7.1 is likely **3–20× too high** |
| **D17** | **MASTER §10.4 calls time sync "the hardest open problem here"** | **Resolved against MASTER by A31.** LongShoT measures **<2 µs on COTS hardware** — ~10× better than the "tens of µs" target, and **0.3–6 mm of position error** across the entire velocity bracket. **Sync is not the limit; velocity is.** Costs one $24.95 GPS |
| **D18** | **MASTER §2 ("DJI Mini 3 class, servo release") vs §8.2 (autonomous grid release every 10–15 m)** | **Mutually exclusive — confirmed from DJI's own table (A30).** No Payload SDK, no Onboard SDK, no PWM out. Third-party kits hijack the landing-light channel or carry a separate RC receiver, i.e. **a human triggers each drop.** Costed in `03` §3 |

---

## D. Tooling failures

| # | Failure | Handling |
|---|---|---|
| **E11** | **A two-state link checker is wrong for publisher sites.** My first-pass detector scanned the **whole body** for `captcha` / `page not found` and flagged RAKwireless and Seeed as SOFT404 | **Both were false positives** — "captcha" appears in **Shopify's bundled hCaptcha JS**, not in a block page. Verified by grepping the match context. **Fix: scope detection to `<title>` + first `<h1>`, and classify three ways** — LIVE / BOTWALL / DEAD. A 403-to-script on a real paper is **not** a dead link and must never be reported as one. Conversely **Mouser serves "Access to this page has been denied" with HTTP 200** — the E9 soft-404 trap again, in a new form |
| **E12** | **Holybro Pixhawk 6C initially reported SOFT404** | Same false positive as E11. The page is real; `"price":19900`. **Corrected before anything was written to a doc** |
| **E13** | **A "downloaded" PDF was a 1817-byte HTML stub** (MDPI *Sensors* 18(3):852 via PMC) | **Detected by header check** (`head -c5` ≠ `%PDF-`) and **deleted immediately**. This is `MEMS/05` E2 recurring. Both alternate routes also failed (MDPI 403, PMC stub). **The paper is cited by DOI with its access status stated — no fake file in `papers/`** |
| **E14** | **Guessed vendor URLs returned real 404s** (`rakwireless.com/products/rak3172-module`, `waveshare.com/sx1262-lora-hat.htm`, `seeedstudio.com/Wio-E5-mini-p-4875.html`) | **I constructed those paths rather than looking them up.** Replaced by searching for the actual product pages, then verifying. **Never hand-build a vendor URL** |
| **E15** | **`UnicodeEncodeError: 'charmap'` killed two scripts mid-run** | Windows console defaults to cp1252; `µ`, `√`, `‐` crash on print. **Fix: `PYTHONIOENCODING=utf-8`.** Already recorded in `CLAUDE.md`; cost two reruns here |
| **E16** | **Full 56-URL audit exceeded the 120 s foreground timeout** | Re-run in background, output read from the task file. Not an error — just the right tool |

---

## E. Honest limits

- **"≥20 papers per concept" is met by citation count, not by depth.** **12 PDFs are HELD and read**
  in `papers/` (18 including `../MEMS/papers/`). The rest are verified-to-exist and read at
  abstract level. **Every number that drives a budget decision comes from a HELD source and is
  quoted.** This is stated at the top of `01-literature.md` rather than buried here.
- **15 of 56 links are BOTWALL.** Those papers are real and open in a human browser, but I did not
  read their full text. They are context, not evidence.
- **Five node-BOM lines are [EST]**, not vendor-quoted: antenna, cell, enclosure, PCB, passives.
  Together $6.60 of a $67.75 node (9.7 %). The **sensor and MCU+radio — 91 % of node cost — are
  both [LIVE]**.
- **The SCA3300 price ($38.98) remains [UNVERIF].** DigiKey 403s. It is load-bearing for the
  cheapest system scenario and **should be confirmed before any purchase decision**.
- **DJI Mini 3's ~$559 is [UNVERIF]** — dji.com publishes no scrapeable price field.
- **No India vendor could be priced by script.** Robu, element14 IN both 403. For a project
  sourcing in India this is the largest open gap in the budget, and Murata's `en-in` locale is the
  only verified India-facing route found.
- **The F450 kit price ($399.99) is [SEARCH]** — the page is ✅ LIVE but its price sits behind a
  variant selector my parser did not reach. Confirm in a browser.

---

*Prev: [03 — Budget](03-budget.md) · Back to [README](README.md)*
