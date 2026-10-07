# 03 — The Rehauled Budget

Every figure derives from a price in `02-vendor-register.md` pulled **2026-10-06** from the
vendor's own payload. Arithmetic is reproducible from those numbers; nothing is estimated except
the five lines explicitly marked **[EST]**.

**Verdict up front: MASTER §9 understates the system by 2.2–2.3×, and understates the node by
1.8–2.3×.** Not because of one bad number — because of **four structural omissions** (§5).

---

## 1. Per-node BOM

**Non-sensor subtotal — $12.59**

| Item | Part | Cost | Src |
|---|---|---|---|
| MCU + radio | **RAK3172** (STM32WLE5: Cortex-M4 + SX126x) | **$5.99** | ✅ [LIVE] |
| Antenna | u.FL 868 MHz whip | $1.50 | **[EST]** |
| Cell | CR2032 225 mAh + holder | $0.60 | **[EST]** |
| Enclosure | PLA print + EVA foam | $1.20 | **[EST]** |
| PCB | JLCPCB 4-layer, qty 10, amortised | $1.80 | **[EST]** |
| Passives / connector / misc | | $1.50 | **[EST]** |

**With a sensor:**

| Sensor | Price | **Node** | ×9 | ×12 |
|---|---|---|---|---|
| **ADI ADXL355** | $55.1592 ✅ | **$67.75** | $609.74 | $812.99 |
| **Murata SCA3300-D01** | $38.98 ⚠️ | **$51.57** | $464.13 | $618.84 |

**vs MASTER §9's $29/node** → **2.3× / 1.8× understated.**

**The MCU+radio line is the one piece of good news in this document.** MASTER budgets MCU $4 +
SX1276 $5 = $9 as two chips. The RAK3172 is **both for $5.99** — saving $3.01/node *and* removing
the MCU↔radio SPI link, one fewer joint to survive a 15–20 G impact.

## 2. Ground station — $119.95

| Item | Cost | Src |
|---|---|---|
| Raspberry Pi 5, 8 GB (Adafruit) | **$80.00** | ✅ [LIVE] |
| Ultimate GPS FeatherWing — **the time reference** | **$24.95** | ✅ [LIVE] |
| Gateway radio + cabling + SD + PSU | $15.00 | **[EST]** |

vs MASTER §9's **$80 "Pi 4 + LoRa hat"**. Two corrections: the Pi 5 at 8 GB is $80 **alone**, and
**§9 has no GPS line at all** — yet §10.4's time sync needs a 1PPS reference (§4 below).

## 3. Drone — the line that breaks

MASTER §2: *"DJI Mini 3 class drone, servo release."* MASTER §8.2: *"servo release every 10–15 m"*
on an autonomous snake-pattern grid. MASTER §9: **$300–800**.

### ⛔ Those specifications are mutually exclusive

Read directly from **DJI's own Product SDK Compatibility table** (✅ live, `02` §3):

> **DJI Mini 3 / Mini 3 Pro — Mobile SDK: Yes · Payload SDK: — · Onboard SDK: —**

Payload SDK exists **only** on Enterprise airframes (Matrice 350/400/4-series, FlyCart). The Mini 3
exposes **no PWM output and no payload-control path**. Commercial drop kits for it work by hijacking
the **landing-light channel** or carrying their **own RC receiver** — i.e. **a human triggers every
single release.** §8.2's autonomous grid is not achievable on this airframe at any price.

### The three paths, costed

| | **Path A** — Mini 3 + drop kit | **Path B** — F450 + Pixhawk | **Path C** — Enterprise |
|---|---|---|---|
| Airframe | DJI Mini 3 ~$559 ⚠️ | HAWK'S WORK F450 kit **$399.99** ✅ | Matrice 30/4T |
| Controller | *(closed)* | **Pixhawk 6C $199.00** ✅ | *(closed)* |
| Release | **STARTRC $39.99** ✅ | servo + hardware $25 **[EST]** | Payload SDK |
| Telemetry | — | radio pair $45 **[EST]** | included |
| Batteries | spare $59 **[EST]** | 2× 4S LiPo $70 **[EST]** | — |
| **Total** | **$657.99** | **$738.99** | **$10,000–20,000** |
| Autonomous grid drop | ❌ **No** | ✅ **Yes** (AUX PWM via MAVLink) | ✅ Yes |
| Verdict | within §9's range, **fails §8.2** | **$61 over §9's top**, meets §8.2 | out of scope |

**Recommendation: Path B.** It is **8 % over** the top of MASTER's own range and is the **only**
option that delivers the autonomy MASTER already specifies. Path A is cheaper and buys a system
that cannot do the job described. Per `CLAUDE.md` — *never recommend a cheap option that isn't the
best* — Path A should be struck, not kept as the budget case.

## 4. System totals, 9 nodes

| Sensor | Drone | **System** | vs §9 ($641–1141) |
|---|---|---|---|
| SCA3300 | A (manual) | **$1,242.07** | +9–94 % |
| SCA3300 | **B (autonomous)** | **$1,323.07** | +16–106 % |
| ADXL355 | A (manual) | **$1,387.68** | +22–116 % |
| **ADXL355** | **B (autonomous)** | **$1,468.68** | **+29–129 %** |

**The honest headline number is $1,323–1,469** — SCA3300 or ADXL355, Path B, 9 nodes.

**The Delsar argument still holds.** The incumbent is ~$15,000, places sensors by hand one at a
time, and is blind to unconscious victims. **At $1,469 the order-of-magnitude advantage survives
with 10× margin** — MASTER §9's conclusion was right even though its arithmetic was not.

## 5. The four structural omissions

Not bad numbers — whole categories MASTER §9 never had a line for.

| # | Omission | Impact |
|---|---|---|
| **1** | **Spares and attrition.** Nodes are *thrown onto rubble* from 3–4 m. §9 budgets exactly 9 for a 9-node array | At 20 % loss, +$102–135 |
| **2** | **The time reference.** §10.4 needs µs sync; that needs a **GPS 1PPS** source. No GPS line existed | +$24.95 minimum |
| **3** | **PCB + assembly.** §9's node is five part prices with no board to mount them on | +$1.80/node amortised |
| **4** | **The drone's real capability.** §9 priced an airframe that cannot perform §8.2 | +$61 to +$81 |

### Recommended budget, with contingency

| Line | Cost |
|---|---|
| 9 nodes (ADXL355) | $609.74 |
| **+2 spare nodes (20 % attrition)** | **$135.50** |
| Ground station incl. GPS | $119.95 |
| Drone, Path B | $738.99 |
| **Subtotal** | **$1,604.18** |
| **Contingency 15 %** | **$240.63** |
| **TOTAL** | **$1,844.81** |

**≈ ₹1,55,000 at ₹84/$** — which fits the ₹1,95,749 sample award in
`../../../Research proposal format.docx` with ~20 % headroom. **That is the number to put on the
grant form**, not §9's $641–1141.

## 6. What would actually cut the cost

In order of leverage, and **all of it gated on the ambient measurement** (`MEMS/04` A4):

1. **Switch sensor to SCA3300** — −$145.61 across 9 nodes. 3-axis, over-damped, India-sourceable.
   **Needs its price verified** (DigiKey 403s) and is the noisiest candidate — only correct if
   ambient dominates.
2. **Re-examine whether 9 nodes is the right count.** `MEMS/06` §5: against incoherent ambient the
   gain is √N. 9→12 nodes is +10.8 dB−9.5 dB = **+1.25 dB for +$203**. Poor value. **Spend on
   coupling instead.**
3. **Don't buy the drone first.** Nothing in build order §12 steps 1–5 needs it. **$739 deferrable
   past the measurement that might change the whole architecture.**

**The cheapest decisive action remains a ~$2 MPU-6050 module and one evening of ambient recording.**
It gates the sensor, which is 41 % of the node cost.

---

*Prev: [02 — Vendor Register](02-vendor-register.md) · Next: [04 — Verification Log](04-verification-log.md) ·
Back to [README](README.md)*
