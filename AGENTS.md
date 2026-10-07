# AGENTS.md

Context for AI coding agents working in this repo. Read this before `docs/MASTER.md`.

**Project:** Heartbeat In The Rubble — drone-deployed seismic mesh for locating survivors in
collapsed structures. **Stage: pre-code.** No hardware acquired, no source code exists yet.

---

## 1. Read this first: the spec is superseded

`docs/MASTER.md` is the detailed spec. **Its core premise has been disproven and the document does
not say so.**

MASTER describes detecting a buried survivor's **heartbeat** with a MEMS accelerometer. A six-agent
adversarial review on 2026-10-07 established that this **cannot work**:

- The cardiac seismic signal is **47–69 dB below the chosen sensor's own noise floor** at 3 m.
- MASTER §3.3's central unmeasured assumption (0.1–1 mg at 2–3 m) is **wrong by 479–19,167×**.
- No filter, averaging scheme or ML model recovers this. Closing the gap would need 2.8 h–3.2 yr of
  phase-coherent integration, and the HRV feature needed to prove a signal is human **destroys the
  phase coherence averaging requires**.

**Do not design, plan or write code toward heartbeat detection.** It is settled, not open.

### What replaced it

Same hardware, different target. Retargeting to **tapping / voice from a responsive survivor**
clears the noise floor by **+23 to +41 dB**, and reuses the drone, LoRa mesh, TDoA solver, time sync
and dashboard almost unchanged.

Read in this order:

| File | Why |
|---|---|
| `docs/critique/README.md` | Index and bottom line |
| `docs/critique/07-verdict.md` | The verdict, findings register, rebuilt design |
| `docs/critique/08-amendment.md` | **Amends 07.** Read immediately after it |
| `docs/MASTER.md` | Spec. Numbers are mostly still good; the premise is not |

---

## 2. Precedence

Highest first:

1. **`docs/critique/07-verdict.md` + `08-amendment.md`** — current engineering position.
2. **`docs/decisions/`** — ADRs, binding where they exist. **Not in this repo** (kept local by the
   maintainer). If a decision seems to be missing, ask rather than assuming none exists.
3. **`docs/MASTER.md`** — consolidated numbers. Loses to the above; wins on raw figures.
4. `docs/research/` — working papers behind the numbers: `MEMS/` sensor selection, `BUDGET/` costing,
   `REDESIGN/` an earlier pass. `MEMS/extracts/` and `BUDGET/extracts/` hold the cited figures pulled
   out of source PDFs, since the PDFs themselves are not in the repo (see Conventions).
5. `docs/reference/` — the original hackathon-era doc. **Stale framing, kept for history only.**

Two things are gitignored and absent from your clone: **`docs/memory/`** (maintainer's project
memory) and **`docs/decisions/`**. The maintainer also has a local `CLAUDE.md` with
machine-specific setup that does not apply to you.

---

## 3. The one error that explains most others

**A repetition rate was mistaken for a signal bandwidth.**

60–120 bpm is how *often* a heartbeat repeats. The beat itself is a broadband impulse (~50–150 ms
rise). MASTER §6 bandpasses **0.5–4 Hz**, which matches the rate and **discards the signal**.

Consequences, all downstream of that single slip:

- Throws away ~48 % of impulse energy; keeps only 2 harmonics.
- **Destroys localization**, because timing precision scales as `σ_t ≈ 1/(B·√SNR)` — narrowing the
  filter makes TDoA *worse*. Correcting the band moves pick error from 8–27 m to 0.86–2.71 m.
- **Caused the wrong sensor choice.** §3.2 marks the ADXL355 **FIXED** and rejects the SM-24
  geophone because its 10 Hz corner sits "above the entire target band" — true only of the *wrong*
  band. The geophone's 48 dB noise-density advantage **is** the detection margin: every tap case is
  buried on the ADXL355 (−7 to −25 dB) and detected on the SM-24 (+23 to +41 dB).

**If you touch the signal chain: the band is 5–40 Hz, the sensor is the SM-24, and §3.2's "FIXED"
marker is wrong.**

---

## 4. Current design decisions

Locked (supersedes MASTER where they conflict):

| Parameter | Value |
|---|---|
| Sensor | **SM-24 geophone** (vendor-verify its 0.1 µg/√Hz before committing) |
| Band | **5–40 Hz** tap; 200 Hz–3 kHz voice |
| Target | Tap / movement / voice. **Cardiac is a stretch goal only** |
| Operating mode | **Command-triggered during "All Quiet"**, not autonomous continuous |
| Duty cycle | **~5–8 %**, set by the incident commander, not by the design |
| Runtime requirement | **≥138–163 h** of presence (not 72 h) |
| Primary discriminator | **Persistence across silences, ≥60 % of available looks** — not an LSTM |
| Output | **DETECTED / NO DETECTION / BLIND per cell**, 2–5 m. Never a pin, never a clearance |
| Localization | **±3.5–5 m**, bounded by node position, not by clock error |
| Impact design | **~200 G** (15 mm crush cannot give 15–20 G) |
| Cost model | **Quadratic in 1/r** — halving detection range quadruples node count |
| Dropped | ICA, depth-from-amplitude, ECG-trained LSTM — invalid as specified |

Known-wrong numbers in MASTER, already corrected in the critique: node mass (15.52 g, not 8 g),
node position (±2–5 m, not ±0.05 m), impact (200 G at 15 mm), LoRa ToA (0.370688 s, not 0.3052 s),
packet size (needs 82–156 B, not 24 B), power (receive current budgeted at zero),
**STM32WLE5JC SRAM is 64 kB, not 100 kB — the planned input buffer alone is 70.3 kB (110 %)**.

### Two things that are not solved

1. **False alarms.** At a realistic prior, 93 % accuracy yields **~16 % positive predictive value** —
   five of six detections false; ~907 false pins/day on empty rubble. The persistence rule above is
   the proposed fix (→ 70–98 % PPV) but is **unmeasured**. Never present detection as confirmation.
2. **Compliance and cost.** All-in capital is **$9,746, not $1,845**; the claimed 8× advantage over
   the $15,000 incumbent compresses to ~1.0–1.5×. As specified the build is **not legal in India**:
   DGFT prohibits importing a drone kit (buy components and assemble domestically) and the radio
   needs WPC type approval, budgeted at $0.

---

## 5. Conventions

- **Units and provenance matter.** This project has been burned repeatedly by unverified numbers.
  Label figures as measured, computed, or assumed, and say which. Don't assert a vendor price or
  stock status without a capture date — prices here drifted 8–16 % in 19 days.
- **Verify links by response body, not status code.** Vendor sites serve soft 404s (HTTP 200 with a
  "Page Not Found" body) and many block scripted access. Use `GET`, not `HEAD`.
- **State what you could be wrong about.** Every critique document ends with that section; match it.
- Markdown docs, LF endings (`.gitattributes` enforces it).
- **Don't commit PDFs.** `*.pdf` is gitignored globally — third-party datasheets and papers are not
  ours to redistribute. Add an `.md` extract with the source URL instead.
- Never commit secrets, env files, or build output.

---

## 6. Contributing

`main` is protected by a ruleset:

- **Pull request required**, 1 approving review.
- Stale approvals are dismissed when new commits land; review conversations must be resolved.
- **No force-push, no branch deletion, linear history required.**
- Signed commits are **not** required.
- Merge, squash and rebase are all allowed.
- The repository admin can bypass these; collaborators cannot.
- **GitHub forbids approving your own PR.** With a small team that means your PR needs the other
  party to review it — plan for that, don't assume you can self-merge.

So: branch, open a PR, get a review. Don't expect to push to `main`.

Issues are used to delegate work — check open issues before starting, and reference the issue in
your PR.

### If you are an agent

- **Ask before acting on a contradiction.** MASTER disagreeing with the critique is expected and
  resolved in §2 above. A disagreement *within* the critique set, or anything touching a locked
  decision in §4, is worth raising rather than resolving silently.
- **Don't re-derive the kill arithmetic to check it.** It was computed independently twice and
  cross-checked by six agents. If you think it's wrong, say so with your own numbers — but read
  `docs/critique/00b-verification-arithmetic.md` first, which already lists the assumptions most
  likely to be wrong.
- **The cheapest open experiment is in `08-amendment.md` §6.** Measure the ambient in-band floor
  first: if it exceeds ~1 mg, the premise fails at any sensor price, because no filter removes
  in-band noise.
