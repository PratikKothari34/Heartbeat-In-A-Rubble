# Submission checklist — what the faculty member must fill in

**For:** `Research_Proposal_Air_Deployed_Seismic_Mesh.docx`.
**All page limits are met** (see [Page limits](#page-limits-against-the-funder-template)).
**Technical content is verified and merged.** Every item below is information only the applicant
has: identity, employment history, teaching load and publication record. Nothing here is a
technical gap, and nothing here can be filled from the repository.

**Edit the `.docx`.** The `.md` beside it is a markitdown conversion for review; the Gantt chart is
cell shading and does not survive the conversion. Regenerate the `.md` after editing so the two
stay in step.

**Never open the `.docx` in Word to measure it.** Word re-saves on open even when asked for
read-only: it rewrites every zip part, drops the archive's 5 directory entries (24 entries -> 15)
and silently alters text. It has already corrupted this file once, inverting "nobody has to climb"
to "nobody must climb". Copy the file elsewhere and measure the copy.

**[`DETAILS-NEEDED.txt`](DETAILS-NEEDED.txt) is the version to hand to the faculty member** — same
17 placeholders, written as plain prose with a paste-back form. This checklist is the working copy.

---

## Page 1 — the cover sheet (5 fields)

| Line | Field | Notes |
|---|---|---|
| 3 | **Name** | Full name as it should appear on the award |
| 5 | **Department / School** | |
| 7 | **E-mail ID** | Institutional address, not a personal one — some schemes reject personal domains |
| 9 | **Address** | Office address |
| 11 | **Phone** | Home / Office / Fax boxes. Leave Fax blank rather than writing "N/A" if there is none |
| 30 | **Printed name + Date** | Signature block. Sign the printed copy; leave the date for the day of submission |

**Already correct on page 1 — do not change:** title, 12 months, `Rs. 1,82,818`, field of
research, nature of work, the human-participants wording (ethics filed month 1, approval before any
participant test, month 2 at the earliest) and the borrowed-drone line. The ethics wording matches
the Gantt and the M3 gate; editing one without the other reintroduces the defect that was just
fixed.

## Elsewhere in the document (10 placeholders)

| Line | Field | Notes |
|---|---|---|
| 24, 177 | **[lab / department]** lending the drone | Appears **twice** — both must name the same lab. The operator must be the drone's registered operator under the Drone Rules, 2021 |
| 124 | **Teaching load, administrative duties, planned conferences** | Suggested venues are already drafted (Near Surface Geophysics / EAGE, IEEE Sensors) — keep or replace |
| 124 | **[number] of students** | Same line as the teaching load now.  The budget funds no student stipend, so this is project work, not hired labour. Keep it consistent with that |

**Line 124 is the tightest fill-in in the document.** Measured in Word, it is the last line on
page 7 and ends 1.8 pt from the bottom margin, with Q3 at 0.94 of its one-page limit. All four
values — teaching load, administrative duties, conferences, student count — share that one line,
about 150 characters. A longer answer takes Q3 over its limit and needs text tightened elsewhere
to pay for it.
| 128 | **"Adapt to the faculty member's background"** | The paragraph after it argues the gap from prior art and needs no change; only the opening clause is yours |
| 151 | **Prior / current grants** | `[None. / or, for each award: ...]`. "None." is acceptable — write it explicitly. The funder **bolds** the requirement to answer in detail *for each* related award, so treat it as scored, not a formality. Currently the last line on page 8 |
| 155 | **Pending applications** + follow-on `[agency]`, `[period]`, `[amount]`, `[follow-on project title]` | **Four** sub-fields — the title was added in v19 because the template requires it. NDRF or a State Disaster Response Force is already suggested as the operational partner; if the target agency *is* NDRF the sentence names it twice and should collapse to one mention |
| 159–163 | **Five publications** | The most-missed section. Five slots, all empty |

## Before submitting

- **Re-quote the two unquoted prices.** The SM-24 at `Rs. 7,140` and the tap-force plate at
  `Rs. 6,000` are an estimate, not a quote. Prices on this project moved 8–16% in 19 days, and the
  Indian distributor listing that matched `Rs. 7,140` showed `Rs. 11,616` on 2026-10-11. SparkFun
  direct is USD 69.95, about `Rs. 7,815` landed. The `Rs. 19,588` contingency absorbs the ten-unit
  gap of about `Rs. 6,750`, so the total stands — but the basis is date-stamped and will go stale.
- **International freight is still unbudgeted** and is stated as such in the document. Leave that
  statement in; removing it overstates the budget's completeness.
- **The WPC ETA at `Rs. 1,50,000` is deliberately unfunded**, with a local-logging fallback if the
  institute has not committed the funding in writing by month 4. If the institute *will* commit,
  get it in writing and say so — that is the single biggest weakness a referee can press on.
- **Check the PDF export**, not just the `.docx`: 5 tables, 5 page breaks and one footnote (the
  ~6.5 dB anchor-correction note) must survive. The footnote is wired to `footnotes.xml` and is the
  only one in the document. The Gantt is cell shading: 44 shaded cells across 13 rows.

## Page limits against the funder template

**Every section is now within its limit.** Re-measured 2026-10-11 against the current file (12
pages, 4,782 words) by rendering a *copy* through Word and taking each section from its heading to
its last line of content plus one line. `Research proposal format.docx` in the repo root is the
authority on the limits, and is also the only way to tell the funder's own wording from ours.

| Section | Rendered | Template limit | |
|---|---|---|---|
| Abstract | 0.53 page | 1 page | OK |
| Q1 objectives / questions | 0.89 page | 1 page | OK |
| Q2 methods | 0.99 page | 1 page | OK — least headroom of any section |
| Q3 activities + timeframe | 0.94 page | 1 page | OK |
| Q4 new line of inquiry | 0.39 page | 1/2 page | OK |
| Q5 anticipated products | 0.29 page | 1/2 page | OK |
| PREV 1 grants received | 0.12 page | 1 page | OK (awaiting content) |
| PREV 2 pending applications | 0.10 page | 1/2 page | OK (awaiting content) |
| PREV 3 five scholarly products | 0.16 page | 1/2 page | OK (awaiting content) |

### How Q1 was brought inside one page

Q1 was 1.77 pages. Four changes, in order of how much each recovered:

- **Prior art moved to Q4.** The seven-row prior-art table left Q1 and its content was folded
  into Q4's prose, which is where the "new line of inquiry for this group" case already sat. All
  seven works, every citation and every distinguishing claim survive. Q4 went 0.25 -> 0.39 page.
- **Each numbered section starts at a page top.** Page breaks were added before Q1, Q2 and Q3,
  matching the two the document already used. Per-section limits are meant to be read this way,
  and it is what made the remaining measurements trustworthy.
- **Sentences stated twice were cut once.** Each was checked to be stated elsewhere before being
  removed: RQ1's point-accuracy clause (Q2 section E), RQ4's cadence rationale (Q2 section D),
  and the sensor-choice margin restated from RQ3.
- **Three layout constraints were relieved**, which is what actually fixed the last 2%:
  `<w:cantSplit/>` on the research-question rows, and widow/orphan control on the
  unmeasured-input paragraph (Q1) and on section G (Q2). Each was relocating a whole block to
  the next page, so trimming text near them changed nothing until they were lifted.

**If you add text, check Q2 first.** It has 0.01 page of headroom. Adding a sentence to any of
sections A-G pushes section G onto the next page and takes Q2 over. Q1 has 0.11 page spare and
Q3 has 0.06.

**The research-question table was not cut.** It carries RQ1-RQ4 with their hypotheses and is the
spine of the proposal.

**PREV 3 has room.** It is 0.16 page holding five empty `[Citation N]` slots. Five real citations
at two to three lines each land it near 0.32 page, inside the half-page limit.

**Not a defect:** the 12 pages include the template's verbatim question prompts, its budget sheet
and the two-page reference list. The template allots roughly 7 pages of narrative and says nothing
about references, so total length is not itself a problem.

## Restored to match the funder's blank form — do not re-cut

Diffing against `Research proposal format.docx` found four places where the proposal had departed
from the form. All four are fixed; they are listed so the edits are not reversed.

- **Previous Research question 1 prompt** had been truncated. The funder's required-field
  enumeration (project title, source of support, period of support, amount awarded, products,
  relation to the proposed project) and a sentence the form puts in **bold** — "If you have
  received awards related in any way to this proposal, you should answer this question in detail
  for each such award" — had both been cut. Restored verbatim. Cost: PREV 1 went 0.05 -> 0.12 page,
  against a 1-page limit, so no page-limit argument justified the truncation.
- **Previous Research question 2 prompt** had the same enumeration missing, and the answer never
  supplied the follow-on *project title* the form asks for. Prompt restored; the title is now a
  fill-in. PREV 2 went 0.06 -> 0.10 page against 1/2 page.
- **The Contingency label** had been rewritten from the form's "Contingency (for field work and
  research purposes only)" to "(field work and research purposes only, 12% of direct costs)".
  Rewriting a funder's own budget-category label is what a compliance check catches. Restored; the
  12% basis already appears in the budget justification prose, so nothing was lost.
- **The attached-sheet instruction** under PROPOSED BUDGET was deleted. There is no attached sheet
  — BUDGET JUSTIFICATION is an inline continuation — so the retained instruction described a
  structure the document does not have.

**Kept deliberately:** the NOTE reading "You may omit this question and the next if they are not
applicable." An earlier pass deleted it on the reasoning that both questions are answered; that
was wrong, because the likely answer to question 1 is "None." — exactly the not-applicable case the
NOTE authorises. The nine italic question prompts and their page allowances stay: they are the
form's questions and reviewers score answers against them. The typo "that may be bear on your
research" in the Q3 prompt is the funder's own — reproduce it, do not correct it.

## Open — not acted on

**The Gantt chart carries no text.** Its 12-month schedule is encoded purely as grey shading across
44 cells. A plain-text extract, a monochrome print or a screen reader shows an empty 13 x 12 grid,
so the section spends a large share of its one-page limit on a table that then conveys nothing.
Putting an `X` in each shaded cell would fix all three at once. It changes the table's appearance,
so it is left to the applicant's call.

## Deliberately left as they are

- **`38–60 dB` and `+23/+41 dB` are frozen.** The corrected anchor would improve both by about
  6.5 dB, and the footnote says so. They are not restated because they also scale off a tap force
  that has not been measured; they are recomputed once, from measured inputs, at M4.
- **The detection band is an output, not an input.** Acquisition is `5–200 Hz`; where one figure was
  unavoidable it is `20–80 Hz [assumed, pending measurement]`. Both `5–40 Hz` and `60–80 Hz` are
  withdrawn in the text, with reasons.
- **Krohn 1984 is marked abstract-only.** It stays marked until the full text is retrieved.
