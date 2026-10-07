> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> arXiv **2405.14740** - *Duty-cycle-efficient synchronization for slotted-Aloha LoRaWAN*.
> Source PDF deleted after conversion.
>
> Listed in `docs/research/BUDGET/01-literature.md` sync row 2 as **HELD**, no figure quoted.
> Synchronisation under the **1 % duty-cycle constraint**. Pairs with **LongShoT** (which is
> HELD-and-read: <2 us average sync error, drift <0.1 ppm, ~1 us per 300 m), the figure the
> project actually relies on. Sync is ~2 orders of magnitude better than needed; the real
> localisation limit is **velocity uncertainty**, not clock error.

A Duty-Cycle-Efficient Synchronization
Protocol for Slotted-Aloha in LoRaWAN
Amavi Dossa and El Mehdi Amhoud
College of Computing, Mohammed VI Polytechnic University (UM6P), Benguerir, Morocco,
emails: {amavi.dossa,elmehdi.amhoud}@um6p.ma
Abstract—InthecurrentcontextofmassiveIoT,thePure-Aloha With that in mind, we propose in this paper a protocol that
schemeusedinLoRaWANisreachingitslimit,andSlotted-Aloha tracks the synchronization state of end-devices based on their
is being considered as an alternative, as it offers twice Pure-
uplink packets arrival time. This allows the network server
Aloha’s packet success rate. It however requires synchronization
to detect the specific moment a device desynchronizes and
accross the nodes. In this paper, we propose a new slot structure
adaptedtodeviceswithlowqualityclock,andaduty-cycleefficient transmits, through the acknowledgement packet, the neces-
synchronization protocol for LoRaWAN class A devices with the sary information for its resynchronization. This minimizes the
lowestoverheadtodate.Wediscusstheconditionsofitsintegration downlink overhead and results in a duty cycle gain for the
intoLoRaWAN.Theexperimentalresultsconfirmthatitsucceeds
gateway, without requiring any additional hardware. This paper
in tracking each device’s synchronization state, identifying the
focuses on the synchronization aspect rather than a slotted-
exact moment they desynchronize and resynchronizing them. The
proposed protocol is also proven to be more duty-cycle efficient Aloha implementation. Our contribution is twofold:
than existing fixed-rate synchronization solutions. • We introduce a two-guard-intervals variant of the existing
Index Terms—LoRaWAN, scalability, slotted-Aloha, synchro- slotstructure.Thisdesignallowsustodefinetheacceptable
nization, massive IoT, duty-cycle efficiency
boundsonend-devicesdrift,foragivenlengthoftheguard
intervals.
I. INTRODUCTION • We propose a monitoring and synchronization proto-
col on top of LoRaWAN that is able to identify any
Since its introduction almost a decade ago, the Long Range desynchronized devices and resynchronize them. We show
Wide Area Network (LoRaWAN) technology has met an un- that it requires only two additional bytes to encode the
precedented success among existing Low Power Wide Area synchronization-related information. To the best of our
Networks (LPWAN) technologies. Its low cost, low power and knowledge,thisistheLoRaWANsynchronizationprotocol
ability to operate over noisy channels made it reach several with the lowest overhead.
markets and application sectors like smart cities, smart grids
The rest of this paper is organized as follows: Section II states
and metering, agriculture monitoring, wireless sensor networks
the problem after a short LoRaWAN overview; Section III
and localization [1]–[5]. With the increasing number of nodes,
introduces the proposed synchronization protocol and Section
LoRaWAN enters the so-called Massive IoT era. Therefore,
IVdescribeshowitintegratesintotheexistingLoRaWANstack;
scalability is currently one of the biggest research challenges
SectionVpresentsanddiscussestheexperimentalresultsofour
[6].
synchronizationsolution;SectionVIconcludesthepaperandset
To cope with the previous challenges, propositions include forth our perspectives.
the use of slotted-Aloha as an alternative to pure-Aloha which
LoRaWAN currently uses. It requires all the nodes to be syn-
II. LORAWANOVERVIEWANDPROBLEMSTATEMENT
chronized.LoRaWANclassBdevicesregularlyreceivebeacons LoRa (Long Range) is a proprietary modulation technique
from the gateway that can be used to synchronize. Similarly, developed by Semtech Corporation. It is based on the Chirp
class C devices are listening to the channel almost all the Spread Spectrum (CSS) technique, and operates in the sub-
time, hence can be synchronized using broadcast signals. The Gigahertz frequency bands. LoRaWAN, on the other hand, is
challenge resides with class A devices that do not share any a communication protocol built on top of LoRa, and designed
synchronization signals. Several works have targeted synchro- specifically for wide-area networks with low-power consump-
nization mechanisms in wireless sensor networks over the past tion, low datarate IoT devices. It was developed by the LoRa
years [7] [8], but very few were dedicated to LoRaWAN, [9]– Alliance[12].Itemploysastarofstarsarchitecture,asdepicted
[11]. Nonetheless, they didn’t take into account the duty cycle in Fig. 1: End-devices are served by one or more gateways
limitation on LoRaWAN gateways, whilst this is a key factor which, in turn, communicates with a network server. The end-
that requires optimization for a wide slotted-Aloha adoption in devices transmit their frames to the gateways using the radio
LoRaWAN. interface; the gateways forward those frames to the network
4202
yaM
32
]IN.sc[
1v04741.5042:viXra

|     |     |     |     |     |     |     |     | qualities | and this | operation | would | take | a huge | amount | of time; |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | -------- | --------- | ----- | ---- | ------ | ------ | -------- |
plus,itwillrequireanon-negligiblesoftwareoverheadtomatch
|     |     |     |     |     |     |     |     | each node | with     | its synchronization |     |     | rate. On | the other | hand, |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | -------- | ------------------- | --- | --- | -------- | --------- | ----- |
|     |     |     |     |     |     |     |     | choosing  | a single | synchronization     |     |     | rate for | all nodes | seems |
practical,butisnotoptimal:nodeswithbetterclockqualitywill
beresynchronizedmoreoftenthatrequired,addingunnecessary
|     |     |     |     |     |     |     |     | overhead,              | while     | those      | with worse |                | clock quality | will   | not be     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------------- | --------- | ---------- | ---------- | -------------- | ------------- | ------ | ---------- |
|     |     |     |     |     |     |     |     | resynchronized         |           | on time,   | leading    | to significant |               | drift, | hence slot |
|     |     |     |     |     |     |     |     | violation.             | Moreover, | a          | node’s     | drift is       | also subject  | to     | external   |
|     |     |     |     |     |     |     |     | conditions             | such      | as voltage | level      | and            | temperature.  |        | Hence, a   |
|     |     |     |     |     |     |     |     | static synchronization |           | becomes    |            | very limited   | facing        | the    | previous   |
challenges.
|     |     |     |     |     |     |     |     | In what     | follows, | we      | propose | a synchronization |     | protocol | that     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----------- | -------- | ------- | ------- | ----------------- | --- | -------- | -------- |
|     |     |     |     |     |     |     |     | dynamically | adapt    | to each | node    | by tracking       | its | drift    | in time. |
Fig.1. LoRaWANStarofStarstopology
|     |     |     |     |     |     |     |     | III. | DYNAMICSYNCHRONIZATIONPROTOCOLDESIGN |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | ------------------------------------ | --- | --- | --- | --- | --- | --- |
server through a back-haul link; the network server is in charge In this section, we describe the layout of the proposed
of sending the payload to the intended application server. synchronization protocol, starting by detailing the underlying
|            |         |      |           |             |        |       |     | slot structure. |     |     |     |     |     |     |     |
| ---------- | ------- | ---- | --------- | ----------- | ------ | ----- | --- | --------------- | --- | --- | --- | --- | --- | --- | --- |
| Similarly, | in case | of a | downlink, | the network | server | sends | the |                 |     |     |     |     |     |     |     |
frametoonegatewaythatforwardsittotheintendedend-device We consider a LoRaWAN gateway (GW) connected to a
through the radio interface. Additionally, three classes of end- network server (NS) and serving N class A end-devices (ED).
tk
devices are supported, corresponding to different power saving We note t ns (t) the local time of NS at a moment t and (t)
ed
policies: class B and C are respectively for deterministic and that of the k-th ED, k ={0,1,...,N−1}. Network servers run
|                 |     |          |             |      |        |       |       | on dedicated | hardware |     | with much | more | stable | clock | compared |
| --------------- | --- | -------- | ----------- | ---- | ------ | ----- | ----- | ------------ | -------- | --- | --------- | ---- | ------ | ----- | -------- |
| lowest downlink |     | latency, | but consume | more | power; | class | A, on |              |          |     |           |      |        |       |          |
the other hand, has the lowest power consumption profile, but to end-devices. So, for the remainder of this paper, we will
does has a non-deterministic downlink latency since the only consider the NS clock perfect. We also suppose that NS and
available downlink windows are after an uplink transmission the EDs share the same time origin. Thus, at any moment t, the
initiated by an end-device. time drift ∆t(k) of the k-th ED is given by Eq. (1).
Pure-Aloha is an access scheme that allows devices to trans- ∆t(k)(t)=t (t)−t(k)(t)
|     |     |     |     |     |     |     |     |     |     |     |     | ns  |     |     | (1) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
mit anytime without any form of coordination. Because of its ed
| simplicity, | it is | adapted | to resource-constrained |     |     | devices | and is |     |     |     |     |     |     |     |     |
| ----------- | ----- | ------- | ----------------------- | --- | --- | ------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
|∆t(k)(t)|≤∆
often adopted by low-power and low-complexity networks. It max (2)
| is however | limited | to  | only 18% | packet | success | rate when | the |       |                    |     |     |         |      |      |            |
| ---------- | ------- | --- | -------- | ------ | ------- | --------- | --- | ----- | ------------------ | --- | --- | ------- | ---- | ---- | ---------- |
|            |         |     |          |        |         |           |     | Given | a maximumtolerable |     |     | drift ∆ | , an | EDis | considered |
max
| number of | nodes | increases, | due | to collisions | [13]. | On the | other |     |     |     |     |     |     |     |     |
| --------- | ----- | ---------- | --- | ------------- | ----- | ------ | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
in-synciftheconditioninEq.(2)holds,andout-syncotherwise.
hand,slotted-Alohadoublesthepacketsuccessrate,butrequires
|     |     |     |     |     |     |     |     | If the NS | can track | a ED’s | drift | accross | time, | it can then | detect |
| --- | --- | --- | --- | --- | --- | --- | --- | --------- | --------- | ------ | ----- | ------- | ----- | ----------- | ------ |
the nodes to be synchronized. LoRaWAN was initially based theexactmomentitgoesout-syncandissuearesynchronization.
| on pure-Aloha |     | but, with | the increasing | number |     | of end-devices, |     |     |     |     |     |     |     |     |     |
| ------------- | --- | --------- | -------------- | ------ | --- | --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
slotted-Aloha is being seen as a good alternative. A. Slot Structure Design
LoRaWAN targets low-cost end-devices, that can have poor With slotted-Aloha, time is divided into slots of predefined
clock quality, leading to significant time drift. Hence, devices length and nodes can transmit only at the beginning of each
should be resynchronized on regular basis to avoid slot viola- slot.TheclassicslotconsistsofatransmissionintervalT r anda
tion. Existing synchronization solutions use the end of uplink confidenceintervalT :thedevice’stransmissionnormallystarts
b
T T
transmission as a common reference between an end-device at the beginning of the slot and lasts r ; b ensures that the
and the network server [9] [10]: the network server appends transmission ends within the slot duration even in case of clock
the timestamp of the end of uplink into the downlink sent drift. As depicted by Fig. 2, T can be seen as virtually made
b
back to the end-device; the latter will compare this value to of two guard intervals: a backward guard interval T b1 – that
the one it locally stored and use the difference to correct its prevents against drift towards the slot’s start – and a forward
clock drift. This however results in a greater downlink air-time, guardintervalT –thatpreventsagainstdrifttowardstheslot’s
b2
thus consumes more duty cycle. Consequently, the challenge end. Moreover, the propagation delay is neglected: uplink air-
resides in finding a synchronization rate that keeps the end- times range from hundreds of ms while the propagation delay
devices drift under a certain threshold, while minimizing the equals 50µs, assuming a line of sight and a typical LoRa
duty cycle overhead. Assessing each node’s clock quality to coverage of 15 km; it can then be neglected even in case of
set the synchronization rate accordingly is not practical: one multipath propagation. The slot is therefore made of the uplink
network could serve thousands of nodes with different clock air-time T and the confidence interval T .
|     |     |     |     |     |     |     |     |     | tx  |     |     |     | b   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

TABLEI
AIR-TIMEEQUATIONSSYMBOLSDESCRIPTION
|         |        |                                                |                                   |     |     |     |             |     | Symbols   |     | Parameters                  |     |         |     |     |
| ------- | ------ | ---------------------------------------------- | --------------------------------- | --- | --- | --- | ----------- | --- | --------- | --- | --------------------------- | --- | ------- | --- | --- |
|         |        |                                                |                                   |     |     |     |             |     | Tpacket   |     | Totalpacketair-time         |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | Tpreamble |     | Preambleduration            |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | Tpayload  |     | Payloadduration             |     |         |     |     |
|         | Fig.2. | Slotted-Aloha:Virtualdoubleconfidenceintervals |                                   |     |     |     |             |     |           |     |                             |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | Ts        |     | Symbolperiod                |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | npayload  |     | Numberofpayloadsymbols      |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | PL        |     | Payloadsize(inbytes)        |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | SF        |     | SpreadingFactor             |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | IH        |     | ImplicitHeaderflag          |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | DE        |     | Lowdatarateoptimizationflag |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | CRC       |     | CyclicRedundancyCheckflag   |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     | CR        |     | CodingRate                  |     |         |     |     |
|         |        | Fig.3.                                         | Apparentdrifteffectonslotposition |     |     |     |             |     |           |     |                             |     |         |     |     |
|         |        |                                                |                                   |     |     |     |             |     |           |     | T                           | =n  |         | ×T  | (9) |
|         |        |                                                |                                   |     |     |     |             |     |           |     | payload                     |     | payload | s   |     |
| Devices |        | – that                                         | are microcontroller-based         |     |     |     | – keep time | by  |           |     |                             |     |         |     |     |
countingperiodicpulsesgeneratedfromthesystemclock,which
frequency f is known. The clock however has frequency (cid:16) (cid:17)
|     |     | 0   |     |     |     |     |     |     | n    |     | = ceil | 8PL−4SF+28+16CRC−20IH |           |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | ------ | --------------------- | --------- | --- | --- |
|     |     |     |     |     |     |     |     |     | bits |     |        |                       | 4(SF−2DE) |     |     |
precision, depending on its quality [14]. The instantaneous (10)
|     |     |     |     |     |     |     |     |     | n   |     | =   | 8+max(n | (CR+4),0) |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | --------- | --- | --- |
frequency is given by Eq. (3). ∆f is a real number, so the payload bits
frequency can either increase or decrease. The guard intervals T b1 and T b2 represent unconsumed time
|     |     |     |     |     |     |     |     |     | slots,sotheyshouldbecalculatedasanacceptableratioofT |     |     |     |     |     | ,   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------------------------------------------------- | --- | --- | --- | --- | --- | --- |
tx
|           |       |            |        |               |         |           |        |         | based on           | the application. |     |            |          |     |     |
| --------- | ----- | ---------- | ------ | ------------- | ------- | --------- | ------ | ------- | ------------------ | ---------------- | --- | ---------- | -------- | --- | --- |
|           |       |            | f(t)=f |               | +∆f(t), |           |        |         |                    |                  |     |            |          |     |     |
|           |       |            |        | 0             |         |           |        | (3)     |                    |                  |     |            |          |     |     |
|           | ∆f(t) | being      | the    | instantaneous |         | frequency | drift. |         |                    |                  |     |            |          |     |     |
|           |       |            |        |               |         |           |        |         | B. Synchronization |                  | and | Monitoring | Protocol |     |     |
| Moreover, |       | relatively | to     | a device      | with    | an ideal  | clock  | running |                    |                  |     |            |          |     |     |
at f , another device running at f >f will be ahead in time Algorithm 1 Network Server
|       | 0       |     |         |      | 1   | 0       |                      |     |           |     |     |     |     |     |     |
| ----- | ------- | --- | ------- | ---- | --- | ------- | -------------------- | --- | --------- | --- | --- | --- | --- | --- | --- |
| while | another | one | running | at f | <f  | will be | late, as illustrated |     | receive() |     |     |     |     |     |     |
|       |         |     |         | 2    | 0   |         |                      |     | 1:        |     |     |     |     |     |     |
by Fig. 3. The maximum tolerated backward and forward drifts 2: arrival ← current_time() - ref
being respectively T and T , the frame in-sync condition can arrival ← arrival mod T_slot
|     |     |     | b1  | b2  |     |     |     |     | 3:  |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
be derived through Eq. (4). Moreover, Eq. (5) gives the in- 4: if out_sync() then
sync condition if the end of uplink transmission is used as a 5: remain ← T_slot - arrival
reference. Therefore, the NS can compute the k-th ED’s drift add_remain_to_ack()
6:
upon a frame reception, where T is the end of uplink 7: wait_for_rx_window()
Tx−ns
| transmission |              | expected          | by          | the NS | and      | T           | the moment   | the |                   |        |         |               |         |                          |      |
| ------------ | ------------ | ----------------- | ----------- | ------ | -------- | ----------- | ------------ | --- | ----------------- | ------ | ------- | ------------- | ------- | ------------------------ | ---- |
|              |              |                   |             |        |          | Tx−ed       |              |     | 8: transmit_ack() |        |         |               |         |                          |      |
| uplink       | transmission |                   | effectively |        | ends. If | an out-sync | is detected, |     |                   |        |         |               |         |                          |      |
| the          | device       | is resynchronized |             | using  | the      | algorithm   | described    | in  |                   |        |         |               |         |                          |      |
|              |              |                   |             |        |          |             |              |     | The core          | idea   | of our  | protocol      | lies in | a unique time reference, |      |
| the          | following    | subsection.       |             |        |          |             |              |     |                   |        |         |               |         |                          |      |
|              |              |                   |             |        |          |             |              |     | ref, stored       | at the | network | server        | and is  | used to synchronize      | all  |
|              |              |                   |             |        |          |             |              |     | the end-devices   |        | and     | later monitor | their   | synchronization          | from |
<∆t(k)(t)<T
−T the incoming packets arrival time. ref is set only once with
|     |     |     | b2  |     |     | b1  |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(t)−t(k)(t)<T the current time when the network server boots up, and it is
|     | =⇒  |     | −T b2 <t | ns  |     |     | b1  | (4) |     |     |     |     |     |     |     |
| --- | --- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ed
=⇒ t (t)−T <t(k)(t)<t (t)+T considered as the beginning of the very first slot. From there it
|     |     |     | ns  | b1  | ed  | ns  | b2  |     |         |        |            |             |         |           |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | ------ | ---------- | ----------- | ------- | --------- | --- |
|     |     |     |     |     |     |     |     |     | is easy | to get | the future | slots start | through | Eq. (11). |     |
<T(k)
|     |     | T Tx−ns | −T b1 |     | <T  | Tx−ns | +T b2 | (5) |     |     |     |     |     |     |     |
| --- | --- | ------- | ----- | --- | --- | ----- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
Tx−ed
Theuplinkair-timeT dependsonphysicallayerparameters slot_start[n]=ref +n×T_slot, n∈N∗ (11)
tx
| and | can be | calculated | from | Eq. | (6), [15]. | Table | I describes | the |     |     |     |     |     |     |     |
| --- | ------ | ---------- | ---- | --- | ---------- | ----- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
Atanytime,Eq.(12)givestherelativepositionintheongoing
| symbols | involved |     | in the equations. |     |     |     |     |     |     |     |     |     |     |     |     |
| ------- | -------- | --- | ----------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
slot–thatis,howmuchtimeelapsedsincethebeginningofthis
slot.Similarly,Eq.(13)givestheremainingtimebeforethenext
|     |     | T        | =T     |          | +T  |         |     | (6) |                                   |                     |     |     |     |             |      |
| --- | --- | -------- | ------ | -------- | --- | ------- | --- | --- | --------------------------------- | ------------------- | --- | --- | --- | ----------- | ---- |
|     |     |          | packet | preamble |     | payload |     |     | slot.                             |                     |     |     |     |             |      |
|     |     |          |        |          |     |         |     |     |                                   | position=(time−ref) |     |     |     | mod T_slot  | (12) |
|     |     | T        | =(n    |          |     | +4.25)T |     | (7) |                                   |                     |     |     |     |             |      |
|     |     | preamble |        | preamble |     |         | s   |     |                                   |                     |     |     |     |             |      |
|     |     |          |        |          |     |         |     |     | remaining_time=T_slot−((time−ref) |                     |     |     |     | mod T_slot) |      |
2SF
|     |     |     |     | T s = |     |     |     | (8) |     |     |     |     |     |     | (13) |
| --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- |
BW

Algorithm 2 end-device sync.Theremainingtimeisextractedandusedtoresynchronize
1: if !is_first_tx then the device. The elapsed time between the moment the network
2: is_first_tx ← 1 servercomputedtheremaining-timeandthemomentthedevice
3: slot_start ← current_time() received the ACK packet – equal to end - beg – is substracted
4: else fromremaining-time.Then,TheEDresynchronizesbyupdating
5: wait_for_next_slot() its slot start reference with remaining-time added to its current
6: transmit() local time. It can happen that the time elapsed is greater than
7: beg ← current_time() the remaining time. This scenario is handled in lines 16-18 by
8: wait_for_rx_window() the mean of a modulo operation. Additionally, the presence
9: get_ack() of remaining-time in the ACK packet can be checked by
10: end ← current_time() different means: for instance, the implementation used for the
11: if remain_in_ack() then experimentalresultssectionbelowassumedadownlinkwithno
12: remain ← get_remain_from_ack() MAC commands; so, checking the packet size was enough in
13: elapsed ← end - beg that case.
14: t ← remain - elapsed
15: if t<0 then
IV. PROTOCOLINTEGRATIONINTOLORAWAN
16: t ← t mod T_slot Withtheprotocolalreadyestablished,wenowdiscusshowit
17: slot_start ← current_time() + t integratesintotheLoRaWANstack.LoRaWANframestructure
includes a Frame Options field for sharing MAC commands
between end-devices and the network server. We use this field
to send the synchronization-related bytes, the remaining-time
The protocol is divided into two algorithms: one for the NS
forinstance.Itsvalueisbetween0–foraframereceivedexactly
and the other one for EDs. For an ED, the synchronization
at the end of the slot – and T – for a frame received at the
slot
consists in simply saving the beginning of a slot into a variable
exactbeginningofaslot.TableIIspecifiestheradioparameters
attherighttime,sothatitcanservetoidentifyfutureslotsstart
that gives the longest packet air-time: LoRa spreading factors
using Eq. (11). To keep the algorithms short, we substituted
rangesfrom5to12,thegreaterthespreadingfactorthemorethe
some portions with self-explanatory function names such as
signalisspreadintime;LoRadefinescodingrates1,2,3and4
current_time(), wait_for_next_slot(), or wait(). Those are just
correspondingresp.toeffectiverates 4, 4, 4 and 4;LoRaWAN
steps of the algorithms that can be simple sets of instructions 5 6 7 8
uses only 125 kHz, 250 kHz and 500 kHz bandwidth, the
instead of functions. Below, we explain the flow of both
smallestbandwidthgivingthegreatestsymboldurationthusthe
algorithms.
longestair-time;LoRaallowsapayloadlimitof255bytes.The
1) Algorithm1:NetworkServer: Lines1-3:Theserverwaits resulting maximum uplink air-time equals 11936 ms, requiring
for incoming packets. Once a packet is received, the server log (11936)=14bitsforencoding.2bytesarethereforeenough
2
immediately uses Eq. (12) to calculate its position inside the to encode the slot length T_slot and leave a margin of 53599
ongoing slot. ms for T +T . Those 2 bytes are the overhead induced by
b1 b2
Lines 4-7: The server checks whether the packet is out-sync; in our protocol, against the 8 bytes in [9].
which case, it gets the time remaining before the next slot from To enable coexistence of devices using this protocol for
Eq. (13), and piggybacks it to the ACK packet. slotted-Aloha with the preexisting ones in LoRaWAN, we
Lines 8-9: Once the ACK packet is ready, the server waits for propose to dedicate special FPort (Frame Port) values to
the next receive window and sends it. this protocol in LoRaWAN specifications. This is an efficient
2) Algorithm2:end-device: Lines1-6:AnEDthattransmits method, as it will allow the NS to distinguish the ED requiring
forthefirsttimedoesnothaveanysynchronizationreferenceon synchronization from those that don’t, and this without any ad-
its side. So, it takes the transmission moment as the reference. ditionaloverheadonthetransmittedpayload.Intheperformance
If that first frame arrives in-sync, this reference will be kept, evaluation section, we set the FPort to 198; it is not used for
otherwise it will be corrected. The corrected reference will be any services in the current specification, except for proprietary
used to determine slot start for future transmissions (line 5). protocols.
The flag is_first_tx, by default initialized to false, is used to
identify the first transmission.
V. EXPERIMENTALRESULTS
Lines 8-11: The end of the transmission is timestamped into In this section, we set up a test bench to evaluate the
beg. This instant coincides with the one when the NS takes the performances of our protocol. We set up a custom gateway
packet arrival time. The moment the ACK packet is received by providing few additional components to the Open Source
from the NS is also timestamped in end. GNURadioimplementationofLoRaphysicallayerin[16].We
Lines 12-20: If the received ACK packet contains remaining- also developed a LoRaWAN network server with the necessary
time bytes, it means the last transmission was received out- mechanisms for this protocol. All the related codes are made

TABLEII
LONGESTAIR-TIMELORARADIOPARAMETERS.
|     |     |     | Parameter       |     | Value |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --------------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     | CodingRate      |     | 4     |     |     |     |     |     |     |     |     |     |
|     |     |     | SpreadingFactor |     | 12    |     |     |     |     |     |     |     |     |     |
|     |     |     | Bandwidth(kHz)  |     | 125   |     |     |     |     |     |     |     |     |     |
|     |     |     | Payload         |     | 255   |     |     |     |     |     |     |     |     |     |
USRP-2920
(a)
TTGO LoRa32
Feather M0
| Fig. 4. | Test bench | equipment: |     | A National | Instruments | USRP-2920 | SDR | as  |     |     |     |     |     |     |
| ------- | ---------- | ---------- | --- | ---------- | ----------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
Gateway;AnAdafruitFeatherM0andaTTGOEsp32LoRaareusedasend-
| devices; | The network |     | server was | running | on a 6-cores | 12-threads | 4.0 GHz |     |     |     |     |     |     |     |
| -------- | ----------- | --- | ---------- | ------- | ------------ | ---------- | ------- | --- | --- | --- | --- | --- | --- | --- |
laptop.
End-node synchronization evolution
Upper bound
|                             | 800 |     |     |     |     | Lower bound   |     |     |     |     |     |     |     |     |
| --------------------------- | --- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| )sm( lavirra emarf evitaleR |     |     |     |     |     | Ideal arrival |     |     |     |     |     |     |     |     |
Feather sync
|     | 700 |     |     |     |     | TTGO sync |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
(b)
600
|     |     |     |     |     |     |     |     | Fig. 6. Fixed-rate | synchronization |     | algorithm | performance, | 6.5 | hours experi- |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------ | --------------- | --- | --------- | ------------ | --- | ------------- |
ment:(a)1hourroundduration;(b)30minsroundduration
500
400
timeinTableIV.Totalslotlengthreferstotheslotdurationand
300 accounts for both the uplink and downlink air-time, the 1000
|     | 0   |     | 5000 | 10000 | 15000 | 20000 |     |     |     |     |     |     |     |     |
| --- | --- | --- | ---- | ----- | ----- | ----- | --- | --- | --- | --- | --- | --- | --- | --- |
Time (s) ms delay, and the slot guards T and T of 180 ms each.
|     |     |     |     |     |     |     |     |     |     |     | b1  |     | b2  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Fig.5. Protocolperformance:devicessynchronizationandmonitoring We run the setup for 6.5 hours, logged the relative position of
|     |     |     |     |     |     |     |     | each frame | within | the ongoing | slot, | and | plotted the | evolution |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ------ | ----------- | ----- | --- | ----------- | --------- |
available on Github [17]. Fig. 4 shows our experimental test of the devices synchronization in Fig. 5. The upper and lower
| bench: | a USRP-2920 |     | serves | as  | a gateway, | and | an Adafruit |             |           |        |                 |     |           |         |
| ------ | ----------- | --- | ------ | --- | ---------- | --- | ----------- | ----------- | --------- | ------ | --------------- | --- | --------- | ------- |
|        |             |     |        |     |            |     |             | bounds mark | the limit | of the | synchronization |     | interval, | and the |
Feather M0 – that has a very unstable clock – and a TTGO ideal arrival line marks the position of frames received from a
| Esp32 | LoRa | – with | a much | more | stable clock | – boards | were |           |              |       |     |              |         |         |
| ----- | ---- | ------ | ------ | ---- | ------------ | -------- | ---- | --------- | ------------ | ----- | --- | ------------ | ------- | ------- |
|       |      |        |        |      |              |          |      | perfectly | synchronized | node. | The | first frames | of both | devices |
used as end-devices. The network server was running locally, were received out-of-sync; that was expected since they have a
on a 6-cores 4.0 GHz laptop. chanceofonly Tb1+Tb2 ≈20%tobereceivedin-sync.Theygot
Tslot
The performance of our protocol will be compared to that synchronized immediately and their next transmission matches
of the algorithm used in [9], where upchirp-modulated symbols the ideal arrival line. The evolution of the synchronization
were used for both the uplink and downlink; as a consequence, graphs shows the difference in the devices’ clocks stability and
the slot was made of the uplink air-time T tx , the downlink air- thesuccessoftheprotocolinresynchronizingthem:Thefeather
time T , the 1s gap, and the guard interval T and T . So, desynchronized three more times – twice during the first two
|     | rx  |     |     |     |     | b1  | b2  |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
we did the same here for a fair comparison. hours–andgetcorrectedrightafter,whiletheTTGOneverdid
We first run an experiment using the proposed synchroniza- becauseitsdriftsareverysmallcomparedtotheguardintervals
tionprotocol.Theend-devicestransmitapacketevery30s.The value; hence it didn’t need any resynchronization. In total, both
parameters in Table III together with Eqs. (6-10) gives the air- devices were synchronized 5 times during the 6.5 hours.

TABLEIII and retransmit if necessary. Furthermore, future works will
EXPERIMENTLORARADIOPARAMETERS investigate the impact of the increasing number of nodes on
the synchronization accuracy.
Parameter Value
Frequency(MHz) 868
Bandwidth(kHz) 125
ACKNOWLEDGMENT
CodingRate 1 ThisworkwassponsoredbytheJuniorFacultyDevelopment
Preamblesize 8
programundertheUM6P-EPFLExcellenceinAfricaInitiative.
UplinkPayloadsize 193
UplinkSpreadingFactor 7
DownlinkPayloadsize 19
DownlinkSpreadingFactor 8
REFERENCES
TABLEIV [1] P.Ferrari,E.Sisinni,P.Bellagente,D.F.Carvalho,A.Depari,A.Flam-
EXPERIMENTPACKETSAIR-TIME mini,M.Pasetti,S.Rinaldi,andI.Silva,“Ontheuseoflorawanandcloud
platformsfordiversificationofmobility-as-a-serviceinfrastructureinsmart
Parameter Value(ms) cityscenarios,”IEEETransactionsonInstrumentationandMeasurement,
Uplinkair-time 306 vol.71,pp.1–9,2022.
Downlinkair-time 91 [2] M.deCastroTomé,P.H.Nardelli,andH.Alves,“Long-rangelow-power
Totalslotlength 1757 wireless networks and sampling strategies in electricity metering,” IEEE
Transactions on Industrial Electronics, vol. 66, no. 2, pp. 1629–1637,
2018.
We run another two other experiments, this time using the [3] H. M. Jawad, R. Nordin, S. K. Gharghan, A. M. Jawad, and M. Ismail,
fixed-rate synchronization algorithm described in [9]: the EDs “Energy-efficient wireless sensor networks for precision agriculture: A
review,”Sensors,vol.17,no.8,p.1781,2017.
transmit a packet every 30s; after each round, the NS measures
[4] N.Podevijn,D.Plets,J.Trogh,L.Martens,P.Suanet,K.Hendrikse,and
their clock drift, logs it and re-synchronizes them; each round W.Joseph,“Tdoa-basedoutdoorpositioningwithtrackingalgorithmina
last 1 hour for the first experiment and 30 minutes for the public lora network,” Wireless Communications and Mobile Computing,
vol.2018,pp.1–9,2018.
second one. The resulting drifts are plotted as comparative bar
[5] Y. Etiabi, M. Jouhari, A. Burg, and E. M. Amhoud, “Spreading factor
diagrams between both devices and for both experiments. For assistedloralocalizationwithdeepreinforcementlearning,”in2023IEEE
the 1 hour round duration in Fig. 6a, the fixed-rate algorithm 97thVehicularTechnologyConference(VTC2023-Spring),pp.1–5,2023.
[6] M. Jouhari, N. Saeed, M.-S. Alouini, and E. M. Amhoud, “A survey
encounters two slot violations by the Feather and none by
on scalable lorawan for massive iot: recent advances, potentials, and
TTGO, and both were resynchronized in total 12 times during challenges,”IEEECommunicationsSurveys&Tutorials,pp.1841–1876,
thewholeexperiment;thisis2.4timesmoreoverheadsthanour 2023.
[7] L.-A.PhanandT.Kim,“Enablingrapidtimesynchronizationwithslow-
adaptive algorithm that does even prevent slot violation . And,
flooding in wireless sensor networks,” IEEE Communications Letters,
for the 30 mins round duration from Fig. 6b, there has been vol.26,no.4,pp.947–951,2022.
no slot violation for any of the devices, but they were however [8] X. Huan, H. He, T. Wang, Q. Wu, and H. Hu, “A timestamp-free time
synchronizationschemebasedonreverseasymmetricframeworkforprac-
resynchronized 26 times; this is five times more overheads than
tical resource-constrained wireless sensor networks,” IEEE Transactions
our algorithm and for the same result. onCommunications,vol.70,no.9,pp.6109–6121,2022.
In summary, it clearly appears that the fixed-rate synchro- [9] T.Polonelli,D.Brunelli,andL.Benini,“Slottedalohaoverlayonlorawan-
adistributedsynchronizationapproach,”inIEEE16thinternationalcon-
nization algorithm is not able to prevent slot violations while
ferenceonembeddedandubiquitouscomputing,pp.129–132,2018.
keeping a low synchronization overhead at the same time. Our [10] T.Polonelli,D.Brunelli,A.Marzocchi,andL.Benini,“Slottedalohaon
algorithm, on the other hand is able to accomplish both by lorawan-design,analysis,anddeployment,”Sensors,vol.19,no.4,p.838,
2019.
adapting to each device separately, hence succeeds in being
[11] L. Beltramelli, A. Mahmood, P. Österberg, M. Gidlund, P. Ferrari, and
more duty-cyle efficient. E. Sisinni, “Energy efficiency of slotted lorawan communication with
out-of-bandsynchronization,”IEEETransactionsonInstrumentationand
VI. CONCLUSION Measurement,vol.70,pp.1–11,2021.
[12] “Lorawan specification v1.1,” https://resources.lora-alliance.org/
In this paper, we proposed and tested a synchronization technical-specifications/lorawan-specification-v1-1, accessed : 2023-
protocol for LoRaWAN class A devices, designed to optimize 08-29.
[13] N. Abramson, “The aloha system: Another alternative for computer
gatewaysdutycycleconsumptionbyreducingthedownlinkair-
communications,” in Proceedings of the fall joint computer conference,
time overhead, along with a novel slot structure. The experi- pp.281–285,1970.
mental results confirmed that our protocol was able to track [14] R. Tjoa, K. L. Chee, P. Sivaprasad, S. Rao, and J. G. Lim, “Clock drift
reduction for relative time slot tdma-based sensor networks,” in IEEE
each device synchronization state separately, and resynchronize
15th International Symposium on Personal, Indoor and Mobile Radio
itonlywhenitdetectsadesynchronization.Furthermore,itslow Communications(IEEECat.No.04TH8754),vol.2,pp.1042–1047,2004.
overhead (only two bytes), duty-cycle efficiency and seamless [15] “Semtechsx1272/73technicaldatasheet,”accessed:2023-07-19.
[16] J. Tapparel, O. Afisiadis, P. Mayoraz, A. Balatsoukas-Stimming, and
integration with existing schemes position it as a powerhouse
A. Burg, “An open-source lora physical layer prototype on gnu radio,”
for slotted-Aloha adoption in LoRaWAN deployments within in IEEE 21st International Workshop on Signal Processing Advances in
the current massive IoT context. WirelessCommunications,pp.1–5,2020.
[17] “Mini-lorawan implementation,” https://github.com/dossam/
Our solution could be improved by reducing downlink ACK
mini-lorawan/,accessed:2024-04-03.
packets, since it currently requires a downlink acknowledge-
ment for each uplink so that devices can identify collisions