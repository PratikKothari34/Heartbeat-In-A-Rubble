# Redesign Proposals — SUGGESTIONS ONLY


> ## ⚠ PARTLY SUPERSEDED — 2026-10-08
>
> **Nothing in this folder was ever applied** (as its own heading says), and the premise it proposed
> redesigns for — heartbeat detection — is **disproven**: see `docs/critique/07-verdict.md`.
>
> **The one finding below that survives and matters is the regulatory one** (G.S.R. 853(E) Table-II,
> duty cycle set per device category, 865–868 MHz): independently re-verified against the Gazette
> PDF and **CONFIRMED**. The supercap recharge *principle* also survives, though a part number in it
> was wrong.
>
 ⚠ **The band is superseded too — ADR 0001, 2026-10-11.** This marker was written 2026-10-08, three
> days before the band was settled, so it reverses the premise and the sensor but **not the band**.
> **None of 0.5–4 Hz, 10–100 Hz, 5–40 Hz or 60–80 Hz is the project's position:** 5–40 Hz came from
> **seismocardiography** literature (a cardiac band, for the dead premise) and 60–80 Hz is *"NO DATA
> FOUND"*. **Acquire 5–200 Hz; the detection band is an output of the M1/M2 bench measurement.**
> Where one figure is unavoidable: `20–80 Hz [ASSERTED — pending M2]`. The margin figures do not move
> on any band (`00b-verification-arithmetic.md:85-95`).
>
> **What does not survive:** the 24 B batched-summary proposal — a tap/voice packet needs **82–156 B**,
> and the STM32WLE5JC has **64 kB** SRAM, not 100 kB, so the planned input buffer alone is 70.3 kB
> (110 % of the part). See `docs/critique/06-prior-research-audit.md`.

**Status: nothing in this folder has been applied.** No existing doc was edited, no decision
recorded, no ADR written. This folder proposes; `MASTER.md` and `docs/decisions/` still say what
they said. Research date **2026-10-06**.

**Scope.** The prior pass (`../BUDGET/`) answered *what it costs* and found three MASTER section
pairs that cannot both be true. This pass answers the next question — **which of those need a
redesign, and what should the redesign be** — at the same evidence bar: ≥20 referred sources per
concept, ≥15 vendors, every link three-state verified, every number recomputed from raw inputs.

---

## The one finding that changes the project

> ### MASTER §5's "~1% duty cycle" is the wrong regulatory limit for this device.
>
> India's **G.S.R. 853(E)** (10 Dec 2021) sets duty cycle **per device category**, not per band.
> MASTER applies the **Table-I** figure (Non-Specific SRD: 25 mW e.r.p., 1%).
> This project belongs in **Table-II**, whose note names the application outright:
>
> > *"Tracking, Tracing and Data Acquisition Devices **also include devices for Emergency
> > detection of buried victims** and valuable items such as detecting avalanche victims…"*
>
> **Table-II allows 500 mW e.r.p. at ≤2.5% duty cycle** (≤10% for network access points),
> subject to Adaptive Power Control and ≤200 kHz bandwidth.

**What that is worth:** **20× the radiated power (+13 dB)** and **2.5× the airtime.** Read from
the Gazette PDF itself, and independently confirmed against ERC Rec 70-03 / ETSI EN 300 220, which
carry the identical category and the same avalanche-victim wording — India mirrors the European
allocation. → `01-literature.md` **R1**, `04-verification-log.md` **A34**

**This does not rescue §4.1.** MASTER's own architecture is still illegal by a wide margin
(§5.1 at SF12 = **179% duty cycle**). It changes *how far the redesign has to go*, and it makes the
link budget far easier than §5 assumes.

---

## Verdict: 2 redesigns, 2 re-derivations, 1 correction

| # | Item | Verdict | Why |
|---|---|---|---|
| **1** | **Node data architecture** (§4.1+§5+§5.1+§10.2+§10.3) | **REDESIGN** | Five sections mutually contradictory; blocks the MCU choice. **A concrete scheme that fits is proposed** |
| **2** | **Drone + flight plan** (§2+§8.2) | **REDESIGN** | Two sections cannot both be true. Already costed (Path B); the *decision* is still unmade |
| 3 | Velocity → spacing (§7.1→§8.2) | re-derive | Method sound, input wrong. **One hammer test** |
| 4 | Sensor choice (§3.2/§9) | re-derive | Gated on the ambient measurement. 41% of node cost |
| 5 | DSP band (§6) | **superseded** | Neither 0.5–4 Hz nor 10–100 Hz. ADR 0001: acquire 5–200 Hz, detection band is an **M1/M2 output** — so this is *not* a parameter edit |

**Not a redesign: §10.4 time sync.** Solved in the literature at <2 µs. But see the caveat in
`03-proposals.md` §5 — *de-risked is not integrated*, and the prior pass slightly overstated this.

---

## The proposed node architecture, in one table

The question §10.2 asks is *what gets transmitted*. The answer that fits the law, the link and the
battery:

| Scheme | Payload | Interval | Duty @SF10 | Legal (2.5%)? |
|---|---|---|---|---|
| **A** — MASTER §5.1 as written, raw stream | 15 B | 2/s | **179%** (SF12) / 7.6% (SF7) | ❌ **No** |
| **B** — event-driven, per-beat packet | 21 B | 1/s | 30.5% | ❌ No |
| **C** — **batched detection summary** | **24 B** | **1/60 s** | **0.509%** | ✅ **Yes, 5× under** |

**Scheme C, 11 nodes, occupies 5.59% of one channel.** Headroom for the whole array.

**Why batching is not a compromise:** TDoA needs the **beat arrival time** at each node, not a
waveform. LongShoT's 2 µs sync already gives 0.3–6 mm of position error. A 60 s window carries
~60 beats as delta-encoded timestamps. **Raw waveform streaming was never required for
localisation** — that is the assumption §5.1 should drop.

**And the power problem dissolves with it:**

| | Current | CR2032 (225 mAh) |
|---|---|---|
| MASTER §4.1 | 9 mA | 25 h |
| **Scheme C** | **1.07 mA** | **211 h = 8.8 days** |

**8.4× better**, and it clears the 72 h survival window on the cell §4.1 already specifies —
**72 h needs only 77 mAh.** The CR2032 objection was about *pulse current*, not capacity, and it
is real: at 40 mA an aged cell (30 Ω) droops to **1.8 V and browns out**. Fix is a supercapacitor
across the cell, or LiMnO₂ over Li-SOCl₂. → `03-proposals.md` §2

---

## Index

| Doc | Contents |
|---|---|
| **[01 — Literature](01-literature.md)** | 5 concepts × ≥20 referred sources, access status per link |
| **[02 — Vendor Register](02-vendor-register.md)** | 18 vendors, prices from payloads, India routes |
| **[03 — Proposals](03-proposals.md)** | The five items, each with the suggested change and its cost |
| **[04 — Verification Log](04-verification-log.md)** | A34–A48, D19–D24, E17–E19, and what I got wrong |

---

## Verification

| | |
|---|---|
| URLs three-state verified | **38** — 30 LIVE, 4 BOTWALL, **3 DEAD**, 1 unreachable |
| Arithmetic claims recomputed from raw inputs | **16 of 16 reproduce** |
| Audit passes per finding | **2** |
| **Errors this pass caught in my own work** | **3** → `04` E17, D19, D20 |

**Three caught errors, stated up front:**

- **E17** — my own link checker tagged a **404 as LIVE**. It special-cased 401/403/429 but not 404
  when the body was not HTML. Patched, then **re-ran**: two cap-xx PDFs are genuinely **DEAD** and
  are *not* cited. The supercapacitor claim rests on TI SLVAES7 and Avnet instead.
- **D19** — I nearly quoted **RAK3172 at $0.8906** from LCSC. That is the **1000+ tier**; qty-1 is
  **$2.3492** and **stock is 0**. Would have understated by 2.6×.
- **D20** — ADXL355 moved **$55.1592 → $53.3316** *within the same day's* ladder read. The 19-day
  drift finding understates how perishable these are.

---

*Related: [../BUDGET/](../BUDGET/) · [../MEMS/](../MEMS/) · nothing here is applied to
[../../MASTER.md](../../MASTER.md).*
