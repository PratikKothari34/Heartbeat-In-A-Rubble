# 06 — Adversarial Audit of the Three Prior Research Passes

**Target:** `docs/research/MEMS/`, `docs/research/BUDGET/`, `docs/research/REDESIGN/` — not MASTER.
**Date:** 2026-10-06 · **Stance:** devil's advocate. Where a prior claim survives my own evidence,
I say so plainly.

**Evidence labels used throughout:** **[MEASURED]** = someone put an instrument on it ·
**[COMPUTED]** = I derived it here from raw inputs, work shown · **[ASSERTED]** = stated in a
source without derivation or measurement.

> **Nothing in this file is applied.** It audits; it does not fix. No file outside `docs/critique/`
> was touched.

---

## Verdict up front

| # | Prior claim | Verdict | One line |
|---|---|---|---|
| 1a | G.S.R. 853(E) has a Table-II allowing **500 mW e.r.p. @ ≤2.5%**, note names buried victims | **CONFIRMED** | I pulled the Gazette PDF and read it myself. Verbatim match, including "e.r.p." and the buried-victims note |
| 1b | Band is **865–868 MHz**, not MASTER's 865–867 | **CONFIRMED** | Rule 1(1) title and all four tables say 865–868. MASTER is on the superseded 2005 instrument |
| 1c | Therefore the project gets **+13 dB and 2.5× airtime** | **WEAKENED — badly** | +13 dB is a *legal ceiling*, not a reachable gain. The BOM radio tops out at +22 dBm. **Real gain ≤8 dB; real range multiplier 1.69×, not 2.35×.** No PA is in the BOM or the budget |
| 1d | Table-II applies to this device | **WEAKENED** | The note is a *non-exhaustive* illustration attached "for the purpose of this Table" — it is interpretive, not a device class. And the pass omitted **rule 5: type approval is mandatory regardless** |
| 2a | **ToA = 0.3052 s** for 24 B @ SF10/BW125/CR4-5 | **OVERTURNED** | My independent Semtech computation gives **0.370688 s**. No combination of CR, header, CRC, LDRO or preamble reproduces 0.3052. **All four downstream numbers inherit the error** |
| 2b | Scheme C duty **0.509%**, 11 nodes **5.59%** | **OVERTURNED (arithmetic)** | Correct values **0.618%** and **6.80%**. Conclusion "legal" survives; the numbers do not |
| 2c | 24 B carries "~60 beats as delta-encoded timestamps" | **OVERTURNED — fatally** | **[COMPUTED]** 60 beats at the 2 µs precision LongShoT provides needs **156 bytes**. 24 B buys **2.13 bits/beat**. The scheme is information-theoretically broken by **6.5×** |
| 2d | **1.07 mA** average, **211 h** on a CR2032 | **OVERTURNED** | Budgets **zero receive current**. A mesh node that never listens is a beacon, and §2's self-healing mesh is dead. Corrected: **0.73–1.93 mA, 116–307 h** |
| 2e | Channel occupancy accounts for the array | **OVERTURNED** | Naive airtime sum. No ACKs, no relay re-occupancy, no collisions. **[COMPUTED]** with ALOHA + 2 hops + ACK: **32.3% at 11 nodes, 83.2% at 20** — 5.8× and 14.9× the claim |
| 3 | "LightEQ fits in 100 kB on a Cortex-M4, so **§10.3 is closed**" | **OVERTURNED** | **STM32WLE5JC has 64 kB SRAM**, not 100 kB. The 60 s × 100 Hz × 3-axis input buffer **alone is 70.3 kB — 110% of total RAM.** The MCU question is wide open, and the BOM part is disqualified |
| 4a | A supercapacitor fixes the CR2032 pulse problem | **CONFIRMED in principle** | **[COMPUTED]** recharge 5τ = 11–33 s against a 60 s interval. Timing works. Leakage ≤1.9% of budget. Both fine |
| 4b | "KEMET/Surge parts are adequate; CAP-XX is quote-only" | **OVERTURNED** | **[COMPUTED]** At KEMET's own 25 Ω ESR, IR drop at 40 mA is **1.00 V** — it *recreates* the brownout it was bought to fix. Only the ≤100 mΩ CAP-XX class works. The orderable part is the wrong part |
| 5 | Pixhawk 6C Mini saves $49 with no loss | **WEAKENED — unverified** | The only spec checked was PWM count. UART count, IMU redundancy, CAN and flash were never compared. A saving asserted on one axis of a multi-axis part |
| 6 | Coupling-vs-self-righting is "solved prior art", software route ~$0 | **OVERTURNED** | Conflates **orientation** with **mechanical coupling**. The MEMS pass's own §6.1 calls the spike/anchor interface *"unsolved… the dominant term… this project's actual contribution."* The pass solved the half that was never the problem |
| 7a | "115 referred sources" | **WEAKENED** | Inflated by range-rows never itemised (R3 lists 13 rows, counts 22; R5 lists 6, counts 21) and by 13 **patents** counted as literature |
| 7b | "16/16 arithmetic reproduces" | **CONFIRMED as stated, meaningless as evidence** | They reproduce — from a wrong ToA constant. **This is the methodology's structural blind spot** |
| 7c | "38 URLs three-state verified", E17 bug caught | **CONFIRMED** | Real finding, honestly reported, correctly re-run. Credit where due |
| 7d | Pattern of findings is suspiciously pro-viability | **CONFIRMED** | 5 of 6 headline findings move the project toward "more feasible." The one that doesn't (E17) is about the pass's own tooling, not the project |

---

## The prior conclusion most likely to be wrong

> ### **Scheme C — "24 bytes per 60 s carries ~60 beat arrival times."**
>
> Not a rounding error. **An information-theoretic impossibility, off by 6.5×.**

This is the lead because it is the most load-bearing *and* the most wrong. Scheme C is the proposed
answer to §10.2, it is claimed to close §10.3, and it is the basis for the 1.07 mA / 211 h power
result that rescues §4.1. If it does not carry the payload it claims, all three of those collapse
together.

### The bit budget — [COMPUTED]

Scheme C's purpose is to deliver **beat arrival times** for TDoA. The pass's own justification:

> *"TDoA needs the beat arrival time at each node… LongShoT's 2 µs sync gives 0.3–6 mm of position
> error. A 60 s window holds ~60 beats as delta-encoded timestamps."*

So the timing resolution that must survive into the payload is set by the pass's own citation: **2 µs.**

| Line | Bits | Note |
|---|---|---|
| Total payload | **192** | 24 B |
| Node ID | 16 | MASTER §5 packet spec, 2 B |
| CRC | 16 | MASTER §5 packet spec, 2 B |
| Window epoch anchor | 32 | MASTER §5 uses a 4 B timestamp. Deltas without an absolute anchor are useless for *cross-node* TDoA |
| **Remaining for ~60 beats** | **128** | |
| **Bits per beat** | **2.13** | |

What 2.13 bits/beat buys, encoding an inter-beat interval over a ~1 s dynamic range:

| Bits/beat | Quantisation | Position error @150 m/s | @3000 m/s |
|---|---|---|---|
| **2** | **250 ms** | **37.5 m** | **750 m** |
| 4 | 62.5 ms | 9.4 m | 187 m |
| 8 | 3.9 ms | 0.59 m | 11.7 m |
| 12 | 244 µs | 37 mm | 0.73 m |
| 16 | 15.3 µs | 2.3 mm | 0.05 m |

At 2 bits/beat the position error is **37–750 m** on a system whose §7.2 target is **±0.3 m**.

### Running it the other way — what the claim actually requires

Delta-encoded IBI, range 0.3–2.0 s, resolution 2 µs:

```
bits/delta = log2(1.7 / 2e-6)        = 19.70
60 beats   = 60 × 19.70              = 1182 bits = 148 bytes
+ 32-bit anchor + 16 ID + 16 CRC     =  156 bytes
```

**Scheme C needs 156 bytes. It budgets 24.** [COMPUTED]

### How many beats *do* fit in 24 B?

| IBI resolution | bits/beat | Beats that fit (need 60) |
|---|---|---|
| 2 µs (LongShoT-matched) | 19.7 | **6.5** |
| 100 µs | 14.1 | 9.1 |
| 1 ms | 10.7 | 11.9 |
| 10 ms | 7.4 | 17.3 |

Even at 10 ms resolution — which throws away 5000× of LongShoT's sync and yields **1.5 m** error at
150 m/s — only 17 beats fit.

### Second audit pass on this finding

**Where I could be wrong, and why I don't think I am:**

1. *Maybe only one or two representative beats per window are sent, not 60.* Then the pass should
   not say "~60 beats," and the claim that batching costs localisation nothing becomes untested —
   averaging beats destroys the per-beat arrival structure TDoA consumes. **Either reading breaks a
   stated claim.**
2. *Maybe the anchor is implicit in the LoRa frame timestamp at the gateway.* Gateway receive time
   is corrupted by queueing, ALOHA backoff and relay hops — exactly the terms LongShoT exists to
   remove. Using it as the anchor discards the 2 µs sync the argument rests on.
3. *Maybe deltas compress below entropy.* IBI is biologically variable (§6 relies on ±5–10% HRV as
   the human discriminator); the variability **is** the signal. You cannot compress away the thing
   you are measuring. Entropy coding might recover ~2×, not 6.5×.
4. *Maybe 2 µs is over-spec and 1 ms is fine.* Then §7.2's ±0.3 m target is unreachable and
   **LongShoT's $24.95 GPS line in §9 is unjustified** — the prior pass cannot have it both ways.

**I audited this twice and it holds both times. 24 B is not a payload size; it is a number that
makes the duty-cycle table come out legal.**

---

## 1. The Table-II spectrum finding

**This was my top priority and it is the one place the prior pass did the hardest work properly.**

### What I did independently

I fetched `thc.nic.in`'s hosted copy of the Gazette, confirmed the `%PDF-` header **[MEASURED]**
(572,832 bytes, PDF-1.6), and extracted the text with `pdfminer` under `py -3.12` — I did not
rely on the prior pass's conversion. **Note:** the prior pass claims it converted the PDF to
`gazette/IN_GSR.md`. **No such file exists anywhere in the repository or in git history.** The
conversion is unreproducible from the artifacts on disk; I had to redo it. That is a provenance
failure, not a correctness failure — my own extraction vindicates the reading.

### Verbatim from the primary source [MEASURED]

Rule 1(1) — the band:

> *"These rules may be called the **Use of Low Power Equipment in the Frequency Band 865-868 MHz**
> for Short Range Devices (Exemption from Licence) Rules, 2021."*

Table-I, Non-Specific Short Range Devices: **865-868**, **25 mW e.r.p.**, *"Duty cycle limit: 1%"*,
FHSS, ≤50 kHz for 58+ hop channels, EN 300 220.

Table-II, *Tracking, Tracing and Data Acquisition Devices*: **865-868**, **500 mW e.r.p.**,
*"Adaptive Power Control (APC) required and the following Duty Cycle restrictions: Duty cycle ≤ 10%
for network access points; ≤ 2.5% otherwise"*, **≤ 200 kHz**, EN 300 220.

The note:

> *"For the purpose of this Table, Tracking, Tracing and Data Acquisition Devices **also include
> devices for Emergency detection of buried victims** and valuable items such as detecting avalanche
> victims; Person detection and collision avoidance; Meter reading; Sensors…"*

Rule 2(1)(c) defines e.r.p. explicitly:

> *"'effective radiated power' or e.r.p. means the product of the power supplied to an antenna and
> its gain in a given direction **relative to a half-wave dipole**."*

### Verdict on each sub-question

| Question | Finding |
|---|---|
| Does Table-II say 500 mW **e.r.p.**? | **YES — CONFIRMED.** Column 3 reads "500 mW e.r.p." and rule 2(1)(c) defines e.r.p. dipole-referenced. **The prior pass got the units right.** EIRP would be 29.15 dBm; e.r.p. is 27.0 dBm |
| 865–868 or 865–867? | **865–868. CONFIRMED — MASTER is wrong.** The 865–867 figure is from the *superseded* 2005 RFID rules, which rule 1 expressly supersedes. **MASTER §4 and §5 are quoting a dead instrument** |
| Later amendment superseding 2021? | **None found.** Searching turned up only a Jan-2024 SRRF *exemption-list* update that does not alter these four tables. I did **not** find a superseding G.S.R. **This is a genuine gap in my audit** — my web access was rate-limited before I could check WPC's own regulations index. **Treat "2021 is current" as [ASSERTED], not verified** |
| Is "buried victims" in the category definition or a note? | **A NOTE — and the prior pass's framing overstates it.** The device category in the table header is *"Tracking, Tracing and Data Acquisition Devices"*. The buried-victims text is in a Note beginning *"For the purpose of this Table… **also include**"*. It is an illustrative, non-exhaustive gloss. It is strong interpretive support — but a note is not an operative provision, and a regulator is not bound by an illustration |
| Conditions the pass omitted | **Partially. The pass did state APC and ≤200 kHz.** It did **not** flag that the ≤200 kHz is a *hard* occupied-bandwidth cap — **LoRa at BW125 complies, but BW250 and BW500 do not**, closing off the obvious "go wider to cut airtime" escape. It also did not note Table-I's FHSS requirement, which MASTER's architecture does not meet either |
| Network access point or "other"? | **"Other" ⇒ 2.5%.** A dropped sensor node is not a network access point. The pass used 2.5% correctly. *(The drone gateway, however, might qualify for 10% — an upside the pass missed)* |
| Device or user/application exemption? | **DEVICE, with a mandatory approval gate the pass under-weighted.** Rule 3 exempts the *apparatus*. But **rule 5(1): "such equipment shall be type approved"** — unconditional, applying to every table. The pass mentions "ETA/WPC still applies" in a risk line; it belongs in the finding, because **a Table-II claim is a claim you must defend in a type-approval filing**, not a reading you adopt unilaterally |

### The part that is wrong: "+13 dB" — [COMPUTED]

The pass's R1 conclusion, repeated in the README and `03` §1, is that the finding is worth
**"+13 dB of ERP = a 4.47× range multiplier (n=2), 2.35× (n=3.5)"**, turning §5's 200–500 m into
**470 m–1.2 km**.

The dB arithmetic is right: `10·log10(500/25) = 13.01 dB`, giving 4.472× and 2.354×. **A41 and A42
reproduce.** But they compute the wrong quantity.

**+13 dB is the headroom between two legal ceilings. It is not a gain this project can realise.**

| Radio | Max conducted | e.r.p. @0 dBi | Gain vs 25 mW | Range mult, n=3.5 |
|---|---|---|---|---|
| SX1276 (MASTER §5) | +20 dBm | 100 mW | **6.0 dB** | **1.49×** |
| STM32WLE5 hi-PA (the actual BOM part) | +22 dBm | 158 mW | **8.0 dB** | **1.69×** |
| Table-II ceiling | +27 dBm | 500 mW | 13.0 dB | 2.35× |

**Shortfall: 5.0 dB from the BOM radio, 7.0 dB from the SX1276.** Reaching 500 mW e.r.p. requires an
**external power amplifier** — a part that appears in no BOM, no cost line, and no power budget in
any of the three passes. An external PA at +27 dBm also roughly triples TX current, which feeds
straight back into the 1.07 mA budget that Scheme C depends on.

So: `03` §1's claim that the change is **"$0 — it is a reading of the law, not a part"** is true of
the *duty cycle* half (2.5% vs 1% is genuinely free) and **false of the power half**. The headline
"20× the radiated power" is not purchasable at $0.

### Verdict

**SOLID on the law. WRONG on what the law buys.**

The regulatory reading is correct and is the strongest single result in the three passes — I
confirmed it from the primary instrument, independently. **Keep it.** But the "+13 dB / 2.35× range"
figure is a ceiling-to-ceiling delta presented as an engineering gain, and it must be replaced by
**+8 dB / 1.69×** unless a PA is budgeted. The downstream link-budget optimism ("200–500 m becomes
470 m–1.2 km") does not survive.

**Second pass — where I could be wrong:** if the design used a +3 dBi antenna, e.r.p. rises ~3 dB
and the gap narrows to ~2 dB. But §4's node is a 4 cm puck with a u.FL whip lying in rubble;
assuming positive gain there is optimistic, and ground proximity typically costs gain rather than
adding it. I am also relying on a *superseding-amendment* check I could not complete.

---

## 2. Scheme C — the data architecture

### 2.1 Time-on-air, recomputed from the Semtech formula — [COMPUTED]

```
Ts        = 2^SF / BW
Tpreamble = (n_pre + 4.25) · Ts
nPayload  = 8 + max( ceil( (8·PL − 4·SF + 28 + 16·CRC − 20·IH) / (4·(SF − 2·DE)) ) · (CR+4), 0 )
ToA       = Tpreamble + nPayload·Ts
```

At SF10, BW125, CR4/5, 8-symbol preamble, explicit header, CRC on, LDRO off (Ts = 8.192 ms < 16 ms,
so LDRO is correctly *off* at SF10):

```
Ts        = 1024/125000            = 0.008192 s
Tpreamble = 12.25 × 0.008192       = 0.100352 s
num       = 8(24) − 40 + 28 + 16   = 196
den       = 4 × 10                 = 40
nPayload  = 8 + ceil(196/40)×5 = 8 + 5×5 = 33
Tpayload  = 33 × 0.008192          = 0.270336 s
ToA       = 0.370688 s
```

**ToA = 0.370688 s. The pass claims 0.3052 s.** Discrepancy **+21.4%**.

**Validation of my implementation:** against published LoRaWAN airtimes for a 51 B application
payload (64 B PHY) — SF10: mine 0.6984 s vs published 0.6984 s (Δ = −0.00003); SF12: mine 2.7935 s
vs published 2.7955 s (Δ = −0.002). **Exact to four decimals at both spot checks.** My formula is
right.

**I then brute-forced the claimed value.** Over CR ∈ {4/5…4/8} × explicit/implicit header ×
CRC on/off × LDRO on/off × preamble ∈ {6,8,10,12} — **128 combinations — not one yields 0.3052 s**
(nearest: 0.3072 s at SF8/PL≈100, a different spectral factor entirely). 0.3052 s is not a defensible
parameter choice; it is an error.

#### Everything that inherits it

| Pass claim | Recomputed | Error |
|---|---|---|
| A35 ToA 24 B SF10 | **0.370688 s** | +21.4% |
| A39 Scheme C duty 0.509% | **0.6178%** | +21.4% |
| A40 11 nodes 5.59% | **6.796%** | +21.6% |
| 20 nodes 10.2% | **12.36%** | +21.2% |
| TX line 0.610 mA | see §2.4 | — |
| A36 ToA 15 B SF12 **0.8929 s** | **1.155072 s** (LDRO on) | **+29.4%** |
| A37 §5.1 @SF12 **179%** | **231%** per node (4620% for 20 nodes) | +29% |
| A38 §5.1 @SF7 **7.6%** | **9.27%** per node | +22% |
| Scheme B 21 B SF10 **30.5%** | **37.07%** | +21.5% |

**Note the direction:** every correction makes the *illegality* of Schemes A and B worse and
Scheme C's margin thinner. The pass's qualitative conclusions (A and B illegal, C legal against
2.5%) survive. **Its numbers do not. "16 of 16 reproduce" certified a consistent error.**

### 2.2 Information budget

**Covered in full above as the lead finding.** Verdict: **OVERTURNED, 6.5× short.**

### 2.3 Channel occupancy under a realistic model — [COMPUTED]

The 5.59% figure is `11 × ToA / 60 s` — a naive airtime sum. It omits every mechanism that actually
consumes a shared channel.

**Pure (unslotted) ALOHA**, which is what an uncoordinated LoRa array is. Vulnerable period = 2·ToA,
so `P(success) = e^(−2G)`, throughput `S = G·e^(−2G)`, peaking at **G = 0.5 → S = 18.4%**:

| Nodes | Offered G | P(collision) | Throughput |
|---|---|---|---|
| 9 | 5.56% | 10.5% | 4.98% |
| 11 | 6.80% | **12.7%** | 5.93% |
| 20 | 12.36% | **21.9%** | 9.65% |

**Even at the claimed single-hop load, 1 in 8 packets collides.** The pass never computes a loss
rate — it reports occupancy as though a channel below 100% is a channel that works.

**Add mesh relay.** §2 specifies a self-healing multi-hop mesh. A relayed packet occupies the
channel again at every hop:

| Nodes | Tx/pkt | Occupancy | P(success) |
|---|---|---|---|
| 11 | 1 | 6.80% | 87.3% |
| 11 | 2 | 13.59% | 76.2% |
| 11 | 3 | 20.39% | 66.5% |
| 20 | 3 | **37.07%** | **47.7%** |

**Add ACKs and retransmission.** A 4 B ACK at SF10 is **0.2068 s** — 56% of a data packet, because
LoRa airtime is dominated by preamble and spreading, not payload. With mean attempts = 1/P(success):

| Nodes | Hops | Naive w/ ACK | Mean attempts | **Real occupancy** |
|---|---|---|---|---|
| 11 | 2 | 21.2% | 1.53 | **32.3%** |
| 20 | 2 | 38.5% | 2.16 | **83.2%** |

**The claim understates by 5.8× at 11 nodes and 14.9× at 20.** The audit brief anticipated 2–5×;
it is worse, because the ACK is nearly as expensive as the data.

And **32.3% occupancy is illegal** — Table-II's ceiling is 2.5% per device, and a node emitting
2 hops × 1.53 attempts × 0.618% = **1.89%** is inside the limit only if nothing is retried twice.
The headroom the README advertises as *"5× under"* is, under a realistic MAC, **not there**.

Also unbudgeted: join/sync traffic, LongShoT's own sync exchanges (it is a *protocol*, it costs
airtime), and neighbour discovery for a self-healing mesh.

**Where I could be wrong:** pure ALOHA is the pessimistic bound. LoRa's capture effect lets a
stronger signal survive a collision, and different SFs are quasi-orthogonal — a real system recovers
some of this. Slotted operation (which arXiv 2405.14740, a paper the pass itself holds, is about)
would double throughput. **But none of that is in Scheme C**, and the pass's own number is the
naive one. My point stands: **5.59% is a lower bound presented as a result.**

### 2.4 The 1.07 mA power budget — line by line

| Line | Claim | Verdict |
|---|---|---|
| ADXL355 sensing | 0.200 mA | **CONFIRMED [MEASURED, datasheet].** The held ADXL354/355 datasheet states *"ADXL355 in measurement mode: 200 μA"* and the Current table gives 150 µA typ (LDO enabled)/200 µA. **Correctly cited** |
| Cortex-M4 DSP @5% | 0.250 mA | **PLAUSIBLE but under-scoped.** Back-solves to 5.0 mA active — about right for an M4 @48 MHz from flash (ST's ~103 µA/MHz ⇒ ~5–7 mA). At 6–7 mA the line is 0.30–0.35 mA (1.2–1.4×). **The real problem is the 5% itself:** LightEQ's inference is 932 ms/60 s = **1.55%**, so 5% looks generous — until you notice it must also cover **always-on 100 Hz × 3-axis SPI reads and 4th-order IIR filtering**, which never sleep. 5% covers inference *or* acquisition, not both |
| TX, SF10 | 0.610 mA | **OVERTURNED, and revealingly so.** Back-solve: `0.610 × 60 / 0.3052 = 119.9 mA`. **The pass assumed a ~120 mA TX current.** The STM32WLE5's high-power PA draws ~118 mA at **+22 dBm** — so the budget silently assumes **max-power TX**, which still falls 5 dB short of the Table-II ceiling the same pass celebrates. At a realistic +17 dBm (~45 mA) and the true ToA, the line is **0.278 mA** |
| Sleep, STOP2 | 0.005 mA | **PLAUSIBLE but incompatible with the architecture.** ~1.1–5 µA is a real STM32WL STOP2 figure. **But STOP2 retains only a limited SRAM subset.** A 70.3 kB rolling input buffer (§3) cannot live in retained RAM on a 64 kB part at all — the question is moot, but the budget assumes retention it never verifies |
| **RX / listen** | **ABSENT** | **The finding.** See below |

#### The missing receive line — the architectural kill

**Scheme C budgets zero receive current.** MASTER §5 gives RX as 1–2 mA (itself optimistic; SX126x
RX is ~4.6 mA boosted, and ~12 mA is typical for an SX127x-class front end).

**A node that never enters RX cannot relay. A node that cannot relay is not a mesh node — it is a
one-way beacon.** MASTER §2's *"Mesh is self-healing (Meshtastic or custom AODV): a destroyed node
reroutes, no single point of failure"* is **dead** under Scheme C as costed. The pass closes §10.2
with an architecture that silently deletes §2.

| Scenario | Total | CR2032 life |
|---|---|---|
| **No RX (what is budgeted)** — beacon only | 0.733 mA | 307 h |
| RX 1% @4.6 mA | 0.779 mA | 288.8 h |
| RX 1% @12 mA | 0.853 mA | 263.8 h |
| RX 5% @12 mA | 1.333 mA | 168.8 h |
| **RX 10% @12 mA** | **1.933 mA** | **116.4 h** |

*(Corrected lines: TX at +17 dBm and ToA 0.370688 s = 0.278 mA; others as claimed.)*

**Two things are true at once, and the pass reported neither:**

1. Its TX line was **2.2× too pessimistic** (120 mA assumed vs ~45 mA realistic), so the beacon-only
   total is *better* than claimed — **307 h, not 211 h.**
2. It omitted RX entirely, so a node that actually meshes is **116–264 h**, and the 211 h headline
   is right only by coincidence — **two large errors in opposite directions.**

**The 72 h survival window is still cleared in every scenario.** That conclusion survives. The
specific numbers 1.07 mA and 211 h do not, and neither does the claim that a mesh is affordable
without measuring the listen duty cycle.

### 2.5 Latency — [COMPUTED]

| Hops | Worst-case detection → gateway |
|---|---|
| 1 | **120 s** (60 s analysis window + up to 60 s until the next slot) |
| 2 | 180 s |
| 3 | 240 s |

§1 promises *"live map pin per detected survivor."* **Two to four minutes is not live.** For a
72 h survival window this is arguably acceptable — but it is a requirements change that §1 and §2
were never told about, and no prior pass flagged it. **Raise it; it is probably fine, but it must be
a decision rather than a side effect.**

---

## 3. "LightEQ fits in 100 kB, so §10.3 is closed"

**This is the cleanest overturn in the audit, and it inverts on a single fact.**

### The fact — [MEASURED, vendor datasheet]

**STM32WLE5 SRAM by variant:**

| Part | Flash | **SRAM** |
|---|---|---|
| STM32WLE5J8 | 64 kB | **20 kB** |
| STM32WLE5JB | 128 kB | **48 kB** |
| **STM32WLE5JC** (the largest) | 256 kB | **64 kB** |

**The family maximum is 64 kB.** The audit brief asked whether the real figure is 64 or 48 kB —
it is **64 kB at best, 48 kB or 20 kB depending on which die the RAK3172 carries**, and the prior
pass never checked which.

### The arithmetic — [COMPUTED]

```
Input buffer alone = 100 Hz × 60 s × 3 axes × 4 B = 72,000 B = 70.3 kB
```

**70.3 kB > 64 kB.** The 60 s analysis window MASTER §4 and §6 both specify **does not fit in the
total SRAM of the best part in the family**, before a single model weight, activation tensor, FFT
scratch buffer, LoRa stack, or stack frame is allocated.

Even packed to int16 (discarding 4 of the ADXL355's 20 bits) the buffer is **35.2 kB = 55% of all
RAM** — leaving ~29 kB for a model the paper says needs 193 kB.

### What the paper actually claims, as the pass itself reports it

> *"Runs on **Cortex-M4 with 100 kB RAM**; smallest model 29 k params, F1 0.99, **193 kB RAM**,
> 932 ms inference per 1 min of raw data."*

**The pass's own citation contains the contradiction.** It quotes "100 kB RAM" as the platform and
"193 kB RAM" as the model footprint **in the same sentence**, then concludes "fits in 100 kB." It
does not fit in 100 kB *by the pass's own numbers* — and the target part has 64 kB.

So: `64 kB (actual part) < 100 kB (paper platform) < 193 kB (smallest model)`. **Two orders of
shortfall stacked.**

### The task-mismatch attack, which also lands

Beyond RAM, LightEQ detects **earthquakes** — P-waves at tens of mg to g in a multi-Hz-to-tens-of-Hz
band, from a large, impulsive, broadband source. The project's task is a **0.1–1 mg cardiac impulse**
(MASTER §3.1) that is quasi-periodic, narrowband, and per §3.1 buried in ~95% noise. These share a
sensor class and nothing else: different SNR regime (orders of magnitude), different signal
structure (impulsive vs periodic), different discriminator (first-arrival picking vs HRV variance).
**F1 0.99 on earthquake detection is not evidence of anything about cardiac detection.** The pass
treats "runs a seismic NN on an M4" as transferable; the only transferable part is the compute
envelope, and that is exactly the part that fails.

### Verdict

**OVERTURNED. §10.3 is not closed — and the BOM part is now in question.**

MASTER §9 and the BUDGET pass selected the RAK3172 partly because "one part replaces two." That
saving is real. But **the MCU half of that part cannot host the inference the architecture now
depends on.** The project must either (a) shrink the window / stream features instead of buffering
raw / use external PSRAM, (b) pick a different MCU and reinstate a separate radio (undoing the
$3.01 saving *and* reinstating the SPI joint the BUDGET pass was pleased to delete), or (c) keep
inference off-node — which brings back the raw-streaming problem Scheme C exists to avoid.

**This is a genuine trilemma that all three passes stepped over.**

**Where I could be wrong:** if the RAK3172 carries the JC die (64 kB) *and* the design drops to a
15 s window at 50 Hz with int16 packing (15×50×3×2 = 4.4 kB), a small model could fit. That is a
real escape route — but it is a **different architecture** from the one in MASTER §4/§6 and
Scheme C, and nobody has specified it. The conclusion "§10.3 is closed, no MCU decision needed"
is false either way.

---

## 4. The CR2032 + supercapacitor fix

### 4a. Does the supercap move the problem rather than fix it? — [COMPUTED]

**No. On timing, the fix is sound.** This was the brief's main hypothesis and it does not survive
contact with the arithmetic — I am confirming the prior pass here.

Recharge from a high-impedance cell through its own internal resistance:

| Cell state | R | τ = RC (0.22 F) | 5τ (≈full) |
|---|---|---|---|
| Fresh | 10 Ω | 2.20 s | **11.0 s** |
| Aged | 30 Ω | 6.60 s | **33.0 s** |

**Inter-pulse interval under Scheme C is 60 s.** Even an aged cell fully recharges in 33 s, with 27 s
to spare. **The supercap genuinely decouples the pulse from the cell** — this is the one place where
Scheme C's slow cadence does real engineering work.

*(Under MASTER §4.1's original 2 pulses/second this fix would fail completely — 11–33 s recharge
against a 0.5 s interval. The supercap only works **because** Scheme C slowed the cadence. The
prior pass did not state this dependency, and it matters: if Scheme C is revised to transmit more
often, the supercap fix dies with it.)*

### 4b. Leakage against the budget — [COMPUTED]

| Part class | Leakage | % of 1.07 mA | Consumed over 211 h |
|---|---|---|---|
| CAP-XX (<1 µA) | 0.001 mA | 0.09% | 0.2 mAh |
| KEMET typ (5 µA) | 0.005 mA | 0.47% | 1.1 mAh |
| EDLC typ (10 µA) | 0.010 mA | 0.93% | 2.1 mAh |
| Worst (20 µA) | 0.020 mA | 1.87% | 4.2 mAh |

**Negligible — CONFIRMED.** Under 2% of budget, under 2% of the 225 mAh cell, in every case. The
brief suspected this would bite; it does not. *(Caveat: supercap leakage rises steeply with
temperature, and these are datasheet room-temperature figures [ASSERTED]. A node sitting on
sun-heated rubble at 60 °C could see several times this. Still not budget-breaking.)*

### 4c. ESR and the droop arithmetic — **the error the pass made**

This is where the fix as *specified* collapses.

The pass's own `02-vendor-register.md` §1 recommends the KEMET/Surge EDLC parts and states:

> *"CAP-XX is the right part class (50–100 mΩ ESR vs KEMET's 25–220 Ω) but is quote-only. For a
> 9–11 node build the **KEMET/Surge parts are adequate** and orderable."*

And `04` D23 repeats: *"For a 40 mA, ~0.3 s pulse the KEMET part is adequate."*

**[COMPUTED] — instantaneous IR drop across the supercap's own ESR, V = I·ESR:**

| ESR | @40 mA | @120 mA |
|---|---|---|
| **0.05 Ω** (CAP-XX) | 0.002 V | 0.006 V |
| **0.10 Ω** (CAP-XX) | 0.004 V | 0.012 V |
| **25 Ω** (KEMET FS0H224ZF) | **1.000 V** | **3.000 V** |
| **220 Ω** (KEMET FYD0H223ZF) | **8.800 V** | impossible |

**At KEMET's own quoted 25 Ω, the IR drop at 40 mA is 1.00 V — compared to the 1.20 V aged-cell
droop the supercap was purchased to eliminate.** The "fix" recreates ~83% of the fault. At 220 Ω it
is not a power source at all; it cannot deliver 40 mA from 3 V through 220 Ω under any circumstance
(that would require 8.8 V of headroom).

**D23's conclusion — "the engineering conclusion is robust to the spread" — is exactly backwards.
The conclusion is entirely determined by the spread.** A 3.5-order-of-magnitude ESR range (0.05 Ω
to 220 Ω) is the difference between a working fix and no fix. The pass noticed the spread, logged it
as a discrepancy, and then declared the conclusion independent of it.

**Capacitance droop (ΔV = I·t/C) is separately binding**, and the pass never computed it:

| C | @40 mA, 0.371 s | @120 mA, 0.371 s |
|---|---|---|
| 0.022 F | 0.674 V | 2.02 V |
| 0.22 F | 0.067 V | 0.202 V |
| 1.0 F | 0.015 V | 0.044 V |

At the pass's own assumed 120 mA TX current (§2.4), **0.22 F is marginal and 0.022 F fails outright.**

**Verdict on 4: the principle is CONFIRMED, the part selection is OVERTURNED.** A supercap across a
CR2032 is the right fix and the recharge timing works. But it must be a **≤100 mΩ ESR, ≥0.22 F**
part — i.e. the CAP-XX class the pass labelled quote-only and set aside — **not** the orderable
KEMET/Surge parts it recommended. The $0.70–2.00/node cost line is therefore **[UNVERIF] for the
part that actually works.**

### 4d. The two questions nobody answered

- **200–2000 G impact survival:** **not addressed by any pass.** MASTER §4 specifies 15–20 G
  (§8.3's drop computation), so the brief's 200–2000 G is a harsher bar than the project's own.
  Still: supercapacitors are **wet electrochemical devices** — EDLCs contain liquid electrolyte and
  have no published shock rating in the cited material. **[ASSERTED, unverified, by everyone.]**
- **Envelope:** MASTER §4 is **4 cm dia × 1.5 cm**. A CR2032 is 20 mm × 3.2 mm. A CAP-XX prismatic
  is roughly 20 × 18 × 1–3 mm; a 0.22 F radial EDLC is ~10–13 mm diameter and 5–20 mm tall. Adding
  a radial EDLC to a 15 mm-tall puck that must also hold a PCB, the RAK3172, the ADXL355 and foam is
  **tight to infeasible**. The prismatic form factor fits; the radial one likely does not — which is
  a **second independent reason the orderable part is the wrong part.** No pass checked the envelope.

---

## 5. The Pixhawk 6C Mini substitution (−$49)

**Verdict: WEAKENED — a saving asserted on one axis of a multi-axis part.**

The pass's entire technical justification is a single sentence:

> *"Still **14 PWM outputs** (8 IO + 6 FMU) with a built-in PWM header; §8.2 needs one servo channel.
> Path B becomes $689.97."*

PWM count is the one thing checked. **Everything else that distinguishes a flight controller went
unexamined:**

| Axis | Checked by the pass? | Why it matters here |
|---|---|---|
| UART/serial count | **No** | §8.5 needs GPS; §10.4 adds a **GPS 1PPS reference**; telemetry radio; optional optical flow (§8.2). That is 3–4 serial consumers on an airframe whose job is autonomous grid flight |
| **IMU redundancy** | **No** | The full-size 6C carries dual IMUs; Mini-class boards commonly carry one. §8.2 specifies **PID at 400–1000 Hz against micro wind tunnels and fire updrafts** — the exact regime where a single un-voted IMU is the failure |
| CAN | **No** | Rules out CAN GPS/ESC paths later |
| Flash / compute | **No** | Both are H7; likely equivalent, but unverified |
| Barometer | **No** | §8.2 requires **barometer + IMU fusion for altitude hold** |
| Connector set / cabling | **No** | Mini boards use different (often JST-GH-reduced) harnesses; may need new cables, eroding the saving |

**I could not independently verify the Mini's specs** — my web access hit a session limit before I
could pull Holybro's page. **I am therefore not asserting a regression; I am asserting the prior
pass did not establish its absence.** That is the finding: the claim is **unaudited**, presented
under a heading ("Two cheaper substitutions found while verifying") that implies it was.

**Is $49 worth it?** Against a $1,845 system it is **2.7%**. §8.2's flight profile — autonomous
low-altitude grid flight over rubble with fire updrafts and servo releases — is the single subsystem
where a failure crashes the hardware onto the disaster site it is trying to survey. **Trading IMU
redundancy for 2.7% is a bad trade if that is the trade; nobody has established whether it is.**

**Where I could be wrong:** the 6C Mini may well carry everything needed (it is a capable board,
and many builds use it for exactly this). If it has dual IMUs and ≥4 UARTs, the substitution is
simply correct and I would withdraw to "unverified but probably fine." **The defect is the evidence
standard, not necessarily the conclusion.**

---

## 6. "Software self-righting" (~$0 via rotation-invariant calibration)

**Verdict: OVERTURNED. The pass declared victory over the half that was never in dispute.**

### The conflation

Solving attitude from the DC gravity vector yields **the sensor's orientation** — a rotation matrix
mapping body axes to the local vertical. It is a **coordinate transform**.

**Mechanical coupling is a transfer function between the ground and the case.** It is governed by
contact area, contact pressure, normal force, and the resonance between device mass and ground
stiffness. The pass's own source says so — R4 #13, the Krohn/NCU coupling reference, which it
summarises correctly:

> *"well-planted spiked geophones are governed by **shear along the spike**; poorly planted ones by
> **weight coupling** (mass × contact pressure). Coupling is a **transfer function**… the main
> feature is a **resonance between device and ground**."*

**No rotation matrix changes contact pressure.** A node resting on a corner couples through that
corner regardless of how precisely it knows which way is down. The pass cites the evidence that
distinguishes the two problems and then uses it to claim one solves the other.

### The prior pass contradicted its own earlier pass — and the earlier one was right

`MEMS/06-build-vs-buy.md` §6.1 is titled **"The coupling interface — this is the real project"** and
states:

> *"A drone-droppable anchor that genuinely mates a node to fractured, air-gapped debris is:
> **unsolved** — no paper was found on heartbeat detection through rubble at all, **the dominant
> term** in the link budget, **this project's actual contribution**."*

And `MEMS/04`'s open-items table, item 10:

> *"**Design the coupling interface** — spike/anchor that mates a dropped node to fractured debris,
> *without* a self-righting round base — **the dominant term in the link budget**."*

Crucially, **the MEMS pass had already reached the software-attitude conclusion**, in the same
paragraph, as the *reason for choosing a 3-axis part*:

> *"it lets the node land in whatever shape couples best, and **recovers attitude afterwards from
> the DC gravity vector** instead of demanding a shape that rights itself."*

**So REDESIGN's `03` §6b and `04` D24 present the MEMS pass's own existing position — re-sourced to
US 9645267 — as a new finding that "overturns" MEMS/04 A8.** It overturns nothing. The MEMS pass
said: *attitude is free in software; the spike/anchor is the hard part.* The REDESIGN pass restated
the first clause, attached patents to it, and announced the conflict "solved prior art twice over."

**The hard part — a drone-droppable anchor for fractured, air-gapped debris — remains exactly as
open as MEMS left it.** `04` D24 is logged as *"Overturning my own earlier conclusion"*; it is
**not an overturn, it is a misreading of the earlier conclusion**, and it has the effect of marking
the project's self-identified "actual contribution" as closed.

### The second attack: does rotation actually reconstruct true vertical motion?

Even granting the orientation half, "~$0" overstates it. Rotating a measurement into the vertical
frame is exact only for an ideal triaxial sensor. In practice:

- **Cross-axis sensitivity.** Rotation mixes axes by construction; cross-axis error (typically
  ~1% for parts in this class) is mixed in with it. At a 0.1 mg target against §3.1's footstep
  interferers at 5–50 mg, **1% cross-axis coupling from a 50 mg horizontal transient injects
  0.5 mg into the reconstructed vertical — five times the signal.** This is not a small term.
- **Per-axis noise asymmetry.** For most MEMS triaxials the Z axis (out-of-plane) has a different —
  usually worse — noise density than X/Y. After an arbitrary rotation the reconstructed vertical is
  a weighted blend, so **the effective noise floor becomes orientation-dependent** and differs node
  to node. §7.1's TDoA and §6's amplitude-based human/machine discriminator both assume comparable
  sensitivity across nodes.
- **Calibration is not free.** US 9645267 is about an **in-situ calibration** procedure producing an
  alignment matrix. Per-unit calibration is a **production step** (fixture, time, data, storage) and
  a per-node parameter. The engineering is cheap; the ~$0 label is a BOM claim doing duty as a
  total-cost claim.

**The pass itself supplies the number that bounds this** — R4 #5: *"up to 20° tilt tolerable before
degradation; above 30°, no acquisition."* **If software rotation were genuinely sufficient, there
would be no tilt limit at all.** A tilt threshold is direct evidence that the physical problem is
not removable in software. The pass quotes the refutation of its own claim one line below it.

**Where I could be wrong:** the ADXL355 is a good part and its cross-axis spec may be better than
the 1% I assumed from the class; I did not extract that figure from the held datasheet. If
cross-axis is ~0.1%, the injected term falls to 0.05 mg and becomes merely significant rather than
dominant. **The coupling/orientation conflation, however, does not depend on that number at all.**

---

## 7. Methodology audit

### 7.1 "115 referred sources" — the metric is inflated

| Concept | Rows actually listed | Count claimed | Carried from an earlier pass |
|---|---|---|---|
| R1 | 23 | 23 | 0 |
| R2 | 24 | 24 | **12** |
| R3 | **13** | **22** | 1 |
| R4 | 25 | 25 | 0 |
| R5 | **6** | **21** | effectively 21 |

**Two of five concepts hit their "≥20" bar by counting sources they do not list.** R3 lists 12 named
sources and one row reading *"13–22 … (R2 sources 20–22 + ../BUDGET/ C3 energy literature … counted
once each)"* — ten sources summoned by a range. R5 lists five and collapses *"6–21"* into a single
parenthetical. **R5 is additionally carried wholesale** — its own header says *"Carried in full from
../BUDGET/01-literature.md C5… Nothing this pass changes the conclusion"* — yet all 21 count toward
this pass's 115.

The log's note *"Sources carried from ../BUDGET/01-literature.md are marked [carried] and counted
once"* is doing heavy lifting: counted once **per pass**, so the same source legitimately inflates
two passes' totals.

**Quality, not just count:**

- **13 of R4's 25 "literature" entries are patents.** Patents are prior art and perfectly valid
  evidence of *what has been tried* — they are **not peer-reviewed literature** and are not evidence
  that a method **works**. A granted patent means novel and non-obvious, not effective. R4's
  conclusion ("solved prior art, twice over") rests almost entirely on this stack.
- **R1's "verified, abstract-level" tier is mostly vendor marketing and SEO content**: NiceRF (×2),
  Zbotic, everythingRF, AutoAbode, Lansitec, Dragino, Actility, Granite River Labs, **and
  Wikipedia**. These are listed in the same numbered sequence as ETSI EN 300 220-2 and the Gazette.
  **R1's real evidentiary content is sources #1 and #5 — the Gazette and the CEPT annex.** The other
  21 pad a count.
- Similarly R3: Battery Power Tips, Machine Design, Longsing, Amicell, Deutsche Telekom's IoT blog,
  Hubble, Qoitech — all vendor/trade content in a 22-source tally.

**To be fair, the pass flags this**: *"I am not claiming 20 deeply-read papers per concept."* That
is an honest disclaimer. **But the README's headline "115 referred sources" and `04`'s tally table
drop the disclaimer** — and that is the number that travels.

### 7.2 Confirmation bias — CONFIRMED as a pattern

Every headline finding across the three passes moves the project toward *more viable*:

| Finding | Direction |
|---|---|
| Table-II → 20× power, 2.5× airtime | **more viable** |
| Scheme C → 8.4× power improvement, 72 h cleared | **more viable** |
| LightEQ → §10.3 "closed, no new hardware" | **more viable** |
| LongShoT → §10.4 "largely answered, downgrade" | **more viable** |
| Coupling → "solved prior art" | **more viable** |
| Pixhawk Mini → −$49 | **more viable** |
| RAK3172 → one part replaces two, cheaper | **more viable** |
| Delsar comparison → "survives intact," "10× margin" | **more viable** |

The genuinely negative findings are of a different kind: the drone incompatibility and the budget
2.2× understatement come from the **BUDGET** pass auditing *MASTER*, and E17/E18/D19 are the pass
auditing *its own tooling*. **The REDESIGN pass — the one asked to propose fixes — found almost
nothing that made its own proposals worse.**

The tell is `03` §7, *"What I am NOT suggesting changing,"* where every item is deferred on a
plausible-sounding ground. And `03` §1's flag — *"If it turns out this is a Table-I device, Scheme C
below still fits at 0.509%"* — is **motivated reasoning in its purest form**: the payload size was
chosen to pass under *both* thresholds, then presented as an engineering result. §2.2 above shows
24 B was never derived from what the data needs; **it was derived from what the duty-cycle table
would accept.** That is fitting the evidence to the conclusion, and it is the root cause of the
single worst error in the three passes.

**The honest counter-weight, stated plainly:** these passes self-reported five errors including a
tooling bug that invalidated prior work and forced a full re-run (E17), a 2.64× price trap caught
before publication (D19), and a repeat of a documented rule (E18). **That is better error hygiene
than most engineering documentation.** The bias is in which *direction* conclusions resolve when
evidence is ambiguous — not in dishonesty.

### 7.3 Numbers that are consistent with each other rather than with reality

The clearest instance: **ToA 0.3052 s → duty 0.509% → 11-node 5.59% → TX 0.610 mA → total 1.07 mA →
211 h.** Six numbers, perfectly mutually consistent, **all wrong**, because the first one is wrong
and the rest are derived from it. `04` A35–A47 verifies the *chain* and reports "16/16 reproduce."

A second instance: **1.07 mA** and **211 h** are each individually wrong (TX over-estimated by 2.2×,
RX omitted entirely) in ways that **roughly cancel**. The pair is internally consistent and the
headline survives by accident. **No check in the methodology could have detected this**, because
both errors are in *inputs*, and the methodology only verifies *operations on inputs*.

### 7.4 ⭐ The methodology's structural blind spot — stated precisely

> **The methodology verifies that operations are performed correctly on inputs, and that sources
> exist. It contains no step that verifies the inputs are the right inputs, or that the formula
> computes the quantity the claim is about.**
>
> **A perfectly reproduced calculation of the wrong quantity passes every check in the system.**

The three instruments are:

1. `final.py` — recompute arithmetic from raw inputs. **Verifies: operations.** Cannot detect a
   wrong constant, because the constant *is* the raw input it starts from.
2. `verify3.py` — three-state link liveness. **Verifies: existence.** Cannot detect that a live page
   does not support the claim it is cited for.
3. "2 audit passes per finding" — re-reading. **Verifies: consistency.** Re-reading a chain derived
   from a wrong premise re-derives the same chain. A35–A47 is exactly that.

**Every major error in this audit lives in the blind spot, and none could have been caught by any of
the three:**

| Error | Why the methodology structurally missed it |
|---|---|
| ToA 0.3052 vs 0.370688 s | A35 "recomputes" it — but 0.3052 was the *seed*. Reproducing a seed is tautological. **Needs:** an independent implementation or an external calculator. Nothing in the method calls for one |
| 24 B cannot carry 60 timestamps | **No step ever asks "is this payload sufficient?"** The method checks that 0.3052/60 = 0.509%. It has no concept of *information sufficiency* — a dimension of correctness the instruments cannot represent |
| RX current omitted | **You cannot arithmetic-check a line that isn't there.** Recomputation validates the four lines present and is silent on the fifth. **Omission is invisible to verification-by-recomputation** |
| STM32WLE5 = 64 kB not 100 kB | The LightEQ link is **LIVE** and the paper **does** say 100 kB. The citation is accurate; the *inference* ("so it fits our part") was never checked against the part's datasheet. **Link-liveness validates the source, never the syllogism** |
| ALOHA/collisions ignored | The sum 11 × 0.509% = 5.59% is arithmetically perfect. **It is the wrong model.** Recomputation cannot flag a model error — it faithfully reproduces whatever model it is handed |
| KEMET 25 Ω ESR unusable | D23 *logged the ESR spread as a discrepancy* and then declared the conclusion robust to it — **without computing I·R.** The discrepancy register records disagreements; it does not evaluate them |
| Coupling ≠ orientation | Both patents are LIVE and both say what they are quoted as saying. **The category error is in the mapping from source to claim** — the one link in every chain the methodology never inspects |

**The missing instrument, named:** a **premise and dimensional audit** — for each load-bearing
number, state (a) the physical quantity it is supposed to be, (b) the independent source or second
implementation that fixes it, (c) the units and the dimensional check, and (d) **what is NOT in the
model**. Step (d) is the one that catches omitted RX current, absent collisions, and unverified
information sufficiency. Step (b) is the one that catches 0.3052 s.

**The sharpest one-line statement of the gap:** the method's own slogan, *"every number recomputed
from raw inputs,"* contains the flaw. **Recomputation from raw inputs cannot audit the raw inputs.**
Of the seven errors above, **recomputation could have caught zero.**

---

## 8. Source table

Sources I accessed directly for this audit. Status is honest: body-inspected where fetched, and
**[RATE-LIMITED]** marks checks I intended and could not complete — those are gaps in my audit, not
findings.

| # | Source | Used for | Access status |
|---|---|---|---|
| 1 | **G.S.R. 853(E), Gazette of India Extraordinary Pt II §3(i), 10 Dec 2021** — `thc.nic.in` hosted copy | **Primary legal instrument.** Tables I–IV, rules 1–5, e.r.p. definition, type-approval rule. Downloaded (572,832 B), `%PDF-1.6` header verified, extracted with pdfminer, **read in full** | ✅ **LIVE** — PDF retrieved and parsed |
| 2 | G.S.R. 853(E) rule 1(1) — short title | Band = **865-868 MHz**, overturning MASTER's 865-867 | ✅ quoted verbatim above |
| 3 | G.S.R. 853(E) rule 2(1)(c) | e.r.p. defined **relative to a half-wave dipole** — settles the e.r.p./EIRP question | ✅ quoted |
| 4 | G.S.R. 853(E) Table-I | 25 mW e.r.p., 1% duty, **FHSS**, ≤50 kHz | ✅ quoted |
| 5 | G.S.R. 853(E) Table-II + Note | 500 mW e.r.p., APC, ≤200 kHz, ≤10%/≤2.5%, buried-victims note | ✅ quoted |
| 6 | G.S.R. 853(E) Table-III / Table-IV | Confirms Table-II is not the only ≤2.5%-class entry; RFID at 2 W is a separate class | ✅ read |
| 7 | G.S.R. 853(E) rule 5(1) | **"such equipment shall be type approved"** — unconditional | ✅ quoted |
| 8 | G.S.R. 853(E) rule 3 | Exemption is on the **apparatus**, non-interference/non-protection/shared | ✅ quoted |
| 9 | **Semtech SX1276/77/78/79 LoRa ToA formula** (§4.1.1.7), implemented from the published equations | Independent ToA recomputation — the 0.3052 s overturn | ✅ implemented & cross-validated |
| 10 | Published LoRaWAN airtime reference values (SF10/SF12, 51 B app payload) | **Validation** of my ToA implementation: Δ = −0.00003 s and −0.002 s | ✅ matched |
| 11 | **STMicroelectronics STM32WLE5J8/JB/JC datasheet** memory table (via distributor datasheet mirrors) | **20/48/64 kB SRAM** — the §10.3 overturn | ✅ **LIVE** |
| 12 | **ADI ADXL354/ADXL355 datasheet** — held locally at `MEMS/datasheets/ADI_ADXL354_ADXL355_datasheet.pdf`, extract at `MEMS/extracts/adxl355.md` | *"ADXL355 in measurement mode: 200 μA"*, standby 21 µA — **confirms** the 0.200 mA line | 📄 **HELD, read** |
| 13 | **TTN — LoRaWAN duty cycle documentation** | Duty cycle applies per channel/sub-band and to **both nodes and gateways**; 1% context | ✅ **LIVE**, body read |
| 14 | `docs/research/MEMS/06-build-vs-buy.md` §6.1 | *"coupling interface… unsolved… the dominant term… this project's actual contribution"* — the §6 overturn | 📄 local, read |
| 15 | `docs/research/MEMS/04-action-report.md` A8 + open item 10 | Tilt table (±15/30/45°), and the spike/anchor item left open | 📄 local, read |
| 16 | `docs/research/REDESIGN/01-literature.md` | Source-count audit; R3/R5 range-rows; patent share of R4 | 📄 local, counted programmatically |
| 17 | `docs/research/REDESIGN/02-vendor-register.md` §1 | KEMET 25 Ω / 220 Ω ESR figures, "adequate" recommendation, CAP-XX 50–100 mΩ | 📄 local, read |
| 18 | `docs/research/REDESIGN/03-proposals.md` | Scheme C tables, power budget, Pixhawk Mini, §6b | 📄 local, read |
| 19 | `docs/research/REDESIGN/04-verification-log.md` A34–A51, D19–D24, E17–E19 | Methodology audit target | 📄 local, read |
| 20 | `docs/research/BUDGET/README.md` + `03-budget.md` | Path B costing, four omissions, LongShoT downgrade | 📄 local, read |
| 21 | `docs/MASTER.md` §3.1, §4, §5, §6, §7 | Target band 0.1–1 mg; 4 cm × 1.5 cm envelope; RX 1–2 mA; 100 Hz/60 s window; packet structure | 📄 local, read |
| 22 | **Pure (unslotted) ALOHA throughput model**, S = G·e^(−2G) | Collision analysis — standard result, implemented and run | ✅ computed |
| 23 | **Shannon/entropy bit-budget method**, bits = log₂(range/resolution) | The 156 B vs 24 B information budget | ✅ computed |
| 24 | Search: India WPC amendments to the 865-868 MHz SRD rules post-2021 | Looked for a superseding instrument; **found only a Jan-2024 SRRF exemption-list update**, no superseding G.S.R. | ⚠️ **inconclusive** — see "where I could be wrong" |
| 25 | Holybro Pixhawk 6C Mini product page | UART/IMU/CAN comparison for §5 | ⛔ **[RATE-LIMITED]** — not retrieved |
| 26 | LightEQ (IoTDI '23, DOI 10.1145/3576842.3582387) primary PDF | Task definition, sample rate, band, RAM breakdown | ⛔ **[RATE-LIMITED]** — assessed from the prior pass's own quoted figures, which are self-contradictory regardless |
| 27 | WPC DoT regulations index (`wpc.dot.gov.in`) | Superseding-amendment check | ⛔ **[RATE-LIMITED]** |

**Access honesty:** my web session hit its rate limit partway through. Items 25–27 are **gaps, not
findings** — I have not asserted a conclusion that depends on them. The findings I do assert rest on
item 1 (primary legal text I parsed myself), items 9–12 (vendor datasheets and a cross-validated
formula implementation), item 12 (a locally held datasheet), and items 22–23 (standard models I ran).
**No finding in this audit rests on a source I could not open.**

---

## 9. Where I could be wrong

Stated per finding, because a critique that cannot be wrong is not a critique.

**On Table-II (§1):**
- **The superseding-amendment check is incomplete.** I searched and found nothing later than 2021
  that touches these four tables, but I could not reach WPC's own regulations index. **If a 2023–2026
  amendment exists, parts of §1 may be moot.** This is the largest single hole in my audit and I
  flag it as such.
- The note-vs-definition distinction may be stronger than I allow. In Indian statutory interpretation
  a note *"for the purpose of this Table"* is reasonably read as part of the instrument. I rate the
  table assignment as **well-supported but not dispositive** — which is roughly where the prior pass
  put it, to its credit.
- My "+8 dB not +13 dB" correction assumes 0 dBi. A better antenna narrows the gap. The PA omission
  stands either way.

**On Scheme C (§2):**
- If the design intends **1–5 representative beats per window** rather than 60, my 6.5× shortfall is
  not the right framing — but then the *stated* claim ("~60 beats") is wrong and the "batching costs
  localisation nothing" argument is unevidenced. I cannot find a reading where both survive.
- My ALOHA model is the **pessimistic bound**. LoRa capture effect and SF quasi-orthogonality recover
  real throughput; slotted operation would roughly double it. My 32.3% is an upper bound as surely as
  5.59% is a lower one. **The truth is between them, and neither pass bracketed it.**
- My RX current figures (4.6 / 12 mA) are class-typical, **not** pulled from the STM32WLE5 datasheet
  this session. If STM32WL RX is genuinely ~4 mA, the mesh penalty is at the gentler end of my table.
  **The omission finding does not depend on the figure.**

**On LightEQ / §10.3 (§3):**
- I did not confirm **which die the RAK3172 carries**. If it is the JC (64 kB) my numbers hold; if JB
  (48 kB) or J8 (20 kB) the conclusion is stronger, not weaker. **No variant makes the claim true.**
- I did not read the LightEQ paper directly (rate-limited). My argument uses **the prior pass's own
  quoted figures**, which are internally contradictory (100 kB platform, 193 kB model) — so reading
  the paper could only change which of the two is operative, not the 64 kB ceiling.
- The 70.3 kB input buffer assumes the full 60 s × 100 Hz × 3-axis × 4 B window held in RAM.
  **Streaming/incremental feature extraction would avoid it.** That is a real escape — but it is not
  the architecture any pass described, and it does not rescue the 193 kB model.

**On the supercap (§4):**
- Leakage figures are **room-temperature [ASSERTED]**. Hot rubble could multiply them several-fold —
  still not budget-breaking, but my "negligible" is a 25 °C claim.
- I did not obtain a **shock rating** for any candidate part. My concern about wet electrolyte under
  impact is reasoning from construction, **not** a sourced failure mode.
- My ESR attack uses the pass's own quoted 25 Ω / 220 Ω. If the actual parts are better than their
  own register says, the attack weakens. **The register is the pass's evidence, and I used it.**

**On the Pixhawk Mini (§5):**
- I am asserting **absence of verification, not presence of a regression.** The Mini may be entirely
  adequate. If it has dual IMUs and ≥4 UARTs I would downgrade this to "unverified but likely fine."

**On coupling (§6):**
- My 1% cross-axis figure is **class-typical [ASSERTED]**, not extracted from the ADXL355 datasheet
  I hold. If it is 0.1%, that sub-argument weakens by 10×. **The orientation/coupling conflation —
  the main finding — does not depend on it at all.**

**On the methodology (§7):**
- The source-count critique is partly a **presentation** complaint. The literature doc *does* disclose
  its tiering honestly; the README and tally table drop the disclosure. Reasonable people could call
  that a summarisation artefact rather than inflation.
- My confirmation-bias finding is a **pattern argument**, which is weaker than a specific-error
  argument. I ground it in one concrete instance — the 24 B payload chosen to clear both thresholds —
  and I would not press it further than that instance supports.

**On myself, structurally:**
- **I was commissioned to find errors**, which is its own bias. I have tried to mark confirmations as
  loudly as overturns — §1's legal reading, §4a/4b's recharge and leakage, and the ADXL355 current
  line are **real results in the prior passes' favour**, and E17 is error hygiene better than most.
- **My own numbers are COMPUTED, not MEASURED.** I validated my ToA implementation against two
  published reference points and it matched to four decimals, which is the strongest check I could
  run offline. **It is still one implementation.** If my formula is wrong in the same way twice, I
  have reproduced the prior pass's exact failure mode — and I would be, by my own §7.4, invisible to
  my own method. The fix is the same one I prescribe: **an independent second implementation.**

---

*Audited against `docs/research/MEMS/`, `docs/research/BUDGET/`, `docs/research/REDESIGN/` and
`docs/MASTER.md`. Nothing outside `docs/critique/` was modified.*
