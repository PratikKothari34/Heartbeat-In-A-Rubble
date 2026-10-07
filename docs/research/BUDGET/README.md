# Budget Rehaul — Heartbeat In The Rubble

Full rebuild of the project budget covering **sensor, node, radio, drone and ground station**.
Prices pulled **2026-10-06** from vendor payloads; literature verified the same day.

**Scope note:** `../MEMS/` answered *which sensor*. This folder answers *what the whole system
costs* — and in doing so found that **three MASTER sections are internally contradictory**, not
merely mispriced.

---

## The headline

> **MASTER §9 says $641–1141. The defensible figure is $1,323–1,469 for 9 nodes,
> or $1,845 with spares and contingency — ≈ ₹1,55,000.**

**Understated 2.2–2.3× at system level, 1.8–2.3× per node.** Not from one bad number — from
**four structural omissions** (`03-budget.md` §5): no spares for sensors *thrown onto rubble*, no
GPS time reference, no PCB, and an airframe that cannot do the job specified.

**The Delsar comparison survives.** Incumbent ~$15,000, hand-placed, blind to unconscious victims.
**At $1,845 the order-of-magnitude advantage holds with 10× margin** — §9's conclusion was right
even though its arithmetic was not.

---

## Four findings that change the project

### 1. ⛔ The specified drone cannot do the specified job

MASTER §2 says *"DJI Mini 3 class drone, servo release."* MASTER §8.2 says *autonomous snake-grid,
servo release every 10–15 m.* From **DJI's own SDK compatibility table**, read directly:

> **DJI Mini 3 / Mini 3 Pro — Mobile SDK: Yes · Payload SDK: — · Onboard SDK: —**

Payload SDK is **Enterprise-only** (Matrice/FlyCart). The Mini 3 exposes **no PWM and no payload
control path**. Third-party drop kits hijack the landing-light channel or carry a separate RC
receiver — **a human triggers every drop.** There is no autonomous grid release on this airframe
at any price.

**→ Path B: F450 + Pixhawk 6C, $738.99.** 8 % over §9's ceiling, and the only option that delivers
the autonomy MASTER already specifies. → `03-budget.md` §3

### 2. ✅ §10.4 — "the hardest open problem" — is solved in the literature

**LongShoT** (CMU, NSF): **<2 µs average sync error**, <0.1 ppm drift, within 4 km, **on COTS
hardware** — read from the PDF, not a summary. That is ~10× better than §10.4's own "tens of µs"
target.

| Velocity | 2 µs → position error |
|---|---|
| 150 m/s | **0.3 mm** |
| 3000 m/s | **6 mm** |

**Sync is ~2 orders of magnitude better than needed at every plausible velocity.** It costs one
**$24.95 GPS** — a line §9 never had. **Downgrade §10.4; the real limit is velocity.**
→ `01-literature.md` C3

### 3. ⚠️ §4.1's power budget breaches §5's own duty-cycle limit by 20×

§4.1 assumes *"SX1276, 40 mA for 100 ms every 500 ms"* = a **20 % radio duty cycle**. §5 states the
band limit is **~1 %**. **The two sections contradict each other**, and the literature's figure is
far away: a LoRaWAN node on 2400 mAh lasts a year at **one message per 5 minutes**; MASTER wants
~2 per second.

Separately, **a 225 mAh CR2032 cannot source 40 mA TX pulses** without severe droop.
**This needs rebuilding, not repricing.** → `01-literature.md` C4

### 4. 💡 One part replaces two — and it's cheaper

MASTER §9 budgets **MCU $4 + SX1276 $5 = $9**. The **RAK3172** is an **STM32WLE5** — Cortex-M4 and
SX126x radio on one die — for **$5.99 [LIVE]**. Saves $3.01/node *and* **deletes the MCU↔radio SPI
link**, one fewer joint to survive a 15–20 G impact. → `02-vendor-register.md` §2

---

## Index

| Doc | Contents |
|---|---|
| **[01 — Literature](01-literature.md)** | 5 concepts, 20+ citations each, access status stated per link. 12 PDFs held and read |
| **[02 — Vendor Register](02-vendor-register.md)** | 17 live vendor pages, prices from payloads, **19-day price drift table** |
| **[03 — Budget](03-budget.md)** | Node BOM, ground station, 3 drone paths, system totals, 4 omissions, cut list |
| **[04 — Verification Log](04-verification-log.md)** | A21–A33, D11–D18, E11–E16, honest limits |

| Folder | Contents |
|---|---|
| `papers/` | **12 PDFs** — LoRa sync/mesh ×5, UAV deployment ×3, velocity ×2, BCG/victim ×2 |
| `extracts/` | markitdown conversions. Working files, not sources |

---

## Budget at a glance

| Line | Cost |
|---|---|
| 9 nodes (ADXL355 @ $67.75) | $609.74 |
| +2 spares (20 % attrition) | $135.50 |
| Ground station (Pi 5 + **GPS**) | $119.95 |
| Drone — Path B, autonomous | $738.99 |
| **Subtotal** | **$1,604.18** |
| Contingency 15 % | $240.63 |
| **TOTAL** | **$1,844.81 ≈ ₹1,55,000** |

Fits the ₹1,95,749 sample award in the proposal template with **20.8 % headroom**.

**Cheapest real saving: switch to SCA3300 (−$145.61).** Gated on the ambient measurement, and its
price is still **[UNVERIF]** (DigiKey 403s).

**Don't buy the drone first.** Build order §12 steps 1–5 need no airframe — **$739 is deferrable
past the measurement that may change the architecture.**

---

## Verification

| | |
|---|---|
| URLs machine-verified | **56** — 38 LIVE, 15 BOTWALL, 3 UNREACHABLE, **0 DEAD** |
| Arithmetic checks recomputed from raw inputs | **22 of 22 reproduce** |
| Audit passes per finding | **2** |
| Tags the audit corrected (my own over-claiming) | **4** → `04` D13 |

**Prices are perishable.** Both MEMS sensors moved **8–16 % in 19 days**; the SM-24 did not move at
all, which is the control proving that drift is real. **Nothing here should be reused after ~30
days without re-pulling.** → `04` D12

---

## Conventions

**[LIVE]** parsed from the vendor's own price field today · **[SEARCH]** from a search result, not
confirmed on the page · **[EST]** my estimate, not a quote · **[UNVERIF]** single-source ·
📄 **HELD** PDF downloaded and read · ✅ **LIVE** · 🔒 **BOTWALL** (exists, blocks scripts — opens
in a browser) · ❌ **DEAD**

---

*Related: [../MEMS/](../MEMS/) — sensor selection, physics and the ambient-measurement gate.*
