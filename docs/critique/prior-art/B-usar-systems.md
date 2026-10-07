# B — USAR listening systems, doctrine, drone-deployed sensors, Indian context

Prior-art sweep for the funding proposal's problem statement and novelty claim. Scope: commercial USAR acoustic/seismic locators; academic geophone/accelerometer arrays for trapped-victim localization; drone-deployed sensor nodes; whether anchor-position uncertainty dominating TDoA is textbook; USAR doctrine on "All Quiet" and responsive tapping; Indian (NDRF/NDMA) context. Cardiac source amplitude and competing modalities are sibling document A; propagation and tap-source parameters sibling document C.

Compiled 2026-10-07, extended 2026-10-08. Access states: **READ-FULL** / **READ-ABSTRACT** / **CITED-ONLY**. Every price carries a capture date.

---

## Bottom line for the proposal

- **The tapping/voice retarget is not a contribution — it is the status quo, in both doctrine and product.** FEMA's own US&R training material lists, as a *disadvantage* of listening devices, that the "**victim must create a recognizable sound pattern**," and runs a parallel "audible call out/knocking method (rescuer hailing method)." Every fielded seismic locator (Delsar LD3, Leader SEARCH, the NDRF "Life Detector Type-I" spec) detects taps, scratches, movement and voice, and **none of them claims heartbeat**. Do not frame "retarget from heartbeat to tapping" as the innovation; a USAR-literate reviewer will recognise it as current practice and the whole proposal will inherit that credibility loss.
- **"Automated localization instead of operator-interpreted listening" was already built, demonstrated and published — by INACHUS (EU FP7 607522, 2015–2018).** Its Ground-Based Seismic Sensor system is a network of distributed vibrational ground sensors in which victim "knocking, hitting, etc. can be **automatically detected and positioned**," with adaptive background suppression and heat-map output, and its own published motivation is verbatim the proposal's intended novelty claim: that "existing operational systems require human operators to listen to and interpret the received signals through headphones." This is the single most dangerous citation in the sweep. It must be cited by the proposal and distinguished explicitly, not omitted.
- **Drone-deployed seismic nodes also already exist, with measured planting performance** — drone-*landed* geophones (Stewart et al., SEG 2016) and the air-dropped **SeismicDart** (Sudarshan et al., NSF IIS-1553063), which reports penetration/angle vs drop height across seven soils and fidelity against planted geophones at ρ = 0.81–0.98. Defensible novelty therefore sits in **the combination at fielded cost and mesh scale**: cost per node, node count/persistence across repeated hourly All Quiet windows, rubble (not soil) emplacement, and the Indian NDRF deployment context — not in the retarget, not in automated knock localization per se, and not in "position uncertainty dominates TDoA."

---

## Is the tapping retarget already the status quo?

**Yes. Unambiguously, in both doctrine and product. This is the most important finding in this document and it is stated here without softening, per the brief.**

Three independent lines of primary evidence converge:

**1. FEMA doctrine explicitly assumes a responsive victim who makes a sound pattern on command.** From the FEMA National US&R Response System training material (`fema.gov/pdf/emergency/usr/mod3_u3.pdf`, text extracted locally in full, 61,971 characters — **READ-FULL**), on physical/listening search, verbatim:

> Disadvantages: "Unconscious person cannot be detected. Ambient site noise is intrusive. **Victim must create a recognizable sound pattern.** Range is limited (acoustic – 25 feet, seismic – 75 feet)."

> Advantages: "**Able to cover larger search areas and sometimes triangulate on victim position.** Capable of picking up faint noises and vibrations."

And, as a named method in the same document:

> "Audible call out/knocking method (rescuer hailing method)" — "Unconscious or physically weak person cannot be detected"; "Personnel can inform victim of expected response. This procedure can be modified and used in conjunction with listening devices."

The responsive-victim assumption is therefore *written into the doctrine as the operating premise*, and the limitation the proposal's retarget accepts (unconscious victims undetectable) is a limitation FEMA already documents and accepts.

**2. Commercial devices already detect exactly the signals the proposal targets.** The Savox/Delsar official datasheet (A02005#B, **READ-FULL**) describes 6 seismic + 2 acoustic inputs, 1 Hz–3000 Hz, with "audio response is summed," two headset jacks, and a 300-second record loop. Leader SEARCH product material states the device detects "moves, scratches, shouts, taps," and that "the rescuer can 'listen' using an audio headset and 'observe' the audio signal using bar graphs." Neither claims heartbeat or breathing. The NDRF's own procurement specification for "Human Life Detector Type-I" (**READ-FULL**) specifies 1 Hz–3000 Hz, not fewer than 6 sensors, and an "LED bar graph any 2 channels or sum of all channel" display.

**3. The hailing instruction to tap a specific number of times is standard taught practice.** Secondary USAR training sources (Firehouse, Fire Engineering — **READ-FULL** as web articles, but *secondary* to doctrine) describe asking "the victim to tap an object 3 times," "knock five times on something solid," and an "array of listeners deployed around the collapse site." I was **not** able to locate the specific "3 to 5 times" numeric instruction inside a primary FEMA or INSARAG PDF; see *Could not access*. The *existence* of a commanded tap-count protocol is nonetheless established by the FEMA primary text above ("Personnel can inform victim of expected response").

**What this means for the proposal, concretely.** The problem statement may say that heartbeat detection through rubble is infeasible (sibling A establishes this) and that doctrine and product therefore already target responsive signals — citing FEMA as above. It **may not** present "we will detect tapping instead of heartbeat" as a novel contribution. The honest framing is: *the target signal is the one doctrine already uses; what is missing is cheap, dense, automatic, drone-emplaced localization of it.* That framing is defensible. The retarget framing is not.

---

## Novelty verdict

**PARTIALLY ANTICIPATED, trending to ALREADY PUBLISHED on three of the four candidate novelty axes.**

| Candidate novelty claim | Verdict | Prior art that anticipates it |
|---|---|---|
| Retarget from heartbeat to tapping/voice | **ALREADY PUBLISHED / status quo.** Not a contribution. | FEMA US&R doctrine; Delsar LD3; Leader SEARCH; NDRF Type-I spec |
| Automated localization of knocks in a distributed seismic network, replacing operator headphone interpretation | **ALREADY PUBLISHED.** Demonstrated by an EU-funded 20-partner consortium. | INACHUS GBSS (FP7 607522, 2015–2018) |
| Drone/air deployment of seismic sensor nodes | **ALREADY PUBLISHED** for soil; **open for rubble.** | Stewart et al. SEG 2016 (drone-landed geophones); Sudarshan et al. SeismicDart (air-dropped); UAV WSN node-dropping from ~2012 |
| "Node position uncertainty, not clock error, bounds TDoA accuracy" | **TEXTBOOK.** Must not be presented as a finding. | GDOP; standard anchor-position-error terms in localization literature |
| Seismic array *on rubble* for survivor location | **ALREADY PUBLISHED** (hand-placed). | Arosio et al. 2010, DOI 10.3997/1873-0604.2010051 (CITED-ONLY, via sibling) |
| **Array extent** — breaking the hand-placement/cable limit on how large and dense the array can be, by air deployment | **DEFENSIBLE NOVELTY, and the strongest axis.** Named as an explicit limitation by the closest prior art. | — (Arosio et al. name "limited array extent" as their own constraint) |
| Cost per node at mesh scale (many tens of nodes), persistent across repeated All Quiet windows, in the Indian NDRF context | **DEFENSIBLE NOVELTY.** Nothing located that does this. | — (gap; see caveats) |

**Where defensible novelty actually sits.** Five things, in descending strength:

0. **Array extent, via air deployment.** The closest prior art on rubble (Arosio et al. 2010) names "limited array extent" as one of its three own limitations, alongside debris inhomogeneity and the need for real-time response. Hand placement bounds how many sensors you can site and how far apart, because every one costs operator time on an unstable pile and, for cabled systems, a cable run. Air deployment removes that bound directly. **This is the cleanest novelty argument in the document** — prior art states the constraint; the proposal's mechanism lifts it. It outranks the cost argument because it is a *capability* difference, not a price claim resting on unverified figures. Conditional on reading Arosio et al. and confirming the limitation as reported.

1. **Cost and therefore node count.** Incumbents are 6-to-8-sensor, cable-tethered, ~USD 10³–10⁴-class instruments (pricing is poorly verified — see table caveats). A sub-USD-100-class node changes the achievable array geometry by an order of magnitude, and *array geometry is precisely what bounds TDoA accuracy* (see GDOP section). This is the strongest claim because it is quantitative, verifiable, and not anticipated by INACHUS, which used a small professional sensor set.
2. **Rubble emplacement rather than soil.** All verified drone-deployment prior art plants spikes in *soil*, characterised by soil compression strength (0.056–4 kg/cm²). Nobody located has characterised coupling of an air-dropped node onto *collapsed structural debris* — broken concrete, rebar, voids, dust. This is a genuine measurement gap and a natural proposal deliverable.
3. **Persistence across the doctrinal duty cycle.** Doctrine runs All Quiet roughly hourly for a few minutes. A permanently emplaced mesh that listens through every window without re-deploying operators and cables is an operational change incumbents cannot make. This is weaker as *novelty* (it follows from the hardware) but strong as *impact*.
4. **Indian deployment context.** NDRF's own equipment schedule and Type-I specification show a procurement baseline with no automated-localization requirement at all. For an India-funded proposal this is a legitimate, documented capability gap.

**What the proposal must concede in writing.** That tapping is doctrine's existing target; that automated knock localization was demonstrated by INACHUS; and that air-dropped geophones exist. A proposal that cites and distinguishes these is far stronger than one a reviewer catches omitting them.

---

## Commercial landscape

All prices **captured 2026-10-07** unless noted. **No vendor list price was obtained for any product in this sweep** — every figure below is reseller, distributor, auction or quote data, and several are unreliable. Per project convention (BOM prices drifted 8–16 % in 19 days), none of these should enter the proposal without hand-retrieval from the vendor.

| Product | Vendor | Price (capture date) | Sensor / band / channels | Automated localization? | Claims heartbeat? | Access |
|---|---|---|---|---|---|---|
| Delsar LifeDetector LD3 | Savox Communications (Delsar brand; Con-Space distribution) | No vendor list price obtained. eBay **used** LD3 sensor USD 5,225.00 (reduced from 5,500.00); used Delsar unit USD 3,490.00; "Complete Kit" USD 2,000.00; goldsupplier (CN) quote USD 28,000–28,500 — all **2026-10-07**, all secondary/auction, treat as indicative only | Official datasheet A02005#B: **6 seismic + 2 acoustic inputs, 1 Hz–3000 Hz**, audio summed, 2 headset jacks, 300 s record loop | **No.** Operator listens on headset and identifies the strongest signal visually | **No** | READ-FULL (datasheet); price data READ-FULL but secondary |
| Delsar LD3 acoustic sensor | Savox / OTB Products (AU distributor) | — | Acoustic **80 Hz–4500 Hz** | n/a | No | READ-FULL (distributor spec) |
| Delsar LD3 Mini | Savox / OTB Products (AU) | AUD 1,565.44 (**2026-10-07**, distributor listing) | Not separately captured | No | No | READ-FULL (listing) |
| Delsar LD3 (full kit), OTB listing | OTB Products (AU) | Page displayed "**$5.00 AUD**" — judged a placeholder or deposit, **NOT a citable unit price**. Recorded here only so it is not mistaken for data later | — | No | No | READ-FULL (page), value rejected |
| Leader SEARCH | Leader (FR) | Not obtained | **6 sensors total: 3 wireless + 3 cabled.** Detects "moves, scratches, shouts, taps" | **No.** "The rescuer can 'listen' using an audio headset and 'observe' the audio signal using bar graphs" | **No** | READ-FULL (product material) |
| Human Life Detector **Type-I** (NDRF procurement spec) | Specification, not a product — open to any bidder | Not a priced item | **1 Hz–3000 Hz**; "not less than 6 sensors. 4/6 sensors"; seismic sensor 1 Hz–300 Hz, shock-resistant >1000 g; high-pass 100 Hz, notch 50/60 Hz, low-pass 600 Hz; 6 seismic + 1 acoustic; 2 headphones; 6 × 10 m cable spools; "LED bar graph any 2 channels or sum of all channel, range 60 dB" | **No — not required anywhere in the specification** | **No** | READ-FULL (NDRF PDF, 5,585 chars extracted) |
| "Life Detector **Type-II**" (NDRF schedule) | Specification | Not obtained | EM-field heartbeat class; 500 m open air; discriminates humans from animals and the dead | Not characterised | **Yes** (different modality — EM, not seismic) | READ-FULL (schedule entry); full spec not retrieved |
| Vibrock V901 | Vibrock (UK) | — | **NOT A USAR VICTIM LOCATOR.** Blasting/piling/construction vibration monitor. Listed here to record the correction: an earlier working assumption misclassified it as a competitor. **Do not cite it as one.** | — | — | READ-FULL (corrected) |
| SearchCam / Con-Space, Bio-Rescue, Rescue Technology | various | Not obtained | Not characterised | Unknown | Unknown | **NOT RETRIEVED** — see *Could not access* |

**Two caveats the proposal must respect.** First, the project's long-standing "~USD 15,000 Delsar" figure was **not** independently confirmed in this sweep; do not use it. Second, the spread in the captured data (USD 2,000 for a "complete kit" to USD 28,500 for a quote) is too wide to support any cost-ratio claim. If the proposal wants to claim a cost advantage over incumbents — and that is its strongest novelty axis — it needs **one vendor-authoritative new-unit price, hand-retrieved and date-stamped.** That is the single highest-value outstanding action in this document.

**What incumbents actually are, summarised.** Six-to-eight channel, cable-tethered, 1 Hz–3000 Hz seismic plus acoustic, summed-audio, headset-plus-bar-graph instruments whose output is interpreted by a trained operator, and whose localization procedure is iterative sensor relocation ("leave the sensor that has the greatest noise in place and move the remaining sensors"). **Not** automated, **not** multilateration, **not** heartbeat.

---

## Academic prior art

| Citation | DOI / URL | Access | Claim | Bearing on the proposal |
|---|---|---|---|---|
| INACHUS (FP7 grant 607522, 2015–2018, 20 partners, coordinated by ICCS, Greece) — **Ground-Based Seismic Sensor system (GBSS)** | Project pages; `inachus.eu/inachus-components` returned HTTP 403 | **READ-ABSTRACT** (project descriptions and component summaries read; no peer-reviewed GBSS paper retrieved) | "A network of distributed vibrational sensors (ground sensors)"; vibrations from victim "knocking, hitting, etc. **can be automatically detected and positioned**"; adaptive background suppression for noisy environments; heat-map output. Verbatim motivation: "The system can automatically detect and locate knocking signals even in noisy environments, which is known to be a very challenging task today, **as existing operational systems require human operators to listen to and interpret the received signals through headphones.**" | **The most dangerous prior art in the sweep.** It is the proposal's automated-localization novelty claim, already executed and published. Must be cited and distinguished. Distinguishing grounds available: node cost, node count, drone emplacement, rubble vs ground. **Its frequency band and its achieved accuracy in metres were not obtained** — without those the distinction cannot be made quantitative. |
| Stewart, R. et al., drone-deployed geophones, **SEG Technical Program Expanded Abstracts 2016** | DOI **not located** in this sweep | **READ-FULL** (paper PDF extracted locally, 15,291 chars) | Drone-*landed* geophones using the spikes as landing legs; recorded traces match conventionally planted geophones; spike penetration up to ~20 mm | Establishes drone emplacement of seismic sensors as prior art. The ~20 mm penetration is **below** the geophone "well planted" threshold (≥40 mm), which is a usable technical distinction for the proposal. |
| Sudarshan, S. et al., "A Heterogeneous Robotics Team for Large-Scale Seismic Sensing" (**SeismicDart**, SeismicSpider), NSF award **IIS-1553063** | Venue/DOI **not pinned** in this sweep; PDF obtained | **READ-FULL** (PDF extracted locally, 14,215 chars) | "A dart-shaped wireless sensor that is planted in the ground when dropped from an unmanned aerial vehicle"; max 4 darts per flight; penetration depth and angle of deviation vs drop height across **7 soil types** (compression strength 0.056 kg/cm² river sand → 4 kg/cm² hard-packed field), 12 trials per point, drop heights 10/15/20/25 m; "**all drops from heights 20 m or more achieved the goals**" of <10° deviation and ≥40 mm penetration; impact velocity 21.1 m/s from 25 m (43 % of terminal velocity), 39 m/s from the FAA 122 m ceiling at Cd = 0.47; fidelity vs traditional geophone **ρ = 0.81–0.98, NRMSE 1.05–4.39 %** | Directly anticipates air-dropped seismic nodes, *with* the planting-quality characterisation the proposal would otherwise claim as its own. **Also the key data point on node position uncertainty**: Fig. 13 reports targeting accuracy from 24 darts commanded to the same GPS waypoint (6 sets × 4, with the UAV flying to a nearby waypoint between sets to cancel hover bias), mean marked by a diamond, σ and 2σ covariance ellipses. **The numeric scatter value appears only in the figure, not in the body text** — it must be read off the figure or obtained from the authors; I did not fabricate a value. This is the number that would substantiate or refute the proposal's ±3.5–5 m node-position-bounded accuracy claim. |
| Arosio, D. et al. — hand-placed microseismic array for survivor location on real rubble | DOI **10.3997/1873-0604.2010051** (*Near Surface Geophysics*, 2010) | **CITED-ONLY — received from a sibling agent, NOT independently verified by me.** DOI, limitations and framing are as reported to me; I did not retrieve the paper | Microseismic survivor-location array deployed by hand on actual rubble. Stated limitations: debris inhomogeneity; need for real-time response; **limited array extent** | **Reshapes the drone novelty claim, and favourably.** It establishes that the *array-on-rubble* concept is prior art (so the proposal cannot claim it), but its three stated limitations are precisely what drone emplacement plus a cheap dense mesh addresses: array extent is limited by hand-placement labour and cable runs, which air deployment removes. This is the cleanest "prior art names the gap we fill" citation in the sweep — **but it must be read first**, because its own accuracy figures and array size determine whether the proposal's ±3.5–5 m is an improvement or a regression |
| Geophone footstep detection and identification; TDoA with non-isotropic multilateration — IIT Delhi (Mukhopadhyay, Anchal, Kar) | DOIs not individually pinned | **READ-ABSTRACT** | Geophone-based footstep detection/identification; TDoA localization with non-isotropic multilateration | Indian academic capability directly adjacent to the proposal's method — a collaboration or citation asset, and simultaneously evidence that geophone TDoA on human-generated seismic signals is established work in India. |
| Seismic-sensing survey, **ACM Computing Surveys** (authors at IIT Ropar) | DOI **10.1145/3568671** — `dl.acm.org/doi/10.1145/3568671` returned HTTP 403 | **CITED-ONLY** | Survey of seismic sensing | Likely the best single citation for positioning the method field, and an Indian-authored one. **Unread** — do not characterise its contents in the proposal beyond its existence until retrieved. |
| Macintyre AG, Barbera JA, Smith ER — *Prehospital and Disaster Medicine* 2006;21(1):4–17, **PMID 16602260** | PMID 16602260 | **CITED-ONLY** (botwalled) | USAR entrapment/survival context | Carried over from sibling critique work. Not read in this sweep. |

**Method-side literature deliberately not re-derived here.** SO-TDOA (sign-only TDOA for dispersive damped concrete) and Kelvin-Voigt thin-plate damping are covered by sibling document C; they bear on whether TDoA works in rubble at all, which is C's territory, not this document's.

---

## Drone / air-deployed sensor nodes — does this exist already?

**Yes. Two independent demonstrated approaches, both verified READ-FULL, plus a decade-old lineage of UAV node-dropping for post-disaster wireless sensor networks.**

- **Drone-*landed* geophones** — Stewart et al., SEG 2016. The drone lands and its spike legs plant the geophone. Traces match conventionally planted geophones. Penetration up to ~20 mm.
- **Air-*dropped* darts** — SeismicDart (Sudarshan et al.). Dropped from a UAV in flight, up to 4 per sortie, characterised across 7 soils and 4 drop heights with 12 trials per point. All drops ≥20 m met the professional geophone planting standard (<10° deviation, ≥40 mm penetration). Signal fidelity against a traditional geophone ρ = 0.81–0.98.
- **SeismicSpider** — a hexapod companion in the same programme, for sensors that must be walked into position rather than dropped.
- **UAV node-dropping for post-disaster WSNs** dates to approximately 2012 in the literature, i.e. the general concept is old.

**And the array-on-rubble concept is itself prior art.** Arosio et al. 2010 (DOI 10.3997/1873-0604.2010051, **CITED-ONLY, received from a sibling agent and not independently verified here**) built a hand-placed microseismic survivor-location array on real rubble. Its stated limitations were debris inhomogeneity, the need for real-time response, and **limited array extent**. So the proposal's method is not new on rubble either — but those three limitations are a near-exact statement of what cheap air-dropped nodes exist to fix, which makes this the strongest "prior art names the gap" citation available. **Read it before relying on that framing**, since its own accuracy and array size decide whether the proposal improves on it.

**Consequence.** "We will deploy sensor nodes from a drone" is not novel and must not be claimed as such. What remains genuinely open, and is defensible:

1. **Rubble, not soil.** Every characterisation above is parameterised by *soil compression strength*. Collapsed structural debris is not soil: it is non-penetrable in large fractions, voided, rebar-laced, and dust-covered. **No characterisation of air-dropped node coupling onto rubble was located.** This is a real gap and a credible deliverable.
2. **Node count per sortie.** SeismicDart carries 4 per flight. A mesh of many tens of nodes is a different logistical and mechanical problem, and the proposal's mesh-scale claim lives here.
3. **Known-position-free operation.** Both prior systems care about *planting quality*; the proposal's accuracy is bounded by *knowing where the node landed*. The SeismicDart Fig. 13 targeting-accuracy result is the direct precedent and the direct threat — if its scatter is large relative to ±3.5–5 m, the proposal's error budget needs a node self-localization story, not just a GPS-waypoint story.

---

## Is "position uncertainty dominates TDoA" textbook knowledge?

**Yes. It is standard, and presenting it as a finding would damage the proposal's credibility.**

- **GDOP (geometric dilution of precision)** is *the* standard metric for how anchor/receiver geometry amplifies measurement error into position error. It is textbook in GNSS and in sensor-network localization alike.
- **Anchor position error is a routinely modelled term**, not an overlooked one. The localization literature explicitly treats it: "by taking into account the error in the anchor positions, a significant improvement in the localization accuracy can be achieved."

**How to use this correctly.** The statement "our accuracy is bounded by node position uncertainty rather than clock error" is a legitimate and valuable *engineering result about this specific system's error budget* — it tells the reviewer where the design effort went and why the time-sync requirement is modest. It is **not** a scientific contribution. Write it as an error-budget conclusion with GDOP cited as the standard framework, and the proposal gains rigour. Write it as a discovery and a reviewer will mark it as a basic-literature gap.

---

## USAR doctrine: All Quiet and responsive tapping

### Primary doctrine, verbatim

**FEMA National US&R Response System**, `fema.gov/pdf/emergency/usr/mod3_u3.pdf` — **READ-FULL**, text extracted locally (61,971 characters). This upgrades the project's earlier secondary-source-only record of the signal set to primary verbatim:

> "Hailing devices shall be used to sound the appropriate signals as follows:"
> "Cease Operations/All Quiet – l long blast (3 seconds)"
> "Evacuate the Area – 3 short blasts (1 second each)"
> "Resume Operations – 1 long and l short blast"

So **All Quiet is a commanded, signalled, site-wide state**, not an informal lull — which is what makes it a usable synchronisation window for a listening mesh.

On listening devices, same document (quoted in full in the status-quo section above): victims "must create a recognizable sound pattern"; devices are "able to cover larger search areas and **sometimes triangulate on victim position**"; ranges "acoustic – 25 feet, seismic – 75 feet." On the hailing method: "Personnel can inform victim of expected response."

**UK NFCC National Operational Guidance**, *Primary search: Unstable or collapsed structure* — **READ-FULL**, link state LIVE:

> "Around once per hour for a few minutes, all activity should cease to listen for sounds made by casualties"

### The duty-cycle estimate

The proposal's **~5–8 % duty cycle** is **consistent with doctrine but not established by it.** The NFCC text gives "around once per hour for a few minutes." Taken literally, "a few minutes" per hour is roughly 3–8 minutes in 60, i.e. **5–13 %**; the proposal's 5–8 % sits inside the lower part of that band. No doctrine document located specifies a *duration* numerically. The honest statement for the proposal is: *doctrine specifies approximately hourly All Quiet periods of "a few minutes" (NFCC); we assume 3–5 minutes per hour, giving a 5–8 % listening duty cycle.* Label it **[ASSERTED]**, derived from a quoted primary source — not **[MEASURED]**, and not attributed to a doctrine document as a stated figure.

### Secondary USAR training sources on tap counts

**READ-FULL as articles, but secondary to doctrine** — use for colour and practice, cite doctrine for authority:

- Firehouse: hailing — "ask the victim to tap an object 3 times"; localization procedure — "leave the sensor that has the greatest noise in place and move the remaining sensors."
- Fire Engineering: ranges 5–25 ft acoustic / 50–150 ft seismic; "up to six sensors"; spacing ≤25 ft, typically 15 ft. **Also contains the phrase "even the vibration of a heartbeat"** — note this: it is a training-article claim, not a vendor specification, and it is the likely origin of the heartbeat folklore the proposal is correcting. Sibling A establishes it is not physically supported. Cite it as *the misconception's source*, carefully, not as a capability claim.
- "The Hailing Search Method… an array of listeners deployed around the collapse site"; "potential victims are told to yell and knock on something solid between 3 and 5 times at the same time"; elsewhere "knock five times on something."

**Declared gap: no INSARAG primary text was obtained.** INSARAG Guidelines Vol. II Manuals B and C are named for hand-retrieval. The proposal should not quote or paraphrase INSARAG until they are read. Equally, the "between 3 and 5 times" instruction is currently **secondary-source only** — it should be found in a primary FEMA or INSARAG document before it is quoted in a faculty-signed proposal.

---

## Indian context: NDRF / NDMA and case history

**NDRF equipment baseline — READ-FULL.** The NDRF CSSR (Collapsed Structure Search and Rescue) equipment schedule, 123 items, includes "Life Detector Type II," "Rescue Radar," and "Victim Location Camera with Breaching System." The NDRF specification for **"Human Life Detector Type-I"** is a seismic/acoustic listening device: 1 Hz–3000 Hz, "not less than 6 sensors. 4/6 sensors," seismic sensor 1 Hz–300 Hz shock-resistant >1000 g, filters (high-pass 100 Hz, notch 50/60 Hz, low-pass 600 Hz), 6 seismic + 1 acoustic sensors, 2 headphones, 6 × 10 m cable spools, "SIGNAL DISPLAY LED Bar graph any 2 channels or sum of all channel, range 60 dB."

**This is the single most useful document for an India-funded proposal.** It is a Delsar-equivalent specification, and it contains **no automated-localization requirement of any kind** — the procurement baseline is an operator-interpreted instrument. That is a documented national capability gap, stated in the procuring agency's own words. "Life Detector Type-II" is the separate EM-field heartbeat class (500 m open air, claims discrimination of humans from animals and the dead) — a different modality, not a seismic competitor.

**NDMA guidelines — CITED-ONLY (titles and dates verified, full texts not read in this sweep):**
- *Management of Earthquakes*, April 2007 — contains the policy line "Zero tolerance to avoidable deaths due to earthquakes."
- *Medical Preparedness and Mass Casualty Management*, October 2007.

**NDRF structure:** raised 2006; 18 search-and-rescue teams of 45 personnel per battalion.

**Indian case history for motivation — READ-FULL (news reporting; treat as journalism, with dates):**
- **Delhi, Satya Niketan, 6 September 2026** — students' hostel collapse; at least 6–7 dead, up to 40 reported trapped; detection dogs used.
- **Delhi, Seemapuri, October 2026** — Delhi Fire Service with NDRF; 8 rescued.
- **Delhi, Mustafabad, April 2025** — 11 dead, approximately 22 trapped.
- **Surat, 2024** and **Bhiwandi, 2020** — building collapses.

For a proposal motivation section this is adequate and recent. Note that these are news reports: give each a date and attribute to reporting, and do not aggregate casualty figures across them into a single statistic.

**Indian academic asset.** IIT Delhi (Mukhopadhyay, Anchal, Kar) already publishes geophone footstep detection/identification and TDoA with non-isotropic multilateration; IIT Ropar authors wrote the ACM Computing Surveys seismic-sensing survey (DOI 10.1145/3568671, unread). Both are citation and collaboration assets, and both mean the method is not foreign to Indian reviewers — the proposal should assume a reviewer who knows this work.

---

## Could not access — exact URLs for hand-retrieval

| What is needed | Exact URL / identifier | Block state (verified by body, not status code) | Priority |
|---|---|---|---|
| **A vendor-authoritative, new-unit Delsar LD3 list price, date-stamped** | `https://www.savox.com/products/search-and-rescue-kits/delsar` and Con-Space distributor pages | Not retrieved as an authoritative price; all captured figures are auction/reseller/quote | **HIGHEST.** The cost-advantage claim is the proposal's strongest novelty axis and it currently rests on nothing citable. The project's old "~USD 15,000" figure is unconfirmed — do not use it. |
| **INACHUS GBSS: peer-reviewed paper, frequency band, and achieved accuracy in metres** | `https://inachus.eu/inachus-components` | **HTTP 403** (botwall) | **HIGHEST.** This is the prior art that most threatens the novelty claim. Without its accuracy figure the proposal cannot quantify how it differs. Try CORDIS (`cordis.europa.eu`, grant 607522) deliverables, and ICCS/NTUA publication lists. |
| **Arosio et al. 2010 full text** — array size, sensor count, achieved accuracy, and the verbatim "limited array extent" limitation | DOI **10.3997/1873-0604.2010051** (*Near Surface Geophysics*) | Not attempted by me — arrived from a sibling agent late. Likely Wiley/EAGE paywall | **HIGHEST (tied).** The proposal's strongest novelty axis (array extent) rests on this paper's own statement of its limitation, which I have only second-hand. Its accuracy figure also sets the bar the proposal's ±3.5–5 m must beat. |
| **INSARAG Guidelines Vol. II, Manual B and Manual C** (primary All Quiet / hailing text) | Named documents; no working URL captured | Not retrieved | **HIGH.** Doctrine authority for a proposal is INSARAG as much as FEMA, and the "3 to 5 times" tap instruction is currently secondary-source only. |
| **SeismicDart Fig. 13 numeric targeting scatter (σ, CEP) in metres**, and the paper's venue + DOI | PDF held locally; value is figure-only, not in body text | Figure not machine-readable; venue not pinned | **HIGH.** This is the direct precedent for the proposal's node-position error budget. Read it off the figure by hand, or email the authors (NSF IIS-1553063). |
| **ACM Computing Surveys seismic-sensing survey** (IIT Ropar) | DOI **10.1145/3568671** — `https://dl.acm.org/doi/10.1145/3568671` | **HTTP 403** (ACM DL blocks scripted access) | **MEDIUM-HIGH.** Best single positioning citation, and Indian-authored. Try an author preprint. |
| **Stewart et al. SEG 2016 DOI** | PDF read in full; DOI not located | — | MEDIUM. Needed for a correct reference entry. |
| **Con-Space / SearchCam, Bio-Rescue, Rescue Technology product specs and prices** | Vendor sites; `https://allsafeindustries.com` **HTTP 403**; `https://safewarecontracts.com` **ECONNREFUSED**; `https://tempest.us.com` **HTTP 404** | Blocked / dead | MEDIUM. Completes the competitive table; none is likely to change the verdict. |
| **Springer chapters** | `10.1007/978-3-032-13612-1_44`, `10.1007/978-3-642-31837-5_44`, `10.1007/s10514-020-09902-3` | **HTTP 303 botwall** (link.springer.com → idp.springer.com) | MEDIUM |
| **MDPI article pages** | `mdpi.com` (various) | **HTTP 403** — workaround found: `mdpi-res.com` PDF mirror | LOW (worked around) |
| **PMC articles** | `pmc.ncbi.nlm.nih.gov/articles/...` | **reCAPTCHA wall.** Note the redirect trap: `ncbi.nlm.nih.gov/pmc/articles/PMCxxxx` → 301 → `pmc.ncbi.nlm.nih.gov/pmc/articles/...` → **404**; the correct form is `pmc.ncbi.nlm.nih.gov/articles/...` | LOW |
| **Macintyre/Barbera/Smith 2006 full text** | PMID **16602260** | Botwalled | LOW |
| **NDRF site** | Use `https://www.ndrf.gov.in` — **not** `https://ndrf.gov.in` (SSL: host not in cert altnames, `DNS:*.ndrf.gov.in`) | Resolved | — (recorded for reuse) |
| **US11063673 patent** | USPTO PDF has **no text layer** (27 characters extracted — scanned image). Use `https://patents.google.com/patent/US11063673B2/en` | Resolved | — (recorded for reuse) |

---

## What I could be wrong about

Stated plainly, because the proposal is faculty-signed.

1. **My INACHUS characterisation rests on project and component descriptions, not a peer-reviewed paper.** The quoted automated-detection-and-positioning language is from project material (**READ-ABSTRACT**), and `inachus.eu/inachus-components` was 403. I do **not** know GBSS's frequency band, its sensor count, its achieved localization accuracy, or whether the "automatically detected and positioned" capability was validated in a field trial or only demonstrated in a lab. All of those could *either* strengthen the proposal (if GBSS was lab-only, low-node-count, or low-accuracy) *or* kill the novelty claim outright (if it was field-validated at metre accuracy). **The verdict "ALREADY PUBLISHED" on the automated-localization axis is therefore my reading of promotional-grade text.** It is the right conservative call for proposal-writing, but it must be confirmed before the proposal commits to how it distinguishes itself. This is the largest single uncertainty in this document.
2. **No INSARAG primary text was read.** All doctrine quotes are FEMA and UK NFCC. If INSARAG's hailing protocol differs materially — a different tap count, a different All Quiet cadence, or an explicit multi-sensor triangulation procedure — my doctrine section is incomplete and possibly skewed toward US practice. For an Indian proposal INSARAG is arguably the more relevant authority (NDRF is INSARAG-classified), so this gap matters more than its position in the priority list suggests.
3. **The "3 to 5 times" / "tap 3 times" / "knock five times" instructions are secondary-source only.** Firehouse and Fire Engineering are credible trade sources but they are not doctrine. The *existence* of a commanded response protocol is primary-sourced (FEMA: "Personnel can inform victim of expected response"); the *specific number* is not. Do not put a tap count in the proposal attributed to doctrine.
4. **Every price in this document is secondary, and the spread is too wide to support a cost claim.** USD 2,000 to USD 28,500 for nominally the same product family. I obtained no vendor list price. The "$5.00 AUD" page is almost certainly a placeholder but I did not confirm that with the vendor. **Any cost-ratio claim built on this table is unsafe.**
5. **The 5–8 % duty cycle is my arithmetic on the phrase "a few minutes," not a doctrine figure.** If a reviewer reads "a few minutes" as 10 minutes, the duty cycle is ~17 % and any power/energy budget keyed to 5–8 % is wrong by a factor of two to three. The proposal should carry the assumption explicitly and show sensitivity to it.
6. **The SeismicDart targeting scatter — the number most load-bearing for the ±3.5–5 m claim — I do not have.** It is in a figure I could not read numerically. I deliberately did not estimate it. If that scatter turns out to be, say, several metres at 2σ, the proposal's node-position error budget is the weak point of the whole design, not a solved detail.
7. **"Nobody has characterised air-dropped node coupling onto rubble" is an absence-of-evidence claim.** I searched in English. Such work could exist in a defence venue, in a non-English literature, in EU project deliverables I could not reach (including INACHUS's own), or in grey/agency literature. Claim it as "no such characterisation was located in a systematic search" rather than "none exists."
8. **I did not retrieve Con-Space/SearchCam, Bio-Rescue or Rescue Technology specifications at all.** My statement that *no* commercial seismic locator offers automated localization is based on Delsar, Leader and the NDRF specification. It is a strong pattern across three independent sources including a national procurement spec, but it is not exhaustive. One of the unretrieved vendors could offer automated positioning.
9. **The Indian case-history items are news reports read in this sweep, not official post-incident reports.** Casualty and trapped-person counts in early reporting are frequently revised. Each should be re-checked against an official source before it appears in a funding proposal, and none should be presented as a precise figure.
10. **The Vibrock correction is a warning about my own earlier classification.** I had Vibrock V901 recorded as a USAR competitor; it is a construction vibration monitor. Per project convention (if one link tag is wrong, re-check everything verified the same way), the rest of the competitive table deserves the same scepticism — it was assembled by the same process, and only Delsar, Leader and the NDRF spec were verified from primary documents.
11. **Arosio et al. 2010 I did not verify at all.** The DOI, the rubble deployment and the three limitations were handed to me by a sibling agent as my session was closing, and I have built the proposal's strongest novelty recommendation (array extent) on top of them. That is a single-source, second-hand foundation for the most load-bearing claim in this document. If the paper's limitation is phrased differently, or if its array was in fact large, or if its reported accuracy is better than ±3.5–5 m, the recommendation changes. **Read it before the proposal is drafted around it.**
12. **"Position uncertainty dominates TDoA is textbook" I assert from GDOP's standard status and from anchor-error terms appearing routinely in the localization literature.** I did not identify a specific textbook chapter and page. The claim is safe as a framing instruction (cite GDOP, don't claim discovery) but if the proposal wants a citation for it, one still needs to be found.

---

## Orchestrator verification, 2026-10-08

Checked by the orchestrating session after hand-back, independently of B. Two load-bearing
claims were re-tested because the whole novelty argument turns on them.

**1. Arosio's "limited array extent" — CONFIRMED by a third source.** B received this
second-hand from a sibling agent and flagged it as the document's most load-bearing unread
claim. An independent search returned the paper's own abstract language naming its three
challenges: *"the inhomogeneity of the debris pile, the need for a real-time response and the
**limited spatial extension of the sensor array**."* Also confirmed from the same abstract:
accuracy *"within the limit of the seismic resolution"*, and *"reduces the investigation time
taken by current seismic S&R systems by a factor of three"* - method is energy focusing via
cross-correlation and semblance operators. Full citation confirmed: **Near Surface Geophysics
8(6):623-633 (2010)**. A ResearchGate copy of *A microseismic approach to locate survivors
trapped under rubble* exists and is the cheapest hand-retrieval route.

So the strongest novelty axis (array extent lifted by air deployment) now rests on a
limitation verified in two independent places, not on one agent's relay. **Still
READ-ABSTRACT, not READ-FULL** - the accuracy figure in metres is not yet in hand, and it sets
the bar that +-3.5-5 m must beat.

**2. INACHUS GBSS - verdict SOFTENED to UNRESOLVED.** B's own caveat was right to doubt it.
A targeted search found the CORDIS project record (FP7 607522, 20 partners, Jan 2015 - Dec
2018, confirmed) but **returned no peer-reviewed paper, no accuracy figure, and no technical
description of the GBSS subsystem.** The "automatically detected and positioned" language
remains promotional-grade and unverified at the level of a result.

**How the proposal must treat this:** cite INACHUS as prior art that stated the same
automation goal, and do **not** claim automated knock localization as novel - B's conservative
read is the safe one for a reviewer. But equally, do **not** write that INACHUS *achieved*
metre-accuracy automated localization; nothing located supports that either. The honest line
is that the goal is published and the validated result is not publicly established. Keeping
this distinction protects the proposal both ways.

**Unchanged and accepted from B:** the retarget is status quo (FEMA primary doctrine,
READ-FULL); drone deployment onto *soil* is published (Stewart SEG 2016; SeismicDart,
READ-FULL); GDOP is textbook and must be written as an error-budget conclusion, never a
finding; the ~USD 15,000 Delsar figure is **unconfirmed and must not be used**; the 5-8 %
duty cycle is [ASSERTED] with no doctrinal duration behind it.
