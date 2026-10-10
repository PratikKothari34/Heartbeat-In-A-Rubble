# Closed issue archive — #1 and #2

**Archived 2026-10-11, immediately before the issues were deleted from GitHub.**

Issues **#1** (*Frame the research proposal from the verified docs*, opened 2026-10-07) and **#2**
(*Anchor correction + three citations verified*, opened 2026-10-07) were closed 2026-10-10 as
superseded by PR #3 and then deleted, leaving `#4`/`#5`/`#6` as the live set.

Every **figure** they carried already lives in the critique and research docs. What did **not** live
anywhere else is recorded below: the three methodological lessons, and the record of which issue was
right when a later audit was wrong. Both are still load-bearing.

> Deleting the issues leaves dangling references. `#4` and `#5` each carry a comment saying *"do not
> work from #1's figures — its footstep anchor was withdrawn."* **That instruction still holds**;
> this file is where #1 went.

---

## 1. The anchor correction — the project's one correction that moved *against* the kill

#2 overturned a figure #1 had instructed the drafter to use.

| | Value | Status |
|---|---|---|
| Anchor frequency | ~~19 Hz~~ ~~17 Hz~~ **40 Hz** | verified, full text |
| Footstep amplitude @ 3 m | ~~36.5 µg~~ ~~32.7 µg~~ **76.9 µg** | recomputed |

**The 17 Hz peak and the −85.7 dB re 1 g cross-check are not in Ekimov & Sabatier, *JASA*
120(2):762.** Both were assembled from abstracts and search snippets; full text gives zero matches.
The paper was being conflated with its *Proc. SPIE* 6241 companion. What it actually says: the
low-frequency vibration maximum is **"near 40 Hz"** for a regular walking style, site transfer
function peaking over 20–90 Hz.

That is **+6.47 dB** on the 19 Hz figure, taking the cardiac deficit from 38–60 dB to roughly
**31–53 dB**. Nothing recovers 31 dB — the premise is still dead, and still a publishable negative
result.

**The frozen-margin policy, and why it exists.** The headline margins (cardiac 38–60 dB; tap
+23/+41 dB; ADXL355 −7/−25 dB) are **deliberately not restated**, though the corrected anchor would
improve each by ~6.5 dB. They also scale off a **tap force and tap spectrum with no source at all**
(50–300 N / 60–80 Hz, `[ASSERTED]`). Re-deriving from a corrected anchor and an unmeasured force
would manufacture precision that does not exist. Recorded at
`00b-verification-arithmetic.md:85-95`; **do not substitute the improved numbers** until the bench
measurement lands.

---

## 2. Three methodological lessons

These are the part of #1/#2 that existed nowhere else, and each one has already caught a real error.

**A verbatim-*looking* quote assembled from abstracts and snippets can be a quote of a paper that
does not contain it.** Two of three figures attributed to one DOI were not in it. **Treat any
READ-ABSTRACT citation as unverified, not weakly verified** — if you cannot see the sentence in the
paper, it does not go in a funded proposal.

**Holding a paper is not reading it; reading an abstract is not reading a paper.** Ten of the twelve
BUDGET papers were retrieved as corroboration with **no figure taken from them**. Do not pull a
number out of a `📄 HELD`-but-unread source — read it first, or cite it only for *what approach
exists*.

**Two-column PDFs interleave columns, so a verbatim quote can grep to nothing and still be in the
paper.** Flatten whitespace and re-search before concluding a figure is absent. This is exactly what
separated the real mis-citation (17 Hz, genuinely absent) from a mere conversion artifact ("near
40 Hz", present but split across the gutter).

Related extraction gotcha: **the PDF text layer drops the micro sign.**
`TDK_MPU-6050_datasheet.md` renders its noise density as `400 g/√Hz`; the unit is **µg/√Hz**. The
docs are right and the extract looks wrong — do not "correct" the docs.

---

## 3. #2 was more right than the audit that followed it

#2 told the drafter *"Do not use '17 Hz' or '32.7 µg'."* The later PR #3 audit then paired a 17 Hz
baseline with the repo's 19 Hz dB figure — corrected as **C7** in `09-pr3-citation-audit.md`
(`a1dcadc`): 17 → 40 Hz is **+7.43 dB**, 19 → 40 Hz is **+6.47 dB**.

**Worth keeping because it cuts the other way.** An instruction issued to a collaborator was sounder
than the review that later audited their work. PR #3 avoided the `−85.7 dB re 1 g` trap and
reproduced the frozen-margin policy without being told to.

---

## 4. Carried forward, still open

- **Krohn 1984**, DOI `10.1190/1.1441700` — SEG paywall, USD 42, no free copy located. The **only**
  load-bearing citation still abstract-only; the 100–500 Hz geophone coupling window rests entirely
  on it. Highest-value single retrieval if institutional access exists.
- **Tap force and tap spectrum** — still unmeasured. This is M2, and the detection band is now an
  output of it (ADR 0001).
- **Two citations verified first-hand** in #2 and still load-bearing: **Arosio et al. 2010** (*"the
  limited spatial extension of the sensor array"*, confirmed among the paper's own three
  limitations — the sentence the surviving novelty claim stands on; accuracy ≤2 m, rubble velocity
  200–600 m/s) and **Sabatier & Ekimov 2008** (*"did not exceed 3 × 10⁻⁶ m/s, even very close
  (3 meters) to the walker"*, an **upper bound**, which is how the project uses it).

---

## 5. Superseded by later work — do not revive

- **#1's 5–40 Hz band.** A *cardiac* band, never derived from a tap. See **ADR 0001** and
  `10-doc-sweep-action-report.md` §2.
- **#1's footstep anchor** (17 Hz / 32.7 µg). Withdrawn; see §1 above.
- **Path references in #2's third comment** — `research/BUDGET/papers/`,
  `research/MEMS/papers/`, `research/MEMS/datasheets/` no longer exist (`f73b73d`). The
  `extracts/*.md` conversions are the sources of record.
- **#2's extract counts** (18 MEMS extracts, 15 datasheets). Corrected in the 2026-10-11 sweep to
  **12 datasheets**, Epson ×3, ADI ×1.
