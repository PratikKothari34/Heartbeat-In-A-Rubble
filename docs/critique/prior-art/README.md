# docs/critique/prior-art/ - literature sweep, 2026-10-08

Three agents, one assigned area each, briefed to find **what has already been published** and to
report access state honestly rather than characterise anything they could not read. Run after the
2026-10-07 adversarial critique, and amending it.

**Read `../07-verdict.md` section 9 first** - it carries the consolidated amendment. These files are
the evidence behind it.

| File | Area | Headline |
|---|---|---|
| `A-cardiac-seismic.md` | Cardiac source force, BCG literature, novelty of the negative result | **The 1-4 N assumption is MEASURED**, three instruments, 70 years apart |
| `B-usar-systems.md` | USAR listening systems, FEMA/NDRF doctrine, drone-deployed sensors, Indian context | **The retarget is doctrine, not novelty**; drone seismic deployment already published |
| `C-propagation-modeling.md` | Propagation, coupling, sensor noise, CRLB - every parameter validated row by row | **The SM-24 datasheet has no noise spec**; coupling resonance contradicted |

## What changed, in order of consequence

**1. The kill is confirmed and better evidenced.** The cardiac source force is no longer assumed:
3.7 N +-0.53 (Starr et al. 1939, n=7), 4.06 N +-1.53 (Inan 2009, Stanford, n=26+, range
0.63-10.95 N), 2 N_pp (Ashouri et al. 2016, Kistler force plate). The worst single healthy subject
costs **+8.75 dB**, moving the deficit to **38-60 dB**. Nothing recovers 38 dB. The "what if the
force is really 20-40 N" escape hatch is now **closed by measurement**. Pathological hearts measure
**0.94-1.05 N** - ~12 dB *below* the healthy mean, so a crush-injured hypothermic survivor is
plausibly weaker than the critique assumed.

**2. The novelty claim moved.** This is the biggest change for the proposal.

- Tapping/voice is **FEMA doctrine**, verbatim: "Victim must create a recognizable sound pattern."
- Automated knock localization was the stated goal of **INACHUS** (EU FP7 607522, 20 partners).
  *No peer-reviewed accuracy result was located* - so do not claim it as novel, and do not assert
  INACHUS achieved it either.
- Drone deployment of seismic sensors is published: **Stewart et al., SEG 2016** (drone-landed
  geophones) and **SeismicDart** (air-dropped, rho = 0.81-0.98 vs planted geophones) - but both
  characterise **soil**, not rubble.
- A seismic array on rubble is published: **Arosio et al. 2010**.
- "Node position dominates TDoA" is **textbook GDOP**. Write it as an error-budget conclusion;
  presenting it as a finding would read as a literature gap.

**Surviving defensible novelty, strongest first:** (0) **array extent** - Arosio names "the limited
spatial extension of the sensor array" as its own limitation and hand placement is what causes it;
(1) **coupling onto rubble rather than soil** - unmeasured by anyone, and the same gap as the
reinstated coupling worry below; (2) **the cardiac bound itself**, publishable as a negative result;
(3) node count / cost at mesh scale; (4) the **NDRF Type-I** spec's complete absence of an
automated-localization requirement - a capability gap in the procuring agency's own words.

**3. Three numbers in the critique were wrong.**

| Was | Is | Source |
|---|---|---|
| Coupling resonance 500 Hz - 67 kHz | **100-500 Hz** | Krohn 1984, DOI 10.1190/1.1441700 |
| Footstep anchor 19 Hz -> 36.5 ug | **40 Hz -> 76.9 ug** | Ekimov & Sabatier, *JASA* 120(2):762, **full text 2026-10-08** (the interim "17 Hz -> 32.7 ug" was a mis-citation; see `C` row 2) |
| SM-24 "0.1 ug/rtHz, vendor-verify it" | **No vendor noise spec exists.** Computed element floor 0.003-0.005 ug/rtHz | SM-24 brochure, re-extracted |

The coupling correction **partially reinstates `01`'s struck condition C4**: our claimed floor was
the literature's ceiling, so a 100 Hz resonance sits only 1.25x above an 80 Hz tap - in band,
distorting amplitude *and phase*. Margin 1.3-6x, not 6-800x. Worst for free-laid nodes on fractured
debris, which is exactly what drone deployment produces.

The noise correction resolves `00b` section G **in the project's favour, for the opposite reason
than expected**: the figure cannot be vendor-verified because it was never a vendor figure, but the
element is 23-30x quieter than assumed, so the +23/+41 dB tap margin holds. **The preamplifier, not
the element, is now the number to specify** (12-16x margin at 4 nV/rtHz; margin vanishes only near
50 nV/rtHz).

## Still unmeasured - the highest-value bench work

**Tap force and tap spectrum.** The 50-300 N / 60-80 Hz figures underpinning every margin in `07`
have **no source**. The nearest literature anchors are destructive (karate chop ~2,800 N) and were
explicitly declined rather than laundered as measured. Measure these before trusting any margin.

**Air-dropped node coupling onto debris.** Nobody has characterised it.

## Citations that must appear in the proposal and currently do not

- **Arosio et al. 2010**, *Near Surface Geophysics* 8(6):623-633, DOI 10.3997/1873-0604.2010051 -
  closest prior art. Accuracy "within the limit of the seismic resolution"; 3x faster than incumbent
  systems; energy focusing via cross-correlation and semblance.
- **Sabatier & Ekimov 2008**, Proc. SPIE 6963, 69630V, DOI 10.1117/12.785235 - already a
  signal-equals-noise range bound for footsteps. This project's method has a published ancestor.
- **HeartQuake** (Park et al. 2020, DOI 10.1145/3411843) - recovers full ECG morphology through a
  mattress **from an SM-24 geophone element**, the same part this project selects. Must be cited and
  distinguished (contact-coupled through bedding, not metres of rubble), because a reviewer who finds
  it unaided will read it as contradicting the kill.
- **Krohn 1984**, DOI 10.1190/1.1441700 - coupling. Also the real source of "lighter couples
  better," which is **not** a project finding.

## Reading the access tags

Every claim in these files is tagged **READ-FULL** (full text read), **READ-ABSTRACT** (abstract
only), or **CITED-ONLY** (known via another source). This matters: **four of the most load-bearing
citations are READ-ABSTRACT** - Arosio's 200-600 m/s rubble velocity, the 3 um/s anchor, Krohn's
100-500 Hz window, and the 17 Hz footstep peak. **Updated 2026-10-08: three of the four are now full
text; the 17 Hz peak was overturned (real value 40 Hz) and Krohn alone remains unverified.** The hand-retrieval list with exact URLs and verified
block states is at the end of `C-propagation-modeling.md`, priority-ordered.

**Hand-retrieve those four before a faculty signature.** An abstract is enough to correct a number
internally; it is not enough to defend one in a funded proposal.

## Terminology fix

**"Force-ratio scaling" is not a standard term.** The method is **linear transfer-mobility scaling**
(FTA ground-borne vibration method; ASTM/FHWA impulse-response mobility spectrum). Elastodynamics is
LTI, so response amplitude is linear in source force - that is *why* it works. Two errors to keep
avoiding: scaling by **energy** instead of force (a factor-2 dB error), and invoking **seismic
moment**, which is defined for internal sources, not a body pressing on a surface.
