# 02 — Vendor Register

Every price below was pulled from the **vendor's own page payload** on **2026-10-06** and
independently re-read. No price is carried over from memory, from search-result snippets, or from
the earlier MEMS pass — **all of those were re-pulled, and several had moved** (§4).

**Link status is three-state, not two** — see `04-verification-log.md` **E11** for why a two-state
check is wrong here:

| Tag | Meaning |
|---|---|
| ✅ **LIVE** | HTTP 200, **and** `<title>`/`<h1>` inspected — real content, not a not-found body |
| 🔒 **BOTWALL** | Resource exists, scripted access challenged (Cloudflare "Client Challenge", reCAPTCHA, 403-to-UA). **A human browser opens it.** Not a dead link |
| ❌ **DEAD** | Genuinely not found |

Price provenance: **[LIVE]** parsed from the page's own price field · **[SEARCH]** from a search
result, not yet confirmed on the page · **[UNVERIF]** single-source, do not trust.

---

## 1. Sensor — 3-axis MEMS (the node's dominant cost)

| Vendor | Part | Price | Stock | Link |
|---|---|---|---|---|
| **LCSC** | **ADI ADXL355BEZ** (C468833) | **$55.1592 @1 · $53.3316 @10 · $55.6146 @30** | **486 / 1192** | <https://www.lcsc.com/product-detail/C468833.html> ✅ |
| **LCSC** | ST IIS2ICLXTR (C1857737) | $22.7341 @1 · $21.6483 @5 · $20.5642 @30 | 324 | <https://www.lcsc.com/product-detail/C1857737.html> ✅ |
| Murata | SCA3300-D01 | $38.98 ⚠️ **[UNVERIF]** — DigiKey 403s to every automated request | — | <https://www.murata.com/en-global/products/sensor/overview/item/sca3300-d01> ✅ |
| Murata **India** | SCA3300 lineup | quote via `en-in` locale | — | <https://www.murata.com/en-in/products/sensor/accel/overview/lineup/sca3300> ✅ |
| ST | IIS2ICLX product page | — | — | <https://www.st.com/en/mems-and-sensors/iis2iclx.html> 🔒 (timeout to script) |
| Analog Devices | ADXL355 product page | — | — | <https://www.analog.com/en/products/adxl355.html> 🔒 (timeout to script) |
| DigiKey | IIS2ICLXTR | — | — | 🔒 **403 to all automated access** |
| Mouser | ADXL355BEZ | — | — | 🔒 **"Access to this page has been denied"** served with **HTTP 200** — see E11 |

**⚠️ Note on the ADXL355 price ladder.** `@10 = $53.33` is **cheaper than `@30 = $55.61`**. That is
not a transcription error — LCSC lists multiple package/reel variants (ADXL355BEZ vs BEZ-RL) whose
ladders interleave. **Quote the variant, not just the quantity.**

## 2. MCU + radio — the architecture change

| Vendor | Part | Price | What it is | Link |
|---|---|---|---|---|
| **RAKwireless** | **RAK3172** | **$5.99** (variants $5.99–$6.99) | **STM32WLE5: Cortex-M4 + SX126x LoRa on one module** | <https://store.rakwireless.com/products/wisduo-lpwan-module-rak3172> ✅ |
| RAKwireless | RAK3172-SiP | $6.99 | SiP variant | <https://store.rakwireless.com/products/wisduo-module-rak3172-sip> ✅ |
| RAKwireless | RAK3172-F | $7.99 | + external flash (FUOTA) | <https://store.rakwireless.com/products/rak3172-f-fuota-lorawan-module> ✅ |
| **OpenELab** | Seeed Wio-E5 bulk module | **$8.80** | bare STM32WLE5JC module | <https://openelab.io/products/seeed-studio-wio-e5-wireless-module-bulk> ✅ |
| Seeed Studio | Grove Wio-E5 | $14.90 / $16.90 | Grove-connector module | <https://www.seeedstudio.com/Grove-LoRa-E5-STM32WLE5JC-p-4867.html> ✅ |
| Seeed Studio | Wio-E5 mini dev board | $19.90 / $21.90 | dev board, for bring-up | <https://www.seeedstudio.com/LoRa-E5-mini-STM32WLE5JC-p-4869.html> ✅ |
| Adafruit | RFM95W LoRa breakout | $19.95 | SX1276 breakout — **radio only, still needs an MCU** | <https://www.adafruit.com/product/3072> ✅ |
| Adafruit | Feather M0 RFM96 | $34.95 | MCU+radio board (dev, not node) | <https://www.adafruit.com/product/3179> ✅ |
| SparkFun | Thing Plus ESP32 WROOM | $29.95 (→$25.46 @100) | ESP32 dev board | <https://www.sparkfun.com/sparkfun-thing-plus-esp32-wroom-usb-c.html> ✅ |

**This is the single biggest finding of the rehaul.** MASTER §9 budgets **MCU $4 + SX1276 $5 = $9**
as two parts. The **RAK3172 is both, for $5.99** — an STM32WLE5 puts a Cortex-M4 and an SX126x
radio on one die. It saves **$3.01/node** and, more importantly, **deletes the inter-chip SPI link**
between MCU and radio, which is one less thing to get wrong on a drop-survivable board.

## 3. Drone platform — where MASTER §9 is most wrong

| Vendor | Item | Price | Link |
|---|---|---|---|
| **Holybro** | **Pixhawk 6C** | **$199.00** (variants to $252.99) | <https://holybro.com/products/pixhawk-6c> ✅ |
| **HAWK'S WORK** | **F450 complete kit** — frame, Pixhawk, GPS, ESC, motors, props, battery, TX/RX | **$399.99** **[SEARCH]** | <https://www.hawks-work.com/products/f450-drone-kit-to-build-diy-450mm-wheelbase-4-axis-multi-rotor-drone-kit-b> ✅ |
| **NewBeeDrone** | **STARTRC payload drop system**, DJI Mini 3 / 3 Pro | **$39.99** | <https://newbeedrone.com/products/startrc-payload-dropping-system-dji-mini-3-mini-3-pro> ✅ |
| DJI | Mini 3 | ~$559 street **[UNVERIF]** — dji.com publishes no scrapeable price field | <https://www.dji.com/mini-3> ✅ |
| DJI (reference) | **Product SDK compatibility table** | — | <https://support.dji.com/help/content?customId=01700000763&lang=en&re=US&spaceId=17> ✅ |
| JOUAV (reference) | SAR drone class pricing, $10k–150k | — | <https://www.jouav.com/search-and-rescue-drone> ✅ |

**⛔ The blocking find.** MASTER §2 specifies *"DJI Mini 3 class drone, servo release"* and §8.2
specifies an **autonomous snake-pattern grid with servo release every 10–15 m**. **Those two cannot
both be true.** From DJI's own compatibility table, read directly:

> **DJI Mini 3 / DJI Mini 3 Pro — Mobile SDK: Yes. Payload SDK: — . Onboard SDK: — .**

Payload SDK appears **only** on Enterprise hardware (Matrice 350/400/4-series, FlyCart). The Mini 3
exposes **no PWM output and no payload control path**. Third-party drop kits work by hijacking the
**landing-light channel** or carrying their **own independent RC receiver** — a human presses a
button per drop. **There is no autonomous grid release on a Mini 3 at any price.** Full costing of
the three paths: `03-budget.md` §3.

## 4. Ground station

| Vendor | Item | Price | Link |
|---|---|---|---|
| **SparkFun** | Raspberry Pi 5, 8 GB | **$89.95** **[LIVE]** | <https://www.sparkfun.com/raspberry-pi-5-8gb.html> ✅ |
| **Adafruit** | Raspberry Pi 5, 8 GB | **$80.00** **[LIVE]** | <https://www.adafruit.com/product/5813> ✅ |
| Adafruit | Ultimate GPS FeatherWing | $24.95 | <https://www.adafruit.com/product/3133> ✅ |
| Raspberry Pi Ltd | Pi 5 / Pi 4B official pages | — | 🔒 403 to script |

**Adafruit is $9.95 cheaper than SparkFun on the identical part.** Both verified the same minute.

## 5. Non-MEMS alternative (carried forward, re-verified)

| Vendor | Item | Price | Link |
|---|---|---|---|
| SparkFun | **Geospace SM-24 geophone** | **$69.95 · $66.45 @25 · $62.96 @100** — **unchanged** since 2026-09-17 | <https://www.sparkfun.com/geophone-sm-24-with-insulating-disc.html> ✅ |

**The SM-24 holding steady while both MEMS parts moved 8–16 % is a useful cross-check** — it shows
the drift in §6 is real repricing, not a parsing artefact in my extractor.

---

## 6. Price drift since the MEMS pass — why re-pulling mattered

19 days, 2026-09-17 → 2026-10-06:

| Part | Then | Now | Δ |
|---|---|---|---|
| ADXL355 @1 | $63.2629 | **$55.1592** | **−12.8 %** |
| ADXL355 @30 | $60.4114 | $55.6146 | −7.9 % |
| IIS2ICLX @1 | $26.5142 | **$22.7341** | **−14.3 %** |
| IIS2ICLX @5 | $25.4324 | $21.6483 | −14.9 % |
| IIS2ICLX @30 | $24.3506 | **$20.5642** | **−15.5 %** |
| SM-24 @1 | $69.95 | $69.95 | **0.0 %** |

**And the supply problem has resolved itself.** `04` A2 recorded **ADXL355 stock = 3 units** and
called the §9 BOM unbuyable. It is now **486 + 1192 units**. That argument is dead and the doc
has been corrected.

**Standing conclusion: a BOM is a perishable artefact.** Any quoted node cost needs a pull date
attached, and nothing in this folder should be re-used after ~30 days without re-pulling. Every
price table here carries **2026-10-06**.

---

## 7. Vendors that cannot be priced from here

| Vendor | Behaviour | Consequence |
|---|---|---|
| DigiKey | 403 to all automated requests | SCA3300 price stays **[UNVERIF]** |
| **Mouser** | **HTTP 200 + "Access to this page has been denied"** | Would have passed a status-code check — see **E11** |
| Robu.in | 403 | No India-rupee pricing obtainable |
| element14 IN | 403 | — |
| pishop.us | 403 | — |
| Raspberry Pi Ltd | 403 | Priced via Adafruit/SparkFun instead |
| analog.com, st.com | Timeout to script | Datasheets already held locally |
| **TDK InvenSense** | **308 redirect loop on every path, incl. bare domain** | IIM-46234 still unobtainable (`MEMS/05` E10) |

**Nothing was invented to fill these gaps.** Every unpriced line is tagged, and the India-sourcing
question is genuinely open: **not one India vendor could be priced by script.** Murata's `en-in`
locale is the only verified India-facing route in the whole project.

---

*Next: [03 — Budget](03-budget.md) · [04 — Verification Log](04-verification-log.md) ·
Back to [README](README.md)*
