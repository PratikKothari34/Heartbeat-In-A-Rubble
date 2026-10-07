PigV2: Monitoring Pig Vital Signs through Ground Vibrations
Induced by Heartbeat and Respiration
YiwenDong∗ JesseRCodling GaryRohrer
ywdong@stanford.edu UniversityofMichigan USDA,ARS,U.S.MeatAnimal
StanfordUniversity AnnArbor,Michigan,USA ResearchCenter,ClayCenter
Stanford,California,USA USA
JeremyMiles SudhenduSharma TamiBrown-Brandl
USDA,ARS,U.S.MeatAnimal UniversityofNebraska-Lincoln UniversityofNebraska-Lincoln
ResearchCenter,ClayCenter Lincoln,Nebraska,USA Lincoln,Nebraska,USA
USA
PeiZhang HaeYoungNoh
UniversityofMichigan StanfordUniversity
AnnArbor,Michigan,USA Stanford,California,USA
ABSTRACT ACMReferenceFormat:
Pigvitalsignmonitoring(e.g.,estimatingtheheartrate(HR)and YiwenDong,JesseRCodling,GaryRohrer,JeremyMiles,SudhenduSharma,
TamiBrown-Brandl,PeiZhang,andHaeYoungNoh.2022.PigV2:Monitor- respiratoryrate(RR))isessentialtounderstandthestresslevelof
ingPigVitalSignsthroughGroundVibrationsInducedbyHeartbeatand
thesowanddetecttheonsetofparturition.Ithelpstomaximize
Respiration.InThe20thACMConferenceonEmbeddedNetworkedSensor
peri-natalsurvivalandimproveanimalwell-beinginswineproduc-
Systems(SenSys’22),November6–9,2022,Boston,MA,USA.ACM,NewYork,
tion.Theexistingapproachmainlyreliesonmanualmeasurement,
NY,USA,7pages.https://doi.org/10.1145/3560905.3568416
whichislabor-intensiveandonlyprovidesafewpointsofinforma-
tion.Othersensingmodalitiessuchaswearablesandcamerasare
1 INTRODUCTION
developedtoenablemorecontinuousmeasurement,butarestill
limitedduetoanimaldiscomfort,datatransfer,andstoragechal- Monitoringpigvitalsigns(e.g.,heartrate(HR)andrespiratoryrate
lenges.Inthispaper,weintroducePigV2,thefirstsystemtomonitor (RR))isimportantinprovidingpighealthinformationforsmart
pigheartrateandrespiratoryratethroughgroundvibrations.Our swineproduction[4,17].Specifically,monitoringthesow’sheart
approachleveragestheinsightthatbothheartbeatandrespiration rateandrespiratoryrateinafarrowingpenenablespredictions
generategroundvibrationswhenthesowislyingonthefloor.We ofstresslevelsandtheonsetofparturition[7,10,16,19,21].This
infervitalinformationbysensingandanalyzingthesevibrations. informationhelpsthecaretakertodeterminewhichsowandwhen
ThemainchallengeindevelopingPigV2istheoverlapofvital-and toassistinreducingneonatalmortalityinswineproduction,im-
non-vital-relatedinformationinthevibrationsignals,includingpig provinganimalwell-beingandproductionefficiency.
movements,pigpostures,pig-to-sensordistances,andsoon.To Traditionalmonitoringreliesonfarmersobservingsowbehav-
addressthisissue,wefirstcharacterizetheireffects,extracttheir ior,whichistime-consuming,requireprofessionaltraining,and
currentstatus,andthenreducetheirimpactbyadaptivelyinterpo- onlyproducessporadicresults.Inaddition,manuallymeasuringthe
latingvitalratesovermultiplesensors.PigV2isevaluatedthrough pig’sHRandRRcausesstresstotheanimalandmayexposethemto
areal-worlddeploymentwith30pigs.Ithas3.4%and8.3%average healthrisks.Priorworkadoptedwearablesensorsandcontact-less
errorsinmonitoringtheHRandRRofthesows,respectively. camerastocollectsuchinformation[1,11,12,14,20].Still,theyface
challengeswithanimaldiscomfort,batterylife,datatransmission,
andinsufficientbandwidthissues,whichhampersthescalability.
CCSCONCEPTS
Priorworkexploredvibration-basedmonitoringforhumansand
•Appliedcomputing→Agriculture.
animals,whichutilizesvibrationsensorsattachedtothefloorto
capturevibrationsinducedbythesubjects[8,9].Groundvibration
KEYWORDS
sensingiscontact-lesstoanimals,wide-ranged,andhasa∼200×
structuralvibration,heartrate,respiratoryrate,vitalsigns,pig, reductionofdatatransmissionandprocessingrequirementcom-
precisionlivestockfarming paredtothecameras[6].Ithassucceededinpigweightmonitoring
andactivityrecognition,includingnursing,posturechanges,and
ACMacknowledgesthatthiscontributionwasauthoredorco-authoredbyanemployee, growthpatterns[2,5,6].
contractor,oraffiliateoftheUnitedStatesgovernment.Assuch,theUnitedStates
governmentretainsanonexclusive,royalty-freerighttopublishorreproducethis
Inthispaper,wepresentPigV2(Pig-inducedgroundVibrations
article,ortoallowotherstodoso,forgovernmentpurposesonly. forVitalmonitoring),whichisthefirstsystemtoachieveanimal
SenSys’22,November6–9,2022,Boston,MA,USA vitalsignmonitoringthroughgroundvibrationsensing.Oursystem
©2022AssociationforComputingMachinery. leveragestheknowledgethatthesow’sheartbeatandrespiration
ACMISBN978-1-4503-9886-2/22/11...$15.00
https://doi.org/10.1145/3560905.3568416 exertforcesontothegroundthatgeneratevibrations.Thisinsight
2202
ceD
7
]PS.ssee[
1v87330.2122:viXra

SenSys’22,November6–9,2022,Boston,MA,USA Dong,etal.
allowsustomonitortheirratesbysensingandanalyzingthesevi-
brationwavescollectedbylow-cost,contact-lessvibrationsensors. Lying 500
Itischallengingtomonitorpigvitalsignsthroughgroundvibra-
tionsduetothemixtureofvital-andnon-vital-relatedinformation 250
inthevibrationsignals.Specifically,vibrationsignalsareinfluenced
significantlybypigbehaviors,includingmovements,differentpos- 0
11:05:52 11:05:56 11:06:00 11:06:04
tures,locations,etc.Inaddition,thesebehaviorschangeovertime Time (s) Apr 26, 2022
and are hard to control because of the choices made by the in- Sitting
dividualpigs.Yet,theyovershadowthevital-relatedinformation,
leadingtolowsignal-to-noiseratios(SNR)andbiasinHRandRR
estimations.
Toovercomethischallenge,wecharacterizethevibrationsignal
under the influence of various pig behaviors and develop a pig
vitalmonitoringmethodwithstableperformancesdespitesuch
changes.Toachievethis,wefirstextractpigbehaviorsbasedon
thecharacterization.Then,wereducetheimpactofsuchbehavior
onvitalmonitoringbydetectingandclassifyingthem.Finally,we
interpolateHRandRRwhenmovementshappenortheposture
changes,andcombinetheresultsamongmultiplesensors.
Toevaluateourmethod,weconductedareal-worldevaluationat
aresearchfarmintheU.S.with30pigsovermultipledeployments.
Ourmethodhasachievedanaverageof3.4%(±3.7heartbeatsper
minute)and8.3%(±3.5respirationsperminute)errorinHRand
RRmonitoring,respectively.
Thecontributionsofthispaperare:
• Wedevelopthefirstanimalvitalsignmonitoringsystem
throughgroundvibrationsensing,whichenablescontinuous,
contact-less,cost-efficientheartrateandrespiratoryrate
monitoring.
• Wecharacterizehowpigmovements,postures,andpig-to-
sensordistancesaffectthevibrationsignalforvitalmonitor-
ingusingphysicalinsightsofgroundvibrations,anddevelop
analgorithmtoreducesuchinfluenceunderchangingpig
behaviors.
• Weconductareal-worldevaluationwith30pigsachieving
anaverageof3.4%and8.3%errorsinHRandRRmonitoring,
respectively.
Theremainderofthepaperfirstpresentsthephysics-informed
characterizationofhowthepigbehaviorsaffecttheHRandRR
monitoring(Section2),thenintroducesourmethodthatmonitors
pigvitalsignsundervariouspigbehaviorinfluences(Section3),and
finallydiscussthereal-worldexperimentandevaluationresults
(Section4),followedbyfuturework(Section5)andconclusions
(Section6).
2 PHYSICS-INFORMED
CHARACTERIZATIONFOR
VIBRATION-BASEDPIGVITAL
MONITORING
Theprimaryphysicalinsightofourvibration-basedpigvitalmon-
itoringisthatgroundvibrationsaregeneratedbythechangeof
forcesfromthesowduetoherheartbeatandrespiration.Whenthe
sowislyingstill,herbodyweightisassumedtobeaconstantforce
exertedonthefloor.Ontopofthat,herheartbeatandrespiration
induceslightbodymotionthatexertsadditionalvaryingforces
muS
.feoC
televaW
Heartbeat Wavelet Sum
Detected Heartbeats
500
250
0
11:29:44 11:29:48 11:29:52 11:29:56
Time (s) Apr 26, 2022
muS
.feoC
televaW
pig movements
good SNR
pig movements
Heartbeat Wavelet Sum
Detected Heartbeats
lower SNR
Figure 1: Samples of wavelet-transformed vibration signal
during sitting and lying postures. The lying posture pro-
ducesmoresignificantimpulsesandbetterSNRthansitting.
Thehighamplitudespikes(inpinkboxes)correspondtothe
pigmovements,whichovershadowtheheartbeats.
ontheground,whichbreakstheforceequilibriumoftheground
andresultsinvibrationstoretainitsequilibrium.Thesevibrations
thenpropagatethroughthefloorandarerecordedbythevibration
sensorsattachedtothebottomofthepigpen.
Duringtheprocessmentionedabove,thevibrationsignalsare
influencedbyvariouspigbehaviors,including1)postures,2)move-
ments,and3)pig-to-sensordistances.Moreover,thesebehaviors
typicallyvaryovertimeandarehardtocontrolinreal-worldsce-
narios,leadingtounstableperformanceandunreliableHRandRR
estimationsfromthevibrationsignals.Toovercomethisissue,we
firstcharacterizetheeffectofeachbehaviortodevelopasystem
insensitivetosuchbehaviorchanges.
EffectofPigPostures. Differentsowposturesresultinvarious
signalpatternsduetothedifferenceinbodymotionsandcontact
surfaces.First,theheartbeatandrespirationcauseuniquemotionin
eachpartofthepigbody,whichpushesthefloorindifferentways.
Inaddition,theweighttransferandthecontactsurfacebetween
thepigbodyandthefloormayalsovarywhentheposturechanges.
Forexample,heartbeatandrespirationinduceapparentmotions
onthesow’sabdomenbutmuchlessonherhind-quarterandfeet,
so the lying posture produces more significant impulses in the
vibrationsignalsthanstandingandsitting.Inaddition,thelateral
lyingpostureinducesbetterSNRthansternallying(seeFigure1).
Thisisbecausetheweighttransferduringlaterallyingleadstoa
morestablegravityforceandalargercontactsurface.
EffectofPigMovements. Movementsfromthesowinduce
significantchangesintheforcemagnitudesexertedontotheground,
whichtypicallyovershadowstheforcechangesduetoheartbeat
andrespiration(seeFigure1).Suchmovementshappenforvarious
reasons,includingwithin-postureadjustments,posturechanges,
dailyactivities(e.g.,ingestionandexcretion),andsoon.Basedon
ourobservations,postureadjustmentinducesminorsignalchanges
amongall,yetitstillhasa5-10×increaseinmagnitudethanthe
vibrationinducedbyheartbeat.
EffectofPig-to-SensorDistances. Thechangingdistancebe-
tweenthepigandthesensoraffectstherecordedvibrationsignals

PigV2:MonitoringPigVitalSignsthroughGroundVibrationsInducedbyHeartbeatandRespiration SenSys’22,November6–9,2022,Boston,MA,USA
§3.1 Pig-induced §3.2 Pre-processing §3.3 Pig Behavior
Vibration and Environmental Compensation
Acquisition Noise Reduction • Pig Behavior Extraction
• Heart Rate
Sensor Sensor • E H n a v rd ir w on a m re e D nt e - s T i o g l n erant • • W Fr h e i q te u e N n o c i y s - e S F pe ilt c e if r i i c n g Noise • a H n e d a r D t i a s n to d r t R io e n s p C i o ra rr to e r c y ti o R n ate • Respiratory Rate
• Ease of Assembly Reduction Estimation (for every second)
• RemoteConfiguration • Environmental Event • Adaptive Multi-Sensor
Pig-induced ground vibration and Data Collection Detection Interpolation
Figure2:PigV2SystemOverview
becausethesignalsaredistortedduringthevibrationwaveprop- designimprovesreliabilityinthefarmenvironmentthrougheaseof
agation. Such distortion is mainly due to the effect of 1) wave deploymentbynon-engineersanditsabilitytoadapttounknown
attenuationand2)wavedispersion.Asthewaveattenuatesover andchangingconditions.
longerdistances,themagnitudeofvitalsign-inducedvibrations
decreasesexponentially,sosensorsoutsidethesensingrangedo 3.2 DataPre-processingandEnvironmental
notcapturethevitalsigns(thesensingrangeisaround2meters
NoiseReduction
basedonpreliminarytesting).Inaddition,sincewavesofdifferent
Thevibrationsignalsarepre-processedthroughfilters,anenviron-
frequenciestravelatvariousvelocities,thearrivaltimeoftheir
mentaleventdetectionalgorithm,andwaveletdecompositionto
peakstendstomisalignasthesensingdistanceincreases,leading
reducevariousenvironmentalnoises.
tomultiplesmallerpeaksperheartbeat.
ThesignalsarefirstappliedwithaWienerfiltertoreducethe
whitenoise.Then,weprocessthesignalthroughaband-passfilter
3 PIGVITALSIGNMONITORINGTHROUGH
and select the 0 to 200 Hz band for further analysis. This step
GROUNDVIBRATIONS
allowsustoreducethehigh-frequencynoisesfromtheelectrical
PigV2consistsofthreemodules:1)pig-inducedvibrationacquisi- andmechanicalcomponentsinthefarmenvironment(i.e.,fans,air
tion,2)pre-processingandenvironmentalnoisereduction,and3) conditioners)whilepreservingthepig’svital-relatedinformation
pigbehaviorcompensation(asdescribedinFigure2). oflowerfrequencies.
Noisesinducedbyenvironmentalevents(e.g.,waterflushing,
3.1 Pig-InducedVibrationAcquisition staffwalking,tractorspassingby)aredetectedandremovedby
PigV2acquiresvibrationdatafromarobustnetworkofgeophone matchingthesignalwithpre-existingtemplatesofthoseevents.To
sensorsmountedbelowthepigs’penssimilartopastworks[2,5, achievethis,wefirstcropthesignalsbasedonthescheduledstart
6].Thenetworkisarrangedintotierstoovercomethetradeoffs andendtimesofregularstaffcheck-inandcleaning.Then,within
ofreliabilityandsensingperformance[5].Atthelowesttierare thesecroppedsignals,weapplyaslidingwindowof10secondswith
low-powergeophonenodeswhichconverttheverticalmovement 50%ofoverlaptodividethecontinuoussignalintosegments.The
velocityofthepigpenfloortoastreamofdata.Thesecondtier 10-secondwindowwaschosenbasedonthemaximumdurationof
aggregatesthesestreamsandforwardsthemtothefinaltier.This thoseevents.Eachsegmentiscomparedwiththeexistingtemplates
tieralsomanagesthenodesbasedonremoteconfiguration.Off-site bytakingthecross-correlationforalignmentandcosinedistance
resourcescomprisethefinaltierwherethedataprocessingoccurs. forsimilaritycomparison.Windowswithsimilarityscoreshigher
Initscurrentiteration,thesensornodesarelow-powerinterms thanthethresholdaremarkedasenvironmentalnoises.
ofprocessingcapability,butnotintermsofelectricityconsumption. Finally,weapplywavetransformtotheprocessedsignal.During
Oursensorsareoptimizedtosurvivetheharshfarmenvironment thewavelettransform,wechoosethegeneralizedMorsewaveletas
(e.g.,waterflushing,animalactivities)andeaseofassemblyfirst. thebasisfunctionbecauseithasasinglepeakforeachheartbeat-
Whilesimpler,low-capabilitydevicesimproverobustnessthrough /respiration-inducedimpulse,allowingHRandRRestimationby
redundancy,theirpowerconsumptionhasthusfarbeenlesscritical. countingthenumberofpeaksperminuteinthetransformedsignal.
Giventhenatureoftheirsensingtask,however,thesesensorscould
bemadetofunctionwithoutexternalpower.Minimalhardware 3.3 PigBehaviorCompensation
adjustmentcanreadilytradesomeconfigurationresponsiveness Inthissection,wemonitorpigHRandRRaccordingtothechang-
forsignificantgainsinpowerconsumptionforoff-griduse. ing pig behaviors (including pig postures, movements, and pig-
Remotemanagementisakeyfacilitatorenablingdeployment to-sensordistances).First,weextractthepigbehaviorsfromthe
bynon-engineers.InPigV2,theaggregatortierconnectstothe vibrationsignalsovertimeandremovethenon-vital-relatedsignal
sensornodesviaawirelesslink,butcanalsobeaccessedremotely segments.Then,wedevelopamethodbasedonwaveletdecom-
throughthesamewayitsendsdataofftotheprocessingtier.Once positionandpeakdetectiontoestimateHRandRR.Finally,we
suppliedwithaninternetconnection,aremotespecialistcanper- combinetheresultsfrommultiplesensorsineachpenforadaptive
formsoftware-levelsetupaslocalstaffmountsthehardwareduring interpolationwhennon-vital-relatedpigbehaviorhappens.
deployment.Asdataarecollected,thesensors’gain,sampling,and
metadatacanbemanipulatedasneededbysendingremoteconfigu- 3.3.1 PigBehaviorExtractionandDistortionCorrection. Weextract
rationchangestotheaggregator,eventhoughthephysicaldevices thepigbehaviorsfromthesignalsinordertoreducethebiasin
areinaccessiblewhenpigsarepresent.Thisconfigurablenetwork estimationandimprovetheconsistencyinperformanceovertime.

SenSys’22,November6–9,2022,Boston,MA,USA Dong,etal.
8000
4000
0
11:16:44 11:16:46 11:16:48 11:16:50 11:16:52
Time (s) Jul 21, 2022
)V(
edutilpmA
Signal of Sensor 1 (0.1m away) Signal of Sensor 2 (2m away) 8000 Corrected Signal of Sensor 2 (2m away)
6000
4000
2000
0
19:15:10 19:15:20
Figure 3: Signals from a sensor away from the pig (pink Time (s) Nov 09, 2021
dashedline)arecorrectedbasedonthedispersionandatten-
uationeffectduringwavepropagationfromthepigtothe
sensorlocation.Thepeaksfromthecorrectedsignal(pink
solidline)alignwellwiththesignalsfromthesensorright
underneaththepig(blackdashedline).
AsdiscussedinSection2,thesebehaviorsinclude1)pigpostures,
2)pigmovements,and3)pig-to-sensordistances.
PigPostureClassification. Thepig’sposturesignificantlyaf-
fectsthevital-relatedsignal-to-noiseratio(SNR).Therefore,clas-
sifyingthepigposturehelpsimprovetheestimationaccuracyby
removingthesegmentsbelowourSNRrequirements.InPigV2,pig
postureispredictedaseitherlying,sitting/kneeling,andstanding,
usingtherandomforestclassifiertrainedinourpriorstudy[2,6].
Apreliminarystudyfoundthatpigsliemorethan80%ofthetime.
Meanwhile,sittingandstandingdonotproducesufficientSNRfor
vitalsignmonitoring,asdiscussedinSection2.Basedontheabove
evidence,weprioritizethesignalsfromthelyingposture(includ-
ingbothlateralandsternallying)andcutoutthesignalsfromthe
otherpostures.Thecutoutsignaldurationwillbecompensatedby
interpolationinSection3.3.3.
PigMovementDetection. Pigmovementsaredetectedbased
onananomalydetectionalgorithminordertoremovethenon-
vital-relatedsignalsegmentsthatbiasthevitalrateestimation.First,
thealgorithmtakesa10-secondvibrationsignalwhenthesowis
lyingstillwitharegularheartbeatandrespirationasareference.
Then,a1-secondslidingwindowisappliedtothesignaltodetect
thepigmovements:anywindowwithameanlargerthanthree
standarddeviationsfromthereferencesignal(i.e.,outof99.7%con-
fidenceinterval)isdetectedasawindowcontainingpigmovements.
Finally,signalswithinthesewindowsareremovedandwillbeinter-
polatedusingadjacentvitalrateestimationsand/orreadingsfrom
thenearbysensors,whichwillbediscussedinSection3.3.3.
Pig-to-SensorSignalDistortionCorrection. Thevibration
signalsaredistortedduringwavepropagation.AsdiscussedinSec-
tion2,suchdistortionisreducedintwoaspects:waveattenuation
andwavedispersion.
Wefirstcomputetheattenuationcoefficient𝛼duringpreliminary
testingwithatleasttwosensorstocorrectthewaveattenuation
effect.Assumingafixedattenuationequationwithintheentirepen,
wesolvetheinverseproblemandrevertthesignalenergytomatch
theamplitudesmeasuredbythesensorrightbelowthepig.
𝑆
𝑙𝑜𝑐2
=𝑆
𝑙𝑜𝑐1
𝑒−𝛼𝑓𝑑 (1)
muS
tneiciffeoC
televaW
Heartbeat Wavelet Sum Detected Heart Beats
Respiration Wavelet Moving Sum
Detected Respirations
Figure4:Heartbeats(greentriangles)andrespirations(pink
circles)aredetectedinthevibrationsignalswhenthesowis
lyingstill.
where𝑆isthevibrationsignalamplitude,𝑓 isthefrequencycom-
ponent,and𝑑isthepig-to-sensordistance.
Thedispersioneffectischallengingtocorrectduetotheun-
knownwavepropagationvelocitieswhenittravelsthroughthe
floor.Therefore,insteadofrevertingthesignaltothepiglocation,
wechoosetomitigatethedispersioneffecttoimprovethevital
monitoringaccuracy.Sincewavedispersionresultsinmisaligned
signalpeaks(asmentionedinSection2),were-alignthosepeaks
bytakingthemovingaveragealongthepre-processedsignalbased
onanapproximatedtimelagforeachsensinglocation,asshownin
Figure3.Forexample,thevibrationwavetypicallytravelsaround
100-200m/saccordingtopreviousstudies[15],a0.05second(i.e.,25
samples)movingaverageischosenwhenthepig-to-sensordistance
is5meters.
3.3.2 HeartRateandRespiratoryRateEstimation. Afterreducing
theeffectofpigbehaviors,weestimatetheHRandRRforeachsen-
sorbycountingthenumberofdetectedheartbeatsandrespirations
withinaminute.
Theheartbeatsaredetectedthroughpeakpickingoverthesum
ofwaveletcoefficientsfrom10to100Hz(seethesolidgreenline
inFigure4).Therangeischosenbasedonthetypicalheartbeat-
inducedvibrationfrequencyrange(0-100Hz)andthesensitivity
rangeofthesensors(≥10Hz).SincetheHRofthesowtypically
rangesfrom60to120beatsperminute,wesettheminimumpeak
prominenceas0.5secondstoavoidthefalsedetectionoftheadja-
centlowerpeakcausedbydiastole.
Unliketheimpulsegeneratedbytheheartbeat,respirationin-
ducesaslowerchangeinforceswhenthesow’sbodypressesonto
theground,indirectlyaffectingtheenergytrendoftheheartbeat
impulses.Therefore,respirationisdetectedbypickpeakingover
themovingsumofthewaveletcoefficientstocapturetheenergy
trendoftheimpulses(seethedashedpinklineinFigure4).Since
theRRofthesowtypicallyrangesfrom10to60breathsperminute,
wesettheminimumpeakprominenceas1secondtoreducethe
falsepositiveratecausedbystrongheartbeats.
3.3.3 Adaptive Multi-Sensor Interpolation. To monitor pig vital
signscontinuouslywithreliableHRandRRestimations,weinter-
polatetheresultsovertimebyadaptivelycombiningtheresults
frommultiplesensorsunderneaththesamepen.

PigV2:MonitoringPigVitalSignsthroughGroundVibrationsInducedbyHeartbeatandRespiration SenSys’22,November6–9,2022,Boston,MA,USA
Wefirstconductinterpolationoneachsensorduringtheremoved
signalswhenthesowisinsitting/standingposturesorinmotion. our vibration
Anexistingstudysuggeststhatthechangeofposturesoftenleads sensor
manual
toanimmediateandsignificantincreaseinHRandthendecreases measurement
graduallyafterthesowreturnstotherestingposture[3].Therefore,
wechoosesplineinterpolationtomodelsuchamechanism,which
capturesthesuddenincreaseandgradualdecreasemoreeffectively
thanalinearfunction.
Aftertheinterpolation,wecombinetheresultsfrommultiple (a) (b)
sensorstoensurecontinuousandaccuratemonitoringofvitalsigns.
Toavoidsysteminterruptionsduetoseldomsensorconnectionis-
Figure5:Experimentsetup:a)ourvibrationsensorinwater-
sues,wecontinuouslymonitorthefunctionalstatusofeachsensor
proofboxes,b)manualmeasurementforgroundtruthsand
andconductanalysisonlyontheactivesensors.Thereisatradeoff
ourcontact-lessvibrationsensorattachedtothebottomof
whencombiningvarioussensors.Whilethesensorsclosertothe
thefloor.
sowtypicallyhaveabetterSNRonvitalsigns,theyaremoresensi-
tivetothepig’smovements.Therefore,thesensorsclosertothepig
typicallyrequirealongerdurationofinterpolation,whichhampers
vitalmonitoringaccuracy.Therefore,wecomputetheweighted
averageofmultiplesensorstoestimatethevitalrates.Theweight
𝑤 basedontheinterpolationduration𝑡𝑖𝑛𝑡 andthedistancefrom
𝑠 𝑠
thepig𝑑 ,computedasfollows:
𝑠
𝑤 𝑠 =
𝑇 −𝑡
𝑠
𝑖𝑛𝑡
𝑒−𝑑𝑠 (2)
𝑇
where𝑇 isthelengthoftimeforeachroundofpeakdetection
(a) Heart Rate Results (b) Respiratory Rate Results
(i.e.,60secondsinthiscase).Thisformulaisdevelopedbasedon
theexponentialdecreaseofSNRw.r.t.thesensingdistanceand
thelineardecreaseofvital-relatedinformationastheinterpolation Figure 6: Overall performance of our PigV2 system: a) the
durationincreases. HR prediction error is 3.4% (±3.7 beats per minute), b) the
RRpredictionerroris8.3%(±3.5breathsperminute).Both
4 REAL-WORLDEVALUATION errorsarecomparabletothePulseOxandmanualcounting
error,whichis2%and7%,respectively.
Weevaluateoursystemthroughmultiplefielddeploymentson
aresearchfarmintheUSA.Inthissection,wefirstdiscussour
experiment setup, then show the system performance in terms
Thedevicehasanerrorof±2beatsperminute(∼2%).TheRRwas
of prediction accuracy, and finally discuss and demonstrate its
countedmanuallybywatchingthepig’sflank(i.e.,abdomen)raise
robustnesstothechangingpigbehaviors.
andlower,whichisestimatedtohaveanaccuracyof±3respirations
perminute(∼7%)bycomparingthecountsfromtwoindividuals.To
4.1 FieldExperimentImplementation
mitigatetheriskduringdatacollection,eachsowismonitoredfor
WeconductedmultipledeploymentsforPigV2 ontheU.S.Meat 1-2minutes.Theaverageheartandrespiratoryratesperminuteare
AnimalResearchCenterinNebraska,USA,with30pigs.Datacol- 98and35,respectively.Thenumbertendstobehigherthannormal
lectionwasperformedinaccordancewithfederalandinstitutional becauseHRandRRusuallyincreasewhenahumanapproachesthe
regulations regarding proper animal care practices and was ap- sowandtakesmeasurements[13].
provedbytheU.S.MeatAnimalResearchCenter’sInstitutional
AnimalCareandUseCommitteeas𝐸𝑂#143.0.and𝐸𝑂#171.0. 4.2 SystemPerformance
Weinstalled30geophonesensorsovereightpens,inwhichthree
Overall,PigV2hasanaverageerrorof3.4%and8.3%forHRandRR,
pensaredeployedwith5sensors,andtheotherfivearedeployed
respectively.AsillustratedinFigure6,theerrorrateiscomparable
with3sensors.Thesamplingfrequencyis500Hz.Allsensorsare
totheaccuracyofPulseOxandmanualRRobservations,whichhas
concealedinplasticboxeswithawatertightenclosuretoprevent
anerrorrateof2%and7%forHRandRR,respectively.Theaccuracy
damagefromhigh-pressurewaterduringcleaningandexcretion
issufficientforpredictingthestresslevelandonsetofparturition
fromthesowduringoperation(seeFigure5a).Thesensorswereall
inpigs,whichtypicallyhasamorethana7-20%increaseinHR
installedunderneaththepen,fixedwithmultiplezip-tiestoensure
anda20-50%increaseinRRbasedonpreviousstudies[7,16,18].
firmcouplingwiththefloorstructure.
Thegroundtruthwascollectedbyouranimalscientistonthe 4.2.1 DailyPatterns. Wealsoobservethedailypatternsofpigvital
farm(seeFigure5b).Videocamerasarealsoinstalledabovethe signstounderstandthesow’sbehaviorchangesovertime.Figure7
pentoprovideinformationonpigposturesandmovements.The showstheHRandRRdailytrendsafterpigbehaviorcompensation
heartratewascollectedusingEdanVE-H100B,aveterinarypulse (withinterpolationwhenthepigismoving).ItappearsthatHRand
oximeter(PulseOx)thatmeasuresthepulseratethroughanearclip. RRhavesimilartrends.Theyfluctuatemoreandhaveahigherrate

| SenSys’22,November6–9,2022,Boston,MA,USA |        |     |             |     |     |                      | Dong,etal.     |
| ---------------------------------------- | ------ | --- | ----------- | --- | --- | -------------------- | -------------- |
| 120                                      |        |     |             |     |     | 15                   |                |
|                                          | active |     | Raw Data    |     |     |                      | HR Pred. Error |
|                                          |        |     | Moving Mean |     |     | )%( rorrE noitciderP |                |
|  etaR traeH )nim/staeb(                  |        |     |             |     |     |                      | RR Pred. Error |
Pulse Ox Error
| 100 |     |     |     |     |     | 10 8.8% | Manual RR Error |
| --- | --- | --- | --- | --- | --- | ------- | --------------- |
7.2%
5
| 80  |     |     | sleeping |     |     | 3.9% |     |
| --- | --- | --- | -------- | --- | --- | ---- | --- |
3%
| 00:00 | 06:00 | 12:00 | 18:00 | 00:00 |     |     |     |
| ----- | ----- | ----- | ----- | ----- | --- | --- | --- |
0
|                   |     | Time | Mar 05, 2021    |     |     | Sternal Lying | Lateral Lying |
| ----------------- | --- | ---- | --------------- | --- | --- | ------------- | ------------- |
| 60                |     |      |                 |     |     |               | Postures      |
|                   |     |      |                 | (a) |     |               | (b)           |
|  etaR yrotaripseR |     |      | Raw Data        |     |     |               |               |
Moving Mean
| )nim/shtaerb(  40 | active |     |     |     |     |     |     |
| ----------------- | ------ | --- | --- | --- | --- | --- | --- |
PigV2
|     |     |     |     | Figure 8: | adapts to | different postures. | a) percentage |
| --- | --- | --- | --- | --------- | --------- | ------------------- | ------------- |
distributionoverdifferentpostures,wherelyingtakes82%
20
|     |     |     |          | of time; b)                                          | the error of | PigV2 in lateral | lying posture is |
| --- | --- | --- | -------- | ---------------------------------------------------- | ------------ | ---------------- | ---------------- |
|     |     |     | sleeping | slightlysmallerthansternallying,andbotharecomparable |              |                  |                  |
0
| 00:00 | 06:00 | 12:00 | 18:00           | 00:00                         |     |     |     |
| ----- | ----- | ----- | --------------- | ----------------------------- | --- | --- | --- |
|       |       | Time  | Mar 05, 2021    | tothePulseOxandmanualRRerror. |     |     |     |
Figure7:DailytrendsofHRandRRsharesimilartrendsdur-
25
HR Pred. Error
| ingactiveandsleepingtimes.Thevariationduringsleeping |     |     |     |     |     | 21% |     |
| ---------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
)%( rorrE noitciderP 20 RR Pred. Error
| mayindicatetheREM/non-REMsleepstages. |     |     |     |     | Pulse Ox Error |     |     |
| ------------------------------------- | --- | --- | --- | --- | -------------- | --- | --- |
Manual RR Error
15 14.8%
inthemorning(around5am)andtheafternoon(4pm)whenthey
tendtobemoreactive.Inaddition,adecreasingtrendisobserved 10 8.9% 8.3%
6.2%
| whenthelightsareturnedoff(i.e.,from6pmto12pm)because |     |     |     |     | 4.9% |     |      |
| ---------------------------------------------------- | --- | --- | --- | --- | ---- | --- | ---- |
|                                                      |     |     |     | 5   | 3.6% |     | 3.4% |
thesowprimarilysleepsduringthattime.
| Itisworthnotingthatthereareregularfluctuationsduringthe |     |     |     | 0   |                         |              |               |
| ------------------------------------------------------- | --- | --- | --- | --- | ----------------------- | ------------ | ------------- |
|                                                         |     |     |     |     | Sen 1 (0m) Sen 2 (0.8m) | Sen 3 (1.4m) | Our Multi-Sen |
sow’ssleeping,whichmayindicatethesleepingstagesofthesow.    System
Basedontheexistingstudy,thenon-REMstageleadstoslower
breathsandheartbeats,whiletheREMstage(whendreamshappen) Figure9:Effectivenessofpig-to-sensordistancecorrection
leadstohigherHRandRR[22].Wewillexplorethistrendinfuture and multi-sensor fusion. While the accuracy decreases as
| work.                                           |     |     |            | thedistanceincreases,PigV2achievesalowererrorthanall |               |                |               |
| ----------------------------------------------- | --- | --- | ---------- | ---------------------------------------------------- | ------------- | -------------- | ------------- |
|                                                 |     |     |            | of these sensors                                     | by correcting | the distortion | effect during |
| 4.2.2 RobustnessAssessmentonPigBehaviorChanges. |     |     | Weevaluate |                                                      |               |                |               |
pig-to-sensorwavepropagationandcombiningresultsfrom
thesensitivityofPigV2withvariouspigbehaviorchangestoun-
multiplesensors.
derstandthesystemrobustnessandgeneralizabilitytowardsthese
changes.AsdiscussedinSection2and3,thesecontextincludepig
sowproducesthelowesterror.Asthepig-to-sensordistancein-
postures,movements,andpig-to-sensordistances. creases,thepredictionaccuracydecreasesbecausetheheartbeat-
andrespiration-inducedsignalsdistortsignificantlyduringwave
| DiscussiononPigPostureRobustness. |     |     | Weobservethepos- |     |     |     |     |
| --------------------------------- | --- | --- | ---------------- | --- | --- | --- | --- |
propagation,resultinginlowSNR.Oursystemreducestheerrorby
turedistributionbasedonthevideodatatounderstandtheper-
centage of lying, a posture that captures the most vital-related distancecorrectionandsensorfusion,whichleadstolowererror
information.AsshowninFigure8a,thelyingposturecovers82% thananyofthesensors’predictions.
ofthetimeduringourdeployment,whichmeansmostsignalscon-
tainvitalinformation.Figure8bshowsthesystemrobustnessover 5 FUTUREWORK
lateralandsternalpostures.Whilesternalpostureleadstoslightly Therearemanydirectionstoexploreinthefuture,giventherich
loweraccuracy,itisstillcomparabletothegroundtruthaccuracy. information inherent in the pig-induced ground vibration data.
Specifically,weidentifiedthreeimportantaspectsbasedonour
| EffectivenessofInterpolationduringPigMovements. |     |     |     | We  |     |     |     |
| ----------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
observationsandunderstandingsdevelopedthroughthisstudy.
evaluatetheeffectivenessofinterpolationbycomparingitwith
Stresslevelandsleepstagemonitoring:HRandRRaregood
thebaselinemethodwithoutcompensatingforthepigbehaviors.
indicatorsofpigs’stresslevelsandsleepingstages[13].Inthisstudy,
Resultsshowthatthepredictionerrorisreducedby3.6×forHR
weobservedchangesinbothrateswhenthefarmstaffapproached
and2×forRR.Ourapproacheffectivelyreducesthefalsepositives
|     |     |     |     | the sow and | when the sow | was sleeping. Further | study on the |
| --- | --- | --- | --- | ----------- | ------------ | --------------------- | ------------ |
causedbymovement-inducedimpulsesandmissingheartbeatsthat
relationshipbetweenthevitalratesandthesow’sstresslevelsand
areovershadowedbythemovements.
sleepingstagescanbehelpfulforcaretakerstoprovidetimelyhelp
toensuretheirwell-being.
EffectivenessofPig-to-SensorDistortionCorrectionand
We compared the prediction errors across var- Onsetofparturitionprediction:AnincreaseinHRandRRis
Sensor Fusion.
ious sensorsto show theeffectiveness of adaptivemulti-sensor alsoanimportantindicatorforparturition.Ourpriorstudyhasob-
fusion.AsdescribedinFigure9,thesensorrightunderneaththe servedincreasingsignalenergybeforethesowgivesbirth.Wewill

PigV2:MonitoringPigVitalSignsthroughGroundVibrationsInducedbyHeartbeatandRespiration SenSys’22,November6–9,2022,Boston,MA,USA
furtherexplorevibration-basedmethodstopredicttheparturition [6] JesseRCodling,YiwenDong,AmelieBonde,AdeolaBannis,AsyaMacon,Gary
time. Rohrer,JeremyMiles,SudhenduSharma,TamiBrown-Brandl,HaeYoungNoh,
andPeiZhang.[n.d.].SowPostureandFeedingActivityMonitoringinaFar-
Cardiaccycledisorderdetection:Weobservedthattheheartbeat-
rowingPenUsingGroundVibration.InECPLF2022-10thEuropeanConferencon
inducedvibrationstypicallyhavetwopeaks-aprimarypeakfol- PrecisionLivestockFarming(Vienna,Austria,2022-08-30).
lowedbyasecondarypeak,whichmaycorrespondtothesystole [7] FrancienHDeJonge,EAMBokkers,WGPSchouten,andFAHelmond.1996.
Rearingpigletsinapoorenvironment:developmentalaspectsofsocialstressin
anddiastolephasesofthecardiaccycle.Byextractingthepromi- pigs.Physiology&behavior60,2(1996),389–396.
nenceandtherelativeamplitudesofthesetwopeaks,wemaydetect [8] YiwenDong,JonathonFagert,PeiZhang,andHaeYoungNoh.2023.Stranger
disordersaffectingthecardiaccycle. DetectionandOccupantIdentificationUsingStructuralVibrations.InEuropean
WorkshoponStructuralHealthMonitoring.Springer,905–914.
Inaddition,wewillcontinueexploringvitalsignmonitoring [9] YiwenDong,JoannaJiaqiZou,JingxiaoLiu,JonathonFagert,MostafaMirshekari,
whentherearemultipleanimalsinthesamepenandanalyzethe LindaLowes,MeganIammarino,PeiZhang,andHaeYoungNoh.2020.MD-Vibe:
physics-informedanalysisofpatient-inducedstructuralvibrationdataformoni-
effectofdifferenttypesofpens.
toringgaithealthinindividualswithmusculardystrophy.InAdjunctproceedings
ofthe2020ACMinternationaljointconferenceonpervasiveandubiquitouscom-
6 CONCLUSIONS putingandproceedingsofthe2020ACMinternationalsymposiumonwearable
computers.525–531.
Inconclusion,weintroducePigV2,thefirstsystemtomonitorpig [10] ICdeJong,AndreaSgoifo,ElbertLambooij,SMechielKorte,HarryJBlokhuis,
HRandRRthroughgroundvibrations.Ourapproachleverages andJaapMKoolhaas.2000.Effectsofsocialstressonheartrateandheartrate
variabilityingrowingpigs. CanadianJournalofAnimalScience80,2(2000),
thephysicalinsightthatheartbeatandrespirationinduceground 273–280.
vibrations through the sow’s body to monitor these vital signs. [11] MariaJorquera-Chavez,SigfredoFuentes,FrankRDunshea,RobynDWarner,
TomasPoblete,RebeccaSMorrison,andEllenCJongman.2020.Remotelysensed
ThemainchallengeindevelopingPigV2 isthemixtureofvital-
imageryforearlydetectionofrespiratorydiseaseinpigs:apilotstudy.Animals
relatedandnon-vital-relatedinformationinthevibrationsignals. 10,3(2020),451.
Toovercomethischallenge,wereducetheinfluenceofnon-vital- [12] AsyaMacon,SudhenduSharma,EricMarkvicka,GaryRohrer,andJeremyMiles.
2021.CharacterizingLactatingSowPostureinFarrowingCratesUtilizingAuto-
relatedinformationbyfirstdetectingandcharacterizingvarious
matedImageCaptureandWearableSensors.634–642.
pigbehaviorsandtheninterpolatingthevitalratesduringthese [13] JeremyNMarchant,XantheWhittaker,andDonaldMBroom.2001.Vocalisations
periodsamongmultiplesensors.PigV2isevaluatedthroughareal- oftheadultfemaledomesticpigduringastandardhumanapproachtestand
theirrelationshipswithbehaviouralandheartratemeasures.AppliedAnimal
worldexperimentwith30pigs,with3.4%and8.3%averageerrorin BehaviourScience72,1(2001),23–39.
monitoringtheirHRandRR,respectively. [14] R.M.Marchant-Forde,D.J.Marlin,andJ.N.Marchant-Forde.2004. Validation
ofacardiacmonitorformeasuringheartratevariabilityinadultfemalepigs:
accuracy,artefactsandediting.PhysiologyandBehavior80,4(2004),449–458.
ACKNOWLEDGMENTS https://doi.org/10.1016/j.physbeh.2003.09.007
[15] MostafaMirshekari,ShijiaPan,JonathonFagert,EveMSchooler,PeiZhang,and
ThisresearchwassupportedinpartbytheNationalScienceFoun-
HaeYoungNoh.2018.Occupantlocalizationusingfootstep-inducedstructural
dation(NSF-CMMI-2026699)andCisco,Inc.TheUSDAprohibits vibration.MechanicalSystemsandSignalProcessing112(2018),77–97.
discrimination in all its programs and activities on the basis of [16] GC Randall. 1990. Induction of parturition in pigs: short term effects of
prostaglandinF2alphaonchronicallycatheterisedfetusesatterm. TheVet-
race,color,nationalorigin,age,disability,andwhereapplicable, erinaryRecord126,3(1990),61–63.
sex,maritalstatus,familialstatus,parentalstatus,religion,sex- [17] WSipos,SWiener,FEntenfellner,SSipos,etal.2013. Physiologicalchanges
ofrectaltemperature,pulserateandrespiratoryrateofpigsatdifferentages
ualorientation,geneticinformation,politicalbeliefs,reprisal,or
includingthecriticalperipartalperiod.Vet.Med.Austria100,3(2013),96.
becauseallorpartofanindividual’sincomeisderivedfromany [18] ThomasCSmith.1956.Therespirationandcompositionofthemammarygland
publicassistanceprogram(Notallprohibitedbasesapplytoall oftheguineapigduringpregnancyandlactation.ArchivesofBiochemistryand
programs.).Personswithdisabilitieswhorequirealternativemeans
Biophysics60,2(1956),485–495.
[19] EberhardvonBorell,JanLangbein,GérardDesprés,SvenHansen,Christine
forcommunicationofprograminformation(Braille,largeprint, Leterrier,JeremyMarchant-Forde,RuthMarchant-Forde,MichelaMinero,Elmar
audiotape,etc.)shouldcontactUSDA’sTARGETCenterat(202) Mohr,ArmellePrunier,DorothéeValance,andIsabelleVeissier.2007.Heartrate
variabilityasameasureofautonomicregulationofcardiacactivityforassessing
720-2600(voiceandTDD).USDAisanequalopportunityemployer. stressandwelfareinfarmanimals—Areview. PhysiologyandBehavior92,
3(2007),293–316. https://doi.org/10.1016/j.physbeh.2007.01.007 Stressand
WelfareinFarmAnimals.
REFERENCES
[20] MeiqingWang,AliYoussef,MonaLarsen,Jean-LoupRault,DanielBerckmans,
[1] Carina Barbosa Pereira, Henriette Dohmeier, Janosch Kunczik, Nadine JeremyNMarchant-Forde,JoergHartung,AndréBleich,MingzhouLu,and
Hochhausen,RenéTolba,andMichaelCzaplik.2019. Contactlessmonitoring TomasNorton.2021.Contactlessvideo-basedheartratemonitoringofaresting
ofheartandrespiratoryrateinanesthetizedpigsusinginfraredthermography. andananesthetizedpig.Animals11,2(2021),442.
Plosone14,11(2019),e0224747. [21] HalinaMZaleskiandRogerRHacker.1993.Variablesrelatedtotheprogress
[2] AmelieBonde,JesseRCodling,KanitthaNaruethep,YiwenDong,Wachirawich ofparturitionandprobabilityofstillbirthinswine. TheCanadianVeterinary
Siripaktanakon,SripongAriyadech,AkkaritSangpetch,OrathaiSangpetch,Shijia Journal34,2(1993),109.
Pan,HaeYoungNoh,etal.2021.PigNet:Failure-TolerantPigActivityMonitor- [22] Danguole˙ŽEmaityte˙,GiedriusVaroneckas,andEugeneSokolov.1984. Heart
ingSystemUsingStructuralVibration.InProceedingsofthe20thInternational rhythmcontrolduringsleep.Psychophysiology21,3(1984),279–289.
ConferenceonInformationProcessinginSensorNetworks(co-locatedwithCPS-IoT
Week2021).328–340.
[3] CBorst,WWieling,JFVanBrederode,AHond,LGDeRijk,andAJDunning.
1982.Mechanismsofinitialheartrateresponsetoposturalchange.American
JournalofPhysiology-HeartandCirculatoryPhysiology243,5(1982),H676–H681.
[4] JohnCarr,Shih-PingChen,JosephFConnor,RoyKirkwood,andJoaquimSegalés.
2018.Pighealth.CRCPress.
[5] JesseRCodling,AmelieBonde,YiwenDong,SiyiCao,AkkaritSangpetch,Orathai
Sangpetch,HaeYoungNoh,andPeiZhang.2021.MassHog:Weight-Sensitive
OccupantMonitoringforPigPensusingActuatedStructuralVibrations.InAd-
junctProceedingsofthe2021ACMInternationalJointConferenceonPervasiveand
UbiquitousComputingandProceedingsofthe2021ACMInternationalSymposium
onWearableComputers.600–605.