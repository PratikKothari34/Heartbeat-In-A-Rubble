# Submission checklist — what the faculty member must fill in

**For:** `Research_Proposal_Air_Deployed_Seismic_Mesh.docx` (on `main` as of `977f284`).
**Technical content is verified and merged.** Every item below is information only the applicant
has: identity, employment history, teaching load and publication record. Nothing here is a
technical gap, and nothing here can be filled from the repository.

**Edit the `.docx`.** The `.md` beside it is a markitdown conversion for review; the Gantt chart is
cell shading and does not survive the conversion. Regenerate the `.md` after editing so the two
stay in step.

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

## Elsewhere in the document (11 fields)

| Line | Field | Notes |
|---|---|---|
| 24, 197 | **[lab / department]** lending the drone | Appears **twice** — both must name the same lab. The operator must be the drone's registered operator under the Drone Rules, 2021 |
| 140 | **Teaching load, administrative duties, planned conferences** | Suggested venues are already drafted (Near Surface Geophysics / EAGE, IEEE Sensors) — keep or replace |
| 142 | **[number] of students** | The budget funds no student stipend, so this is project work, not hired labour. Keep it consistent with that |
| 146 | **"Adapt to the faculty member's background"** | The paragraph after it argues the gap from prior art and needs no change; only the opening clause is yours |
| 169 | **Prior / current grants** | `[None / or list: title, source, period, amount, products, relation to this proposal]`. "None" is an acceptable answer — write it explicitly rather than leaving the bracket |
| 173 | **Pending applications** + follow-on `[agency]`, `[period]`, `[amount]` | Three sub-fields. NDRF or a State Disaster Response Force is already suggested as the operational partner |
| 177–181 | **Five publications** | The most-missed section. Five slots, all empty |

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
- **Check the PDF export**, not just the `.docx`: 6 tables, 2 page breaks and one footnote (the
  ~6.5 dB anchor-correction note) must survive. The footnote is wired to `footnotes.xml` and is the
  only one in the document.

## Deliberately left as they are

- **`38–60 dB` and `+23/+41 dB` are frozen.** The corrected anchor would improve both by about
  6.5 dB, and the footnote says so. They are not restated because they also scale off a tap force
  that has not been measured; they are recomputed once, from measured inputs, at M4.
- **The detection band is an output, not an input.** Acquisition is `5–200 Hz`; where one figure was
  unavoidable it is `20–80 Hz [assumed, pending measurement]`. Both `5–40 Hz` and `60–80 Hz` are
  withdrawn in the text, with reasons.
- **Krohn 1984 is marked abstract-only.** It stays marked until the full text is retrieved.
