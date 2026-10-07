> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> arXiv **2006.12570** - *Hybrid LPWA mesh network for IoT*. Source PDF deleted after conversion.
>
> Listed in `docs/research/BUDGET/01-literature.md` comms row 3 as **HELD**, no figure quoted.
> It is the published form of the **mesh-over-LPWAN topology** that `docs/MASTER.md` section 2
> assumes. Cite it if the proposal claims the topology is established practice rather than novel
> - the mesh is **not** a contribution of this project.

|     | IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |           |     |     |     |     |              |     |      |     |     |         |     |     | 1   |
| --- | ------------------------------------- | --- | --------- | --- | --- | --- | --- | ------------ | --- | ---- | --- | --- | ------- | --- | --- | --- |
|     | Hybrid                                |     | Low-Power |     |     |     |     | Wide-Area    |     | Mesh |     |     | Network |     |     | for |
|     |                                       |     |           |     |     |     | IoT | Applications |     |      |     |     |         |     |     |     |
Xiaofan Jiang, Member, IEEE, Heng Zhang, Member, IEEE, Edgardo Alberto Barsallo Yi, Member, IEEE,
Nithin Raghunathan, Member, IEEE, Charilaos Mousoulis, Member, IEEE, Somali Chaterji, Member, IEEE,
Dimitrios Peroulis, Fellow, IEEE, Ali Shakouri, and Saurabh Bagchi, Fellow, IEEE,
Abstract—The recent advancement of the Internet of Things and smart homes. In the digital agriculture context, these
|                                          | (IoT) enables | the   | possibility  |               | of data     | collection | from          | diverse   |            |             |              |          |               |           |             |         |
| ---------------------------------------- | ------------- | ----- | ------------ | ------------- | ----------- | ---------- | ------------- | --------- | ---------- | ----------- | ------------ | -------- | ------------- | --------- | ----------- | ------- |
|                                          |               |       |              |               |             |            |               |           | devices    | may monitor | various      |          | environmental |           | conditions, | such    |
| 0202 nuJ 22  ]IN.sc[  1v07521.6002:viXra | environments  | using | IoT          | devices.      | However,    |            | despite       | the rapid |            |             |              |          |               |           |             |         |
|                                          |               |       |              |               |             |            |               |           | as soil    | moisture,   | nutrient     | quality, | or            | microbial | activity    | [1].    |
|                                          | advancement   | of    | low-power    | communication |             |            | technologies, | the       |            |             |              |          |               |           |             |         |
|                                          |               |       |              |               |             |            |               |           | The sensor | data        | is collected |          | and routed    | through   |             | the WSN |
|                                          | deployment    | of    | IoT networks |               | still faces | many       | challenges.   | In        |            |             |              |          |               |           |             |         |
this paper, we propose a hybrid, low-power, wide-area network and sent to the cloud for further analysis and possible closed-
(LPWAN) structure that can achieve wide-area communication loop control. Our work addresses the development of a large-
coverageandlowpowerconsumptiononIoTdevicesbyutilizing scale WSN that is suitable for distinct application areas,
|     | both sub-GHz  | long-range     |             | radio    | and       | 2.4 GHz | short-range  | radio.     |           |          |             |            |             |     |           |            |
| --- | ------------- | -------------- | ----------- | -------- | --------- | ------- | ------------ | ---------- | --------- | -------- | ----------- | ---------- | ----------- | --- | --------- | ---------- |
|     |               |                |             |          |           |         |              |            | namely:   | digital  | agriculture | and        | smart       | and | connected | cities.    |
|     | Specifically, | we             | constructed | a        | low-power |         | mesh network | with       |           |          |             |            |             |     |           |            |
|     |               |                |             |          |           |         |              |            | Our study | is based | on          | real-world | deployments |     | and       | highlights |
|     | LoRa, a       | physical-layer |             | standard | that      | can     | provide      | long-range |           |          |             |            |             |     |           |            |
(kilometers) point-to-point communication using custom time- the practical design challenges and insights that arise from
division multiple access (TDMA). Furthermore, we extended the long-term unattended operation of those IoT systems. They
capabilities of the mesh network by enabling ANT, an ultra highlight a distinct set of challenges in terms of the wireless
|     | low-power,      | short-range |        | communication |         | protocol | to             | satisfy data |            |               |        |     |              |     |              |     |
| --- | --------------- | ----------- | ------ | ------------- | ------- | -------- | -------------- | ------------ | ---------- | ------------- | ------ | --- | ------------ | --- | ------------ | --- |
|     |                 |             |        |               |         |          |                |              | networking | capabilities. |        |     |              |     |              |     |
|     | collection      | in dense    | device | deployments.  |         | Third,   | we demonstrate |              |            |               |        |     |              |     |              |     |
|     |                 |             |        |               |         |          |                |              | Digital    | agriculture   | refers | to  | using modern |     | technologies | to  |
|     | the performance |             | of the | hybrid        | network | with     | two real-world | de-          |            |               |        |     |              |     |              |     |
ploymentsatthePurdueUniversitycampusandattheuniversity- increase the quantity and quality of agricultural products.
ownedfarm.Theresultssuggestthatbothnetworkshavesuperior Understanding the environmental conditions (e.g., tempera-
advantages in terms of cost, coverage, and power consumption ture, humidity, and soil fertility) is important for agricultural
|     | vis-a`-vis | other IoT | solutions, | like | LoRaWAN. |     |     |     |             |                |     |     |          |             |     |            |
| --- | ---------- | --------- | ---------- | ---- | -------- | --- | --- | --- | ----------- | -------------- | --- | --- | -------- | ----------- | --- | ---------- |
|     |            |           |            |      |          |     |     |     | management. | Traditionally, |     | it  | has been | challenging |     | to consis- |
IndexTerms—LoRa,WSN,TDMA,IoT,MeshNetwork,Com- tently monitor large farmlands due to the lack of automation
|     | munications, | Smart | City, | Digital      | Agriculture. |     |     |     |                 |              |              |              |                 |             |           |           |
| --- | ------------ | ----- | ----- | ------------ | ------------ | --- | --- | --- | --------------- | ------------ | ------------ | ------------ | --------------- | ----------- | --------- | --------- |
|     |              |       |       |              |              |     |     |     | and inefficient | labor.       | Recent       | agricultural |                 | industries  |           | have been |
|     |              |       |       |              |              |     |     |     | adopting        | automation   | technologies |              | that            | can monitor |           | the envi- |
|     |              |       |       |              |              |     |     |     | ronment         | and optimize |              | farming      | [1]–[4].        | Some        | analytics | can       |
|     |              |       | I.    | INTRODUCTION |              |     |     |     |                 |              |              |              |                 |             |           |           |
|     |              |       |       |              |              |     |     |     | also be         | run on       | the back-end |              | cloud computing |             | resource  | and       |
AsInternetofThings(IoT)devices,representinganetwork
|     |                   |     |         |             |     |      |              |       | derive actionable |     | knowledge |     | from the | raw data, | such | as, how |
| --- | ----------------- | --- | ------- | ----------- | --- | ---- | ------------ | ----- | ----------------- | --- | --------- | --- | -------- | --------- | ---- | ------- |
|     | of interconnected |     | things, | proliferate |     | with | an estimated | popu- |                   |     |           |     |          |           |      |         |
lation of 125 billion IoT devices in the next decade, systems to fertilize specific parts of the farm in a localized manner.
Suchkindsofdecisionsdonotrequirereal-time(or,nearreal-
builtoutofthesedeviceswillplayaroleinmanydeployments,
|     |                     |            |               |                 |                  |          |                     |            | time) decision | making.         |          |              |              |              |           |             |
| --- | ------------------- | ---------- | ------------- | --------------- | ---------------- | -------- | ------------------- | ---------- | -------------- | --------------- | -------- | ------------ | ------------ | ------------ | --------- | ----------- |
|     | including           | those      | that          | need extended   |                  | periods  | of                  | unattended |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | In addition    | to              | digital  | agriculture, |              | smart        | city      | is another  |
|     | operation.          | These      | things        | are essentially |                  | sensors  | and                 | actuators, |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | important      | application     | in       | IoT.         | It refers    | to using     | different | types       |
|     | fitted with         | a wireless |               | network         | interface,       |          | and computing       | and        |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | of sensors     | in urban        | areas    | to collect   | data         | and          | then use  | the data    |
|     | storage             | units.     | IoT provides  |                 | the connectivity |          | to                  | physically |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | to manage      | urban           | assets   | and          | resources    | efficiently. |           | According   |
|     | distributed         | devices,   | home          | appliances,     |                  | and      | even                | devices    | in             |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | to the United  | Nations         |          | Department   | of           | Economic     | and       | Social      |
|     | more critical       | sectors,   | such          | as              | healthcare,      | public   | utilities           | (e.g.,     |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | Affairs,       | it is estimated |          | that by      | 2050 there   | will         | be        | 2.5 billion |
|     | electric            | grids),    | environmental |                 | monitoring,      |          | and transportation. |            |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | people living  | in              | urban    | areas.       | WSNs are     | becoming     |           | part of a   |
|     | These IoT           | devices    | sense,        | compute,        |                  | and      | communicate,        | often      |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | smart city     | infrastructure  |          | that         | can combat   | the          | strain    | of city     |
|     | in resource-limited |            | deployments,  |                 | forming          |          | a Wireless          | Sensor     |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | growth         | by providing    | access   |              | to real-time | data         | and       | can be      |
|     | Network             | (WSN).     | In the        | smart           | city             | context, | the IoT             | devices    |                |                 |          |              |              |              |           |             |
|     |                     |            |               |                 |                  |          |                     |            | realized       | through         | a robust | network.     |              |              |           |             |
|     | may monitor         | energy     | and           | utility         | distribution     |          | (e.g., smart        | grid);     |                |                 |          |              |              |              |           |             |
However,thereareseveraltechnicalchallengestobesolved
enableintelligenttransportationsystems,buildingautomation,
|     |     |     |     |     |     |     |     |     | for the | successful | deployment |     | of such | a   | WSN, | such as |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | ---------- | ---------- | --- | ------- | --- | ---- | ------- |
harshenvironmentalconditions,communicationrange,quality
|     | X. Jiang, | H. Zhang, | N.  | Raghunathan, | D.  | Peroulis, | A. Shakouri | and | S.  |     |     |     |     |     |     |     |
| --- | --------- | --------- | --- | ------------ | --- | --------- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
BagchiarewiththeSchoolofElectricalandComputerEngineering,Purdue of service (QoS), deployment cost and energy consumption
University,WestLafayette,IN,47906USA(e-mail:jiang175@purdue.edu.)
|     |     |     |     |     |     |     |     |     | (battery | life). These | technical |     | challenges | are | further | discussed |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | ------------ | --------- | --- | ---------- | --- | ------- | --------- |
E.YiiswiththeDepartmentofComputerScience,PurdueUniversity,West
Lafayette,IN,47906USA. in our technical report [5]. To handle the above challenges,
S.ChaterjiiswiththeSchoolofAgriculturalandBiologicalEngineering, we designed and fabricated a new custom wireless IoT hard-
PurdueUniversity,WestLafayette,IN,47906USA.
|     |            |          |       |     |       |         |        |           | ware platform |     | that is | connected | to  | temperature, |     | humidity, |
| --- | ---------- | -------- | ----- | --- | ----- | ------- | ------ | --------- | ------------- | --- | ------- | --------- | --- | ------------ | --- | --------- |
|     | Manuscript | received | April | XX, | XXXX; | revised | August | XX, XXXX. |               |     |         |           |     |              |     |           |
(XiaofanJiangandHengZhangareco-firstauthors.) and nitrate soil sensors and additional I/O pins for enabling

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |                      |        |              |        |              |        |     | 2     |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | -------------------- | ------ | ------------ | ------ | ------------ | ------ | --- | ----- |
|                                       |     |     |     |     |     |     |     | (Throckmorton-Purdue |        | Agricultural |        | Center–TPAC) |        | and | urban |
|                                       |     |     |     |     |     |     |     | (West Lafayette      | campus | at           | Purdue | university)  | areas. |     |       |
Therestofthispaperisorganizedasfollows.InSectionII,
|     |     |     |     |     |     |     |     | we provide   | a summary |         | of popular |       | WPANs       | and LPWANs |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --------- | ------- | ---------- | ----- | ----------- | ---------- | --- |
|     |     |     |     |     |     |     |     | technologies | and       | discuss | related    | works | of LoRaWAN. |            | In  |
SectionIII,wepresentoursolutionwiththenetworkstructure
|     |     |     |     |     |     |     |     | as well as      | the new                       | hardware     | platform. |              | The evaluation |            | results |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------- | ----------------------------- | ------------ | --------- | ------------ | -------------- | ---------- | ------- |
|     |     |     |     |     |     |     |     | are presented   | in Section                    |              | IV and    | the paper    | is concluded   |            | with    |
|     |     |     |     |     |     |     |     | the discussions | of                            | limitations  | and       | future       | work           | in Section | VI.     |
|     |     |     |     |     |     |     |     |                 | II. BACKGROUNDANDRELATEDWORKS |              |           |              |                |            |         |
|     |     |     |     |     |     |     |     | A. Summary      | of Current                    | Technologies |           |              | in WSN         |            |         |
|     |     |     |     |     |     |     |     | Low power       | communication                 |              |           | technologies | for            | wireless   | IoT     |
|     |     |     |     |     |     |     |     | communication   | can                           | grossly      | fall      | within       | two categories |            | (Fig.   |
2):
|     |     |     |     |     |     |     |     | Wireless | Personal | Area | Networks |     | (WPANs): | typically |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | -------- | ---- | -------- | --- | -------- | --------- | --- |
•
Fig.1. HybridNetworkArchitecture.LongRangeMeshNetwork(LRMN)
|             |         |             |      |         |        |           |      | communicate |     | from 10 | meters | to  | a few hundred |     | meters. |
| ----------- | ------- | ----------- | ---- | ------- | ------ | --------- | ---- | ----------- | --- | ------- | ------ | --- | ------------- | --- | ------- |
| consists of | several | Short Range | Star | Network | (SRSN) | and a few | LoRa |             |     |         |        |     |               |     |         |
nodes. Each node is capable of communicating in a WPAN protocol (ANT This category includes Bluetooth, Bluetooth Low En-
| in this case) | or an | LPWAN | protocol (LoRa | in  | this case). | SRSN | is used | to   |             |         |     |             |     |            |     |
| ------------- | ----- | ----- | -------------- | --- | ----------- | ---- | ------- | ---- | ----------- | ------- | --- | ----------- | --- | ---------- | --- |
|               |       |       |                |     |             |      |         | ergy | (BLE), ANT, | ZigBee, |     | etc., which | are | applicable | di- |
satisfydensesensingdeploymentwhileindividualLoRanodesareforsparse
rectlyinshort-rangepersonalareanetworksorifdesigned
deployment.
inameshtopologyandwithhighertransmitpower,larger
|     |     |     |     |     |     |     |     | area | coverage | is possible. |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | -------- | ------------ | --- | --- | --- | --- | --- |
the connections to other sensors. We choose LoRa [6] as Low-Power Wide Area Networks (LPWANs): have a
•
the communication protocol because of its long range and communication range greater than one kilometer. Each
low power consumption (Section II-B). LoRa utilizes chirp gateway could communicate with thousands of end-
spread spectrum (CSS) modulation and operates in the sub- devices. This category includes LoRaWAN, Sigfox, NB-
| GHz ISM | band | to void | penetration | capability |     | and heavy | in- |      |                |     |     |       |              |     |      |
| ------- | ---- | ------- | ----------- | ---------- | --- | --------- | --- | ---- | -------------- | --- | --- | ----- | ------------ | --- | ---- |
|         |      |         |             |            |     |           |     | IoT, | etc. A summary |     | of  | these | technologies | are | sum- |
band interference. Furthermore, we proposed a lightweight, marised in Table I [7]–[9].
| hybrid network |      | combining | the          | advantages | of             | LoRa’s | wide   |     |     |     |     |     |     |     |     |
| -------------- | ---- | --------- | ------------ | ---------- | -------------- | ------ | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
| area coverage  |      | and ANT’s | ultra-low    | power      | consumption    |        | by     |     |     |     |     |     |     |     |     |
| integrating    | them | into a    | mesh network |            | with following |        | design |     |     |     |     |     |     |     |     |
goal:
| • Must   | be low-cost |          | in system    | level, | meaning      | not       | only |     |     |     |     |     |     |     |     |
| -------- | ----------- | -------- | ------------ | ------ | ------------ | --------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
| hardware | of          | the node | is low-cost, |        | the receiver | (gateway) |      |     |     |     |     |     |     |     |     |
| must     | be low-cost | as       | well.        |        |              |           |      |     |     |     |     |     |     |     |     |
| Should   | be          | able to  | cover a      | large  | geographic   | area.     | For  |     |     |     |     |     |     |     |     |
•
| example, | in         | our farming | deployment,     |         | the network |         | covers   |     |     |     |     |     |     |     |     |
| -------- | ---------- | ----------- | --------------- | ------- | ----------- | ------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
| 2.2      | km2 of     | a farm      | and our         | campus  | deployment  |         | covers   |     |     |     |     |     |     |     |     |
| around   | 1.2        | km2 of      | Purdue          | campus. |             |         |          |     |     |     |     |     |     |     |     |
| • Has    | to be      | robust      | enough to       | survive | the harsh   |         | environ- |     |     |     |     |     |     |     |     |
| mental   | conditions |             | and the network |         | should      | able to | handle   |     |     |     |     |     |     |     |     |
| node     | failures   | and         | recover from    | it.     |             |         |          |     |     |     |     |     |     |     |     |
• The deployment procedure for the IoT devices should Fig. 2. A summary of current wireless commutation technologies, where
trade-offbetweencommunicationrange(x-axis)andpower/speed(y-axis)are
notrequireanyspecificdomainknowledge.Regularusers
clearlyrepresented.
shouldbeabletosimplyinstallbatteriestotheIoTdevice
and the device will work properly. A more detailed discussion on the technologies can also be
| In addition |     | to LoRa, | the proposed |     | network | should | also |          |               |        |      |     |     |     |     |
| ----------- | --- | -------- | ------------ | --- | ------- | ------ | ---- | -------- | ------------- | ------ | ---- | --- | --- | --- | --- |
| •           |     |          |              |     |         |        |      | found in | the technical | report | [5]. |     |     |     |     |
incorporate ultra-low power radio such as ANT to im- In conclusion, we choose LoRa in our deployment because
| prove | the | performance | and | efficiency | of the | network |     | in               |             |     |     |            |     |              |     |
| ----- | --- | ----------- | --- | ---------- | ------ | ------- | --- | ---------------- | ----------- | --- | --- | ---------- | --- | ------------ | --- |
|       |     |             |     |            |        |         |     | of the following | advantages: |     | i)  | the number | of  | LoRa-enabled |     |
dense deployments. deployment is increasing continuously while, on the other
• The proposed IoT device must be able to adopt to hand, few initial NB-IoT deployments have been already
| additional |     | sensors. |     |     |     |     |     |           |          |          |        |     |              |     |          |
| ---------- | --- | -------- | --- | --- | --- | --- | --- | --------- | -------- | -------- | ------ | --- | ------------ | --- | -------- |
|            |     |          |     |     |     |     |     | deployed; | ii) LoRa | operates | in the | ISM | band whereas |     | cellular |
To evaluate the performance of the proposed hybrid net- IoT operates in licensed bands; this fact favors the private
work, we conduct a series of experiments. First, we conduct LoRa networks without the involvement of mobile operators;
several in-lab tests to show the power efficiency, deployment iii) LoRaWAN, a cloud-based medium access control (MAC)
feasibility as well as the reliability of the network over layer protocol based on LoRa, has growing backing from
time. Next, we deploy two real-world testbeds in both rural industry,e.g.loRaAlliance,CISCO,IBMorHP,amongothers.

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     |     |     |     |     | 3   |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
TABLEI
OVERVIEWOFLPWANTECHNOLOGIES:SIGFOX,LORA,ANDNB-IOT.
|            |     |     |     | Sigfox[7] |     |     |     |     | LoRaWAN[8] |     |     |     | NB-IoT[9] |     |     |
| ---------- | --- | --- | --- | --------- | --- | --- | --- | --- | ---------- | --- | --- | --- | --------- | --- | --- |
| Modulation |     |     |     | BPSK      |     |     |     |     | CSS        |     |     |     | QPSK      |     |     |
UnlicensedISMbands(868MHzin UnlicensedISMbands(868MHzin LicensedLTEfrequency
Band
Europe,915MHzinNorthAmerica) Europe,915MHzinNorthAmerica) bands
| Bandwidth       |     |     |     | 100Hz  |     |     |     |     | 125or250kHz |     |     |     | 200kHz  |     |     |
| --------------- | --- | --- | --- | ------ | --- | --- | --- | --- | ----------- | --- | --- | --- | ------- | --- | --- |
| Maximumdatarate |     |     |     | 100bps |     |     |     |     | 50kbps      |     |     |     | 200kbps |     |     |
Bidirectional Limited/Half-duplex Yes/Half-duplex Yes/Half-duplex
| Maximummessages/day |     |     |     | 140(UL),4(DL) |     |     |     |     | Unlimited |     |     |     | Unlimited |     |     |
| ------------------- | --- | --- | --- | ------------- | --- | --- | --- | --- | --------- | --- | --- | --- | --------- | --- | --- |
Maximumpayloadlength 12bytes(UL),8bytes(DL) 243bytes 1600bytes
1km(urban),10km
| Range |     |     |     | 10km(urban),40km(rural) |     |     |     |     | 5km(urban),20km(rural) |     |     |     |     |     |     |
| ----- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | ---------------------- | --- | --- | --- | --- | --- | --- |
(rural)
| Interferenceimmunity |     |     |     | Veryhigh |     |     |     |     | Veryhigh |     |     |     | Low |     |     |
| -------------------- | --- | --- | --- | -------- | --- | --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- |
Authentication&encryption Notsupported Yes(AES128b) Yes(LTEencryption)
| Adaptivedatarate |     |     |     | No  |     |     |     |     | Yes |     |     |     | No  |     |     |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
End-devicesjoina
Handover End-devicesdonotjoinasinglebasestation End-devicesdonotjoinasinglebasestation
singlebasestation
| Localization        |     |     |     | Yes(RSSI) |     |     |     |     | Yes(TDoA)     |     |     |     | No(underspecification) |     |     |
| ------------------- | --- | --- | --- | --------- | --- | --- | --- | --- | ------------- | --- | --- | --- | ---------------------- | --- | --- |
| Allowprivatenetwork |     |     |     | No        |     |     |     |     | Yes           |     |     |     | No                     |     |     |
| Standardization     |     |     |     | No        |     |     |     |     | LoRa-Alliance |     |     |     | 3GPP                   |     |     |
B. Related Studies in LoRaWAN Furthermore, since we are talking about multi-hopping, the
|             |       |           |          |           |         |               |          |         | energy | consumption | for        | RX has | to be considered | as well | and |
| ----------- | ----- | --------- | -------- | --------- | ------- | ------------- | -------- | ------- | ------ | ----------- | ---------- | ------ | ---------------- | ------- | --- |
| The LoRaWAN |       | network   |          | relies on | the     | hub-and-spoke |          | topol-  |        |             |            |        |                  |         |     |
|             |       |           |          |           |         |               |          |         | can be | calculated  | as follows | (P     | rx = 15.2 mW     | [12]):  |     |
| ogy in      | which | LoRaWAN   | gateways |           | relay   | messages      |          | between |        |             |            |        |                  |         |     |
| end-devices | and   | a central | network  |           | server. | This          | approach | in-     |        |             |            |        |                  |         |     |
|             |       |           |          |           |         |               |          |         |        |             | P          | ·T     | 15.2·36.096      |         |     |
troduces two main problems: cost and power consumption. rx onair
|           |          |          |     |       |       |         |     |         | SF =7,E |     | =   |     | =   | =8.57uJ/bit |     |
| --------- | -------- | -------- | --- | ----- | ----- | ------- | --- | ------- | ------- | --- | --- | --- | --- | ----------- | --- |
|           |          |          |     |       |       |         |     |         |         | rx  |     | 8   | 8∗8 |             |     |
| Deploying | multiple | gateways |     | for a | large | LoRaWAN |     | network |         |     |     |     |     |             |     |
(2)
| is expensive, |               | since LoRaWAN |               | gateways         |                | normally      | cost         | from    |        |           |        |             |            |            |     |
| ------------- | ------------- | ------------- | ------------- | ---------------- | -------------- | ------------- | ------------ | ------- | ------ | --------- | ------ | ----------- | ---------- | ---------- | --- |
|               |               |               |               |                  |                |               |              |         | Hence, | the total | energy | consumption | for        | 3 hops is: |     |
| hundreds      | to thousands  |               | of            | dollars.         | In             | addition,     | LoRaWAN      |         |        |           |        |             |            |            |     |
| gateways      | require       | internet      |               | access           | to communicate |               | with         | the     |        |           |        |             |            |            |     |
|               |               |               |               |                  |                |               |              |         |        | E Total   | =3·E   | tx +2·E     | rx =0.67mJ |            | (3) |
| server,       | which         | for many      | applications, |                  | like           | smart         | agriculture, |         |        |           |        |             |            |            |     |
| internet      | access        | might         | not be        | available.       | In             | such          | cases,       | we will |        |           |        |             |            |            |     |
| have to       | rely on       | cellular      | network       | which            | increases      |               | the          | network |        |           |        |             |            |            |     |
| development   | cost.         |               |               |                  |                |               |              |         |        |           |        |             |            |            |     |
| The           | second        | issue         | is the        | power            | consumption.   |               | To           | achieve |        |           |        |             |            |            |     |
| optimal       | transmission, |               | LoRa          | utilises         | configuration  |               | parameters:  |         |        |           |        |             |            |            |     |
| the carrier   | frequency,    |               | the spreading |                  | factor,        | the bandwidth |              | and     |        |           |        |             |            |            |     |
| the coding    | rate          | [10].         | The           | combination      |                | of these      | parameters   |         |        |           |        |             |            |            |     |
| affects       | energy        | consumption   |               | and transmission |                | ranges.       |              | Taoufik |        |           |        |             |            |            |     |
etal.[11]calculatethetheoreticalmaximumrangethatcanbe
| achieved | at given | output | power | (P  | ) level | with | at  | different |     |     |     |     |     |     |     |
| -------- | -------- | ------ | ----- | --- | ------- | ---- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
Tx
spreadingfactors(SF).Inaddition,theyalsoproposedaenergy
| consumption | model  | based | on   | these   | parameters |            | as following: |     |     |     |     |     |     |     |     |
| ----------- | ------ | ----- | ---- | ------- | ---------- | ---------- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
|             | P      | (P    | )·(N |         | +N         | +4.25)·2SF |               |     |     |     |     |     |     |     |     |
| E           | = cons | Tx    |      | Payload | p          |            |               | (1) |     |     |     |     |     |     |     |
tx
8·PL·BW
| where        | E                                           | is the | energy | consumed |         | per bit, | P            | (P  | )   |     |     |     |     |     |     |
| ------------ | ------------------------------------------- | ------ | ------ | -------- | ------- | -------- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
|              | tx                                          |        |        |          |         |          | cons         | Tx  |     |     |     |     |     |     |     |
| is the total | consumed                                    |        | power  | which    | depends | on       | transmission |     |     |     |     |     |     |     |     |
| power(P      | Tx ),PListhepayloadsizeandBWisthebandwidth. |        |        |          |         |          |              |     |     |     |     |     |     |     |     |
ToachievelongcommunicationrangeswithLoRaWAN(>
|     |     |     |     |     |     |     |     |     | Fig.3. LoRaTime-on-AirvsdifferentSFwith8bytespayload(CR=4/5, |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------------------------ | --- | --- | --- | --- | --- | --- |
10km),highspreadingfactor(SF)arerequiredwithatransmit
BW=125kHzand8preamblesymbols)
| power greater |     | than 20 | dBm | (assuming |     | a path-loss | exponent |     |     |     |     |     |     |     |     |
| ------------- | --- | ------- | --- | --------- | --- | ----------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
equal to 3). However, a similar range can be achieved with 3 Similar observations could be found for SF9, SF10, SF11
continuoushopsusing3differentnodeswithSF=7.Lowering and SF12. As a conclusion, for a battery operated LoRa net-
the spreading factor consumes significantly less energy. Total work covering a large range (> 10km), a dynamic multi-hop
energy consumption for these two scenarios can be calculated mesh network could be much more efficient than LoRaWAN.
basedonEquation1forSX1262LoRatransceiversat20dBm The power consumption is also distributed across multiple
(P (20dBm) = 389.4 mW [12]) with 8 bytes payload. Fig. nodes, resulting in overall better life span for “battery driven”
cons
3 shows the E tx for all spreading factors (6 to 12). WSN compared with LoRaWAN.

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     |     |     |     |     | 4   |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Inaddition,LoRaWAN’sasynchronous,ALOHA-basedpro- infrastructure. The key feature of their network is the use of
tocol limits its scalability and reliability [13]. Capacity of intermediate repeater nodes (RN) that allow the formation of
LoRaWAN networks are simulated and discussed in [14], individual linear multi-hop network with clusters of sensor
which indicates LoRaWAN network has very limited capacity nodes (SN). Although this network works for monitoring
due to desiccation and duty-cycle restrictions. Varsier and underground infrastructure, their implementation comes with
Schwoerer [15] found that PDR reduced to 25% due to some limitations. The bare-bone underlying structure is still
packetcollisionsforavirtuallarge-scaleapplicationwithhigh LoRaWAN. As discussed in Section II-B, the limitations of
node densities. To overcome the limitations of LoRaWAN, LoRaWAN still remain unsolved. In addition, the maximum
more recent studies describe time-slot-based medium access number of the child-nodes is limited to 5 SNs due to the
mechanisms.WhilePiyareetal.[16]describeanasynchronous inherent payload restriction of the LoRaWAN standard. The
time division multiple access (TDMA) with a separate wake- author also observed that the RNs consume about twice as
up radio channel (range of wake-up radio tested in lab envi- much energy as SNs because of the additional LoRaWAN
ronment, not multi-hop within sub-net), Reynders et al. [17] communication with the gateway. This means the RNs will
suggest using lightweight scheduling that needs an adoption drain faster than SNs in battery life, resulting in a dispropor-
of the LoRaWAN network. tionatefailurerate.WhenRNsfail,allconnectedSNswilllose
|     |     |     |     |     |     |     |     | the network | connection. |     | Thus these | limitations |     | could | result in |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----------- | --- | ---------- | ----------- | --- | ----- | --------- |
C. Concurrent Transmission (CT) with LoRa higher failure rates in certain nodes and non-optimal power
consumption.
Chun-HaoLiaoetal.[18]developedaconcurrenttransmis-
| sion (CT) | flooding | based | multi-hop | LoRa | network | with | low |     |     |      |             |     |     |     |     |
| --------- | -------- | ----- | --------- | ---- | ------- | ---- | --- | --- | --- | ---- | ----------- | --- | --- | --- | --- |
|           |          |       |           |      |         |      |     |     |     | III. | OURSOLUTION |     |     |     |     |
collisionratebyintroducingrandomdelay.Theydemonstrated
|     |     |     |     |     |     |     |     | To enable | the | data collection |     | with varying |     | sensors | as well |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | --- | --------------- | --- | ------------ | --- | ------- | ------- |
asuccessfuldeploymentof18sensorsbetweenmultiplebuild-
|     |     |     |     |     |     |     |     | as to support | wide | area | coverage | with | low energy |     | consump- |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------- | ---- | ---- | -------- | ---- | ---------- | --- | -------- |
ingsacross290mx195marea.However,theirapproachfalls
|          |               |     |            |       |         |     |     | tion, we | proposed | a hybrid | network |     | with | short | and long- |
| -------- | ------------- | --- | ---------- | ----- | ------- | --- | --- | -------- | -------- | -------- | ------- | --- | ---- | ----- | --------- |
| short in | the following |     | two design | rules | of WSN. |     |     |          |          |          |         |     |      |       |           |
rangecommunicationlinksanddesignedourownsensornode
|     |     |     |     |     |     |     |     | by integrating |              | low-power   | micro-controller |          | with         | dual          | wireless   |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------- | ------------ | ----------- | ---------------- | -------- | ------------ | ------------- | ---------- |
|     |     |     |     |     |     |     |     | communication  |              | interfaces  | (915MHz          | and      | 2.4GHz)      |               | to support |
|     |     |     |     |     |     |     |     | the proposed   | network.     |             |                  |          |              |               |            |
|     |     |     |     |     |     |     |     | A. Network     | Architecture |             |                  |          |              |               |            |
|     |     |     |     |     |     |     |     | Our hybrid     |              | network     | architecture     | is       | shown        | in Fig.       | 1. Our     |
|     |     |     |     |     |     |     |     | network        | topology     | is a mesh   | of               | multiple | smaller      | star-topology |            |
|     |     |     |     |     |     |     |     | sub-networks.  |              | We use LoRa | to               | build    | a Long-Range |               | Mesh       |
|     |     |     |     |     |     |     |     | Network        | (LRMN)       | and         | ANT to           | build    | a Short      | Range         | Star       |
|     |     |     |     |     |     |     |     | Network        | (SRSN)       | for         | each individual  |          | sub-network. |               | SRSN       |
Fig.4. DemonstrationofLoRaConcurrentTransmissionProblem[18] can cover a circular area of a radius of about 30 meters.
|     |     |     |     |     |     |     |     | SRSN works | in  | the hub-and-spoke |     | mode | with | a   | single hub |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --- | ----------------- | --- | ---- | ---- | --- | ---------- |
First, the CT-flooding approach is not applicable for WSN node receiving data from multiple spoke nodes. There are
due to high-power consumption. Figure 4 shows a basic two reasons behind the hybrid architecture. First, the IoT
relay map of a CT-LoRa network with 18 sensors. For the network should enable data collection in a wide area. Though
| source node | to  | transmit | one data | package | to the | destination |     |     |     |     |     |     |     |     |     |
| ----------- | --- | -------- | -------- | ------- | ------ | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
LoRaWANiscapableofprovidingend-to-endcommunication
node, this CT-LoRa will have a total of 17 transmission of several miles, it suffers from high energy cost and the
and 17 receiving windows across the network. While in a inadaptability of dynamic environments in applications like
| very optimized |     | network | only 5 | transmission |     | and receiving |     |              |            |     |            |     |      |               |     |
| -------------- | --- | ------- | ------ | ------------ | --- | ------------- | --- | ------------ | ---------- | --- | ---------- | --- | ---- | ------------- | --- |
|                |     |         |        |              |     |               |     | agriculture. | Therefore, |     | we utilize | the | long | communication |     |
windows are required for transmitting the same package. This ability of LoRa to design the LRMN while we use the much
isespeciallytrueforany“batterydriven”LoRabasednetwork
|     |     |     |     |     |     |     |     | more energy | efficient | SRSN | for | near-neighbor |     | communica- |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --------- | ---- | --- | ------------- | --- | ---------- | --- |
since LoRa transmission is extremely expensive in terms of tion.Second,forcertainapplications,theremaybesomeareas
power when operating at high SF and transmission power. with dense deployments of sensor nodes, in which LoRa is
| Second, | collision | still | exists | with a | high density |     | of end |             |     |            |         |             |     |            |     |
| ------- | --------- | ----- | ------ | ------ | ------------ | --- | ------ | ----------- | --- | ---------- | ------- | ----------- | --- | ---------- | --- |
|         |           |       |        |        |              |     |        | an overkill | and | will cause | network | contention. |     | Therefore, | we  |
devices. The authors studied the packet reception rate (PRR) design SRSN to collect data in such subareas for energy
| with different                                           | numbers |          | of relays     | for each | node.  | The    | results | conservation. |      |     |     |     |     |     |     |
| -------------------------------------------------------- | ------- | -------- | ------------- | -------- | ------ | ------ | ------- | ------------- | ---- | --- | --- | --- | --- | --- | --- |
| show that                                                | the PRR | degrades | significantly |          | as the | number | of      |               |      |     |     |     |     |     |     |
| relaysincreases.Thesedrawbackslimitthegeneralscalability |         |          |               |          |        |        |         | B. LoRa       | Mesh |     |     |     |     |     |     |
| of their                                                 | work in | WSN.     |               |          |        |        |         |               |      |     |     |     |     |     |     |
OurLoRaMeshnetworksupportsthedynamicadditionand
|                |     |      |              |     |     |     |     | removal | of sensor | node | without | causing | other | nodes | to stop |
| -------------- | --- | ---- | ------------ | --- | --- | --- | --- | ------- | --------- | ---- | ------- | ------- | ----- | ----- | ------- |
| D. Synchronous |     | LoRa | mesh Network |     |     |     |     |         |           |      |         |         |       |       |         |
functioningorothermanualeffortstoreconfigurethenetwork.
Recently,Ebietal.[19]proposedameshnetworkapproach During deployment, the new node only needs to be placed
toextendthecapabilityofLoRaWANbyintegrationwithalin- in the location of interest and it will join the mesh network
earmeshnetworkwithmulti-hoppingtomonitorunderground automatically (Setup Phase in Algorithm 2).

IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 5
1) TDMA Scheduling Algorithm: One important require- Algorithm 1 LoRa Communication Mode Scheduling
mentforthemeshnetworkistoensurethedataissuccessfully 1: procedure BUILDSCHEDULEONTHEHUBNODE
uploaded to the cloud, no matter how far the sensor node is Input: nodelist
|            |               |      |          |       |        |         |           |       | Output: | schedule |     |     |     |
| ---------- | ------------- | ---- | -------- | ----- | ------ | ------- | --------- | ----- | ------- | -------- | --- | --- | --- |
| away from  | the           | LoRa | gateway. | Since | the    | sensor  | node that | is    |         |          |     |     |     |
| out of the | communication |      | range    | of    | a LoRa | gateway | needs     | to 2: | do      |          |     |     |     |
find a intermediate node for routing its data, the intermediate slot=new Slot();
3:
nodesandthesensornodeneedtocoordinatethetimewindow 4: send coll list = [];
so that the intermediate node is in reception mode while the 5: recv coll list = [];
|             |     |         |     |       |           |          |     |         |     | while nodelist.length>0 |     | do  |     |
| ----------- | --- | ------- | --- | ----- | --------- | -------- | --- | ------- | --- | ----------------------- | --- | --- | --- |
| sensor node | is  | sending | its | data. | A trivial | solution | to  | this 6: |     |                         |     |     |     |
coordination problem is to always open the reception channel 7: node=nodelist[0];
of the intermediate node. However, an always-on reception 8: if (node.recv ==0
channelisenergyinefficient(approximately10mAcurrentfor 9: and
the device in LoRa reception mode vs 2 µA in sleep mode, 10: node.packet>0
and
| 5000 times | increase |     | in power). |     |     |     |     | 11: |     |     |     |     |     |
| ---------- | -------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Therefore, we adopt a Time-Division Multiple Access 12: !send coll list.contains(node)
(TDMA) scheduling algorithm [20] and customize it to our 13: and
|     |     |     |     |     |     |     |     |     |     | !receive | coll | list.contains(node)) |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | ---- | -------------------- | --- |
system. The pseudo-code is shown in Algorithm 1. The 14: then
input, nodelist is the list of nodes in the network sorted 15: slot[node]=(cid:48) SEND(cid:48);
in the descending hops to the LoRa gateway. Therefore, the slot[node.dest]=(cid:48) RECV(cid:48);
16:
algorithm starts with the node which is the furtherest from 17: send coll list.insert(node.dest.nbrs)
the gateway (line 7 in Algorithm 1) and ends with the node 18: send coll list.insert(node.dest)
|          |         |     |              |     |       |           |           |     |     | recv | coll | list.insert(node.nbrs) |     |
| -------- | ------- | --- | ------------ | --- | ----- | --------- | --------- | --- | --- | ---- | ---- | ---------------------- | --- |
| which is | closest | to  | the gateway. |     | There | are three | operating | 19: |     |      |      |                        |     |
modes (Receive / Send / Sleep) of LoRa. The scheduling 20: node.dest.recv−−;
algorithm coordinates the sending and receiving actions for node.packet−−;
21:
all nodes in the mesh network so that the data is transmitted 22: if (node.packet==0) then
without collisions with any other neighboring nodes that are 23: nodelist.remove(node);
alsosendingdataatthesametime.Additionally,customization 24: schedule.insert(slot)
puts the nodes mostly in Sleep mode. The difference between while slot.length>0
25:
theoriginalalgorithm[20]andAlgorithm1isthattheoriginal
|           |         |     |      |          |         |       |           | 26: | return | schedule |     |     |     |
| --------- | ------- | --- | ---- | -------- | ------- | ----- | --------- | --- | ------ | -------- | --- | --- | --- |
| algorithm | assumes | a   | node | can send | all the | data, | including | its |        |          |     |     |     |
ownsensordataaswellasthedatareceivedfromothernodes,
in the same packet in one timeslot. However, each node can followsthescheduletosendorreceivedata.Inthethirdphase
only send data with fixed size. Therefore, if the data to be (line 8 in Algorithm 2), the node sleeps to save energy since
| sent is too | large, | it has | to be | fragmented | into | multiple | packets |          |     |               |      |        |     |
| ----------- | ------ | ------ | ----- | ---------- | ---- | -------- | ------- | -------- | --- | ------------- | ---- | ------ | --- |
|             |        |        |       |            |      |          |         | it knows | no  | one will send | data | to it. |     |
andsentatmultipletimeslots.Thiscustomizationisduetothe
| packet size      | limitation |            | in a single  | LoRa        | transmission. |                 | SX1262 |        |     |     |     |     |     |
| ---------------- | ---------- | ---------- | ------------ | ----------- | ------------- | --------------- | ------ | ------ | --- | --- | --- | --- | --- |
| LoRa transceiver |            | [12],      | which        | we used     | in            | our deployment, |        | has    |     |     |     |     |     |
| only 256         | bytes      | of the     | transmission |             | buffer.       | Thus, assuming  |        | the    |     |     |     |     |     |
| size of a        | single     | fragmented |              | data packet | is            | 256 bytes,      | if a   | node   |     |     |     |     |     |
| has received     | 3          | packets    | from         | 3 neighbors |               | plus 1          | packet | of its |     |     |     |     |     |
| own sensor       | data,      | it         | will need    | to send     | 4             | packets         | with   | 1 KB   |     |     |     |     |     |
sizeofdata.The1KBdatacannotbefulfilledinonetimeslot
| due to the | SX1262 | buffer | limitation. |     | Line | 22 of | Algorithm | 1   |     |     |     |     |     |
| ---------- | ------ | ------ | ----------- | --- | ---- | ----- | --------- | --- | --- | --- | --- | --- | --- |
checks the remaining packets (including those received from Fig.5. ThreephasesofthenodesinLoRamesh.Dutycycleconsistsofthe
|     |     |     |     |     |     |     |     | initial | Setup phase | and any | Data Passing | phases. One period | cycle consists |
| --- | --- | --- | --- | --- | --- | --- | --- | ------- | ----------- | ------- | ------------ | ------------------ | -------------- |
other nodes as well as the packets generated by itself) of a ofoneDataPassingandthefollowedSleepphase.
| node and     | only    | after all | of its | packets    | have    | been          | scheduled,  | it   |                 |      |           |     |     |
| ------------ | ------- | --------- | ------ | ---------- | ------- | ------------- | ----------- | ---- | --------------- | ---- | --------- | --- | --- |
| will be      | removed | from      | the    | nodelist   | so that | the algorithm |             | will |                 |      |           |     |     |
| not schedule | it      | for the   | future | timeslots. | Section |               | III-C gives | a    |                 |      |           |     |     |
|              |         |           |        |            |         |               |             | C.   | Why centralized | mesh | protocol? |     |     |
concreteexampletoexplainhowthemeshnetworkisbuiltup
using Algorithms 1 and 2 The communication in our mesh network must guarantee
2) Our Mesh Protocol: The LoRa node in our mesh net- there is no collision where two nodes send data to a third
work has three phases as shown in Figure 5, namely Setup, node at the same time. Therefore, when creating the schedule
Data Passing, and Sleep. The first phase (line 2 to 6 in foreachnodetocommunicatedata,weneedtounderstandthe
Algorithm 2) is the setup phase where the nodes build up a whole network structure so as to avoid such communication
routing table and the LoRa hub node builds a communication collisions. Therefore, we design a centralized approach where
schedule that indicates the time window for which nodes the hub node in the LoRa mesh is in charge of collecting
to send data (Algorithm 1). The second phase (line 7 in informationfromothernodestounderstandthewholenetwork
Algorithm 2) is the data passing phase where each node structure as well as creates the schedule according to the

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     |     |     |     | 6   |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Algorithm 2 LoRa Mesh Network Protocol during the next TDMA cycle, and will switch to reception
1: procedure OPERATIONSOFEACHNODE mode for further instructions. Eventually, all nodes will not
Setup Phase transmit anything, and the hub node detects there is a failure.
|     | Each | node | builds | local | routing | table | using | distance |     |     |     |     |     |     |
| --- | ---- | ---- | ------ | ----- | ------- | ----- | ----- | -------- | --- | --- | --- | --- | --- | --- |
2: The hub node will issue a reset beacon message and floods it
vector routing protocol. to all node with similar techniques discussed in Section III-D.
Each node broadcasts its own routing table and for- After receiving the beacon, the network will repeat the setup
3:
wards others’ routing tables, for the purpose of gathering phase and recovers from the node failure.
|     | all routing | tables | at     | the Hub          | node. |       |     |           |     |     |     |     |     |     |
| --- | ----------- | ------ | ------ | ---------------- | ----- | ----- | --- | --------- | --- | --- | --- | --- | --- | --- |
|     | Hub         | node   | builds | the connectivity |       | table | for | the whole |     |     |     |     |     |     |
4:
|     | network | after | collecting |     | all routing |     | tables | from other |     |     |     |     |     |     |
| --- | ------- | ----- | ---------- | --- | ----------- | --- | ------ | ---------- | --- | --- | --- | --- | --- | --- |
nodes.
5: HubnodeexecutesAlgorithm1tobuildthecommuni-
|     | cation | schedule | of each | node | and | floods | the schedule | out; |     |     |     |     |     |     |
| --- | ------ | -------- | ------- | ---- | --- | ------ | ------------ | ---- | --- | --- | --- | --- | --- | --- |
alltheothernodesforwardthescheduleafterreceivingit.
|     | Data | Passing |       | Phase      |     |          |       |        |     |     |     |     |     |     |
| --- | ---- | ------- | ----- | ---------- | --- | -------- | ----- | ------ | --- | --- | --- | --- | --- | --- |
| 6:  | Each | node    | sends | / receives |     | / sleeps | based | on the |     |     |     |     |     |     |
schedule.
|     | Sleep | Phase |       |       |          |      |         |        |     |     |     |     |     |     |
| --- | ----- | ----- | ----- | ----- | -------- | ---- | ------- | ------ | --- | --- | --- | --- | --- | --- |
|     | All   | nodes | sleep | until | the next | Data | Passing | Phase. |     |     |     |     |     |     |
7:
|     |     |     |     |     |     |     |     |     | Fig.6. Floodhellomessagetobuildroutingtableineachsensornode.After |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----------------------------------------------------------------- | --- | --- | --- | --- | --- |
routingtablesarebuiltandcollectedbyNode1,aconnectivitytableiscreated
toreflecttheconnectivityofthewholenetwork.
| network | structure. |     | It first      | collects | the              | routing | table   | from each   |     |     |     |     |     |     |
| ------- | ---------- | --- | ------------- | -------- | ---------------- | ------- | ------- | ----------- | --- | --- | --- | --- | --- | --- |
| LRMN    | node       | so  | that based    | on       | the neighborhood |         |         | information |     |     |     |     |     |     |
| of      | each node, | it  | can construct |          | the              | whole   | network | structure,  |     |     |     |     |     |     |
TABLEII
namelytheconnectivitytablereferredinline5ofAlgorithm2. THESCHEDULEBUILTFORTHENETWORKINFIGURE6.AFTERTIMESLOT
Therefore, the scheduling algorithm is centralized and we 6,ALLNODESSWITCHTOSLEEPMODE.
empirically choose the node closest to the LoRa gateway as Node/Timeslot 1 2 3 4 5 6
| the   | LoRa       | hub to | do those | jobs. |     |     |     |     | 1   |     | Rx Rx    | Rx Tx       | Tx    | Tx    |
| ----- | ---------- | ------ | -------- | ----- | --- | --- | --- | --- | --- | --- | -------- | ----------- | ----- | ----- |
| Build | individual |        | routing  | table |     |     |     |     | 2   |     | Rx Tx    | Tx Sleep    | Sleep | Sleep |
|       |            |        |          |       |     |     |     |     | 3   |     | Tx Sleep | Sleep Sleep | Sleep | Sleep |
We used a simple version of routing information proto- 4 Tx Sleep Sleep Sleep Sleep Sleep
| col         | [21]    | to create | the       | routing  | table.   | Figure    | 6               | shows how |         |                 |     |     |     |     |
| ----------- | ------- | --------- | --------- | -------- | -------- | --------- | --------------- | --------- | ------- | --------------- | --- | --- | --- | --- |
| the         | routing | table     | is built. | The      | LoRa     | hub       | node broadcasts |           | a       |                 |     |     |     |     |
| hello       | message | and       | whoever   | receives |          | the hello | message         | will      |         |                 |     |     |     |     |
|             |         |           |           |          |          |           |                 |           | D. Time | Synchronization |     |     |     |     |
| rebroadcast |         | it. The   | hello     | message  | includes |           | the information | of        |         |                 |     |     |     |     |
who the sender is and the shortest distance from the sender to Time accuracy is crucial for any TDMA based collision-
thehubnode.Eventually,allnodeswillhearthehellomessage free network. Un-synchronized time across the network will
|      |       |           |     |       |               |     |         |        | result in | data | loss and network | failure. In | addition, | without |
| ---- | ----- | --------- | --- | ----- | ------------- | --- | ------- | ------ | --------- | ---- | ---------------- | ----------- | --------- | ------- |
| from | their | neighbors | and | build | an individual |     | routing | table. |           |      |                  |             |           |         |
Collect individual routing table an external time source, the micro-controller often relies on
The individual routing tables are sent to the hub to create crystaloscillatortorecordtime.However,thecrystaloscillator
the connectivity table, which is then referred by the TDMA driftsovertime.Therefore,periodictimesynchronizationover
algorithm to create routing schedules. Every node will broad- the network is required for stable operation. Ebi et al [19].
cast its routing table to its neighbors. Additionally, when a employanexternaltimesourcemodule(GPS)intheirnetwork
node receives a routing table that it has not received yet to acquire the coordinated universal time (UTC) at RNs [19].
will rebroadcast that routing table. Eventually, after all the This time will transmit to the connected SNs by a ”beacon
routing tables are collected at the hub node, the hub node flooding” with TDMA scheduling. However, using TDMA
will build a connectivity table that reflects the whole network in a LoRa mesh network for down-link communication will
structure. Figure 6 also shows the connectivity table for that significantly increase the overhead of the network. On the
mesh network. other hand, concurrent flooding addressed the need of the
Create schedules for all the nodes smaller overhead at a cost of higher chances of package
The hub node will refer to the connectivity table as well as collision [18]. Fig. 7 demonstrates the possible collision that
thecustomizedTDMAschedulingalgorithminSectionIII-B1 could happen in such approach. To overcome this issue, we
to build the schedule of each node as shown in Table II. The insert a random delay between the flooding messages to
schedule is used by each node in the Data Passing phase to minimize the possibility of package collision similar to Liao
| either | send | or receive | data. |     |     |     |     |     | et al.’s work | [18]. |     |     |     |     |
| ------ | ---- | ---------- | ----- | --- | --- | --- | --- | --- | ------------- | ----- | --- | --- | --- | --- |
Recover from node failure Fig. 7 shows the detailed time synchronization process, for
Incaseofanodefailure,theassociatednodesthatnormally each synchronization cycle, the center node (Node 1 in Fig.
receive data from the failed node will immediately discover 7) will initiate a 5 bytes beacon package containing source
thefailure(nodownlinkcommunicationfromthefailednode) of this beacon (N source ), number of hops (N hops ) from the

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |             |     |             |        |     |       |      | 7           |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | ----------- | --- | ----------- | ------ | --- | ----- | ---- | ----------- |
|                                       |     |     |     |     |     |     | the network | is  | stabilized, | during | the | first | TDMA | cycle, each |
nodewillbeawareoftheRSSIfromitsprevioustransmission.
|     |     |     |     |     |     |     | Then each | node | will | adjust | its P | based | on collected | RSSI |
| --- | --- | --- | --- | --- | --- | --- | --------- | ---- | ---- | ------ | ----- | ----- | ------------ | ---- |
TX
|     |     |     |     |     |     |     | value. After | the           | adjustment, |            | a new       | RSSI  | will be   | updated to |
| --- | --- | --- | --- | --- | --- | --- | ------------ | ------------- | ----------- | ---------- | ----------- | ----- | --------- | ---------- |
|     |     |     |     |     |     |     | verify the   | quality       | of          | each LoRa  | link        | (RSSI | -120dBm). | This       |
|     |     |     |     |     |     |     | process      | will increase |             | the energy | efficiency  |       | of each   | LoRa link  |
|     |     |     |     |     |     |     | without      | degrading     | link        | quality.   |             |       |           |            |
|     |     |     |     |     |     |     | F. ANT       | Hub-and-Spoke |             | Network    |             |       |           |            |
|     |     |     |     |     |     |     | We use       | ANT           | to build    | the        | Short-Range |       | Network   | (SRSN).    |
Fig.7. Leftfigurerepresentsthepossiblepackagecollisioncausedbytime
|           |                      |       |        |           |             |          | ANT auto | shared | channel | (ASC) | is  | a communication |     | channel |
| --------- | -------------------- | ----- | ------ | --------- | ----------- | -------- | -------- | ------ | ------- | ----- | --- | --------------- | --- | ------- |
| sync with | concurrent flooding. | Right | figure | shows the | solution of | the time |          |        |         |       |     |                 |     |         |
synchronizationprocesswithrandomdelay. specified by ANT [23], and it is used to build reliable bi-
|                               |     |     |     |                     |     |     | directional       | communication |     | in        | a hub-and-spoke |     | topology. | The       |
| ----------------------------- | --- | --- | --- | ------------------- | --- | --- | ----------------- | ------------- | --- | --------- | --------------- | --- | --------- | --------- |
|                               |     |     |     |                     |     |     | ASC communication |               |     | structure | is shown        | in  | Figure    | 8. An ANT |
| centernodeandtherandomdelay(T |     |     |     | )beforetransmitting |     |     |                   |               |     |           |                 |     |           |           |
delay hub node receives data from other spoke nodes. All spoke
| this beacon | from the center | node.    | Any         | node    | that receives | this |              |     |        |         |                |        |             |          |
| ----------- | --------------- | -------- | ----------- | ------- | ------------- | ---- | ------------ | --- | ------ | ------- | -------------- | ------ | ----------- | -------- |
|             |                 |          |             |         |               |      | nodes share  | a   | single | channel | to communicate |        | with        | the hub. |
| beacon will | wait for        | T delay  | that is     | smaller | than the      | LoRa |              |     |        |         |                |        |             |          |
|             |                 |          |             |         |               |      | ASC supports |     | up to  | 66K     | spoke          | nodes. | By default, | ASC      |
| symbol      | time T          | and then | immediately |         | re-transmit   | this |              |     |        |         |                |        |             |          |
symbol requires a user specified channel master node to establish the
| beacon. | This approach | minimizes |     | the package | collision | as  |     |     |     |     |     |     |     |     |
| ------- | ------------- | --------- | --- | ----------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
network,weaddedalayerontopofthatcalledAdaptiveMode
| well as                       | the down-link     | overhead   | since       | the                    | flooding | beacon |                |       |                |                 |        |         |             |             |
| ----------------------------- | ----------------- | ---------- | ----------- | ---------------------- | -------- | ------ | -------------- | ----- | -------------- | --------------- | ------ | ------- | ----------- | ----------- |
|                               |                   |            |             |                        |          |        | Switching      | (AMS) | to             | dynamically     | select | the     | hub         | node. AMS   |
| is only 5                     | bytes. After      | the beacon |             | has been               | received | by the |                |       |                |                 |        |         |             |             |
|                               |                   |            |             |                        |          |        | is based       | on a  | round          | robin (based-on |        | battery | level)      | campaign    |
| nodes,therelativetimeelapsedT |                   |            | past        | sincethepreviousnode’s |          |        |                |       |                |                 |        |         |             |             |
|                               |                   |            |             |                        |          |        | to select      | the   | hub node.      | During          | the    | setup   | phase,      | each node   |
| transmission                  | can be calculated |            | as follows: |                        |          |        |                |       |                |                 |        |         |             |             |
|                               |                   |            |             |                        |          |        | will broadcast |       | its ID         | and battery     | level  | and     | actively    | listens for |
|                               |                   |            |             |                        |          |        | other near-by  |       | ANT broadcast, |                 | node   | with    | the highest | battery     |
|                               | T =T              |            | +T          | +T                     |          | (4)    |                |       |                |                 |        |         |             |             |
past beacon node delay level will become the hub node. If multiple nodes have the
|       |          |      |         |          |         |         | same battery | level, | the | node | with the | lowest | ID  | will become |
| ----- | -------- | ---- | ------- | -------- | ------- | ------- | ------------ | ------ | --- | ---- | -------- | ------ | --- | ----------- |
| where | T is the | time | that is | need for | node to | process |              |        |     |      |          |        |     |             |
node
and re-transmit the beacon, T is the time on air of the the hub node. Once the hub node was selected, the ASC uses
beacon
|     |     |     |     |     |     |     | an ANT | proprietary |     | shared | channel | topology | to  | establish the |
| --- | --- | --- | --- | --- | --- | --- | ------ | ----------- | --- | ------ | ------- | -------- | --- | ------------- |
package.
However, because of the variability of the T due to network, with the hub node being channel master and the rest
node
|                  |               |               |     |                       |     |     | of the nodes | become |     | shared | slaves | [23]. |     |     |
| ---------------- | ------------- | ------------- | --- | --------------------- | --- | --- | ------------ | ------ | --- | ------ | ------ | ----- | --- | --- |
| the SPI          | communication | between       |     | the micro-controller  |     | and |              |        |     |        |        |       |     |     |
| LoRa transceiver | and           | the imperfect |     | time synchronization, |     | we  |              |        |     |        |        |       |     |     |
manuallyexpandthereceivingwindowsby5mstocompensate
fortheinconsistency.Thisprocesswillsynchronizethetiming
acrossallthenodeinthenetworktoavoidthetimedriftsover
| a long period | of time.  |       |     |     |     |     |                                                                  |     |     |     |     |     |     |     |
| ------------- | --------- | ----- | --- | --- | --- | --- | ---------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
| E. Adaptive   | LoRa Link | (ALL) |     |     |     |     |                                                                  |     |     |     |     |     |     |     |
|               |           |       |     |     |     |     | Fig.8. ANTsharedchannelhub-and-spokenetworkstructure.Hrepresents |     |     |     |     |     |     |     |
One of the benefits of adapting the LoRa technology is thehubnode(ChannelMaster)andSrepresentsthespokenode(sharedslave)
| the “degrees | of freedom” |     | at the | physical | layer. Ochoa |     | et  |     |     |     |     |     |     |     |
| ------------ | ----------- | --- | ------ | -------- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
al. study suggested that the the potential of an adaptive In each SRSN, all the spoke nodes send data to a hub
LoRa solution (i.e., in terms of spreading factor, bandwidth, node via ANT and the hub node is in charge of uploading
transmission power, and topology) could greatly optimize the aggregated data to the cloud. The hub node has two
energy consumption without sacrificing the communication methods to upload the aggregated data. First, if the SRSN
range [22]. In our proposed LoRa mesh network, we provide is a standalone network and associated with an ANT gateway,
the proof of such concept by adopting the Adaptive LoRa it does not need to enable the AMS functionality but directly
Link (ALL) to further improve the energy performance of the sends data to the ANT gateway. Second, if the SRSN is part
network.Althoughtherearemanyphysicalparametersthatcan ofaLRMN(theSRSNclustersinFigure1),thehubnodewill
affecttheenergyoftheLoRalink,SFandtransmissionpower switchtoLoRamodetoroutetheaggregateddatatotheLoRa
have the most impact in term of the energy consumption. In gateway. Clearly, the hub node consumes more energy than
this work, as a proof of concept, we are only focusing on the spoke nodes. Therefore, AMS is used for balancing the
adjusting the transmission power of the network. However, energy consumption. Figure 9 demonstrates this idea. When
similar methodologies will apply for adjusting the SF. a hub node drains to a lower-than-threshold battery level, it
During the setup phase, in addition to building a routing will issue a AMS message and the spoke node with highest
table, each node will note the Received Signal Strength batteryandwithinthesameSRSNwillbeselectedasthenew
Indicator (RSSI) which is a estimated measure of the signal hub. The original hub node then works as a spoke. This AMS
powerlevelfromeachoftheLoRapackagesitreceived.Once feature guarantees no single node in SRSN is significantly

IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 8
drainedandensurestheSRSNclusterstillremainsinthesame The hardware platform used in this study builds on the
LRMN network. hardware platform that we reported in our earlier work [24]
asshowninFig.11andFig.12(a).ItutilizestheHMAA-1220
wireless transceiver module (Fig.12(b)) from HuWoMobility
[25]. The HMAA-1220 wireless transceiver was powered by
nRF52832chipfromNordicSemiconductor[26]andSX1262
LoRa transceiver from Semtech [27]. nRF52832 features a
low power 32-bit ARM Cortex-M4F processor with a built-
in-radio that operates in the 2.4 GHz ISM band and supports
ANT, BLE and Bluetooth 5 wireless protocols with up-to +4
dBmtransmitpower.Itisalsoequippedwith64kBRAMand
512kBofflashstoragewhichcanbeusedforstoringdatafor
in-node data analysis.
Fig.9. AdaptiveModeSwitching(AMS)flowchart
To address the potential failures of the hub node, we use a
heuristic method, a timer (Failure Detection Timer in Fig. 10)
to detect the failure of the hub node. As shown in the left
part of Figure 10, during normal operation, the hub node
periodically sends an update request to each spoke node to
request for new sensor and battery data. When a spoke node
finishes data upload, the spoke node will reset the failure
detection timer. This timer is set to be much longer than the
data upload periodicity (e.g. 5 × periodicity) to count for any
possible data loss. In the scenario of hub node failure (the
right part of Fig. 10, the timers on the hub nodes will expire
and all the spoke nodes will reset itself, resulting in the entire
SRSN to be re-initialized. The remaining nodes will form a
new SRSN without the failed node. After the new SRSN is
initialized, the new hub node will switch on LoRa reception
mode and waits for the next TDMA cycle to join back to the Fig.11. Systemblockdiagramofthehardwareplatform.Adoptedfrom[24]
LoRa mesh network.
SX1262 from Semtech [12] is the new sub-GHz radio
transceiverswhichisidealforlongrangewirelessapplications.
It supports both LoRa modulation for LPWAN applications
andFSKmodulationforlegacyusecases.Inaddition,SX1262
also complies with the physical layer requirements of the
LoRaWAN specification released by the LoRa Alliance [28]
and the continuous frequency coverage of SX1262 from 150
MHz to 960 MHz allows the support of all major sub-GHz
ISM bands. SX1262 was designed for long battery life with
current consumption of 4.6 mA in active receive mode and
600 nA in sleep mode. With the highly efficient integrated
power amplifiers, SX1262 can transmit up-to +22 dBm while
having a high sensitivity down to -148 dBm. Along with
the co-channel rejection of 19 dB in LoRa mode and 88
dB blocking immunity at 1 MHz offset, SX1262 provides
Fig.10. SRSNNormalOperationsandFailureTolerance.
a maximum of 170 dB link budget which is ideal for long
distance communication.
Figure12(a) shows the printed circuit board (PCB) with its
G. Hardware Sensing Platform in Our Deployment
packaging.TheHMAA-1220(Fig.12(b))modulewasmounted
There are three main challenges when designing our plat- on a “motherboard” with 4 LEDs and some pinouts for
form for deployment: building a sufficiently low weight, low connectingdifferent“daughterboard”(Fig.12(c)).Thisdesign
costandenergyefficienthardwarecapableofmassproduction, choice allow us to extend the flexibility of our hardware plat-
incorporatingnumeroussubsystemstofacilitatevariousappli- form to facilitate different applications. The entire PCB was
cations (e.g.smart agriculture and smart city), and protecting enclosed in an IP67 Industrial-grade packaging for protection
the electronics from harsh environmental conditions. against environmental factors.

IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 9
meaning from a network stack point of view, this lab test will
be able to simulate the real-world conditions.
Table III shows the LoRa configuration of the lab experi-
ment. To fully review the performance as well as the stability
of the network, we kept the network running with each node
programmedtotransmitone64Bytesdatapackageperminute
(1.8kBps)foranentireweek.Astheperformanceindicator,the
receiverrecordsallofthenetworktrafficfromallnodes.RSSI
are not evaluated in this test since we intentionally lowered
the TX power of all LoRa nodes. We evaluated the reliability
and stability of data packet delivery for each individual node
using the packet deliver rate (PDR), i.e. the ratio between the
number at the center node (# RECEIVED) and the number of
packets that should have been received (# EXPECTED). With
the help of the traffic monitoring receiver, two sets of PDRs
Fig. 12. The hardware platform: (a) Motherboard PCB and battery holder
were can be calculated, PDR and Total PDR :
with its packaging, (b) Motherboard PCB with two daughter boards, (c)the i d
HMAA-1220module (cid:80)
#RECEIVED
PDR = i (5)
TABLEIII i (cid:80) #EXPECTED i
LORACONFIGURATIONFORTHEIN-LABTESTANDFIELDDEPLOYMENT
Where PDR is the packet delivery rate of node i during
i
Parameter In-labtest FieldDeployment the entire week.
Spreading
Factor SF 7 7 (cid:80) #RECEIVED
B Pr a e n a d m w b i l d e th BW 125 8 kHz 125 8 kHz Total PDR d = (cid:80) d d #EXPECTED (6)
length
Transmission Where Total PDR d is total the packet deliver rate of all
Power
PTx +0dBm Variable
the node during the #dth day.
CodingRate CR 4/5 4/5
Theestimationofthenumberofexpectedpacketsarebased
Head& Head&
CRCchecking Payload Payload on each specific node with constant transmission interval (1
min). Because of the nature of multi-hop network, counting
the number of packets arriving at the receiver will counts
IV. RESULTS for both node-specific performance as well as the multi-hop
A. In-lab Evaluation route from that specific node to the center node. In contrast,
Total PDR provides an overview of the network stabil-
To verify the functionality and stability of our network, we d
ity over time. Instead evaluating node-specific parameters,
conducted a series of both in-lab tests as well as real-world
Total PDR provides an overview of the system stability
deployments. d
of time synchronization as well as the TDMA routing.
1) Network Stability Test: We performed laboratory exper-
Fig. 14(a) shows the results of the PDR of our one-week
iments with 9 sensor nodes with 1 node acting purely as i
test, all nodes show more than 99% PDR except for node 4.
standalone receiver monitoring the entire network to check
Fig.14(b)showstheresultsoftheTotal PDR forthesame
the stability of the network. d
a) Network Setup: Fig. 13 shows the configuration of test, it suggests our network stability is very strong and is not
the network structure. All 8 nodes are placed together on a time dependent.
lab bench along with the receiver. Node 1 is the center node
for this test. Testing the network structure in this condition is
nontrivial since all sensors are in close proximity, the long-
range capability of LoRa will not able to form the structure
that we desired since all node are in range with each others
no matter how we configure the LoRa parameters. To resolve
this issue, we created a filter in the low-level firmware (LoRa
driver)toblockconnectionsfromun-wantedsensornodes.For
example,inthestructureshowninFig13,Node4shouldonly
Fig.13. Networkstructureforthein-labsystemstabilitytest.
receive data from Node 3 and Node 5 in the desired structure.
However, in reality node 4 is able to receive data from all 2) PowerConsumption: Thepowerconsumptionwasmea-
nodes because of the close proximity between sensors. The sured for one node under real-life conditions for a network
firmware filter will filter any data from nodes other than node structured with four nodes as shown in Fig 15. In addition,
3 and node 5. All other data will be ignored to simulate the each sensor is connected with HDC2010 temperature and
desirednetwork structure.Thebiggestbenefit oftheapproach humidity sensor. For each cycle, each node will transmit a
isthatthemesh-layerofthenetworkiscompletelyun-touched, package of 64 bytes including one temperature and humidity

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     |     |     |     |     | 10  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
TABLEIV
MEASUREDPOWERPROFILEANDEXPECTEDBATTERYLIFEWITH2XAA
BATTERY
|     |     |     |     |     |     |     |     |                  | AverageCurrentDraw(Iavg) |                      |             |             | ExpectedBatteryLife |               |          |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | ------------------------ | -------------------- | ----------- | ----------- | ------------------- | ------------- | -------- |
|     |     |     |     |     |     |     |     | Node1            |                          | 33µA                 |             |             |                     | 9years        |          |
|     |     |     |     |     |     |     |     | Node2            |                          | 74µA                 |             |             |                     | 4years        |          |
|     |     |     |     |     |     |     |     | Node3            |                          | 56µA                 |             |             |                     | 5years        |          |
|     |     |     |     |     |     |     |     | Node4            |                          | 25µA                 |             |             |                     | 11years       |          |
|     |     |     |     |     |     |     |     | batteries)       | of each                  | node.                | Comparing   | between     |                     | nodes         | 1,2, and |
|     |     |     |     |     |     |     |     | 3, the energy    | consumption              |                      | of          | different   | nodes               | is determined |          |
|     |     |     |     |     |     |     |     | by the number    |                          | of receive/transmits |             | windows.    |                     | Note that     | Node     |
|     |     |     |     |     |     |     |     | 4 consumes       | significantly            |                      | lower       | power.      | This                | shows that    | ANT      |
|     |     |     |     |     |     |     |     | radio is         | superior                 | in terms             | of energy   | efficiency  |                     | compared      | with     |
|     |     |     |     |     |     |     |     | LoRa. In         | conclusion,              |                      | even though |             | energy              | consumption   | is       |
|     |     |     |     |     |     |     |     | highly dependent |                          | on the               | network     | structure   |                     | and while     | some     |
|     |     |     |     |     |     |     |     | nodes do         | consume                  | high                 | power,      | our network |                     | still has     | a very   |
Fig.14. Results(PDRandTotal PDR)forthein-labsystemstabilitytest. acceptable expected battery life across all nodes.
| reading.    | Due to | the | nature  | of our | mesh      | network, | energy    |     |     |     |     |     |     |     |     |
| ----------- | ------ | --- | ------- | ------ | --------- | -------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
| consumption | within | the | network | varies | depending |          | on i) the |     |     |     |     |     |     |     |     |
positionoftheparticipatingnodeinthehierarchyofthemesh
| network,     | and ii)       | the topology |                    | type of           | the network.  |               | As shown |                                                                  |        |            |        |        |            |     |            |
| ------------ | ------------- | ------------ | ------------------ | ----------------- | ------------- | ------------- | -------- | ---------------------------------------------------------------- | ------ | ---------- | ------ | ------ | ---------- | --- | ---------- |
| in Fig.      | 15 node       | 1, 2, and    | 3 are              | connected         | with          | the           | proposed |                                                                  |        |            |        |        |            |     |            |
| LoRa mesh    | protocol.     | Node         | 3                  | also communicates |               | with          | node     | 4                                                                |        |            |        |        |            |     |            |
| via ANT.     | The goal      | of           | this configuration |                   | is            | to route      | the data |                                                                  |        |            |        |        |            |     |            |
| from Node    | 4 (ANT),      |              | Node               | 3 (ANT            | + LoRa),      | and           | Node     | 2                                                                |        |            |        |        |            |     |            |
| (LoRa)       | to Node       | 1 (LoRa).    | For                | each TDMA         |               | scheduling    | cycle,   |                                                                  |        |            |        |        |            |     |            |
| Node 4       | will transmit |              | one package        | via               | ANT           | to Node       | 3 and    |                                                                  |        |            |        |        |            |     |            |
| Node 3       | will forward  |              | this package       | plus              | its           | own package   |          | to                                                               |        |            |        |        |            |     |            |
| Node 2       | via the LoRa. |              | Then, Node         | 2                 | will transmit | 3             | packages |                                                                  |        |            |        |        |            |     |            |
| (2 received  | + 1           | own) to      | Node               | 1. The            | LoRa          | configuration | for      |                                                                  |        |            |        |        |            |     |            |
| this test    | is identical  | to           | the field          | deployments       |               | with          | +18 dBm  |                                                                  |        |            |        |        |            |     |            |
| transmission | power.        |              |                    |                   |               |               |          |                                                                  |        |            |        |        |            |     |            |
|              |               |              |                    |                   |               |               |          | Fig.16. MeasuredcurrentprofileforNode3duringonetransmissioncycle |        |            |        |        |            |     |            |
|              |               |              |                    |                   |               |               |          | where blue                                                       | region | represents | LoRa’s | Tx and | Rx windows | and | red region |
representstheANTtransmissionwindow.
|     |     |     |     |     |     |     |     | 3) Hardware       |          | durability:            | To             | fully test | the          | performance | and      |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------------- | -------- | ---------------------- | -------------- | ---------- | ------------ | ----------- | -------- |
|     |     |     |     |     |     |     |     | durability        | of our   | hardware               | platform       |            | against      | harsh       | environ- |
|     |     |     |     |     |     |     |     | ments, we         | deployed | 4                      | units equipped |            | with         | our smart   | agri-    |
|     |     |     |     |     |     |     |     | culture interface |          | at Throckmorton-Purdue |                |            | Agricultural |             | Center   |
Fig.15. Networksetupfortheenergyconsumptiontest (TPAC) at Purdue University. All four units were equipped
|     |     |     |     |     |     |     |     | with temperature |     | and humidity |     | sensors | to monitor |     | the envi- |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ------------ | --- | ------- | ---------- | --- | --------- |
Power consumption was measured using a N6705B DC ronmental conditions at the farm and were placed 1 meter
power analyzer from Agilent Technology [29]. Each sensor above the ground. The deployment locations are shown in
node is powered with 3.3V DC by the DC power analyzer. Fig.17.Two oftheunitswith printedthin-filmnitratesensors
Fig.16showspartofthecurrentprofileofNode3whereeach were installed in the stream to measure the nitrate pollutants
state of operation is clearly marked. The hardware consumes from fertilizer runoffs in the stream. The other two units were
around25µAduringsleep,10mAduringANTTX,12.5mA interfaced with four independent ECH2O 5TE Soil sensors
during LoRa RX and 72.5 mA during LoRa TX. Therefore, to monitor the soil temperature, conductivity, moisture, and
the average current consumption with 10 minutes TDMA dielectric at four different depths [30]. All four units were
cycle delay for Node 3 is 56 µA which can be translate to programmed to send data every 10 minutes and the data
5.2 years of expected battery life with standard AA alkaline received at the receiver is uploaded to the data server and
batteries (2500 mAh). Table IV shows the average current displayed on the web. As of January 2020, these units have
consumptionandtheexpectedbatterylife(with2AAalkaline been continuously operating for more than a year without

IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 11
21(a)).Therednoderepresentsthelocationofthecenternode.
Thegreendotrepresentsthereceiver,alaptopconnectedwith
SX1272DVK1CAS (LoRa development kit) from Semtech
[31].EachsolidlinerepresentstheactualLoRalinkforthede-
ployed network and the dotted line represents available LoRa
links that were not being used. The node junction represents
two nodes (node 12 and node 13) that were deployed on
purpose at close range and were communicating via ANT
instead of LoRa (Fig.21(b)). In addition, three paths that are
highlighted in Fig. 18 represent three distinguished data flows
that are formed by the mesh network. For instance, path
number 1 represents the path 9 → 8 → 7 → 1. All nodes
(including the center node) are located 1 meter above ground
level as shown in Fig. 21 and the receiver is placed on the
3rd floor inside of an office building facing south-east. The
furthest node is placed 1.5 km away from the receiver and
Fig. 17. Deployment of the proposed mesh network on Purdue University across more than 18 buildings in between.
WestLafayettecampus.EachbluedotrepresentsaLoRanodeandtheblack
dashlinerepresentastableLoRalink Eachnodewasprogrammedtotransmit64Bytepackageat
a fixed time interval (2 minute) with the LoRa configuration
shownintableIII.Inaddition,twofurthestnodes6and9will
major failure. The highest temperature recorded is above send an additional package with SF12 outside of the TDMA
110 oF and the lowest temperature is -40 oF. This proves cycle as comparison with transitional ALOHA based network
our hardware is capable of withstanding harsh environmental suchasLoRaWAN.Furthermore,sincetheLoRaradioofnode
conditions while being in situ in an unmonitored outdoor 13inthenodejunctionwasnotactive(itonlycommunicatesto
environment. node12viaANT),itwasenabledtobroadcast(inparallelwith
the mesh network, acting like a LoRaWAN node) with SF12
B. Large-scale Deployment directly to the receiver used as the comparison for evaluation.
After each transmission cycle, the center node will forward
1) Farmdeployment: Ourproposednetworkwasfirsttested
all incoming packages to the receiver which will upload all
in TPAC to evaluate the multi-hop performance of the mesh
data to the cloud for future analysis. All data packages are
network for covering long-ranges. Five mesh nodes were
checkedwith16-bitCyclicRedundancyCheck(CRC)toverify
deployed in linear hop formation in addition to the existing
their integrity, corrupted data package will be marked and
4 sensing nodes equipped with soil moisture sensors and
stored. Fig. 20 shows the TDMA schedule of the deployed
flexible nitrate sensors. The newly deployed mesh nodes were
network with each slot set to 125 ms for transmitting a 64
equipped with temperature and humidity sensors as well as
Byte package. The three paths represent the three continuous
nitratesensorsandpoweredwith4AAbatteries.Fig.17shows
LoRa links as shown in Fig. 18. Each section represents one
themapofthefarmdeployment:Thegreendotrepresentsthe
different LoRa hop and are color coded for clarity. The delay
receiving computer; The red dot represents the center node
insertedafterthe3rdhopisrequiredtoavoidpackagecollision
of the mesh network; The blue dots represents the 5 mesh
withnode7frompath1.SF12referencerepresentsthetimeit
nodes;Theyellowdotsrepresentthefourpreviouslydeployed
took for one 64 Bytes transmission with SF12 as comparison.
sensornodesthatwerenotpartofthemeshnetwork.TheLoRa
It is clear that even for the longest path (Path #2) with 5 hops
configurationofeachnodeisshowninTableIIIwithSF7and
in between, the overhead of the furthest mesh node (Node 6)
TXpower=15dBm.Eachnodewasprogrammedtosendone
is smaller than the single-hop LoRaWAN node. However, it
64-bytepacketevery10minutes.Onceeachcycleiscomplete,
is worth noticing that the overheads are greater for the nodes
the center node will forward the packages to the receiver for
that were closer to the center node (Node 7, 10, and 2) and it
upload.With4linearhops,theproposedmeshnetworkisable
isanecessarytrade-offbetweenpowerefficiencyandnetwork
to cover 3 km in farmland with more than 98% PDR across
robustness.
all nodes with SF7. This experiment confirmed that our mesh
network is able to cover long distances with low spreading Over the entire evaluation period of two weeks, each node
factor (SF7). transmitted one 64 Byte package every two minutes, which
2) Campus deployment: In the campus-scale deployment, meansatotalof9360packageswereexpectedfromeachnode
we placed 13 LoRa nodes, distributed in a 1.1 km by 1.8 (13 days of operation were considered, network was taken
km area of Purdue University campus. All 13 nodes were down by one day for evaluation). As in the previous section,
deployedandcontinuouslyoperatedforaperiodoftwoweeks. the network integrity is evaluated by analyzing PDR of all
Fig. 18 shows the the complete map of our campus-scale nodes.Inaddition,thePackageMissRate(PMR)andPackage
experiment where a complete mesh network is established. Error Rate (PER) are analyzed as well. Similar to PDR, PER
Each blue dot represents a network node which are randomly is calculated based on the number of the package that were
and evenly distributed across the entire Purdue campus (Fig. markedascorruptedandPMRarecalculatedbasedonnumber

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     |     |     | 12  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Fig.18. MapofthenetworkdeploymentonPurduecampuswith13nodes.Thereddotrepresentsthecenternode(CN),thenetworknodesarerepresented
asbluedots,thebluesquarerepresentsthenodejunction(Node#12and#13)andthegreendotsrepresentsthereceiver.
of missed packages: However, from the observation based on the results from Fig.
19,althoughbothofthePMRandPERdidtrendtoincreaseas
|     |     |       | (cid:80)   | #ERROR |     |     |                                                       |     |     |     |     |     |     |
| --- | --- | ----- | ---------- | ------ | --- | --- | ----------------------------------------------------- | --- | --- | --- | --- | --- | --- |
|     |     |       |            |        | i   |     | numberofhopsincreased,theseeffectsareminimalcomparing |     |     |     |     |     |     |
|     |     | PER i | = (cid:80) |        |     |     | (7)                                                   |     |     |     |     |     |     |
#EXPECTED
|     |     |     |     |     | i   |     | with the   | PDR. Furthermore, |            | node | 12 and    | 13    | showed much |
| --- | --- | --- | --- | --- | --- | --- | ---------- | ----------------- | ---------- | ---- | --------- | ----- | ----------- |
|     |     |     |     |     |     |     | higher PER | (> 4%),           | we suspect |      | that this | might | be due to   |
(cid:80) #EXPECTED − (cid:80) #RECEIVED higher interference in the sub-GHz ISM band since both of
|     |     |     |          | i   |     |     | i   |     |     |     |     |     |     |
| --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| PMR | i = |     | (cid:80) |     |     |     | (8) |     |     |     |     |     |     |
#EXPECTED those two nodes were located in one of the most populated
i
|     |     |     |     |     |     |     | areas on | campus. On the | otherhand, |     | the LoRaWAN |     | reference |
| --- | --- | --- | --- | --- | --- | --- | -------- | -------------- | ---------- | --- | ----------- | --- | --------- |
Fig.19showstheend-to-endPDR,PMRandPERbasedon
|            |                |           |            |              |              |              | node 13*      | shows a very       | low PDR    | (51.5%)  |       | and very | high PER     |
| ---------- | -------------- | --------- | ---------- | ------------ | ------------ | ------------ | ------------- | ------------------ | ---------- | -------- | ----- | -------- | ------------ |
| the total  | expected       | number    | of         | packages     | and received | packages     |               |                    |            |          |       |          |              |
|            |                |           |            |              |              |              | and PMR,      | when compared      | to         | our mesh | node  | deployed | at the       |
| for all    | 13 nodes       | including |            | the SF12     | reference,   | where        | the           |                    |            |          |       |          |              |
|            |                |           |            |              |              |              | same location | (node 12).         | This       | confirms | that  | our      | mesh is able |
| blue bars  | represent      | all       | nodes      | in the mesh  | network,     |              | and the       |                    |            |          |       |          |              |
|            |                |           |            |              |              |              | to provide    | better quality     | of service |          | which | further  | supports our |
| orange     | bar represents |           | the SF12   | reference.   | Over         | the          | entire        |                    |            |          |       |          |              |
|            |                |           |            |              |              |              | purposed      | network structure. |            |          |       |          |              |
| deployment | period         | of        | two weeks, | the proposed |              | mesh network |               |                    |            |          |       |          |              |
achievesmorethan96%PDRexceptfornode12andnode13
|           |     |          |          |           |       |              |     |     | V. LIMITATIONS |     |     |     |     |
| --------- | --- | -------- | -------- | --------- | ----- | ------------ | --- | --- | -------------- | --- | --- | --- | --- |
| comparing | to  | 51.5% of | the SF12 | reference | node. | In addition, |     |     |                |     |     |     |     |
from Fig. 19 (b) and (c), both the PMR and PER for all As Ochoa et al. [22] point out, the energy consumption
nodes are significantly lower than the SF12 reference node. of LoRa mesh nodes can be further optimized by exploiting
Thisconfirmsthattheproposednetworkprovidesmuchbetter different radio configurations and the network topology (e.g.,
quality of service particularly for large area networks. Where the number of hops, the network density, the cell coverage).
higherspreadingfactorsarenecessaryfortransitionalstarnet- Forsparsenetworks,higherSFisnecessaryalongwithhigher
worktocoversuchasintheALOHAprotocolinLoRaWAN’s transmittedpower.TheAdaptiveLoRaLinkinourimplemen-
approach, it is worth noticing that the PMR increases as the tationdidnotincludethefunctionalitytochangethespreading
number of hops increases, this is expected since the time factor as the network topology in our deployment did not
floodingwill degradeasthe numberofhops increases.Imper- change over time. One aspect of our future work is to include
fect time synchronization will cause time slot mismatch and such adaptivity in our implementation.
therefore results in either missed packages (TX/RX window Another important limitation of the network occurs during
miss match) or package collision (TXs windows miss match). the flooding for the TDMA scheduling. In our current con-

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     | 13  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(a)
(b)
(c)
Fig.19. (a)PacketDeliveryRate(PDR),(b)PackageErrorRate(PER),(c)PackageMissRate(PMR)ofthetwoweekson-campusdeployment.Bluebars
representnode1to13acrossthenetwork.OrangebarrepresentstheSF12LoRaWANreferencefromnode6,9and13respectively
figuration, one TDMA schedule table for the entire network basedontheroutingpath.OnlythenecessaryTDMAschedule
is flooded to each node for the simplicity of the design. will be flooded to each multi-hop path in the network. This
However, there are two inherent problems with this approach. approach will significantly reduce the overhead time during
First, flooding the entire table requires transmitting multiple the setup phase without sacrificing the network performance.
| LoRa packages | throughout      | the entire            | network. Not   | only is  |             |           |                  |                   |               |     |
| ------------- | --------------- | --------------------- | -------------- | -------- | ----------- | --------- | ---------------- | ----------------- | ------------- | --- |
|               |                 |                       |                |          | While       | LoRaWAN   | allows for       | AES 128-bit       | encryption,   | in  |
| this approach | inefficient,    | but it also increases | the overhead   |          |             |           |                  |                   |               |     |
|               |                 |                       |                |          | the current | phase     | of our work,     | no encryption     | mechanisms    |     |
| for the setup | phase. Second,  | due to                | the limitation | of the   |             |           |                  |                   |               |     |
|               |                 |                       |                |          | have been   | deployed. | While we         | plan on deploying | AES-128       |     |
| maximum       | data package    | (255 bytes at         | SF7) of LoRa,  | the      |             |           |                  |                   |               |     |
|               |                 |                       |                |          | encryption  | in future | LoRaWAN          | deployments,      | a caveat      | of  |
| maximum       | number of nodes | in the network        | will be        | limited. |             |           |                  |                   |               |     |
|               |                 |                       |                |          | introducing | secure    | network channels | will be           | the reduction | of  |
Although,thislimitationcanbepatchedwithfloodingmultiple
theavailablepayloadsize,whichmayfurtherlimitthenumber
scheduletablesthroughoutthenetwork,thisapproachwillstill
ofsupportablenodesinasub-network.Thus,wewilllookinto
beinefficientandwillsignificantlyimpacttheoverheadduring
deployinglightweightencryptionmechanismsforIoTdevices,
| the setup      | phase. For our | future work, | instead of flooding | a      |         |            |                  |       |             |       |
| -------------- | -------------- | ------------ | ------------------- | ------ | ------- | ---------- | ---------------- | ----- | ----------- | ----- |
|                |                |              |                     |        | such as | ACES [32], | [33].            |       |             |       |
| entire network | table to every | node, we     | will divide the     | table, |         |            |                  |       |             |       |
|                |                |              |                     |        | As of   | the sensor | data management, | there | are several | other |

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     |     |     |     | 14  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Fig.20. TDMAscheduleofthecampusdeployednetwork,eachHopisclearlymarked.Path1to3correspondstothepathfromFig.18.Thetotallength
representsthetotaloverheadofthecorrespondingpath.
|     |     |     |     |     |     |     | consumption,     |     | we designed         | and | manufactured |          | our           | own sensor |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | ------------------- | --- | ------------ | -------- | ------------- | ---------- |
|     |     |     |     |     |     |     | node integrating |     | a micro-controller, |     |              | wireless | communication |            |
interfaces,andahybridnetworkwithshort(2.4GHz)andlong-
|     |     |     |     |     |     |     | range (915MHz)    |            | communication |           | links.            |      |             |            |
| --- | --- | --- | --- | --- | --- | --- | ----------------- | ---------- | ------------- | --------- | ----------------- | ---- | ----------- | ---------- |
|     |     |     |     |     |     |     | With              | our hybrid | mesh          | network,  | we                | have | shown       | a signif-  |
|     |     |     |     |     |     |     | icant improvement |            | in            | both      | power consumption |      |             | as well as |
|     |     |     |     |     |     |     | communication     |            | range while   | comparing |                   | with | traditional | single     |
hopnetworklikeLoRaWAN.Inaddition,full-scalereal-world
|     |     |     |     |     |     |     | experiments | on            | both Purdue |         | Campus      | and agricultural |            | farms    |
| --- | --- | --- | --- | --- | --- | --- | ----------- | ------------- | ----------- | ------- | ----------- | ---------------- | ---------- | -------- |
|     |     |     |     |     |     |     | with more   | than          | 20 nodes    | further | suggested   |                  | that the   | proposed |
|     |     |     |     |     |     |     | network     | significantly | improves    |         | the quality |                  | of service | while    |
maintainlong-termstability.Weprovideseveralareasoffuture
Fig.21. DeploymentatPurduecampus.(a)node#7installedonastreetlamp work motivated by our design and experiments on these large
post(b)nodejunctionconsistingnode12and13nexttoacampusbuilding scale IoT testbeds, including sophisticated anomaly detection,
|     |     |     |     |     |     |     | on-device | computation, |     | and network |     | synchronization. |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------- | ------------ | --- | ----------- | --- | ---------------- | --- | --- |
challengesaboutnetworklatencyanddataanalytics,whichwe
| have more | thorough | discussion |     | in [5] |     |     |     |     | ACKNOWLEDGMENT |     |     |     |     |     |
| --------- | -------- | ---------- | --- | ------ | --- | --- | --- | --- | -------------- | --- | --- | --- | --- | --- |
Theworkdescribedinthispaperispartofaprojectfunded
|            |                 | VI. | CONCLUSION |              |              |       |         |            |           |            |            |         |             |        |
| ---------- | --------------- | --- | ---------- | ------------ | ------------ | ----- | ------- | ---------- | --------- | ---------- | ---------- | ------- | ----------- | ------ |
|            |                 |     |            |              |              |       | through | the Wabash | Heartland |            | Innovation | Network |             | (WHIN) |
|            |                 |     |            |              |              |       | and the | SMART      | Film      | consortium | at         | Purdue  | University. |        |
| The recent | advancement     |     | of         | the Internet | of Things    | (IoT) |         |            |           |            |            |         |             |        |
| enables    | the possibility |     | of data    | collection   | from diverse | en-   |         |            |           |            |            |         |             |        |
vironments using IoT devices. However, despite the rapid REFERENCES
| advancement | of  | low-power | communication |     | technologies, | the |     |     |     |     |     |     |     |     |
| ----------- | --- | --------- | ------------- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
deployment of IoT network still faces many challenges. In [1] S. Chaterji, N. DeLay, J. Evans, N. Mosier, B. Engel, D. Buckmaster,
|     |     |     |     |     |     |     | and | R. Chandra, | “Artificial | intelligence | for | digital | agriculture | at scale: |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | ----------- | ------------ | --- | ------- | ----------- | --------- |
particular, large-scale WSN such as digital agriculture and Techniques,policies,andchallenges,”arXivpreprintarXiv:2001.09786,
| smart and | connected     |     | cities | remains | a major challenge |           | in 2020.         |                 |        |           |            |                           |           |           |
| --------- | ------------- | --- | ------ | ------- | ----------------- | --------- | ---------------- | --------------- | ------ | --------- | ---------- | ------------------------- | --------- | --------- |
|           |               |     |        |         |                   |           | [2] K. Matthews. |                 | (2019, | Nov.)     | 5 iot use  | cases                     | that will | shape the |
| terms of  | communication |     | range, | quality | of service        | and power |                  |                 |        |           |            |                           |           |           |
|           |               |     |        |         |                   |           | future           | of agriculture. |        | [Online]. | Available: | https://ubidots.com/blog/ |           |           |
consumption.
agriculture-smart-farming/
| This paper | presents |             | the design | of a          | hybrid LPWAN       | mesh |                      |           |         |       |                     |     |              |           |
| ---------- | -------- | ----------- | ---------- | ------------- | ------------------ | ---- | -------------------- | --------- | ------- | ----- | ------------------- | --- | ------------ | --------- |
|            |          |             |            |               |                    |      | [3] M. Aleksandrova. |           | (2018,  | Jun.) | Iot in agriculture: |     | 5 technology | use       |
|            |          |             |            |               |                    |      | cases                | for smart | farming | (and  | 4 challenges        | to  | consider).   | [Online]. |
| network    | for IoT  | application |            | that delivers | several-kilometers |      |                      |           |         |       |                     |     |              |           |
Available:https://easternpeak.com/blog/
| with only | low-power |     | nodes | while provides | excellent | QoS. |     |     |     |     |     |     |     |     |
| --------- | --------- | --- | ----- | -------------- | --------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
[4] S.Chaterji,P.Naghizadeh,M.A.Alam,S.Bagchi,M.Chiang,D.Cor-
Our work addresses the development of large-scale WSN that man, B. Henz, S. Jana, N. Li, S. Mou et al., “Resilient cyberphysical
is suitable for distinct application areas with real world de- systems and their application drivers: A technology roadmap,” arXiv
preprintarXiv:2001.00090,2019.
| ployments. | To enable | the | data | collection | with varying | sensors |     |     |     |     |     |     |     |     |
| ---------- | --------- | --- | ---- | ---------- | ------------ | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
[5] X.JiangandH.Zhang.(2020,Apr.)Technicalreport.[Online].Avail-
as well as to support wide area coverage with low energy able:https://lladzhang.github.io/heng.github.io/Technical report.pdf

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     |     |     | 15  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
[6] K.Mikhaylov,J.Petaejaejaervi,andT.Haenninen,“Analysisofcapacity IEEE/IFIP International Conference on Dependable Systems and Net-
andscalabilityoftheloralowpowerwideareanetworktechnology,”in works(DSN). IEEE,2019,pp.234–246.
European Wireless 2016; 22th European Wireless Conference. VDE, [33] A.A.Clements,N.S.Almakhdhub,S.Bagchi,andM.Payer,“ACES:
2016,pp.1–6. Automatic compartments for embedded systems,” in 27th {USENIX}
[7] (2017, Feb.) M2m and iot redefined through cost effective and energy SecuritySymposium(USENIXSecurity18),2018,pp.65–82.
| optimized                                        | connectivity. |         | SIGFOX. | [Online].      | Available: |                    | https://www. |     |     |     |     |     |     |
| ------------------------------------------------ | ------------- | ------- | ------- | -------------- | ---------- | ------------------ | ------------ | --- | --- | --- | --- | --- | --- |
| sigfox.com/sites/default/files/1701-SIGFOX-White |               |         |         |                |            | Paper Security.pdf |              |     |     |     |     |     |     |
| [8] L. Alliance.                                 |               | What is | lorawan | specification. |            | [Online].          | Available:   |     |     |     |     |     |     |
https://lora-alliance.org/about-lorawan
| [9] “Lte | evolution | for iot    | connectivity,”                         |     | White Paper, | Nokia, | Nov. |     |               |     |                   |     |               |
| -------- | --------- | ---------- | -------------------------------------- | --- | ------------ | ------ | ---- | --- | ------------- | --- | ----------------- | --- | ------------- |
| 2016.    | [Online]. | Available: | https://www.open-ecosystem.org/assets/ |     |              |        |      |     |               |     |                   |     |               |
|          |           |            |                                        |     |              |        |      |     | Xiaofan Jiang | is  | a Ph.D. Candidate |     | at the School |
lte-evolution-iot-connectivity
|                    |     |           |        |                 |     |      |             |     | of Electrical | and | Computer | Engineering, | Purdue |
| ------------------ | --- | --------- | ------ | --------------- | --- | ---- | ----------- | --- | ------------- | --- | -------- | ------------ | ------ |
| [10] O. Khutsoane, |     | B. Isong, | and A. | M. Abu-Mahfouz, |     | “Iot | devices and |     |               |     |          |              |        |
applicationsbasedonlora/lorawan,”inIECON2017-43rdAnnualCon- UniversityinWestLafayette,Indiana.Heisadvised
ference of the IEEE Industrial Electronics Society. IEEE, 2017, pp. by Dimitrios Peroulis. He received the B.S. degree
fromPurdueUniversityin2015.Hisresearchinter-
6107–6112.
|     |     |     |     |     |     |     |     |     | ests include | design | and implementation |     | of various |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------ | ------ | ------------------ | --- | ---------- |
[11] T.Bouguera,J.-F.Diouris,J.-J.Chaillout,R.Jaouadi,andG.Andrieux,
|         |             |     |           |        |             |     |              |     | embedded | systems, | wireless | sensor | networks and |
| ------- | ----------- | --- | --------- | ------ | ----------- | --- | ------------ | --- | -------- | -------- | -------- | ------ | ------------ |
| “Energy | consumption |     | model for | sensor | nodes based | on  | lora and lo- |     |          |          |          |        |              |
rawan,”Sensors,vol.18,no.7,p.2104,2018. IoTdevicesforgeneralandindustryapplications.
| [12] “SX1261/2 | Long | Range, | Low Power, | sub-GHz |     | RF Transceiver | data |     |     |     |     |     |     |
| -------------- | ---- | ------ | ---------- | ------- | --- | -------------- | ---- | --- | --- | --- | --- | --- | --- |
sheet,”Semtech,Camarillo,CA,USA.
| [13] D. Zorbas, | K.  | Abdelfadeel, | P. Kotzanikolaou, |     | and         | D. Pesch, | “Ts-lora: |     |     |     |     |     |     |
| --------------- | --- | ------------ | ----------------- | --- | ----------- | --------- | --------- | --- | --- | --- | --- | --- | --- |
| Time-slotted    |     | lorawan for  | the industrial    |     | internet of | things,”  | Computer  |     |     |     |     |     |     |
Communications,vol.153,pp.1–10,2020.
| [14] F. Adelantado, |        | X. Vilajosana, | P.             | Tuset-Peiro, | B.         | Martinez,    | J. Melia- |     |     |     |     |     |     |
| ------------------- | ------ | -------------- | -------------- | ------------ | ---------- | ------------ | --------- | --- | --- | --- | --- | --- | --- |
| Segui,              | and T. | Watteyne,      | “Understanding |              | the limits | of lorawan,” | IEEE      |     |     |     |     |     |     |
Communicationsmagazine,vol.55,no.9,pp.34–40,2017.
|     |     |     |     |     |     |     |     |     | Heng Zhang | is a | Ph.D. Student | at  | the School of |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ---- | ------------- | --- | ------------- |
[15] N.VarsierandJ.Schwoerer,“Capacitylimitsoflorawantechnologyfor Electrical and Computer Engineering, Purdue Uni-
smartmeteringapplications,”in2017IEEEInternationalConferenceon versity West Lafayette, Indiana. He is advised by
| Communications(ICC). |     |     | IEEE,2017,pp.1–6. |     |     |     |     |     |                 |     |          |          |             |
| -------------------- | --- | --- | ----------------- | --- | --- | --- | --- | --- | --------------- | --- | -------- | -------- | ----------- |
|                      |     |     |                   |     |     |     |     |     | Saurabh Bagchi. | He  | received | the B.S. | degree from |
[16] R.Piyare,A.L.Murphy,M.Magno,andL.Benini,“On-demandtdma
ShanghaiJiaoTongUniversityin2016.Hisresearch
forenergyefficientdatacollectionwithloraandwake-upreceiver,”in
|     |     |     |     |     |     |     |     |     | interests include | edge | computing, | mobile | sensing, |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ----------------- | ---- | ---------- | ------ | -------- |
201814thInternationalConferenceonWirelessandMobileComputing, wearableresilience,andIoTnetworking.
| NetworkingandCommunications(WiMob). |             |          |                 |     | IEEE,2018,pp.1–4. |         |             |     |     |     |     |     |     |
| ----------------------------------- | ----------- | -------- | --------------- | --- | ----------------- | ------- | ----------- | --- | --- | --- | --- | --- | --- |
| [17] B. Reynders,                   |             | Q. Wang, | P. Tuset-Peiro, |     | X. Vilajosana,    | and     | S. Pollin,  |     |     |     |     |     |     |
| “Improving                          | reliability |          | and scalability | of  | lorawans          | through | lightweight |     |     |     |     |     |     |
scheduling,”IEEEInternetofThingsJournal,vol.5,no.3,pp.1830–
1842,2018.
[18] C.-H.Liao,G.Zhu,D.Kuwabara,M.Suzuki,andH.Morikawa,“Multi-
|          |          |         |               |     |                | IEEE | Access, |     |     |     |     |     |     |
| -------- | -------- | ------- | ------------- | --- | -------------- | ---- | ------- | --- | --- | --- | --- | --- | --- |
| hop lora | networks | enabled | by concurrent |     | transmission,” |      |         |     |     |     |     |     |     |
vol.5,pp.21430–21446,2017.
[19] C.Ebi,F.Schaltegger,A.Ru¨st,andF.Blumensaat,“Synchronouslora
meshnetworktomonitorprocessesinundergroundinfrastructure,”IEEE Edgardo Barsallo Yi is a Ph.D. Candidate at the
| access,2019. |     |     |     |     |     |     |     |     | Computer | Science | Department, | Purdue | University. |
| ------------ | --- | --- | --- | --- | --- | --- | --- | --- | -------- | ------- | ----------- | ------ | ----------- |
[20] N. A. Pantazis, D. J. Vergados, D. D. Vergados, and C. Douligeris, HeisadvisedbySaurabhBagchi.Beforehejoined
“Energyefficiencyinwirelesssensornetworksusingsleepmodetdma Purdue,heworkedasasoftwareengineerandasoft-
scheduling,”AdHocNetworks,vol.7,no.2,pp.322–343,2009. warearchitectattheIndraSoftwareLabs,Panama.
[21] C.L.Hedrick,“Routinginformationprotocol,”1988. He holds a Master in Software Engineering from
[22] M. N. Ochoa, A. Guizar, M. Maman, and A. Duda, “Evaluating lora UPSAM (Spain) and a B.S. in Computer Systems
energyefficiencyforadaptivenetworks:Fromstartomeshtopologies,” from UTP, Panama. His research interests include
2017 IEEE 13th International Conference on Wireless and Mobile databases, distributed systems, mobile computing,
in
Computing, Networking and Communications (WiMob). IEEE, 2017, andwearableresilience.
pp.1–8.
| [23] (2007, | Jul.) Ant | message | protocol | and usage. | Dynastream |     | Innovations |     |     |     |     |     |     |
| ----------- | --------- | ------- | -------- | ---------- | ---------- | --- | ----------- | --- | --- | --- | --- | --- | --- |
Inc.[Online].Available:https://www.sparkfun.com/datasheets/Wireless/
Nordic/ANT-UserGuide.pdf
| [24] X. Jiang, | J.  | F. Waimin, | H. Jiang, | C.  | Mousoulis, | N. Raghunathan, |     |     |     |     |     |     |     |
| -------------- | --- | ---------- | --------- | --- | ---------- | --------------- | --- | --- | --- | --- | --- | --- | --- |
R.Rahimi,andD.Peroulis,“Wirelesssensornetworkutilizingflexible
| nitratesensors |     | for smart | farming,” | in IEEE | SENSORS | 2019. | IEEE, |     |     |     |     |     |     |
| -------------- | --- | --------- | --------- | ------- | ------- | ----- | ----- | --- | --- | --- | --- | --- | --- |
NithinRaghunathanreceivedhisPh.Dinelectrical
2019.
engineeringfromPurdueUniversity,WestLafayette,
[25] (2019)Huwomoibilty.[Online].Available:http://www.huwomo.com/ IN, USA, in 2014. His dissertation focused on
[26] (2019) nrf52832. [Online]. Available: https://www.nordicsemi.com/ thedevelopmentonmicro-machinedg-switchesfor
Products/Low-power-short-range-wireless/nRF52832
|     |     |     |     |     |     |     |     |     | impact applications |     | typically | in the | ranges of 100 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------------------- | --- | --------- | ------ | ------------- |
[27] (2018)semtech.[Online].Available:https://www.semtech.com/products/
|     |     |     |     |     |     |     |     |     | 60,000 gs. | He worked | as Post-Doctoral |     | Research |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --------- | ---------------- | --- | -------- |
wireless-rf/lora-transceivers
|     |     |     |     |     |     |     |     |     | associate | from 2014 | to 2015 | and was | involved in |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | --------- | ------- | ------- | ----------- |
[28] L.Alliance,“Atechnicaloverviewofloraandlorawan,”WhitePaper, the development of wireless radiation sensors for
| 2015. |     |     |     |     |     |     |     |     | dosimetry | applications. | He is | currently | a Staff Sci- |
| ----- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | ------------- | ----- | --------- | ------------ |
[29] (2019) nrf52832. [Online]. Available: https://www.keysight.com/en/ entist at the Birck Nanotechnology Center at Pur-
pd-1842303-pn-N6705B/dc-power-analyzer-modular-600-w-4-slots
dueUniversity.HeiscurrentlyworkingonWabash
[30] (2019)Metergroupech2o5tesoilmoisturesensor.[Online].Available:
|     |     |     |     |     |     |     |     | Heartland innovation | Network (WHIN) | on  | the development |     | of IoT sensors |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------- | -------------- | --- | --------------- | --- | -------------- |
https://metos.at/portfolio/decagon-5te-soil-moisture-sensor/ and network for Industrial and agricultural operations. His other interests
[31] (2019) Semtech sx1272dvk1cas development kit, sx1272, 915 mhz. include novel MEMS inertial devices, development of new microfabrication
[Online]. Available: https://www.semtech.com/products/wireless-rf/ techniques, wireless and flexible sensors and sensors for Lyophilization and
lora-transceivers/sx1272dvk1cas
asepticprocessingandalsosensorsforindustrialandharshenvironments.
[32] N.S.Almakhdhub,A.A.Clements,M.Payer,andS.Bagchi,“Benchiot:
Asecuritybenchmarkfortheinternetofthings,”in201949thAnnual

| IEEEINTERNETOFTHINGSJOURNAL,APRIL2020 |     |     |     |     |     |     |     |     |     |     | 16  |
| ------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Charilaos Mousoulis received the Ph.D. degree in Ali Shakouri is the Mary Jo and Robert L. Kirk
Electrical and Computer Engineering from Purdue DirectoroftheBirckNanotechnologyCenteratPur-
University,WestLafayette,IN,USAin2012.Since dueUniversity.Hereceivedhisdiplomed’Ingenieur
2014heisaSeniorResearchScientistattheSchool in 1990 from Telecom ParisTech, France and his
of Electrical and Computer Engineering, Purdue Ph.D.in1995fromCaliforniaInstituteofTechnol-
University, West Lafayette. He was previously a ogy in Pasadena, CA. His group studies nanoscale
Postdoctoral Research Associate at the School of heattransportandelectrothermalenergyconversion
Biomedical Engineering, Purdue University, West to improve electronic and optoelectronic devices.
Lafayette. His research interests include microsys- Theyhavealsodevelopednovelimagingtechniques
temsforbiomedicalapplications,silicon-basedradi- to obtain thermal maps with sub diffraction-limit
ationsensorsforoccupationaldosimetry,sensorsfor spatial resolution and 800ps time resolution. He is
food safety, flexible hybrid electronics, and IoT-based sensors for precision applying similar methods to enable real-time monitoring of functional film
agricultureandadvancedmanufacturing. continuous manufacturing. He is leading SMART industry consortium to
manufacturelow-costinternetofthing(IoT)devicesandsensornetwork.As
apartofWabashHeartlandInnovationNetwork(WHIN),theyaredeveloping
communityIoTtestbedsinadvancedmanufacturingandhightechagriculture.
|     |     |        |          |     |     |     |     | Saurabh Bagchi | is a Professor       | in  | the School of |
| --- | --- | ------ | -------- | --- | --- | --- | --- | -------------- | -------------------- | --- | ------------- |
|     |     |        |          |     |     |     |     | Electrical and | Computer Engineering |     | and the De-   |
|     |     | Somali | Chaterji |     |     |     |     |                |                      |     |               |
is an Assistant Professor in the partmentofComputerScienceatPurdueUniversity
|     |     | Department |     | of Agricultural |     | and Biological | Engi- |     |     |     |     |
| --- | --- | ---------- | --- | --------------- | --- | -------------- | ----- | --- | --- | --- | --- |
inWestLafayette,Indiana.HeisthefoundingDirec-
neeringatPurdueUniversity,whereshespecializes
|     |     |     |            |            |     |             |            | tor of a university-wide | resilience | center | at Purdue |
| --- | --- | --- | ---------- | ---------- | --- | ----------- | ---------- | ------------------------ | ---------- | ------ | --------- |
|     |     | in  | developing | algorithms | and | statistical | models for |                          |            |        |           |
calledCRISP(2017-present).Hewaselectedtothe
genome engineering, precision health, and digital IEEEComputerSocietyBoardofGovernorsforthe
|     |     | agriculture. |             | Dr. Chaterji | got    | her PhD     | in Biomed- |              |                |          |             |
| --- | --- | ------------ | ----------- | ------------ | ------ | ----------- | ---------- | ------------ | -------------- | -------- | ----------- |
|     |     |              |             |              |        |             |            | 2017-19 term | and re-elected | in 2019. | He is a co- |
|     |     | ical         | Engineering | from         | Purdue | University, | winning    |              |                |          |             |
leadontheWHIN-SMARTcenteratPurdueforIoT
|     |     | the | Chorafas | International | Award, | College | of En- |     |     |     |     |
| --- | --- | --- | -------- | ------------- | ------ | ------- | ------ | --- | --- | --- | --- |
anddataanalytics.Saurabh’sresearchinterestisin
|     |     | gineering |     | Best Dissertation |     | Award, and | the Future |                      |                 |     |             |
| --- | --- | --------- | --- | ----------------- | --- | ---------- | ---------- | -------------------- | --------------- | --- | ----------- |
|     |     |           |     |                   |     |            |            | dependable computing | and distributed |     | systems. He |
FacultyFellowshipAward.ShedidherPost-doctoral isproudestofthe21PhDstudentsand50Mastersthesisstudentswhohave
|     |     | Fellowship |     | at the University |     | of Texas | at Austin in |     |     |     |     |
| --- | --- | ---------- | --- | ----------------- | --- | -------- | ------------ | --- | --- | --- | --- |
graduatedfromhisresearchgroupandwhoareinvariousstagesofbuilding
| the Department | of  | Biomedical | Engineering, |     | where her | work was | supported |     |     |     |     |
| -------------- | --- | ---------- | ------------ | --- | --------- | -------- | --------- | --- | --- | --- | --- |
wonderfulcareersinindustryoracademia.Inhisgroup,heandhisstudents
byanAmericanHeartAssociationaward.ShefollowedthisupwithaPost-
havewaytoomuchfunbuildingandbreakingrealsystems.
doctoralstintatPurdueComputerSciencewhenshegotherfirstNIHR01on
computationalmetagenomics.Dr.Chaterjiisatechnologycommercialization
| enthusiast | and has | been consulting |     | for the IC2 | Institute | at the | University of |     |     |     |     |
| ---------- | ------- | --------------- | --- | ----------- | --------- | ------ | ------------- | --- | --- | --- | --- |
TexasatAustin,sinceSpring2014.
DimitriosPeroulis(S99M04SM15F17)istheReilly
ProfessorandMichaelandKatherineBirckHeadof
theSchoolofElectricalandComputerEngineering
|     |     | at       | Purdue      | University.  | He received     | his       | PhD degree     |     |     |     |     |
| --- | --- | -------- | ----------- | ------------ | --------------- | --------- | -------------- | --- | --- | --- | --- |
|     |     | in       | Electrical  | Engineering  | from            | the       | University of  |     |     |     |     |
|     |     | Michigan |             | at Ann Arbor | in              | 2003. His | research in-   |     |     |     |     |
|     |     | terests  | are         | focused      | on the areas    | of        | reconfigurable |     |     |     |     |
|     |     | systems, | cold-plasma |              | RF electronics, |           | and wireless   |     |     |     |     |
sensors.Hehasbeenakeycontributorindeveloping
|                  |            | high            | quality | widely-tunable |                 | filters and | novel filter |     |     |     |     |
| ---------------- | ---------- | --------------- | ------- | -------------- | --------------- | ----------- | ------------ | --- | --- | --- | --- |
|                  |            | architectures   |         | based          | on miniaturized | high-Q      | cavity-      |     |     |     |     |
| based resonators | in         | the 1-100       | GHz     | range. He      | is currently    | leading     | research     |     |     |     |     |
| efforts in       | high-power | multifunctional |         | RF electronics |                 | based on    | cold-plasma  |     |     |     |     |
technologies.HereceivedtheNationalScienceFoundationCAREERaward
| in 2008.    | He is an        | IEEE Fellow    | and         | has co-authored |          | over 380  | journal and |     |     |     |     |
| ----------- | --------------- | -------------- | ----------- | --------------- | -------- | --------- | ----------- | --- | --- | --- | --- |
| conference  | papers.         | In 2019        | he received | the Tatsuo      | Itoh     | Award     | and in 2014 |     |     |     |     |
| he received | the Outstanding |                | Young       | Engineer        | Award    | both from | the IEEE    |     |     |     |     |
| Microwave   | Theory          | and Techniques |             | Society         | (MTT-S). | In 2012   | he received |     |     |     |     |
theOutstandingPaperAwardfromtheIEEEUltrasonics,Ferroelectrics,and
FrequencyControlSociety(Ferroelectricssection).Hisstudentshavereceived
numerousstudentpaperawardsandotherstudentresearch-basedscholarships.
| He has been | a Purdue | University | Faculty | Scholar | and | has also | received ten |     |     |     |     |
| ----------- | -------- | ---------- | ------- | ------- | --- | -------- | ------------ | --- | --- | --- | --- |
teachingawardsincludingthe2010HKNC.HolmesMacDonaldOutstanding
| Teaching | Award and | the 2010 | Charles | B. Murphy | award, | which | is Purdue |     |     |     |     |
| -------- | --------- | -------- | ------- | --------- | ------ | ----- | --------- | --- | --- | --- | --- |
University’shighestundergraduateteachinghonor.