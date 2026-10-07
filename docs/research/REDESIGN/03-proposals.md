# 03 — Proposals

**Nothing here is applied.** Each item states what MASTER says now, what I suggest instead, the
evidence, and what it costs. Decisions are the user's.

Ordered by **what blocks the most other work**, not by severity.

---

## 1. §5 — Change the regulatory basis *(do this first; it is free)*

| | |
|---|---|
| **MASTER says** | §5: *"Duty-cycle limit ~1%"*, band 865–867 MHz |
| **Suggest** | **Duty cycle ≤2.5%, e.r.p. up to 500 mW**, band **865–868 MHz**, with APC and ≤200 kHz |
| **Evidence** | **G.S.R. 853(E)**, Table-II, read from the Gazette PDF; confirmed against ERC 70-03 / ETSI EN 300 220 |
| **Cost** | **$0.** It is a reading of the law, not a part |
| **Risk** | Must implement **Adaptive Power Control**. Exemption is non-interference/non-protection. ETA/WPC still applies to any device sold |

MASTER applies **Table-I** (Non-Specific SRD: 25 mW, 1%). The Gazette's **Table-II** note names
*"Emergency detection of buried victims"* explicitly. **This project is a Table-II device.**

**What it buys: +13 dB and 2.5× airtime.**

| n (path loss exponent) | Range multiplier from +13 dB |
|---|---|
| 2.0 (free space) | **4.47×** |
| 3.5 (cluttered/urban) | **2.35×** |

§5's own *"200–500 m through rubble"* becomes **470 m–1.2 km at n=3.5** on the same link budget.

> **Flag.** I am reading a statute, not practising law. The table assignment is mine, from the
> Gazette's own category note. **Confirm with whoever signs the ETA application** before it
> becomes load-bearing. If it turns out this is a Table-I device, Scheme C below **still fits**
> at 0.509% — **that is why Scheme C was chosen against the 1% figure too.**

---

## 2. §4.1 + §5.1 + §10.2 — Replace raw streaming with batched detections *(THE redesign)*

| | |
|---|---|
| **MASTER says** | §5.1: 15 B × 2 pkt/s × 20 nodes = 4800 bps, *"PENDING… the architecture must change"*. §4.1: 9 mA → 25 h |
| **Suggest** | **On-node detection; transmit one 24 B batched summary per 60 s** |
| **Evidence** | LightEQ (100 kB RAM, F1 0.99, Cortex-M4); volcano WSN (16% of data); LongShoT (<2 µs) |
| **Cost** | **$0 in parts.** It is firmware. Possibly **−$55/node** if it moves inference on-node |

### Why raw streaming cannot be rescued

| Scheme | Payload | Rate | Duty @SF10 | vs 2.5% | vs 1% |
|---|---|---|---|---|---|
| **A** — §5.1 as written | 15 B | 2/s | **179%** @SF12, 7.6% @SF7 | ❌ | ❌ |
| **B** — per-beat event packet | 21 B | 1/s | **30.5%** | ❌ | ❌ |
| **C** — **batched summary** | **24 B** | **1/60 s** | **0.509%** | ✅ **5× under** | ✅ **2× under** |

**Scheme B is the important negative result.** "Event-driven" alone does **not** fix this —
at one report per second it is still 12× over. **The batching is what makes it legal.**

### Channel capacity, Scheme C

| Nodes | Channel occupancy |
|---|---|
| 11 (9 + 2 spares) | **5.59%** |
| 20 | 10.2% |

### Why batching does not cost localisation

TDoA needs the **beat arrival time** at each node, not a waveform. LongShoT's 2 µs sync gives
**0.3–6 mm** of position error. A 60 s window holds ~60 beats as delta-encoded timestamps.

> **Raw waveform streaming was never required for localisation.** That is the assumption §5.1
> should drop — and it is the reason §10.2's own note ("likely forces on-node timestamping of
> detected beats instead") was already pointing the right way.

### The power budget falls out

| Line | Current |
|---|---|
| ADXL355 sensing | 0.200 mA |
| Cortex-M4 DSP @5% duty | 0.250 mA |
| **TX** — SF10, 0.305 s per 60 s | **0.610 mA** |
| Sleep (STM32WLE5 STOP2) | 0.005 mA |
| **Total** | **1.07 mA** |

| | MASTER §4.1 | **Scheme C** |
|---|---|---|
| Average current | 9 mA | **1.07 mA** |
| CR2032 225 mAh | 25 h | **211 h = 8.8 days** |

**8.4× better, and the 72 h window needs only 77 mAh.**

**This also answers §10.3.** LightEQ runs in **100 kB of RAM on a Cortex-M4** — which is what the
**RAK3172 already contains**. **No MCU decision is needed; the one in the BOM suffices.**

---

## 3. §4.1 — Fix the pulse current, keep the cell

| | |
|---|---|
| **MASTER says** | §4.1 contested note: *"a 225 mAh CR2032… cannot source 40 mA TX pulses"* |
| **Suggest** | **Keep the CR2032. Add a supercapacitor across it** — or switch to **LiMnO₂** |
| **Evidence** | TTN (CR2032 = 10 Ω fresh, 15–30 Ω aged); Avnet (1 F supercap → ~10:1 pulse reduction); Battery Power Tips (Li-MnO₂ = high pulse, Li-SOCl₂ = low) |
| **Cost** | **+$0.70–$2.00/node** |

**The objection is right, but it is about pulse current, not capacity:**

| Cell state | R | Droop @40 mA | Rail (from 3.0 V) | |
|---|---|---|---|---|
| Fresh | 10 Ω | 0.40 V | 2.60 V | marginal |
| Aged | 30 Ω | **1.20 V** | **1.80 V** | **brownout** |

Under Scheme C the cell needs **77 mAh of its 225 mAh** for 72 h. **Capacity was never the
problem.** A supercap buffers the TX pulse and the coin cell survives.

**Chemistry trap worth stating:** Li-SOCl₂ (Saft LS14250) has the best energy density and the
**worst** pulse capability. **Do not "upgrade" to it** without a hybrid pulse capacitor.

---

## 4. §2 + §8.2 — The drone decision is still unmade

| | |
|---|---|
| **MASTER says** | §2 row struck, §8.6 added, Path B costed — **but §8.2 still describes autonomous grid release and no decision is recorded** |
| **Suggest** | **Record the decision.** Either adopt Path B, or amend §8.2 to manual piloting |
| **Cost** | Path B **$738.99**, or **$689.97** with the Mini (§6 below) |

The budget pass proved §2 and §8.2 mutually exclusive and costed the fix. **What is missing is the
choice.** This is the clearest **ADR candidate** in the project: irreversible (it sets the
airframe), cross-cutting (§2, §8.2, §9, §12 step 6), and contested (two sections disagree).

**Not urgent for build order.** §12 steps 1–5 need no airframe. **$739 stays deferrable.**

---

## 5. §10.4 — A correction to the previous pass

| | |
|---|---|
| **Previous pass said** | *"✅ LARGELY ANSWERED — downgrade"*, *"solved in the literature, costs $24.95"* |
| **Suggest** | Keep the downgrade. **Soften "solved" to "de-risked."** |

That claim is accurate **about the literature** and overstated **about this project**. LongShoT is
**LoRaWAN with a gateway and a GPS 1PPS reference**; §10.2's architecture was unsettled when it was
written. The *approach* is validated and the cost is known; **the integration is unbuilt.**

**No number changes.** 2 µs → 0.3–6 mm still holds, and §10.5 is still the binding unknown.
**It is the word "solved" I would change** — flagged because it is my own overstatement.

---

## 6. Two cheaper substitutions found while verifying

**a) Pixhawk 6C → Pixhawk 6C Mini.** $199.00 → **$149.98 [LIVE]**, **−$49.02**.
Still **14 PWM outputs** (8 IO + 6 FMU) with a built-in PWM header; §8.2 needs one servo channel.
Path B becomes **$689.97**.

**b) Enclosure — use prior art instead of designing it.**
`MEMS/04` A8 called coupling-vs-self-righting the unsolved mechanical conflict. **It is solved
prior art:**

| Option | Mechanism | Cost |
|---|---|---|
| **Gimbal** (US 5866827, US 12650530) | Spherical inner housing rotates freely in the outer case; CoG below rotational centre. Outer couples, inner self-levels | moving parts, drop-fragile |
| **✅ Software** (US 9645267) | Rotationally-invariant calibration — solve attitude from the gravity vector a 3-axis part already measures | **~$0** |

**The software route is near-free and consistent with the 3-axis decision already made.**
It also puts a number on `MEMS/04` A8's "bounded, not controlled": the self-orienting art gives
**≤20° tolerable, >30° no acquisition.**

Two further constraints for whoever designs the case:

- **The enclosure must have a better frequency response than the MEMS inside it** (ADI). Geometry
  and height dominate its natural frequencies — **an enclosure resonance inside 10–100 Hz would
  corrupt the band the heartbeat lives in.**
- **Impedance-match the ground** — a cellular-solid casing matched to the soil reduces reflection
  at the interface (Uni. Luxembourg).

> ⚠️ **Freedom to operate.** **SeismicDart** (UAV-dropped sensor darts, NSF/Univ. Houston) and
> **US 11624847 / 10845492** (automated geophysical sensor deployment) cover this mechanism space.
> **Check FTO before mechanism design, not after.** SeismicDart also gives the aerodynamic spec
> for free: **low CoG, aerodynamically stable, lands near-vertical**; drop height increases
> penetration and removes the need for a level landing site.

---

## 7. What I am NOT suggesting changing

| Item | Why not |
|---|---|
| **§6 LSTM → CNN** | An **optimisation**, not a defect. A 38 k-param CNN is cheaper and proven on a Pi 5, but the LSTM is not broken. *(Reconsider if inference moves on-node under Scheme C — then it matters.)* |
| **§7.1 velocity** | **Re-derivation, not redesign.** One hammer test, then the numbers update. Don't touch the solver |
| **§3.2 / §9 sensor** | Gated on the ambient measurement. 41% of node cost. **No change until that exists** |
| **§9 totals** | Rebuilt 19 days ago at live prices. Only the two substitutions above would move it |
| **The Delsar argument** | Survives at every figure computed. ~$15,000 vs $1,845 |

---

## Summary of proposed deltas

| # | Change | Δ cost | Blocks |
|---|---|---|---|
| 1 | §5 → Gazette Table-II (500 mW / 2.5%) | **$0** | nothing — do it now |
| 2 | §5.1/§4.1/§10.2 → Scheme C batched detections | **$0** (firmware) | **resolves §10.3** |
| 3 | §4.1 → supercap across the coin cell | **+$0.70–2.00/node** | — |
| 4 | §2/§8.2 → record the airframe decision | $0 (ADR) | §12 step 6 |
| 5 | §10.4 → "de-risked", not "solved" | $0 | — |
| 6a | Pixhawk 6C → 6C Mini | **−$49.02** | — |
| 6b | Enclosure → rotation-invariant calibration | **~$0** | §12 step 5 |

**Net: roughly −$30 on the system, and §10.2 and §10.3 both close.**

**The sequencing point:** items 1 and 2 cost nothing, need no hardware, and unblock the MCU
choice — **and §12's build order touches neither.** §10.1 is still the right first bench
experiment, but **the data architecture can be settled in parallel, on paper, today.**

---

*Next: [04 — Verification Log](04-verification-log.md) · Back to [README](README.md)*
