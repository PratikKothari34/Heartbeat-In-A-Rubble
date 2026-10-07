> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> arXiv **2111.05457** - *Optimizing the number, placement and backhaul of multi-UAV networks*.
> Source PDF deleted after conversion.
>
> Listed in `docs/research/BUDGET/01-literature.md` deployment row 4 as **HELD**, no figure
> quoted. Node-count optimisation under a connectivity constraint - the formal treatment of the
> **node-count question** behind the budget scaling table, where the 4-vs-N node trade is
> currently argued informally.

1
Optimizing Number, Placement, and Backhaul
Connectivity of Multi-UAV Networks
Javad Sabzehali, Vijay K. Shah, Qiang Fan, Biplav Choudhury, Lingjia Liu, and Jeffrey H. Reed
Abstract—Multi-Unmanned Aerial Vehicle (UAV) Networks is cancollaboratetoformaMulti-UAVNetworkandprovideend-
a promising solution to providing wireless coverage to ground to-end wireless communication services to all ground users
usersinchallengingruralareas(suchasInternetofThings(IoT)
(e.g., IoT devices, etc.) in the area of operation. However,
devicesinfarmlands),wherethetraditionalcellularnetworksare
there are several challenges in doing so.
sparse or unavailable. A key challenge in such networks is the
3D placement of all UAV base stations such that the formed Deploying a Multi-UAV Network in order to provide wire-
Multi-UAV Network (i) utilizes a minimum number of UAVs lesscoveragetoallgroundusersinacertainareaofoperation
while ensuring – (ii) backhaul connectivity directly (or via other incurs enormous investment for network providers. Thus, it is
UAVs) to the nearby terrestrial base station, and (iii) wireless
critically important to utilize minimum number of UAVs and
coverage to all ground users in the area of operation. This
facilitate the engineering application of Multi-UAV Networks.
joint Backhaul-and-coverage-aware Drone Deployment (BoaRD)
problem is largely unaddressed in the literature, and, thus, is As the ground user distribution in a typical rural or remote
the focus of the paper. We first formulate the BoaRD problem area exhibits spatial and temporal dynamics, it is favorable to
as Integer Linear Programming (ILP). However, the problem is place UAVs close to more users and increase the number of
NP-hard, and therefore, we propose a low complexity algorithm
userscoveredbydeployedUAVs.Moreover,inordertoensure
withaprovableperformanceguaranteetosolvetheproblemeffi-
end-to-end wireless connectivity between the terrestrial base
ciently.OursimulationstudyshowsthattheProposedalgorithm
performsveryclosetothatoftheOptimalalgorithm(solvedusing station (BS) and any UAV (via other UAVs as relay hops), it
ILP solver) for smaller scenarios, where the area size and the is important that all the deployed UAVs in the formed Multi-
numberofusersarerelativelysmall.Forlargerscenarios,where UAV Network maintain a backhaul connectivity among UAVs
the area size and the number of users are relatively large, the
(in other words, there exists at least one path from a UAV to
proposedalgorithmgreatlyoutperformsthebaselineapproaches
any other UAV in the formed Multi-UAV Network) [3]–[6]. –backhaul-awaregreedyandrandomalgorithm,respectivelyby
upto17%and95%inutilizingfewerUAVswhileensuring100% Several works on UAV-assisted wireless communications
groundusercoverageandbackhaulconnectivityforalldeployed have investigated optimal 3D placement of UAVs with a
UAVs across all considered simulation setting.
variety of objective functions such as ground user coverage
Index Terms—Unmanned Aerial Vehicles, Multi-UAV Net- maximization [7], maximizing average rate under worst-case
works, Graph Theory, Approximate Algorithms, Backhaul bit error rate threshold [8], energy-efficient communication
maximization [9], etc. with applications in coverage and ca-
I. INTRODUCTION pacityenhancement.PleaserefertoRelatedWorksfordetailed
discussion of related works. However, there is no work that
Unmanned Aerial Vehicles (UAVs), or drones, have found
studies the joint optimization of number, 3D placement and
numerous applications in recent years in the industry, gov-
backhaul connectivity of Multi-UAV Networks.
ernment, and commercial fields, such as telecommunications,
In this paper, we first formulate the above Backhaul-and-
rescue operations, safety aerial sensing, safety surveillance,
coverage-aware Drone Deployment (BoaRD) optimization
package delivery, and precision agriculture [1]. In particular,
problem as an integer linear programming (ILP) problem,
UAVshaveattractedsignificantattentionasthekeyenablersof
considering communication channel constraints for all the
end-to-endwirelesscommunications,owingtotheirsmallsize,
access links and backhaul links, and show that it is NP-Hard.
positioning flexibility, and agile autonomy. One of the critical
Following this, we propose a low computational complexity
applications of UAVs is to provide wireless connectivity in
algorithm, using graph theoretic concepts, for solving the
remote/rural areas to wireless devices, such as Internet of
BoaRD problem with a provable performance guarantee.
Things(IoT)devices,wheretheconventionalcellularwireless
coverage is sparse or largely unavailable [2]. Multiple UAVs The key contributions of the paper are as follows.
• WeinvestigatetheproblemofUAV3Dplacementsuchthat
ThisworkispartiallysupportedbyOfficeofNavalResearchunderGrant
the formed Multi-UAV Network (i) employs a minimum
N00014-19-1-2621andCommonwealthCyberInitiative(CCI),aninvestment
intheadvancement ofcyberR&D,innovation, andworkforcedevelopment. numberofUAVs,(ii)ensureswirelesscoveragetoallground
FormoreinformationaboutCCI,visitwww.cyberinitiative.org users in the area of operation, and finally, (iii) guarantees
Javad Sabzehali, Biplav Choudhury, Lingjia Liu, and Jeffrey H. Reed are
that all UAVs in the Multi-UAV Network are directly or
withWireless@VT,TheBradleyDepartmentofECEatVirginiaTech,Blacks-
burg,VA24061USA(e-mails:{jsabzehali,biplavc,ljliu,reedjh}@vt.edu). indirectly (via one or more UAV relay hops) connected
Vijay K. Shah is with Department of Cybersecurity Engineering, George to the nearby terrestrial BS, i.e., the formed Multi-UAV
MasonUniversity,Fairfax,VA22030USA(e-mail:vshah22@gmu.edu).
Network maintains an end-to-end backhaul connectivity
Qiang Fan is with Qualcomm, San Jose, CA 95110 USA (e-mail: qiang-
fan29@gmail.com). among UAVs.
2202
nuJ
61
]TI.sc[
2v75450.1112:viXra

2
We formulate the joint optimization problem of num- capacity enhancement of 4G/5G cellular networks, flying ad-
•
ber, placement, and backhaul connectivity of Multi-UAV hoc networks (FANETS), and flying base stations for post-
Networks, termed, Backhaul and coverage-aware Drone disaster situations, mmWave Communications, among others.
Deployment (BoaRD) problem as an Integer Linear Pro- Thoughthereexistsarichandgrowingbodyofliteratureon
gramming (ILP) optimization problem. We show that the UAV communications, including optimal placement of UAVs,
Geometric Set Cover problem is reducible to the BoaRD thereisscantworkonthedesign,analysis,andoptimizationof
problem,andprovethatitisNP-Hard.Tosolvetheproblem backhaulconnectivityofMulti-UAVNetworkswhileoptimizing
efficiently, we use graph theoretic concepts and propose a the placement of UAVs for ground user coverage. Bor-Yaliniz
low computational complexity algorithm with a provable et al. [15] proposed a 3-D placement algorithm to cover the
performance guarantee. maximum number of ground users given the fixed number
We solve the BoaRD problem using ILP solver (namely, of UAVs. Zhang et al. [36] optimized the 3D position of
•
Gurobi optimizer) and compare our proposed algorithm UAVs aiming to jointly minimize the number of UAVs and
against it for smaller scenarios, where the area size of the coverage rate. Lin et al. [37] proposed an adaptive UAV
considered operation area is small (up to 10×10 sq. Km) deployment scheme to optimize UAV locations for more user
and number of users is few (e.g., up to 60 users). The coverage,andlesscommunicationenergyconsumption.Zhang
results shows that the Proposed algorithm performs quite et al. [38] studied the joint 3D deployment of the UAVs
well and utilizes close to optimal number of UAVs for and power allocation problem to maximize the throughput
smaller scenarios. of the UAV base station system. However, the mentioned
For larger scenarios (with larger operation area sizes (e.g., works only focused on the access link in the drone-assisted
•
50×50 sq Km.) and hundred’s of ground users), our large- network without considering the backhaul link. Ansari et
scale simulations demonstrate that the Proposed algorithm al. [33] proposed a drone communications framework, in
significantly outperforms the two baselines – Backhaul- which free space optical links are employed to serve as the
aware Greedy (described in Section VIII) and Random backhaul link between UAV and ground base stations. They
algorithmsinutilizingfewernumberofUAVs,byupto17% used the free space link to transfer data and energy to the
and 95%, respectively, across varying number of ground UAV simultaneously and thus provision high-speed backhaul
users, area sizes and SNR thresholds for backhaul links. as well as prolong the UAV’s flight. Lyu et al. [34] aimed to
Moreover, the Proposed algorithm outperforms the basic minimize the number of UAV-mounted mobile base stations
greedy solution (with no backhaul) by up to 13% in high (MBS) needed to provide wireless coverage for a group of
user density scenarios at low backhaul SNR thresholds distributed ground terminals (GTs), with the assumption that
(i.e., minimum SNR threshold for a successful connection MBSs are backhaul-connected via satellite links. Neeto et al.
betweentwoUAVs),whichfurthercorroboratestheefficacy [42] proposed an approach to partition the available resource
of the Proposed algorithm. between access links and a backhaul link by optimizing the
|     |     |     |     |     |     | placement | of a | single UAV | in  | the area of | operation. | Hu et |
| --- | --- | --- | --- | --- | --- | --------- | ---- | ---------- | --- | ----------- | ---------- | ----- |
Theremainderofthispaperisorganizedasfollows.Section
|            |             |                |     |          |            | al. [43] maximized |     | the | system | uplink throughput |     | by jointly |
| ---------- | ----------- | -------------- | --- | -------- | ---------- | ------------------ | --- | --- | ------ | ----------------- | --- | ---------- |
| II reviews | the related | works. Section | III | presents | the system |                    |     |     |        |                   |     |            |
model.InSectionIV,weformulatetheBoaRDproblemasan optimizing the UAV altitude, power control, and bandwidth
|                  |         |           |     |              |         | allocation | between | the backhaul |     | and access | links. Pham | et al. |
| ---------------- | ------- | --------- | --- | ------------ | ------- | ---------- | ------- | ------------ | --- | ---------- | ----------- | ------ |
| ILP optimization | problem | and prove | its | NP-hardness. | Section |            |         |              |     |            |             |        |
[39]aimedtomaximizethesumrateachievedbygroundusers
| V discusses | the key intuitions |     | behind the | Proposed | solution, |     |     |     |     |     |     |     |
| ----------- | ------------------ | --- | ---------- | -------- | --------- | --- | --- | --- | --- | --- | --- | --- |
byjointlyoptimizingtheUAVplacement,spectrumallocation,
| which are  | at the basis   | of the | Proposed   | algorithm | discussed   |           |          |       |          |          |             |     |
| ---------- | -------------- | ------ | ---------- | --------- | ----------- | --------- | -------- | ----- | -------- | -------- | ----------- | --- |
|            |                |        |            |           |             | and power | control. | Their | scenario | consists | of a single | UAV |
| in Section | VI. In Section | VII,   | we analyze | the       | performance |           |          |       |          |          |             |     |
guarantee of the Proposed algorithm. Section VIII discusses connected to a macro base station by a backhaul link and
|                  |          |              |         |     |              | serves several       | ground | users             | via     | access links. | Iradukunda | et          |
| ---------------- | -------- | ------------ | ------- | --- | ------------ | -------------------- | ------ | ----------------- | ------- | ------------- | ---------- | ----------- |
| the experimental | results. | Finally,     | Section | IX  | presents the |                      |        |                   |         |               |            |             |
|                  |          |              |         |     |              | al. [5] investigated |        | the               | problem | of maximizing |            | the worst   |
| concluding       | remarks. |              |         |     |              |                      |        |                   |         |               |            |             |
|                  |          |              |         |     |              | achievable           | rate   | for ground        | users   | by optimizing |            | the UAV     |
|                  |          |              |         |     |              | placement            | and    | power allocation, |         | and bandwidth |            | allocation. |
|                  | II.      | RELATEDWORKS |         |     |              |                      |        |                   |         |               |            |             |
|                  |          |              |         |     |              | They considered      |        | that several      | users   | are connected |            | to a single |
Recentyearshavewitnessedasurgeofworkssuchasin[2], UAV via access links, which is connected to a macro base
[5]–[40](aswellasthecomprehensiveoverview[1][41])that station via a backhaul link, by incorporating non-orthogonal
attempts to address several research challenges in UAV com- multiple access (NOMA) scheme. Santos et al. [44] provided
municationsandnetworking.Existingliteraturehasfocusedon an approach to optimally place the UAVs as gateways in the
the following research directions – (i) air-to-ground channel area to address the dynamic traffic demand of access points,
modeling [10]–[13], (ii) UAV trajectory optimization [19]– which itself is based on dynamic attributes of users. Nguyen
[24], (iii) performance analysis of UAV-enabled wireless net- et al. [40] aimed to maximize the user sum rate in a UAV-
works[25]–[28],and(iv)optimalplacementofUAVsasflying assisted cellular network by jointly optimizing the location
base stations with a variety of objective functions such as of UAVs, the transmit bemformer at UAVs and a macro cell
energy-efficient communication maximization, sum-rate max- base station, and the decoding order of the NOMA-successive
imization, ground user coverage maximization, and maximize interference cancellation on wireless backhaul transmissions.
average rate under worst-case bit error rate threshold [2], [5]– They considered a number of UAVs directly backhauling to
[9], [14]–[18], [29]–[40], with applications in coverage and the macro cell base station and forming a two-hop backhaul

3
connectivity. Dai et al. [6] aimed to maximize the end-to-end division multiple access (and furthermore, channel resource
throughput in a UAV-assisted cellular network consisting of a scheduling protocols) so as to ensure no or little co-channel
single user, a macro cell base station, and a fixed number of interference between two ground users.
UAVs.TheyderivedtheoptimalpositionofUAVsconsidering Even after employing proper frequency planning and mul-
power control, and orthogonal frequency schemes. tiple frequency/time division access schemes, we understand
As evidenced, none of the existing work have investigated that both these communication links are wireless and are
the joint optimization problem of number, placement, and susceptible to channel interference and other factor such as,
backhaul connectivity of Multi-UAV Networks, which is the large scale fading, small-scale fading and shadowing. How-
key focus of our work. ever, since the focus of our work is on the deployment and
|     |     |     |     |     |     |     | coverage | of Multi-UAV |     | Network |     | (rather | than lower | PHY | or  |
| --- | --- | --- | --- | --- | --- | --- | -------- | ------------ | --- | ------- | --- | ------- | ---------- | --- | --- |
III. MULTI-UAVNETWORKMODEL MAC layer design for a certain wireless link), we utilize
|                    |     |             |      |          |       |            | simplified        | communication     |                       | path           | loss          | model     | for               | wireless | links   |
| ------------------ | --- | ----------- | ---- | -------- | ----- | ---------- | ----------------- | ----------------- | --------------------- | -------------- | ------------- | --------- | ----------------- | -------- | ------- |
|                    |     |             |      |          |       |            | (both access      | and               | backhaul              |                | links).       | One can   | extend            | our      | work    |
|                    |     |             |      |          |       |            | to account        | for               | channel               | interference   |               | and other | specific          |          | channel |
|                    |     |             |      |          |       |            | related factors   |                   | by employing          |                | sophisticated |           | path              | loss     | models, |
|                    |     |             |      |          |       |            | such as,          | measurement-based |                       |                | path loss     | models.   |                   |          |         |
|                    |     |             |      |          |       |            | A. Average        | path              | loss                  | model          | between       | a ground  |                   | user and | UAV     |
|                    |     |             |      |          |       |            | The air-to-ground |                   |                       | communications |               | channel   |                   | may be   | line-   |
|                    |     |             |      |          |       |            | of-sight          | (LoS),            | and non-line-of-sight |                |               | (NLoS),   |                   | and thus | both    |
|                    |     |             |      |          |       |            | of them           | need              | to be                 | taken into     | account.      |           | The communication |          |         |
| Fig. 1: Envisioned |     | Multi-UAV   |      | network  | model | with UAVs, |                   |                   |                       |                |               |           |                   |          |         |
|                    |     |             |      |          |       |            | channel           | is assumed        | to                    | be a           | probabilistic |           | LoS channel.      |          | Given   |
| ground users,      | and | terrestrial | base | station. |       |            |                   |                   |                       |                |               |           |                   |          |         |
anaccesslinkbetweengrounduserilocatedat(x(cid:48),y(cid:48),0),and
i i
|                                                |       |           |     |             |           |            | UAV j         | located | at (x       | ,y ,h | ), the     | path | loss of | the LoS | and |
| ---------------------------------------------- | ----- | --------- | --- | ----------- | --------- | ---------- | ------------- | ------- | ----------- | ----- | ---------- | ---- | ------- | ------- | --- |
| AsshowninFig.1,weconsideraMulti-UAVNetworkwith |       |           |     |             |           |            |               |         |             | j j   | j          |      |         |         |     |
|                                                |       |           |     |             |           |            | NLoS channels |         | are modeled |       | as follows | [7]: |         |         |     |
| V ground                                       | users | 1, J UAVs | as  | aerial base | stations, | and one or |               |         |             |       |            |      |         |         |     |

more nearby terrestrial BS via which the Multi-UAV Network (cid:16) 4πfcdij (cid:17)
|     |     |     |     |     |     |     |     | ϕL | =20log |     |     | +ηL, |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | --- | --- | ---- | --- | --- | --- |
can communicate with outside world. Denote B as the set of ij c
|     |     |     |     |     |     |     |     |     |     |     | (cid:16) | (cid:17) |     |     | (1) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | -------- | --- | --- | --- |
terrestrialBSsintheareaofoperation.Weassumethatground ϕN 4πfcdij +ηN.
=20log
|           |             |     |             |        |       |              |     |     | ij  |     | c   |     |     |     |     |
| --------- | ----------- | --- | ----------- | ------ | ----- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| users and | terrestrial | BSs | are located | at the | given | locations on |     |     |     |     |     |     |     |     |     |
|           |             |     |             |        |       |              |     | ηL  | ηN  |     |     |     |     |     |     |
the horizontal plane (ground). For simplicity, let V =V ∪B where and are denoted as the system loss for the
|            |        |        |       |            |                 | BSs)2 | LoS and | NLoS       | of an  | access | link,          | f is the | carrier | frequency,  |     |
| ---------- | ------ | ------ | ----- | ---------- | --------------- | ----- | ------- | ---------- | ------ | ------ | -------------- | -------- | ------- | ----------- | --- |
| be the set | of all | ground | users | (including | the terrestrial |       |         |            |        |        |                | c        |         |             |     |
|            |        |        |       |            |                 |       | d = [(x | −x(cid:48) | )2 +(y | −y     | (cid:48))2 +h2 | ]2 1     | is this | 3D distance |     |
that are required to be covered by J UAVs deployed in the ij j i j i j
region of interest. between user i and UAV j, and c is the speed of light. As the
|           |      |            |     |                |          |     | access link | is a | probabilistic |     | LoS channel, |     | the probabilities |     | of  |
| --------- | ---- | ---------- | --- | -------------- | -------- | --- | ----------- | ---- | ------------- | --- | ------------ | --- | ----------------- | --- | --- |
| Note that | both | the height |     | and horizontal | distance | of  | a           |      |               |     |              |     |                   |     |     |
UAV towards ground users significantly impact the channel both the LoS and NLoS channels can be expressed as [7]:
c o n d it io n s o f th e a c c es s l i nk . O n t h e o t h e r h a n d , a l l g ro u n d (cid:26) −1
|     |     |     |     |     |     |     |     |     | pL  | =[1+ae−b(θij−a)] |     |     | ,   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- |
u se r s n e e d to c o m m u n ic a t e w it h ea c h o t h e r ( o r t o t h e re m o t e (2)
pN =1−pL,
| server) via | the | backhauls | between | UAVs, | which requires | that |     |     |     |     |     |     |     |     |     |
| ----------- | --- | --------- | ------- | ----- | -------------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
all UAVs keep connectivity with each other. Thus, UAVs where a and b are constant parameters based on the environ-
should be deployed close enough to each other to ensure the ment (e.g., urban, rural, etc.), which can be measured proac-
| channel condition |     | threshold | of  | the UAV-UAV | backhaul | links. |           |           |           |       |         |     |        |      |       |
| ----------------- | --- | --------- | --- | ----------- | -------- | ------ | --------- | --------- | --------- | ----- | ------- | --- | ------ | ---- | ----- |
|                   |     |           |     |             |          |        | tively. θ | ij is the | elevation | angle | between |     | ground | user | i and |
Asaresult,boththe(UAV-grounduser)accesslinkand(UAV- UAV j that can be modeled as θ = arctan(h /δ ) where
|     |     |     |     |     |     |     |     |     |     |     | ij  |     |     | j ij |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- |
UAV) backhaul link are taken into account in the Multi-UAV h istheheightoftheUAVandδ =[(x −x )2+(y −y )2]1
|     |     |     |     |     |     |     | j   |     |     |     | ij  | j   | i   | j   | i 2 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Network to provide seamless coverage for all ground users. is the horizontal distance between user i and UAV j.
In this work, we consider that the adjacent UAVs (in the Hence, the average path loss of the access link can be
| backhaul  | links)   | in our Multi-UAV |           | Network | utilize      | orthogonal |         |            |      |       |        |     |     |     |     |
| --------- | -------- | ---------------- | --------- | ------- | ------------ | ---------- | ------- | ---------- | ---- | ----- | ------ | --- | --- | --- | --- |
|           |          |                  |           |         |              |            | derived | as follows | [7]: |       |        |     |     |     |     |
| frequency | channels | to not           | interfere | with    | one another. | This       |         |            |      |       |        |     |     |     |     |
|           |          |                  |           |         |              |            |         |            | ϕ    | =pLϕL | +pNϕN. |     |     |     | (3) |
is a typical frequency planning approach employed in the ij ij ij
terrestrialcellularnetworks.ItmeansthattwoUAVscanreuse B. Average path loss model between two UAVs
| the same | frequency | channel | (and   | spectrum | band)        | if those two |           |          |          |        |          |     |         |         |       |
| -------- | --------- | ------- | ------ | -------- | ------------ | ------------ | --------- | -------- | -------- | ------ | -------- | --- | ------- | ------- | ----- |
|          |           |         |        |          |              |              | Since     | UAVs     | fly over | ground | users,   | we  | assume  | that    | their |
| UAVs not | adjacent  | to each | other. | For      | access link, | we can       |           |          |          |        |          |     |         |         |       |
|          |           |         |        |          |              |              | altitudes | are high | enough   | to     | maintain | LoS | channel | between |       |
use the same frequency channel with various frequency/time each other. Thus, the path loss between UAV j and UAV k
|     |     |     |     |     |     |     | can be expressed |     | as  |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- | --- |
1Sincethegoalofourworkistoprovidewirelesscoveragetogroundusers
|     |     |     |     |     |     |     |     |     |     |     | (cid:18) |     | (cid:19) |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- | -------- | --- | --- |
inruralareas,e.g.InternetofThingsdevicesinfarmlands,theyareconsidered 4πf d
|     |     |     |     |     |     |     |     |     | ϕL  | =20log |     | c jk | .   |     | (4) |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------ | --- | ---- | --- | --- | --- |
tobestaticorlowmobilitygroundusers.Highmobilitygroundusersisout jk
| ofscopeofthisworkandwillbeinvestigatedasapartoffuturework. |     |     |     |     |     |     |     |     |     |     |     | c   |     |     |     |
| ---------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
2AswefocusonthedeploymentandcoverageofUAVnetwork,essentially,
|     |     |     |     |     |     |     | Without | loss | of generality |     | and for | the | ease of | presentation, |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | ---- | ------------- | --- | ------- | --- | ------- | ------------- | --- |
UAVsneedtocoverboththegroundusersandBSs(i.e.,BScanbeassumed
|                                  |     |     |     |     |     |     | we consider    | same | carrier | frequency |     | (f ) for | backhaul |     | link (as |
| -------------------------------- | --- | --- | --- | --- | --- | --- | -------------- | ---- | ------- | --------- | --- | -------- | -------- | --- | -------- |
| asa“grounduser”intheUAVnetwork.) |     |     |     |     |     |     |                |      |         |           |     | c        |          |     |          |
|                                  |     |     |     |     |     |     | that of access |      | link).  |           |     |          |          |     |          |

4
TABLE I: List of Symbols
u = 1 to indicate whether a certain UAV-UAV backhaul
jk
Symbol Definition link is selected in the Multi-UAV Network topology.
B SetofterrestrialBSs.
V Setofagroundusers(includingterrestrialBSs).
J SetofUAVsinMulti-UAVNetwork. (cid:88)
(xj,yj,hj) 3DlocationofUAVj. min f j (6)
(x(cid:48) i ,y i (cid:48),0) 3Dlocationofgrounduseri. (βij,fj,zjk) j
γij SNRbetweenUAVj anduseri (cid:88)
γ(cid:48) SNRbetweenUAVj andUAVk. β ij ≥1,∀i∈V, (7)
jk
γ0 MinimumSNRthresholdforsuccessfulconnectionbe- j∈J
tweenagrounduseriandaUAV.
γ β ≥γ β ,∀i∈V,∀j ∈J, (8)
γ(cid:48)
MinimumSNRthresholdforasuccessfulcommunica-
ij ij 0 ij
0 tionlinkbetweentwoUAVs. β ij ≤f j , (9)
R Radiusofmaximumradiocoverageonground (cid:48)
γ z ≥γ z ,∀j ∈J,∀k ∈J,k (cid:54)=j, (10)
R(cid:48) RadiusofmaximumUAVcoverage,(i.e.,inair) jk jk 0 jk
z ≤f ,z ≤f , (11)
jk j jk k
C. Communications Model (cid:88)
z ≥1,∀j ∈J, (12)
jk
Given the path loss model, P as the transmission power of
j k∈J
UAV j, and δ2 as the noise power, we can derive the signal-
u ≤z , (13)
jk jk
to-noise ratio (SNR) between UAV j and ground user i as
(cid:88) (cid:88)
follows: u jk ≥ f p −1, (14)
j,k∈J, p∈J
j(cid:54)=k
γ ij =10logP j −ϕ ij −10logδ2. (5) (cid:88)
u ≤|S|−1,∀S ⊆J,|S|≥1, (15)
jk
Note that the SNR of a ground user i determines if it is j,k∈S,
covered by the corresponding UAV. In other words, a ground j(cid:54)=k
user is assumed to be within the coverage of UAV j when f j ,β ij ,z jk ,u jk ∈{0,1}. (16)
its γ meets the SNR threshold γ (i.e., γ ≥ γ ). Given
ij 0 ij 0
the 3D location and transmission power of UAV j, we can ObjectiveFunction.AsshowninEq.6,theobjectivefunc-
determine the transmission range of a certain UAV. Similarly, tion is to minimize the number of UAVs (and determine the
we assume that UAV j and UAV k have a successful connec- optimal 3D placement of each UAV) in Multi-UAV Network,
tionprovidedthatγ exceedsthecorrespondingthresholdγ(cid:48). sothateachgrounduserisservedbyatleastoneUAVandthe
jk 0
Major notations used in this paper are listed in Table I. backhaul connectivity among UAVs is guaranteed. Note that
this does not preclude the possibility that some ground users
may be covered by more than one UAVs, and each UAV may
IV. PROBLEMFORMULATION
have links with more than one UAVs in Multi-UAV Network.
In this section, we formulate the Backhaul and coverage
Constraints.Eq.7imposeseachgroundusertobecovered
aware Drone deployment (BoaRD) problem as an Integer
by at least one UAV in the area. Eq. 8 indicates that a
LinearProgramming(ILP)optimizationproblem.BoaRDaims
ground user can only be covered by a certain UAV if the
to minimize the number of UAVs needed to provide wireless
SNR threshold (γ ) is met. Eq. 9 indicates that ground user i
0
coveragetoallgroundusersintheareaofoperation,suchthat
may be associated with UAV j only if UAV j is deployed in
(i)eachgrounduserisefficientlycoveredbyatleastoneUAV,
the area. Eq. 10 ensures that a UAV-UAV backhaul link exists
and (ii) the backhaul connectivity is guaranteed. onlyifitmeetstheSNRthresholdγ(cid:48) betweenthem.Similarly,
0
Notations. Let V and J denote the set of ground users
Eq.11indicatesthataconnectionbetweentwoUAVsj andk
and UAVs, respectively. γ denotes the SNR between ground
ij existsonlyifbothUAVsaredeployedintheareaofoperation.
user i ∈ V and UAV j ∈ J, whereas γ(cid:48) denotes the SNR
jk Eq. 12 ensures that a certain UAV has a backhaul link with
betweentwoUAVsj andk.Letγ denotestheminimumSNR
0 at least one other UAV. Note this constraint by itself does not
thresholdforsuccessfulconnectionbetweenagrounduserand
guarantee that the backhaul connectivity constraint is met.
a UAV. Similarly, let γ(cid:48) denotes the minimum SNR threshold
0 Inordertoaddressthis,weintroducethreemoreconstraints,
for successful communication between any two UAVs. For
i.e., Constraints 13, 14, and 15. Eq. 13 restricts a certain
backhaul connectivity criteria, a UAV must have a link with
UAV-to-UAV link be a part of connected network topology
atleastoneotherUAV.Finally,let(x ,y ,h )denotesthe3D
j j j only if the communication link exists between those two
location of UAV j (in case of deployment in the 3D space) in
UAVs. Constraint 14 ensures that there exists at least (n−1)
the considered area of operation. (cid:80)
connectionsamongnUAVs,wheren= f andn≤|J|.
Variables. We introduce a decision variable f = 1, if a j∈J j
j Moreover,constraintinEq.15ensuresthatthereisnocyclein
UAV j is located at a 3D location (x ,y ,h ) in the area of
j j j any subset S ⊆J. These two are the necessary and sufficient
operation, otherwise f = 0. We use another variable β =
j ij conditions to ensure a connected backhaul connectivity in
1, if a ground user i ∈ V is associated with a UAV j ∈ J,
Multi-UAV Network with n UAVs. Eq. 16 represents the
otherwise β = 0. We consider a third variable z = 1, if
ij jk binary decision variables, that take values either 0 or 1.
a UAV j is connected to UAV k, otherwise z = 0 (where
jk
j,k ∈ J). Fourth, we introduce a dummy decision variable Theorem 1. The BoaRD problem is NP-Hard.

5
Proof. We show that Geometric Set Cover (GSC) problem,
whichisNP-Hard,ispolynomial-timereducibletotheBoaRD
problem,whichfurthershowsthattheBoaRDproblemisNP-
Hard. Let us consider a generic instance of GSC problem:
Given a set X of points in R2, and R is a family of subsets
of X, which is called ranges. The goal is to select a subset
C ⊆ R whose size is minimum and all points in the X are
covered by at least one range in C.
The proof is quite straightforward. Suppose that the SNR
thresholdforUAV-to-UAVlinkis−∞(i.e.,γ(cid:48) =−∞),which
0
relaxes Constraint 10. Furthermore, it also means all UAVs
arein communicationrange, andthus,relaxes allconnectivity
constraints, i.e., Constraints 13, 14, and 15. Given SNR
Fig. 2: Constructed graph G, with V ground users and K
thresholdforUAV-to-grounduserlinkγ ,wecancomputethe
0
candidate locations in the area of operation. Blue and Red
radiusofmaximumgroundcoverage(denotedbyR)[7].Then,
dots respectively represent ground users and candidate 3D
BoaRD Problem is transformed into choosing the minimum
locations. An edge (in red) represents the communication link
number of radio coverage disks (with radius R) that provides
between a ground user and a candidate location. Whereas, an
coverage to all ground users. Considering the set of users
edge (in green) denotes the link between two UAVs.
J =X,andthesetofusersonthegroundthatcanbecovered
by deploying UAVs R = R, then the optimal solution to the
location covers the set of ground users {u ,u ,u ,u }, then
1 2 3 4
transformed problem C is equivalent to the optimal solution
the Proposed solution does not need to consider 3D locations
to the GSC problem C. We reduced the GSC problem to
that cover its subsets, such as, {u ,u } or {u ,u ,u } 3.
1 2 2 3 4
an instance of BoaRD problem. Since the GSC problem is (IV) Account for UAV-UAV connectivity guarantee. The
a classic NP-hard problem [45], the BoaRD problem is also proposed solution to the BoaRD problem not only minimizes
NP-Hard. the number of UAVs needed to cover all the ground users,
but also guarantees that the deployed UAVs ensure backhaul
connectivity. Now the average path loss in the UAV-UAV
V. KEYINTUITIONSBEHINDTHEPROPOSEDSOLUTION
backhaul link is usually much smaller compared to that of
In this section, we discuss key intuitions behind the pro- UAV-to-ground user access link, thanks to LOS path loss
posed solution (discussed in Section VI) that solves BoaRD model in case of backhaul links. Thus, the maximum radius
problem in polynomial-time with performance guarantees. R(cid:48) of UAV coverage is much larger than the maximum radius
(I) Focus on the optimal altitude of the UAVs that provides R of the radio coverage on the ground, i.e., R(cid:48) >R.
maximum radio coverage on the ground. Since one of the key 3D candidate locations of UAVs. Intuitively, the number
objectives of BoaRD problem is to provide coverage to all of candidate locations of UAVs in the area of operation is
ground users in the area, it becomes intuitive that UAVs are infinite. Utilizing intuitions I and II, we present a simple
deployed at the optimal altitude that provides maximum radio grid approach to reduce the infinite solution space of BoaRD
coverage on the ground while meeting the SNR threshold, problem to finite solution space – We first determine the
thanks to their capability of maintaining that height. From the optimal altitude of the UAVs that provides the maximum
seminal work [7], such an optimal altitude can be computed coverage on the ground (See Intuition I). Next, as depicted in
mathematically given the environmental parameters, carrier Figure 2, we divide the area of operation into N grids, each
frequency, LoS and NLoS system loss, and transmit power. with diagonal length = R, and length = breadth = √R , where
2
Let h and R respectively be the optimal altitude of UAV and Ristheradiusofthemaximumradiocoverageontheground.
the radius of the maximum radio coverage by a UAV on the All these grid intersection points are the candidate locations
ground (corresponding to SNR threshold γ 0 for access link). of UAVs. Notice this approach allows 8 grid intersections
(II) Focus on possible covered sets of ground users for ({k | i ∈ [1,9],i (cid:54)= 5}) in addition to the central grid
i
UAVs rather than candidate 3D locations of UAVs. Since intersection (k ). Given that there are 9 candidate locations
5
UAVs can be deployed in any 3D location in the area of within a grid of diagonal length R, it is very likely that the
operation R3, the number of candidate locations of UAVs is resultant finite solution space (with N grids) will have the
infinite, or the solution space of BoaRD problem is infinite. (near) optimal solution to the problem. Compared to state-of-
However, several of those candidate locations are essentially the-art grid based approach [30], [31] that simply discretizes
equivalent if they provide wireless coverage to the same set theareaofoperation,ourapproachhereistocreateaminimum
of ground users. Thus, the Proposed solution only needs to number of grids that discretizes the area without loosing out
consider one representative 3D location among its associated on the potential of finding an optimal solution. However,
classofallequivalent3Dlocations,andthenumberofallsuch our proposed approach is independent of this approach, and
representative 3D locations is finite because the number of all
possible covered set of ground users is finite. 3Note that this intuition holds for our BoaRD problem setting as it only
ensures ground user coverage (with no constraint on bit rate thresholds).
(III) Focus on those candidate 3D locations that provide
However, it will not hold for Multi-UAV Network system where user bit
coveragetoalargesetofgroundusers.Ifarepresentative3D ratethresholdshavetobemet.Wewillinvestigatethisinourfuturework.

6
will work perfectly with any state-of-the-art grid discretion Algorithm 1 Initialization
approaches. Input: Locations of ground users, Radius of maximum radio cov-
(cid:48)
erage on ground R, and Radius of maximum UAV coverage R
Output:GraphGandListofcandidatelocationswithitsassociated
VI. PROPOSEDALGORITHM ground users, U
1: Initialize a graph G=φ, and a list U =φ
In this section, we model Multi-UAV Network as a graph 2: for candidate location, j ∈K do
(See Figure 2), and then transform the BoaRD problem as a 3: for candidate location, k∈K do
(cid:48)
graph problem. Next, we propose a low-complexity algorithm 4: if dist jk ≤R then
with performance guarantee to effectively solve the trans- 5: G.add edge(j,k)
formed BoaRD problem. 6: U k = φ //Set of ground users in coverage range of candidate
location k∈K, i.e., dist ≤R where i∈V
Graph modeling. A UAV will provide wireless coverage ik
7: for ground user, i∈V do
to a certain ground user if it lies within the UAV’s maximum 8: for candidate location, k∈K do
radio coverage (R). On the other hand, a UAV will have a 9: if dist ik ≤R then
backhaul link with another UAV in the area of operation, if 10: G.add edge(i,k)
theyarewithinthetransmissionrangeofeachother(i.e.,R(cid:48)). 11: U k =U k ∪i
As depicted in Figure 2, let graph G(V ∪K,E∪E(cid:48)) denotes 12: U =∪ k∈K V k
13: return G,U
the Multi-UAV Network with V as the set of ground users
and K as the set of 3D candidate locations. For edge set E,
Algorithm 2 Proposed Algorithm
we include an edge e between user i ∈ V and candidate
ik
Input:V groundusers,Kcandidatelocations,andMaximumground
location k ∈K, if user i is covered by the UAV at location k,
(cid:48)
and UAV coverage radius, R and R respectively.
i.e., γ ≥γ . In other words, the euclidean distance between
ik 0 Output: D chosen candidate locations, where D⊆K
user i and candidate location k is less than or equal to R, i.e.,
(cid:48)
dist ≤ R. Similarly, the edge set E(cid:48) reflects the backhaul 1: G, U = INITIALIZATION (V, K, R, R )
ik 2: D=K
links, where a link e(cid:48) jk between UAV j and k exists if they 3: F =φ //Set of fixed nodes
are within each other’s transmission range. i.e., γ ≥ γ(cid:48) (or 4: while D\F (cid:54)=φ do
jk 0
euclidean distance between UAV j and k, dist ≤R(cid:48)). 5: U min ={k|U k ∈U,|U k | is minimum}
GiventhegraphG,theBoaRDproblemistra j n k sformedinto 6: u=argmin{δ(k)|k∈U min }
7: ifG[D\{u}]isnotconnectedorV\∪ k∈D\{u} U k (cid:54)=φthen
choosing the minimum subset D of K such that every node in 8: F =F ∪{u}
V is adjacent to at least one member of D and the members 9: for candidate location, k∈D\{F} do
in D form a connected network topology. 10: for ground user, i∈U u do
Let D ⊆ K be the minimum connected subset of G, i.e., 11: U k =U k \{i}
12: else
the solution of the BoaRD problem. It means that all nodes
13: D=D\{u}
in D can cover every node in V, and keep connected (i.e.,
the nodes of D can reach each other via a path that stays 14: U =U \{U u }
15: return D
entirely within D). In other words, deploying |D| UAVs at
the selected locations can provision coverage to all ground
users, whereas all the UAVs form a connected network,
U = ∪ U where each U contains the set of the ground
k∈K k k
i.e., backhaul connectivity is guaranteed. Note that though
users associated with the UAV at candidate location k ∈K.
the BoaRD problem seems similar with a well-known graph ThedetailsofINITIALIZATION(V,K,R,R(cid:48))ispresented
problem, i.e., Minimum Connected Dominating Set (MCDS)
in Algorithm 1. At the beginning, the algorithm initializes an
problem4[46],itisdifferentintwoaspects:(i)Disasubsetof
emptygraphGandlistU inLine1.Then,asshownlines2-5,
K (insteadofbeingasubsetofV itself);and(ii)eachnodein
thegraphGincorporatesedgesbetweeneachpairofcandidate
V is adjacent to at least one node in D, where D ⊆K. Note, location j,k ∈ K, whose euclidean distance is ≤ R(cid:48) (in
we do not consider any connectivity constraint on remaining
other words, the UAVs at the candidate locations j and k are
K\D. Next we detail the Proposed algorithm that efficiently within the maximum UAV coverage radius R(cid:48) of each other).
solves the transformed BoaRD problem with low computa-
Similarly, the algorithm also adds edges between ground user
tional complexity and provable performance guarantee.
i∈V and candidate location k ∈K if the euclidean distance
Algorithm Description. The pseudocode of the Proposed
between them is ≤R (See lines 7-10). In addition, as shown
algorithm is presented in Algorithm 2. As shown in Line 1,
in Line 11, we add ground user i into U (w.r.t to candidate
the algorithm first calls a function INITIALIZATION (V, K, k
location k) if user i is within the coverage range of UAV k.
R,R(cid:48))thatreturns–(i)theaforestatedgraphG,and(ii)alist
After the initialization step, we take the set of candidate
locations K as the initial D (Line 2 of Algorithm 2). (Note D
4AdominatingsetofagraphG,denotedasD,isasetofnodeswherefor
istheminimumconnectedsubsetofG,i.e.,thesolutiontothe
every node u∈G, either u∈D or u is adjacent to a node v ∈D. Then,
A connected dominating set of a graph G, denoted as D, is a dominating BoaRD problem). At each iteration, the algorithm first selects
set of graph G where for every node in D there exists a path to any other the list of candidate locations U which have the minimum
min
nodeinD thatstaysentirelywithinD.Andfinally,Aminimumconnected
cardinality of covered ground users (See line 5). Sequentially
dominatingset(MCDS)ofagraphGisaconnecteddominatingsetwiththe
smallestpossiblecardinalityamongallconnecteddominatingsetsofG. in Line 5, it selects a candidate location u, which has the

7
minimum degree in set U . As shown in Lines 7 - 14, the Lemma 1. Let OPT be an MCDS of G , any maximal
min r
algorithm removes the candidate location u from graph G if independent set5 of G has a maximum size of 5|OPT|+1.
r
both of the following conditions are met – (1) Removing u
Proof. Inspired by the work in [47], assume OPT be any
does not make the graph G disconnected, and (2) Remaining
MCDSinG ,andW isanyMISofG .LetT beanarbitrary
candidatelocations(K\{u})cancoverallthenodesinground r r
spanningtreeofOPT,and{v ,v ,...,v }beanyarbitrary
user set V. If the above conditions are not satisfied, candidate 1 2 opt
preorder traversal of T after picking an arbitrary node as the
location u is dispensible in the final solution D, and thus, u
rootofT.LetW bethesetofverticesinW thatareadjacent
must be fixed (See Line 8). Following this in Lines 9 - 11, i
to v , but none of v ,v ,...,v , for any 1<i≤opt. Also,
all the ground users that are associated with u are removed i 1 2 i−1
let W be the set of vertices in W that are adjacent to node
from the remaining U . Otherwise as shown in line 13, we 1
k v .Then,W ,W ,...,W formapartitionofW.W hasat
remove the candidate location u from D. Such a candidate 1 1 2 opt 1
most one of the u s defined in the above discussion. All other
location is referred to as non-fixed candidate location as its i
vertices of the W , which are nodes from the set K, should
removal neither disconnects the subgraph in D nor hampers 1
haveapairwisedistanceofmorethanR(cid:48) andthustherecould
thecoverageofgroundusersinV.Afterwards,weremovethe
be at most five nodes. Therefore, |W | could be at most 6. In
correspondingsetU fromthelistU.Thesestepsarerepeated 1
u other words, let us scale down all distances from R(cid:48) to 1, and
until there is no non-fixed candidate location in D.
assumetwoUAVswillbeconnectediftheireuclideandistance
Theorem 2. The time complexity of the Proposed algorithm is ≤ 1. Hence, any node will be adjacent to a maximum of
is O(|K|2.(|V|+|K|). five independent nodes in a Unit Disk Graph [47]. Because of
the preorder traversal labeling of the T, there is at least one
Proof. Since the Proposed algorithm calls the INITIALIZA-
node in {v ,v ,...,v } adjacent to v , and let us name it
TION function, we first check the time complexity of Al- 1 2 i−1 i
v . Hence, by considering the coverage range of v and v ,
gorithm 1. The time complexity for lines 2-5, and 7-11 j i j
there is a sector of at most 240 degrees, which is within the
of Algorithm 1 are O(|K|2) and O(|V|.|K|), respectively.
coverage area of v , but not v . Therefore, W \{u } should
Hence, the running time of Algorithm 1 (or line 1) of the i j i i
lie in the mentioned sector, and thus |W \{u }| is at most 4,
Proposed algorithm becomes O(|K|.(|V| + |K|)). Line 5, i i
and |W | is at most 5. Therefore,
and 6 of the Proposed algorithm have the time complexity |W|= (cid:80) i opt |W |≤6+5(opt−1)=5.opt+1.
O(|K|.|log(|K|)) (the time needed to sort the list and make a i=1 i
binary search), and O(|K|2) respectively. In addition, the pro- Lemma 2. Given the graph G and the resulting subset D
r
cedure of checking if a graph G (with D nodes and E edges) calculated by Proposed Algorithm on graph G, there is an
is connected or not, has the time complexity O(|D|+|E|), independent set of G containing at least |D|/4 vertices.
r
which is the time needed for running the depth first search.
Proof. The goal is to find an independent set with the car-
It implies that the running time of the first condition in line
dinality of at least (cid:100)|C |/2(cid:101) for each induced cycle6 C =
7 is (O(|K|+|K|2)). The second condition in line 7 has the m m
{v ,v ,...,v } in graph G[D], and remove them afterwards
complexity of O(|V|.|K|). The cost of lines 9-11 is O(|K|2). 1 2 k
[46]. If |C | is even, then there is a set I = {v | i is
Thewhileloopinline4willrepeatedfor|K|time,becausein m m i
even}, which, by the definition of an induced cycle, is an
each step a node in K will be either fixed or removed. Hence,
independent set. However, if |C | is odd, then there are two
the total time complexity of the Proposed algorithm can be m
cases. First, at least one of the vertices in C , let us name it
expressedasO(|K|(|V|.|K|+|K|2))=O(|K2|(|V|+|K|)). m
v , have a neighbor u , which is not the neighbour of other
i i
vertices in D, by our definition. Therefore, we can construct
VII. PERFORMANCEGUARANTEEANALYSIS
I by picking u with half of nodes from C \{v }, which
In this section, we analyze the performance guarantee of m i m i
is a bipartite tree, so that it is independent. Second, if none
theProposedalgorithmpresentedinaforestatedSectionVI.In
of vertices in C is connected to a user-representation node
order to accomplish this, we first reduce graph G into graph m
u , it implies that all the nodes in C are fixed to ensure the
G in the following manner. i m
r connectivityofthegraph,otherwiseatleastoneofthemwould
Consider a candidate location i ∈ D that provide wireless
have been removed by Algorithm 2. In this case, assume v
coverage to ground users which are not in the coverage area i
is a vertex of C , and it is connected to subgraph L , which
of any j ∈ D \ {i}. Let U ∈ V be the set of ground i i
i is out of C . It is obvious that if we remove v from C ,
users in the coverage area of candidate location i. We remove m i m
there is no path from any vertices in L to any vertices in
all ground users in the set U , and instead, add one dummy i
i C . Therefore, each vertex v ∈C is connected to a unique
node u (representing all the ground users in U ) connected m i m
i i subgraph L . There is at least one user-representation node
to candidate location i. By repeating this procedure, until no i
u in each L , otherwise all vertices of L should have been
ground users remain, we will have a set U =∪ u . Let graph j i i
i i removed. Let us construct I by selecting u with half of
G (U ∪K,E(cid:48) ∪E(cid:48)(cid:48)) where E(cid:48)(cid:48) is the set of edges between m j
r
added nodes u i ∈ U and UAV i. Note that each node in D 5Set S is an independent set if the subgraph S contains no edges. Then,
is connected to a unique node u ∈U or employed to ensure an independent set S ⊂G is a maximal independent set (MIS) if and only
i
the connectivity of subset D, otherwise it could have been if for every vertex u∈G−S the set S∪{u} is not independent (i.e. the
graphS∪{u}isnotindependent).
removed (recall such a node corresponds to a fixed candidate
6An induced cycle is a cycle such that no two nodes of the cycle are
location in Algorithm 2). connectedbyanedgethatdoesnotitselfbelongtothecycle.

8
nodes from C \ {v } so that it is independent. We should scenarios, and thus, we do not show the results for Optimal
i
ensurethatifweselectu j toconstructtheindependentsetI m algorithm in the large-scale simulation experiments presented
corresponding to set C , u is not needed for constructing I in the following section.
|                                |     |                  | m      | j              |           |      |                  |          | l      |        |                      |          |              |                |
| ------------------------------ | --- | ---------------- | ------ | -------------- | --------- | ---- | ---------------- | -------- | ------ | ------ | -------------------- | -------- | ------------ | -------------- |
| corresponding                  |     | to set           | C .    | If L , itself, | consists  |      | of any           | induced  |        |        |                      |          |              |                |
|                                |     |                  | l      | i              |           |      |                  |          | TABLE  | II:    | No. of UAVs (Optimal |          | vs. Proposed | algorithm)     |
| cycle(s)                       | C   | with odd         | number | of             | vertices, | then | we               | can find |        |        |                      |          |              |                |
|                                | l   |                  |        |                |           |      |                  |          | Number | of     | ground users (#GU)   | Approach |              | Number of UAVs |
| a node                         | u   | for constructing |        | I . Because    |           | |C | | > 2, then        | C        | is     |        |                      |          |              |                |
|                                | k   |                  |        | l              |           | l    |                  | l        |        |        |                      |          | Optimal      | 3              |
| connectedtosubgraphs{L(cid:48) |     |                  |        | ,...,L(cid:48) |           |      |                  |          |        | #GU=20 |                      |          |              |                |
|                                |     |                  |        |                |           | }⊂L  | i .Itimpliesthat |          |        |        |                      | Proposed |              | 3              |
|                                |     |                  |        | 1              | |Cl|−1    |      |                  |          |        |        |                      |          |              |                |
there are more than one user-representation node to select for Optimal 4
#GU=40
constructing I , and I . It is clear that when the number of Proposed 5
|     |     | m   | l   |     |     |     |     |     |     |     |     |     |         |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | --- |
|     |     |     |     |     |     |     |     |     |     |     |     |     | Optimal | 5   |
vertices in the graph D is finite, then the number of such #GU=60
|         |        |            |     |     |     |     |     |     |     |     |     | Proposed |     | 6   |
| ------- | ------ | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- | --- |
| induced | cycles | is finite. |     |     |     |     |     |     |     |     |     |          |     |     |
After removal of all induced cycles from D, independent TABLE III: Execution time (Optimal vs. Proposed algorithm)
| trees | will | compose | the | remaining | set. | As  | shown | in [46], |     |     |     |     |     |     |
| ----- | ---- | ------- | --- | --------- | ---- | --- | ----- | -------- | --- | --- | --- | --- | --- | --- |
we can select at least half of the nodes in each tree so Area size (sq. Km) Approach Time for execution (s)
|      |                |     |             |           |       |                |             |        |     |     | Optimal  |     |     | 36.67   |
| ---- | -------------- | --- | ----------- | --------- | ----- | -------------- | ----------- | ------ | --- | --- | -------- | --- | --- | ------- |
| that | they compose   |     | independent |           | sets. | An independent |             | set I∗ |     | 8 × | 8        |     |     |         |
|      |                |     |             |           |       |                |             |        |     |     | Proposed |     |     | 0.13    |
| can  | be constructed |     | from        | the union | of    | obtained       | independent |        |     |     |          |     |     |         |
|      |                |     |             |           |       |                |             |        |     |     | Optimal  |     |     | 1198.89 |
|      |                |     |             |           |       |                |             |        |     | 9 × | 9        |     |     |         |
sets with the cardinality of at least 1/2×|∪ i I i |, and thus Proposed 0.14
|I∗|≥|D|/4.
|              |           |                 |             |          |             |         |          |          |     |      | Optimal  |     |     | 22625.85 |
| ------------ | --------- | --------------- | ----------- | -------- | ----------- | ------- | -------- | -------- | --- | ---- | -------- | --- | --- | -------- |
|              |           |                 |             |          |             |         |          |          |     | 10 × | 10       |     |     |          |
|              |           |                 |             |          |             |         |          |          |     |      | Proposed |     |     | 0.16     |
| Similar      | to        | [46],           | theorem     | provided | as          | follows | can      | estimate |     |      |          |     |     |          |
| the Proposed |           | algorithm       | performance |          | guarantees. |         |          |          |     |      |          |     |     |          |
| Theorem      | 3.        | The cardinality |             | of the   | subset      | D       | computed | by the   |     |      |          |     |     |          |
| Proposed     | algorithm |                 | is at       | most     | 20OPT       | +4,     | where    | OPT      | is  |      |          |     |     |          |
| the size     | of        | an MCDS         | of          | G .      |             |         |          |          |     |      |          |     |     |          |
r
| Proof. | From | the Lemma |     | 2 and | 1, we | have |     |     |     |     |     |     |     |     |
| ------ | ---- | --------- | --- | ----- | ----- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
5.opt+1≥|MaximalIndependentSet|≥|I∗|≥|D|/4
⇒20.opt+4≥|D|.
|     |               | VIII. | SIMULATIONEXPERIMENTS |          |     |      |     |          |     |     |     |     |     |     |
| --- | ------------- | ----- | --------------------- | -------- | --- | ---- | --- | -------- | --- | --- | --- | --- | --- | --- |
| In  | this section, |       | we first              | showcase | how | well | the | Proposed |     |     |     |     |     |     |
algorithmperformscomparedtotheOptimalalgorithm(using
| ILP | solver) | for small | scenarios | only | (ILP | solver | takes | several |     |     |     |     |     |     |
| --- | ------- | --------- | --------- | ---- | ---- | ------ | ----- | ------- | --- | --- | --- | --- | --- | --- |
hours,ratherdays,torunforlargerscenarios.).Followingthis,
| we focus | on        | the performance |                     | analysis    |              | of the      | Proposed       | algo-   |     |     |     |     |     |     |
| -------- | --------- | --------------- | ------------------- | ----------- | ------------ | ----------- | -------------- | ------- | --- | --- | --- | --- | --- | --- |
| rithm    | against   | three           | comparison/baseline |             |              | algorithms, |                | namely, |     |     |     |     |     |     |
| Greedy   | algorithm |                 | (No backhaul        |             | constraint), |             | Backhaul-aware |         |     |     |     |     |     |     |
| Greedy   | (BaG)     | algorithm       |                     | and Random  |              | algorithm,  | for            | general |     |     |     |     |     |     |
| (larger) | scenarios |                 | in the              | rest of the | section.     |             |                |         |     |     |     |     |     |     |
A. ComparativeAnalysisofProposedandOptimalalgorithms
| Before  | we           | evaluate | the        | performance |            | of the | proposed | al-      |      |              |           |         |           |              |
| ------- | ------------ | -------- | ---------- | ----------- | ---------- | ------ | -------- | -------- | ---- | ------------ | --------- | ------- | --------- | ------------ |
| gorithm | for          | general  | simulation |             | scenarios, | we     | first    | showcase |      |              |           |         |           |              |
|         |              |          |            |             |            |        |          |          | Fig. | 3: Resultant | Multi-UAV | Network | topology: | (a) Proposed |
| how     | our Proposed |          | algorithm  |             | compares   | with   | the      | Optimal  |      |              |           |         |           |              |
algorithm (solved using ILP solver called Gurobi optimizer). and (b) Optimal algorithms. Red nodes are UAV candidate
|        |             |                |        |              |       |            |          |          | locations,    | while        | blue ones | are ground   | users. | Green and red     |
| ------ | ----------- | -------------- | ------ | ------------ | ----- | ---------- | -------- | -------- | ------------- | ------------ | --------- | ------------ | ------ | ----------------- |
| The    | experiments | are            | done   | for a        | small | scenario   | where    | the size |               |              |           |              |        |                   |
|        |             |                |        |              |       |            |          |          | edges         | respectively | represent | the backhaul |        | and access links. |
| of the | area        | is 9×9         | sq.    | Km, and      | the   | number     | of users | is 40.   |               |              |           |              |        |                   |
| The    | rest of     | the simulation |        | parameters   |       | are listed | in table | IV.      |               |              |           |              |        |                   |
| As     | shown       | in table       | II,    | the Proposed |       | algorithm  | utilizes | the      |               |              |           |              |        |                   |
|        |             |                |        |              |       |            |          |          | B. Simulation |              | Setting   |              |        |                   |
| same   | or slightly | higher         | number | of           | UAVs  | for        | forming  | a multi- |               |              |           |              |        |                   |
UAV networks compared to that of Optimal approach. Figure Unless otherwise stated, we consider a simulation area of
3 showsthe resultantMulti-UAV networkusing Proposedand size 50 km × 50 km with 200 ground users. The major
Optimal algorithms. These results show that the Proposed parameters of the simulation setting are listed in Table IV.
algorithm performs really well and is close to the Optimal The optimal altitude (h) for placing the UAVs, and its cor-
algorithm for smaller scenarios. respondingradiocoverageradiusonground(R)arecomputed
Moreover, table III shows the exponential time complex- as 1500 and 3300 m, respectively for a sub-urban area as per
ity of the Optimal algorithm for increasing area size (i.e., theseminalwork[7].RefertoTableIVfortheconsideredthe
increasing number of candidate locations). We can see that values of environmental parameters, LoS and NLoS system
running Optimal algorithm may take several hours for larger loss and other required parameters for calculating h and R.

9
TABLE IV: Simulation parameters Euclidean Minimum Spanning Tree (EMST)7 to determine
Parameters Value the minimum spanning tree of subset D where the weight
SimulationArea 50km∗50km of the edge between each pair of UAVs is the euclidean
NumberofUsers 200 distance between them. However, since the only possible 3D
|     |                    | Carrierfrequency(fc) |     |     | 2GHz  |      |     |           |          |           |           |      |               |             |              |
| --- | ------------------ | -------------------- | --- | --- | ----- | ---- | --- | --------- | -------- | --------- | --------- | ---- | ------------- | ----------- | ------------ |
|     |                    |                      |     |     |       |      |     | locations | for      | placement | of        | UAVs | are candidate |             | locations in |
|     |                    | LOSSystemLoss(ηL)    |     |     | 0.1dB |      |     |           |          |           |           |      |               |             |              |
|     |                    |                      |     |     |       |      |     | set K,    | the edge | set       | H in EMST |      | can not       | be directly | utilized     |
|     | NLOSSystemLoss(ηN) |                      |     |     |       | 21dB |     |           |          |           |           |      |               |             |              |
EnvironmentParameters(a,b) 4.88,0.429 for the placement of additional UAVs in order to ensure the
UAVTransmitPower(Pj)
|     |                           |           |     |     |            | 1W  |     | backhaul     | connectivity. |         | To address |           | this, we  | set the | weights of |
| --- | ------------------------- | --------- | --- | --- | ---------- | --- | --- | ------------ | ------------- | ------- | ---------- | --------- | --------- | ------- | ---------- |
|     |                           | Bandwidth |     |     | 15MHz      |     |     |              |               |         |            |           |           |         |            |
|     |                           |           |     |     |            |     |     | the existing | edges         | between |            | candidate | locations | as      | 1. Now for |
|     | NoisePowerSpectralDensity |           |     |     | -174dBm/Hz |     |     |              |               |         |            |           |           |         |            |
SNRThresholdforusercoverage(γ0) 4dB each selected edge e ∈ H (where j,k ∈ D), we utilize
jk
|     |     |     |     |     |     |     |     | Dijkstra’s | algorithm |               | to find | the     | shortest | path between | end        |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --------- | ------------- | ------- | ------- | -------- | ------------ | ---------- |
|     |     |     |     |     |     |     |     | nodes      | j and     | k. It returns | the     | minimum | number   | of           | additional |
Dˆ,
Using the Eq. 4, and 5, the UAV coverage radius R(cid:48) is candidate locations (relay nodes), denoted by that are
calculated. For instance, we observe that R(cid:48) ≈2.5∗R≈8.3 required to connect the end nodes of the selected edge e .
jk
γ(cid:48)
km when the backhaul SNR threshold, =15 dB. However, We repeat the process for all edges in set H and include
0
note that different γ(cid:48) will result in different R(cid:48), and is the additional candidate locations to the set Dˆ. Since there
0
calculated accordingly for each experiment. Also, since UAVs may be overlaps of candidate locations between two or more
are hovering over the air constantly, we considered a higher shortest paths for different edges in set H, we only include
SNR threshold to address the antenna pointing variations and the additional candidate locations for a certain path if those
improve the backhaul links. additional candidate locations are not already included in the
In our experiments, grounds users are randomly distributed set Dˆ. The set D∪Dˆ is the final solution of BaG algorithm.
inclusters,whereeachclusterhouses10−15groundusers,in 3) Random Algorithm: Random algorithm deploys UAVs
the considered simulation area. This is a realistic user distri- at randomly chosen candidate locations until and unless all
|           |      |                  |     |           |      |                 |     | ground | users | are covered |     | and the | deployed | UAVs | ensure |
| --------- | ---- | ---------------- | --- | --------- | ---- | --------------- | --- | ------ | ----- | ----------- | --- | ------- | -------- | ---- | ------ |
| bution in | case | of post-disaster |     | scenarios | [48] | or rural/remote |     |        |       |             |     |         |          |      |        |
areas [49], instead of completely random distribution of backhaul connectivity in the formed Multi-UAV Network.
| ground       | users in   | the entire | simulation |            | area usually | considered   |          |                 |        |         |           |     |        |        |           |
| ------------ | ---------- | ---------- | ---------- | ---------- | ------------ | ------------ | -------- | --------------- | ------ | ------- | --------- | --- | ------ | ------ | --------- |
| in the UAV   | literature | [34].      | In         | order      | to ensure    | the accuracy | of       |                 |        |         |           |     |        |        |           |
|              |            |            |            |            |              |              |          | D. Experimental |        | Results |           |     |        |        |           |
| the results, | we         | execute    | each       | experiment | 100          | times        | for each |                 |        |         |           |     |        |        |           |
|              |            |            |            |            |              |              |          | Varying         | number |         | of ground |     | users. | Fig. 4 | shows the |
algorithmandtaketheaveragevalueasthesimulationresults.
|               |       |           |            |            |              |         |           | impact        | of varying  | number |           | of ground | users    | on    | the number |
| ------------- | ----- | --------- | ---------- | ---------- | ------------ | ------- | --------- | ------------- | ----------- | ------ | --------- | --------- | -------- | ----- | ---------- |
| For extensive |       | analysis, | we         | evaluate   | the Proposed |         | algorithm |               |             |        |           |           |          |       |            |
|               |       |           |            |            |              |         | varying   | of required   | UAVs,       | under  | different |           | backhaul | SNR   | thresholds |
| against the   | other | three     | comparison | approaches |              | for (1) |           |               |             |        |           |           |          |       |            |
|               |       |           |            |            |              |         |           | γ(cid:48). In | particular, | we     | consider  | γ(cid:48) | as 10dB, | 15dB, | and 20dB   |
number of ground users, ranging from 50 - 500, (2) varying 0 0
areasizes,from(10km×10km)to(100km×100km),both and the corresponding results for each case is reported in
|             |          |     |             |     |         |       |        | Fig. 4 | (a), 4   | (b), and | 4              | (c) respectively. |           | The       | number of |
| ----------- | -------- | --- | ----------- | --- | ------- | ----- | ------ | ------ | -------- | -------- | -------------- | ----------------- | --------- | --------- | --------- |
| for varying | backhaul | SNR | thresholds, |     | from 10 | dB to | 20 dB. |        |          |          |                |                   |           |           |           |
|             |          |     |             |     |         |       |        | UAVs   | required | by       | all algorithms |                   | gradually | increases | with      |
increasingnumberofgroundusers,underanyconsideredvalue
|               |     |            |     |     |     |     |     | of γ(cid:48). | This is | because | more | UAVs | will be | required | to provide |
| ------------- | --- | ---------- | --- | --- | --- | --- | --- | ------------- | ------- | ------- | ---- | ---- | ------- | -------- | ---------- |
| C. Comparison |     | Algorithms |     |     |     |     |     | 0             |         |         |      |      |         |          |            |
wirelesscoveragetoincreasingnumberofusers(spreadoutin
1) GreedyAlgorithm(Nobackhaul): Greedyalgorithmhas multiple clusters in the area). Moreover, the number of UAVs
been proposed in the literature [50], [51] to determine the required by all algorithms (except for Greedy) increases with
| minimum | number | of  | UAVs | (and its | 3D placement) |     | required |            | γ(cid:48), |          |         |        |     |        |             |
| ------- | ------ | --- | ---- | -------- | ------------- | --- | -------- | ---------- | ---------- | -------- | ------- | ------ | --- | ------ | ----------- |
|         |        |     |      |          |               |     |          | increasing |            | even for | a fixed | number | of  | ground | users. This |
toprovidewirelesscoveragetoallgroundusers.Thealgorithm is because UAV coverage radius R(cid:48) decreases with increasing
| works in | the | following | manner: | The | algorithm | first | sorts | γ(cid:48)                                         |     |     |     |     |     |     |     |
| -------- | --- | --------- | ------- | --- | --------- | ----- | ----- | ------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
|          |     |           |         |     |           |       |       | 0 andtherefore,morenumberofUAVswouldberequiredfor |     |     |     |     |     |     |     |
the candidate locations K in the non-increasing order of the ensuring backhaul connectivity. Since Greedy does not ensure
number of ground users associated with different locations backhaul connectivity, the number of required UAVs in this
k ∈ K, i.e., ground user density. Denote Kˆ as the sorted list γ(cid:48).
|     |     |     |     |     |     |     |     | case remains |     | constant | and | does not | change | with changing |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------ | --- | -------- | --- | -------- | ------ | ------------- | --- |
0
of candidate locations. Then, the UAVs are placed sequen- The Proposed algorithm outperforms the other two
| tially at | candidate | locations | with | higher | user | density | until all |     |     |     |     |     |     |     |     |
| --------- | --------- | --------- | ---- | ------ | ---- | ------- | --------- | --- | --- | --- | --- | --- | --- | --- | --- |
backhaul-awarealgorithms,i.e.,BaGandRandom,forvarying
groundusersarecovered.Notethisalgorithmdoesnotalways number of ground users under all considered backhaul SNR
guarantee backhaul connectivity among UAVs. thresholds. The Proposed algorithm requires fewer number of
2) Backhaul-aware Greedy Algorithm (BaG): We extend UAVs by up to 15% and 95% compared to that of BaG and
Greedyalgorithmtoaccountforbackhaulconnectivityamong Random algorithm respectively. This shows the superiority
| UAVs, | which | we call | Backhaul-aware |     | Greedy | Algorithm |     |        |          |           |     |            |     |       |          |
| ----- | ----- | ------- | -------------- | --- | ------ | --------- | --- | ------ | -------- | --------- | --- | ---------- | --- | ----- | -------- |
|       |       |         |                |     |        |           |     | of the | Proposed | algorithm |     | in solving | the | BoaRD | problem, |
(BaG). The algorithm works as follows: i.e., optimizing the number and placement of UAVs while
| First, | BaG | utilizes | Greedy | Algorithm | to deploy |     | the min- |              |     |     |     |     |     |     |      |
| ------ | --- | -------- | ------ | --------- | --------- | --- | -------- | ------------ | --- | --- | --- | --- | --- | --- | ---- |
|        |     |          |        |           |           |     |          | 7Considering |     |     |     |     |     |     | Rd), |
imum number of UAVs at optimal 3D candidate locations a set of k points in the plane (or more generally in
|          |        |        |         |         |          |          |     | its Euclidean | minimum | spanning |              | tree (EMST) | is a    | minimum   | spanning tree, |
| -------- | ------ | ------ | ------- | ------- | -------- | -------- | --- | ------------- | ------- | -------- | ------------ | ----------- | ------- | --------- | -------------- |
| (denoted | as the | subset | D) that | ensures | wireless | coverage |     | to            |         |          |              |             |         |           |                |
|          |        |        |         |         |          |          |     | where the     | weight  | of the   | edge between | each        | pair of | points is | the Euclidean  |
all ground users. Following this, we utilize the concept of distancebetweenthosetwopoints.

10
Fig. 4: Number of UAVs needed vs. Number of ground users when SNR threshold γ(cid:48) is (a) 10dB, (b) 15dB, (c) 20dB
0
Fig. 5: Number of UAVs needed vs. Area sizes, when SNR threshold γ(cid:48) is (a) 10dB. (b) 15dB. (c) 20dB
0
| ensuring         | backhaul   | connectivity |                | and       | ground      | user           | coverage.      |           | It  |     |     |     |
| ---------------- | ---------- | ------------ | -------------- | --------- | ----------- | -------------- | -------------- | --------- | --- | --- | --- | --- |
| is noteworthy    |            | that         | the difference |           | in the      | number         |                | of UAVs   |     |     |     |     |
| required         | by the     | Proposed     |                | algorithm | and         | BaG            | is even        | larger    |     |     |     |     |
|                  | γ(cid:48). |              |                |           | γ(cid:48)   |                |                |           |     |     |     |     |
| for higher       |            | This         | is because     | when      |             | is high,       | UAVs           | have      |     |     |     |     |
|                  | 0          |              |                |           |             | 0              |                |           |     |     |     |     |
| to be placed     |            | close        | to each        | other     | to maintain |                | the successful |           |     |     |     |     |
| connection       | between    |              | UAVs           | (for      | backhaul    | connectivity), |                | and       |     |     |     |     |
| BaG necessitates |            | relatively   |                | large     | number      | of UAVs        | compared       |           |     |     |     |     |
| to that          | of the     | Proposed     | algorithm.     |           | For         | clarity        | of exposition, |           |     |     |     |     |
| we employ        | Fig.       | 6            | (a) and        | 6 (b)     | that        | depicts        | the            | resultant |     |     |     |     |
| UAV placement    |            | (and         | multi-UAV      |           | network)    | corresponding  |                |           | to  |     |     |     |
| the Proposed     |            | and BaG      | for            | a simple  | simulation  |                | setting        | with 60   |     |     |     |     |
| ground           | users      | in an        | area of        | 75 Km     | ×           | 75 Km.         | (We            | consider  |     |     |     |     |
60groundusersfortheclarityoftheplot.)HeretheProposed
| algorithm         | requires  | 40         | UAVs      | whereas    | BaG      | requires      | 50         | UAVs.      |     |     |     |     |
| ----------------- | --------- | ---------- | --------- | ---------- | -------- | ------------- | ---------- | ---------- | --- | --- | --- | --- |
| As                | expected, | the        | Greedy    | algorithm  |          | requires      | a          | relatively |     |     |     |     |
| smaller           | number    | of         | UAVs      | to ensure  | wireless |               | coverage   | to all     |     |     |     |     |
| ground            | users,    | for almost | all       | considered |          | cases         | in Fig     | 4. Note    |     |     |     |     |
| that Greedy       |           | does not   | guarantee |            | backhaul | connectivity, |            | and        |     |     |     |     |
| thus does         | not       | always     | provide   | a solution |          | to BoaRD      |            | problem.   |     |     |     |     |
| It is interesting |           | to         | note that | for        | lower    | SNR           | thresholds | such       |     |     |     |     |
| as 10             | dB (Fig.  | 4 (a))     | and       | 15 dB      | (Fig.    | 4 (b)),       | the        | Proposed   |     |     |     |     |
algorithm outperforms the Greedy algorithm by up to 13% Fig. 6: Resultant Multi-UAV Network topology: (a) Proposed
|        |           |             |     |       |       |     |             |     | and (b) BaG | algorithms. | Red nodes are UAV | candidate loca- |
| ------ | --------- | ----------- | --- | ----- | ----- | --- | ----------- | --- | ----------- | ----------- | ----------------- | --------------- |
| in the | reduction | of required |     | UAVs. | There | are | two reasons | for |             |             |                   |                 |
this.First,sincetheUAVcoverageradius(R(cid:48))islarge(dueto tions, while blue ones are ground users. Green and red edges
lowerSNRthresholds),negligiblenumberofadditionalUAVs respectively represent the backhaul and access links.
| are required |     | to ensure | backhaul |     | connectivity. |     | Second, | fewer |     |     |     |     |
| ------------ | --- | --------- | -------- | --- | ------------- | --- | ------- | ----- | --- | --- | --- | --- |
UAVsmayberequiredtoensuregroundusercoverageincase applying the Proposed algorithm, selected candidate locations
|     |     |     |     |     |     |     |     |     | will be {k | ,k }, while greedy | algorithm | selects {k ,k ,k }. |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ------------------ | --------- | ------------------- |
of the Proposed algorithm. Let us explain this with a simple 1 3 1 2 3
example. Assume 6 ground users {v ,...,v } ∈ V could Varying area sizes. Fig. 5 represents the variation of
|     |     |     |     |     | 1   | 6   |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
be covered by 3 UAV candidate locations {k ,k ,k } ∈ K number of required UAVs w.r.t varying size of areas under
|     |     |     |     |     |     |     | 1 2 | 3   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
γ(cid:48)
that are pairwise connected (backhaul connectivity ensured). various SNR thresholds, i.e., = 10dB, 15dB, and 20dB.
0
Assume {v ,v ,v }, {v ,v ,v ,v }, and {v ,v ,v } are in As expected, the number of UAVs required by all algorithms
|     | 1   | 2 3 | 2   | 3 4 | 5   | 4   | 5   | 6   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
γ(cid:48).
thecoverageareaofk 1 ,k 2 ,andk 3 respectively.Therefore,by increases with increasing area size, under all values of
0

11
This is intuitive as more UAVs will be required to provide [3] K. Hazra, V. K. Shah, S. Roy, S. Deep, S. Saha, and S. Nandi,
wireless coverage to users spread out in the larger area sizes “Exploringbiologicalrobustnessforreliablemulti-uavnetworks,”IEEE
Transactionson Networkand ServiceManagement, vol. 18, no.3, pp.
and maintain the backhaul connectivity. The number of UAVs
2776–2788,2021.
required by the Proposed algorithm is fewer than BaG and [4] B. Galkin, J. Kibilda, and L. A. DaSilva, “Backhaul for low-altitude
Random algorithms, respectively by up to 17% and 95%. The uavs in urban environments,” in 2018 IEEE International Conference
onCommunications(ICC),2018,pp.1–6.
Proposed algorithm significantly outperforms both backhaul-
[5] N. Iradukunda, Q.-V. Pham, M. Zeng, H.-C. Kim, and W.-J. Hwang,
awarealgorithms,i.e.,BaGandRandom,forthesamereasons “Uav-enabledwirelessbackhaulnetworksusingnon-orthogonalmultiple
discussed before that the Proposed algorithm solves BoaRD access,”IEEEAccess,vol.9,pp.36689–36698,2021.
[6] Y.Dai,Y.Guo,andJ.Hao,“Uavplacementandresourceallocationfor
problem efficiently.
multi-hop uav assisted backhaul system,” in IEEE INFOCOM 2021 -
Interestingly, compared to the Greedy algorithm, the Pro- IEEEConferenceonComputerCommunicationsWorkshops(INFOCOM
posed algorithm requires fewer number of UAVs for smaller WKSHPS),2021,pp.1–6.
area sizes (<50 km × 50 km) and lower γ(cid:48) (10 and 15 dB). [7] A.Al-Hourani,S.Kandeepan,andS.Lardner,“Optimallapaltitudefor
0 maximum coverage,” IEEE Wireless Communications Letters, vol. 3,
However, it gradually increases afterwards mainly because of
no.6,pp.569–572,2014.
theincreasednumberofUAVsrequiredforensuringbackhaul [8] C.-C. Lai, C.-T. Chen, and L.-C. Wang, “On-demand density-aware
connectivity. When the area becomes larger, the distances uav base station 3d placement for arbitrarily distributed users with
guaranteed data rates,” IEEE Wireless Communications Letters, vol. 8,
betweentheclusteroftheusersintheareaarelarger,andthus,
no.3,pp.913–916,2019.
more UAVs are needed to ensure the backhaul connectivity. [9] M.Alzenad,A.El-Keyi,F.Lagum,andH.Yanikomeroglu,“3-dplace-
Since, as discussed earlier, Greedy does not ensure backhaul ment of an unmanned aerial vehicle base station (uav-bs) for energy-
efficient maximal coverage,” IEEE Wireless Communications Letters,
connectivity, more UAVs are needed by Proposed and BaG
vol.6,no.4,pp.434–437,2017.
algorithms compared to Greedy approach in larger areas. [10] D.W.Matolak,“Air-groundchannels&models:Comprehensivereview
Also, larger γ(cid:48) values results in shorter backhaul links, which and considerations for unmanned aircraft systems,” in 2012 IEEE
0
AerospaceConference. IEEE,2012,pp.1–17.
increase the number of UAVs needed by Proposed and BaG
[11] A. Al-Hourani, S. Kandeepan, and A. Jamalipour, “Modeling air-to-
algorithmsincomparisontotheGreedyalgorithmtomaintain groundpath lossforlow altitudeplatformsinurban environments,”in
the backhaul connectivity. IEEEglobalcommunicationsconference. IEEE,2014,pp.2898–2904.
[12] D. W. Matolak and R. Sun, “Air–ground channel characterization for
IX. CONCLUSIONSANDFUTUREWORK unmannedaircraftsystems—parti:Methods,measurements,andmodels
for over-water settings,” IEEE Transactions on Vehicular Technology,
In this paper, we investigated the joint optimization of vol.66,no.1,pp.26–44,2016.
number, placement and backhaul connectivity of multi-UAV [13] E.Yanmaz,R.Kuschnig,andC.Bettstetter,“Achievingair-groundcom-
municationsin802.11networkswiththree-dimensionalaerialmobility,”
networks,suchthat,thenetworkprovideswirelesscoverageto
in2013ProceedingsIEEEINFOCOM. IEEE,2013,pp.120–124.
allgroundusersintheregionofoperation.Weformulatedthe [14] M.Mozaffari,W.Saad,M.Bennis,andM.Debbah,“Mobileunmanned
above problem, named, Backhaul-and-Coverage-aware Drone aerialvehicles(uavs)forenergy-efficientinternetofthingscommunica-
tions,”IEEETransactionsonWirelessCommunications,vol.16,no.11,
Deployment (BoaRD) problem as ILP problem and showed
pp.7574–7589,2017.
that it is NP-Hard. Utilizing graph theoretic concepts, we [15] R. I. Bor-Yaliniz, A. El-Keyi, and H. Yanikomeroglu, “Efficient 3-d
proposed a low computational complexity algorithm to solve placementofanaerialbasestationinnextgenerationcellularnetworks,”
in2016IEEEIntl.Conf.onComm.(ICC),May2016.
the BoaRD problem with provable performance guarantees.
[16] M. Mozaffari, W. Saad, M. Bennis, and M. Debbah, “Efficient de-
Our extensive simulations demonstrated the superiority of the ployment of multiple unmanned aerial vehicles for optimal wireless
Proposed algorithm in minimizing the number of UAVs to coverage,”IEEECommunicationsLetters,vol.20,no.8,pp.1647–1650,
2016.
formaMulti-UAVNetwork,whencomparedtobothbackhaul-
[17] E. Kalantari, H. Yanikomeroglu, and A. Yongacoglu, “On the number
awaregreedyandrandomalgorithmsforallconsideredscenar- and3dplacementofdronebasestationsinwirelesscellularnetworks,”
ios. Interestingly, the Proposed algorithm even outperformed in2016IEEE84thVehicularTechnologyConference(VTC-Fall). IEEE,
2016,pp.1–6.
thebaselinegreedyalgorithm(nobackhaul)forhigherground
[18] W. Wang, H. Dai, C. Dong, X. Cheng, X. Wang, P. Yang, G. Chen,
userdensityandlowerbackhaulSNRthresholds,whichfurther
and W. Dou, “Placement of unmanned aerial vehicles for directional
corroboratedtheefficacyoftheProposedalgorithm.Infuture, coveragein3dspace,”IEEE/ACMTransactionsonNetworking,vol.28,
we will explore the problem of UAV placement (with fewest no.2,pp.888–901,2020.
[19] C. You and R. Zhang, “3d trajectory optimization in rician fading for
number of UAVs) such that the formed Multi-UAV Network
uav-enabled data harvesting,” IEEE Transactions on Wireless Commu-
is resilient against various UAV node and link failures and nications,vol.18,no.6,pp.3192–3207,2019.
provides end-to-end wireless coverage to ground users in the [20] J.Cui,Z.Ding,Y.Deng,A.Nallanathan,andL.Hanzo,“Adaptiveuav-
trajectoryoptimizationunderqualityofserviceconstraints:amodel-free
region of operation. Another interesting future direction is
solution,”IEEEAccess,pp.1–14,2020.
to investigate designing the Multi-UAV Networks under very [21] J.Xiong,H.Guo,andJ.Liu,“Taskoffloadinginuav-aidededgecomput-
high mobility ground users. ing:Bitallocationandtrajectoryoptimization,”IEEECommunications
Letters,vol.23,no.3,pp.538–541,2019.
[22] X. Hu, K.-K. Wong, K. Yang, and Z. Zheng, “Uav-assisted relaying
REFERENCES
and edge computing: Scheduling and trajectory optimization,” IEEE
[1] M. Mozaffari, W. Saad, M. Bennis, Y.-H. Nam, and M. Debbah, “A Transactions on Wireless Communications, vol. 18, no. 10, pp. 4738–
tutorial on uavs for wireless networks: Applications, challenges, and 4752,2019.
open problems,” IEEE communications surveys & tutorials, vol. 21, [23] D. Huang, M. Cui, G. Zhang, X. Chu, and F. Lin, “Trajectory opti-
no.3,pp.2334–2360,2019. mization and resource allocation for uav base stations under in-band
[2] A. Ahmed, M. Awais, T. Akram, S. Kulac, M. Alhussein, and backhaul constraint,” EURASIP Journal on Wireless Communications
K. Aurangzeb, “Joint placement and device association of uav base andNetworking,vol.2020,no.1,pp.1–17,2020.
stations in iot networks,” Sensors, vol. 19, no. 9, 2019. [Online]. [24] Y.-C.Kuo,J.-H.Chiu,J.-P.Sheu,andY.-W.P.Hong,“Uavdeployment
Available:https://www.mdpi.com/1424-8220/19/9/2157 and iot device association for energy-efficient data-gathering in fixed-

12
wing multi-uav networks,” IEEE Transactions on Green Communica- [45] V.E.Brimkov,A.Leach,J.Wu,andM.Mastroianni,“Approximation
tionsandNetworking,pp.1–1,2021. algorithms for a geometric set cover problem,” Discrete Applied
[25] P. Pawar, S. M. Yadav, and A. Trivedi, “Performance study of dual Mathematics,vol.160,no.7,pp.1039–1052,2012.[Online].Available:
unmanned aerial vehicles with underlaid device-to-device communica- http://www.sciencedirect.com/science/article/pii/S0166218X11004768
tions,” Wireless Personal Communications, vol. 105, no. 3, pp. 1111– [46] S. Butenko, X. Cheng, C. A. Oliveira, and P. M. Pardalos, A New
1132,2019. Heuristic for the Minimum Connected Dominating Set Problem on Ad
|     |     |     |     |     |     |     |     | HocWirelessNetworks. | Boston,MA:SpringerUS,2004,pp.61–73. |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------------------- | ----------------------------------- | --- | --- |
[26] W.Yi,Y.Liu,M.Elkashlan,andA.Nallanathan,“Modelingandcover-
ageanalysisofdownlinkuavnetworkswithmmwavecommunications,” [Online].Available:https://doi.org/10.1007/978-1-4613-0219-3 4
in2019IEEEInternationalConferenceonCommunicationsWorkshops [47] K. M. Alzoubi, P.-J. Wan, and O. Frieder, “Distributed heuristics for
(ICCWorkshops). IEEE,2019,pp.1–6. connected dominating sets in wireless ad hoc networks,” Journal of
[27] H. Nguyen, H. Tuan, T. Duong, H. Poor, and W. Hwang, “Joint Communications and Networks, vol. 4, no. 1, pp. 22–29, Mar. 2002.
[Online].Available:http://ieeexplore.ieee.org/document/6596929/
| d2d | assignment, | bandwidth | and | power | allocation | in cognitive | uav- |     |     |     |     |
| --- | ----------- | --------- | --- | ----- | ---------- | ------------ | ---- | --- | --- | --- | --- |
enabled networks,” IEEE Transactions on Cognitive Communications [48] V.K.Shah,S.Roy,S.Silvestri,andS.K.Das,“Ctr:Clusterbasedtopo-
andNetworking,2020. logical routing for disaster response networks,” in IEEE International
[28] M. Banagar, V. V. Chetlur, and H. S. Dhillon, Stochastic Geometry- ConferenceonCommunications(ICC). IEEE,2017,pp.1–6.
BasedPerformanceAnalysisofDroneCellularNetworks. JohnWiley [49] V.K.Shah,S.Silvestri,B.Luciano,andS.K.Das,“X-chant:Adiverse
|     |     |     |     |     |     |     |     | dsa based architecture | for next-generation | challenged networks,” | in  |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------------- | ------------------- | --------------------- | --- |
&Sons,Ltd,2020,ch.9,pp.231–254.
IEEEINFOCOM2019-IEEEConferenceonComputerCommunications.
[29] J.Sabzehali,V.K.Shah,H.S.Dhillon,andJ.H.Reed,“3dplacement
and orientation of mmwave-based uavs for guaranteed los coverage,” IEEE,2019,pp.586–594.
IEEEWirelessCommunicationsLetters,vol.10,no.8,pp.1662–1666, [50] L. Zhang, Q. Fan, and N. Ansari, “3-d drone-base-station placement
within-bandfull-duplexcommunications,”IEEEComm.Lett.,vol.22,
2021.
no.9,pp.1902–1905,Sept.2018.
| [30] V. Mayor, | R.        | Estepa, | A. Estepa,    | and | G. Madinabeitia, |             | “Deploying |                                                                    |     |     |     |
| -------------- | --------- | ------- | ------------- | --- | ---------------- | ----------- | ---------- | ------------------------------------------------------------------ | --- | --- | --- |
|                |           |         |               |     |                  |             |            | [51] Q.FanandN.Ansari,“Towardstrafficloadbalancingindrone-assisted |     |     |     |
| a Reliable     | UAV-Aided |         | Communication |     | Service          | in Disaster | Areas,”    |                                                                    |     |     |     |
Wireless Communications and Mobile Computing, vol. 2019, pp. 1– communicationsforiot,”IEEEInternetofThingsJournal,vol.6,no.2,
| 20, Apr. | 2019. | [Online]. | Available: | https://www.hindawi.com/journals/ |     |     |     | pp.3633–3640,2019. |     |     |     |
| -------- | ----- | --------- | ---------- | --------------------------------- | --- | --- | --- | ------------------ | --- | --- | --- |
wcmc/2019/7521513/
| [31] E. Kalantari, |     | M. Z. Shakir, | H.  | Yanikomeroglu, |     | and A. | Yongacoglu, |     |     |     |     |
| ------------------ | --- | ------------- | --- | -------------- | --- | ------ | ----------- | --- | --- | --- | --- |
“Backhaul-awarerobust3ddroneplacementin5g+wirelessnetworks,”
| in 2017         | IEEE | international         | conference |     | on communications |     | workshops |     |     |     |     |
| --------------- | ---- | --------------------- | ---------- | --- | ----------------- | --- | --------- | --- | --- | --- | --- |
| (ICCworkshops). |      | IEEE,2017,pp.109–114. |            |     |                   |     |           |     |     |     |     |
[32] M.Nafees,J.Thompson,andM.Safari,“Multi-tiervariableheightuav
| networks: | User | coverage | and | throughput | optimization,” |     | IEEE Access, |     |     |     |     |
| --------- | ---- | -------- | --- | ---------- | -------------- | --- | ------------ | --- | --- | --- | --- |
vol.9,pp.119684–119699,2021.
| [33] N. Ansari, | Q.  | Fan, X. | Sun, and | L. Zhang, | “Soarnet,” | IEEE | Wireless |     |     |     |     |
| --------------- | --- | ------- | -------- | --------- | ---------- | ---- | -------- | --- | --- | --- | --- |
Communications,vol.26,no.6,pp.37–43,2019.
| [34] J. Lyu, | Y. Zeng, | R. Zhang, | and | T. J. Lim, | “Placement | optimization | of  |     |     |     |     |
| ------------ | -------- | --------- | --- | ---------- | ---------- | ------------ | --- | --- | --- | --- | --- |
UAV-mountedmobilebasestations,”IEEEComm.Lett.,vol.21,no.3,
pp.604–607,March2017.
[35] N.Nouri,J.Abouei,A.R.Sepasian,M.Jaseemuddin,A.Anpalagan,and
| K. N.            | Plataniotis, | “3d                 | multi-uav | placement | and      | resource  | allocation for |     |     |     |     |
| ---------------- | ------------ | ------------------- | --------- | --------- | -------- | --------- | -------------- | --- | --- | --- | --- |
| energy-efficient |              | iot communication,” |           | IEEE      | Internet | of Things | Journal,       |     |     |     |     |
pp.1–1,2021.
| [36] C. Zhang, | L.   | Zhang, L.    | Zhu,        | T. Zhang,       | Z. Xiao, | and X.-G. | Xia, “3d   |     |     |     |     |
| -------------- | ---- | ------------ | ----------- | --------------- | -------- | --------- | ---------- | --- | --- | --- | --- |
| deployment     | of   | multiple     | uav-mounted | base            | stations | for uav   | communi-   |     |     |     |     |
| cations,”      | IEEE | Transactions | on          | Communications, |          | vol. 69,  | no. 4, pp. |     |     |     |     |
2473–2488,2021.
| [37] N. Lin, | Y. Liu, | L. Zhao, | D. O. | Wu, and | Y. Wang, | “An | adaptive uav |     |     |     |     |
| ------------ | ------- | -------- | ----- | ------- | -------- | --- | ------------ | --- | --- | --- | --- |
deploymentschemeforemergencynetworking,”IEEETransactionson
WirelessCommunications,vol.21,no.4,pp.2383–2398,2022.
[38] M.Zhang,S.Fu,andQ.Fan,“Joint3ddeploymentandpowerallocation
| for uav-bs: | A   | deep reinforcement |     | learning | approach,” | IEEE | Wireless |     |     |     |     |
| ----------- | --- | ------------------ | --- | -------- | ---------- | ---- | -------- | --- | --- | --- | --- |
CommunicationsLetters,vol.10,no.10,pp.2309–2312,2021.
| [39] Q.-V. | Pham, | N. Iradukunda, |     | N. H. | Tran, W.-J. | Hwang, | and S.-H. |     |     |     |     |
| ---------- | ----- | -------------- | --- | ----- | ----------- | ------ | --------- | --- | --- | --- | --- |
Chung,“Jointplacement,powercontrol,andspectrumallocationforuav
wirelessbackhaulnetworks,”IEEENetworkingLetters,vol.3,no.2,pp.
56–60,2021.
| [40] T. M. | Nguyen,      | W. Ajib,           | and C.   | Assi,    | “A novel   | cooperative | noma for   |     |     |     |     |
| ---------- | ------------ | ------------------ | -------- | -------- | ---------- | ----------- | ---------- | --- | --- | --- | --- |
| designing  | uav-assisted |                    | wireless | backhaul | networks,” | IEEE        | Journal on |     |     |     |     |
| Selected   | Areas        | in Communications, |          | vol.     | 36, no.    | 11, pp.     | 2497–2507, |     |     |     |     |
2018.
[41] A.Fotouhi,H.Qiang,M.Ding,M.Hassan,L.G.Giordano,A.Garcia-
| Rodriguez, | and | J. Yuan, | “Survey | on  | uav cellular | communications: |     |     |     |     |     |
| ---------- | --- | -------- | ------- | --- | ------------ | --------------- | --- | --- | --- | --- | --- |
Practicalaspects,standardizationadvancements,regulation,andsecurity
challenges,”IEEECommunicationsSurveys&Tutorials,vol.21,no.4,
pp.3417–3442,2019.
| [42] N. R.R, | A. Gupta,   | G.       | Ghatak,       | A. Srivastava, | and        | V. A. Bohara,     | “Joint       |     |     |     |     |
| ------------ | ----------- | -------- | ------------- | -------------- | ---------- | ----------------- | ------------ | --- | --- | --- | --- |
| bandwidth    | and         | position | optimization  |                | in uav     | networks          | deployed for |     |     |     |     |
| disaster     | scenarios,” | in       | 2021 National |                | Conference | on Communications |              |     |     |     |     |
(NCC),2021,pp.1–6.
[43] B.Hu,L.Wang,S.Chen,J.Cui,andL.Chen,“Anuplinkthroughputop-
timizationschemeforuav-enabledurbanemergencycommunications,”
IEEEInternetofThingsJournal,pp.1–1,2021.
[44] G.Santos,J.Martins,A.Coelho,H.Fontes,M.Ricardo,andR.Campos,
“Afastgatewayplacementalgorithmforflyingnetworks,”in2021IEEE
93rdVehicularTechnologyConference(VTC2021-Spring),2021,pp.1–
6.