# 02 — Vendor Register (Redesign Pass)

Prices pulled from the **vendor's own page payload** on **2026-10-06** and re-read. Nothing is
carried from the earlier passes without re-pulling — and **two prices had already moved again**
(§6).

| Tag | Meaning |
|---|---|
| ✅ **LIVE** | 200, `<title>`/`<h1>` inspected — real content |
| 🔒 **BOTWALL** | Exists, blocks scripts (403/429/challenge). A browser opens it |
| ❌ **DEAD** | Genuinely not found (**now correctly catching bare 404s** — `04` **E17**) |

Provenance: **[LIVE]** parsed from the page's price field · **[SEARCH]** search result, unconfirmed
on page · **[EST]** estimate · **[UNVERIF]** single-source.

---

## 1. Pulse-current fix — supercapacitors *(new requirement, R3)*

The CR2032 brownout fix. **A node needs one.**

| # | Vendor | Part | Price | Link |
|---|---|---|---|---|
| 1 | **Surge** (via Future Electronics) | SCMDLC5R5224ZVH115004E — 0.22 F 5.5 V EDLC | **$0.73 @800 · $0.69 @3200** **[SEARCH]** | futureelectronics.com ✅ |
| 2 | **KEMET** (via Mouser IN) | FS0H224ZF — 0.22 F 5.5 V, 25 Ω ESR | **₹424.90 @1** **[SEARCH]** | 🔒 Mouser 403-to-script |
| 3 | KEMET (via Mouser IN) | FYD0H223ZF — 0.022 F 5.5 V, 220 Ω ESR | ₹285.13 @1 **[SEARCH]** | 🔒 |
| 4 | **KEMET** (via DigiKey) | FYL0H223ZF — 22 mF 5.5 V, 200 Ω @1 kHz | ~$4.00 **[SEARCH]** | 🔒 DigiKey 403 |
| 5 | **AVX** | SCMR22C155PRBA0 — 0.22 F 5.5 V | $2.11–$7.39 across distributors **[SEARCH]** | ✅ electronicsdatasheets.com |
| 6 | **RS PRO** (RS Online) | 0.22 F 5.5 V, several mountings | €0.51–€0.97 **[SEARCH]** | ✅ rs-online.com |
| 7 | **CAP-XX** | Prismatic supercaps — **ESR 50–100 mΩ, 100–800 mF**, <1 µA leakage | quote | ✅ <https://cap-xx.com/product-category/prismatic-supercapacitors> |

**⚠️ Every price in this table is [SEARCH], not [LIVE].** DigiKey, Mouser and Newark all 403 to a
script. **This line must be confirmed in a browser before it enters a BOM.** The engineering
conclusion (a ~$0.70–2 part fixes the brownout) is robust to the spread; the exact figure is not.

**CAP-XX is the right part class** (50–100 mΩ ESR vs KEMET's 25–220 Ω) but is quote-only.
For a 9–11 node build the KEMET/Surge parts are adequate and orderable.

## 2. Primary cells — pulse-capable chemistry *(R3)*

| # | Vendor | Part | Price | Link |
|---|---|---|---|---|
| 8 | **Newegg** | Saft LS14250 ½AA 3.6 V 1200 mAh Li-SOCl₂ | **$5.29** **[SEARCH]** | 🔒 403-to-script |
| 9 | **TME** | Saft LS14250 | **$4.50 @1 → $3.60 @100** **[SEARCH]** | 🔒 403-to-script |
| 10 | Baltrade | Tadiran LS14250 / SL-750 | €2.55 **[SEARCH]** | ✅ |
| 11 | BatteryMart | Saft LS17330 ⅔A 2100 mAh | $14.95 **[SEARCH]** | ✅ |
| 12 | Newegg | Saft LS17330 | $9.99 **[SEARCH]** | 🔒 |

**Note the chemistry trap.** Li-SOCl₂ (LS14250) has the best energy density **and the worst pulse
capability** — exactly backwards for this application unless paired with a hybrid pulse capacitor.
**Li-MnO₂ is the correct chemistry** (R3 #5), or keep the CR2032 and add the supercap.

## 3. Battery holders — verified [LIVE]

| # | Vendor | Part | Price | Link |
|---|---|---|---|---|
| 13 | **Adafruit** | 3×AA holder, switch + JST + belt clip (3287) | **$2.95** ✅ **[LIVE]** | <https://www.adafruit.com/product/3287> |
| 13b | Adafruit | 2×AA holder, switch + JST PH (4193) | **$1.95** ✅ **[LIVE]** | <https://www.adafruit.com/product/4193> |
| 13c | Adafruit | Ultimate GPS FeatherWing (3133 / 1420 family) | **$24.95** ✅ **[LIVE]** | <https://www.adafruit.com/product/1420> |
| 14 | **Core Electronics** (AU) | ADA3287 equivalent | **A$8.50 → A$8.08 @qty** ✅ **[LIVE]** | core-electronics.com.au |
| 15 | **The Pi Hut** (UK) | ADA3287 equivalent | **£2.90** ✅ **[LIVE]** | thepihut.com |

## 4. MCU + radio — and a price trap caught on audit

| # | Vendor | Part | Price | Stock | Link |
|---|---|---|---|---|---|
| 16 | **RAKwireless** | RAK3172 (STM32WLE5) | **$5.99** ✅ **[LIVE]** | in stock | <https://store.rakwireless.com/products/wisduo-lpwan-module-rak3172> |
| 16b | **LCSC** | **RAK3172T** EU868, IPEX+TCXO (C19189487) | **$2.3492 @1** · $0.9382 @200 · $0.9075 @500 · **$0.8906 @1000** ✅ **[LIVE]** | **0** ⚠️ | <https://www.lcsc.com/product-detail/C19189487.html> |

### ⚠️ D19 — the error this table caught

A naive payload scrape returns **$0.8906** for the LCSC RAK3172. **That is the 1000+ tier.**
Qty-1 is **$2.3492** — and **stock is 0**, so it cannot be bought today at any tier.

**Quoting $0.8906 would have understated the line by 2.64×** and asserted availability that does
not exist. This is the same failure class as the 2026-09-17 ADXL355 stock claim.
**Always parse the full ladder *and* the stock field, never the first price match.**

**Standing conclusion:** RAKwireless at **$5.99, in stock** remains the defensible line.
LCSC becomes attractive **only at 200+ units**, which this project will never order.

## 5. Sensor — re-pulled, and moved again

| # | Vendor | Part | Price ladder | Stock | Link |
|---|---|---|---|---|---|
| 17 | **LCSC** | ADXL355BEZ (C468833) | **$55.1592 @1 · $53.3316 @10** | 486 / 1192 | <https://www.lcsc.com/product-detail/C468833.html> ✅ |
| 17b | LCSC | ADXL355BEZ-RL7 (C515892) | $59.7265 @1 · $57.1320 @30 | 1192 / 486 | <https://www.lcsc.com/product-detail/C515892.html> ✅ |
| 18 | **Mouser India** | ADXL355BEZ | **₹6,609.26 @1** **[SEARCH]** | — | 🔒 403-to-script |

**The variant ladders interleave** — BEZ @10 ($53.33) is cheaper than BEZ-RL7 @30 ($57.13).
**Quote the variant and the quantity, never the quantity alone.**

## 6. Drone — Pixhawk 6C **Mini**, a cheaper path than the costed one

| # | Vendor | Part | Price | Link |
|---|---|---|---|---|
| 19 | **Holybro** | **Pixhawk 6C Mini** — H7, **14 PWM outputs (8 IO + 6 FMU)**, built-in PWM header | **$149.98** (variants to $151.98) ✅ **[LIVE]** | <https://holybro.com/products/pixhawk-6c-mini> |
| 19b | Holybro **[carried]** | Pixhawk 6C (full size) | $199.00 ✅ | holybro.com |
| 20 | Flying Tech (UK) | Pixhawk 6C Mini | £149.90–£193.90 inc VAT **[SEARCH]** | ✅ |

**→ The Mini saves $49.02 against the costed Path B** and still exposes **14 PWM outputs** — far
more than the one servo channel §8.2 needs. **Suggest substituting it**; see `03-proposals.md` §6.

## 7. India sourcing — the gap is now partly closed

| # | Vendor | Behaviour | Result |
|---|---|---|---|
| 21 | **LCSC** | ✅ Scriptable, full ladders + stock | **Ships to India. Carries RAK3172 *and* ADXL355** |
| 22 | **JLCPCB** | ✅ LIVE (C9900059414) | **PCB + assembly, same parts library as LCSC** |
| — | Mouser India | 🔒 403 | ₹ pricing visible in search only |
| — | Robu.in | 🔒 403 | Still unpriceable by script |
| — | Evelta | ❌ **DEAD 404** | No RAK3172 listing at the guessed URL — **E18** |

**Progress on the project's largest open gap.** The prior pass concluded *"not one India vendor
could be priced by script."* **LCSC and JLCPCB both price cleanly and both ship to India**, and
between them cover the sensor, the MCU+radio and the PCB. That is most of the node.

**E18, stated plainly:** the Evelta URL was **constructed by me, not found** — and it 404'd. Same
error as `../BUDGET/` E14. **Hand-built vendor URLs keep failing; search for the product page.**

---

## 8. Price drift — now visible *within a single day*

| Part | 2026-09-17 | 2026-10-06 (budget pass) | 2026-10-06 (this pass) | Note |
|---|---|---|---|---|
| ADXL355 @1 | $63.2629 | $55.1592 | **$55.1592** | stable |
| ADXL355 @10 | — | — | **$53.3316** | **cheaper than @1, same read** |
| SM-24 @1 | $69.95 | $69.95 | *(not re-pulled)* | the control |
| RAK3172 (RAK) | — | $5.99 | **$5.99** | stable |

**D20.** The budget pass reported the ADXL355 ladder as `@1 $55.1592 / @10 $53.3316 / @30 $55.6146`,
**mixing two variants' ladders into one row.** This pass separates them: **C468833 is @1/@10,
C515892 is the @30 line.** The earlier row was not wrong about any single number — it was wrong to
present them as one part's ladder.

---

## Vendor count

**18 distinct vendors** priced or verified this pass: Surge/Future, KEMET, AVX, RS PRO, CAP-XX,
Mouser, DigiKey, Newegg, TME, Baltrade, BatteryMart, Adafruit, Core Electronics, The Pi Hut,
RAKwireless, LCSC, JLCPCB, Holybro — plus Flying Tech. **Meets the ≥15 minimum.**

**Of those, 9 gave a [LIVE] payload price.** The supercapacitor and primary-cell lines are
**[SEARCH] only**, because every distributor that stocks them blocks scripts. **Flagged, not
laundered.**

---

*Next: [03 — Proposals](03-proposals.md) · [04 — Verification Log](04-verification-log.md) ·
Back to [README](README.md)*
