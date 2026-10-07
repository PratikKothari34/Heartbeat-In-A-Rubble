> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> arXiv **2312.08387** - *JMAC: a cross-layer multi-hop protocol for LoRa*. Source PDF deleted
> after conversion.
>
> Listed in `docs/research/BUDGET/01-literature.md` comms row 4 as **HELD**, no figure quoted.
> Multi-hop MAC design. Relevant to the duty-cycle budget, which is the weakest part of the
> comms case: doctrine gives **no stated transmission duration**, so the 5-8 % duty cycle is
> [ASSERTED] and may be ~17 %.

1
JMAC Protocol: A Cross-Layer Multi-Hop Protocol
for LoRa
Juan José López Escobar, Felipe Gil-Castiñeira, Rebeca P. Díaz-Redondo
Abstract
he emergence of Low-Power Wide-Area Network (LPWAN) technologies allowed the development of revolutionary Internet
Of Things (IoT) applications covering large areas with thousands of devices. However, connectivity may be a challenge for
non-line-of-sight indooroperation orfor areaswithout goodcoverage. Technologies suchas LoRaand Sigfoxallow connectivity
for up to 50,000 devices per cell, several devices that may be exceeded in many scenarios. To deal with these problems, this
paper introduces a new multi-hop protocol, called JMAC, designed for improving long range wireless communication networks
that may support monitoring in scenarios such smart cities or Industry 4.0. JMAC uses the LoRa radio technology to keep low
consumption and extend coverage area, and exploits the potential mesh behaviour of wireless networks to improve coverage and
increasethenumberofsupporteddevicespercell.JMAC isbasedonpredictivewake-uptoreachlonglifetimeonsensordevices.
OurproposalwasvalidatedusingtheOMNeT++simulatortoanalyzehowitperformsunderdifferentconditionswithpromising
results.heemergenceofLow-PowerWide-AreaNetwork(LPWAN)technologiesallowedthedevelopmentofrevolutionaryInternet
Of Things (IoT) applications covering large areas with thousands of devices. However, connectivity may be a challenge for non-
line-of-sight indoor operation or for areas without good coverage. Technologies such as LoRa and Sigfox allow connectivity
for up to 50,000 devices per cell, several devices that may be exceeded in many scenarios. To deal with these problems, this
paper introduces a new multi-hop protocol, called JMAC, designed for improving long range wireless communication networks
that may support monitoring in scenarios such smart cities or Industry 4.0. JMAC uses the LoRa radio technology to keep low
consumption and extend coverage area, and exploits the potential mesh behaviour of wireless networks to improve coverage and
increasethenumberofsupporteddevicespercell.JMAC isbasedonpredictivewake-uptoreachlonglifetimeonsensordevices.
OurproposalwasvalidatedusingtheOMNeT++simulatortoanalyzehowitperformsunderdifferentconditionswithpromising
results.T
Index Terms
Smart city, IoT, LoRa, multi-hop, mesh network, OMNeT++
I. INTRODUCTION
Since the development of the Internet of Things (IoT) paradigm a few years ago, related technologies have dramatically
evolved to turn IoT into a widely spread reality. The evolution in Low-Power Wide-Area Network (LPWAN) technologies [1]
is particularly remarkable, which support long range communications with notably low power consumption, becoming a good
alternativetotraditionalwirelessnetworksthatdonotsupportthesecommunicationrequirements:(i)WirelessWideAreaNetworks
(WWAN) support long distance communications, but require from higher power consumption; and (ii) Wireless Personal Area
Networks(WPAN)requirefromlowerpowerconsumption,buttheyarenotsuitableforlongdistances.Infact,thereisageneral
consensusaboutwhatcharacteristicsaredesirableinLPWAN[2]:(i)lowpowerconsumption,neededforbatteries;(ii) inexpensive
chips; (iii) easy and scalable deployment; (iv) ALOHA with single hop routing as Medium Access Control (MAC) protocol; (v)
secured data; and (vi) robust radio modulation to minimize the impact of channel fading.
There are some relevant technologies within the LPWAN field. LoRaWAN [3], a point-to-multipoint networking protocol
that is built upon the LoRa physical layer [4], must be highlighted for different reasons, being its easy deployment and open
nature two of the most remarkable ones. Additionally, Sigfox [5] is managed by a single operator and offers a complete IoT
architecture, although quite constrained because of using a proprietary UNB modulation and infrastructure. Besides, DASH7 [6]
andWeightless[7]areopenstandardizedstacks,butwithlowerimpactintheIoTdomain.Alltheaboveoptionshaveincommon
the use of unlicensed bands of the spectrum, but there are alternatives in licensed bands from the 3rd Generation Partnership
Project(3GPP)[8].ThisisthecaseofNB-IoT[9],whichexploitstheexistingcellularnetworktoconnectdeviceswhichgenerate
a small data flow, or LTE-M [10], a wider bandwidth option for applications which frequently require to exchange high volumes
of data.
Mostofthesetechnologiesarecurrentlyusedinmanysituationsandsupportanonlysinglehopcommunication.Thismeans
thatforlargeareasitisnecessarytodeployinfrastructureforunlicensedtechnologies,ortogetasubscriptiontoanetworkoperator.
This problem is exacerbated in areas where physical phenomena (interference, noise, obstacles, etc.) reduce the coverage range
toafewkilometersorhectometers,suchasinurbanareasorinindustrialsettings(indoorplaces).Ourproposalpreciselytriesto
overcomethisproblem,butstillsatisfyingtheLPWANgeneralrequirementspreviouslymentioned.Thus,ourfirstcontributionis
topresentaninnovativelayoutformulti-hopnetworkingontopofameshedversionofLoRacommunication,whichwecoinedas
JMAC.Enablingmulti-hopcapabilityallowsreusingresourcesandexpandthecoverageareasubstantially.Oursecondcontribution
is the development of an appropriate framework within the OMNeT++ simulator [11] that behaves as close as possible to the
real behaviour of LoRa, which we coined as FLoRaPHY. We needed from this new software module to check the behaviour and
scalability of the new protocol. This software is available for the research community in GitHub [12].
This paper is organized as follows. Section II describes the base technologies that we used to define our new protocol: the
LoRatechnology,neededforthephysicallayerandthatsupportsthenewprotocolJMACandtheOMNeT++simulator,usedfor
validationpurposes.SectionIIIsummarizestherelatedworkwithinthemulti-hopnetworks,notonlyusingLoRaandLoRaWAN,
juanjo@det.uvigo.es,xil@det.uvigo.es,rebeca@det.uvigo.es;atlanTTic,UniversidadedeVigo;Vigo,36310,Spain.
3202
ceD
21
]IN.sc[
1v78380.2132:viXra

2
but also describing interesting approaches for multi-hop Wireless Sensor Networks (WSN). Section IV describes the JMAC
protocol:behaviour,frameformatsanddesignrestrictions.InSectionVwedescribethenewsoftwaremodulecreatedtosimulate
LoRawithintheOMNeT++simulatorandwealsoshowtheresultsobtainedundertwodifferentscenarios:asimpleone,tocheck
the impact of the different parameters in the protocol, and a more complex and dense topology to check the scalability of the
proposedprotocol.SectionVIsummarizesconclusionsandlimitationsofourproposal,givingsomecluestofurtherimprovement.
Finally, Section VII summarizes the conclusions and future work.
II. BACKGROUND
TheJMACprotocolworkswithLoRa,alowerphysicallayerdescribedinSectionII-A,toofferasuitablemulti-hopsolution
ortheuppernetworkinglayer.Usually,solutionsoverLoRaworkwithLoRaWAN,aprotocoldefinedpreciselyforthisnetworking
layer, so this approach is also explained in the same subsection. Since we need to validate our proposal, we opted to use the
OMNeT++ simulation environment, which is described in Section II-B.
A. LoRa
The origins of LoRa date back to 2010, as a new long range and low power modulation technique created by the French
start-up Cycleo. Two years later, the American company Semtech acquired Cycleo and (i) the first LoRa chips for end-devices
and gateways were launched to market and (ii) the new protocol LoRaMAC was created under a proprietary license in order to
enablenetworkingintotheupperlayersanddefinemessageformatandsecurityaspects.In2015theLoRaAlliance[13],anopen,
nonprofit association of companies, universities, research groups and developer communities worldwide, was founded and the
LoRaMAC protocol was renamed to LoRaWAN, with the aim of establishing a new standard for LPWAN. In fact, the LoRa
Alliance is only in charge of writing the LoRaWAN specification of the technical implementation to ensure interoperability
between manufacturers and developers, whereas companies are free to define any commercial model or type of deployment of
cloudservices(public,private,hybridorenterprise).NotableexamplesofrealworlddeploymentsareTheThingsNetwork(TTN)
platform [14], an open cloud service which leads LoRaWAN usage and is supported by a great community, and its commercial
version The Things Industries (TTI) [15].
The LoRa technology is based on a proprietary version of the Chirp Spread Spectrum CSS modulation [16], which tolerates
receivingsuccessfullysignalsbelowthenoisefloor.Thisincreasesthelinkbudgetandtheimmunitytointerference,whichallows
longrangecommunicationandgivesrisetothetechnologyname.Itisdefinedasaspreadspectrumtechniquewhichsymbolsare
transmitted using up- and down-chirps, i.e., a digital chirp signal that varies in frequency within boundaries of the channel. This
simpleconcepthastheadvantageofhavingequivalenttimingandfrequencyoffsetsbetweentransmitterandreceiver,simplifying
the receiver design. Despite the limited information provided by the manufacturer in a few manuals [17, 18], many studies have
addressed the objective of reverse-engineer the exact modulation technique, experiment with it in real world and try to guess a
mathematical model [19, 20, 21, 22, 23], so more information about it is available nowadays. LoRa was not the first modulation
of its kind, since it is popular in radar applications. However, LoRa was the first low cost implementation for commercial usage,
which gives the opportunity to exploit this kind of technology in new contexts, such as IoT and smart cities because of its main
characteristics:
• Narrowband/Wideband: it can operate in the same way both narrowband and wideband configurations because bandwidth
and central frequency are scalable and easy to adapt to any application requirement.
• Constant Envelope: the information of the signal lies in frequency variation and it is independent of the amplitude. Then,
the low-power high-efficient power amplifier can operate at saturation level or near it.
• High Robustness: symbols are very long compared to bandwidth, which provides outstanding immunity to adjacent-channel
interference.
• Pseudo-orthogonality: it might be one of the most relevant and interesting topics in LoRa. Spreading factors (𝑆𝐹) have an
effectthatallowstransmitting/receivingcorrectlymultiplesignalsinthechannelatthesametime,aslongastheyusedifferent
𝑆𝐹. This feature may be expanded to some combinations of overlapping channels as long as the power difference between
them is high enough to consider the interference as noise, as it is shown in [21].
• Multipath/Fading Immunity: chirp pulses are relatively long time duration, therefore they are resistant against multipath and
fading of the signal.
• DopplerResistant:mobilecommunicationsarecorrectlysupportedbyLoRa,sincetheDopplereffectonlygeneratesasmall
and negligible frequency shift in the pulse which does not require very accurate clock sources.
• Localization:LoRaissuitableforrangingtransmitterlocationduetotheabilitytodiscriminatebetweenfrequencyandtime
errors which may be produced by multi-path effects, similar to radar applications.
TheLoRaWANarchitectureisdeployedinastar-of-starstopology(Figure1)inwhichsingle-channelend-devicescommunicate
directly with any multi-channel gateway. Gateways are connected to a back-end through conventional Internet, and serve as a
transparent bridge between end-devices and back-end, so they must be active at all times. In this architecture, end-devices are
usuallysensorsthatsenddataeventuallyandtrytowasteaslittleenergyaspossible.Theyareusuallyclassifiedintothreetypes.
(i) Class A devices send an uplink message at any time and stay in receiver mode for two short downlink windows right after,
to give the opportunity for bidirectional communication or for receiving control commands. The rest of the time stay in sleep
mode, so they have the lowest power operating mode. This is the default class and must be supported by all LoRaWAN end-
devices,asitisusedtobuildthefollowingones.(ii)ClassBdevicesoperateasClassA,buttheyaddanextrareceivingwindow
periodically. This window is announced via beacon frames to time-synchronize the back-end. Finally, (iii) Class C devices keep
thereceivingwindowopenatalltimes,exceptwhentransmitting(half-duplex),sothelatencyfordownlinkmessagesisdecreased
drastically. Such devices should not operate with batteries because of the high power consumption. The class of end-devices
actually determines the MAC protocol used in LoRaWAN.
GatewaysmustimplementaPacketForwardlayertoconvertLoRaRFpacketstostandardIPpacketsandviceversatoallow
bidirectional communication. In addition, they are usually able to operate simultaneously in combinations of frequency channel
and𝑆𝐹, which enhances network capacity and allows frequency hopping.

3
Back-end
App 1
NS
Gateway AS App 2
Internet
LoRa Radio Backhaul
Gateway JS
Fig. 1: LoRaWAN architecture.
The back-end is an infrastructure composed of several micro-services detailed in [24]. It is essentially comprised of three
units. (i) The Network Server (NS) that is the center of the star topology, marks the edges of the LoRaWAN MAC layer for
the end-devices and processes and routes the messages. It is responsible for data rate adaptation, MAC layer issues (control and
commands)andqueuingdownlinkmessages.Besides,NScopeswithroamingaspectsifitwerenecessary.(ii)TheJoinServer(JS)
managesauthenticationofend-devicesandactivationofkeysviaOver-The-Air(OTA)procedure.Itstoresallnecessaryelements
toidentifysecurelyanend-deviceandmustestablishasecurecommunicationwithNS.Finally,(iii)TheApplicationServer(AS)
handlesallapplicationfeatures,bothmanagingpayloaduplinkanddownlinkmessages,offeringthisdatatotheend-user.It must
share with the Join Server (JS) the application credentials.
TheLoRaWANspecificationconsidersspectrumusageindifferentregulatoryregionsworldwide[25]andidentifiesthemost
commonchannelplans,althoughwefocusonthemostcommoninEuropeancountries(EU868-870).Specifically,itmustoperate
atleastinthe3defaultchannels(868.1 MHz.,868.3MHz.and868.5MHz.)witharestrictionofatmost1%dutycycle.Currently,
the most popular version is v1.0.3 [26], but the latest one is v1.1 [27], which adds new functionalities.
B. OMNeT++
OMNeT++[11]isapopularopen-sourcediscreteeventsimulatorforanykindofnetwork,supportingfromwiredandwireless
networkstophotonicones.ItprovidesacompleteextensibleandmodularframeworkwritteninC++andanEclipse-basedIDEwith
agraphicalenvironmenttofacilitatedevelopment,simulationexecutionandanalysisofdataresultsandperformanceofthenetwork.
ItisdistributedunderanAcademicPublicLicensewhichallowsusingitinnon-commercialenvironments,forinstanceresearchand
teaching.ThereisalsoacommercialversioncalledOMNEST[28].Besides,it issupportedbyanimportantcommunity,makingit
averysuitableoptionformodellingcomputernetworksscenarios.OMNeT++definesalightweightclasscalledcObjectasroot
elementforanysimulationfunctionality.Inordertorepresentthesimulationscenario,thecModuleandcChannelclassesare
defined. The former deals with the main logic of the modules, whereas the latter is in charge of modelling the physical medium.
Inadditiontothekernellibraries,projectsarebuiltusingatopologydescriptionlanguage,calledNED,whichallowsassembling
complex components and reuse modules using a high-level language.
OneofthestrengthsofOMNeT++istheamountofexternalframeworksthathavebeendevelopedbythecommunity,whether
they are researchers or independent developers. The simulation models are indexed in the official website, but not all of them
are completely mature or offer technical support. However, there is one model library which stands above the others: the INET
Framework [29]. It contains modules for any traditional Internet protocol (TCP, UDP, IPv4, IPv6, BGP, Ethernet, IEEE 802.11,
etc.), physical modulation techniques (APSK, DSSS, etc.), mobility and QoS support, power consumption estimators and a lot
more which may be useful to design and evaluate new technologies. Additionally, INET is often the basis for further libraries,
sinceitprovidesessentialcomponentswhichfitperfectlyandsavetimeindevelopmentphase,suchasvehicularnetworksorLTE.
Asidefromversatilityofthesimulator,themainreasonitwaschosenwastheavailabilityofaLoRaWAN-orientedframework,
called FLoRa [30], developed by researchers from the Aalto University (Finland). It does not support the complete LoRaWAN
protocol, but the crucial parts to implement new simulation scenarios, such as the developed in this work, are there and can
be used.
III. RELATEDWORK
Sensornetworkdeployments,alsoLoRaWANnetworks,mayhavecoveragecapacityproblemswhentheyareusedinadverse
scenarios,suchasinurbanorindoorareas,duetohighinterference,noiselevelandpathlosses[31].Consequently,inthelastfew
years,researchershavedesignedmechanismstocreatemulti-hopnetworksthatcanexpandthecoverageunderthesecircumstances.
These proposals can be organized into three philosophies: (i) providing a completely new protocol stack over the LoRa radio
(SectionIII-A);(ii)extendingaLoRaWANnetworkwithmulti-hoproutingbetweenend-devicesorbetweenintermediategateways
(Section III-B); and (iii) using WSN approaches that are more mature in the multi-hop strategies field (Section III-C).
A. LoRa Multi-Hop
A very clear trend in mesh networks using LoRa technology is exploiting the features of LoRa modulation to implement
the Concurrent Transmission (CT) protocol [32], as in [33]. Concretely, the CT-based multi-hop protocol has an initiator which

4
broadcastsamessagealongthenetworkusingtheothernodesasfloodingforwarders.ThisispossiblebecausetheLoRamodules
only receive correctly the highest-energy packet and no collision avoidance mechanism has to be considered. In order to support
allnodestoinitiatethetransmission,theymustbesynchronizedbyaTime-DivisionMultipleAccess(TDMA)protocolusingthe
receivedmessages.Moreover, this approachisimproved with asmalltimingoffset insertionduringthetransmission time,which
leads to a better receiving performance.
Anotherrelevantproposalisthedeploymentof19LoRameshnodesinthecampusoftheNationalChung-ChengUniversity
(Taiwan)whichimplementamulti-hopnetworkcoordinatedbyacentralgatewaywhichrequestssequentiallythedatafromeach
sensor [34]. It is clear that the main drawback of this proposal is the fact that the medium access is managed by the gateway,
thustheyhavebeenworkingmoreonthisprojectanddevelopedamechanismtosendemergencypacketsautomaticallyfromthe
nodes [35].
One of the first attempts to define multi-hop networks using LoRa is LoRaBlink [36]. They propose a TDMA protocol
that assumes the communication is only between the nodes and a sink, which uses beacons to synchronize the nodes in each
epoch, and it benefits from the concurrent transmission feature of LoRa to decode correctly at most only one packet in each slot
and receiver.
In [37] the authors present an anycast LoRa multi-hop application, known as LOCATE, to enable emergency warnings
where cellular connectivity is not available. This is achieved through a DTN dissemination mechanism which tries to avoid
collisions randomly.
Additionally, a linear multi-hop LoRa network is implemented inside the aqueducts of Siena (Italy) [38]. This system was
designed under the assumptions of an underground environment which is free of collisions. This ensures that the presented
synchronization algorithm can optimize the wake-up time of the nodes.
Finally, a new TDMA scheme especially designed to achieve low-latency multi-hop over LoRa was introduced in [39]. It
operatesinthreephases,aninitialonetobuildthetreestructureandassignthecorrectchannelandtimeslottothenodes.Next,
periodic groups of several upward and one downward cycles are executed in accordance with the initialization setup. Despite
positivepointsrelatedtolatencyandreliability,adeepstudyabouttheenergyconsumptionmustbedonetoevaluateitssuitability.
Regarding practical implementations, some efforts were made to standardize the LoRa stack using the open-source Contiki
OS,anopen-sourceoperatingsystemforresourceconstrainedIoTdevices,andtakeadvantageoftheincludedprotocolsforWSN
such as Routing Protocol for Low-Power and Lossy Networks (RPL) and Radio Duty Cycling (RDC), as well as enabling IPv6
connectivity.Thiswasfirstdevelopedin[40]forasimplepoint-to-pointlink.Then,in[41]theauthorsempoweredasmallLoRa
multi-hop network using a custom MAC layer using the fast loop technique to select the suitable 𝑆𝐹 (RLMAC) and the RPL
protocol. Further pursuing the desire to standardize LoRa networks, a complete framework called KRATOS for Contiki OS over
LoRaphysicallayerwasdevelopedandopentoeverybody[42].Similarly,anewprotocolstackcalledHARE[43]orientedtowards
the deployment of power-efficient uplink multi-hop wireless networks was implemented in Contiki OS. It takes advantage of the
existing protocols in Contiki, such as TDMA and RPL, to create a protocol stack which is agnostic to the LPWAN technologies
inthephysicallayer.SincethetraditionalContikiOSiscurrentlyabandoned,anewonewasreleasedin2017,Contiki-NG[44].
Precisely,in[45]theTCSHmechanismoftheIEEE802.15.4standardisadaptedtoLoRaunderthisnewIoTOS.This way,this
solution allows creating LoRa mesh networks using the RPL routing algorithm which meet the duty cycle regulation.
Furthermore,theIoTcompanyPycomrecentlydevelopedaMicroPythonAPIwhichenablesaneasyimplementationofLoRa
meshnetworks[46].ItwasimplementedusingtheOpenThreadstack,anopen-sourceimplementationofThread,aprotocolstack
designed by Google, which provides reliable communication and tries to standardize mesh networking technology. This solution
is used in [47] to send the information of fire-detecting sensors to the backend.
B. LoRaWAN Multi-Hop
As previously mentioned, there are other approaches that tried to extend a LoRaWAN network with multi-hop routing. One
alternativeisprovidingmulti-hoproutingbetweenend-devices,suchasin[48]whereamodifiedversionofDSDVroutingprotocol
issuccessfullyimplementedinalineartopologyofnodes,althoughenergyconsumptionisnotconsidered.Besides,underground
sensors are considered in [49] using a tree topology with TDMA synchronization for the receive slots, which reduces power
consumption. Finally, [50] sets a variation of LoRaWAN out, indeed it keeps in mind the imbalance coverage of the gateways to
establish the routing tables of the end-devices.
Theotheralternative,whichhasbeenwidelyexploited,isprovidingmulti-hoproutingbetweenintermediategateways,suchas
in [51] mixingthe HWMP and AODVprotocols to encapsulate theLoRaWAN packets between finaland intermediate gateways.
A further proposal defining a new LoRaWAN class to create mesh networks between gateways (both final and intermediate
gateways), which employs estimated time-on-air as metric and packet aggregation and disaggregation to increase throughput, is
explained in [52].
C. Multi-Hop WSN
TheWSNfieldoffersinterestingalternativesforwirelessmulti-hopping.Althoughtheyaregenerallyolddesigns,itisworthy
to summarize their main characteristics, since they may inspire strategies for our purpose: create a LoRa based network with
multi-hop capabilities.
Sensor MAC (S-MAC) [53] is considered one of the first medium access protocols for sensor networks. Inspired in the
RST/CTS mechanism of the 802.11 standard, which provides collision avoidance and good scalability, it is the basis of many
other ones. InS-MAC, nodes are programmed to sleep during long periods of timeto save energy and controlthe duty cycle, so
theyhavetodisseminatetheirwake-upschedulestotheneighbourstoenablesynchronizationamongtransmissionandreception.
Given that idle listening is one of the main sources of energy waste, in Timeout MAC (T-MAC) [54] the active period ends
earlier.Similarly,theAdaptiveenergyefficientMAC(AEEMAC) [55]proposesthreeoptimizationtechniquestosaveframeslots
by combining control packets and avoid overhearing using the information that has been sent to the channel.
The lightweight MAC (LMAC) [56] protocol is based on another strategy: a distributed TDMA synchronization. This is
carried out indicating which time slots are occupied in the current broadcast coverage area, and assigning a free time slot on
it randomly.

5
WiseMAC [57] combines Preamble Sampling technique with learning neighbours’ sampling schedule: nodes must sample
the channel for a short time periodically to receive data, and must send a preamble before sending the data frame at the correct
moment of the receiver. The information about the receiver wake-up schedule is computed from the control information in the
ACKframes.Inthecaseofthefirstcommunicationtoperformbyanode,alongpreambleisusedtobedetectedbyanyneighbour.
B-MAC [58] obtains good performance by executing the Clear Channel Assessment (CCA) procedure, a CSMA-based
mechanism to estimate noise floor using software automatic gain control, before transmitting. When the channel is empty, some
preamblesaresenttoawarethereceiveraboutthenextdataframe.Nodesareconfiguredtostayasleepforlongtimeperiodsand
wake up periodically to check potential receptions.
PMAC[59]adoptsacompletelynewscheme:eachnodeshareswiththeneighbourhooditstentativesleep-awakepattern(string
ofbits)overseveralslottimes,sotheyknowthepotentialmomentstobeactive.Thisactivitypatternisgeneratedaccordingtothe
networktraffic.Theresultsstandoutovertraditionalapproaches,suchasS-MAC,intermsofpowerconsumptionandthroughput.
In the X-MAC [60] protocol the main aim is minimizing the energy waste in nodes that are listening to data frames that are
notaddressedtothem.Thus,inX-MACthetransmittersendsashortstrobedpreamblewithinformationaboutthereceiver.Then,
the target node acknowledges the reception the earliest possible using pauses between preambles, and the rest of nodes go back
to sleep quickly. In addition, an optimal algorithm to control duty cycle is presented, resulting network traffic load adaptation.
In AS-MAC [61], nodes wake up periodically to receive data and the transmission of data is scheduled to the target node’s
receivingwindow.Concretely,whenanodehasapackettosend,it waitsfortherightmoment,whenthereceiverisawake.This
moment might also be a “Hello time” when the receiver sends a Hello packet with information about scheduling and offset time
beforethedatapacket.Beforetheperiodiclistening-sleepphase,aninitializationisperformedtodiscoverthedirecttopologyand
set the node up.
Finally,anothervaluableideaisintroducedinReceiver-InitiatedMAC(RI-MAC)[62],whosenodeswakeupperiodicallyand
broadcast a beacon to notify any transmitter that they are ready to receive data. The data frames are acknowledged by another
beacon which allows the same transmitter to send more data if necessary. Therefore, collision and overhearing are reduced,
and it can operate over a wide range of traffic loads. Following up on this idea, PW-MAC [63] changes the fixed schedule to
pseudo-random schedule which avoids neighbour nodes to wake up at the same time constantly.
D. Comparison
Theavailableapproachesformulti-hopmightbeorganizedintotwomaingroups:(i)LoRaandLoRaWANsolutionsand(ii)
WSN protocols, whose main characteristics and performance results are summarized in Tables I and II respectively. The column
LinkLayersdisplaysthelinkprotocolsusedtocontrolthemediumaccessandtosynchronizethecommunications.Thosesolutions
basedontimedivisionandchannelactivitydetectionmustbehighlightedsincetheyachievelowconsumptionandgoodreliability,
as well as protection against collisions. The column Network Layers shows the network protocol chosen to enable routing and
topologyshaping,whereasthecolumnCross-Layershowsiftheproposalcombineslinkandnetworklayersinasingleone.Since
WSN protocols are mainly link layer ones, these two last columns were not included in Table II. Regarding the performance,
we completed an in-depth analysis of the publications to determine their relative Reliability, Consumption or Latency. Both
tables include a column with a qualitative assessment of (i) Reliability, the degree of messages that are correctly delivered, (ii)
Consumption, the amount of energy required for the proposal to properly work, (iii) Latency, the delay to reach the collector of
themessagesand(iv)theDutyCycleLimit,whichstatesiftherestrictionsonusageoffrequencybandsthatareregulatedbylaw
are respected or not.
IV. JMAC:ANEWPROTOCOL
Ourproposalisdesignedforsensingsmartcitiesand,consequently,hastofulfilseveralcharacteristics.First,(i)weconsidered
a cross-layer approach (combining link and network layers) to support a complete and flexible solution for different applications
in smart cities. Second, and since sensors are powered by batteries, (ii) assuring low power consumption is essential. Since the
main purpose is gathering information from an indefinite number of sensors of different nature to, at least, one sink or gateway,
(iii) we propose to work under a tree-topology. Without losing flexibility, (iv) we assume the packet length is fixed by the APP
layer,whereas(v)periodicityofgenerateddataisconsideredtobelimitedtofifteenminutesatmost.Additionally,(vi)thedelay
todeliverapackettothefinaldestinationisunknown.Sincedownlinkmessages(fromgatewaytosensors)aremostlyintendedto
conduct control operations, (vii) we consider they are rarely sent, so they must be prioritized (viii). We also assume that (ix) the
sensing network is fixed, with sporadic changes is the topology (addition of new devices and/or shutoff of sensors). Finally, (x)
sinceLoRaworksonlicensefreebutregulatedbands,thenewprotocolmustcomplytheregulationrelatingmaximumtransmission
power, radio frequency channel arrangement and duty cycle over the usage of the channel.
Consequently, our proposal, the JMAC protocol, broadly consists of a cross-layer architecture formed by a link layer similar
toAS-MAC[61]andRI-MAC[62]protocolsandanetworklayerinspiredbyatreestructurewithmeshedrouting.Itsupportstwo
typesofdevices.First,agateway(orsink)thatisthedestinationoftheuplinkmessages.Itservesasliaisonwiththefinalback-end
and is the root node of the tree topology. It is always in receiver mode, except when it has to send control messages downwards
thesensorsinthenetwork(half-duplex).Theremaybemorethanonegatewayinthesamenetworkforredundancyandtheyare
pluggedtothemainelectricitysupplyandhigh-capacityInternetconnections.Second,sensorsthatcollecttheinformationdirectly
from the local application and also collaborate among themselves to forward the messages across the network to the destination.
They are usually powered by batteries, so power consumption must be limited to extend lifetime of the devices.
JMACincludesamulti-hopschemedesignedtominimizetheenergyconsumptioninsensornodes.Withthisaim,theobjective
iskeepingnodessleepingaslongaspossible.Theywouldonlywakeupperiodicallytoreceiveaframe,andtherestofthetime
they can save energy by staying in stand-by/sleep mode. Thus, the underlying idea is to know when the next-hop node is awake
toreceivedataandschedulethetransmissionofmessagestothatmoment.Tobeabletopredictnext-hop’swaking-uptime,each
sensormustannounceitstimeperiod𝑇 (thetimewhileanodehasitsradioactiveforreception)andtheremainingtime(Offset)
for its next receiving wake-up moment (wakingTime). That way, neighbours can estimate the right moment when the sensor will

6
TABLE I: Summary of the structure, main objectives and evaluation of the LoRa/LoRaWAN proposals.
|     |     |     |     |     |     | Reliability/ | Duty |
| --- | --- | --- | --- | --- | --- | ------------ | ---- |
Network
|     | Ref. LinkLayer |     |       | Cross-Layer | Objective | Consumption/ | Cycle |
| --- | -------------- | --- | ----- | ----------- | --------- | ------------ | ----- |
|     |                |     | Layer |             |           | Latency      | Limit |
CT
|     | [33] |     | Broadcast | No  | Reliability | High/-/- | No  |
| --- | ---- | --- | --------- | --- | ----------- | -------- | --- |
TDMA
Tree
[34]
|     | Centralized |     | Distance | No  | Reliability | High/High/Medium | No  |
| --- | ----------- | --- | -------- | --- | ----------- | ---------------- | --- |
|     | [35]        |     | Vector   |     |             |                  |     |
|     |             |     | Tree     |     | Consumption |                  |     |
TDMA
|     | [36] |     | Distance | Yes | Reliability | High/-/Medium | No  |
| --- | ---- | --- | -------- | --- | ----------- | ------------- | --- |
CAD
|     |      |     | Vector     |     | Latency     |                 |     |
| --- | ---- | --- | ---------- | --- | ----------- | --------------- | --- |
|     |      |     | Anycast    |     | Reliability |                 |     |
|     | [37] | -   |            | No  |             | Medium/High/Low | No  |
|     |      |     | withmemory |     | Latency     |                 |     |
Consumption
|     | [38] | TDMA | Broadcast | No  |     | High/Medium/Low | No  |
| --- | ---- | ---- | --------- | --- | --- | --------------- | --- |
Reliability
|     | Distributed |     | Tree |     |     |     |     |
| --- | ----------- | --- | ---- | --- | --- | --- | --- |
Reliability
|     | [39] | TDMA | Distance | Yes |     | High/-/Low | No  |
| --- | ---- | ---- | -------- | --- | --- | ---------- | --- |
Latency
|     | andCAD     |     | Vector |     |     |            |     |
| --- | ---------- | --- | ------ | --- | --- | ---------- | --- |
|     | [41] RLMAC |     | RPL    | No  | -   | -/-/Medium | Yes |
|     | [42]       | -   | RPL    | No  | -   | -/-/-      | Yes |
TDMA
|     | [43] |     | RPL | No  | -   | -/-/High | Yes |
| --- | ---- | --- | --- | --- | --- | -------- | --- |
CSMA/CA
|     | [45] | TSCH | RPL | No  | Reliability | -/-/- | Yes |
| --- | ---- | ---- | --- | --- | ----------- | ----- | --- |
Reliability
|     | [46] | LBS | IPv6 | No  |     | High/-/- | No  |
| --- | ---- | --- | ---- | --- | --- | -------- | --- |
Security
Modified
LoRaWAN
|     | [48] | CAD |     | No  | Reliability | Medium/-/- | No  |
| --- | ---- | --- | --- | --- | ----------- | ---------- | --- |
andDSDV
Tree
|     | [49] | TDMA | Distance | No  | Reliability | Medium/-/Medium | No  |
| --- | ---- | ---- | -------- | --- | ----------- | --------------- | --- |
Vector
Tree
|     | [50] | TDMA | Distance | Yes | Reliability | -/-/- | No  |
| --- | ---- | ---- | -------- | --- | ----------- | ----- | --- |
Vector
HWMP
|     | [51] | CAD |     | No  | Reliability | -/High/Low | No  |
| --- | ---- | --- | --- | --- | ----------- | ---------- | --- |
AODV
Modified
|     | [52] LoRaWAN |     | AODV | No  | Reliability | -/High/Low | No  |
| --- | ------------ | --- | ---- | --- | ----------- | ---------- | --- |
bereadytoreceivepacketstakingthearrivaltimeofthelastannounce(lastSeen)andthetransmissiontimeofthemessage(ToA)
| into consideration | as it is shown | as follows: |            |                          |     |     |     |
| ------------------ | -------------- | ----------- | ---------- | ------------------------ | --- | --- | --- |
|                    |                |             | 𝑤𝑎𝑘𝑖𝑛𝑔𝑇𝑖𝑚𝑒 | =𝑙𝑎𝑠𝑡𝑆𝑒𝑒𝑛+𝑂𝑓𝑓𝑠𝑒𝑡−𝑇𝑜𝐴+𝑛·𝑇 |     |     |     |
(1)
where𝑛isamultipliertoensurethattheestimatedmomentisinthefuture.Thisistheidealapproximation,butlongtransmission
times on LoRa allows avoiding clock drifts and processing times on sensors and propagation delays of messages.
Toenableupwardrouting,eachsensorhastodisseminatethedistancetothegatewayℎ𝑜𝑝𝑠𝑇𝑜𝐺𝑎𝑡𝑒𝑤𝑎𝑦 toenablechildsensors
join the network and make parent nodes aware of their existence. The metric to route uplink messages is indeed the number
of hops to the gateway ℎ𝑜𝑝𝑠𝑇𝑜𝐺𝑎𝑡𝑒𝑤𝑎𝑦 and the next upward hop selection is done dynamically from all those available direct
parents (a node will create links with all the available nodes in range that are closer to the gateway), to choose the one which
wakes up earlier. Additionally, downlink traffic from the gateway to sensors can be routed by recording in each node the list
of children from each direct child. This way, parent nodes can extract from the frames identifiers of grandchildren nodes and
schedule downlink messages to the right intermediate node to reach the final destination. Nevertheless, as downlink messages
will be sporadic in data collection use cases, this version of the protocol does not include a downlink functionality, which will
| be completed         | as future work. |     |     |     |     |     |     |
| -------------------- | --------------- | --- | --- | --- | --- | --- | --- |
| A. Devices Operation |                 |     |     |     |     |     |     |
Gatewaysbehave as described by the Finite State Machine (FSM) shown in Figure 2a. Once the gateway is installed and
connected to the backend (INIT), it is ready to execute an endless loop centralized in RECEIVE_UP_DATA mode to handle
uplink messages from sensors or wait to send the next scheduled BEACON frame. Thus, if any message is received (frame), it
will be used to update the topology information (neighbour_map). In case of an UP_DATA frame, it will also be processed
| to prevent duplication | and an | ACK frame | will be | sent to the sensor | (SEND_ACK). |     |     |
| ---------------------- | ------ | --------- | ------- | ------------------ | ----------- | --- | --- |

7
TABLE II: Summary of the structure, main objectives and evaluation of the WSN protocols.
Reliability/
DutyCycle
|     | Reference | LinkLayer | Objective   | Consumption/    |       |
| --- | --------- | --------- | ----------- | --------------- | ----- |
|     |           |           |             | Latency         | Limit |
|     | [53]      | RTS/CTS   | Consumption | -/Medium/Medium | No    |
RTS/CTSand
|     | [54] |     | Consumption | -/Low/Medium | No  |
| --- | ---- | --- | ----------- | ------------ | --- |
EarlyTimeout
RTS/CTSand
|     | [55] |     | Consumption | -/Low/Medium | No  |
| --- | ---- | --- | ----------- | ------------ | --- |
CombiningPackets
|     | [56] | DistributedTDMA | Consumption | -/Low/Low | No  |
| --- | ---- | --------------- | ----------- | --------- | --- |
PreambleSamplingand
|     | [57] |     | Consumption | Medium/Low/Medium | No  |
| --- | ---- | --- | ----------- | ----------------- | --- |
NeighbourLearning
CCAand
|     | [58] |     | Consumption | High/Low/Medium | No  |
| --- | ---- | --- | ----------- | --------------- | --- |
PreambleSampling
|     |      | Sleep-AwakePatternand | Consumption |               |     |
| --- | ---- | --------------------- | ----------- | ------------- | --- |
|     | [59] |                       |             | High/Medium/- | No  |
|     |      | NeighbourLearning     | Throughput  |               |     |
StrobedPreamble
|     | [60] |     | Consumption | Medium/Low/Medium | No  |
| --- | ---- | --- | ----------- | ----------------- | --- |
Sampling
Asynchronous
|     |      | Wake-upand | Consumption |                 |     |
| --- | ---- | ---------- | ----------- | --------------- | --- |
|     | [61] |            | Reliability | High/Low/Medium | No  |
NeighbourLearning
|     |      | TargetPreamble | Consumption |              |     |
| --- | ---- | -------------- | ----------- | ------------ | --- |
|     | [62] |                |             | High/Low/Low | No  |
|     |      | Sampling       | Reliability |              |     |
TargetPreamble
|     | [63] | Samplingand   | Consumption | High/VeryLow/Low | No  |
| --- | ---- | ------------- | ----------- | ---------------- | --- |
|     |      | Pseudo-Random | Reliability |                  |     |
NeighbourLearning
Otherwise,ifthetimeoutforthenextBEACONexpires(beacon_timeout),thegatewayswitchestoSEND_BEACONstate
to broadcast the BEACON and set beacon_timeout again to come back to RECEIVE_UP_DATA mode. BEACON frames are
used for helping nodes to discover their neighbors. The time between each BEACON varies randomly between 15 and 25 s in
order to avoid messages from a direct children to interfere always with the scheduled BEACON of the gateway, if there were the
case.Inthisparticularcase,thefirstBEACONissent(SEND_BEACON)rightafterinitialization(INIT)tosimplifydevelopment.
Sensors operate in two phases (Figure 2b): an initial one to discover the surrounding neighbours, and a second one which
actually performs the JMAC protocol. The first one starts just after starting up, sensors need to wait in RECEIVE_INIT mode
for a single frame which allows them to join the network. After that, they enter an announcing phase in which they announce
periodically their information using a BEACON (SEND_BEACON) controlled by beacon_timeout, while the rest of the time
they expect receiving announcements (frame) from their neighbours to update the known topology (RECEIVE_ANNOUNCE).
Thedurationofthisinitializationphasecanbeconsideredtobenegligibleinconsumptiontermsbecausethejoiningphaseisset
to a maximum of 5 min, and if it is not possible, the procedure is restarted and a notification is displayed through some user
| interface (e.g., | a LED is turned | on). |     |     |     |
| ---------------- | --------------- | ---- | --- | --- | --- |
Uponcompletionofinitializationphase,thenewnetworkisreadytorun.First,eachnodeopensareceptionwindowtoreceive
oneUP_DATAframefromachild(RECEIVE_DATA).Ifanyframeisreceived,itisusedtoupdateneighbour_mapandifit
isalsoanUP_DATAframe,thedatapayloadisinsertedinaqueueandanACKframeistransmittedtothecorrespondingchild
(SEND_ACK).Conversely,iftimeoutexpiresorthereceivedframeisnotUP_DATAtype,itdirectlygoestoWAIT_OR_SLEEP
mode.
InWAIT_OR_SLEEPstate,sensorsactivatepower-savingmodeandestimatewhethertheclosestparent(next_hop)willbe
listening on the channel during any moment of that time interval𝑇. Additionally, a new parameter𝐶 is included which manages
the probability of sending to the designated next_hop (1) in order to avoid potential collisions between sensors which would
𝐶
transmitatthesametime.Ifallgoeswell,thesensorwillwaituntilthedesirednext-hop’sawaking_time(WAIT_NEXT_HOP),
otherwise until the sensor has to wake up again to start over the periodic operation (SLEEP).
At the end of the WAIT_NEXT_HOP state, the sensor checks if there is any pending data stored in the queues (both from
the upper application layer and children nodes). If this is the case, a new UP_DATA frame is created with a packet from the
localrunningapplication(ifany)andatmost𝑐 𝑚𝑎𝑥 aggregatedpacketsfromchildren.Inothercaseitremainsinsleepmodeand
| changes to | SLEEP state. |     |     |     |     |
| ---------- | ------------ | --- | --- | --- | --- |
ThegeneratedUP_DATAframeistransmittedwhenthecorrespondingnext_hopisexpectedtobeawake(SEND_UP_DATA).
If the packet is received correctly by the next_hop, the sensor will receive back an ACK and the information can be deleted
fromthequeues(RECEIVE_ACK).AfterexitingtheRECEIVE_ACKstate,thesensorcomesbacktoWAIT_OR_SLEEPmode.
By doing so, it would be possible to send data to multiple parents in the same operational period𝑇.
Finally,Figure3showsanexampleoftheoperationoftheJMACprotocolwhenbothkindofdevicesareinvolved(Gateway
and Sensors).

8
RECEIVE_DATA
up_data_frame
|     |     |     |     |     |     |          |     |          | t im e o u t 	O R 	           |
| --- | --- | --- | --- | --- | --- | -------- | --- | -------- | ----------------------------- |
|     |     |     |     |     |     | SEND_ACK |     | NOT(up_d | a ta _ fr a m e 	f rom	child) |
INIT
ack_sent
timeout
INIT
|     |     |     | RECEIVE_INIT |     |     | WAIT_OR_SLEEP         |     |     |     |
| --- | --- | --- | ------------ | --- | --- | --------------------- | --- | --- | --- |
|     |     |     | frame        |     |     | send_now	AND	next_hop |     |     |     |
NOT(send_now)	OR
| SEND_BEACON |     |                | SEND_BEACON |     |     | WAIT_NEXT_HOP |                | NOT(next_hop) |     |
| ----------- | --- | -------------- | ----------- | --- | --- | ------------- | -------------- | ------------- | --- |
|             |     | beacon_timeout | beacon_sent |     |     | awa k in g _  | t im e 	 A ND	 |               |     |
beacon_timeout beacon_sent frame N O T ( e m p t y ) aw a k in g _t im e
|     | frame |     |     |     |     |     |     | A N D 	e m p ty |     |
| --- | ----- | --- | --- | --- | --- | --- | --- | --------------- | --- |
RECEIVE_ANNOUNCE
SEND_UP_DATA
timeout
RECEIVE_UP_DATA
|     |     |     |     |     | timeout	 | up_data_sent |     |     |     |
| --- | --- | --- | --- | --- | -------- | ------------ | --- | --- | --- |
OR	frame
up_data_frame
RECEIVE_ACK
ack_sent
| SEND_ACK |     |     |     |     |     | timeout |     |     |     |
| -------- | --- | --- | --- | --- | --- | ------- | --- | --- | --- |
SLEEP
| (a) |      |           |               |     |         | (b)         |     |     |             |
| --- | ---- | --------- | ------------- | --- | ------- | ----------- | --- | --- | ----------- |
|     | Fig. | 2: Finite | State Machine | (a) | Gateway | (b) sensor. |     |     |             |
|     |      | U A       | U A U         | A   | UU      | AA          | UU  | AA  | UU AA UU AA |
Gateway
|     |     | U A | U A U | A   | U A U | A   |     |     | UU AA |
| --- | --- | --- | ----- | --- | ----- | --- | --- | --- | ----- |
Sensor	1
|     |     |     | APP |     |     |     |     |     | APP     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- |
|     | U A | U A |     |     |     |     | UU  | AA  | U UU AA |
Sensor	2
|     |     |     |     |     |     |     | AAPPPP |     | APP |
| --- | --- | --- | --- | --- | --- | --- | ------ | --- | --- |
|     | U A | U A |     | U   | U A |     |        |     |     |
Sensor	3
|     | APP | APP | APP |     |        |          |           |     |         |
| --- | --- | --- | --- | --- | ------ | -------- | --------- | --- | ------- |
|     |     |     |     |     | SLEEP: | RX_IDLE: | RX_ERROR: |     | RX: TX: |
Fig. 3: Example of the operation of the JMAC protocol (U → UP_DATA, A → ACK).
B. Frame Format
Theprotocoloperatesusingthreetypesofframesthatsharethefirsttwofields:(i)theType,composedof3bitstodistinguish
the message type in reception (it has capacity for future messages types) and (ii) the Source, 8 bits long to identify the source
node.Thus,itispossibletoaddnewfuturemessagestypesand,sincethegatewayisidentifiedusingtheaddress0,eachnetwork
is limited to 255 sensors.
The first type of frame, BEACON (B), is used to advertise neighbours that a node exists in the coverage area. When sent by
a gateway, it only carries the common part (blue part in Figure 4) because gateways are the sink nodes and are always listening
on the channel (except when transmitting). When sent by sensors, they also include the green part in Figure 4), which is (i) the
number of hops Hops to the gateway, which is only 2 bits and limits multi-hop to 4 hops; (ii) the time period Period and (iii)
the time offset Offset with 64 bits to express each one to calculate the next awaking time accurately, and a list of at most𝑐
𝑚𝑎𝑥
child addresses.
The UP_DATA (U) frame (Figure 4) is generated by sensors to carry the application data of the current sensor and its
children. Besides including all the fields that the BEACON (B) frame has, this second frame also contains a 10 bits sequence
numberSequence,whichisusedtoacknowledgetheframeinadirectlinkandtoassociatetheMy_Datapayloadoffixedlengthof
𝑀 bytes.ItalsocontainstheChild_*_DatapayloadandChild_*_Sequencesequencenumbertoforwardtheinformationgenerated
by its children nodes. If there is no application data in the current sensor, My_Data is empty.
Finally,theACK(A)frame(Figure5)confirmsthattheimmediatelyprecedingUP_DATAframeidentifiedbySequence_To_Ack
was correctly received.
It is also worth mentioning that depending on the amount of data 𝑀, the corresponding network allows sending in the same
UP_DATA frame up to𝑐 children, considering the LoRa 255 bytes payload constraint. The way to calculate this limitation is
𝑚𝑎𝑥
expressedinEquation2anditlimitsUP_DATAandACKframestohaveamaximumlength.Thus,forinstance,when𝑀 =100𝐵,
the network only supports 1 children, but when 𝑀 =10𝐵 it is possible to have 18 children:
|     |     | (cid:22) 255·8−3−8−2−64−64−10−𝑀·8 |     |     |     | (cid:23) |     |     |     |
| --- | --- | --------------------------------- | --- | --- | --- | -------- | --- | --- | --- |
𝑐
𝑚𝑎𝑥 = (2)
8+10+𝑀·8

9
TYPE SOURCE HOPS PERIOD OFFSET CHILD_1...CHILD_C MY_DATA SEQUENCE CHILD_1_DATA...CHILD_C_DATA CHILD_1_SEQ ... CHILD_C_SEQ
Fig. 4: Format of the UP_DATA frame from sensor.
TYPE SOURCE DESTINATION SEQUENCE_TO_ACK
(a)
TYPE SOURCE HOPS PERIOD OFFSET CHILD_1 ...CHILD_C DESTINATION SEQUENCE_TO_ACK
(b)
Fig. 5: Format of (a) the ACK frame from gateway and (b) the ACK frame from sensor.
Bothreceptionwindowsarecontrolledbyatimeoutsettothepertinentmaximumframelength(𝑈𝑃_𝐷𝐴𝑇𝐴 𝑚𝑎𝑥 or𝐴𝐶𝐾 𝑚𝑎𝑥)
fromasensornodetoallowcompletingthereceptionintheworstcasescenario.Apart,thepropagationdelayisconsideredbecause
nodesmightbefarawayfromeachotherandthepropagationdelayinLoRaisnotmarginal,soadistanceof15kmwaschosen
because it is the upper limit coverage in LoRa for urban areas.
𝑡𝑖𝑚𝑒𝑜𝑢𝑡(𝑈𝑃_𝐷𝐴𝑇𝐴)=𝑇𝑜𝐴(𝑈𝑃_𝐷𝐴𝑇𝐴 𝑚𝑎𝑥)+𝑝𝑟𝑜𝑝𝑎𝑔𝑎𝑡𝑖𝑜𝑛𝐷𝑒𝑙𝑎𝑦(15𝑘𝑚) (3)
𝑡𝑖𝑚𝑒𝑜𝑢𝑡(𝐴𝐶𝐾)=𝑇𝑜𝐴(𝐴𝐶𝐾 𝑚𝑎𝑥)+𝑝𝑟𝑜𝑝𝑎𝑔𝑎𝑡𝑖𝑜𝑛𝐷𝑒𝑙𝑎𝑦(15𝑘𝑚) (4)
C. Time Period
The time period𝑇 is the time when a node listens for new messages. In our protocol we take into account the worst case
scenario (Figure 6) where a sensor node receives one UP_DATA frame and has to send back the corresponding ACK, and in
average has the opportunity to transmit an UP_DATA frame to 𝑝/𝐶 parents, whose reception windows are inside the same time
interval for the child sensor. Thus, the time period𝑇 is calculated respecting also the band duty cycle regulation. Precisely, this
only affects the active usage of the channel, so as it expressed in the equation it only covers the transmissions of longest frames
(𝐴𝐶𝐾 𝑚𝑎𝑥 and𝑈𝑃_𝐷𝐴𝑇𝐴 𝑚𝑎𝑥) and is expanded according to the corresponding duty cycle 𝐷𝐶 limit.
In this way, when there are many available parents 𝑝, the time period 𝑇 increases to ensure that sensors keep sleeping
enoughtimetopreservelowconsumption.Onthecontrary,thehigherparameter𝐶,thelowertimeperiod𝑇,whichavoidshaving
extremelylongdelaysinfinalmessagedelivery.Theapplicationpayloadlength𝑀 hasalsolittleeffectinitsvariation,ascanbe
seen in Table III.
V. VALIDATION
We carried out a complete set of experiments using the OMNeT++ simulator [11] to validate our proposed protocol JMAC.
We started by developing a realistic LoRa framework within OMNeT++ (Section V-A). Then, we simulated a simple testbed to
checktheperformanceaccordingtothedifferentparameters(SectionV-B).Finally,wealsostudiedthebehaviourofJMACusing
a more complex scenario with a denser topology to analyze the scalability and the performance of the protocol (Section V-C).
A. FLoRaPHY: A New LoRa Framework for OMNeT++
LoRaisaradiotechnologywithmanyfeaturesthatarenotcurrentlysupportedinOMNeT++.Thus,wecreatedanewmodule
for OMNeT++ using FLoRa [30], which is focused on LoRaWAN, as a base for our work. FLoRaPHY is a new module that
simulates the behaviour of the available information regarding the LoRa physical layer.
FLoRaPHY, follows the hierarchy of the INET framework [29], the OMNeT++ model suite for wired, wireless and mobile
networks. This framework defines two big blocks: FlatRadioBase and RadioMedium. We extended them in (i) LoRaRadio
and (ii) LoRaMedium, as Figure 7 details.
LoRaRadioextendstheFlatRadioBaseclassandmodelsthespecialLoRareceptionissueofcapturingthemostpowerful
signalthatissimultaneouslyavailableonthemedium.ThisactiondoesnottrulyreflecttheactualbehaviourofLoRamodulation
becauseforcapturingatmostoneofthesignalstheSNIRmustbeoveraspecificthresholddependingontheSFsineachsignal,
butitfacilitatestheverificationofthemainprotocolandassumesthatcollisionrateiszero.ItalsocomputestheToAofaframe
according to the parameter setup and payload. It is composed of the following blocks (Figure 7a):
• LoRaTransmitter: it extends FlatTransmitterBase and is in charge of creating the transmissions.
• LoRaReceiver: it inherits from FlatReceiverBase and is responsible for computing whether signal decoding is
possible according to the sensitivity of the transceiver and channel interference. It may discard the reception if it collides
with interference signals as discussed above.
• IsotropicAntenna: it describes an ideal isotropic antenna, i.e., it radiates the same signal intensity in all directions.
• LoRaStateBasedEpEnergyConsumer: it records the power consumption of the radio module according to its state.
LoRaMedium decides which transmitted signals would arrive to each node according to the following models:
• LoRaAnalogModel: it models how a radio signal arrives to destination, specifically, it computes the final reception, RSSI
and SNIR.
• LoRaPathLossOulu:itcalculatesthepathlossoftheradiosignalinspiredinthepathlossmodelofthecityofOulu[64],
but variability was reduced to simplify simulations.

10
|     | U A |     | U   | A   |     | U A |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
...
|     |     |     |     |         |         |                      | RX:  | TX:         | SLEEP:       |     |
| --- | --- | --- | --- | ------- | ------- | -------------------- | ---- | ----------- | ------------ | --- |
|     |     |     |     | Fig. 6: | Average | worst case situation | of a | time period | in a sensor. |     |
|     |     |     |     | period𝑇 |         |                      |      | 𝑀           |              | 𝑀   |
TABLE III: Time for an application payload of (a) =30 B and (b) =100 B.
|     |     |     |     |     | 𝑴=30B  | 𝒑=1       | 𝒑=2       | 𝒑=3        |     |     |
| --- | --- | --- | --- | --- | ------ | --------- | --------- | ---------- | --- | --- |
|     |     |     |     |     | 𝑪=1    | 44.032s.  | 81.9968s. | 119.9104s. |     |     |
|     |     |     |     |     | 𝑪=2    | 25.1264s. | 44.0832s. | 63.0400s.  |     |     |
|     |     |     |     |     | 𝑪=3    | 18.8075s. | 31.4453s. | 44.0832s.  |     |     |
|     |     |     |     |     | 𝑪=4    | 15.6480s. | 25.1264s. | 34.6048s.  |     |     |
|     |     |     |     |     | 𝑴=100B | 𝒑=1       | 𝒑=2       | 𝒑=3        |     |     |
|     |     |     |     |     | 𝑪=1    | 40.4992s. | 75.3508s. | 110.1824s. |     |     |
|     |     |     |     |     | 𝑪=2    | 23.0784s. | 40.4992s. | 57.9200s.  |     |     |
𝑪=3
|     |     |     |     |     |     | 17.2715s. | 28.8853s. | 40.4992s. |     |     |
| --- | --- | --- | --- | --- | --- | --------- | --------- | --------- | --- | --- |
|     |     |     |     |     | 𝑪=4 | 14.3680s. | 23.0784s. | 31.7888s. |     |     |
• ConstantSpeedPropagation:itisusedtoemulatethepropagationdelaytimeoftransmissionsinaccordanceoftraveled
distance.
| •   | IsotropicScalarBackgroundNoise: |     |     |     |     | it adds uniform | noise to | the medium. |     |     |
| --- | ------------------------------- | --- | --- | --- | --- | --------------- | -------- | ----------- | --- | --- |
Additionallytothislinklayer,itisnecessarytocreatethesoftwaretosupportthecross-layerprotocolJMACforOMNeT++,
whichcombinesthelinklayer(describedabove)andthenetworklayerinasingleone.Withthisaim,wecreatedanewbaseclass
MacNetworkProtocolBase that combines both link and network layer functionalities. From it, we created the abstract class
JMACusedtoimplementcommonfeaturesofthenewprotocol.ThisJMACwasextendedforaparticulargateway(JMacGateway)
| and | sensor (JMacSensor). |     |     |     |     |     |     |     |     |     |
| --- | -------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Sensors were configured to wake up randomly when the simulation starts and they are fed from a dummy application layer
which generates fake data of length 𝑀 each 15 min from the moment they enter the operational loop. Finally, JMAC instances
record information about the exchanged messages with the aim of generating a final report to evaluate our proposal according to
| the | following | three metrics: |     |     |     |     |     |     |     |     |
| --- | --------- | -------------- | --- | --- | --- | --- | --- | --- | --- | --- |
• Packet delivery Ratio (PDR): it is the percentage of successfully received UP_DATA frames, i.e., UP_DATA frames which
havereceivedthecorrespondingACKframe,overthetotalsent.ItislocaltotheJMacSensornodeanditusuallyconverge
|     | if the system | is  | static. |     |     |     |     |     |     |     |
| --- | ------------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- |
• End-to-end delay: it is the time taken for an application packet to arrive to the JMacGateway. It depends on the load of
thepathtothegateway,soitisarandomvariablewhichmaybeidentified.Ifthesystemiscongesteditwillgrowinfinitely
|     | because | packets | will never | arrive | to destination. |     |     |     |     |     |
| --- | ------- | ------- | ---------- | ------ | --------------- | --- | --- | --- | --- | --- |
Throughput:itistheratiobetweenthepayloadlengthoftheapplicationpacket𝑀
| •   |           |           |       |        |          |              |     |     | andtheend-to-enddelay.Itestimatesthe |     |
| --- | --------- | --------- | ----- | ------ | -------- | ------------ | --- | --- | ------------------------------------ | --- |
|     | effective | data rate | which | can be | achieved | by a sensor. |     |     |                                      |     |
Finally,toadjustthesimulatorwithrealisticparameters,weusedthecharacteristicsoftheSX1276transceiver[65].Inorder
to estimate the average power consumption of each sensor and check if the theoretical consumption is compatible with a 1000
mAh battery, we modeled the consumption of the SX1276 transceiver in OMNeT++ according to the state of its radio: (i) when
the transceiver is OFF, its consumption is 0.2μA; (ii) if it is in SLEEP mode, its consumption is 1.5μA; (iii) if it is RX_IDLE,
the transceiver is ready but the channel is empty, its consumption is 1.6 mA; (iv) if it is RX, receiving a signal, its consumption
| is 10.3 | mA;       | and, finally, | (v) | if it is | TX, transmitting | a frame, | its consumption | is 29 | mA. |     |
| ------- | --------- | ------------- | --- | -------- | ---------------- | -------- | --------------- | ----- | --- | --- |
| B.      | Testbed1: | Checking      | the | Impact   | of Parameters    |          |                 |       |     |     |
In this first approach, we used a simple and low-density network (Figure 8a) and a small combination of possible values
for the parameters (𝑀 = 30 B, 50 B, 100 B and 𝐶 = 1,2,3,4). The three aforementioned metrics (PDR, end-to-end delay and
throughput) were evaluated on average over 20 runs of each experiment, which emulates the operation of the network during
7 days.
According to the results summarized in Figure 9a, we can conclude that using a higher𝐶 parameter significantly improves
thePDRinallsensors,sinceitmakeslessprobabletohavetwoormoredevicestransmittingduringthesamereceivingwindow.
𝐶
Thus, a low value for could cause interference and all devices, except the most powerful one, would have to retransmit.
Theapplicationpayloadlength𝑀 hasverylittleimpact,exceptfortheparticularcase𝑀 =100and𝐶
=1becauseitonlyallows
sendinginformationaboutonechildatatimecausinghighloadperiodsthatwillgeneratemoremessagesandpotentialcollisions.
|     | It is important | to  | remark | that: |     |     |     |     |     |     |
| --- | --------------- | --- | ------ | ----- | --- | --- | --- | --- | --- | --- |

11
RadioMedium
FlatRadioBase
LoRaMedium
LoRaRadio
|     |                     |     |                  |     |                  |     | ScalarAnalogModelBase |     | LoRaAnalogModel          |     |                   |
| --- | ------------------- | --- | ---------------- | --- | ---------------- | --- | --------------------- | --- | ------------------------ | --- | ----------------- |
|     | FlatTransmitterBase |     | LoRaTransmitter  |     |                  |     |                       |     |                          |     |                   |
|     |                     |     |                  |     |                  |     |                       |     | LoRaPathLossOulu         |     | FreeSpacePathLoss |
|     |                     |     | LoRaReceiver     |     | FlatReceiverBase |     |                       |     |                          |     |                   |
|     | AntennaBase         |     | IsotropicAntenna |     |                  |     | PropagationBase       |     | ConstantSpeedPropagation |     |                   |
LoRaStateBasedEpEnergyConsumer StateBasedEpEnergyConsumer IsotropicScalarBackgroundNoise IBackgroundNoise
|     |     |     |      | (a)          |                  |     |       |                    |     | (b)    |     |
| --- | --- | --- | ---- | ------------ | ---------------- | --- | ----- | ------------------ | --- | ------ | --- |
|     |     |     | Fig. | 7: Structure | of (a) LoRaRadio |     | class | and (b) LoRaMedium |     | class. |     |
• Sensors1and2achievesimilarresults,butevenwhen𝐶 ishigherthanonethePDRisnot100%becausethegatewaydoes
not have a specific receiving window and it may happen that UP_DATA messages interfere with BEACON or ACK frames
| from | the | gateway, | but still | performance | is really good. |     |     |     |     |     |     |
| ---- | --- | -------- | --------- | ----------- | --------------- | --- | --- | --- | --- | --- | --- |
• Sensor 4 performs worse than sensors 3 and 5 because both parents (sensors 1 and 2) are shared with the other sensors,
| and | there | are more | probability | to interfere. |     |     |     |     |     |     |     |
| --- | ----- | -------- | ----------- | ------------- | --- | --- | --- | --- | --- | --- | --- |
• Sensor 6 has better PDR compared to sensors 7 and 8 because it has his own parent (sensor 4), apart from the shared one
| (sensor | 5). |     |     |     |     |     |     |     |     |     |     |
| ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
• The PDR in sensor 10 is quite better than its sibling sensor 9 because it benefits from two parents simultaneously.
Regardingenergyconsumption,fortheselectedvaluesfor𝑀 andtakingintoaccountthattimeperiod𝑇
decreaseswhenthey
increase,wecanobservehowsensorsstayactivemoretime.Then, asshowninFigure9b,theytendtowastemoreenergywhen
ahigherpayloadissupported.Contrarytowhatwouldbeexpected,powerconsumptionincreaseswithparameter𝐶
becausetime
| period𝑇 |     |     |     |     |     |     |     |     |     | higher𝐶 |     |
| ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | --- |
is smaller and sensors keep sleeping less time. However, it increases lightly because the the more packets are
groupedinasingleframe,whenpossible.Besides,somesensorssufferfromabnormalhighpowerconsumptionfor𝑀 =100and
𝐶 =1, this peak results from the successive retransmissions which have to be done when the frame is interfered by another one.
| This | is the case | for sensors | 1,  | 2 4, 5, 6, | 7 and 8, which | have a | low PDR | in that situation. |     |     |     |
| ---- | ----------- | ----------- | --- | ---------- | -------------- | ------ | ------- | ------------------ | --- | --- | --- |
Figure10showstheresultsobtainedforbothaverageend-to-enddelayandthroughput.Itcanbeconcludedthatthehigherthe
numberofhopstothegateway,thehigherdelayandthelowerthroughput.Concretely,delayandthroughputareproportionaland
tothetimeperiod𝑇 andthedistancetothegateway.Moreover,𝐶 parameterhasanoticeableimpactinbothmetrics.Inaverage,
𝐶−1 out of𝐶 reception windows are skipped, so an increase in the value of𝐶 means further delay and slower effective data
rate. However, this effect is compensated with time period𝑇 formula, which decreases with higher𝐶. Furthermore, application
payload𝑀 onlyhasremarkableimpactonthedelayofsensorswhichhaveseveralchildren.Thatisthecasefor𝑀 =100,which
only supports sending information about a single children in each UP_DATA frame and latency is increased because messages
keep in the waiting queues longer when the network traffic is substantial. However, the impact of the payload length 𝑀 is not
marginal for the throughput and it will increase proportionally the effective data rate. There is a large variance anomaly of the
delay for 𝑀 =100 and𝐶 =1 for sensors 7, 8 and 10 because they share parents 5 and 2, which are nodes with many possible
end-to-end paths. The effect is less severe in sensor 10 because it also has sensor 6 as parent.
| C. Testbed2: |     | Checking | the | Scalability | and Performance |     |     |     |     |     |     |
| ------------ | --- | -------- | --- | ----------- | --------------- | --- | --- | --- | --- | --- | --- |
Asecondscenario(Figure8b)wasusedtostudythescalabilityandperformanceoftheprotocol.Specifically,itwasconfigured
with𝑀
=30B,becausemostofthetargetapplicationsforthisprotocolonlyrequiretransmittingsmallamountsofdata,andwe
𝐶
used = 3 in order to achieve a good PDR and not increasing delay and consumption. The simulation replicates a scenario
executing the protocol for 7 days and repeating 20 times, so the following results depict the average behaviour.
ConsideringtheaverageresultsfromFigure11a,theattainedPDRisgenerallyhigherforsituationswithlowtrafficdemand.
Oneoutstandingcaseisthegoodperformanceofsensors16and17(higherthan99%).Thisisbecausetheyhavethreecommon
parents,whichallowsthemtobalancethetraffic.AsshowninFigures11c,d,end-to-enddelayincreasesandthroughputdecreases
withthenumberofhopstothegateway,buttheyarenormallywithinreasonablevaluesforthisscenario.Havingseveralparents
imposesasubstantialincrementinthefinaldelay,suchisthecaseofsensors17and18,whichconsiderablyreducethedatarate.
Finally, and regarding the power consumption (Figure 11b), they turn out as expected. On one side, leaf nodes consume a low
amount of power as they rarely transmit and do not usually receive a message for them. On the other side, sensors which act as
| relayers | require | higher | amounts | of energy. |     |     |     |     |     |     |     |
| -------- | ------- | ------ | ------- | ---------- | --- | --- | --- | --- | --- | --- | --- |
Given this realistic scenario, it is useful to estimate whether an ordinary battery (1000 mAh) is adequate for having long
3.3
life cycle. To do so, the average highest consumption will be selected (sensor 1) and a power supply of V will be assumed.
Theestimateddurationofthebatteryfortheworstcaseunderidealcircumstancesassumedinthisstudyislongerthanoneyear,
so this deployment could be adopted without the need for maintenance for a long period of time:
|     |     |           |                   |     | 𝑃𝑜𝑤𝑒𝑟𝑆𝑢𝑝𝑝𝑙𝑦      |            |           | 3.3𝑉    |                  |     |      |
| --- | --- | --------- | ----------------- | --- | ---------------- | ---------- | --------- | ------- | ---------------- | --- | ---- |
|     |     | 𝐿𝑖𝑓𝑒𝐶𝑦𝑐𝑙𝑒 | =𝐵𝑎𝑡𝑡𝑒𝑟𝑦𝐶𝑎𝑝𝑎𝑐𝑖𝑡𝑦· |     |                  |            | =1000𝑚𝐴ℎ· |         | =13,772.96ℎ.≈573 |     | days |
|     |     |           |                   |     | 𝑃𝑜𝑤𝑒𝑟𝐶𝑜𝑛𝑠𝑢𝑚𝑝𝑡𝑖𝑜𝑛 |            |           | 239.6𝜈𝑊 |                  |     |      |
|     |     |           |                   |     | VI.              | DISCUSSION |           |         |                  |     |      |
the𝐶
After analysing the conducted experiments, we can conclude some relevant aspects. First, parameter always cause a
𝐶,
notable variation in the performance: the higher the better PDR, but end-to-end delay, throughput and consumption tend to

12
Sensor	25
Sensor	30
Sensor	26
Gateway
|     |     |     |     |     |     |     |     | Sensor	19 | Sensor	20 |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | --------- | --- |
Sensor	11
|     |     | Sensor	1 |     | Sensor	2 |     |     |           |     | Sensor	12 |           |
| --- | --- | -------- | --- | -------- | --- | --- | --------- | --- | --------- | --------- |
|     |     |          |     |          |     |     | Sensor	18 |     |           | Sensor	27 |
Sensor	21
Sensor	1
|     |          |     |          |     |          |     | Sensor	10 |     | Sensor	2 |           |
| --- | -------- | --- | -------- | --- | -------- | --- | --------- | --- | -------- | --------- |
|     |          |     |          |     |          |     | Sensor	9  |     | Sensor	3 |           |
|     | Sensor	3 |     | Sensor	4 |     | Sensor	5 |     |           |     |          | Sensor	28 |
Gateway
|     |     |     |     |     |     |     | Sensor	17 |     | Sensor	4 |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | --- | -------- | --- |
Sensor	8
Sensor	13
|     |     |     |     |          |          |          | Sensor	7  |          | Sensor	5 Sensor	22 |     |
| --- | --- | --- | --- | -------- | -------- | -------- | --------- | -------- | ------------------ | --- |
|     |     |     |     | Sensor	6 | Sensor	7 | Sensor	8 | Sensor	16 | Sensor	6 |                    |     |
Sensor	29
|     |     |     |          |           |     |     | Sensor	15 |     | Sensor	14 |     |
| --- | --- | --- | -------- | --------- | --- | --- | --------- | --- | --------- | --- |
|     |     |     | Sensor	9 | Sensor	10 |     |     | Sensor	24 |     |           |     |
Sensor	23
|     |     |     |     | (a)     |          |                 |       |             | (b) |     |
| --- | --- | --- | --- | ------- | -------- | --------------- | ----- | ----------- | --- | --- |
|     |     |     |     | Fig. 8: | Topology | for (a) testbed | 1 and | (b) testbed | 2.  |     |
worsen. Second, the value of 𝐶 has a major impact when the system is heavily charged, because it allows aggregating more
| application | packets | in a | single frame | and | interference | between signals | is less | probable. |     |     |
| ----------- | ------- | ---- | ------------ | --- | ------------ | --------------- | ------- | --------- | --- | --- |
Besides, the application payload length 𝑀 only affects to the performance of a sensor when it has more children than the
maximumsupported𝑐 orthepathstothegatewayaresharedbetweenmanysiblings.Additionally,ahighernumberofavailable
𝑚𝑎𝑥
parents for a sensor increases the PDR, but also the latency. Having a much denser network may enable more paths for children
| sensors, | which | increases | scalability | of the | solution. |     |     |     |     |     |
| -------- | ----- | --------- | ----------- | ------ | --------- | --- | --- | --- | --- | --- |
During the protocol design and evaluation, some insights were gained to modify and enhance the proposal. Regarding the
infrastructure deployment, it is highly recommended to use RSSI and SNR measurements to set up routing links between nodes.
This is because in urban areas signals are scattered and there may be lossy links, but it was not included in this version because
it would be necessary to develop a new model for the channel degradation effects (interference, noise, obstacles...). Besides,
we suggest to adjust the𝐶 parameter locally by each sensor to pseudo-coordinate the transmissions to avoid possible collisions.
Ideally, it would be the total number of sibling sensors, but sensors may not know all their neighbours.
Regarding the protocol behaviour, there are some aspects that might be improved or, at least, checked to assess their impact.
First, it could be convenient for sensors to include the transmission of a BEACON at the beginning of each time interval,
because there may be occasions when a sensor does not send any frame with information and could delay the joining procedure
of a new sensor. This extra BEACON would only be sent if there is no UP_DATA frame scheduled to send in that time interval,
and could be used to ensure that a sensor is still active and improve mobility aspects. Another improvement for reducing power
consumption is to force sensors located near the gateway to send UP_DATA frames only when their transmission buffer is full.
Nevertheless, this would increase the end-to-end delay, so it is necessary to reach an equilibrium. It would also be interesting to
checktheperformancewithauniquequeueforpendingmessages,insteadofusingtwoqueueswhichmayprioritizethemessages
| from the | local | sensor. |     |     |     |     |     |     |     |     |
| -------- | ----- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
Finally, it is worth comparing the proposed protocol with the most relevant and similar proposals about LoRa multi-hop
exhibitedinSectionIII.TableIVshowsthemostrelevantfeaturesconsideredforthedesignofthedifferentprotocols.Asshown,
JMAC deals with almost all critical points, but further work must be done to enable auto-configuration of nodes and facilitate
deployments. Besides, it addresses energy consumption and keeps control over duty cycle of sensors, which are important issues
| in IoT | solutions | that are | not usually | covered. |     |     |     |     |     |     |
| ------ | --------- | -------- | ----------- | -------- | --- | --- | --- | --- | --- | --- |
VII. CONCLUSIONSANDFURTHERWORK
LPWAN technologies are designed to support long range communications with low power consumption. However, most of
themarebasedonsinglehopcommunications,whichmayentailproblemsinareaswherethecoveragerangeisreducedbecause
of contextual elements (interference, noise, obstacles, etc.). This is especially relevant for indoor locations (such as in industrial
settings)orincrowdedareas(suchassmartcities).OurJMACproposal,across-layermulti-hopprotocolforLoRa,wasconceived
to overcome this issue by combining two successful strategies. On the one hand the LoRa radio technology to keep low energy
consumption and extend the coverage area and, on the other hand, enabling multi-hop capabilities to reuse resources and expand
the coverage area without adding more gateways, which usually make the infrastructure more expensive. Our proposal is also
compliant with the main general requirements of LPWAN [1], with the exception of using ALOHA with single-hop routing,
asthiswaspreciselythereasonforthisresearchwork.Thisfirstcontributioniscomplementedwithanewsimulationframework
within the OMNeT++ simulator, coined as FLoRaPHY, to simulate as close as possible to the real behaviour of LoRa to check
theoperationandscalabilityofthenewprotocolJMAC.Finally,andaccordingtothesimulationresults,wecanconcludethatour
proposalensuresaverylowpowerconsumption,facilitatingthedeploymentitinrealscenarioswithsensorpoweredbybatteries.

13
TABLE IV: Comparison of addressed topics in JMAC and other releveant LoRa multi-hop protocols.
Duty
|     | Proposal |     | Coverage | Consumption |     | Latency | Throughput | Routing | Cycle | Auto- |
| --- | -------- | --- | -------- | ----------- | --- | ------- | ---------- | ------- | ----- | ----- |
Configuration
Control
|     |     | JMAC | x   |     | x   | x   | x   |     | x x |     |
| --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | [33] | x   |     |     | x   |     |     | x   |     |
[34]
|     |     |     | x   |     |     | x   |     |     | x   | x   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
[35]
|     |     | [36] | x   |     | x   | x   |     |     | x   |     |
| --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | [38] | x   |     | x   | x   |     |     | x   | x   |
|     |     | [39] |     |     |     | x   |     |     | x   | x   |
|     |     | [48] | x   |     |     |     | x   |     | x   | x   |
|     |     | [49] | x   |     | x   | x   | x   |     | x   | x   |
|     |     | [50] | x   |     |     |     |     |     | x   |     |
It is interesting to mention that our approach can supplement the current LoRaWAN protocol, offering a more powerful strategy
| to increase the | coverage. |     |     |     |     |     |     |     |     |     |
| --------------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Therearesomeopenissuesthatweplantostudyinafuturework,suchasatheoreticalstudyoftheperformanceoftheJMAC
protocol.ItrequiresadeeperunderstandingofthephysicalmodulationofLoRaandtheformulationofamathematicalmodelfor
LoRasignalcollision.Thisway,allothermetrics,suchasend-to-enddelay,throughput,errorrate,etc.,couldbebetter-modelled.
Besides, more experiments can be performed to estimate the maximum capacity of the network. One option is to allow sensors
to generate data more often and study when the network becomes saturated and how it thereby performs to set a maximum time
to generate application data. LoRa allows simultaneous virtual channels (combination of SF and frequency channel) to operate
without interfering between them, so it would be possible to increase the total capacity of the deployment by creating different
multi-hop networks allocated to different virtual channels. This idea has already been explored in [66] to improve scalability.
It would also be interesting to adapt the protocol to the existing LoRaWAN solution, achieving compatibility, so they can be
bettercomparedintermsofperformance.Ofcourse,securityaspectsmustbealsoconsideredacriticalpriorityinfutureworkfor
multi-hopstrategies.Last, butnotleast,we arecurrentlyworkingonanimplementationofthesolutionin arealworldsettingto
assess the performance and to elaborate a new propagation loss model for urban areas as well as to explore the actual coverage
rangeofthesolution.Withinthiscontext,wearealsoworkingonthedownlinkflow,inordertohaveacompletesolutionforthe
JMAC protocol.
|     |     |     |     |     | VIII. | ACKNOWLEDGMENTS |     |     |     |     |
| --- | --- | --- | --- | --- | ----- | --------------- | --- | --- | --- | --- |
The authors would like to thank the European Regional Development Fund (ERDF) and the Galician Regional Government,
under the agreement for funding the AtlanTTIC Research Center for Information and Communication Technologies; the Spanish
Ministry of Economy and Competitiveness, under the National Science Program (TEC2017-84197-C4-2-R); and the Spanish
Ministry of Science, Innovation and Universities, under the Formación de Profesorado Universitario (FPU, FPU19/01284).
IX. ABBREVIATIONS
| LPWA | Low-Power | Wide-Area |     |     |     | IoT | Internet | of  | Things |     |
| ---- | --------- | --------- | --- | --- | --- | --- | -------- | --- | ------ | --- |
LPWAN Low-Power Wide-Area Network WSN Wireless sensor network
| CT  | Concurrent | Transmission |        |     |     | CSS | Chirp      | Spread | Spectrum  |     |
| --- | ---------- | ------------ | ------ | --- | --- | --- | ---------- | ------ | --------- | --- |
| FSK | Frequency  | Shift        | Keying |     |     | ADR | Adaptative |        | Data Rate |     |
AES Advanced Encryption Standard ABP Activation By Personalization
| OTAA    | Over-The-Air | Activation |            |         |     | TTN     | The           | Things    | Network         |     |
| ------- | ------------ | ---------- | ---------- | ------- | --- | ------- | ------------- | --------- | --------------- | --- |
| TTI     | The Things   | Industries |            |         |     | MAC     | Medium        | Access    | Control         |     |
| CRC     | Cyclic       | Redundancy | Check      |         |     | RF      | Radio         | frequency |                 |     |
| NwkSKey | Network      | Session    | Key        |         |     | AppSKey | Application   |           | Session Key     |     |
| AppKey  | Application  | Key        |            |         |     | DevAddr | Device        | Address   |                 |     |
| EUI     | Extended     | Unique     | Identifier |         |     | OTA     | Over-The-Air  |           |                 |     |
| NS      | Network      | Server     |            |         |     | JS      | Join          | Server    |                 |     |
| AS      | Application  | Server     |            |         |     | TDMA    | Time-Division |           | Multiple Access |     |
| CR      | Coding       | Rate       |            |         |     | RDC     | Radio         | Duty      | Cycling         |     |
| TSCH    | Time Slotted | Channel    |            | Hopping |     | SF      | Spreading     |           | Factor          |     |
| PHY     | Physical     | Layer      |            |         |     | OS      | Operating     |           | System          |     |
DTN Delay-Tolerant Networking API Application Programming Interface
DSDV Destination-Sequenced Distance Vector HWMP Hybrid Wireless Mesh Protocol
| SRD  | Short Range                       | Devices   |          |           |       | UNB | Ultra           | Narrow   | Band  |     |
| ---- | --------------------------------- | --------- | -------- | --------- | ----- | --- | --------------- | -------- | ----- | --- |
| LTE  | Long-Term                         | Evolution |          |           |       | ToA | Time            | On       | Air   |     |
| RSSI | Received                          | Signal    | Strength | Indicator |       | SNR | Signal-To-Noise |          | Ratio |     |
| SNIR | Signal-To-Noise-Plus-Interference |           |          |           | Ratio | PDR | Packet          | Delivery | Ratio |     |
| RTS  | Request                           | To Send   |          |           |       | CTS | Clear           | To Send  |       |     |
CSMA Carrier-Sense Multiple Access CCA Clear Channel Assesement

14
REFERENCES
[1] Mekki, K.; Bajic, E.; Chaxel, F.; Meyer, F. A comparative study of LPWAN technologies for large-scale IoT deployment.
| ICT Express | 2019, | 5, 1–7. |     |     |     |     |     |
| ----------- | ----- | ------- | --- | --- | --- | --- | --- |
[2] Bardyn, J.P.; Melly, T.; Seller, O.; Sornin, N. IoT: The era of LPWAN is starting now. In Proceedings of the ESSCIRC
Conference 2016: 42nd European Solid-State Circuits Conference, Lausanne, Switzerland, 2016; pp. 25–30.
[3] LoRa Alliance. About LoraWAN®. Available online: https://lora-alliance.org/about-lorawan (accessed on December 1st,
2020).
[4] Ferré, G.; Giremus, A. Lora physical layer principle and performance analysis. In Proceedings of the 2018 25th IEEE
International Conference on Electronics, Circuits and Systems (ICECS), Bordeaux, France, 2018; pp. 65–68.
[5] Sigfox. Sigfox-The Global Communications Service Provider for the Internet of Things (IoT). Available online: https:
| //www.sigfox.com |     | (accessed | on December | 1st, | 2020). |     |     |
| ---------------- | --- | --------- | ----------- | ---- | ------ | --- | --- |
[6] DASH7 Alliance. DASH7 Alliance—An open Specification. Available online: https://dash7-alliance.org (accessed on
| December | 1st, 2020). |     |     |     |     |     |     |
| -------- | ----------- | --- | --- | --- | --- | --- | --- |
[7] Weightless. Weightless—Setting the standard for IoT. Available online: http://www.weightless.org (accessed on December
1st, 2020).
[8] Lin,X.;Bergman,J.;Gunnarsson,F.;Liberg,O.;Razavi,S.M.;Razaghi,H.S.;Rydn,H.;Sui,Y. Positioningfortheinternet
| of things: | A 3GPP | perspective. | IEEE | Commun. | Mag. | 2017, | 55, 179–185. |
| ---------- | ------ | ------------ | ---- | ------- | ---- | ----- | ------------ |
[9] Hoglund,A.;Lin,X.;Liberg,O.;Behravan,A.;Yavuz,E.A.;VanDerZee,M.;Sui,Y.;Tirronen,T.;Ratilainen, A.;Eriksson,
| D. Overview | of  | 3GPP release | 14  | enhanced NB-IoT. |     | IEEE Netw. | 2017, 31, 16–22. |
| ----------- | --- | ------------ | --- | ---------------- | --- | ---------- | ---------------- |
[10] Hoglund, A.; Bergman, J.; Lin, X.; Liberg, O.; Ratilainen, A.; Razaghi, H.S.; Tirronen, T.; Yavuz, E.A. Overview of 3GPP
| release 14 | further | enhanced | MTC. | IEEE Commun. |     | Stand. Mag. | 2018, 2, 84–89. |
| ---------- | ------- | -------- | ---- | ------------ | --- | ----------- | --------------- |
[11] OMNeT++. OMNeT++:DiscreteEventSimulator. Availableonline:https://omnetpp.org/(accessedonDecember1st,2020).
[12] LópezEscobar,J.J.FLoRaPHYAvailableonline:https://github.com/juanjole/FLoRaPHY(accessedonDecember1st,2020).
[13] LoRa Alliance. LoRa Alliance. Available online: https://lora-alliance.org/ (accessed on December 1st, 2020).
[14] TheThingsNetwork. TheThingsNetwork. Availableonline:https://www.thethingsnetwork.org(accessedonDecember1st,
2020).
[15] TheThingsIndustries. TheThingsIndustries. Availableonline:https://www.thethingsindustries.com(accessedonDecember
1st, 2020).
[16] Reynders, B.; Pollin, S. Chirp spread spectrum as a modulation technique for long range communication. In Proceedings
of the 2016 Symposium on Communications and Vehicular Technologies (SCVT), Mons, Belgium, 2016; pp. 1–5.
[17] Semtech.AN1200.22:LoRa™ModulationBasics.Availableonline:https://semtech.my.salesforce.com/sfc/p/#E0000000JelG/
a/2R0000001OJa/2BF2MTeiqIwkmxkcjjDZzalPUGlJ76lLdqiv.30prH8 (accessed on December 1st, 2020).
[18] Semtech. LoRa®and LoRaWAN®:A Technical Overview. Available online: https://lora-developers.semtech.com/uploads/
documents/files/LoRa_and_LoRaWAN-A_Tech_Overview-Downloadable.pdf (accessed on December 1st, 2020).
[19] Knight, M.; Seeber, B. Decoding LoRa: Realizing a modern LPWAN with SDR. In Proceedings of the GNU Radio
| Conference, | Bourlder, | USA, | 2016; | Volume 1. |     |     |     |
| ----------- | --------- | ---- | ----- | --------- | --- | --- | --- |
[20] Marquet, A.; Montavont, N.; Papadopoulos, G.Z. Towards an SDR implementation of LoRa: Reverse-engineering,
demodulation strategies and assessment over Rayleigh channel. Comput. Commun. 2020, 153, 595–605.
[21] Croce, D.; Gucciardo, M.; Mangione, S.; Santaromita, G.; Tinnirello, I. Impact of LoRa imperfect orthogonality: Analysis
| of link-level | performance. |     | IEEE | Commun. Lett. | 2018, | 22, 796–799. |     |
| ------------- | ------------ | --- | ---- | ------------- | ----- | ------------ | --- |
[22] Talla,V.;Hessar,M.;Kellogg,B.;Najafi,A.;Smith,J.R.;Gollakota,S. Lorabackscatter:Enablingthevisionofubiquitous
| connectivity. | Proc. | Acm Interact. |     | Mob. Wearable | Ubiquitous |     | Technol. 2017, 1, 1–24. |
| ------------- | ----- | ------------- | --- | ------------- | ---------- | --- | ----------------------- |
[23] Marquet, A.; Montavont, N.; Papadopoulos, G.Z. Investigating theoretical performance and demodulation techniques for
lora. In Proceedings of the 2019 IEEE 20th International Symposium on “A World of Wireless, Mobile and Multimedia
| Networks” | (WoWMoM), |     | Washington | DC, USA, | 2019; | pp. 1–6. |     |
| --------- | --------- | --- | ---------- | -------- | ----- | -------- | --- |
[24] LoRa Alliance. LoRaWAN® Back-End Interfaces v1.0. Available online: https://lora-alliance.org/resource-hub/
| lorawanr-back-end-interfaces-v10 |     |     |     | (accessed | on December | 1st, | 2020). |
| -------------------------------- | --- | --- | --- | --------- | ----------- | ---- | ------ |
[25] LoRa Alliance. LoRaWAN® Regional Parameters RP002-1.0.0. Available online: https://lora-alliance.org/resource-hub/
| lorawanr-regional-parameters-rp002-100 |     |     |     | (accessed | on  | December | 1st, 2020). |
| -------------------------------------- | --- | --- | --- | --------- | --- | -------- | ----------- |
[26] LoRa Alliance. LoRaWAN® Specification v1.0.3. Available online: https://lora-alliance.org/resource-hub/
| lorawanr-specification-v103 |     |     | (accessed | on December |     | 1st, 2020). |     |
| --------------------------- | --- | --- | --------- | ----------- | --- | ----------- | --- |
[27] LoRa Alliance. LoRaWAN® Specification v1.1. Available online: https://lora-alliance.org/resource-hub/
| lorawanr-specification-v11 |     |     | (accessed | on December | 1st, | 2020). |     |
| -------------------------- | --- | --- | --------- | ----------- | ---- | ------ | --- |
[28] OMNEST. OMNEST: High-Performance Simulation for All Kinds of Networks. Available online: https://omnest.com/
| (accessed | on December | 1st, | 2020). |     |     |     |     |
| --------- | ----------- | ---- | ------ | --- | --- | --- | --- |
[29] OMNeT++. INET Framework. Available online: https://inet.omnetpp.org/ (accessed on December 1st, 2020).
[30] Slabicki, M.; Premsankar, G. FLoRa: Framework for LoRa. Available online: https://flora.aalto.fi/ (accessed on December
1st, 2020).
[31] Centenaro, M.; Vangelista, L.; Zanella, A.; Zorzi, M. Long-range communications in unlicensed bands: The rising stars in
| the IoT and | smart | city scenarios. |     | IEEE Wirel. | Commun. | 2016, | 23, 60–67. |
| ----------- | ----- | --------------- | --- | ----------- | ------- | ----- | ---------- |
[32] Ferrari, F.; Zimmerling, M.; Thiele, L.; Saukh, O. Efficient network flooding and time synchronization with glossy. In
Proceedings of the 10th ACM/IEEE International Conference on Information Processing in Sensor Networks, Chicago,
| USA, 2011; | pp. 73–84. |     |     |     |     |     |     |
| ---------- | ---------- | --- | --- | --- | --- | --- | --- |
[33] Liao,C.H.;Zhu,G.;Kuwabara,D.;Suzuki,M.;Morikawa,H.Multi-hopLoRanetworksenabledbyconcurrenttransmission.
| IEEE Access | 2017, | 5, 21430–21446. |     |     |     |     |     |
| ----------- | ----- | --------------- | --- | --- | --- | --- | --- |
[34] Lee,H.C.;Ke,K.H.Monitoringoflarge-areaIoTsensorsusingaLoRawirelessmeshnetworksystem:Designandevaluation.
| IEEE Trans. | Instrum. | Meas. | 2018, | 67, 2177–2187. |     |     |     |
| ----------- | -------- | ----- | ----- | -------------- | --- | --- | --- |
[35] Liang,C.W.;Wu,Y.L.;Shi,C.Y.;Lu,S.M.;Lee,H.C.EvaluationofaLoRameshwirelessnetworkingsystemsupportingtime-

15
critical transmission and data lost recovery. In Proceedings of the 18th International Conference on Information Processing
in Sensor Networks, Montreal, Canada, 2019; pp. 317–318.
[36] Bor, M.; Vidler, J.; Roedig, U. LoRa for the Internet of Things. In Proceedings of the 2016 International Conference on
Embedded Wireless Systems and Networks; Junction Publishing: USA, 2016; pp. 361–366.
[37] Sciullo, L.; Trotta, A.; Di Felice, M. Design and performance evaluation of a LoRa-based mobile emergency management
system (LOCATE). Ad. Hoc. Netw. 2020, 96, 101993.
[38] Abrardo, A.; Pozzebon, A. A multi-hop LoRa linear sensor network for the monitoring of underground environments: the
case of the Medieval Aqueducts in Siena, Italy. Sensors 2019, 19, 402.
[39] Mai, D.L.; Kim, M.K. Multi-Hop LoRa Network Protocol with Minimized Latency. Energies 2020, 13, 1368.
[40] Thielemans,S.;Bezunartea,M.;Steenhaut,K. EstablishingtransparentIPv6communicationonLoRabasedlowpowerwide
area networks (LPWANS). In Proceedings of the 2017 Wireless Telecommunications Symposium (WTS), Chicago, USA,
2017; pp. 1–6.
[41] Sartori, B.; Thielemans, S.; Bezunartea, M.; Braeken, A.; Steenhaut, K. Enabling RPL multihop communications based on
LoRa. InProceedingsofthe2017IEEE13thInternationalConferenceonWirelessandMobileComputing,Networkingand
Communications (WiMob), Rome, Italy, 2017; pp. 1–8.
[42] Piyare,R.;Murphy,A.L.;Magno,M.;Benini,L.KRATOS:AnOpenSourceHardware-SoftwarePlatformforRapidResearch
in LPWANs. In Proceedings of the 2018 14th International Conference on Wireless and Mobile Computing, Networking
and Communications (WiMob), Limassol, Cyprus, 2018; pp. 1–4.
[43] AdameVázquez,T.;Barrachina-Muñoz,S.;Bellalta,B.;Bel,A. HARE:Supportingefficientuplinkmulti-hopcommunica-
tions in self-organizing LPWANs. Sensors 2018, 18, 115.
[44] Contiki-NG.Contiki-NG:TheOSforNextGenerationIoTDevicesAvailableonline:https://github.com/contiki-ng/contiki-ng
(accessed on December 1st, 2020).
[45] Bezunartea, M.; Van Glabbeek, R.; Braeken, A.; Tiberghien, J.; Steenhaut, K. Towards Energy Efficient LoRa Multihop
Networks.InProceedingsofthe2019IEEEInternationalSymposiumonLocalandMetropolitanAreaNetworks(LANMAN),
Paris, France, 2019; pp. 1–3.
[46] Pycom. PyMesh Available online: https://docs.pycom.io/firmwareapi/pycom/network/lora/pymesh/ (accessed on December
1st, 2020).
[47] Saldamli, G.; Deshpande, S.; Jawalekar, K.; Gholap, P.; Tawalbeh, L.; Ertaul, L. Wildfire Detection using Wireless Mesh
Network. InProceedingsofthe2019FourthInternationalConferenceonFogandMobileEdgeComputing(FMEC),Rome,
Italy, 2019; pp. 229–234.
[48] Dias, J.; Grilo, A. LoRaWAN multi-hop uplink extension. Procedia Comput. Sci. 2018, 130, 424–431.
[49] Ebi, C.; Schaltegger, F.; Rüst, A.; Blumensaat, F. Synchronous LoRa mesh network to monitor processes in underground
infrastructure. IEEE Access 2019, 7, 57663–57677.
[50] Huh, H.; Kim, J.Y. LoRa-based Mesh Network for IoT Applications. In Proceedings of the 2019 IEEE 5th World Forum
on Internet of Things (WF-IoT), Limerick, Ireland, 2019; pp. 524–527.
[51] Lundell,D.;Hedberg,A.;Nyberg,C.;Fitzgerald,E. AroutingprotocolforLoRameshnetworks. In Proceedingsofthe2018
IEEE 19th International Symposium on “A World of Wireless, Mobile and Multimedia Networks” (WoWMoM), Chania,
Greece, 2018; pp. 14–19.
[52] Dwijaksara,M.H.;Jeon,W.S.;Jeong,D.G. MultihopGateway-to-GatewayCommunicationProtocolforLoRaNetworks. In
Proceedings of the 2019 IEEE International Conference on Industrial Technology (ICIT), Melbourne, Australia, 2019; pp.
949–954.
[53] Ye, W.; Heidemann, J.; Estrin, D. An energy-efficient MAC protocol for wireless sensor networks. In Proceedings of
the Twenty-First Annual Joint Conference of the IEEE Computer and Communications Societies, New York, USA, 2002;
Volume 3, pp. 1567–1576.
[54] Van Dam, T.; Langendoen, K. An adaptive energy-efficient MAC protocol for wireless sensor networks. In Proceedings of
the 1st international conference on Embedded networked sensor systems, Los Angeles, USA, 2003; pp. 171–180.
[55] Roy,A.;Sarma,N. AEEMAC:AdaptiveenergyefficientMACprotocolforwirelesssensornetworks. In Proceedingsofthe
2011 Annual IEEE India Conference, Hyderabad, India, 2011; pp. 1–6.
[56] Van Hoesel, L.; Havinga, P. A lightweight medium access protocol (LMAC) for wireless sensor networks. In Proceedings
of the 1st Int. Workshop on Networked Sensing Systems (INSS 2004), Tokio, Japan, 2004.
[57] El-Hoiydi, A.; Decotignie, J.D. WiseMAC: An ultra low power MAC protocol for multi-hop wireless sensor networks. In
International Symposium on Algorithms and Experiments for Sensor Systems, Wireless Networks and Distributed Robotics;
Springer: Berlin, Germany, 2004; pp. 18–31.
[58] Polastre, J.; Hill, J.; Culler, D. Versatile low power media access for wireless sensor networks. In Proceedings of the 2nd
international conference on Embedded networked sensor systems, Baltimore, USA, 2004; pp. 95–107.
[59] Zheng,T.;Radhakrishnan,S.;Sarangan,V. PMAC:anadaptiveenergy-efficientMACprotocolforwirelesssensornetworks.
In Proceedings of the 19th IEEE International Parallel and Distributed Processing Symposium, Denver, USA, 2005; pp.
8–pp.
[60] Buettner, M.; Yee, G.V.; Anderson, E.; Han, R. X-MAC: a short preamble MAC protocol for duty-cycled wireless sensor
networks. InProceedingsofthe4thinternationalconferenceonEmbeddednetworkedsensorsystems,Boulder,USA,2006;
pp. 307–320.
[61] Jang, B.; Lim, J.B.; Sichitiu, M.L. AS-MAC: An asynchronous scheduled MAC protocol for wireless sensor networks. In
Proceedings of the 2008 5th IEEE International Conference on Mobile Ad Hoc and Sensor Systems, Atlanta, USA, 2008;
pp. 434–441.
[62] Sun, Y.; Gurewitz, O.; Johnson, D.B. RI-MAC: a receiver-initiated asynchronous duty cycle MAC protocol for dynamic
trafficloadsinwirelesssensornetworks. InProceedingsofthe6thACMconferenceonEmbeddednetworksensorsystems,
Raleigh, USA, 2008; pp. 1–14.
[63] Tang,L.;Sun,Y.;Gurewitz,O.;Johnson,D.B. PW-MAC:Anenergy-efficientpredictive-wakeupMACprotocolforwireless
sensor networks. In Proceedings of the 2011 IEEE INFOCOM, Shanghai, China, 2011; pp. 1305–1313.

16
[64] Petajajarvi, J.; Mikhaylov, K.; Roivainen, A.; Hanninen, T.; Pettissalo, M. On the coverage of LPWANs: range evaluation
and channel attenuation model for LoRa technology. In Proceedings of the 2015 14th International Conference on ITS
| Telecommunications | (ITST), Copenhagen, | Denmark, 2015; | pp. 55–59. |     |
| ------------------ | ------------------- | -------------- | ---------- | --- |
[65] Semtech. SX1276 | 137 MHz to 1020 MHz Long Range Low Power Transceiver. Available online: https://www.semtech.
| com/products/wireless-rf/lora-transceivers/sx1276 |     | (accessed | on December | 1st, 2020). |
| ------------------------------------------------- | --- | --------- | ----------- | ----------- |
[66] Zhu,G.;Liao,C.H.;Sakdejayont,T.;Lai,I.W.;Narusue,Y.;Morikawa,H. ImprovingthecapacityofameshLoRanetwork
| by spreading-factor-based | network clustering. | IEEE Access | 2019, 7, | 21584–21596. |
| ------------------------- | ------------------- | ----------- | -------- | ------------ |

17
M = 30 B M = 50 B M = 100 B
100 100 100
90 90 90
80 80 80
)% )% )%
(
R
(
R
(
R
D D D
P 70 P 70 P 70
60 60 60
Sensor 1 Sensor 1 Sensor 1
Sensor 2 Sensor 2 Sensor 2
Sensor 3 Sensor 3 Sensor 3
Sensor 4 Sensor 4 Sensor 4
Sensor 5 Sensor 5 Sensor 5
Sensor 6 Sensor 6 Sensor 6
Sensor 7 Sensor 7 Sensor 7
50 Sensor 8 50 Sensor 8 50 Sensor 8
Sensor 9 Sensor 9 Sensor 9
Sensor 10 Sensor 10 Sensor 10
Average Average Average
1 2 3 4 1 2 3 4 1 2 3 4
C C C
(a)
M = 30 B M = 50 B M = 100 B
450 450 450
400 400 400
350 350 350
300 300 300
)W )W )W
(
n
250 (
n
250 (
n
250
o o o
itp itp itp
m m m
u u u
sn200 sn200 sn200
o o o
C C C
150 150 150
100 100 100
50 50 50
Sensor 1 Sensor 5 Sensor 9 Sensor 1 Sensor 5 Sensor 9 Sensor 1 Sensor 5 Sensor 9
Sensor 2 Sensor 6 Sensor 10 Sensor 2 Sensor 6 Sensor 10 Sensor 2 Sensor 6 Sensor 10
Sensor 3 Sensor 7 Average Sensor 3 Sensor 7 Average Sensor 3 Sensor 7 Average
Sensor 4 Sensor 8 Sensor 4 Sensor 8 Sensor 4 Sensor 8
0 0 0
1 2 3 4 1 2 3 4 1 2 3 4
C C C
(b)
Fig. 9: Results for the Testbed1 (a) PDR and (b) power consumption.

18
|         |     | M = 30 B  |     |         |     | M = 50 B  |     |         |     | M = 100 B |     |
| ------- | --- | --------- | --- | ------- | --- | --------- | --- | ------- | --- | --------- | --- |
| 600     |     |           |     | 600     |     |           |     | 600     |     |           |     |
|         |     | Sensor 1  |     |         |     | Sensor 1  |     |         |     | Sensor 1  |     |
|         |     | Sensor 2  |     |         |     | Sensor 2  |     |         |     | Sensor 2  |     |
|         |     | Sensor 3  |     |         |     | Sensor 3  |     |         |     | Sensor 3  |     |
|         |     | Sensor 4  |     |         |     | Sensor 4  |     |         |     | Sensor 4  |     |
|         |     | Sensor 5  |     |         |     | Sensor 5  |     |         |     | Sensor 5  |     |
| 500     |     | Sensor 6  |     | 500     |     | Sensor 6  |     | 500     |     | Sensor 6  |     |
|         |     | Sensor 7  |     |         |     | Sensor 7  |     |         |     | Sensor 7  |     |
|         |     | Sensor 8  |     |         |     | Sensor 8  |     |         |     | Sensor 8  |     |
|         |     | Sensor 9  |     |         |     | Sensor 9  |     |         |     | Sensor 9  |     |
|         |     | Sensor 10 |     |         |     | Sensor 10 |     |         |     | Sensor 10 |     |
|         |     | Average   |     |         |     | Average   |     |         |     | Average   |     |
| 400     |     |           |     | 400     |     |           |     | 400     |     |           |     |
| )s( ya  |     |           |     | )s( ya  |     |           |     | )s( ya  |     |           |     |
| le      |     |           |     | le      |     |           |     | le      |     |           |     |
| d       |     |           |     | d       |     |           |     | d       |     |           |     |
|  d n300 |     |           |     |  d n300 |     |           |     |  d n300 |     |           |     |
| e       |     |           |     | e       |     |           |     | e       |     |           |     |
| -o      |     |           |     | -o      |     |           |     | -o      |     |           |     |
| t-d     |     |           |     | t-d     |     |           |     | t-d     |     |           |     |
| n       |     |           |     | n       |     |           |     | n       |     |           |     |
| E       |     |           |     | E       |     |           |     | E       |     |           |     |
| 200     |     |           |     | 200     |     |           |     | 200     |     |           |     |
| 100     |     |           |     | 100     |     |           |     | 100     |     |           |     |
|         | 0   |           |     |         | 0   |           |     |         | 0   |           |     |
|         | 1   | 2         | 3   | 4       | 1   | 2         | 3   | 4       | 1   | 2         | 3 4 |
|         |     |           | C   |         |     | C         |     |         |     |           | C   |
(a)
|     |     | M = 30 B |           |     |     | M = 50 B |           |     |     | M = 100 B |     |
| --- | --- | -------- | --------- | --- | --- | -------- | --------- | --- | --- | --------- | --- |
| 350 |     |          |           | 350 |     |          |           | 350 |     |           |     |
|     |     |          | Sensor 1  |     |     |          | Sensor 1  |     |     |           |     |
|     |     |          | Sensor 2  |     |     |          | Sensor 2  |     |     |           |     |
|     |     |          | Sensor 3  |     |     |          | Sensor 3  |     |     |           |     |
|     |     |          | Sensor 4  |     |     |          | Sensor 4  |     |     |           |     |
| 300 |     |          | Sensor 5  | 300 |     |          | Sensor 5  | 300 |     |           |     |
|     |     |          | Sensor 6  |     |     |          | Sensor 6  |     |     |           |     |
|     |     |          | Sensor 7  |     |     |          | Sensor 7  |     |     |           |     |
|     |     |          | Sensor 8  |     |     |          | Sensor 8  |     |     |           |     |
|     |     |          | Sensor 9  |     |     |          | Sensor 9  |     |     |           |     |
|     |     |          | Sensor 10 |     |     |          | Sensor 10 |     |     |           |     |
|     |     |          | Average   |     |     |          | Average   |     |     |           |     |
| 250 |     |          |           | 250 |     |          |           | 250 |     |           |     |
Sensor 1
Sensor 2
| )s/b 200 |     |     |     | )s/b 200 |     |     |     | )s/b 200 |     |     |     |
| -------- | --- | --- | --- | -------- | --- | --- | --- | -------- | --- | --- | --- |
S e n s o r   3
| ( tu |     |     |     | ( tu |     |     |     | ( tu |     |     | S e n s o r   4 |
| ---- | --- | --- | --- | ---- | --- | --- | --- | ---- | --- | --- | --------------- |
S e n s o r   5
| p h     |     |     |     | p h     |     |     |     | p h     |     |     | Sensor 6        |
| ------- | --- | --- | --- | ------- | --- | --- | --- | ------- | --- | --- | --------------- |
| g u     |     |     |     | g u     |     |     |     | g u     |     |     | Sensor 7        |
| o       |     |     |     | o       |     |     |     | o       |     |     | Sensor 8        |
| rh T150 |     |     |     | rh T150 |     |     |     | rh T150 |     |     | S e n s o r   9 |
S e n s o r   10
Average
| 100 |     |     |     | 100 |     |     |     | 100 |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 50  |     |     |     | 50  |     |     |     | 50  |     |     |     |
|     | 0   |     |     |     | 0   |     |     |     | 0   |     |     |
|     | 1   | 2   | 3   | 4   | 1   | 2   | 3   | 4   | 1   | 2   | 3 4 |
|     |     |     | C   |     |     | C   |     |     |     |     | C   |
(b)
Fig. 10: Results for the Testbed1 (a) average end-to-end delay and (b) throughput.

19
(a)
(b)
(c)
(d)
Fig. 11: Results for the Testbed2 (a) PDR, (b) power consumption, (c) average end-to-end delay and (b) throughput.