> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> *Laboratory measurements of velocity and attenuation in sediments*, OSTI technical report.
> Source PDF deleted after conversion (`*.pdf` is gitignored project-wide; third-party papers
> are not ours to redistribute).
>
> Listed in `docs/research/BUDGET/01-literature.md` velocity table row 3 as **HELD** with
> **no figure quoted from it** - it was held as corroboration for the unconsolidated-media
> velocity/attenuation bracket, never read. The bracket the project actually cites comes from
> **USGS SIR 2023-5061** (200-1000 m/s above the water table), which has its own extract.
>
> Read this before using it as a second source: it is a *laboratory* measurement on sediments,
> not rubble, so it shares the medium-mismatch caveat that applies to every velocity figure
> in this project.

UCRL-JRNL-205155
Laboratory Measurements of
Velocity and Attenuation in
Sediments
M. Prasad, M. A. Zimmer, P. A. Berge, and B.
P. Bonner
July, 2004
Society of Exploration Geophysicists, Tulsa
UCRL-JRNL-205155

2
DISCLAIMER
This document was prepared as an account of work sponsored by an agency of the
United States Government. Neither the United States Government nor the University of
California nor any of their employees, makes any warranty, express or implied, or
assumes any legal liability or responsibility for the accuracy, completeness, or
usefulness of any information, apparatus, product, or process disclosed, or represents
that its use would not infringe privately owned rights. Reference herein to any specific
commercial product, process, or service by trade name, trademark, manufacturer, or
otherwise, does not necessarily constitute or imply its endorsement, recommendation, or
favoring by the United States Government or the University of California. The views and
opinions of authors expressed herein do not necessarily state or reflect those of the
United States Government or the University of California, and shall not be used for
advertising or product endorsement purposes.
This work was performed under the auspices of the U.S. Department of Energy
by University of California, Lawrence Livermore National Laboratory under
Contract W-7405-Eng-48.

3
Laboratory measurements of velocity and attenuation in sediments
M. Prasad1, M. A. Zimmer1, P. A. Berge2, and B. P. Bonner2
1Geophysics Department, Stanford University, Stanford, CA 94305. E-mail:
manika.prasad@stanford.edu, zimmer@pangea.stanford.edu.
2Earth Science Division, Lawrence Livermore National Laboratory, 7000 East Ave.,
Livermore, CA 94550. E-mail: bonner1@llnl.gov, berge1@llnl.gov.
ABSTRACT
Laboratory measurements are required to establish relationships between the physical
properties of unconsolidated sediments and P- and S-wave propagation through them.
Previous work has either focused on measurements of compressional wave properties at
depths greater than 500 m for oil industry applications or on measurements of dynamic
shear properties at pressures corresponding to depths of less than 50 m for geotechnical
applications. Therefore, the effects of lithology, fluid saturation, and compaction on
impedance and P- and S-wave velocities of shallow soils are largely unknown. We
describe two state–of–the–art laboratory experiments. One setup allows us to measure
ultrasonic P-wave velocities at very low pressures in unconsolidated sediments (up to
0.1 MPa). The other experiment allows P- and S-wave velocity measurements at low to
medium pressures (up to 20 MPa). We summarize the main velocity and attenuation
results on sands and sand – clay mixtures under partially saturated and fully saturated
conditions in two ranges of pressures (0 – 0.1 MPa and 0.1 – 20 MPa) representative of
the top few meters and the top 1 km, respectively. Under hydrostatic pressures of 0.1 to
20 MPa, our measurements demonstrate a P- and S-wave velocity-dependence in dry
sands around a fourth root (0.23 –0.26) with the pressure dependence for S-waves being
slightly lower. The P- velocity-dependence in wet sands lies around 0.4. The Vp-Vs and
the Qp-Qs ratios together can be useful tools to distinguish between different lithologies
and between pressure and saturation effects. These experimental velocities at the
frequency of measurement (200 kHz) are slightly higher that Gassmann’s (Gassmann,
1951) static result. For low pressures under uniaxial stress, Vp and Vs were a few
hundred meters per second with velocities showing a strong dependence on packing, clay
content, and microstructure. We provide a typical shallow soil scenario in a clean sand
environment and reconstruct the velocity profile of such a sediment packet.

4
INTRODUCTION
Seismic velocities and attenuations collected in the field with, for example, reflection,
refraction, and cross-hole surveys serve as valuable constraints on subsurface lithology,
porosity, permeability, and fluid saturation. Until recently, the measurement resolution of
seismic velocities in the shallow subsurface had limited the use of the complete power of
seismic attribute analysis in shallow soils. Recent advances in field techniques for
seismic measurements in shallow soils (e.g., Bachrach et al., 1998, 2002 (this volume);
Baker et al., 1999; Carr et al., 1998; Steeples et al., 1999) as well as the development of
seismic cone penetration tests (SCPT) and other improved geotechnical methods (e.g.,
Crouse et al., 1993; Boulanger et al., 1998) have begun to permit the application of
seismic attribute analysis to shallow soils. Unfortunately, the laboratory studies required
for establishing relations between the physical properties of the soils and their seismic
properties have not been extended to the low pressures analogous to these shallow depths,
so the effects of lithology, fluid saturation, and compaction on seismic (P- and S-wave)
properties of shallow soils are largely unknown.
Interpretation of shallow seismic data requires knowledge about P- and, to a lesser
extent, S-wave propagation in sediments at low pressures. A wealth of geotechnical
literature exists in measurements of shear modulus at low pressures (e.g., Santamarina et
al., 2001). Often, these measurements lack P-wave information, which is crucial for field
seismic studies. In geophysical literature, the focus has been mainly for oil industry
application. Thus, the effects of physical properties and fluid content on the seismic
properties of sedimentary rocks have been studied extensively at higher pressures using
ultrasonic measurements and other laboratory techniques (e.g., Domenico, 1976; Cheng,
1978; Han et al., 1986; Wilkens et al., 1986; Knight and Nolen-Hoeksema, 1990; Vernik
and Nur, 1992; Green et al., 1993; Prasad and Manghnani, 1997). Interpretation methods
in common use for seismic field data have been developed for oil industry applications
(e.g., Wyllie et al., 1956; Kuster and Toksöz, 1974). They are not optimized for the
shallow depths and unconsolidated materials of environmental or engineering
applications. P- and S-wave laboratory data collected for soils at low-pressure conditions
appropriate to the near surface are sparse in the literature. Although laboratory data sets
are available in the exploration geophysics, marine geophysics, and soil mechanics
literature (e.g., Rao, 1966; Domaschuk and Wade, 1969; Domenico, 1976; Hamilton and
Bachman, 1982; Prasad and Meissner, 1992; Santamarina et al., 2001), few studies

5
(Hamilton and Bachman, 1982; Zimmer et al., 2000; 2002a; Prasad, 2002) include both
compressional and shear wave velocity measurements as a function of pressure at the
extremely low pressures representing the shallow subsurface. Relevant laboratory
measurements of soil properties will enable us to develop new interpretation techniques
for seismic field data for environmental and engineering applications.
To this end, we describe state–of–the–art laboratory experiments involving the
measurement of ultrasonic velocities at low pressures in unconsolidated sediments and
summarize the main velocity results. The on-going experiments at Stanford University
and Lawrence Livermore National Laboratory (LLNL) were developed to make accurate
measurements of compressional-wave (Vp, Qp) and shear-wave (Vs, Qs) velocities and
attenuations in highly-attenuating soils at low pressures (e.g., Aracne-Ruddle et al., 1998;
1999; Bonner et al., 1999a, 2000, 2001; Zimmer et al., 2002a; 2002b; Prasad, 2002). The
data presented here include LLNL uniaxial measurements on dry, saturated, and partially-
saturated sands and sand-clay mixtures made at pressures below approximately 0.1 MPa;
and Stanford hydrostatic measurements made on dry and water-saturated sands at
pressures from 0.1 MPa to 20 MPa. Also presented here are velocity – pressure
transforms developed from the Stanford data for predicting Vp and Vs. Methods
developed from the LLNL data for relating velocities to lithology are described elsewhere
(for example, Bertete-Aguirre and Berge, 2002). The LLNL and Stanford ultrasonic
velocity measurements for unconsolidated soils at low stresses confirm recent field
observations of extremely low seismic velocities in shallow soils (e.g., Bachrach et al.,
1998; Carr et al., 1998; Steeples et al., 1999). These experimental results should allow for
the development of empirical and theoretical models that will permit more accurate
inversions of shallow seismic data for the physical properties and fluid content of soft
soils (e.g., Bertete-Aguirre and Berge, 2002; Berge and Bonner, 2002). Such seismic
interpretation methods can help guide effective in situ environmental remediation and
foundation engineering.
EXPERIMENTAL METHODS
Laboratory experiments under well-controlled conditions allow us to understand the
physics of wave propagation in sediments and to develop predictive empirical relations. It
has been standard geophysical laboratory practice to conduct such experiments on rocks
typically at 1 MHz frequency under high confining pressures. Considerable design is

6
required to modify such experiments to overcome experimental challenges and simulate
shallow soil conditions in the laboratory. For example,
1. Very low pressures must be maintained in experiments to simulate the in situ
conditions of shallow soils.
2. Experimental design should avoid impedance mismatch between standard high-
impedance acoustic transmitters and low-impedance soils. Thus, the commonly
used high-impedance metal transducer plates need to be replaced with plates
made from low impedance materials.
3. Maintain high signal amplitude and high signal-to-noise ratio: Since
unconsolidated sediments are highly attenuating, high signal energy is necessary
to propagate elastic waves through them. Using lower frequencies reduces
attenuation and produces a higher energy signal.
We report here two different types of equipment to simulate very low pressures and
generate a high signal output to propagate through unconsolidated materials. One
experiment (called the LLNL experiment) was designed to measure ultrasonic velocities
in sediments at dry, fully and partially saturated conditions under uniaxial loads up to 0.1
MPa. The second experiment (called the Stanford experiment) was designed to measure
velocities in sediments at dry and at fully saturated conditions under confining pressures
up to 20 MPa. Special care was taken to ensure generation of interpretable signals at low
pressures of 0.1 MPa.
The LLNL experimental setup
In the Experimental Geophysics Laboratory at LLNL, we used the pulse transmission
technique (Sears and Bonner, 1981) to measure ultrasonic compressional and shear wave
velocities for dry and fully saturated sediments. We also measured velocities in sand
samples with various degrees of partial saturation (Bonner et al., 2001).
Measurements were made on 4.49 cm long cylinders with 4.7 cm diameter at room
temperature and at pressures between about 0.01 and about 0.1 MPa to simulate the top
few meters of the subsurface. In order to obtain good ultrasonic signals at these low
pressures, the transmitting transducer was driven with unusually high voltages,
approaching the dielectric breakdown. The transducers were also operated at frequencies
at the low end of the available range, from about 100 to 500 kHz. A low noise, high-gain
preamplifier was needed and extensive signal averaging was used to improve the signal-
to-noise ratio. High-insertion-loss sample containers were required to suppress arrivals

7
that travel around the sample to obscure true arrivals, to make it possible to detect shear
waves in unconsolidated samples at low pressures. The sample containers provided over
100 dB insertion loss to control leakage of ultrasound, by using geometric constraints to
suppress low frequencies and material selection to attenuate high frequencies (Bonner et
al., 1999b). The sample assemblies were closed with latex membranes that transmitted
sound from the transducer and contained the soil mixture. Accuracy (= repeatability of
measurements) was limited to 20% at the lowest stresses near 1 psi (0.007 MPa), but
improved with signal amplitude to about 3% for compressional (P) waves and 10% for
shear (S) waves at higher stresses. Precision in timing the arrivals (= uncertainity of first
arrival picks) was about 1% for P and 2 to 5% for S arrivals in most cases. Sample length
change was less than 0.1% at the highest pressures and thus was considered negligible.
Details of the experimental procedures are given in Aracne-Ruddle et al. (1999).
Up to several meters of overburden were simulated by applying low uniaxial stress up
to about 0.1 MPa to the sample using a pneumatic system. Although the sample sleeve
was not perfectly rigid, the internal stress in the sample approximately corresponded to
the uniaxial strain condition. Pore fluid pressures, applied using a regulated gas tank
(Figure 1), could be increased beyond the sample bubble pressure to expel water and
produce partial saturation. Tensiometers were used to measure the pressure in the
continuous aqueous phase when the sample was partially saturated. The difference
between applied and water-phase pressure is the capillary pressure. Results of LLNL
measurements for some samples are presented later in this chapter.
The Stanford experimental setup
The apparatus developed in the Rock Physics Laboratory at Stanford University used
pulse transmission to measure the ultrasonic P and S velocities and attenuations of
unconsolidated sands at hydrostatic pressures from 100 kPa to 20 MPa. Zimmer et al.
(2000; 2002a) have described details of the experimental setup; the main features are
given here. The apparatus consists of a sample holder (Figure 2a) that is placed into a
pressure vessel (Figure 2b) capable of producing confining pressures of up to 20 MPa.
The samples are 3.8 cm in diameter and about 3 cm in length. The sample holder consists
of two end caps that contain the ultrasonic transducers and that are supported in a steel
frame. The transducers were constructed with lower (200 kHz) than traditional ultrasonic

8
(1 MHz) frequency piezoelectric crystals and with low-impedance face plates made out
of a glass-filled polycarbonate in order to maximize the elastic wave energy propagated
through the sample. The sample holder was also designed to be disassembled and
reassembled easily, and can be placed in the pressure vessel with minimal disturbance.
These features were necessary in order to permit consistent sample preparation so as not
to obscure the effects of the textural variations of the sands on the ultrasonic
measurements. With this arrangement we were able to get interpretable shear wave
signals through saturated samples at pressures as low as 100 kPa. An error analysis that
took into account errors in the length measurements, the measurement of the delay times,
and ambiguities in the pick of arrival times gave error estimates of about 2% for the Vp
values, and about 4% for the Vs values over the entire pressure range (Zimmer et al.,
2002a).
The static strain on the sample was registered using three axial gauges that measured
the length change between the end caps and one circumferential gauge that measured the
change in the circumference of the middle of the sample. The axial measurements
allowed us to determine accurately the length of the sample and to detect any tilting of
the end caps relative to each other. The circumferential gauge allowed us to make better
estimates of the volume and porosity of the sample, as it told us how much the sample
deviated from a purely cylindrical shape.
The next section of this paper describes some of the LLNL and Stanford samples, and
following sections summarize and discuss some measurement results.
SAMPLES
The sediments used in both the LLNL and the Stanford experiments were made
artificially in order to study the relations between sediment texture (that is, porosity,
composition, and compaction) and its seismic properties under well-defined and
reproducible conditions. In the LLNL experiments, sand and sand-clay mixtures were
measured. The Stanford experiments were made on natural sands. Both experiments were
first made to understand the physical processes in sediments. Future research will
concentrate on effects of fabric differences between artificial samples and natural soils.

9
LLNL sand-clay and sand samples
The artificial sediment samples that LLNL made were fabricated from Ottawa sand
mixed with a swelling clay. The sand comes from a quarry near the city of Ottawa,
Illinois and is Middle Ordovician in age. It is composed entirely of well-rounded quartz
grains (Domenico, 1976). The sand was sieved to a median grain diameter of 273 m m,
with grain sizes ranging from 74 to 420 m m. The clay was Wyoming bentonite, a sodium
montmorillonite from Wyoming that is a swelling smectite. The clay was equilibrated in
a 100% humid atmosphere for seven days before sample preparation, in order to achieve
reproducible water content. The clay content in the sand-clay samples was 1 to 40 percent
3
by mass. Bulk density ranged from about 1400 to 1700 kg/m , where the lowest density
corresponded to the sample having 40% clay by mass and pure sand samples had
densities of about 1700 kg/m3. We found that the packing affected measured velocities
and their load dependence. We were able to achieve reproducible results using a hand-
held brass weight that fit snugly in the sample holder. Sample preparation and
composition are discussed in detail in Aracne-Ruddle et al. (1999) and Bonner et al.
(2001).
Stanford sand samples for hydrostatic experiments
The measurements collected with the hydrostatic apparatus at Stanford were all made
on samples of the Santa Cruz aggregate, a fine-grained, well-sorted, angular quartz sand
from Santa Cruz, California. We prepared water-saturated samples first sliding the jacket
over the lower end cap and then filling it with water. The sand was then poured slowly
into the water and was stirred slightly to allow any air bubbles to escape and to level off
the top of the sample. The upper end cap was then slid into the jacket above the sample
until it just rested on the top of the sand, so the sand was not pre-compacted. The sample
holder was then assembled and placed into the pressure vessel. To ensure repeatability
and yet maintain high initial porosity, dry samples were prepared by air pluviating the
sand into the jacket, and then leveling off the top by placing a 160 g aluminum weight on
top of the sand about 20 times.

10
Once the sample holder was placed in the pressure vessel, measurements were made
at regular pressure steps as the pressure was cycled through one to five pressure cycles,
with each cycle peaking at a slightly higher pressure up to 20 MPa. The measurement
results from two water-saturated sand samples and two dry sand samples are presented in
the results section of this paper. Typical waveforms for P- and S-waves in a sand sample
at two pressures (0.05 and 20 MPa) are shown in Figures 3a – d.
RESULTS
Vp and Vs results for sands and sand-clay mixtures from the LLNL experiments
Figures 4a and 4b present LLNL results for Vp and Vs with respect to pressure for
dry sands and sand-clay mixtures. The pressures are equivalent to about the top 5 m of
the subsurface. Differences in packing and clay content control the measured velocities.
Figure 4c shows velocities vs. clay content for samples packed in the same way, for
measurements made at about 0.1 MPa. Clay content is shown schematically below the
plot in Figure 4c. We see in Figure 4c that although Vs decreases monotonically with
increasing clay content, Vp initially increases as clay causes sand grains to stick together
and fills dry pores. Then, Vp decreases with increasing clay content when the amount of
clay is enough to form a continuous clay matrix through the sample. Similar behavior has
been observed for sand-clay mixtures at 10 to 50 MPa (Marion et al., 1992). Vs does not
show the same behavior. Apparently, the clay does not impede sliding between grains.
Table 1 shows velocity as a function of saturation for Ottawa sand samples. The
water content was obtained from the water retention curve (Bonner et al., 2001). Velocity
results and related uncertainties are described in detail elsewhere (Bonner et al., 1997,
1999a, 2000, 2001; Aracne-Ruddle et al., 1998, 1999; Berge et al., 1999). Our main
findings are that the microstructure controls the velocities; the velocities are low, a few
hundred m/s in dry samples, with Vp values being about twice the Vs values; velocities
and amplitudes depend on the amount and distribution of fluid in saturated and drained
samples; and the velocity gradients at the lowest pressures are strongly influenced by
grain packing (Figure 4). Comparison of our laboratory velocity results to available

11
seismic reflection and refraction data (e.g., Crouse et al., 1993; Taylor and Wilson, 1997;
Bachrach et al., 1998; Boulanger et al., 1998; Steeples et al., 1999) showed agreement
between velocities measured in the lab and field for soils of similar types, at lab pressures
equivalent to the appropriate depth for the field measurements.
Vp and Vs results for sands from the Stanford experiments
Figure 5 shows the Vp and Vs results for four samples of the Santa Cruz aggregate
tested in the Stanford hydrostatic apparatus. Details of our results are described in
Zimmer et al. (2002a; 2002b). The most important point relevant to shallow seismic
applications is that the velocity – pressure dependence can be described for the S-waves
by a fourth-root relation over the entire pressure range from 100 kPa to 20 MPa, while
the P-wave dependence is closer to a fifth root dependence. The velocity data are very
consistent between different samples and between different pressure cycles for the same
sample. They also agree well with similar sand data from Domenico (1976), Prasad and
Meissner (1992), Yin (1992), and Robertson et al. (1995). Solid lines in Figure 5
represent empirical fits to the data.
Empirical fits to the velocity data in Figure 5 are of the form
V =a+bPc (1)
where V is the velocity (m/s), and P is the pressure (MPa). These empirical fits
demonstrate a velocity dependence to approximately the fifth root of the pressure. The
exact empirical coefficients for each case are given in Table 2.
Attenuation results
As seismic waves pass through sediments and rocks, they loose energy. This
attenuation or dissipation of seismic wave energy is greater in the loose sediments typical
of the shallow subsurface. Since attenuation depends, among other factors on material
properties, it can potentially be used to predict these properties. Futterman (1962) defines
the dissipation, Q-1, (inverse of quality factor, Q) as the ratio of energy loss per cycle
(ΔE) to the maximum energy (E) stored in the system:
D E 4P V
Q- 1 = = (1- exp( i))2p , (2)
2P E V
r

|     |     |     |     | 12  |
| --- | --- | --- | --- | --- |
where the complex velocity V = Vr + iVi.
O’Connell and Budiansky (1977) have shown that the quality factor can also be
described in terms of the complex moduli as
M
=
|     | Q r | ,   | (3)   |     |
| --- | --- | --- | ----- | --- |
M
i
where the complex modulus M = Mr + iMi. Thus, Qp, the P-wave quality factor is
4
|     | K + | m   |      |     |
| --- | --- | --- | ---- | --- |
|     | r 3 | r   |      |     |
|     | Q = | ,   | (4)  |     |
|     | P 4 |     |      |     |
|     | K + | m   |      |     |
|     | i 3 | i   |      |     |
and Qs, the S-wave quality factor is
m
|     | = r |     |      |     |
| --- | --- | --- | ---- | --- |
|     | Q   | ,   | (5)  |     |
|     | S m |     |      |     |
i
where K is the complex bulk modulus and μ is the complex shear modulus. Winkler and
Nur (1982) have shown that a plot of Qp/Qs versus (Vp/Vs)2 allows us to differentiate
between the losses in bulk (Ki/Kr) and in shear (µi/µr). Prasad and Meissner (1992) and
Prasad (2002) have shown that using both P- and S-wave velocity and attenuation allows
us to differentiate between grain size and saturation in sands. Figure 6 shows a plot of
(Vp/Vs)2 versus Qp/Qs for dry and fully water-saturated sands. The figure shows that
velocity  and  attenuation  data  can  be  useful  tools  to  distinguish  between  different
lithologies and between pressure and saturation effects.  Whereas, Vp is low at both low
effective pressures and in gas saturated sands, Vs is unaffected by saturation state and is
extremely  low  at  low  effective  pressures.  Thus,  Vp/Vs  ratio  will  move  in  different
directions for the dry and the saturated cases. In addition to low Vp-Vs ratios, dry sands
also have fairly high Qp/Qs values. Analyses of the main loss mechanism (Prasad and
Meissner, 1992) (solid lines in Figure 6) show that the shear losses equal bulk losses in
the  dry  sands;  bulk  losses  are  predominant  in  saturated  sands.  Increasing  effective
pressure decreases Qp/Qs and Vp/Vs ratios in both cases.

DISCUSSION AND RELEVANCE TO SHALLOW SEISMIC MEASUREMENTS
Field seismic studies in the past decade have shown measurements of extremely low
velocities for the shallow subsurface (e.g., Crouse et al., 1993; Taylor and Wilson, 1997;
Bachrach et al., 1998; Carr et al., 1998; Steeples et al., 1999). Due to an absence of rock

13
physics data corresponding to such sites, interpretation of sediment properties from
seismic surveys has been limited to areas where ground-truth was provided by boreholes
or existing geological descriptions. Added to this lack of data is the fact that most
theoretical models of unconsolidated granular media fail to predict both P- and S-wave
velocities realistically. Specifically, they do not predict the very low velocities and very
steep gradients that are measured in the field. This breakdown of the theoretical models
has lead to uncertainties in interpretations of field seismic measurements. Our laboratory
measurements of ultrasonic velocities corroborate the low velocities and high gradients
observed in the seismic surveys mentioned above. The agreement between laboratory and
field measurements shows that theoretical models are, at best, an oversimplification of
the natural case and modifications are required for accurate predictions of natural
phenomena. A further consequence of the inadequacy of the velocity models arises when
analyzing Poisson’s ratio values. The theoretical smooth contact radius models predict
Poisson’s ratio values much lower than 0.1 (Winkler, 1983; Prasad and Meissner, 1992;
Bachrach et al., 1998). By adding grain roughness, Palciauskas (1992) has shown that the
Poisson’s ratio can be as high as 0.14. Our measured Poisson’s ratio in dry sands at very
low pressures lies around 0.18 – 0.36. At these low pressures in the laboratory, Poisson’s
ratio does not depend significantly on pressure or on partial saturation. However, after
addition of clay or at full saturation, Poisson’s ratio values rise to about 0.4, close to fluid
values. At very low pressures, velocity is strongly dependent on composition,
microstructure, and pressure.
Our results of velocities in sediments can be used for characterizing physical
properties of sediments from field seismic surveys. They may also be useful for site-
specific modeling. For example, Bertete-Aguirre and Berge (2002) have shown that
having shear velocities available as well as P-velocities significantly improves the ability
to recover lithology from seismic data even when the velocity uncertainties are high.
In a simplified, typical shallow sediment environment, the vadose zone consists of
dry to partially saturated sediments. Below the water table, these sediments are water
saturated (e.g., Hübner et al., 1985; Robertson et al., 1995; Bachrach et al., 2002, this
volume). Depth of the water table will depend on the geographic location and on climatic
conditions. We consider, as an example, a typical shallow soil scenario in a clean sand
environment where the water table lies at a depth of 50m. Dry and partially saturated
sands lie above the water table and fully saturated sands below it. Using our experimental
results, we can now reconstruct the velocity profile of such a sediment packet as shown in

14
Figure 7. A steep velocity gradient will be characteristic of the uppermost layer, as shown
in Figure 7. The water table will be marked by strong Vp/Vs contrast. Details of
composition and fabric will affect the velocities. For example, addition of clay to the
sands in the dry region will decrease velocity even further. From Figure 4, addition of
moderate amounts of clay increases Vp due to cementation and pore-filling effects. With
larger amounts of clay, once clay becomes load-bearing, the Vp decreases. Vs, on the
other hand, decreases monotonically with addition of clay. Thus, the laboratory
measurements can be powerful predictive tools to interpret field seismic data from the
shallow sub-surface and to construct synthetic seismograms.
CONCLUSIONS
We have shown the importance of conducting laboratory experiments at pressures
relevant for the shallow depths typical for environmental geophysics. Our results on
unconsolidated sediments show that in dry sands, the pressure dependence of P- and S-
wave velocities can be empirically described by a fourth root (0.23 –0.26). The P-
velocity-dependence in wet sands lies around 0.4. At low pressures, velocity in dry sands
shows a strong increase with pressure. Poisson’s ratio values are low (0.18 – 0.3) at low
pressures. Addition of water or clay to sands increases the Poisson’s ratio to about 0.4.
ACKNOWLEDGEMENTS
Zimmer and Prasad’s work was performed under the auspices of the Department of
Energy (Award No. DE-FC26-01BC15354). Zimmer was also supported by a Chevron
Stanford Graduate Fellowship. Work of Bonner and Berge was performed under the
auspices of the U.S. Department of Energy by the University of California Lawrence
Livermore National Laboratory under contract W-7405-ENG-48 and supported
specifically by the Environmental Management Science Program of the Offices of
Environmental Management and Science. Any opinions, findings, conclusions, or
recommendations expressed herein are those of the authors and do not necessarily reflect
the views of the DOE. We thank the reviewers for their comments.

15
REFERENCES
Aracne-Ruddle, C., Wildenschild, D., Bonner, B., and Berge, P., 1998, Direct observation
of morphology of sand-clay mixtures with implications for mechanical properties in
sediments: Eos, Transactions of the American Geophysical Union, 1998 Fall Meeting
Supplement, 79, F820.
Aracne-Ruddle, C. M., Bonner, B. P., Trombino, C. N., Hardy, E. D., Berge, P. A., Boro,
C. O., Wildenschild, D., Rowe, C. D., and Hart, D. J., 1999, Ultrasonic velocities in
unconsolidated sand/clay mixtures at low pressures: LLNL report UCRL-JC-135621,
Lawrence Livermore National Laboratory, Livermore, CA 53 pp., available at
http://www.llnl.gov/tid/lof/documents/pdf/237096.pdf; also summarized in Eos,
Transactions of the American Geophysical Union, Fall Meeting Supplement,
Proceedings of the Fall Annual Meeting, held in San Francisco, CA, Dec. 13-17, 1999,
80, F397.
Bachrach, R., Dvorkin, J., and Nur, A., 1998, High-resolution shallow-seismic
experiments in sand, Part II: Velocities in shallow unconsolidated sand: Geophysics,
63, 1233-1284.
Bachrach, R., Mukerji, T., and Nur, A., 2002 (this volume), Analysis of 3D high-
resolution seismic reflection and crosswell radar tomography for aquifer
characterization: A case study: Near-Surface Geophysics, v. II, Soc. Expl. Geoph.,
Tulsa.
Baker, G. S., Steeples, D. W., and Schmeissner, C., 1999, In-situ, high-resolution P-
Wave velocity measurements within 1 m of the Earth's surface: Geophysics, 64, 323-
325.
Berge, P. A., and Bonner, B. P., 2002, Seismic velocities contain information about
depth, lithology, fluid content, and microstructure: Expanded Abstracts of the Annual
Symposium on the Application of Geophysics to Engineering and Environmental
Problems (SAGEEP), Las Vegas, NV, February 10-14, 2002, Environmental and
Engineering Geophysical Society, Wheat Ridge, CO, also submitted to the Journal of
Environmental and Engineering Geophysics.
Berge, P. A., Berryman, J. G., Bonner, B. P., Roberts, J. J., and Wildenschild, D., 1999,
Comparing geophysical measurements to theoretical estimates for soil mixtures at low
pressures: in Powers, M. H., Cramer, L., and Bell, R. S., Eds., Proceedings of the 12th
Annual Symposium on the Application of Geophysics to Engineering and
Environmental Problems (SAGEEP), Oakland, California, March 14-18, 1999,
Environmental and Engineering Geophysical Society, Wheat Ridge, CO, 465-472.
Bertete-Aguirre, H., and Berge, P. A., 2002, Recovering soil distributions from seismic
data using laboratory velocity measurements: Journal of Environmental and
Engineering Geophysics, 7, 1-10.
Bonner, B. P., Hart, D. J., and Berge, P.A., 1997, Influence of chemistry on physical
properties: ultrasonic velocities in mixtures of sand and swelling clay (abstract): Eos,

16
Transactions of the American Geophysical Union, Fall Meeting Supplement, 78,
F679.
Bonner, B. P., Berge, P. A., Aracne-Ruddle, C., Boro, C., Hardy, E., and Trombino, C.,
1999a, Ultrasonic characterization of synthetic soils for application to near-surface
geophysics: in Powers, M. H., Cramer, L., and Bell, R. S., Eds., Proceedings of the
12th Annual Symposium on the Application of Geophysics to Engineering and
Environmental Problems (SAGEEP), Oakland, California, March 14-18, 1999,
Environmental and Engineering Geophysical Society, Wheat Ridge, CO, 455-463.
Bonner, B. P., Boro, C., and Hart, D. J., 1999b, Anti-waveguide for ultrasonic testing of
granular media under elevated stress: LLNL Patent disclosure IL-10607, and patent
application, DOE Patent Docket No. S-94-182, October 28, 1999.
Bonner, B. P., Wildenschild, D., Berge, P. A., Ruddle, D., and Aracne-Ruddle, C. M.,
2000, Ultrasonic velocities of artificial sediments with minimal overburden: Eos,
Transactions of the American Geophysical Union, Fall Meeting Supplement,
Proceedings of the Fall Annual Meeting, San Francisco, CA, Dec. 15-19, 2000, 81,
F1105.
Bonner, B. P., Berge, P. A., and Wildenschild, D., 2001, Compressional and shear wave
velocities for artificial granular media under simulated near surface conditions
Expanded abstract, Society of Exploration Geophysicists International Exposition and
Seventy-First Annual Meeting, Sept. 9-14, 2001, San Antonio, TX.
Boulanger, R. W., Arulnathan, R., Harder, L. F., Jr., Torres, R. A., and Driller, M. W.,
1998, Dynamic properties of Sherman Island peat: ASCE Journal of Geotechnical and
Geoenvironmental Engineering, 124, 12-20.
Carr, B. J., Hajnal, Z., and Prugger, A., 1998, Shear-wave studies in glacial till:
Geophysics, 63, 1273-1284.
Cheng, C. H., 1978, Seismic velocities in porous rocks: direct and inverse problems:
Ph.D. thesis, Mass. Inst. of Technol., Cambridge, Mass.
Crouse, C. B., Kramer, S. L., Mitchell, R., and Hushmand, B., 1993, Dynamic tests of
pipe pile in saturated peat: ASCE Journal of Geotechnical Engineering 119, 1550-
1567.
Domaschuk, L., and Wade, N. H., 1969, A study of bulk and shear moduli of a sand: J.
Soil Mech. Found. Div., Proc. ASCE, 95, 561-581.
Domenico, S. N., 1976, Effect of brine-gas mixture on velocity in an unconsolidated sand
reservoir: Geophysics, 41, 882-894.
Futterman, W. I., 1962, Dispersive body waves: JGR, 67, 5279-5291.
Gassmann, F., 1951, Über die elastizität poröser medien: Vierteljahrsschrift der
Naturforschenden Gesellschaft in Zürich, 96, 1-23.
Green, D. H., Wang, H. F., and Bonner, B. P., 1993, Shear wave attenuation in dry and
saturated sandstone at seismic to ultrasonic frequencies: Int. J. Rock Mech. Min. Sci.
& Geomech. Abstr. 30, 755-761.

17
Hamilton, E. L., and Bachman, R. T., 1982, Sound velocity and related properties of
marine sediments: J. Acoust. Soc. Am., 72, 1891-1904.
Han, D., Nur, A. and Morgan, F. D., 1986, Effect of porosity and clay content on wave
velocities of sandstones: Geophysics, 51, 2093-2107.
Hübner, S., Meissner, R., and Stümpel, H., 1985, Einflüsse lithologischer Parameter
oberflächennaher Sedimente auf Kompressions- und Scherwellengeschwindigkeiten:
in Ingenieurgeologische Probleme in Grenzbereich zwischen Locker- und
Festgesteinen, Springer-Verlag, Berlin, 583-596.
Knight, R., and Nolen-Hoeksema, R., 1990, A laboratory study of the dependence of
elastic wave velocities on pore scale fluid distribution: Geophys. Res. Lett. 17, 1529-
1532.
Kuster, G. T., and M. N. Toksöz, 1974, Velocity and attenuation of seismic waves in
two-phase media, Part I, Theoretical formulations, and Part II, Experimental results:
Geophysics 39, 587-618.
Marion, D., Nur, A., Yin, H., and Han, D., 1992, Compressional velocity and porosity in
sand-clay mixtures: Geophysics, 57, 554-563.
OConnell, R. J., and Budiansky, B., 1977, Viscoelastic properties of fluid-saturated
cracked solids: JGR, 82, no. 36, 5719-5735.
Palciauskas, V. V., 1992, Compressional to shear wave velocity ratios of granular rocks:
role of rough grain contacts: GRL, 19, no.16, 1683-1686.
Prasad, M., 2002, Acoustic measurements in sands at low effective pressure:
Overpressure detection in sands: Geophysics, 67, no. 2, 405 – 412.
Prasad, M., and Manghnani, M. H., 1997, Effects of pore and differential pressures on
compressional wave velocity and quality factor on Berea and Michigan sandstones:
Geophysics, 62, no. 4, 1163-1176.
Prasad M., and Meissner, R., 1992, Attenuation mechanisms in sands: Laboratory versus
theoretical (Biot) data: Geophysics, 57, no. 5, 710-719.
Rao, H. A. B., 1966, Wave velocities through partially saturated sand-clay mixtures:
Response of Soils to Dynamic Loadings Report 24, Mass. Inst. Tech. Dept. Civ. Eng.
Research Report R66-13, Soils Pub. 194, Defense Documentation Center, Cameron
Station, Alexandria, VA.
Robertson, P. K., S. Sasitharan, J. C. Cunning, and D. C. Sego, 1995, Shear-wave
velocity to evaluate in-situ state of Ottawa Sand: J. Geotech. Eng., 121, 262-273.
Santamarina, J.C., Klein, K.A., and Fam, M.A., 2001, Soils and Waves: John Wiley and
Sons, West Sussex, England.
Sears, F. M., and Bonner, B. P., 1981, Ultrasonic attenuation measurement by spectral
ratios utilizing signal processing techniques: IEEE Transactions on Geoscience and
Remote Sensing, GE-19, 95-99.

18
Steeples, D. W., Baker, G. S., and Schmeissner, C., and Macy, B. K., 1999, Geophones
on a board: Geophysics, 64, no. 3, 809-814.
Taylor, W. P., and Wilson, C. D. V., 1997, Tectonically influenced glacial erosion, and
ensuing valley infill: A geophysical survey: Quarterly Journal of Engineering Geology
30, 97-113.
Vernik, L., and Nur, A., 1992, Petrophysical classification of siliciclastics for lithology
and porosity prediction from seismic velocities: Am. Assoc. Petr. Geol. Bull. 76,
1295-1309.
Wilkens, R. H., Simmons, G., Wissler, T. M., and Caruso, L., 1986, The physical
properties of a set of sandstones--Part III. The effects of fine-grained pore-filling
material on compressional wave velocity: Int. J. Rock Mech. Min. Sci. & Geomech.
Abstr. 23, 313-326.
Winkler, K. W., 1983, Contact stiffness in granular porous materials. Comparison
between theory and experiments: Geophy. Res. Lett., 10, 1073-1076.
Winkler, K. W., and Nur, 1982, Seismic attenuation: Effects of pore fluids and frictional
sliding: Geophysics, 47, no. 1, 1-15.
Wyllie, M. R. J., Gregory, A. R., and Gardner, L. W., 1956, Elastic wave velocities in
heterogeneous and porous media: Geophysics, 21, 41-70.
Yin, H., 1992, Acoustic velocity and attenuation of rocks: isotropy, intrinsic anisotropy,
and stress induced anisotropy: Ph.D. thesis, Stanford Univ.
Zimmer, M. A., Prasad, M., and Nur, A., 2000, Ultrasonic velocities of sand at low
effective pressures (abstract): Eos, Transactions of the American Geophysical Union,
Fall Meeting Supplement, Proceedings of the Fall Annual Meeting, held in San
Francisco, CA, Dec. 15-19, 2000, 81, F1105-1106.
Zimmer, M. A., Prasad, M., and Nur, A., 2002a, Laboratory P- and S-wave
measurements on sands: Implications for pressure trends: Expanded Abstracts of the
Annual Symposium on the Application of Geophysics to Engineering and
Environmental Problems (SAGEEP), Las Vegas, NV, February 9-13, 2002,
Environmental and Engineering Geophysical Society, Wheat Ridge, CO.
Zimmer, M., Prasad, M., and Mavko, G., 2002b, Pressure and porosity influences on Vp-
Vs ratio in unconsolidated sands: The Leading Edge, 21, no. 2, 178-183.

19
FIGURE CAPTIONS
Fig. 1. Schematic diagram of pore fluid pumping system for LLNL apparatus.
Fig. 2. (a) The Stanford sample holder. (b) The Stanford pressure vessel in its stand.
Fig. 3. Typical signals from the Stanford experiment. P-wave signals in a sand sample are
shown in (a) at 0.05 MPa and (b) at 20 MPa confining pressures. S-wave signals in a
sand sample are shown in (c) at 0.05 MPa and (d) at 20 MPa confining pressures.
Arrows in (c) and in (d) mark onset of the S-wave.
Fig. 4. (a) Vp and (b) Vs versus pressure for various sand-clay mixtures. Numbers in
legend of plot refer to date of measurement and clay content (by mass) for sand-clay
mixtures. Different samples had different packing in some cases. (1 MPa = 145 psi).
Fig. 4. (c) (top) Velocity vs. clay content for dry sand-clay mixtures at 16 psi (0.11 MPa)
and (bottom) schematic diagram of microstructure for various amounts of clay (black)
mixed with sand grains (gray circles).
Fig. 5. Ultrasonic velocity results for dry and water-saturated samples of the Santa Cruz
aggregate. (a) Vp and (b) Vs for the four sand samples.
Figure 6. Separation of saturation effects using a loss diagram (Prasad and Meissner,
1992). Water-saturated sands (filled circles) are characterized by high Vp/Vs and Qp/Qs
values, whereas dry sands (open triangles) have low Vp/Vs values but high Qp/Qs. The
solid lines are calculations for various values of bulk (K) and shear (µ) losses. Shear
i i
losses are as high as bulk losses in dry sands whereas in saturated sands, shear losses are
higher. Vp/Vs and Qp/Qs values decrease with confining pressure as marked by arrows
(data from Prasad and Meissner, 1992; and Prasad, 2002).
Figure 7. A typical shallow soil scenario in a clean sand environment and the Vp, Vs,
Vp/Vs profile of such a sediment packet. The water-table is clearly marked by high
Vp/Vs ratios that decrease with depth. In the dry and the partially saturated zones, Vp/Vs
values are low and they do not change much with pressure. In all cases, velocity is
strongly dependent on depth.

20
LIST OF TABLES
Table 1. LLNL velocity results for partially-saturated sand samples at 40 kPa load.
Table 2. Empirical fits to the velocity data for Santa Cruz aggregate samples (between 0.1
and 20 MPa).
Table 3. Poisson’s ratios for dry samples at low pressures.
Table 4. Poisson’s ratios for dry and saturated samples at hydrostatic pressures.

|     |     | 21  |
| --- | --- | --- |

FIGURES

|     |     | 22  |
| --- | --- | --- |

Fig. 1. Schematic diagram of pore fluid pumping system for LLNL apparatus.

|     |        |     |     |      | 23  |
| --- | ------ | --- | --- | ---- | --- |
|     |   (a)  |     |     | (b)  |     |
|     |        |     |     |      |     |
Fig. 2. (a) The Stanford sample holder. (b) The Stanford pressure vessel in its stand.

|     |     |     |     |     |     |     | 24  |
| --- | --- | --- | --- | --- | --- | --- | --- |

|     | 125 |     |          | 250 |     |     |     |
| --- | --- | --- | -------- | --- | --- | --- | --- |
|     | a   |     | 0.05 MPa | b   |     |     |     |
20 MPa
|                | 100  |           |          | 200            |           |        |     |
| -------------- | ---- | --------- | -------- | -------------- | --------- | ------ | --- |
| )Vm( edutilpmA |      |           |          | )Vm( edutilpmA |           |        |     |
|                | 75   |           |          | 150            |           |        |     |
|                | 50   |           |          | 100            |           |        |     |
|                | 25   |           |          | 50             |           |        |     |
|                | 0    |           |          | 0              |           |        |     |
|                | 0 50 | 100 150   | 200 250  | 0              | 50 100    | 150    |     |
|                |      | Time (µs) |          |                | Time (µs) |        |     |
|                | 40   |           |          | 250            |           |        |     |
|                | c    |           | 0.05 MPa | d              |           | 20 MPa |     |
35
200
30
| )Vm( edutilpmA |     |     |     | )Vm( edutilpmA |     |     |     |
| -------------- | --- | --- | --- | -------------- | --- | --- | --- |
|                | 25  |     |     | 150            |     |     |     |
20
|     | 15  |     |     | 100 |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
10
50
5
|     | 0    |           |         | 0   |           |     |     |
| --- | ---- | --------- | ------- | --- | --------- | --- | --- |
|     | 0 50 | 100 150   | 200 250 | 0   | 50 100    | 150 |     |
|     |      | Time (µs) |         |     | Time (µs) |     |     |

Fig. 3. Typical signals from the Stanford experiment. P-wave signals in a sand sample
are shown in (a) at 0.05 MPa  and (b) at 20 MPa confining pressures. S-wave signals in a
sand sample are shown in (c) at 0.05 MPa  and (d) at 20 MPa confining pressures.
Arrows in (c) and in (d) mark onset of the S-wave.

25
Fig. 4. (a) Vp vs. pressure for various sand-clay mixtures. Numbers in legend of plot refer
to date of measurement and clay content (by mass) for sand-clay mixtures. Different
samples had different packing in some cases. (1 MPa = 145 psi)

26
Fig. 4. (b) Vs versus pressure for various sand-clay mixtures. Numbers in legend of plot
refer to date of measurement and clay content (by mass) for sand-clay mixtures. Different
samples had different packing in some cases. (1 MPa = 145 psi)

27
Fig. 4. (c) (top) Velocity vs. clay content for dry sand-clay mixtures at 16 psi (0.11 MPa)
and (bottom) schematic diagram of microstructure for various amounts of clay (black)
mixed with sand grains (gray circles).

28
(a) P-waves
(b) S-waves
Fig. 5. Ultrasonic velocity results for dry and water-saturated samples of the Santa Cruz
aggregate. (a) Vp and (b) Vs for the four sand samples.

29
3
2
1
0
0 10 20 30 40
2
(Vp/Vs)
sQ/pQ
Ki=µi Ki=2µi
dry
saturated
Ki=5µi
Figure 6. Separation of saturation effects using a loss diagram (Prasad and Meissner,
1992). Water-saturated sands (filled circles) are characterized by high Vp/Vs and Qp/Qs
values, whereas dry sands (open triangles) have low Vp/Vs values but high Qp/Qs. The
solid lines are calculations for various values of bulk (K) and shear (µ) losses. Shear
i i
losses are as high as bulk losses in dry sands whereas in saturated sands, shear losses are
higher. Vp/Vs and Qp/Qs values decrease with confining pressure as marked by arrows
(data from Prasad and Meissner, 1992; and Prasad, 2002).

|     |     |     |     | 30  |
| --- | --- | --- | --- | --- |

Velocity (m/s)
Vp/Vs
|   Geology   | Depth  | 0   1000 | 2 000 2  | 4    6  8  |
| ----------- | ------ | -------- | -------- | ---------- |
|             | 0m     |          |          |            |
|             |        |          |          |            |
Vadose zone       Dry – partially saturated
Vp
|     | 5m (0.1MPa)  |     |     |     |
| --- | ------------ | --- | --- | --- |
Water table
|     | 5m (0.1MPa)  |     |     |     |
| --- | ------------ | --- | --- | --- |
|     |              |     |     |     |
  saturated
|     | 50m (1.0MPa)  |     |     |     |
| --- | ------------- | --- | --- | --- |
Vs

|     | 1km (20MPa)  |     |     |     |
| --- | ------------ | --- | --- | --- |
Bedrock

Figure 7. A typical shallow soil scenario in a clean sand environment and the Vp, Vs,
Vp/Vs profile of such a sediment packet. The water-table is clearly marked by high
Vp/Vs ratios that decrease with depth. In the dry and the partially saturated zones, Vp/Vs
values are low and they do not change much with pressure. In all cases, velocity is
strongly dependent on depth.

|     |     |     |     |     | 31  |
| --- | --- | --- | --- | --- | --- |
TABLES

Table 1. LLNL velocity results for partially-saturated sand samples at 40 kPa load

| Waveform  | Vp (m/s)   | Vs (m/s)  | Poisson’s  | Notes  |     |
| --------- | ---------- | --------- | ---------- | ------ | --- |
ratio
| Sample 1:  |     |     |     |     |     |
| ---------- | --- | --- | --- | --- | --- |
6/27/00 #1  375 ± 75  232 ± 6  0.19  Saturated, but some bubbles.
(Vp =1500 ± 40 through sat. patches)
| Sample A:  |     |     |     |     |     |
| ---------- | --- | --- | --- | --- | --- |
6/29/00 #2  357 ± 30  214 ± 10  0.22  Saturated, no visible bubbles
6/30/00 #1  308 ± 10  214 ± 10  0.03  Draining (capillary press = 35 cm),
water content 22 to 28 %.
6/30/00 #3  326 ± 10  204 ± 6  0.18  Draining (capillary press = 44 cm),
water content 13 to 17 %.
12/7/00  349 ± 8  249 ± 20  ~0  Dried (chemical alteration probable)

|     |     |     |     |     | 32  |
| --- | --- | --- | --- | --- | --- |
Table  2.  Empirical  fits  to  the  velocity  data  for  Santa  Cruz  aggregate  samples
(between 0.1 and 20 MPa).
R2
|           | a   | b    | c      | 1/c (root)  |         |
| --------- | --- | ---- | ------ | ----------- | ------- |
| V  – dry  | 0   | 436  | 0.243  | 4.11        | 0.9852  |
S
| V  – wet  | 0   | 428  | 0.260  | 3.84  | 0.9572  |
| --------- | --- | ---- | ------ | ----- | ------- |
S
| V  – dry  | 0   | 774  | 0.227  | 4.40  | 0.9656  |
| --------- | --- | ---- | ------ | ----- | ------- |
P
| V  – wet  | 1753  | 168  | 0.408  | 2.45  | 0.9295  |
| --------- | ----- | ---- | ------ | ----- | ------- |
P

|     |     |     |     |     | 33  |
| --- | --- | --- | --- | --- | --- |
Table 3. Poisson’s ratios for dry samples at low pressures.
|     | Clay content   | Pressure   | Vp/Vs      | Poisson’s ratio  |     |
| --- | -------------- | ---------- | ---------- | ---------------- | --- |
|     | 0%             | ~0 MPa     | 1.7 - 2.2  | 0.23 - 0.36      |     |
|     | 0%             | ~0.1 MPa   | 1.6 - 2.1  | 0.18 - 0.36      |     |
|     | 1%             | ~0 MPa     | 3.6        | 0.46             |     |
|     | 1%             | ~0.1 MPa   | 2.3        | 0.38             |     |
|     | 3%             | ~0 MPa     | 1.8 - 2.2  | 0.29 - 0.36      |     |
|     | 3%             | ~0.1 MPa   | 2.1 - 2.2  | 0.35 - 0.37      |     |
|     | 10%            | ~0 MPa     | 1.8 - 3.2  | 0.26 - 0.45      |     |
|     | 10%            | ~0.1 MPa   | 2.0 - 3.2  | 0.33 - 0.45      |     |
|     | 20%            | ~0 MPa     | 2.5        | 0.4              |     |
|     | 20%            | ~0.1 MPa   | 2.5        | 0.41             |     |
|     | 30%            | ~0 MPa     | 2.2        | 0.38             |     |
|     | 30%            | ~0.1 MPa   | 2.4        | 0.4              |     |
|     | 40%            | ~0 MPa     | 2.4        | 0.39             |     |
|     | 40%            | ~0.1 MPa   | 2.5        | 0.41             |     |

|     |     |     |     |     | 34  |
| --- | --- | --- | --- | --- | --- |
Table 4. Poisson’s ratios for dry and saturated samples at hydrostatic pressures.
DRY
|     | Pressure  | Vp  Vs        | Vp/Vs  | Poisson’s  |     |
| --- | --------- | ------------- | ------ | ---------- | --- |
|     | (MPa)     | (m/s)  (m/s)  |        | ratio      |     |
|     | 0.0       | 275  160      | 1.72   | 0.24       |     |
|     | 0.101     | 501  235      | 2.13   | 0.36       |     |
|     | 0.15      | 500  268      | 1.87   | 0.30       |     |
|     | 0.201     | 510  290      | 1.76   | 0.26       |     |
|     | 0.3       | 549  330      | 1.66   | 0.22       |     |
|     | 0.5       | 640  365      | 1.75   | 0.26       |     |
|     | 1.02      | 821  434      | 1.89   | 0.31       |     |
|     | 2.46      | 982  534      | 1.84   | 0.29       |     |
|     | 5.03      | 1131  631     | 1.79   | 0.27       |     |
|     | 7.52      | 1225  697     | 1.76   | 0.26       |     |
|     | 9.97      | 1309  750     | 1.75   | 0.26       |     |
|     | 15.05     | 1445  861     | 1.68   | 0.22       |     |
|     | 17.54     | 1504  895     | 1.68   | 0.23       |     |
|     | 19.96     | 1566  925     | 1.69   | 0.23       |     |
SATURATED
|     | 0.111   | 1810  244  | 7.42  | 0.49  |     |
| --- | ------- | ---------- | ----- | ----- | --- |
|     | 0.2     | 1836  271  | 6.77  | 0.49  |     |
|     | 0.292   | 1877  338  | 5.53  | 0.48  |     |
|     | 0.5     | 1883  378  | 4.87  | 0.48  |     |
|     | 1.049   | 1938  477  | 4.05  | 0.47  |     |
|     | 2.499   | 1973  569  | 3.48  | 0.45  |     |
|     | 4.947   | 2062  651  | 3.18  | 0.44  |     |
|     | 7.52    | 2108  752  | 2.83  | 0.43  |     |
|     | 9.792   | 2180  786  | 2.79  | 0.43  |     |
|     | 15.017  | 2246  850  | 2.65  | 0.42  |     |
|     | 17.526  | 2285  880  | 2.60  | 0.41  |     |
|     | 19.992  | 2286  908  | 2.52  | 0.41  |     |