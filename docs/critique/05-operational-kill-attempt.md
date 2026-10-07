# 05 — Operational Kill Attempt

**Reviewer stance:** hostile. USAR operational experience + systems engineering. Target is the
**concept of operations**, which `MASTER.md` barely addresses — it has a signal chain and a BOM and
no CONOPS at all.

Date **2026-10-07**. Companion to `00-my-own-arithmetic.md` (whose findings 1, 3, 4 and 7 I treat as
inputs, not as claims to re-derive). Nothing here is applied to `MASTER.md`.

**Evidence labels used throughout:** **[DOC]** documented in a cited source · **[INF]** inferred by me
from a cited fact · **[ASR]** asserted by me or by the spec with nothing behind it ·
**[UNVERIF-SESSION]** well-established knowledge I could not re-verify this session — treat as a lead,
not a citation.

---

## VERDICT UP FRONT

**Would this ever be used in a real disaster, as specified? No.** Not because the physics is
impossible — the physics is *unmeasured*, which is a different problem — but because **the CONOPS
does not exist, and when you write it down the system's central claimed advantage disappears.**

Three independent blocks, any one of which is sufficient:

1. **The advantage is continuous 72 h passive monitoring. The site is not continuously quiet.**
   USAR sites run cranes, jackhammers, generators and dozens of personnel, and sensitive listening
   happens inside a commanded **site-wide All Quiet** — machinery off, everyone still, **"around
   once per hour for a few minutes"** per UK national operational guidance **[DOC]**. If the node
   only has usable SNR during that window, "continuous" is marketing and the system is **operating
   in the incumbent's own duty cycle, on the incumbent's own schedule** — with none of the
   incumbent's advantages. §1's gap claim collapses, and §4.1/§10.2 were optimizing the wrong
   schedule.
2. **The output is not the output the spec promises, and the spec's own promise is the wrong
   requirement.** `00` finding #3 fixes node position at ±2–5 m; `00` finding #4 fixes the arrival-time
   pick at metres. So the best honest output is **"a survivor is somewhere in this area,"** not a pin.
   Meanwhile USAR does not dig to a coordinate — it breaches along paths a structures specialist
   approves. The whole §7/§10.4/§10.5 effort buys precision nobody consumes.
3. **No incident commander will accept it, and that is a credentialing fact, not an opinion.**
   Uncertified sensor, no validation data, no environmental spec at all, non-credentialed operator,
   and a drone in disaster airspace. INSARAG classification and DGCA zoning are both gates this
   does not pass. **[DOC]** on the existence of the gates, **[INF]** on the refusal.

**What it actually is:** a **research platform** that could, if §10.1 returns a usable detection
range, become a **triage and prioritization aid** — a cheap way to rank which 10 m × 10 m cells of a
large pile deserve the next breach, from **20+ simultaneous points that stay in place across dozens
of hourly All Quiets.** Its defensible edge is **coverage and persistence**, not accuracy and not
cost. That is a real and useful product. It is not a survivor-locating instrument, and nothing in
`MASTER.md` is written for it.

**"Bulletproof" has to be redefined.** For a research platform, bulletproof means *the measurement
is honest and the limits are published*. It does not mean *ready for a rubble pile*. Every claim in
the spec written in the register of a deployable rescue tool is a liability the project does not need
and cannot currently defend.

---

## THE SINGLE OPERATIONAL FACT THAT MOST CHANGES THE DESIGN

> **Sensitive listening on a collapse site happens inside a deliberately imposed site-wide silence —
> cranes stopped, jackhammers stopped, personnel still. UK national operational guidance puts it at
> "around once per hour for a few minutes." That is the only window in which a 0.1–1 mg signal is
> physically available: roughly a 5 % operational duty cycle, on a schedule the system does not
> control.**

**[DOC], and this is doctrine, not just journalism.** **UK NFCC National Operational Guidance**,
*Primary search: Unstable or collapsed structure*, states the procedure as a rule:

> *"Around once per hour for a few minutes, all activity should cease to listen for sounds made by
> casualties"* — and notes that **sound detection devices** are used during this phase (Stage 4,
> exploration of voids and spaces) *"to listen for movement or noise from within the debris."*

**[DOC]** Corroborated independently by **FEMA US&R signalling**, where **"All Quiet / Cease
Operations" is a defined site-wide emergency signal (1 long blast)** — i.e. the silence is not an
informal pause, it is a **commanded state of the whole worksite** with its own signal in the same
table as evacuation. **[UNVERIF-SESSION]** on the exact table (the Kansas Fire Marshal PDF would not
parse this session; the signal itself appeared in search-result body text).

**[DOC]** Corroborated again by practitioner literature and by reporting from two separate events a
continent and three years apart. Fire Engineering's technical-search article: listening devices
*"are best used in an environment where there is minimal noise,"* and *"search teams will often stop
for several minutes to try to hear any calls, scratches or taps."* AP from Adana, Turkey, Feb 2023:
*"They lifted slabs of cement with enormous cranes and smashed rubble with jackhammers. Then, they
stopped. Silence. Key to detecting the faintest noise, which could be the sign of a survivor buried
beneath rubble."* AP from Colombia, Aug 2026, M7.4: rescuers *"signal for engines to be shut off,
cranes to stop and drills to be silenced,"* and the noise *"gradually fades as the rescuers climb
the rubble."*

**Four independent source classes — national doctrine, a federal signalling standard, trade
practitioner literature, and event reporting — agree. This is the best-evidenced fact in this
document, and it is the one the spec does not contain.**

**The number that matters: ~5 minutes in 60, called by command.** That is a **~8 % duty cycle at
best**, and the system has no say in when it happens.

### Why this is the most expensive fact in the document

It does not attack any number. It attacks **the shape of the system.**

| Spec commitment | What the silence fact does to it |
|---|---|
| §1 *"reads that wave through concrete whether or not the survivor is conscious"* — framed as continuous | Survives as physics. **Dies as an operational advantage**: the usable window is the silence, which is minutes, not 72 h. |
| §2/§4 node *"capture ground vibration continuously"* | Pointless. 99 %+ of continuous capture is during machinery operation, when the band is saturated (§3.1 lists machinery at *high* amplitude vs a 0.1–1 mg target — `00` would call that a −40 dB SNR problem, **[INF]**). |
| §4.1 power budget, 25 h, and the entire redesign agony over duty cycle | **Optimized for a scenario that never happens.** At ~5 min/hour **[DOC]**, a 7-day deployment needs **~14 hours of actual sensing spread over 168 hours** — and most of those windows are at night or after the crew has moved to another sector, so call it **6–14 h of useful sensing**. §4.1's 25 h of *continuous* draw is roughly the right energy for the *wrong schedule*. |
| §10.2 radio budget crisis (4800 bps vs a 1 % duty cycle) | **Largely dissolves.** Nothing needs to stream during machinery operation. Burst during silence, sleep otherwise. |
| §9 Delsar cost argument | Weakens badly. If both systems only work during silences, you are not replacing Delsar's *mode*, only its *price* — and `00` finding #7 shows the price advantage is quadratic in an unmeasured number. |

**The design the silence fact implies is a different system:** command-triggered, not autonomous.
A node that sleeps deeply, wakes on a broadcast "silence starting now" command from the gateway,
samples hard for ~180 s, reports, and sleeps again. Power stops being the binding constraint. Radio
stops being the binding constraint. **The two problems the project has spent the most effort on are
artifacts of a CONOPS nobody wrote.** That is the finding.

**And there is a free bonus the spec cannot currently claim.** The All Quiet is a **commanded,
signalled, site-wide state** **[DOC]** — which means the system has access to a **ground-truth
trigger it does not have to infer.** It does not need to detect quiet; it can be *told*. That is a
one-wire integration with the incident command structure (a button on the gateway, pressed by the
safety officer who blows the whistle anyway) and it replaces an entire adaptive-threshold problem
§11 currently hand-waves. **The cheapest sensor-fusion input available to this project is the
incident commander.**

> **There is also a second free gift, and it is the one that could save the detection problem.**
> Because the All Quiet recurs **~hourly** **[DOC]**, the system gets **repeated, independent looks
> at the same cell under the same quiet conditions** — perhaps 20–100 of them over a multi-day
> deployment. A detector that is only marginally better than chance in one window becomes
> **genuinely useful across 50 windows**, because a real survivor is **persistently present in the
> same cell** while noise is not. **Persistence across silence periods is a discriminator worth more
> than the LSTM**, it is immune to the HRV-vs-coherence conflict in `00` #6 (you are correlating
> *detections*, not waveform phase), and it is the one advantage a left-in-place node has that a
> hand-carried Delsar sensor structurally cannot have. **The spec does not mention it. It should be
> the headline.**

### The counter-argument, stated fairly

Continuous monitoring is not worthless even so. **[INF], and I think it is the project's strongest
remaining card:** a node that has been sitting in place for 6 hours has 6 hours of **noise
characterization** that a hand-placed Delsar sensor, planted 60 seconds ago, does not. It knows the
local machinery spectrum, the local baseline, and — critically — it can tell you *this cell got
quiet and something periodic is still there.* Continuous presence buys **a noise reference and
change detection**, not continuous detection. That is a defensible claim. It is not the claim §1
makes.

---

## ATTACK 1 — The ambient noise problem is operational, not a filter problem

§3.1 lists machinery at 20–200 Hz and dismisses it with a high-cut. §11 lists *"machinery running
nearby"* with the mitigation *"adaptive threshold + notch filter at machine frequency."* Both are
category errors.

**(a) Machinery does not politely occupy 20–200 Hz.** **[INF]** A jackhammer, an excavator track, a
concrete saw and a diesel generator are broadband impulsive sources. Their energy appears in the
0.5–4 Hz band as: engine idle sub-harmonics; the duty rhythm of a hydraulic breaker (impulses at
roughly 1–3 Hz — *in band, and periodic*); track slew and boom slew (sub-Hz); and, worst, the
**envelope** of everything above, which modulates at exactly the rate the spec's detector looks for.
A notch filter at "machine frequency" presumes a line spectrum. These are not line spectra.

**(b) The project's own human/machine discriminator is weakest exactly here.** §6 separates human
from machine on **HRV** (±5–10 % beat-to-beat) and on **amplitude** (>10 mg machine vs 0.1–1 mg
human). A hydraulic breaker operated by a human is **not** at zero variance — an operator's trigger
rhythm has far *more* than 10 % variability. **[ASR]** but I would defend it: the single most
HRV-like signal on a collapse site is a person operating an intermittent tool. The spec's
discriminator is pointed at the wrong adversary. And `00` finding #6 already showed HRV-based ID and
coherent averaging are mutually exclusive, so the project cannot even use averaging to dig out from
under it.

**(c) Footsteps are listed as in-band and rejected on amplitude at 5–50 mg.** §3.1. That is a 1.5–2.7
decade amplitude margin, which sounds safe until you ask about a rescuer **standing still 3 m away**
— see FMEA row F-14. Amplitude rejection is a range-dependent rejection, and the spec treats it as
absolute.

**(d) The operational conclusion.** Everything in §6 that is framed as a filtering problem is really
a **scheduling** problem with a filtering residue. The correct architecture is: *do not try to detect
through machinery noise; detect during the silence the site already provides, and use the machinery
periods to learn the noise.* The spec has this exactly inverted.

**(e) The claimed advantage over the incumbent, re-scored honestly.** The reference doc's comparison
table (§1 of `reference/`) gives "Seismic Mesh (Ours)" a ✓ under **"Works in Noise"** with the
parenthetical *"ML filtered."* Against the acoustic sensor's ✗.

> **That ✓ is the single least defensible mark in the reference document.** It is the one cell where
> the project claims to beat the incumbent at the incumbent's hardest problem, on the strength of an
> untrained model, with no measurement, in a band where the noise is both in-band and periodic.
> It should be a ✗, or at best "✓ with site silence" — which is what the incumbent's cell already
> means.

---

## ATTACK 2 — Does TDoA help operationally? Mostly no, and the priorities are inverted

### (a) Rescuers do not dig to a coordinate

**[DOC]/[INF].** Fire Engineering on technical search: *"Communicating which areas have been covered
and those that have not been reached is a very important part of the collapse rescue plan"* — the
output consumed by the operation is **coverage and area status**, not coordinates. Extrication path
selection is a structural-stability decision: you breach through a slab you can shore, you tunnel
along a void you can follow, you do not cut a vertical shaft to a GPS point because a laptop said so.
**[ASR]** on the specifics of path selection — I could not pull an INSARAG Manual C passage this
session; label it a lead. But the direction is not seriously contestable, and the consequence is:

> **A 0.3 m pin and a 5 m × 5 m area produce the same dig plan**, because the dig plan is chosen
> from the structure's geometry, not from the target's coordinates. Sub-metre precision changes
> nothing a rescuer does.

Where precision *would* pay is the last 1–2 m: confirming you are about to breach into the right
void rather than the one next door. **[INF]** And at that range the operation already has better
instruments — a search cam pushed through a bore hole, with *"an audio sensor that enables the camera
operator to speak with a victim entombed in a void"* **[DOC]**. The system cannot win the endgame.

### (b) What precision do operators actually use? Not trilateration

This is the finding that embarrasses §7 most, and it is documented.

**[DOC]** Fire Engineering, on listening-device operation: *"Being able to compare several sensors and
to switch from one to another allows the operator to quickly identify the sensor with the largest
and/or clearest signal."* And: *"If a signal is detected, it is generally advised that the sensor
emitting the signal be left in position and that the sensors surrounding it be repositioned for more
accurate determination of the location."* Firehouse, independently: *"leave the sensor that has the
greatest noise in place and move the remaining sensors in an attempt to 'close in' on the victim."*

> **The incumbent's localization algorithm is: pick the loudest sensor, then move the other sensors
> closer and repeat.** It is a hill-climb on amplitude with a human in the loop. There is no TDoA, no
> hyperbolas, no velocity model, no time sync. The practitioner literature uses the word
> "triangulate" loosely — Fire Engineering says *"the objective is to triangulate the exact
> location"* in the same article that describes amplitude comparison, so **"triangulate" here is
> tradecraft vocabulary for "close in from several directions," not a geometric solve.** **[INF]**,
> but the two procedural quotes are unambiguous about the actual method.

Three consequences, each expensive:

1. **The spec built the wrong solver.** §7's TDoA, §10.4's sync, §10.5's velocity model all exist to
   produce a number the user's own tradecraft does not use.
2. **It also built the wrong deployment.** Hill-climbing requires **movable** sensors. Dropped nodes
   are **fixed**. The project has deliberately removed the one degree of freedom the incumbent
   procedure depends on. This is not a minor loss — it means a single drop pass gives you one fixed
   lattice and no refinement path, where the Delsar operator iterates to convergence. **[INF], and
   I rate this a top-three finding in this document.**
3. **The fixed lattice has an answer, and the project should adopt it:** fixed sensors *can* do
   amplitude-ratio localization (relative RSSI-style, across nodes, on the seismic amplitude) without
   any timing at all. Lower precision, far cheaper, and — crucially — it works in the spec's own
   narrow band, where `00` finding #4 says timing never will. **This is the localization method the
   system should have specified.**

### (c) Is 2 m sufficient? Yes — which is the project's good news and its bad news

`00` finding #3 caps the system at ~2 m by node-position uncertainty alone. §7.2's ±0.05 m row is
unreachable. Operationally, **2 m is fine** — it identifies a cell, which is all triage needs.

> **So the honest position is: the achievable accuracy is operationally sufficient, and the project
> spent its effort on the accuracy it could neither achieve nor use.**

| Spec effort | Operational value | Verdict |
|---|---|---|
| §10.4 time sync (declared "largely answered," 2 µs, a GPS line item) | Zero at the achievable position floor | **Cut.** `00` #4 already showed it is 10⁴ below the binding term. |
| §10.5 velocity model (promoted to "binding unknown") | Near-zero for area output | **Defer.** Binding only on a solve nobody consumes. |
| §7 hyperbolic TDoA solver | Near-zero | **Replace** with amplitude-ratio area localization. |
| §10.1 detection range | **Everything.** Sets r, sets node count, sets cost as 1/r² (`00` #7), sets whether there is a product at all | **Under-resourced by a factor I would put at 10×.** It is one bench test and it is listed as step 1 of 7, co-equal with "dashboard." |

**§10.1 is not the first of seven tasks. It is the gate on whether the other six exist.**

---

## ATTACK 3 — False positives are operationally catastrophic; the value proposition is triage

### What a false positive costs

**[INF]**, and this is the cost structure the spec never writes down. A pin on a map that a crew acts
on consumes: hours of shoring and breaching; **exposure of rescuers to secondary collapse**, which is
the single largest life-safety risk in the operation; heavy-equipment time that is the scarcest
resource on site; and **a silence period**, which is the scarcest resource of all because the whole
site stops for it. A false pin does not waste a little time. It spends the site's rationed attention
and puts people under an unstable slab for nothing.

### What false-positive rate is acceptable?

The spec's §6 threshold is **>0.75 sigmoid, "tuned for low false-negative rate."** That is the wrong
direction for an unvalidated instrument, and it is tuned on an axis the spec has no data to tune on.

**[ASR], my own number, offered as a requirement to argue with:** for an instrument whose output
triggers a dig, the acceptable false-positive rate is **well under 1 per site-deployment** — call it
<1 % per cell per silence period across a 20-cell pile. For an instrument whose output only *ranks*
cells for further investigation, **20–30 % is tolerable**, because the next step is cheap and
non-destructive. **Those two numbers are three orders of magnitude apart in detector difficulty, and
they correspond to two different products.** The spec has not chosen which product it is, and §6's
threshold tuning silently chose the harder one.

### How USAR actually confirms a hit — multi-modal, always

**[DOC]** on the components: search cameras that *"locate a victim within a void, assess the
victim's condition"* with two-way audio; direct victim communication, *"perhaps with a bull horn.
Ask the victim to tap an object 3 times and listen"*; canine search alongside technical search
(the reference doc's own table lists Search Dogs). **[UNVERIF-SESSION]** on the formal rule, which I
believe is standard INSARAG/FEMA practice: **a single-modality alert is a lead, not a confirmation —
two independent indications (e.g. two canine alerts from separate handlers, or canine plus
technical) are required before committing to an extrication.** I could not pull the governing
passage this session. Flag it; it is checkable in INSARAG Guidelines Vol. II Manual B/C.

> **If a single-modality alert from a *certified, validated* instrument is already only a lead, then
> an alert from an *uncertified, unvalidated* instrument is at most a lead to a lead.**

### The reframe

This is not a demotion. It is the first honest statement of what the system sells.

| | Claimed value proposition | Defensible value proposition |
|---|---|---|
| Output | A pin: survivor at (x, y, z) ±0.1 m | A ranked list of cells with a confidence and a noise quality flag |
| Consumed by | A drill operator | **The search planner deciding where the next silence and the next Delsar setup go** |
| Confirmation | Implied none — it is "the answer" | Mandatory. Canine, search cam, or hailing, before anything is cut |
| Dominant failure | Missing a survivor | **Sending a crew to the wrong cell** — so tune for specificity, not sensitivity |
| Beats the incumbent at | Accuracy, cost, autonomy | **Area throughput per silence period.** 20 simultaneous points vs 6 hand-placed ones |

**That last cell is the whole product.** §1's real problem statement should not be "thermal can't see
through concrete" — it should be **"a 5000 m² pile gets a handful of silence periods and a 6-sensor
instrument, and nobody can afford to listen to all of it."** Cheap disposable nodes are a genuine
answer to *that*. **[INF]** The spec is selling the wrong advantage, and the right one is better.

---

## ATTACK 4 — Timeline reality

### (a) Arrival, and where a hobby-grade system fits

**[DOC]** Macintyre, Barbera & Smith, *"Surviving collapsed structure entrapment after earthquakes:
a 'time-to-rescue' analysis,"* **Prehosp Disaster Med 2006;21(1):4–17, PMID 16602260**: survivors are
recovered well beyond 48 h; *"the average maximum times reported from 18 earthquakes was 6.8 days
(median = 5.75 days),"* longest reliable survival **14 days**; the 1999 Marmara, Turkey event gave 43
distinct reported rescues ranging **0.5 days (12 h) to 6.2 days (146 h)**.

**Two things fall out, and the second is the one nobody has said.**

1. **The 72 h framing in §1 and the reference doc is wrong in the direction that hurts the project.**
   The reference doc's §10 "key stat" is *"Survival probability drop ~50 % after 72 hours — FEMA /
   USAR research consensus."* Macintyre's data shows rescues clustering across days 0–6 with a tail to
   14. **The operational window is longer than the spec assumes**, which is good for the mission and
   **very bad for the node**, because:
2. **Node runtime must cover days, not hours.** §4.1's **25 h** does not reach the *median* maximum
   time-to-rescue (5.75 d). The 211 h redesign figure (~8.8 d) does. **[INF]** So runtime is a real
   requirement with a real number behind it at last — **≥144 h to cover the median, ≥168 h to be
   defensible** — and the silence-period CONOPS (Attack 1) is what makes that achievable, because
   ~50 min of actual sensing over 7 days is a trivial energy budget. The two findings resolve each
   other.

**Where does the system fit in the arrival timeline?** **[INF]** Local response is immediate and
untrained; organized national response (NDRF in India) in hours; international INSARAG teams
typically 24–72 h in, by which time the pile has been worked over. The window where a cheap
wide-area triage aid has the most value is therefore **hours 2–24**, with local/national responders
— exactly the window in which nobody has read your manual, nobody has your spare batteries, and
nobody will pause to let a student fly a drone. This is a distribution and training problem the spec
does not acknowledge exists.

### (b) Time to first actionable result — the comparison the spec never makes

**[ASR]**, my estimate, built to be argued with. The §8.2/§9 claim is "~5 min for 9 nodes."

| Step | Honest time | Note |
|---|---|---|
| Unpack, assemble F450, bind radio | 10–20 min | Path B is a *kit* airframe (§8.6), not a folding DJI |
| Boot ground station, bring up Pi + GPS 1PPS lock | 5–15 min | Cold GPS lock in an urban canyon is the long tail |
| Get flight authorization on site | **10 min – never** | Attack 5 |
| Pre-flight, GPS lock on airframe, arm | 5–10 min | §8.2's optical-flow fallback is a *hover* aid, not a nav solution |
| Fly snake grid, drop 9 nodes | **5 min** | The only number the spec costs |
| Nodes wake, settle, mesh forms, routes converge | 2–10 min | Attack 8 says this may be ∞ |
| **Wait for an All Quiet to be called** | **0–60 min, mean ~30 min** | **Not under the operator's control**, but **bounded** — ~hourly **[DOC]**. The dominant term, and the one the spec does not know exists. |
| Capture 180 s, uplink, classify, solve, render | 5–10 min | |
| **Total to first actionable output** | **1–2 hours** | And that assumes authorization is instant |

**Against the incumbent:** *"the Delsar device can be quickly deployed on the rubble pile to convert
the entire collapsed structure into a large sensitive microphone"* **[DOC]**, with a trained operator
planting a sensor in about a minute and listening immediately. **[INF]**

> **The spec compares 5 minutes of flight to 45–60 minutes of manual placement (§8.1) and declares a
> 10× win. The honest comparison is 1–2 hours to first result against a sensor that is listening 60
> seconds after it leaves the bag.** §8.1's win is an artifact of timing only the single step the
> project finds interesting.

And the deeper point: **both systems are gated by the silence period anyway**, so the throughput
comparison is *per silence*, not per minute. 20 nodes already in place beat 6 sensors being
hand-carried. **That is the real win and it survives this entire critique** — but only once the nodes
are already down, which makes pre-positioning and persistence the valuable properties, not deploy
speed.

### (c) Node runtime vs the operational window

Covered in (a). Summary: **25 h fails the requirement. The requirement is ~144–168 h. The
command-triggered CONOPS makes it easy.** This is the one place where a spec number and an
operational fact meet and produce a clean, actionable redesign.

### (d) Environmental envelope — the absence is itself the finding

**`MASTER.md` contains no environmental specification. Not a weak one. None.** No temperature range,
no IP rating, no humidity, no rain, no dust, no wind limit, no night provision, no fire/heat limit, no
aftershock response, no submersion. For a device whose entire purpose is to be **thrown onto an
earthquake-damaged building and left there for days**, this is the largest single omission in the
document — larger than any individual wrong number, because wrong numbers can be corrected and a
missing requirements section means the design was never constrained.

What the envelope has to contain, and what each item breaks:

| Condition | Consequence | Status in spec |
|---|---|---|
| **Rain / wet rubble** | A PLA-print-plus-EVA-foam enclosure (§9) is **not sealed**. Water ingress kills the node. Separately: **868 MHz is attenuated by water** — the reference doc's §4 claim that sub-GHz *"passes through concrete, soil, water"* is backwards for water. Wet rubble cuts the already-unmeasured 200–500 m NLOS range by an unknown factor. **[INF]** And §11's "waterlogged debris" mitigation is *"recalibrate velocity to ~1500 m/s"* — it treats flooding as a **solver parameter** when it is an **enclosure and link-budget** failure. | **Absent** |
| **Dust / concrete fines** | Pulverized concrete is the defining medium of a collapse. Coats the node, fouls any vent, changes the ground coupling the sensor depends on. | **Absent** |
| **Night** | Fine for the sensor. **Not fine for the drone** — §8.2 relies on bottom-facing optical flow, which needs texture and light. Night operations are standard in USAR; rescue does not stop at sunset. | **Absent** |
| **Fire / heat** | §8.1 explicitly claims the drone *"reaches fire zones people cannot enter."* PLA softens around 60 °C, a CR2032 is not rated for a fire ground, and §8.2 hand-waves *"fire updrafts"* as a PID problem. **The spec claims a capability it has specified nothing to survive.** | **Claimed, not specified** |
| **Aftershock** | Saturates the sensor (§3.1 lists 10–1000 mg against a 0.1–1 mg target), buries or displaces nodes, voids the position solution, and **evacuates the pile** — which also ends the silence period. | **Listed as a filter band only** |
| **Wind** | Gates the drone. A kit F450 in gusts near standing damaged structures is the limiting factor on whether deployment happens at all. | **Absent** |
| **Temperature** | CR2032 capacity collapses in cold; the 225 mAh figure is a room-temperature number. A night-time Himalayan or Turkish-winter deployment is a different battery problem. **[UNVERIF-SESSION]** on magnitudes. | **Absent** |

> **Write the environmental spec before the next hardware decision.** Not because it is good practice
> — because at least two current design choices (PLA+foam enclosure, optical-flow night navigation)
> are already known-wrong against conditions the spec has not yet admitted are in scope, and every
> further hardware choice made without it inherits the error.

---

## ATTACK 5 — Who operates it, and does the org chart allow it?

### The gates that exist

**[DOC]** **INSARAG External Classification (IEC).** *"The primary intention of the INSARAG External
Classification (IEC) system is to provide a better understanding of the individual abilities of USAR
teams making themselves available for international assistance,"* with Light / Medium / Heavy levels
and **checklists applied by classifiers** to ensure objectivity. Equipment and capability are audited
against INSARAG Guidelines **Volume II, Manual C**. I could not extract the technical-search equipment
line items this session — **[UNVERIF-SESSION]**, and worth the user hand-retrieving, because the
precise question is: *does Manual C name device categories, or named models?* If categories, there is
a legitimate path in. If models, there is not.

**[DOC]** **DGCA / India airspace.** Airspace is partitioned into **Red Zone (flying not permitted),
Yellow Zone (controlled, permission required), Green Zone (automatic)**, with restrictions around
airports, international borders, coastline, state secretariat complexes and military installations.
Operators file through the **Digital Sky** platform; a UAOP application is **≥7 working days** ahead of
operations, issued within 7 working days. Critically: *"RPA owned and operated by agencies do not
require UAOP, however, the agency shall intimate local police office and concerned ATS Units prior
to conduct of actual operations."*

> **Read that exemption carefully — it is the whole answer.** The lawful fast path through disaster
> airspace belongs to **the agency**, not to the builder. NDRF can fly. A student with an F450
> cannot, on any timeline that matters, and a major urban disaster zone will have helicopter and
> medevac traffic that makes an unauthorized multirotor an active hazard. **[INF]**

**[UNVERIF-SESSION]** on the NDRF-specific SOP and on whether India issues a formal TFR-equivalent
over disaster zones. Named for hand-retrieval; do not cite as found.

### The org-chart answer

**[INF], and I will defend it.** Put the question to an incident commander as it would actually
arrive: *a volunteer wants to fly an unregistered home-built drone over your active site, in your
helicopter airspace, to scatter 11 unsealed electronic devices across a pile your structures
specialist has not cleared, and then advise you where to dig, using a detector with no validation
data and no stated environmental limits.* Every element of that sentence is independently
disqualifying. The answer is no, and **a competent commander's no is correct** — the system has
offered no evidence that would justify a yes.

**So the honest answer is yes: this is a research platform, not a rescue tool.** Saying so plainly is
not a retreat. It changes the deliverable in ways that *help*:

- The validation burden becomes **publishable measurement**, not field readiness.
- Operation moves to a **bench, a test slab, and a demolition/training site** — where the §10.1
  measurement actually lives anyway.
- The drone (§8.6 Path B, **$739**) becomes **deferrable past every decision that matters** —
  which §9 already noticed but filed as a purchasing tip rather than the structural insight it is.
- The real route to a field system is **partnership with an agency that already holds the
  credential** (NDRF, a state SDRF, a fire service training wing). That is a years-long path, and
  naming it is more useful than a spec that pretends the path is not there.

---

## ATTACK 6 — Full FMEA

Likelihood/Consequence/Detectability on 1–5 (5 = worst: near-certain / mission-and-life-critical /
invisible to the operator). **RPN = L × C × D.** Rows are the whole chain, node through operator.
Labels: **[DOC]** cited · **[INF]** reasoned from a cited fact or from `00` · **[ASR]** my judgment.

| # | Failure mode | L | C | D | RPN | Consequence in the operation | Mitigation |
|---|---|---|---|---|---|---|---|
| F-1 | **Node destroyed/damaged on impact** — `00` #1: 200–1300 G actual vs 15–20 G design **[INF from `00`]** | 5 | 4 | **2** | 40 | Silent coverage hole. §9's 20 % attrition spare allowance is a guess against an impact figure wrong by 10–100× | Re-derive crush stack; **drop-test to destruction before anything else**; node must self-report health on landing so the hole is *visible* |
| F-2 | **Node lands in a void / wedged / upside down** **[ASR]** | 4 | 3 | 4 | 48 | Decoupled from the medium it must listen through. Sensitivity silently gone; the node still reports "alive" | Report orientation from the accelerometer's own DC gravity vector + a coupling quality metric in every packet. **Cheap, and the spec has neither** |
| F-3 | **Node position error ±2–5 m** — `00` #3 | 5 | 3 | **5** | **75** | **Localization is area-only, permanently.** Invisible: the dashboard draws a confident pin regardless | **Stop claiming a pin.** Render the actual uncertainty ellipse. Optional UWB inter-node ranging if sub-metre is ever truly needed |
| F-4 | **Out of radio range / NLOS through wet rubble** **[INF]** | 3 | 3 | 2 | 18 | Node lost to the network; data stranded | Measure NLOS range **wet and dry** before trusting 200–500 m; store-and-forward so a node holds its own detections |
| F-5 | **Mesh partition / routing never converges** — Attack 8 | 4 | 4 | 3 | 48 | Partial or total data loss; §2's "no single point of failure" is void | **Abandon multi-hop.** Star to an elevated gateway + store-and-forward. See Attack 8 |
| F-6 | **Drone crash (wind, updraft, GPS loss, kit-airframe failure)** **[ASR]** | 3 | 5 | 1 | 15 | **Injury risk to personnel on an active site.** Ends the deployment. A crash on a rescue site is a reportable incident that ends the *programme*, not just the flight | Never overfly personnel; geofence; deploy from the pile edge; **treat this as the risk most likely to end the project politically** |
| F-7 | **Gateway loss (drone lands, battery, crash)** — ~25 min endurance (§8.4) vs a multi-day operation | **5** | 4 | 1 | 20 | **Entire network mute.** This is a **single point of failure** that §2 denies having | **Ground-mounted gateway on a mast.** The drone's elevation argument (§2) is real but it cannot be the *only* gateway for 7 days on a 25-minute battery |
| F-8 | **GPS denied / multipath beside standing structures** **[DOC-adjacent, INF]** | 4 | 3 | 3 | 36 | Node positions degrade further (feeds F-3); §10.4's 1PPS sync reference is also lost — **one failure takes out both position and time** | Separate the two: survey a local reference by hand; don't let one GPS be both position and clock |
| F-9 | **Ground station (Pi) failure** — single Pi, §2 | 3 | 4 | 1 | 12 | All processing and display gone. **Second single point of failure** | Spare SD image + spare Pi. Trivial, and not in §9's BOM |
| F-10 | **Operator misreads the dashboard** **[ASR]** | 4 | 4 | **4** | **64** | A pin on a Leaflet map **reads as certainty**. The uncertainty lives in a doc nobody on a rubble pile is reading | **UI is a safety control.** Ship areas and confidence bands; make an un-confirmed detection visually un-actionable; put "REQUIRES INDEPENDENT CONFIRMATION" on the artifact itself |
| F-11 | **Sensor saturation from nearby machinery** — Attack 1 | **5** | 3 | 2 | 30 | No detection possible. If the dashboard shows "no detection" rather than "blind," it reads as a **cleared cell** | **Report BLIND as a distinct state.** Never let saturation render as absence. This is the single highest-value dashboard requirement in the document |
| F-12 | **Aftershock mid-scan** **[DOC]** on aftershocks; **[INF]** on effect | 4 | 3 | 2 | 24 | Saturation, node displacement (voids F-3 further), pile evacuated, silence period ended | Detect, discard the window, **flag all node positions as stale**, re-survey |
| F-13 | **Survivor dies mid-scan — signal vanishes** **[ASR]** | 2 | **5** | **5** | **50** | A detection followed by a disappearance. The system cannot distinguish *died* from *false positive* from *node failed* from *noise returned*. **The likely reading is "false alarm," and the cell gets deprioritized** | **A detection must latch and never silently clear.** Persist with a timestamp and a reason-for-loss field. Ethically this is the most serious row in the table |
| F-14 | **A rescuer's own heartbeat or footsteps detected as a survivor** **[INF]** | **4** | 4 | **5** | **80** | **Highest RPN in the table.** A crew member standing or kneeling still on the pile 2–3 m from a node — exactly what a silence period requires everyone to do — presents a real human cardiac signature at *shorter range and better coupling* than any buried victim. §3.1's amplitude rejection assumes footsteps are 5–50 mg, but a *motionless* rescuer is not footsteps | **Mandatory personnel accountability**: log who is on the pile and where, during every silence. Cross-reference every detection against it. Prefer detections from nodes with **no personnel within 5 m**. **This requirement does not exist in the spec and it is not optional** |
| F-15 | **Multiple survivors merged into one detection** — §6 claims ICA to N−1 | 3 | 3 | 4 | 36 | Undercount. Crew extricates one and moves on while a second is still buried | Report **"≥1 survivor"**, never a count. ICA's N−1 claim is untested and inherited from EEG practice |
| F-16 | **False positive → crew tunnels into an unstable structure** — Attack 3 | 4 | **5** | 3 | **60** | **Rescuer life-safety risk** + hours lost + a spent silence period + resources pulled from a real survivor | Mandatory multi-modal confirmation **before any cutting**; tune for specificity; publish a measured FP rate or publish nothing |
| F-17 | **False negative → cell declared clear, crew moves on** — Attack 3, ethics | 3 | **5** | **5** | **75** | **A survivor is abandoned.** Undetectable by construction: you never learn you were wrong | **The system must never output "clear."** Only "detected" or "no detection — not a clearance." Reporting coverage as *searched* is the specific act that kills someone |
| F-18 | **Node battery dies before the operation ends** — 25 h vs 5.75 d median max **[DOC]** | **5** | 3 | 3 | 45 | Coverage silently decays across exactly the days when late rescues happen | Command-triggered sensing (Attack 1) + report state-of-charge every uplink + size the cell for ≥168 h |
| F-19 | **Nodes become FOD / obstruction / trip hazard; unrecovered e-waste** **[ASR]** | 4 | 2 | 1 | 8 | 11 unsealed lithium-ish devices scattered on a site that will be worked by heavy equipment and later demolished. Someone has to account for them | Recovery plan, hi-vis casing, serialized inventory. **Not mentioned anywhere in the spec** |
| F-20 | **Classifier out-of-distribution** — §6 trains on MIT-BIH + USGS + synthetic noise **[INF]** | **5** | 4 | **5** | **100** | **Highest RPN overall.** The model is trained on **cardiac waveforms and earthquake noise** and deployed on **seismic coupling through rubble, with jackhammers**. Nothing in the training set resembles the test distribution. The confidence score will be well-calibrated on data that does not exist and meaningless on data that does | **No field use before real measured positive and negative examples exist.** This row alone is sufficient to classify the whole system as a research platform |

### §2's "no single point of failure" — attacked directly

> §2: *"Mesh is self-healing (Meshtastic or custom AODV): a destroyed node reroutes, no single point
> of failure."*

**There are at least four single points of failure, and the mesh addresses none of them.**

1. **The drone gateway** (F-7). Every packet funnels through one airborne node with ~25 min of
   endurance against a 7-day operation. Node redundancy is irrelevant when the exit is singular.
2. **The Pi ground station** (F-9). One box does filtering, classification, solving and display.
3. **The GPS time/position reference** (F-8). §10.4 made one $24.95 module the root of the timing
   tree *and* §8.5 makes GPS the root of the position tree. One failure, both trees.
4. **The operator** (F-10). One human, untrained in USAR, reading one dashboard, with no second
   opinion in the loop.

The mesh claim is **redundancy at the cheapest, most numerous, least critical layer, cited as
evidence of robustness at every layer.** And per Attack 8 the mesh may not even deliver that.

### Ethics and liability

**[ASR]** throughout; I found no Indian case law or standard this session and will not invent one.

- **A false negative is a decision to stop searching.** F-17. If the system's output ever functions
  as a clearance, it participates in a life-safety decision with no validation behind it. The
  mitigation is linguistic and absolute: **this system can say "detected" and "no detection." It can
  never say "clear."** Any dashboard affordance that reads as clearance is a defect.
- **Liability is unallocated and the structure is bad.** The builder supplies an uncertified
  instrument with no stated envelope; the commander acts on it; a survivor dies or a rescuer is
  injured in a secondary collapse at a false-positive site. **[INF]** No indemnity, no insurance, no
  standard conformance, no logged provenance.
- **The minimum ethical package before *any* field exposure**, including a training exercise:
  (1) a measured, published detection curve with its environmental conditions; (2) a measured false-
  positive rate against real site noise; (3) a written statement of limits delivered **to the
  commander, in writing, before use**; (4) immutable logging of every input and output for
  after-action review; (5) operation **only** under an agency that holds the credential and accepts
  the output as a lead.
- **Until all five exist, the correct deployment posture is: bench and training sites only.** That is
  not caution. Items (1) and (2) do not exist, so there is nothing to disclose and nothing to accept.

---

## ATTACK 7 — Project feasibility, person-weeks, and what to cut

§12's seven steps, costed honestly. **[ASR]** — these are my estimates for one competent person
working part-time, which is what this project is.

| § | Step | Person-weeks | Risk | Notes |
|---|---|---|---|---|
| 1 | **Bench detection** — answer §10.1 | **4–10** | **UNBOUNDED — can kill the premise** | The only step that matters. Needs a subject, a slab, a quiet room, and honest statistics. Wide range because "quiet room" is the hard part |
| 2 | Pipeline on synthetic data | 3–5 | Low, and **deceptive** | Will "work." Proves nothing — F-20. Synthetic-data success is the project's main self-deception risk |
| 3 | Two-node TDoA + sync | 6–12 | High, **and should be cut** | Attack 2: builds a solver nobody uses, in a band where `00` #4 says timing cannot work |
| 4 | Mesh, n-node | **8–20** | **UNBOUNDED — may be impossible** | Attack 8. Could consume the project and return nothing |
| 5 | Node hardware — case, drop test, power | 8–16 | High | `00` #1 and #2 mean a redesign, not a validation. Plus the missing environmental spec (Attack 4d) |
| 6 | Drone integration | **10–20** | **UNBOUNDED — external gates** | Kit airframe build + PX4 + AUX PWM + airspace. Attack 5 |
| 7 | Dashboard | 4–8 | Low | But F-10/F-11/F-17 make the UI a **safety control**, not a demo |
| — | Environmental spec, enclosure qual | 4–8 | — | **Not in §12 at all** |
| — | Validation, FP/FN measurement, documentation | **8–16** | — | **Not in §12 at all, and it is the actual deliverable** |

**Totals.** As written: **55–115 person-weeks** = **1.5–3.5 years** part-time, with three unbounded
steps. **§12 is a 3-year plan presented as a 7-item list.** Not 6 months.

**Critical path:** §10.1 → *everything*. Every other step is either downstream of it or orthogonal to
it. §12 lists it first but weights it equally with "dashboard," and `00` #7 showed the cost model is
**quadratic** in its result — so step 1 does not just gate the schedule, it gates whether the economic
argument survives at all.

**Cut, and why:**

| Cut | Reason |
|---|---|
| **§12 step 3 (TDoA + sync) entirely** | Attack 2(b): the user does amplitude hill-climbing, not hyperbolic solves. §10.4's "answered" sync is 10⁴ below the binding term (`00` #4) |
| **§12 step 4 (mesh) entirely** | Attack 8: likely contradictory with the duty cycle. Replace with star + store-and-forward |
| **§12 step 6 (drone) — defer past step 1 and step 5** | §9 already says $739 is deferrable. Attack 5 says it may never be lawfully flyable by this operator. The drone is the *least* load-bearing part of the system and has consumed §8.6's entire re-costing exercise |
| **§6's LSTM — defer, do not delete** | F-20. With zero real training data, a 64→32 LSTM is a way to overfit synthetic noise. Start with a periodicity/HRV detector you can reason about and whose FP rate you can state |
| **§7.2's accuracy table — delete, do not rebuild** | `00` #3 and #7. It has been patched twice and is wrong at the root |

**Add, because they are the real deliverables:** the environmental spec; the FP/FN measurement
protocol; the amplitude-ratio area-localization method; the BLIND-state dashboard; the personnel-
accountability cross-reference (F-14).

### The minimum viable experiment

§12 step 1 as written ("ADXL355 + dev board, Python capture, bandpass + FFT") is already decent but
it still **buys $55 sensors and a dev board first**, and it tests the *wrong* thing first — it asks
"can I see a heartbeat?" when the question that kills the project is "can I see it through anything,
against anything?"

**There is something cheaper, faster, and more decisive.**

> ### MVE: the tiered coupling test — **₹0–3,000, one weekend, no ADXL355, no drone, no node**
>
> **Step 0 (free, do it tonight).** Use a **smartphone accelerometer** (~1–4 mg/√Hz, roughly 100×
> worse than an ADXL355 **[UNVERIF-SESSION]** on the exact figure) on a hard floor, with a person
> lying still at 0.5 m and at 1 m. Phone taped flat, 5-minute records, FFT the 0.5–4 Hz band.
> **Decision rule:**
> - **A peak is visible at 0.5 m on a phone** → the signal is ~100× above the project's assumption
>   and a real sensor has enormous margin. **Proceed, and expect §10.1 to return good news.**
> - **Nothing at 0.5 m on a phone** → this is the expected and uninformative result. Go to step 1.
> This costs nothing and can only return good news or no news, which is why it goes first.
>
> **Step 1 (the decisive one, ~₹1,500–3,000).** One **ADXL355 breakout** — *one*, not nine — plus a
> dev board you already own. Then measure the **four numbers that decide the project**, in this
> order — and the order is the point, because each one can stop the next:
> 1. **Ambient floor, in situ.** Record the 0.5–4 Hz band on a concrete floor in a **normal,
>    un-silenced environment** — a building with people and traffic nearby. This is the number
>    `MEMORY.md` already identifies as the one unmade ~$2 measurement that decides the sensor choice.
>    **If ambient in-band noise exceeds ~1 mg, the premise is dead at any sensor price**, because the
>    target is 0.1–1 mg and no filter removes in-band noise.
> 2. **Coupling loss through a barrier.** Subject on one side of a concrete paver / slab / stack of
>    bricks, sensor on the other, at 0.5 / 1 / 2 / 3 m. **Returns r, which sets node count, which
>    sets cost as 1/r² (`00` #7).**
> 3. **Noise with a machine running.** Repeat (1) with an angle grinder or a compressor running
>    5–10 m away. **This is the Attack-1 measurement and nobody has proposed it.** It returns the
>    answer to the question that decides the CONOPS: *is there any usable SNR outside a silence
>    period?* If no — and I expect no — **the command-triggered silence-window architecture is
>    confirmed as the only viable design, and §4.1/§10.2 stop being problems.**
> 4. **Persistence, if and only if (2) returned something marginal.** Repeat the best marginal
>    configuration **20 times** with the subject present and **20 times** with the subject absent,
>    3 minutes each. Score detections. **If per-window detection is 60 % with a 20 % false-positive
>    rate, then persistence across 5 windows is decisive** — and that, not the LSTM, is the
>    detector. This is the measurement that tests the project's one surviving advantage, it needs no
>    extra hardware, and it costs an afternoon.
>
> **Total: one $55 sensor, a board, a slab, a cooperative human, a noisy power tool, a weekend.**
>
> **Why it beats §12 step 1:** it adds measurement (1) which can kill the premise *before* any
> coupling work, and measurement (3) which decides the architecture the project has been guessing at
> for two revisions. Same hardware. Different questions, in a better order.

**[ASR]** on the thresholds — they are mine, derived from §3.1's own 0.1–1 mg target, and they are
stated in advance deliberately: **write the decision rule down before you take the measurement**, or
the result will be interpreted generously.

---

## ATTACK 8 — The reference doc's framing, and the mesh contradiction

### Demo-grade claims inherited as engineering

`reference/Heartbeat_In_The_Rubble.md` ends with *"Judges don't expect a working product"* and
*"SECTION 12 — HACKATHON PITCH STRUCTURE."* Its numbers were chosen to survive 3 minutes of Q&A.
Several were promoted into `MASTER.md` as specifications, and the promotion stripped the hedges while
keeping the figures.

| Reference claim | Became | What the promotion lost |
|---|---|---|
| Accuracy/coverage/deploy-time table (ref §6) | **MASTER §7.2** | Marked PENDING and patched twice — **but the node counts, coverage and cost in §9 still flow from the 10 m-spacing row** (`00` #7). The table was never rebuilt, only annotated |
| *">93 % at >1 m, >87 % at 0.5 m (based on analogous medical MEMS studies)"* | **MASTER §6** "TARGET" | The reference's own parenthetical **analogy** became a target number. No measurement ever existed. `00`-style note: a bed-sensor measuring through a mattress and a node measuring through 2 m of rubble share only the word "MEMS" |
| *"TDoA triangulation delivers exact GPS coordinates — not a zone, a point"* (ref §2 step 5) | **MASTER §1** signal chain ending in "map pin" | The most consequential inheritance in the document. **`00` #3 says area; Attack 2 says area is what the user wants anyway.** "Not a zone, a point" is a pitch line that became the architecture |
| *"reducing rescue dig time by an estimated 60–80 %"* (ref §6) | Dropped — correctly | The one unsupported claim that did **not** survive. Good |
| *"Expected model accuracy"* from PhysioNet + USGS + synthetic | **MASTER §6** training plan | F-20. The training set never contained the deployment distribution, in either doc |
| 48–72 h battery (ref §3) | **MASTER §4.1**, corrected to 25 h, then contested | §4.1's correction is sound and the contested box is good practice. **But the requirement it should be measured against — 144+ h per Macintyre — appears in neither document** |
| *"~$29/node, ~$550 system, 96 % cheaper than Delsar"* (ref §10) | **MASTER §9**, rebuilt to $1,845 | Honest rebuild. **Still one point on a 1/r² curve** (`00` #7), presented as *the* system cost |
| The 5-step flow diagram (ref §2) | **MASTER §1** signal chain | **The diagram's real damage is its implied completeness.** Node → mesh → gateway → FFT → LSTM → TDoA → pin reads as a finished architecture. It contains **no detection threshold, no confirmation step, no blind/saturated state, no uncertainty, no human in the loop, no failure path.** Every single FMEA row above lives in a gap this diagram makes invisible — and it was inherited verbatim as §1 |
| *"Works in Noise ✓ (ML filtered)"* comparison table (ref §1) | **MASTER §1** gap argument | Attack 1(e). The least defensible cell in either document |
| *"Self-healing mesh, no single point of failure"* (ref §4) | **MASTER §2**, verbatim | Below |

### The mesh is a hidden contradiction — and it may be fatal to §2's topology

§2: *"Mesh is self-healing (Meshtastic or custom AODV): a destroyed node reroutes, no single point of
failure."* Reference §4 adds *"continuously re-maps shortest path using AODV."*

**The duty cycle and the mesh are in direct conflict, and nobody has written it down.** **[INF]**,
built from the spec's own numbers (§5: ~1 % duty-cycle limit; §4.1's 20 % breach; `00` #5's packet work):

1. **Relaying multiplies airtime, per hop, per packet.** A packet crossing 3 hops consumes the band's
   airtime **3 times** and consumes **3 nodes'** duty-cycle allowances. §5's budget treats airtime as
   a per-node cost. **In a mesh it is a per-hop cost and a shared-medium cost.** The §10.2 crisis
   (4800 bps against a 1 % limit) is therefore *understated* by roughly the mean hop count.
2. **Relaying requires listening, and listening is the expensive state.** §5 lists **1–2 mA RX** vs
   10–40 mA TX. TX looks worse per instant and is far cheaper per hour: a 1 % TX duty cycle costs
   ~0.4 mA average, while **RX at 10 % duty costs ~0.15 mA and RX at 100 % costs 1–2 mA** — i.e.
   **continuous receive alone is 3–5× the entire §4.1 LoRa budget**, before a single packet is
   relayed. A node that sleeps 99 % of the time to meet §4.1 **is not available to relay.** A node
   available to relay **cannot meet §4.1.** These are the same radio.
3. **AODV route discovery is itself broadcast traffic.** Route requests flood. Route maintenance is
   periodic. On a link where the *payload* already does not fit (§5.1), **the control plane has no
   budget at all.** AODV was designed for always-on WiFi-class radios; porting it to a 1 %-duty
   sub-GHz link is not a tuning exercise.
4. **"Self-healing" presumes topology change worth healing.** Nodes are **static**. The topology
   changes only when a node **dies** or rubble shifts — rare, discrete events. **[INF]** AODV's
   entire value is adapting to mobility that does not exist here. The project is paying mobile
   ad-hoc routing's full airtime and power cost to solve a problem it does not have.
5. **Meshtastic is a real, working system — which makes it the wrong citation.** It works by being
   *generous* with airtime: always-on receive, mains or large-battery nodes, and duty cycles that
   suit a hiker's handset. **[UNVERIF-SESSION]** on its exact numbers. Citing "Meshtastic or custom
   AODV" as evidence that the mesh is solved conflates a system whose power budget is 3 orders of
   magnitude larger with a CR2032 node.

> **Conclusion: the mesh as specified is near-impossible on this link, and §2's "no single point of
> failure" dies with it.** The node redundancy §2 offers as robustness evidence is the redundancy the
> mesh was supposed to deliver, and the mesh cannot be afforded. **Remove the mesh claim from §2
> before it is designed around any further.**

**And the replacement is better, not worse** — which is why this is a finding rather than a
catastrophe:

- **Star topology to an elevated gateway.** §2's own best insight is *"the drone's elevation is what
  makes the gateway link work."* Elevation buys LOS to every node at once. **A star needs no routing,
  no route discovery, no relay listening, and no per-hop airtime multiplication.**
- **Store-and-forward at the node.** A node holds its detections in flash and uplinks when polled.
  This also fixes F-4 (stranded data) and is the natural fit for command-triggered sensing (Attack 1):
  the gateway broadcasts "silence starting," nodes sample, the gateway polls them in sequence.
  **One broadcast, N scheduled replies, zero contention, zero routing.**
- **Put the gateway on a mast, not only on the drone.** Fixes F-7, the most under-acknowledged single
  point of failure in §2. §8.4's 25-minute endurance cannot serve a 7-day operation; a mast can.

**Scheduled TDMA star + store-and-forward is simpler than AODV, cheaper in airtime and power, fixes
three FMEA rows, and is the topology the silence-period CONOPS wants anyway.** The mesh was never
load-bearing; it was inherited because "self-healing mesh" is a good phrase in a pitch.

---

## THE HONEST VALUE PROPOSITION — rewritten

Everything above, in the form the project should actually defend.

> ### Heartbeat In The Rubble — what it is
>
> **A cheap, disposable, drone- or hand-placed seismic node network that tells a search planner which
> parts of a large collapse site are worth the next silence period.**
>
> **The problem it solves** — not the one the spec claims. A 500–5,000 m² collapse gets a handful of
> site-wide silence periods and a 6-sensor hand-placed listening device. **Nobody can afford to listen
> to all of it.** Coverage, not sensitivity, is the binding constraint on the incumbent workflow.
>
> **What it does.** 10–30 nodes are placed once, early, and stay for days. They sleep. **The site
> already calls an All Quiet about once an hour for a few minutes** **[DOC]**; on that command the
> gateway broadcasts, every node samples simultaneously for ~180 s, and reports. The ground station
> returns, per cell: **DETECTED / NO DETECTION / BLIND (saturated or decoupled)**, with a confidence
> and an uncertainty area of **2–5 m** — **and a count of how many consecutive All Quiets that cell
> has detected in.**
>
> **What it is honestly better at than Delsar — two things, and the second is the real one.**
> 1. **Coverage per All Quiet.** **20+ simultaneous points vs ~6 hand-placed** **[DOC]**, with nobody
>    walking the pile to place them. The site's listening capacity stops being limited by how many
>    sensors an operator can carry and plant inside a 5-minute window.
> 2. **Persistence across All Quiets.** The nodes stay. Over a multi-day operation they accumulate
>    **20–100 independent looks at the same cell**, plus a local noise baseline. **A survivor is
>    persistently present in one cell; noise is not.** That turns a marginal single-window detector
>    into a usable multi-window one, and **no hand-carried instrument can do it**, because it leaves
>    with the operator. This is the only claimed advantage in the project that survives every attack
>    in this document.
>
> Cost is a *secondary* advantage and is quadratic in an unmeasured number (`00` #7) — **do not lead
> with cost.**
>
> **What it does NOT do, stated first and in writing, to the incident commander:**
> - **It does not produce a pin.** Area only, 2–5 m, and the physics says that is the floor.
> - **It does not clear anything.** "No detection" is **not** "no survivor." F-17.
> - **It does not replace confirmation.** Every detection is a lead requiring canine, search cam or
>   hailing before anything is cut. F-16.
> - **It does not work through running machinery.** It works in the silence the site already calls.
> - **It does not detect reliably at all yet.** §10.1 is unmeasured. F-20.
>
> **Who operates it.** A credentialed agency (NDRF / SDRF / fire service), under its own airspace
> authority, with the builder in support. Not a volunteer with a drone. Attack 5.
>
> **Current readiness: research platform.** Bench and training sites only, until a measured detection
> curve and a measured false-positive rate exist and are published.

**Three sentences the project should be able to say without flinching, and currently cannot:**
1. "Here is the measured detection range, with the slab thickness and the ambient floor it was
   measured against." *(§10.1 — does not exist)*
2. "Here is the measured false-positive rate against real site noise, and here is the threshold it
   implies." *(does not exist)*
3. "Here is the written limits statement we hand the incident commander before use." *(does not
   exist)*

**Until those three exist, every operational claim in `MASTER.md` is unsupported — and the first one
is one weekend and one $55 sensor away.** That is the genuinely good news in this document.

---

## SOURCE TABLE

Link status conventions per project practice: **LIVE** = fetched, body inspected, content matched the
title. **BOTWALL** = reachable but gated. **DEAD** = 404/gone. **UNVERIF-SESSION** = not fetched this
session; do not cite as verified. HTTP 200 ≠ exists; every LIVE below was confirmed by body content.

| # | Source | Used for | Status |
|---|---|---|---|
| 1 | Fire Engineering, *Listening Devices in Heavy Search and Rescue* — fireengineering.com/technical-rescue/listening-devices-in-heavy-search-and-rescue/ | **Attack 2(b):** operators compare sensors for *"the largest and/or clearest signal"*; leave the hot sensor, **reposition the others**; spacing ≤25 ft, typically 15 ft; more sensors = more area, faster | **LIVE** |
| 2 | Fire Engineering (Donnelly), *Building Collapse: Rescue Operation's Technical Search Capabilities* | **Attacks 1, 2, 3:** *"minimal noise"* requirement; *"stop for several minutes"*; ranges 5–25 ft acoustic / 50–150 ft seismic; *"even the vibration of a heartbeat"*; *"up to six sensors"*; search cam with two-way audio; coverage communication | **LIVE** |
| 3 | Firehouse, *Building Collapse Rescue: Life Detection Systems* | **Attacks 1, 2(b), 3:** *"All Quiet"* baseline; *"leave the sensor that has the greatest noise in place and move the remaining sensors"*; interference masking victims; hailing — *"ask the victim to tap an object 3 times"* | **LIVE** |
| 4 | AP via Clarke County Tribune, Adana Turkey, 2023-02-08 | **THE LEAD FACT:** *"lifted slabs of cement with enormous cranes and smashed rubble with jackhammers. Then, they stopped. Silence. Key to detecting the faintest noise"* | **BOTWALL** (quote visible above paywall; AP wire text, widely syndicated) |
| 5 | AP wire, Colombia M7.4, 2026-08-13 (abcnews / local10 / kiro7 / wftv syndications) | **THE LEAD FACT:** rescuers *"signal for engines to be shut off, cranes to stop and drills to be silenced"*; noise *"gradually fades"*; ≥265 dead; 48–72 h prime window with extension if water is available | **Search-snippet LIVE; article URLs DEAD (404 on two syndications tried).** Treat the quotes as AP wire text confirmed via search result body, not via a fetched page |
| 6 | **Macintyre AG, Barbera JA, Smith ER**, *Surviving collapsed structure entrapment after earthquakes: a "time-to-rescue" analysis*, **Prehosp Disaster Med 2006;21(1):4–17, PMID 16602260** | **Attack 4(a):** survivors beyond 48 h; **average max time-to-rescue 6.8 d, median 5.75 d** across 18 earthquakes; longest reliable **14 d**; Marmara 1999 — 43 rescues, 12 h to 146 h | **BOTWALL** (Cambridge Core abstract; figures from search-result body + prior session) |
| 7 | *Survival interval in earthquake entrapments: research findings reinforced during the 2010 Haiti earthquake response*, Disaster Med Public Health Prep (Cambridge) | Corroborates #6 — survival intervals confirmed in Haiti. **Not read this session** | **UNVERIF-SESSION** |
| 8 | *Maximum time-to-rescue after the 1908 Messina–Reggio Calabria earthquake was 20 days*, Prehosp Disaster Med | Upper tail on entrapment survival. **Not read** | **UNVERIF-SESSION** |
| 6a | **UK NFCC National Operational Guidance**, *Primary search: Unstable or collapsed structure* — nfcc.org.uk | **THE LEAD FACT, as doctrine:** *"Around once per hour for a few minutes, all activity should cease to listen for sounds made by casualties"*; sound detection devices used in Stage 4 void exploration; *"around half of the casualties in a structural collapse may be rescued near the surface of the debris and early in the operation"* | **LIVE** |
| 6b | FEMA US&R — *"All Quiet / Cease Ops = 1 Long Blast"* emergency signal; and Kansas Fire Marshal *Urban Search and Rescue Markings and Signals* PDF | **THE LEAD FACT, as a commanded state:** the silence is a signalled site-wide condition in the same table as evacuation — not an informal pause | **Signal text via search body (LIVE); source PDF would not parse — [UNVERIF-SESSION] on the exact table** |
| 9 | INSARAG — insarag.org/iec/iec/ | **Attack 5:** IEC exists; Light/Medium/Heavy; classifier-applied checklists; *"objective manner"* | **LIVE** (via search body) |
| 9a | INSARAG Guidelines Vol. II **Manual B — Operations** (insarag.org annexes; insarag-docs.readthedocs.io mirror; preparecenter.org copy) | **Attack 3:** the document that should contain the victim-confirmation rule. **Located but not read** — the readthedocs mirror is the most promising route | **UNVERIF-SESSION — named for hand-retrieval, highest-value remaining target** |
| 10 | INSARAG IEC/R Checklist 2018 (PDF, insarag.org) | Classification criteria. Referenced, **not read this session** | **UNVERIF-SESSION** |
| 11 | INSARAG Guidelines **Vol. II Manual C** | Equipment/capability requirements for technical search. **The specific document that answers "device categories or named models?"** — worth hand-retrieval | **UNVERIF-SESSION — named for hand-retrieval** |
| 12 | INSARAG Technical Guidance Notes — insarag.org/methodology/insarag-technical-guidance-notes/ | *"non-binding guidance beyond minimum requirements"* — shows the two-tier structure | **LIVE** (via search body) |
| 13 | Draft Drone Rules 2021 Gazette — digitalsky.dgca.gov.in | **Attack 5:** primary DGCA source. **Not fetched this session** | **UNVERIF-SESSION** |
| 14 | ksandk.com, *DGCA Regulations on the use of Drones in India* | **Attack 5:** Red/Yellow/Green zones; restricted locations; Digital Sky UAOP, ≥7 working days, issued in 7, valid 5 years; **agency exemption** — no UAOP but must notify local police and ATS | **LIVE** (via search body) |
| 15 | bhattandjoshiassociates.com, *Drones and the DGCA: A Comprehensive Analysis* | Corroborates #14 | **LIVE** (via search body) |
| 16 | drishtiias.com, Draft UAS Rules 2020 / Digital Sky | Corroborates #14; COVID relief as the driver that exposed gaps in disaster-use rules | **LIVE** (via search body) |
| 17 | NDRF standing orders / SOP for structural collapse | **Attack 5:** the India-specific procedural gate. **Not found this session** | **UNVERIF-SESSION — named for hand-retrieval** |
| 18 | FEMA US&R resource typing / Task Force equipment cache list | **Attack 5:** US-side credentialing analogue. **Not found this session** | **UNVERIF-SESSION** |
| 19 | Delsar / Savox product pages (allsafeindustries.com, directindustry.com) | Incumbent capability and *"quickly deployed… converts the structure into a large sensitive microphone"* | **LIVE** (via search body); vendor marketing copy, not independent |
| 20 | After-action reports — Turkey/Syria 2023, Nepal 2015, Haiti 2010, L'Aquila 2009 | Site-condition and workflow evidence. **None retrieved this session** | **UNVERIF-SESSION — the largest evidence gap in this document** |

### Declared evidence gaps

Honest accounting, because an unlabelled gap is indistinguishable from a fabrication:

1. **~~No formal procedural text was obtained.~~ RESOLVED for the silence protocol.** **UK NFCC
   national operational guidance (#6a)** gives the written rule — *"around once per hour for a few
   minutes"* — and **FEMA's All Quiet signal (#6b)** confirms it is a commanded site-wide state.
   Four independent source classes agree. **Remaining gap: no *INSARAG* text specifically, so the
   figure is UK/US doctrine, and I have not verified that NDRF (#17) uses the same cadence.** The
   ~hourly number should be treated as **well-evidenced for UK/US practice, [INF] for India.**
2. **The multi-modal confirmation requirement is [UNVERIF-SESSION].** I believe two independent
   indications are required before committing to extrication. **I did not find the passage. Do not
   cite me for it.**
3. **No after-action reports were read** (#20). Everything about real site conditions, personnel
   density and equipment tempo is **[INF]** from #1–5.
4. **DGCA sourcing is secondary** (law-firm and explainer summaries, #14–16). The primary Gazette
   text (#13) was not fetched. The agency exemption is the load-bearing clause and should be read in
   the original.
5. **Macintyre figures come from search-result body text plus a prior session**, not from the
   article. Abstract is **BOTWALL**. The figures are consistent across both retrievals, and PMID
   16602260 is correct, but **the full paper has not been read.**
6. **Two AP syndications 404'd.** The Colombia quotes are from search-result body text. Verify
   against the AP original before publishing them anywhere.

---

## WHERE I COULD BE WRONG

Stated as specifically as the attacks, because a critique that cannot be falsified is not engineering.

1. **The silence fact may be less binding than I claim — and this is the one that matters most.**
   My argument assumes machinery noise swamps the 0.5–4 Hz band *at the node*. Seismic coupling is
   distance- and path-dependent: a node 50 m from the working face across a discontinuity may have a
   far quieter in-band floor than I assume. **If MVE measurement (3) shows usable SNR at 20–30 m from
   a running machine, Attack 1 weakens substantially and continuous monitoring returns as a real
   advantage.** That single measurement decides my lead finding, which is why it is in the MVE.
2. **I may be wrong that rescuers cannot use sub-metre precision.** My evidence for amplitude
   hill-climbing is strong **[DOC]**, but it describes *current* tradecraft with *current* tools.
   Procedure follows capability: an instrument that reliably delivered 0.3 m might change the
   procedure, as thermal imaging changed interior search. **My argument is that this system cannot
   deliver 0.3 m anyway (`00` #3), so the question is moot — but if RTK plus UWB collapsed the
   position term, Attack 2 would need re-arguing on its merits rather than on the floor.**
3. **The mesh argument is an airtime/power argument, not an impossibility proof.** A gossip or
   flooding protocol with aggressive scheduling, or a two-tier design (a few mains-powered relays
   plus many leaf nodes), could make multi-hop work. **I did not model a specific protocol.** My claim
   is narrower than "mesh is impossible": **AODV-class on-demand routing on CR2032 nodes at 1 % duty
   is not viable, and the star is strictly better for this topology.** A two-tier mesh would defeat
   my framing while conceding the main point.
4. **The FMEA L/C/D scores are my judgment, unvalidated.** F-14's likelihood-4 is the one I would
   most expect to be argued down — it depends on personnel density near nodes during a silence, which
   I have not measured. **The row survives even at likelihood 2**, because D=5 and C=4, but the
   ranking would shift.
5. **Person-week estimates could be 2× in either direction.** They assume one part-time person. A
   funded team with a machine shop and an agency partner changes every unbounded step. The **critical
   path (§10.1 first) is robust to the estimates**; the totals are not.
6. **"Research platform" may be too harsh for one specific case.** At a **USAR training site or a
   controlled demolition**, with a cooperative volunteer in a known void, this system could be
   exercised end to end **legally and safely, today, with an agency partner.** That is not a real
   disaster, but it is not a bench either, and it is the obvious next step after the MVE. I should
   not have framed the options as bench-vs-rubble.
7. **If §10.1 returns r ≥ 3 m and MVE (1) returns a sub-0.1 mg in-band ambient floor, much of my
   framing softens.** The project would then have a genuinely sensitive wide-area instrument, and the
   CONOPS objections become design work rather than reframing. **I consider that outcome unlikely —
   but it is one weekend of measurement away, and no argument in this document should be allowed to
   substitute for taking it.**
8. **I am reviewing a pre-code spec as though it were a product submission.** Some of what I call
   omissions (environmental spec, validation protocol) are legitimately not yet written at this
   stage. **My defence: the spec makes deployment-grade claims — "no single point of failure,"
   "reaches fire zones," "exact GPS coordinates" — and a claim is fair game the moment it is made,
   regardless of project stage.** Were those claims hedged, several attacks here would reduce to
   to-do items.
