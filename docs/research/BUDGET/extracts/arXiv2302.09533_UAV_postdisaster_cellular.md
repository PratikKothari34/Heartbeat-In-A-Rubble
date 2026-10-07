> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> arXiv **2302.09533** - *UAV-aided post-disaster cellular networks*. Source PDF deleted after
> conversion.
>
> Listed in `docs/research/BUDGET/01-literature.md` deployment row 5 as **HELD**, no figure
> quoted. A post-disaster UAV deployment model. **Adjacent, not the same problem**: it restores
> *communications* coverage, whereas this project deploys *sensors*. Distinguish it rather than
> citing it as precedent for sensor deployment - the actual sensor-deployment prior art is
> Stewart et al. SEG 2016 and SeismicDart.

1
| UAV-Aided | Post-Disaster |          | Cellular | Networks: |
| --------- | ------------- | -------- | -------- | --------- |
| A Novel   | Stochastic    | Geometry |          | Approach  |
Maurilio Matracia, Mustafa A. Kishk, and Mohamed-Slim Alouini
3202 beF 91  ]YS.ssee[  1v33590.2032:viXra
Abstract
Motivatedbytheneedforubiquitousandreliablecommunicationsinpost-disasteremergencyman-
agementsystems(EMSs),weherebypresentanovelandefficientstochasticgeometry(SG)framework.
This mathematical model is specifically designed to evaluate the quality of service (QoS) experienced
by a typical ground user equipment (UE) residing either inside or outside a generic area affected by a
calamity. In particular, we model the functioning terrestrial base stations (TBSs) as an inhomogeneous
Poisson point process (IPPP), and assume that a given number of uniformly distributed unmanned
aerial vehicles (UAVs) equipped with cellular transceivers is deployed in order to compensate for the
damagesufferedbysomeoftheexistingTBSs.Thedownlink(DL)coverageprobabilityisthenderived
based on the maximum average received power association policy and the assumption of Nakagami-
m fading conditions for all wireless links. The proposed numerical results show insightful trends in
terms of coverage probability, depending on: distance of the UE from the disaster epicenter, disaster
radius, quality of resilience (QoR) of the terrestrial network, and fleet of deployed ad-hoc aerial base
stations (ABSs). The aim of this paper is therefore to prove the effectiveness of vertical heterogeneous
networks(VHetNets)inemergencyscenarios,whichcanbothstimulatetheinvolvedauthoritiesfortheir
| implementation | and inspire researchers | to further investigate | related problems. |     |
| -------------- | ----------------------- | ---------------------- | ----------------- | --- |
|                |                         | Index Terms            |                   |     |
Coverage analysis, stochastic geometry, binomial point process, UAVs, quality of resilience, post-
| disaster communications. |     |     |     |     |
| ------------------------ | --- | --- | --- | --- |
MaurilioMatraciaandMohamed-SlimAlouiniarewiththeComputer,Electrical,andMathematicalSciencesandEngineering
(CEMSE)DivisionatKingAbdullahUniversityofScienceandTechnology(KAUST),Thuwal,KingdomofSaudiArabia(KSA)
| (email: {maurilio.matracia; | slim.alouini}@kaust.edu.sa). |     |     |     |
| --------------------------- | ---------------------------- | --- | --- | --- |
Mustafa Kishk is with the Department of Electronic Engineering, National University of Ireland, Maynooth, W23 F2H6,
| Ireland (email: mustafa.kishk@mu.ie). |     |     |     |     |
| ------------------------------------- | --- | --- | --- | --- |

2
I. INTRODUCTION
Disasters represent of the main threats to modern communities, because they can potentially
compromise every form of life within the region involved, apart from the risk of damaging its
economy and cultural heritage. Contextually, the United Nations (UN) established the Interna-
tional Search and Rescue Advisory Group (INSARAG) in 1991 in order to essentially [1]:
(i) Improve the effectiveness of emergency preparedness and response operations;
(ii) Design activities that improve search-and-rescue (SAR) missions in disaster-prone countries;
(iii) Ameliorate cooperation among international urban-SAR (USAR) teams and develop proce-
dures and systems for national teams operating internationally;
(iv) Develop USAR procedures, guidelines and best practices for the emergency relief phase.
Emergency situations often require reliable cellular coverage over large areas to ensure the
safety of victims and first responders (FRs), especially during SAR missions. However, telecom
infrastructure dysfunction (e.g., failure or lack of power supply) is one of the main concerns
related to current network architectures. Indeed, the quality of telecommunications usually de-
creases after the occurrence of a disaster. Perturbations to the networking equipment can often
lead to continuous reconfiguration of the routing tables, a larger ratio of packet losses, distur-
bances to radio frequency (RF) signals, and many other issues [2], [3]. Consequently, ABSs
consisting of UAVs equipped with cellular transceivers are gaining more and more attention
as an alternative solution for supporting TBSs in post-disaster scenarios [3], [4]. The latter, in
fact, are generally susceptible to earthquakes, tornadoes, explosions, and many other serious
perturbations.
Apart from their mobility, using ABSs as ad-hoc nodes in emergency situations is also more
appropriate than using cell towers because of their lower cost, faster deployment, and higher
altitude [5]. By reaching a higher altitude, indeed, it is possible for a BS to achieve a larger
footprint as well as a higher probability of establishing line-of-sight (LoS) transmissions, which
can generally lead to better communication channels compared to the case of non-LoS (NLoS)
transmissions [6]. Furthermore, promising advancements in avionics and especially drone tech-
nology have enabled the use of such vehicles for several purposes (including disaster monitoring
[7], damage assessment [8], and first aid and supply delivery [9], for instance), although their
flight time is considerably reduced whenever operating in multi-task mode. However, there are
many types of vehicles that can be used as ABSs: these are usually categorized as low-altitude

3
platforms (LAPs) and high-altitude platforms (HAPs) [4]. Drones (either tethered [10], [11] or
untethered) and tethered balloons are common examples of LAPs, and usually their altitude
does not exceed 10km. On the other hand, airships, gliders, and untethered balloons fall in the
category of HAPs, since they are usually designed to operate in the stratosphere.
In this paper, we consider both LAPs and HAPs as a potential solution for supporting post-
disaster communications while capturing the resiliency of the terrestrial cellular infrastructure.
Given the inherent randomness of the network nodes’ deployment and resilience, for our analysis
we decided to implement an SG approach due to its tractability and accuracy.
More details on the contributions of this work are provided in Sec. I-B.
A. Related Works
This subsection provides a concise summary of the relevant literature works on UAV-assisted
disaster communications and SG-based analysis of UAV networks.
1) UAV-Aided Disaster Communications: As explained in [12], the importance of UAVs in
emergency scenarios is not limited to post-disaster situations but also concerns the phases of pre-
disaster preparedness and disaster assessment. Indeed, many works in the literature discussing
disaster communications have considered using UAVs for applications related to situational
awareness [13], damage assessment [14], and network rehabilitation [4], [15], [16]. Authors
in [13], in fact, approached the problem of situational awareness by deploying drones in order
to capture a digital terrain model and place sensors in a disaster-struck area, creating a dynamic
sensor network. On the other hand, [14] proposed combining UAV-based imagery with ground
observations and collaborative sharing with domain experts for either post-disaster assessment,
environmental management, or monitoring of infrastructure development. However, the most
interesting application for UAVs in disaster scenarios is probably to support or even substitute
the terrestrial cellular infrastructure, as respectively suggested in [15] and [16].
Finally, it is worth mentioning the current research interest in achieving UAVs’ minimum
energy consumption and optimal placement. For example, the work presented in [17] introduced
the first multi-layered heterogeneous network architecture that integrates ad hoc UAVs into
public safety communications; in particular, said architecture is expected to enable reliable
communications in basements by means of both wired and wireless links. On the other side,
in [18] a novel multi-objective integer linear optimization problem (ILP) was solved in order to

4
optimally deploy the UAVs assisting disaster-affected users; the authors compared the branch-
and-bound (B&B) algorithm with their proposed low-complexity heuristic one.
For a more detailed overview of this topic, the reader can refer to Ref. [3].
2) SG for UAV-Assisted Networks: During the last decade, SG has emerged in the literature as
one of the most effective mathematical tools for modeling and analyzing large scale VHetNets.
More specifically, the performances of UAV-assisted terrestrial cellular networks have been
evaluated via SG approaches in works such as [19]–[23].
Arshad et al. [19] proposed an architecture consisting of macro and small TBSs supported by
ABSs for evaluating the QoS experienced by either stationary or mobile users (by taking into
account the effect of handover rates). Moreover, a setup with TBSs and ABSs modeled by means
of distinct homogeneous Poisson point processes (HPPPs) was introduced in [20] in order to
derive both the coverage probability and average data rate experienced by a typical ground UE.
Following the same lines, in [21] we used two different Poisson point processes (PPPs) to model
the aerial and terrestrial nodes, and introduced specific features such as the aerial exclusion zone
and the inhomogeneous distribution of the TBSs’ density to accurately model comprehensive
environments that include both urban and exurban areas.
Furthermore, authors in [22] relied on SG to evaluate the effectiveness of ABSs, modeled as
a binomial point process (BPP), while taking into account also the backhaul probability. Finally,
we consider [23] as the most related work since it is the only one modeling also the resilience of
the terrestrial nodes, which is done by introducing a thinning probability for the PPP-distributed
TBSs. However, for the sake of simplicity, the latter work assumed the damages to spread over
the entire ground plane, which may not be accurate for typical post-disaster scenarios.
B. Contributions
The contributions of our paper involve multiple aspects, as explained in this subsection.
1) System Model: We consider a large-scale post-disaster wireless network consisting of both
terrestrial and aerial nodes. We devise accurate inhomogeneous PPPs (IPPPs) to model the planar
distribution of the functioning TBSs (that is, we assume that the original distribution is thinned
according to a certain probability depending on the distance from the disaster epicenter), both
inside and outside a circular disaster-struck zone, whereas the aerial network is modeled as a
BPP confined to the vertical projection of the disaster area.

5
Thus, the length of the disaster radius and the behavior of the QoR of the terrestrial network
represent crucial parameters since they allow to capture the severity of any catastrophic event [4].
This, in turn, has an influence on the optimal fleet of ABSs (identified by number and the type
of ad hoc nodes required to provide the highest QoS).
Inconclusion,weconsideroursystemmodelasacontributiontotheexistingliteraturebecause
it takes into account both the vertical heterogeneity (due to the presence of aerial and terrestrial
BSs) and the horizontal heterogeneity (due to the distribution of the surviving TBSs and the
consequent placement of the ABSs) of integrated post-disaster wireless networks in an original
way.
2) Performance Analysis: To the best of our knowledge, this paper provides the first SG-based
framework specifically designed to analyze the DL performances of 5G and beyond cellular
VHetNets affected by a localized disaster while taking into account the QoR of the terrestrial
infrastructure. Also, our framework is more general compared to the baseline ones [24], [25],
since it allows to evaluate the performance of the network even when the user is outside the
ground projection of the considered BPP’s domain.
More specifically, the devised framework introduces a new method that makes use of indicator
functions in order to avoid bulky piecewise expressions for describing the novel cumulative
distribution functions (CDFs), probability density functions (PDFs), and Laplace transforms of
the interference derived for each layer. In other words, compared to the methods available in the
literature [20], [21], [25], this one better conveys the meaning of the derived expressions and
eases their numerical implementation.
We applied our method to compute the spatial coverage probability (that is, we focus on
covering an area independently from the actual distribution of the users), and validated the
results via Monte Carlo simulations. In addition to better conveying the meaning of the derived
expressions and easing their numerical implementation, another advantage of our method is its
generality: indeed, the proposed expressions hold irrespective of the UE’s location, whereas the
conventional approaches would require different expressions depending on whether the typical
user resides inside or outside the disaster-struck area.
3) System-Level Insights: Several fruitful insights can be extracted by investigating the be-
havior of the coverage probability in response to the considered parameters. For example, the
obtained results show that the type and cardinality of a fleet of ABSs have a strong influence
on the coverage probability, and should be optimized based on topological aspects such as the

6
|     |     |     |     |     | TABLE | I   |     |     |     |
| --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- |
MAINSUBSCRIPTS
|     |     | Notation |     | Description |     |     |     | Definition |     |
| --- | --- | -------- | --- | ----------- | --- | --- | --- | ---------- | --- |
A
|     |     |     |      | ABSs           |             |         |     | —        |                  |
| --- | --- | --- | ---- | -------------- | ----------- | ------- | --- | -------- | ---------------- |
|     |     | T   |      | Functioning    | TBSs        |         |     | —        |                  |
|     |     | O   |      | Generic        | type of BSs |         |     | A⊕T      |                  |
|     |     | B   |      | Type of        | tagged BS   | B∈{A,T} |     | ∧ Q∗ >Q∗ | , ∀O(cid:54)=B   |
|     |     |     |      |                |             |         |     | B        | O                |
|     |     | C   | Type | of interfering | BSs         | C∈{A,T} | ∧   | Q <Q∗    | , ∀W (cid:54)=W∗ |
|     |     |     |      |                |             |         |     | C,Wi     | B i              |
state of the terrestrial infrastructure, the disaster radius, and the typical UE’s location. Indeed,
even when neglecting the strict technological and economic constraints (e.g., UAVs’ autonomy
and backhaul, as well as their availability and associated cost of deployment), exploiting dense
VHetNets imposes a trade-off between offering a strong desired signal and causing considerable
| interference | to    | the UE. |     |     |            |       |     |     |     |
| ------------ | ----- | ------- | --- | --- | ---------- | ----- | --- | --- | --- |
|              |       |         |     |     | II. SYSTEM | MODEL |     |     |     |
| A. Network   | Model |         |     |     |            |       |     |     |     |
We consider a post-disaster scenario where the DL cellular network infrastructure is affected
by a disaster, and thus a fleet of ad-hoc ABSs is deployed in order to make up for the failure
of some TBSs within the suffered region. For the sake of both conciseness and readability we
introduce a specific notation for the types of BSs, in accordance with Table I (where Q denotes
| the average | received | power |     | and W | the location | of the | BS). |     |     |
| ----------- | -------- | ----- | --- | ----- | ------------ | ------ | ---- | --- | --- |
Without any loss of generality, we set the origin O at the epicenter of the disaster. The
disaster area is assumed with altitude 0, circular with radius r , and can thus be expressed as
d
| A         |     | R2, |       | R2  |                  |        |     |        |     |
| --------- | --- | --- | ----- | --- | ---------------- | ------ | --- | ------ | --- |
| = b(O,0,r |     | ) ⊂ | where |     | is the Euclidean | ground |     | plane. |     |
| d         |     | d   | 0     | 0   |                  |        |     |        |     |
As in the absence of any calamity the TBSs’ planar distribution can generally be modeled
by means of an HPPP [20], [26] of intensity λ > 0, we hereby assume that the original
0
infrastructure experience random failures within the disaster-struck area. Therefore, the IPPP
R2
Φ ≡ {Y } ⊆ describes the surviving TBSs’ distribution; the intensity of this process is
| T   | i               | 0   |       |     |         |     |     |     |     |
| --- | --------------- | --- | ----- | --- | ------- | --- | --- | --- | --- |
|     | (cid:0) χ(r)1(r |     | )+1(r |     | (cid:1) |     |     |     |     |
λ (r)=λ ≤ r > r ) , where r > 0 represents the horizontal distance from
| T   | 0   |     | d   |     | d   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
the origin and χ(r) ∈ [0,1] identifies the QoR of the terrestrial network.

7
|     | Functioning  | Failed  |     |     |
| --- | ------------ | ------- | --- | --- |
TBS
TBS
𝒜
|     | Disaster  | UAV area  |     | ℎ   |
| --- | --------- | --------- | --- | --- |
|     | area (𝒜 ) |           |     |     |
|     | 𝑑         | (𝒜 ℎ )    |     |     |
|     | ABS       | Typical   |     |     |
user
ℎ
𝑶 𝑟
𝑢
[epicenter]
𝒜
𝑑
Fig.1. Schematicrepresentationofthesystemsetupconsidered:thetypicaluserislocatedatdistancer fromtheepicenterof
u
the disaster (i.e., the origin) and associates to the BS that provides the maximum average received power. All the failed TBSs
belong to a circular disaster-struck region A , whereas a fixed number of UAVs reside within its projection A .
d h
Finally, since the number of deployed UAVs decided by the authority is supposedly determin-
istic, the ABSs’ planar distribution is described by means of a uniform binomial point process
|     |     | }⊆A | A   |     |
| --- | --- | --- | --- | --- |
(BPP) Φ ≡ {X , where = b(O,h,r ) indicates the vertical projection at altitude h of
|     | A   | i h | h   | d   |
| --- | --- | --- | --- | --- |
A
(see Fig. 1). Although ABSs may definitely be subject to failures (especially in case of harsh
d
weather conditions), we henceforth consider them totally resilient, because their deployment
| would      | occur after | the actual | disaster. |     |
| ---------- | ----------- | ---------- | --------- | --- |
| B. Channel | model       |            |           |     |
This subsection aims to characterize both the terrestrial and aerial wireless channels. Keeping
in mind Table I, we assume that the signals transmitted by any BSs belonging to a given tier O
haveafixed,constanttransmitpowerρ andexperiencestandardpower-lawpathlosspropagation
O
| with | path loss exponent | α   | ≥2. |     |
| ---- | ------------------ | --- | --- | --- |
O
Let η denote the mean additional transmission losses, then we can define ξ = η ρ .
O O O
We assume both the terrestrial and aerial links experience small-scale fading in the form of
a Nakagami-m distribution with generic shape parameter m . Note that small-scale fadings
O

8
are usually Rayleigh or Rician distributed. However, the Nakagami-m distribution with shape
m = (K+1)2
parameter (and scale parameter equal to its reciprocal) allows a fair approximation
2K+1
of the Rician distribution with factor K [20]. For every W ∈ Φ , the channel fading power
|         |     |        |         |     |              |     |          |       | i   | O   |     |
| ------- | --- | ------ | ------- | --- | ------------ | --- | -------- | ----- | --- | --- | --- |
| gains G | ’s  | follow | a Gamma |     | distribution |     | with PDF | given | by  |     |     |
O,Wi
|     |     |     |     |     |     |       | mmO gmO−1 |     |        |     |     |
| --- | --- | --- | --- | --- | --- | ----- | --------- | --- | ------ | --- | --- |
|     |     |     |     | f   |     | (g) = | O         |     | e−mOg, |     | (1) |
GO,Wi
|     |     |     |     |     |     |     | Γ(m | )   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
O
∞
(cid:82)
| where Γ(m) | =   | xm−1e−xdx |     | identifies |     | the | Gamma | function. |     |     |     |
| ---------- | --- | --------- | --- | ---------- | --- | --- | ----- | --------- | --- | --- | --- |
0
For a given tier O, let Q denote the random variable referring to the average power received
O
by the typical UE. We define Q∗ and Q as the received powers coming from the closest
|     |     |     |     |     | O   | O,Wi |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- |
and any generic O-BSs located at point W , respectively. Thus, the random power received by
i
| the typical | user | from | a BS | located | at  | W can | be expressed |     | as  |     |     |
| ----------- | ---- | ---- | ---- | ------- | --- | ----- | ------------ | --- | --- | --- | --- |
i
D−αO,
|     |     |     | Q    | = ξ | G      | (1+D | )−αO | ≈   | ξ G    |     | (2) |
| --- | --- | --- | ---- | --- | ------ | ---- | ---- | --- | ------ | --- | --- |
|     |     |     | O,Wi |     | O O,Wi |      | Wi   |     | O O,Wi | Wi  |     |
where we introduced the modified path loss to formally avoid the absurdity Q > ξ ,
O,Wi O
|     |     | D < | 1m; |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
occurring for Wi nonetheless, we will (fairly) use the above approximation as we are
considering large scale networks. Finally note that if O = T then D = Ω .
Wi Wi
| C. Association |     | Policy |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- |
In this paper, the strongest average received power association rule is adopted, meaning that
the user connects to the BS providing the highest average received power. This, however, does
not exclude the possibility of having interferers providing higher received powers during a given
instant. Moreover, due to the fact that each type of BS is characterized by a specific path-loss
exponent, mean additional transmit losses, and transmit power, the serving BS is guaranteed to
| be the closest |     | BS but | only | among | the | BSs | of the same |     | type. |     |     |
| -------------- | --- | ------ | ---- | ----- | --- | --- | ----------- | --- | ----- | --- | --- |
(i.e.,
Finally, we assume the expected values of the fading gains over all the sets of BSs
E[G
],∀W ∈ Φ ) to equal 1. Hence, the location of the tagged BS will be simply provided
| O,Wi | i   | O   |     |     |     |     |     |     |     |     |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
DαO
| by the maximum |     | product | ξ   |     | , that | is  |     |     |     |     |     |
| -------------- | --- | ------- | --- | --- | ------ | --- | --- | --- | --- | --- | --- |
O O,Wi
|     |     |     | W∗  | =   | arg max(ξ |     | D−αO), | ∀O  | ∈ {A,T}. |     | (3) |
| --- | --- | --- | --- | --- | --------- | --- | ------ | --- | -------- | --- | --- |
O O,Wi
Wi∈ΦO
| D. Interference   |     | and | Signal-to-Interference-plus-Noise |     |              |     |     | Ratio | (SINR) |     |     |
| ----------------- | --- | --- | --------------------------------- | --- | ------------ | --- | --- | ----- | ------ | --- | --- |
| The instantaneous |     |     | SINR                              | can | be expressed |     | as  |       |        |     |     |
Q∗
|     |     |     |     |     |     | SINR | =   | B   | ,   |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- |
(4)
|     |     |     |     |     |     |     | σ2  | +I  |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
n

9
where σ2 is the additive white Gaussian noise (AWGN) power and I is the aggregate interference
n
C
power. Letting denote the layer hosting each interfering BS and assuming that all BSs share
the same frequency or time resource blocks, then the random variable (RV) I can be introduced
as
(cid:88) (cid:88)
|     |     |     | I = |     | Q . |     | (5) |
| --- | --- | --- | --- | --- | --- | --- | --- |
C,Wi
|     |     |     |     | C={A,T} Wi∈ΦC |     |     |     |
| --- | --- | --- | --- | ------------- | --- | --- | --- |
Wi(cid:54)=W∗
| E. Coverage | Probability |     |     |     |     |     |     |
| ----------- | ----------- | --- | --- | --- | --- | --- | --- |
The coverage probability is defined as the complementary cumulative distribution function
(CCDF) of the SINR evaluated at a designated threshold τ ensuring reliable decoding, that is
|     |     |     | P   | = P(SINR | > τ). |     | (6) |
| --- | --- | --- | --- | -------- | ----- | --- | --- |
c
|     |     |     | III. PERFORMANCE |     | ANALYSIS |     |     |
| --- | --- | --- | ---------------- | --- | -------- | --- | --- |
In this section, the distributions of the distance to the closest O-BS, the association proba-
bilities, and the conditional Laplace transforms of the interference will be derived for both the
aerial and terrestrial layers of BSs in order to obtain the approximate and exact expressions of
| the coverage | probability. |              |     |     |     |     |     |
| ------------ | ------------ | ------------ | --- | --- | --- | --- | --- |
| A. Distance  | to the       | Nearest O-BS |     |     |     |     |     |
Intuitively, the coverage probability is a function of the distance between the UE and the
tagged BS. In order to derive the exact and approximate expressions of the coverage probability,
the theorems in this subsection characterize the distribution of the horizontal distance between
the UE and each closest O-BS by computing its CDF. Consequently, the respective PDF will be
| derived | in a corollary. |     |     |     |     |     |     |
| ------- | --------------- | --- | --- | --- | --- | --- | --- |
Theorem 1. Let r be the distance between the typical user and the center of a disaster with
u
radius r , then the CDF of the random horizontal distance1 Z between the UE and the closest
d T
| TBS in | an IPPP with | density | λ (r) is | given by |     |     |     |
| ------ | ------------ | ------- | -------- | -------- | --- | --- | --- |
T
2π z
|     |     |     |     | (cid:18) (cid:90) (cid:90) |     | (cid:19) |     |
| --- | --- | --- | --- | -------------------------- | --- | -------- | --- |
(cid:0) (cid:1)
|     |     | F (z) | =1−exp | −   | λ r (ω,β) ωdωdβ | ,   | (7) |
| --- | --- | ----- | ------ | --- | --------------- | --- | --- |
|     |     | ZT    |        |     | T Ω             |     |     |
0 0
1Whenever
not specified, we always refer to the distance from the typical UE, around which the polar coordinate system
(ω,β) is centered.

10
(cid:112)
where r (ω,β) = r2 +ω2 −2r ω cosβ describes the ground distance from the origin.
| Ω   |     |     |     | u   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
u
| Proof: | See Appendix |     | A.  |     |     |     |     |
| ------ | ------------ | --- | --- | --- | --- | --- | --- |
Henceforth,lettheoverlinecharacterizethecomplementaryfunctions(i.e.,F¯
| Corollary1. |     |     |     |     |     |     | (z) = |
| ----------- | --- | --- | --- | --- | --- | --- | ----- |
ZO
1−F (z)). The PDF of the distance Z between the UE and the closest surviving TBS is
| ZO  |     |     |     |     | T   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
(cid:90) 2π
|     |     |     |       | zF¯ |       | (cid:0) (cid:1) |     |
| --- | --- | --- | ----- | --- | ----- | --------------- | --- |
|     |     |     | f (z) | =   | (z) λ | r (z,β) dβ.     | (8) |
|     |     |     | ZT    |     | ZT    | T Ω             |     |
0
| Proof: | See Appendix |     | B.  |     |     |     |     |
| ------ | ------------ | --- | --- | --- | --- | --- | --- |
Due to the inherent complexity of the BPP, the distance distribution to the closest ABS cannot
be computed directly. Therefore, as an intermediate step, we now leverage a well-known property
of BPPs in order to obtain the distribution of the horizontal distance Ω between the UE and
A
any ABS.
Proposition 1. For a given set of N points uniformly distributed over an area A, the points
(cid:0) (cid:1)
residing in any subarea Σ ⊆ A are uniformly distributed with cardinality n ∼ Bin N, Σ [27,
A
| Theorem | 2.9]. |     |     |     |     |     |     |
| ------- | ----- | --- | --- | --- | --- | --- | --- |
Lemma 1. In accordance to [25, Lemma 1], the horizontal distances Ω ’s to the set of inde-
A
pendently and uniformly distributed UAVs are independent and identically distributed (iid), with
| the CDF | and PDF | of each | element | respectively | given | by  |     |
| ------- | ------- | ------- | ------- | ------------ | ----- | --- | --- |
Σ(ω)
|     |     |     |     | F   | (ω) = | ,   | (9) |
| --- | --- | --- | --- | --- | ----- | --- | --- |
|     |     |     |     |     | ΩA    | A   |     |
d
and
1 dΣ(ω)
|     |     |     |     | f   | (ω) = | ,   | (10) |
| --- | --- | --- | --- | --- | ----- | --- | ---- |
ΩA
|     |     |     |     |     | A   | dω  |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
d
|     | (cid:82) 2π | (cid:82) ω 1(cid:0) |     | (cid:1) |     |     |     |
| --- | ----------- | ------------------- | --- | ------- | --- | --- | --- |
in which Σ(ω) = r (ω(cid:48),β)<r ω(cid:48)dω(cid:48)dβ describes the intersection area between A
|     |     |     | Ω   | d   |     |     | d   |
| --- | --- | --- | --- | --- | --- | --- | --- |
|     | 0   | 0   |     |     |     |     |     |
(cid:82) 2π 1(cid:0) (cid:1)
and the disc of radius ω centered around the UE, and dΣ(ω) = ω r (ω,β)<r dβ.
Ω d
dω
0
Proof: The expression of dΣ(ω) can be easily derived by applying the Leibniz rule to Σ(ω).
dω
These latter results allow us to extract the distribution of the respective minimum horizontal
| distance | Z , as shown | in  | what follows. |     |     |     |     |
| -------- | ------------ | --- | ------------- | --- | --- | --- | --- |
A

11
|     |     |     |     |                             |     | TABLE | II  |     |     |     |     |     |
| --- | --- | --- | --- | --------------------------- | --- | ----- | --- | --- | --- | --- | --- | --- |
|     |     |     |     | MINIMUMINTERFERERDISTANCESD |     |       |     |     | (z) |     |     |     |
BC
C
|     |     |     |     |     | T   |     |     |     | A   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
B

|     |     |     |     |      |          |     | ξ  | 1 α T     |          |        |     |     |
| --- | --- | --- | --- | ---- | -------- | --- | ---- | --------- | -------- | ------ | --- | --- |
|     |     |     |     |      |          |     | A    | α A zα A  | , if z>D | AT (0) |     |     |
|     |     |     | T   |      | z        |     | ξ T  |           |          |        |     |     |
|     |     |     |     |      |          |     | h, | otherwise |          |        |     |     |
|     |     |     |     |      | 1 √      | α A |      | √         |          |        |     |     |
|     |     |     | A   | ξT α | ( z2+h2) | α   |      |           | z2+h2    |        |     |     |
|     |     |     |     | ξA   | T        | T   |      |           |          |        |     |     |
Theorem 2. Let N denote the number of deployed UAV-mounted BSs, then the CDF of the
A
| closest | horizontal | distance |     | to a | UAV is | [24]             |     |     |     |     |     |      |
| ------- | ---------- | -------- | --- | ---- | ------ | ---------------- | --- | --- | --- | --- | --- | ---- |
|         |            |          |     |      | F      | (z) = 1−F¯NA(z). |     |     |     |     |     | (11) |
ZA
ΩA
| Proof: |       | Z   | = min{Ω |     | },   |        |        |     |        |     |     |     |
| ------ | ----- | --- | ------- | --- | ---- | ------ | ------ | --- | ------ | --- | --- | --- |
|        | Since |     | A       | A,i | then | we can | derive | its | CDF as |     |     |     |
i
|     |     |     |       | P(Z |      | 1−P(cid:0) |       |     | (cid:1) 1−F¯NA(z). |     |     |     |
| --- | --- | --- | ----- | --- | ---- | ---------- | ----- | --- | ------------------ | --- | --- | --- |
|     |     | F   | (z) = | ≤   | z) = |            | min{Ω | }   | > z =              |     |     |     |
|     |     | ZA  |       |     |      |            |       | A,i |                    | ΩA  |     |     |
i
| Corollary | 2.  | The PDF | of  | the closest | ground | distance     |     | to a | UAV is |     |     |      |
| --------- | --- | ------- | --- | ----------- | ------ | ------------ | --- | ---- | ------ | --- | --- | ---- |
|           |     |         |     | f           | (z) =  | N F¯NA−1(z)f |     |      | (z).   |     |     |      |
|           |     |         |     |             | ZA     | A            |     | ΩA   |        |     |     | (12) |
ΩA
Proof: The result trivially follows from taking the derivative of F (z) with respect to z.
ZA
| B. Association |     | Probabilities |     |     |     |     |     |     |     |     |     |     |
| -------------- | --- | ------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
The B-association probability quantifies the likelihood that the UE associates to an B-BS.
Based on our assumptions, this can be computed as the probability that the maximum average
received power comes from the closest B-BS, as conveyed in the following theorem.
Theorem 3. Recalling the subscripts defined in Table I, we denote as D (z) the minimum Eu-
BC
clidean distance of any C-interferer if the user associates to a B-BS situated at ground distance

(cid:112)
|     |     |     |     |    | D2 (z)−h2, |     | C   | = A |     |     |     |     |
| --- | --- | --- | --- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |    |            |     | if  |     |     |     |     |     |
BC
| z. Consequently, |     | Z   | (z) | =   |     |     |     |     | expresses | the horizontal | projection |     |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- | --------- | -------------- | ---------- | --- |
BC
|     |     |     |     |  D | (z), |     | C   | = T |     |     |     |     |
| --- | --- | --- | --- | ---- | ---- | --- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |      | BC   |     | if  |     |     |     |     |     |

12
|     |     |     |     |     |     | ℎ 𝐷 |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
𝑍
|     |     | 𝑶           |     | 𝑟   |     |     | 𝑼𝓩   | (𝑍) |     |
| --- | --- | ----------- | --- | --- | --- | --- | ---- | --- | --- |
|     |     |             |     | 𝑢   |     |     |      | 𝐵𝐶  |     |
|     |     | [epicenter] |     |     |     |     | [UE] |     |     |
Fig.2. GenericrepresentationoftheminimuminterfererhorizontaldistanceZ (Z)inrelationtotheEuclideanandhorizontal
BC
distancestotheclosestB-BS.Notealsothat,forthesakeofaneasierrepresentation,theminimuminterfererdistanceD (Z)
BC
has been omitted.
|     |     |     |     | R   | (cid:2) | (cid:2) | R   | (cid:2) | (cid:3) |
| --- | --- | --- | --- | --- | ------- | ------- | --- | ------- | ------- |
of D (z) (see Fig. 2). Let r± = r ±r , = 0,∞ , and = max(0,−r−),r+ ,2 then
| BC                 |     |             | d      | u         | T   |     | A   |     |     |
| ------------------ | --- | ----------- | ------ | --------- | --- | --- | --- | --- | --- |
| each B-association |     | probability | can be | expressed | as  |     |     |     |     |
(cid:90)
|     |     |     | A   | =   | f (z)a | (z)dz, |     |     | (13) |
| --- | --- | --- | --- | --- | ------ | ------ | --- | --- | ---- |
|     |     |     | B   |     | ZB     | B      |     |     |      |
R
B
|     |     | (cid:81) F¯ (cid:0) | (cid:1) |     |     |     |     |     |     |
| --- | --- | ------------------- | ------- | --- | --- | --- | --- | --- | --- |
where a (z) = Z (z) represents the association probability conditioned on the
| B   |     | ZC  | BC  |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
C(cid:54)=B
association to a B-BS, which we refer to as the conditional B-association probability.
| Proof:         | See Appendix | C.         |     |                  |     |     |     |     |     |
| -------------- | ------------ | ---------- | --- | ---------------- | --- | --- | --- | --- | --- |
| C. Conditional | Laplace      | Transforms | of  | the Interference |     |     |     |     |     |
Assuming that all BSs operate within the same frequency band, it follows that co-channel
interference is generated by each BS except the tagged one. Therefore, it is possible to charac-
terize the interference statistics by computing the Laplace transform of the RV I, which denotes
the aggregate interference. To this extent, the theorems in this subsection preliminary provide
the expressions of the conditional Laplace transforms of the interference generated by each tier
| of base stations | (BSs). |     |     |     |     |     |     |     |     |
| ---------------- | ------ | --- | --- | --- | --- | --- | --- | --- | --- |
2It is evident that the first argument of max(x,y) is chosen if and only if the user is located inside A .
d

13
Again, the first result we propose refers to the working TBSs, now considered as interferers
| in the | following | theorem. |     |     |     |     |     |     |     |     |     |     |     |
| ------ | --------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Theorem 4. By recalling the expression of r (ω,β) from Theorem 1, the conditional Laplace
Ω
| transform | of  | the interference |     | due | to TBSs  | can  | be expressed |     | as  |     |     |          |     |
| --------- | --- | ---------------- | --- | --- | -------- | ---- | ------------ | --- | --- | --- | --- | -------- | --- |
|           |     |                  |     |     | (cid:18) | 2π ∞ |              |     |     |     |     | (cid:19) |     |
(cid:90) (cid:90)
|     |     |     |       |       |     |     | (cid:0) |        | (cid:1) |               |     |     |      |
| --- | --- | --- | ----- | ----- | --- | --- | ------- | ------ | ------- | ------------- | --- | --- | ---- |
|     |     | L   | (s|z) | = exp | −   |     | λ r     | (ωˇ,β) | I       | (s|ωˇ)ωˇdωˇdβ |     | ,   | (14) |
|     |     | IBT |       |       |     |     | T       | Ω      | T       |               |     |     |      |
0 ZBT(z)
|       |         |      | (cid:16) |     | (cid:17)mT |     |     |     |     |     |     |     |     |
| ----- | ------- | ---- | -------- | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- |
| where | I (s|ω) | = 1− |          | mT  |            | .   |     |     |     |     |     |     |     |
T
mT+ξTsω−αT
| Proof: |     | See Appendix |     | D.  |     |     |     |     |     |     |     |     |     |
| ------ | --- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Again, due to the greater complexity of the BPP compared to the PPP, an intermediate step is
required to obtain the conditional Laplace transform of the interference coming from the aerial
nodes. To this extent, the following lemma defines the expression of the PDF of the horizontal
Ωˇ
| distance |     | between | the | UE and | any interfering |     | ABS. |     |     |     |     |     |     |
| -------- | --- | ------- | --- | ------ | --------------- | --- | ---- | --- | --- | --- | --- | --- | --- |
A
Ωˇ
Lemma 2. Let r+ = r +r , then the aerial interferers’ horizontal distances ’s constitute
|              |     |        | d       | u    |     |           |     |     |     |     |     | A,i |     |
| ------------ | --- | ------ | ------- | ---- | --- | --------- | --- | --- | --- | --- | --- | --- | --- |
| an unordered |     | set of | iid RVs | with | PDF | expressed | as  |     |     |     |     |     |     |
f (ωˇ)
|     |     |     |     |     |           |     | ΩA     |       | r+.  |     |     |     |      |
| --- | --- | --- | --- | --- | --------- | --- | ------ | ----- | ---- | --- | --- | --- | ---- |
|     |     |     |     | f   | Ωˇ (ωˇ|z) | =   |        | , z ≤ | ωˇ ≤ |     |     |     | (15) |
|     |     |     |     |     | A         |     | F¯ (z) |       |      |     |     |     |      |
ΩA
Proof: Let us preliminarily define n = 1+1(B = A) and Nˇ = N −1(B=A). Then,
|     |     |     |     |     |     | 1   |     |     |     | A   | A   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
the conditional joint PDF of the aerial interferers’ horizontal distances is
N
(cid:81)A
|     |     |      |             |     | N          | !f  | (z)     | f                | (ωˇ ) |         |            |       |      |
| --- | --- | ---- | ----------- | --- | ---------- | --- | ------- | ---------------- | ----- | ------- | ---------- | ----- | ---- |
|     |     |      |             |     |            | A   | ΩA      | ΩA               | i     |         | NA         |       |      |
|     |     |      |             |     |            |     |         |                  |       |         | (cid:89) f | (ωˇ ) |      |
|     |     | f    | (ωˇ ,...,ωˇ |     | |z) ( = a) |     | i=n1    |                  | ( =   | b) Nˇ ! | ΩA         | i ,   | (16) |
|     |     | Ωˇ   | n1          | NA  |            |     |         |                  |       | A       |            |       |      |
|     |     | BA,i |             |     |            |     | (z)F¯ 1 | (B(cid:54)=A)(z) |       |         | F¯         | (z)   |      |
|     |     |      |             |     |            | f   |         |                  |       |         |            | ΩA    |      |
|     |     |      |             |     |            | ZA  | Ω A     |                  |       | i=n1    |            |       |      |
where (a) follows from the joint PDF for the order statistics of a sample of size N drawn from
A
the distribution of Ω [25, Appendix C], and (b) follows by expressing the term f (z) as in
|     |     |     | A   |     |     |     |     |     |     |     |     | ZA  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(12). By recalling [24, Lemma 3], we notice that the factorial term (N −1)! indicates all possible
A
permutations of the elements in the ordered set of the aerial interferers’ horizontal distances. As
a result, by the joint PDF of the ground distances in the ordered set, the corresponding ground
| distances | in  | the unordered |     | set are | iid with | PDF | given | by  | (15). |     |     |     |     |
| --------- | --- | ------------- | --- | ------- | -------- | --- | ----- | --- | ----- | --- | --- | --- | --- |
As already anticipated, we can now express the conditional Laplace transform of the aerial
| interference |     | by means | of  | the following |     | theorem. |     |     |     |     |     |     |     |
| ------------ | --- | -------- | --- | ------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- |

14
Theorem 5. The conditional Laplace transform of the interference due to the ABSs in the case
| of B-association |     |     | can be | expressed |     | as  |     |     |     |     |     |     |     |
| ---------------- | --- | --- | ------ | --------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ΥˇNˇ
|     |     |     |     |     |     | L   | (s|z) | =   | A(s,z), |     |     |     | (17) |
| --- | --- | --- | --- | --- | --- | --- | ----- | --- | ------- | --- | --- | --- | ---- |
IBA
BA
|       |            |          | r +      |     |         |         |      |         |      |          | (cid:16) |          | (cid:17)mA |
| ----- | ---------- | -------- | -------- | --- | ------- | ------- | ---- | ------- | ---- | -------- | -------- | -------- | ---------- |
|       |            |          | (cid:82) |     |         | (cid:0) |      | (cid:1) |      |          |          |          |            |
| where | Υˇ (s,z)   | =        |          | I   | (s|ωˇ)f |         | ωˇ|Z | (z) dωˇ | with | I (s|ωˇ) | =        | mA       | .          |
|       | BA         |          |          | A   |         | Ωˇ      | BA   |         |      | A        |          | − αA(ωˇ) |            |
|       |            |          |          |     |         | A       |      |         |      |          | mA+ξAsD  |          |            |
|       |            |          | ZBA(z)   |     |         |         |      |         |      |          |          | A A      |            |
|       | Proof: See | Appendix |          | E.  |         |         |      |         |      |          |          |          |            |
To conclude, the following corollary defines the conditional Laplace transform of the aggregate
interference.
Corollary 3. The conditional Laplace transform of the aggregate interference can be expressed
as
(cid:89)
|     |     |     |     |     | L   | (s|z) | =   |     | L   | (s|z). |     |     | (18) |
| --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | ------ | --- | --- | ---- |
|     |     |     |     |     |     | I,B   |     |     | IBC |        |     |     |      |
C={A,T}
Proof: The proof trivially follows by recalling that the aggregate interference is the sum of
| the interferences |     | coming      |     | from | each | layer. |     |     |     |     |     |     |     |
| ----------------- | --- | ----------- | --- | ---- | ---- | ------ | --- | --- | --- | --- | --- | --- | --- |
| D. Coverage       |     | Probability |     |      |      |        |     |     |     |     |     |     |     |
Based onthe expressions derivedfor the PDFs of thedistance to theclosest BS, theconditional
association probabilities, the SINR, and the Laplace transform of the interference, we hereby
provide the exact and approximate expressions of the coverage probability under Nakagami-m
fading conditions.
Theorem 6. Letp (z)denotethe exactcoverage probabilityconditioned ontheassociation toa
c,B
R
B-BS located at horizontal distance z within its own planar domain defined as in Theorem 3.
B
Then, the exact coverage probability for a typical user in the wireless system described in
| Section | II is | given | by  |     |     |     |     |     |     |     |     |     |     |
| ------- | ----- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:90)
(cid:88)
|     |     |     |     | P   | =   |     | a   | (z)p  | (z)f | (z)dz, |     |     | (19) |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | ---- | ------ | --- | --- | ---- |
|     |     |     |     |     | c   |     |     | B c,B |      | ZB     |     |     |      |
B={A,T}R
B
where
|     |     |     |     |     |               | (cid:0) |     | (cid:1)k |     |          |     |     |     |
| --- | --- | --- | --- | --- | ------------- | ------- | --- | -------- | --- | -------- | --- | --- | --- |
|     |     |     |     |     | m (cid:88)B−1 |         | −µ  | (z)      | ∂k  | (cid:12) |     |     |     |
B
|     |     |     |     | p (z) | =   |     |     |     | L   | (s|z) (cid:12) |     |     | (20) |
| --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | -------------- | --- | --- | ---- |
|     |     |     |     | c,B   |     |     |     |     |     | J,B (cid:12)   |     |     |      |
|     |     |     |     |       |     |     | k!  |     | ∂sk | s=µB(z)        |     |     |      |
k=0

15
with L (s|z) = e−sσ 2 L (s|z) and µ (z) = m τ D αB (z). The expressions of the functions
|     | J,B |     | n   | I,B | B   | B   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ξ B B B
f (z)’s are provided in Corollaries 1 and 2; the general expression of the association proba-
ZB
bilities a (z)’s is given by Theorem 3; the functions L (s|z)’s respectively refer to Theorems 4
|     | B   |     |     |     |     | I,B |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
and 5.
|     | Proof: See | Appendix |     | F.  |     |     |     |     |     |     |
| --- | ---------- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
Since computing the exact expression of the conditional coverage probability may require
computing high-order derivatives of the conditional Laplace transform of the interference, it is
usually preferable to approximate it, as suggested by the following theorem.
Theorem 7. To ease the evaluation of the coverage probability, the conditional coverage prob-
| ability | can be | approximated |     | as [20,  | Sec. III-D]       |     |         |         |         |      |
| ------- | ------ | ------------ | --- | -------- | ----------------- | --- | ------- | ------- | ------- | ---- |
|         |        |              |     | mB       | (cid:18) (cid:19) |     |         |         |         |      |
|         |        |              |     | (cid:88) | m                 |     | (cid:0) |         | (cid:1) |      |
|         |        |              | p˜  | (z) =    | B (−1)k+1L        |     | kε      | µ (z),z | ,       | (21) |
|         |        |              | c,B |          |                   | J,B | 2,B     | B       |         |      |
k
k=1
|     |     |     |     |     |     |     |     |     | − 1 |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
where L (s|z) and µ (z) are given by Theorem 6, and ε = (m !) mB .
|     | J,B        |          |     | B   |         |            | 2,B |     | B   |     |
| --- | ---------- | -------- | --- | --- | ------- | ---------- | --- | --- | --- | --- |
|     | Proof: See | Appendix |     | G.  |         |            |     |     |     |     |
|     |            |          |     | IV. | RESULTS | DISCUSSION |     |     |     |     |
AND
In this section, the analytical results based on the expressions derived in Sec. III are verified
by means of Monte Carlo simulations. By inspecting these results, we will try to understand how
eachsystemparameteraffectsthenetwork’sperformance asdefinedinTheorem7(orTheorem6
when no ABSs are deployed). However, let us recall that we are: (i) assuming ideal backhaul
links, (ii) evaluating the QoS only in terms of coverage probability, and (iii) for the sake of
conciseness and mathematical tractability, not specifying the difference between LoS and NLoS
transmissions for both the terrestrial and aerial tiers (this, however, is a precautionary assumption
since the presence of NLoS nodes would strongly reduce the average aerial interference power
without significantly increase the average desired signal power, leading to more optimistic
behaviors of the coverage probability as the number of UAVs N is increased). Note also that
A
aerial BSs present limitations in terms of capacity (e.g., due to the small number of antennas
supported) and autonomy, which considerations are beyond the scope of this study. Nonetheless,
the observed trends can effectively support cellular operators in network planning. For example,

16
|     |     |     |     |     | TABLE | III |     |     |
| --- | --- | --- | --- | --- | ----- | --- | --- | --- |
MAINSYSTEMPARAMETERS’STANDARDVALUES
|     | Parameters |               |     |     |              | Values |                |     |
| --- | ---------- | ------------- | --- | --- | ------------ | ------ | -------------- | --- |
|     |            |               |     |     | λ =3TBSs/km2 |        | =3×10−6TBSs/m2 |     |
|     | Original   | TBSs’ density |     |     | 0            |        |                |     |
ABSs’ altitudes h=[0.2, 20]km=[200, 2×104]m, respectively for LAPs and HAPs
|     |               | QoR      |        |     |     | χ=0 |     |     |
| --- | ------------- | -------- | ------ | --- | --- | --- | --- | --- |
|     | UEs’ distance | from the | origin |     |     | r   | =0  |     |
u
Disaster radius r =[1, 10]km, respectively for LAPs- and HAPs-based solution
d

α
|     |      |                |     |     | A =[3, | 2.5], respectively | for LAPs | and HAPs |
| --- | ---- | -------------- | --- | --- | ------ | ------------------ | -------- | -------- |
|     | Path | loss exponents |     |     |        |                    |          |          |
α =3.5
T

|     |     |     |     | ρ | =[5, 50] | W, respectively | for LAPs | and HAPs |
| --- | --- | --- | --- | --- | -------- | --------------- | -------- | -------- |
A
|     | Transmit | powers |     |     |       |     |     |     |
| --- | -------- | ------ | --- | --- | ----- | --- | --- | --- |
|     |          |        |     | ρ | =10 W |     |     |     |
T
|     | Nakagami-m      | shape parameters |        |     |                 | m =2,          | m =1          |     |
| --- | --------------- | ---------------- | ------ | --- | --------------- | -------------- | ------------- | --- |
|     |                 |                  |        |     |                 | A              | T             |     |
|     | SINR            | threshold        |        |     |                 | τ =−5dB=0.3162 |               |     |
|     |                 |                  |        |     |                 | σ2 =10−12W     |               |     |
|     | Noise           | power            |        |     |                 | n              |               |     |
|     |                 |                  |        | η   | =−1.6dB=0.6918, |                | η =−2dB=0.631 |     |
|     | Mean additional | transmit         | losses |     | A               |                | T             |     |
they would be able to quantify the advantage of strengthening the terrestrial infrastructure, as
well as predicting the number of ad hoc ABSs needed in the occurrence of a specific calamity.
Forthisstudy,unlessstatedotherwise,wehaveassumedthevaluesoftheparametersaccording
to Table III and used markers and lines to represent analysis and simulation results, respectively.
Note also that, although the standard values of the disaster radius r and the QoR χ do not
u
reflect typical disaster scenarios (since the majority of the users should be close to the edge of
A
the disaster-struck area d and the network should not be fully destroyed), they may correspond
to the most critical situation (since users at the disaster epicenter have more chances to be
trapped and/or seriously injured, and a less resilient network has more chances of becoming
overloaded).
| A. Influence | of  | the Disaster | Radius |     |     |     |     |     |
| ------------ | --- | ------------ | ------ | --- | --- | --- | --- | --- |
In Fig. 3, the impact of the disaster radius r is investigated under the assumption that either
d
LAPs, HAPs, or none of them are deployed. In particular, the plots describe different coverage
probability behaviors depending on the cardinality N of each type of fleet of ABSs. Different
A

17
(a)
(b)
Fig. 3. Coverage probability as function of the disaster radius when the ABSs deployed are: (a) LAPs and (b) HAPs.
positive values of N have been selected for LAPs and HAPs because of their difference in
A
terms of coverage area. Finally note that, to better highlight the influence of r , here we assume
d
χ = 0 and r = 0. From Fig. 3 we can extract some precious insights:
u
1) Outer TBSs: Based on the considered system parameters, outer TBSs can support the UE
(assuming r = 0) only for very small values of r ; in other words, P rapidly approaches zero
u d c
as r exceeds a couple of hundred meters. This occurs because a larger disaster radius implies a
d
longer average distance to the closest functioning TBS (which in this case is lower-bounded by
r ): in other words, the higher path loss overcompensates the weaker interference. Therefore,
u

18
unless A is very small, non-resilient networks (χ = 0) should not be considered self-sufficient.
d
2) LAPs: If r is less than two kilometers, deploying one single LAP is generally the optimal
d
choice, as the red curve in Fig. 3-a confirms. Our explanation to this fact relies in the well-known
trade-off for VHetNets’ densification: while increasing the number of nodes statistically reduces
the distance to the tagged BS, it increases the power of the aggregate interference. However, for
r ≥ 2km the optimal N rapidly increases: for r = 10km even eight LAPs are not enough to
d A d
ensure sufficient reliability (for which we may expect P (cid:39) 0.6) at the epicenter of the calamity.
c
3) HAPs: In case of relatively small disasters, deploying HAPs is highly discouraged, as
Fig. 3-b confirms. On the other side, as r exceeds a few kilometers, HAPs can be successfully
d
deployedbyleveragingtheirstrongtransmitpowerandfavorablechannelconditions.Theoptimal
cardinality of the fleet is usually N = 1, but it rapidly increases as r → 100km: in fact, here
A d
the aerial interference experienced at the disaster epicenter becomes much less detrimental while
a higher value of N generally implies a shorter distance between the UE and the closest HAP.
A
B. Influence of the UE’s Location
In this subsection we investigate the influence, in terms of coverage probability, of the distance
of the user with respect to the epicenter. This time, r is specifically fixed in order to simulate a
d
typical disaster scenario for various LAPs- or HAPs-aided networks, which based on the results
obtained in Fig. 3 (and also in our previous paper [4]) are assumed to be conveniently deployed
in case of small or large disasters, respectively. Once again, we assume there are no surviving
TBSs inside the disaster-struck zone.
1) Outer TBSs: As expected, the blue curves in Fig. 4 convey that the TBSs surrounding A
d
can be quite effective in serving UEs located relatively close to the edge of the suffered region
(roughly within a hundred meters). We can also see that the QoS experienced by the typical user
slightly depends on r , and is mostly affected by the distance to the closest working TBS.
d
2) LAPs: Fig. 4-a illustrates an overall improvement when deploying low-altitude aerial nodes
above a relatively small disaster region of radius 1km. We can notice that all the considered
LAP fleets are able to cover more than twice the area of A . In addition, for a typical user
d
located at the origin the highest QoS is achieved for N = 1, as anticipated in Fig. 3-a.
A
Fortheconsideredsetup,ahighnumberofaerialnodes(seethevioletcurve)wouldnotmaximize
the network performance for any distance from the epicenter, and therefore is not recommended.

19
(a)
(b)
Fig. 4. Coverage probability as function of the UE’s location when the ABSs deployed are: (a) LAPs and (b) HAPs. The
disaster radius is assumed equal to one and ten kilometers, respectively.
Finally, for outer UEs the aerial interference is quite negligible as long as N ≤ 3, which would
A
promote the deployment of multiple LAPs in case of a considerable traffic demand.
3) HAPs: For this scenario, we considered a disaster radius of 10km. From Fig. 4-b, it
is evident that deploying multiple HAPs is not convenient since it implies a strong aerial
interference, although it might be needed in case of a considerably larger size of the disaster.
Furthermore, we can state that the users located around the epicenter are the ones which benefit
the most from the deployed HAPs, up to the point that for N ≤ 2 their experienced post-
A

20
Fig. 5. Coverage probability as a function of the QoR (assumed uniform over the disaster-struck area) and the user is located
at the origin.
disaster QoS surpasses its pre-disaster counterpart. As the typical user moves away from the
epicenter, the A-association generally decreases and the aerial interference becomes more and
more problematic; then, a minimum coverage is experienced at around 600m before the edge of
A , where the outer TBSs become close enough to frequently serve the user and the terrestrial
d
interference dominates over its aerial counterpart.
C. Influence of the QoR
Letusnowfocusontheconceptofresiliencybyevaluatingthecoverageprobabilityforvarious
expressions of χ(r). We propose two studies to better understand the importance of having
resilient TBSs: one assumes a uniform QoR and includes ABSs in the network architecture,
whereas the other investigates various QoR’s planar distributions while omitting ABSs.
1) Uniform QoR: The dashed curves of Fig. 5 tell us that, from a pure coverage perspective,
if N = 0 then a small value of A can be much more problematic than a hundred times
A d
larger one. This can be explained by taking into account that a larger disaster area paradoxically
benefits a typical user located at its epicenter because it increases the distance to the interfering
outer TBSs. Instead, the solid lines show that even one single aerial node can lead to a high
A-association probability (because of the advantaged channel conditions) and consequently boost
the coverage probability, especially as χ → 0, which confirms the results previously shown in

21
Fig. 6. Coverage probability as function of the UE’s location for various QoR behaviors, considering N =0 and r =2km.
A d
Figs. 3 and 4.
Generally speaking, P decreases or increases depending on whether the ABS (and especially
c
the HAP) is present or not. As Fig. 5 illustrates, by assuming a fully-resilient terrestrial network
(which is equivalent to the scenario without any perturbation) we would always have 0.7 <
P < 0.8, meaning that the aerial node would not remarkably improve the existing infrastructure.
c
Actually, for χ ≥ 0.4 a small degradation of P due to the presence of a HAP can be observed
c
by comparing the red curves.
2) QoR Distributions: We hereby consider a medium-size disaster with r = 2km and
d
investigate the behavior of P as a function of r . As a parameter, we consider various planar
c u
distributions (namely, constant, square-root-like, linear, and exponential with respect to r ) of
u
the QoR and compare them in the presence of only terrestrial nodes. The expression of χ(r )
u
might strongly depend on the entity of the disaster: for example, we may expect an explosion
leading to a sharp variation of the density of surviving TBSs as we move away from the origin,
while a flood should have a more uniform influence on the surrounding environment.
All the curves displayed in Fig. 6 convey that, compared to the case with full TBS density (which
can be fairly assumed if r (cid:29) r ), even halving the original TBS density (that is, reducing the
u d
QoR to just0.5) would nowhere compromise the QoS, becauser is relatively small. Consistently
d
with Fig. 5, we can also notice that for r → 0 the QoS directly depends on the local density
u
λ (r ); in this scenario, the interference coming from the outer TBSs is usually negligible and
T u

22
the inner interferers are much farther than the tagged TBS. Instead, if the user is close to the
edge of A , the interference becomes relevant and hence a higher density of the surrounding
d
TBSs leads to a slightly lower value of P .
c
V. CONCLUSION AND FUTURE WORKS
In this paper, we proposed a concise and tractable mathematical framework which borrows
tools from SG and makes use of indicator functions in order to enable the estimation of the
QoS in UAV-assisted post-disaster wireless networks. In particular, given a typical VHetNet
consisting of partially-resilient TBSs and ad-hoc ABS, we provided novel analytical expressions
for the minimum distance distributions, association probabilities, and Laplace transforms of the
interference in order to obtain the exact and approximate expressions of the coverage probability
experienced by a typical UE, which can be arbitrarily located anywhere on the ground plane.
Furthermore, by verifying the obtained numerical results, we proved that a properly chosen
fleet of ad-hoc ABSs can strongly support the terrestrial infrastructure in various scenarios, and
highlighted the trade-off between wider coverage and stronger interference due to heterogeneous
network’s densification.
This study could be extended in various research directions. For example, a more general
setup where the ABSs operate in either LoS or NLoS condition with respect to the user should
be considered in the future. Furthermore, it would be interesting to evaluate novel solutions
for interference mitigation in post-disaster scenarios, perhaps by switching off some specific
extra-region TBSs that are unlikely to serve any high-priority users involved in the disaster;
this strategy would also help to reduce the overall power consumption, which is a critical issue
since power systems are also susceptible to calamities. Finally, other important aspects such as
network overload and backhaul issues could be taken into account in future extensions of this
work.
APPENDIX A
PROOF OF THEOREM 1
Recalling that the altitude of terrestrial antennas is assumed to be negligible compared to that
of their aerial counterparts, the ground (and Euclidean) distance between the UE and the tagged
TBS is identified by the RV Z . Thus, the expression of the respective CDF can be derived
T

23
from the null probability of the PPP [26]. Let N (z) be the number of TBSs residing within a
T
z
| distance |     | from the | UE, | then:   |     |                   |          |         |            |          |     |      |
| -------- | --- | -------- | --- | ------- | --- | ----------------- | -------- | ------- | ---------- | -------- | --- | ---- |
|          |     | F        | (z) | = P(Z   | ≤   | z) = 1−P(Z        |          | >       | z) = 1−P(N | (z) =    | 0)  |      |
|          |     |          | ZT  |         | T   |                   |          | T       |            | T        |     |      |
|          |     |          |     |         |     | 2π                | z        |         |            |          |     |      |
|          |     |          |     |         |     | (cid:18) (cid:90) | (cid:90) |         |            | (cid:19) |     |      |
|          |     |          |     |         |     |                   |          | (cid:0) | (cid:1)    |          |     |      |
|          |     |          |     | = 1−exp |     | −                 | λ        | r (ω,β) | ωdωdβ      | ,        |     | (22) |
T Ω
|     |     |     |     |     |     | 0   | 0   |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(cid:112)
where r (ω,β) = r2 +ω2 −2r ω cosβ and λ (ω,β) describe the horizontal distance from
|     | Ω   |     | u   |     | u   |     |     | T   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
the origin and the behavior of the post-disaster TBSs’ density, respectively.
|     |            |     |      |        |       | APPENDIX |              | B   |     |     |     |     |
| --- | ---------- | --- | ---- | ------ | ----- | -------- | ------------ | --- | --- | --- | --- | --- |
|     |            |     |      |        | PROOF |          | OF COROLLARY |     | 1   |     |     |     |
| The | derivative |     | of F | (z) is |       |          |              |     |     |     |     |     |
ZT
|     |           |     | (cid:32) | 2π z              |         |       |         | (cid:33)(cid:32) | 2π         | z         |         | (cid:33) |
| --- | --------- | --- | -------- | ----------------- | ------- | ----- | ------- | ---------------- | ---------- | --------- | ------- | -------- |
|     |           |     |          | (cid:90) (cid:90) |         |       |         |                  | d (cid:90) | (cid:90)  |         |          |
|     |           |     |          |                   | (cid:0) |       | (cid:1) |                  |            | (cid:0)   | (cid:1) |          |
| f   | (z) =−exp |     | −        |                   | λ r     | (ω,β) | ωdωdβ   |                  | −          | λ r (ω,β) | ωdωdβ   | ,        |
|     | ZT        |     |          |                   | T Ω     |       |         |                  |            | T Ω       |         |          |
dz
|     |     |     |     | 0 0 |     |     |     |     | 0   | 0   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
(23)
z
|     |     |     |     |     | (cid:82) | (cid:0) | (cid:1) |     |     |     |     |     |
| --- | --- | --- | --- | --- | -------- | ------- | ------- | --- | --- | --- | --- | --- |
where, introducing g (z,β) = λ r (ω,β) ωdω and applying the Leibniz integral rule, we
|     |     |     | z   |     | T   | Ω   |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
0
have
| (cid:90) | 2π  |     |     |     |     |     |     |     | (cid:90) 2π |     | (cid:90) 2π |     |
| -------- | --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | ----------- | --- |
| d        |     |     |     |     | d   |     |     | d   | ∂           |     | ∂           |     |
g (z,β)dβ = g (z,2π) (2π)−g (z,2π) (0)+ g (z,β)dβ = g (z,β)dβ
| dz  | z   |     | z   |     | dz  | z   |     | dz  | ∂z  | z   | ∂z  | z   |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 0   |     |     |     |     |     |     |     |     | 0   |     | 0   |     |
2π
(cid:90)
|     |     |     |     | (cid:0) |       | (cid:1) |     |     |     |     |     |      |
| --- | --- | --- | --- | ------- | ----- | ------- | --- | --- | --- | --- | --- | ---- |
|     |     |     | = z | λ r     | (z,β) | dβ,     |     |     |     |     |     | (24) |
|     |     |     |     | T       | Ω     |         |     |     |     |     |     |      |
0
| which | completes | the | proof. |     |     |          |            |     |     |     |     |     |
| ----- | --------- | --- | ------ | --- | --- | -------- | ---------- | --- | --- | --- | --- | --- |
|       |           |     |        |     |     | APPENDIX |            | C   |     |     |     |     |
|       |           |     |        |     |     | PROOF    | OF THEOREM |     | 3   |     |     |     |
The B-association probability represents the probability that the UE associates to a BS of type
B (i.e., the average power received from the closest BS of type B exceeds the average powers
| received | from | the | closest | BSs | of the | other | types). |     |     |     |     |     |
| -------- | ---- | --- | ------- | --- | ------ | ----- | ------- | --- | --- | --- | --- | --- |
Now, let D (z) express the minimum Euclidean distance of any interfering BS of type C
BC
|     |     |     |     |     |     | B   |     |     |     | z.  |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
when the UE associates to a BS of type located at ground distance Noting that the Euclidean

24
√
distance to the tagged BS equals z2 +h2 if B=A and z otherwise, we define the projection
|        |        |     | D (z) |     |     |     |     |     |     |     |     |     |     |
| ------ | ------ | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| on the | ground | of  | BC    | as: |     |     |     |     |     |     |     |     |     |

(cid:112)
|     |     |     |     |     |     |    | D2 (z)−h2, |     | if C=A |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------- | --- | ------ | --- | --- | --- | --- |

|     |     |     |     | Z   | (z) | =   | BC  |     |     | ,   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
BC
|     |     |     |     |     |     |  D | (z), |     | if C=T |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---- | ---- | --- | ------ | --- | --- | --- | --- |
BC
| which | is conceptually |     | represented |     | in  | Fig. | 2.  |     |     |     |     |     |     |
| ----- | --------------- | --- | ----------- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
By recalling that ξ = ρ η with O ∈ {A,T}, and introducing the random Euclidean
|     |     |     | O   |     | O O |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
distance D = D (Z ) as function of its own horizontal component Z , we can finally derive
|     | O   | OO  | O   |     |     |     |     |     |     |     | O   |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
B-association
| the              |     |     | probabilities, |     | as follows. |     |     |     |     |     |     |     |     |
| ---------------- | --- | --- | -------------- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- |
| A. T-Association |     |     | Probability    |     |             |     |     |     |     |     |     |     |     |
Recalling that Q∗ denotes the average power received from the closest A- or T-BS, then the
O
|             | P(Q∗ |     | > Q∗) |         |     | Z   |             |     |     |     |     |     |     |
| ----------- | ---- | --- | ----- | ------- | --- | --- | ----------- | --- | --- | --- | --- | --- | --- |
| probability |      |     |       | depends | on  | T   | , and hence |     |     |     |     |     |     |
|             |      | T   | A     |         |     |     |             |     |     |     |     |     |     |
∞
(cid:90)
|     |     |     |     | P(cid:0) |       |     | (cid:1) |     | (cid:0) | (cid:1) |        |     |      |
| --- | --- | --- | --- | -------- | ----- | --- | ------- | --- | ------- | ------- | ------ | --- | ---- |
|     |     |     | A   | =        | Z > Z | (Z  | ) =     | F¯  | Z (z)   | f       | (z)dz, |     | (25) |
|     |     |     | T   |          | A     | TA  | T       | ZA  | TA      | ZT      |        |     |      |
0
|     |     | F¯  | (cid:0) |     | (cid:1) |     |     |     |     |     |     |     |     |
| --- | --- | --- | ------- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- |
where a (z) = Z (z) expresses the conditional T-association probability.
|                  | T   | ZA              | TA            |               |             |     |                    |          |           |     |     |     |     |
| ---------------- | --- | --------------- | ------------- | ------------- | ----------- | --- | ------------------ | -------- | --------- | --- | --- | --- | --- |
| B. A-Association |     |                 | Probability   |               |             |     |                    |          |           |     |     |     |     |
| Trivially,       |     | the association |               | probabilities |             |     | are complementary, |          | therefore |     |     |     |     |
|                  |     |                 |               |               |             | A   | = 1−A              |          | .         |     |     |     |     |
|                  |     |                 |               |               |             |     | A                  | T        |           |     |     |     |     |
| Alternatively,   |     | the             | A-association |               | probability |     | can be             | computed | as        |     |     |     |     |
r+
(cid:90)
|     |     |     | P(cid:0) |     |     |      | (cid:1) |     | F¯ (cid:0) | (cid:1) |          |     |      |
| --- | --- | --- | -------- | --- | --- | ---- | ------- | --- | ---------- | ------- | -------- | --- | ---- |
|     |     | A   | =        | Z   | > Z | (Z ) | =       |     | Z          | (z)     | f (z)dz. |     | (26) |
|     |     |     | A        | T   | AT  | A    |         |     | ZT AT      |         | ZA       |     |      |
max(0,−r−)
|     |     |     |     |     |     |       | APPENDIX   | D   |          |     |     |         |      |
| --- | --- | --- | --- | --- | --- | ----- | ---------- | --- | -------- | --- | --- | ------- | ---- |
|     |     |     |     |     |     | PROOF | OF THEOREM |     | 4        |     |     |         |      |
|     |     |     |     |     |     |       | Φˇ         |     | (cid:0)B |     |     | (cid:1) | B(z) |
Let us first define the sets of the C-BSs as = Φ \ (Z (z)) ∪ W∗ , where
|     |     |     |     |     |     |     |     | C   | C   | z BM |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- |
denotes the circle of radius z centered around the typical user. Now, we can denote the set of
|     |     |     |     |     |     |     |     |     | (cid:16) |     | (cid:17)mT |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- | ---------- | --- | --- |
TBSs’ coordinates as Y and recall that I (s|ω) = 1− mT . In order to obtain
T
|     |     |     |     |     |     |     |     |     | mT+ξTsD | − αT(ω) |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | ------- | --- | --- | --- |
|     |     |     |     |     |     |     |     |     |         | T T     |     |     |     |

25
the expression of the conditional Laplace transform of the terrestrial interference, we firstly take
the expectation over both the point process and the set of fading gains [28, Sec. III-C]:
|     |     |         |     |          |          |              | (cid:20) |          |        | (cid:21) |     |     |     |
| --- | --- | ------- | --- | -------- | -------- | ------------ | -------- | -------- | ------ | -------- | --- | --- | --- |
|     |     |         |     | E(cid:2) |          | (cid:3) ( a) |          | (cid:89) |        |          |     |     |     |
|     |     | L (s|z) | =   |          | e−sIBT|z | =            | E        |          | ψ (s,Y | )        |     |     |     |
|     |     | IBT     |     |          |          |              | ΦT       |          | T      | i        |     |     |     |
Yi∈Φˇ
T
|     |     |     |      |     | (cid:18)          | (cid:90)  |                         |          |         |               |         | (cid:19) |      |
| --- | --- | --- | ---- | --- | ----------------- | --------- | ----------------------- | -------- | ------- | ------------- | ------- | -------- | ---- |
|     |     |     | (b)  |     |                   |           |                         |          | (cid:0) |               | (cid:1) |          |      |
|     |     |     | =exp |     | −                 |           | λ ((cid:107)Y(cid:107)) |          | 1−ψ     | (s,Y)         | dY      |          |      |
|     |     |     |      |     |                   |           | T                       |          |         | T             |         |          |      |
|     |     |     |      |     | R2\B              | z(ZBT(z)) |                         |          |         |               |         |          |      |
|     |     |     |      |     |                   | 2π ∞      |                         |          |         |               |         |          |      |
|     |     |     |      |     | (cid:18) (cid:90) | (cid:90)  |                         |          |         |               |         | (cid:19) |      |
|     |     |     |      |     |                   |           | (cid:0)                 |          | (cid:1) |               |         |          |      |
|     |     |     | =exp |     | −                 |           | λ                       | r (ωˇ,β) | I       | (s|ωˇ)ωˇdωˇdβ |         | .        | (27) |
|     |     |     |      |     |                   |           | T                       | Ω        | T       |               |         |          |      |
|     |     |     |      |     | 0                 | ZBT(z)    |                         |          |         |               |         |          |      |
Notethat(a)followsfromtheindependenceoftheexponentiallydistributedgainsG ’s,having
T,Yi
|     |     |     |     |     |     | (cid:104) | (cid:16) |        | (cid:17)(cid:105) |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --------- | -------- | ------ | ----------------- | --- | --- | --- | --- |
|     |     |     |     |     |     |           |          | sGC,Wi | ξC                |     |     |     |     |
introduced the function ψ (s,W ) = E exp − for any type of interferers, and
|     |     |     | C   |     | i   | GC,Wi |     | (cid:107)Wi(cid:107)αC |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ----- | --- | ---------------------- | --- | --- | --- | --- | --- |
(b) derives from the application of the probability generating functional (PGFL) to the latter
function.
|     |     |     |     |     |       | APPENDIX |         | E   |     |     |     |     |     |
| --- | --- | --- | --- | --- | ----- | -------- | ------- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     | PROOF | OF       | THEOREM |     | 5   |     |     |     |     |
By letting Ωˇ denote the set of aerial interferers’ horizontal distances and recalling that
A
| Nˇ  |     | 1(B |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
= N − = A), the Laplace transform of the aerial interference conditioned on B-
| A           | A   |            |     |          |     |            |           |          |          |           |     |                             |     |
| ----------- | --- | ---------- | --- | -------- | --- | ---------- | --------- | -------- | -------- | --------- | --- | --------------------------- | --- |
| association | can | be derived |     | as [28,  | Eq. | (4), (16)] |           |          |          |           |     |                             |     |
|             |     |            |     |          |     |            |           |          | Nˇ       | A         |     |                             |     |
|             |     |            |     | (cid:2)  |     | (cid:3)    | (cid:104) | (cid:16) | (cid:88) |           |     | (cid:17) (cid:12) (cid:105) |     |
|             | L   | (s|z)      | = E | e−sIBA|z |     | = E        |           | exp      | −s       | G D−αA(Ωˇ |     | ) (cid:12)z                 |     |
|             | IBA |            | IBA |          |     |            | IBA       |          |          | i         |     | A,i                         |     |
AA
i=1
Nˇ
|     |     |     |      | (cid:104) | (cid:104)(cid:89) A |         |     |       |     | (cid:105)(cid:105) |     |     |     |
| --- | --- | --- | ---- | --------- | ------------------- | ------- | --- | ----- | --- | ------------------ | --- | --- | --- |
|     |     |     | ( a) |           |                     | (cid:0) |     | αA(Ωˇ |     | (cid:1)(cid:12)    |     |     |     |
|     |     |     | = E  | E         |                     | exp −sG |     | D −   | )   | (cid:12)z          |     |     |     |
|     |     |     | Ωˇ   | G         |                     |         | i   | A A   | A,i |                    |     |     |     |
A
i=1
Nˇ
|     |     |     |        | (cid:104)(cid:89) | A         |         |     |         |     | (cid:105)       |     |     |     |
| --- | --- | --- | ------ | ----------------- | --------- | ------- | --- | ------- | --- | --------------- | --- | --- | --- |
|     |     |     | ( b) E |                   | E (cid:2) |         |     | − αA(Ωˇ |     | (cid:3)(cid:12) |     |     |     |
|     |     |     | =      |                   |           | exp(−sG |     | D       | ))  | (cid:12)z       |     |     |     |
|     |     |     | Ωˇ     |                   | Gi        |         | i   | A A     | A,i |                 |     |     |     |
A
i=1
|     |     |     |          | Nˇ                |         |     |                    | (cid:18) |           |       |             | (cid:19)Nˇ  |      |
| --- | --- | --- | -------- | ----------------- | ------- | --- | ------------------ | -------- | --------- | ----- | ----------- | ----------- | ---- |
|     |     |     |          | (cid:104)(cid:89) | A       |     | (cid:12) (cid:105) |          | (cid:104) |       | (cid:12)    | (cid:105) A |      |
|     |     |     | ( = c) E |                   | I (s|Ωˇ |     | ) (cid:12)z ( =    | d) E     | I         | (s|Ωˇ | ) (cid:12)z | ,           |      |
|     |     |     | Ωˇ       |                   | A,i     | A,i |                    |          | Ωˇ A,i    |       | A,i         |             | (28) |
|     |     |     |          | A                 |         |     |                    |          | A,i       |       |             |             |      |
i=1
|         |       |     | (cid:16) |     |         | (cid:17)mA |        |     |         |      |     |              |        |
| ------- | ----- | --- | -------- | --- | ------- | ---------- | ------ | --- | ------- | ---- | --- | ------------ | ------ |
|         | (s|Ωˇ |     |          | mA  |         |            |        |     |         |      |     |              |        |
| where I |       | ) = |          |     |         |            | . Step | (a) | follows | from | the | independence | of the |
|         | A,i   | A,i |          |     | − αA(Ωˇ |            |        |     |         |      |     |              |        |
|         |       |     | mA+ξAsD  |     | A A     | A,i)       |        |     |         |      |     |              |        |
channel gains and the distances of the aerial interferers, whereas (b) follows from rewriting the
expectation of a product as a product of the expectations owing to iid channel gains. Then,
(c) follows from the moment generating function (MGF) of the gamma-distributed fading gains
G ’s [25, Appendix E], and (d) from the conditional iid distances of the aerial interferers.
i

26
|     |     |     |     |     |     | APPENDIX |            | F   |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | -------- | ---------- | --- | --- | --- | --- | --- | --- |
|     |     |     |     |     |     | PROOF    | OF THEOREM |     | 6   |     |     |     |     |
Let us first recall from Table II and Theorem 3 the expressions of the Euclidean distances
(z)’sandtheplanardomainsR
| D   |     |     |     |     |     | ’s,respectively.Now,followingthesameapproachproposed |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
| BB  |     |     |     |     |     | B                                                    |     |     |     |     |     |     |     |
in [29], the exact expression of the coverage probability can be obtained as
(cid:88)
P = E (cid:2)P(SINR > τ |Z = z) (cid:3) = E (cid:2) a (Z )p (Z ) (cid:3)
|     |     | c   | ZB  |     |     | B   |     |     |     | ZB B | B   | c,B B |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | ----- | --- |
B={A,T}
(cid:90)
(cid:88)
|     |     | =   |     |     | a (z)p | (z)f | (z)dz, |     |     |     |     |     | (29) |
| --- | --- | --- | --- | --- | ------ | ---- | ------ | --- | --- | --- | --- | --- | ---- |
|     |     |     |     |     | B      | c,B  | ZB     |     |     |     |     |     |      |
B={A,T}R
B
in which the exact expressions of the conditional coverage probabilities are given by 3
|     |     |     |     | (cid:18) |      |         |     | (cid:19) | (cid:18) |     |         | (cid:19) |      |
| --- | --- | --- | --- | -------- | ---- | ------- | --- | -------- | -------- | --- | ------- | -------- | ---- |
|     |     |     |     |          | ξ G∗ | D−αB(z) |     |          |          |     | τ J     |          |      |
|     |     |     |     | P        | B B  | BB      |     |          | P G∗     |     |         |          |      |
|     |     | p   | (z) | =        |      |         | >   | τ =      |          | >   |         | ,        | (30) |
|     |     | c,B |     |          |      | J       |     |          |          | B   | D−αB(z) |          |      |
ξ
B BB
Γu(m,mg)
with J = σ2 + I. By definition, the CCDF of the Gamma distribution is F¯ (g) = ,
|     | n   |     |     |     |     |     |     |     |     |     |     | G   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Γ(m)
∞
| Γu(m,mg) |     |     | (cid:82) | tm−1e−tdt |     |        |       |            |     |       |           |       |       |
| -------- | --- | --- | -------- | --------- | --- | ------ | ----- | ---------- | --- | ----- | --------- | ----- | ----- |
| where    |     |     | =        |           |     | is the | upper | incomplete |     | Gamma | function. | Let µ | (z) = |
B
mg
m τ DαB(z), taking the expectation with respect to J implies that [20]
| B   | BB  |     |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ξB
|     |     |       |     | (cid:20) Γu | (cid:0) m | ,µ (z)J | (cid:1)(cid:21) | (cid:20) |          | m (cid:88)B−1 | (cid:0) µ | (z)J (cid:1)k(cid:21) |     |
| --- | --- | ----- | --- | ----------- | --------- | ------- | --------------- | -------- | -------- | ------------- | --------- | --------------------- | --- |
|     |     |       |     |             | B         | B       |                 | ( a)     |          |               | B         |                       |     |
|     |     | p (z) | = E |             |           |         |                 | = E      | e−µB(z)J |               |           |                       |     |
|     |     | c,B   |     | J           |           |         |                 | J        |          |               |           |                       |     |
|     |     |       |     |             | Γ(m       | )       |                 |          |          |               |           | k!                    |     |
B
k=0
m (cid:88)B−1
|     |     |     |      |     | µk (z) |                    |     |            |     |     |     |     |      |
| --- | --- | --- | ---- | --- | ------ | ------------------ | --- | ---------- | --- | --- | --- | --- | ---- |
|     |     |     | ( b) |     | B      | E (cid:2) e−µB(z)J |     | Jk (cid:3) |     |     |     |     |      |
|     |     |     | =    |     |        |                    |     | ,          |     |     |     |     | (31) |
|     |     |     |      |     | k!     | J                  |     |            |     |     |     |     |      |
k=0
m−1
|     |     |     |     |     |     | Γu(m,g) |     | (cid:80) | gk  |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ------- | --- | -------- | --- | --- | --- | --- | --- |
where (a) follows from the definition = e−g , and (b) is obtained from the linearity
|     |     |     |     |     |     | Γ(m) |     |     | k!  |     |     |     |     |
| --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- |
k=0
| of the expectation |     |     | operator. | Taking |     | into account |     | that |     |     |     |     |     |
| ------------------ | --- | --- | --------- | ------ | --- | ------------ | --- | ---- | --- | --- | --- | --- | --- |
∂k
|     |     |     |     |     | E (cid:2) e−sJ | Jk (cid:3) | (−1)k |     |     |        |     |     |     |
| --- | --- | --- | --- | --- | -------------- | ---------- | ----- | --- | --- | ------ | --- | --- | --- |
|     |     |     |     |     |                |            | =     |     | L   | (s|z), |     |     |     |
|     |     |     |     |     | J              |            |       | ∂sk | J   |        |     |     |     |
where
|     |     |       | E(cid:2) |      | (cid:3) E(cid:2) |           | 2(cid:3) |        | E(cid:2) | (cid:3) |      |            |     |
| --- | --- | ----- | -------- | ---- | ---------------- | --------- | -------- | ------ | -------- | ------- | ---- | ---------- | --- |
|     | L   | (s|z) | =        | e−sJ | =                | e−sI e−sσ |          | = e−sσ | 2        | e−sI =  | e−sσ | 2 L (s|z), |     |
|     |     | J     |          |      |                  |           | n        |        | n        |         |      | n I        |     |
the final expression is obtained. This, however, may require the computation of high-order
derivatives of the conditional Laplace transform of the interference, resulting in a number of
| terms proportional |     |     | to m | .   |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
B
3In
the particular case of Rayleigh fading channel (m B = 1), we can compute the conditional coverage probability as
|               | (cid:16) | −τD αB | (z)σn 2(cid:17) | (cid:16) | τD αB (z),z | (cid:17) |     |     |     |     |     |     |     |
| ------------- | -------- | ------ | --------------- | -------- | ----------- | -------- | --- | --- | --- | --- | --- | --- | --- |
| p c,B (z)=exp |          | B B    |                 | L I,B    | B B         | .        |     |     |     |     |     |     |     |
|               |          | ξB     |                 |          | ξB          |          |     |     |     |     |     |     |     |

27
|     |     |     |     |     |       | APPENDIX |         | G   |     |     |     |     |
| --- | --- | --- | --- | --- | ----- | -------- | ------- | --- | --- | --- | --- | --- |
|     |     |     |     |     | PROOF | OF       | THEOREM |     | 7   |     |     |     |
A tight bound can be applied to the CDF of the Gamma distribution in order to ease the
computation of the conditional coverage probabilities provided in Theorem 6. Let Γ (m,mg) =
l
mg
(cid:82) tm−1e−tdt
denote the lower incomplete Gamma function, then the CDF of the Gamma
0
|              |     | F (g) | = Γ (m,mg)  | =   | 1− Γu(m,mg), |          |        |              |     |      |     |     |
| ------------ | --- | ----- | ----------- | --- | ------------ | -------- | ------ | ------------ | --- | ---- | --- | --- |
| distribution |     | G     | l           |     |              |          | can be | bounded      | as  | [30] |     |     |
|              |     |       | Γ(m)        |     |              | Γ(m)     |        |              |     |      |     |     |
|              |     |       |             |     |              | Γ (m,mg) |        |              |     |      |     |     |
|              |     |       | (1−e−ε1mg)m |     |              | l        |        | (1−e−ε2mg)m, |     |      |     |     |
|              |     |       |             |     |              | ≤        |        | ≤            |     |      |     |     |
Γ(m)
|     |     |     |     |     |      |     |     |     |     |           |        |     |
| --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | ---------- | ------ | --- |
|     |     |     |     |     |  1, |     | if  | m ≥ | 1   |  (m!)− 1 | , if m | > 1 |
m
| where | we defined |     | the constants |     | ε =      |     |      |     | and ε | =     |      | .   |
| ----- | ---------- | --- | ------------- | --- | -------- | --- | ---- | --- | ----- | ----- | ---- | --- |
|       |            |     |               |     | 1        |     |      |     | 2     |       |      |     |
|       |            |     |               |     |  (m!)− | 1   | , if | m < | 1     |  1, | if m | ≤ 1 |
m
Γ (1,g)
Note that for m = 1 the upper and the lower bounds become equal and thus l = 1−e−g.
Γ(1)
It has been shown in [31] that the upper bound actually is a good approximation, hence we
| consider | ε   | = (m!)−1 | .   |     |     |     |     |     |     |     |     |     |
| -------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|          | 2   |          | m   |     |     |     |     |     |     |     |     |     |
Recalling that µ (z) = m τ DαB(z), the conditional coverage probabilities can be approx-
|     |     |     | B   | B   |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
ξB BB
| imated | as [20,  | Appendix |                | F]  |          |     |     |     |          |     |     |     |
| ------ | -------- | -------- | -------------- | --- | -------- | --- | --- | --- | -------- | --- | --- | --- |
|        | (cid:20) |          | (z)J)k(cid:21) |     | (cid:20) |     |     |     | (cid:21) |     |     |     |
Γu(m ,µ Γ (m ,µ (z)J) ( a) (cid:104) (cid:0) (cid:1)mB (cid:105)
| p =  | E   |             | B B      |                          | = E 1− | l   | B B |          | ≈ 1−E | 1−e−ε2,BµB(z)J |     |     |
| ---- | --- | ----------- | -------- | ------------------------ | ------ | --- | --- | -------- | ----- | -------------- | --- | --- |
| c,B  | J   |             |          |                          | J      |     |     |          |       | J              |     |     |
|      |     |             | Γ(m )    |                          |        |     | Γ(m | )        |       |                |     |     |
|      |     |             | B        |                          |        |     | B   |          |       |                |     |     |
|      |     | (cid:20) mB | (cid:18) | (cid:19)                 |        |     |     | (cid:21) |       |                |     |     |
|      |     | (cid:88)    | m        |                          |        |     |     |          |       |                |     |     |
| ( b) | 1−E |             | B        | (−1)mB−k(−e−ε2,BµB(z)J)k |        |     |     |          |       |                |     |     |
=
|     |     | J   | k   |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
k=0
|     | (cid:20) | mB (cid:18) | (cid:19) |     |     |     |     | (cid:21) |     |     |     |     |
| --- | -------- | ----------- | -------- | --- | --- | --- | --- | -------- | --- | --- | --- | --- |
(cid:88) m
|     | E   |     | B (−1)k+1 |     |         |       |       |     |     |     |     |     |
| --- | --- | --- | --------- | --- | ------- | ----- | ----- | --- | --- | --- | --- | --- |
| =   |     |     |           |     | exp(−kε | µ     | (z)J) |     |     |     |     |     |
|     | J   |     | k         |     |         | 2,B B |       |     |     |     |     |     |
k=1
|     | mB       | (cid:18) (cid:19) |          |         |         |     |      |                |     |     |     |      |
| --- | -------- | ----------------- | -------- | ------- | ------- | --- | ---- | -------------- | --- | --- | --- | ---- |
|     | (cid:88) | m                 |          |         |         |     |      |                |     |     |     |      |
|     |          | B                 | (−1)k+1E | (cid:2) | (cid:0) |     |      | (cid:1)(cid:3) |     |     |     |      |
| =   |          |                   |          |         | exp −kε | µ   | (z)J | ,              |     |     |     | (32) |
|     |          | k                 |          | J       |         | 2,B | B    |                |     |     |     |      |
k=1
where(a)followsfromtheupperboundpreviouslyintroducedand(b)fromthebinomialtheorem
under the assumption that m ∈N. The final result in (21) can be obtained by applying the
B
| definition | of  | the | conditional | Laplace | transform |     | of the | interference. |     |     |     |     |
| ---------- | --- | --- | ----------- | ------- | --------- | --- | ------ | ------------- | --- | --- | --- | --- |
REFERENCES
[1] United Nations Office for Coordination of Humanitarian Affairs (UNOCHA), “The Story of INSARAG 20 Years On...”
2010.
[2] C. Esposito, Z. Zhao, and J. Rak, “Reinforced secure gossiping against DoS attacks in post-disaster scenarios,” IEEE
| Access, | vol. | 8, pp. | 178651–178669, |     | 2020. |     |     |     |     |     |     |     |
| ------- | ---- | ------ | -------------- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |

28
[3] M. Matracia, N. Saeed, M. A. Kishk, and M.-S. Alouini, “Post-disaster communications: Enabling technologies,
architectures, and open challenges,” IEEE Open Journal of the Communications Society, vol. 3, pp. 1177–1205, 2022.
[4] M. Matracia, M. A. Kishk, and M.-S. Alouini, “On the topological aspects of UAV-assisted post-disaster wireless
communication networks,” IEEE Communications Magazine, vol. 59, no. 11, pp. 59–64, 2021.
[5] M. Mozaffari, W. Saad, M. Bennis, Y. Nam, and M. Debbah, “A tutorial on UAVs for wireless networks: Applications,
|     |     |     | IEEE | Communications |     | Surveys | Tutorials, |     |
| --- | --- | --- | ---- | -------------- | --- | ------- | ---------- | --- |
challenges, and open problems,” vol. 21, no. 3, pp. 2334–2360, 2019.
[6] A. Al-Hourani, S. Kandeepan, and S. Lardner, “Optimal LAP altitude for maximum coverage,” IEEE Wireless Communi-
| cations Letters, | vol. | 3, no. 6, | pp. 569–572, | 2014. |     |     |     |     |
| ---------------- | ---- | --------- | ------------ | ----- | --- | --- | --- | --- |
[7] A.V.SavkinandH.Huang,“Navigationofanetworkofaerialdronesformonitoringafrontierofamovingenvironmental
| disaster | area,” IEEE | Systems | Journal, | vol. 14, no. | 4, pp. | 4746–4749, | 2020. |     |
| -------- | ----------- | ------- | -------- | ------------ | ------ | ---------- | ----- | --- |
[8] W. Wu, M. A. Qurishee, J. Owino, I. Fomunung, M. Onyango, and B. Atolagbe, “Coupling deep learning and UAV
for infrastructure condition assessment automation,” in IEEE International Smart Cities Conference (ISC2), Kansas City,
| Missouri, | USA, 2018, | pp. 1–7. |     |     |     |     |     |     |
| --------- | ---------- | -------- | --- | --- | --- | --- | --- | --- |
[9] P. Sanjana and M. Prathilothamai, “Drone design for first aid kit delivery in emergency situation,” in 6th International
Conference on Advanced Computing and Communication Systems (ICACCS), Piscataway, New Jersey, USA, 2020, pp.
215–220.
[10] M. Kishk, A. Bader, and M.-S. Alouini, “Aerial base station deployment in 6G cellular networks using tethered drones:
The mobility and endurance tradeoff,” IEEE Vehicular Technology Magazine, vol. 15, no. 4, pp. 103–111, 2020.
[11] M. A. Kishk, A. Bader, and M.-S. Alouini, “On the 3-D placement of airborne base stations using tethered UAVs,” IEEE
| Transactions | on Communications, |     | vol. | 68, no. 8, | pp. 5202–5215, |     | 2020. |     |
| ------------ | ------------------ | --- | ---- | ---------- | -------------- | --- | ----- | --- |
[12] M.ErdeljandE.Natalizio,“UAV-assisteddisastermanagement:Applicationsandopenissues,”inInternationalConference
on Computing, Networking and Communications (ICNC). IEEE Computer Society, Kauai, Hawaii, USA, 2016, pp. 1–5.
[13] O. H. Graven, J.-V. Sørli, J. Bjørk, D. A. H. Samuelsen, and J. D. Bjerknes, “Managing disasters-rapid deployment of
sensornetworkfromdrones:Providingfirstresponderswithvitalinformation,”in2ndInternationalConferenceonControl
| and Robotics | Engineering | (ICCRE). |     | IEEE, Bangkok, |     | Thailand, | 2017, | pp. 184–188. |
| ------------ | ----------- | -------- | --- | -------------- | --- | --------- | ----- | ------------ |
[14] C.A.F.Ezequiel,M.Cua,N.C.Libatique,G.L.Tangonan,R.Alampay,R.T.Labuguen,C.M.Favila,J.L.E.Honrado,
V.Canos,C.Devaney,A.Loreto,J.Bacusmo,andB.Palma,“UAVaerialimagingapplicationsforpost-disasterassessment,
environmental management and infrastructure development,” in International Conference on Unmanned Aircraft Systems
| (ICUAS). | IEEE, Orlando, | Florida, | USA, | 2014, | pp. 274–283. |     |     |     |
| -------- | -------------- | -------- | ---- | ----- | ------------ | --- | --- | --- |
[15] S. A. R. Naqvi, S. A. Hassan, H. Pervaiz, and Q. Ni, “Drone-aided communication as a key enabler for 5G and resilient
| public safety | networks,” | IEEE | Communications |     | Magazine, | vol. 56, | no. | 1, pp. 36–42, 2018. |
| ------------- | ---------- | ---- | -------------- | --- | --------- | -------- | --- | ------------------- |
[16] M. Y. Selim and A. E. Kamal, “Post-disaster 4G/5G network rehabilitation using drones: Solving battery and backhaul
| issues,” | in IEEE Globecom | Workshops |     | (GC Wkshps), | Abu | Dhabi, | UAE, | 2018, pp. 1–6. |
| -------- | ---------------- | --------- | --- | ------------ | --- | ------ | ---- | -------------- |
[17] S. Shakoor, Z. Kaleem, M. I. Baig, O. Chughtai, T. Q. Duong, and L. D. Nguyen, “Role of UAVs in public safety
communications: Energy efficiency perspective,” IEEE Access, vol. 7, pp. 140665–140679, 2019.
[18] R. Masroor, M. Naeem, and W. Ejaz, “Efficient deployment of UAVs for disaster management: A multi-criterion
| optimization | approach,” | Computer | Communications, |     | vol. | 177, pp. | 185–194, | 2021. |
| ------------ | ---------- | -------- | --------------- | --- | ---- | -------- | -------- | ----- |
[19] R. Arshad, L. Lampe, H. ElSawy, and M. J. Hossain, “Integrating UAVs into existing wireless networks: A stochastic
geometry approach,” in IEEE Globecom Workshops (GC Wkshps), Abu Dhabi, UAE, 2018, pp. 1–6.
[20] M. Alzenad and H. Yanikomeroglu, “Coverage and rate analysis for vertical heterogeneous networks (VHetNets),” IEEE
| Transactions | on Wireless | Communications, |     | vol. | 18, no. | 12, pp. 5643–5657, |     | 2019. |
| ------------ | ----------- | --------------- | --- | ---- | ------- | ------------------ | --- | ----- |

29
[21] M.Matracia,M.A.Kishk,andM.-S.Alouini,“CoverageanalysisforUAV-assistedcellularnetworksinruralareas,”IEEE
Open Journal of Vehicular Technology, vol. 2, pp. 194–206, 2021.
[22] N. Kouzayha, H. ElSawy, H. Dahrouj, K. Alshaikh, T. Y. Al-Naffouri, and M.-S. Alouini, “Stochastic geometry analysis
of hybrid aerial terrestrial networks with mmWave backhauling,” in IEEE International Conference on Communications
(ICC), Dublin, Ireland, 2020, pp. 1–7.
[23] A.M.Hayajneh,S.A.R.Zaidi,D.C.McLernon,M.DiRenzo,andM.Ghogho,“PerformanceanalysisofUAVenabled
disaster recovery networks: A stochastic geometric framework based on cluster processes,” IEEE Access, vol. 6, pp.
26215–26230, 2018.
[24] M. Afshang and H. S. Dhillon, “Fundamentals of modeling finite wireless networks using binomial point process,” IEEE
Transactions on Wireless Communications, vol. 16, no. 5, pp. 3355–3370, 2017.
[25] V. V. Chetlur and H. S. Dhillon, “Downlink coverage analysis for a finite 3-D wireless network of unmanned aerial
vehicles,” IEEE Transactions on Communications, vol. 65, no. 10, pp. 4543–4558, 2017.
[26] J. G. Andrews, F. Baccelli, and R. K. Ganti, “A tractable approach to coverage and rate in cellular networks,” IEEE
Transactions on Communications, vol. 59, no. 11, pp. 3122–3134, 2011.
[27] M. Haenggi, Stochastic Geometry for Wireless Networks. Cambridge University Press, 2012.
[28] J.G.Andrews,A.K.Gupta,andH.S.Dhillon,“Aprimeroncellularnetworkanalysisusingstochasticgeometry,”2016.
[Online]. Available: https://arxiv.org/abs/1604.03183
[29] B. Galkin, J. Kibilda, and L. A. DaSilva, “A stochastic model for UAV networks positioned above demand hotspots in
urban environments,” IEEE Transactions on Vehicular Technology, vol. 68, no. 7, pp. 6985–6996, 2019.
[30] H. Alzer, “On some inequalities for the incomplete gamma function,” Mathematics of Computation, vol. 66, no. 218, pp.
771–778, 1997.
[31] T.BaiandR.W.Heath,“Coverageandrateanalysisformillimeter-wavecellularnetworks,”IEEETransactionsonWireless
Communications, vol. 14, no. 2, pp. 1100–1114, 2015.
Maurilio Matracia [S’21] received his M.Sc. degree in Electrical Engineering from the University of Palermo (UNIPA), Italy,
in 2019. He is currently a Doctoral Student at the Communication Theory Lab (CTL), King Abdullah University of Science
and Technology (KAUST), Kingdom of Saudi Arabia (KSA). His main research interest is stochastic geometry, with a special
focus on rural and emergency communications.
Mustafa A. Kishk [S’16, M’18] received his Ph.D. degree in Electrical Engineering from Virginia Tech, USA, in 2018. He
is currently an Assistant Professor with the Electronic Engineering Department, Maynooth University, Ireland. His research
interests include stochastic geometry, energy harvesting wireless networks, UAV-enabled communication systems, and satellite
communications. His current research interests include stochastic geometry, energy-harvesting wireless networks, UAV-enabled
communication systems, and satellite communications.

30
Mohamed-Slim Alouini [S’94, M’98, SM’03, F’09] was born in Tunis, Tunisia. He received his Ph.D. degree in Electrical
Engineering from California Institute of Technology (Caltech), Pasadena, CA, USA. He served as a faculty member at the
UniversityofMinnesota,Minneapolis,MN,USA,thenatTexasA&MUniversityatQatar,EducationCity,Doha,Qatar,before
joining KAUST as a Professor of Electrical Engineering in 2009. His current research interests include modeling, design, and
performance analysis of wireless communication systems.