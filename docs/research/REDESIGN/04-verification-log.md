# 04 — Verification Log

Everything claimed in this folder, and how it was checked. **Audit passes per finding: 2.**
Continues the numbering from `../BUDGET/` (A33, D18, E16).

| Prefix | Meaning |
|---|---|
| **A** | Audited claim — verified, states the source |
| **D** | Discrepancy — two sources disagree, or a figure moved |
| **E** | Error — **mine**, caught and fixed |

---

## A — Audited claims

### A34 — The Table-II finding *(the load-bearing one; audited 3×, not 2)*

| Pass | Method | Result |
|---|---|---|
| 1 | WebSearch snippets | Table-II exists, 500 mW figure appears |
| 2 | **Downloaded the Gazette PDF**, checked `%PDF-` header, `markitdown` → `gazette/IN_GSR.md`, read the tables | ✅ Confirmed verbatim |
| 3 | Independent cross-check against ERC Rec 70-03 / ETSI EN 300 220-2 | ✅ Same category, same avalanche-victim wording |

Quoted from the converted PDF:

> *"Tracking, Tracing and Data Acquisition Devices also include devices for Emergency detection of
> buried victims and valuable items such as detecting avalanche victims…"*

Table-II: **500 mW e.r.p., duty cycle ≤10% for network access points / ≤2.5% otherwise, ≤200 kHz,
Adaptive Power Control required.**

**Source**: `thc.nic.in` hosted copy of the Gazette — ✅ **LIVE 200**, `%PDF-` verified.
(Primary `egazette.nic.in` is behind a session wall; the `thc.nic.in` copy is a court-hosted
mirror of the same instrument, G.S.R. 853(E), 10 Dec 2021.)

**Limit of this claim:** I am reading a statute. **The table assignment is my inference** from the
Gazette's own category note — it is not an opinion from counsel or a WPC ruling.
Flagged in `03` §1 and repeated here because it is the single most consequential claim in the folder.

### A35–A40 — Arithmetic, 16 of 16 reproduce

Every number recomputed from raw inputs by `final.py` (Semtech LoRa ToA formula, from `Ts=2^SF/BW`
upward — no calculator figures, no carried results).

| # | Claim | Recomputed |
|---|---|---|
| A35 | SF10, 24 B, BW125, CR4/5, 8-sym preamble, CRC on | **ToA 0.3052 s** |
| A36 | SF12, 15 B, same settings (LDRO on) | **ToA 0.8929 s** |
| A37 | §5.1 as written @SF12 | **179% duty** |
| A38 | §5.1 fallback @SF7 | **7.6% duty** — still 3× over Table-II |
| A39 | Scheme C: 0.3052 s / 60 s | **0.509%** |
| A40 | Scheme C × 11 nodes | **5.59% channel** |

| # | Claim | Recomputed |
|---|---|---|
| A41 | 25 mW → 500 mW | **+13.0 dB (20×)** |
| A42 | Range multiplier, n=2.0 / n=3.5 | **4.47× / 2.35×** |
| A43 | 2.5% ÷ 1% | **2.5× airtime** |
| A44 | Scheme C average current (4 lines summed) | **1.065 mA** |
| A45 | 225 mAh ÷ 1.065 mA | **211.2 h = 8.8 d** |
| A46 | vs MASTER 9 mA / 25 h | **8.4×** |
| A47 | 72 h × 1.065 mA | **77 mAh** |
| A48 | CR2032 droop @40 mA, 10 Ω / 30 Ω | **2.60 V / 1.80 V** |

Plus **A49** LCSC qty-1 ÷ 1000+ = **2.64×**, and **A50** Pixhawk delta $199.00 − $149.98 =
**$49.02**.

> **One figure superseded mid-pass.** An earlier `power.py` printed **1.473 mA** using a mislabeled
> ToA constant. `final.py`'s **1.065 mA** is the document-of-record figure and the only one quoted.
> Recorded because the wrong number existed in my working set before it was caught.

### A51 — Link verification: 38 URLs, three-state

| State | Count |
|---|---|
| ✅ LIVE | 30 |
| 🔒 BOTWALL | 4 |
| ❌ **DEAD** | **3** |
| ⚠️ UNREACHABLE | 1 |

Verified by `verify3.py`, which scopes its DEAD/BOTWALL regexes to **`<title>` + first `<h1>` only**
— never the whole body (the E11/E12 false-positive fix carried from the MEMS pass).

**The 1 unreachable**: `docdb.cept.org/.../Rec7003e.pdf` (URLError, not a 404). ERC Rec 70-03 is
instead confirmed via the **CEPT EFIS annex 5** route, which carries the same table.

**The 3 DEAD**: all `cap-xx.com/wp-content/uploads/datasheets/*` — see E17. **None is cited for a
claim anywhere in this folder.**

---

## D — Discrepancies

### D19 — LCSC price tier *(caught before it entered a document)*

A naive payload scrape of `C19189487` returns **$0.8906**. Writing `lcsc.py` to parse the **full
ladder plus the stock field** showed:

| Qty | Price |
|---|---|
| 1 | **$2.3492** |
| 200 | $0.9382 |
| 500 | $0.9075 |
| **1000** | **$0.8906** ← what the naive scrape returned |

**Stock: 0.**

Quoting $0.8906 would have **understated the line 2.64×** and asserted availability that does not
exist. **Same failure class as the 2026-09-17 ADXL355 stock claim.**
**Rule: parse the ladder *and* the stock field. Never the first price match.**

### D20 — Variant ladders mixed into one row

`../BUDGET/02` presented the ADXL355 ladder as `@1 $55.1592 / @10 $53.3316 / @30 $55.6146`.
**Those are two different parts:**

| Part | LCSC | Ladder |
|---|---|---|
| ADXL355BEZ | C468833 | @1 $55.1592 · @10 $53.3316 |
| ADXL355BEZ-RL7 | C515892 | @1 $59.7265 · @30 $57.1320 |

No individual number was wrong. **Presenting them as one part's ladder was.** It makes the @30 tier
look like a price *increase* at higher volume, which it is not — it is a different part.

**Not corrected in the BUDGET doc** — the goal is suggest-only. Logged here.

### D21 — Price moved within a single day

ADXL355 @1 read **$55.1592** in the budget pass and **$55.1592** again here (stable), but the @10
tier at **$53.3316** was not visible in the earlier read. The 19-day drift finding
(`bom-prices-are-perishable`) understates the volatility: **the ladder itself changes shape.**

### D22 — RAKwireless $5.99 vs LCSC $2.3492

Both ✅ LIVE, both correct. **RAKwireless wins on availability** (in stock vs 0) and on quantity
relevance. **LCSC only wins at 200+**, which this project will never order.
Not a discrepancy to resolve — a sourcing conclusion.

### D23 — Two valid supercapacitor part classes, order of magnitude apart in ESR

CAP-XX prismatic: **50–100 mΩ**, quote-only.
KEMET/Surge EDLC: **25–220 Ω**, orderable at $0.70–$2.

For a 40 mA, ~0.3 s pulse the KEMET part is adequate. **The engineering conclusion is robust to the
spread; the exact part is not chosen.** Flagged rather than resolved because every distributor
carrying them 403s to a script.

### D24 — `MEMS/04` A8 vs the patent literature

`MEMS/04` A8 called coupling-vs-self-righting **"the project's unsolved mechanical conflict."**
It is **solved prior art twice over** — US 5866827 / US 12650530 (gimballed inner housing) and
US 9645267 (rotationally-invariant calibration). Both ✅ LIVE on Google Patents.

**Overturning my own earlier conclusion**, not someone else's. The A8 wording should soften;
suggested, not applied (`03` §6b).

---

## E — My errors

### E17 — My link checker tagged a 404 as LIVE *(the worst one)*

`verify3.py` special-cased **401/403/429 → BOTWALL** in its `HTTPError` handler but had **no
404/410 branch**. A 404 whose body was not HTML fell through to the default **LIVE**.

Caught by eyeballing a literal `LIVE  404` line in the background output:

```
LIVE     404 https://www.cap-xx.com/wp-content/uploads/datasheets/AB1004-...pdf
```

**Patch:**

```python
        if c in (401,403,429):
            print("BOTWALL  %-3s %s"%(c,u)); continue
        if c in (404,410):                      # <-- E17 FIX
            print("DEAD     %-3s %s"%(c,u)); continue
```

**Then re-ran everything.** The memory rule is explicit — *"if one tag is wrong, re-check
everything verified the same way"* — so this was not a one-line patch and move on.
Result: **cap-xx's entire `/datasheets/` path is gone.** 3 URLs are genuinely DEAD.

**Consequence handled:** the supercapacitor pulse-buffering claim was **re-sourced** to
**TI SLVAES7 + Avnet**, both ✅ LIVE. **No claim in this folder rests on a dead link.**

**Why this one matters most:** it is a bug in the instrument, not in a reading. Every ✅ LIVE tag
produced before the patch was suspect until re-run — which is exactly the scenario
`verify-links-by-body-not-status-code` was written for.

### E18 — Hand-built vendor URL 404'd. Again.

The Evelta RAK3172 URL was **constructed by me from the site's URL pattern**, not found by search.
It 404'd. **Identical to `../BUDGET/` E14.**

**Second occurrence of the same error.** The rule is not new, it was not followed:
**search for the product page; never synthesise a vendor URL.**

### E19 — Foreground timeout, then a buffered-output trap

A 13-URL verify batch hit the **120 s foreground timeout** (known E16 pattern) → backgrounded.
Then the background output file **read as empty while still buffered**, which could easily have
been misread as "the batch returned nothing."

Re-running smaller chunks in the foreground produced the results; the full background output
appeared on completion and **agreed**. **An empty background output file means "not finished," not
"no results."**

---

## What is NOT verified in this folder

Stated plainly, because an unflagged gap is worse than a known one.

| Item | State | What would close it |
|---|---|---|
| **Supercapacitor prices** (7 vendors) | **[SEARCH] only** | A browser. DigiKey/Mouser/Newark all 403 |
| **Primary cell prices** (5 vendors) | **[SEARCH] only** | Same |
| **The Table-II table assignment** | My inference from the Gazette's category note | Counsel, or the WPC/ETA filing |
| **ERC Rec 70-03 primary PDF** | ⚠️ UNREACHABLE | Confirmed via CEPT EFIS annex instead |
| Scheme C's 24 B payload | **Designed, not implemented** | Firmware + a bench test |
| LightEQ on RAK3172 specifically | Paper reports Cortex-M4 / 100 kB; **not run on this part** | Port and measure |
| 1.07 mA power budget | **Datasheet arithmetic, not measured** | A bench measurement, §12 step 1 |
| SCA3300 price | **[UNVERIF]**, carried | DigiKey 403s |

> **The four load-bearing engineering numbers in `03` — 0.509%, 5.59%, 1.07 mA, 211 h — are all
> computed from datasheet figures and a published formula. None has been measured.** They are
> sound enough to decide an architecture on. They are **not** sound enough to skip §12 step 1.

---

## Tally

| | |
|---|---|
| Referred sources across 5 concepts | **115** (23 / 24 / 22 / 25 / 21) — all ≥20 |
| Vendors | **18** — ≥15 ✅ |
| URLs three-state verified | **38** |
| Arithmetic claims recomputed | **16 / 16 reproduce** |
| Audit passes per finding | **2** (A34: **3**) |
| **Errors caught in my own work** | **E17, E18, E19, D20, D24** — 5, of which **2 were repeats of documented rules** |

---

*Back to [README](README.md) · [01 — Literature](01-literature.md) ·
[02 — Vendor Register](02-vendor-register.md) · [03 — Proposals](03-proposals.md)*
