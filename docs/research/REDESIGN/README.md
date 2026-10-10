# Redesign Pass — consolidated

**Consolidated 2026-10-11** from five files (`01-literature.md`, `02-vendor-register.md`,
`03-proposals.md`, `04-verification-log.md` and the previous README) into this one. The originals
were never applied, and the premise they proposed redesigns *for* is disproven — so the pass is
preserved as **one finding that matters, two that partly survive, and a methodological record**,
rather than five documents implying live work.

> ### ⛔ Status: SUGGESTIONS ONLY — nothing in this pass was ever applied
>
> **The premise is dead.** This pass proposed redesigns for **heartbeat detection**, disproven by
> 38–60 dB (`../../critique/07-verdict.md`). The retarget is **tap/voice**.
>
> **The band is superseded too — ADR 0001, 2026-10-11.** **None of 0.5–4 Hz, 10–100 Hz, 5–40 Hz or
> 60–80 Hz is the project's position.** 5–40 Hz came from **seismocardiography**; 10–100 Hz (which
> this pass used) is **PigV²'s heartbeat band**; 60–80 Hz is *"NO DATA FOUND."* **Acquire 5–200 Hz;
> the detection band is an output of the M1/M2 bench measurement.** See
> `../../critique/10-doc-sweep-action-report.md` §2.
>
> **The sensor is superseded.** This pass argued MEMS-vs-geophone from Sercel vendor material; the
> project **reversed** that conclusion. **The SM-24 is the selected sensor.**

**Audited by** `../../critique/06-prior-research-audit.md` (rows 16–19), whose verdict was that
*"the REDESIGN pass — the one asked to propose fixes — found almost nothing wrong with its own
tooling."* That audit cites this pass's findings by designator (**R1–R5**, **A34–A51**, **D19–D24**,
**E17–E19**), and every designator it names is preserved below.

---

## ⭐ R1 — The one finding that fully survives, and it is a large one

**MASTER §5 cites the wrong Gazette table.** This is the decisive result of the pass and it is
**unaffected** by the dead premise, the band or the sensor, because it is a matter of law.

**Primary source:** **G.S.R. 853(E)**, *Gazette of India* Extraordinary Pt II §3(i), **10 Dec 2021**
— *Use of Low Power Equipment in the Frequency Band 865–868 MHz for Short Range Devices (Exemption
from Licence) Rules, 2021.* 📄 **HELD, quoted from the PDF.**
<https://thc.nic.in/Central%20Governmental%20Rules/use%20of%20low%20power%20Equipment%20in%20the%20frequency%20band%20865%20to%20868%20MHz%20for%20Short%20Range%20Devices%20Exemption%20from%20Licence%20Rules,2021.pdf>

The device is **not** a Non-Specific SRD. **The Gazette's own note places "Emergency detection of
buried victims" in Table-II.**

| | Table-I (what MASTER assumed) | **Table-II (what applies)** |
|---|---|---|
| Role | Non-Specific SRD | **Tracking / Tracing / Data Acquisition** |
| Power | 25 mW e.r.p. | **500 mW e.r.p.** |
| Duty cycle | 1% | **≤2.5%** (≤10% for network access points) |
| Occupied BW | — | **≤200 kHz** |
| Other | — | **Adaptive Power Control required** |

**Worth +13 dB of e.r.p.** = a **4.47× range multiplier** in free space (n=2), **2.35×** in clutter
(n=3.5), and **2.5× the airtime**. Verified against two independent regulatory sources.

**Caveats, stated once.** APC must be *implemented*, not assumed. LoRa at **BW125 complies** on
bandwidth — **BW250 and BW500 do not**, which closes the "go wider to cut airtime" escape. Licence
exemption is **non-interference, non-protection, shared basis** (rule 3). A device sold in India
needs **ETA/WPC** conformance regardless (~$1,786 per model, `../../critique/04-cost-kill-attempt.md`).

**Band:** **865–868 MHz**, per rule 1, which expressly supersedes the 2005 RFID instrument. The
865–867 figure in older docs is that dead instrument — corrected across the tree 2026-10-11.

Supporting: **ETSI EN 300 220-2 V3.2.1 (2018-06)**, the harmonised standard G.S.R. 853(E) cites in
its own column 6 · **LoRa Alliance RP002** (IN865 duty cycle/dwell, LBT, max EIRP) · TTN duty-cycle
docs (**1% = 864 s airtime/day**, applied per device/channel/sub-band).

---

## R3 — The CR2032 finding: partly survives, and the diagnosis is right

**The coin-cell problem is pulse current, not capacity.** 72 h needs 77 mAh, which the cell has.
What it does not have is pulse capability:

| Cell state | ESR | Droop @40 mA | Rail | |
|---|---|---|---|---|
| Fresh | 10 Ω | 0.40 V | 2.60 V | marginal |
| Aged | 30 Ω | **1.20 V** | **1.80 V** | **brownout** |

**The principle survives.** Two independent cheap fixes, neither requiring abandonment of the coin
cell: a **supercapacitor across the cell** (~10:1 pulse reduction — Avnet Abacus: a 1 F supercap at
860 mΩ ESR cuts pulse draw to ~3 mA), or **LiMnO₂ instead of Li-SOCl₂** where pulse capability is
the selection criterion.

**A part number in it was wrong** (the reason this finding is "partly"). Vendor register, prices
pulled from vendor page payloads **2026-10-06** and **perishable** — two had already moved again
within the pass:

| Vendor | Part | Price | Access |
|---|---|---|---|
| KEMET (Mouser IN) | FS0H224ZF — 0.22 F 5.5 V, **25 Ω** ESR | ₹424.90 @1 `[SEARCH]` | 🔒 403-to-script |
| KEMET (Mouser IN) | FYD0H223ZF — 0.022 F 5.5 V, **220 Ω** ESR | ₹285.13 @1 `[SEARCH]` | 🔒 |
| KEMET (DigiKey) | FYL0H223ZF — 22 mF 5.5 V, 200 Ω @1 kHz | ~$4.00 `[SEARCH]` | 🔒 403 |
| **CAP-XX** | Prismatic — **ESR 50–100 mΩ**, 100–800 mF, <1 µA leakage | quote-only | ✅ |

**CAP-XX is the right part class** (50–100 mΩ vs KEMET's 25–220 Ω) but is quote-only. Supercap
figures come from **TI SLVAES7** and **Avnet**, not from the cap-xx PDFs — see the dead-link note
below.

---

## R2, R4, R5 — superseded or absorbed

| # | Finding | Disposition |
|---|---|---|
| **R2** | **Every working system in the literature transmits inferences, not waveforms.** LightEQ: 100 kB RAM, F1 0.99. Volcano WSN: 16% of data | **Still true and still the right architecture**, but it was never this pass's to own — it is the MEMS pass's position, re-sourced. The 24 B batched summary once per 60 s is critiqued at `../../critique/00-my-own-arithmetic.md:145` |
| **R4** | **Coupling vs self-righting is solved prior art** — gimballed inner housing, or rotationally-invariant calibration in software. **The enclosure must out-perform the MEMS in frequency response** and should impedance-match the ground | **Absorbed and now load-bearing elsewhere.** `06:638-640` found this restated the MEMS pass's own existing position (*attitude is free in software; the spike/anchor is the hard part*). The live version is in `../MEMS/06-build-vs-buy.md` as an open problem — ±10° tilt vs ±30° landing, coupling vs self-righting |
| **R5** | **UAV sensor-dart deployment is prior art with a stated aerodynamic spec, and patents cover it. Check FTO before designing** | **Survives as a live warning.** Prior art is Stewart et al. SEG 2016 and SeismicDart. Note `arXiv 2302.09533` restores *communications* coverage, **not sensor coverage** — it is not precedent for sensor deployment |

---

## Verification record (A34–A51, D19–D24, E17–E19)

Numbering continues from `../BUDGET/` (A33, D18, E16). **Audit passes per finding: 2.**

**38 URLs machine-verified, three-state, title-scoped:** ✅ 30 LIVE · 🔒 4 BOTWALL · ❌ **3 DEAD** ·
⚠️ 1 UNREACHABLE.

**The three DEAD links are cap-xx PDFs** (`AB1004`, `AB1025`, `CAP-XX-Product-Guide`) — that whole
`/datasheets/` path is gone. **They are cited for no claim**; the supercapacitor numbers come from
TI SLVAES7 and Avnet instead.

**E17 — the lesson worth keeping: the link classifier was itself wrong first.** It tagged a 404 as
LIVE until patched. **HTTP 200 does not mean a page exists** — vendor sites serve soft 404s, 200
with a "Page Not Found" body. Always inspect the response body, and `GET` not `HEAD`. If one tag is
wrong, re-check everything verified the same way.

**Superseded instruments correctly identified as superseded** (do not "fix" these rows): G.S.R.
37(E) — 865–867 MHz amendment rules 2007; *Use of low power equipment 865–867 MHz for RFID
(Exemption) Rules,* **2005**. Both are the dead instruments G.S.R. 853(E) replaced.

---

## Citations unique to this pass

All but one of this pass's sources also appear in `../BUDGET/01-literature.md`. The exception,
preserved here so it is not orphaned:

- **ETH Zürich, DOI `10.3929/ETHZ-B-000281405`**

Everything else — USGS SIR 2023-5061, DSME-LoRa (`arXiv 2206.14077`), `arXiv 2302.09533`,
`arXiv 2006.12570`, `arXiv 2312.08387`, `arXiv 2111.05457` — is cited from `../BUDGET/01` with
extracts in `../BUDGET/extracts/`.
