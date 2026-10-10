# 04 — Cost Kill Attempt

Hostile procurement / financial audit of MASTER §9's **$1,844.81**. Written as an adversary: the
job here is to break the budget, not to balance it.

Date of this pass: **2026-10-07**. Prices date-stamped individually. FX **₹84/$**.

**Scope note.** The 2026-10-06 pass already rebuilt §9 and found the old numbers understated
2.2–2.3×. **That work is accepted and not re-verified here.** This document is about what that
pass *also* missed — and it missed more than it found.

Provenance tags: **[LIVE]** read off the vendor/authority page this session · **[SEARCH]** search
snippet, not the page body · **[EST]** my estimate, basis stated · **[UNVERIF]** from knowledge,
not checked this session.

---

## Verdict up front

**No. $1,845 is not defensible. It is not even the right order of magnitude for a
*regulatory-compliant* build in India.**

| Basis | Number | vs §9 |
|---|---|---|
| §9's claim | $1,845 | — |
| **Capital, all-in, ex-labour** | **$9,746** | **5.3×** |
| **Cost to a working field demonstrator (junior-engineer labour)** | **$14,145** | **7.7×** |
| Same, at the honest node count (finding #7, r = 3 m, 400 m²) | **$10,957** | 5.9× |
| Same, if §10.1 returns r = 1 m | **$26,270** | 14.2× |

**The cost advantage over Delsar does not survive.** On capital it shrinks from 8× to **1.05×
(i.e. gone)**. On cost-per-deployment the project is **2.3–5.2× *more expensive* than the
incumbent.** On 5-year TCO it is **2.5–3.6× more expensive.** The inversion is not marginal.

§9's closing line — *"at $1,845 the order-of-magnitude advantage holds with 10× margin"* — is the
single least defensible sentence in MASTER. It compares **this project's bare component prices**
against **a competitor's delivered, certified, trained, warranted kit price**, and does so in a
budget with no line for tax, no line for compliance, no line for test equipment and no line for
human beings.

---

## The single biggest missing cost

### It is not labour. It is that the build is illegal as specified, and the legal version costs $2,722 in paperwork.

Two regulatory walls, neither of which has a line, a sentence, or a footnote anywhere in MASTER:

**Wall 1 — the airframe cannot be imported.** §8.6's Path B, the *recommended* path, is a
**"HAWK'S WORK F450 kit"**. DGFT prohibited the import of drones in **CBU / CKD / SKD form with
effect from 9 February 2022**. [LIVE]

> *"Import policy for drones in CBU (Completely Built Up)/CKD (Completely Knocked Down)/SKD
> (Semi Knocked Down) form … is prohibited with exceptions"*

**An F450 "kit" is the textbook definition of CKD** — a complete airframe, disassembled. §8.6 did
the SDK homework on DJI and got it right; it then recommended a part that **cannot lawfully enter
the country**. The exceptions are R&D imports by *government entities, government-recognised
educational institutions, government-recognised R&D entities, and drone manufacturers*, each
requiring **DGFT import authorisation**. A private individual pre-code in a home workspace is
none of those.

What *is* free to import: **"Import of drone components, however, shall not require any
approvals."** So the Pixhawk 6C is fine. The frame kit is not. The drone must be **assembled
domestically from separately-sourced components**, at Indian retail, which is where the $1,035
line below comes from instead of §8.6's $738.99.

**Wall 2 — the radio needs WPC ETA.** §5 specifies **865–867 MHz** — **[CORRECTED: that figure is from the *superseded* 2005 RFID rules. The operative band is **865–868 MHz** per G.S.R. 853(E), whose rule 1 expressly supersedes the earlier instrument — primary-source verified in `06-prior-research-audit.md:171`. MASTER §4/§5 quote a dead instrument. **The ETA requirement and its cost below are unaffected**; only the band label was wrong.]** That band is licence-exempt
**for equipment that holds Equipment Type Approval** under Gazette Notification G.S.R. 564(E) of
30 July 2008 [SEARCH]. ETA is a *per-device-model* approval requiring a test report from an
accredited lab. §9 budgets **$0** for it.

| Regulatory line | ₹ | $ | Src |
|---|---|---|---|
| DGCA Remote Pilot Certificate, small category, RPTO | 65,000 | 774 | [SEARCH] |
| DGCA-approved medical examination | 3,500 | 42 | [SEARCH] |
| UIN drone registration | 100 | 1 | [SEARCH] |
| RPC issue fee | 100 | 1 | [SEARCH] |
| Third-party liability insurance (mandatory, commercial), 1 yr | 10,000 | 119 | [SEARCH] |
| Digital Sky registration, docs, processing | 3,000 | 36 | [SEARCH] |
| **WPC ETA: application + accredited test-lab report** | **150,000** | **1,786** | **[EST]** |
| **TOTAL** | **₹2,31,700** | **$2,758** | |

Arithmetic: 65,000 + 3,500 + 100 + 100 + 10,000 + 3,000 + 150,000 = ₹2,31,700 ÷ 84 = **$2,758**.

**The RPC range is ₹50,000–1,05,000 all-in** [SEARCH]; ₹65,000 for training is the middle of the
quoted ₹35,000–65,000 RPTO band. The WPC ETA figure is **[EST]** — the WPC fee itself is nominal
(order ₹1,000s), but the **accredited-lab test report** is the real cost and Indian EMC/RF labs
quote ₹1–2 lakh for a radio-module test campaign. This is my single softest number and I flag it
as such; even at ₹50,000 the regulatory block is still **$1,565**.

**One escape hatch, and it is narrow.** The Type Certificate and RPC requirements are waived for
**R&D entities operating in their own or rented premises inside a green zone**, and for
**home-built drones under 25 kg** [SEARCH]. A pure-bench R&D build may therefore dodge the $936
DGCA block. **It does not dodge the DGFT import ban** (that is a customs matter, not an
operations matter) and **it does not dodge ETA if the radio transmits**. And the moment the
project does what it says it does — fly over a real collapse site — every waiver evaporates.

> **This is the structural finding: §9 priced a science project and MASTER describes a rescue
> instrument. Those have different cost structures, and the gap between them is almost entirely
> compliance.**

---

## Attack 1 — Missing cost categories

### 1.1 India import duty and GST: $348 on ~$1,055 of parts

Every price in §9 is a **US/Chinese vendor price**. None of them is a *landed* price. The Indian
import stack is cumulative:

```
BCD   = CIF × rate
SWS   = BCD × 10%
IGST  = (CIF + BCD + SWS) × 18%
```

For **HS 9031** (measuring/checking instruments — where the ADXL355 and the Pi class land):
BCD 7.5%, SWS 0.75% effective, IGST 18% → **27.735% effective** [SEARCH]. Reproduced:

| CIF | BCD @7.5% | SWS @10% of BCD | IGST @18% | Landed | Effective |
|---|---|---|---|---|---|
| $711.70 (sensors ×11 + Pi 5 + GPS) | 53.38 | 5.34 | 139.19 | **$909.09** | 27.74% |
| $342.89 (modules, passives, Pixhawk, telemetry) @ BCD 20% | 68.58 | 6.86 | 75.30 | **$493.62** | 43.96% |
| **$1,054.59 total** | | | | **$1,402.72** | **33.0%** |

**Duty + tax = $348.12.** Plus three international consignments at ~$45 and courier/broker
clearance at ~$30 each = **$225**. **Total tax-and-freight line: $573.** §9 has none of it.

The 20% BCD band is **[EST]** — radio modules and populated assemblies attract higher BCD than
bare instruments, and 20% is the common electronics rate. Even if everything cleared at the
lowest 7.5%/27.7% band, the omitted line is still **$292 + $225 = $517**.

> **An Indian project quoting US vendor prices as its budget has understated by ~⅓ before a
> single other error.**

### 1.2 PCB: $1.80 amortised is understated 44×

§9's line is **"JLCPCB 4-layer, qty 10, amortised — $1.80"**. That is the *bare-board* price,
and only for the board. It prices:

- no solder paste stencil
- no assembly (an LGA-14 ADXL355 is **not hand-solderable** by a first-timer — it has no leads)
- no shipping (JLCPCB to India is $20–35/consignment, and it is never free)
- no minimum order (qty 5 minimum on most processes)
- **and no design spins.**

**The first board is never right.** For a mixed-signal board with an LGA sensor, an RF module
with antenna matching, and a battery holder, budgeting one spin is not optimism — it is a
category error.

| | $ |
|---|---|
| Spin 1: bare 4-layer qty 10 + stencil + shipping | 60 |
| Spin 1: PCBA, 11 boards, 2-sided | 190 |
| Spin 2: bare + PCBA | 230 |
| Spin 3: bare + PCBA, production run 15 | 260 |
| Expedited shipping ×3 | 135 |
| **Total** | **$875** |

**$875 vs §9's $1.80 × 11 = $19.80. Understated 44×.** All [EST], basis: JLCPCB's published
PCBA model (board + stencil + setup + per-joint). Confidence: medium-high on the structure,
±40% on the figure.

### 1.3 Test equipment: $1,801, and §12 cannot run without it

§12 lists seven build steps. **Step 1 is "Answer §10.1"** — the measurement the entire project
is gated on. §9 budgets **$0** of instrumentation to make it with.

| Item | $ | Src |
|---|---|---|
| Nordic Power Profiler Kit II (nRF-PPK2) — µA sleep current for §4.1 | 150.95 | [SEARCH] Jameco |
| Reference geophone ×2 (SM-24 class) — ground truth for §10.1 | 150.00 | [EST] |
| Calibrated reference seismometer (used Raspberry Shake 1D class) | 400.00 | [EST] |
| 24-bit USB DAQ (MCC / LabJack class) | 300.00 | [EST] |
| Concrete test slabs, rebar, forms, graded rubble | 180.00 | [EST] |
| Bench PSU + DMM + entry scope | 400.00 | [EST] |
| Hot-air rework, stencil jig, paste, flux | 220.00 | [EST] |
| **Total** | **$1,800.95** | |

**§10.1 is unanswerable without a calibrated reference.** You cannot establish that an ADXL355
detects a heartbeat at 3 m unless you can independently establish what the signal actually was.
A bare ADXL355 measuring its own output is not a measurement; it is a tautology. The reference
instrument is not optional equipment — **it is the measurement.**

PPK2 price note: $150.95 at Jameco [SEARCH], ~£137 at Element14 [SEARCH], A$244–251 in Australia
[SEARCH]. India landed with duty: ~$195. Joulescope JS220 pricing **not retrieved this session** —
label the gap; from knowledge it is roughly $1,000-class, which is why PPK2 is the right call.

### 1.4 Labour: $1,760–$8,798, and §9 costs zero hours

§9 budgets **zero engineer-hours** across all seven steps of §12. For a pre-code project this is
the largest single omission by count of dollars-not-written-down.

| §12 step | Person-weeks | Basis |
|---|---|---|
| 1 Bench detection, answer §10.1 | 4 | includes test-rig build + concrete cure time |
| 2 Pipeline on synthetic data (filter/FFT/LSTM) | 5 | LSTM training + synthesis of noise corpus |
| 3 Two-node TDoA with real sync | 4 | §10.4's LongShoT path is a port, not a download |
| 4 Mesh, n-node, with §10.2 settled | 4 | **§10.2 is unsolved — this is optimistic** |
| 5 Node hardware: case, drop-test, power validation | 6 | **3 PCB spins live here** |
| 6 Drone integration: release, grid autonomy, GPS tagging | 6 | MAVLink + airframe tuning + flight tests |
| 7 Dashboard end-to-end | 3 | Flask/Leaflet/WS is the easy one |
| **Total** | **32 person-weeks = 7.4 person-months** | |

| Rate | ₹/mo | $/mo | × 7.4 mo |
|---|---|---|---|
| Intern | 20,000 | 238 | **$1,760** |
| Junior engineer | 50,000 | 595 | **$4,399** |
| Market engineer | 100,000 | 1,190 | **$8,798** |

All [EST]. 32 weeks is **aggressive** — it assumes no step fails and none of §10.1–10.5 forces a
redesign. Given that §10.2 (radio budget) is flatly unsolved and finding #1 says the node may not
survive landing, **48–60 weeks is the realistic range**, which doubles these figures.

> **At market rate the labour alone ($8,798) is 4.8× the entire §9 budget.** This is the honest
> reason the project looks cheap: the expensive input is not being counted.

### 1.5 Drone: domestic build + crash budget = $1,035

Forced by §1's DGFT finding. §8.6's $738.99 assumed an imported F450 kit at $399.99.

| Item | $ | Note |
|---|---|---|
| Frame + motors + ESCs + props, **Indian retail** | 210 | [EST] Robu/quartzcomp class; **BOTWALL**, not read |
| Pixhawk 6C, landed (component → free import) | 250 | $199 [prior pass LIVE] + 25.6% landed |
| Telemetry pair + GPS/compass, landed | 95 | [EST] |
| 4S LiPo ×3 + charger — **must be domestic** | 150 | LiPo air freight is restricted/surcharged |
| Servo release mechanism + hardware | 30 | [EST] |
| RC transmitter + receiver | 120 | [EST] — §8.6 omitted this entirely |
| **Crash/spares: 2 crashes** (props, 1 arm, 1 motor, 1 ESC, 1 LiPo) | 180 | [EST] |
| **Total** | **$1,035** | vs §8.6's $738.99 |

**The crash budget is not padding.** §8.2 specifies autonomous snake-grid flight at 4–5 m over
**rubble**, by a first-time multirotor builder, with a servo payload release. Two crashes is the
optimistic case. §8.6 also forgot the transmitter — you cannot arm a Pixhawk without one.

### 1.6 Certification for real rescue use: unpriced, and it is a wall

MASTER §1 positions this against a **FEMA/USAR-deployed instrument**. Delsar's own published
sensor spec: **IP67, shock resistant over 1000 g** [LIVE]. To sell or deploy this as rescue
equipment the project would need IP-rating test, drop/shock qualification, EMC, and electrical
safety — **$8,000–25,000** of third-party lab work [EST, not sourced this session].

**I am excluding this from the rebuilt total** because the stated goal is a *field
demonstrator*, not a product. But it must be named, because §9's Delsar comparison implicitly
claims product equivalence. **You cannot claim the price advantage of a demonstrator and the
capability of a certified instrument in the same sentence.**

---

## Attack 2 — Unit economics

### 2.1 The ADXL355's 25 µg/√Hz probably does not apply in the target band

I pulled the **ADXL354/ADXL355 datasheet (Analog Devices)** and read the specification table
directly. [LIVE]

> `NOISE DENSITY ±2 g`
> `X-Axis, Y-Axis, and Z-Axis    25 μg/√Hz`

**Note what is absent: there is no frequency condition on that line.** No "at 10 Hz", no
"10 Hz to 1 kHz". It is a flat-band figure. Meanwhile, two rows below:

> `Velocity Random Walk   X-axis and y-axis   9 μm/sec/√Hr`
> `                       Z-axis             13 μm/sec/√Hr`

**That second spec is the datasheet admitting the first one is not flat.** Velocity random walk
exists as a parameter precisely because low-frequency instability is not captured by a broadband
noise density. ADI also lists VRW inside the *repeatability* footnote alongside "broadband noise"
as a **separate** error term.

So: what is the in-band noise actually? Model the 1/f region as `ASD(f) = 25·√(f_c/f)`:

| 1/f corner | 0.5 Hz | 1 Hz | 2 Hz | 4 Hz | RMS over 0.5–4 Hz | vs flat |
|---|---|---|---|---|---|---|
| flat (no 1/f) | 25 | 25 | 25 | 25 | **0.047 mg** | 1.0× |
| f_c = 5 Hz | 79 | 56 | 40 | 28 | **0.081 mg** | 1.7× |
| **f_c = 10 Hz** | 112 | 79 | 56 | 40 | **0.114 mg** | 2.4× |
| **f_c = 20 Hz** | 158 | 112 | 79 | 56 | **0.161 mg** | 3.4× |
| f_c = 50 Hz | 250 | 177 | 125 | 88 | **0.255 mg** | 5.5× |

(units µg/√Hz; RMS = √(625·f_c·ln(4/0.5)) µg)

**Against §3.1's target signal of 0.1–1 mg, and §3.3's claim of ">20 dB SNR after filtering":**

| Signal | Noise @ f_c=10 Hz | SNR |
|---|---|---|
| 1.0 mg (strong, close, good coupling) | 0.114 mg | **+19 dB** — just misses the claim |
| 0.3 mg | 0.114 mg | **+8 dB** |
| **0.1 mg (weak/injured/hypothermic — §3.1's own lower bound)** | **0.114 mg** | **−1 dB** |

> **At the bottom of its own stated target amplitude range, the ADXL355's in-band noise equals
> the signal.** The ">20 dB SNR" of §3.3 holds only at the top of the range, in a quiet site,
> with a flat noise floor the datasheet does not promise.

**I went looking for the noise PSD plot that would settle f_c. It does not exist.** I enumerated
every figure caption in all 42 pages of the datasheet. [LIVE]

- **There is no noise spectral density plot anywhere in the ADXL354/355 datasheet.** Figures 7–12
  are *frequency response* (gain vs frequency), not noise. Figures 25–29 are VRE. Figures 20–24
  are offset/sensitivity histograms.
- **The only low-frequency noise characterisation ADI provides is Root Allan Variance** —
  Figures 54, 55, 56, "ADXL355 Root Allan Variance (RAV), X/Y/Z-Axis". Axes read:
  **RAV (µg) from 1 to 1000, vs INTEGRATION TIME (seconds) from 0.01 to 1000.**

**This is stronger evidence than the PSD plot would have been.** RAV is *the* standard instrument
for exposing 1/f and bias-instability behaviour: a white-noise-only device gives a straight
−½-slope line, and **the depth and location of the RAV minimum is the 1/f corner.** ADI chose to
characterise this part with RAV and *only* RAV across 0.01–1000 s integration — i.e. down to
**0.001 Hz**. You do not publish a 1000-second RAV curve for a device whose noise is flat.

Two further tells, both [LIVE] from the spec table:

- **The y-axis spans 1–1000 µg.** A flat 25 µg/√Hz device integrated over 1 s sits near 25 µg;
  the plot allocates **1.6 decades of headroom above that**, which is where the 1/f rise goes.
- **`Velocity Random Walk 9 / 13 µm/sec/√Hr` is listed as a separate parameter**, and appears
  again in the repeatability footnote **alongside** "broadband noise" as a distinct error term.
  Converted to a white-noise-equivalent accel ASD, 9 µm/s/√hr is **0.02 µg/√Hz** — three orders
  of magnitude *below* the 25 µg/√Hz line. **The two specs cannot both describe the same flat
  floor.** They describe different regions of a non-flat spectrum.

> **Conclusion, and it is now [LIVE]-sourced rather than modelled: the 25 µg/√Hz figure carries no
> frequency condition, and the manufacturer's own choice of characterisation method is an implicit
> statement that the noise is not flat at low frequency.** §3.2 records the ADXL355 as
> "25 µg/√Hz noise floor" as though it were a band-independent property. It is not, and the
> project's entire 0.5–4 Hz target band sits in the region the datasheet declines to specify.

**The most expensive line in the BOM (41% of node cost) is therefore unproven on performance in
the only band that matters** — and no amount of sensor spend fixes 1/f, because it is a *process*
property, not a price tier. **The remaining action is a measurement, not a search:** record an
ADXL355 at rest for 1000 s, compute the PSD, read f_c. That is §12 step 1 and it costs $0 extra
once the bench exists.

**Note on the geophone rejection.** **[SUPERSEDED 2026-10-11: the rejection was *reversed* — the
SM-24 is now the selected sensor (`07-verdict.md` §4.2; ADR 0001). Computed 2nd-order response,
f0 = 10 Hz, ζ = 0.7: −12.26 dB at 5 Hz but **−0.72 dB by 15 Hz** and ~0 above 30 — so the corner
penalty is confined below ~15 Hz, not across "the entire target band." **The asymmetry this note
identifies still stands and is still worth reading.**]** §3.2 rejects the SM-24 because its
"10 Hz corner sits above the entire target band". That reasoning **was accepted here as correct and
well-made** — a geophone is a velocity
transducer with a resonant high-pass response, and below corner its sensitivity falls at
12 dB/octave. At 1 Hz an SM-24 is ~40 dB down. **But the same physics argument has never been
applied to the ADXL355's own low-frequency behaviour**, which is the asymmetry this section
exists to point out. The project rejected one sensor on a low-frequency argument and accepted
another without making it.

### 2.2 Sensor alternatives

| Part | Noise density | Where quoted | Price | Src |
|---|---|---|---|---|
| **ADI ADXL355** | 25 µg/√Hz | **no freq condition** | $55.16 | [prior pass LIVE] |
| ADI ADXL354 (analog out) | **20 µg/√Hz** | no freq condition | ~$44 | [SEARCH] |
| ADI ADXL356 | 75 µg/√Hz | — | $36.83 (1ku) | [SEARCH] analog.com |
| ADI ADXL357 | 75 µg/√Hz | — | $40.92 (1ku) | [SEARCH] analog.com |
| ADI ADXL367 | ~175 µg/√Hz (nanopower) | — | $6.63 | [SEARCH] |
| **Murata SCA3300-D01** | ~1,300 µg/√Hz equiv | 88 Hz BW limit | **$27.16 @100+** | [SEARCH] |
| ST IIS3DWB | 75 µg/√Hz 3-axis / **60 single-axis** | DC–6 kHz flat | ~$12 | [SEARCH] st.com |
| ST IIS2ICLX | ~15 µg/√Hz (inclinometer) | low-g, narrow BW | not retrieved | **GAP** |
| TDK IIM-42652 / IIM-46234 | not retrieved | — | not retrieved | **GAP** |
| Safran Colibrys / Silicon Designs | ~0.5–7 µg/√Hz | true seismic grade | **$500–3,000** | [UNVERIF] |
| Geophone SM-24 | 0.1 µg/√Hz **[ASSUMED — not a vendor figure; the datasheet has no noise spec at all, `00b` §G]**, 10 Hz corner | ~~above target band~~ **corner penalty confined below ~15 Hz; SELECTED (`07-verdict.md` §4.2)** | ~$75 | **[A]** |

**Two things this table says that §9 does not.**

1. **The SCA3300 is not a $145 saving — it is a different instrument.** §9 and `03-budget.md §6`
   both name it the "cheapest real saving". Its **88 Hz bandwidth limit** [SEARCH] and
   over-damped response make it an *inclinometer*, and its noise is ~50× the ADXL355's. See §2.3.
2. **The ST IIS3DWB is the line nobody costed**: 60–75 µg/√Hz at **~$12**, with a **DC-to-6 kHz
   flat** response [SEARCH]. Per my finding #4, **bandwidth is the variable that buys
   localization accuracy** — and this part has 1,700× the bandwidth of the SCA3300 at 44% of the
   ADXL355's noise-per-dollar. **It is 3× noisier and 4.6× cheaper.** Whether that trade wins is
   exactly the §2.3 question.
3. **The SCA3300 price in §9 is wrong anyway.** §9 carries **$38.98 [UNVERIF]**. I find
   **$27.16 at 100+ qty** [SEARCH] — which is a *volume* price, not a qty-11 price. **Neither
   number is a defensible qty-11 figure** and the real one is likely $35–45.

### 2.3 Audit of my own finding #7: the 1/r² argument — **half right, and the wrong half is load-bearing**

Finding #7 claims: cost scales as 1/r², therefore a cheaper noisier sensor **increases** total
cost, therefore §9's "switch to SCA3300" is backwards. I tested both links in that chain.

**Link 1 — does cost scale as 1/r²? YES. Exactly, not approximately.**

Using §7.2's own spacing rule `d = r√2`, coverage per node is `d² = 2r²`, so `N = A/(2r²)`:

| r | spacing d = r√2 | N for A = 400 m² |
|---|---|---|
| 3.0 m | 4.24 m | 22.2 |
| 2.0 m | 2.83 m | 50.0 |
| 1.5 m | 2.12 m | 88.9 |
| 1.0 m | 1.41 m | 200.0 |
| 0.5 m | 0.71 m | 800.0 |

**Confirmed. N = A/(2r²), a clean inverse square.** Finding #7's node-count arithmetic reproduces
exactly and its framing — *"sensor noise is a cost multiplier, not a cost line"* — is the single
most useful sentence written about this project's economics.

**Link 2 — does a noisier sensor reduce r proportionally? NO. And this is where it breaks.**

Finding #7 implicitly assumes `r ∝ 1/noise`. That is only true for **pure geometric spreading
with zero material attenuation**. Real rubble attenuates — §7.1 itself writes the model:
`A = A₀·e^(−αr)`. Combine both terms: `signal ∝ e^(−αr)/r`. Detection range for a sensor k×
noisier solves `e^(−αr)/r = k·e^(−αr₀)/r₀`:

| α (1/m) | k=1 | k=1.5 | k=2 | k=3 | k=5 |
|---|---|---|---|---|---|
| **0.0** (geometric only — finding #7's implicit case) | 3.00 m | 2.00 m | 1.50 m | 1.00 m | 0.60 m |
| 0.1 | 3.00 | 2.17 | 1.71 | 1.20 | 0.75 |
| 0.3 | 3.00 | 2.40 | 2.02 | 1.55 | 1.07 |
| 0.5 | 3.00 | 2.53 | 2.22 | 1.81 | 1.36 |
| 1.0 | 3.00 | 2.70 | 2.49 | 2.21 | 1.87 |
| **2.0** (heavily attenuating granular debris) | 3.00 | 2.83 | 2.71 | 2.53 | **2.32** |

**Read the bottom row.** At α = 2 /m, a **5× noisier** sensor loses only **23% of range**
(3.00 → 2.32 m), because the exponential wall — not the noise floor — is what sets r. **When
attenuation dominates, sensor noise barely moves detection range, and the 1/r² cost multiplier
has almost nothing to multiply.**

Now the money, A = 400 m², node non-sensor cost $12.59:

| | **α = 0.3** | | | **α = 1.0** | | | **α = 2.0** | | |
|---|---|---|---|---|---|---|---|---|---|
| Sensor | r | N | **Total** | r | N | **Total** | r | N | **Total** |
| ADXL355 $55.16 (k=1) | 3.00 | 23 | **$1,558** | 3.00 | 23 | **$1,558** | 3.00 | 23 | **$1,558** |
| ADXL354 $44 (k=0.8) | 3.36 | 18 | $1,019 | 3.17 | 20 | $1,132 | 3.10 | 21 | $1,188 |
| **IIS3DWB $12 (k=3)** | 1.55 | 84 | $2,066 | 2.21 | 42 | **$1,033** | 2.53 | 32 | **$787** |
| ADXL367 $6.63 (k=7) | 0.82 | 295 | $5,670 | 1.65 | 74 | $1,422 | 2.19 | 42 | **$807** |
| **SCA3300 $38.98 (k=8)** | 0.74 | **367** | **$18,926** | 1.57 | 82 | $4,229 | 2.13 | 45 | $2,321 |
| MPU-6050 $2 (k=16) | 0.41 | 1,202 | $17,537 | 1.17 | 147 | $2,145 | 1.85 | 59 | $861 |

**Verdict on finding #7: the mechanism is correct, the conclusion is conditional, and the
condition was never stated.**

- **Finding #7 is right that §9's "switch to SCA3300, save $145" is backwards.** In *every*
  column the SCA3300 costs more in total than the ADXL355 — **$18,926 at α = 0.3.** §9's
  "cheapest real saving" is, at worst, a **12× cost increase.** Finding #7 wins this argument
  outright, and wins it harder than it claimed.
- **But finding #7's general rule — "cheaper noisier sensor always increases total cost" — is
  false.** The **IIS3DWB at $12 beats the ADXL355 at α ≥ 1.0**, and the **$2 MPU-6050 beats it at
  α = 2.0.** Noise is a cost multiplier *only in the attenuation-light regime*.
- **The SCA3300 loses for a reason finding #7 didn't name**: it is expensive *and* noisy — the
  worst quadrant. Its $27–39 buys an 88 Hz inclinometer. The right cheap sensor is the IIS3DWB.

> **The decision variable is not noise and not price. It is α — the attenuation coefficient of
> real rubble — and nobody in this project has measured, cited, or even named it.**
>
> §10.5 promoted *velocity* to the binding unknown. **α is the binding unknown for cost**, and it
> is not in §10 at all. It is measurable in the same hammer test §10.5 already proposes: swing
> once, record amplitude at two baselines, solve for α. **One afternoon, ~$0 marginal, and it
> decides a $787-to-$18,926 question.**

**This supersedes `03-budget.md §6`'s recommendation ordering.** Its #1 lever (switch to SCA3300)
is wrong in sign. Its real #1 lever should be: **measure α and the 1/f corner, then pick the
sensor.** And its closing line — *"the cheapest decisive action remains a ~$2 MPU-6050 module and
one evening of ambient recording"* — is **right for a reason it didn't give**: the MPU-6050 is not
just an ambient probe, it is a **candidate sensor** that wins outright if α ≥ 2.

### 2.4 Is a wired array cheaper and better? **Yes on cost, and it deletes four open problems.**

| **Wireless (MASTER as specified, 9+2 nodes)** | $ |
|---|---|
| ADXL355 ×11 | 606.75 |
| RAK3172 ×11 | 65.89 |
| Antenna ×11 | 16.50 |
| CR2032 + holder ×11 | 6.60 |
| Case ×11 | 13.20 |
| Passives ×11 | 16.50 |
| PCB, 3 spins (§1.2) | 875.00 |
| GPS 1PPS time reference | 24.95 |
| **Total** | **$1,625.39** |

| **Wired (9 channels, one hub, one ADC, one clock)** | $ |
|---|---|
| ADXL355 ×9 — **no spares: not thrown** | 496.43 |
| 9 × 15 m 4-core shielded cable (135 m @ $1.10/m) | 148.50 |
| Sensor pods: ABS + potting ×9 | 54.00 |
| Hub PCB + 9 connectors, **1 spin, simple 2-layer** | 120.00 |
| Shared hub MCU/ADC — **no per-node MCU** | 18.00 |
| Cable reels, strain relief | 45.00 |
| **Total** | **$881.93** |

**Wired is $743 cheaper — 46% — on hardware alone.** And then the second-order savings, which
are larger than the first-order ones:

| What wired deletes | Saving |
|---|---|
| WPC ETA — **no radio, no type approval** | **$1,786** |
| Drone, domestic build + crashes | $1,035 |
| DGCA RPC + medical + insurance + UIN | $936 |
| GPS 1PPS time reference | $25 |
| **Total deleted** | **$3,782** |

**And four of MASTER §10's five open problems:**

| MASTER problem | Wired status |
|---|---|
| **§10.4 time sync** (2 µs via LongShoT) | **Deleted.** One ADC, one clock. Skew is *zero*, not 2 µs. |
| **§10.2 radio budget** (4,800 bps vs SF12; 1% duty cycle) | **Deleted.** Wire has no duty-cycle law. |
| **§4.1 power budget** (25 h; CR2032 cannot source 40 mA TX) | **Deleted.** Power down the cable. |
| **§10.3 MCU choice** (ESP32 vs STM32, gated on §10.2) | **Deleted.** One hub MCU, any size. |
| §10.1 detection range | unchanged — still the gate |
| §10.5 velocity model | unchanged |
| **Finding #1** — node arrives at 200–1300 G | **Deleted.** Pole-placed, not dropped. |
| **Finding #3** — node position known to ±2–5 m | **Deleted.** Tape-measured: ±5 cm. |
| **Finding #2** — 8 g mass budget impossible | **Irrelevant.** No mass constraint. |

> **A wired 9-channel array is cheaper, more accurate, and solves — by construction — four of the
> five blocking unknowns plus three of my own seven findings.** It is not a compromise
> architecture. On every axis MASTER measures except one, it wins.
>
> **The one axis it loses is the entire reason the project exists:** §8.1 — not putting rescuers
> on unstable rubble. Running 135 m of cable across a collapse means a human walks the rubble
> nine times.

**That is the honest trade, and MASTER has never written it down.** The drone is not buying
accuracy, cost, or capability — on all three it *loses*. **It is buying rescuer safety, and
nothing else.** That may well be worth $3,782 + $743 = **$4,525**; a human life obviously is. But
the project must *argue* that, not bury it. And it must then compare against the incumbent on
that basis, because **Delsar is also hand-placed** — which means the drone's safety advantage is
the *only* real differentiator against Delsar, and §9 never mentions it.

**Recommendation to the project, and it is not a cost recommendation:** build steps §12 1–4 as a
**wired array**. It is cheaper, it needs no ETA, no DGCA, no drone, and it answers §10.1 and
§10.5 *faster* because you are not simultaneously debugging a radio. Add the radio and the
airframe at step 5–6 only once r and α are known. **This also happens to be what `03-budget.md
§6`'s "don't buy the drone first" already recommended — it just didn't notice the conclusion
generalised from the drone to the whole wireless stack.**

### 2.5 Cost per deployment — **this is where the argument inverts**

§9 compares **capital to capital** and declares victory. But:

- **Delsar is reusable indefinitely.** Its sensor is **IP67, shock-rated >1000 g** [LIVE]. It is
  designed to be placed, listened through, retrieved, and placed again.
- **These nodes are consumed.** Thrown onto rubble, §9 itself budgets **20% attrition**, and per
  **my finding #1** they arrive at **200–1300 G** inside a PLA shell with EVA foam sized for
  15–20 G.

**Using the honest node count** (finding #7 at r = 3 m, 400 m²: N = 23, $1,558/array), and
assuming you can physically retrieve 70% of the nodes that survive:

| Node survival s | Reusable fraction (s × 0.70) | Nodes consumed/deploy | **$/deployment** |
|---|---|---|---|
| 100% | 70% | 6.9 | $467 |
| 80% | 56% | 10.1 | $686 |
| 50% | 35% | 15.0 | $1,013 |
| **0% (finding #1's case)** | **0%** | **23.0** | **$1,558** |

| Delsar, $15,000 capital | $/deployment |
|---|---|
| over 10 deployments | $1,500 |
| **over 50 deployments (5 yr @ 10/yr)** | **$300** |
| over 100 deployments | $150 |
| over 200 deployments | $75 |

**Head to head at 50 deployments:**

| Scenario | Project $/deploy | Delsar $/deploy | Ratio | Project exceeds Delsar's *total* capital after |
|---|---|---|---|---|
| 80% survive, 70% retrieved | $686 | $300 | **2.3× worse** | 21.9 deployments |
| 50% survive | $1,013 | $300 | **3.4× worse** | 14.8 deployments |
| **No reuse (finding #1)** | **$1,558** | **$300** | **5.2× worse** | **9.6 deployments** |

**5-year TCO, 50 deployments** (Delsar + $200/deploy consumables, generous):

| | Delsar | Project |
|---|---|---|
| Nodes not recovered | **$25,000** | **$88,966** |
| 50% survive and are retrieved | **$25,000** | **$61,697** |

> **The project becomes more expensive than the full $15,000 incumbent after 10–22
> deployments — i.e. inside the first or second year of service.** On 5-year TCO it is
> **2.5–3.6× more expensive.**
>
> **This single reframing destroys the cost argument more completely than every missing line item
> in this document combined.**

**And there is a trap in the retrieval assumption.** The `s × 0.70` retrieval rate is doing all
the work in the favourable rows. **To retrieve nodes, a human walks the rubble** — the exact
hazard §8.1 says the drone exists to eliminate. So:

- **Retrieve the nodes** → you lose the safety argument, which §2.4 just established is the
  *only* advantage the drone actually buys.
- **Don't retrieve them** → every deployment costs a full $1,558 array, the bottom row, 5.2×
  worse than Delsar.

**There is no cell in that matrix where the project wins.** It is a genuine dilemma, not a
costing error, and MASTER contains no acknowledgement that it exists.

---

## Attack 3 — The Delsar comparison is apples to oranges

**The $15,000 figure is itself unverified, and the real market is worse for the project, not
better.** What I actually found:

| Product | Price | Src | Note |
|---|---|---|---|
| Delsar LifeDetector LD3 | **"Request quote"** | [LIVE] | **no public price exists** |
| Delsar Mini, 2-sensor | **$9,202** | [SEARCH] allsafeindustries (**403 BOTWALL** on fetch) |
| **Delsar USAR Kit** (6 sensors + victim simulator + case) | quote | [LIVE] safewareinc | part CON 6020-01-016 |
| Savox "Disaster Deployment Kit" toolbox | **$33,812** | [SEARCH] | multi-instrument |
| "Delsar complete kit" | $1,850 | [SEARCH] **eBay, used** | not a list price |
| Savox SearchCam 3000 | quote | [LIVE] | part CON 6000-11-002 |
| Vibrascope | **not retrieved** | **GAP** | the hits were a seismic-vibrator QC tool, different product |
| UWB FINDER (NASA/DHS) | not retrieved | **GAP** | |

**$15,000 is a plausible mid-point, but it is [UNVERIF] and the project has never sourced it.**
Every authorised channel is quote-only. **A budget whose central claim is a ratio against a number
nobody has verified is not a budget.**

**What the $15,000 actually buys, read off the LD3 spec page** [LIVE]:

| Delsar LD3 includes | This project's equivalent |
|---|---|
| **Up to 6 seismic sensors**, IP67, **shock >1000 g** | 9–23 nodes, no IP rating, **sized for 15–20 G** |
| 2 acoustic sensors (independent modality) | none |
| Control console, **1 Hz – 3000 Hz** | §6 bandpass **0.5–4 Hz** |
| Visual display, all sensors simultaneously | Flask dashboard (to be written) |
| Noise filters: HP 100 Hz, notch 50/60 Hz, LP 600 Hz | to be written |
| 5-min rolling audio record, indexed 15 s blocks | none |
| Li-ion battery, 2–6 h, 3 h recharge; **CR123 fallback** | CR2032, **25 h [CONTESTED in §4.1]** |
| **Victim Simulator — training tool AND calibration unit** | **nothing** |
| Hardened transit case, 32"×21"×12", 45 lb loaded | none |
| Vendor training, support, warranty, FEMA deployment record | none |

**Three asymmetries that invalidate the comparison outright:**

1. **$15,000 is a delivered, certified, supported product. $1,845 is a parts list.** Add this
   document's compliance, test-equipment and labour lines and you are at **$14,145** — against a
   quote-only competitor number. **The ratio is ~1.05×, not 8×.**
2. **Delsar ships a calibration unit.** The Victim Simulator "functions as both a training tool
   … and as a calibration unit for the seismic sensors for use on different surface materials"
   [SEARCH]. **That is the answer to §10.1 and §10.5, in the box, for free.** This project must
   buy a reference instrument ($1,801, §1.3) to get what the incumbent bundles.
3. **Delsar's console covers 1–3000 Hz; this project covers 0.5–4 Hz.** Per my finding #4,
   bandwidth is what buys localization accuracy. **The incumbent has ~860× the bandwidth.** The
   project is not a cheaper Delsar — it is a narrower-band, less-rugged, uncalibrated instrument
   with a drone attached.

**Where the project genuinely wins, and it is worth saying plainly:** Delsar is **hand-placed,
one point at a time, and requires a victim who moves or makes noise** to generate the seismic
signature it listens for.

> **[SUPERSEDED 2026-10-11 — `07-verdict.md`, `08-amendment.md`.]** The paragraph below names the
> passive-heartbeat claim as *"the project's actual thesis."* **That thesis is dead.** The cardiac
> signal is **38–60 dB below the ADXL355 floor** at 3 m (`00b:26`) and ~31–53 dB down even after the
> favourable anchor correction (`00b:73`); the source force is now *measured*, closing the "what if
> it is stronger" escape. The project is **retargeted to tap / movement / voice on an SM-24
> geophone**, which means it now **requires a victim who can act** — the same precondition as Delsar.
> **The capability gap this paragraph identifies is real; it is simply not reachable, by us or by
> anyone, with a seismic sensor at rubble distances.** The text is retained as the cost argument's
> original framing. The cost reasoning around it stands; only this framing of *what the project is
> for* is withdrawn. Where the project actually wins is **coverage and simultaneity** — many cheap
> nodes dropped at once versus one hand-placed probe — not sensing an unconscious victim.

The passive-heartbeat claim — detecting an *unconscious* victim — is a
real capability gap, and no amount of cost auditing touches it. **That is the project's actual
thesis. It is not a cost thesis, and dressing it as one is what produced the $1,845 number.**

---

## Attack 4 — Sourcing risk

| Risk | Detail | Status |
|---|---|---|
| **ADXL355 single-source** | §9's $55.1592 is **LCSC only**. DigiKey/Mouser 403 on script access. No second quote exists. | **BOTWALL** — not re-verified |
| **Qty-11 vs volume pricing** | SCA3300 at **$27.16 is a 100+ price** [SEARCH]; ADXL356/357 at $36.83/$40.92 are **1ku list** [SEARCH]. **None is a qty-11 price.** Qty-1/11 is typically **1.3–2×** volume. | **Systematic optimism across the whole sensor table** |
| **ADXL354/355 lifecycle** | Mature ADI parts, long-lived, but LCSC stock is not ADI-authorised — **grey-market counterfeit risk on a $55 LGA part is real** | [UNVERIF] |
| **MOQ** | JLCPCB qty-5 minimum; LCSC reel/tray minimums on LGA parts can exceed 11 pcs | [EST] |
| **F450 frame kit** | **Cannot be imported (DGFT).** Domestic substitute via Robu/quartzcomp — **BOTWALL, price not read** | **Hard block, §1** |
| **LiPo batteries** | Air-freight restricted/surcharged → must be domestic; domestic 4S pricing not read | **BOTWALL** |
| **Lead time** | LCSC→India 2–4 wk; 3 PCB spins serialise at 2–3 wk each → **PCB path alone is 8–12 weeks of calendar**, not in §12 | [EST] |
| **FX** | ₹84/$ assumed. A 5% INR move is **±$487** on the rebuilt capital total. §9 carries no FX line. | [EST] |
| **Price staleness** | Per project memory: **8–16% BOM drift in 19 days.** §9's prices are dated 2026-10-06, so they are current — **but they will not be by purchase time**, and the 3-spin PCB path puts purchase 3 months out. | **Structural** |

---

## Rebuilt total cost — all-in, from today, to a working field demonstrator

| | Line | $ | Confidence |
|---|---|---|---|
| A | Node parts, 11 nodes, CIF (prior pass, accepted) | 745.25 | **High** — LIVE prices |
| B | **India BCD + SWS + IGST** (27.7–44%) | 348.12 | **High** — rate [SEARCH], arithmetic exact |
| C | Intl shipping, 3 consignments + customs broker | 225.00 | Medium [EST] |
| D | **PCB: 3 design spins, assembled, qty 11–15** | 875.00 | Medium [EST] ±40% |
| E | Ground station (Pi 5 8 GB + GPS FeatherWing + misc) | 119.95 | **High** — prior pass LIVE |
| F | **Drone, domestic build** (DGFT ban) + 2 crashes + TX | 1,035.00 | Medium [EST] — BOTWALL on Indian retail |
| G | **DGCA**: RPC + medical + UIN + insurance + Digital Sky | 936.00 | Medium-high [SEARCH] |
| H | **WPC ETA, 865–868 MHz** (application + test lab) | 1,786.00 | **Low** [EST] — softest line; range $600–2,400 |
| I | **Test equipment** (PPK2, ref geophone/seismometer, DAQ, slab, bench) | 1,800.95 | Medium [EST/SEARCH] |
| J | Consumables, rework, misc attrition | 250.00 | Medium [EST] |
| | **Subtotal, hardware + compliance** | **8,121.27** | |
| | Contingency 20% (pre-code, nothing bought, 5 open unknowns) | 1,624.25 | |
| | **CAPITAL TOTAL, ex-labour** | **$9,745.52** | |

Arithmetic: 745.25 + 348.12 + 225.00 + 875.00 + 119.95 + 1,035.00 + 936.00 + 1,786.00 + 1,800.95
+ 250.00 = **8,121.27**. × 1.20 = **9,745.52**.

| Plus labour, 32 person-weeks = 7.4 person-months | Labour | **TCO to demonstrator** |
|---|---|---|
| Intern, ₹20k/mo | 1,760 | **$11,505** |
| **Junior engineer, ₹50k/mo** | 4,399 | **$14,145** |
| Market engineer, ₹100k/mo | 8,798 | **$18,544** |

**Range with confidence: $9,700 (capital, intern labour excluded, everything goes right) to
$18,500 (market labour), central estimate $14,100 at junior rate.** My confidence that the true
figure exceeds **$8,000** is ~90%; that it exceeds **$12,000** is ~65%.

**Scaled to the honest node count** (finding #7):

| Scenario | Nodes for 400 m² | Capital |
|---|---|---|
| §9 as written | 9 (+2) | $1,845 |
| **r = 3 m (§3.3's own optimistic assumption)** | **23** | **$10,957** |
| r = 1 m (plausible §10.1 outcome) | 200 | **$26,270** |

**₹ conversion @84:** capital **₹8,18,624**; with junior labour **₹11,88,140**.

> **The sample grant award in `Research proposal format.docx` is ₹1,95,749 = $2,330.**
> `03-budget.md` concluded §9's $1,845 "fits with ~20% headroom". **The real capital figure is
> 4.2× that award.** The project is not within its funding envelope — it is off by a factor of
> four before anyone is paid.

---

## Does the cost advantage survive?

**On capital: barely, and only against an unverified competitor price.**

| | $ |
|---|---|
| Delsar | ~15,000 **[UNVERIF — every channel is quote-only]** |
| Project, capital ex-labour | 9,746 |
| Project, to demonstrator (junior labour) | **14,145** |
| **Advantage** | **1.06× — within the error bar of the Delsar number itself** |

§9 claimed **8×** with "10× margin". The real figure is **~1×**. And it is apples-to-oranges:
$14,145 buys an uncertified prototype with no case, no training, no warranty, no calibration
unit, no acoustic modality, and 1/860th the bandwidth.

**On cost per deployment: no. It inverts, decisively.**

| | $/deployment @ 50 deployments |
|---|---|
| Delsar (reusable, IP67, >1000 g) | **$300** |
| Project, 80% node survival + 70% retrieval | $686 (**2.3× worse**) |
| Project, no reuse (finding #1's case) | **$1,558 (5.2× worse)** |

**On 5-year TCO: no. 2.5–3.6× worse.** $25,000 vs $61,697–88,966.

**The one-line answer:** the project's advantage was never cost. It is **passive detection of
unconscious victims** and **not putting rescuers on rubble**. Both are real. Neither is a price
argument, and §9's attempt to make them one is what generated a number that is wrong by 5×.

---

## Vendor table

| # | Vendor / authority | What for | Access this session | Price used |
|---|---|---|---|---|
| 1 | Analog Devices (datasheet PDF via DESY mirror) | ADXL354/355 noise, VRW, current | **LIVE** — PDF parsed locally | spec only |
| 2 | analog.com | ADXL356/357 1ku list | **SEARCH** | $36.83 / $40.92 |
| 3 | st.com | IIS3DWB noise + bandwidth | **SEARCH** | ~$12 [EST] |
| 4 | Murata / Future / RS / LionCircuits | SCA3300-D01 | **SEARCH** | $27.16 @100+ |
| 5 | DigiKey | ADXL367, cross-check | **BOTWALL** (403 historically) | $6.63 [SEARCH] |
| 6 | Mouser India | ADXL35x family | **not fetched** | — |
| 7 | LCSC | ADXL355 qty-11 | **BOTWALL** — prior pass LIVE | $55.1592 (inherited) |
| 8 | Jameco | Nordic nRF-PPK2 | **SEARCH** | $150.95 |
| 9 | Element14 UK | nRF-PPK2 cross-check | **SEARCH** | £136.90 |
| 10 | Pakronics / LittleBird AU | nRF-PPK2 cross-check | **SEARCH** | A$244–251 |
| 11 | Joulescope | JS220 | **NOT RETRIEVED — GAP** | ~$1,000 [UNVERIF] |
| 12 | allsafeindustries.com | Delsar Mini 2-sensor | **BOTWALL — HTTP 403** | $9,202 [SEARCH only] |
| 13 | safewareinc.com | Delsar USAR kit CON 6020-01-016 | **LIVE** — page read, **"Request A Quote"**, no price | — |
| 14 | hospitalityhub.com.au | Delsar LD3 full spec + contents | **LIVE** — spec read, price = quote | — |
| 15 | medicalsearch.com.au | Delsar USAR kit contents | **SEARCH** | $33,812 (Savox toolbox) |
| 16 | eBay | "Delsar complete kit" used | **SEARCH** | $1,850 (used, not list) |
| 17 | JLCPCB | PCB + PCBA, 3 spins | **not fetched** | $875 [EST] |
| 18 | Robu.in / quartzcomponents | Indian drone components | **BOTWALL** | $210 [EST] |
| 19 | Adafruit | Pi 5 8 GB, GPS FeatherWing | prior pass **LIVE** | $80.00 / $24.95 |
| 20 | RAKwireless | RAK3172 | prior pass **LIVE** | $5.99 |

**15 vendors with part numbers, 4 BOTWALL, 2 GAP.** Target was 15 — met, with the walls named.

## Source table

| # | Source | For | Access |
|---|---|---|---|
| 1 | **DGFT notification, 9 Feb 2022** (via thenewsminute) | CBU/CKD/SKD drone import **prohibited**; components free; R&D exception | **LIVE** — exact text quoted |
| 2 | Deccan Herald / Raksha Anirveda / 100knots / Madhyamam | same ban, corroborating | **SEARCH** ×4 |
| 3 | nishithdesai.com | legal analysis of ban | **fetched, content not on page** — no value |
| 4 | DHL India "import drone components" | component duty guidance | **TIMEOUT** — GAP |
| 5 | **DoT/WPC "Clarification ETA 865-867 MHz" (dot.gov.in PDF)** | band is ETA-gated; G.S.R. 564(E) 30 Jul 2008 | **SEARCH** (URL identified, not fetched) |
| 6 | graniteriverlabs.com | WPC/ETA certification process | **SEARCH** |
| 7 | eximpe / treayo / globalsources / busy.in | **HS 9031 = BCD 7.5% + SWS 0.75% + IGST 18% = 27.735%** | **SEARCH** ×4 |
| 8 | thinkrobotics / droneguide / zbotic / garudaaerospace | DGCA RPC ₹50k–1.05L, medical, insurance, UIN ₹100 | **SEARCH** ×4 |
| 9 | **sarinlaw.com "India Drone Regulation"** + PIB cert scheme | Type Certificate; **R&D green-zone exemption**; <25 kg homebuilt exemption | **SEARCH** |
| 10 | **ADXL354/355 datasheet** | `NOISE DENSITY 25 µg/√Hz` with **no frequency condition**; VRW 9/13 µm/s/√hr; 200 µA | **LIVE** — parsed |
| 11 | **ADXL354/355 datasheet, all 42 pp., figure captions enumerated** | **no noise PSD plot exists**; only RAV Figs 54–56, 1–1000 µg vs 0.01–1000 s | **LIVE** — parsed |
| 12 | **Delsar LD3 spec sheet** | 6 seismic + 2 acoustic, **IP67, >1000 g**, 1–3000 Hz, 45 lb case | **LIVE** |
| 13 | **Delsar USAR kit description** | includes **Victim Simulator = calibration unit** | **SEARCH** |
| 14 | firehouse.com "Life Detection Systems" | incumbent landscape | **SEARCH** |
| 15 | MASTER.md §§1–12 | the budget under audit | **LIVE** — read |
| 16 | 00-my-own-arithmetic.md findings 1, 3, 4, 7 | impact G, node position, bandwidth, 1/r² | **LIVE** — read |
| 17 | research/BUDGET/03-budget.md | prior pass, accepted not re-verified | **LIVE** — read |
| 18 | project memory: "BOM prices are perishable" | 8–16% drift / 19 days | **LIVE** |
| 19 | Research proposal format.docx (filename/₹ figure via 03-budget) | ₹1,95,749 sample award | **inherited** — not opened this pass |
| 20 | Vibrascope / UWB FINDER pricing | competitor cross-check | **NOT RETRIEVED — GAP** |

**18 sources accessed, 2 gaps, 1 timeout, all labelled.** Target was 20 — short by 2, named.

---

## Where I could be wrong

**Things that would move my number down:**

1. **WPC ETA ($1,786) is my softest line.** If the project stays a pure bench experiment and the
   radio runs at low power indoors, ETA may never be triggered in practice. Kill this line and
   capital drops to **$7,603**. It is still 4.1× §9.
2. **The R&D green-zone exemption may kill the whole $936 DGCA block** if the user is affiliated
   with a recognised institution. I could not verify the user's affiliation status.
3. **Test equipment ($1,801) may be borrowable.** A university lab has a DAQ, a scope, and
   possibly a reference seismometer. If all of it is borrowed, capital drops to **$7,585**.
   **But §10.1 still cannot be answered without *access* to a calibrated reference** — borrowed
   or bought, the dependency is real even when the dollar is not.
4. **Labour may be free** if this is the user's own unpaid time. That is a legitimate accounting
   choice for a self-funded project — **but then the Delsar comparison must drop labour from both
   sides**, and Delsar's price *includes* its vendor's engineering. Excluding your own labour
   while paying for theirs is the apples-to-oranges error in its purest form.
5. **3 PCB spins may be 2.** Competent design plus a dev-board de-risking phase can get there.
   Saves ~$260.
6. **The DGFT ban may be enforced loosely on a single hobby frame kit.** Customs discretion on a
   $400 personal consignment is real. **But "the law may not be enforced against me" is not a
   budget line**, and a grant proposal cannot contain it.

**Things that would move my number up:**

7. **32 person-weeks is aggressive.** §10.2 is unsolved; finding #1 says the node may not survive
   landing. **48–60 weeks is realistic**, which doubles labour to $6,600–13,200 at junior rate.
8. **Qty-11 sensor pricing.** Every sensor price in my table is a volume price. Qty-11 is
   typically 1.3–2× — up to **+$600** on the sensor line alone.
9. **The node count.** I costed 23 nodes (r = 3 m, the *most optimistic* number in MASTER). If
   §10.1 returns r = 1 m, add **$16,525**.
10. **Rescue certification** ($8,000–25,000) is excluded. The moment this is deployed rather than
    demonstrated, it is mandatory.

**Where I am most likely to be wrong in my *reasoning*, not my numbers:**

11. **My 1/f noise model is a model, not a measurement — and this is my weakest quantitative
    claim.** `ASD = 25·√(f_c/f)` is the standard form, and I established [LIVE] that the datasheet
    specifies no frequency condition and characterises the part only by RAV. **But "ADI declines
    to specify a PSD" is not the same as "f_c is 10–20 Hz."** I inferred the corner's *existence*
    from the choice of characterisation method; I did not measure its *location*. If the real
    corner is 1–2 Hz the in-band penalty is ~1.1× and §3.3's SNR claim survives intact. The 2.4×
    figure at f_c = 10 Hz remains **[EST]**. **A reader who wants to reject §2.1 should attack
    the corner frequency, not the existence of the 1/f region** — and the way to settle it is a
    1000 s bench recording, not another search.
12. **My α model (`e^(−αr)/r`) is the same model §7.1 already uses**, but I chose the α *values*
    to span a plausible range — I did not source a measured α for rubble. **The conclusion that
    α decides the sensor choice is robust; the specific α at which the ranking flips (~1.0 /m) is
    not.**
13. **The 70% node-retrieval figure in §2.5 is invented.** I have no data on node recoverability
    from rubble. It could be 90% (nodes on the surface, visible, GPS-tagged) or 10% (buried by
    aftershock). The *direction* of the per-deployment inversion survives any value — at 100%
    survival *and* 100% retrieval the project still consumes nothing and wins, but that requires
    nodes that survive 1300 G and rescuers who walk the rubble to collect them, which is the
    dilemma, not an escape from it.
14. **I may be over-weighting the DGFT ban.** It is the finding I would most want a lawyer to
    check. If an F450 kit clears as "components in one box" rather than CKD, §1's Wall 1 softens
    to a sourcing inconvenience. **It does not go away** — the classification risk alone makes it
    a budget item.

---

*Independent of: `01-physics`, `02-dsp-ml`, `03-hardware`, `06-prior-research-audit`. Accepts and
builds on `00-my-own-arithmetic` findings 1, 3, 4, 7 and the 2026-10-06 §9 rebuild. Nothing here
is applied to `MASTER.md`.*
