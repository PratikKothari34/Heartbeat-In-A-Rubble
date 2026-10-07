LongShoT: Long-Range Synchronization of Time
CeferinoGabrielRamirez AntonSergeyev
CarnegieMellonUniversity,SiliconValley CarnegieMellonUniversity,SiliconValley
MoffettField,CA MoffettField,CA
cef.ramirez@sv.cmu.edu anton.sergeyev@sv.cmu.edu
AssyaDyussenova BobIannucci
CarnegieMellonUniversity,SiliconValley CarnegieMellonUniversity,SiliconValley
MoffettField,CA MoffettField,CA
assya.dyussenova@sv.cmu.edu bob@sv.cmu.edu
ABSTRACT QC,Canada.ACM,NewYork,NY,USA,12pages.https://doi.org/10.1145/
Low-PowerWideAreaNetworks,suchasLoRaWAN,arerapidly 3302506.3310408
gainingpopularityinthefieldofwirelesssensingandactuation.
WhileLoRaWANisheavilystudiedinapplicationsandperformance,
1 INTRODUCTION
theconceptoftimehasrarelybeencharacterizedinsuchnetworks.
Low-PowerWideAreaNetworks(LPWANs),suchasLoRaWAN[15],
Manyapplicationswillrequiresynchronizedlocalclockswithvary-
arerapidlygainingpopularityinthefieldofwirelesssensingand
inglevelsofprecisioninordertomaintainconsistencyandcoordi-
actuation[2,20].Theirlong-range,low-powerpropertiesmakes
nationinthenetwork.Traditionaltimesynchronizationprotocols
themanenticingoptionforSmartCityapplications[10].
however do not fit LoRaWAN’s delay-inherent, low duty cycle,
LoRaWANisoneofthemostoftencitedLPWANs.Itsopenar-
networkmodelandwide-areadeploymenttopology.Meanwhile,
chitectureandconsumerhardwaremakesiteasilyaccessibleforde-
relyingonGPSfortimeisnotanoptionforlow-powerapplications.
ploymentandapplicationstudies.Whileseveralstudieshavelooked
In this paper, we present LongShoT, a time synchronization
intoLoRaWANintermsofapplicability[22,27]andperformance[1,
schemebuiltonLoRaWANcapableofsynchronizingdeviceclocks
towithin10μsofareferenceclockwithasinglenetworkrequest. 4,19,35],weconcernourselveswithanimportantaspectofdis-
tributedsystems—theconceptofTime.
This is achieved by utilizing the deterministic properties of Lo-
Aswithtraditionalsensornetworks,acommonnotionoftime
RaWANnetworksalongwithhardware-andMAC-leveltimestamp-
isimportanttoanysensingandactuatorsystemtomaintaindata
ingofpackets.LongShoTwasimplementedonconsumeroff-the-
consistencyandcoordinationofdevicesthroughoutthedistributed
shelfhardwareandevaluatedoverphysicallydistributeddevices
system[32]. The level of time accuracy and precision varies by
usingGPS1PPSasareference.OurresultsshowthatLongShoT
achievesanaveragesynchronizationerroroflessthan2μsandcom- applicationrequirements,whereasatrafficsignalingsystemmay
pensatesoscillatordrifttolessthan0.1ppmwithdevicesdistributed requireonlysecond-levelaccuracy,whilealocalizationandtracking
within4kmofagateway. systemwillrequiremicrosecond-levelaccuracy[31,33].
ExistingtimesynchronizationprotocolsdonotscalewelltoLo-
CCSCONCEPTS RaWAN,wherestringentbandwidthandbatteryconstraintslimit
therateatwhichdevicescansynchronizeforaccuratetime.Tradi-
•Networks→Timesynchronizationprotocols;•Computer
tionalwirelesssensornetwork(WSN)synchronizationapproaches
systemsorganization→Sensornetworks.
[6,9,18,24]arenotapplicableduetothedifferenceinnetwork
topology(starvs.mesh)andthepreferencefordevicestobeshut-off
KEYWORDS
mostofthetime.LoRaWANdevicescanneitherparticipateinLAN
TimeSynchronization,LoRaWAN,Low-PowerNetworking andWANbasedmethods[5,21]toacquiretime.Arecentupdate
ACMReferenceFormat: totheLoRaWANspecification[16]includesaDeviceTimeRequest
CeferinoGabrielRamirez,AntonSergeyev,AssyaDyussenova,andBob commandwhichdefinesthatthenetworkshouldprovidetimeto
Iannucci.2019.LongShoT:Long-RangeSynchronizationofTime.InThe
adevicewithanaccuracyof±100ms.Thespecification,however,
18thInternationalConferenceonInformationProcessinginSensorNetworks doesnotprovideanyimplementationdetailsorstrategiesonhow
(co-locatedwithCPS-IoTWeek2019)(IPSN’19),April16–18,2019,Montreal, tomaintainsynchronicityofdevices.
Otheroptionsacquiretimethroughambientsignals,suchas
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalor
GPS. This is especially applicable to systems distributed over a
classroomuseisgrantedwithoutfeeprovidedthatcopiesarenotmadeordistributed
forprofitorcommercialadvantageandthatcopiesbearthisnoticeandthefullcitation wide geographical area. These approaches, however, do not fit
onthefirstpage.CopyrightsforcomponentsofthisworkownedbyothersthanACM theconstrainedenergyrequirementsandwillquicklydrainthe
mustbehonored.Abstractingwithcreditispermitted.Tocopyotherwise,orrepublish,
batteriesofsuchdevices.
topostonserversortoredistributetolists,requirespriorspecificpermissionand/ora
fee.Requestpermissionsfrompermissions@acm.org. ThereexistsaneedforatimesynchronizationprotocolforLo-
IPSN’19,April16–18,2019,Montreal,QC,Canada RaWANthatdistributesprecisetimeoverthenetworkwhilemain-
©2019AssociationforComputingMachinery.
tainingitslow-powerproperties.Suchaprotocolmustaddressthe
ACMISBN978-1-4503-6284-9/19/04...$15.00
https://doi.org/10.1145/3302506.3310408 followingchallenges:
289

| IPSN’19,April16–18,2019,Montreal,QC,Canada |     |     |     |     | C.Ramirezetal. |     |
| ------------------------------------------ | --- | --- | --- | --- | -------------- | --- |
• Delay-InherentNetwork-Lowdataratesinthephysical LongShoT is designed to operate for Class A devices, the most
| layerandnetworkprotocolamountstoconsiderable,but |     |     | energyconstrainedclass. |     |     |     |
| ------------------------------------------------ | --- | --- | ----------------------- | --- | --- | --- |
deterministic,delaysinnetworktransactionssuchthatos- ClassAdevicesconserveenergybybeingofflinemostofthetime.
cillatordriftbecomesavisiblefactorinsynchronizingtime. Anend-devicecannotreceiveamessageunlessithastransmitted
Theprotocolmustbeabletocompensateforoscillatordrift anuplinkpacket.Aftertransmission,theend-deviceopenstwo
overthepresumeddelayperiod. possiblereceivewindows.Thefirstreceivewindowisanetwork
| •   |     |     | parameterdefinedasRxDelayandbydefaultissettoonesecond. |     |     |     |
| --- | --- | --- | ------------------------------------------------------ | --- | --- | --- |
SubstantialPropagationDelay-AttherangesthatLoRa
supports, wireless propagation delay also begins to be a Thesecondreceivewindowisopened1secondafterthefirst,ifno
factor.Approximately,a1μsoffsetisaddedforevery300m
messageisreceivedinthefirstwindow.
ofdistance.Withoutknowingthepreciselocationsofthe LoRaWANalsodefinesaDeviceTimeRequest commandthatis
gatewayanddevice,theprotocolmustbeabletoaccount compatiblewithClassAdevices.Thiscommandrequiresthenet-
forpropagationdelay. worktorespondwithtimeaccurateto±100ms.LongShoTdoes
notrelyonthiscommandandprovides±10μsaccuratetime,along
| In this paper, | we present LongShoT, | a time synchronization |     |     |     |     |
| -------------- | -------------------- | ---------------------- | --- | --- | --- | --- |
withstrategiestocompensatefordrift.
schemebuiltonLoRaWANcapableofsynchronizingtimetowithin
10μs
ofareferencewithoneLoRaWANtransactionatlowduty
2.2 Two-WayTimeTransferandDrift
cycles.WeimplementLongShoToncommercial-off-the-shelfhard-
wareandevaluatewithasetofdevicesdistributedwithina4km Thetwo-waytimetransfermodelisthebasisofmanytimesynchro-
radiusofaLoRaWANgateway.OurresultsshowthatLongShoT nizationschemes[5,11,21].Itholdsanadvantageoverone-way
maintainsanaveragesynchronizationerroroflessthan2μs,mea- modelstoaccountforpropagationdelaybetweentwodevices.Itis
alsocompatiblewithLoRaWANClassAdeviceprotocolsinwhich
suredovertwohourswithasinglesynchronizationtransaction
everyfiveminutes.Thekeycontributionsofthispaperare: asynchronizationrequestisend-deviceinitiated.Figure1showsa
diagramofthetwo-waymodelannotatedwithLoRaWANparame-
• anin-depthtiminganalysisofLoRaWANClassAdevicesto
ters.
implementasub-10μsaccuratetimesynchronizationproto-
| colwhilepreservinglow-powerrequirements;         |     |     |                                                                 | (cid:10) | (cid:10) |     |
| ------------------------------------------------ | --- | --- | --------------------------------------------------------------- | -------- | -------- | --- |
| •                                                |     |     |                                                                 | (cid:12) | (cid:13) |     |
| anevaluationofLongShoTimplementedonoff-the-shelf |     |     | (cid:2)(cid:4)(cid:5)(cid:4)(cid:9)(cid:4)(cid:8)(cid:3)(cid:4) |          |          |     |
hardwareandcomparingtheaccuracyagainstGPStimeata
distanceofupto4km; (cid:2)(cid:11)(cid:1)(cid:5)(cid:6)(cid:4)(cid:12)
|     |     |     |     | (cid:3) | (cid:3) |     |
| --- | --- | --- | --- | ------- | ------- | --- |
• anenergycomparisonbetweenLongShoTandaGPSreceiver (cid:8)(cid:9)(cid:7)(cid:8) (cid:8)(cid:9)(cid:7)(cid:8)
asameansforwide-areatimesynchronization.
(cid:1)(cid:7)(cid:6)(cid:4)(cid:8)(cid:10)
Theremainderofthispaperisasfollows.Section2provides (cid:10) (cid:10)
|     |     |     |     | (cid:11) | (cid:14) |     |
| --- | --- | --- | --- | -------- | -------- | --- |
atiminganalysisofLoRaWANandtheunderlyinghardwareto
determinethephysicallimitsthatboundsynchronizationaccuracy. (cid:3)
(cid:9)(cid:10)(cid:10)
Section3describestheprotocolandtheapproachestoovercomethe
varioussourcesoferror.Section4containstheexperimentsetup
andresultsgatheredfromourevaluationofLongShoT.Section5 Figure1:Two-waytimetransfermodel
presentsanenergycomparisonofsynchronizingtimeusingLong-
|     |     |     | Thetimestampst | ,t ,t 2andt |     |     |
| --- | --- | --- | -------------- | ----------- | --- | --- |
ShoTandaconsumergradeGPSreceiverasameansforwide-area 0 1 3markthepacketsendandreceive
timesynchronization.Section6offersareviewofrelatedworkon timesbasedonthelocalclocksofaClientandReferencetimeserver.
timesynchronizationandtheircomparisonwithLongShoT.Finally, Atagiventime,thelocalclockofaclientdeviceisoffsetfromthe
thepapersummarizesourcontributionsinSection7. referenceclockbysomevalueofθ.
|     |     |     |     | t =t      | +θ     | (1) |
| --- | --- | --- | --- | --------- | ------ | --- |
|     |     |     |     | Reference | Client |     |
2 TIMINGINLORAWAN
Usingthesendandreceivetimestamps,wecancalculatetheclock
LoRaWANisarelativelynewprotocolanditstimingaspectsare
offsetforuplinkanddownlinkpackets,whiletakingintoaccount
leastunderstood.ThissectiongivesabriefoverviewofLoRaWAN thepropagationdelay,T
prop.
protocolsforlow-powerdevices.Wepresentthechallengesthat
|     |     |     |     | t =t +θ    | +T   |     |
| --- | --- | --- | --- | ---------- | ---- | --- |
|     |     |     |     | 1 0 uplink | prop | (2) |
LongShoTfacesindeterminingthelocalclockoffsetalongwith
|     |     |     |     | t =t +θ | −T  |     |
| --- | --- | --- | --- | ------- | --- | --- |
compensatingforbothoscillatordriftandpropagationdelay.Fur- 2 3 downlink prop (3)
thermore,weinvestigateanddiscusstiminguncertaintiesrelatedto
where
thewirelesstransmissionandpresentastrategytomitigatethese
|                     |     |     |                  | θ +T                 | =t −t            |     |
| ------------------- | --- | --- | ---------------- | -------------------- | ---------------- | --- |
| effects.            |     |     |                  | uplink prop          | 1 0              | (4) |
|                     |     |     |                  | θ −T                 | =t −t            |     |
|                     |     |     |                  | downlink prop        | 2 3              | (5) |
| 2.1 LoRaWANProtocol |     |     |                  |                      | thatθ            |     |
|                     |     |     | In the classical | model, it is assumed | remains constant |     |
LoRaWANusesastarofstarstopologywhereend-devicescom- overthetime-transferperiod.Thisapproach,however,cannotbe
municatedirectlywithagateway.Itspecifiesthreeclassesforend- directlyappliedtoLoRaWANdueto(a)theroundtriptime(T rtt)of
devices[16].Eachclassistargetedatdifferentenergyrequirements. arequest,intheorderofseconds;and(b)thelocaloscillatordrift,α,
290

LongShoT:Long-RangeSynchronizationofTime IPSN’19,April16–18,2019,Montreal,QC,Canada
whichforinexpensivesensorscanbeintheordersof10−100ppm, ThegatewayradiotypicallycontainsanSX1301[30]whichis
suchthat capableofdecodingupto8simultaneousLoRapackets.TheSX1301
containsa32-bithardwarecounterwitharesolutionof1μs,which
θ downlink =θ uplink +α·T rtt (6)
canalsobeslavedtoanexternalGPS1PPSsignal.Thisunique
T rtt =T RxDelay +2·T prop (7) addition allows the gateway to timestamp incoming packets in
AnRxDelayof1sissignificantenoughtointroduceupto5μs theradiohardwareortoinitiatesendingonascheduledtime—
errorwitha5ppmcrystal. removingallvariabledelaysfromOSsystemcallsonthegateway
side.
Thechallengeisfurthercompoundedbysubstantialpropagation
delaysin thewirelessrange ofLoRaWAN.A distanceof1.5km
betweenanend-deviceandgatewayaddsa5μsoffsetbetweenthe 2.3.3 SourcesofDelay. TodeterminetheboundofLongShoT’s
accuracy,wedecomposeanddescribethesourcesofthedelayfound
localclocks.Havingdrifterrorandpropagationdelayinthesame
inLoRaWANanddiscusshowtheycanbemitigated.
orderofmagnitudepreventsusfromcompensatingforoneeffect
SendTimeandReceiveTime—Thesedelaysareincurreddue
withoutindependentlymeasuringtheother.LongShoTpresentsa
tovariabilityinsoftwareandprocessorloadwhenanapplication
methodtoaccountforbothdriftandpropagationdelaywithtwo
initiatesatransmissioncycle.End-devicescanmitigatethesedelays
consecutivesynchronizationrequests.
byperformingtimelabelingattheboundarybetweentheMAC
2.3 TimingUncertainties andtheradio,usuallyonaninterruptsignal.Onthegateway,these
delaysaredeterministicduetotheradiohardware,whichperforms
Thesourcesoferrorintimesynchronizationprotocolsaremainly
internaltimestampingonRxandsupportsscheduledTxbasedona
determinedbythevariabilityofdelaysinmeasuringtimeandsend- 1μshardwarecounter.
ingthemoverthenetwork.Thesedelayshavebeendecomposed
AccessTime—Adelayusedtoaccessthewirelesschannelon
extensivelyinliterature[9,18].Weofferaviewofhowthesevalues
transmitandminimizecollisions.SinceLoRaWANisanALOHA-
arepresentinLoRaWANandiftheycanbemitigated.
basedprotocol,thisisnegligible.Furthermore,LoRaradiosprovide
2.3.1 LoRaPHYLimitations. TheLoRaPHYlayerusesaChirp aninterruptafteratransmissioniscompleted.Capturingtimeon
SpreadSpectrum(CSS)modulationschemewithanarrowband- thissignalismoredeterministic.Gatewayscanignorethistime
widthofeither125,250or500kHz.Inthisscheme,eachsymbolis sincetheyimplementscheduledtransmissionstorespectprotocol
encodedusingasequenceofchipsonalinearlysweptfrequency, definitions.
orchirps. TransmissionandReceptionTime—Thetimeittakestoemitor
Thelengthofeachchipisderivedfromthebandwidthofthe receiveanentirepacketinthewirelesschannel,alsoknownas
signal,whichdefinesthechippingrate.A125kHzbandwidthcor- TimeOnAir(ToA).Thistimecanvaryfromtenstoafewhundred
respondsto125kilo-chips-per-second(kcps)[28],or8μsperchip. milliseconds,butcanbecalculatedbythelengthoftheframeand
Whenasignalistransmittedovertheair,noiseandothereffects, theselectedradiodatarate.[29]
suchasmulti-path,mayblurtheboundariesbetweeneachchip, PropagationTime—Thetimeittakesforawirelesssignalto
thereforecausingamisalignmentduringdemodulation.Insuch travelthedistancebetweensenderandreceiver.Thisisdeterminis-
cases,aframemisalignmentofmorethanthechiplengthwillcause ticfornon-movingdevices,butcanbeintheorderofafewtotens
ademodulationfailureandultimatelydroptheframe.Assuch,a
ofmicrosecondsfordevicesplacedbeyond300mfromagateway.
demodulatedframemayhaveamaximumtimestamperrorupto InterruptHandlingTime—Thistimeisdependentonthebehav-
thechiplengthinlowSNRscenarios. iorofthehostmicrocontrolleronend-devices.Theseareusually
SimilarprotocolsthatuseCSSmodulation,suchas802.15.4a, lessthanafewmicrosecondsbutcanvaryduetothenumberofin-
havebeenstudiedtoprovidetimeofarrivalmeasurementsdown terruptsbeinghandledbytheprocessor.Interruptroutinesmustbe
totheorderofafewnanosecondsprovidedgoodSNR[3].Given carefullydesignedtominimizethiseffectandensurehigh-accuracy
acceptableSNR,wecanexpectthesameaccuracyinarrivaltime oftimelabeling.
estimationusingLoRa.AsSNRlowers,thedelayuncertaintyrises Radio State Delays — These delays are attributed to different
towardstheupperboundasdefinedbybandwidthlimitations. stagesahardwareradiomovesthroughtoperformspecificfunc-
WithconsumerLoRaradiohardware, we cannotinspectthe tions.Typicaldelaysareencoding/decodingtimeandfrequency
approachestakeninternallytomarkthearrivalofapacket.As synthesis.Whilethesedelaysarefromdeterministicstatemachines,
such,wetreattheradiosubsystemasablackboxthatiscapableof theydilutetheprecisionoftimeifnotaccountedfor.Wedescribe
markinganincomingpackettowithinafewnanosecondsgiven these delays in further detail and how they are handled in the
goodsignalconditions,butmayexhibitworst-caseerrorsofupto followingsection.
8μsfor125kHztransmissionswithlowSNRs.
2.3.2 LoRaWANHardware. InLoRaWAN,theradiohardwareof 2.4 PreciseTimeLabeling
anend-deviceisdifferentfromthegatewayradio.Theend-deviceis Timesynchronizationaccuracydependsonhowwellwecanlabel
typicallyanSX1272/76[29]whichiscapableofhalf-duplexcommu- specificpointsintime,e.g.thetimeapacketwassentorreceived.
nication.Theend-deviceradiodoesnotcontainahardwarecounter Thesespecificpointsintime,however,areembeddedinhardware
andreliesonaninterruptlinetosignalthehostmicrocontroller functionsthatpreventusfrompreciselymeasuringthosemoments
whenatransactioniscompleted. —unlessproperlysupportedbythehardwarethemselves.Suchis
291

| IPSN’19,April16–18,2019,Montreal,QC,Canada |     |     |     |     |     |     |     |     |     | C.Ramirezetal. |     |     |
| ------------------------------------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------------- | --- | --- |
1
1
|     | egatloV dezilamroN 0.8 |     |     |     |     | egatloV dezilamroN |     |     |     | Rx Signal  |     |     |
| --- | ---------------------- | --- | --- | --- | --- | ------------------ | --- | --- | --- | ---------- | --- | --- |
|     |                        |     |     |     |     | 0.8                |     |     |     | Power In   |     |     |
|     | 0.6                    |     |     |     |     |                    |     |     |     | RxDone IRQ |     |     |
0.6
t=1.48ms
|     | 0.4 |     |       |     | Tx Signal  |     |     |     |       |     |     |     |
| --- | --- | --- | ----- | --- | ---------- | --- | --- | --- | ----- | --- | --- | --- |
|     |     |     |       |     | Power In   | 0.4 |     |     |       |     |     |     |
|     | 0.2 |     |       |     | TxDone IRQ |     |     |     |       |     |     |     |
|     |     |     |       |     | t=43.6 s   | 0.2 |     |     |       |     |     |     |
|     | 0   |     |       |     |            | 0   |     |     |       |     |     |     |
|     | 0   | 20  | 40 60 |     | 80 100     | 0   | 0.5 | 1   | 1.5 2 | 2.5 |     | 3   |
Time (ms)
Time ( s)
|     |     | (a)TxDoneSignalTiming |     |     |     |     |     | (b)RxDoneSignalTiming |     |     |     |     |
| --- | --- | --------------------- | --- | --- | --- | --- | --- | --------------------- | --- | --- | --- | --- |
Figure 2: Timing measurements of SX1276 Tx/RxDone interrupts. In (a), the interrupt line is raised after the radio ramps
downthepoweramplifier.Thisvalueisconfiguredinregistersandissetto40μs
bydefault.Inourmeasurements,weseean
additional3.6μs fromthetimethepowerdrawstartstofall.Therampdowntimeisindependentofdatarate,packetlength
andtransmitpower.In(b),theinterruptlineisraised1.48msafterreceivingthelastsymbol(t <0.5ms).Thisismostlikelydue
toprocessinganddecoding,whichissupportedbytheslightincreaseinpowerdrawduringthatinterval.Thedecodingtime
variesdependingonthedatarateusedfordownlink.
thecaseforRadioStateDelayswhichenvelopthepreciseevent DownlinkDataRate DecodeTime(μs)
| timeofourpackets. |     |     |     |     |     |     | DR10/SF10 |     |     | 1487±1 |     |     |
| ----------------- | --- | --- | --- | --- | --- | --- | --------- | --- | --- | ------ | --- | --- |
717±1
We define a Precise Time Labeling scheme for LongShoT to DR11/SF9
339±1
clearlyspecifythepacketeventtimesthatneedtobecaptured. DR12/SF8
ThisispresentedinFigure3.LongShoTusesthetimeofthelastbit DR13/SF7 176±1
toenter/exittheradioasthereferencepointfordeterminingthe
|     |     |     |     |     |     | Table 1: Measured |     | decoding | time of | a 8-byte | payload | Lo- |
| --- | --- | --- | --- | --- | --- | ----------------- | --- | -------- | ------- | -------- | ------- | --- |
precisetimelabel.Furthermore,wegointodetailonhoweachof
RaWANdownlinkpacketatdifferentdatarates.
thetimelabelswillbemeasuredbasedonobservablesignals.
43±3μsdelay,mostlikelyduetoadditionalstatetransitionsofthe
radio.
|     | (cid:6)(cid:10)(cid:12)(cid:15)(cid:18) | (cid:7)(cid:22)(cid:10)(cid:20)(cid:22) | (cid:8)(cid:15)(cid:16)(cid:13)(cid:1)(cid:18)(cid:17)(cid:1)(cid:2)(cid:15)(cid:20) | (cid:4)(cid:15)(cid:17)(cid:15)(cid:21)(cid:14) |     |                          |     |     |                          |     |     |     |
| --- | --------------------------------------- | --------------------------------------- | ------------------------------------------------------------------------------------ | ----------------------------------------------- | --- | ------------------------ | --- | --- | ------------------------ | --- | --- | --- |
|     |                                         |                                         |                                                                                      |                                                 |     | ForDownlinkReceiveTime,t |     |     | 3,weseeanevenhigherdelay |     |     |     |
betweentheRxDoneinterruptandthelastsymbolobservableon
(cid:3)(cid:5)(cid:9)
(cid:22) (cid:22) (cid:22) theRFinputline.Thisislikelyduetoprocessinganddecoding
|     |     | (cid:19)(cid:20)(cid:13) | (cid:1) (cid:19)(cid:20)(cid:13)(cid:11)(cid:15)(cid:21)(cid:13) | (cid:1) | (cid:19)(cid:18)(cid:21)(cid:22) |     |     |     |     |     |     |     |
| --- | --- | ------------------------ | ---------------------------------------------------------------- | ------- | -------------------------------- | --- | --- | --- | --- | --- | --- | --- |
ofthereceivedsignal,asindicatedbytheriseinpoweroverthat
Figure 3: Determining a precise time label. Without hard- periodoftime.Thedecodingtimeisdependentonthedatarate
usedfordownlink.Table1showsourmeasureddecodingtimesfor
| ware             | timestamp | support, | we can only                     | measure | a packet |                     |     |     |     |     |     |     |
| ---------------- | --------- | -------- | ------------------------------- | ------- | -------- | ------------------- | --- | --- | --- | --- | --- | --- |
| eventfromeithert |           |          | ort                             |         |          | differentdatarates. |     |     |     |     |     |     |
|                  |           | pre      | post afteranotificationfromara- |         |          |                     |     |     |     |     |     |     |
dio.Ifwecanmeasureprecisetimingbehaviorofthehard- 2.4.2 GatewayTimeLabels.
Gatewaytimelabelsareexpectedto
| ware,wecandeterminet |     |     | precise byapplyingthatknowledge |     |     |     |     |     |     |     |     |     |
| -------------------- | --- | --- | ------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
bemoreaccurateduetotheuseofaninternalhardwarecounter
toeventtimemeasuredbydevices.
fortimestampingandscheduleddownlinktransmissions.Conse-
|     |     |     |     |     |     | quently, without |     | access to timing | signals | externally, | we  | cannot |
| --- | --- | --- | --- | --- | --- | ---------------- | --- | ---------------- | ------- | ----------- | --- | ------ |
reliablymeasuretheaccuracyofthesemechanisms.
2.4.1 End-DeviceTimeLabels.
Forend-devices,werelyoninter- According to the SX1301 datasheet [30], receive packets are
timestampedwitha±1μsaccuracy.Wecannothoweverdetermine
ruptsignalsfromaLoRaradiotoindicatetheendofTxandRx.
Welabeltheseeventsast tx_done andt rx_done,respectively.These, whetherthisreportedtimestampincludesanyprocessingdelays.It
however, do not indicate the exact moment a packet is sent or hasbeenreportedby[26]thatagatewaycantimestamppackets
receivedbytheradio. withanaccuracyof±3μs.Wetakethereportedtimestampasis
Wedeterminethetimingbehaviorsoftheradiobycomparing andassumethatitaccuratelyrepresentsexactreceivetimeofthe
incomingpacket,t
| theTx/RxRFlines,powerinputlineandinterruptlinewithan |     |     |     |     |     |     |     | 1.  |     |     |     |     |
| ---------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
oscilloscope.ThesecanbeseeninFigure2. Formeasuringscheduleddownlinktransmissionaccuracy,we
ForUplinkSendTime,t 0,weseeasignificantdelaybetween relyonaclientradioRxDonesignal.Weplacetheclientradioto
theTxDoneinterruptandthedropinvoltageforbothpowerand continuouslywaitforadownlinkpacketandusingmodifiedgate-
RFlines.Accordingtothedatasheet[29],thisisattributabletothe waysoftware,weinjectknowndownlinkpacketstosendonthe
rampdownofthepoweramplifieraftertransmission.Theramp risingedgeofGPS1PPS.Bycomparingthe1PPSrisingedgeandthe
downtime,T ramp,isconfigurablethroughdeviceregisters,and RxDonerisingedge,wedeterminethelengthofacompletedown-
issetto40μs bydefault.However,ourmeasurementsindicatea linktransmission.Subtractingouttheairtimeofthepacket,the
292

LongShoT:Long-RangeSynchronizationofTime IPSN’19,April16–18,2019,Montreal,QC,Canada
knowndecodingtimeoftheclientradio,andnegligiblepropagation matterasitdoesnotaffectthecomputationoftime.Adevicesimply
delay,shouldresultintotheactualstarttimeoftransmission.Our needstoindicatetotheNetworkServerthatitisrequestingfortime.
measurementsshowaresidualtimeof6±1μsfromthetotaltime.
Assuch,arequestcanbemixedinwithanytelemetrypacketofa
Thisindicatesthatagatewayemitsthefirstsymbolontotheairat device.Aftertheradiosendsthepacketsuccessfully,theend-device
6μsafterthescheduledtime.WelabelthisdelayasT GwTxDelay. MCUcapturestime,t tx_done,fromtheTxDoneinterruptofthe
Byaddingthedownlinkpackettimeonairwiththistransmitdelay, radioandcomputest 0basedontheknownradiorampdowntime,
| wecancomputetheexpectedvaluefortimelabelt |     |     |     |     |     |     |     | T                  |     |     |     |     |     |     |
| ----------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ------------------ | --- | --- | --- | --- | --- | --- |
|                                           |     |     |     |     |     | 2.  |     | ramp,asconfigured. |     |     |     |     |     |     |
2 .4 . 3 Su m m a r y . t , t , t Onthegatewayside,thepacketisreceivedandthearrivaltime
W e d e fi ne h ow s t a n d a r d ti m e l a b el s , 0 1 2a n d t
|           |            |            |          |              |                    |             |             | i s t i m e s ta | m p e d in | th e ra d io | h a r d w a r | e . T h i s | t i m e s t a m p is | 1 . T h e |
| --------- | ---------- | ---------- | -------- | ------------ | ------------------ | ----------- | ----------- | ---------------- | ---------- | ------------ | ------------- | ----------- | -------------------- | --------- |
| t , a rem | e as u r e | d b as e d | o n th e | ob s e r v a | b le s i gn a l s. | T a b l e 2 | s u m m a - |                  |            |              |               |             |                      |           |
3 n e t w o r k s er v e r,u po n se e in g th a t t h e e n d - d e v i c e r e q u es ts fo r t im e ,
rizesthesedefinitions,whileTable3consolidatesthenetworkdelay
|                                                        |     |     |     |     |     |     |     | replieswiththevalueoft |     |     | astheresponse.t |     | isencodedasan |     |
| ------------------------------------------------------ | --- | --- | --- | --- | --- | --- | --- | ---------------------- | --- | --- | --------------- | --- | ------------- | --- |
| valuesforLoRaWAN.Consequently,thenetworkroundtriptime, |     |     |     |     |     |     |     |                        |     |     | 1               |     | 1             |     |
8-byteintegerdeclaringtimeinmicroseconds.
T
rtt canbecomputedusingEquation8. Theend-devicethenexpectsaresponsewithT
|     |     |     |     |     |     |     |     |     |     |     |     |     | RxDelay | seconds |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | ------- |
afteritsuplinkandopensareceivewindowtoacceptthedownlink
|     | T rtt | =T RxDelay |     | +T GwTxDelay | +T ToA |     |     |     |     |     |     |     |     |     |
| --- | ----- | ---------- | --- | ------------ | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
packet.Uponreceivingthepacket,theend-devicethenacquires
|     |     | +T  |     | −T  | +2·T |     | (8) |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
decode ramp prop t fromtheradiointerruptsignal.Withknowledgeofthe
rx_done
|     |           |     |     |            |     |     |     | datarateusedandnumberof  |     |     | bytesinthepacket,we  |     |     | canthen |
| --- | --------- | --- | --- | ---------- | --- | --- | --- | ------------------------ | --- | --- | -------------------- | --- | --- | ------- |
|     |           |     |     |            |     |     |     | computefordecodingtime,T |     |     | andpackettimeonair,T |     |     |         |
|     |           |     |     |            |     |     |     |                          |     |     | decode               |     |     | ToA,    |
|     | TimeLabel |     |     | Definition |     |     |     |                          | t   | t   |                      |     | t   | t       |
t t −T toa cq u ir e b o t h 2 a nd 3 b a s e d o n o u r kn o w l ed g e o f 1 a nd r x _d o n e .
|     | 0   |     |                     | tx_done | ramp    |        |     |                                                           |                    |            |                   |            |                 |             |
| --- | --- | --- | ------------------- | ------- | ------- | ------ | --- | --------------------------------------------------------- | ------------------ | ---------- | ----------------- | ---------- | --------------- | ----------- |
|     |     |     |                     |         |         |        |     | W it h a                                                  | v a i la b i li ty | o f a ll r | e q u i re d t im | e s ta m p | s , w e ca n th | e n c o m - |
|     | t   |     | asreportedbygateway |         |         |        |     |                                                           |                    |            |                   |            |                 |             |
|     | 1   |     |                     |         |         |        |     | puteforoffsetanddriftusingtheapproachesdescribedinthenext |                    |            |                   |            |                 |             |
|     | t   | t   | +T                  |         | +T      | +T ToA |     |                                                           |                    |            |                   |            |                 |             |
|     | 2   |     | 1 GwTxDelay         |         | RxDelay |        |     | sections.                                                 |                    |            |                   |            |                 |             |
|     | t   |     |                     | t       | −T      |        |     |                                                           |                    |            |                   |            |                 |             |
|     | 3   |     |                     | rx_done | decode  |        |     |                                                           |                    |            |                   |            |                 |             |
Table2:PreciseTimeLabelDefinitions 3.2 One-ShotSynchronization
One-shotsynchronizationusesasinglenetworkrequesttoadjust
|     | Measurement |     |     |     | Value |     |     |     |     |     |     |     |     |     |
| --- | ----------- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
localclocksandperformafirst-ordercompensationofdriftrate.
|     | T ramp |     | 43μs±3μs(Configurable) |     |     |     |     |     |     |     |     |     |     |     |
| --- | ------ | --- | ---------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Thisapproachisusefulforverylowdutycycleoperations,wherea
|     | T   |     |     | 6μs±1μs |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
GwTxDelay devicecommunicatesinfrequently,butmaybenefitfromaccurately
|     | T   |     |     | 1μsper300mofrange |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
prop compensateddriftrates.However,thisapproachdoesnotaccount
T
RxDelay Networkconfiguredparameter for propagation time and will introduce errors proportional to
|     | T ToA |     |     |     | See[29] |     |     |     |     |     |     |     |     |     |
| --- | ----- | --- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
distancefromthereferencegateway.
|     | T decode |     |     | SeeTable1 |     |     |     |              |                  |     |     |            |                  |     |
| --- | -------- | --- | --- | --------- | --- | --- | --- | ------------ | ---------------- | --- | --- | ---------- | ---------------- | --- |
|     |          |     |     |           |     |     |     | For one-shot | synchronization, |     | it  | is best to | use the downlink |     |
Table3:SummaryofNetworkDelaysValues timestampstocomputeone-wayoffset,
|     |     |     |     |     |     |     |     |     |     | θ OneShot | =t 2 | −t 3 |     | (9) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | ---- | ---- | --- | --- |
3 LONGSHOTPROTOCOL
|     |     |     |     |     |     |     |     | θ OneShot | isexpectedtorepresentthetimeoffsetbetweenend- |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | --------------------------------------------- | --- | --- | --- | --- | --- |
Intheprevioussection,wedescribedhowtheclassicaltwo-way deviceandgatewaymoreaccuratelythantheuplinktimemeasure-
timetransfermodelisinadequateforsynchronizingtimeinLo- mentsduetothepresenceofdrift.However,thisvalueincludes
RaWANdueto(a)theaccumulateddriftoverthenetworkround-
propagationdelayintheoffset.
triptimeand(b)theinabilitytodistinguishtheoffsetduetodrift Tocompensatefordrift,α,werelyonthepredictablenetwork
versusthatofpropagationdelay.Inthissection,wepresenthow roundtriptimeandcompareitagainstthedevicemeasuredtime
| LongShoTaddressesthesefactorstoprovidesynchronizationto |     |     |     |     |     |     |     | delay, |     |     |     |     |     |     |
| ------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | --- | --- | --- |
within10μs.
|                                                         |     |     |     |     |     |     |     |           |     | t   | −t =α·t | rtt |     | (10) |
| ------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | --- | ------- | --- | --- | ---- |
| Wefirstdescribethepackettransactionsmadebytheend-device |     |     |     |     |     |     |     |           |     | 3   | 0       |     |     |      |
| andthenetworkresponseinordertodeterminethenecessarytime |     |     |     |     |     |     |     | suchthat, |     |     |         |     |     |      |
t −t
measurements.Wethendescribetwosynchronizationapproaches: α = 3 0
|                                                          |     |     |     |     |     |     |     |     |     |     | T   |     |     | (11) |
| -------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- |
| One-ShotSynchronizationandTwo-StepCorrection.Bothprovide |     |     |     |     |     |     |     |     |     |     | rtt |     |     |      |
accuratetimeanddriftcorrectionbutaretargetedfordifferentuse Thisapproachhastwopotentialsourcesoferror:(a)thetick
casestocomplywithenergyanddutycyclerequirements.
resolutionofthedeviceclockinwhichitcanmeasurablycompare
theaccumulateddriftoverthespanoftimeand(b)thedifficulty
3.1 SynchronizationRequest
|     |     |     |     |     |     |     |     | of measuring | accumulated |     | drift against | other | delays of | similar |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | ----------- | --- | ------------- | ----- | --------- | ------- |
LongShoTbeginswithdeterminingtheprecisetimelabelstoesti- magnitude,suchaspropagationdelay.
mateoffsetanddrift.Figure4showsasingleLoRaWANtransmis- Toaddressthese,wetakeadvantageofLoRaWAN’sconfigurable
networkdelay,RxDelay.ByincreasingRxDelay,i.e.thetimebe-
sioncycleannotatedwiththeexpectedtimingdelaysthroughout
thenetwork. tween reception of an uplink packet and the transmission of a
Arequestisinitiatedbytheend-devicebysendinganuplink response,weallowthedrifttoaccumulateovertime,sothatitis
packettothenetworkserver.Thecontentsofthispacketdonot dominantlymeasurablecomparedtootherdelays.Weexpecterrors
293

| IPSN’19,April16–18,2019,Montreal,QC,Canada |     |     |     |     |     |     | C.Ramirezetal. |
| ------------------------------------------ | --- | --- | --- | --- | --- | --- | -------------- |
(cid:10)(cid:21)(cid:33)(cid:36)(cid:29)(cid:31)(cid:25)(cid:1)
(cid:13)(cid:21)(cid:31)(cid:35)(cid:21)(cid:31)
(cid:4)
|     |     |     |     | (cid:3)(cid:21)(cid:1)(cid:8)(cid:11)(cid:5)(cid:22) (cid:33) | (cid:32)(cid:21)(cid:28)(cid:20) (cid:49)(cid:33) (cid:43)(cid:1) (cid:48)(cid:4) (cid:3)(cid:21)(cid:1)(cid:8)(cid:11)(cid:5)(cid:22) (cid:48)(cid:4) | (cid:2)(cid:20)(cid:4)(cid:21)(cid:1)(cid:8)(cid:11)(cid:5)(cid:22) |     |
| --- | --- | --- | --- | ------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------- | --- |
(cid:6)(cid:11)(cid:13)(cid:1)(cid:12)(cid:21)(cid:22)(cid:21)(cid:31)(cid:21)(cid:28)(cid:19)(cid:21)
|     |     |     | (cid:33) |     |     | (cid:33) |     |
| --- | --- | --- | -------- | --- | --- | -------- | --- |
(cid:6)(cid:17)(cid:33)(cid:21)(cid:36)(cid:17)(cid:38)(cid:1) (cid:43) (cid:44)(cid:1)
(cid:9)(cid:3)(cid:15)
(cid:11)(cid:29)(cid:26)(cid:26)
(cid:31)(cid:21)(cid:19)(cid:21)(cid:24)(cid:35)(cid:21)(cid:20)(cid:1) (cid:7)(cid:28)(cid:32)(cid:21)(cid:31)(cid:33)(cid:1)
(cid:13)(cid:19)(cid:23)(cid:21)(cid:20)(cid:34)(cid:26)(cid:21)(cid:20)(cid:1)
|     |                                                  |     | (cid:30)(cid:17)(cid:19)(cid:25)(cid:21)(cid:33)(cid:32) |                                                  |     | (cid:14) (cid:14)(cid:29)(cid:2) |     |
| --- | ------------------------------------------------ | --- | -------------------------------------------------------- | ------------------------------------------------ | --- | -------------------------------- | --- |
|     | (cid:13)(cid:16)(cid:43)(cid:45)(cid:42)(cid:43) |     |                                                          | (cid:11)(cid:17)(cid:19)(cid:25)(cid:21)(cid:33) |     |                                  |     |
(cid:45)(cid:44)(cid:39)(cid:18)(cid:24)(cid:33)(cid:1)(cid:19)(cid:17)
(cid:6)(cid:11)(cid:13)(cid:1)(cid:43)(cid:11)(cid:11)(cid:13)
(cid:19)(cid:29)(cid:34)(cid:28)(cid:33)(cid:21)(cid:31) (cid:4) (cid:15)(cid:16)(cid:14)(cid:15) (cid:4) (cid:16)(cid:8)(cid:6)(cid:8)(cid:15)(cid:18)(cid:10)(cid:14)(cid:13)(cid:23)(cid:18)(cid:10)(cid:12)(cid:8) (cid:4) (cid:7)(cid:8)(cid:6)(cid:14)(cid:7)(cid:8) (cid:4) (cid:8)(cid:13)(cid:6)(cid:14)(cid:7)(cid:8) (cid:4) (cid:18)(cid:16)(cid:5)(cid:13)(cid:17)(cid:12)(cid:10)(cid:17)(cid:17)(cid:10)(cid:14)(cid:13)(cid:23)(cid:18)(cid:10)(cid:12)(cid:8) (cid:4) (cid:17)(cid:9)(cid:19)(cid:18)(cid:7)(cid:14)(cid:20)(cid:13)
|     |     |                                                                                                                                                                                     | (cid:8)(cid:17)(cid:32)(cid:33)(cid:1)                           |     |                                  | (cid:8)(cid:17)(cid:32)(cid:33)(cid:1)                                                                       |                                             |
| --- | --- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | --- | -------------------------------- | ------------------------------------------------------------------------------------------------------------ | ------------------------------------------- |
|     |     |                                                                                                                                                                                     | (cid:13)(cid:38)(cid:27)(cid:18)(cid:29)(cid:26)(cid:1)          |     |                                  | (cid:13)(cid:38)(cid:27)(cid:18)(cid:29)(cid:26)(cid:1)                                                      |                                             |
|     |     |                                                                                                                                                                                     | (cid:14)(cid:31)(cid:17)(cid:28)(cid:32)(cid:22)(cid:21)(cid:31) |     |                                  | (cid:14)(cid:31)(cid:17)(cid:28)(cid:32)(cid:22)(cid:21)(cid:31)                                             |                                             |
|     |     | (cid:4) (cid:4)                                                                                                                                                                     | (cid:4)                                                          |     | (cid:4)                          | (cid:4)                                                                                                      | (cid:4)                                     |
|     |     | (cid:8)(cid:13)(cid:6)(cid:14)(cid:7)(cid:8) (cid:18)(cid:16)(cid:5)(cid:13)(cid:17)(cid:12)(cid:10)(cid:17)(cid:17)(cid:10)(cid:14)(cid:13)(cid:23)(cid:18)(cid:10)(cid:12)(cid:8) | (cid:16)(cid:5)(cid:12)(cid:15)                                  |     | (cid:15)(cid:16)(cid:14)(cid:15) | (cid:16)(cid:8)(cid:6)(cid:8)(cid:15)(cid:18)(cid:10)(cid:14)(cid:13)(cid:23)(cid:18)(cid:10)(cid:12)(cid:8) | (cid:7)(cid:8)(cid:6)(cid:14)(cid:7)(cid:8) |
(cid:13)(cid:16)(cid:43)(cid:44)(cid:47)(cid:46)
(cid:5)(cid:28)(cid:20)(cid:39)(cid:4)(cid:21)(cid:35)(cid:24)(cid:19)(cid:21)(cid:1)
(cid:3)(cid:26)(cid:29)(cid:19)(cid:25)
(cid:4)(cid:21)(cid:35)(cid:24)(cid:19)(cid:21)(cid:1)
|     | (cid:9)(cid:3)(cid:15) |     | (cid:33) (cid:33)                                                 |     |     | (cid:33) | (cid:33)                                                 |
| --- | ---------------------- | --- | ----------------------------------------------------------------- | --- | --- | -------- | -------------------------------------------------------- |
|     |                        |     | (cid:42) (cid:33)(cid:37)(cid:40)(cid:20)(cid:29)(cid:28)(cid:21) |     |     | (cid:45) | (cid:31)(cid:37)(cid:40)(cid:20)(cid:29)(cid:28)(cid:21) |
Figure4:LoRaWANClassAtransmissioncycletimingdiagramannotatedwiththesourcesofdelayalongthenetworkpath.
witht
The process begins with an end-device initiating a Tx and timestamping the end of transmission tx_done based on a
hardwareinterruptsignal.Thepacketisreceivedbyagatewayandtimestamped(t )inradiohardwarewitha32-bit1μscounter.
1
The gateway host forwards the received packet to a LoRaWAN Network Server, which in turn responds with a scheduled
downlink packet to be sent att send = t +T RxDelay. The gateway host queues this packet into the radio. When the radio
1
hardware counter reachest send, it initiates the downlink transmission. Meanwhile, the end-device, knowing the expected
responsetime,receivesthepacketandtimestampstheendofreceptionwitht rx_done.Theprecisetimelabels(t ,t ,andt
|                                             |     |     |           |                                                 |     |     | 0 2 3)can |
| ------------------------------------------- | --- | --- | --------- | ----------------------------------------------- | --- | --- | --------- |
| thenbecalculatedfromthemeasuredtimestamps(t |     |     | ,t ,andt  |                                                 |     |     |           |
|                                             |     |     | 1 tx_done | rx_done)byapplyingknowndeterministicdelaysinthe |     |     |           |
networkpath.
tobeinverselyproportionaltoRxDelayresultingtohigherdrift (cid:1)
(cid:4)(cid:6)(cid:8)(cid:3)(cid:7)(cid:9)(cid:2)(cid:5)
compensationaccuracyasweincreaseRxDelay.
|     |     |     |     | (cid:1) | (cid:1) |     |     |
| --- | --- | --- | --- | ------- | ------- | --- | --- |
3.3 Two-StepCorrection (cid:2) (cid:2) (cid:2) (cid:1)(cid:7)(cid:4) (cid:2) (cid:1)(cid:7)(cid:4)
|     |     |     |     | (cid:4) | (cid:5) |     |     |
| --- | --- | --- | --- | ------- | ------- | --- | --- |
(cid:4) (cid:5)
TheTwo-StepCorrectionapproachusestwonetworkrequeststo
estimatedrift,accountforpropagationtimeanddeterminetheexact
clockoffsetcomparedtothereference.Thisapproachisappropriate (cid:2) (cid:1) (cid:2) (cid:1) (cid:2) (cid:1)(cid:7)(cid:4) (cid:2) (cid:1)(cid:7)(cid:4)
forapplicationsthatexpectconstantsynchronizationandmaintain (cid:3) (cid:6) (cid:3) (cid:6)
| accuracywithin | a certain bound. | While it requires | at least two |     |     |     |     |
| -------------- | ---------------- | ----------------- | ------------ | --- | --- | --- | --- |
networkrequests,thesetworequestscanbespacedaccordingto Figure5:Two-StepCorrectionModel
dutycyclelimitations.Thedeviceisfreetochooseanappropriate
intervalasneeded.Thelargertheintervalbetweenrequests,the
betterLongShoTcancorrectlong-termdrift.
| FollowingthemodelinFigure5,webeginbyperformingthe |     |     |     |     | ti+1−(ti |     |     |
| ------------------------------------------------- | --- | --- | --- | --- | -------- | --- | --- |
+θ i )
firstsynchronizationrequest.Fromthisrequest,wecanestimate α = 0 0 (13)
ti+1−ti
aninitialoffsetbyusingthetimemeasurementsandperforma
|     |     |     |     |     | 1   | 1   |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
first-ordercorrection.Inthisstephowever,weavoidperforminga Withanestimatefordrift,wecanthensolveforthepropagation
driftcorrectionandmaintainthenaturaldriftrateofthedevice.
delaybyexaminingthetotalroundtriptime,
|     |     |         |      | i+1=t | i+1+α·(T | (cid:2)        |        |
| --- | --- | ------- | ---- | ----- | -------- | -------------- | ------ |
|     |     |         |      | t     |          | r tt +2·T prop | ) (14) |
|     | θ   | =ti −ti |      | 3     | 0        |                |        |
|     | i   |         | (12) |       |          |                |        |
1 0
where,
ThedevicethenperformsasecondrequestafterT
|                                                          |     |     | interval to | T(cid:2)   |              |                  |         |
| -------------------------------------------------------- | --- | --- | ----------- | ---------- | ------------ | ---------------- | ------- |
|                                                          |     |     |             | =T RxDelay | +T GwTxDelay | +T ToA +T decode | −T ramp |
| collectasecondsetoftimemeasurements.Usingthemeasurements |     |     |             | rtt        |              |                  |         |
(15)
| fromthetwosets,wecomputedrift,α |     | asfollows: |     |     |     |     |     |
| ------------------------------- | --- | ---------- | --- | --- | --- | --- | --- |
294

LongShoT:Long-RangeSynchronizationofTime IPSN’19,April16–18,2019,Montreal,QC,Canada
thus, Anopen-sourceLoRaWANServer2 isusedalongwithasimple
ti+1−ti+1 T(cid:2) Node.jsapplicationservertoprovideresponsestoLongShoTre-
T prop = 3 0 − rtt (16) quests.
2·α 2
Inallexperiments,thegatewayhoststhereferenceclockwhich
Withaproperestimateforbothdriftandpropagationdelay,we isassumedtobeperfectlysynchronizedwithGPStime,hencewe
canthencomputethetrueoffset, willrefertoGPStimeasthesystemreference.Tocollectdatawith
GPSasgroundtruth,eachdevicesamplesitsclockonthefalling
θ i+1 =t
2
i+1−t
3
i+1+T prop (17) edgeoftheGPS1PPSsignal,whichis200msaftertherisingedge.
Thefallingedgeisusedtonotconflictwiththelocaltimertick
UsingEquations13,16and17,wecansynchronizethedevice interrupt.TheGPS1PPSaccuracyerrorismeasuredtobe<50ns
clocks,correctlong-termdriftandestimatethewirelesspropagation fortheORG1411.[25]Eachlocaltimesampleistaggedwiththe
timebetweenthegatewayanddevice. correspondingGPStimestamptoalignsamplesfromalldevices.To
Theaccuracyofresultswilldependontheaccuracyatwhich optimizedatatransferoverLoRaWAN,onlysamplesoneach10th
wecandeterminedrift.Thesourcesoferrorforthisapproachare secondofGPStimearerecorded.GPSpositionisalsocollectedfor
mainlyduetolong-termdriftstabilityandjitterinmeasuringtime. eachsynchronizationinterval.Alldevicessynchronizeat5-minute
Driftstabilitycanbeaffectedbyseveralfactors,suchastempera- intervals,basedonGPStime.AllLoRaWANmessagesaresentwith
tureandvibration.Compensationfortheseeffectsarepossiblebut DR0toprovideconsistentbehaviorirrespectiveofdistancefrom
outsidethescopeofLongShoT. thegateway.
4 EVALUATION
4.2 Metrics
WeevaluateLongShoTtodeterminethelevelofaccuracywecan
Wedefineourfiguresofmeritbasedontheaccuracyofsynchro-
synchronizedevicesatlongdistance.Inthissection,wedescribeour
nizingourdeviceclockswithGPStimeandtheratesatwhichwe
experimentapproach,thehardwareandsoftwareelementsrequired,
canmaintainsynchronization.Thefollowingmetricsareusedto
followedbyourtargetmetrics.Thefirstexperimentmeasuresthe
measuretheperformanceofLongShoT:
performanceofusingtheone-shotsynchronizationapproach.In SynchronizationErrorisdefinedastheoffsetofalocalclock
thesecondexperiment,wemeasuresynchronizationofdevices
comparedtoGPStimemeasuredusingthefirstsampleimmedi-
physicallydistributedupto4kmfromthereferencegateway.
atelyafterasynchronizationrequest.Thisindicateshowaccurate
LongShoTisabletosynchronizetimewitheachrequest.Dueto
4.1 ExperimentSetup
variationsinsourcesofnetworkdelaysandphysicallimitationsin
LongShoTwasimplementedonconsumer-off-the-shelfhardware, signalbandwidthandhardware,theexpectederrorsmayriseupto
as described in Figure 6. An ESP-WROOM-32[7] is used as the afewmicroseconds.Wethussetagoalof±10μsfromthereference
microcontroller and a Semtech SX1276[29] as the sensor radio. asameasureofacceptablesynchronizationerrorperformance.
EachsensorincludesanOriginGPSORG1411[23]GPSReceiver DriftRateistheresultofdevicescorrectingtheirlocalclock
thatprovidesa1PPSsignalandGPStime.Thesensorfirmware ratesbasedonLongShoTmeasurements.Thismetriciscalculated
uses Semtech’s LoRaMac stack, modified to provide MAC-level fromeachconsecutiveoffsetmeasurementandaveragedoverthe
timestamps to the application. The local clock is driven by the correspondingsynchronizationinterval.Reducingdriftincreases
ESP-32’stimermoduleconfiguredtorunat40MHz.Internally,an thelengthofvalidsynchronizationandreducestheneedforfre-
ESP-WROOM-32usesa40MHzreferencecrystaloscillatorwithan quentrequests.InLongShoT,weset1ppmasthestandardfordrift
accuracyof±10ppm. andaimtobewellbelowthosebounds.
4.3 One-ShotSynchronizationResults
(cid:5)(cid:11)(cid:10) (cid:9)(cid:9)(cid:12)
(cid:6)(cid:17)(cid:11)(cid:16) (cid:7)(cid:2)(cid:14) (cid:4)(cid:9)(cid:12)
The first experiment investigates the effectiveness of One-Shot
(cid:12)(cid:15)(cid:20)(cid:21)(cid:25)(cid:24) (cid:3)(cid:12)(cid:9)(cid:18)(cid:22)(cid:21) (cid:8)(cid:11)(cid:4)(cid:20)(cid:23)(cid:20)(cid:20)
(cid:12)(cid:9)(cid:5) (cid:14)(cid:1)(cid:11)(cid:13) Synchronization for correcting both synchronization offset and
drift.
Figure 6: Block diagram of the LongShoT sensor imple- 4.3.1 ExperimentProcedure. Theexperimentusestwodevices,co-
mentedwithanESP-WROOM-32andanSX1276LoRaradio. locatedataround200mfromthegateway.Inthisexperiment,we
AGPS1PPSsignalisusedtosamplethedevice’scurrenttime varythevalueofRxDelayfrom1sto9s,inincrementsof2seconds.
andestablishgroundtruthwithrespecttoGPStime.
Witheachcase,weexaminetheeffectonsynchronizationoffset
anddriftrate.
For the LoRaWAN network, a Raspberry Pi 3 is used as the We also gather a special case whereRxDelay = 1s but only
gatewayalongwithaRisingHFRHF0M301LoRaConcentrator(in- performingoffsetcorrectionwithoutdriftcorrection.Thisprovides
ternallyaSemtechSX1301)module.AU-BloxNeo-6MGPSmodule abaselineforoffsetaccuracyandnaturaldevicedrift.
providesthetimereferencetoboththeRaspberryPiandconcentra- Theexperimentgatheredtwohoursworthofdevicetimedata
tor.ThegatewaysoftwareisavanillaSemtechPacketForwarder1. foreachcasetested.Devicessynchronizeevery5minutesandeach
1SemtechGithub-https://github.com/lora-net/packet_forwarder 2LoRaServer-https://loraserver.io
295

IPSN’19,April16–18,2019,Montreal,QC,Canada C.Ramirezetal.
20
0
-20
-40
-60
Baseline 1s 3s 5s 7s 9s
RxDelay
)s
(
tesffO
5
0
-5
Device 1
Device 2
-10
Baseline 1s 3s 5s 7s 9s
RxDelay
(a)SynchronizationError
)mpp(
tfirD
Device 1
Device 2
(b)DriftRates
Figure7:EffectsofincreasingRxDelayforOne-ShotSynchronization.Highersynchronizationaccuracyandbetteroverall
driftratesareseenwithincreasingRxDelay.AnRxDelayvalueofatleast5s providessatisfactoryresultswithasinglesyn-
chronizationrequest.
synchronizationrequestisindependentoftheprevious.Atotalof below1ppmwithasinglesynchronizationrequest.Itisimportant
6caseswerecollected,resultingin12hoursworthofdevicetime tonotethatOne-ShotSynchronizationcannotfactorinpropagation
data. delayandwillthusappearasaconstantoffsetdependingonthe
distanceofdeviceandgateway.ItissuggestedtouseOne-Shot
4.3.2 Analysis. TheresultsforthisexperimentcanbeseeninFig-
Synchronizationfordeviceswithincloserangeofthegateway,or
ure7where(a)showsSynchronizationErrorand(b)showsthe
forthoseapplicationswhichcantoleratethedeterministicerrors
resultingDriftRates.Meanandstandarddeviationofresultscan
introducedbypropagationdelay.
befoundinTable4.
Wecanseefromthebaselinecasethatsimplyapplyingclassical
4.4 Long-Range,Two-StepSynchronization
two-waytimetransferdoesnotguaranteeaccuratesynchronization.
The baseline drift rates vary between devices but are naturally Oursecondexperimentinvestigatestheperformanceofsynchro-
stable.ThisalsoconfirmsEquation7thatsynchronizationerroris nizationatlong-range.Inthisexperiment,Two-Stepcorrection
largerwithhigherdriftratesduetothenetworkroundtriptime. approachwasusedtoproperlysynchronizewhileaccountingfor
propagationdelay.Theexperimentwasconductedwiththreede-
Sync.Error(μs) DriftRate(ppm) vicesplacedatsignificantdistancesfromthereferencegateway.
Case
Device1 Device2 Device1 Device2
Base −2.0±2.6 −37±21 −1.3±0.9 −4.6±0.8 4.4.1 ExperimentProcedure. Inthisexperiment,weplacedthree
1s −4.2±9.4 −3.2±5.9 −1.1±3.4 −1.7±2.7 devicesatrangeswherepropagationdelaywouldplayasignificant
3s 1.1±1.9 1.2±8.2 −0.1±1.0 −0.1±1.1 factorintimesynchronization.Twodeviceswereplacedatapprox-
5s 1.4±5.6 2.7±4.5 −0.2±0.6 0.03±0.6 imately1kmfromthegateway,whileathirddevicewasplacedata
7s 2.3±3.3 2.7±2.6 −0.01±0.4 0.03±0.5 distanceof4km.Figure8showsthelocationsofdevicesonamap
9s 2.9±2.4 2.1±4.2 0.04±0.2 −0.001±0.2 withrespecttothegateway,alongwithphotosofactualdevice
placements.
Table4:One-ShotSynchronizationResults AlldevicesuseRxDelayof5swhileperformingoffsetanddrift
correctionusingtheTwo-Stepapproach.Devicesarelefttosyn-
WithOne-ShotSynchronizationactive,weimmediatelyseeim- chronizewiththegatewayat5-minuteintervalsforatimespanof
provementsinbothsynchronizationerroranddriftrates.Synchro- twohours.EachdevicereportsitsGPS1PPSsampledtimeandthe
nizationerrorisinverselyproportionaltoRxDelay.AtRxDelay=
devicetemperatureevery10seconds.
5s,theerrorisconsistentlywithinboundsof10μsofGPStime.This
ThecollecteddatasetcanbeseeninFigure9.Measurement
indicates5sasagoodcandidatevalueforusewithLongShoT.
errorsduetoGPS1PPSinterruptconflictsarefilteredfromthedata
LookingatDriftRates,weseethesametrendofincreasingaccu- set—thesearesuddenimpulsesinthedatawhichresultinseveral
racywithhigherRxDelays.Importantly,usinglowRxDelays(<5s),
millisecondsoferror.TheseerrorsaremainlyseeninDevice2and
theresultingratescouldbehigherthanthenaturaldriftrateofthe amounttoonly1.2%ofthedataset.
device.Thelowerthenaturaldriftrate,thehighertheprobabilityof
miscalculatingthecorrectionfactorduetomeasurementerrors,as 4.4.2 Analysis. ObservingthetimeplotinFigure9,wecansee
seeninRxDelay=1s.RxDelay=5salsoprovidessufficienttime thatatalltimes,theoffsetfromGPStimeiswithin±100μs.Device3
tobringourcorrecteddriftratestobelow1ppm.Thisresolvesto exhibitsafewcrossingsof50μsduetosignificanttemperatureshift
withinphysicallimitsof±1-bitquantizationerrorwiththeESP-32’s andincreaseddriftoverthesynchronizationinterval.LongShoT
internal40MHzcounter. doesnottakeintoaccounttemperaturechangesfordriftcorrection,
WithOne-ShotSynchronization,weachievesynchronization but it is feasible to implement for such devices as suggested in
errorswithin3μsofGPStimeandsuccessfullycorrectdriftratesto [36]. Being able to account for temperature changes will allow
296

LongShoT:Long-RangeSynchronizationofTime IPSN’19,April16–18,2019,Montreal,QC,Canada
Device Distance(m) Temp.Range(C) Synch.Error(μs) Drift(ppb) Prop.Delay/Error(μs)
|         |      |           | μ =1.61,σ | =2.41 | μ =5,σ   | =53 | μ =2.6,σ =1.5,ϵ | =−1.1 |     |
| ------- | ---- | --------- | --------- | ----- | -------- | --- | --------------- | ----- | --- |
| Device1 | 1112 | 34.3-35.9 |           |       |          |     |                 |       |     |
|         |      |           | μ =1.64,σ | =2.35 | μ =−14,σ | =45 | μ =2.4,σ =1.6,ϵ | =−1.3 |     |
| Device2 | 1113 | 34.1-35.3 |           |       |          |     |                 |       |     |
Device3 3960 30.2-32.8 μ =1.22,σ =3.74 μ =−38,σ =124 μ =12.1,σ =2.2,ϵ =−1.1
Table5:Summaryofresultsforsynchronizationaccuracy,driftandpropagationdelayfordevicesdistributedoverawidearea.
40
100
35
|     |     |     |     | 50  |     |     |     |     | )C( erutarepmeT |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --------------- |
|     |     |     |     | )s  |     |     |     |     | 30              |
( tesffO
|     |     |     |     |     | 0   |     |     |     | 25  |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
20
-50
|     |     |     |     |     | D1 Offset | D1 Temp |     |     | 15  |
| --- | --- | --- | --- | --- | --------- | ------- | --- | --- | --- |
|     |     |     |     |     | D2 Offset | D2 Temp |     |     |     |
-100
|     |     |     |     |     | D3 Offset | D3 Temp |     |     |     |
| --- | --- | --- | --- | --- | --------- | ------- | --- | --- | --- |
(a)DeviceLocations:gateway(green)andthreesensors(blue,red, 10
|                                   |     |     |     |     | 0 20 | 40             | 60 80 | 100 | 120 |
| --------------------------------- | --- | --- | --- | --- | ---- | -------------- | ----- | --- | --- |
| purple)(MapSource:OpenStreetMaps) |     |     |     |     |      | Time (Minutes) |       |     |     |
Figure9:TimeOffsetfromGPStimeofthreedevicesplaced
|     |     |     |     | at significant |     | distances from | the gateway. | All | devices are |
| --- | --- | --- | --- | -------------- | --- | -------------- | ------------ | --- | ----------- |
±100μs
|     |     |     |     | well-below |     | at all times. | Device | temperatures | swing |
| --- | --- | --- | --- | ---------- | --- | ------------- | ------ | ------------ | ----- |
between30to35°C.Itcanbeseeninthetimeplotsthatthe
driftratesofdevicesareaffectedbysmallchangesintemper-
ature.LongShoTattemptstocorrectforthesechangeswith
eachrequest.
betterthanthenaturaldriftratesexhibitedbythesedevices.Achiev-
ingtheseratesmeanthatwecanmaintainsynchronizationlonger
andusefewerpacketstore-synchronize.Factoringintemperature
(b)Device1 (c)Device3 compensationwillimprovethisfurther,butisoutsidethescopeof
thiswork.
Inadditiontocollectingoffsetanddriftdata,thedevicesrecord
Figure8:Approximatelocationsofgatewayanddevices.(a)
thepropagationdelaycomputedwitheachrequestandisshownin
showsthelocationofthegatewayononeendofarunway,
|     |     |     |     | Figure11.Whilethedistributionofresultsisquitehigh(σ |     |     |     |     | =1.7μs), |
| --- | --- | --- | --- | --------------------------------------------------- | --- | --- | --- | --- | -------- |
withtwodevicesplaced1.1kmawayattheotherend.Athird
deviceisplaced3.96kmawayfromthegateway.Actualdevice themeanestimatesfallcloselytotheexpectedvaluetakinginto
placementsareseenin(b)and(c). accountthespeedoflighttravelingthedevicedistance.Amean
errorof−1.1μsisobservedacrossalldevices.
LongShoTtoperformslightadjustmentsshorttermdriftcorrections Theestimationofpropagationdelayreliesdirectlyonthesta-
andmaintaintightersynchronizationbetweenintervals.LongShoT bilityofdriftoverthesynchronizationinterval.Thiscaneasily
ismoresuitedtoadjustingforlong-termdriftandoscillatoraging. beaffectedbyseveralfactors,suchastemperatureandvibration.
ItcanbeseeninFigure10athatsynchronizationerrorsforallde- Whiletheresultsarenotprecisetoenableinverselyestimating
vicesarewithin±10μs.Thisiswithintheboundsofouracceptable thedistancefromagateway,itisenoughtosynchronizedevice
performancerange.Furthermore,themeansynchronizationerror clocksatthemicrosecondlevel.Onesuchapproachtoimprove
foralldevicesis1.49μswithastandarddeviationof2.83μs.Most
theseresultsfurtherinvolvesincreasingtheclockresolutionon
thegateway,whichislimitedto1μsticks,andallownanosecond
notably,wedonotobserveasignificantoffsetduetopropagation
delay,inwhichDevice3wouldexhibitupto13.3μsat4kmaway leveltimestamps.Anotherapproachistostatisticallyaccumulate
fromthereference.ThisindicatesthatLongShoTcancompensate propagationdelayestimatesoverseveralindependentprobesand
forpropagationdelayinsynchronizinglocaldeviceclocks. convergeonthemostlikelyvalueforpropagationdelay.
TheachieveddriftratesarealsoremarkableasseeninFigure10b. Our results show that LongShoT can accurately synchronize
Alldevicedriftrateshaveameanof15ppbwithastandarddeviation
deviceclocksoversignificantdistanceswithsingleperiodicnetwork
of83ppb.Thesecompensatedratesareatthelimitofourdevices’ requests.Table5summarizestheresultsofsynchronizationerror,
40MHzcrystaloscillators.Thisisatleasttwoordersofmagnitude driftandpropagationdelayestimatesacrossallthreedevices.
297

| IPSN’19,April16–18,2019,Montreal,QC,Canada |     |     |     |     |     |     |     | C.Ramirezetal. |     |
| ------------------------------------------ | --- | --- | --- | --- | --- | --- | --- | -------------- | --- |
thetotaltime.Dependingontheapplication,thesynchronization
10
intervalcanbeadjustediftheapplicationrequirestightersynchro-
nizationattheexpenseofmoreenergy,orcanberelaxedtoreduce
5
theamountofenergyusedoverall.Table6summarizesthesyn-
)s
chronizationperformanceofalldevicesovertheentireexperiment
( tesffO
| 0   |     |     |     | duration. |     |     |     |     |     |
| --- | --- | --- | --- | --------- | --- | --- | --- | --- | --- |
-5
-10
|     | Device 1 Device 2 | Device 3 |     |     |     |     |     |     |     |
| --- | ----------------- | -------- | --- | --- | --- | --- | --- | --- | --- |
(a)SynchronizationError
0.3
0.2
0.1
)mpp( tfirD
0
-0.1
|     |     |     |     | Figure 12: | Distribution | of  | device offsets | for | three devices |
| --- | --- | --- | --- | ---------- | ------------ | --- | -------------- | --- | ------------- |
-0.2 over 2 hours. Devices maintain synchronization to within
|      |                   |          |     | ±100μs at            | all times, | with 97.5% | of all | offsets | falling within |
| ---- | ----------------- | -------- | --- | -------------------- | ---------- | ---------- | ------ | ------- | -------------- |
| -0.3 |                   |          |     | ±50μsofthereference. |            |            |        |         |                |
|      | Device 1 Device 2 | Device 3 |     |                      |            |            |        |         |                |
(b)DriftRates
|     |     |     |     |     | MeanAbs.Offset(μs) |     |     | OffsetWithin50μs |     |
| --- | --- | --- | --- | --- | ------------------ | --- | --- | ---------------- | --- |
Device
Figure 10: Results of Synchronization at Long-Range. All μ =6.6,σ =6.8
|                   |               |      |                      | Device1 |          |      |     | 100%  |     |
| ----------------- | ------------- | ---- | -------------------- | ------- | -------- | ---- | --- | ----- | --- |
| 3 devices perform | comparatively | well | despite varying dis- |         |          |      |     |       |     |
|                   |               |      |                      | Device2 | μ =6.3,σ | =6.0 |     | 96.4% |     |
tancefromthegateway.ThehigherdriftdistributionforDe-
|     |     |     |     | Device3 | μ =16.4,σ | =16.8 |     | 96.1% |     |
| --- | --- | --- | --- | ------- | --------- | ----- | --- | ----- | --- |
vice3isduetotemperatureshiftsatitslocation.
|     |     |     |     | All      | μ =9.8,σ        | =12.0       |     | 97.5%   |         |
| --- | --- | --- | --- | -------- | --------------- | ----------- | --- | ------- | ------- |
|     |     |     |     | Table 6: | Synchronization | performance |     | summary | showing |
15
themeanabsoluteoffsetofdeviceclockswithrespecttoGPS
| )s  |     |     |     | timeoverthedurationoftheexperiment. |     |     |     |     |     |
| --- | --- | --- | --- | ----------------------------------- | --- | --- | --- | --- | --- |
( yaleD noitagaporP
10
5 LONGSHOTANDGPSENERGY
Synchronizingtimeoverawideareaistypicallydoneusingon-
5
boardGPSreceivers.WhileGPSreceiversprovidesynchronization
|     |     | Measurement Data |     | accuracytowithin100ns[34],itrequiresatleast10X |     |     |     |     |     |
| --- | --- | ---------------- | --- | ---------------------------------------------- | --- | --- | --- | --- | --- |
moreenergy
| 0   |     | Speed of Light (300m/ | s)  |     |     |     |     |     |     |
| --- | --- | --------------------- | --- | --- | --- | --- | --- | --- | --- |
thansynchronizingtimewithLongShoT.Inthissection,wecom-
0 500 1000 1500 2000 2500 3000 3500 4000 paretheenergyusageofperformingLongShoTrequestsversus
Distance from GW (m)
usingaGPSreceivertosynchronizetimeoverlongdistances.Fora
faircomparison,weevaluatetheenergyrequiredforonesynchro-
| Figure 11: Propagation | delay | as estimated | by end-devices |     |     |     |     |     |     |
| ---------------------- | ----- | ------------ | -------------- | --- | --- | --- | --- | --- | --- |
nizationattempt,orEnergyPerSync(EPS),onconsumergrade
usingtwo-stepsynchronizationrequests.Theestimatedde-
| laysshowanaverageerrorof−1.1μs |     | withrespecttotheex- |     | devices. |     |     |     |     |     |
| ------------------------------ | --- | ------------------- | --- | -------- | --- | --- | --- | --- | --- |
pecteddelaygivendistancetraveledoverthespeedoflight.
5.1 LongShoTRequestEnergy
TheenergyrequiredtoperformaLongShoTtransactionisequalto
4.4.3 SynchronizationPerformance.
Finally,weobservehowwell theenergyconsumedbyoneLoRaWANtransaction.Theenergyef-
ourdevicesremainsynchronizedoverthespanoftimeoftheexperi- ficiencyofLoRaWANpackettransactionshavebeenstudiedin[19].
mentthroughtheuseofLongShoT.Figure12showsthedistribution AssumingLongShoToperatesonafixedsynchronizationinterval,
ofallreportedtimeoffsetscollectedoveratwo-hourperiod.This theEPSforLongShoTcanbecalculatedgivenEquation18,
plotshowsthatsynchronizingataperiodic5-minuteintervalkeeps
|     |     |     |     | EPS | LonдShoT =V | ∗[(I tx | ∗T tx )+(I | rx ∗T rx )+ |     |
| --- | --- | --- | --- | --- | ----------- | ------- | ---------- | ----------- | --- |
ourdevicessynchronizedtowithin±100μsofourreferencetime
(18)
|     |     |     |     |     | (I idle | ∗T RxDelay | )+(I | sleep ∗T | sleep )] |
| --- | --- | --- | --- | --- | ------- | ---------- | ---- | -------- | -------- |
atalltimes.
Lookingclosely,Device1stayswithin±50μs ofthereference where,thetotalenergyisthesumoftheenergyconsumedwith
atalltimes,whileDevices2and3holdwithin±50μs for96%of eachstateoftheLoRaWANtransaction(Tx,Idle,Rx,Sleep).Table7
298

LongShoT:Long-RangeSynchronizationofTime IPSN’19,April16–18,2019,Montreal,QC,Canada
providesthetypicalvaluesforasingleLongShoTrequestperformed cost time fixes, it requires ephemeris downloads every 30 min-
intheUS915bandspecificationandasusedintheevaluationsin utes.Figure13comparesthetotalenergyconsumedbyLongShoT
Section4. andGPSwithanincreasingintervalbetweenconsecutiverequests.
Usingthemaximumtransmitpowerof20dBmandanRxDelay
Basedfromthisprojection,LongShoTuseslessenergythanGPS
of5s,theenergypersyncisroughly190mJ. forintervalslongerthan50sbetweensynchronizationrequests.
| Parameter |     | Conditions | Value |  rep ygrenE latoT |                     |     |     |          |     |
| --------- | --- | ---------- | ----- | ----------------- | ------------------- | --- | --- | -------- | --- |
| V         |     |            | 3.3V  |                   | )J( sruoH 5.0    10 |     |     | LongShoT |     |
InputVoltage
| I   | RFOutPower | =20dBm | 120mA |     |     |     |     | GPS |     |
| --- | ---------- | ------ | ----- | --- | --- | --- | --- | --- | --- |
tx
| I rx |     | BW =500kHz | 12.6mA |     | 5   |     |     |     |     |
| ---- | --- | ---------- | ------ | --- | --- | --- | --- | --- | --- |
| I    |     | -          | 1.8mA  |     |     |     |     |     |     |
idle
| I   |     | -   | 1μA |     | 0   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
sleep
| T   | 4bytes@SF | =10,BW =125kHz | 329.728ms |     |     | 102 |     | 103 |     |
| --- | --------- | -------------- | --------- | --- | --- | --- | --- | --- | --- |
tx
Sync Interval (s)
| T rx   | 8bytes@SF      | =10,BW =500kHz | 92.672ms |     |     |     |     |     |     |
| ------ | -------------- | -------------- | -------- | --- | --- | --- | --- | --- | --- |
| T idle | BasedonRxDelay |                | RxDelay  |     |     |     |     |     |     |
T SyncInterval Varies Figure13:Totalenergyconsumedfortimesynchronization
sleep
|     |     |     |     | by  | synchronization | interval. LongShoT | consumes |     | less en- |
| --- | --- | --- | --- | --- | --------------- | ------------------ | -------- | --- | -------- |
Table7:LoRaWANEnergyParametersbasedonanSX1276
ergythanGPSforintervalsgreaterthan50s.
transmittingatfullpowerintheUS915band.[28,29]
6 RELATEDWORK
5.2 GPSEnergyComparison Timesynchronizationinwirelesssensornetworkshasbeenstudied
GPSreceiversarecapableofprovidingtimeassoonasitcanes- indepth.Synchronizationistypicallyachievedbymessagepassing
tablishafixinlocation.Forconsumer-gradeGPSreceivers,the andregressionofmultipletimemeasurementsacrossthemessage
accuracyofthefirstfixmaybeoffbyseveralmeters[12].Thistrans- exchange.ReferenceBroadcastSynchronization(RBS)[6]usesa
latesto<100nsoferror,butissufficientenoughtocompareagainst broadcastmessagefromareferencenodeandthereceptiontime
LongShoT’ssub-10μsaccuracy.Toquantifytheenergyusageofsyn- oneachnodeasamarkerfortimeacrossthesystemofdevices.
chronizingtimewithGPS,weconsiderthetime-to-first-fix(T
|     |     |     | ttff) | Similarly,theLoRaWANstandard[16]specifiesamode(ClassB)for |     |     |     |     |     |
| --- | --- | --- | ----- | --------------------------------------------------------- | --- | --- | --- | --- | --- |
givendifferentstartupstatesofaGPSreceiver. receivingbroadcastmessagesfromgatewaystosynchronizenodes.
Thetime-to-first-fixtypicallydependsonthepreviousstateheld TPSN[9]usesatwo-waymessagepassingschemeacrosspair-
bytheGPSreceiverandthevalidityofthesatelliteephemerisdata wisenodestofactorindelaysincurredinthenetworkstack.It
inmemory.Withintheseconditions,aGPSreceivermayperform howeverassumesthatclockdriftduringmessageexchangeisneg-
thefollowingonstartupsequences:
ligibleandwouldamounttosignificanterrorsinthetimescalesof
| • HotStart-thereceiverhasavalidlast-knownpositionand |     |     |     | LoRaWAN. |     |     |     |     |     |
| ---------------------------------------------------- | --- | --- | --- | -------- | --- | --- | --- | --- | --- |
validephemerisdata. FloodingTimeSynchronizationProtocol(FTSP)[18],Pulse-Sync
| •         |                                         |     |     | [13]andGlossy[8]synchronizetimeacrosssizeable,multi-hop |     |     |     |     |     |
| --------- | --------------------------------------- | --- | --- | ------------------------------------------------------- | --- | --- | --- | --- | --- |
| WarmStart | -thereceiverhasavalidlast-knownposition |     |     |                                                         |     |     |     |     |     |
networksbyutilizingnetworkfloodingtoachieveaccuracy.Fur-
buttheephemerisdatahasexpired.
thermore,propagationdelayhasbeenshowntoaccumulatewith
| • ColdStart | -bothpositionandephemerisdataareinvalid, |     |     |     |     |     |     |     |     |
| ----------- | ---------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
typicallyonfirstpowerup. eachhopalongthenetwork.TATS[14]improvesonGlossyand
Pulse-Synctofactorpropagationdelayandincreasethesynchro-
Satelliteephemerisdataareupdatedevery30minutesandtakes
nizationaccuracyacrossthenetworkofnodes.
atleast30s toacquirewithfull-poweracquisition.Oneachcold
IncontrasttoLongShoT,theseapproachesdonotapplytoLo-
startandeachsubsequent30minutes,aGPSreceivermustexpend
|     |     |     |     | RaWAN | due to bandwidth | limitations | and the | fundamental | dif- |
| --- | --- | --- | --- | ----- | ---------------- | ----------- | ------- | ----------- | ---- |
energytore-acquiretheephemeris.Table8showsthetypicalenergy
ferenceinnetworktopology.LongShoToperateswiththerange
consumedtostartupaGPSreceiverandwaitingforthefirstfix.
achievablebyLoRaWAN,factoringinpropagationdelayandthe
compoundedeffectsduetoclockdrift.
Mode T ttff Power EnergyPerSync Furthermore,theuseofameshtopologyorbroadcastpackets
ColdStart 35s 77mW 2695mJ increasestheenergyrequiredtosynchronizetime,eitherbykeep-
|     | 32s | 67mW 2144mJ |     |     |     |     |     |     |     |
| --- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
WarmStart ingthedeviceawaketoreceiveortransmittingmorepacketsthan
|     | 2s  | 67mW 134mJ |     |     |     |     |     |     |     |
| --- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
HotStart needed.LongShoTenablestimesynchronizationon-demandallow-
ingadevicetoremainindeep-sleepandmaintainawake-sync-
Table8:OriginGPSNano-HornetORG1411TypicalStartup
ModeEnergyConsumption@1.8V measure-sleeproutineasnecessaryforultralow-poweroperation.
[23]
OthermethodssuchasStitch[17],similarly,usesnarrow-band
transceiverstoperformfrequencysyntonizationoflocaloscillators.
FromTable8,wecanobservethatperformingaColdorWarm WhileStitchdoesnotprovidephasesynchronization,itseaseof
Startisatleast10X morecostlythanasingleLongShoTrequest. syntonizationcanbenefitLongShoTinaddressingdriftbetween
WhileadditionalHotStartsprovidelow-latencyandlow-energy twooscillatorsandthusloweringenergycostfurther.
299

IPSN’19,April16–18,2019,Montreal,QC,Canada C.Ramirezetal.
7 CONCLUSION [10] BobIannucciandAnthonyRowe.2017.CrowdsourcedSmartCities.Intelligent
TransportationSystems(ITS)WorldCongress(2017).
In this paper, we presented LongShoT, a time synchronization [11] DieterKirchner.1991.Two-WayTimeTransferViaCommunicationSatellites.
schemebuiltonLoRaWANthatallowsdevicesynchronizationto Proc.IEEE79,7(1991),983–990. https://doi.org/10.1109/5.84975
within10μsofacommonclockatbothlong-rangeandlow-power [12] MikkoLehtinen,AriHapponen,andJouniIkonen.[n.d.].Accuracyandtimeto
firstfixusingconsumer-gradeGPSreceivers.([n.d.]).
throughanin-depthtiminganalysisofLoRaWANanditshard- [13] ChristophLenzen,PhilippSommer,andRogerWattenhofer.2015.PulseSync:An
ware.WeimplementedLongShoTonoff-the-shelfcomponentsand efficientandscalableclocksynchronizationprotocol.IEEE/ACMTransactionson
Networking23,3(2015),717–757. https://doi.org/10.1109/TNET.2014.2309805
inourexperimentsshowthatLongShoTcanachieveanaverage
[14] RomanLim,BalzMaag,andLotharThiele.2016. Time-of-FlightAwareTime
synchronizationerroroflessthan2μsanditcanmaintainsynchro- SynchronizationforWirelessEmbeddedSystems.InternationalConferenceon
nizationtowithin50μsofthereferencetimewithasinglepacket EmbeddedWirelessSystemsandNetworks(2016),149–158.
[15] LoRa-Alliance.2015.AtechnicaloverviewofLoRaandLoRaWAN.November
synchronizationrequestevery5minutes. (2015),1–20. https://doi.org/10.1038/scientificamerican1013-22
Wehaveshownthataccuratesynchronizationanddriftcorrec- [16] LoRaAlliance.2018.LoRaWAN1.0.3specification.Lora-Alliance.Org1[Online],
Accessible:https://lora-alliance.org/sites/default/files/2018-07/lorawan1.0.3.pdf
tionmaybeachievedwithasinglepacketbytakingadvantage
(2018),1–72. https://lora-alliance.org/sites/default/files/2018-07/lorawan1.0.3.
ofLoRaWAN’sconfigurablenetworkdelay.Thisallowsasimple pdf
wake-sync-measure-sleeppatternwhichcanbeperformedattheap- [17] AnhLuong,PeterHillyard,AlemayehuSolomonAbrar,CharissaChe,Anthony
Rowe,ThomasSchmid,andNealPatwari.2018.AStitchinTimeandFrequency
plication’sdiscretionandsupportultralow-powerconsumptionfor
Synchronization.201817thACM/IEEEInternationalConferenceonInformation
battery-powereddevices.Furthermore,LongShoTcansynchronize ProcessinginSensorNetworks(IPSN)(2018),96–107. https://doi.org/10.1109/IPSN.
devicesupto4kmawayfromaLoRaWANgateway.Synchroniza- 2018.00016
[18] MMaróti,BKusy,GSimon,andÃĄLédeczi.2004.Thefloodingtimesynchro-
tionatsuchdistanceswaspreviouslyonlyachievedbyhavingGPS nizationprotocol.SenSys’04-ProceedingsoftheSecondInternationalConference
timingreceiversonsensordevices,butLongShoTunlocksthiscapa- onEmbeddedNetworkedSensorSystems(2004),39–49. https://doi.org/10.1145/
1031495.1031501
bilityfordevicesincapableofsupportingtheenergyrequirements
[19] SamarthMathur,AnandSankar,PrajwalPrasan,andBobIannucci.2017.Energy
ofasustained,activeGPSreceiver. AnalysisofLoRaWANTechnologyforTrafficSensingApplications.Intelligent
LongShoT is capable of achieving accurate results with sim- TransportationSystems(ITS)WorldCongress(2017).
[20] YasirMehmood,FarhanAhmad,IbrarYaqoob,AsmaAdnane,MuhammadIm-
plisticapproaches,inparticular,byrelyingonpredictabletiming
ran,andSghaierGuizani.2017.Internet-of-Things-BasedSmartCities:Recent
behaviorsoftheradiohardware.FollowingIEEE-1588andStitch,it AdvancesandChallenges.IEEECommunicationsMagazine55,9(2017),16–24.
wouldbebeneficialforthenetworkinterfacetomanagetheclock https://doi.org/10.1109/MCOM.2017.1600514
[21] DavidL.Mills.1991.InternetTimeSynchronization:TheNetworkTimeProtocol.
anddistributetimetotherestofthesystem.Similarly,LongShoT IEEETransactionsonCommunications39,10(1991),1482–1493. https://doi.org/
demonstratesthesamecapabilityforLPWANsandrecommend 10.1109/26.103043
[22] UmberNoreen,AhceneBounceur,andLaurentClavier.2017.AstudyofLoRa
thathardwaremanufacturersconsiderbuildingthisfunctionality
lowpowerandwideareanetworktechnology. 2017InternationalConference
in. onAdvancedTechnologiesforSignalandImageProcessing(ATSIP)(2017),1–6.
https://doi.org/10.1109/ATSIP.2017.8075570
REFERENCES [23] OriginGPS.2014.NanoHornet(ORG1411)GPSAntennaModule.(2014).
[24] KristoferS.J.PisterandLanceDoherty.2008.TSMP:Timesynchronizedmesh
[1] FerranAdelantado,XavierVilajosana,PereTuset-Peiro,BorjaMartinez,Joan protocol.PdcsJANUARY2008(2008),391–398.
Melia-Segui,andThomasWatteyne.2017.UnderstandingtheLimitsofLoRaWAN. [25] Inc.Qualcomm.2015.SiRFstarGSD4e1PPSTimingAccuracy.(2015).
IEEECommunicationsMagazine55,9(2017),34–40. https://doi.org/10.1109/ [26] MattiaRizzi,PaoloFerrari,AlessandraFlammini,andEmilianoSisinni.2017.
MCOM.2017.1600613 EvaluationoftheIoTLoRaWANSolutionforDistributedMeasurementAppli-
[2] MarcoCentenaro,LorenzoVangelista,AndreaZanella,andMicheleZorzi.2016. cations. IEEETransactionsonInstrumentationandMeasurement66,12(2017),
Long-rangecommunicationsinunlicensedbands:TherisingstarsintheIoTand 3340–3349. https://doi.org/10.1109/TIM.2017.2746378
smartcityscenarios.IEEEWirelessCommunications23,5(2016),60–67. [27] H.G.SchroderFilho,J.PissolatoFilho,andV.L.Moreli.2016.Theadequacyof
[3] ChiaraMariaDeDominicis,StudentMember,PaoloPivato,PaoloFerrari,David LoRaWANonsmartgrids:AcomparisonwithRFmeshtechnology.IEEE2nd
Macii,EmilianoSisinni,andAlessandraFlammini.2013.TimestampingofIEEE InternationalSmartCitiesConference:ImprovingtheCitizensQualityofLife,ISC2
802.15.4aCSSsignalsforwirelessrangingandtimesynchronization. IEEE 2016-Proceedings(2016). https://doi.org/10.1109/ISC2.2016.7580783
TransactionsonInstrumentationandMeasurement62,8(2013),2286–2296. https: [28] Semtech.2013.LoRaModemDesignGuide.July(2013),1–9.
//doi.org/10.1109/TIM.2013.2255988 [29] Semtech.2016.SX1276/77/78/79Datasheet.August(2016).
[4] A.Dongare,C.Hesling,K.Bhatia,A.Balanuta,R.L.Pereira,B.Iannucci,andA. [30] Semtech.2016.SX1301Datasheet.(2016),1–63.
Rowe.2017.OpenChirp:ALow-PowerWide-AreaNetworkingarchitecture.In [31] GyulaSimon,MiklÃşsMaróti,ÃĄkosLédeczi,GyÃűrgyBalogh,BranislavKusy,
2017IEEEInternationalConferenceonPervasiveComputingandCommunications AndrÃąsNádas,GÃąborPap,JÃąnosSallai,andKenFrampton.2004. Sensor
Workshops,PerComWorkshops2017. https://doi.org/10.1109/PERCOMW.2017. Network-basedCountersniperSystem.InProceedingsofthe2NdInternational
7917625 ConferenceonEmbeddedNetworkedSensorSystems(SenSys’04).ACM,NewYork,
[5] JohnEidson.2005.IEEEStandardforaPrecisionClockSynchronizationProtocol NY,USA,1–12. https://doi.org/10.1145/1031495.1031497
forNetworkedMeasurementandControlSystems.IEEEStd1588-2008(Revisionof [32] FikretSivrikayaandBulentYener.2004.TimeSynchronizationinSensorNet-
IEEEStd1588-2002)(2005),1–269. https://doi.org/10.1109/IEEESTD.2008.4579760 works:ASurvey.(2004).
[6] JeremyElson,LewisGirod,andDeborahEstrin.2002. Fine-grainedNetwork [33] SanjibSur,TengWei,andXinyuZhang.2014. Autodirectiveaudiocapturing
TimeSynchronizationUsingReferenceBroadcasts.SIGOPSOper.Syst.Rev.36,SI throughasynchronizedsmartphonearray.Mobisys(2014),28–41. https://doi.
(122002),147–163. https://doi.org/10.1145/844128.844143 org/10.1145/2594368.2594380
[7] EspressifSystems.2018.ESP32Datasheet.(2018),58. [34] MarcWeiss.2014.AccurateTimeandFrequencyTransferDuringCommon-View
[8] FedericoFerrari,MarcoZimmerling,LotharThiele,andOlgaSaukh.2011.Ef- ofaGPSSatellite. February1980(2014). https://doi.org/10.1109/FREQ.1980.
ficientnetworkfloodingandtimesynchronizationwithGlossy-IEEEXplore 200424
Document.InformationProcessinginSensorNetworks(IPSN),201110thInterna- [35] AndrewJ.Wixted,PeterKinnaird,HadiLarijani,AlanTait,AliAhmadinia,and
tionalConferenceon(2011),73–84. http://ieeexplore.ieee.org/document/5779066/ NiallStrachan.2017. EvaluationofLoRaandLoRaWANforwirelesssensor
?arnumber=5779066 networks. ProceedingsofIEEESensors0(2017),5–7. https://doi.org/10.1109/
[9] SaurabhGaneriwal,RamKumar,andManiBSrivastava.2003. Timing-sync ICSENS.2016.7808712
ProtocolforSensorNetworks.InProceedingsofthe1stInternationalConference [36] MiaoXu,WenyuanXu,TingruiHan,andZhiyunLin.2016. Energy-Efficient
onEmbeddedNetworkedSensorSystems(SenSys’03).ACM,NewYork,NY,USA, TimeSynchronizationinWirelessSensorNetworksviaTemperature-Aware
138–149. https://doi.org/10.1145/958491.958508 Compensation.ACMTransactionsonSensorNetworks12,2(2016),1–29. https:
//doi.org/10.1145/2876508
300