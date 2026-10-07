> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> arXiv **2206.14077** - *DSME-LoRa: long-range communication between arbitrary nodes*.
> Source PDF deleted after conversion.
>
> Listed in `docs/research/BUDGET/01-literature.md` comms row 5 as **HELD**, no figure quoted.
> Node-to-node LoRa rather than star topology - prior art for the mesh assumption, same role as
> arXiv 2006.12570.

Ifyoucitethispaper,pleaseusetheTOSNreference:J.Alamos,P.Kietzmann,T.C.Schmidt,M.Wählisch.
DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT.ACMTrans.Sen.
Netw.,ACM,2022.https://doi.org/10.1145/3552432
DSME-LoRa: Seamless Long Range Communication
Between Arbitrary Nodes in the Constrained IoT
JOSÉÁLAMOS,PETERKIETZMANN,andTHOMASC.SCHMIDT,HAWHamburg,Germany
MATTHIASWÄHLISCH,FreieUniversitätBerlin,Germany
LongrangeradiocommunicationispreferredinmanyIoTdeploymentsasitavoidsthecomplexityofmulti-
hopwirelessnetworks.LoRaisapopular,energy-efficientwirelessmodulationbutitsnetworkingsubstrate
LoRaWANintroducesseverelimitationstoitsusers.Inthispaper,wepresentandthoroughlyanalyzeDSME-
LoRa,asystemdesignofLoRawithIEEE802.15.4DeterministicSynchronousMultichannelExtension(DSME)
asaMAClayer.DSME-LoRaofferstheadvantageofseamlessclient-to-clientcommunicationbeyondthepure
gateway-centrictransmissionofLoRaWAN.Weevaluateitsfeasibilityviaafull-stackimplementationonthe
popularRIOToperatingsystem,assessitssteady-statepacketflowsinananalyticalstochasticMarkovmodel,
andquantifyitsscalabilityinmassivecommunicationscenariosusinglargescalenetworksimulations.Our
findingsindicatethatDSME-LoRaisindeedapowerfulapproachthatopensLoRatostandardnetworklayers
andoutperformsLoRaWANinmanydimensions.
CCSConcepts:•Computersystemsorganization Sensornetworks;•Networks Link-layerpro-
→ →
tocols;Networkperformanceanalysis.
AdditionalKeyWordsandPhrases:InternetofThings,wireless,LPWAN,MAClayer,networkexperimentation
ACMReferenceFormat:
JoséÁlamos,PeterKietzmann,ThomasC.Schmidt,andMatthiasWählisch.2022.DSME-LoRa:Seamless
LongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT.ACMTrans.SensorNetw.1,1
(January2022),45pages.https://doi.org/xx.yyyy/zzzzzzz.aaaaaaa
1 INTRODUCTION
LoRaisapopularwirelessmodulationfortheIoTthatisrobustagainstinterferenceandDoppler
effect.ItusesnarrowbandChirpSpreadSpectrummodulationtoachievelongrangetransmission
(km)withlowpowerconsumption(mW).LoRaoperatesinunlicensedspectraandthereforeis
subjecttoregionalregulationsthatshallpreventasaturationofthespectrum.InEurope,theETSI
EN300.220standard[17]limitsthetransmissiondutycycleto0.1%,1%or10%dependingonthe
sub-band.
LoRaWANwasdesignedasanupperlayerforLoRathatprovidesMediaAccessControland
Internet communication between LoRa end devices and end user applications. LoRaWAN is a
cloud-based Media Access Control (MAC) layer for LoRa that organizes Physical Layer (PHY)
configurationsandMACschedules,androutestrafficbetweenenddevicesandenduserapplications.
TheLoRaWANarchitectureconsistofthreecomponents:anApplicationServer,whichcontains
Authors’addresses:JoséÁlamos,jose.alamos@haw-hamburg.de;PeterKietzmann,peter.kietzmann@haw-hamburg.de;
ThomasC.Schmidt,t.schmidt@haw-hamburg.de,DepartmentInformatik,HAWHamburg,BerlinerTor7,Hamburg,20099,
Germany;MatthiasWählisch,m.waehlisch@fu-berlin.de,InstitutfürInformatik,FreieUniversitätBerlin,Takustr.9,Berlin,
14195,Germany.
Permissiontomakedigitalorhardcopiesofallorpartofthisworkforpersonalorclassroomuseisgrantedwithoutfee
providedthatcopiesarenotmadeordistributedforprofitorcommercialadvantageandthatcopiesbearthisnoticeand
thefullcitationonthefirstpage.CopyrightsforcomponentsofthisworkownedbyothersthanACMmustbehonored.
Abstractingwithcreditispermitted.Tocopyotherwise,orrepublish,topostonserversortoredistributetolists,requires
priorspecificpermissionand/orafee.Requestpermissionsfrompermissions@acm.org.
©2022AssociationforComputingMachinery.
1550-4859/2022/1-ART$15.00
https://doi.org/xx.yyyy/zzzzzzz.aaaaaaa
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.
2202
guA
62
]IN.sc[
2v77041.6022:viXra

2 Álamosetal.
theapplicationlogic;aNetworkServer,whichcoordinatesaccesstothemediabetweennodes
androutestrafficbetweentheApplicationServerandEndDevices;andGateways,whichactas
thebackboneoftheLoRaWANnetwork.Thearchitecturepreventspeertopeercommunication
betweenenddevices,whichoperatewithoutnetworklayer.
LoRaWANdefinesthreeoperationalclasses(modes)thatshowatrade-offbetweendownlink
delayandpowerconsumption.WithclassA,thereceptionofdownlinkpacketsisonlypossible
duringashortintervalafteranuplinktransmission.Consequently,classAdevicesexhibitahigh
downlink latency, but the highest power efficiency. With class C, the end devices are always
listening.Thedownlinklatencyisconsequentlylowestatthecostofahighenergyconsumption.
InclassB,beacon-synchronizedenddeviceswakeupperiodicallyinordertobeabletoreceive
data.Thisclassprovidesagoodtrade-offbetweendownlinklatencyandpowerconsumption.
LoRaWANimposesaseriesoflimitations,whichmakeitimpracticalforscenarioswithhet-
erogeneouscommunicationpatterns.ToincreasetheLoRaversatilityaswellasitsefficiency,we
proposetheusageofIEEE802.15.4DSMEasaMAClayerforLoRa.DSMEisaflexibleMAClayer
introducedinthe802.15.4erevision(2012)thatprovidescommunicationincontention-access,as
wellascontention-free(time/frequencyslots).
Inthispaper,wewanttoanswertheresearchquestionofhowLoRacanbeintegratedwithsuch
aflexibleMAClayerandhowthisstackperformsinvarioussettings.Inparticular,wewantto
showhowLoRaendnodescanbeopenedupforhostingvariousnetworklayerssuchasstandard
IPordata-centricadaptations[32].Thecontributionsofthisarticleareasfollows.
(1) WepresentDSME-LoRa,asystemdesignofLoRawithIEEE802.15.4DeterministicSynchro-
nousMultichannelExtension(DSME)asaMAClayer.
(2) We evaluate in this work the performance of DSME-LoRa on real hardware, based on a
DSME-LoRaimplementation[5]onthepopularIoToperatingSystemRIOT[7].
(3) Weproposeanovelanalyticalstochasticmodeltopredicttransmissiondelayandthroughput
forDSMEslottedtransmission.
(4) Weperformalarge-scalesimulationofDSME-LoRanodestoassessthescalingbehaviorof
ourproposedsolution.
(5) Basedontheevaluationandmodelresults,wederivepreferredmappingsforimplement-
ing different transmission patterns, with a balance trade-off of energy consumption and
transmissiondelay.
Theremainderofthispaperisstructuredasfollows.Weoutlinetheshortcomingsofthecurrent
LoRaWANsystemalongwithaproblemstatementinSection2.Therelevantbackgroundonlow
powerradiocommunicationissummarizedinSection3.Section4presentsourDSME-LoRasystem
design,whichweevaluateonrealhardwareinSection5.Wedevelopananalyticalstochasticmodel
inSection6,fromwhichwepredicttheperpacketperformancefortheslottedtransmission.Peer-
wisecommunicationinlargeensemblesofLoRanodesissubjecttoasimulationstudyinSection7.
InSection8wediscussdesigndecisionsandoptionsforoptimization.Finally,wereviewrelated
work in Section 9 and give a conclusion and outlook in Section 10. The Appendix provides a
supplementaryfigure(AppendixA)andlistsatableofabbreviations(AppendixB)whichweuse
throughoutthisarticle.
2 PROBLEMSTATEMENT
ThecommonLoRaWANarchitectureaddsrigidconstraintstolong-rangenetworking,whichhinder
manyIoTdeployments.Itscentralizeddesignfacilitatesuplink-orientedapplications,butchallenges
datasharingandthecreationofdistributedapplications.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 3
Controller OptionalApp.Logic
Sensor
NS Actuator
GW
(a)LoRaWAN (b)Directcommunication
Fig.1. ControltrafficofsmartlightningscenarioinLoRaWAN(left)throughagateway(GW),anddirect
communication(right).
WearguethatdirectcommunicationbetweenLoRadevicesovercomestheselimitations,whileit
stillenablesreliablecommunicationinlong-rangedeploymentsorharshenvironments.Tofurther
motivatetheneedfordirectcommunication,weanalyzeanIoTcontrolscenarioforsmartlightning.
Sanchez-Sutiletal.[20]designaLoRasystemforsmartregulationofstreetlights(seeFigure1
(b))andproposeanarchitecturewithilluminationleveldevices(sensors),whichtransmitsensor
dataeveryminute.Agatewayforstreetlightssystem(controller),whichacquireilluminationdata
fromsensors,transmitcontrolmessagestoactuatorsandsendmeasurementdatafromstreetlights
tothecloud.Operatingandmonitoringdevicesforstreetlights(actuators)controllightleveland
transmitelectricalmeasurementstothecontrollers.Theauthorsdeployseveralscenarios(upto64
actuators)withalldevicesinLoRawirelessreach.
ALoRaWANimplementationofsuchsystemmaymovecontrollerlogictothecloudapplication
anduseLoRaWANtotransmitdatabetweensensorsandactuators(seeFigure1(a)).However,this
approachhasthefollowingdisadvantages:
(i)TrafficbetweencontrollerandactuatorisforcedthroughLoRaWANgateways.Ifcontrollers
transmit unicast control data every minute to all actuators, nearby gateways will forward 64
downlinkpacketsperminute.EveniftheLoRadevicesandtheLoRaWANNetworkServeragree
onthefastestdownlinkdatarate,asinglegatewayscenariowillrender7%dutycycle.Because
LoRaWAN gateways are half-duplex, packets received during downlink transmission are lost.
Therefore,suchadeploymentrequiresatleasttwodedicatedgatewaystoenableaDataExtraction
Rate(DER) 99%.InregionswithdutycycleregulationssuchasEU868,evenmoregatewaysare
≥
requiredtopreventadditionalpacketlossesasaresultofdownlinkbudgetdepletion.Addingmore
gatewaysaddressestheseproblems,butitincreasesdeploymentcostsanditisnotalwayspractical.
(ii)TheLoRaWANinfrastructurepreventsthedeploymentofedgedevicesandblindlyforwards
sensordatatothecloudinfrastructure.Tofurthermotivatetheusageofedgedevices,considera
deploymentinthecityofLondon( 2.8millionstreetlights).Ifsensorsareonparwithactuators
≈
andtransmiteveryminute,thecloudinfrastructurereceives1.5trillionLoRaWANmessagesper
year,whichartificiallyleadstoacostexplosionincloudinfrastructure.
(iii)DeviceswithpoorLoRaWANwirelesscoverageincreasetransmissiontimeonairtoimprove
linkbudget.Thisincreasesenergyconsumption[36],whichreduceslifecycleofnodes.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

4 Álamosetal.
(iv)Inmanyremoteareas,cellularnetworksaretheonlyuplinkoptionsforLoRaWANgateways.
PoorInternetconnectivitywillleadtopacketlossatthegateway,whichthreatenstheversatility
ofthecontrolsystem.
The proposed smart lightning topology (see Figure 1 (b)) overcomes the limitations of the
LoRaWANarchitecture.Insteadofusingacentralizedcontrollerinthecloud,thesystemimplements
low-costcontrollersthatrunthecontrollogicinadistributedway.Therefore,downlinktraffic
isdistributedbetweenmanycontrollerdevicesinsteadofaggregatingatafewgateways.This
effectivelyreducesdownlinkstress.Becausesensorsandcontrollersarelikelyinwirelessreach,
sensorscantransmitusingafastdatarate,whichfacilitatesbattery-poweredoperation.Controllers
cantransmitpreprocesseddataatalowerrate,whicheffectivelyreducescloudtransmissions
andinfrastructurecosts.Thesystemdoesnotinterruptcontroloperationincaseofintermittent
connectivity at controllers. In addition, controllers are free to implement caching strategies to
reducepacketlossonintermittentInternetuplinks.
Inthelightofthisusecase,wearguethataDSMEMACshouldperformbetterthantheproposed
systemfortworeasons:(i)DSMEenablesmultichanneltimeslottedcommunication,incontrastwith
thesinglechannelapproachofthesystem.Thisenablesconcurrentcollision-freecommunication
withoutspecialhardwarerequirements(e.g.,LoRaconcentrator).Therefore,controllersmaybe
implementedwithlowcostcomponents,whilestillmaintaininghighPacketReceptionRatio(PRR).
(ii) DSME offers powerful built-in features such as device discovery and security mechanisms,
whichfacilitatedeploymentandsecureoperation.
WefollowtheDSME-LoRadirectionintheremainderofthispapertofosterflexiblelong-range
node-to-nodecommunication.
3 BACKGROUNDONLOWPOWERRADIOS
3.1 IEEE802.15.4withDSMEMAC
TheDeterministicandSynchronousMultichannelExtension(DSME)initiatesabeacon-synchronized
superframestructurethatconsistsofabeaconslot,aContentionAccessPeriod(CAP)andaCon-
tentionFreePeriod(CFP).EnddevicescanchoosetocommunicateduringCAPorCFP.During
CAP,devicestransmitusingCarrierSenseMultipleAccess/CollisionAvoidance(CSMA/CA)in
a common channel. During CFP, end devices transmit in a dedicated time-frequency slot. The
CFPisdividedinthetimedomainintosevenmultichannelslots,namelyGuaranteedTimeSlot
(GTS).EachGTSisdividedinthefrequencydomainintothenumberofavailablechannelsinthe
channelpage(usually16).DSMEsupportsbothpeertopeerandclustertreetopologies.Similarto
traditionalIEEE802.15.4,therearethreedeviceroles:PersonalAreaNetwork(PAN)coordinator,
regularcoordinators,andchilddevices.Devicescantransmitconfirmedmessages,wheretheMAC
layerretransmitsframesincaseofmissedACKframe.Wesummarizetheconfigurationparameters
inTable1andintroduceinthereminderofthissection.
Networkformation.ThePANcoordinatoristhedeviceinchargeofdefiningthesuperframe
structure.Forthispurposethedevicewilltransmitenhancedbeaconsperiodically.Thetransmission
ofenhancedbeaconsalwaysoccursduringabeaconslotandtheperiodisamultipleofthesuperframe
duration.DevicesthatwanttojointheDSMEnetworkperformascanningproceduretodetect
enhancedbeacons.Whenthescanningproceduresucceeds,thejoiningdevicesendsanassociation
requesttothecoordinator.Theassociationfinisheswhenthecoordinatoracknowledgeswitha
positiveassociationreply.
TheDSMEnetworkcanbeextendednativelybyaddingmorecoordinators.Insuchcasethe
coordinatorwillemitenhancedbeacons usingthesameperiodasthePANcoordinatorbutina
differentbeaconslotoffset.Thisensuresmultiplecoordinatorscansharethesameareawithout
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 5
BS CAP CFP BS CAP CFP BS CAP CFP BS CAP CFP BS
Superframe
Multisuperframe
GTS
Beaconinterval
Fig.2. OverviewoftheDSMEMultisuperframetransmissionresources.
Table1. ListofMACconfigurationparametersfortheDSMEMAC.
Parameter Description
macMinBE Minimumbackoffexponent
macMaxBE Maximumbackoffexponent
macMaxCsmaBackoff No.ofaccessattemptsbeforedeclaringchannelfailure
macMaxFrameRetries No.offrameretransmissions.
macSuperframeOrder (SO) Describesthelengthofthesuperframeslot
macMultisuperframeOrder (MO) Describesthelengthofthemultisuperframe
macBeaconOrder (BO) Describesthelengthofthebeaconinterval
macCapReduction Opt.replaceCAPwithCFPinallsuperframesexceptfirst
macRxOnWhenIdle Opt.keepreceiveronduringCAP
riskofbeaconcollisions.Intheeventofbeaconcollisions(i.e.,twocoordinatorsstartedemitting
beaconsinthesameslotoffset),DSMEprovidesanativemechanismtoresolvecollisions.Tobeable
toswitchthecommonchannelandPHYproperties,thestandarddefinesthePHY-OP-SWITCH
mechanisminwhichneighbourdevicesareinstructedtoswitchtoadifferentPHYconfiguration
onreceptionofadedicatedMACcommand.Thisallowsdynamicswitchingbetweendatarates,
modulationsandfrequencybands.
Superframestructure. SuperframesmergeintoamultisuperframestructureasvisualizedinFig-
ure2.DSMEsupportsaCAPreductionmodeinthemultisuperframestructure(macCapReduction),
inwhichtheCAPperiodisreplacedby8CFPadditionalslotsinallsuperframesexceptthefirst.
Forexample,aconfigurationwithfoursuperframespermultisuperframeexposes28GTS(448
uniquetime-frequencyslots).WithCAPreduction,thesamestructureexposes52GTS(832unique
time-frequencyslots).
DSME defines three parameters to describe the superframe structure, namely Superframe
Order (SO), Multisuperframe Order (MO), and Beacon Order (BO) (compare Table 1). The su-
perframe order defines the slot duration as: aBaseSuperframeDuration 𝑇 2𝑆𝑂, where
𝑆𝑦𝑚𝑏𝑜𝑙
· ·
aBaseSuperframeDuration=60symbols,asperstandard.Asmallsuperframeorder,whichleads
toashortersuperframeduration,offersshorterlatenciesatthecostofhigherenergyconsumption
andsmallerpayload.SO=3enablesthetransmissionofstandard127bytes802.15.4frames.The
multisuperframeorder,togetherwiththesuperframeorder,definethenumberofsuperframes
permultisuperframeas2 𝑀𝑂 𝑆𝑂 .HighermultisuperframeordersleadtohigherGTSresources
( − )
withthecostofhigherlatencies.Finally,thebeaconordersetsthebeaconintervalto2 𝐵𝑂 𝑀𝑂
( − )
multisuperframes.Higherbeaconordersleadtohigherbeaconintervals,whichextendthenumber
ofpotentialcoordinatordevicesatthecostoflongerassociationtime.Thesethreeparameters
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

| 6   |     |     |     |     |     | Álamosetal. |
| --- | --- | --- | --- | --- | --- | ----------- |
Table2. NumberofavailableGTSwithandwithoutCAPreduction,andmultisuperframeduration(𝑇 )for
𝑚𝑠𝑓
varyingmultisuperframeorders(MO),withasuperframeorder(SO)of3andsymboltime1 ms.
| Multisuperframe |     | NumberofGTS        |     | NumberofGTS       |     | Duration |
| --------------- | --- | ------------------ | --- | ----------------- | --- | -------- |
| order(MO)       |     | (w/oCAPreduct.)[#] |     | (w/CAPreduct.)[#] |     | 𝑻 [𝒔]    |
𝒎𝒔𝒇
|                 | 3   |     | 7                                           |     | 7   | 7.68   |
| --------------- | --- | --- | ------------------------------------------- | --- | --- | ------ |
|                 | 4   |     | 14                                          |     | 22  | 15.36  |
|                 | 5   |     | 28                                          |     | 52  | 30.72  |
|                 | 6   |     | 56                                          |     | 112 | 61.44  |
|                 | 7   |     | 112                                         |     | 232 | 122.88 |
|                 | 𝑆𝑂  | 𝑀𝑂  | 𝐵𝑂                                          |     |     |        |
| mustcomplywith0 |     |     | 14.WesummarizethenumberofavailableGTSandthe |     |     |        |
|                 | ≤   | ≤ ≤ | ≤                                           |     |     |        |
multisuperframedurationfordifferentmultisuperframeordersforthecaseSO=3inTable2.
CSMA/CAtransmissions. OnscheduleofaCSMA/CAtransmission,theMACqueuesthepacket
intheCAPqueueandperformsslottedCSMA/CA,aimingtoavoidcollisionswhileaccessingthe
commonchannel.TheCSMA/CAalgorithmrequiresfourparametersdisplayedinthefirstfour
rowsinTable1.OntransmissiontheMACalignstothebackoffperiod,whichoccursevery20
symbolssincethestartoftheCAP,andwaitsarandomnumberofbackoffperiodsbetween0and
2macMinBE.IncasethedurationoftheremainingportionoftheCAPisshorterthantherequired
backoffperiods,theMACwaitsforthenextCAPperiodandcontinuesitscountdownaccordingly.
The MAC then performs a series of clear channel assessments (at least two), each one at the
beginningofabackoffperiod.Onfailure,theMACdoublesthebackoffperiod(below2macMaxBE)
andtheCSMA/CAalgorithmretriesuntilitsucceedsortheMACrunsoutofCSMA/CAattempts
(macMaxCsmaBackoff).Whensuccessfullyaccessingthechannel,theMACtransmitstheframeand
(optionally)waitsforanACKframe.IftheMACexpectsanACKframeanddoesnotreceiveit,the
MACrepeatstheCSMA/CAprocedureuntilitrunsoutofCSMA/CAattemptsorretransmissions
(macMaxFrameRetries).
DuringCAPtheMACcantransmitbothunicastandbroadcastframes.Inordertominimizethe
energyconsumptiononconstraineddevices,theMACoffersthemacRxOnWhenIdleconfiguration
parametertoturnoffthereceiverduringCAP.Thisdoesnotaffectoutgoingtransmissions,but
preventstheMACfromreceivingframes.Totransmitframestotheseconstraineddevices,the
standarddefinestheindirecttransmissionmechanism.Acoordinatorqueuesframesscheduledwith
indirecttransmissionandappendsthetargetaddresstothenextbeacon.Aconstraineddevicethat
findsitsaddressinthebeaconpollsthecoordinatorwithadatarequestcommand,andwaitsforan
ACKframewiththesubsequentdataframe.
GTS transmission. End devices that require communication with other devices during CAP
needtonegotiateoneormoreGTSwiththetargetdevice.DSMEprovidesanativemechanismto
negotiateslots—incontrasttoTimeSlottedChannelHopping(TSCH).DSMEGTSareunidirectional
(RXorTX)andonlysupportunicastframes.WhenadeviceAwantstoallocateoneorseveralslots
withdeviceB(coordinatororchild),itsendsaDSME-GTSrequestframeduringCAPtodeviceB.
Incasethedeviceacceptstheslot,itreplieswithaDSME-GTSresponseframeindicatingsuccess.
Finally,deviceAbroadcastsaDSME-GTSnotifyframetoindicatetheothernodeinreachaboutthe
newslotallocation.Alternatively,adevicecanallocateaslotduringtheassociationprocedure,by
sendingaDSMEAssociationRequestcommand.OnscheduleofGTStransmission,theMACqueues
thepacketintheCFPqueue,whichdividesintomultipleFIFOqueues,oneforeachdestination
deviceamongtheallocatedGTSresources.GTStransmissionssupporttwochanneldiversitymodes,
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 7
namelychanneladaptationandchannelhopping.Inchanneladaptationmode,asourcedevicemay
allocateGTSinasinglechannelorindifferentchannelsbasedontheknowledgeofthechannel
quality.Thesourcedevicerequestschannelqualityinformationtoadestinationdeviceusingthe
DSMELinkReportMACcommand.Therebydevicesagreeonadifferentchannelifthechannel
qualityispoor.Inchannelhoppingmode,eachGTShopsoverapredefinedsequenceofchannels.
DSME supports message priority for GTS transmissions. On the occurrence of a valid GTS,
theMAClayertransmitsfirsttheframeswithhighpriorityandthenregularframes,providinga
class-basedservicedifferentiation.
The802.15.4eamendmentintroducesthegroupACKfeature,inwhichacoordinatorreceiving
data from multiple senders transmits one group ACK frame to all nodes in a single slot of a
multisuperframe.Thelatestversionsofthestandarddonotincludethisfeature,butwediscussits
potentialusecasesforreducingtimeonairinSection8.3.
3.2 LoRamodulation
TheLoRamodulationutilizesthechirpspreadspectrumtechniquetotransmitdataoverthewireless
channel.Thistechniquedefinesalinearfrequencymodulatedsymbol,namelychirp,whichutilizes
theentireallocatedbandwidthspectrum.Asaresult,theLoRasignalisrobustagainstinterference
and multi-path fading, and enables transmission ranges of kilometers depending on the PHY
configuration.AninterestingpropertyoftheLoRamodulation,namelythecaptureeffect,allows
tosuccessfullydecodeaframeundercollisionifthepowerdifferencewiththecollidingframesis
largeenough.
LoRareliesontwoPHYparameters,namelybandwidthandspreadingfactor,whichdefinethe
symbolduration.Ahighersymboldurationrendersbetterreceiversensitivity,whichincreases
transmissionrangeatthecostofhighertimeonairandlowerPHYbitrate.Athirdparameter,
coderate,definestheredundancybitsencodedintheLoRatransmission.Similarly,thecoderate
trades-offtransmissionrangewithtimeonair.
TheLoRaPHYframeconsistofapreamble,usedtosynchronizethetransceivertotheframe;an
optionalLoRaPHYheader,whichencodespayloadlength,forwarderrorcorrectioncoderateand
thepresenceofapayloadCRCattheendofthePHYpacket;apayload,whichcontainsthePSDU;
andanoptionalpayloadCyclicRedundancyCheck(CRC).TheLoRapreambledefinesasyncword
attheend,withthepurposeofisolatingnetworksofLoRadevices.Forexample,LoRaWANsets
thesyncwordto0x34forpublicnetworksand0x12forprivatenetworks.
LoRadevicesaresubjecttoregionalSub-GHzregulationsthatimposerestrictionsonthetrans-
missionofLoRaframes.Theserestrictionscanbecategorizedin(i)dutycyclerestrictions,inwhich
atransmittermaynotexceedamaximumtimeoveranobservationperiod(usually1%oftime
overanhour);(ii)dwelltimerestrictions,inwhichthetransceivermaynotexceedamaximum
timeonasinglechanneland(iii)channelrestriction,inwhichthedevicemustswitchchannelson
consecutivetransmissionsortransmitoveraminimumnumberofchannels.
LoRatransceiverscandecodesignalsbelowthenoisefloor,whichrendersenergydetection
mechanismssuchasRSSIimpracticalfordetectingthepresenceofsignalsontheair.Tocircumvent
thisproblem,commonLoRatransceiversimplementaChannelActivityDetection(CAD)mechanism
tonotethepresenceofaLoRapreamblesignal.
An interesting feature of LoRa transceivers, which has not been exploited by LoRaWAN, is
Frequency-hoppingspreadspectrum(FHSS)transmission.Thisfeatureallowstorepeatedlyswitch
carrierfrequenciesduringradiotransmission,aimingtoreduceinterferenceandavoidinterception.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

8 Álamosetal.
802.15.4DSMEMAC
802.15.4frame 802.15.4channel CCA
Framemapping Channelmapping CCAmapping
LoRaframe LoRaPHYchannel LoRaCAD
LoRaRadio
aRoL-EMSD
Fig.3. DSME-LoRaarchitectureoverview.
4 DSME-LORASYSTEMDESIGN
TooperateLoRaradiosbelowDSMEwedefineaDSME-LoRaadaptation,basedonouroriginal
work[4],thatmaps802.15.4MACoperationstoLoRaoperations.Theadaptationlayerperforms
threetasks:(i)mappingof802.15.4channelstoLoRaPHYchannels.(ii)conversionof802.15.4
framestoLoRaframes.(iii)implementationof802.15.4ClearChannelAssessment(CCA)ontopof
theLoRadevice.Figure3depictsthesystemarchitecture.
Channel mapping. The adaptation layer maps 802.15.4 channels to LoRa PHY channels. For
thiswork,wedefineachannelpagewithsixteenLoRachannels(seeTable3)intheEU868[17]
region.Notethatthechannelpagemaydefinemorethansixteenchannels,aslongasthechannel
informationfitsintheMACframesthatcontrolGTSallocation.
In the EU868 region the duty cycle of a band limits the time on air of a transmitting device
toapercentagewithinonehourobservationperiod.For1%and10%bandsthedutycyclelimits
thecumulativetimeonair36sand360srespectively.Forexample,devicesina1%bandcannot
transmitaframeiftheactivesendtimeexceeds36sduringthelasthour.Notethatthedutycycle
ismeasuredperbandandnotperchannel.Ifadevicetransmitsinmultiplechannelsonasame
band,thedutycycleofeachchanneladdsuptothedutycycleoftheband.
AllchannelsutilizethesamePHYconfigurations:spreadingfactor7,bandwidth125kHzandcode
rate4/5,whichresultsinaPHYbitrate 5.5kbpsandasymboltimeof 1ms.Wechoosethese
≈ ≈
settingstoprovideabalancedtrade-offbetweentransmissionrange,timeonair,andthroughput.
Note that different sets of LoRa PHY settings can be encoded using different channel pages.
Therebydevicescanagreeondifferentchannelpages,usingthePHY-OP-SWITCHfeatureSec-
tion3.1,toincreasetransmissionrangeorincreasethechannelsforconcurrentPHYcommunication.
Wewillinvestigatethefeasibilityofthisproposalinfuturework.
DefiningLoRaPHYchannelsforotherregionsisviable,albeitchallenging.Wefurtherdiscuss
thissituationinSection8.3.
Wedefineonechannelinsidetheg3 band(10%dutycycle)andfifteenchannelsinsidetheg
band(1%dutycycle)with200kHzchannelspacing.Inordertorelaxdutycyclerestrictions,we
utilizethe10%bandchannelforbeacontransmissions,CAPchannel,andGTStransmissions.The
remainingchannelsareusedexclusivelyforGTStransmissions.
SincetheproposedchannelsoverlapwithLoRaWANchannels,wedefinethesynchronization
wordofthepreambleto0x17inordertoavoiddecodingofLoRaWANframes.Furthermore,we
includetheLoRaPHYheaderandpayloadCRCdescribedinSection3.2.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 9
Table3. DSME-LoRaPHYchanneldefinition,EU868frequencybandinformation,andpurpose.
| Channel Band | Frequency[MHz] | DutyCycle[%] |     | Purpose         |
| ------------ | -------------- | ------------ | --- | --------------- |
| 11-25 g      | 863.00–868.00  |              | 1   | GTStransmission |
Beacontransmission,
| 26 g3 | 869.40–869.65 |     | 10  | CSMA/CAtransmission, |
| ----- | ------------- | --- | --- | -------------------- |
GTStransmission
GNRC
|     | Application / Lower Network Stack |     |     | Pktbuf er |
| --- | --------------------------------- | --- | --- | --------- |
|     |                                   |     |     | API  uff  |
|     | GNRC NetAPI/Netreg                |     |     | B         |
et
|     |                 |     |     | GNRC k   |
| --- | --------------- | --- | --- | -------- |
|     | GNRC Netif DSME |     |     | Pktbuf c |
a
|     |     |     |     | API  P |
| --- | --- | --- | --- | ------ |
C
|     | DSME Adaption Layer API |     |     | R   |
| --- | ----------------------- | --- | --- | --- |
N
|     |                       |     | D S M E   | G N R C G   |
| --- | --------------------- | --- | --------- | ----------- |
|     | E DSME Adaption Layer |     |           | P k t b u f |
|     | M                     | M   | e ss a ge | A P I       |
S
|     | D MLME-SAP/MCPS-SAP | IDSMEMessage |     |     |
| --- | ------------------- | ------------ | --- | --- |
n
e
p O
DSME Layer
IDSMEPlatform
|     | DSME Platform |     |     | Our |
| --- | ------------- | --- | --- | --- |
contribution
|     | 802.15.4 Radio HAL | High-level Timer API |     | OpenDSME |
| --- | ------------------ | -------------------- | --- | -------- |
module
|     | LoRa Driver | Platform Timer |     | RIOT |
| --- | ----------- | -------------- | --- | ---- |
module
Fig.4. DSME-LoRaintegrationintothenetworkingsubsystemofRIOT.
Framemapping. Onframetransmissiontheadaptationlayercalculatesandappendsachecksum
totheMACframeandpassestheframetotheLoRatransceiver.Onframereception,thelayer
receivestheLoRaframefromthetransceiverandcalculatestheframechecksum.Onsuccess,the
layerdispatchestheframetotheMAClayer.Inordertotransmitfull127bytes802.15.4frames,
we set the superframe order to 3. The adaptation layer defines the MAC symbol time to 1 ms,
whichisinlinewiththeLoRasymboltimeforthechannelconfiguration.Withthissuperframe
orderconfigurationandsymboltime,thesuperframeslotdurationresolvesto0.48s.Hence,the
superframeduration(16superframeslots)is7.68s.Weleavethemultisuperframeandbeaconorder
configurationtotheapplication.
CCAmapping. OnCCArequestsfromtheMAClayer,theadaptationlayermapstotheLoRa
CADfeature,whichdetectsthepresenceofaLoRapreambleontheair.Onsuccessfuldetection,
thelayerreportschannelbusytotheMAClayer.Otherwise,thelayerassumesthechannelisfree
andreportsclearchannel.
4.1 DSME-LoRaimplementation
TheintegrationofDSME-LoRaonrealhardwareimposesaseriesofchallenges.(i)longtimeonair
ofLoRarequiresalongsuperframeslotduration,whichresultsinlongbeaconintervals.IoTdevices
arepronetoclockdriftfromcheapcrystals,whichincreasesthechancesofdesynchronization
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

10 Álamosetal.
betweenchilddevicesandcoordinators.(ii)commonLoRatransceiversdonotaddamechanismto
timestampframereception,whichisrequiredtosynchronizetimebetweenneighbour.(iii)DSME
accessesthetransceiverbasedoninterruptsduringcriticaloperations.Thisfacesconcurrentaccess
withhardwareserialperipheralbuses(e.g.,SPI)andlimitstheresponsivenessonrealtimeoperating
systems.(iv)commonLoRahardwareplatformsareconstrainedandhavelowmemoryresources.
ThisservesacommonLoRaWANstack.Incontrast,DSMErequiresadditionalmemoryduetothe
complexityoftheMAC.
WeintegrateopenDSMEintotheRIOTnetworkstack(GNRC),whichprovidesagenericmessag-
inginterface(GNRCNetapi),acentralizedpacketbuffer(GNRCPktbuf),andapacketdispatch
registry(GNRCNetreg).RIOTprovidesahighlevelplatformtimerAPIandahardwareabstraction
layerfor802.15.4devices.WefurtherextendopenDSMEtosupportthemacRxOnWhenIdlemode
(Table1),inordertoturnthetransceiveroffduringCAPandsaveenergy,whenCAPisnotused.
Figure4presentsthesystemintegrationofDSME-LoRainRIOTandourcontributions.
GNRCNetifDSME. implementstheGNRCnetworkinterfaceforDSME.Thisallows,viathe
GNRCNetapi:(i)transmissionofDSMEframes.(ii)configurationoftheDSMEMAC(devicerole,
staticslotallocation).(iii)scanningandassociationprocedures.WeusetheDSMEAdaptationLayer,
aconvenienceAPIprovidedbyopenDSME,toimplementtheMAClayerlogicbelowthenetwork
interface.TheinterfacedispatchestheincomingframesviatheGNRCNetreg.Inordertominimize
memoryconsumption,weutilizethecallbackextensionofGNRCNetregasanalternativetothe
defaultIPCimplementation.Thissavesanadditionalthreadforreception,whichheavilyreduces
RAMutilization.
DSMEMessage. implementstheDSMEMessageinterface(IDSMEMessage)whichabstractsthe
packetrepresentation.WeusetheGNRCPktbuftoimplementthepacketrepresentation.This
approachhasadvantagesonmemoryconsumption.(i)centralizedstoragepreventsdataduplication.
(ii)thescatteredpacketrepresentationofGNRCPktbufallowsappendingchunksofdatatoapacket
withoutmemoryreallocation.(iii)GNRCPktbufsupportsallocationwithmalloc.Thisfacilitates
theoperationofDSMEinthesamememorypoolasopenDSME,whichbasesonheap.
DSMEPlatform. implementstheDSMEPlatforminterface(IDSMEPlatform)whichdefinesthe
platformabstractionlayerofopenDSME.TheinterfaceimplementstheaccesstotheLoRatransceiver
ontopofthe802.15.4RadioHAL.Itfurtherimplementstheaccesstotimerfunctionalitiesofthe
operatingsystem.Thereby,weconfigurethehigh-leveltimertousethereal-timetimerperipheral,
aimingtomitigatetheeffectofclockdriftduetolongbeaconintervals.Wedelegatetheprocessing
oftransceiverinterruptsandsystemtimerstotheRIOTscheduler,inordertoavoidconcurrent
access to the system bus between the transceiver and operating system. The implementation
reconfiguresthesymboltimeoftheMAClayerto1ms(LoRa)incompliancewithSection4.
LoRaDriver. implementsa802.15.4compatibledriverfortheLoRatransceiver(SX1272/SX1276).
ThedriverimplementsthethreecomponentsoftheDSME-LoRaAdaptationLayer(Section4),
namelychannelmapping,framemappingandCCAmapping.Totimestampframereception,we
calculatethetimedifferencebetweenthepacketreceptioninterrupt(RxDone)andthevalidheader
interrupt(ValidHeader).Weusethistimedifferencetocalculatetheexactreceptiontimestampof
theframe.
Asaresultofthesedesigndecisions,ourDSME-LoRaimplementationconsumes 108kBof
≈
ROMand 12kBofRAMonARMCortex-M0CPU,whichisenoughforcommonLoRahardware
≈
platforms.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 11
Sourcedevices Sinkdevices
Fig.5. TopologyofaDSME-LoRanetworkwithsourceandsinkdevices.Onesinkdevicecanreceivefrom
multiplesources.
Fig.6. DeploymentofLoRaplatforms(B-L072z-lrwan1)ontheFITIoT-LABtestbed[3].
5 EVALUATIONONREALHARDWARE
WeevaluatetheDSME-LoRaimplementation(seeSection4.1)inapeertopeertopologywithsource
devices(TX-only)andsinkdevices(RX-only),asdepictedinFigure5.Duringourexperiments,
eachsourcedevicetransmitsdatawithexponentiallydistributedinterarrivaltimestoasinglesink.
Wevarythenumberofsourcedevices(N)andtheaveragetransmissioninterval.
Ourresultsincludethetransmissiondelay(timebetweenpacketscheduleandsuccessfulrecep-
tion),timeonairandenergyconsumptionfortransmissionsduringCAPandCFP.FortheCAP,
wefurtheranalyzetheimpactofCSMA/CAwithCADusingdifferentbackoffparameters.Wealso
evaluatetheimpactofcross-trafficbetweencoexistentDSME-LoRaandLoRaWANnetworksand
theeffectofinterferenceonDSME-LoRa.
5.1 Experimentsetup
Testbeddeployment. WeconductourexperimentsintheSaclaysiteoftheFITIoT-LABtestbed,
whichsupplies25LoRaboards(B-L072z-lrwan1).Thesearedistributedina12mby12mroom,as
showninFigure6.TheB-L072z-lrwan1platformconsistsofanARMCortex-M0CPU,whichruns
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

12 Álamosetal.
TXinterval=20s TXinterval=10s TXinterval=5s
1
0.8
0.6
0.4 N=5
N=10
0.2
N=15
0
1
0.8
0.6
0.4
0.2
0
0 20 40 60 80 0 20 40 60 80 0 20 40 60 80
FDC
CAP
CFP
Transmissiondelay[s]
Fig.7. TransmissiondelayforunconfirmedtransmissionsduringtheCAP(CSMA/CA)andCFP(GTS)witha
varyingnumber(N)ofsourcedevicesandtransmissionintervals.
at32MHz,provides192kBofROM/20kBofRAM,andcontainsaSX1276LoRatransceiver.The
testbedcontributesaserial_aggregator toolthataggregatesallUARToutputofthedeploymentand
addsatimestamp.Weaddloggingtoourmeasurementfirmwareforpacketschedule,transmission,
reception,andMACqueuelengthsandusethisinformationtocalculatetransmissiondelay,PRR,
andtimeonair.
Multisuperframestructure. WeconfigureDSMEtoonesuperframepermultisuperframe,which
results in a multisuperframe duration of𝑇 =7.68s. This configuration exposes 7 GTS over
𝑚𝑠𝑓
16 channels, which enables 112 unique time-frequency slots. We use a beacon interval of two
multisuperframeswhichresultsinabeaconperiodof15.36s.
Networktopology.Avariablenumberofsourcedevicestransmitsdatatothreesinkdevicesusing
directcommunication(gateway-less).ThismappingaccommodatessolelyGTStransmissionson
theproposedmultisuperframeconfiguration.Duringbootstrap,arandomsinkisassignedtoeach
sourcedevice.WeusestaticallocationforGTS.Withthat,weimitateGTSallocationduringdevice
associationwiththeDSMEAssociationRequestcommand(seeSection3.1).Wedeployanextra
devicethatoperatesasthePANcoordinator,thatestablishthesuperframestructurebytransmitting
enhancedbeacons.AlthoughanysinkorsourcedevicemayoperateasthePANcoordinator,weopt
forthisapproachtosimplifythedeployment.
MACconfigurations. Ifnotmentionedotherwise,weconfiguretheCSMA/CAbackoffparame-
terstomacMinBE=7,macMaxCsmaBackoff=5,macMaxBE=8(seeFigure3.1),whichareclosetothe
maximumvalues,inordertocopewithlongtimeonair.Section5.3furthercomparesthesevalues
to802.15.4defaultvalues.Inagreementwiththe802.15.4standard,wesetthemaximumnum-
berofretransmissionstomacMaxFrameRetries=4.WeutilizethechannelhoppingmodeforGTS
transmissions.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 13
5.2 DatatransmissioninCAPandCFP
Figure7showsthedistributionoftransmissiondelayforunconfirmedtransmissionsduringCAP
(CSMA/CA)andCFP(GTS),fordifferentnetworksizesandtransmissioninterval.Theintersections
betweeneachcurveandtherightaxisreflectthePRR
CSMA/CA transmission. The transmission delay increases with the network size and lower
transmissionintervals.Inbothcases,theon-airtrafficincreases,whichleadstoenhancedwireless
interference.Asaresult,theCCAprocedurefacesmoreoftenabusychannelwhichincrements
thenumberofCSMA/CAbackoffperiodspertransmission.Thiseffectincreasesthedelaybetween
packetscheduleandtheactualtransmissionandcausesahighertransmissiondelay.Similarly,
thePRRdecreaseswiththenetworksizeandlowertransmissionintervals.MultipleCCAfailures
enhancetheprobabilityofexceedingthemaximumnumberofCCAretries.TheMACdropsthe
packetinsuchcase,hence,itdecreasesthePRR.NotethatduetoinaccuraciesoftheCCAprocedure,
theMACtransmitsafractionofpacketsevenwhenthechannelisbusywhichdecreasesthePRR
marginally.WefurtheranalyzethiseffectinSection5.3.Highertransmissiondelaysincreasethe
CAPqueuestress,sincepacketshavetobebuffereduntiltheyareactuallysent.Hence,afraction
ofpacketlossesoccurduetoCAPqueueoverflows.Thestressedscenario(TXinterval=5s)reflects
thissituation,inwhichanincreasingnumberofsendersdecreasethereceptionratio.
GTStransmission. Thetransmissiondelayincreaseswithalowertransmissionintervalduring
CFP, but it does not vary with the network size. In contrast to the CSMA/CA scenario, each
sourcedevicetransmitsdataduringadedicatedtimeslotwhichrepeatsevery𝑇 7.68s.Inthe
𝑚𝑠𝑓
≈
adventofpacketqueuingforaparticularsinkdevice,thelastqueuedpacketdelaysuntiltheMAC
transmittedallprecedingframes.Asaconsequence,alowertransmissioninterval(TXinterval=5s)
increasesthetransmissiondelay,byincreasingtheaveragequeueoccupation–introducingMAC
queuestress.ThissituationexplainsalargertransmissiondelayinCSMA/CAthaninGTS,most
notableinscenarioswithTXinterval=5s/10s,evenwithhighbackoffexponentconfigurationfor
CSMA/CA.Notethatthenetworksizeonlyaffectsthenumberofallocatedtimeslotsduringone
multisuperframe.Consequently,thenetworksizedoesnotaffectthetransmissiondelayaslongas
asufficientnumberofGTSinthemultisuperframestructureexist.
Effectofretransmissions. Figure8comparesthedelayandPRRforconfirmedandunconfirmed
transmissionsduringCAPandCFP.ConfirmedframesundertransmissionstayintheMACqueue
untilthereceptionofavalidACKframe.Incaseofpacketloss,theMACretransmitsapending
frame until reception of the ACK frame or running out of retransmission attempts. Following
ourprecedingmeasurements,wevarytransmissionintervalsinanetworkoftensourcedevices.
ConfirmedtransmissionsduringCAPrevealahighertransmissiondelayinrelaxedscenarios(TX
interval=10s/20s),i.e.,90%ofconfirmedpacketsfinishwithin40s,whereasthesameamountof
unconfirmedpacketsfinishinlessthan20s.Therefore,thereceptionratioincreasesfrom95%to
100%withconfirmedtraffic.Inthestressedscenario(TXinterval=5s),thetransmissiondelayofthe
confirmedscenarioincreasesaswell,whilethePRRdecreasesincomparisontotheunconfirmed
scenario.Twocausesareworthstressing:(i)retransmissionsincreasetheon-airtraffic,whichleads
tocollisionsandahighnumberofCCAfailures;(ii)framesinretransmitoccupytheMACqueue
foralongertimeandaredroppedoccasionallyduetoCAPqueueoverflow.
IntheCFP,confirmedpacketsimprovethePRRbyonly 0.5%toachieve100%success.Similar
≈
to the CSMA/CA scenario, frame retransmissions increase the probability of packet reception,
however,sinceGTStransmissionsareexclusive,retransmitsarebarelyrequired.Therefore,the
contributionofframeretransmissionstoMACqueuestressisnegligible.Onlyafewretransmitted
frames slightly increase the transmission delay. This effect is notable in the scenario with TX
interval=10s.IncontrasttothestressedCSMA/CAscenario,thequeueloadinthestressedGTS
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

14 Álamosetal.
TXinterval=20s TXinterval=10s TXinterval=5s
1
0.8
0.6
0.4
Confirmed
0.2
Unconfirmed
0
1
0.8
0.6
0.4
0.2
0
0 20 40 60 80 0 20 40 60 80 0 20 40 60 80
FDC
CAP
CFP
Transmissiondelay[s]
Fig. 8. Comparison of transmission delays for confirmed and unconfirmed transmissions during CAP
(CSMA/CA)andCFP(GTS),fortensourcedevicesandvaryingtransmissionintervals.
scenario(TXinterval=5s)withconfirmedtransmissionsissimilartounconfirmedtransmissions.
Hence,thePRRdoesnotdecreaseanyfurther.
5.3 EffectofCADunderdifferentCSMA/CAconfigurations
Effect on collisions. We evaluate the collision avoidance capabilities of the CAD feature for
transmissionsduringtheCAPandcomparetotheALOHAprotocol,i.e.,randomizeddelaybefore
transmissions.Thereby,weutilizetwotimingparameterssetsforCSMA/CAwithCAPandthe
initialALOHAbackoff.
(1) HighBE:ourdefaultchoice(compareSection5.1)withmacMinBE=7,macMaxCsmaBackoff=5,
macMaxBE=8.
(2) StandardBE:802.15.4estandardvalues(forradiosthatoperateinthe2.4GHzband)with
macMinBE=3,macMaxCsmaBackoff=4,macMaxBE=5.
Figure 9 displays the fraction of packets that face a clear channel, collide, are dropped due to
maximumnumberofCSMA/CAreattemptsorqueueoverflow.Naturally,thelatteroptionsdonot
occurusingALOHA.IntheALOHAscenario(Figure9left),theresultsshowthatcollisionsincrease
withalowertransmissioninterval.Duetohighertrafficonair,thechancesofpacketcollision
increaseupto38%withtennodesandTXinterval=5sinthestandardBEscenario(Figure9,bottom
left).NotethatscenarioswithstandardBECSMA/CAsettingsshowhighercollisionratesthan
scenarioswithhighBEsettings(Figure9leftbottomvstop).Thehigherbackoffexponentincreases
theinitialTXdelay,hence,theaveragetransmissioninterval,andtherebyreducestheprobability
ofcollisions.Thenumberoftransmittedpacketsstaysconstant(100%)inallALOHAscenarios,
regardlessofinterferenceorbusychannel.ThisisbecausetheMACalwaysassumesafreechannel
attheendofthebackoffperiodandunconditionallytransmitstheframe.
ThenumberofcollisionsintheCSMA/CACADscenario(Figure9right),issmallerthaninthe
ALOHAscenarioandincreasesatalowerratewithalowertransmissioninterval.Incontrastto
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 15
ALOHA CSMA/CACAD
100
50
0
100
50
0
20 10 5 20 10 5
Clearchannel Collision
Drop(CSMA/CA) Drop(queueoverflow)
]%[stekcapdeludehcS
HighBE
StandardBE
TXinterval[s]
Fig.9. ProportionofCAPpacketsthatfaceaclearchannelontransmission,collide,oraredroppedby
CSMA/CA.ResultsareseparatedintohighBEandstandardBECSMA/CAconfigurationswithandwithout
CAD,fortensourcedevicesandvaryingtransmissionintervals.
ALOHA,thenumberoftransmittedpacketsdecreaseswithalowertransmissioninterval.This
isthepositiveeffectofchannelsensingindicatedbyCCAfailures,whichavoidssendingduring
ongoingtransmissionsonthechannel.PacketsthataredelayedduetoCCAremainqueuedand
theMACdropsapendingframeifCSMA/CArunsoutofretries.Thisdecreasesthenumberof
transmittedframesinastressfulscenario(CSMA/CAstandardBE,TXinterval=5s).Itisworth
notingthatCADisaffectedbyinaccuracies;itdetectsaclearchanneliftwonodesstartCSMA/CA
aboutsimultaneously.Asaresult,afractionofpacketscollidesdespiteCCA.SimilartotheALOHA
scenario,highBECSMA/CAsettingstriggerfewercollisionsthanstandardBEsettings.Areduction
intransmissionrateduetohigherbackoffdelaysrelaxesthechannel,though,anegativesideeffect
isadditionalCAPqueueloadwhichincreasespacketlossesduetooccasionalqueueoverflows
(CSMA/CAhighBE,TXinterval=5s).
Effect on transmission delay. The results in Figure 10 show that the transmission delay in
theCSMA/CAscenarioincreaseswithdecreasingTXintervals.Increasedchannelaccessfailures
withCSMA/CAdelaythetransmissions(untilCCAreportsclearchannel).Hence,theaverage
transmissiondelayincreases.IncreasingTXintervalswithALOHAdonotaffectthetransmission
delay,sincesendingisindependentofthechannelstate.ALOHAthereforesuffersfromwireless
interference.Inallcases,CSMA/CAleadstoahigherPRRthanALOHAtransmission.Although
CSMA/CAwithCADreducestheproportionoftransmittedpackets,thenumberofnon-transmitted
packets(whichavoidedacollision)issmallerthancollisionsupfront.Asaresult,thePRRincreases.
ScenarioswithhighBECSMA/CAsettingsrevealhigherpacketreceptionratios,asaresultof
reducedcollisionsandhighertransmissiondelayasaresultofhigherbackoffdelay.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

16 Álamosetal.
TXinterval=20s TXinterval=10s TXinterval=5s
1
0.75
0.5
0.25 HighBE
StandardBE
0
1
0.75
0.5
0.25
0
0 10 20 0 10 20 30 40 0 20 40 60 80
FDC
ALOHA
CSMA/CACAD
Transmissiondelay[s]
Fig.10. ComparisonoftransmissiondelaysbetweenCAPtransmissionswithCSMA/CACADandALOHAfor
tensourcedevices,withvaryingtransmissionintervalsandCSMA/CAbackoffexponent(BE)configurations.
Effectonretransmissions.Figure11analyzestheeffectofusingCADwhenenablingconfirmable
trafficandretransmissions.WecomparethePRRandtheaveragenumberofretransmissionsper
packet(Figure 11b)forboththeCSMA/CAwithCADandALOHAscenarios.ThePRRdecreases
withhigherTXintervalsandCSMA/CACADmeasurementsoutperformALOHA.Theeffectis
most notable in the stressed scenario (TX interval=5s) where the difference amounts to 8%.
≈
RetransmissionsremainrarewithCSMA/CAwhichindicatesthatlossesaremainlycausedby
avoidedtransmissionsinstressedcases.Nevertheless,CSMA/CAoutperformsALOHAintermsof
receptionratio.Incontrast,nodesretransmiteverypacketupto1.5x(onaverage)usingALOHA,
withoutimprovingpacketreception.Thisuselessamountofretransmissionsdemonstratesthe
advantageofCSMA/CAwithCAD.
5.4 Timeonairanddutycyclecompliance
TransmissiontimewithLoRaradiosislimitedbybandregulations.Weanalyzetheon-airtime
withrespecttoduty-cyclecompliance.AsdepictedinSection5.1,wesetuptopologiesinwhicha
variablenumberofsourcedevicessendsdatatothreesinkdevices.Theassignmentisuniformly
random.Sinkdevices,inturn,replywithanACKtoeveryincomingpacket.Notethatadataframe
contains27Bytesofdata,whereastheACKframecontainsonly5Bytes.DuetotheLoRaPHY
frameoverhead,however,theACKpackettakes 31msonair,whichisaroundhalfofthedata
≈
frame( 67ms).WesetupmostlystressedTXintervalstofosterdutycycleviolationsandpresent
≈
ourresultsofthetimeonairpernodeinFigure12.Thereby,thedashedgraylineindicatesthe
maximumonairtimetocomplywitha1%bandoccupationduringCFP.FortheCAPweutilizea
10%oftheband(seeSection4)whichisnotvisibleonthisscale.
CSMA/CAtransmission. Thetimeonairincreaseswithalowertransmissionintervalasaresult
ofahighertransmissionrateontheMAC(Figure 12atoplefttoright).FortheN=5case,thetime
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 17
| 100 |     |     |     | 2   | CSMA/CACAD |     |
| --- | --- | --- | --- | --- | ---------- | --- |
ALOHA
]#[.snarteR
75
]%[RRP
| 50  |     |     |     | 1   |     |     |
| --- | --- | --- | --- | --- | --- | --- |
25
| 0                       |               |     |     | 0                          |               |      |
| ----------------------- | ------------- | --- | --- | -------------------------- | ------------- | ---- |
|                         | 20            | 10  | 5   |                            | 20            | 10 5 |
|                         | TXinterval[s] |     |     |                            | TXinterval[s] |      |
| (a)Packetreceptionratio |               |     |     | (b)Retransmissionsperframe |               |      |
Fig.11. Packetreceptionratio(left)andaverageretransmissionsperframe(right)forfifteensourcedevices
andvaryingtransmissionintervals.
| TXinterval=10s |     | TXinterval=5s |     | TXinterval=10s |     | TXinterval=5s |
| -------------- | --- | ------------- | --- | -------------- | --- | ------------- |
| 80             |     |               |     | 80             |     |               |
| 60             |     |               |     | 60             |     |               |
CAP
| 40  |     |     |     | 40  |     |     |
| --- | --- | --- | --- | --- | --- | --- |
]s[rianoemiT
| 20  |     |     |     | 20  |     |     |
| --- | --- | --- | --- | --- | --- | --- |
| 0   |     |     |     | 0   |     |     |
| 80  |     |     |     | 80  |     |     |
| 60  |     |     |     | 60  |     |     |
CFP
| 40 1%           |     | 1%  |      | 40  | 1%            | 1%       |
| --------------- | --- | --- | ---- | --- | ------------- | -------- |
| 20              |     |     |      | 20  |               |          |
| 0               |     |     |      | 0   |               |          |
| N=5 N=15        |     | N=5 | N=15 | N=5 | N=15          | N=5 N=15 |
| (a)Sourcedevice |     |     |      |     | (b)Sinkdevice |          |
Fig.12. Timeonairofdataframesonsourcedevices(left)andACKframesonsinkdevices(right)compared
to1%bandlimitations(grayline).FramesaresentinCAP(CSMA/CA)orCFP(GTS)andwevarythenumber
ofsourcedevices(N)andtransmissionintervals.
almostdoublesfrom 20sto40swithhalftheTXinterval.Notethatweapplya10%bandtothe
≈
CAP,hence,on-airtimesofupto360spernodedocomplywithdutycyclerestrictions.
Our results further show that the average time on air of source devices decreases in larger
networks(Nincreases).TheeffectismostnotableinthescenariowithTXinterval=5s.Inthat
scenario, CCA fails more often due to higher on-air traffic, which persuades the MAC to drop
afractionofdataframes,eitherduetoexceededCSMA/CAattemptsoroverflowedCAPqueue
(seeSection5.3).ThecasewithN=15sourcedevicesdoesnotvaryonairtimewithvaryingTX
intervalsduetotheseMACdrops.
Inthecaseofsinkdevices,thetimeonairincreaseswithalowertransmissioninterval,similarly
tosourcedevices.Incontrast,though,thetimeonairalsoincreaseswiththenetworksize.ACK
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

18 Álamosetal.
100
95
90
Scenario
]%[RRP
Baseline
Withcross-traffic
Fig.13. ComparisonofPRRfortenDSME-LoRasourcedeviceswithandwithoutcrosstrafficfromaLoRaWAN
networkwithtenclassAdevices.Alldevicestransmitunconfirmedframeswith16bytespayloadanduniformly
distributedinterarrivaltimesbetween7and13s.DSME-LoRadevicestransmitduringCFP(GTS).
packetsaresentinresponsetoeveryincomingsourcedeviceframeanddonotutilizeCSMA/CA.
Due to our topology choice, a sink device has to return multiple ACK packets to satisfy all its
assignedsourcedevices.Consequently,ahighernumberofsourcedevicesleadstoahigherACK
frametransmissionratepersinkdevice,whichincreasesthetimeonairupto60sfor scenarios
withN=15sourcedevices.Thisisstillinlinewith10%restrictions.Notethattherandomsource-
sinkassignmentleadstoadifferentnumberofsourcedevicespersinkoneachscenario,which
introducesvariationsbetweentimeonairmeasurementsacrosssinkdevices.
SinkdevicessendmultipleACKpacketsbackbyback,contrastinga‘simultaneous’channel
accessofsourcedeviceswhichintroducedMACdropping.Overall,increasingtransmissionrates
havealesssevereimpactonnodedutycyclesthanincreasingnumberofnodesthattrytoaccess
themediumduringthesametimeperiod.
GTStransmission. TheaveragetimeonairofsourcedevicesincreaseswithalowerTXinterval,
whichisinagreementwithCSMA/CAtransmissions(Figure 12abottomlefttoright).OurCFPas-
signmentwithoneGTSpersource-sinklink,however,limitstheeffectiveTXintervalto𝑇 =7.68s
𝑚𝑠𝑓
in our multisuperframe configuration as described in Section 5.1. Note that this configuration
preservesdutycyclecompliancenatively.Sendinga67mslongpacketevery7.68sresultsin31.4s
active send time per hour, which is below the 1% regulation mark of 36s per device and hour.
Conversely,weintentionallychoseaverystressfulmeasurementsetupwithTXinterval=5s.
SimilartotherelaxedCSMA/CAscenario,theaveragetimeonairofsinkdevicesincreaseswith
alowerTXinterval(Figure 12bbottomlefttoright)duetoanincreasedframerate.Increasingthe
networksize,incontrasttoCSMA/CA,furtherincreasestheon-airtimesofsinkdevices.Observe
that the time on air exceeds 1% of duty cycle in scenarios with N=15. The reasons for this are
threefold.(i)Duetoourtopologychoice,eachsinkdevicehastoconfirmfivesourcepacketson
averageintheN=15scenario.Thisamplificationburdensthelinkbudgetofasinglesinkdevice.
Hence,wedeliberatelyviolatethedutycycleregulationsbyourexperimentsetup.(ii)Sinkdevices
onlysendACKframesbackbybackandwithoutCSMA/CA.Hence,sinkdevicestransmit100%of
thescheduledACKframes.(iii)GTStransmissionsutilizeguaranteedresources,whichincreases
thereceptionratioanddecreaseslossesincomparisontoCSMA/CAtransmissions.Asaresult,
the number of transmitted ACK frames is in line with the number of transmitted data frames,
regardlessofthenetworksize.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 19
5.5 CoexistencewithLoRaWAN
TheproposedDSME-LoRaPHYchannelsoverlapwithchannelsofLoRaWANnetworks.Therefore,
weareinterestedintheeffectsofLoRaWANcross-trafficinDSME-LoRanetworks.Forthisanalysis
wefocusonlyoncross-trafficbetweenGTStransmissionsandLoRaWANtrafficfortworeasons:(i)
thecommonCAPchanneldoesnotoverlapwithstandardLoRaWANuplinkchannels.(ii)LoRaWAN
downlinktrafficistypicallytransmittedusingahigherspreadingfactorandtherebydonotcollide
withDSME-LoRapackets.
Fortheevaluation,wedeployDSME-LoRaandLoRaWANnetworkssimultaneouslyandmeasure
thePRRoftheDSME-LoRanetwork.WecomparethesevaluesagainstthesameDSMEnetwork
withoutcross-traffic.
FortheLoRaWANnetwork,wesetuptennodeswithclassAtransmissionsandDR5(spreading
factor7,bandwidth125kHz).Thedeploymentusesasingle8-channelTTN[11]LoRaWANgateway,
availableinthetestbed.TheDSME-LoRanetworkconsistoftensourcedeviceswiththetopology
and configuration in agreement with Section 5.1. All devices transmit 16 bytes payload using
unconfirmedtransmissionsanduniformlydistributedinterarrivaltimesbetween7and13s.
Figure13showsthePRRoftheisolatedDSME-LoRanetwork(baseline)andthenetworkwith
LoRaWAN cross-traffic. With DSME cross-traffic, the PRR reduces 0.7%. From all available
≈
DSME-LoRachannels,onlysevenoverlapwithTTNLoRaWANchannels,whichmeans56.25%of
transmissionsarecollisionfree.Afractionoftheremainingpacketsistransmittedconcurrently
withDSME-LoRatransmissions,whichreflectthePRRreduction.TheLoRaWANtrafficdoesnot
collidewithDSMEbeaconsandtherefore,devicedesynchronizationasaresultofcollisionbetween
LoRaWANpacketsandDSME-LoRabeaconsisnegligible.EventhoughLoRaWANtrafficdegrades
PRRasaresultofconcurrenttransmissionsonsharedchannels,thecross-trafficdoesnotprevent
normaloperationoftheDSME-LoRanetwork.WeconcludethatDSME-LoRatrafficiscompatible
withstandardLoRaWANuplinktraffic.
5.6 Effectofinterferenceincommonchannel
Section5.5confirmedthatDSME-LoRanetworkstoleratechannelinterferenceinGTSchannels.
However,theresultsdonotreflecttolerancetonoiseinthecommonchannelusedforCAPand
beacontransmissions.WhilecommonLoRaWANdeploymentsintheEU868regiondonottransmit
inthe10%band(CAPchannel)usingthesamePHYsettingsasDSME-LoRa,theLoRaWANnetwork
serverdoesnotpreventtheconfigurationofadownlinkchannelusingspreadingfactor7,which
maycauseLoRaWANframestocollidewithDSME-LoRaframes.Sincesynchronizationtothe
DSMEsuperframestructurereliesonbeacons,weevaluatewhetherDSME-LoRacanoperateunder
noiseinthecommonchannel.WefocusonlyonGTStransmission,becausetheeffectofnoise
duringCSMA/CAtransmissionshasalreadybeenanalyzedinSection5.2.
Wegenerateaharshenvironmentbydeployingfivejammerdevicesthatsend127bytespayload
datainthecommonchannelwithuniformlydistributedinterarrivaltimesbetween1sand6s,next
totheDSME-LoRanetworkwithtensourcedevices.TheinterarrivaltimeofpacketsandtheMAC
configurationsoftheDSME-LoRanetworkareidenticaltothenetworkinSection5.5.
Figure14showsthemovingaveragePRRovertimeforthreereplicas(R1,R2andR3).ThePRR
ofallreplicasoscillatesaround92%beforeT=100s.AfterT=100sthePRRinR3reducesto 50%
≈
anddoesnotrecover.Similarly,aroundT=270sthePRRinR2dropsto 89%.Tounderstandthese
≈
results,observethatthecommonchannelisincludedasoneofthetransmissionchannelsinCFP.
Therefore,GTStransmissionsinthecommonchannelarelikelytocollidewithtrafficfromthe
jammers.Assuming 1 ofGTSvulnerabletransmissions(i.e.,onechannelgetsjammed),around
16
94%oftransmissionarecollisionfree.ThisreflectstheloweraveragePRRbeforeT=100s.ThePRR
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

| 20  |     |     |     |     | Álamosetal. |
| --- | --- | --- | --- | --- | ----------- |
100
80
]%[RRP
60
|     | 40 R1 |     |     |     |     |
| --- | ----- | --- | --- | --- | --- |
R2
20
R3
0
|     | 0 50 | 100 | 150 200 250 | 300 350 | 400 |
| --- | ---- | --- | ----------- | ------- | --- |
Time[s]
Fig.14. EvolutionofPRRforthreereplicasofaDSME-LoRadeploymentwithtensourcedevices,unconfirmed
GTStransmissionsandTXinterval=10s,underheavyinterferenceonthecommonchannel.
Table4. Energyconsumptionforeachsuperframeperiod.Passive(top)componentsrelatethemaintenance
ofthesuperframestructureundervaryingtransmissionsoptions.Active(bottom)componentsrelatetothe
actualdatatransmission.Staterelatestothefollowingcomponents.idle:deviceisreadyforoperationw/o
ongoingtransmissions,off:deviceisnotoperabletosaveenergy,TX/RX:transmission/receptionofframes.
|     | Period | State | AdditionalDescription | Energy[mJ] |       |
| --- | ------ | ----- | --------------------- | ---------- | ----- |
|     |        | RX    | Beaconsynchronization |            | 18.28 |
BeaconSlot(BS)
|     |     | RXoff | Inactivebeaconslot |     | 0.08 |
| --- | --- | ----- | ------------------ | --- | ---- |
evissaP
|     |     | RXidle | macRxOnWhenIdle=1 |     | 146.12 |
| --- | --- | ------ | ----------------- | --- | ------ |
CAP
|        |     | RXoff  | macRxOnWhenIdle=0   |     | 0.50  |
| ------ | --- | ------ | ------------------- | --- | ----- |
|        |     | TXidle | SingleGTSallocation |     | 2.20  |
|        | CFP | RXidle | SingleGTSallocation |     | 19.31 |
|        |     | RXoff  | NoGTSallocation     |     | 0.69  |
|        |     | TX     |                     |     | 12.04 |
|        | CAP |        | SingleCSMA/CATX     |     |       |
| evitcA |     | RX     |                     |     | 6.44  |
|        |     | TX     |                     |     | 11.27 |
|        | CFP |        | SingleGTSTX         |     |       |
|        |     | RX     |                     |     | 6.44  |
dropsinR2andR3arecausedbythedesynchronizationoftwosinkdevicesandasourcedevice,
respectively,asaresultofbeaconloss.WhentheMACmissesanumberofconsecutivebeacons(4
bydefault),thedevicedisassociatesandignoresalltransmissionrequestandGTSreceptionslots.
Therefore,incomingandoutgoingpacketsaresimplydiscarded.
Tosummarize,interferenceonasinglechannelreducestheefficiencyofGTStransmissions,but
doesnotpreventnormaloperation.Interferenceonthecommonchannel,however,increasesbeacon
loss,whichdesynchronizesdevicesfromcoordinators.Whileraisingthethresholdofconsecutive
missedbeaconscandelaydesynchronizationonsporadicinterference,itcannotsolvetheproblem.
Additionally, long time on air and long range of LoRa frames make wireless attacks plausible,
in which an attacker blocks beacon reception through channel jamming. We discuss potential
solutionstothisprobleminSection8.5.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 21
150
]Wm[rewoP
| 100 | 0   |     |     |     |     | 1   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     | SB  | CAP |     | CFP |     | SB  | CAP |     | CFP |     |
|     |     |     | 00  | 00  |     |     |     | 01  | 01  | S1  |
50
0
150
]Wm[rewoP
| 100 | 0   |     |     |        |     | 1   |     |     |        |     |
| --- | --- | --- | --- | ------ | --- | --- | --- | --- | ------ | --- |
|     | SB  | CAP | 10  | CFP 10 |     | SB  | CAP | 11  | CFP 11 | S2  |
50
0
| 150 |     | 2   | 4   | 6   |     | 8   | 10  | 12  | 14  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
]Wm[rewoP
Time[s]
| 100 | 0   | CAP |     | CFP |     | 1   | CAP |     | CFP |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     | SB  |     | 20  | 20  |     | SB  |     | 21  | 21  | S3  |
50
0
|     |     | 2   | 4   | 6   |     | 8   | 10  | 12  | 14  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Time[s]
Fig.15. PowerconsumptionduringonebeaconintervalwithtwomultisuperframesseparatedintoCSMA/CA
transmissions(top),GTStransmissionswithtransceiveroffduringCAP(middle)andGTSreceptionswith
transceiveroffduringCAP(bottom).
|     |     |     | CSMA/CA |       |     |     |     | GTS   |     |     |
| --- | --- | --- | ------- | ----- | --- | --- | --- | ----- | --- | --- |
|     | CCA |     | TX      | ACKRX |     | TX  |     | ACKRX |     |     |
]Wm[rewoP 150
100
TX
50
0
| ]Wm[rewoP | 150 |     | RX  | ACKTX |     | RX  |     | ACKTX |     |     |
| --------- | --- | --- | --- | ----- | --- | --- | --- | ----- | --- | --- |
|           | 100 |     |     |       |     |     |     |       | RX  |     |
50
0
|     | 0   | 50  | 100      | 150 | 0   |     | 50       | 100 | 150 |     |
| --- | --- | --- | -------- | --- | --- | --- | -------- | --- | --- | --- |
|     |     |     | Time[ms] |     |     |     | Time[ms] |     |     |     |
Fig.16. PowerconsumptionfortransmissionandreceptionofonepacketwithCSMA/CA(left)andina
guaranteedtimeslot(right).
5.7 Energyconsumption
We evaluate the power consumption on the target board using a digital multimeter (Keithley
DMM751071/2).Therefore,wesamplethecurrentconsumptionat100kHzandprovidetheboard
withanexternallystabilizedvoltagesupply.Ouranalysesareseparatedintopassiveandactive
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

22 Álamosetal.
consumption.Passiveconsumptionincludesthemaintenanceofthesuperframestructurewithout
datatransmission.Activeconsumption,incontrast,includesthetransmissionandreceptionofdata
andACKframesindifferentsuperframeperiods.Hence,thetotalconsumptionofanodeconsistsof
bothpassiveandactivecomponents.Figure15representsthepassivepowerconsumptionovertime
duringonebeaconintervalandthreetrafficoptions.Itisnoteworthy,though,thatweexemplary
includeactiveTX/RXspikesintheplot,forpresentativereasons.
(1) S1enablestransmissionduringCAP.Thisrequiresbothsenderandreceivertoenablethe
transceiverduringthatperiod(Figure15top).
(2) S2disablestheCAPtosavepowerandrepresentsthecaseforsendingdataduringoneGTS
(Figure15middle).
(3) S3issimilarto(2),however,itdisplaysdatareceptionduringoneGTS(Figure15bottom).
Figure 16 represents active power consumption for the sender and receiver of a frame with
CSMA/CA(usedintheCAP)aswellaswithoutchannelsensing(intheCFP).Table4integrates
thepoweroverdedicatedintervalsandpresentstheenergyconsumptionforpassive(toppart)and
active(bottompart)actions.Inthereminderofthissection,wewillfirstanalyzepassiveandactive
componentsseparately.Wethenevaluatethetotalenergyconsumptionandpresentourresults
inTable5.InallmeasurementconfigurationswesetthetransmissionintervaltoTXinterval=20s
andthepayloadsizeto16bytes.
Passive consumption (Table 4 top). During BS 0 the MAC turns the transceiver on for the
durationofthebeaconslot(0.48s),inordertoreceivethebeaconfromitscoordinator.Theenergy
forbeaconsynchronizationis18.28mJforCPUprocessing,listeningandreceiving(RX).During
BS theMACrepeatsthesuperframestructureandbeginswithanewinactivebeaconslot,reserved
1
forbeaconcollisionavoidance(seeSection3.1).TheMACkeepsthetransceiveroff(RXoff)during
thattimeandtheenergyconsumptionreducesto0.08mJ.
The MAC switches to the CAP after a beacon slot. In the S1 scenario (Figure 15 top), the
transceiver stays idle listening during CAP
00
for 3.84s (RX idle, macRxOnWhenIdle=1), which
consumes146.12mJ.Thishighconsumptionshowstheneedforbatterypowereddevicestoturn
thetransceiveroffduringCAP.
TheS2scenario(Figure15middle)reflectsthatthetransceiveristurnedoff(RXoff,macRx-
OnWhenIdle=0) during CAP
10
, as it reduces the consumption during CAP to 0.5mJ, only for
maintenancepurposes(i.e.,timers,interrupts,etc.).Thismakesthenode,however,unavailablefor
packetreceptionduringthatperiod.TheCFPfollowstheCAP(T=4.32s)andtheMACswitchesto
slotmode.WithoutaGTSallocation,thetransceiverstaysoff(RXoff)andasystemwake-upfor
internalhousekeepingrequires0.69mJ,whichissimilarlylowasthesleepmodeoftheCAP.In
thepresenceofanallocatedGTSTXslotintheCFP,theMACturnsthetransceiveron(TXidle)
beforetheGTSinordertopreparethenexttransmission.Anemptytransmissionqueuetriggers
theimmediateshutdownofthetransceiver,tosaveenergy.Thissituationreflectsthepowerpeak
inCFP (T=4.32),whichconsumesnomorethan2.20mJandcanbemitigatedbyslotdeallocation.
10
AnactualGTStransmissionisvisibleinCFP .
11
ScenarioS3(Figure15bottom)presentsthecorrespondingconsumptioninCFP toreceive
20
duringoneGTS.Here,theMACenablesthetransceiverduringonefullGTSduration(RXidle),
which requires 19.31mJ and provides a frugal alternative to the CAP receiver. An actual GTS
receptionontopofthebaselineisdisplayedinCFP .
21
Activeconsumption(Table4bottom). AtthebeginningofCSMA/CAtransmission(Figure16,
topleft),theMACwaitsforthedurationofthebackoffperiodandperformsthreeconsecutiveCCA
measureswhichconsumes0.73mJ.Onclearchannel,thetransceiverloadstheframeandperforms
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 23
Table5. Passiveandactiveenergyconsumptionperbeaconinterval[mJ],fortheCSMA/CAscenarioS1and
bothGTSscenariosS2&S3.
S1 S2 S3
Period Energy[mJ] Prop.[%] Energy[mJ] Prop.[%] Energy[mJ] Prop.[%]
BS 18.36 5.68 18.36 45.15 18.36 28.74
CAP
passive 292.23 90.45 0.99 2.43 0.99 1.55
active 11.12 3.44 0.00 0.00 0.00 0.00
CFP
passive 1.38 0.43 4.40 10.82 38.62 60.45
active 0.00 0.00 16.91 41.59 5.92 9.27
Total 323.09 100 40.66 100 63.89 100
theframetransmission(TX),whichconsumes9.07mJ,followedbyACKframereceptionat2.23mJ.
Intotal,thismakes 12.04mJforCSMA/CAtransmissionduringCAP.
≈
TheCSMA/CAreceiver(Figure16,bottomleft)consumes2.75mJforthebareframe,however,
awaitingtheturnaroundtimeandsendingtheACKbackconsumesadditional3.69mJ.Hence,pure
receiving(RX)requires6.44mJ,whichappearslowcomparedtotransmission.Ithoweverrequires
anactiveCAP,whichconsumes>20timesmoreenergy(seeTable4).
OntransmissionduringGTS(Figure16,topright),theMACloadstheframeintothetransceiver
buffer without a preceding CCA, immediately transmits, and receives an ACK. This total con-
sumptionof11.27mJoutperformstheCSMA/CAsenderslightly.Notethatthedeviceturnsoff
thetransceiveriftheMACqueueisempty,whichfurtherreducesthepassiveCFPconsumption
occasionally.
SimilartothereceptionduringCSMA/CA,thereceptionduringGTS(Figure16,bottomright)
turnsthereceiveronforthedurationoftheframe,delays,andtransmitstheACKframe,which
leadstothesameconsumption.Incontrast,however,GTSreceiverscanturnthetransceiveroff
duringCAP.
Total energy consumption. Table 5 presents the total energy consumption and proportions
duringBS,CAP,andCFP,forthethreescenariosinFigure15.Wenormalizetheconsumptionto
onebeaconintervalandpresentaveragevaluesfromtenmeasurements.Resultsareseparatedinto
passiveandactiveoperationsinalignmentwiththeprecedingmicroanalysis.Allthreescenarios
unsurprisinglyconsumethesameamountofenergy(18.36mJ)formaintainingthebeaconslot.
IntheS1scenarios,over90%oftheconsumedenergyaccountstopassiveCAPconsumption—for
keepingtheradioon—whereasonly 3.5%isusedforsending.SincetheCFPisnotactivelyused,
the overhead remains small (< 0.5% ≈ ). We also conducted measurements at the receiver side in
thisscenario,butthevariationremainsnegligible.Astheresultsdonotcontributetoadditional
insights,weexcludedtheseexperiments.TheoverallconsumptionforscenariosS2andS3behaves
similar.TheCAPremainsunusedtosaveenergy.Thus,onlythepassivecomponentconsumes1mJ
(<2.5%).TheGTSscenariossaveabout290mJoverS1.ThemainproportionisspentintheCFP.
ActivesendinginaGTS( 17mJ)ismoreexpensivethanreceiving( 6mJ).Conversely,turning
≈ ≈
onthetransceiverforaGTSduration( 39mJ)consumes4timesmoreenergythanschedulinga
≈
transmissionslotwithoutsending( 11mJ).Intotal,thisleadstoa50%higherconsumptionofthe
≈
GTSreceiverscenarioS3.ComparingS1toS2andS3,atotalconsumptionof323.09mJrevealsa
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

| 24  |     |     |     |     |     | Álamosetal. |
| --- | --- | --- | --- | --- | --- | ----------- |
Table6. ListofvariablesusedinourmodelforDSME-LoRa.
| Variable | Description           |     |     |     |     |     |
| -------- | --------------------- | --- | --- | --- | --- | --- |
| 𝐿 𝑡      | Packetsinqueueattime𝑡 |     |     |     |     |     |
( )
| 𝑇   | Timeattheendoftheslot𝑛 |     |     |     |     |     |
| --- | ---------------------- | --- | --- | --- | --- | --- |
𝑛
| 𝐿 𝑛   | Queuelengthat𝑇                   | 𝑛 ,equivalentto𝐿 |     | 𝑇 𝑛       |       |     |
| ----- | -------------------------------- | ---------------- | --- | --------- | ----- | --- |
|       |                                  |                  |     | ( )       |       |     |
| 𝑆     | Elapsedtimesincetheendofthela    |                  |     | sts lot(0 | 𝑆 <𝑇  | )   |
|       |                                  |                  |     |           | ≤ 𝑚𝑠𝑓 |     |
| 𝑁 𝑡,𝑠 | Numberofpacketsscheduledbetween𝑡 |                  |     | and𝑡      | 𝑠     |     |
| ( )   |                                  |                  |     |           | +     |     |
| 𝜆     | Transmissionschedulerate         |                  |     |           |       |     |
| 𝑇     | Durationofamultisuperframe       |                  |     |           |       |     |
𝑚𝑠𝑓
| 𝜌   | Systemutilization,definedas𝜆 |     |     | 𝑇 𝑚𝑠𝑓 |     |     |
| --- | ---------------------------- | --- | --- | ----- | --- | --- |
·
| 𝐷   | Numberofneighbouringdevices                      |     |     |     |     |     |
| --- | ------------------------------------------------ | --- | --- | --- | --- | --- |
| 𝐿 𝑡 | Numberofqueuedpacketswithdestinationtoneighbour𝑑 |     |     |     |     | 0,𝐷 |
𝑑
| ( ) |                | =(cid:205) | 𝐷 1𝐿  |     |     | ∈ [ ) |
| --- | -------------- | ---------- | ----- | --- | --- | ----- |
|     | bydefinition,𝐿 | 𝑡          | =−0 𝑡 |     |     |       |
|     |                | ( )        | 𝑑 𝑑 ( | )   |     |       |
]seirtne[eueuQ
𝐿 𝑁 𝑇 ,𝑆
𝑛 + ( 𝑛 )
𝐿
𝑛
S
|     | 𝑇   |      | 𝑡 𝑇 |     | 𝑇   |     |
| --- | --- | ---- | --- | --- | --- | --- |
|     | 𝑛   |      | 𝑛 1 |     | 𝑛 2 |     |
|     |     | Time | +   |     | +   |     |
Fig.17. QualitativeevolutionoftheMACqueueovertime:occupationgrowsonpacketschedulingevents
(green)andreducesatslotoccurrences(purple).
notableoverheadtotheGTSalternatives,whichrequire5-8timeslessenergy.StressduringCAP
(seeSection5.3)canfurtherworsentheenergyexcessforCSMA/CAreattemptsandretransmits.
Conversely,S1scenarios(i)arerequiredtoassociateslotsinS2andS3inareal-worddeployment
and(ii)enablesporadictransmissionswithoutassociationoverhead.Inpractice,however,mixed
scenarioscanbuildacompromisetofacilitatemoderateconsumptioninflexibledeployments.
6 ANALYTICALSTOCHASTICMODEL
An important measure for the feasibility of our solution is its performance under continuous
network load. To evaluate this, we introduce an analytical stochastic model, which allows to
calculatethestationaryprobabilitydistributionsoftheMACqueuelengthatanarbitrarytimeand
fortransmissionsduringCFP(GTS).OursymbolsandnomenclaturearesummarizedinTable6.
ThetemporalevolutionoftheMACqueueataDSME-LoRadeviceisvisualizedinFigure17.
Packetsarriverandomlyovertimeandareaddedtothequeue.Attheendofanarbitraryslot
𝑇 ,packetsaretransmittedandremovedfromthequeue.Correspondingly,thenumberofqueue
𝑛
entriesattheendofslot𝑛is𝐿 𝑛 ,while𝑁 𝑇 𝑛 ,𝑆 packetsareaddedinthetimespan𝑆 after𝑇 𝑛 .Ina
( )
| homogeneousprocess,𝑁 | 𝑇 ,𝑆  | isproportionalto𝑆. |     |     |     |     |
| -------------------- | ----- | ------------------ | --- | --- | --- | --- |
|                      | ( 𝑛 ) |                    |     |     |     |     |
6.1 AMarkovqueuingprocess
WemodelourDSME-LoRatransmissionsystemasasimpleMarkovqueuingprocess,Forthiswe
makethefollowingsimplifyingassumptions.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 25
|     | 𝑘   | 𝑘   |     | 𝑘   |     | 𝑘   |     | 𝑘   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     | 0   | 1   |     | 1   |     | 1   |     | 1   |     |
+
|     |     |     | 𝑘   |     | 𝑘   |     | 𝑘   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     | 0   |     | 0   |     | 0   |     |     |
...
|     | 𝐿   | 0   |     | 𝐿 1 |     | 𝐿 2 |     | 𝐿 3 |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     | 𝑘   |     | 𝑘   |     | 𝑘   |     |     |
|     |     |     | 2   |     | 2   |     | 2   |     |     |
|     |     |     |     | 𝑘   |     | 𝑘   |     |     |     |
|     |     |     |     | 3   |     | 3   |     |     |     |
𝑘
4
Fig.18. EmbeddedMarkovchain:Thequeueoccupation𝐿𝑖remainsconstantbetweenslots,ifonlyonepacket
arrives(𝑘1).Itincreasesby𝑖 1for𝑘𝑖 packetarrivals,anddecreasesfor𝑘0.
−
(1) packetsarriveindependently
|     |     |     |     |     |     |     |     | <1(𝜆 | < 1 |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- |
(2) exponentiallydistributedinterarrivaltimesbetweenscheduledpacketswith𝜌 )
𝑇𝑚𝑠𝑓
(3) MACqueuehasunlimitedcapacity
(4) unacknowledgedtransmissionsand100%packetreceptionratio
(5) transmissiontimeonairisneglected.
Westartbyconsideringtransfertoonlyoneneighbour(𝐷 =1).Thereafter,weextendthemodel
>1.WefurtheranalyzethissituationinSection6.4.
undermoderateconditionstoscenarioswith𝐷
OurMarkovqueuingmodelisshowninFigure18.Thestateofthequeue𝐿 isreducedbyoneat
𝑖
theendofeverytimeslot.Packetsarriverandomlyduringanytimeinterval𝑠 inthequeueofthe
systemandfollowaPoissonprocesswithparameter𝜆𝑠.Foracompletemultisuperframetime,let
usdenote
𝜌𝑖 𝑒 𝜌
|     |     |     |     | =𝑃  |              | =𝑖 = | −   |     |     |
| --- | --- | --- | --- | --- | ------------ | ---- | --- | --- | --- |
|     |     |     |     | 𝑘 𝑖 | 𝑁 𝑇 𝑛 ,𝑇 𝑚𝑠𝑓 | ·    |     |     |     |
|     |     |     |     |     | { ( )        | } 𝑖! |     |     |     |
theprobabilityof𝑖 packetsarrivingduringonemultisuperframe(𝜌 =𝜆 𝑇 denotesthearrival
· 𝑚𝑠𝑓
intensity,i.e.,systemutilization).ThenthetransitionarcsoftheMarkovmatrix𝑃 aredefinedby
|     |     |     |     |       |  𝑘 0   | i f j -i = - 1  |     |     | ( 1 ) |
| --- | --- | --- | --- | ----- | ------------- | --------------- | --- | --- | ----- |
|     |     |     |     |       | 𝑘 0 𝑘 1       | i f i= 0 , j =0 |     |     | ( 2 ) |
|     |     |     |     | 𝑃 𝑖,𝑗 | = +           |                 |     |     |       |
|     |     |     |     | [     | ]             |                 |     |     |       |
|     |     |     |     |       |  𝑘 𝑗 𝑖 1 | i f j i         |     |     | ( 3 ) |
|     |     |     |     |       | − +           | ≥               |     |     |       |
|     |     |     |     |       | 0             | o th e rw ise   |     |     | ( 4 ) |

Theprobabilityofaqueuereductioncorrespondstonopacketarrival(Equation1),ofagrowth
by(j-i)toj-i+1packetarrivals(Equation3),andaconstantinitialconditiontoeithernoneorone
packetarriving(Equation2).
6.2 Queuelength
Forcalculatingtheactualqueueoccupation,wenotethatthenumberofqueuedpacketsatan
| arbitrarytimeis𝐿 |     | 𝑡   | =𝐿  | 𝑁 𝑡 𝑆,𝑆 | ,asseeninFigure17. |     |     |     |     |
| ---------------- | --- | --- | --- | ------- | ------------------ | --- | --- | --- | --- |
|                  |     | ( ) | 𝑛   | + ( −   | )                  |     |     |     |     |
Consequently,thedistributionofqueuelengthisgivenas
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

| 26  |     |     |      |     |     |     |        |     |     | Álamosetal. |     |
| --- | --- | --- | ---- | --- | --- | --- | ------ | --- | --- | ----------- | --- |
|     |     | 𝑃 𝐿 | 𝑡 =𝑖 | =   | 𝑃 𝐿 | 𝑁 𝑡 | 𝑆,𝑆 =𝑖 |     |     |             |     |
𝑛
|     |     | {   | ( ) | }   | {   | + ( − | )   | }   |     |     |     |
| --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- |
𝑖
∑︁
|     |     |     |     | =   | 𝑃   | 𝐿 =𝑖 | 𝑗,𝑁 | 𝑡 𝑆,𝑆 | = 𝑗 |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --- | ----- | --- | --- | --- |
|     |     |     |     |     |     | { 𝑛  | − ( | −     | ) } |     |     |
𝑗=0
𝑖
∑︁
|     |     |     |     | =   | 𝑃   | 𝐿 =𝑖 | 𝑗 𝑃  | 𝑁 𝑡   | 𝑆,𝑆 = | 𝑗   | (5) |
| --- | --- | --- | --- | --- | --- | ---- | ---- | ----- | ----- | --- | --- |
|     |     |     |     |     |     | { 𝑛  | − }· | { ( − | )     | }   |     |
𝑗=0
Wefirstderivearesultfor𝑃 𝑁 𝑡 𝑆,𝑆 =𝑖 .Notethat𝑃 𝑁 𝑡 𝑆,𝑆 =𝑖 𝑆 =𝑠 isaPoissonian
|     |     |     | {   | ( − | )   | }   |     | { ( − | )   | | } |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- |
withparameter 𝜆 𝑠 and𝑆 isuniformin 0,𝑇 .Thereforewecancalculate𝑃 𝑁 𝑡 𝑆,𝑆 = 𝑗
𝑚𝑠𝑓
|     | (   | · ) |     |     | (   | )   |     |     |     | { ( − | ) } |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- |
viathelawoftotalprobability:
∫
|     | 𝑃   | 𝑁 𝑡 𝑆,𝑆 | =   | 𝑗 = | ∞   | 𝑃 𝑁 𝑡 | 𝑆,𝑆 | = 𝑗 𝑆 =𝑠 | 𝑃 𝑆  | =𝑠 𝑑𝑠 |     |
| --- | --- | ------- | --- | --- | --- | ----- | --- | -------- | ---- | ----- | --- |
|     |     | { ( −   | )   | }   |     | { (   | − ) | |        | }· { | }     |     |
0
|     |     |       |       |     | ∫ 𝑇𝑚𝑠𝑓 |     | 𝑗𝑒 𝜆𝑠 |     |     |       |     |
| --- | --- | ----- | ----- | --- | ------ | --- | ----- | --- | --- | ----- | --- |
|     |     |       |       |     |        | 𝜆𝑠  | −     | 1   | 1   |       |     |
|     |     |       |       | =   |        | ( ) |       | 𝑑𝑠  | = Γ | 𝑗 1,𝜌 | (6) |
|     |     |       |       |     |        | 𝑗!  | ·𝑇    |     | 𝜌   |       |     |
|     |     |       |       |     | 0      |     |       | 𝑚𝑠𝑓 | ·   | ( + ) |     |
|     |     | ∫ 𝑥𝑡𝑗 | 1𝑒− 𝑡 |     |        |     |       |     |     |       |     |
whereΓ 𝑗,𝑥 = 0 − istheregularizedlowerincompletegammafunction.
∫
|     | ( ) | ∞𝑡𝑗 − | 1𝑒 − 𝑡 |     |     |     |     |     |     |     |     |
| --- | --- | ----- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
0
Forthecalculationof𝑃 𝐿 𝑛 =𝑖 ,observethat𝐿, 𝑖 𝑖 0, isaMarkovchain(Figure18),for
|     |     |     | (   | )   |     |     | ∀ ∈ [ | ∞)  |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- |
whichwesearchthestationarydistribution.WealsoobservethattheMarkovchainisergodic
(positiverecurrentandaperiodic).Thus,thestationarydistribution𝜋 =lim 𝑃 𝐿 =𝑖 exists
|     |     |     |     |     |     |     |     |     | 𝑖   | 𝑛 𝑛   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- |
|     |     |     |     |     |     |     |     |     |     | → ∞ ( | )   |
andcomplieswith𝑃𝑇𝜋 =𝜋.Thecalculationofaclosed-formanalyticalsolution f or𝜋 isnot trivial.
|     |     | (cid:174) | (cid:174) |     |     |     |     |     |     | 𝑖   |     |
| --- | --- | --------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
WedescribeadetailednumericproceduretocalculatethevectorinAppendixA.
CombiningthestationarydistributionoftheMarkovchainandEquation6intoEquation5leads
tothedistributionofqueuelength:
|     |     |     |     |       |     | ∑︁ 𝑖 | Γ 𝑗   | 1,𝜌 |     |     |     |
| --- | --- | --- | --- | ----- | --- | ---- | ----- | --- | --- | --- | --- |
|     |     |     |     | 𝑃 𝐿 𝑡 | =𝑖  | = 𝜋  | 𝑖 𝑗 ( | + ) |     |     |     |
|     |     |     |     | { (   | ) } |      | −     | 𝜌   |     |     |     |
𝑗=0
It is possible to calculate the average queue length directly. Observe that𝐸 𝐿 𝑡 = 𝐸 𝐿
𝑛
|               |     | =(cid:205) |      |         |     | ∫ 𝑇𝑚𝑠𝑓 |     |        | 𝜌   | ( ( )) | ( ) + |
| ------------- | --- | ---------- | ---- | ------- | --- | ------ | --- | ------ | --- | ------ | ----- |
| 𝐸 𝑁 𝑆 ,where𝐸 |     | 𝐿          |      | 𝑖𝜋 and𝐸 | 𝑁   | 𝑆 =    | 𝜌   | 1 𝑑𝑡 = | .   |        |       |
| ( ( ))        |     | ( 𝑛 )      | 𝑖∞=0 | 𝑖       | ( ( | )) 0   | 𝑇𝑚  |        | 2   |        |       |
𝑠𝑓
Therefore
𝜌
∑︁∞
|     |     |     |     |     | 𝐸 𝐿 𝑡 | =   | 𝑖𝜋    | .   |     |     | (7) |
| --- | --- | --- | --- | --- | ----- | --- | ----- | --- | --- | --- | --- |
|     |     |     |     |     | ( (   | ))  | 𝑖 + 2 |     |     |     |     |
𝑖=0
6.3 Transmissiondelay
Wenowcalculatethedistributionoftransmissiondelayinmultiplesof𝑇 fromthedistribution
𝑚𝑠𝑓
ofqueuelength:
|     |     |     |     | 𝑃 𝑊 | 𝑛𝑇  | =𝑃  | 𝐿 𝑡 | 𝑛 1 |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
𝑚𝑠𝑓
|     |     |     |     | {   | ≤   | } { | ( ) ≤ | − } |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- |
Asanexample,thefractionofpacketswithtransmissiondelaylessthanonemultisuperframeis
| 𝑃 𝐿 𝑡 | 0 =𝜋 | 1 𝑒− 𝜌 |     |     |     |     |     |     |     |     |     |
| ----- | ---- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0 −𝜌
| { ( ) ≤ | }   |     |     |     |     |     |     |     |     |     |     |
| ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Little’sLaw[41]𝐿 =𝜆𝑊 calculatestheaveragenumberofqueueditems(L)usingthearrival
rate(𝜆)andaveragewaitingtimeW.Weusetheresulttocalculatetheaveragetransmissiondelay
directly
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 27
(cid:32) (cid:33)
1 1 ∑︁∞ 𝜌
𝑊 = 𝐸 𝐿 𝑡 = 𝑖𝜋 (8)
𝑖
𝜆 ( ( )) 𝜆 + 2
𝑖=0
6.4 AllocationofmultipleGTS
So far the model assumes only one neighbour device (𝐷 = 1) and the allocation of only one
slot.Themodel,however,isstillvalidfor𝐷 > 1ifeachtargetdeviceallocatesonlyoneslotper
multisuperframe.Insuchcase,theMACutilizesthequeueasmultipleindependentFIFOsub-queues
(𝐿 ).Asaresult,themodelisvalidforeachsub-queueandthedistributionofthetotalqueuelength
𝑑
is:
(cid:40) (cid:41)
𝐷 1
∑︁−
𝑃 𝐿 𝑡 =𝑖 =𝑃 𝐿 𝑡 =𝑖
𝑑
{ ( ) } ( )
𝑑=0
Notethattheaveragequeuelengthisthesumofallaveragesub-queuelengthandtheaverage
transmission delay the fraction of the average queue length and the total schedule rate (Little
equation).
Theproposedformulas,however,ceasetoholdiftheMACallocatesmorethanoneslottothe
sameneighbour.Nevertheless,𝐷 =1setstheworstcasescenariofortransmissiondelayandqueue
lengthoverthesescenarios.
6.5 Validationofthemodel
Wevalidatethemodelaccuracyforthedistributionofqueuelengthandtransmissiondelay.We
chosetheGTStransmissionscenariowiththehighestrateoftransmittedpackets,namelywith15
sourcedevices,inorderminimizetheeffectofthetransientqueue.Wedonotincludethescenario
withTXinterval=5s,becauseitisshorterthanthemultisuperframeduration(7.68s).Insuchcase
the model does not converge. For the calculation of theoretical results we clipped the Markov
matrixto100elements.
InFigure19wevalidateourmodelbycomparingtoexperimentalresults(seeSection5).Fig-
ure 19acomparestheprobabilitymassfunctionofthequeuelengthatpacketschedulebetweenthe
resultsoftheexperimentsandthemodel.Themodelpredictsthedistributionofqueuelengthwith
morethan99.99%ofaccuracy.Intherelaxedscenariotheprobabilityofmorethanfiveelementsin
thequeueis6.17 10 5,whichisconsistentwiththeobservationthatthequeuedoesnotexceed
−
·
thisvalue.Similarly,themodelpredictsthetransmissiondelaywithanaccuracyof99.99%,asseen
inFigure 19b.
Thesmallvariationsbetweentheexperimentresultsandthemodelareduetotheeffectofthe
transientqueueandasmallfractionofpacketlosses.Theformereffectmitigateseitherwitha
biggernetworksizeorwithalongerexperimentrun.
7 SIMULATIONSTUDY:ASSESSMENTOFLARGESCALEENSEMBLES
WeproceedtoevaluatetheperformanceofDSME-LoRaforalargernetworksusingtheINET[28]
/OMNeT++[63]basedonoursimulationenvironment[4].Thesimulatorutilizestheradiomodule
ofFLoRa[60]andtheOMNeT++adaptationofopenDSME[31],namelyinet-dsme,fortheMAC
implementation.Weextendinet-dsme toenableDSMEcommunicationovertheLoRaradio,as
showninFigure20.Wereusethetrafficgeneratorapplicationofinet-dsme,namelyPRRTrafGen,
whichbasesontheIpvxTrafGentrafficgeneratormoduleofINET.WeutilizethenextHopmodule
ofINETtoresolveL3addressfrompacketsintothedestinationMACaddress.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

28 Álamosetal.
| 1   |     | 1   |     |
| --- | --- | --- | --- |
Experiment
| 0.8 |     | 0.8 |     |
| --- | --- | --- | --- |
Model
| FMP 0.6              | FMP      | 0.6                  |          |
| -------------------- | -------- | -------------------- | -------- |
| 0.4                  |          | 0.4                  |          |
| 0.2                  |          | 0.2                  |          |
| 0                    |          | 0                    |          |
| 0                    | 5 10     | 0                    | 5 10     |
| Queuelength[#]       |          | Queuelength[#]       |          |
| 1                    |          | 1                    |          |
| 0.8                  |          | 0.8                  |          |
| 0.6                  |          | 0.6                  |          |
| FDC                  | FDC      |                      |          |
| 0.4                  |          | 0.4                  |          |
| 0.2                  |          | 0.2                  |          |
| 0                    |          | 0                    |          |
| 0 20                 | 40 60 80 | 0 20                 | 40 60 80 |
| Transmissiondelay[s] |          | Transmissiondelay[s] |          |
| (a)TXinterval=20s    |          | (b)TXinterval=10s    |          |
Fig.19. Validationoftheanalyticalstochasticmodelwithexperimentalresults.Comparisonofdistributions
ofthequeuelengthandtransmissiondelayforvaryingtransmissionintervals.
Application Trafficgenerator
L3addressresolver
openDSME
FLoRa
inet-dsme
|     | DSMEMAC | Ownextension |     |
| --- | ------- | ------------ | --- |
DSME-LoRa
INET
OMNeT++
LoRaRadio
Fig.20. DSME-LoRasimulationenvironmentandourcontribution.
7.1 Validationofthesimulationenvironment
Tovalidateoursimulator,wefirstcomparesimulationresultswithreal-worldmeasurementson
hardware(seeSection5).Inparticular,Figure21comparessimulationresultsandourexperiments
conductedinSection5.2.InCSMA/CAtransmissions,afractionofcollidedpacketsaresuccessfully
decoded(captureeffect).Thefractionofpacketsvariesbetweenthesimulationandtheexperiment,
which lead to a different number of retransmissions and dropped frames by the MAC. In GTS
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 29
TXinterval=20s TXinterval=5s
1
0.8
N=5
0.6 N=5(sim)
N=10
0.4
N=10(sim)
0.2 N=15
N=15(sim)
0
1
0.8
0.6
0.4
0.2
0
0 10 20 30 0 50 100 150
FDC
Transmissiondelay[s]
CAP
CFP
Fig.21. Comparisonoftransmissiondelaysfromsimulationsandexperimentsforconfirmedtransmissions
duringCAP(CSMA/CA)andCFP(GTS).Wevarythenumber(N)ofsourcedevicesandthetransmission
interval.
transmissions,thecollisionfreetransmissionrendershighreceptionratioforMACtransmissions
inthesimulation.Intheexperiment,inpractice,atinyfractionoftransmittedframesislost,which
increasethenumberofretransmissions.Overall,theresultsofthesimulatorconvergewiththe
experimentsresults.Differingbehaviorbetweenthephysicalchannelandthesimulationchannel
modelexplainsmallvariations.
7.2 Largescalepeertopeercommunication
WeevaluatethetransmissiondelayandpacketreceptionratioofconfirmedCSMA/CAandGTS
transmissions,forvaryingnetworksizes(N=100andN=300)andvaryingtransmissioninterval
(Figure 22). In agreement with Figure 5.1, we use high backoff exponent settings to minimize
packetcollision.ToaccommodateoneslotforeverysourcedeviceduringCFP,weconfigurethe
multisuperframe order to 5, which renders 28 GTS and a multisuperframe duration of 30.72s
(Table2).Figure22presentsourresults.
CSMA/CAtransmission..Ourresultsshowthatthesmallnetwork(N=100)rendersa95%packet
receptionratiointherelaxedscenario(Figure22,topleft).Thehighon-airtrafficduetothenetwork
sizeincreasespacketcollisionsandCCAfailurerates,asanalyzedinSection5.Asaresult,afraction
ofpacketislost.Withhalfofthetransmissioninterval(Figure22,bottomleft),thesmallnetwork
reducesthepacketreceptionratioto 60%,asaresultofthehigheron-airtraffic.
≈
Scenarioswithbignetworksrenderanevenhigheron-airtime,whichreflects 38%packet
≈
receptionratiointherelaxedscenario(Figure22,topleft,N=300)and 14%inthestressedscenario
≈
(Figure22,bottomleft).ThisconcludesthatCSMA/CAisnotreliableforlargescaledeployments.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

30 Álamosetal.
CAP CFP
1
0.8
0.6
0.4
N=100
0.2
N=300
0
1
0.8
0.6
0.4
0.2
0
0 2 4 6 8 0 50 100 150 200
FDC
TXinterval=80s
TXinterval=40s
Transmissiondelay[s]
Fig.22. Comparisonoftransmissiondelaysforrelaxedandstressedscenarios,duringCAP(CSMA/CA)and
CFP(GTS),forconfirmedtransmissionsandavaryingnumber(N)ofnodes.
Observer that the transmission delay of the majority frames do not exceed 10s even in the
stressedscenario(Figure22,bottomleft,N=300).Thisvaluereflectstheworstcasetransmission
(maximumCSMA/CAretriesandmaximumframeretransmissions).Thedelayintheworstcaseis
lowerthantheTXintervalinbothCAPscenarios.Therefore,thestressintheCAPqueueislow,
hencethetransmissiondelay.
GTStransmission..Intherelaxedscenario(Figure22,topright),thetransmissiondelayhitsthe
maximumvalueat 120sinbothnetworksizes,asaresultofthedelayofqueuedpackets.As
≈
perSection5,thetransmissiondelaydoesnotvarywiththenetworksizes,becausealldeviceshave
equalGTSresources(oneslotpermultisuperframe).Incontrast,inthestressedscenario(Figure22,
bottomright)thetransmissiondelay,asaresultofthehigherMACqueuestress,hitsthemaximum
at 500s(notshowninthesubfigure).Similartotherelaxedscenario,thetransmissiondelaydoes
≈
notvarywiththenetworksize.
Thepacketreceptionratiohits 100%inallGTSscenarios,asaresultoftheslotallocation.
≈
TheresultsreflecttherobustnessofGTStransmissionsoverCSMA/CA,whichmakeitsuitablefor
largescalescenarios.WefurtheranalyzethisinSection8.1.
7.3 Impactofthemultisuperframeduration
Weanalyzetheeffectofthemultisuperframedurationontheaveragequeuelengthandtransmission
delayontransmissionsduringCFP.Figure23showstheresultsoftheanalyticalstochasticmodel
(Section6)forqueuelength(left)andtransmissiondelay(right)ofunconfirmedtransmissions
duringCFP,fordifferentmultisuperframeconfigurationsandtransmissionintervals.Theresults
showthattheaveragequeuelengthincreaseswiththemultisuperframeorder.Anincrementof
onemultisuperframeorderduplicatesthenumberofsuperframespermultisuperframe,ergothe
multisuperframeduration.Withafixedtransmissionintervalthissituationincreasesthesystem
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 31
| 40            | 0.12 0.31 | 1.66 |     | 1.5           | 40  | 4.75 12.47 | 66.21 |     |     |
| ------------- | --------- | ---- | --- | ------------- | --- | ---------- | ----- | --- | --- |
| ]s[lavretniXT |           |      |     | ]s[lavretniXT |     |            |       |     |     |
100
| 80  | 0.05 0.12 | 0.31 | 1.66 |     | 80  | 4.25 9.5 | 24.94 | 132.41 |     |
| --- | --------- | ---- | ---- | --- | --- | -------- | ----- | ------ | --- |
1
| 160 | 0.03 0.05 | 0.12 | 0.31 |     | 160 | 4.03 8.5 | 19.01 | 49.87 | 50  |
| --- | --------- | ---- | ---- | --- | --- | -------- | ----- | ----- | --- |
0.5
| 320 | 0.01 0.03         | 0.05 | 0.12 |     | 320 | 3.93 8.07               | 16.99 | 38.02 |     |
| --- | ----------------- | ---- | ---- | --- | --- | ----------------------- | ----- | ----- | --- |
|     |                   |      |      | 0   |     |                         |       |       | 0   |
|     | 3 4               | 5    | 6    |     |     | 3                       | 4 5   |       | 6   |
|     |                   | MO   |      |     |     |                         | MO    |       |     |
|     | (a)Queuelength[#] |      |      |     |     | (b)Transmissiondelay[s] |       |       |     |
Fig.23. Queuelength23aandtransmissiondelay23bforvaryingtransmissionintervalsandmultisuperframe
orders.Invalidconfigurationsaremarkedwithhatches.
utilization(𝜌 =𝜆 𝑇 𝑚𝑠𝑓 ),whichreflectsthehigherqueuelength.Thequeuelengthsinthediagonals
·
areequal,asaresultofequalsystemutilization.
Observethatvariationsinthequeuelength,asaresultofvariationsinthesystemutilization,are
higherasthesystemutilizationapproaches100%,asdepictedinFigure24.Thisreflectsinthehigher
queueutilizationintheupperrightcorner(Figure 23a).TransmissionswithTXinterval=40sand
multisuperframeorderof6(𝑇 𝑚𝑠𝑓 =61.44s)areoutoftheconvergenceregion,hence,theyarenot
showninthefigure.
Figure 23breflectsthatthetransmissiondelayistheproductbetweenthetransmissioninterval
andtheaveragequeuelength,asseeninSection6.3.Theincreaseinqueuelengthonvarying
multisuperframereflectsintheincreasedtransmissiondelayonhighermultisuperframeorders.
Note that equal queue lengths reflect different transmission delays, as a result of the longer
multisuperframeduration.
We use the model to calculate the worst case scenario of queue length for a given system
utilization(Figure24).Wedefinetheworstcasescenarioasthemaximumqueuelengthwitha
confidenceof99.9%.Theresultsshowthatthequeuelengthintheworstcasescenarioincreases
linearlyuntilasystemutilizationof60%,fromwherethequeuelengthgrowsexponentially.The
queuelengthexceedsthemaximumofopenDSME(22frames)at𝜌 =85.6%.Weusethisvalueto
𝑚𝑎𝑥
calculatethethroughput(𝜆 )foreachmultisuperframeorder,giventhat𝜌 =𝜆 𝑇 .We
|     |     | 𝑚𝑎𝑥 |     |     |     |     | 𝑚𝑎𝑥 | 𝑚𝑎𝑥 | 𝑚𝑠𝑓 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
·
comparethethroughputresultsfromthemodelagainstsimulationenvironmentresults(Table7).
Themodelshowthemaximumthroughput(401.24packets/hour)withMO=3.Observethatan
incrementinMOhalvesthemaximumthroughput(Table7,secondcolumn,toptobottom).This
is required to maintain the maximum system utilization (85.6%), because an increment in MO
duplicatesthemultisuperframeduration(Table2),Themodelshowsadeviationoflessthan0.02%
withrespecttothesimulation.
8 DESIGNDISCUSSIONS
Basedontheevaluationresultsandtheanalyticalstochasticmodel,wecannowdiscussoptimal
transmissionpatternsfordifferentscenariosandtrade-offsbetweendifferentsuperframeconfigu-
rations.Wealsocomparedesignoptionstocomplywithlocalregulationsandimprovetheenergy
consumption.Finally,wediscussDSME-LoRaoperationundercross-traffic.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

32 Álamosetal.
| ]#[htgneleueuQ |     | Queuesizelimit |     |     |     |     |
| -------------- | --- | -------------- | --- | --- | --- | --- |
timilecnegrevnoC
20
𝜌𝑚𝑎𝑥
Average
10
Max(p=99.9%)
0
| 0 10 | 20 30 | 40 50 | 60  | 70  | 80 90 | 100 |
| ---- | ----- | ----- | --- | --- | ----- | --- |
Systemutilization[%]
Fig.24. Averageandmaximumqueuelengthforvaryingsystemutilizationcases(𝜌).
Table7. Comparisonofthroughput(𝜆𝑚𝑎𝑥)usingresultsfromtheanalyticalstochasticmodelandsimulation,
forGTStransmissionwith85.6%systemutilization(maximumqueuelength),forsingleGTSallocationand
varyingmultisuperframeorders.
𝑝𝑎𝑐𝑘𝑒𝑡𝑠
| MultisuperframeOrder |     | Throughput[ |     | ] Error[%] |     |     |
| -------------------- | --- | ----------- | --- | ---------- | --- | --- |
ℎ𝑜𝑢𝑟
|     |     | Model  | Simulation |     |       |     |
| --- | --- | ------ | ---------- | --- | ----- | --- |
|     |     |        |            |     | 2.5 3 |     |
|     | 3   | 401.24 | 401.25     |     | 10 −  |     |
·
|     | 4   | 200.58 | 200.62 |     | 1.9 10 2 |     |
| --- | --- | ------ | ------ | --- | -------- | --- |
|     |     |        |        |     | · −      |     |
|     | 5   | 100.29 | 100.31 |     | 1.9 10 2 |     |
−
|     |     |       |     |       | · 3      |     |
| --- | --- | ----- | --- | ----- | -------- | --- |
|     | 6   | 50.15 |     | 50.16 | 2.5 10 − |     |
·
8.1 Analysisondatatransmission
OurevaluationrevealsdifferentpropertiesforCSMA/CAandGTStransmissions.Ontheonehand,
CSMA/CAtransmissionsinlowon-airtrafficshowlowertransmissiondelaysthanGTStransmis-
sionsandsimilarpacketreceptionratio.Inhighon-airtrafficscenarios,CSMA/CAfailuresand
packetcollisionsincreasetransmissiondelaysandsharplyreducespacketreception,whichrender
CSMA/CAtransmissionunusableforperiodiccommunicationinlargescalenetworks.Confirmed
transmissionsimprovethepacketreceptionratioforCSMA/CA,butincreasestransmissiondelay.
Ontheotherhand,GTStransmissionsadmit 100%packetreceptionratiosandtransmission
≈
delaysfortransmissionintervalsbelowthemaximumsystemutilization,(85.6%ofthemultisu-
perframeduration, seeSection 7.3). Thedelay ofGTS transmissiondepends onlyon the MAC
queuelengthatthemomentofpacketscheduling.Forapplicationsthatrequireclass-basedservice
differentiation,prioritylevelofDSMEtransmissionshaspotentialstoreducetransmissiondelayof
highprioritymessages.Thenetworksizedoesnotaffecttransmissiondelaynorpacketreception
ratiofordevicesinanetworkthatallocateaGTS.IncontrasttoCSMA/CA,unconfirmedtransmis-
sionsinGTSperformsimilartoconfirmedtransmissions.Hence,werecommendtouseconfirmed
transmissioninGTSonlyforhighprioritydata.
Duetothedeterministicbehaviorandveryhighpacketreceptionratio,GTStransmissionisa
betteralternativethanCSMA/CAtransmissionsforreliablelargescaleunicastcommunication.
However, CSMA/CA transmissions are still important for two reasons: (i) CSMA/CA support
broadcastframetransmissions.ThismakesCSMA/CAtransmissionseffectiveforapplicationwhere
asmallgroupofdevicesbroadcastsdatatomultiplereceivers,suchasfirmwareupdatescenarios.We
leavetheevaluationofbroadcasttransmissionsforfuturework.(ii)theCAPisusedfortransmission
ofMACcommandsrequiredforassociationandslotallocation.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 33
GTS
0
GTS 2 GTS 1 GTS 1 GTS 0
GTS 3 GTS 0 GTS 1 GTS 2 GTS 3
GTS
4 GTS
7 GTS
0
GTS 5 GTS 6 GTS 0
GTS
1
(a)Startopology (b)Peer-to-peertopology
Fig.25. GTSassignmentbetweenneighbourdevicesforstartopology(left)andpeer-to-peertopology(right)
TooptimizeCSMA/CAtransmissions,werecommendtheusageofsmallCSMA/CAbackoff
exponentsettingsforscenarioswithlowon-airtraffic,aimingtoreducetransmissiondelay.On
theotherhand,werecommendahighbackoffexponenttoincreasethepacketreceptionratiofor
higheron-airtraffic,inordertoincreasePRR.
IncommonLoRaWANdeployments,theadditionofgatewaysincreasesPRRbyexploitingthe
captureeffect(seeSection3.2).Onframecollision,afractionofLoRaWANgatewayscanstillrecover
aframeifthepowerdifferencewiththecollidingframesislargeenough.Duetothegateway-less
natureofDSME-LoRa,itisnotpossibletoincreasePRRofunicastframesbyaddingmorereceivers.
However,thecaptureeffectcanimprovedeliveryofbroadcastframes,inwhichagroupofdevices
successfullydecodethebroadcastframedespitecollision.Forexample,devicesataclosedistance
toacoordinatormaystillsuccessfullydecodebeaconsunderLoRacross-trafficinterference.
WeshowthatCADimprovestheperformanceofCSMA/CAtransmissionsbyreducingcollisions,
whicheffectivelyincreasesPRRandreducesframeretransmissions(Figure5.3).Thelatternotonly
reducethetimeonairofdevices,butreducesenergyconsumption.Webelieveitispossibleto
reducecollisionsevenfurtherbyutilizingamoresophisticatedCSMA/CAmechanismsuchas
LMAC[21].
8.2 Selectionofmultisuperframeconfiguration
OurevaluationshowsthatsmallermultisuperframeordersdecreasethedelayofGTStransmissions.
However,thisreducestheGTSresources(Table2).AlthougheachGTSdefinesmultipleunique
frequencyslots,adevicecanonlyallocateonefrequencyslotperGTS.Thislimitsthenumberof
GTSlinksperdevicetothenumberofGTSinthemultisuperframestructure,whichinturnfavors
cluster-treeandpeertopeertopologiesoverstartopologies.
ConsiderthetwoexampletopologiesfromFigure25with9devices.Inthestartopology(Fig-
ure 25a)eachchilddeviceallocatesatransmissionGTSwiththecoordinator.Inthepeer-to-peer
topologyeachdeviceallocatesatransmissionGTSwithanotherdeviceofthenetwork.Thestar
topologyrequires8GTS,oneperchilddevice,toestablishalllinks.Hence,thesuperframestructure
requiresatleasttwosuperframespermultisuperframe,whichsetsthemultisuperframedurationto
atleast15.36s.
Ontheotherhand,thepeer-to-peertopology(Figure 25b)allowstransmittingframesinthe
sameGTS,usingdifferentchannels.Asaresult,only4GTSareneededtoschedulealltransmissions.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

34 Álamosetal.
104
103
102
101
100
0 20 40 60 80 100 120 140 160 180 200 220 240 260 280 300
Sourcedevicespersink[#]
𝑠𝑡𝑒𝑘𝑐𝑎𝑝
]
[etarnoissimsnarT
𝑟𝑢𝑜ℎ
10%band
1%band
Fig.26. Maximumtransmissionrateofasourcedevicethattransmitsconfirmeddata(16bytespayload)toa
singlesink(startopology),forvaryingnumberofsourcedevicesinthenetworkanddutycycle
Therefore,aconfigurationwithonesuperframepersuperframesuffices,whichsetsthemultisuper-
framedurationto7.68s.Underthesamedatatransmissionrates,thepeer-to-peertopologyreflects
shorter transmission delays than the star topology, as a result of the shorter multisuperframe
duration.Incontrasttothestartopology,thepeer-to-peertopologydoesnotuseallavailableGTS
resources,whichallowstofurtherextendthenetwork.
Forscenarioswithmorethantwosuperframespermultisuperframe,theCAPreductionmech-
anismoffersasolutiontoextendtheGTSresources,inwhichtheCAPofallsuperframesina
multisuperframe,excludingthefirst,isreplacedby8GTS.However,thisreducestheCAPtimeofa
multisuperframe,whichstressesCSMA/CAtransmissionsandtherebychallengesdynamicGTS
allocation.WewillanalyzetheimpactofCAPreductiononslotallocationinfuturework.
8.3 Compliancewithregionalregulations
Regionswithdutycyclerestrictions. WeshowinSection5.4thatunconfirmeddatatransmis-
siontoneighbouringnodesdoesnotstressthetimeonairresourcesofthenetworkinregions
withdutycyclerestrictions,becausetransmissionsdonotrequireanintermediateforwarder(in
contrasttoLoRaWAN).ThismakesDSME-LoRasuitableforscenarios,inwhichaseriesofdevices
communicatedirectlywithoneormoresinkdevices(seeSection2).Ontheotherhand,confirmed
transmissionsstresstimeonairresourcesofsinkdevices(Section5.4).Itisthereforecrucialto
limitthetransmissionintervalforscenarios,inwhichasinkdevicereceivespacketsfrommultiple
sourcedevices,toensurecompliancewithdutycyclerestrictions.
WeshowinFigure26thetheoreticallimitsoftransmissionratepersourcedeviceasafunction
ofsourcedevicesthattransmittoasinglesink(startopology).Weassumethatsourcedevicesdo
notretransmitdata(100%packetreceptionratioonfirsttransmission).Forexample,astartopology
with10sourcedevicesallowstransmissionof 100packetsperhourinthe1%bandand1,000
≈
packetsperhourinthe10%bandwithoutexceedingthedutycyclerestriction.Ontheotherhand,
anetworkwith115sourcedevicesallowsinthe1%and10%bandstransmissionratesof10and100
packetsperhour,respectively.
CSMA/CAtransmissionsbenefitfromthe10%band.Nevertheless,themajorityofchannelsin
CFPbelongtothe1%band,whichrestrictsdatatransmissionsonsourcedevicesandACKframes
on sink devices. We propose two potential solutions to overcome these limitations (i) use the
groupACKfeature(Section3.1),whichrestrictsACKtransmissiontoonecommonACKframe
permultisuperframe.GroupACKsdonotcontributetobetterperformanceoverregularACK[45],
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 35
2
1
0
3 4 5 6 7
Beaconorder
]Wm[rewoP
CAP+CFPperiod
Beaconslot
Fig.27. PassiveconsumptionofsuperframestructurewithtransceiveroffduringCAP(macRxOnWhenIdle=0),
forvaryingbeaconorder.
butreducethetimeonairutilizationofsinkdevicesbyremovingthedependencytothenumber
ofsourcedevices.(ii)distributetheDSME-LoRachannelsinmorebands.Forexample,channels
11–25(seeTable3)canbearrangedintotwelvechannelsinthegband,twochannelsintheg1
band(868.0–868.6MHz)andonechannelintheg4band(869.7–870.0MHz).IfGTStransmissions
distributeevenlyamongchannels.Thisallowsfor 20%additionaltransmissionsperdevice.
≈
Regionswithdwelltimeorchannelhopping.Dwelltimerequirements(e.g.,inUS902–928
)canbeeasilyaddressedbyrestrictingpayloadsize,however,thechannelhoppingrequirement
(e.g.,inUS902–928andCN779–787)isincompatiblewithsinglechannelcommunicationduring
CAP.Whileontheonehand,limitingCAPtransmissionsintheseregionsisnotanoption,because
CAPisrequiredforslotallocationandMACcontroltraffic,enablingmultichannelCAP,onthe
otherhand,wouldrequiredevicestolistenonmultiplechannels(e.g.,byusingaLoRaconcentrator).
Althoughfeasible,itincreasesdeploymentcosts.
WearguethatFHSStransmissions(seeSection3.2)canenabletransmissionsduringCAPforthese
regions.Inthisregard,thechannelnumbermaydictateauniqueFHSSsequence.Thisaddresses
theproblemofchannelhoppinganddwelltime,sincetransmissionsarespreadamongdifferent
carrierfrequencies.Therebythetransmissiontimeperchannelisreduced.Still,itdegradesCCA
performance,becauseCADcandetectonlyonecarrierfrequencyatatime.Therefore,theCCA
implementationrequiresadifferentstrategy.Wewilladdressthisprobleminfuturework.
8.4 Energyconsiderations
Onstandarddeployments,thepassiveconsumptionofCAPis146.12mJpersuperframe(19.02mW)
and therefore not a good option for battery powered devices. To overcome this problem, we
proposedtoturnofftheCAPinbatterypowereddevices,asshowninSection5.7.Althoughthis
preventsframereception,theindirecttransmissionfeature(Section3.1)providesamechanismto
communicatewithadevicewiththereceiveroffduringCAP.Ontheotherside,adevicecanstill
turnonthetransceiverduringCAPtotransmitdatatootherdevices.Thisallows,forexample,to
triggerGTSRXallocationfrombatterypowereddevice.
WeshowinSection5.7thatthebeaconperiodhasahighimpactintheenergyconsumption.
Awaytoimprovethissituationistoconfigureahigherbeaconorder,whichresultsonahigher
beaconintervalandthereforereducesthepassiveconsumptionofthebeaconslot.Weestimate
thepowerconsumptionfromthemeasurementsinSection5.7andpresentthebaseconsumption
(superframestructure)fordifferentbeaconorderconfigurationsinFigure27.
Noteworthy,thebeaconorderhasahighimpactontheenergyconsumption.Inthescenariowith
BO=3,thetotalpassiveconsumptionhits2.73mW,inwhichthebeaconperiodconsumes 87%.
≈
OnthecontraryinscenarioswithBO=7thepowerconsumptionis0.49mW,inwhichthebeacon
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

36 Álamosetal.
Table8. Comparisonofaveragetransmissiondelay,power,andlifetimeforaDSME-LoRasenderdevicewith
TXinterval=15mandBO=7,forvaryingmultisuperframeorder.
MultisuperframeOrder Delay[s] Power[mW] Lifetime[y]
3 3.87 0.58 1.82
4 7.81 0.47 2.24
5 15.9 0.42 2.53
6 32.97 0.39 2.71
7 71.16 0.38 2.81
periodconsumes 30%oftheenergy.NotethatBO=7rendersthebeaconperiodto 122.88s–in
≈ ≈
linewiththedurationofLoRaWANclassBbeaconperiod(128s).
Inherently,higherbeaconintervalshavetwopotentialproblems:Thescanningproceduretakes
longer,whichincreasestheenergyconsumptionduringassociation,andthedevicessynchronize
totheirneighbourslessoften,whichpotentiallyleadstodesynchronizationduetoclockdrifts.
Addingmorecoordinatorsmitigatesthelongerassociationtimes,becausethefrequencyofbeacons
increases. The use of real time clocks, available in common LoRa target platforms, mitigates
desynchronizationissues(Section4.1)
Toillustratethetrade-offbetweentransmissiondelayandenergyconsumption,wepresentin
Table8theenergyconsumptionandlifetimeofaDSME-LoRasendernodefordifferentmultisu-
perframeorders.WeassumeexponentiallydistributedinterarrivaltimeswithTXinterval=15m.
Thebeaconintervalissetto122.28s(BO=7)–inlinewithLoRaWANclassBbeaconinterval–
andassumethedevicekeepsthetransceiveronfortwobeaconintervalstoassociatewithasingle
coordinator.Wealsoestimatethevoltageregulatorefficiencytobe90%.Forthelifetimeestimation
weassumethedeviceoperatesonabatteryof2800mAhcapacity–inlinewithcommonoffthe
shelfAAalkalinebatteries.Weutilizethemodel(Section6)toestimatetransmissiondelay.
MO=7 renders the lowest power consumption (0.38mW) and allows 3 years of operation.
≈
However,italsodepictsthehighestaveragelatency( 71s).Notethatthedelaycanincreaseup
≈
tothebeaconduration(122.28s)ifthepacketisscheduledrightaftertheboundaryoftheGTS.If
theusecasedoesnottoleratehighdelays,thedevicemayoptforalowermultisuperframeorder.
Pleaseobservethat(i)theenergyconsumptiondecreaseswithanincreaseofmultisuperframe
orderand(ii)theenergyconsumptiondecreasesatalowerrateonhighermultisuperframeorder.
Forexample,areductionfromMO=7toMO=6increasesconsumptiononlyby0.01mW,whilea
reductionfromMO=4toMO=3increases0.11mW.ThiseffectoccursbecauseadecrementinMO
duplicatesthenumberofGTSperbeaconinterval.RecallthatascheduledGTS-TXconsumes2.2mJ
evenifthereisnotransmission(seeSection5.7),whichreflectstheincreaseinenergyconsumption.
AdevicewithMO=3rendersanaveragedelayof3.87sandlifetimeof 2years.Iftransmission
≈
delayisnotcritical,adevicecanextendthelifetimeupto1yearbysettingMO=7.AlthoughMO
beyond7ispossible,itincreasesthebeaconinterval,whichchallengesdevicesynchronization.
Ingeneral,theenergyfootprintofDSME-LoRAforuplinkorientedapplicationsishigherthan
LoRaWAN,consideringanequivalentLoRaWANclassAdevicecanoperate>10yearsrunningon
batteries.
Finally,wepresentpotentialoptimizationsforopenDSMEandtheintegrationintoRIOT,aiming
toreducepowerconsumption:(i)avoidturningonthetransceiveronaTXGTSiftheMACqueue
is empty, which reduces the energy consumption by 1.5mJ per superframe ( 0.20mW) for
≈ ≈
theallocationofoneGTSTXslot.ThisispossiblewithaminorchangeintheGTSmanagement
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 37
routinesofopenDSME.(ii)turnoffthetransceiverinthebeaconslotrightafterthereceptionofthe
beacon,whichpotentiallyreduces 16mJinthereceivingbeaconslot.(iii)useCADtodetectthe
≈
preambleofaLoRaframeatthebeginningofaGTSRXandproceedtoreceptionifCADsucceeds,
insteadofkeepingthetransceiveridlelisteningforthedurationoftheslot(0.48s).Forexample.
threeCADattemptsconsume0.73mJ,asanalyzedinSection5.7.Underthisscenario,thepassive
consumptionoftheCFPreducesby18.58mJpersuperframe(2.41mW).
8.5 Analysisofcross-traffic
WeshowinSection5.5thatDSME-LoRacancoexistwithLoRaWANintheEU868region,because
LoRaWANtrafficneitherinterfereswithDSMEMACcontroltrafficnorwithbeacons.Therefore,
concurrentDSME-LoRaandLoRaWANcommunicationonlydegradesPRR.Aslongasthecommon
channeldoesnotoverlapwithLoRaWANchannels,thecoexistenceofDSME-LoRaandLoRaWAN
inregionsotherthanEU868isfeasible.
ThechannelhoppingmodeinGTSallowscommunicationdespiteheavyinterferenceonasingle
channel,butdegradesPRRasaresultofafractionofpacketsbeingtransmittedinthenoisychannel.
To overcome this problem, a device may transmit confirmed messages. Thereby the MAC will
performtheretransmissiononachannelwithbetterquality.Analternativesolutionistousethe
channeladaptationmodeofDSME-LoRa(seeSection3.1),inwhichthesourceandtargetdevice
agreeonadifferentchannelifthechannelqualityispoor.AlthoughopenDSMEimplementsthe
channeladaptationmode,itdoesnotimplementtherequiredMACcommand(DSMELinkReport)
torequestchannelqualityinformation.Therefore,thereisnowaytoinferchannelqualityand
agreeonadifferentchannel.
Poorchannelqualityinthecommonchannelchallengesdevicesynchronization(seeSection5.6),
whichpreventsnormaloperationoftheDSME-LoRanetwork.Whilethisisalsoaproblemfor
standardDSME,thelongtimeonairandlongrangeofLoRapacketsrepresentsasecuritythread
forDSME-LoRanetworks.Attackersmaydesynchronizedevicesbyjammingthechannelduring
beacontransmissions.
To address this problem, coordinators may request children devices to switch to a channel
withbetterqualityusingthePHY-OP-SWITCHmechanism(seeSection3.1).Thisrequiresthe
coordinatordeviceto estimatethechannelquality,forexample,bykeepingtrackofthefailed
CCAattemptsduringCSMA/CAtransmissions.However,theMACcontrolframesrequiredby
thePHY-OP-SWITCHmechanismaresentduringCAP,whichchallengespacketdeliveryunder
noisyconditions.Also,adevicemaydetectgoodchannelqualityduringCAPevenifanattacker
jamsonlybeaconframes.AnalternativesolutionistotransmitframesusingtheFHSS,asanalyzed
inFigure8.3.Therebypackettransmissionscantoleratenoiseinasinglechannel,byrelyingon
forwarderrorcorrectionmechanismsontheLoRaPHY.Topreventselectivejamattacks,packets
canbetransmittedwithapseudorandomFHSSsequencesharedbyalldevices.Wewillanalyze
thisproposalinfuturework.
9 RELATEDWORK
9.1 IEEE802.15.4standardsTSCHandDSME
The802.15.4MACmodesTSCHandDSME[26]havebeenanalyzed[34],modeled[10,30],and
simulated[6,16,29].TheresultsindicatethatTSCHobtainslowerlatencyandhigherthroughput
forsmallnetworks(<30nodes).DSMEoutperformsTSCHforhigherdutycyclesandanincreasing
numberofnodes.Kaueretal.[31]introduceopenDSME,animplementationthatisavailablefor
OMNeT++andasaportableC++library.WeutilizeopenDSMEinourwork.Theauthorscompare
simulatedperformancestoreal-worldmeasurements—whichareonpar—andfurtherinvestigate
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

38 Álamosetal.
groupACKs[45]thatdonotcontributetobetterperformanceoverdirectACKs.Vallatietal.[62]
findinefficienciesinDSMEnetworkformationandprovidecountermeasures,however,wemove
networkformationtofuturework.ImprovementsontheQoSofDSMEnetworkswereproposedby
Kurunathan[33].SimilartotheIETFstandardsolutionIPv6overtheTSCHmodeofIEEE802.15.4e
(6TiSCH)[64]forIPv6overTSCH,Kurunathanetal.presentRPL(RoutingProtocolforLowpower
andLossyNetworks)overDSME[35].TheIETFfurtherprovidesanapplicabilitystatement[9]
forRPLinmeteringusecasesandproposesDSMEasaMAC.TheIEEE802.15workinggroup,in
contrast,introduces”Low-EnergyCriticalInfrastructureMonitoring”inthew-amendment[27],
which adds long-range radios that operate in the sub-GHz band. These networks are primary
definedtooperateinstartopologies,whichsupportsourtopologychoiceofasingle-hopDSME
network.
9.2 AnalysisofLoRaWAN
ExistingLoRaWAN[43]networksaresusceptibletocollisions[18,49]aswellasenergydeple-
tion[46].Liandoetal.[40]providereal-worldmeasurementsofLoRaandLoRaWANandexplore
theimpactoftransmissionparametersofthechirpspreadspectrummodulation.Theythereby
identifyoptimizationpotentialsforthemediumaccesslayer.Slabickietal.[60]contributeFLoRa,a
LoRasimulatorforOMNeT++,andimprovetheadaptivedatarate(ADR)mechanismofLoRaWAN.
WeutilizeFLoRainoursimulations.Rizzietal.[53]andLeonardietal.[39]showthatslightmodifi-
cationsoftheLoRaWANMACalreadyimproveperformancemetricsofclassAdeployments,which
arecenteredaroundtheconceptofuplinkpacketsfromanendnode.LoRaWAN,however,poses
aseverechallengeondownlinktrafficduetobandlimitations[17,55]inthesub-GHzband,and
contentionwithunpredictableuplinkpackets[47].Vincenzoetal.[65]proposecountermeasures
tothatproblem,byaddingmultiplegatewaysandagatewayselectionmechanism.Thisdecreases
lossesbutaddsdeploymentcost.
LoRaWANclassB(seeSection1),thoughbarelydeployed,providesperiodicdownlinkslots
(unlikeclassA&C)andmulticastcapabilities[44]thoroughtheseslots.Elbsniretal.[15]confirm
thatclassBdecreasesdownlinklatencyandlossoverclassA.Ronetal.[54]deriveanoptimal
classBconfigurationtotradewaitingtimewithenergyconsumption,andPasettietal.[50]designa
single-gatewayclassBLoRaWANnetworkfor312LoRanodes.Unfortunately,apracticalevaluation
ismissing.OperatinginclassB,however,suffersfromscalabilityissues[19,59].Despite,classB
stillburdensthegatewaydutycycleandrequiresaninfrastructurenetwork,hence,itisnotan
optionforlong-rangenodetonodecommunication.
9.3 NewprotocolsforLoRa
TheIETFstandardizedacompression[22]schemeforLoRanetworks.Similarly,Perešínietal.[51]
introduceaslimpacketformatwithanewLoRalinklayer,toreduceeffectivepayload.Gonzalezet
al.[23]motivatethedevelopmentofanewLoRaMACandpresentLoRaPHYconfigurationsto
definelogicalchannels,whichassistsfrequency-andtimedivisionmultipleaccessprotocols.We
applytheseconsiderationsinourwork.
Cotrimetal.[12]provideaclassificationformulti-hopLoRaWANnetworks.Enablingmulti-hop
withlong-rangeradiosiscommondesire[1,8,56,61].Newdesignsoftime-slottedLoRaproto-
cols[71]havebeenanalyzedwithsimulations[38,69]andpracticaldeployments[70].Haubroet
al.[25]presentanadaptationofthe802.15.4TSCHmode[26]forLoRa.Theirreal-worldmeasure-
mentsshowtheapplicabilityof802.15.4MAClayersforlong-rangecommunication,however,the
experimentdeploymentconsistsofonlythreenodesandlimitedtraffic.Theanalysisofduty-cycle
complianceremainsopen.Incontrast,wefocusonLoRaandthe802.15.4DSMEmodeinourwork
andaimtofillinthegapofalarge-scaledeploymentwhichfurtherincludesduty-cycleanalyses.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 39
SeveralMACandPHYapproacheshavebeenanalyzedtoovercometheproblemofconcurrent
LoRacommunication.Xuetal.[68]proposeS-MAC,anadaptiveschedulingmechanismforLow
PowerWideAreaNetwork(LPWAN)thatexploitsthefactmanyLPWANapplicationstransmit
perioduplinkdata.Deviceswiththesamespreadingfactorandknowntransmissionintervalare
groupedandassignedauniquecarrierfrequencytominimizeintergroupframecollisions.The
approachbringsa4×throughputimprovementforperiodicuplinkcommunication,butdoesnot
addressdownlinklimitationsofLoRaWAN(seeSection2).Theauthorsof[48,52]presentexperi-
mentalresultsforcontentionbasedmediaaccesswithLoRa.Kennedyetal.[48]exploreCSMA/CA
withCAD.ResultsshowthatlistenbeforetalkperformsbetterthanALOHAindensedeployments,
whichmotivatedoureffortsofusingCSMA/CAwithCADinthecontentionaccessperiodofa
DSMEframe(seeSection5.3).Gamageetal.[21]proposeLMAC,animprovedCSMA/CAprotocol,
andevaluateonatestbedthedesignofthreeadvancingversionsoftheprotocol.Resultsindicate
thattheapproachbrings2.2×goodputimprovementand2.4×reductionofenergyconsumption.
WemotivatetheLMACapproachforfutureworktoreducecollisionsduringCAPtransmissions
(see Section 5.3). There have been multiple proposals to resolve LoRa frames collisions at the
physicallayer([58,66,67]).Evaluationsofthosemechanismsonsoftwaredefinedradioshowa
clearimprovementofthroughputandoverallnetworkcapacity,butaddhardwarecomplexityand
extradeploymentcostincomparisontocommonofftheshelfLoRanodes.
LittleworkanalyzesalternativecommunicationpatternoverLoRa.Leeetal.[37]proposegateway
driven requests. This approach follows a request-response pattern and indicates performance
benefitsoverproducerdrivenALOHA.Similarly,theauthorsof[13,14,42]deployinformation-
centricnetworkingoverLoRaradios,whichisadatarequestdrivenprotocol.Theirworkshowed,
however,theneedforaproperLoRamediaaccesslayer.
10 CONCLUSIONSANDOUTLOOK
Inthiswork,weexposedtheproblemsofLoRaWANfornodetonodecommunicationandmoti-
vatedtheusageofIEEE802.15.4DSMEoverLoRa,whichopensLoRatogeneralnetworking.We
summarizedtheDSMEmappingsfortheEU868regionwithsystemintegrationintotheoperating
systemRIOT,andpresentedacomprehensiveevaluationofDSME-LoRaonanIoTtestbed.The
resultsrevealedthatCSMA/CAtransmissionsduringthecontentionaccessperiodprovideagood
trade-off between transmission delay and packet reception ratio for networks with low traffic
and a few nodes. On the contrary, GTS transmissions show about 100% packet reception ratio
andpredictabletransmissiondelaysfornetworkswithhighernetworksizeandhighertraffic.We
couldshowthatunderthelimitsofavailableGTSresources,theseperformancemetricsdonot
degradewiththenetworksize.TheresultsalsoconfirmedthatcoexistencebetweenLoRaWANand
DSME-LoRaispossible.Nevertheless,noiseinthecommonchannelaffectsnormaloperationof
thenetworkduetobeaconloss.
OurfindingsconfirmedthattheChannelActivityDetectionfeatureofLoRaradiosisapow-
erfulclearchanneldetectionmechanismforCSMA/CA,andeffectivelyreducesthenumberof
retransmissions 15timesinscenarioswithmoderatetraffic.WeevaluatedtheeffectofCSMA/CA
≈
backoff exponent settings and could show that higher values mitigate frame collisions during
CAP.Theevaluationevidencedthatdirectcommunicationbetweendevicesfacilitatescompliance
withregionaldutycycleregulations.WealsoconfirmedthatwithoptimalMACconfigurations,
DSME-LoRaoffersapassiveconsumptionoflessthan1mW.Basedonanovelanalyticalstochastic
modelwecalculatedaveragequeuelengthintheMACforslottedtransmission,fromwhichwe
estimatedthetransmissiondelays.Validationofthemodelwithdatafromtheexperimentsusing
realIoThardwareshowedanaccuracyof99.99%.WealsoevaluatedDSME-LoRaforlargernetwork
sizesusingawell-knownsimulationenvironmentandconfirmedourexperimentalfindings.We
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

40 Álamosetal.
evaluatedtheeffectoftheMACconfigurationandutilizedthemodeltooptimizethroughputfor
eachconfiguration.Fromtheevaluationresultswebuiltanoverviewoftransmissionpatternsand
configurationsaimingtoprovideagoodtrade-offbetweentransmissiondelay,timeonair,and
energyconsumption,whichledtoproposingchangesintheMACimplementationforimproving
energyconsumption.
Therearethreefuturedirectionsofthisresearch.First,recentIETFconceptsofthe6TiSCHand
IPv6overLPWANworkinggroupsshouldbeadoptedwhiletakingadvantageofbuilt-infeatures
of DSME to enable IPv6 over DSME-LoRa. Second, studying dynamic slot allocation between
DSME-LoRanodescanfosterdeploymentexperienceforrealworldscenarios.Third,thestudy
ofsuitablenetworklayersontopofDSME-LoRaanditsperformanceundermassiveindustrial
deployment[24]shallopenanewdirectionofLoRa-centricresearch.
Acknowledgment.ThisworkwassupportedinpartbytheGermanFederalMinistryforEducation
andResearch(BMBF)withintheprojectPIVOT:Privacy-IntegrateddesignandValidationinthe
constrainedIoT.
Availabilityofsoftwareandreproducibility. Westronglysupportreproducibleresearch([2,
57])andutilizeopensourcesoftwareandopentestbedplatforms.Allofourworkisintendedfor
publicrelease.Thecodeofthesoftwarecomponents(implementationofDSME-LoRaonRIOT,
simulationenvironment),theimplementationoftheanalyticalstochasticmodel,documentation,
datasetsandrelatedtoolsareavailableonGitHubathttps://github.com/inetrg/tosn-dsmelora22.
REFERENCES
[1] AndreaAbrardoandAlessandroPozzebon.2019.AMulti-HopLoRaLinearSensorNetworkfortheMonitoringof
UndergroundEnvironments:TheCaseoftheMedievalAqueductsinSiena,Italy.Sensors19,2(2019),402.
[2] ACM.Jan.,2017.ResultandArtifactReviewandBadging.http://acm.org/publications/policies/artifact-review-badging.
[3] CedricAdjih,EmmanuelBaccelli,EricFleury,GaetanHarter,NathalieMitton,ThomasNoel,RogerPissard-Gibollet,
FredericSaint-Marcel,GuillaumeSchreiner,JulienVandaele,andThomasWatteyne.2015.FITIoT-LAB:Alargescale
openexperimentalIoTtestbed.In2015IEEE2ndWorldForumonInternetofThings(WF-IoT).IEEEPress,Piscataway,
NJ,USA,459–464.
[4] JoseAlamos,PeterKietzmann,ThomasC.Schmidt,andMatthiasWählisch.2021.DSME-LoRa–AFlexibleMACfor
LoRa.InProc.of29thIEEEInternationalConferenceonNetworkProtocols(ICNP2021),PosterSession.IEEE,Piscataway,
NJ,USA,2pages. https://doi.org/10.1109/ICNP52444.2021.9651945
[5] JoseAlamos,PeterKietzmann,ThomasC.Schmidt,andMatthiasWählisch.2022.WIP:ExploringDSMEMACfor
LoRa–ASystemIntegrationandFirstEvaluation.In23rdIEEEInternationalSymposiumonaWorldofWireless,Mobile
andMultimediaNetworks(WoWMoM)(Belfast,UK).IEEE,Piscataway,NJ,USA.
[6] GiulianaAlderisi,GaetanoPatti,OrazioMirabella,andLuciaLoBello.2015. SimulativeassessmentsoftheIEEE
802.15.4eDSMEandTSCHinrealisticprocessautomationscenarios.In13thInternationalConferenceonIndustrial
Informatics(INDIN’15).IEEE,Piscataway,NJ,USA,948–955.
[7] EmmanuelBaccelli,CenkGündogan,OliverHahm,PeterKietzmann,MartineLenders,HaukePetersen,Kaspar
Schleiser,ThomasC.Schmidt,andMatthiasWählisch.2018.RIOT:anOpenSourceOperatingSystemforLow-end
EmbeddedDevicesintheIoT.IEEEInternetofThingsJournal5,6(December2018),4428–4440. http://dx.doi.org/10.
1109/JIOT.2018.2815038
[8] MaiteBezunartea,RoaldVanGlabbeek,AnBraeken,JacquesTiberghien,andKrisSteenhaut.2019.TowardsEnergy
EfficientLoRaMultihopNetworks.InInternationalSymposiumonLocalandMetropolitanAreaNetworks(LANMAN
’19)(Paris,France).IEEE,Piscataway,NJ,USA,1–3.
[9] N.Cam-Winget,J.Hui,andD.Popa.2017.ApplicabilityStatementfortheRoutingProtocolforLow-PowerandLossy
Networks(RPL)inAdvancedMeteringInfrastructure(AMI)Networks.RFC8036.IETF.
[10] NikumaniChoudhury,RakeshMatam,MithunMukherjee,andJaimeLloret.2020.APerformance-to-CostAnalysisof
IEEE802.15.4MACWith802.15.4eMACModes.IEEEAccess8(2020),41936–41950.
[11] TTNCommunity.2022.TheThingsNetwork.https://www.thethingsnetwork.org/,lastaccessed04-12-2022.
[12] JefersonRodriguesCotrimandJoaoHenriqueKleinschmidt.2020. LoRaWANMeshNetworks:AReviewand
ClassificationofMultihopCommunication.Sensors20,15(2020),4273.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 41
[13] AnthonyDowling,LaurenHuie,LaurentNjilla,HongZhao,andYaoqingLiu.2021. Towardlong-rangeadaptive
communicationviainformationcentricnetworking.IntelligentandConvergedNetworks2,1(2021),1–15.
[14] AnthonyDowling,YaoqingLiu,LaurenHuie,andKangChen.2021.BuildinganInformation-CentricandLoRa-Based
SensingPlatformforIoT.InProc.ofIEEEConf.onComputerCommunicationsWorkshops(INFOCOMWKSHPS).IEEE
Press,Piscataway,NJ,USA,1–6.
[15] HoussemEddinElbsir,MohammedKassab,SamiBhiri,andMohamedHediBedoui.2020.EvaluationofLoRaWAN
ClassBefficiencyfordownlinktraffic.In16thInternationalConferenceonWirelessandMobileComputing,Networking
andCommunications(WiMob’20).IEEE,Piscataway,NJ,USA,105–110.
[16] AtisElsts.2020.TSCH-Sim:ScalingUpSimulationsofTSCHand6TiSCHNetworks.Sensors20,19(2020),5663.
[17] EuropeanTelecommunicationsStandardsInstitute.2006.ElectromagneticcompatibilityandRadiospectrumMatters
(ERM);ShortRangeDevices(SRD);Radioequipmenttobeusedinthe25MHzto1000MHzfrequencyrangewithpower
levelsrangingupto500mW;Part1:Technicalcharacteristicsandtestmethods.TechnicalReportETSIEN300220-1
V2.1.1.IEEE,SophiaAntipolis,France.
[18] GuillaumeFerre.2017.CollisionandpacketlossanalysisinaLoRaWANnetwork.In25thEuropeanSignalProcessing
Conference(EUSIPCO’17).IEEE,Piscataway,NJ,USA,2586–2590.
[19] JosephFinnegan,StephenBrown,andRonanFarrell.2018. EvaluatingtheScalabilityofLoRaWANGatewaysfor
ClassBCommunicationinns-3.InIEEEConferenceonStandardsforCommunicationsandNetworking(CSCN’18).IEEE,
Piscataway,NJ,USA,1–6.
[20] F.Sanchez-SutilandA.Cano-Ortega.2022.SmartregulationandefficiencyenergysystemforstreetlightingwithLoRa
LPWAN.SustainableCitiesandSociety83(2022).
[21] AmalindaGamage,JansenChristianLiando,ChaojieGu,RuiTan,andMoLi.2020.LMAC:EfficientCarrier-SenseMultiple
AccessforLoRa.AssociationforComputingMachinery,NewYork,NY,USA. https://doi.org/10.1145/3372224.3419200
[22] O.GimenezandI.Petrov.2021.StaticContextHeaderCompressionandFragmentation(SCHC)overLoRaWAN.RFC
9011.IETF.
[23] NicolasGonzalez,AdrienVanDenBossche,andThierryVal.2018. SpecificitiesoftheLoRaphysicallayerforthe
developmentofnewadhocMAClayers.In17thInternationalConferenceonAdHocNetworksandWireless(AdHoc-
Now’18)(StMalo,France),Vol.11104.Springer,Cham,Switzerland,163–174.
[24] CenkGündogan,PeterKietzmann,MartineS.Lenders,HaukePetersen,MichaelFrey,ThomasC.Schmidt,Felix
Shzu-Juraschek,andMatthiasWählisch.2021.TheImpactofNetworkingProtocolsonMassiveM2MCommunication
intheIndustrialIoT. IEEETransactionsonNetworkandServiceManagement(TNSM)18,4(Dec.2021),4814–4828.
https://doi.org/10.1109/TNSM.2021.3089549
[25] MartinHaubro,CharalamposOrfanidis,GeorgeOikonomou,andXenofonFafoutis.2020. TSCH-over-LoRA:long
rangeandreliableIPv6multi-hopnetworksfortheinternetofthings.InternetTechnologyLetters3,4(2020),e165.
[26] IEEE802.15WorkingGroup.2016.IEEEStandardforLow-RateWirelessNetworks.TechnicalReportIEEEStd802.15.4™–
2015(RevisionofIEEEStd802.15.4-2011).IEEE,NewYork,NY,USA.1–709pages.
[27] IEEE802.15WorkingGroup.2020. IEEEStandardforLow-RateWirelessNetworks–Amendment2:LowPowerWide
AreaNetwork(LPWAN)ExtensiontotheLow-EnergyCriticalInfrastructureMonitoring(LECIM)PhysicalLayer(PHY).
TechnicalReportIEEEStd802.15.4™–2020w(AmendmenttoIEEEStd802.15.4-2020).IEEE,NewYork,NY,USA.1–46
pages.
[28] INETAuthors.2021. INETFramework-Anopen-sourceOMNeT++modelsuiteforwired,wirelessandmobile
networks.https://inet.omnetpp.org/,lastaccessed06-04-2021.
[29] Wun-CheolJeongandJunheeLee.2012.PerformanceevaluationofIEEE802.15.4eDSMEMACprotocolforwireless
sensornetworks.InFirstIEEEWorkshoponEnablingTechnologiesforSmartphoneandInternetofThings(ETSIoT’12).
IEEE,Piscataway,NJ,USA,7–12.
[30] IacobJuc,OlivierAlphand,RobertoGuizzetti,MichelFavre,andAndrzeDudaj.2016. EnergyConsumptionand
PerformanceofIEEE802.15.4eTSCHandDSME.InProc.oftheIEEEWirelessCommunicationsandNetworking
Conference(WCNC’16)(Doha,Qatar).IEEE,Piscataway,NJ,USA,1–7pages.
[31] FlorianKauer,MaximilianKöstler,andVolkerTurau.2018.ReliableWirelessMulti-HopNetworkswithDecentralized
SlotManagement:AnAnalysisofIEEE802.15.4DSME.TechnicalReportarXiv:1806.10521.OpenArchive:arXiv.org.
[32] PeterKietzmann,JoseAlamos,DirkKutscher,ThomasC.Schmidt,andMatthiasWählisch.2022.Long-RangeICN
fortheIoT:ExploringaLoRaSystemDesign.InProc.of21thIFIPNetworkingConference(Catania,Italy).IEEEPress,
Piscataway,NJ,USA.
[33] HarrisonKurunathan.2021. ImprovingQoSforIEEE802.15.4eDSMENetworks. DoctoralDissertation.Facultyof
Engineering,niversityofPorto. https://hdl.handle.net/10216/132005
[34] HarrisonKurunathan,RicardoSeverino,AnisKoubaa,andEduardoTovar.2018.IEEE802.15.4einaNutshell:Survey
andPerformanceEvaluation.IEEECommunicationsSurveysTutorials20,3(2018),1989–2010.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

42 Álamosetal.
[35] HarrisonKurunathan,RicardoSeverino,AnisKoubaa,andEduardoTovar.2020.Symphony:RoutingAwareScheduling
forDSMENetworks.SIGBEDReview16,4(January2020),26–31.
[36] YandjaLalle,MohamedFourati,LamiaChaariFourati,andJoaoPauloBarraca.2021.RoutingStrategiesforLoRaWAN
Multi-HopNetworks:ASurveyandanSDN-BasedSolutionforSmartWaterGrid.IEEEAccess9(2021),168624–168647.
[37] Huang-ChenLeeandKai-HsiangKe.2018.MonitoringofLarge-AreaIoTSensorsUsingaLoRaWirelessMeshNetwork
System:DesignandEvaluation.IEEETransactionsonInstrumentationandMeasurement67,9(2018),2177–2187.
[38] LucaLeonardi,FilippoBattaglia,GaetanoPatti,andLuciaLoBello.2018.IndustrialLoRa:ANovelMediumAccess
StrategyforLoRainIndustry4.0Applications.In44thAnnualConferenceoftheIEEEIndustrialElectronicsSociety
(IECON’18).IEEEPress,Piscataway,NJ,USA,4141–4146.
[39] LucaLeonardi,LuciaLoBello,FilippoBattaglia,andGaetanoPatti.2020.ComparativeAssessmentoftheLoRaWAN
MediumAccessControlProtocolsforIoT:DoesListenbeforeTalkPerformBetterthanALOHA?Electronics9,4(2020),
553.
[40] JansenC.Liando,AmalindaGamage,AgustinusW.Tengourtius,andMoLi.2019.KnownandUnknownFactsofLoRa:
ExperiencesfromaLarge-ScaleMeasurementStudy. TransactionsonSensorNetworks(TOSN)15,2(Feb.2019),16.
https://doi.org/10.1145/3293534
[41] JohnD.C.Little.1961.AProoffortheQueuingFormula:L=𝜆W.OperationsResearch9,3(1961),383–387.
[42] YaoqingLiu,LaurentNjilla,AnthonyDowling,andWanDu.2020.EmpoweringNamedDataNetworksforAd-Hoc
Long-RangeCommunication.InWirelessandOpticalCommunicationsConference(WOCC’20).IEEE,Piscataway,NJ,
USA,1–6.
[43] LoRaAlliance–TechnicalCommittee.2017.LoRaWAN1.1Specification.TechnicalReport.LoRaAlliance. https://lora-
alliance.org/sites/default/files/2018-04/lorawantm_specification_-v1.1.pdf
[44] LoRaAlliance–TechnicalCommittee.2018.LoRaWANRemoteMulticastSetupSpecificationv1.0.0.TechnicalReport.
LoRaAlliance. https://lora-alliance.org/sites/default/files/2018-09/remote_multicast_setup_v1.0.0.pdf
[45] FlorianMeyer,PhilMalessa,JanNiklasDiercks,andVolkerTurau.2022. AreGroupAcknowledgementsWorth
AnythinginIEEE802.15.4DSME:AComparativeAnalysis.TechnicalReport.5thConferenceonCloudandInternetof
Things,CIoT2022:114-121.IEEE.Piscataway,NJ.
[46] KonstantinMikhaylov,RadekFujdiak,AriPouttu,VoznakMiroslav,LukasMalina,andPetrMlynek.2019.Energy
AttackinLoRaWAN:ExperimentalValidation.In14thInternationalConferenceonAvailability,ReliabilityandSecurity
(ARES’19)(Canterbury,CA,UnitedKingdom).ACM,NewYork,NY,USA,1–6.
[47] KonstantinMikhaylov,JuhaPetäjäjärvi,andAriPouttu.2018.EffectofDownlinkTrafficonPerformanceofLoRaWAN
LPWANetworks:EmpiricalStudy.In29thAnnualInternationalSymposiumonPersonal,IndoorandMobileRadio
Communications(PIMRC’18).IEEE,Piscataway,NJ,USA,6pages.
[48] MorganO’Kennedy,ThomasNiesler,RiaanWolhuter,andNathalieMitton.2020. Practicalevaluationofcarrier
sensingforaLoRawildlifemonitoringnetwork.InProc.of19thIFIPNetworkingConference(Paris,France).IEEEPress,
Piscataway,NJ,USA,10–18.
[49] CharalamposOrfanidis,LauraMarieFeeney,MartinJacobsson,andPerGunningberg.2019.Cross-TechnologyClear
ChannelAssessmentforLow-PowerWideAreaNetworks.In16thInternationalConferenceonMobileAdHocand
SensorSystems(MASS’19).IEEEComputerSociety,Washington,DC,USA,199–207.
[50] MarcoPasetti,EmilianoSisinni,PaoloFerrari,StefanoRinaldi,AlessandroDepari,PaoloBellagente,DavideDella
Giustina,andAlessandraFlammini.2020. EvaluationoftheUseofClassBLoRaWANfortheCoordinationof
DistributedInterfaceProtectionSystemsinSmartGrids.JournalofSensorandActuatorNetworks9,1(2020),13.
[51] OndrejPerešíniandTborKrajčovič.2017.MoreefficientIoTcommunicationthroughLoRanetworkwithLoRa@FIIT
andSTIOTprotocols.In11thInternationalConferenceonApplicationofInformationandCommunicationTechnologies
(AICT’17)(Moscow,Russia).IEEE,Piscataway,NJ,USA,1–6.
[52] ConducPham.2018.InvestigatingandexperimentingCSMAchannelaccessmechanismsforLoRaIoTnetworks.In
WirelessCommunicationsandNetworkingConference(WCNC’18)(Barcelona,Spain).IEEE,Piscataway,NJ,USA,1–6.
[53] MattiaRizzi,PaolFerrari,AlessandraFlammini,EmilianoSisinni,andMikaelGidlund.2017.UsingLoRaforindustrial
wirelessnetworks.In13thInternationalWorkshoponFactoryCommunicationSystems(WFCS’17).IEEEPress,Piscataway,
NJ,USA,1–4.
[54] DaraRon,Chan-JaeLee,KisongLee,Hyun-HoChoi,andJung-RyunLee.2020.PerformanceAnalysisandOptimization
ofDownlinkTransmissioninLoRaWANClassBMode.IEEEInternetofThingsJournal7,8(2020),7836–7847.
[55] MartijnSaelens,JeroenHoebeke,AdnanShahid,andEliDePoorter.2019.ImpactofEUdutycycleandtransmission
powerlimitationsforsub-GHzLPWANSRDs:anoverviewandfuturechallenges. EURASIPJournalonWireless
CommunicationsandNetworking2019,219(2019),219–251.
[56] BenjaminSartori,SteffenThielemans,MaiteBezunartea,AnBraeken,andKrisSteenhaut.2017.EnablingRPLmultihop
communicationsbasedonLoRa.In13thInternationalConferenceonWirelessandMobileComputing,Networkingand
Communications(WiMob’17)(Rome,Italy).IEEEComputerSociety,Washington,DC,USA,1–8.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 43
[57] QuirinScheitle,MatthiasWählisch,OliverGasser,ThomasC.Schmidt,andGeorgCarle.2017.TowardsanEcosystem
forReproducibleResearchinComputerNetworking.InProc.ofACMSIGCOMMReproducibilityWorkshop.ACM,New
York,NY,USA,5–8.
[58] MuhammadOsamaShahid,MillanPhilipose,KrishnaChintalapudi,SumanBanerjee,andBhuvanaKrishnaswamy.
2021.ConcurrentInterferenceCancellation:DecodingMulti-PacketCollisionsinLoRa.InProceedingsofthe2021ACM
SIGCOMM2021Conference(VirtualEvent,USA)(SIGCOMM’21).AssociationforComputingMachinery,NewYork,
NY,USA,503–515. https://doi.org/10.1145/3452296.3472931
[59] YonatanShiferaw,ApoorvaArora,andFernandoKuipers.2020.LoRaWANClassBMulticastScalability.InProc.of
19thIFIPNetworkingConference(Paris,France).IEEEPress,Piscataway,NJ,USA,609–613.
[60] MariuszSlabicki,GopikaPremsankar,andMarioDiFrancesco.2018.AdaptiveConfigurationofLoRaNetworksfor
DenseIoTDeployments.InProc.ofIEEE/IFIPNetworkOperationsandManagementSymposium(NOMS’18).IEEEPress,
Piscataway,NJ,USA,1–9.
[61] SteffenThielemans,MaiteBezunartea,andKrisSteenhaut.2017.EstablishingtransparentIPv6communicationon
LoRabasedlowpowerwideareanetworks(LPWANS).InWirelessTelecommunicationsSymposium(WTS’17)(Chicago,
IL,USA).IEEE,Piscataway,NJ,USA,1–6.
[62] CarloVallati,SimoneBrienza,MaurizioPalmieri,andGiuseppeAnastasi.2017.ImprovingNetworkFormationinIEEE
802.15.4eDSME.ComputerCommunications114,C(December2017),9pages.
[63] AndrásVarga.2003.TheOMNeT++DiscreteEventSimulationSystem.,1–7pages.Retrievedfromhttps://omnetpp.org/
[64] X.Vilajosana,K.Pister,andT.Watteyne.2017.MinimalIPv6overtheTSCHModeofIEEE802.15.4e(6TiSCH)Configuration.
RFC8180.IETF.
[65] ValentinaDiVincenzo,MartinHeusse,andBernardTourancheau.2019.ImprovingDownlinkScalabilityinLoRaWAN.
InIIEEEInternationalConferenceonCommunications(ICC’19).IEEE,Piscataway,NJ,USA,7pages.
[66] XianjinXia,NingningHou,YuanqingZheng,andTaoGu.2021. PCube:ScalingLoRaConcurrentTransmissions
withReceptionDiversities.InProceedingsofthe27thAnnualInternationalConferenceonMobileComputingand
Networking(NewOrleans,Louisiana)(MobiCom’21).AssociationforComputingMachinery,NewYork,NY,USA,
670–683. https://doi.org/10.1145/3447993.3483268
[67] XianjinXia,YuanqingZheng,andTaoGu.2019.FTrack:ParallelDecodingforLoRaTransmissions.InProceedings
ofthe17thConferenceonEmbeddedNetworkedSensorSystems(NewYork,NewYork)(SenSys’19).Associationfor
ComputingMachinery,NewYork,NY,USA,192–204. https://doi.org/10.1145/3356250.3360024
[68] ZhuqingXu,JunzhouLuo,ZhimengYin,TianHe,andFangDong.2020. S-MAC:AchievingHighScalabilityvia
AdaptiveSchedulinginLPWAN.InIEEEINFOCOM2020-IEEEConferenceonComputerCommunications.506–515.
https://doi.org/10.1109/INFOCOM41043.2020.9155474
[69] GokcerYapar,TunaTugcu,andOrhanErmis.2019.Time-SlottedALOHA-basedLoRaWANSchedulingwithAggregated
AcknowledgementApproach.In25thConferenceofOpenInnovationsAssociation(FRUCT’19).IEEE,Piscataway,NJ,
USA,383–390.
[70] DimitriosZorbas,KhaledAbdelfadeel,PanayiotisKotzanikolaou,andDirkPesch.2020. TS-LoRa:Time-slotted
LoRaWANfortheIndustrialInternetofThings.ComputerCommunications153(2020),1–10.
[71] DimitriosZorbasandXenofonFafoutis.2021.Time-SlottedLoRaNetworks:DesignConsiderations,Implementations,
andPerspectives.IEEEInternetofThingsMagazine4,1(32021),84–89.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

| 44  |     |     |     |     |     |     | Álamosetal. |     |
| --- | --- | --- | --- | --- | --- | --- | ----------- | --- |
1
0.8
0.6
0
𝜋
0.4
0.2 Expected
𝜋0( 𝜌
| 0     | )   |     |     |     |     |         |         |     |
| ----- | --- | --- | --- | --- | --- | ------- | ------- | --- |
| 0 0.1 | 0.2 | 0.3 | 0.4 | 0.5 |     | 0.6 0.7 | 0.8 0.9 | 1   |
𝜌
Fig.28. Comparisonbetweentheexpectedandthepolynomialapproximationofthedistribution𝜋0 for
varyingsystemloads𝜌.
A NUMERICALCALCULATIONOFSTATIONARYMARKOVDISTRIBUTION
Inthisappendix,wewanttoexplainhowtoevaluatethestationMarkovdistribution.Forthis,let
| usdefine𝑥 asanyeigenvectorof𝑃 |     | tothevalueof1.Notethat: |     |     |     |     |     |     |
| ----------------------------- | --- | ----------------------- | --- | --- | --- | --- | --- | --- |
(cid:174)
𝑥
|     |     |     | 𝜋   | = (cid:174) | .   |     |     | (9) |
| --- | --- | --- | --- | ----------- | --- | --- | --- | --- |
(cid:174) (cid:205) 𝑥
|     |     |     |     | 𝑖∞=0 | 𝑖   |     |     |     |
| --- | --- | --- | --- | ---- | --- | --- | --- | --- |
Theequationsystemthatdescribestheeigenvectorsis:
|     |     |       | 𝑘     | 𝑘 𝑥     | 𝑘 𝑥 | = 𝑥 |     |     |
| --- | --- | ----- | ----- | ------- | --- | --- | --- | --- |
|     |     |       | ( 0 + | 1 ) 0 + | 0 1 | 0   |     |     |
|     |     |       | 𝑘 𝑥   | 𝑘 𝑥     | 𝑘 𝑥 | = 𝑥 |     |     |
|     |     |       | 2 0 + | 1 1 +   | 0 2 | 1   |     |     |
|     |     | 𝑘 𝑥   | 𝑘 𝑥   | 𝑘 𝑥     | 𝑘 𝑥 | = 𝑥 |     |     |
|     |     | 3 0 + | 2 1 + | 1 2 +   | 0 3 | 2   |     |     |
...
𝑛
∑︁
|     |     | 𝑘   | 𝑥       | 𝑘   | 𝑥     | = 𝑥 |     |     |
| --- | --- | --- | ------- | --- | ----- | --- | --- | --- |
|     |     |     | 0 𝑛 1 + | 𝑛   | 1 𝑖 𝑖 | 𝑛   |     |     |
|     |     |     | +       | +   | −     |     |     |     |
𝑖=0
Whichresolvesto:
|     |     | 1     | 𝑘     | 𝑘   |     |     |     |     |
| --- | --- | ----- | ----- | --- | --- | --- | --- | --- |
|     | 𝑥   | = 𝑥 ( | − 0 − | 1 ) |     |     |     |     |
1 0
𝑘 0
|     |     | 1     | 𝑘 𝑥 | (cid:205)𝑖 | 2 𝑘       | 𝑥      |     |     |
| --- | --- | ----- | --- | ---------- | --------- | ------ | --- | --- |
|     |     |       | 1   | 𝑖 1        | 𝑗−= 0 𝑖 𝑗 | 𝑗      |     |     |
|     | 𝑥   | = 𝑥 ( | − ) | − −        | −         | , 𝑖 2, |     |     |
𝑖 0
|     |     |     |     | 𝑘 0 |     | ∀ ∈ [ ∞] |     |     |
| --- | --- | --- | --- | --- | --- | -------- | --- | --- |
Weset𝑥 =1andcalculate𝑥 ,𝑥 ,𝑥 ...𝑥 with𝑁 abigenoughnumber.Wethenobtain𝜋 using
| 0   |     | 1 2 | 3 𝑁 |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:174)
Equation9.Thismethodisnotpracticalbecauseitrequiresthecalculationofallvectormembers.
| Therefore,weproposetoapproximate𝜋 |     |     | withapolynomialfunction. |     |     |     |     |     |
| --------------------------------- | --- | --- | ------------------------ | --- | --- | --- | --- | --- |
0
|     |     |     |     |     |     | =   |     | =   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
We calculate 𝜋 0 using the former method for different 𝜌 and 𝑁 500. We then fit 𝑓 𝑥
( )
𝑎𝑥4 𝑏𝑥3 𝑐𝑥2 𝑑𝑥 𝑒 accordingly. The result of the fit procedure produces the polynomial
| + + + | +   |     |     |     |     |     |     |     |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- |
function:
|     |     | 0.24𝜌4 |     | 0.21𝜌3 | 0.55𝜌2 | 0.01𝜌1 |     |     |
| --- | --- | ------ | --- | ------ | ------ | ------ | --- | --- |
|     | 𝜋 0 | 𝜌 =    |     |        |        | 1      |     |     |
|     |     | ( ) −  | −   | −      |        | + +    |     |     |
Theproposedpolynomialfunctionconvergestotheexpectedvaluesof𝜋 0 ,asdepictedinFigure28.
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.

DSME-LoRa:SeamlessLongRangeCommunicationBetweenArbitraryNodesintheConstrainedIoT 45
B GLOSSARY
6TiSCH IPv6overtheTSCHmodeofIEEE802.15.4e.38,40,45
BO BeaconOrder.5,6,35,36,45
BS BeaconSlot.20,22,23,45
CAD ChannelActivityDetection.7,9,11,14–16,33,35,37,39,45
CAP ContentionAccessPeriod.4–6,8,10–17,19–24,29,30,32,34,35,37,39,45
CCA ClearChannelAssessment.8–10,13,15,17,22,23,29,35,37,45
CFP ContentionFreePeriod.4,5,7,11–14,16–20,22–24,29,30,34,37,45
CRC CyclicRedundancyCheck.7,8,45
CSMA/CA CarrierSenseMultipleAccess/CollisionAvoidance.4,6,9,11–24,28–30,32–34,37,
39,45
DER DataExtractionRate.3,45
DSME DeterministicSynchronousMultichannelExtension.1,2,4–12,18–20,24,27,28,31–40,
45
FHSS Frequency-hoppingspreadspectrum.7,35,37,45
GTS GuaranteedTimeSlot.4–9,12–14,17–24,27–30,32–37,39,45
LPWAN LowPowerWideAreaNetwork.39,40,45
MAC MediaAccessControl.1,2,4–10,12–20,22–25,27–30,32,35–40,45
MO MultisuperframeOrder.5,6,31,32,36,45
PAN PersonalAreaNetwork.4,12,45
PHY PhysicalLayer.1,5,7–9,16,19,37–39,45
PRR PacketReceptionRatio.4,12–16,18–20,33,37,45
PSDU PhysicalServiceDataUnit.7,45
RSSI ReceivedSignalStrengthIndicator.7,45
SO SuperframeOrder.5,6,45
TSCH TimeSlottedChannelHopping.6,37,38,45
ACMTrans.SensorNetw.,Vol.1,No.1,Article.Publicationdate:January2022.