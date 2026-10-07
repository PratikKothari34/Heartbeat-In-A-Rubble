○
E
| Performance |     |     |     | of  | Several |     |     | Low-Cost |     |     |     |     |     |     |
| ----------- | --- | --- | --- | --- | ------- | --- | --- | -------- | --- | --- | --- | --- | --- | --- |
Accelerometers
by J. R. Evans, R. M. Allen, A. I. Chung, E. S. Cochran, R. Guy,
| M. Hellweg, |     |     | and | J. F. | Lawrence |     |     |     |     |     |     |     |     |     |
| ----------- | --- | --- | --- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
OnlineMaterial:DescriptionoftypicalClass-CMEMSaccel- 2010; sensor roughly US$500–1000). Class C is the lowest
erometers;exampleofExcelanalysissheet;tablesummariesof performance level potentially usable by ANSS and has useful
box-flip test results, sensor performance, and pricing infor- resolutionfromabout12to16bits,typicallyover(cid:1)2g ranges
| mation. |     |     |     |     |     |     |     |                 | US$100–200). |     |     | Ⓔ   |              |           |
| ------- | --- | --- | --- | --- | --- | --- | --- | --------------- | ------------ | --- | --- | --- | ------------ | --------- |
|         |     |     |     |     |     |     |     | (sensor roughly |              |     |     | We  | describe the | design of |
typicalClass-Caccelerometersandprovidelinksonthesubject
| INTRODUCTION |     |     |     |     |     |     |     | in the electronic |     | supplement | to  | this paper. |     |     |
| ------------ | --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | ---------- | --- | ----------- | --- | --- |
InordertofacilitatetheuseofClass-Csensorsinregional
Severalgroupsareimplementinglow-costhost-operatedsystems networksitiscriticalthat weareabletounderstandthe capa-
|     |     |     |     |     |     |     |     | bilities and | limitations |     | of these | instruments. | This | report |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | ----------- | --- | -------- | ------------ | ---- | ------ |
ofstrong-motionaccelerographstosupportthesomewhatdiver-
gent needs of seismologists and earthquake engineers. The Ad- describes performance-test results for the following five types
|                 |     |         |        |           |     |                |     | of triaxial | Class-C | sensors | together |     | with their | recording |
| --------------- | --- | ------- | ------ | --------- | --- | -------------- | --- | ----------- | ------- | ------- | -------- | --- | ---------- | --------- |
| vanced National |     | Seismic | System | Technical |     | Implementation |     |             |         |         |          |     |            |           |
Committee(ANSSTIC,2002),managedbytheU.S.Geological systems, public or private:
Survey(USGS)incooperationwithothernetworkoperators,is 1. Droidsmartphones,oneexampleofaGoogleNexusOne
|     |     |     |     |     |     |     |     | (we | call this, | Serial | Number | 2[SN2]; | https://sites.google |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ------ | ------ | ------- | -------------------- | --- |
exploringtheefficacyofsuchsystemsifusedinANSSnetworks.
Tothisend, ANSSconvenedaworkinggrouptoexploreavail- .com/a/pressatgoogle.com/nexusone/; November 2013),
|            |                 |     |                |     |          |         |     | and | two examples | of  | HTC | Magic | phones (we | call these |
| ---------- | --------------- | --- | -------------- | --- | -------- | ------- | --- | --- | ------------ | --- | --- | ----- | ---------- | ---------- |
| able Class | C strong-motion |     | accelerometers |     | (defined | later), | and |     |              |     |     |       |            |            |
toconsideroperationalandqualitycontrolissues,andthemeans SN3 and SN4; there is no SN1; http://www.htc.com/us/;
ofannotating,storing,andusing suchdatainANSSnetworks. November 2013); note that iPhones, laptop computers,
andprobablyothershavesimilarcapability,sowewillrefer
| The working | group | members |     | are largely | coincident | with | our |     |     |     |     |     |     |     |
| ----------- | ----- | ------- | --- | ----------- | ---------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
author list, and this report informs instrument-performance to tested devices generically as smart phones;
|           |            |     | group’s |               |     |         |       | 2. Gulf | CoastDataConcepts(GCDC;gcdataconcepts.com) |     |     |     |     |     |
| --------- | ---------- | --- | ------- | ------------- | --- | ------- | ----- | ------- | ------------------------------------------ | --- | --- | --- | --- | --- |
| mattersin | theworking |     |         | reporttoANSS. |     | Present | exam- |         |                                            |     |     |     |     |     |
plesofoperationalnetworksofsuchdevicesaretheCommunity model X6-2 shipping monitors used to detect drops and
Seismic Network (CSN; csn.caltech.edu), operated by the Cal- bumpsofvaluablepackagesduringshipmentandhandling
|                   |     |                |     |                   |     |         |     | (SNs | 4086, | 4097, and | 4128); |     |     |     |
| ----------------- | --- | -------------- | --- | ----------------- | --- | ------- | --- | ---- | ----- | --------- | ------ | --- | --- | --- |
| ifornia Institute |     | of Technology, |     | and Quake-Catcher |     | Network |     |      |       |           |        |     |     |     |
(“JWF14”;
(QCN; Cochran et al., 2009; qcn.stanford.edu; November 3. JoyWarrior model 24F14 accelerometers Code
|                |          |     |                       |     |     |              |     | Mercenaries |     | Hard- und | Software | GmbH, | codemercs.com), |     |
| -------------- | -------- | --- | --------------------- | --- | --- | ------------ | --- | ----------- | --- | --------- | -------- | ----- | --------------- | --- |
| 2013), jointly | operated |     | by StanfordUniversity |     |     | and theUSGS. |     |             |     |           |          |       |                 |     |
1–6;
Several similar efforts are in development at other institutions. a type often used to control video games (SNs SNs
1,2,and5are(cid:1)1gdevices,theotherthreeare(cid:1)2gdevices);
Theoverarchinggoalsofsucheffortsaretoaddspatialdensityto
|          |         |             |      |      |            |          |     | 4. two | models | of similar |     | video-game | controllers | from |
| -------- | ------- | ----------- | ---- | ---- | ---------- | -------- | --- | ------ | ------ | ---------- | --- | ---------- | ----------- | ---- |
| existing | Class-A | and Class-B | (see | next | paragraph) | networks | at  |        |        |            |     |            |             |      |
O-NaviLLC(o‑navi.com),models23567-A(“O-NaviA”)
lowcost,andtoincludemanyadditionalpeoplesotheybecome
|     |     |     |     |     |     |     |     | and | 23567-B | (“O-Navi | B”); | and |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | -------- | ---- | --- | --- | --- |
investedintheissuesofearthquakes,theirmeasurement,andthe
damage they cause. 5. twomodelsofPhidgets(phidgets.com),fiveofmodel1056
145444–252220),
ClassesA,B,andCaredefinedintermsofperformanceby (SNs and one prototype model 1043
(SN999990);thesedevicesareaimedatgeneralprototyp-
ANSS(2008).ClassAreferstothehighestperformance,state-
of-the-art instrumentation, presently for accelerometers with ing (often for navigation) and amateur users.
22–24 (cid:1)2 Unless otherwise stated, these are (cid:1)2g devices. The tests
| useful resolution |        | of about |         | bits           | peak-to-peak | over  |      |           |      |     |     |     |     |     |
| ----------------- | ------ | -------- | ------- | -------------- | ------------ | ----- | ---- | --------- | ---- | --- | --- | --- | --- | --- |
| (cid:1)4g         |        |          |         | US$2000–4000). |              |       |      |           |      |     |     |     |     |     |
| to                | ranges | (sensor  | roughly |                |              | Class | B is | performed | were |     |     |     |     |     |
illustratedwellbytheNetQuakesinstrument(GeoSIGmodel 1. “boxflip”testsfor0 Hz sensitivity, offset,and axisorien-
| GMS-18) | that | is an effectively |     | 16-bit | (vertical) | and | 18-bit | tations; |     |     |     |     |     |     |
| ------- | ---- | ----------------- | --- | ------ | ---------- | --- | ------ | -------- | --- | --- | --- | --- | --- | --- |
(horizontal) instrument over (cid:1)3g ranges (notwithstanding 2. transferfunctiontests(responsefunctions)inthiscasefor
|             |        |       |     |           |          |         |       | amplitude, | but | not | phase; |     |     |     |
| ----------- | ------ | ----- | --- | --------- | -------- | ------- | ----- | ---------- | --- | --- | ------ | --- | --- | --- |
| that longer | sample | words | are | recorded; | Luetgert | et al., | 2009, |            |     |     |        |     |     |     |
doi:10.1785/0220130091 Seismological Research Letters Volume 85, Number 1 January/February 2014 147

3. tests of clipping behavior and sensor linearity (sensitivity wetestedwereoldmodels.Wehearthatnewermodelsperform
versus input acceleration level); far betterin resolution and noise so our tests maynotbe rep-
4. sensor self-noise levels, which determine useful operating resentative (R. Allen, personal comm., 2013).
ranges in decibels or bits; and Thebestdevicesappeartobehavegreaterresolutionthan
5. adoubleintegrationtesttodeterminewhetherpermanent the venerable Kinemetrics SMA-1 optical accelerograph (data
displacements can be recovered accurately from these ac- from which drove the early decades of earthquake building
celerometers. code development), so we expect they can contribute useable
|         |             |             |     |       |         |          |            | data for      | some       | purposes,  | such       | as input   | to        | ShakeMap and     |
| ------- | ----------- | ----------- | --- | ----- | ------- | -------- | ---------- | ------------- | ---------- | ---------- | ---------- | ---------- | --------- | ---------------- |
| We      | note a      | terminology |     | issue | between | commonly | used       |               |            |            |            |            |           |                  |
|         |             |             |     |       |         |          |            | ground-motion | prediction |            | equations, | if         | other     | issues are found |
| Class-A | and Class-B | sensors     | and | the   | Class-C | sensor   | used here. |               |            |            |            |            |           |                  |
|         |             |             |     |       |         |          |            | tractable.    | Thus,      | we believe | they       | are viable | candidate | instru-          |
AlthoughweuseessentiallythesameANSStestsasforClassesA
|     |     |     |     |     |     |     |     | ments for | use by | host-operated |     | low-cost | networks | for seismo- |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ------ | ------------- | --- | -------- | -------- | ----------- |
andB,theoutputsofsuchdevicesareinvolts,withfilteringand
|     |     |     |     |     |     |     |     | logical research, |     | engineering |     | research | and | practice, and |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------------- | --- | ----------- | --- | -------- | --- | ------------- |
conversiontocountsperformedbyhigh-precisionrecorders.We
|     |     |     |     |     |     |     |     | emergency | response. |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | --------- | --- | --- | --- | --- | --- |
recommendusingasimilarsetoftestsforClass-Cdevices,butin
| those we     | test here | and    | most       | others, | the analog-to-digital |           | con-   |          |       |     |     |     |     |     |
| ------------ | --------- | ------ | ---------- | ------- | --------------------- | --------- | ------ | -------- | ----- | --- | --- | --- | --- | --- |
|              |           |        |            |         |                       |           |        | BOX-FLIP | TESTS |     |     |     |     |     |
| verter (ADC) | and       | likely | anti-alias | filters | are                   | contained | within |          |       |     |     |     |     |     |
thesensorpackage,withthatpackageoutputtingadigitalstream
|               |             |       |             |           |          |            |          | Accelerometers    |                | of most | types | have the        | helpful | behavior of a   |
| ------------- | ----------- | ----- | ----------- | --------- | -------- | ---------- | -------- | ----------------- | -------------- | ------- | ----- | --------------- | ------- | --------------- |
| of converted  | data.       | Thus, | we          | will use  | the term | sensor     | here to  |                   |                |         |       |                 |         |                 |
|               |             |       |             |           |          |            |          | flat response     | all            | the way | to 0  | Hz representing |         | sensor output   |
| mean those    | integrated, |       | digital-out | packages. |          | Similarly, | while    |                   |                |         |       |                 |         |                 |
|               |             |       |             |           |          |            |          | when it           | is motionless. |         | Thus, | one can         | measure | basic perfor-   |
| the recording | methods     |       | we used     | are not   | complete | data       | acquisi- |                   |                |         |       |                 |         |                 |
|               |             |       |             |           |          |            |          | mance information |                | simply  | by    | attaching       | the     | sensors rigidly |
tionunits(DAUsinANSSparlance)inthesenseofcombining
|     |     |     |     |     |     |     |     | inside an | accurately | rectilinear |     | box, | with | the sensor-case |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---------- | ----------- | --- | ---- | ---- | --------------- |
ADC,timing,storage,andcommunications,theyperformmost
ofthoseduties,andwethereforecallthemrecorders.ⒺMostof orientationwellalignedtotheboxedges.Bysequentiallyplac-
|           |        |          |          |     |             |     |            | ing the boxand |     | sensorsin | eachof | its | sixpossibleorientations |     |
| --------- | ------ | -------- | -------- | --- | ----------- | --- | ---------- | -------------- | --- | --------- | ------ | --- | ----------------------- | --- |
| these are | laptop | software | supplied | by  | the vendors |     | or network |                |     |           |        |     |                         |     |
onaflat,stable,carefullyleveledsurface(Fig.1),onecanobtain
| operators      | (enumerated  |        | in the           | electronic | supplement). |     | GCDC       |            |              |         |     |              |     |                |
| -------------- | ------------ | ------ | ---------------- | ---------- | ------------ | --- | ---------- | ---------- | ------------ | ------- | --- | ------------ | --- | -------------- |
|                |              |        |                  |            |              |     |            | the static | sensitivity, | offset, | and | orientations |     | of every axis; |
| devices record | ADC          | counts | internally       |            | and download |     | them as    |            |              |         |     |              |     |                |
| such, so       | are complete |        | data acquisition |            | systems,     | or  | “ DASs” in |            |              |         |     |              |     |                |
ANSSparlance.Finally,wedidnothavedirectaccesstothesen-
sordigitaloutputs,sowhatisreportedhereismuddiedbyusing
existingrecordersandtheirsoftwareorfirmwareasprovidedby
thevariousnetworkoperatorsorsensorvendors.Here,wemust
| assume | that the | recorders | faithfully |     | report | sensor | outputs in |     |     |     |     |     |     |     |
| ------ | -------- | --------- | ---------- | --- | ------ | ------ | ---------- | --- | --- | --- | --- | --- | --- | --- |
unitsspecifictothatmodel.Themostlikelyexceptionsareaddi-
tionalfilteringthatmaybeperformedbytherecordersandfilter-
| ing, which        | is performed |            | in                                | our analyses           |     | by resampling | to  |     |     |     |     |     |     |     |
| ----------------- | ------------ | ---------- | --------------------------------- | ---------------------- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| 200 samples=s.    |              | MATLAB     | usesalinear-phasefiniteimpulsere- |                        |     |               |     |     |     |     |     |     |     |     |
| sponse[FIR]filter |              | withKaiser |                                   | windowwhendownsampling |     |               | is  |     |     |     |     |     |     |     |
needed,sothesefiltereffectsarelikelytobeathighfrequencies
| and have | little effect | on        | our     | results. |          |             |     |     |     |     |     |     |     |     |
| -------- | ------------- | --------- | ------- | -------- | -------- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
| Tests    | were          | performed | largely | at       | the USGS | Albuquerque |     |     |     |     |     |     |     |     |
SeismologicalLaboratory(ASL;e.g.,Huttetal.,2011)inJune
| 2012 to          | evaluate   | sensitivity,     |     | axis orientation, |      | system   | noise,     |     |     |     |     |     |     |     |
| ---------------- | ---------- | ---------------- | --- | ----------------- | ---- | -------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
| response         | functions, | clipping         |     | and linearity,    |      | and the  | ability to |     |     |     |     |     |     |     |
| double integrate |            | the acceleration |     | records           | to   | recover  | 400 mm     |     |     |     |     |     |     |     |
| quasi-static     | steps      | in displacement. |     | They              | were | attached | to an      |     |     |     |     |     |     |     |
▴
aluminum plate with removable adhesives because many lack Figure 1. Exampleoftherawdatafor abox-fliptest, showing
bolt-down provisions; the plate was bolted or clamped to the periods of stasis at the six possible orientations of the box at
shaketables.Someofthenoisedatacamefromotherlocations whichthesensorsareattachedandaligned;thefirstorientation,
and serial numbers, with the sensor plate simply resting on a normalinstallationorientation,isrepeatedattheendofthetestto
concrete pier. These tests are all routinely applied at ASL to constrain instrument drift. Signals between stasis intervals are
Class-A and Class-B systems as well. The Class-C devices we due to moving the box to its new orientations. The dashed lines
tested vary in overall performance from poor by seismological indicate the segments for which mean output levels were com-
standards (smart phones with internal accelerometers; an puted in this example; segments are selected by an analyst.
iPhonewetestedafewyearspriortothepresenttestshadres- Zaxisisoffsetby1gbecauseitsoutputiscorrectedfortheEarth’s
olution similar to the present examples) to quite good by the staticfield,perhapsbysimplyadjustingtheoutputvoltageinthe
same standards (Phidgets and O-Navi),withthe range of per- sensor;thecorrectiondoesnotappeartolimitsensorrangenorto
formancebetweenthoseextremes.Notethatthesmartphones be anything but a simple constant.
148 Seismological Research Letters Volume 85, Number 1 January/February 2014

|     |     |     |     |     |     |     |     | as an electronic |     | supplement | to  | this | paper). | All brands | tested |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ---------- | --- | ---- | ------- | ---------- | ------ |
(a)
|     |     |     |     |     |     |     |     | have some  | sensitivity |            | errors | greater | than          | 1% (up | to 2.4%)     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ----------- | ---------- | ------ | ------- | ------------- | ------ | ------------ |
|     |     |     |     |     |     |     |     | so would   | need        | individual | box    | tests   | and amplitude |        | scaling to   |
|     |     |     |     |     |     |     |     | bring them | within      | the        | 1%     | ANSS    | guidance      | for    | sensitivity. |
∼10%
|     |     |     |     |     |     |     |     | There are       | excessively | large         | offsets    | (more        |           | than     | of full   |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | ----------- | ------------- | ---------- | ------------ | --------- | -------- | --------- |
|     |     |     |     |     |     |     |     | scale) in       | some        | axes of       | some       | models,      | including | some,    | which     |
|     |     |     |     |     |     |     |     | likely resultin |             | significantly | asymmetric |              | clipping, | thus,    | to low-   |
|     |     |     |     |     |     |     |     | ered effective  | recording   |               | range.     | Orientations |           | relative | to sensor |
(b)
|     |     |     |     |     |     |     |     | cases are | within | 4° and | the majority |     | within | 2°; however, | this |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ------ | ------ | ------------ | --- | ------ | ------------ | ---- |
toowouldneedindividualtesting(andaxisrotationinprocess-
|     |     |     |     |     |     |     |     | ing) to bring | all | within | the ANSS |     | guidance | of 1% | cross-axis |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ------ | -------- | --- | -------- | ----- | ---------- |
excitation.A2°alignmenterrorequatesto3.5%crossaxis;mit-
|     |     |     |     |     |     |     |     | igatingeventhisresultisthefactthatmanyusesof |     |     |     |     |     |     | thesedata |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------------------------------- | --- | --- | --- | --- | --- | --- | --------- |
willuserandom-orgreatest-horizontalmotions,andtherefore
arenotparticularlysensitivetoorientations.Further,thesede-
vicesarelikelytobeinstalledbytheirhosts,whoarenotexperts
andmaynotorientthemaccuratelyorcommunicatetheirori-
|     |     |     |     |     |     |     |     | entation   | accurately | to  | network   | operators. |            | (Hutt     | et al., 2010, |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ---------- | --- | --------- | ---------- | ---------- | --------- | ------------- |
|     |     |     |     |     |     |     |     | imply 0.6° | accuracy   | by  | their −40 | dB         | cross-axis | guidance, | but           |
thisiscommonlyallowedtoreach1°,anindustrynorm.)The
▴
Figure 2. (a) Example of amplitude-response analysis for a active-axisorientationismeasuredby0Hzoutputsinthefour
sine-signal input by a shake table (dashed trace, here synthetic) boxorientationswherethenominalactiveaxisisperpendicular
to the output signal (solid). Only the first few cycles of the sine totheg vector.Wedidnotdynamicallytestforcross-axissen-
segment are shown, but the entire signal is used for analysis. sitivitysosourcesotherthandiemisalignmentmaybepresent;
| (b) A narrowband |     | part | of the spectral |     | responses | (simple | fast |          |         |            |     |           |     |                 |     |
| ---------------- | --- | ---- | --------------- | --- | --------- | ------- | ---- | -------- | ------- | ---------- | --- | --------- | --- | --------------- | --- |
|                  |     |      |                 |     |           |         |      | based on | general | experience |     | with MEMS |     | accelerometers, | we  |
Fourier transforms [FFTs]) centered at the input sine frequency. suspect such sources are small.)
Themiddlefivefrequencybins(indicatedbyleaders)aresquared Drift in some exemplars is very large and likely would
andintegratedtoyieldband-limitedpowerinunitsofacceleration makeimpossibleintegrationof thosedatatoretrievedisplace-
squared); finally, the root is taken to compute acceleration– ment,acriticalfunctionforengineering applications.Mostof
amplituderatios.Thenumericalspectralamplituderatioisshown
|     |     |     |     |     |     |     |     | the sensors | have | very modest |     | drift over | time, | driftmost | likely |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ---- | ----------- | --- | ---------- | ----- | --------- | ------ |
in that panel as well; the records in (a) have been scaled caused by small temperature variations during the tests. Even
accordingly. someClass-Aaccelerometershavesignificanttemperaturesen-
sitivity;ANSSrecommendsthatallaccelerometersandrecord-
ers,beatleastmodestlyinsulatedfromtemperaturevariations.
| orientations | are | relative | to the | sensor | case axes | (the latter | by  |     |     |     |     |     |     |     |     |
| ------------ | --- | -------- | ------ | ------ | --------- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
comparingoutputsduetogravityineachoftheg-normalori-
entationsthatarehighlysensitivetodeviationsfromhorizon- TRANSFER-FUNCTION TESTS
| tal). Finally, | returning |     | the box | to  | its original |     | upright |     |     |     |     |     |     |     |     |
| -------------- | --------- | --- | ------- | --- | ------------ | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
orientation allows a rough estimate of sensor drift over time. Transfer functions (TFFs, also called response functions)
| Class A | and ClassB | accelerometers |     | are | expected | to be | within |          |           |     |       |        |        |        |          |
| ------- | ---------- | -------------- | --- | --- | -------- | ----- | ------ | -------- | --------- | --- | ----- | ------ | ------ | ------ | -------- |
|         |            |                |     |     |          |       |        | describe | amplitude | and | phase | of the | sensor | output | relative |
1% of their expected sensitivities (ANSS, 2008), to have to motions input to the sensor. In this case, we did not have
modestinherentoffsetssothatsensorclippingremainsapprox-
adequatecontroloftimefortheinputsignals,socannotevalu-
| imately | symmetrical | about | their | resting | output | levels | and do |     |     |     |     |     |     |     |     |
| ------- | ----------- | ----- | ----- | ------- | ------ | ------ | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
atephase.Mostmacroscopic(i.e.,traditionalnon-MEMS)and
notclipasymmetrically,andtohavetrueactivesensitivityaxes accelerometers, including all those reported here, are
MEMS
within1°ofthecaseaxes,whichareusedduringdeploymentto
|     |     |     |     |     |     |     |     | nearly flat | from | 0 Hz | to near | a fairly | high-corner |     | frequency |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ---- | ---- | ------- | -------- | ----------- | --- | --------- |
orient the sensors to the Earth or to buildings, bridges, and (typically ≥100 Hz). Analog-to-digital converters (ADCs)
otherstructuresofinterest.Inthisinstance,becausewedonot
|                                  |     |     |     |     |                       |     |     | and processing |        | by recorders |     | typically | lead    | to amplitude | roll       |
| -------------------------------- | --- | --- | --- | --- | --------------------- | --- | --- | -------------- | ------ | ------------ | --- | --------- | ------- | ------------ | ---------- |
| haveaccesstotherawoutputsofthese |     |     |     |     | MicroElectricalMecan- |     |     |                |        |              |     |           |         |              |            |
|                                  |     |     |     |     |                       |     |     | off at lower   | corner | frequencies, |     | and       | control | that         | portion of |
ical Systems (MEMS) accelerometers, we use the continuous the TFF. In the case of these Class-C sensors, these matters
| time seriesas | recordedby |     | supporting | software, |     | and then | mea- |     |     |     |     |     |     |     |     |
| ------------- | ---------- | --- | ---------- | --------- | --- | -------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
arecontrolledlargelywithinthesensoritself;thedigitizeddata
sure the mean output levels of appropriate segments of those aretransferredtothehostcomputerviaaUSBconnectionand
| data (e.g., | Figs. 1 | and | 2). |     |     |     |     |                            |                   |           |     |                             |       |          |       |
| ----------- | ------- | --- | --- | --- | --- | --- | --- | -------------------------- | ----------------- | --------- | --- | --------------------------- | ----- | -------- | ----- |
|             |         |     |     |     |     |     |     | canbefurthermodifiedduring |                   |           |     | sample-rateadjustmentsasde- |       |          |       |
|             |         |     |     |     |     |     |     | scribed in                 | the Introduction. |           |     |                             |       |          |       |
| Results     |         |     |     |     |     |     |     | We                         | measured          | amplitude |     | response                    | using | a linear | shake |
These Class-C accelerometers are of significantly variable table to input sine wave motion at various amplitudes and
accuracy, with that variation sometimes dependent on which frequencies(slightlyimperfectsines,e.g.,solidlinesinFig.2a),
(Ⓔ
axis or individual device is considered Table S1 available and comparing the output signals with these input reference
Seismological Research Letters Volume 85, Number 1 January/February 2014 149

(a) (b)
(c) (d)
(e) (f)
▴ Figure 3. (a–f) Credible amplitude ratios versus frequency for each model tested. Note varying computational methods.
150 Seismological Research Letters Volume 85, Number 1 January/February 2014

signals. In two cases (smart phones and GCDC), sample rates theprimarycauseofdifferencesinFigures3and4betweenthe
werenotstableandaccurate,sosimplerootmeansquare(rms) evident corner frequencies.
amplituderatiosinthetimedomainhadtobeused.Theserms We also observe soft shouldered behavior below their
ratiosarequitesensitivetosensorandothernoise,particularly cornerfrequencies;thisfeatureisquitevisiblenear10Hz.This
fortheweaksignalsrequiredatlongperiods,whicharelimited soft-shoulderedfeatureisequivalenttoover-dampinganoscil-
inaccelerationbythe40cmeffectivelengthoftheshaketable. lator, and in this instancemeans thatthesensor responses fall
In all other cases, a more accurate spectral method was below the widely used −3 dB in-band limit, well below the
used,comparingthetotalpowerinthefivefrequencybinssur- nominalcornerfrequency,atanywherefromabout7to80Hz.
roundingtheexpected(andnearlyalwayspeak)sinefrequency, Commonly,Class-A instruments are nearly flat to about 80%
asshowninFigure2b.Theuseofonlythefivebinsofthepeak of the Nyquist frequency then fall sharply, this largely con-
spectralresponsegreatlyimprovessignal-to-noiseratiosbynar- trolled by the ADC. It is likely that the Class-C sensors use
rowing the bandwidth of the noise; it has shown itself many internaloversampling anddigitaldecimationofsometypebe-
timestoproducecredibleresultsoverawiderrangeoffrequen- causeMEMSaccelerometersaremechanicallyalmostflatinthe
ciesthansimplerms(particularlyatlowfrequencieswherein- seismic band, because they have natural frequencies of several
put signals are limited by the shake-table length) for many hundredhertzorabove.However,thereisachancethatanalog
typesof sensors.Simplermsoftenfailsquitebadly,greatlyde- filtering is applied in their feedback loops, and we could not
viating from expected responses where the spectral method separatetheseeffects.AssumingthatADCdigitalfilteringdomi-
does not. An example of our analysis results for a single fre- natesClass-Caccelerometerresponses,theirresponsesarelikely
quencysinewaveisshowninFigure2;thesine-wavesegment somethingakintothesincn(cid:2)x(cid:3)(cid:4)(cid:5)sin(cid:2)x(cid:3)=x(cid:6)ndecimationfilters,
isselected byananalyst(thefirstfewsecondsof thatsegment which are common in low-cost delta-sigma ADCs, including
are shown in Fig. 2). In this seriesof tests,we lackedan inde- those in the GeoSIG/USGS NetQuakes Class-B instrument.
pendent reference sensor for the shake table so we generated Ifdesired,suchsofteningnearthecornerfrequencycanbe
synthetic sine waves of the known input amplitude and fre- partially deconvolved to something more like typical Class-A
quency, but no phase information, and took amplitude ratios accelerographswithrelativeeaseduring processing,arelatively
relative to this synthetic sine wave. stable partial deconvolution. NetQuakes and all other ANSS
|     |     |     |     |     | data are | stored | without | deconvolutions |     | of any | type, | but are |
| --- | --- | --- | --- | --- | -------- | ------ | ------- | -------------- | --- | ------ | ----- | ------- |
storedasis,butwithTFFspecificationsintheirmetadata.This
Results
|              |                |           |               |                       | practice      | leaves any | deconvolution |           | under   | the       | control     | of users. |
| ------------ | -------------- | --------- | ------------- | --------------------- | ------------- | ---------- | ------------- | --------- | ------- | --------- | ----------- | --------- |
| Most of      | these sensors  | had to    | be upsampled, | typically from        |               |            |               |           |         |           |             |           |
|              |                |           |               |                       | Similarly,    | Class-C    | data          | would     | also be | stored    | unmodified, | but       |
| 50 samples=s | 200            | samples=s |               |                       |               |            |               |           |         |           |             |           |
|              | to the         |           | we            | normally use for such |               |            |               |           |         |           |             |           |
|              |                |           |               |                       | with theirTFF |            | in the        | metadata. |         |           |             |           |
| analyses     | and a standard | in ANSS.  | Phidgets      | had to be down-       |               |            |               |           |         |           |             |           |
|              |                |           |               |                       | The           | smart      | phones        | could     | not be  | evaluated | for         | theirTFFs |
200 samples=s,
sampled slightly, from 250 to which we use exceptinthemostgeneralsenseusingasimplermsratiointhe
theMATLABfunctionresample(),andanintegerratioofup-
|     |     |     |     |     | time domain; |     | waveforms | were | peculiar. | GCDCs |     | had good |
| --- | --- | --- | --- | --- | ------------ | --- | --------- | ---- | --------- | ----- | --- | -------- |
sample,thendownsampleveryclosetotheideal,typicallyparts
|     |     |     |     |     | waveforms, | but | because | of sample |     | skipping | the sample | rate |
| --- | --- | --- | --- | --- | ---------- | --- | ------- | --------- | --- | -------- | ---------- | ---- |
perbillion,and,inthiscase,exactwitharatiooffourup,then
|     |     |     |     |     | was not | stable | enough | for spectral | analysis; |     | their simple | rms |
| --- | --- | --- | --- | --- | ------- | ------ | ------ | ------------ | --------- | --- | ------------ | --- |
fivedown.Thelowsampleratesoftheothersensorslikelyare
|     |     |     |     |     | ratios in | the time | domain | yield | reasonable | results. |     | The other |
| --- | --- | --- | --- | --- | --------- | -------- | ------ | ----- | ---------- | -------- | --- | --------- |
sensorswereevaluatedwiththespectralratiotechnique.They
|     |     |     |     |     | all exhibit     | a more        | or less | flat       | response   | at low         | frequency      | with       |
| --- | --- | --- | --- | --- | --------------- | ------------- | ------- | ---------- | ---------- | -------------- | -------------- | ---------- |
|     |     |     |     |     | one overdamped  |               | corner  | at high    | frequency. | This           | pattern        | is in      |
|     |     |     |     |     | general         | conformity    | with    | Class-A    | and        | Class-B        | accelerometers |            |
|     |     |     |     |     | though          | the sharpness |         | and phase  | of the     | high-frequency |                | corner     |
|     |     |     |     |     | rolloff varies, | most          | often   | in amanner |            | controlled     | by             | the delta- |
|     |     |     |     |     | sigma ADC       | decimation    |         | filtering. |            | The non-MEMS   |                | force-     |
feedbackaccelerometersoftypicalClass-Aaccelerometersmay
|     |     |     |     |     | have natural   | frequencies    |           | near            | the          | seismic | passband         | (e.g.,    |
| --- | --- | --- | --- | --- | -------------- | -------------- | --------- | --------------- | ------------ | ------- | ---------------- | --------- |
|     |     |     |     |     | 100 Hz)        | and contribute |           | significantly   |              | to the  | overall          | response. |
|     |     |     |     |     | CLIP AND       | LINEARITY      |           | TESTS           |              |         |                  |           |
|     |     |     |     |     | The degree     | to             | which     | the sensitivity |              | of each | accelerometer    | is        |
|     |     |     |     |     | constant       | at a fixed     | frequency |                 | with changes | in      | input            | accelera- |
|     |     |     |     |     | tion amplitude |                | is called | linearity.      | At           | some    | high amplitudes, |           |
▴ Figure4. Asummaryofamplituderesponsesforallmodels,in sensitivitydeparts froman acceptably linearresponseby more
each case selecting those examples believed to be the most than about 1% of its lower-amplitude sensitivity, which is
accurate and representative. Colors indicate sensor models termed as the soft clipping acceleration level. Above a some-
(O-NaviAandBareessentiallyidentical,soBisdifficulttosee). whathigheramplitude,thesensoroutputdoesnotchangewith
Seismological Research Letters Volume 85, Number 1 January/February 2014 151

(a) (b)
(c) (d)
▴
Figure5. Examplesoftimeseriesusedforclip/linearitytests:(a)timeseriesofanentiresequenceofamplitudesatonefrequency(light
and dark gray are the off-axis components); (b) an example of typical clipping (gray in upper panel; ignore phase); (c) an example of
adequateclippingbehavior;and(d)anexampleofforce-to-valueclipping,whichappearstohavebeencorrectedinproductionversions.
increasingamplitude—thehardclippingamplitude.Normally, wouldlooknormaluptothesoft-clipamplitude,thenprogres-
softandhardclippingareveryclosetogetherandgenerallynot sivelydistorteduptothehard-clipamplitudeatwhichitwould
distinguished,butsomeoftheseClass-Csensorsappeartosoft becomeaconstantuntiltheinputsignalfellbelowtheclipping
clip significantly for unknown reasons. amplitudes, there resuming normal appearance. Although the
Theinputsandanalysisforclippingandlinearityprogress spanbetween soft and hard clipping may be infinitesimal,the
muchasTFFtests,buttheinput-sineshaking isheldatoneor amplitude ratio will decrease only slowly because a distorted,
more fixed frequencies while a range of amplitudes is applied then clipped, sine still has a lot of energy at the original sine
(Fig.5a);inthiscase,weinputasmanyasptenamplitudesfrom frequency (Figs. 5 and 6); when clipping, the amplitude ratio
0:25g to 2:5g at a midband frequency 4 2 Hz. For a given decreases because the input amplitude is increasing, whereas
frequency,onehopestoseeaflatsensitivityresponseexpressed theapparentoutputamplitudestaysaboutthesame.Thus,soft
as output/input ratio to within a few percent of the hard- clippingmaybeevidentonlytotheeyeinthetimedomainor
clipping amplitude, and then some kind of gentle rolloff in ifoneperformedsomethinglikeaharmonicdistortiontest.We
which the output signal becomes a cleanly clipped sine wave. did not correct forTFF or 0 Hz sensitivity before performing
In the time domain, a clipped sine wave for a typical sensor this test.
152 Seismological Research Letters Volume 85, Number 1 January/February 2014

(a) (b)
Z−on-axis; Droid SN 2
Z−on-axis; Droid SN 3 and 4
(c) (d)
Y; JWF14 SN 1
(not corrected)
(e) (f)
▴
Figure6. Summaryofclipandlinearitytesting;spectralamplituderatiomethodifnototherwisestated.Thedashedhorizontallines
showtheexpectedratio(unity)(cid:1)1%ofthatratio(linearscale),themaximumspanexpectedbytheANSSinClass-AandClass-Bsensors.
Herewehaveshiftedtounity,theamplituderatioofeachsensoratthermsofa1gsine(6:9 m=s2,exceptGCDCcorrectedatrmsof2g),
effectivelycorrectingthemforindividualsensitivityerrorsatthatamplitude.Theverticalsolidlinesshowexpectedclippingamplitudes;
vertical scaling differs between models. Model and axes are indicated by text and line type.
Seismological Research Letters Volume 85, Number 1 January/February 2014 153

Results ofthosesixsensorsbeing(cid:1)1g devicessothattheyshouldclip
Examplesofwaveformsandanalysiswhenthesensorsaredriven atlowamplitude;theotherthreeare(cid:1)2g andbehaveaboutas
beyond their hard-clip level are given in Figure 5b–d. They well as the O-Navi and Phidgets sensors. The model 1056
exhibitareasonablytypicalclippingpattern(Fig.5b),asimilar Phidgets and O-Navi A and B behaved well, as did the hori-
patterndistortedbysensorandupsamplingfilters(Fig.5c),and zontal axes of the GCDC. The (cid:1)2g JWF14, model 1056
the single Phidgets prototype, which, when clipped to a fixed Phidgets,and O-NaviAandB sensorsallshowloweroutputs
value,causeslargeexcursionsfromtheotheramplitudeextremes atlowfrequencies;thisresultmaysimplybeduetohighersig-
(Fig.5d).Thelatterapparentlyhasbeenchangedinproduction nal-to-noiseatthosefrequenciesasaresultofthesmallerinput-
modelstothesymmetricalclippingfamiliarinseismologyand sine amplitudes. The behavior of Z axes of the GCDC and
engineering. smartphonesensorsmaybeduetoprematureclipping caused
AssummarizedinFigure6,mostofthesensorsclippedin byin-sensorcorrectionsforthe1g gravitationalfieldnormally
a reasonably well-behaved manner, rolling over above their seen by Z axes.
nominal clipping amplitudes; however, there are a number of
exceptions. As mentioned, the single prototype Phidgets
(model 1043) clipped atypically (Fig. 5d), though we believe NOISE TESTS
this has been corrected in production versions. The smart
phones clipped asymmetrically; the cause is not clear. The The noise generated by the sensor itself is a measure of the
JWF14 sensors exhibit two behaviors and variation within smallest signals that can be resolved by that instrument, and
each.Mostoftheoutwardlyprematureclippingisduetothree along withclippinglevelsdetermineitsusefuloperatingrange
▴
Figure7. Operatingrangesforthetestedsensorsrangefromthenoisefloor(half-octavetotalrms)totheclippinglevel(rmsofjust-
clipping 2g sine). Box-like features are caused by integrating to half-octaves narrowband peaks, which are of little impact to sensor
performance.Allsensorsrolloffattheiranti-aliascorners,setbytheirsamplerates;thePhidgethasthehighestsuchcornerbecauseof
itshigh-samplingrate.Large-EventExamplesareatthepeakamplitude(times0.707forcomparisontormsnoise)andspanthehalf-width
of their spectrum.
154 Seismological Research Letters Volume 85, Number 1 January/February 2014

(Holcomb, 1989; Sleeman et al., 2006; Evans et al., corrections and the baseline-corrections we apply. It is the
2010, 2012).
|            |     |            |              |           |      |         | amplitudes | and waveforms | of the input | steps that | need to be |
| ---------- | --- | ---------- | ------------ | --------- | ---- | ------- | ---------- | ------------- | ------------ | ---------- | ---------- |
| Instrument |     | self noise | is generally | estimated | from | records | recovered  | accurately.   |              |            |            |
recorded,whenthesensorsarefixedtoalow-noisepierduring We use the same linear shake table as forTFF and clip/
alate-nightintervalwithlowculturalandwindnoise.InClass- linearitytests,butinputaroundedsquarewaveindisplacement
A and Class-B accelerometers, background ambient noise at (400 mm peak to peak; peak accelerations ∼0:5g; peak veloc-
thetestsitesometimescanbeseenevenundertheseconditions, ities∼800 mm=s;period11.6s;andastationarywaitingperiod
so a coherency method is used to estimate which part of the ateachendoftheshaketableof5s).Eachexcursionfromone
noise is inherent to the sensor, while rejecting coherent por- ∼0:77 s)
|     |     |     |     |     |     |     | end of | the table to | the other (transit | duration |     |
| --- | --- | --- | --- | --- | --- | --- | ------ | ------------ | ------------------ | -------- | --- |
tions of the noise as likely caused by external seismic or elec- amountstoaquasi-permanentdisplacementoffsetofthekind
tronic sources. Ambient seismic noise is dominantly from that must be recovered reliably.
| oceanic | microseisms | and local | cultural | and | weather | sources, |            |              |                   |     |             |
| ------- | ----------- | --------- | -------- | --- | ------- | -------- | ---------- | ------------ | ----------------- | --- | ----------- |
|         |             |           |          |     |         |          | Recovering | displacement | from acceleration | is  | formally an |
so is coherent between collocated sensors on the same pier. underdeterminedproblem(zerosensoroutputat0Hz),which
InthecaseoftheseClass-Csensors,however,thesensornoise
|     |     |     |     |     |     |     | has led to | many methods | for preprocessing | the | acceleration |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ------------ | ----------------- | --- | ------------ |
iswellabovethesitenoise,whichmadethecoherencemethod recordstoremoveormitigateartifactsduetofixedordrifting
andevennightrecordingunnecessary.Instead,allofthesensor
offsets,forexample.Commonly,theanalystremovesmeansor
| output is | attributed | to instrument |     | noise. | We did | not correct |             |                  |         |                   |         |
| --------- | ---------- | ------------- | --- | ------ | ------ | ----------- | ----------- | ---------------- | ------- | ----------------- | ------- |
|           |            |               |     |        |        |             | trends from | the acceleration | record, | applies a low-cut | filter, |
forTFFor0Hzsensitivitybeforeperforming thistest;asmall then performs a numerical integration twice. This method
| amount | of the noise | variation | seen | results | from | variations in |            |              |               |           |           |
| ------ | ------------ | --------- | ---- | ------- | ---- | ------------- | ---------- | ------------ | ------------- | --------- | --------- |
|        |              |           |      |         |      |               | works well | for records, | which have no | permanent | displace- |
0 Hz sensitivity, but this is a tiny correction. ments.However,wedesiretorecoverpermanentdisplacements
andcannotusealow-cutfilter;wefitalinetotheresultofthe
Results firstintegration(velocity),correcttheaccelerationaccordingly,
andⒺTable
Figure 7,with onelinepermeasuredaxis, S2of and then double integrate the corrected acceleration to dis-
the electronic supplement summarize our noise results as well placement.WedidnotcorrectforTFFor0Hzsensitivitybe-
as showing a clipping level at the rms of a just-clipping (2g foreperforming thistest,butthesignalsarelargelyunaffected
peak)sinewave.Thespanbetweenthesemetricsfromrmsclip because these are midband signals other than during the 5 s
tormsnoiseistheusefuloperatingrangeofeachsensor.There motionlessperiods; amplitudes will vary some, but waveforms
isawiderangeofinstrumentnoiselevelsamong thesedevices should be a good match.
(43dB∼140×inamplitudenear1Hz)fromtheworst(smart
| phones) | to the | best (two | axes of | the single |     | tested). |     |     |     |     |     |
| ------- | ------ | --------- | ------- | ---------- | --- | -------- | --- | --- | --- | --- | --- |
GCDC
| Phidgets | are the | next quietest. | We  | obtained | only | one noise | Results |     |     |     |     |
| -------- | ------- | -------------- | --- | -------- | ---- | --------- | ------- | --- | --- | --- | --- |
sample,thatforadifferentindividualthantestedatASL;that The results of our double-integration tests are shown in
Figure8a–f,eachlabeledbysensormodel.Severalsensorsper-
Phidgetshasausefuloperatingrangeof78dBat1Hz.Equiv-
alentbitsresolution(peakonly,i.e.,onesidedandone-bitless formpoorlyin thistest (Figs.8a–c)inthesenseofnotrecov-
thanpeak-to-peakresolution)areshownattherightmarginof
|     |     |     |     |     |     |     | ering waveforms | well or | having large extraneous |     | excursions in |
| --- | --- | --- | --- | --- | --- | --- | --------------- | ------- | ----------------------- | --- | ------------- |
thefigureandrangefromabout8to16usefulbits(9–17bits
|     |     |     |     |     |     |     | displacement;thesesensorsincludethesmartphones, |     |     |     | JWF14, |
| --- | --- | --- | --- | --- | --- | --- | ----------------------------------------------- | --- | --- | --- | ------ |
peak-to-peak).ⒺThesummaryinTableS2showsequivalent andtwoofsixaxesoftheGCDC(thelattermaybecausedby
bits resolution for the full peak-to-peak range. missing samples during peak accelerations). Smart phone and
|     |     |     |     |     |     |     | GCDC sampling | problems | are also clear | in the | uneven step |
| --- | --- | --- | --- | --- | --- | --- | ------------- | -------- | -------------- | ------ | ----------- |
DOUBLE-INTEGRATION TESTS durationsmostevidentinaccelerationtraces;theyshouldover-
lapveryclosely,asdotheothersensors.Hysteresisiseasilyseen
Attempting to recover transient or permanent displacement inthevelocitytracesofallmodels,butparticularlyinthesmart
signalsfromaccelerationrecordsisahighlysensitive,butnon- phones, JWF14,andGCDC(thesametwotracesmentioned).
specific, test of end-to-end system viability for strong-motion The O-Navi A and B have noticeable hysteresis that does not
work. This is an important test because engineers and many seemtodistortthedisplacementresult,thoughtherearevisible
second-orderchangesintrendatanumberoflargerhysteretic
| seismologists | must | use acceleration |     | records | to recover | perma- |     |     |     |     |     |
| ------------- | ---- | ---------------- | --- | ------- | ---------- | ------ | --- | --- | --- | --- | --- |
nent displacements (e.g., near-field fault fling and interstory steps.ThePhidgetshaveslightdrift,butnoevidenthysteresis.
drift, permanent structural deformation; Çelebi et al., 2004; Long-period wandering of the displacement baselines is
Çelebi, 2008; Chopra, 2012). The test is highly sensitive typical of these tests using our simple processing method,
because even very tiny acceleration steps, changes in trend, whichdoesnotproperlyaccountforexponentialacceleration-
missingsamples,hysteresis,andotherproblemsaregreatlyam- baselinedriftduetotemperaturevariationsandperhapsother
plified by the integration process into large signals that are sources. The remaining drift amplifies into the displacement
easily identified; in some cases, these errors in displacement wanderseen,butisofnoimportancehereandisseenroutinely
arecomparabletoorlargerthantheinputsignal.Long-period in Class A and Class B sensors tested this way. Earthquake
wanderinthedisplacementtracesisnormalinourexperience records would be similarly affected by temperature etc., how-
(Classes A and B), because of imperfections in temperature ever, for such valuable records, custom, if demanding baseline
Seismological Research Letters Volume 85, Number 1 January/February 2014 155

(a) (b)
(c) (d)
(e) (f)
(g)
▴ Figure8. Doubleintegrationresultsforalltestedaxes.Figures(a–f)arelabeledbysensormodel;alltracesevaluatedforagivenmodel
areshowninthatfigureandcanbedistinguishedbycolor(whichhasnoothermeaning).Panel(g)istheapproximateinputdisplacement
waveform.Withineachfigure,thecorrectedaccelerationtracesandresultingvelocityanddisplacementestimatesareshown;in(b)the
large greenandblue chevrons arelarge displacementsclipped to allowplotting. Displacement reveals overall performance, whereas
velocity shows hysteresis most clearly and acceleration shows the best sample-rate stability.
correctionsgenerallyallowonetorecoverdisplacementsbetter able amplitude and waveform, but not duration because of
than the automated method used for Fig. 8. sample-rateinstability,exceptinthetwothatseemtobemiss-
Stepamplitudesandwaveformsseemreasonablygoodfor ing a critical sample during high-acceleration intervals.
theO-NaviAandBandthePhidgets.TheGCDChasreason- The smart phones sensors perform very poorly in waveform,
156 Seismological Research Letters Volume 85, Number 1 January/February 2014

|     |     |     |     |     |     |     |     | 9:79188087 | m=s2 |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ---- | --- | --- | --- | --- | --- | --- |
whereasJWF14 sensors intermittently recover reasonable am- . We correct all our results from the local
plitudes and some semblance of waveforms, but are otherwise value of g to the standard value.
quite poor. A note on trademarks: Trademarked or otherwise re-
strictednamesusedinthisreportincludeDroid,GoogleNexus
CONCLUSIONS One, HTC Magic, iPhone, O-Navi LLC, Phidgets Inc., Joy-
|     |     |     |     |     |     |     |     | Warrior, | and Code | Mercenaries |     | Hard- | und | Software | GmbH, |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | -------- | ----------- | --- | ----- | --- | -------- | ----- |
GulfCoastDataConcepts(GCDC),Excel,GeoSIG,Kinemet-
| Ⓔ Table | S3 summarizes |     | the performance |     | of  | sensors | in each |     |     |     |     |     |     |     |     |
| ------- | ------------- | --- | --------------- | --- | --- | ------- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
ricsSMA-1,andMATLAB.Anyuseoftrade,firm,orproduct
| test with | a mix | of objective | and | interpretive |     | rankings | among |          |                 |     |          |      |     |      |           |
| --------- | ----- | ------------ | --- | ------------ | --- | -------- | ----- | -------- | --------------- | --- | -------- | ---- | --- | ---- | --------- |
|           |       |              |     |              |     |          |       | names is | for descriptive |     | purposes | only | and | does | not imply |
thefivemodelstested,aswellasasummaryranking.Thesen-
sors exhibit a very wide range of performance: three are pres- endorsement by the U.S. Government.
| ently unacceptable |        | per          | general | ANSS    | guidance; |       | two are |     |     |     |     |     |     |     |     |
| ------------------ | ------ | ------------ | ------- | ------- | --------- | ----- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
| acceptable         | as is, | both O-Navis |         | (though | sample    | rates | need to |     |     |     |     |     |     |     |     |
REFERENCES
behigherthanarepresentlyprovidedbyQCN)andthePhidg-
ets.TheO-Navisensorshavelessthanidealoffsets.Overall,the
ANSSTechnicalIntegrationCommittee(TIC)(2002).Technicalguide-
Phidgetsmayhavetheedgeinperformancebecauseofsmaller
|                |             |     |            |           |     |           |      | lines          | for the | implementation |       | of the          | Advanced | National | Seismic  |
| -------------- | ----------- | --- | ---------- | --------- | --- | --------- | ---- | -------------- | ------- | -------------- | ----- | --------------- | -------- | -------- | -------- |
| offsets, lower | hysteresis, |     | and higher | currently |     | available | sam- |                |         |                |       |                 |          |          |          |
|                |             |     |            |           |     |           |      | System,version |         | 1.0, U.S.      | Geol. | Surv. Open-File |          | Rept.    | 02-9296. |
ple rates. ANSSWorkingGrouponInstrumentation,Siting,Installation,andSite
If operated at relatively high sample rates Metadata of the Advanced National Seismic System Technical
|     |     |     |     |     |     |     |     | Integration |     | Committee | (2008). |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | --------- | ------- | --- | --- | --- | --- |
(100–200 samples=s), either O-Navi or Phidgets sensors Instrumentation Guidelines for
|     |     |     |     |     |     |     |     | the Advanced |     | National | Seismic | System, | U.S. Geol. | Surv. | Open-File |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --- | -------- | ------- | ------- | ---------- | ----- | --------- |
shouldproducedataofusetoANSS,ifthosedatacanbeprop-
|     |     |     |     |     |     |     |     | Rept. | 2008-1262, | 41  | pp. |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | ---------- | --- | --- | --- | --- | --- | --- |
erlytaggedasClass-Ctoensurethattheirusesareappropriate. Çelebi,M.(2008).Real-timemonitoringofdriftforoccupancyresump-
Asmentionedabove,analoginstrumentsofsignificantlylower
|     |     |     |     |     |     |     |     | tion,     | Proc. 14th | World    | Conference |               | on Earthquake |     | Engineering |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---------- | -------- | ---------- | ------------- | ------------- | --- | ----------- |
|     |     |     |     |     |     |     |     | (14WCEE), |            | Beijing, | 12–17      | October 2008. |               |     |             |
resolutionwereusedforsomedecadesandproducedmuchuse-
|     |     |     |     |     |     |     |     | Çelebi, M., | A. Sanli, | M. Sinclair, |     | S. Gallant, | and D. | Radulescu | (2004). |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --------- | ------------ | --- | ----------- | ------ | --------- | ------- |
fulinformation.Theirdatafoundmanyapplications,including
Real-Timeseismicmonitoringneedsofabuildingowner—andthe
| reliablepicturesofregionalseismicityandstrong |     |                      |     |     |          | shaking,and |     |            |               |          |         |                |         |                     |     |
| --------------------------------------------- | --- | -------------------- | --- | --- | -------- | ----------- | --- | ---------- | ------------- | -------- | ------- | -------------- | ------- | ------------------- | --- |
|                                               |     |                      |     |     |          |             |     | solution:  | A cooperative |          | effort, | Earthq.        | Spectra | 20, 333–346.        |     |
| several generations                           |     | of earthquake-safety |     |     | building | codes.      |     |            |               |          |         |                |         |                     |     |
|                                               |     |                      |     |     |          |             |     | Chopra, A. | K. (2012).    | Dynamics |         | of Structures, | 4th     | Ed., Prentice-Hall, |     |
ThereareanumberofpotentialpathstocreateaClass-C
|     |     |     |     |     |     |     |     | Upper     | Saddle | River,      | New Jersey, | International |         | Series | in Civil En- |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | ------ | ----------- | ----------- | ------------- | ------- | ------ | ------------ |
|     |     |     |     |     |     |     |     | gineering | and    | Engineering | Mechanics,  |               | 992 pp. |        |              |
instrumentcompatiblewithcurrentANSSoperations,inpar-
ticularwiththeANSSEarthwormsoftwaresystem,forcapture Cochran,E.S.,J.F.Lawrence,C.Christensen,andR.Jakka(2009).The
|     |     |     |     |     |     |     |     | Quake-Catcher |     | Network: |     | Citizen | science | expanding | seismic |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- | -------- | --- | ------- | ------- | --------- | ------- |
andanalysisofseismicdata.Thereareatleasttwosuchpathsin
|     |     |     |     |     |     |     |     |           |          |      |       | 80, 26–30. |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | -------- | ---- | ----- | ---------- | --- | --- | --- |
|     |     |     |     |     |     |     |     | horizons, | Seismol. | Res. | Lett. |            |     |     |     |
developmentandlikelyotherswedonotknowof;inanycase
Evans, J.R.,F.Followill,C.R.Hutt,R.P.Kromer,R.L.Nigbor,A.T.
the details of those implementations will change over time so Ringler, J.M.Steim,andE.Wielandt(2010).Methodforcalculat-
Ⓔ
are not listed here. Table S4 is a list of parts that could be ingself-noisespectraandoperatingrangesforseismographicinertial
sensorsandrecorders,Seismol.Res.Lett.81,640–645,doi:10.1785/
| used in | a hypothetical |     | high-end | Class-C | DAS, | simply | as an |     |     |     |     |     |     |     |     |
| ------- | -------------- | --- | -------- | ------- | ---- | ------ | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
gssrl.81.4.640.
| example | of the | available | options | and | likely | cost ranges. |     |     |     |     |     |     |     |     |     |
| ------- | ------ | --------- | ------- | --- | ------ | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Evans, J.R.,F.Followill,C.R.Hutt,R.P.Kromer,R.L.Nigbor,A.T.
In all, these results are hopeful, suggesting that it may be Ringler, J.M.Steim,andE.Wielandt(2012).Methodforcalculat-
possibletointegratesomeClass-CinstrumentsintoANSSop-
ingself-noisespectraandoperatingrangesforseismographicinertial
83,
erations to produce information useful to ShakeMap (Wald sensors and recorders, Erratum, Seismol. Res. Lett. 586, doi:
10.1785/gssrl.83.3.588.
etal.,1999),seismologicalresearch,andearthquakeengineering.
Holcomb,L.G.(1989).Adirectmethodforcalculatinginstrumentnoise
levelsinside-by-sideseismometerevaluations,U.S.Geol.Surv.Open-
|     |     |     |     |     |     |     |     | File | Rept. 89-214, | 35  | pp. |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | ------------- | --- | --- | --- | --- | --- | --- |
ACKNOWLEDGMENTS Hutt, C. R., J. R. Evans, F. Followill, R. L. Nigbor, and E. Wielandt
(2010).Guidelinesforstandardizedtestingofbroadbandseismom-
|               |     |         |         |       |     |      |           | eters | and accelerometers, |     | U.S. | Geol. Surv. | Open-File |     | Rept. 2009- |
| ------------- | --- | ------- | ------- | ----- | --- | ---- | --------- | ----- | ------------------- | --- | ---- | ----------- | --------- | --- | ----------- |
| The Community |     | Seismic | Network | (CSN; | R.  | Guy) | is funded | 1295, | 62 pp.              |     |      |             |           |     |             |
byGordonandBettyMooreFoundationandNSFawardCNS
|     |     |     |     |     |     |     |     | Hutt, C. | R., J. Peterson, |     | L. Gee, | J. Derr, | A. Ringler, | and | D. Wilson |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ---------------- | --- | ------- | -------- | ----------- | --- | --------- |
(2011).AlbuquerqueSeismologicalLaboratory—50yearsofglobal
| 0932392;     | special | thanks          | to Leif | Strand | of CSNfor |         | authoring |             |      |       |       |            |            |     |     |
| ------------ | ------- | --------------- | ------- | ------ | --------- | ------- | --------- | ----------- | ---- | ----- | ----- | ---------- | ---------- | --- | --- |
|              |         |                 |         |        |           |         |           | seismology, | U.S. | Geol. | Surv. | Fact Sheet | 2011-3065, | 4   | pp. |
| the Phidgets | testing | application(s). |         | The    | Quake     | Catcher | Net-      |             |      |       |       |            |            |     |     |
work (QCN; E. Cochran, J. Lawrence, and A. Chung) is a Luetgert, J.H., J.R.Evans, J.Hamilton,C.R.Hutt,E.G.Jensen,and
D.H.Oppenheimer(2009).NetQuakes—Anewapproachtour-
joint project of theUSGS and Stanford University. MyShake ban strong-motion seismology, AGU Fall Meeting S11B-1707.
| (Droid | smart phones; |     | R. Allen) | is  | funded | by  | Deutsche |           |                          |           |     |       |             |      |             |
| ------ | ------------- | --- | --------- | --- | ------ | --- | -------- | --------- | ------------------------ | --------- | --- | ----- | ----------- | ---- | ----------- |
|        |               |     |           |     |        |     |          | Luetgert, | J. H., J                 | Hamilton, | and | D. H. | Oppenheimer |      | (2010). The |
|        |               |     |           |     |        |     |          | NetQuakes | Project—Research-quality |           |     |       | Seismic     | Data | Transmitted |
Telekom.
“g”
A note on units: In this report the unit (in italics) is viatheInternetfromCitizen-hostedInstruments,AGUFallMeet-
| usedtomeantheaccelerationofgravityattheEarth’ssurface; |     |     |     |     |     |     |     | ing S51E-03. |            |         |     |             |         |               |     |
| ------------------------------------------------------ | --- | --- | --- | --- | --- | --- | --- | ------------ | ---------- | ------- | --- | ----------- | ------- | ------------- | --- |
|                                                        |     |     |     |     |     |     |     | Sleeman,     | R., A. van | Wettum, | and | J. Trampert | (2006). | Three-channel |     |
itdoesnotmeangrams(“g”notitalicized).One“standardg”is
correlationanalysis:Anewtechniquetomeasureinstrumentalnoise
9:80665 m=s2 , but at the siteof these experiments(Albuquer- 96, 258–
|     |     |     |     |     |     |     |     | of digitizers | and | seismic | sensors, | Bull. | Seismol. | Soc. Am. |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | --- | ------- | -------- | ----- | -------- | -------- | --- |
1g
que Seismological Laboratory) the local value of is 271, doi: 10.1785/0120050032.
Seismological Research Letters Volume 85, Number 1 January/February 2014 157

Wald,D.J.,V.Quitoriano,T.H.Heaton,H.Kanamori,C.W.Scrivner, A. I. Chung
andC.B.Worden(1999).TriNet“ShakeMaps”:Rapidgeneration
|     |     |     |     | J. F. | Lawrence |
| --- | --- | --- | --- | ----- | -------- |
ofinstrumentalgroundmotionandintensitymapsforearthquakes
|                                 | 15, 537–556. |           |             | Department of | Geophysics |
| ------------------------------- | ------------ | --------- | ----------- | ------------- | ---------- |
| in southern California, Earthq. | Spectra      |           |             |               |            |
|                                 |              |           |             | Stanford      | University |
|                                 |              | Stanford, | California, | U.S.A.        | 94305-2215 |
J. R. Evans
|             |                     |        |            | E.               | S. Cochran |
| ----------- | ------------------- | ------ | ---------- | ---------------- | ---------- |
| Earthquake  | Hazards Science     | Center |            |                  |            |
|             |                     |        | Earthquake | Hazards Science  | Center     |
|             | U.S. Geological     | Survey |            |                  |            |
|             |                     |        |            | U.S. Geological  | Survey     |
|             | 400 Natural Bridges | Drive  |            |                  |            |
| Santa Cruz, | California 95060    | U.S.A. |            | 525 South Wilson | Avenue     |
|             |                     |        | Pasadena,  | California 91106 | U.S.A.     |
jrevans@usgs.gov
R. Guy
R. M. Allen
|     |     |     |     | Seismological | Laboratory |
| --- | --- | --- | --- | ------------- | ---------- |
M. Hellweg
Department of Earth and Planetary Sciences California Institute of Technology
|                      |               |          | 1200      | East California  | Boulevard |
| -------------------- | ------------- | -------- | --------- | ---------------- | --------- |
| University           | of California | Berkeley |           |                  |           |
|                      |               |          | Pasadena, | California 91125 | U.S.A.    |
| Berkeley, California | 94720-4760    | U.S.A.   |           |                  |           |
158 Seismological Research Letters Volume 85, Number 1 January/February 2014