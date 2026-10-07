# 00 — My Own Independent Arithmetic

Computed by me, from raw inputs, **before** any critic subagent reported. Recorded separately so
the critics' findings can be checked against an independent source rather than agreeing with
themselves. Nothing here is applied to `MASTER.md`.

Script of record: `own.py` (session scratchpad). Date **2026-10-06**.

---

## 1. §8.3's impact figure is wrong by 10–100×

**MASTER §8.3 claims:** drop 3–4 m → 7.7 m/s → **"15–20 G, inside foam tolerance."**

`v = sqrt(2gh)` gives **7.67 m/s at 3 m** — that part is right. The G figure is not.
`a = v²/(2d)`, where `d` is the **stopping distance**:

| Stopping distance | Deceleration (h = 3 m) |
|---|---|
| 150 mm | 20 G ← *what §8.3's number implies* |
| **15 mm** (the node's entire height, fully crushed) | **200 G** |
| 10 mm | 300 G |
| 5 mm | 600 G |
| 3 mm (realistic foam crush onto concrete) | **1000 G** |

**To actually reach 15–20 G you need 150–200 mm of crush.** The node is **15 mm tall**.

> **§8.3's number is not conservative or optimistic — it is dimensionally impossible for the
> stated geometry.** Even with the entire node crushing to zero thickness you get 200 G.
> Realistic impact onto rubble is **600–1300 G**.

This is **ASSERTED** in MASTER with no derivation shown; **COMPUTED** here. The spec's
"foam shell absorbs 15–20 G" sizing is built on it, so the foam is sized for the wrong load.

---

## 2. The 8 g node mass is impossible

**MASTER §4 claims:** *"~4 cm dia × 1.5 cm, ~8 g assembled"* with a **3 g tungsten base**.

| Item | Mass |
|---|---|
| CR2032 cell | 3.00 g |
| tungsten ballast (spec'd) | 3.00 g |
| ADXL355 LGA-14 | 0.12 g |
| RAK3172 module | 1.90 g |
| PCB, 30 mm, 4-layer | 1.50 g |
| cell holder | 1.20 g |
| antenna + u.FL | 1.00 g |
| PLA shell | 2.50 g |
| EVA foam | 1.00 g |
| passives | 0.30 g |
| **Total** | **15.5 g** |

**The cell and the ballast alone are 6 g of the claimed 8 g budget.** Realistic total is
**~1.9× the spec**, and that is before fasteners or potting.

Not fatal on its own — §8.4 shows the airframe has margin — but it means **every number derived
from node mass is wrong**, and mass is the input to the coupling question (§ below).

*Component masses are [EST] from typical package data, not pulled from datasheets in this pass.
Flagged for the hardware critic to confirm.*

---

## 3. Node position uncertainty destroys the localization spec

**This is the one I think is hardest to answer.**

§8.5: *"Node position = drone GPS at moment of release + drift correction."*
§7.2 claims **±0.05–0.1 m** localization at 9–16 nodes.

**TDoA cannot locate a target more precisely than it knows where its own sensors are.**

| GPS CEP | Post-impact bounce/roll | Node position σ |
|---|---|---|
| 2 m | 0.5 m | **2.06 m** |
| 3 m | 1.5 m | **3.35 m** |
| 5 m (urban canyon / multipath beside standing structures) | 1.5 m | **5.22 m** |

**The spec's claimed accuracy is ~30× better than the position knowledge of its own sensors.**
A node that is dropped from 3–4 m onto irregular rubble also *bounces and rolls* an unknown
distance — that term is not in §8.5 at all.

> §7.2 already corrects the table for a *timing* floor (±0.3 m). **It never corrects it for the
> node-position floor, which is an order of magnitude larger.** The ±0.05 m row is not merely
> optimistic; it is unreachable by this deployment method regardless of sensor, clock or band.

**Consequence:** either the system adopts inter-node ranging (UWB, as §11 hints) and pays for it
in money, power and complexity, or **the localization claim must be restated in metres.**

---

## 4. The project has been optimizing the wrong timing term

§10.4 declares time sync *"largely answered"* at **2 µs**, which at 300 m/s is **0.6 mm** of
position error. True — and irrelevant.

TDoA error is driven by the **arrival-time pick** uncertainty, not the clock. For time-delay
estimation, σ_t scales roughly as `1/(B·√SNR)` — **inversely with bandwidth**:

| Band | B | SNR 20 dB | SNR 10 dB | SNR 3 dB | SNR 0 dB |
|---|---|---|---|---|---|
| **0.5–4 Hz** (§6 as written) | 3.5 Hz | 0.029 s | 0.090 s | 0.202 s | 0.286 s |
| → position error at v=300 m/s | | **8.6 m** | **27 m** | **61 m** | **86 m** |
| **10–100 Hz** (proposed elsewhere) | 90 Hz | 0.0011 s | 0.0035 s | 0.0079 s | 0.011 s |
| → position error at v=300 m/s | | **0.33 m** | **1.05 m** | **2.4 m** | **3.3 m** |

**Clock sync at 2 µs = 0.0006 m.** The pick uncertainty in the spec's own band is
**four to five orders of magnitude larger.**

> **Two conclusions, and the second is the useful one.**
> 1. §7.2's accuracy table is unreachable in a 3.5 Hz band at any plausible SNR.
> 2. **Bandwidth is the design variable that buys localization accuracy.** Narrowing the filter
>    to 0.5–4 Hz to isolate the heartbeat *rate* is precisely what destroys the timing
>    resolution. The band choice and the localization spec are in direct conflict, and nobody
>    has written that down.

This also means §10.4's "solved" and §10.5's velocity model are both **second-order** next to a
term nobody has costed. Even a perfect velocity model cannot rescue an 8.6 m pick error.

*Method note: `1/(B·√SNR)` is a rule-of-thumb form of the Cramér–Rao bound for time-delay
estimation, not the exact CRLB (which carries an RMS-bandwidth term and a BT factor). The
**order of magnitude** is what matters here and is robust to that choice. Independent derivation
delegated to the DSP critic.*

---

## What I could be wrong about

- **Impact G**: if the node is designed to land on a *deliberately crushable sacrificial nose*
  substantially taller than 15 mm, the geometry changes. The spec does not describe one.
- **Mass**: component masses are estimates. A smaller cell and no holder would cut several grams.
- **Position**: RTK GPS (~2 cm) would collapse the position term — at real cost, and it does not
  fix post-impact bounce.
- **Timing**: the rule-of-thumb σ_t overstates error for a *coherent template match* over many
  beats; averaging N≈60 beats buys √60 ≈ 7.7×. That reduces the 0.5–4 Hz figures to ~1.1 m at
  20 dB — **better, but still 10× the spec's claim, and it assumes the beats are coherent over
  60 s, which HRV says they are not.** The conclusion survives the correction.

---

## 5. Scheme C's 24-byte packet cannot carry what TDoA needs

The REDESIGN pass's headline proposal is a **24 B batched summary once per 60 s**, justified as
*"~60 beats as delta-encoded timestamps."* **I checked whether 24 B can hold them. It cannot.**

**Budget of a 24 B = 192-bit packet:**

| Field | Bits |
|---|---|
| node ID | 16 |
| packet seq / type | 8 |
| CRC | 16 |
| window start timestamp | 32 |
| **overhead** | **72** |
| **left for beat data** | **120** |

| Beats encoded | Bits available per beat |
|---|---|
| 60 | **2.0** |
| 30 | 4.0 |
| 10 | 12.0 |

**What a given bit-depth buys, as timing precision over a 60 s window:**

| Bits/beat | Time quantum | Position error at v=300 m/s |
|---|---|---|
| 2 | 15 s | **4500 m** |
| 4 | 3.75 s | 1125 m |
| 8 | 0.234 s | 70 m |
| **16** | 0.916 ms | **0.275 m** ← first row that is useful |

**The requirement, derived properly:** for ±0.3 m at 300 m/s you need Δt = **1.0 ms**.
Over a 60 s window that is **15.9 bits** per absolute timestamp, or **11.0 bits** per
delta (assuming ≤2 s between beats).

> **60 beats × 11 bits = 658 bits = 82 bytes.**
> **Scheme C allocates 15 bytes. It is short by a factor of ~5.5.**

At the 2 bits/beat that 24 B actually permits, the timing quantum is **15 seconds** — a position
error of **4.5 km**. The scheme as specified does not degrade TDoA; it **destroys** it.

**This is an information-theoretic result, not an engineering estimate.** No amount of firmware
skill recovers bits that were never sent.

**It is fixable** — and the fix is cheap, which is why this matters rather than kills:

- **82 B per 60 s at SF10** is still roughly **1.1% duty cycle** (ToA scales sub-linearly with
  payload), i.e. still legal under the 2.5% reading and marginal under 1%.
- Or **send fewer beats**: 10 beats × 16 bits = 20 B, comfortably inside 24 B, and 10 beats is
  plenty to establish a rate and a confidence.
- Or **transmit only the detection, not the timestamps**, and accept area-localization.

**The correct conclusion is not "Scheme C is wrong" but "Scheme C's payload was never
dimensioned against its own purpose."** The duty-cycle arithmetic was audited 16/16 and
reproduces perfectly — of a payload size that was chosen without checking what had to fit in it.

---

## 6. Does coherent averaging rescue the narrow band? Partly — and not enough

Honest self-check on §4 above. Averaging N beats buys √N:

| N beats | Gain |
|---|---|
| 10 | 3.2× |
| 60 (one 60 s window) | **7.75×** |
| 600 (ten windows, 10 min) | 24.5× |

Applying N=60 to the 0.5–4 Hz band:

| SNR | σ_t after averaging | Position error at 300 m/s |
|---|---|---|
| 20 dB | 3.7 ms | **1.11 m** |
| 10 dB | 11.7 ms | **3.50 m** |
| 3 dB | 26.1 ms | **7.83 m** |

**So the narrow band gives metre-scale localization at best, in a quiet site, at high SNR.**
Not the ±0.05–0.1 m §7.2 claims — but **not useless either**, which is the honest reading.

**Caveat that weakens even this:** coherent averaging over 60 beats assumes the beat train is
**phase-coherent** across the window. §6 relies on **HRV of ±5–10%** to distinguish humans from
machinery. **HRV is exactly the thing that destroys coherence.** You cannot simultaneously
claim the beat interval varies enough to identify a human and is stable enough to average
coherently for 60 s. The two arguments in §6 are in tension, and resolving it costs accuracy on
one side or the other.

> The defensible position: **average the ENVELOPE (incoherent averaging, gain ~N^(1/4))** which
> is HRV-immune, and accept the smaller gain. That lands the 0.5–4 Hz band back near
> **3–8 m** — and makes the wider band the only route to sub-metre localization.

---

## 7. §7.2's coverage table contradicts §7.2's own spacing rule

§7.2 states the rule itself: **`d = r·√2`**. It then builds a coverage table at **10 m spacing**
while §3.3 assumes **r = 3 m**. Those cannot both hold — at r = 3 m the rule gives **4.24 m**.

The spec *notices* this ("spacing vs range") but **never rebuilds the table**, so the node counts
and the cost that flows from them are still the 10 m figures.

**Node count to cover the claimed areas at the spec's own correct spacing:**

| Claimed coverage | Spec node count | Honest count at r = 3 m | Factor |
|---|---|---|---|
| 75 m² | 3 | 4.2 | 1.4× |
| 150 m² | 5 | 8.3 | 1.7× |
| 400 m² | 9 | **22.2** | **2.5×** |
| 900 m² | 16 | **50.0** | **3.1×** |

**And the cost, at §9's $67.75/node — this is where it becomes a project-level problem:**

| Area | r = 3 m | r = 1 m | r = 0.5 m |
|---|---|---|---|
| 400 m² | $1,506 | $13,550 | $54,200 |
| 900 m² | $3,388 | $30,488 | $121,950 |

> **The cost model is not linear in the unmeasured §10.1 number — it is quadratic.**
> Halving the detection range **quadruples** the node count and the cost.
> If §10.1 returns r = 1 m instead of 3 m, the 400 m² deployment costs **$13,550** and
> **the entire Delsar cost argument (~$15,000) evaporates at a single bench measurement.**

That is the real stake of §10.1, and the spec does not say it. §9 presents **$1,845** as *the*
system cost when it is the cost of one point on a steep curve, at the most optimistic
assumption in the document.

**This also reframes the sensor decision.** §9 calls the ADXL355 *"41% of node cost"* and the
$55 line the obvious saving. **Wrong lever.** A cheaper, noisier sensor **reduces r**, and cost
scales as **1/r²**. Saving $145 across 9 nodes while halving r turns a $1,506 deployment into a
$13,550 one. **Sensor noise is a cost multiplier, not a cost line.**

---

## Summary of my own seven findings

| # | Finding | Severity |
|---|---|---|
| 1 | §8.3 impact G wrong by 10–100× (200–1300 G, not 15–20 G) | **Fatal to node design as drawn** |
| 2 | §4's 8 g node mass is ~1.9× too low; cell + ballast alone are 6 g | Serious |
| 3 | Node position known to ±2–5 m; §7.2 claims ±0.05 m — **30× gap** | **Fatal to localization spec** |
| 4 | Pick uncertainty (metres) swamps clock sync (0.6 mm) by 10⁴ | **Project priorities inverted** |
| 5 | Scheme C's 24 B holds 2 bits/beat; TDoA needs 82 B — **5.5× short** | **Fatal to Scheme C as written; cheaply fixable** |
| 6 | HRV-based ID and coherent averaging are mutually exclusive | Serious |
| 7 | Coverage table ignores its own spacing rule; cost scales as **1/r²** | **Fatal to the cost argument** |

**Findings 3, 4 and 7 are the ones I would defend hardest.** None of them depends on a
literature search, a vendor price, or a regulatory reading — they are internal contradictions
and error-propagation arguments, derivable from the spec's own numbers.

**The through-line:** the project has repeatedly audited *the arithmetic it chose to do*, and
the audits pass. What has never been audited is **whether the right quantity was being
computed.** Findings 4, 5 and 7 are all instances of that one failure mode.
