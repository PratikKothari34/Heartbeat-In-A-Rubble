MEMS Accelerometer Mini-Array
(MAMA): A Low-Cost Implementation for
Earthquake Early Warning Enhancement
Ran N. Nof,a),b) Angela I. Chung,a) Horst Rademacher,a) Lori Dengler,c)
and Richard M. Allena)
Earthquake Early Warning Systems (EEWS) are often challenged when the
earthquakes occur outside the seismic network or where the station density is
sparse.Inthesesituations,poorlocationsandlargealertdelaysaremorecommon
becauseofthelimitedazimuthalcoverageandthetimerequiredforthewavefield
toreachtheminimumnumberofseismicstationstoissueanalert.Seismicarrays
can be used to derive the directivity of the wavefield and obtain better location.
However, they are uncommon because of the prohibitive cost of the sensors.
Here,weproposethedevelopmentofanarray-basedapproachusingmini-arrays
oflow-costMicroelectromechanicalSystems(MEMS)accelerometersandshow
how they can be used to improve EEWS. In this paper, we demonstrate this
approach using data from two MEMS Accelerometer Mini-Arrays (MAMA)
deployed at University of California Berkeley and Humboldt State University.
We use a new low-cost (<U.S. $150) Data Acquisition Unit and solve for the
back azimuth of seven events with magnitudes ranging from Mw 2.7 to 5.1
at distances of 5km to 106km. [DOI: 10.1193/021218EQS036M]
INTRODUCTION
AsignificantproblemfacedbyEarthquakeEarlyWarningSystems(EEWS)isthecorrect
characterizationofearthquakesthatoccurateithertheedgeoforoutsideoftheseismicnetwork.
Because of poor azimuthal coverage, location estimate errors can be considerable (Figure 1).
The median location error for earthquakes occurring outside of the Northern California EEW
seismicnetworkforM≥4eventsbetween1February2016andSeptember11,2017,detected
bytheElarmSEEWS(Kuyuketal.2014)is44.4km,withastandarddeviationof49.9km.In
contrast, the median location error for all M≥4 eventsthat occurred within the Northern and
SouthernCalifornianetworksduringthesametimeperiodisjust4.0km,withastandarddevia-
tion of 26.5km.Without accurate locationestimates, EEWS cannot correctly estimate ground
shaking, and they are then unable to deliver timely alerts to affected areas.
Seismic arrays have been used for nuclear test monitoring and seismological research
since the 1960s (e.g., Birtill and Whiteway 1965). They are commonly used to obtain
the slowness vector of the wavefield and to increase signal-to-noise ratio (SNR). Despite
a)BerkeleySeismologyLab,UniversityofCaliforniaBerkeley,Berkeley,CA94703;Email:ran.nof@gmail.com
(R. N.N.)
b)Geological SurveyofIsrael, Jerusalem, Israel9550161
c)Geology Department,Humboldt StateUniversity, Arcata, CA95521
21
EarthquakeSpectra,Volume35,No.1,pages21–38,February2019;©2019,EarthquakeEngineeringResearchInstitute

22 NOFETAL.
Figure 1. Map of M≥4 earthquakes occurring within (stars) or outside of (circles) California
EEWseismicnetwork(triangles)between1February2016andSeptember11,2017,anddetected
by ElarmS, colored by distance error from the ANSS catalog locations. Note that there is one
event in Southern California on 10 June 2016 with a distance error of 153km because ofsome
traces picking on the S-wave. Without this event, the median distance error is 3.9km, with a
standard deviation of 9.0km for earthquakes within the network.
theobviousadvantagesoverregularseismicnetworks,seismicarraysarenotverycommon
worldwide. One reason they are not frequently used is the high cost of augmenting each
network station with further conventional seismic sensors to give it array functionality.
Here, we describe the development of an array-based approach using low-cost Microelec-
tromechanical Systems (MEMS) accelerometers.
MEMScapacitiveaccelerometersaredeviceswithaverysmallfootprint(micrometersto
afewmillimetersinsize)andwithlowpowerconsumption.Theyarecapableofmeasuring
relativegravitationalchanges(Middlemissetal.2015).MEMShavebeenusedinseismology
sincethebeginningofthemillennium(Holland2003).Recently,severalattemptsweremade
to include class-C [Advanced National Seismic System (ANSS) 2008] low-cost MEMS
accelerometersinseismologicalinvestigations,mainlybyusingdensenetworksofsuchsen-
sors (e.g., Clayton et al. 2015). The individual instruments can be attached to volunteers’
computers (e.g., Cochran et al. 2009), or they can be installed as independent instruments
atindividualhosts(e.g.,Claytonetal.2011)orinpublicbuildingssuchasschools,hospitals,
andplacesofworship(e.g.,D’Alessandro2014).Anotherapproachistoexploitanetworkof
built-in MEMS sensors in smartphones (Finazzi 2016, Kong et al. 2016).

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 23
Low-costMEMSsensorshavealsobeenusedtorapidlycreateseismicnetworks,monitor-
ing aftershock seismic activity following large events (e.g., Chung et al. 2011, Lawrence
etal.2014).Becauseoftheirlowprice,lowpower,andsmallsize,alargenumberofdevices
canbedeployedinashorttime.AnotheruseofMEMSaccelerometersinseismologicalresearch
is to combine them with single-channel GPS devices to resolve baseline errors (Minson et al.
2015,Tuetal.2013).Thedevelopmentofanearthquakeearlywarningalertingdevicebasedon
a MEMS sensor and a 10-bit digitizer has also been proposed (e.g., Zheng et al. 2011).
It is clear that these low-cost MEMS sensors with maximum resolutions of 16 bits are
capableofdetectingmoderatetolargeearthquakesatdistancesofseveraltensofkilometers
away (D’Alessandro andD’Anna 2013,Evans etal. 2014,Yildirim etal. 2015). With their
growth in popularity and commercial potential in many research fields, the sensitivity of
MEMS devices has significantly improved over time. For instance, between 2011 and
2013, the noise level of smartphone MEMS was reduced by ∼20dB at the bandwidth of
1–10Hz (Kong et al. 2016). Somepnew MEMS accelerometers currently being tested
have low noise floors of up to 2 ng/ Hz (Pike et al. 2014), while others have wider band-
width(aslowas10(cid:2)4Hz)andhigherresolutionbasedonresonancetechnology(Middlemiss
etal.2015,Zouetal.2014).Theseimprovementsledtotheuseofclass-BsensorsinEEWS
in Japan and Taiwan (Horiuchi et al. 2009, Wu 2015).
Availableoff-the-shelfclass-Csensorsare,however,limitedtodigitalsensorswithreso-
lutions of 16 bits or less or to analog sensors that require additional analog-to-digital con-
verter (ADC) units. In the following, we first describe our rationale for building a MEMS
Accelerometer Mini-Array (MAMA) and demonstrate its use to estimate the back azimuth
(BAZ) of local earthquakes. The array uses a new specially designed data acquisition unit
(DAU),whichisasingledevicewithintegratedclass-CMEMSsensor,24-bitdigitizer,and
data logger. Finally, we discuss how the application of MAMA can enhance EEWS.
MAMA DESIGN
Inordertomitigatethehighcostofinstallingaseismicarrayusingconventionalseism-
ometers,weproposetheuseofmultiplelow-costMEMSaccelerometerDAUs.Theywillbe
arranged as a MAMA with a small aperture of 200–1,000 m, preferably around an existing
conventionalseismometerorstrong-motionsensorwhereavailable.Ideally,oneoftheDAUs
should be colocated with the existing instrument. Such a layout is designed to improve the
recordingsofasingleconventionalnetworkstationbyemployingwell-knownarraymethods
whenever the epicentral distance is much greater (at least 10-times larger) than the array
aperture. For its power and telemetry needs, each DAU in the mini-array can draw from
the already available resources of the conventional station at remote locations or simply
be connected to dedicated power and Wi-Fi where available. Colocating one of the
DAUswiththeconventionalseismicinstrumentwillfurtherconstrainthepossibletimeshifts
between the time controllers of the traditional network and the MEMS DAU, which most
likely will be using Network Time Protocol. It can also be used for other quality control
evaluations based on the comparison of waveforms.
ThemajorlimitationofusingaMAMAisthehighintrinsicnoiseandlowsensitivityof
currentlyavailableclass-Clow-costMEMSsensors.Thoughthesedevicesarestillusablefor
analyzing large magnitude earthquakes or moderate earthquakes at shorter distances,

24 NOFETAL.
thelowerqualityofthesedeviceslimitsthemagnitudedetectionthreshold(Evansetal.2014).
Some examples of possible uses of MAMAs include calculating BAZ based on the arrival
timesateachnodeorsolvingfortheslownessvectorofawavefieldoritspropagationpattern
withinthearray.Forlargemagnitudeearthquakes,wheretherupturepropagatesalonglonger
fault traces, back-projecting the source location would make it possible to investigate fault
dimensions (Fletcher et al. 2006, Meng et al. 2014, Spudich and Cranswick 1984). The
method of back-projecting is commonly used at teleseismic distances and low frequencies.
Given the lower sensitivity of the MEMS and limited bandwidth, our approach is to use
MAMA for BAZ or back-projection at local distances and high frequencies of 1–10Hz
(AllmannandShearer2007).Inthefollowing,wedescribeournewDAUdevice,deployment,
and processing scheme.
MAMA DAU
Currently used off-the-shelf digital class-C MEMS accelperometers are limited to 16-bit
resolutionwithrootmeansquarenoiselevelsdownto45μg/ Hz(Evansetal.2014).Fora
fullscale(cid:3)2-gsensor,the16-bitdigitizercreatesamaximumresolution(minimalsingle-bit
value)of61μg/count,providedtheself-noiseofthesensorislower.Inaddition,off-the-shelf
sensorsneedtobeconnectedtoacomputeroradataloggerwithappropriatecodetomakethe
data available for further processing on site or at a remote data center (e.g., Clayton et al.
2015). We have developed a new low-cost (<U.S. $150) DAU (hereafter referred to as a
MAMA node). This unit consists of a printed circuit board (PCB) bearing four analog
MEMSaccelerometers((cid:3)2-grange)anda24-bitADC,anditiscombinedwithaRaspber-
ryPi single-board computer. The RaspberryPi serves as a data logger and is capable of pro-
viding online access to the 100 samples-per-second data streams via an onboard seedlink
server (for more technical details about the MAMA node, see online Appendix A).
p
TheMAMAnodesensor’sself-noiselevelof50μg/ Hzisatthelowerendofthenoise
range of most currently available off-the-shelf devices (Evans et al. 2014). In the current
version of MAMA node (Revision 0.3), we use four MEMS sensors in parallel to reduce
the noise by half and provide improvement of more than 15dB over off-the-shelf digital
accelerometers. Figure 2 shows the MAMA node’s mean power spectral density (PSD;
McNamara and Buland 2004) for a 1-day period measured at the Berkeley Byerly Vault,
which also houses the conventional seismic station BKS Episensor. We also measured
the well-tested Quake Catcher Network sensor O-Navi B (Evans et al. 2014) by replacing
thePCBonourMAMAnodewiththeO-NaviBsensorandadjustingthecodeappropriately.
For our frequency band of interest of 1 to 10Hz, the mean PSD levels are –73 to –80dB
(0.22(cid:4)10(cid:2)3(cid:2)0.1(cid:4)10(cid:2)3m2s(cid:2)4∕Hz),respectively(coloredlines,Figure2).Thisimprove-
ment, though still noisier than class-A strong-motion devices with noise levels lower than
–120dB, significantly improves our capability to obtain useful signals of small magnitude
eventsandallows ustotestourapproachwithoutneedingsignificanteventsto occurinthe
MAMA vicinity. Figure 3 shows a comparison between traces of a Güralp 5TC acceler-
ometer, a MAMA node, and an O-Navi B sensor placed at the Berkeley Byerly Vault for
a Mw 3.8 at 40km event. This figure demonstrates the improved sensitivity of the MAMA
node over the O-Navi B, which is one of the highest grade 16-bit sensors available (Evans
etal.2014),aswellasitscompatibilitywithahigh-endstandardforce-balancestrong-motion
sensor where the signal is above its noise levels.

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 25
Figure2. MeanPSD(McNamaraandBuland2004)ofarepresentativeMAMAnode(MAMA
Rev 0.3, blue line) and Quake Catcher Network’s O-Navi B 16-bit MEMS sensor (O-Navi B,
green line)installedattheBerkeleyByerlyVault.The conventionalstrongmotion sensor(Epi-
sensor)oftheBKnetworklocatedattheByerlyVaultismarkedasaredline(BKSstation)for
comparisonofbackgroundnoiselevels.LinesarethemeanPSDofthehorizontaltraces,between
1 September 2016 and 5 September 2016. Earthquake representative spectra responses are
marked as dark solid and dashed gray lines for near and far fields, respectively (Clinton and
Heaton2002).NewHighNoiseModel(Peterson1993)ismarkedasasolidgrayline.Earthquake
data converted to dB following Cauzzi and Clinton (2013).
MAMA DEPLOYMENT
We deployed two MAMA arrays (Figure 4a). The first, BRK M AMA, is at the Uni-
versity of California Berkeley campus and is composed of nine nodes around the seismic
station (BK.BRK) in Havilland Hall. The maximum distance between two MAMA nodes
is 1,200 m (Figure 4b). We placed the MAMA nodes in basement or ground floor offices
or in utility rooms. Each node was connected to a wall outlet for power and attached to the
floor(alignedtomagneticnorthusingacompass)withatwo-sidedtape.Wenotethatusing
thismethodwiththecouplingtothegroundisnotideal,butitisaveryrapid,low-cost,and
nonintrusivemethodsuitableforofficesandoccupiedurbanareas.Communicationwiththe
nodesisdoneviaWi-FiorEthernet.TheBRKMAMAwaspartlyoperationalattheendof
December 2016 and was fully deployed in May 2017.
The second MAMA setup is the Accessible Resources Center (ARC) MAMA at the
Humboldt State University campus. This array is composed of 13 nodes at nine locations

26 NOFETAL.
Figure 3. Comparison of north component from a MAMA node device (red), a Güralp 5TC
accelerometer(black),andanO-NaviBdevice(gray)foreventnc72795746,anMw3.78located
40.2km away. All devices were colocated at Berkeley Byerly Vault. Time is relative to origin
time. Traces are bandpass filtered between 1 and 10Hz.
(2 nodes are collocated at four locations). No standard station is available at this site. The
maximumdistancebetweentwonodesofthisMAMAis845m(Figure4c).Allsensorsare
locatedatutilityroomsandcommunicateoverEthernet.ARCMAMAhasbeenfullyopera-
tional since 9 March 2017.
Both BRK and ARC MAMA are located within the campuses where power and com-
munication are conveniently available, and MAMA node installations at utility rooms or
officesarestraightforward andsecured.BRKMAMAisin closeproximityto theHayward
Fault with the highest earthquake probability in the Bay Area (Field et al. 2017), and ARC
MAMAislocatedclosetotheMendocinoTripleJunction,oneofthemostseismicallyactive
regionsalongtheSanAndreasfaultsystemandwheretheseismicnetworkissparse.MAMA
node locations are based on the availability of suitable locations across the campuses.
USING MAMA TO SOLVE FOR BAZ
Aseismicarrayconsistsofnumerousseismicinstrumentslocatedwithinarelativelyclose
range of one another. Depending on the spacing of the sensors and the wavelength of
the signal,a wavefield passingthroughthe arraymayshowa coherent signal.Itis alsopos-
sible to observe the difference in arrival times of the wavefield at each of the instruments.
Coherency and arrival time offsets can be used to increase the SNR of a recording and to
derive the slowness vector. This can provide the directivity of the wavefield signal. For
more details on seismic arrays, see Harjes and Henger (1973), Rost and Thomas (2002,
2009), Schweitzer et al. (2011), and the references therein. Here, we concentrate on using
the array capability to calculate BAZ in order to improve the EEWS earthquake location.

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 27
Figure 4. MAMA location map. (a) General location map. (b) BRK MAMA at University of
California Berkeley campus, Berkeley, CA. BRK marks the location of the conventional BK.
BRK station at Haviland Hall. (c) ARC MAMA at Humboldt State University campus, Arcata,
CA. MAMA nodes are marked as triangles.
To calculate the BAZ, we used the freely available ObsPy (Beyreuther et al. 2010) FK
analysis tool. This tool uses frequency domain beamforming (i.e., Conventional or Bartlett
beamformer)tofindthemaximumofthepowerofthebeamgivendifferentslownessvectors
(Bartlett1950,HarjesandHenger1973,Nawabetal.1985).Foreachevent,wecalculatethe
maximumpower,normalizedbythesignalcovariance(relativepower)andthecorrespond-
ing BAZ and slowness using 1-s windows with 0.05-s steps.
Though we are aiming at developing a real-time processing module, we currently use an
automatedoff-lineprocessingscheme.Whilethereal-timemoduleshouldhaveitsownearth-
quake identifier,the current code isregularly querying USGS’s ANSSCatalog (see data and
resources section) for events of Mw>2.5 up to a 110-km radius from the MAMA center.

| 28  |     |     |     |     |     | NOFETAL. |     |
| --- | --- | --- | --- | --- | --- | -------- | --- |
WeautomaticallyprocessthewaveformsfromtheMAMAnodesandthestandardseismicsta-
tionasavailable,beginning20sbeforeandending40saftertheorigintimeoftheevent.Weuse
asimpleSTA/LTAtriggeringdetectortoidentifytheeventarrivalifmorethan40%ofalltraces
(two horizontals and one vertical for each node) have triggered with SNR above 5. Once an
event is labeled as “Identified,” the BAZ is then calculated using the following steps:
| 1. Detrend, | removing | a   | mean | value. |     |     |     |
| ----------- | -------- | --- | ---- | ------ | --- | --- | --- |
1–10Hz.
| 2. Bandpass | using | a Butterworth     |     | filter at |        |     |     |
| ----------- | ----- | ----------------- | --- | --------- | ------ | --- | --- |
| 3. Remove   | gain  | value, converting |     | to m∕s2   | units. |     |     |
4. Obtainarepresentativetracetr foreachnodefromthethreecomponents.Thisisto
| mitigate | misaligned | nodes: |     |     |     |     |     |
| -------- | ---------- | ------ | --- | --- | --- | --- | --- |
pffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffiffi
|     |     |     | tr  | ¼ N2þE2þZ2 |     | ·signðZÞ | (1) |
| --- | --- | --- | --- | ---------- | --- | -------- | --- |
EQ-TARGET;temp:intralink-;e1;41;505
where N, E, and U are the North, East and Z traces of the node, respectively. All
| following | processing |     | is done | on the representative |     | trace tr. |     |
| --------- | ---------- | --- | ------- | --------------------- | --- | --------- | --- |
5. UseasimpleSTA/LTAtriggertodetectfirstarrivaltimetotheMAMA.Calculate
theCumulativeCross-Correlationvalues(CCC)foreachnodeusingthefollowing
equations:
Xn
¼
|     |     |     |     | CCC                                 | cc  |     | (2) |
| --- | --- | --- | --- | ----------------------------------- | --- | --- | --- |
|     |     |     |     | i                                   |     | ij  |     |
|     |     |     |     | EQ-TARGET;temp:intralink-;e2;41;409 | j≠i |     |     |
P
tr ·tr
|     |     |     |     | cc ¼ qffi | P ffiffiffiffiffiffiffiffiffiffiiffiffiffiffiffi P | ffiffiffiffijffiffiffiffiffiffiffi | (3) |
| --- | --- | --- | --- | --------- | -------------------------------------------------- | ---------------------------------- | --- |
ij
|     |     |     |     | EQ-TARGET;temp:intralink-;e3;41;366 | tr2 · | tr2 |     |
| --- | --- | --- | --- | ----------------------------------- | ----- | --- | --- |
i j
where i indicates a node, and j iterates over the rest of the n nodes.
6. Where collocated nodes exist, discard the one with lower CCC values.
7. If CCC <meanðCCCÞ(cid:2)1.5·σðCCCÞ, then discard the trace with the lowest
CCC, recalculate CCC, and repeat discarding until a minimum of four traces
are left or no trace has such a low CCC value. This step helps to mitigate strong
| site effects |     | and poorly | coupled | nodes. |     |     |     |
| ------------ | --- | ---------- | ------- | ------ | --- | --- | --- |
8. BAZ process for a span of 2 s before the first trigger and 20 s after. Processing is
| done | using | a sliding | window | of 1 s and | a 0.05-s | step. |     |
| ---- | ----- | --------- | ------ | ---------- | -------- | ----- | --- |
9. Theprocessingresultsforeachwindowarethemaximalrelativepowerofthearray,
BAZ,andslowness.WederivethemeanBAZofallwindowswhererelativepower
15%
is within the top along the processing span and the slowness is below one to
exclude non–body wave signals and maintain relatively high coherence values.
RESULTS
Using the automatic processing scheme described above, between 9 March 2017 and 1
August2017,4outof23eventswereidentifiedbytheBRKMAMAand6outof33events
were identified by the ARC MAMA (Table 1). Of the identified events, we successfully
calculateBAZforthreeandfoureventsattheBRKandARCMAMAs,respectively.Figure5

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 29
| dna | tnorf-evaw |     |     |
| --- | ---------- | --- | --- |
deifitnedI
| KRB | S S | S S S P P | S P P |
| --- | --- | --------- | ----- |
morf
dradnats
| mk011 | noitaived |              |         |
| ----- | --------- | ------------ | ------- |
|       | A/N 3.77  | A/N A/N 8.08 |         |
|       |           | 6.0 6.8      | 1.0 5.2 |
1
ZAB
naht
ssel
detaluclaC
|          | 8.59 | 5.94 6.153 6.323 | 6.481 8.172 2.372 |
| -------- | ---- | ---------------- | ----------------- |
| ecnatsid | ZAB  |                  |                   |
|          | A/N  | A/N A/N          |                   |
dna
devresbO
| 5.2> | ZAB 151 79 | 55 85 552 153 323 | 591 462 282 |
| ---- | ---------- | ----------------- | ----------- |
edutingam
epyT
|     | dm wm | dm dm dm wm wm | wm wm wm |
| --- | ----- | -------------- | -------- |
htiw
|     | 87.3 | 27.2 25.2 26.2 35.3 20.3 | 30.4 11.5 75.4 |
| --- | ---- | ------------------------ | -------------- |
M 8.2
tneve
ecnatsiD
|     | )mk( 3.04 2.04 | 1.12 9.91 9.66 7.81 | 8.76 6.39 7.701 |
| --- | -------------- | ------------------- | --------------- |
| lla |                | 5                   |                 |
morf
stneve
|     | 70:12:11 91:92:10 | 30:05:22 95:65:70 90:43:91 92:91:21 02:00:91 | 30:22:12 04:20:00 62:80:71 |
| --- | ----------------- | -------------------------------------------- | -------------------------- |
golatac
emit
|     | nigirO 7102 7102 | 7102 7102 7102 7102 7102 | 7102 7102 7102 |
| --- | ---------------- | ------------------------ | -------------- |
SSNA
|     | hcraM lirpA | yaM yaM yaM enuJ enuJ | enuJ yluJ yluJ |
| --- | ----------- | --------------------- | -------------- |
deifitnedi
|     | 03  | 51 62 92 11 12 | 42 92 92 |
| --- | --- | -------------- | -------- |
9
|     | 64027727cn 64759727cn | 67910827cn 64660827cn 16970827cn 10141827cn 10191827cn | 16702827cn 15125827cn 64925827cn |
| --- | --------------------- | ------------------------------------------------------ | -------------------------------- |
DI
fo SSNA
| tsil | tneve |     |     |
| ---- | ----- | --- | --- |
A AMAM
.1 AMAM
elbaT
| CRA | CRA KRB | KRB KRB CRA CRA KRB | CRA CRA CRA |
| --- | ------- | ------------------- | ----------- |

30 NOFETAL.
Figure5. MAMAdetectionandBAZcalculationperformance.AlleventswithM>2.5andless
than 110km from a MAMA are plotted as triangles and squares for ARC and BRK MAMAs,
respectively. Red markers represent identified events with calculated BAZ within 30° of the
observed BAZ. Blue markers represent identified events with calculated BAZ more than 30°
different from the observed BAZ. Empty markers represent events unidentified by MAMA.
shows the BAZ and event identification threshold with respect to magnitude and distance.
Withtheavailabledata,weareabletocalculateBAZforearthquakeswithmagnitudesaslow
as Md 2.7 at 20km distance.
Toillustratetheprocessingresults,weshowinFigure6theresultsoftheFKanalysisof
eventnc72819101,whichoccurredon2017-06-21T19:00:20,withMw3atadistanceof5
km from the BRK MAMA. The observed BAZ between the MAMA center and the ANSS
catalog location is 323°. The mean calculated BAZ is 323.6°, with a standard deviation of
8.6°. The BAZ was obtained using just 1.8 s of data following the P-wave trigger. Event
nc72795746, which occurred on 2017-04-30T01:29:19, with Mw 3.78 at 41km away
from the BRK MAMA does not perform as well. The BAZ between the MAMA center
and the ANSS catalog location is 95°. Though the mean MAMA-estimated BAZ is
95.8°, which is very close to the observed BAZ, the standard deviation is 77.3° and the
BAZ rangesfrom –9.5°to 162°, as shownin Figure7.Finally,Figure 8shows an example
of event nc72806646, which occurred on 2017-05-26T07:56:59, with Mw 2.52 at 19.9km
away from the BRK MAMA. This event was identified by the automatic triggering, but it
failed to obtain BAZ using our current processing scheme because of low SNR. BAZ plots
for all the identified events listed in Table 1 are available in the online Appendix B.
DISCUSSION AND OUTLOOK
Comparing the MAMA nodes’ mean PSD noise floor with representative earthquake
spectralresponses(ClintonandHeaton2002)suggeststhatthenewMAMAnodedescribed

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 31
Figure6. BAZcalculationplotforeventnc728191012017-06-21T19:00:20,Mw3,5kmaway
from BRK MAMA. Subplots from the top are relative power, absolute power, BAZ, slowness,
and a typical MAMA node acceleration waveform with the trigger time marked by a dashed
red line. Each point represents the calculations done for a 1-s data window ending at point
positionalongx-axis.Colorsrepresenttheamplitudeoftherelativepowervalues.Theobserved
BAZ between the MAMA center and the ANSS catalog location is 323°. The mean calculated
BAZ is 323.6°, with a standard deviation of 8.6°. This result was obtained 1.8 s after the
trigger time.
abovehasthepotentialtodetectpeakaccelerationsofMw>2.5earthquakesat∼10kmand
Mw>3.0 at ∼100km (Figure 2). Indeed, the current MAMA node (Rev 0.3) was able to
detect a Mw 2.5 at 20km using our automatic processing scheme.
Though our results correspond well to the expected performance of our low-cost DAU,
therearesomelimitations.Thelownumberofeventsdetected,withrespecttothenumberof
events at a 100-km range, is a result of the low sensitivity of the sensors and the method’s
sensitivitytolowSNR.Thissensitivitylimitsthenumberofeventsavailableforprocessing
andobtainingBAZ results.Typically for EEW,destructive earthquakesof Mw>4.5are of

32 NOFETAL.
Figure 7. Similar to Figure 6, BAZ calculation plot for event nc72795746 2017-04-
30T01:29:19, Mw 3.78, 41km away from BRK MAMA. The observed BAZ between the
MAMA center and the ANSS catalog location is 95°. The mean calculated BAZ is 95.8°,
with a standard deviation of 77.3°. The result was obtained 1.65 s after the trigger time.
interestformitigationactions.However,testingandtrainingtheEEWSaswellasthepublic
wouldrequireahigherrateofevents,whichmaynotbeavailableeverywhere.Forthatrea-
son, higher sensitivity is required to be able to obtain BAZ results for lower magnitudes
events, which are more common.
Our new devices, when arranged in mini-arrays, can be used for improved source char-
acterizationthatcouldbeparticularlyimportantforEEW.Asdemonstrated,theMAMAcan
be used to rapidly obtain the BAZ of an event 2–3 s after the arrival of P-waves to the
MAMA, depending on the SNR. To illustrate a potential use of MAMA, Figure 9 shows
an example of a mislocated Mw 4.5 event on 5 December 2016 near Petrolia, CA. The
BAZ from the second station to detect the event, Station NC.KMPB, to the ANSS location
is 236°, while the BAZ to the ElarmS location of first alert is 303°. Assuming a MAMA
aroundstationNC.KMPBanda5-sdelaytoprocessthedataandcalculatetheBAZ,abetter

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 33
Figure 8. Similar to Figure 6, BAZ calculation plot for event nc72806646 2017-05-
26T07:56:59, Mw 2.52, 19.9km away from BRK MAMA. The observed BAZ between the
MAMAcenterandtheANSScataloglocationis58°.TheBAZcouldnotbecalculatedbecause
of the low SNR.
locationmightbeachievedwithoutdelayingthealerttime,whichwassent6safterP-wave
arrival to the station. The large alert time delay is due to an ElarmS requirement that four
stations must have detected an event before an alert can be sent out. Combining multiple
MAMA may make it possible to robustly estimate the epicenter of an earthquake based
on just two arrays instead of the current requirement of four stations. This would decrease
the time needed for point source EEWS to issue an alert, especially where the seismic
network is sparse.
InadditiontoprovidinginformationaboutBAZforpoint-sourceearthquakes,theevolu-
tion of BAZ information during a large magnitude event can provide more detailed source
characterization. Using local high-frequency energy back projection (e.g., Allmann and
Shearer2007,Mengetal.2014)allowsfortheestimationoftherupturepropagationpattern
(speed, duration, directivity, segmentation) and the better estimation of the total rupture

34 NOFETAL.
Figure9. ElarmSreviewtoolsnapshotofthefirstalertofMw4.5earthquakethatoccurredon5
December2016at18:55.YellowcirclemarkstheANSScataloglocation(latitude:40.28,long-
itude:–124.39);greencirclemarksElarmScalculatedlocation.Seismicstationsusedforsolving
the event parameters are marked as green triangles, while other stations are marked as blue tri-
angles.TheblindzoneismarkedasaredcircleandthepropagatingS-wavefrontinincrementsof
1 s are marked as white circles.
length. Implementing MAMA back projection in real time and incorporating that into
EEWS (Meng et al. 2014) could improve estimates of earthquake magnitude and shaking
intensity distribution based on finite-fault models rather than point-source models. Other
methods for estimating rupture size through the finite-fault approach have been developed
for EEWS using Global Navigation Satellite Systems stations (e.g., Allen and Ziv 2011,
Crowell et al. 2016, Grapenthin et al. 2014, Minson et al. 2014) or dense seismic stations
(e.g., Böse et al. 2015). Using a MAMA deployed around an existing seismic station will
allowacost-effectiveaugmentationofthestationaswellasenablefinite-fault-basedEEWS
in remote areas with sparse stations or no GPS measurements.
Finally,theredundantdataoftheMAMAcanalsobeusedtoeliminatefalsetriggersand
compute more robust event classifications, thus mitigating false alerts more common at the
edgeoftheseismicnetwork(Chungetal.2016).Therobustnessandrapidityofthesolutions
obtainedusingMAMAcansignificantlyimprovewarningtimesfornaturalhazardssuchas
earthquakes and tsunamis, providing better estimation of source parameters and expected
ground shaking (Melgar et al. 2016).
CONCLUSIONS
We have discussed the potential benefits of using MAMA in EEWS and seismological
research.Byexploitingarrayprocessingapproaches,cost-effectiveMAMAcanbeusedfor

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 35
faster,morereliableearthquakelocationsolutions,faulttracedimensionestimation,andrup-
turepropagationcharacterizationaswellastosupportEEWSnetworks,particularlyaround
theedgesofnetworksandinsparselyinstrumentedregions.MAMAnodescanaugmentan
existingseismicstationorbeusedasanadditionallower-qualitystationtodensifyaseismic
network(e.g.,Wu2015).ThelimitedresourcesneededtoinstallaMAMAnodealsomakeit
appealing for fast deployment and crisis response.
WehaveshownexamplesoftheusefulnessofMAMAbycalculatingtheBAZforseveral
earthquakesusingournewMAMAnodes.WehavedescribedaprototypeofaMEMSDAU,
whichincludestelemetrycapabilitiesandadataloggerwithalimitedproductioncostofless
thanU.S.$150,whichcanbefurtherloweredbymassproduction.Thoughthedeviceisstill
under development, initial results and noise measurements show it can theoretically detect
Mw 2.5 and larger events at 10km and Mw 4.5 and larger at 100km (Figure 2) using a
frequencybandof1–10Hz.Usingnine-nodeMAMAs,currentlydeployedattheUniversity
ofCaliforniaBerkeleyandattheHumboldtStateUniversitycampuses,wedemonstrateBAZ
calculationsofseveneventsrangingfromMw2.7toMw5.1anddistancesrangingfromas
nearas5kmtoover100km.FutureworkwillincludeimprovingMAMAnodesanddeploy-
ingmoreMAMAsatvariouslocationsaswellasimplementingBAZcalculationsinrealtime
(e.g., Eisermann et al. 2018).
ACNOWLEDGMENTS
RanN.NofwasfundedbyafellowshipfromtheGeologicalSurveyofIsrael(GSI),atthe
Ministry of Energy and Water Resources, and the project was supported by the United
States–Israel Binational Science Foundation and the Raymond and Beverly Sackler Fund
for Convergence Research in Biomedical, Physical and Engineering Sciences. The authors
would like to thank the Berkeley Seismology Lab Technicians, George Dorian and Zack
Alexy, and Oren Huber, Soenke Moeller, Eli Megidish, Andy Morrish, and Anatoli
Mordakhay for their tips and help with the MAMA Node PCB design. Figures in this
paper were produced by Python 2D plotting module Matplotlib (Hunter 2007) and
ObsPy (Beyreuther et al. 2010). Background maps tiles are downloaded from ESRI
world street map service: http://server.arcgisonline.com/ArcGIS/rest/services/Canvas/
World_Light_Gray_Base/MapServer (last accessed August 5, 2017). Waveform data for
this study are available upon request at the Northern California Earthquake Data Center
(Stations names are BK.BRKXX..HN? and BK.ARCXX..HN?, where XX is in the range
of01–12and20–33fortheBRKandARCMAMAs,respectively;the“?”maybereplaced
byE,N,orZforchannelorientation).Wewouldliketothanktheeditor,JonathanP.Stewart,
the Associateeditor, AntoninoD’Alessandro, andtwoother anonymousreviewers for their
comments and suggestions to improve this manuscript.
APPENDICES
Pleaserefertotheonlineversionofthismanuscripttoaccessthesupplementarymaterial
provided in Appendices A and B.
REFERENCES
Allen, R. M., and Ziv, A., 2011. Application of real-time GPS to earthquake early warning,
Geophysical Research Letters 38, 1–7.

36 NOFETAL.
Allmann,B.P.,andShearer,P.M.,2007.Spatialandtemporalstressdropvariationsinsmallearth-
quakes near Parkfield, California, Journal of Geophysical Research: Solid Earth 112, 1–17.
AdvancedNationalSeismicSystemTechnicalIntegrationCommitteeWorkingGrouponInstru-
mentation, Siting, Installation, and Site Metadata, 2008. Instrumentation Guidelines for the
AdvancedNationalSeismicSystem,Report2008-1262,U.S.GeologicalSurveyReston,VA.
Bartlett, M. S., 1950. Periodogram analysis and continuous spectra, Biometrika 37, 1–16.
Beyreuther,M.,Barsch,R.,Krischer,L.,Megies,T.,Behr,Y.,andWassermann,J.,2010.ObsPy:
A Python toolbox for seismology, Seismological Research Letters 81, 530–533.
Birtill, J. W., and Whiteway, F. E., 1965. The application of phased arrays to the analysis of
seismic body waves, Philosophical Transactions of the Royal Society A: Mathematical,
Physical and Engineering Sciences 258, 421–493.
Böse,M.,Felizardo,C.,andHeaton,T.H.,2015.Finite-FaultRuptureDetector(FinDer):going
real-time in Californian ShakeAlert Warning System, Seismological Research Letters
86, 1692–1704.
Cauzzi, C., and Clinton, J., 2013. A high- and low-noise model for high-quality strong-motion
accelerometer stations, Earthquake Spectra 29, 85–102.
Chung, A. I., Allen, R. M., Henson, I., Hellweg, M., and Neuhauser, D., 2016. ElarmS 2015
performance and new Filterbank Teleseismic Filter, in Seismological Society of America
Annual Meeting, 20–22 April, 2016, Reno, NV.
Chung,A.I.,Neighbors,C.,Belmonte,A.,Miller,M.,Sepulveda,H.H.,Christensen,C.,Jakka,
R.S.,Cochran,E.S.,andLawrence,J.,2011.TheQuake-CatcherNetworkRapidAftershock
Mobilization Program following the 2010 M 8.8 Maule, Chile Earthquake, Seismological
Research Letters 82, 526–532.
Clayton,R.W.,Heaton,T.,Chandy,M.,Krause,A.,Kohler,M.,Bunn,J.,Guy,R.,Olson,M.,
Faulkner, M., Cheng, M., Strand, L., Chandy, R., Obenshain, D., Liu, A., and Aivazis, M.,
2011. Community seismic network, Annals of Geophysics 54, 738–747.
Clayton,R.W.,Heaton,T.,Kohler,M.,Chandy,M.,Guy,R.,andBunn,J.,2015.Community
Seismic Network: a dense array to sense earthquake strong motion, Seismological Research
Letters 86, 1–10.
Clinton, J. F., and Heaton, T. H., 2002. Potential advantages of a strong-motion velocity meter
over a strong-motion accelerometer, Seismological Research Letters 73, 332–342.
Cochran,E.,Lawrence,J.,Christensen,C.,andChung,A.,2009.Anovelstrong-motionseismic
network for community participation in earthquake monitoring, IEEE Instrumentation and
Measurement Magazine 12, 8–15.
Crowell,B.W.,Schmidt,D.A.,Bodin,P.,Vidale,J.E.,Gomberg,J.,RenateHartog,J.,Kress,
V.C.,Melbourne,T.I.,Santillan,M.,Minson,S.E.,andJamison,D.G.,2016.Demonstration
of the Cascadia G-FAST Geodetic Earthquake Early Warning System for the Nisqually,
Washington, Earthquake, Seismological Research Letters 87, 930–943.
D’Alessandro,A.,2014.MonitoringofearthquakesusingMEMSsensors,CurrentScience107,
733–734.
D’Alessandro, A., and D’Anna, G., 2013. Suitability of low-cost three-axis MEMS
accelerometersinstrong-motionseismology:testsontheLIS331DLH(iPhone)accelerometer,
Bulletin of the Seismological Society of America 103, 2906–2913.
Eisermann, A. S., Ziv, A., and Wust-Bloch, H. G., 2018. Array-based earthquake location for
regionalearthquakeearlywarning:casestudiesfromtheDeadSeaTransform,Bulletinofthe
Seismological Society of America 108, 2046–2053.

MAMA:ALOW-COSTIMPLEMENTATIONFOREARTHQUAKEEARLYWARNINGENHANCEMENT 37
Evans,J.R.,Allen,R.M.,Chung,A.I.,Cochran,E.S.,Guy,R.,Hellweg,M.,andLawrence,J.F.,
2014. Performance of several low-cost accelerometers, Seismological Research Letters
85, 147–158.
Field, E. H., Jordan, T. H., Page, M. T., Milner, K. R., Shaw, B. E., Dawson, T. E., Biasi, G.,
Parsons,T.E.,Hardebeck,J.L.,Michael,A.J.,Weldon,R.,Powers,P.,Johnson,K.M.,Zeng,
Y., Bird, P., Felzer, K., van der Elst, N., Madden, C., Arrowsmith, R., Werner, M. J., and
Thatcher, W. R., 2017. A synoptic view of the third uniform California Earthquake Rupture
Forecast (UCERF3), Seismological Research Letters 88, 1259–1267.
Finazzi, F., 2016. The Earthquake Network Project: toward a crowdsourced smartphone-based
earthquake early warning system, Bulletin of the Seismological Society of America 106,
1088–1099.
Fletcher,J.B.,Spudich,P.,andBaker,L.M.,2006.Rupturepropagationofthe2004Parkfield,
California,earthquakefromobservationsattheUPSAR,BulletinoftheSeismologicalSociety
of America 96, S129–S142.
Grapenthin, R., Johanson, I., and Allen, R. M., 2014. The 2014 Mw 6.0 Napa earthquake,
California:observationsfromreal-timeGPS-enhancedearthquakeearlywarning,Geophysical
Research Letters 41, 8269–8276.
Harjes, H. P., and Henger, M., 1973. Array-Seismologie, Zeitschrift für Geophysik 39,
865–905.
Holland,A.,2003.EarthquakedatarecordedbytheMEMSaccelerometer:fieldtestinginIdaho,
Seismological Research Letters 74, 20–26.
Horiuchi,S.,Horiuchi,Y.,Yamamoto,S.,Nakamura,H.,Wu,C.,Rydelek,P.A.,andKachi,M.,
2009. Home seismometer for earthquake early warning, Geophysical Research Letters 36,
L00B04.
Hunter,J.D.,2007.Matplotlib:A2Dgraphicsenvironment,ComputinginScience&Engineer-
ing 9, 90–95.
Kong,Q.,Allen,R.M.,Schreier,L.,andKwon,Y.W.,2016.MyShake:asmartphoneseismic
network for earthquake early warning and beyond, Science Advances 2, e1501055.
Kuyuk, S. H., Allen, R. M., Brown, H., Hellweg, M., Henson, I., and Neuhauser, D., 2014.
Designing a network-based earthquake early warning algorithm for California: ElarmS-2,
Bulletin of the Seismological Society of America 104, 162–173.
Lawrence,J.F.,Cochran,E.S.,Chung,A.,Kaiser,A.,Christensen,C.M.,Allen,R.,Baker,J.
W., Fry, B., Heaton, T., Kilb, D., Kohler, D., and Taufer, M., 2014. Rapid earthquake
characterization using MEMS accelerometers and volunteer hosts following the M 7.2
Darfield, New Zealand, earthquake, Bulletin of the Seismological Society of America 104,
184–192.
McNamara, D. E., and Buland, R. P., 2004. Ambient noise levels in the Continental United
States, Bulletin of the Seismological Society of America 94, 1517–1527.
Melgar,D.,Allen,R.M.,Riquelme,S.,Geng,J.,Bravo,F.,Baez,J.C.,Parra,H.,Barrientos,S.,
Fang, P., Bock, Y., Bevis, M., Caccamise, D. J., II, Vigny, C., Moreno, M., and Smalley,
R., Jr., 2016. Local tsunami warnings: perspectives from recent large events, Geophysical
Research Letters 43, 1109–1117.
Meng, L., Allen, R. M., and Ampuero, J. P., 2014. Application of seismic array processing
to earthquake early warning, Bulletin of the Seismological Society of America 104,
2553–2561.
Middlemiss,R.P.,Samarelli,A.,Paul,D.J.,Hough,J.,Rowan,S.,andHammond,G.D.,2016.
Measurement of the earth tides with a MEMS gravimeter, Nature 531, 614–617.

38 NOFETAL.
Minson,S.E.,Brooks,B.A.,Glennie,C.L.,Murray,J.R.,Langbein,J.O.,Owen,S.E.,Heaton,
T. H., Iannucci, R. A., and Hauser, D. L., 2015. Crowdsourced earthquake early warning,
| Science | Advances 1, e1500036. |     |     |     |     |
| ------- | --------------------- | --- | --- | --- | --- |
Minson,S.E.,Murray,J.R.,Langbein,J.O.,andGomberg,J.S.,2014.Real-timeinversionsfor
finite fault slip models and rupture geometry based on high-rate GPS data, Journal of
| Geophysical | Research: | Solid Earth | 119, 3201–3231. |     |     |
| ----------- | --------- | ----------- | --------------- | --- | --- |
Nawab, S. H., Dowla, F. U., and Lacoss, R. T., 1985. Direction determination of wideband
signals, IEEE Transactions on Acoustics, Speech, and Signal Processing 33, 1114–1122.
Peterson,J.,1993. Observations andModeling ofSeismicBackground Noise, USGSOpen File
| Report 93-322, | U.S. Geological | Survey, | Reston, | VA. |     |
| -------------- | --------------- | ------- | ------- | --- | --- |
Pike,W.T.,Delahunty,A.K.,Mukherjee,A.,Dou,G.,Liu,H.,Calcutt,S.,andStandley,I.M.,
2014. A self-levelling nano-g silicon seismometer, in Proceedings of IEEE SENSORS 2014,
| 2–5 November, | 2014, | Valencia, Spain. |     |     |     |
| ------------- | ----- | ---------------- | --- | --- | --- |
Rost, S., and Thomas, C., 2002. Array seismology: methods and applications, Reviews of
| geophysics | 40, 1–2. |     |     |     |     |
| ---------- | -------- | --- | --- | --- | --- |
Rost, S., and Thomas, C., 2009. Improving seismic resolution through array processing techni-
| ques, Surveys | in Geophysics | 30, 271–299. |     |     |     |
| ------------- | ------------- | ------------ | --- | --- | --- |
Kühn,
Schweitzer, J., Fyen, J., Mykkeltveit, S., Gibbons, S. J., Pirli, M., D., and Kvaerna, T.,
2011. Seismic arrays, in New Manual of Seismological Observatory Practice (NMSOP-2)
(P.Bormann,ed.),GFZGermanResearchCentreforGeosciences,Potsdam,Germany,1–80.
Spudich,P.,andCranswick,E.,1984.Directobservationofrupturepropagationduringthe1979
Imperial Valley Earthquake using a short baseline accelerometer array, Bulletin of the Seis-
2083–2114.
| mological | Society of America | 74, |     |     |     |
| --------- | ------------------ | --- | --- | --- | --- |
Tu,R.,Wang,R.,Ge,M.,Walter,T.R.,Ramatschi,M.,Milkereit,C.,Bindi,D.,andDahm,T.,
2013. Cost-effective monitoring of ground motion related to earthquakes, landslides, or vol-
canicactivitybyjointuseofasingle-frequencyGPSandaMEMSaccelerometer,Geophysical
| Research | Letters 40, 3825–3829. |     |     |     |     |
| -------- | ---------------------- | --- | --- | --- | --- |
Wu,Y.M.,2015.Progressondevelopmentofanearthquakeearlywarningsystemusinglow-cost
| sensors, | Pure and Applied | Geophysics | 172, | 2343–2351. |     |
| -------- | ---------------- | ---------- | ---- | ---------- | --- |
Yildirim,B.,Cochran,E.S.,Chung,A.,Christensen,C.M.,andLawrence,J.F.,2015.Onthe
reliabilityofQuake-CatcherNetworkEarthquakeDetections,SeismologicalResearchLetters
856–869.
86,
Zheng,H.,Shi,G.,Zeng,T.,andLi,B.,2011.WirelessearthquakealarmdesignbasedonMEMS
accelerometer,in2011IEEEInternationalConferenceonConsumerElectronics,Communi-
16–18
| cations | and Networks | (CECNet), | April, | 2011, XianNing, | China. |
| ------- | ------------ | --------- | ------ | --------------- | ------ |
Zou, X., Thiruvenkatanathan, P., and Seshia, A. A., 2014. A seismic-grade resonant MEMS
768–770.
| accelerometer, | Journal   | of Microelectromechanical |       | Systems  | 23,           |
| -------------- | --------- | ------------------------- | ----- | -------- | ------------- |
|                | (Received | 12 February               | 2018; | Accepted | 20 July 2018) |