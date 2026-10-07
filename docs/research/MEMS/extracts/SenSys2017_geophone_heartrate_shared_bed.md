> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> Jia, Bonde, Li, Xu, Wang, Zhang, Howard, Zhang, *"Monitoring a Person's Heart Rate and
> Respiratory Rate on a Shared Bed Using Geophones"*, **ACM SenSys '17**, Delft, 6-8 Nov 2017,
> DOI 10.1145/3131672.3131679. Source PDF deleted after conversion (gitignored).
>
> Cited in `MEMS/03-literature.md` (entry 10), `MEMS/01-requirements.md`, `MEMS/05-verification-log.md`,
> `MEMS/README.md` and `BUDGET/01-literature.md`. An earlier hand-made extract was deleted
> 2026-10-08 as orphaned after confirming its figures survive in `research/MEMS/`; this replaces
> it with the full text.
>
> **Geophones under a bed sense ballistic force from the heartbeat**, handling the hard case of
> two people on one mattress, free to move.
>
> **Must be cited AND distinguished, for the same reason as HeartQuake.** This paper recovers a
> cardiac signal with the same *class* of sensor this project selects, so a reviewer who finds it
> unaided will read it as contradicting the kill. The difference is the coupling path, not the
> sensor: a geophone **contact-coupled through bedding, centimetres from the torso**, versus
> **metres of rubble**. The cardiac deficit at 3 m is ~31-53 dB; nothing in this paper addresses
> propagation loss through debris.

Monitoring a Person’s Heart Rate and Respiratory Rate on a
Shared Bed Using Geophones
ZhenhuaJia†,AmelieBonde§,SugangLi†,ChenrenXu‡,JingxianWang§,YanyongZhang†,
RichardE.Howard†,PeiZhang§
†WirelessInformationNetworkLaboratory,RutgersUniversity
§DepartmentofElectricalandComputerEngineering,CarnegieMellonUniversity
‡CenterforEnergy-efficientComputingandApplications,PekingUniversity
ABSTRACT ACMReferenceformat:
Usinggeophonestosensebedvibrationscausedbyballisticforce ZhenhuaJia†,AmelieBonde§,SugangLi†,ChenrenXu‡,JingxianWang
§,YanyongZhang†,RichardE.Howard†,PeiZhang§.2017.Monitoringa
hasshowngreatpotentialinmonitoringaperson’sheartrateduring
Person’sHeartRateandRespiratoryRateonaSharedBedUsingGeophones.
sleep.Itdoesnotrequireaspecialmattressorsheets,andtheuser
InProceedingsofSenSys’17,Delft,Netherlands,November6–8,2017,14pages.
isfreetomovearoundandchangepositionduringsleep.Earlier
DOI:10.1145/3131672.3131679
workhasstudiedhowtoprocessthegeophonesignaltodetect
heartbeatswhenasinglesubjectoccupiestheentirebed. Inthis
study,wedevelopasystemcalledVitalMon,aimingtomonitora
1 INTRODUCTION
person’srespiratoryrateaswellasheartrate,evenwhensheis
sharingabedwithanotherperson.Insuchsituations,thevibrations Monitoringaperson’svitalsignsduringsleep,especiallyheartrate
frombothpersonsaremixedtogether.VitalMonfirstseparatesthe andrespiratoryrate,hasreceivedagreatdealofattentioninthe
twoheartbeatsignals,andthendistinguishestherespirationsignal lastfewyears.Manysystems[2,3,10,18,21,22,25,27,30,32,40,
fromtheheartbeatsignalforeachperson.Ourheartbeatseparation 49,51,52,54]havebeenproposedinbothindustryandacademia,
algorithmreliesonthespatialdifferencebetweentwosignalsources promisingtopotentiallyserveasaproxytovarioushealth/medical
withrespecttoeachvibrationsensor,andourrespirationextraction applications,suchasmonitoringsleepquality[53],detectingob-
algorithm deciphers the breathing rate embedded in amplitude structivesleepapnea[38],evaluatingtheriskofheartfailureun-
fluctuationoftheheartbeatsignal. dercertainsituations[29,39],andevenmonitoringpatientswith
Wehavedevelopedaprototypebedtoevaluatetheproposed Parkinson’sdiseases[12],etc.
algorithms. Atotalof86subjectsparticipatedinourstudy,and Mostofthesesystemsmonitorvitalsignsbymeasuringoneor
wecollected5084geophonesamples,totaling56hoursofdata.We moreaspectsoftheballisticforceduringaheartbeatpulse,ranging
showthatourtechniqueisaccurate–itsbreathingrateestimation fromforcemagnitude[18,40],pressure[25,49],totheresulting
errorforasinglepersonis0.38breathsperminute(medianerror positionchange[10,21,32,51,52,54].Eventhoughtheyareableto
is0.22breathsperminute),heartrateestimationerrorwhentwo performaccuratemonitoring,mostofthemarequitecumbersome
personsshareabedis1.90beatsperminute(medianerroris0.72 toinstallonabed(e.g.,requiringspecialmattress/sheets,requiring
beatsperminute),andbreathingrateestimationerrorwhentwo theusertokeepthesamesleepingposition/posture,etc),orare
personsshareabedis2.62breathsperminute(medianerroris1.95 inconvenient/invasivetotheusers.
breathsperminute).Byvaryingsleepingpostureandmattresstype, Recentwork[27]hasshownthatthegeophonesensor[4],which
weshowthatoursystemcanworkinmanydifferentscenarios. measuresthevibrationvelocitycausedbyballisticforce,provides
aviablealternativeindetectingheartrateduringsleepwithout
CCSCONCEPTS having the above problems of the existing systems. Thanks to
beingsensitivetoevenminutevibrations,geophonesofferaccurate
•Human-centeredcomputing→Ubiquitousandmobilecom-
monitoring,areeasytoinstall,canbeinstalledanywhereonthe
putingsystemsandtools;
bedframe,anddonotassumeanysleepingpatternsfromtheuser.
Despitethesenicefeatures,agreatdealofeffortisstillrequiredto
KEYWORDS
buildafull-fledgedvitalsignmonitoringsystemusingthegeophone
VitalSigns,Geophone,UnobtrusiveSensing,BlindSourceSepara-
sensor.First,weneedtodetectrespirationusinggeophones,which
tion,Time-frequencyMasking
isverydifficultbecausethevibrationscausedbyrespirationare
weakandthefrequencycomponentsarebelowtheextremelylow
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalor
classroomuseisgrantedwithoutfeeprovidedthatcopiesarenotmadeordistributed frequency(ELF)band(<1Hz).Thusgeophonesdon’tcapturethose
forprofitorcommercialadvantageandthatcopiesbearthisnoticeandthefullcitation vibrationswell. Second, weneedtoextractthetargetsubject’s
onthefirstpage.CopyrightsforcomponentsofthisworkownedbyothersthanACM
heartratefromthemixedvibrationsignalwhenmultiplepeople
mustbehonored.Abstractingwithcreditispermitted.Tocopyotherwise,orrepublish,
topostonserversortoredistributetolists,requirespriorspecificpermissionand/ora shareabed.Thedifficultyofthisproblemismainlyduetothefact
fee.Requestpermissionsfrompermissions@acm.org. thattheheartbeatvibrationsignalsaremixedtogetherinthetime
SenSys’17,Delft,Netherlands domainandthefrequencycomponentsfrommultiplepeoplecanbe
©2017ACM. 978-1-4503-5459-2/17/11...$15.00
DOI:10.1145/3131672.3131679 quiteclosetoeachother.Inthispaper,weseektodevelopVitalMon,

| SenSys’17,November6–8,2017,Delft,Netherlands |     |     |     |     |     |     | Z.Jiaetal. |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | ---------- | --- |
0.04 0.04 domains.Inthisstudy,weaddressthischallengebytakingadvan-
tageofthespatialdifferencesbetweentwoheartbeats.Supposewe
| )V( edutingaM 0.03 |     | )V( edutingaM 0.03 |     |                    |                                   |     |     |     |
| ------------------ | --- | ------------------ | --- | ------------------ | --------------------------------- | --- | --- | --- |
|                    |     |                    |     | havetwogeophonesG1 | andG2 .AsfarasthesourceclosertoG1 |     |     | is  |
0.02 0.02 concerned,itsvibrationsignalcapturedbyG1 hashigheramplitude
0.01 0.01 andlessphasedelaycomparedtothesamesource’ssignalcaptured
|     |                |      |                | bygeophoneG2                           | .Baseduponthisspatialdifference,wecanextract |     |     |     |
| --- | -------------- | ---- | -------------- | -------------------------------------- | -------------------------------------------- | --- | --- | --- |
| 0   |                | 0    |                |                                        |                                              |     |     |     |
| 0   | 5              | 10 0 | 5 10           | thetargetsource’ssignalfromthemixture. |                                              |     |     |     |
|     | Frequency (Hz) |      | Frequency (Hz) |                                        |                                              |     |     |     |
Consideringthesimilaritybetweenheartbeatsignalsandhuman
|     | (a) |     | (b) |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
soundsignals,andhowtheyaresimilarlymixedtogetherinreal
Figure1: (a)Thegeophonesignalinthefrequencydomain, life,weturntoliteratureintheacousticfieldforwisdom. Popu-
| withasinglesubjectonthebed, |     | and(b)thegeophonesig- |     |     |     |     |     |     |
| --------------------------- | --- | --------------------- | --- | --- | --- | --- | --- | --- |
larsolutionsincludeIndependentComponentAnalysis(ICA)[26],
nalinthefrequencydomain,withtwosubjectsonthebed. PrincipalComponentAnalysis(PCA)[28],etc. Amongthesolu-
Peakscausedbyheartbeatsandharmonicsareobviousin(a), tionsthathavebeenproposed,DegenerateUnmixingEstimation
makingsingle-subjectheartratemonitoringrathersimple. Technique(DUET)[48,55]iswell-suitedtoaddressourneedsbe-
Whenwehavetwosubjectsononebed,however,heartbeat cause(1)unlikeICA,itcantoleratepropagationdelays; and(2)
peaksarelessobviousandhardtodetectdirectly.
thesuddenchangeinaheartbeatsignalmaymakeconsecutive
heartbeatpulseslookuncorrelated,whichmaytricksomemethods
anin-bedheartrateandrespiratoryratemonitoringsystemusing intotreatingthosesignalsasindependent,buthaslessimpacton
geophones,andsetouttoaddressthesetwochallenges. theDUETbecauseitdoesnotrelysolelyonsuchcorrelation.
|                                    |     |                      |     | Applying         | DUET to our heartbeat | separation      | problem      | is not |
| ---------------------------------- | --- | -------------------- | --- | ---------------- | --------------------- | --------------- | ------------ | ------ |
| ChallengesofRespirationMonitoring: |     | Detectingrespiration |     |                  |                       |                 |              |        |
|                                    |     |                      |     | straightforward, | due to the unique     | characteristics | of heartbeat |        |
usinggeophonesischallenging.Ageophoneisnaturallyaveloc-
|     |     |     |     | signals that | propagate through | a bed. Firstly, | the fundamental |     |
| --- | --- | --- | --- | ------------ | ----------------- | --------------- | --------------- | --- |
itysensorandasecond-orderhigh-passfilter,thusinsensitiveto
frequencyofaheartbeatissignificantlylowerthanthatoftheau-
low-speedlow-frequencyvibrations.Unfortunately,thevibration
diosignal.Itsaveragerangeisfrom0.33Hzto4Hz,corresponding
speedofthethoraciccavityduringeachbreathisslowcompared
|     |     |     |     | to20BPM | (e.g.,theheartrateforpatientswithheartblockdis- |     |     |     |
| --- | --- | --- | --- | ------- | ----------------------------------------------- | --- | --- | --- |
hr
totheballisticmovementofaheartbeat,andtherespirationsignal
|                 |     |     |     | ease)to240BPM | (themaximumheartbeatrateestimatedbased |     |     |     |
| --------------- | --- | --- | --- | ------------- | -------------------------------------- | --- | --- | --- |
| frequencyislow. |     |     |     |               | hr                                     |     |     |     |
ontheminimumcardiacrefractoryperiodofahumanbeing),re-
Ingeneral,thevibrationsignalcausedbyeachrespirationevent
spectively.Asaresult,weneedhighfrequencyresolutionwhenwe
issoweakthattherespirationsignalisburiedundernoisefrom
extractindividualheartbeatsfromamixture,whichisparticularly
theenvironment.Inthispaper,weproposeanalternativeapproach
challengingforusbecauseheartbeatsarenotperfectlyperiodic
bymodelingthegeophonesignalasasignalafteramplitudemod-
andstable.
ulation(AM).Here,theheartbeatsignalisourcarriersignaland
Secondly,thebedandmattresshavemuchmorecomplexpropa-
| therespirationsignalisourinformationsignal. |     |     | Then,weusea |     |     |     |     |     |
| ------------------------------------------- | --- | --- | ----------- | --- | --- | --- | --- | --- |
gationpropertiesthanair.Thegroupingvelocityofanyvibration
square-lawamplitudedemodulation(SLD)algorithm[9]combined
throughabedisaround1km/s,whoseformisacomplexmechani-
withautocorrelationfunction(ACF)[15]toestimatetherespiratory
calresonancedependingonthedetailsoftheentiresystem–e.g.,
rate.
thehumanbody,thebed,thegeophone,andthefloor,etc.
Challenges of Heart Rate Monitoring: Even though earlier Inaddition,thestructureofamodernbedoftenallowsvibra-
work[27]hasshownthatgeophonesaresuitabletomonitorheart tionstolastforatleastafewcycles,andforaheartbeatsignal,
ratewhenthepersonoccupiesabedalone,monitoringaperson’s theprecedingheartbeatmayaffectthesubsequentones.Because
heartratewhenhe/shesharesthebedwithothersremainsanun- ofthesecomplexpropagationproperties,eachheartbeatsource’s
spatialsignaturesbecomelessseparablethanaudiosignals,making
| solved challenge. | The | heartbeat vibration signals | from the bed |     |     |     |     |     |
| ----------------- | --- | --------------------------- | ------------ | --- | --- | --- | --- | --- |
occupantsaremixedtogetherinthetimedomainduringpropa- heartbeatseparationamuchharderproblem.
gation,andthefrequencyoftheheartbeatsignalsandrespiration
OurContributions:Inthisstudy,wecarefullydesigntheVital-
signalsfrommultiplepeoplecanbeverycloseinthefrequencydo-
Monsystemtosolvethesechallenges.Forheartrateestimation,we
main.Figures1(a)and(b)showtwoFastFourierTransform(FFT)
takeadvantageofthehighfrequencycomponentsoftheheartbeat
examplesofthevibrationsignalswhenwehave(a)onepersonon
1(about1.28Hz),and(b)two signals,suchastheharmonics,sothatwehavelargerfrequency
abed,withaheartrateof76.7BPM
hr differencesbetweendifferentheartbeatsignalstoenablesmaller
peopleononebed,withheartratesof62.8(about1.05Hz)and59.2
windowsizes.Forrespiratoryrateestimation,wemodelthesignal
(about0.99Hz),respectively.Itishardtotelltherearetwo
| BPM hr |     |     |     | asAMandusethemodulatedsignalitselftoachievedemodula- |     |     |     |     |
| ------ | --- | --- | --- | ---------------------------------------------------- | --- | --- | --- | --- |
heartbeatsfromthemixedsignal.Infact,theamplitudeatdifferent
tion,whichallowsustoapplydemodulationwithoutknowingthe
frequenciesisevensmallerthanwhenwehadonlyonesubject,
|     |     |     |     | frequencyofthecarriersignal(heartbeatsinourcase). |     |     | Through |     |
| --- | --- | --- | --- | ------------------------------------------------- | --- | --- | ------- | --- |
mainlyduetotherelativephasedelaybetweentwoheartbeatsig-
detailedexperimentation,weshowthatVitalMoncansuccessfully
nals.Furthermore,heartbeatsovertimearenotperfectlyperiodic.
monitorthetargetperson’srespirationandheartrate,evenwhen
Therefore,itishardtoseparatetheminbothtimeandfrequency
|     |     |     |     | he/shesharesthebedwithothers. |     | Wemeasuredatotalof5084 |     |     |
| --- | --- | --- | --- | ----------------------------- | --- | ---------------------- | --- | --- |
datasetsandcollectedvitalsignsignalsover56hours2.Theoverall
| 1 In t h is p a p e | r , w e u se | t o d e n o te ‘ b e a t sp e r m inutes’forheartrateandBPMrr |     |     |     |     |     |     |
| ------------------- | ------------ | ------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
B P M h r
to d e n ot e ‘ b r e a th s p er m i nu t e’ f o r r e sp ir a t o r y ra t e . 2OurstudieswereapprovedbytheInstitutionalReviewBoard(IRB)ofourinstitution.

VitalMon:GeophoneBasedHeartRateandRespiratoryRateMonitoring SenSys’17,November6–8,2017,Delft,Netherlands
absoluteestimationerrorforheartrateandrespiratoryrateisat positionchangewhenitisembeddedinamattressand
1.90BPM
hr
and2.62BPMrr ,respectively,andthemedianis0.72 placedinthethoraxarea[51,52];anultrasound-basedsen-
BPM
hr
and1.95BPMrr . sorcandetectpositionchange[54],butrequiresmounting
aplywoodboardandanaluminumguiderailonthebed
Insummary,ourworkhasmadethefollowingcontributions:
frame; awireless-basedsystemcanalsodetectposition
(1) Wehavedevelopedarespirationdetectiontechniquebased change[10],butrequiresadditionalwirelessinfrastructure
onsquare-lawamplitudedemodulationthatcanestimate andcouldbeeasilyinterferedbyotherwirelesssignalsin
the respiratory rate from the vibration signals. To our theenvironment.
bestknowledge,thisisthefirstpaperwhichshowsthat (4) Accelerometersensorscandetectthevibrationacceleration
theoverallamplitudeofaheartbeatsignalismodulatedto causedbytheballisticforce,suchasachestbelt[45]or
carrytherespirationsignalandweshowourtechniquecan thecommercialsystemin[5].However,suchasystemis
successfullydemodulatetherespiratoryrateinformation. invasiveanduncomfortable.
(2) Wehavedevelopedaheartbeatseparationtechniquethat (5) Velocity sensors, such as geophones [27], measure the
canaccuratelytracktheheartbeatofaspecificpersonwhen speedofvibrationscausedbytheballisticforce.Theycan
therearemultiplepeopleononebed. Indevelopingour beattachedanywhereonabed,andareunobtrusiveand
technique,wehavetakenintoconsiderationtheunique convenient.
propertiesofheartbeatsignalsaswellasthecomplexprop-
agationpropertiesofthebedandmattress.
2.2 VitalMonOverview
(3) Wehavedevelopedatestbedwithmultiplevibrationsen-
AmongtheaboveBCGmonitoringsystems,thevelocitysensing
sors(geophonesinourcase). Indevelopingthetestbed,
approachoffersaccurate,unobtrusive,low-cost,androbustmon-
wehavetakenintoconsiderationthefeaturesofgeophone
itoring,asshowninarecentstudy[27]. Inthisstudy,weusea
sensorsandtheirplacement.
commercialoff-the-shelfgeophone,whichisamovingcoilbased
velocitysensor.
2 BACKGROUNDANDOVERVIEW Geophones,traditionallyusedtomeasureseismicwavesingeol-
Inthissection,wefirstprovidethebackgroundonballistocardio- ogy,havebeenwidelyusedinmeasuringvibrationsfromdifferent
graph(BCG)basedheartrateandrespiratoryratemonitoring.Then sources. Recently, geophones have been used in several appli-
wepresentanoverviewofourgeophone-basedBCGmeasurement cations: building occupancy estimation by monitoring ambient
system. vibration[41],indoorpersonlocalizationviafloorvibration[36],
interactiontrackingviasurfacevibration[42],heartrateestimation
2.1 BCGBasedHeartRateandRespiratory bymonitoringbedvibrationduringsleep[27],etc. Ageophone
RateMonitoring consistsofaspring-mountedmagneticmassmovingwithinacoil.
Itconvertsthephysicalvibrationfromtheenvironmentintoanelec-
ManyBCGbasedsystemshavebeendevelopedtomonitoraper-
tricalvoltage.Thegeophoneweuse,SM-24GeophoneElements[4],
son’sphysiologicalsignsbysensingtheballisticforceontheheart.
isnaturallyasecond-orderhigh-passfilteranditsnaturalfrequency
TheearliestworkwecanfindwasdonebyJ.W.Gordonin1877[23].
is10Hz.
HedesignedananalogBCGsystemwhichconsistsof(1)aspecial
TheoverviewofVitalMonisillustratedinFigure2. InVital-
designedmattressthatissmallbutstiff,(2)fourropestohangthe
mattresstotheceilinginaroom,(3)abunchofleverstoamplify
Mon,ourobjectiveistocontinuouslymonitortheheartrateand
theanalogvibrationsignal,and(4)aweighingmachinetorecord breathingrateofouruser(say,Alice),whetherAliceoccupiesabed
thesignalonpaper. Despiteofthecumbersomenatureofsuch aloneorsharesabedwithBob. Formonitoringpurposes,weuse
thesamenumberofgeophonesasthenumberofpersonsonabed.
asystem,itsuccessfullycapturedtheweakvibrationsfromeach
WhenbothAliceandBobarepresent,weusetwogeophonesto
heartbeat. Later,manyBCG-basedsystemshavebeenproposed
measurethevibrationscausedbytheirheartbeatsandbreathing.
andwecategorizethembelowbasedonthesensortypes:
Sinceheartbeatsleadtomuchmorepronouncedvibrationsthan
(1) Forcesensors[18,40],commonlyinstalledunderbedposts,
breathing,wefirstextractAlice’sheartbeatsignals(theamplitude
measuretheforcechangeduetotheballisticforce. The
andfrequency)fromthegeophonesignals.Thenwefurtherextract
ideaisstraightforward,butitrequiresafairlyhighsensi-
therespirationsignalfromherheartbeatsignals.Bothstepsintro-
tivitysinceittriestodetectaweakforcechangeunderthe
duceseriouschallenges,andwehavedevisedefficienttechniques
influenceofthegravityofthebedandpeople.
toaddressthem. Inthefollowingtwosections, wepresentour
(2) Air/waterpressuresensors[25,34,49],usuallysandwiched
proposedsignalprocessingtechniques–wefirstfocusonhowto
betweenmattressandbedframe, measurethepressure
extractrespirationfromheartbeatsignals,andthenfocusonhow
exertedbytheballisticforce.Duetothelimitationofthe
toextractindividualheartbeatsignalsfromthemixturesignal.
sensitivity,thesensorshouldbeinstalledunderthethorax
areaofthehumanbody,whichrequirespriorknowledge
3 MONITORINGRESPIRATORYRATEUSING
oftheperson’slocationonthebed.
(3) Positionsensorsmeasurethepositionchangeduetothe GEOPHONE
ballisticforce.Positionchangecanbedetectedbyavari- Inthissection,wediscusshowwemonitortherespiratoryrate
etyofmeans. Forexample,anopticalsensorcandetect using geophones, assuming there is only one person on a bed.

| SenSys’17,November6–8,2017,Delft,Netherlands |     |     |     |     |     |     |     |     | Z.Jiaetal. |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- |
Vibration Propagation & Measurement
001          01               1             1.01               10
H e a r t b e a t
|     |                 |     |     |             |     | A m p l i t u d e   |     |         |        |
| --- | --------------- | --- | --- | ----------- | --- | ------------------- | --- | ------- | ------ |
|     | )s/m            |     |     | S i g n a l |     |                     |     |         |        |
|     |                 |     |     |             |     | M o d u l a t i o n |     | G e o p | h o ne |
|     | /V( ytivitisneS |     |     |             |     | b y                 |     | S e n s | in g   |
R e s p ir a t i o n
|     |     | 0 0 |     |     |     | H u m a n   B o d y |     |     |     |
| --- | --- | --- | --- | --- | --- | ------------------- | --- | --- | --- |
S i g n a l
|     |     |     |     |     | Source S | e p a r a t i o n |     |     |     |
| --- | --- | --- | --- | --- | -------- | ----------------- | --- | --- | --- |
             100            1000
Frequency (Hz)
Spatial
|     |     |     | Binary Masking    |     | Energy Histogram |            |     |              |     |
| --- | --- | --- | ----------------- | --- | ---------------- | ---------- | --- | ------------ | --- |
|     |     |     |                   |     |                  | Clustering |     | Information  |     |
|     |     |     | Signal Separation |     |                  |            |     | Extraction   |     |
Heart Rate & RespiratoryRate Estimation
Bob’s Heartbeat
Heart Rate &
|     |     |     |     | & Respiration |     |     | Respiratory  |     |     |
| --- | --- | --- | --- | ------------- | --- | --- | ------------ | --- | --- |
Rate
|     |     | Bob Alice |     | Alice’s Heartbeat  |     |     | Estimation  |     |     |
| --- | --- | --------- | --- | ------------------ | --- | --- | ----------- | --- | --- |
& Respiration
Figure2: TheoverviewofVitalMon. Whentwopersons(AliceandBob)shareabed,weusetwogeophonestocapturethe
mixedvibrationsignals,andthenperformasequenceofsignalprocessingstepstomonitortheheartrateandbreathingrate
ofourtargetuser(say,Alice).
| 0.04          |     |     |     | 2             |                  |     |               | 2   |                  |
| ------------- | --- | --- | --- | ------------- | ---------------- | --- | ------------- | --- | ---------------- |
|               |     |     |     |               | Heartbeat Signal |     |               |     | Heartbeat Signal |
| )V( edutingaM |     |     |     | )V( edutilpmA | Envelope         |     | )V( edutilpmA |     | Envelope         |
0.03
|     |     |     |     | 1   |     |     |     | 1   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.02
|     |     |     |     | 0   |     |     |     | 0   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.01
| 0   |                |     |     | -1  |          |       | -1  |     |          |
| --- | -------------- | --- | --- | --- | -------- | ----- | --- | --- | -------- |
| 0   | 5              | 10  |     | 0   | 5        | 10 15 |     | 0   | 5 10 15  |
|     | Frequency (Hz) |     |     |     | Time (s) |       |     |     | Time (s) |
|     | (a)            |     | (b) |     | (c)      |       |     |     | (d)      |
Figure3: (a)Thegeophonesignalinthefrequencydomain,withasinglepersononthebed,(b)thesamegeophonesignalasin
(a),butinthetimedomain,(c)thegeophonesignalwithasinglepersonholdinghisbreath,and(d)thegeophonesignalwith
asinglepersonbreathingnormally.In(b)and(d),thesubject’sbreathingrateisembeddedintheheartbeatsignalamplitude
fluctuation,ortheenvelope.
Wefirstformulatetherespirationsignalextractionproblemasan Ontheotherhand,acloserlookatthegeophonesignalreveals
amplitudemodulationproblem. Wethenexplainthedifference aninterestingphenomenon–theamplitudeofthegeophonesignal
between our problem and the traditional amplitude problem in fluctuatesinaperiodicfashion,andthefluctuationfrequencyis
communications.Finally,wepresentouramplitudedemodulation veryclosetothesubject’sbreathingfrequency. Forexample,in
algorithm. Figure3(b),thesubject’srespiratoryrateis15.04BPMrr ,which
isveryclosetotheamplitudefluctuationfrequencyof0.251Hz.
Tofurtherinvestigatethisobservation,weconductedanexperi-
3.1 FormulatingRespirationSignalsas
mentandcomparedthegeophonesignalswhenthesubjectheld
AmplitudeModulation hisbreathwiththesignalswhenthesubjectbreathednormally.
Themoststraightforwardapproachtoextractingtherespiration Figure3(c)showsthegeophonesignalwhenasubjectliesonabed
whileholdinghisbreathforatleast15seconds,whileFigure3(d)
signalwouldinvolvedirectlyperformingFFTonthegeophone
showsthegeophonesignalwhenthesubjectbreathesatarate
signalandthenlookingforthefrequencycomponentcorresponding
torespiration.However,asshowninFigure3(a),wedon’tobserve of10BPMrr . Inbothfigures,weplottheestimatedenvelopeof
any obvious respiration frequency components (that should be thesignals. Itisclearthatthereisadirectrelationshipbetween
below1Hz)fromthegeophonesignal.Thisisbecauseageophone breathingandtheamplitudefluctuation.
Afterdeliberation,weconcludethatrespirationcausestheam-
isanaturalsecond-orderhigh-passfilter,insensitivetomotions
plitudefluctuationofthegeophonesignal.Itcanbeexplainedas
whosefrequenciesarebelowacertainthreshold(referredtoas
follows.Breathingchangestheamountofairinthechest,which
detectionthreshold,8.4Hzinourcase).Thefrequencycomponents
ofrespirationareusuallylowerthanthisdetectionthreshold.Also, inturnchangestheeffective‘stiffness’ofthechestandtheamount
thevelocityofbreathingisquiteslow,whichmakesitevenharder ofenergylossoftheheartbeatsignalafterpropagationthrough
todetectbygeophones. Asaresult,thisdirectapproachfailsto thechest.Assuch,therelationshipbetweentherespirationsignal
andtheheartbeatsignalcanbemodeledasamplitudemodulation
detectrespirationsignals.

VitalMon:GeophoneBasedHeartRateandRespiratoryRateMonitoring SenSys’17,November6–8,2017,Delft,Netherlands
(AM)incommunications[46].Here,theheartbeatsignal,including
0.05
itsfundamentalfrequencyandtheassociatedharmonics, isthe
   (0.253, 4.14)
| carriersignal,therespirationsignalistheinformationsignal,and |     |     |     |     | 0.04       |     |     |
| ------------------------------------------------------------ | --- | --- | --- | --- | ---------- | --- | --- |
| thegeophonesignalisthesignalafteramplitudemodulation.        |     |     |     |     | )2V( rewoP |     |     |
0.03
Followingamplitudemodulation,wecanmodelthethreesignals
0.02
asfollows:
0.01
N
| s(t)=sr | (cid:213) |      |     |     |         |       |     |
| ------- | --------- | ---- | --- | --- | ------- | ----- | --- |
|         | (t) s hj  | (t), |     |     |         |       |     |
|         |           |      |     |     | 0 0 0.5 | 1 1.5 | 2   |
|         | j=1       |      | (1) |     |         |       |     |
Frequency (Hz)
| sr  | (t)=ar ×cos(2πfrt+θi | ),  |     |     |     |     |     |
| --- | -------------------- | --- | --- | --- | --- | --- | --- |
Figure4:FFTofthepowersignalafterouramplitudedemod-
| s   | (t)=a ×cos(2πf | t+θ   | ),j =1,2,...,N, |                                                 |     |     |     |
| --- | -------------- | ----- | --------------- | ----------------------------------------------- | --- | --- | --- |
| hj  | hj             | hj hj |                 | ulation. Weobserveapeakat0.253Hz(markedwithared |     |     |     |
wheres(t)denotesthesourcesignalforsinglepersoncase,sr de- invertedtriangle), whichcorrespondstoarespiratoryrate
notestherespirationsignalands denotesthej-thharmonicsof of15.18BPMrr andagreeswiththegroundtruthmeasured
hj
theheartbeatsignal.Note,s meansthefundamentalfrequency byaZephyrstrip[8].
h1
oftheheartbeatsignal.
Next,wedeviseasuitableamplitudedemodulationalgorithmto
extracttherespiratoryrateinformationfromthegeophonesignal.
However,ourproblemsignificantlydiffersfromtheconventional mostofwhichareequippedwithpowerfulfans.Next,wecollect
RFamplitudemodulationprobleminthattheRFsignal’scarrier thegeophonesignalwhenasinglesubjectislyingonabed.The
frequencies are known beforehand, while the frequency of our correspondingFFTresultsshowthefrequencycomponentsofour
carriersignal–theheartbeatsignal–remainsunknown.Tomake targetsignals(heartbeatsignalsandrespirationsignals)arebelow
15Hz. Therefore,webelieveahigh-orderlow-passfilterwitha
| matters worse, | unlike the | RF signal which | has a single carrier |     |     |     |     |
| -------------- | ---------- | --------------- | -------------------- | --- | --- | --- | --- |
frequency,theheartbeatsignalincludesafundamentalfrequency cutofffrequencyat10Hzcaneffectivelyminimizetheimpactof
| andmultiplehigherfrequencycomponents. |     |     |     | environmentalnoise. |     |     |     |
| ------------------------------------- | --- | --- | --- | ------------------- | --- | --- | --- |
Duetothesedifferences,typicaldetectorsfordemodulatingAM Next,weperformamplitudedemodulationbymultiplyingthe
signals that were proposed for RF signals are ill suited for our geophonesignalwithitself.Thatis,wetreatthegeophonesignal
|     |     |     |     | as its own carrier | signal. For | our objective | of estimating heart |
| --- | --- | --- | --- | ------------------ | ----------- | ------------- | ------------------- |
problem.Forexample,anenvelopedetector,suchastheMoving
rateandrespiratoryrate,weonlyneedtorecovertheirfrequency
Root-Mean-Square(RMS)envelopesapproach[43]ortheanalytic
signalapproach[31],issensitivetothechoiceofthewindowsize; components,butnotphaseinformation.Assuch,wecansimplyset
windowsizedependsonthefrequencyoftheinformationsignal, bothsignals’phasestobe0.Then,basedonEquation1,wehave
whichisunknowninourcase.TheRMSenvelopesapproachalso
| doesn’tworkwellwithanimpulse-likesignalsuchastheballistic |     |     |     |     | N         |     |     |
| --------------------------------------------------------- | --- | --- | --- | --- | --------- | --- | --- |
|                                                           |     |     |     | 2   | (cid:213) | 2   |     |
forcewithineachheartbeat. Meanwhile,aproductdetector[44] s (t)=(sr ∗ s )
hj
usuallyrequiresknowledgeofthecarrierfrequency,whichisagain j=1
unknown in our case. Finally, neither of these detectors work 2N
wellwhencarriersignalsarequasi-periodic,likeheartbeatsinour =a (cid:48)∗cos(4πfrt)+ (cid:213) (cid:48) ∗cos(2πf
|         |     |     |     |     |     | (a  | hj t)) |
| ------- | --- | --- | --- | --- | --- | --- | ------ |
| system. |     |     |     |     | i   | h j |        |
j=1
(2)
| Therefore,wechoosethesquare-lawdemodulationapproachin |     |     |     |     | 2N  |     |     |
| ----------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
(cid:213)
thisstudy,usingthegeophonesignalasthecarriersignalwhichcan + (a (cid:48) ∗cos(2π(f −2fr )t))
|     |     |     |     |     | h − | hj  |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
demodulateitselftoextracttheinformationsignal(therespiration j=1 j
signalinourcase).AMduringpropagationshiftstherespiration
2N
frequencycomponentstoahigherfrequencyrange(aroundthe (cid:213) (cid:48)
|     |     |     |     |     | + (a  | ∗cos(2π(f +2fr | )t)) |
| --- | --- | --- | --- | --- | ----- | -------------- | ---- |
|     |     |     |     |     | h + j | hj             |      |
heartbeatfrequencyrange).Bysquaringthesignal,wereversethe j=1
frequencyshiftandcanseparatetherespirationsignalbyapplying
alow-passfilter.
Themultiplicationresultconsistsofseverallowfrequencycom-
ponentsthatarelessthan1Hzandmanyfrequencycomponents
3.2 RespiratoryRateEstimation thataregreaterthanorequalto1Hz. AsweobservefromEqua-
Next,wepresentourrespiratoryrateestimationalgorithmbased tion2,thelowestfrequencycomponent,a1∗cos(4πfrt),hastwice
onthesquare-lawdemodulation. the frequency of the respiration signal. If we can identify this
Beforepresentingouralgorithm, wefirstdiscusshowwees- particularcomponent,wecanderivetherespirationfrequency.
timatetheenvironmentalnoiseandeliminateitsimpact. Wedo Figure4showsanexampleofthedemodulationresult. After
sobyrecordingthegeophonesignalwhenthebedisemptyand applyingalow-passfilterwithacutofffrequencyof0.6Hz,we
computingtheFFT.TheFFTresultsshowthatthemajorityofthe successfullyremovethehighfrequencyenergy.Then,wecompute
noiseisabove11Hz.Wenotethatourlabenvironmenthasacon- thesquarerootofthefilteredsignalintimedomainandobtainthe
siderablygreaternoiselevelthananaveragebedroomenvironment lowfrequencysignalinfrequencydomainat0.253Hz(about15.2
aswehaveafewhundredcomputerssharingthesamelabspace, BPMrr )whichistherespiratoryrate.

| SenSys’17,November6–8,2017,Delft,Netherlands |     |     |     |     |     |     | Z.Jiaetal. |     |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | ---------- | --- |
4 MONITORINGTARGETHEARTRATE
WHENMULTIPLESUBJECTSAREPRESENT
Inthissection,wediscusshowwemonitortheheartrateforthe
|     |     |     |     |     | x1  |     | x2  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
targetperson–say,Alice–whenshesharesabedwithBob. In (1,0) (a1,δ1 )
ordertoachievethisobjective,weneedtobeabletoextractAlice’s
(1,0)
(a2,δ2 )
heartbeatsignalfromthegeophonesignalinwhichbothheartbeat
signalsarelumpedtogether.Inthisstudy,weaimtoseparatethe
|     |     |     |     |     | s1  | s2  |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
twoheartbeatsignals(theirfrequencycomponents)sothatwecan
extracteitherifneeded.Thatwaywecanmonitorthephysiological
signsforbothpeopleonthebed.
4.1 ModelingMixtureSignals
Wefirstformulatetheheartbeatseparationproblembyformally Figure 5: We illustrate our experiment setting, which in-
definingthemixedsignal[35].Supposewehave2signalsourcess1 cludestwosubjects(s1ands2)andtwogeophonesensors(x1
ands2 ,withsignalss1(t)ands2(t),respectively.Supposewehave andx2).Wemarkthecorrespondingattenuationcoefficients
2geophonereceiversx1 andx2 ,whichreceivemixedsignalsx1(t) andtimedelayparametersonthefigure,usinggreenforone
| andx2(t)suchthat |     |     |     | sourceandbrownfortheothersource. |     |     |     |     |
| ---------------- | --- | --- | --- | -------------------------------- | --- | --- | --- | --- |
2
(cid:213)
|     | x (t)= | a sj (t−δ | ),k =1,2, | (3) |     |     |     |     |
| --- | ------ | --------- | --------- | --- | --- | --- | --- | --- |
k k,j k,j anaudiosourceandthereceiverareunique.Inaddition,mixture
j=1
audiosignalsusuallyhavesparsefrequencycomponentsbecause
wherea andδ aretheattenuationcoefficientsandtimedelay itisraretohavetwopeopletalkingatthesamefrequencyatthe
| k,j                                   | k,j |     |                   |           |     |     |     |     |
| ------------------------------------- | --- | --- | ----------------- | --------- | --- | --- | --- | --- |
| parametersassociatedwiththepathfromsj |     |     | tox .Sincewedon’t | sametime. |     |     |     |     |
k
havepriorknowledgeofthetruesignalattenuationanddelayin Inthisstudy,wechoosetoadoptDUETduetothesimilarity
oursystem,werelyonrelativesignalattenuationanddelay.Here,
betweenaudiosignalsandheartbeatsignals.Firstly,bothheartbeat
weconsiderx1(t)asreferencesignal(witha1,1 = a1,2 = 1and signalsandaudiosignalshaveafundamentalfrequencycomponent
δ1,1 =δ1,2 =0),andcomparex2(t)toittoobtainthecorresponding andhighfrequencycomponents(harmonics).Secondly,wehaveno
relativeattenuationanddelaycoefficients. controlof,noraprioriknowledgeof,thefrequenciesofheartbeat
After calculating the short-time Fourier transform (STFT) of signalsoraudiosignals.Thirdly,thepathsbetweendifferentsources
x1(t)andx2(t),weobtaintheirtime-frequencyrepresentation: andreceivershavediversity,makingitpossibletoestablishspatial
|     | (cid:20) ˆ | (cid:21) (cid:20) ˆ | (cid:21)  | fea tu r e s fo | r ea c h s o u r c e. |     |     |     |
| --- | ---------- | ------------------- | --------- | --------------- | --------------------- | --- | --- | --- |
|     | x 1 ( τ ,  | ω ) s 1             | ( τ , ω ) |                 |                       |     |     |     |
=P2×2 , (4) H e a r tb e at si g n a ls , h o wever,havetheirowncharacteristics.For
|     | x ˆ 2 ( τ , | ω ) s ˆ 2 | ( τ , ω ) |     |     |     |     |     |
| --- | ----------- | --------- | --------- | --- | --- | --- | --- | --- |
examples,heartbeatsignalshavemuchnarrowerfrequencyranges
wherethepropagationmatrixP2×2 isdefinedas thanaudiosignals;heartbeatsfrommultiplepeoplehavelessfre-
quencydifferencethanaudiosignals;thefrequencyofheartbeat
|     | (cid:20) | 1   | 1 (cid:21) |     |     |     |     |     |
| --- | -------- | --- | ---------- | --- | --- | --- | --- | --- |
|     | P2×2 =   |     | .          | (5) |     |     |     |     |
a2,1e−iωδ2,1 a2,2e−iωδ2,2 signalsfluctuatesfrombeattobeatwhileaudiosignalsareconsis-
tentforatleastafewcycles.Thesecharacteristicsmaynotsatisfy
InFigure5,Weillustrateourexperimentsettingwhichincludes
theimplicitassumptionsmadebyDUETandimposechallengesin
| twosubjects(s1 | ands2 )andtwogeophonesensors(x1 |     | andx2 | ).The |     |     |     |     |
| -------------- | ------------------------------- | --- | ----- | ----- | --- | --- | --- | --- |
oursystemdesign.Wewillexplainhowwetacklethesechallenges
direct propagation paths froms1 to both geophone sensors are intherestofthissection.
| markedingreen,andthepathsfroms2 |                 |          | tobothgeophonesensors |                                           |     |     |     |     |
| ------------------------------- | --------------- | -------- | --------------------- | ----------------------------------------- | --- | --- | --- | --- |
| are marked                      | in brown. Using | the same | color, we also mark   | the                                       |     |     |     |     |
|                                 |                 |          |                       | 4.3 HeartbeatSignalSeparationandHeartRate |     |     |     |     |
correspondingattenuationcoefficientsandtimedelayparameters.
Estimation
Next,wepresentouralgorithmthatseparatesindividualheartbeat
4.2 BackgroundonBlindSourceSeparation
andtheDUETAlgorithm signalsandestimateseachperson’sheartrate.
Hereweassumewehavetwosynchronizedgeophonereceivers
Ourheartbeatseparationproblemissimilartothecocktailparty
|         |                         |        |               | that continuously | collect mixed | signals from | two subjects. | We  |
| ------- | ----------------------- | ------ | ------------- | ----------------- | ------------- | ------------ | ------------- | --- |
| problem | [20] where an arbitrary | number | of people are | talking           |               |              |               |     |
partitionthesignalsintoprocessingwindowsofequallength(40
simultaneouslyatacocktailpartyandalisteneristryingtoidentify
seconds)andapplythefollowingsignalprocessingstepsonboth
andfollowoneparticulardiscussion.DUET[48,55]hasprovento
signalswithinthesamewindow:
beagoodsolutiontothecocktailpartyproblem.Itcomputesthe
symmetricattenuationandrelativedelayofthesignals,calculates (1) Filtering. Weapplyasuitablelow-passfiltertofilterout
theenergyhistogramwithindifferentrangesofattenuation-delay environmentalnoise(discussedinSection4.3.1),andthen
values,andfinallyidentifieseachenergypeakasasignalsource. removethedirectcurrent(DC)componentfromthefiltered
| Thisissuitableforthecocktailpartyproblembecauseitcleverly |     |     |     | signal; |     |     |     |     |
| --------------------------------------------------------- | --- | --- | --- | ------- | --- | --- | --- | --- |
leveragestheuniquepropertiesofaudiosignals.Audiosignalshave (2) We compute the STFT results of the two filtered
STFT.
spatialsignaturesastheattenuationanddelayparametersbetween signals(discussedinSection4.3.2);

VitalMon:GeophoneBasedHeartRateandRespiratoryRateMonitoring SenSys’17,November6–8,2017,Delft,Netherlands
Energy Histogram at certain
SSeennsosor rSsig Sniaglnal PPrerepprroocceesssseedd SSiiggnnaall Weighted Energy for Relative SSeeppaararatetde dS oSuorucercses
attenuation and delay
Delay and Attenuation
Phase Correction LoLwow-p-paassss F Fiilltteerriinngg CluCslutsetre rP Peeaakks FFiinnddiningg Auto-correlation &
w&ith Roeumt Pohvaese D DCelay && B Bininaarryy MMaasskkiinngg AutPoe-acko Frirnedliantgio n &
Peak Finding
Figure6: Overviewofourheartbeatseparationalgorithm.
(a) (b)
Figure7: (a)AnormalButterworthfilterintroducesphase
delays,while(b)aforward-backwardfiltercanleavethefil-
teredsignalinperfectalignmentwiththeoriginalsignal. Figure8: Theinstantaneousheartratesoftwoparticipates
at a calm state, fluctuate around their average heart rates,
57.2and63.1BPM .
hr
(3) SpatialSignatures.Wecalculatesymmetricattenuationand
relativedelaybetweenthetwoSTFTresults(discussedin
Section4.3.3);
notcauseanysignaldistortionsthatmaychangethesignalsig-
(4) EnergyClustering. Wecalculatetheenergyofeachfre-
nature. Forthispurpose,weperformahigh-orderlow-passBut-
quencybin(wepartitiontheentirefrequencyrangeinto
terworthfilter,followedwithaforward-backwarddigitalfiltering
discrete bins) and sum the energy values for different
technique[50]. Byapplyingthisforward-backwarddigitalfilter
rangesofsymmetricattenuationandrelativedelay. We
techniqueinbothdirections,thephasedistortionscausedbythe
thenrebuildthesignalsinthenewcoordinatesystemwith
twofilterscancelouteachother.Eventually,weintroducenophase
therelativedelayonx-axis,symmetricattenuationony-
distortionatall.
axisandtheenergyhistogramonz-axis(discussedinSec-
ShowninFigure7(b),thesignalaftertheforward-backwarddig-
tion4.3.3);
italfilteralignsperfectlywiththeoriginalsignal,whileanormal
(5) BinaryMasking.Weidentifythecoordinatesofthepeaks
high-orderlow-passButterworthfilterintroducesdelaybetween
inthisnewthree-dimensionalspaceandapplyabinary
theoriginalsignalandtheresultingsignal(Figure7(a)).Inaddition,
masktoseparatepeaksthatrepresentdifferentheartbeats
theforward-backwardfilteralsosquarestheamplituderesponse.
(discussedinSection4.3.4);
Finally,afterapplyingthelow-passfilter,weremovetheDCcom-
(6) HeartRateEstimation.Weconvertthesignalfromthefre-
ponentsinceitcontainsnoheartbeatrelatedinformation.
quencydomainbacktothetimedomain,andthenestimate
theheartrateusingthemethoddiscussedin[13,27].We
4.3.2 Time-FrequencyRepresentationforLocatingSpatialInfor-
alsoestimatetherespiratoryrateusingthealgorithmin
mation. Inthisstep,weobtainthetime-frequencyrepresentation
Section3.
ofthefilteredsignals.WechooseSTFTforthispurpose.
Figure6pictoriallyshowsthesestepsinvolvedinouralgorithm.
LackofShort-TermFrequencyStability:Audiosignalsusually
4.3.1 FFTandLow-passFilteringforNoiseReduction. Geophone havestablefrequencycomponentswithinashorttimewindow.
signalsareusuallyhighlynoisybecausethesensorisquitesensitive, Rabiner[47]pointedoutthataudiosignalfrequencieswithina45
andthereforeefficientnoisereductionbecomesanessentialstep. mstimewindowcanbeconsideredstable. However,thisisnot
Wenotethat,asmentionedinSection3,mostofthenoiseisabove trueforheartbeats.AsshowninFigure8,theinstantaneousheart
11Hzwhilethetargetsignalsaremainlybelow15Hz.Therefore,a ratefluctuatesconsiderablyaroundtheaverageheartrate.Hence,
high-orderButterworthlow-passfilterwithcut-offfrequencyat10 compared to the audio signal, the heartbeat signal’s frequency
Hzcaneffectivelyreducethenoise. variesalotmorefromcycletocycle.Asaresult,whenwecompute
SinceDUETseparatessignalsfromdifferentsourcesusingtheir STFT,wehavetofurtherpartitionthesignalswithinaprocessing
spatialsignatures,wewanttomakesurethefilteringstepdoes windowof40secondsintosmallersegments.

SenSys’17,November6–8,2017,Delft,Netherlands Z.Jiaetal.
InsufficientFrequencyDifference:Foranypairofsignalsthat
25
havethesamelength,s1(t)ands2(t),theyareW-disjointorthogonal
whentheysatisfy: 20
sˆ 1(τ,ω)sˆ 2(τ,ω)=0,∀τ,ω, (6) 15
wheresˆ 1(τ,ω)andsˆ 2(τ,ω)arethetime-frequencyrepresentation 10
ofsignals1(t)ands2(t),respectively.Itmeansthattheenergyfrom
5
onesourceismuchlargerthantheothersource.
Thisassumptiondoesn’tholdtrueforsignalsatthesamefre- 0
0 0.5 1 1.5 2
quency.Thesumofanytwosignalsatthesamefrequency,regard- Slot Duration (s)
lessoftheiramplitudeandphasevalues,constitutesasinglesignal
atthatfrequency.Asaresult,ifwedon’thaveadditionalinforma-
tionaboutthetwosignals’amplitudeandphaseinformation,we
can’tseparatethemsincethereareaninfinitenumberofwaysof
decomposingthemixedsignal.Assuch,heartbeatseparationdoes
notworkiftheindividualheartbeatsareatthesamefrequency.
Thoughitisrarefortwopeopletohaveexactlythesameheart-
beats,itisquiteoftenthattheirheartbeatfrequenciesarecloseto
eachotherduetothesmallheartbeatfrequencyrange.Forexample,
letusconsidertwoheartbeatsignalswhosefrequenciesare1Hz
and1.1Hzrespectively.Inordertodiscriminatethetwosignals,we
actuallyneedatleasta10-secondsignaltoseethedifference:one
has10beatswithin10s,whiletheotheronehas11beats.However,
it is very hard, if not impossible, for a heartbeat signal to hold
steadyatathesamefrequencyforadurationof10seconds.
OurSolution:InVitalMon,wedealwiththesechallengesbythe
following tricks. First, we focus on the heartbeat signal’s high
frequencycomponentsformoresparsity.Forexample,forheartbeat
signalsat1Hzand1.1Hz,theireighthharmonics–8Hzand8.8
Hzrespectively–havegreaterfrequencydifference. Second,we
partitioneachprocessingwindow(40seconds)intomuchsmaller
slotstoensurethetwosignalsareW-disjointorthogonalduring
eachslot.Figure9plotstheheartrateestimationerrorwithdifferent
slotdurations.Generally,aslotdurationlessthan1.7secondsleads
to much lower estimation error. In particular, we find the slot
durationaround0.7secondyieldsthelowestestimationerror,1.90
BPM . Inourevaluation, wethenadoptaslotdurationof0.7
hr
secondforourheartbeatseparationandextraction.
4.3.3 Calculating Symmetric Attenuation and Relative Delay.
From the STFT results, we are able to compute the relative at-
tenuationandrelativedelayasin[55]:
aˆ(τ,ω)= (cid:12) (cid:12) (cid:12) (cid:12) x x ˆ ˆ 2 1 ( ( τ τ , , ω ω ) ) (cid:12) (cid:12) (cid:12) (cid:12) , (7)
θ ˆ (τ,ω)=− 1 (cid:93) xˆ 2(τ,ω) , (8) ω xˆ 1(τ,ω)
wherexˆ 1(τ,ω),xˆ 2(τ,ω)arethetime-frequencyrepresentationfrom
theSTFTresults,andωisthefrequencyvector.Consideringthat
symmetricattenuationyieldshigherresolutionswhensignalsfrom
thesamesourcegetdifferentattenuationatdifferentreceivers,we
furthercomputetheestimatedsymmetricattenuation:
1
α˜(τ,ω)=aˆ(τ,ω)− . (9)
aˆ(τ,ω)
Combiningsymmetricattenuationandrelativedelay, weare
able to separate signals from the two sources. The next step is
tocomputetheenergyhistogrambasedontheattenuation-delay
)
MPB(
rorrE
noitamitsE
rh
Figure 9: The mean absolute estimation error (in BPM )
hr
withdifferentslotdurations.Theslotdurationof0.7second
givesthebestestimation,withanerrorof1.90BPM .
hr
values.Foranygivenfrequencythatfallsintotherangethathas
thesamesymmetricattenuationandrelativedelay,wecomputethe
energyhistogrambysumminguptheestimatedenergyinthose
frequencyranges. Followingthisprocess,weeventuallycluster
thefrequenciesthatarefromthesamesourceandhavesimilar
symmetricattenuationandrelativedelayvalues.
4.3.4 FindingClusterPeaksandApplyingBinaryMaskingin3D
Space. Next,weexplainhowwefindclusterpeaks,whicheach
correspondtoaseparatesignal.Inourproblem,symmetricatten-
uationanddelayvaluesfromdifferentsourcesoverlapwitheach
other,leadingtopoorlyformedclustersthatarehardtoidentify.
Asaresult,wecannotrelyonnormalpeakfindingalgorithmsor
machinelearningalgorithmssuchasK-MeansClustering[33],or
CLIQUE[11]toidentifythepeaks.
Instead,wetakeadvantageofthespatialdiversityinoursystem.
Ifweplacegeophonex2 closetoAlice,andx1 closetoBob,and
usex1(t)asthereference,thensymmetricattenuationofAlice’s
heartbeatsignalispositivewhilesymmetricattenuationofBob’s
heartbeatsignalisnegative.Then,wecanuseasimplebinarymask
toassigneachattenuation-delaypairtoeitherAliceorBob.
4.3.5 EstimatingTargetHeartRate. Oncesignalsfromdifferent
sourcesareproperlyseparated,weperforminverseSTFTtoreturn
themtothetimedomain.Wethenapplytheheartbeatdetection
algorithmdiscussedin[27]toextracttheheartbeats.Namely,we
computethesignalpower,calculatethesampleauto-correlation
function(ACF),findpeaksinthesampleACFresults[7],andfi-
nallyconvertthepeaklocationstocorrespondingheartbeatpulses.
Onceweobtaintheheartrates, weassociateeachheartrateto
thecorrectpersononthebed,basedonthelocationinformation. Meanwhile,wealsoapplyourrespiratoryrateestimationalgorithm
inSection3.2oneachheartbeatsignaltoestimateeachsubject’s breathingrate.
5 VITALMONTESTBED
AmplifierandADC:Inourtestbed,weusetwoSM-24geophones
[4]totracktheheartrateandrespiratoryrate.Therawanalogsignal
fromeachgeophoneisfirstamplifiedthroughitsownamplifier
circuitwhoseamplificationis200.Then,theamplifiedsignalsare
fedintoa12-bitanalog-to-digitalconverter(ADC)onanArduino
Due[1]whoserangeis0to3.3Vandsamplingfrequencyis2.5
kHz.Meanwhile,thetwogeophonesignalsaresyncedthroughthe
internalclockoftheArduinoDue.Figure10showstheexperiment

VitalMon:GeophoneBasedHeartRateandRespiratoryRateMonitoring SenSys’17,November6–8,2017,Delft,Netherlands
G1
AC Amplifier
|     |     |     |     |     |     |     |     | G6  |     |     | G2  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Arduino Due
𝒛
|     | 𝒙   |     |     |     |     |     |     |     | S1  | S2  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
𝒚
|     |     |     |     |     |     |     |     | G5  |     |     | G3  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Geophone
| Figure                       | 10:  | Our prototype  | bed. We                | install      | two geophone |         |                                                   |                                         |                               |                 |                 |
| ---------------------------- | ---- | -------------- | ---------------------- | ------------ | ------------ | ------- | ------------------------------------------------- | --------------------------------------- | ----------------------------- | --------------- | --------------- |
| boards                       | that | are sandwiched | between                | the mattress |              | and the |                                                   |                                         |                               |                 |                 |
| frame,oneoneachsideofthebed. |      |                |                        |              |              |         |                                                   |                                         |                               | G4              |                 |
| edutilpmA dezilamroN 1       |      |                | edutilpmA dezilamroN 1 |              |              |         |                                                   |                                         |                               |                 |                 |
|                              |      |                |                        |              |              |         | Figure12:                                         | Thisfigureshowsthetopviewofabed,thathas |                               |                 |                 |
| 0.5                          |      |                | 0.5                    |              |              |         | twosourcess1                                      | ands2.                                  | Hereweshowtwoexampleinstalla- |                 |                 |
| 0                            |      |                | 0                      |              |              |         | tionplans.Theplanmarkedbyreddashedlinesrepresents |                                         |                               |                 |                 |
| -0.5                         |      |                | -0.5                   |              |              |         | apoorinstallationwheretwosourceshavesamesymmetric |                                         |                               |                 |                 |
|                              |      |                |                        |              |              |         | attenuation                                       | and relative                            |                               | delay. The plan | marked by green |
| -1                           |      |                | -1                     |              |              |         |                                                   |                                         |                               |                 |                 |
| 0                            | 0.5  | 1 1.5          | 2 0                    | 0.5          | 1 1.5        | 2       | solidlinesisagoodinstallation.                    |                                         |                               |                 |                 |
|                              |      | Time (s)       |                        | Time (s)     |              |         |                                                   |                                         |                               |                 |                 |
|                              |      | (a)            |                        | (b)          |              |         |                                                   |                                         |                               |                 |                 |
geophonesthatcanmeasurehorizontalvibrationsarenotsuitable
| Figure11: | Whenwegentlytaptheprototypebed,response |     |     |     |     |     | foroursystem. |     |     |     |     |
| --------- | --------------------------------------- | --- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- |
fromaverticalgeophone(a)ismuchmorecrisp(shorteros- Figures11(a)and(b)showtheresponsesfromaverticalgeo-
cillation)thantheresponsefromahorizontalgeophone(b). phoneandahorizontalgeophonewhenwelightlytapthebedjust
once.Foreachsignal,wenormalizedtheamplitudetoobservehow
settingwithtwoparticipantsonourprototypebed.Thebedhasa longtheoscillationlasts.Thetappingmotionoccurredattime0.2
memoryfoammattressandasteelframe. second.Theverticaloscillationlastedforroughly0.3second,while
thehorizontaloscillationlastedformorethan1.8seconds.
VerticalvsHorizontalGeophones:Manygeophonesrespondto
vibrationsinasingledirection,althoughmorecomplexgeophones GeophonePlacement:Next,wecarefullyconsiderhowthetwo
thatcansensevibrationsinmultipledirectionsareavailable. In geophonesshouldbeplacedonthebed.Ourheartbeatseparation
ourexperiments,wehavetriedverticalgeophones(respondingto algorithminvolvesinferringthesymmetricattenuationandrelative
delayinformationfromtheamplitudeandphaseoffrequenciesin
vibrationsinthezdirectioninFigure10)andhorizontalgeophones
thesignalSTFT.Toavoidanyambiguityofphasedelaycausedby
(respondingtovibrationsinthex−yplaneinFigure10).Through
experimentation,wechooseverticalgeophonesinourtestbed.We phasewrap[14],weshouldnotseparatethetwogeophonesensors
explainthereasonbelow. bymorethanhalfofthewavelengthofthesignal.Fortunately,in
Ourfirstintuitionwastochoosehorizontalgeophones. Each ourcase,thisrequirementiseasytosatisfybecausethewavelength
oftheheartbeatsignalisusuallymuchlargerthanthelengthofa
heartbeatismainlycausedbythesuddenejectionofbloodduring
|     |     |     |     |     |     |     | regularbed. | Forexample,foraheartbeatsignalwhoserateis60 |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ------------------------------------------- | --- | --- | --- |
theventriclesystole.Thedirectionofsuchmomentaryejectionfirst
goesfromtheventricletotheaortaandthengetssplittodifferent bpm,itswavelengthroughlyis1km.
bloodvessels ofa humanbody. Dueto suchdirectionality, the Ourtechniqueseparatessignalsfromdifferentsourcesbytheir
strongestvibrationisalongthehead-footdirection(inthex uniquespatialsignatures.Asaresult,whenweinstallgeophone
−y
|     |     |     |     |     |     |     | sensors, | we need to | make | sure there is | difference between the |
| --- | --- | --- | --- | --- | --- | --- | -------- | ---------- | ---- | ------------- | ---------------------- |
plane).Intuitively,wewouldliketocapturethestrongestvibration
sources’spatialsignatures.Supposethetwohearts’positionsare
byusingmultiplehorizontalgeophones.
However,whenweconsiderthehumanbody,thebed,thefloor s1 ands2 ,andthetwogeophones’positionsarex1 andx2 .Thenwe
andoursystemasawholepiece,wefindhorizontalgeophones needtothefollowinginequalityissatisfied
apoorchoicebecausebedsaredesignedtoallowthejointstobe
|     |     |     |     |     |     |     |     |     | ||x1s1|| | ||x2s1|| |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | -------- | --- |
(cid:44)
| underdampedonthex−yplane,yieldingmorehorizontaloscilla- |     |     |     |     |     |     |     |     |          |          | ,   |
| ------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | -------- | --- |
|                                                         |     |     |     |     |     |     |     |     | ||x1s2|| | ||x2s2|| |     |
tions.Suchoscillationsusuallylastformorethan1second,which
isoneheartbeatcycle,suchthataheartbeatmaylastlongenough where||x1s1||isthedistancebetweenx1 ands1 .InFigure12,we
toaffectthefollowingheartbeat(s). Ontheotherhand,wefind illustratesixpossiblegeophonepositionsnamedG1 ,…,andG6 in
verticalgeophonesexperiencemuchsmallerandshorteroscilla- theclockwisesequenceandthetwoheartbeatlocations. Inthis
tionsbecauseoscillationsinthez directionaredampedagainst example,wecannotplacethefollowinggeophonepairs,(G1,G4),
thefloor.Asaresult,horizontalgeophonesandmulti-dimension (G2,G3),and(G5,G6). Anyoftherestofthecombinationscould

| SenSys’17,November6–8,2017,Delft,Netherlands |     |     |     |     |     |     |     |     | Z.Jiaetal. |
| -------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- |
| 1                                            |     |     |     |     |     | 1   |     |     |            |
Our Algorithm
ACF Based Algorithm
| FDC |     |     |     |     |     | FDC |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0.5 |     |     |     |     |     | 0.5 |     |     |     |
Window 30 s
Window 35 s
Window 40 s
| 0                     |                                            |       |     |     |     | 0                     |            |                           |          |
| --------------------- | ------------------------------------------ | ----- | --- | --- | --- | --------------------- | ---------- | ------------------------- | -------- |
| 0                     | 5                                          | 10 15 |     |     |     | 0 5                   | 10 15 20   | 25                        |          |
| Estimation Error (BPM |                                            | )     |     |     |     |                       |            |                           |          |
|                       |                                            | rr    |     |     |     | Estimation Error (BPM | hr )       |                           |          |
|                       | (a)                                        |       |     | (b) |     |                       |            |                           |          |
|                       |                                            |       |     |     |     |                       | (a)        | (b)                       |          |
|                       |                                            |       |     |     |     | Figure 14:            | We compare | the heart rate estimation | error of |
| Figure13:             | CDF(a)andboxplot(b)oftherespiratoryratees- |       |     |     |     |                       |            |                           |          |
timationerrorwhenwehaveasinglesubject,withthepro- ouralgorithmwiththeACF-basedheartbeatseparational-
cessingwindowof30,35,and40seconds.Windowlengthof gorithm: (a) CDF, and (b) box plot of the estimation error.
40secondshasthebestresults–meanestimationerrorof Ouralgorithmyieldsmuchlowerestimationerror.
0.38BPMrr,andmedianerrorof0.22BPMrr,over525sam-
|     |     |     |     |     |     | subject. Forexample,theestimationerrorreportedin[13,21]is |     |     |     |
| --- | --- | --- | --- | --- | --- | --------------------------------------------------------- | --- | --- | --- |
ples–whichisthenadoptedintherestoftheevaluation. 0.47andabove2BPMrr ,respectively.
| work well | for our | purpose. | In our testbed, | we mount | the two |                                   |     |     |     |
| --------- | ------- | -------- | --------------- | -------- | ------- | --------------------------------- | --- | --- | --- |
|           |         |          |                 |          |         | 6.2 MonitoringTargetHeartRatewhen |     |     |     |
geophonesaccordingto(G6,G2)inthediagram.
MultipleSubjectsareAvailable
Inthispartoftheevaluation,weconductmorethan3000exper-
6 EVALUATION
imentsandrecordmorethan33hoursofgeophonedatafroma
In this section, we use our testbed to evaluate VitalMon in the totalof35subjects.WecomparetheestimatedBPM againstthe
followingaspects:(1)estimatingtherespiratoryrateforasingle hr
|     |     |     |     |     |     | groundtruthBPM | measuredbyamedicalgradepulseoxime- |     |     |
| --- | --- | --- | --- | --- | --- | -------------- | ---------------------------------- | --- | --- |
subject,(2)estimatingthetargetsubject’sheartratewhentwosub- hr
ter[6]andreporttheestimationerror.
jectsarepresent,and(3)estimatingthetargetsubject’srespiratory
ratewhentwosubjectsarepresent.Also,wehaveadiscussionon Participants:Wehadatotalof35healthyvolunteerparticipants
therealworlddeployment. forthisexperiment,including19malesand16females.Themean
ageoftheparticipantswas25.26yearswithastandarddeviation
6.1 MonitoringaSingleSubject’sRespiratory of3.25years.Theyoungestparticipantwas21yearsoldwhilethe
oldestwas35yearsold.
Rate
Weconducted525experimentsandrecordedmorethan350minutes Wefirstconducteda
6.2.1 MeanHeartRateEstimationError.
datafromatotalof23subjects. Wereporttherespiratoryrate seriesofexperimentstoevaluatehowouralgorithmperformsover
estimationerrorastheabsolutedifferencebetweentheestimated alargerangeofheartrateswhiletwosubjectssharetheprototype
BPMrr andthegroundtruthBPMrr . bed (without gross body motions). To ensure we evaluate our
systemoveralargerangeofheartrates,weaskedoneofthetwo
Participants:Wehadatotalof23healthyvolunteerparticipants
subjectstoexercise(e.g.runningoutdoor,climbingstairs,etc.)for
forthisexperiment,including14malesand9females.Themean
afewminutesbeforeeachexperiment.Theparticipantslayontheir
ageoftheparticipantswas25.14yearswithastandarddeviation
backinthissetofexperiments.
of3.42years.Theyoungestparticipantwas21yearsoldwhilethe
Wecollected952experimentsinthispart,includingalargerange
oldestwas34yearsold.
|     |     |     |     |     |     | ofheartratesthatrangefrom43to137BPM |     | .Figure15shows |     |
| --- | --- | --- | --- | --- | --- | ----------------------------------- | --- | -------------- | --- |
Duringeachexperiment,subjectswereaskedtolieontheproto- hr
theestimationerroroverdifferentheartrateranges.Basedonthe
typebedandbreatheatacertainrateforthedurationof40seconds.
groundtruthheartratecollectedbyapulseoximeter,wegroupthe
Specifically,weplayedametronomeat1tickpersecondandasked
4304samples(wehavetwosamplesperexperiment)into6groups:
thesubjectstobreatheinandoutevery2,3,4,5,or6ticks(the
<60,[60,70),[70,80),[80,90),[90,100),and≥100.Themedianand
respiratoryrateduringeachexperimentwasthusfixed).Wemanu-
themeanofoverallestimationerrorovermorethan4000samplesis
allymonitoredtheparticipant’sbreathingratebyobservinghow
|     |     |     |     |     |     | 0.72and1.90BPM | ,respectively.Wenotethatthisresult,which |     |     |
| --- | --- | --- | --- | --- | --- | -------------- | ---------------------------------------- | --- | --- |
hr
| his/herchestmovedduringtheexperiment. |     |     |     | Eachsubjectwent |     |     |     |     |     |
| ------------------------------------- | --- | --- | --- | --------------- | --- | --- | --- | --- | --- |
evaluatestwosubjectstogether,isintherangeofothersystems
| through at | least 20 | experiments | and in | total we conducted | 525 |                                          |     |                 |     |
| ---------- | -------- | ----------- | ------ | ------------------ | --- | ---------------------------------------- | --- | --------------- | --- |
|            |          |             |        |                    |     | thatdetectasingleperson’sheartrate(e.g., |     | meanerrorof1.17 |     |
experiments.
|     |     |     |     |     |     | BPM in[13]andmeanerroraround2BPM |     | in[32]). |     |
| --- | --- | --- | --- | --- | --- | -------------------------------- | --- | -------- | --- |
Figures13(a)and(b)showthecumulativedistributionfunction hr hr
(CDF)andaboxplotoftheestimationerrorwithdifferentpro- ComparisonwiththeACF-basedApproach:Wenextcompare
cessingwindowlengths.Bothplotsshowthatlargerwindowsizes ouralgorithmwiththedirectACF-basedheartbeatdetectionalgo-
yieldlowerestimationerrors:wehavemeanerrorof0.38BPMrr , rithm(resultsshowninFigure14),whereweuseourACF-based
andmedianerrorof0.22BPMrr ,whenthewindowlengthis40sec- heartrateestimationalgorithm,butdon’tfirstseparatethesignal.
onds.Intherestoftheevaluation,weusetheprocessingwindow Instead,weassumegeophonex1 ’ssignalisdominatedbys1(t),and
of40seconds.Wealsonotethatamedianestimationerrorof0.22 usetheACF-basedheartbeatdetectionalgorithmin[27]todirectly
andameanestimationerrorof0.38BPMrr arebetterthan counttheheartbeatsinx1(t)fors1 . Similarly, werunthesame
BPMrr
manyothersystemswhenestimatingthebreathingrateforasingle algorithmonx2(t)tocountheartbeatsfors2 . Weshowthatour

VitalMon:GeophoneBasedHeartRateandRespiratoryRateMonitoring SenSys’17,November6–8,2017,Delft,Netherlands
|     | ) rh 5 |     |     |     |     | 1   |     |     |     |
| --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
MPB( rorrE noitamitsE
4
0.8
3
0.6
|     | 2   |     |     |     |     | FDC |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0.4
1
|     | 0           |                          |        |     |     | 0.2 |     | Memory Foam |     |
| --- | ----------- | ------------------------ | ------ | --- | --- | --- | --- | ----------- | --- |
|     | <60 [60,70) | [70,80) [80,90) [90,100) | >= 100 |     |     |     |     | Spring      |     |
Hardwood
0
|     |                   |     |     |     |     | 0 5                   | 10 15 | 20  | 25  |
| --- | ----------------- | --- | --- | --- | --- | --------------------- | ----- | --- | --- |
|     | Ground Truth (BPM | )   |     |     |     | Estimation Error (BPM |       | )   |     |
|     |                   | hr  |     |     |     |                       |       | hr  |     |
Figure 15: When two subjects share a bed, average heart Figure17: CDFoftheheartrateestimationerrorwhentwo
rateestimationerrorsareshownforeachofthefollowing
subjectsshareabedwithdifferentmattresstypes.Aspring
| heartbeat | rate ranges: < | 60, [60, 70), | [70, 80), [80, | 90), [90, |          |                     |            |       |              |
| --------- | -------------- | ------------- | -------------- | --------- | -------- | ------------------- | ---------- | ----- | ------------ |
|           |                |               |                |           | mattress | has slightly higher | estimation | error | than a hard- |
100),≥100.Overmorethan1900samples,ourmeanerroris
woodoramemoryfoammattress.
| 1.90BPM hr | ,andmedianerroris0.72BPM |     | hr . |     |            |                                               |     |     |     |
| ---------- | ------------------------ | --- | ---- | --- | ---------- | --------------------------------------------- | --- | --- | --- |
|            |                          |     |      |     | and1.53BPM | ,respectively,whilethemedianerroris0.73,0.88, |     |     |     |
hr
|     |     |     |     |     | and0.66BPM | .Theresultsareasexpected–amongthesethree |     |     |     |
| --- | --- | --- | --- | --- | ---------- | ---------------------------------------- | --- | --- | --- |
hr
mattresstypes,ahardwoodoneaddstotheleastoscillationsto
thegeophonesignalwhileaspringmattresshasthemostoscilla-
tion.However,wearguethatevenwiththespringmattresswhich
givesthehighestestimationerror,theestimationaccuracyisstill
sufficientformostapplications.
|     |     |     |     |     | 6.3 MonitoringTargetRespiratoryRateWhen |     |     |     |     |
| --- | --- | --- | --- | --- | --------------------------------------- | --- | --- | --- | --- |
MultipleSubjectsarePresent
Figure16: Theboxplotoftheheartrateestimationerror Inthispartoftheevaluation,weconducted1503experimentsonour
whentwosubjectsshareabedandlieindifferentpostures, prototypebedandrecordedmorethan16hoursofdata.Duringeach
includinglyingonback/stomach/left/right. Ourmeanesti- experiment,wedidn’tgiveanyinstructionsonhowthesubjects
mationerrorisbelow2.5BPM andmedianerrorisbelow shouldbreathe. Weevaluatetheperformanceofourrespiration
hr
0.74BPM regardlessoftheposture,suggestingoursystem detectionalgorithmbycomparingtheestimatedrespiratoryrate
hr
againstthegroundtruthmeasuredbyaZephyrbioharnessbelt[8]
isrobustagainstdifferentlyingpostures.
andreporttheestimationerror.
algorithmhasamuchlowerestimationerror,meanerrorof1.90
Participants:Wehadatotalof28healthyvolunteerparticipants
BPM ,comparedtotheACFbasedalgorithmwhosemeanerror
| hr         |                                            |     |     |     | forthisexperiment,including15malesand13females.Themean  |     |     |     |     |
| ---------- | ------------------------------------------ | --- | --- | --- | ------------------------------------------------------- | --- | --- | --- | --- |
| is66.53BPM | .TheACF-basedseparationapproachworkspoorly |     |     |     |                                                         |     |     |     |     |
|            | hr                                         |     |     |     | ageoftheparticipantswas24.79yearswithastandarddeviation |     |     |     |     |
becauseitoftencapturesbothheartbeatsfromeachgeophonesig-
| nal. |     |     |     |     | of2.99years.Theyoungestparticipantwas21yearsoldwhilethe |     |     |     |     |
| ---- | --- | --- | --- | --- | ------------------------------------------------------- | --- | --- | --- | --- |
oldestwas34yearsold.
| 6.2.2 TheImpactofLyingPosture. |     | Inthispart,weconducted |     |     |     |     |     |     |     |
| ------------------------------ | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- |
Weconductedmorethan1500experi-
1203experimentstoevaluatetheimpactoflyingpostureonour ExperimentProcedure:
mentsandevaluatedouralgorithmoveralargerangeofrespiratory
performance.Duringeachexperiment,twosubjectswereaskedto
adoptoneofthefollowingpostures:(1)lyingonback,(2)lyingon rates,from8.61to25.09BPMrr .Beforeexperiments,somesubjects
wereaskedtoexercise,includingrunning,climbingstairs,etc.
stomach,(3)lyingonhis/herleftside,and(4)lyingonhis/herright
BasedontherespiratoryratemeasuredbyaZephyrbelt,we
side.Thelengthofeachexperimentisagain40seconds.
|     |     |     |     |     | groupedthe3006samplesinto5groups: |     |     | <12, | [12, 15), [15, 18), |
| --- | --- | --- | --- | --- | --------------------------------- | --- | --- | ---- | ------------------- |
Figure16showstheboxplotoftheheartrateestimationerror
|                            |     |                               |     |     | [18,21),and≥21BPMrr | . Figure18showsthattheoverallmean |     |     |     |
| -------------------------- | --- | ----------------------------- | --- | --- | ------------------- | --------------------------------- | --- | --- | --- |
| fordifferentlyingpostures. |     | Theresultsshowthatoursystemis |     |     |                     |                                   |     |     |     |
robustagainstdifferentlyingpostures–themeanestimationerror estimation error across more than 3000 samples is 2.62 BPMrr ,
|     |     |     |     |     | whilethemedianerroris1.95BPMrr |     |     | .Wenotethatthisresultis |     |
| --- | --- | --- | --- | --- | ------------------------------ | --- | --- | ----------------------- | --- |
forlyingonback,stomach,left,andrightis1.75,1.62,2.17,and2.47
worsethanoursingle-personbreathingrateestimationbecausewe
BPM ,respectively,whilethemedianerroris0.61,0.57,0.73,and
| hr      |                                             |     |     |     | havetogothroughtwolevelsofindirectioninestimatebreathing |     |     |     |     |
| ------- | ------------------------------------------- | --- | --- | --- | -------------------------------------------------------- | --- | --- | --- | --- |
| 0.70BPM | .Wenotethattheestimationerrorwhenthesubject |     |     |     |                                                          |     |     |     |     |
| hr      |                                             |     |     |     | ratewhenmultiplepeopleshareabed.Inouron-goingwork,we     |     |     |     |     |
waslyingontherightisslightlyhigherbecausetheheartposition
isslightlyfurtherawayfromthemattressinthisposture. aredevelopingtechniquestoimproveourperformanceinthiscase.
Next,weevaluatehowdifferenttypesofsleepposturesaffect
6.2.3 TheImpactofDifferentMattressType. Wealsoconducted ourestimationerror.Figure19showsthatlyingpostureshavelittle
901experimentstoevaluatetheimpactofdifferentmattresstypes, impact on estimating respiratory rate – the average estimation
includingamemoryfoammattress(ourdefaultmattress),aspring errorforthesedifferentpostures(lyingonback/stomach/left/right)
mattress,andahardwoodmattress.Figure17showsthatthemean is2.77,2.36,2.68,and2.40BPMrr ,respectively whilethemedian
estimationerrorforthesethreetypesofmattressesis1.85,2.44, erroris2.15,1.66,2.09,and1.67BPMrr .

SenSys’17,November6–8,2017,Delft,Netherlands Z.Jiaetal.
8
6
4
2
0
<12 [12,15) [15,18) [18,21)
>=
21
Ground Truth (BPM )
rr
)
MPB(
rorrE
noitamitsE
rr
Figure18: Whentwosubjectsshareabed,meanbreathing Figure19: Boxplotofthebreathingrateestimationerror
rateestimationerrorsareshownforeachofthefollowing whentwosubjectsshareabedandlieindifferentpostures,
breathingrateranges: <12,[12,15),[15,18),[18,21), ≥ 21 includinglyingonback/stomach/left/right. Theaveragees-
–2.51,2.53,2.42,2.90,3.09BPMrr,respectively. Theaverage timationerrorsforthesedifferentposturesareverycloseto
error rate across all the 2406 samples is 2.62BPMrr, while eachother.
themedianerroris1.95BPMrr.
lightcausedbyvibration. Theheartbeatandrespirationsignals
6.4 DiscussiononRealWorldDeployment canbeseparatedbyapplyingasimplelow-orderhigh-passfilter.
Realworlddeploymentofoursystemcouldpotentiallyenablequite S˘prageretal.[52]usedanopticalsensorwhichtransmittedand
afewinterestingapplications.Sofar,wehaveshownoursystem receivedinterferometricsignaltocaptureopticalvariationcaused
canmonitorheartrateandrespiratoryrateforoneortwopeopleon byvibrationsfromheartbeatandrespiration.Laterawavelet-based
abed.Wehavefoundoursystemisalsoabletodetectauser’sgross decompositiontechniquewasappliedtoextractheartbeatsand
bodymotions, orsmalleractivitiessuchassnoresduringsleep. respirationsignalfromthereceivedsignal.Kortelainenetal.[30]
Thesefunctionscombined,wecouldbuildamoresophisticated deployedseveralpressuresensitivefoilsunderthemattress.The
sleepmonitoringsystemthatcanaccuratelydetectaperson’ssleep heartbeatswereextractedfromthechannelaveragedcepstrum
stageandevaluatethesleepquality.Toachievethisobjective,we basedonFouriertransformation,whilerespirationiscalculated
need to carefully tune several system parameters to detect and byanadaptiveprincipalcomponentanalysis. Aubertetal.[13]
classifythesefine-grainedinformation.Onepossiblesolutionisto putafoilpressuresensorinthethoraxareaunderathinmattress
addmoregeophonesensorsatdifferentlocationstoformasmall- todetectvitalsignsduringsleep. Theheartrateandrespiratory
scalesensornetworkthatfacilitatesmoreaccurateseparationof rateareobtainedfromanalyzingtheautocorrelationfunctionafter
varioustargetsignals. applyingappropriatebandpassfilters.
Sensorsthatrequiresspecialcushion:Heiseetal.[24]deployed
7 RELATEDWORK
fourhydraulic-transducertubesunderthemattressandshowed
Inthissection,wecategorizedifferentvitalsignmonitoringsystems threepossiblesignalprocessingstrategies(aWindow-basedPeak-
intwoways:(1)systemswhichdetecttheheartrateandrespira- to-PeakDeviationalgorithm,aK-meansclusteringalgorithm,anda
toryrateofasingleperson,e.g.[13,16–19,24,27,30,32,40,52]; Hilberttransformalgorithm)toextracttheheartbeats.Yamana[54]
(2)systemswhichdetectheartrateandrespiratoryrateoftwo designedanultrasoundtransmitterandreceiversystemmounted
peoplesimultaneously,suchasthesystemshownin[10,32].Also, underaplywoodsupport.Thesystemisplacedunderthemattress
wesummarizetheirsignalprocessingmethodsforheartrateand andmeasurestheshapechangeoftheplywoodsupport.Asimple
respiratoryrateestimation. bandpassfilterisappliedtoseparatetheheartbeatsignal.
7.1 VitalSignMonitoringofaSinglePerson Sensorsinstalledunderthebedpost: Nukayaetal.[40]pro-
posed to use a piezoceramic system to detect heartbeats. Four
Therearediversesystemsproposedtodetectheartbeatsandrespi-
sensorswerebondedtotwometalplatesontopandbottom,then
rationofasingleperson.Sofar,itisthemostcommonlystudied
sandwichedbetweenfloorandbedposts.Asimplebandpassfilter
field.
wasappliedtogettheheartbeatsignal. Brinketal.[16]builta
Sensorsinstalledunderthethoraxarea:Buetal.[19]inserted setoffouropticalloadcellswhichwereinstalledundereachbed
apiezoelectricsensorwhichmeasuresthepressurefluctuationdue postanddirectlyfindtheheartbeatsasthelocalmaximumsafter
to heartbeats and respiration. The detected signal is processed low-passfiltration.
byEmpiricalModeDecompositionandthevitalsignsignalsare
WearableSensors:Phanetal.[45]usesachestbeltwithabuilt-in
reconstructed by summing up the signal within the predefined
biaxialaccelerometertomeasurethevibrationsonthesurfaceofthe
frequencyrange.Bruseretal.[18]packagedaWheatstonebridge
chestcavity.Abandpassfilterisappliedtoextracttherespiration
offoursensitiveloadcellsontooneslatfromtheslattedframeand
signal,andacombinationofenvelopedetectionandpeakfinding
measuredthevibrationcausedbyheartbeats. Anunsupervised
algorithmisusedforestimatingtheheartrate.
learningtechniqueisusedtoextracttheshapeofasingleheart
beatfromthesignal.In[17],anarrayofphotodetectorsunderthe MobileSensors:Nandakumaretal.[37]detectssleepapneaevents
mattressareusedtodetectthechangeofreflectedandscattered withinameterbyturningasmartphoneintoasonarsystem.The

VitalMon:GeophoneBasedHeartRateandRespiratoryRateMonitoring SenSys’17,November6–8,2017,Delft,Netherlands
systememitsfrequency-modulatedsoundsignalsanddetectsthe was supported in part by the U.S. National Science Foundation
frequencyshiftsofthereflectionsduetochestmovements. (NSF)undergrantCNS-1404118,CNS-1423020,CNS-1149611and
CMMI-1653550,Intel,PennsylvaniaInfrastructureTechnologyAl-
Sensorsthatcanbeattachedtoanywhereonthebedframe: liance(PITA),Google,ScienceandTechnologyInnovationProject
Jiaetal.[27]proposedaheartbeatmonitoringsystembasedonan
ofFoshanCity,ChinaunderGrantNo.2015IT100095andScience
on-the-shelfgeophonewhichcouldbeinsertedanywherebetween
andTechnologyPlanningProjectofGuangdongProvince,China
amattressandabedframe.Acombinationoflow-passfilter,sample
underGrantNo.2016B010108002.
auto-correlationfunctionandpeakfindingalgorithmareusedto
extracttheperiodicityofheartbeats.Anevaluationofrealworld
datavaryingdifferenttypesofbedandhouseenvironmentshows REFERENCES
thepossibilityofusingthesystemindailyheartbeatmonitoring. [1] Arduinodue.https://www.arduino.cc/en/Main/arduinoBoardDue.
[2] Fitbit.https://www.fitbit.com/.
[3] Gearfit2.http://www.samsung.com/global/galaxy/gear-fit2/.
7.2 VitalSignMonitoringofMultiplePeople [4] Geophonesm-24.https://www.sparkfun.com/products/11744.
[5] Muratacontactlessbedsensor.http://www.murata.com/en-us/products/sensor/
Onlyafewpapersaddresseddetectingmultiplepeople’svitalsigns
accel/sca10h11h.
simultaneously.Adibetal.[10]useawirelessradartomeasurethe [6] Neulogheartrate&pulseloggersensor.https://neulog.com/heart-rate-pulse/.
distancechangeofahumanchest,duetoheartbeatsandrespiration. [7] Peakfindingandmeasurement. http://terpconnect.umd.edu/∼toh/spectrum/
PeakFindingandMeasurement.htm.
ThedevicecansendFrequencyModulatedCarrierWaves(FMCW) [8] Zephyrperformancesystems. https://www.zephyranywhere.com/benefits/
whichcanisolatesignalsfromdifferentdistances,andthenestimate physiological-biomechanical.
theheartrateandrespiratoryrateofmultiplepeopleviaFFT.Liuet
[9] AnalogCommunication(Jntu).McGraw-HillEducation(India)PvtLimited,2006.
[10] F.Adib,H.Mao,Z.Kabelac,D.Katabi,andR.C.Miller.Smarthomesthatmonitor
al.[32]useWiFitomeasuretheChannelStateInformation(CSI)of breathingandheartrate.InProceedingsofthe33rdAnnualACMConferenceon
thereflectionsoffthehumanbody.Thesystemtakestheadvantages HumanFactorsinComputingSystems,pages837–846.ACM,2015.
ofReceivedSignalStrength(RSS)frommultiplesubcarriersand [11] R.Agrawal,J.Gehrke,D.Gunopulos,andP.Raghavan. Automaticsubspace
clusteringofhighdimensionaldatafordataminingapplications,volume27.ACM,
estimates the heart rate and respiratory rate by using a power 1998.
spectraldensitybasedalgorithm. RSSvaluesaresensitivetothe [12] M.Apps,P.Sheaff,D.Ingram,C.Kennard,andD.Empey. Respirationand
sleepinparkinson’sdisease.JournalofNeurology,Neurosurgery&Psychiatry,
multipath situation in the environment, and therefore wireless 48(12):1240–1245,1985.
systemsthatarebasedonRSSreadingsmaybeaffectedbythe [13] X.L.AubertandA.Brauers. Estimationofvitalsignsinbedfromasingle
changesintheenvironment.
unobtrusivemechanicalsensor:Algorithmsandreal-lifeevaluation.InEngineer-
inginMedicineandBiologySociety,2008.EMBS2008.30thAnnualInternational
ConferenceoftheIEEE,pages4744–4747.IEEE,2008.
8 CONCLUDINGREMARKSANDFUTURE [14] J.M.Blackledge. Digitalsignalprocessing: mathematicalandcomputational
methods,softwaredevelopmentandapplications.Elsevier,2006.
DIRECTION [15] J.BoxandG.M.Jenkins.Reinsel.TimeSeriesAnalysis,ForecastingandControl.
PrenticeHall,EnglewoodCliffs,NJ,USA,3rdeditionedition,1994.
Inthispaper,wediscussandevaluateanunobtrusive,vibration- [16] M.Brink,C.H.Mu¨ller,andC.Schierz.Contact-freemeasurementofheartrate,
basedvitalsignmonitoringsystemduringsleep.Oursystemcenters respirationrate,andbodymovementsduringsleep.Behaviorresearchmethods,
38(3):511–521,2006.
aroundageophonesensorthatcansensethevibrationvelocity
[17] C.Bruser,A.Kerekes,S.Winter,andS.Leonhardt.Multi-channelopticalsensor-
causedbyballisticforce.Comparedtoearliergeophone-basedin- arrayformeasuringballistocardiogramsandrespiratoryactivityinbed. In
bedvitalsignmonitoringsystemsthatcouldonlydetectheartbeats EngineeringinMedicineandBiologySociety(EMBC),2012AnnualInternational
ConferenceoftheIEEE,pages5042–5045.IEEE,2012.
fromasubjectlyinginbed,oursystemissignificantlyimproved. [18] C.Bruser,K.Stadlthanner,S.deWaele,andS.Leonhardt. Adaptivebeat-to-
First,itcanmonitorthesubject’sbreathingrate,eventhoughgeo- beatheartrateestimationinballistocardiograms. InformationTechnologyin
phonescannotdirectlydetectbreathing.Second,itcantrackthe Biomedicine,IEEETransactionson,15(5):778–786,2011.
[19] N.Bu,N.Ueno,andO.Fukuda.Monitoringofrespirationandheartbeatduring
subject’sheartrateandbreathingratewhenhe/shesharesthebed sleepusingaflexiblepiezoelectricfilmsensorandempiricalmodedecomposition.
withanotherperson. Inthiscase,vibrationscausedbymultiple InEngineeringinMedicineandBiologySociety,2007.EMBS2007.29thAnnual
heartbeatsaremixedtogetherandneedtobeseparated.Afterin-
InternationalConferenceoftheIEEE,pages1362–1366.IEEE,2007.
[20] E.C.Cherry.Someexperimentsontherecognitionofspeech,withoneandwith
volving86participantsandcollecting56hoursofgeophonedata, twoears.TheJournaloftheacousticalsocietyofAmerica,25(5):975–979,1953.
we show that our system is accurate and can work in different [21] B.Fang,N.D.Lane,M.Zhang,A.Boran,andF.Kawsar. Bodyscan:Enabling
radio-basedsensingonwearabledevicesforcontactlessactivityandvitalsign
scenarios(e.g.,lyingpostures,mattresstypes). monitoring.InProceedingsofthe14thAnnualInternationalConferenceonMobile
Goingforward,thereareseveralimportantdirectionsweplanto Systems,Applications,andServices,pages97–110.ACM,2016.
investigate,including(1)obtainingbettersignal-to-noiseratiofor [22] R.FletcherandJ.Han.Low-costdifferentialfront-endfordopplerradarvital
signmonitoring. InMicrowaveSymposiumDigest,2009.MTT’09.IEEEMTT-S
moreaccurateheartrateandrespiratoryratemonitoring;(2)under- International,pages1325–1328.IEEE,2009.
standingthephysicalrespirationphenomenonbetterandadjusting [23] J.Gordon. Certainmolarmovementsofthehumanbodyproducedbythe
ourrespirationmodelaccordingly;(3)investigatingthetimeand
circulationoftheblood.JournalofAnatomyandPhysiology,11(Pt3):533,1877.
[24] D.Heise,L.Rosales,M.Sheahen,B.-Y.Su,andM.Skubic. Non-invasivemea-
frequencycharacteristicsofgrossbodymotionsandupdatingour surementofheartbeatwithahydraulicbedsensorprogress,challenges,and
modelaccordingly. opportunities. In2013IEEEInternationalInstrumentationandMeasurement
TechnologyConference(I2MTC),pages397–402.IEEE,2013.
[25] D.Heise,L.Rosales,M.Skubic,andM.J.Devaney.Refinementandevaluation
ACKNOWLEDGMENT ofahydraulicbedsensor.InEngineeringinMedicineandBiologySociety,EMBC,
2011AnnualInternationalConferenceoftheIEEE,pages4356–4360.IEEE,2011.
WearegratefultotheSenSysreviewersfortheirconstructivecri- [26] A.Hyva¨rinen,J.Karhunen,andE.Oja. Independentcomponentanalysis,vol-
tique,andourshepherd,Dr.WenHu,forhisvaluablecomments, ume46.JohnWiley&Sons,2004.
[27] Z.Jia,M.Alaziz,X.Chi,R.E.Howard,Y.Zhang,P.Zhang,W.Trappe,A.Siva-
allofwhichhavehelpedusgreatlyimprovethispaper.Thiswork subramaniam,andN.An.Hb-phone:Abed-mountedgeophone-basedheartbeat

SenSys’17,November6–8,2017,Delft,Netherlands Z.Jiaetal.
monitoringsystem.In201615thACM/IEEEInternationalConferenceonInforma- [41] S.Pan,A.Bonde,J.Jing,L.Zhang,P.Zhang,andH.Y.Noh. Boes:building
tionProcessinginSensorNetworks(IPSN),pages1–12.IEEE,2016. occupancyestimationsystemusingsparseambientvibrationmonitoring.InSPIE
[28] I.Jolliffe.Principalcomponentanalysis.WileyOnlineLibrary,2002. SmartStructuresandMaterials+NondestructiveEvaluationandHealthMonitoring,
[29] R.E.Kleiger,J.P.Miller,J.T.Bigger,andA.J.Moss. Decreasedheartrate pages90611O–90611O.InternationalSocietyforOpticsandPhotonics,2014.
variabilityanditsassociationwithincreasedmortalityafteracutemyocardial [42] S.Pan,C.G.Ramirez,M.Mirshekari,J.Fagert,A.J.Chung,C.C.Hu,J.P.Shen,
infarction.TheAmericanjournalofcardiology,59(4):256–262,1987. H.Y.Noh,andP.Zhang.Surfacevibe:vibration-basedtap&swipetrackingon
[30] J.M.Kortelainen,M.vanGils,andJ.Parkka.Multichannelbedpressuresensor ubiquitoussurfaces.InIPSN,pages197–208,2017.
forsleepmonitoring.ComputinginCardiology,39:313–316,2012. [43] T.Park.IntroductiontoDigitalSignalProcessing:ComputerMusicallySpeaking.
[31] C.Langton.Hilberttransform,analyticsignal,andthecomplexenvelope.Signal WorldScientific,2010.
ProcessingandSimulationNewsletter,1999. [44] D.O.PedersonandK.Mayaram.Demodulatorsanddetectors.AnalogIntegrated
[32] J.Liu,Y.Wang,Y.Chen,J.Yang,X.Chen,andJ.Cheng.Trackingvitalsignsduring CircuitsforCommunication,pages457–484,2008.
sleepleveragingoff-the-shelfwifi.InProceedingsofthe16thACMInternational [45] D.Phan,S.Bonnet,R.Guillemaud,E.Castelli,andN.P.Thi. Estimationof
SymposiumonMobileAdHocNetworkingandComputing,pages267–276.ACM, respiratorywaveformandheartrateusinganaccelerometer. InEngineering
2015. inMedicineandBiologySociety,2008.EMBS2008.30thAnnualInternational
[33] S.Lloyd.Leastsquaresquantizationinpcm.IEEEtransactionsoninformation ConferenceoftheIEEE,pages4916–4919.IEEE,2008.
theory,28(2):129–137,1982. [46] J.G.Proakis.Digitalcommunications.McGraw-Hill,NewYork,1995.
[34] D.C.Mack,J.T.Patrie,P.M.Suratt,R.A.Felder,andM.Alwan.Developmentand [47] L.R.Rabiner.Atutorialonhiddenmarkovmodelsandselectedapplicationsin
preliminaryvalidationofheartrateandbreathingratedetectionusingapassive, speechrecognition.ProceedingsoftheIEEE,77(2):257–286,1989.
ballistocardiography-basedsleepmonitoringsystem.InformationTechnologyin [48] S.Rickard.Theduetblindsourceseparationalgorithm.BlindSpeechSeparation,
Biomedicine,IEEETransactionson,13(1):111–120,2009. pages217–237,2007.
[35] R.MersereauandT.Seay.Multipleaccessfrequencyhoppingpatternswithlow [49] L.Rosales,M.Skubic,D.Heise,M.J.Devaney,andM.Schaumburg.Heartbeat
ambiguity.IEEETransactionsonAerospaceandElectronicSystems,pages571–578, detectionfromahydraulicbedsensorusingaclusteringapproach.InEngineering
1981. inMedicineandBiologySociety(EMBC),2012AnnualInternationalConferenceof
[36] M.Mirshekari,S.Pan,P.Zhang,andH.Y.Noh.Characterizingwavepropagation theIEEE,pages2383–2387.IEEE,2012.
toimproveindoorstep-levelpersonlocalizationusingfloorvibration.InSPIE [50] J.O.Smith.Introductiontodigitalfilters:withaudioapplications,volume2.Julius
SmartStructuresandMaterials+NondestructiveEvaluationandHealthMonitoring, Smith,2008.
pages980305–980305.InternationalSocietyforOpticsandPhotonics,2016. [51] S.SˇpragerandD.Zazula. Heartbeatandrespirationdetectionfromoptical
[37] R.Nandakumar,S.Gollakota,andN.Watson.Contactlesssleepapneadetection interferometricsignalsbyusingamultimethodapproach.IEEEtransactionson
onsmartphones.InProceedingsofthe13thAnnualInternationalConferenceon biomedicalengineering,59(10):2922–2929,2012.
MobileSystems,Applications,andServices,pages45–57.ACM,2015. [52] S.SˇpragerandD.Zazula. Detectionofheartbeatandrespirationfromopti-
[38] K.Narkiewicz,N.Montano,C.Cogliati,P.J.VanDeBorne,M.E.Dyken,andV.K. calinterferometricsignalbyusingwavelettransform.Computermethodsand
Somers.Alteredcardiovascularvariabilityinobstructivesleepapnea.Circulation, programsinbiomedicine,111(1):41–51,2013.
98(11):1071–1077,1998. [53] T.WatanabeandK.Watanabe.Noncontactmethodforsleepstageestimation.
[39] J.Nolan,P.D.Batin,R.Andrews,S.J.Lindsay,P.Brooksby,M.Mullen,W.Baig, IEEETransactionsonbiomedicalengineering,51(10):1735–1748,2004.
A.D.Flapan,A.Cowley,R.J.Prescott,etal. Prospectivestudyofheartrate [54] Y.Yamana,S.Tsukamoto,K.Mukai,H.Maki,H.Ogawa,andY.Yonezawa. A
variabilityandmortalityinchronicheartfailure.Circulation,98(15):1510–1516, sensorformonitoringpulserate,respirationrhythm,andbodymovementinbed.
1998. InEngineeringinMedicineandBiologySociety,EMBC,2011AnnualInternational
[40] S.Nukaya,T.Shino,Y.Kurihara,K.Watanabe,andH.Tanaka.Noninvasivebed ConferenceoftheIEEE,pages5323–5326.IEEE,2011.
sensingofhumanbiosignalsviapiezoceramicdevicessandwichedbetweenthe [55] O.YilmazandS.Rickard.Blindseparationofspeechmixturesviatime-frequency
floorandbed.SensorsJournal,IEEE,12(3):431–438,2012. masking.IEEETransactionsonsignalprocessing,52(7):1830–1847,2004.