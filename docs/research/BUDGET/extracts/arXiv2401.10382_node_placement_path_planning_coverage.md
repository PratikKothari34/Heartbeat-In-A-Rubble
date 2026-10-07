> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> arXiv **2401.10382** - *Node placement and path planning for coverage in a mixed WSN*.
> Source PDF deleted after conversion.
>
> Listed in `docs/research/BUDGET/01-literature.md` deployment row 3 as **HELD**, no figure
> quoted. A **MILP formulation for static + mobile node coverage** - the formal version of the
> deployment grid in `docs/MASTER.md` section 8.2. The most directly useful of the deployment
> papers if the proposal needs to show the placement problem is well-posed.

1
| Node |          | Placement |     |       | and    |     | Path   | Planning       |         |        | for  | Improved |          |     |     |
| ---- | -------- | --------- | --- | ----- | ------ | --- | ------ | -------------- | ------- | ------ | ---- | -------- | -------- | --- | --- |
| Area | Coverage |           |     | in    | Mixed  |     |        | Wireless       |         | Sensor |      |          | Networks |     |     |
|      |          |           |     | Survi | Kumari | and | Seshan | Srirangarajan, | Member, |        | IEEE |          |          |     |     |
Abstract—Forthelarge-scalemonitoringofaphysicalphenom- the entire area of interest at all time instances is referred to as
| ena using | a wireless | sensor | network | (WSN), | a   | large number |     | of         |           |     |          |         |               |     |          |
| --------- | ---------- | ------ | ------- | ------ | --- | ------------ | --- | ---------- | --------- | --- | -------- | ------- | ------------- | --- | -------- |
|           |            |        |         |        |     |              |     | continuous | coverage. |     | However, | in many | applications, |     | periodic |
staticand/ormobilesensornodesarerequired,resultinginhigher
|            |       |               |     |         |              |           |     | monitoring | is sufficient |     | instead | of continuous |     | monitoring, | and |
| ---------- | ----- | ------------- | --- | ------- | ------------ | --------- | --- | ---------- | ------------- | --- | ------- | ------------- | --- | ----------- | --- |
| deployment | cost. | In this work, | we  | develop | an efficient | algorithm |     |            |               |     |         |               |     |             |     |
thisisreferredtoassweepcoverage.Typicalexamplesinclude
| that can | employ | a small | number | of static | nodes | together | with |     |     |     |     |     |     |     |     |
| -------- | ------ | ------- | ------ | --------- | ----- | -------- | ---- | --- | --- | --- | --- | --- | --- | --- | --- |
4202 naJ 81  ]IN.sc[  1v28301.1042:viXra
a set of mobile nodes for improved area coverage. An efficient data gathering and message ferrying [7], [8]. For a mixed
deployment of static nodes and guided mobility of the mobile WSN, efficient path planning strategies need to be developed
| nodes is      | critical | for maximizing    |         | the area     | coverage.   | To       | this end, |             |             |            |      |                |               |           |           |
| ------------- | -------- | ----------------- | ------- | ------------ | ----------- | -------- | --------- | ----------- | ----------- | ---------- | ---- | -------------- | ------------- | --------- | --------- |
|               |          |                   |         |              |             |          |           | for mobile  | nodes       | to achieve |      | sweep/periodic |               | coverage. |           |
| we propose    | three    | mixed             | integer | linear       | programming |          | (MILP)    |             |             |            |      |                |               |           |           |
|               |          |                   |         |              |             |          |           | Coverage    | path        | planning   | has  | been           | and continues |           | to be an  |
| formulations. | The      | first formulation |         | efficiently  |             | deploys  | a set     | of          |             |            |      |                |               |           |           |
|               |          |                   |         |              |             |          |           | active area | of research |            | with | the growing    | popularity    |           | of mobile |
| static nodes  | and      | the other         | two     | formulations | plan        | the path | of        | a           |             |            |      |                |               |           |           |
set of mobile nodes so as to maximize the area coverage and nodesintheformofmobilerobotsandunmannedaerialvehi-
minimizethetotalnumberofmovementsrequiredtoachievethe cles. The use of mobile nodes in WSNs for improving sweep
| desired         | coverage. | We present   | extensive  |                | performance   | evaluation     |          |             |          |               |           |               |           |            |             |
| --------------- | --------- | ------------ | ---------- | -------------- | ------------- | -------------- | -------- | ----------- | -------- | ------------- | --------- | ------------- | --------- | ---------- | ----------- |
|                 |           |              |            |                |               |                |          | coverage    | has been | addressed     |           | through       | different |            | approaches. |
| of the proposed |           | algorithms   | and        | its comparison |               | with benchmark |          |             |          |               |           |               |           |            |             |
|                 |           |              |            |                |               |                |          | The authors | in       | [9] presented |           | approximation |           | algorithms | that        |
| approaches.     | The       | simulation   | results    | demonstrate    |               | the            | superior |             |          |               |           |               |           |            |             |
|                 |           |              |            |                |               |                |          | minimize    | the time | taken         | by mobile | nodes         | for       | visiting   | a set of    |
| performance     | of        | the proposed | algorithms |                | for different |                | network  |             |          |               |           |               |           |            |             |
sizes and number of static and mobile nodes. targets. The objective is to reduce the target detection period,
|                    |              |         |              |                |        |               |     | while minimizing |            | the     | trajectory    | length          | of       | the mobile | nodes.    |
| ------------------ | ------------ | ------- | ------------ | -------------- | ------ | ------------- | --- | ---------------- | ---------- | ------- | ------------- | --------------- | -------- | ---------- | --------- |
| Index              | Terms—Mobile |         | nodes,       | area coverage, |        | mixed-integer |     |                  |            |         |               |                 |          |            |           |
|                    |              |         |              |                |        |               |     | In [10],         | the static | sensors |               | detect coverage |          | holes      | by using  |
| linear programming |              | (MILP), | mixed        | wireless       | sensor | network.      |     |                  |            |         |               |                 |          |            |           |
|                    |              |         |              |                |        |               |     | Voronoi          | diagrams   | and     | bid for       | mobile          | sensors  | based      | on the    |
|                    |              |         |              |                |        |               |     | size of the      | coverage   |         | hole detected |                 | by them. | Mobile     | sensors   |
|                    |              | I.      | INTRODUCTION |                |        |               |     |                  |            |         |               |                 |          |            |           |
|                    |              |         |              |                |        |               |     | accept the       | highest    | bids    | and move      | to              | heal the | largest    | holes. To |
Wireless sensor networks (WSN) are being used in various reducethemovementdistanceofmobilenodes,aproxy-based
monitoring or surveillance applications and ensuring full area bidding protocol is employed where mobile sensors perform
coverage is one of the key objectives in such applications [1]. virtual movements from small holes to large holes and only
Deployment of only static nodes typically leads to coverage perform physical movements after the final destinations are
| holes and | overlapping | coverage |     | due to | sub-optimal | placement |     | identified. |     |     |     |     |     |     |     |
| --------- | ----------- | -------- | --- | ------ | ----------- | --------- | --- | ----------- | --- | --- | --- | --- | --- | --- | --- |
of nodes and/or nodes becoming non-functional over a period In[2],theauthorsconsidervariouscostmeasurestoaddress
of time after the initial deployment. Increasing the number of trade-offs between area coverage and distance traveled by
nodes or their sensing region are typically not cost effective. mobile nodes or information exchange among nodes. In [11],
In addition, these measures do not address the issue of non- the authors proposed a distributed technique for iteratively
functional nodes or overlapping coverage or the effect of computing the paths for mobile nodes in a greedy manner.
environmental factors on the network. Thus, a mixed WSN, They employ a bidding approach similar to that in [10] while
a network with combination of static and mobile nodes, has usingthemovementschemedescribedin[2],[12].Inaddition,
been proposed to address these limitations [2], [3]. the static nodes employ the zoom algorithm to determine the
Mobilityinsensornodesistheabilityofthenodestomove largest hole [13], [14]. A review of several other methods that
and change their locations post their initial deployment. With exploit mobility of nodes for network coverage problems can
theadvancementintechnology,theapplicationsofmobilesen- be found in [15], [16].
sor nodes have gradually increased. The use of mobile nodes Our work is inspired by [17], which proposes an optimiza-
significantly improves the possibility of maintaining a robust tion framework to plan the path of a single mobile node to
network coverage [4]. In WSN literature and applications, the maximize area coverage and/or minimize the total trip time
mobility of nodes is primarily exploited in two ways. In some for the mobile node. In this work, we present strategies to
cases, the fusion center or sink is mobile and the mobile sink plan the path of a set of mobile nodes to achieve sweep
moves throughout the network area to gather data from the coveragethroughperiodicmonitoringofthenetworkarea.The
sensing nodes [5], [6]. In other cases, one or more of the proposed system model assumes a small number of mobile
sensing nodes are mobile and move through the network area sensor nodes along with a limited number of static sensor
to record data along with location information and deliver the nodes. The objective is to plan the paths of the mobile nodes,
collected data to the fusion center. primarily over the uncovered areas, so as to improve the
A WSN is usually deployed in an area of interest for overall area coverage and total trip time. We also propose
monitoring or detection applications. The ability to monitor an algorithm for the deployment of static nodes that aids

2
j=N TABLEI
NOTATIONS
Symbol Definition
Ns Numberofstaticsensornodes
L Numberofmobilesensornodes
C,|C| Setofallthecellsinthenetworkareaanditscardinality
B Setofcellsattheboundaryofthenetworkarea
A Setofcellsotherthantheboundarycells
C1 Setofcellsnotcoveredbystaticnodes
C2 Setofcellscoveredbystaticnodes
cr Areacoverageratio
rs Sensingradiusofasensornode
ρx,ρy One-step traveling range of mobile node along x and y
directions
j=1 co Overlappingcellcoveragefactor
i=1 i=M Kmax Maximumnumberofiterations
Staticsensornode Mobilesensornode xs xs =1ifthesth staticsensornodeislocatedatcell(i,j),
i,j i,j
otherwisexs =0.
Fig. 1. A typical network area. The colored cells around a sensor node xl,k xl,k=1if i t , h j elth mobilenodeislocatedatcell(i,j)inthe
indicate the sensing region of that sensor node (rs = 1). The cells marked i,j i,j
with diagonal lines around each mobile node represent potential locations kth iteration.
wherethemobilenodecouldmovetointhenextiteration(ρx=ρy =2). cs i,j cs i,j =1ifthecell(i,j)iscoveredbythesth staticsensor
node,otherwisecs =0.
i,j
cl,k cl,k =1ifthecell(i,j)iscoveredbythelth mobilenode
i,j i,j
in the path planning of the mobile nodes by avoiding the inthekth iteration,otherwisecl,k=0.
i,j
challenges that can arise due to a random deployment of ci,j ci,j =1ifthecell(i,j)iscoveredbyasensornodeduring
static nodes, such as boundary coverage holes [18], network
anyiteration,otherwiseci,j =0.
partition, and redundant coverage [12]. The proposed system
model includes a parameter that determines the permissible
such that r is the number of cells that can be sensed by a
levelofredundantcoverageoroverlappingcoverageduringthe s
node in each direction from its current location. The network
path planning process. The proposed strategies are formulated
is assumed to be connected such that the sensor nodes can
as mixed integer linear programming (MILP) problems. The
communicate with the sink node at all times.
key contributions of this work are as follows:
After the initial deployment of static nodes is completed,
• An MILP-Static formulation that places static nodes
the paths to be followed by the mobile nodes is planned
to maximize area coverage with more weight given to
centrally. The path planning is an iterative procedure where
covering the network boundary areas.
the location of each mobile node is computed simultaneously
• An MILP-Cov formulation that plans the path of a set of
at each iteration. The mobile nodes sense the parameter(s) of
mobilenodeswhilemaximizingthecoverageareawithin
interest in the cells within their sensing range r and then
a given number of movements or time steps. s
move to their next locations within the one-step traveling
• An MILP-Mov formulation that plans the path of a
range, denoted by ρ and ρ along the x and y directions,
set of mobile nodes while minimizing the number of x y
respectively. The one-step traveling range of a mobile node is
movements required to achieve a desired coverage level.
the maximum number of cells up to which the mobile node
• Extensivesimulationscomparingperformanceofthepro-
can move in each direction from its current location in one
posed algorithms with benchmark methods and compu-
iteration.Thecoverageratio,denotedbycr,istheratioofthe
tational complexity analysis.
numberofgridcellscoveredatleastonceinanyiterationand
the total number of grid cells within the network area; thus,
II. SYSTEMMODEL
0≤cr ≤1. An example network area is shown in Fig. 1.
Consider a rectangular network area which is subdivided
intogridswithM×N unitsquarecells.Eachgridcelllocation
is denoted by coordinates (i,j) with 1≤i≤M and 1≤j ≤
III. PROPOSEDSTRATEGIES
N. We assume a mixed WSN, consisting of a few static and
mobile nodes for monitoring the network area, and a single
In this section, we describe the proposed algorithms for the
data sink node. The first objective is to place the static nodes
placement of static nodes and path planning of the mobile
withinthenetworkareainamannerthataidsthepathplanning
nodes. Consider the variables xs and xl,k which indicate the
of the mobile nodes. Next, we plan the paths of the mobile i,j i,j
locationsofstaticandmobilenodes,respectively.Also,letcs ,
nodes to maximize the area coverage and minimize the trip i,j
cl,k, and c be the coverage variables. These variables are
time. The key parameters of the proposed system model are i,j i,j
listed in Table I, which are described next. definedinTableI.Wedefinexs andxl,k asbinaryvariables,
i,j i,j
LetN andLdenotethenumberofstaticandmobilenodes, whereas c , cs , and cl,k are defined as continuous variables
s i,j i,j i,j
respectively. The coordinate of the grid cell in which a sensor in the range [0,1]. Thus, the proposed node placement and
islocatedisdefinedasthelocationofthatsensor.Letr denote path planning strategies result in MILP formulations which
s
the sensing radius (or sensing range) of static/mobile nodes are described next.

3
of covered cells, where α is a weight parameter associated
with the coverage of the boundary cells. Using α > 1, gives
more importance to the coverage of the boundary cells. We
use α = 4 in our simulations. (2) is the position constraint
which ensures that each static node is placed in only one cell.
The constraint (3) ensures that a cell (i,j) is considered as
coveredbythesth staticnode,i.e.,cs =1,ifthecell(i,j)is
i,j
withinthesensingrangeofthesthstaticnode.Theoverlapping
coverage constraint (4) ensures that each cell is covered by at
most c static nodes.
(a) (b) o
B. Coverage Maximization
Afterthestaticnodeshavebeenplaced(usingMILP-Static),
the mobile nodes must traverse the network area to cover
the uncovered cells (i,j) ∈ C , so as to maximize the area
1
coverage.Thepathplanningofthemobilenodes,tomaximize
areacoverage,canbeformulatedasthefollowingoptimization
problem and is referred to as MILP-Cov.
(cid:88)
max c (5)
i,j
(i,j)∈C1
(c) (d) (cid:88)
s.t. xl,k =1, l=1,...,L,k =1,...,K (6)
i,j max
Fig.2. Possiblechallengesduetorandomdeploymentofstaticsensornodes (i,j)∈C1
in a network area. (a), (b) network partition, (c) boundary coverage hole,
and(d)overlapping/redundantcoverage. (cid:88)
ρx
(cid:88)
ρy
xl,k+1 = xl,k , ∀(i,j)∈C , (7)
i,j i+p,j+q 1
p=−ρxq=−ρy
A. Static Node Placement l=1,...,L,k =1,...,(K −1)
max
The first step is to place the static sensor nodes within (cid:88) rs (cid:88) rs
cl,k = xl,k , ∀(i,j)∈C , (8)
the network area so as to maximize the area coverage. As i,j i+p,j+q 1
noted earlier, the random deployment of static nodes can p=−rsq=−rs
result in challenges such boundary coverage holes, network l=1,...,L,k =1,...,K max
partitioning, and redundant coverage. Some of these scenarios c ≥cl,k,∀(i,j)∈C , ∀l=1,...,L,k =1,...,K (9)
i,j i,j 1 max
are illustrated in Fig. 2. In addition, if the static nodes do
(cid:88) L K (cid:88)max
not cover the boundary cells, the mobile nodes would have c ≤ cl,k, ∀(i,j)∈C (10)
i,j i,j 1
to cover these resulting in a larger number of movements
l=1 k=1
and redundant coverage. Thus, in the proposed static node (cid:88) L K (cid:88)max
placement strategy we would like to maximize the covered cl,k ≤c , ∀(i,j)∈C (11)
i,j o 1
areawhilegivingmoreimportance/weighttocoveringthecells
l=1 k=1
at the network boundary. 0≤c ,cl,k ≤1,∀(i,j)∈C ,l=1,...,L,k =1,...,K
i,j i,j 1 max
Let B represent the set of cells at the boundary of the
(12)
network area. It can be seen that |B| = 2(M + N − 2).
Theobjectivefunctionin(5)maximizestheareacoveredby
The static node placement can be formulated as the following
the mobile nodes from the uncovered set as they traverse the
optimization problem, referred to as MILP-Static.
networkareaoverK iterations.(6)isthepositionconstraint
  max
(cid:88)
Ns
(cid:88)
Ns whichensuresthateachmobilenodeislocatedinonlyonecell
max cs + αcs  (1) in any given iteration. The mobility constraint in (7) restricts
 i,j i,j
s=1 s=1 the distance that each mobile node can travel along x and y
(i,j)∈A (i,j)∈B
directions to ρ and ρ , respectively. (8)-(10) represent the
(cid:88) x y
s.t. xs i,j =1, s=1,...,N s (2) cell coverage constraints. Constraint (8) states that cell (i,j)
(i,j)∈C issaidtobecoveredbythelth mobilenodeinthekth iteration,
cs i,j = (cid:88)
rs
(cid:88)
rs
xs i+p,j+q ,∀(i,j)∈C 1 ,s=1,...,N s (3) t
i
h
.e
e
.,
lt
c
h
l
i
,
, m
k
j o
=
bi
1
le
,
n
if
od
th
e
e
a
c
t
e
t
l
h
l
e
(
k
i,
th
j)
ite
is
ra
w
tio
it
n
h
.
in
Co
th
n
e
st
s
ra
e
i
n
n
s
t
in
(9
g
)
r
s
a
e
n
t
g
s
e
c i
o
,j
f
p=−rsq=−rs to zero if cell (i,j) is not covered by any mobile node during
(cid:88) Ns anyiteration.Constraint(10)ensuresthatifacelliscoveredin
cs ≤c , ∀(i,j)∈C (4)
i,j o any iteration by a mobile node, it is considered as covered for
s=1 the rest of the algorithm. Constraint (11) allows for limited
The objective function in (1) maximizes the total number overlap or redundancy in coverage (i.e., allows each cell to

4
be covered at most c o times) due to multiple mobile nodes TABLEII
covering the same cell across iterations. This is essential to AREACOVERAGE(MILP-COV)USINGTWODIFFERENTSTATICNODE
PLACEMENTSTRATEGIES:RANDOMANDMILP-STATIC.
ensure that area coverage can be maximized while allowing
s
m
o
o
m
b
e
ile
re
n
d
o
u
d
n
e
da
p
n
a
c
th
y
s
in
ge
c
t
o
ti
v
n
e
g
ra
s
g
tu
e
c
.
k
Se
a
t
t
t
a
in
c
g
e
c
ll
o
b
=
efo
1
re
m
K
ayres
i
u
te
lt
ra
in
tio
th
n
e
s
NetworkSize L Ns
Ra
A
nd
re
o
a
m
Cove
M
ra
I
g
L
e
P-
(
S
%
ta
)
tic
max
at the cost of limiting the area coverage. 1 3 63.18 85.93
1 5 68.23 100
2 3 95.93 100
8×8
C. Movement Minimization 2 5 93.39 100
3 3 100 100
An alternative strategy for planning the paths of the mobile
3 5 94.47 100
nodes is to minimize the total number of movements by the 1 3 42.12 60
mobile nodes for attaining a desired coverage ratio (cr). This 1 5 44.91 77
can be formulated as the following optimization problem and 10×10 2 3 75.11 88
2 5 78.14 96
is referred to as MILP-Mov.
3 3 93.24 99
K (cid:88)max (cid:88) L 3 5 94.88 100
min xl,k (13)
i,j
k=1 l=1
(i,j)∈C1 MILP-CovandMILP-Movwhilec o =1forMILP-Static.The
s.t. (cid:88) xl,k ≤1,l=1,...,L,k =1,...,K (14) algorithms were implemented in MATLAB R2020b and used
i,j max
12.10.0 version of IBM ILOG CPLEX optimization software.
(i,j)∈C1
(cid:88) The CPLEX parameter settings used include ‘TimeLimit’ of
c ≥cr·|C| (15)
i,j 18000 s, ‘MIPGap’ of 0, and branch and cut method as the
(i,j)∈C ‘MIP Strategy Search’.
Constraints (7), (8), (9), (10), (11), (12)
B. Static Node Placement
The objective function in (13) minimizes the total number
of cells that are visited by the mobile nodes while achieving We first compare the two static node placement strategies,
the desired coverage ratio. The number of cells visited by random and MILP-Static, in terms of area coverage. We
the mobile nodes represents the number of mobile node assume that after the static node placement, the paths of the
movements. (14) is the position constraint, which is similar to mobilenodesareplannedusingMILP-Cov.TableIIcompares
the position constraint (6) of MILP-Cov, except that MILP- the network area coverage achieved using different numbers
Mov allows the possibility that after a certain number of of mobile and static sensor nodes for two network sizes. In
iterations xl,k for all the mobile nodes can be zero. This the random placement strategy, the static nodes are placed
i,j
implies that all the mobile nodes would stop their movements according to a uniform distribution. The area coverage values
assoonasthedesiredcoverageratioisachieved.(15)indicates reported are obtained with K max = 4 and by averaging over
thatthetotalcoverageachievedbythestaticandmobilenodes fivesimulationruns.Theresultsindicatethattheareacoverage
must satisfy the desired coverage ratio. performance is significantly better in the case where the static
It is to be noted that even though c , cs , and cl,k have nodes are placed using the MILP-Static strategy, as compared
i,j i,j i,j
beendefinedascontinuousvariables,duetotheirdefinedrange to random placement. Based on these results, for the rest of
and other constraints, they will behave as binary variables. thesimulationsofMILP-CovandMILP-Mov,theMILP-Static
Thisisbecausetheconstraintshavebeenformulatedsuchthat algorithm will be used for the placement of static nodes.
they can only take values 0 or 1. They have been defined
as continuous variables in order to reduce the complexity of C. MILP-Cov and MILP-Mov Performance
the integer linear programs (ILPs). It is well-known that the In Fig. 3, we compare the performance of MILP-Cov,
complexityofILPsincreaseexponentiallywiththenumberof MILP-Mov, random movement, and greedy approaches in
binary/integer variables [17]. terms of the area coverage, with three mobile nodes. In the
greedy approach, each mobile node considers the cells within
IV. SIMULATIONRESULTS its one-step traveling range and moves to the cell location
that would cover the maximum number of cells which are yet
In this section, we present detailed performance analysis of
to be covered. On the other hand, in the random movement
the proposed MILP-based node placement and path planning
approach, each mobile node moves to a cell that is selected
algorithms.
randomly from all the potential cells within its one-step trav-
elingrange.ItisseenthatMILP-Covconsistentlyoutperforms
A. Simulation Setup
random and greedy approaches with the greedy approach
We consider network area of sizes ranging from 8×8 to performing better than the random movement approach. With
15×15withgridcellsofsize1×1.Thenumberofstaticand N =0 or 1, the area coverage using MILP-Mov and greedy
s
mobilenodesarevariedintherange0-10and1-5,respectively. approachesissimilarsincewiththislevelofcoveragethrough
We assume sensing range r = 1, one-step traveling range staticnode,theoverallcoveragesearchspacedoesnotchange
s
ρ =ρ =2, and overlapping cell coverage factor c =3 for significantly.
x y o

5
|     |     |     | Network size: 8 x 8 |     |     |     |     | Network size: 12 x 12 |     |     |     |
| --- | --- | --- | ------------------- | --- | --- | --- | --- | --------------------- | --- | --- | --- |
|     | 100 |     |                     |     |     |     | 35  |                       |     |     |     |
L=3
L=4
30
|     | 80  |     |     |     |     |     | stn |     |     |     | L=5 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
)%
e25 m
( e
|     | g 60 |     |     |     | R a n d o m     |     | e v  |     |     |     |     |
| --- | ---- | --- | --- | --- | --------------- | --- | ---- | --- | --- | --- | --- |
|     | a    |     |     |     |                 |     | o 20 |     |     |     |     |
|     | r    |     |     |     | G r ee d y      |     | M    |     |     |     |     |
|     | e v  |     |     |     | M I L P - M o v |     |  fo  |     |     |     |     |
|     | o    |     |     |     |                 |     | 15   |     |     |     |     |
|     | C 40 |     |     |     | M I L P - Co v  |     |  r   |     |     |     |     |
|     |  a   |     |     |     |                 |     | e b  |     |     |     |     |
|     | e r  |     |     |     |                 |     | m10  |     |     |     |     |
|     | A    |     |     |     |                 |     | u    |     |     |     |     |
|     | 20   |     |     |     |                 |     | N    |     |     |     |     |
5
|     |     | 0                      |                       |     |     |     | 0   |                        |     |     |     |
| --- | --- | ---------------------- | --------------------- | --- | --- | --- | --- | ---------------------- | --- | --- | --- |
|     |     | 0                      | 1                     |     | 5   |     |     | 0                      | 5   |     | 10  |
|     |     | Number of Static Nodes |                       |     |     |     |     | Number of Static Nodes |     |     |     |
|     |     |                        | (a)                   |     |     |     |     |                        | (a) |     |     |
|     |     |                        | Network size: 10 x 10 |     |     |     |     | Network size: 15 x 15  |     |     |     |
|     | 100 |                        |                       |     |     |     | 60  |                        |     |     |     |
L=3
|     |     |     |     |     |     |     | 50  |     |     |     | L=4 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     | 80  |     |     |     |     |     | stn |     |     |     | L=5 |
)%
e
|     | ( e |     |     |     |             |     | m 40   |     |     |     |     |
| --- | --- | --- | --- | --- | ----------- | --- | ------ | --- | --- | --- | --- |
|     | 60  |     |     |     |             |     | e v    |     |     |     |     |
|     | g a |     |     |     | R a n d o m |     | o      |     |     |     |     |
|     | r   |     |     |     | G r ee d y  |     | M      |     |     |     |     |
|     | e v |     |     |     | MILP-Mov    |     |  fo 30 |     |     |     |     |
o
|     | C 40 |     |     |     | MILP-Cov |     |  r   |     |     |     |     |
| --- | ---- | --- | --- | --- | -------- | --- | ---- | --- | --- | --- | --- |
|     |  a   |     |     |     |          |     | e 20 |     |     |     |     |
|     | e    |     |     |     |          |     | b m  |     |     |     |     |
r A
|     | 20  |     |     |     |     |     | u N |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
10
|     |     | 0                      |     |     |     |     | 0   |                        |     |     |     |
| --- | --- | ---------------------- | --- | --- | --- | --- | --- | ---------------------- | --- | --- | --- |
|     |     | 0                      | 1   |     | 5   |     |     | 0                      | 5   |     | 10  |
|     |     | Number of Static Nodes |     |     |     |     |     | Number of Static Nodes |     |     |     |
|     |     |                        | (b) |     |     |     |     |                        | (b) |     |     |
Fig. 3. Area coverage using three (L = 3) mobile nodes with different Fig.4. Numberofmovementsrequiredbymobilenodesforfullareacoverage
numberofstaticnodes. (cr=1)usingMILP-Movwithdifferentnumberofstaticandmobilenodes.
| In  | Fig. 4, we | consider | the performance |     | of the MILP-Mov |             |         |            |       |      |                 |
| --- | ---------- | -------- | --------------- | --- | --------------- | ----------- | ------- | ---------- | ----- | ---- | --------------- |
|     |            |          |                 |     |                 | the Vecchio | method, | the mobile | nodes | stop | their movements |
strategy in terms of the number of movements needed to before achieving full coverage as they are unable to locate
achieve full area coverage (cr =1) for two different network the uncovered areas and wait endlessly while looking for the
sizes. The results show that, for a given network size, as the next location using the zoom algorithm [13], [14]. Although,
number of static and mobile nodes increases, the required the three methods show improved coverage performance with
| number   | of movements | decreases. |              |               |                  |                  |               |            |          |        |        |
| -------- | ------------ | ---------- | ------------ | ------------- | ---------------- | ---------------- | ------------- | ---------- | -------- | ------ | ------ |
|          |              |            |              |               |                  | increase         | in the number | of static  | and      | mobile | nodes. |
| In       | Fig. 5,      | we compare | performance  |               | of the MILP-Cov, |                  |               |            |          |        |        |
| MILP-Mov | algorithms,  |            | and the path | planning      | technique        | pre-             |               |            |          |        |        |
|          |              |            |              |               |                  | D. Computational |               | Complexity | Analysis |        |        |
| sented   | in [11],     | in terms   | of the       | area coverage | as a             | function         |               |            |          |        |        |
of the number of mobile node movements. We refer to the We analyze the complexity of the proposed methods in
method presented in [11] as Vecchio method, based on the termsofthenumberofcontinuousvariables,numberofinteger
first author’s last name. For a fair comparison, the initial variables, and the number of constraints. These are listed in
locations of the static and mobile nodes are kept the same TableIIIanditisseenthatthesecomplexitymeasuresincrease
for all the three algorithms. The initial locations of static and linearly with the network size and the number of nodes in
mobile nodes are obtained based on MILP-Static and MILP- the network. In Table IV, we list the number of movements
Mov algorithms, respectively. For implementing the Vecchio along with the computational time required for full coverage
method, we use r s = 1.5, r c = 2r s , µ = 2, ρ = 2, ϕ = π/6, by MILP-Cov and MILP-Mov methods for different network
n = 10, and these parameters have the same definitions as sizes and with different number of static and mobile nodes.
in [11]. The values of weight parameters associated with the The static node placement is performed using the proposed
cost function and other parameters are as given in [11]. From MILP-Static strategy. The simulations are performed on an
Fig. 5, it is seen that the proposed MILP-Cov and MILP- Intel(R) Core(TM) i7-8550U CPU @ 1.80 GHz-1.99 GHz,
Mov algorithms achieve full area coverage, and outperform 16 GB RAM, and running Microsoft Windows 10 Pro. The
the Vecchio method [11] by requiring much fewer mobile number of constraints in MILP-Cov and MILP-Mov only
node movements for achieving a given level of area coverage. differ by one, however MILP-Cov has a consistently lower
It is observed that the Vecchio method does not achieve full CPUtimethanMILP-Mov.Thisisbecause,inMILP-Mov,the
area coverage even with a very large number of movements objectivefunctioninvolvesbinaryvariablesandthecomplexity
and the coverage saturates at some point. In addition, in of ILP increases exponentially with integer/binary variables.

6
TABLEIII
COMPARISONOFTHENUMBEROFCONSTRAINTSANDVARIABLES.
|     |     | Method      |     | No.ofBinaryVariables |          | No.ofContinuousVariables |              |       |                          | No.ofConstraints |     |     |     |     |     |
| --- | --- | ----------- | --- | -------------------- | -------- | ------------------------ | ------------ | ----- | ------------------------ | ---------------- | --- | --- | --- | --- | --- |
|     |     | MILP-Cov    |     |                      | LKmax|C| |                          | (1+LKmax)|C| |       | LKmax(3|C|+1)+|C|(2−L)   |                  |     |     |     |     |     |
|     |     | MILP-Mov    |     |                      | LKmax|C| |                          | (1+LKmax)|C| |       | LKmax(3|C|+1)+|C|(2−L)+1 |                  |     |     |     |     |     |
|     |     | MILP-Static |     |                      | Ns|C|    |                          |              | Ns|C| |                          | Ns+(Ns+1)|C|     |     |     |     |     |     |
TABLEIV
|     | 100 |     |     |     |     |     |     | COMPARISONOFTHENUMBEROFMOVEMENTSANDCPUTIMES |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
REQUIREDFORFULLCOVERAGEBYMILP-COVANDMILP-MOV.
80
|     | )%     |     |     |     |     |     |     | Ne t w o rk |      |       | M o vem | en ts      |      | C PU Tim | e (s )    |
| --- | ------ | --- | --- | --- | --- | --- | --- | ----------- | ---- | ----- | ------- | ---------- | ---- | -------- | --------- |
|     |        |     |     |     |     |     |     |             | L Ns |       |         |            |      |          |           |
|     | ( e    |     |     |     |     |     |     | S i z e     |      | MILP- | Co v    | M IL P-Mov | MILP | -C ov M  | IL P -Mov |
|     | g a 60 |     |     |     |     |     |     |             | 0    | 17    |         | 16         | 7.2  |          | 1573.6    |
r
|     | e v |     |     |     |     |     |     | 10×10 | 3 5 | 12  |     | 11  | 1.3 |     | 6.4 |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- |
o
|     | C 40 |     |     |     |     |     |     |     | 10  | 8   |     | 6   | 1.5 |     | 2.3 |
| --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
 a
|     | e   |     |     |     |     |     |     |     | 0   | 32  |     | 32  | 454.2 |     | 18000 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | ----- |
r A
|     | 20  |     |     |     |     |     |     | 12×12 | 3 5 | 18  |     | 16  | 16.9 |     | 18000  |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | ---- | --- | ------ |
|     |     |     |     |     |     |     |     |       | 10  | 9   |     | 8   | 3.4  |     | 117.2  |
|     |     | 0   |     |     |     |     |     |       | 0   | 16  |     | 16  | 3.6  |     | 1536.8 |
|     |     | 0 5 | 10  | 15  | 20  | 25  |     | 10×10 | 4 5 | 12  |     | 11  | 1.2  |     | 31.9   |
Number of Movements
|     |     |     |     |     |     |     |     |       | 10  | 7   |     | 6   | 1.4   |     | 2.9     |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | ----- | --- | ------- |
|     |     |     |     | (a) |     |     |     |       | 0   | 28  |     | 25  | 137.6 |     | 18000   |
|     |     |     |     |     |     |     |     | 12×12 | 4 5 | 16  |     | 16  | 9.0   |     | 18000   |
|     |     |     |     |     |     |     |     |       | 10  | 10  |     | 7   | 3.6   |     | 164.8.1 |
|     |     |     |     |     |     |     |     |       | 0   | 16  |     | 16  | 5.6   |     | 3326.7  |
|     | 100 |     |     |     |     |     |     | 10×10 | 5 5 | 11  |     | 11  | 1.3   |     | 188.4   |
|     |     |     |     |     |     |     |     |       | 10  | 8   |     | 6   | 1.4   |     | 3.2     |
|     | 80  |     |     |     |     |     |     |       | 0   | 25  |     | 24  | 118.3 |     | 18000   |
)%
|     |     |     |     |     |     |     |     | 12×12 | 5 5 | 1   | 8   | 1 6 | 1   | 0 .4 | 1 8 0 0 0 |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | --- | --- | --- | --- | --- | ---- | --------- |
( e
|     | g 60 |     |     |     |     |     |     |     | 1 0 | 1   | 0   | 7   | 3   | .4  | 1 5 . 6 |
| --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- |
a
r e
v
|     | o C 40 |     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| --- | ------ | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
 a
e
r
A [2] T.P.LambrouandC.G.Panayiotou,“Collaborativepathplanningfor
20
|     |     |     |     |     |     |     |     | event | search and | exploration | in  | mixed | sensor networks,” | Int. | J. Robot. |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | ---------- | ----------- | --- | ----- | ----------------- | ---- | --------- |
Res.,vol.32,no.12,pp.1424–1437,2013.
0 [3] L.Zhu,C.Fan,H.Wu,andZ.Wen,“Coverageoptimizationalgorithmof
|     |     | 0 5 | 10  | 15  | 20  | 25  |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
wirelesssensornetworkbasedonmobilenodes,”Int.J.OnlineBiomed.
Number of Movements
Eng.,vol.12,no.08,p.45–50,2016.
(b) [4] B.Liu,P.Brass,O.Dousse,P.Nain,andD.Towsley,“Mobilityimproves
coverageofsensornetworks,”inProc.ACMInt.Symp.MobileAdHoc
Netw.Comput.,2005,p.300–308.
| Fig. 5. | Area coverage | as a | function | of the | number of movements |     | by the |               |         |     |        |             |         |          |       |
| ------- | ------------- | ---- | -------- | ------ | ------------------- | --- | ------ | ------------- | ------- | --- | ------ | ----------- | ------- | -------- | ----- |
|         |               |      |          |        |                     |     |        | [5] W. Liang, | J. Luo, | and | X. Xu, | “Prolonging | network | lifetime | via a |
mobilenodes(Networksize=10×10).
|     |     |     |     |     |     |     |     | controlled | mobile | sink | in wireless | sensor | networks,” | in  | IEEE Glob. |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ------ | ---- | ----------- | ------ | ---------- | --- | ---------- |
Telecommun.Conf.,2010,pp.1–6.
|     |     |     |     |     |     |     |     | [6] P.ZhongandF.Ruan,“Anenergyefficientmultiplemobilesinksbased |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
V. CONCLUSION
routingalgorithmforwirelesssensornetworks,”IOPConf.Ser.:Mater.
Sci.Eng.,vol.323,p.012029,2018.
| We  | have proposed | three | MILP-based |     | formulations, |     | MILP- |             |         |        |        |       |              |       |          |
| --- | ------------- | ----- | ---------- | --- | ------------- | --- | ----- | ----------- | ------- | ------ | ------ | ----- | ------------ | ----- | -------- |
|     |               |       |            |     |               |     |       | [7] X. Gao, | J. Fan, | F. Wu, | and G. | Chen, | “Cooperative | sweep | coverage |
Static, MILP-Cov, and MILP-Mov, for efficient placement problem with mobile sensors,” IEEE Trans. Mobile Comput., vol. 21,
of static nodes and path planning of mobile nodes in order no.2,pp.480–494,2022.
|             |     |             |      |          |     |          |     | [8] X. Gao, | X. Zhu, | Y. Feng, | F. Wu, | and | G. Chen, | “Data ferry | trajectory |
| ----------- | --- | ----------- | ---- | -------- | --- | -------- | --- | ----------- | ------- | -------- | ------ | --- | -------- | ----------- | ---------- |
| to maximize |     | the network | area | coverage | and | minimize | the |             |         |          |        |     |          |             |            |
planningforsweepcoverageproblemwithmultiplemobilesensors,”in
number of mobile node movements to achieve a desired area IEEEInt.Conf.Sens.Commun.Netw.,2016,pp.1–9.
coverage. The static node placement strategy addresses the [9] X. Gao, J. Fan, F. Wu, and G. Chen, “Approximation algorithms for
|     |     |     |     |     |     |     |     | sweep | coverage | problem | with | multiple | mobile | sensors,” | IEEE/ACM |
| --- | --- | --- | --- | --- | --- | --- | --- | ----- | -------- | ------- | ---- | -------- | ------ | --------- | -------- |
issuesthatcanariseduetorandomdeploymentofstaticnodes
Trans.Netw.,vol.26,no.2,pp.990–1003,2018.
| and the | path | planning | strategies | allow | for an explicit |     | limit on |                                                                |     |     |     |     |     |     |     |
| ------- | ---- | -------- | ---------- | ----- | --------------- | --- | -------- | -------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
|         |      |          |            |       |                 |     |          | [10] G.Wang,G.Cao,P.Berman,andT.F.LaPorta,“Biddingprotocolsfor |     |     |     |     |     |     |     |
overlapping/redundant coverage. The proposed path planning deployingmobilesensors,”IEEETrans.MobileComput.,vol.6,no.5,
methods achieve improved area coverage and improve the pp.563–576,2007.
M.VecchioandR.Lo´pez-Valcarce,“Improvingareacoverageofwire-
| sweep | coverage | time | by minimizing |     | the number | of  | move- | [11] |     |     |     |     |     |     |     |
| ----- | -------- | ---- | ------------- | --- | ---------- | --- | ----- | ---- | --- | --- | --- | --- | --- | --- | --- |
lesssensornetworksviacontrollablemobilenodes:Agreedyapproach,”
ments, which in turn can improve the network lifetime. J.Netw.Comput.Appl.,vol.48,pp.1–13,2015.
|     |     |     |     |     |     |     |     | [12] T. Lambrou, | C.       | Panayiotou, | S.        | Felici-Castell, | and       | B. Beferull-Lozano, |        |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------------- | -------- | ----------- | --------- | --------------- | --------- | ------------------- | ------ |
|     |     |     |     |     |     |     |     | “Exploiting      | mobility | for         | efficient | coverage        | in sparse | wireless            | sensor |
REFERENCES networks,”WirelessPers.Commun.,vol.54,pp.187–201,2010.
|     |     |     |     |     |     |     |     | [13] T. P. | Lambrou | and C. | G. Panayiotou, |     | “Collaborative | event | detection |
| --- | --- | --- | --- | --- | --- | --- | --- | ---------- | ------- | ------ | -------------- | --- | -------------- | ----- | --------- |
[1] A.V.SavkinandH.Huang,“Amethodforoptimizeddeploymentofa usingmobileandstationarynodesinsensornetworks,”inInt.Conf.Col-
networkofsurveillanceaerialdrones,”IEEESyst.J.,vol.13,no.4,pp. laborative Comput.: Netw., Appl. and Worksharing (CollaborateCom),
| 4474–4477,2019. |     |     |     |     |     |     |     | 2007,pp.106–115. |     |     |     |     |     |     |     |
| --------------- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- | --- | --- | --- | --- | --- |

7
| [14] ——, | “Collaborative | area | monitoring | using wireless | sensor | networks |
| -------- | -------------- | ---- | ---------- | -------------- | ------ | -------- |
withstationaryandmobilenodes,”J.Adv.SignalProcess.,2009.
[15] R.Elhabyan,W.Shi,andM.St-Hilaire,“Coverageprotocolsforwireless
| sensor | networks: | Review | and future | directions,” | J. Commun. | Netw., |
| ------ | --------- | ------ | ---------- | ------------ | ---------- | ------ |
vol.21,no.1,pp.45–60,2019.
| [16] N. Temene, | C.          | Sergiou, C. | Georgiou,  | and V. Vassiliou, | “A survey   | on      |
| --------------- | ----------- | ----------- | ---------- | ----------------- | ----------- | ------- |
| mobility        | in wireless | sensor      | networks,” | Ad Hoc            | Netw., vol. | 125, p. |
102726,2022.
| [17] C. Zygowski | and | A. Jaekel, | “Optimal | path planning | strategies | for |
| ---------------- | --- | ---------- | -------- | ------------- | ---------- | --- |
monitoringcoverageholesinwirelesssensornetworks,”AdHocNetw.,
vol.96,p.101990,2020.
[18] M.WatfaandS.Commuri,“Boundarycoverageandcoverageboundary
| problems | in wireless | sensor | networks,” | Int. J. Sens. | Netw., vol. | 2, pp. |
| -------- | ----------- | ------ | ---------- | ------------- | ----------- | ------ |
273–283,2007.