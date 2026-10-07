MEMS-based 3C accelerometers for land seismic acquisition:
Is it time?

DENISMOUGENOT, Sercel, Carquefou Cedex, France
NIGELTHORBURN, Sercel, Houston, Texas, U.S.

Recent  advances  have  allowed  development  of  micro
electro  mechanical  system  (MEMS)  sensors  with  the
sensitivity, low noise, and dynamic range needed in seismic
acquisition.  This  is  a  possible  “breakthrough”  because
MEMS accelerometers have the potential to provide broader
bandwidth, more accurate amplitude, and less sensitivity
to planting tilt than the coil-based geophones that have long
been used in the industry.

Several papers have presented the advantages of three-
component acquisition with single digital sensors based on
MEMS, and the advent of these sensors has been promoted
as the next big advance in land seismic acquisition—much
like the shift to 24-bits recording systems 10 years ago. So,
this  is  a  good  time  to  ask  an  obvious  question:  Has  this
technology really advanced to the point that it can, or should,
be used for general-purpose land seismic acquisition? This
paper will attempt to answer that question by addressing
the  advantages  and  disadvantages  for  the  general
application of single 3C digital sensors.

Why accelerometers for digital sensors? Ground motion can
be  measured  as  displacement,  velocity,  or  acceleration. A
mass/spring assembly is used for all these measurements.
With a soft spring, the mass (the coil in the geophone) does
not move and represents the reference for displacement or
velocity measurements. With a stiff spring, the mass moves
with the case, but with a small residual displacement related
to the acceleration. This acceleration can be measured either
by the strain on the spring (e.g., low cost, low power, high
distortion air bags) or by a feedback force applied to the mass
to cancel the displacement (e.g., high performance digital
sensors requiring power supply).

In this last implementation the sensor based on MEMS
is still analog, while the control loop and the output provided
by an application specific integrated chip (ASIC) are digital.
Such  a  “digital”  sensor  is  much  smaller  than  the  current
standard. A MEMS accelerometer is a tiny silicon chip with
a length of ~1 cm and weighing less than 1 g. A coil-based
sensor is a cartridge with a length of 3 cm and weight of 76
g. Within the chip, the residual displacement between the
inertial  mass  and  the  frame  is  on  the  order  of  a  few
nanometers, while the motion of a geophone coil may reach
2 mm.

However,  manufacturing  such  a  “digital”  sensor  is
expensive due to the cost of MEMS + ASIC. Therefore, actual
recording in the field will use a single-sensor configuration
(i.e., only one sensor per active channel).

Comparison of MEMS-based sensors and coiled geophones.
From the specification point of view, the essential benefit of
MEMS accelerometers is a broadband linear amplitude and
phase response that may extend from 0 (dc) to 800 Hz within
1% in amplitude and 20 ms in time (Figure 1) . MEMS resonant
frequency  is  far  above  the  seismic  band  pass  (1  kHz).  This
makes it possible to record frequencies below 10 Hz without
attenuation,  including  the  direct  current  (dc)  related  to  the
gravity  acceleration.  The  gravity  vector  provides  a  useful
reference for sensitivity calibration and tilt measurement of

Figure 1. Linear phase and amplitude response of a digital sensor unit
(DSU) with MEMS compared with that of a 10-Hz geophone. The
response is in the velocity domain for the geophone and in the acceleration
domain for the DSU.

3C MEMS-based sensors that has no equivalent for geophones.
Because  acceleration  increases  with  frequency  (at  constant
velocity), MEMS accelerometers also are excellent for high-
frequency  measurements.  In  this  domain  (>  50  Hz)  the
floor/electric  noise  of  the  MEMS  is  lower  than  that  of  the
equivalent geophone/station electronics.

These  broadband  capabilities  offer  possible  dramatic
improvement in the vertical resolution of seismic data, which
depends on the ratio between the maximum and minimum
frequencies of the signal (Fmax/Fmin = 2n, n being the number
of octaves). A MEMS accelerometer is particularly suited for
recording low frequency signals (< 5 Hz) like reflections at the
main  boundaries  between  lithological  formations  (or  even
earthquakes). In this frequency range, the limitation is more
on the source side because such LF signals cannot be emitted
with a sufficient S/N ratio. Recording of high frequencies is
limited  by  their  strong  attenuation  during  propagation.
However, MEMS sensors should be able, if close enough, to
listen to microseismic events (~500 Hz) as fluids move in the
reservoir during oil and gas production.

The total dynamic range of a 24-bit recording system using
MEMS can be up to 120 dB (ratio between the floor noise at
4 ms sampling rate—4.5 µm/s2—and the maximum signal—
4.5  m/s2—that  can  be  recorded  with  less  than  -90  dB
distortion). It is lower than the total dynamic range of the same
system using single geophones that should be up to 140 dB
(this  is  also  the  total  dynamic  range  of  the  latest  24  bits
recording  systems).  In  practical  situations  (including  the
distortion  generated  by  a  strong  signal  or  noise),  the
instantaneous dynamic range of a MEMS accelerometer (95
dB) is much better than the one of a single geophone (no more
than  70  dB,  but  this  may  be  improved  by  using  groups  of
geophones).  These  differences  in  total  and  instantaneous
dynamic ranges explain why a MEMS-based sensor is more
suited to record a weak signal in presence of strong noise (near
offsets)  while  a  geophone  (and  even  more  a  string  of
geophones)  is  more  effective  in  recording  a  weak/deep
reflection in presence of low noise (far offsets).

246

THE LEADING EDGE MARCH 2004

MARCH 2004 THE LEADING EDGE

0000

accelerometers.

The  advantages  for  the  full  digital  transmission  have
already been checked. During field tests, records by bunched
geophones  were  compared  to  MEMS  sensors  at  the  same
location (Figure 3). 50 Hz (picked up below a high voltage
line)  is  obvious  on  the  shotpoint  recorded  by  bunched
phones.  On  the  corresponding  f-k diagram,  the
electromagnetic noise interferes strongly with signal. This
noise does not occur on any of the three components of the
MEMS sensors due to the full digital transmission.

Digital  sensors  to  replace  arrays  of  geophones? Arrays  of
geophones may tremendously improve the dynamic range of
a  receiver  point  by  reducing  ambient  and  coherent  noise.
Compared to a single geophone, an array of N geophones,
whether  connected  in  series  or  in  parallel,  improves  the
dynamic  range  by  10  (cid:1)
logN  dB,  as  the  ambient
noise  is  reduced  by  the
square  root  of  N.  For
attenuation  of  coherent
noise,  geophones  are  laid
out in a spatial pattern that
provides  array  filtering.
The  size  of  the  array  and
the  number  of  wired
geophones should be large
enough to properly sample
the maximum wavelength
of the ground roll.

Despite  these  advan-
tages,  field  geophysicists
would  like  to  get  rid  of
arrays  because  they  are
large and heavy and, as a
result,  slow  crew  pro-
ductivity and require expensive logistics. At first glance, the
use of single digital sensors would have many operational
and geophysical advantages over geophone arrays. Layout
and positioning are easier than with geophone strings, and
this is even more relevant for 3C receiver points. Recording
is isotropic (no azimuth-dependent array filtering), and the
high  frequency  content  of  the  signal  is  not  attenuated  by
intra-array  statics  (particularly  in  S-wave  recording).
However,  these  benefits  are  only  true  in  an  ideal  world
where reflected signal is not contaminated by noise—i.e., in
a situation where a single coiled geophone would have been
sufficient.

In the field, the spacing of single sensors should decrease
with respect to the length of a geophone array. This shorter
spacing will not attenuate noise while recording, but it will
provide enough multiplicity (fold coverage) to decrease the
ambient noise while stacking data. Denser spatial sampling
also prevents the coherent noise from aliasing. Therefore,
we cannot expect to get better looking shotpoint displays
while  recording  with  single  digital  sensors.  The  benefits
(larger  frequency  content,  more  accurate  amplitude)  will
only show up with the final sections, after data processing.

New requirements for acquisition geometry. In practice,
how many MEMS sensors would be necessary to replace a
string of N geophones? It is unlikely that anyone will record
as many single digital sensors as hard-wired geophones, and
it is probably not necessary, even though that would provide
excellent noise attenuation.

Let  us  consider  ground  roll  (GR),  often  the  strongest
noise. In this case, the digital sensor spacing D should be

Figure 2. In the first digital recording system (top), all transmissions
between geophone groups and central unit, including the A/D converter,
were analog. About 30 years later (center), only transmission between
geophone groups and the field digitizing unit (FDU) was analog. Today
(bottom), the digital sensor unit (DSU) makes possible full digital
transmission.

Figure 3. Shotpoint comparison between the vertical component of a
digital sensor unit (DSU3) and bunched phones planted at the same
location (photo). Strong pick up of a high voltage line is due to analog
transmission up to the station electronics. The f-k diagram shows this 50-
Hz noise interfere with signal. DSU data are not contaminated. (Data
courtesy of BatchNeftGeofisika)

Amplitude calibration of a MEMS sensor and its stability
over aging and temperature variations are better than that
of  traditional  geophones.  Overall,  the  performance  of  a
digital sensor, in which MEMS are integrated with the station
electronics in a single housing, is better than conventional
station electronics that is connected during the same survey
to different strings of geophones of variable characteristics.

The full digital transmission. In the early 1970s, the A/D
converter  of  the  first  digital  recording  system  was
implemented in the central unit. One analog pair of wires
for each channel was used for transmission between strings
of geophones and the recording truck (Figure 2). Noise from
electromagnetic  interference,  signal  cross-talk,  and
sensitivity to leakage were common. About 30 years later,
the electronics distributed in the seismic network provided
digitization close to the geophone groups. Only two pairs
of wires are necessary for telemetric transmission of 10 000
or  more  channels  in  real  time.  Sensitivity  to  leakage  is
reduced and the digital data are controlled by each node of
the  seismic  network  (and,  thus,  may  be  retransmitted  if
necessary).  However,  noise  pick  may  still  contaminate  the
analog signals transmitted through the strings of geophones.
This should disappear with the integration of the sensor with
the  station  electronics  as  it  is  done  with  the  MEMS

0000

THE LEADING EDGE MARCH 2004

MARCH 2004 THE LEADING EDGE

247

Figure 7. Real time display of three-component digital sensor shot points
(Z and X components) in the doghouse after velocity conversion and low-
cut (10 Hz) filtering. (Data courtesy of Veritas DGC and Devon)

Figure 4. Shotpoint (GR = ground roll, BS = backscattering) with 10-m
spacing between single digital sensors. On the f-k diagram, GR is aliased
and interferes with signal. (Data courtesy of CGG)

Figure 8. Comparison of PP and PS final sections corresponding to the
previous SPs. The PS section is squeezed to PP time by assuming
constant VP/VS = 3. The frequency content of the PP section is above 200
Hz; in the PS section, frequencies above 70 Hz have been attenuated. The
reflectivity of the two sections recorded in sand/shale formations is quite
different. (Data courtesy of Veritas DGC and Devon)

With  3D  acquisition  or  complex  near-surface-generated
backscattered  noise,  it  would  be  necessary  to  sample  the
noise properly both in the inline and crossline directions.
Such  areal  sampling  would  require  a  corridor  of  single
digital  sensors  equivalent  to  the  patches  of  hard-wired
geophones. Since digital sensors are directly connected to a
telemetry  cable,  deployment  of  such  receiver  line  would
require several parallel cables (Figure 6) instead of only one
telemetry cable for all geophones. A quick calculation of the
channel requirement for a 3D swath of 4 (cid:1) 4 km2 with 100 m
between  receiver  lines  (each  having  five  individual  cables
with single digital sensors at 10-m spacing) produces a figure
of 80 000 active channels. This amount is still beyond the real-
time  capability  of  all  recording  systems  at  2  ms  sampling.
Today,  this  type  of  single  sensor  arrangement  is  only
compatible with a 2D acquisition.

Due to the continuous spatial sampling, this corridor of
single sensors provides a sort of 2D universal acquisition
design. Different single sensor combinations, often referred
as  digital  group  forming,  may  be  used  to  attenuate  noise
after  recording  by  all  single  digital  sensors.  Since  groups
overlap from point-to-point, each single sensor may be used
in  different  digital  groups. At  a  given  receiver  point,  this
“group forming” may even involve time-dependent digital
arrays  since  S/N  ratio  decreases  as  traveltime  increases.

A new era for 3C recording. Connecting strings of three-
component  geophones  (triphones)  to  a  telemetry  cable
involves  heavy  equipment,  lots  of  wire,  and  many
connectors.  With  standard  equipment,  planting,  leveling,
and  properly  orienting  these  triphones  is  painful  but

Figure 5. Shotpoint with 3.3 m spacing between single digital sensors.
On the f-k diagram, GR is still aliased but does not interfere with signal.
(Data courtesy of CGG)

Figure 6. 2D acquisition design that uses a corridor of 1C single digital
sensor units connected along parallel telemetric cables. At a given receiver
point (RP) different types of digital groups (DG1, DG2) may be
considered to reduce ambient noise and filter the ground roll.

such  that  the  GR  wavelength  L =  Va/Fa  (Va  =  apparent
velocity, Fa = apparent frequency) will be sampled at least
two times (i.e., D = Va/2Fa). This often provides values in
the range of 3 to 30 m. Figures 4 and 5 compare f-k diagrams
of  two  SPs  recorded  at  the  same  location  with  different
spatial  sampling.  At  10-m  spacing,  the  very  low  velocity
ground  roll  (330  m/s  which  is  as  low  as  the  air  blast)  is
aliased and interferes with signal. At 3.33-m spacing, GR is
still aliased but it vanishes at high frequencies (70 Hz) before
intersecting the signal. Considering this maximum frequency
limitation of the noise it is possible to adequately sample
with a spacing a little more than half of the GR wavelet, as
suggested by Baeten et al. (2000).

Up to now, we have considered only 2D propagation.

248

THE LEADING EDGE MARCH 2004

MARCH 2004 THE LEADING EDGE

0000

Figure 9. Back-to-back comparison of a 408UL station electronics (FDU)
that should be connected to a string of geophones with a 408UL 3C digital
sensor unit (DSU3) that includes three sensors with the corresponding
electronics. Base assembly to the telemetry line is the same to switch easily
from analog to digital sensors.

mandatory.  The  final  output  is  the  electric  sum  of  all
triphones connected to the same station electronics and any
correction is impossible at a later stage. Having sensors and
station electronics integrated in the same housing will reduce
overall  weight  and  wiring  errors,  and  should  make  all
multicomponent surveys faster, better, and cheaper.

Of course, planting a 3C digital sensor would need some
attention to get the proper coupling, but ensuring its exact
verticality  is  not  mandatory.  This  is  because  of  a  unique
feature of the MEMS-based 3C digital sensor—its ability to
measure  the  continuous  effect  of  the  gravity  vector.  This
vector is used as a reference to automatically compute with
high accuracy (±0.5°) the tilt of each horizontal sensor. These
tilt values are stored in the trace header extensions, and data
may be even corrected for tilt in real time by the central unit.
Sensor  orientation  may  be  corrected,  if  necessary,  during
processing by assuming a radial propagation between the
source and the single sensor (3D surveys only).

Tilt measurement is only one aspect of the advantages
provided,  in  terms  of  vector  fidelity,  by  the  MEMS-based
3C digital sensors. Their broadband capabilities (0-800 Hz
linear response), the very precise orthogonality of the sensors
(±0.25° accuracy)  and  the  accurate  and  stable  amplitude
calibration (±0.25% accuracy) will improve overall quality
of 3C seismic data.

Many surveys have already field proven this 3C digital
sensor  technology.  Data  in  Figures  7  and  8,  from  a  2D
acquisition  recorded  with  explosives  in  North  America,
demonstrate  the  broadband  capabilities  of  the  MEMS  3C
digital sensor. High frequency preservation while stacking
has  required  careful  static  definition  and  efficient
deconvolution  after  noise  attenuation.  On  the  final  PP
section, the frequency spectrum of the signal in a 0.4-1.0 s
window  is  above  200  Hz,  and  signal  beyond  300  Hz  is
evident down to 0.2 s.

Crew productivity with single 3C digital sensors. Seismic
data  acquisition  with  high-density  single  digital  sensors
will  require  recording  a  large  number  of  channels.  Short
receiver point spacing to get adequate noise sampling may
double (or more) the number of channels. Three components
instead of one will triple the number of channels. For 3D
surveys, this may mean tens of thousands of channels. To
maintain productivity with a such high channel count, the

Figure 10. Real time QC of a shotpoint (Z component) coming from
digital sensor units and conventional geophone strings (FDU) laid out at
the same location and recorded by the same central unit. For visual
comparison it is possible in real time to integrate acceleration data into the
velocity domain, and to apply low cut filtering to mimic geophone data.

ground equipment must be light, and the acquisition system
low power. Transmission redundancy should be available
thanks to multipath telemetry, and real-time quality control
of the spread and of the seismic data should be available
for quick quality control.

As implemented in the 408UL recording system (Figure
9), the 580 g of a 3C digital sensor unit (including the base
assembly with the telemetry cable, all station electronics for
the three channels and the three MEMS sensors) compares
favorably  with  the  450  g  of  the  1C  field  digitizing  unit
(including the same base assembly and the electronics for
only one channel to be connected to a string of geophones).
This  comparison  illustrates  the  high  level  of
sensor/electronics  integration  that  MEMS  accelerometers
makes it possible.

Considering  costs  associated  with  manpower  and
health/safety/environmental  issues  related  to  the  use  of
vehicles, a seismic crew should use the smallest number of
batteries  and  use  each  to  its  maximum  duration  (i.e.,  the
recording  system  must  be  low  power).  Even  the  fact  that
MEMS require some power while the geophone does not is
not  a  disadvantage  for  digital  sensor  recording.  At  least
with the 408UL recording system, the overall consumption
of a three-component digital sensor (400 mW) is less than
the equivalent consumption of three field digitizing units
connected to triphones (420 mW).

Distributed  electronics  with  computing  and  buffering
capabilities as implemented in the most advanced telemetry
cable systems makes it possible to secure data transmission.
In  case  of  a  cable  failure,  the  use  of  multiple  transverses
between the receiver lines and the central units will permit
the seismic network to reroute data through a different path.
As  the  number  of  channels  increases  up  to  10  000  and
beyond, manual or visual checking of the entire system and
data quality becomes impossible. This explains the importance
of automated real-time quality control as already implemented
for  single  digital  sensor  recording.  For  example,  the  tilt
measured from the residual dc on the horizontal components
can be checked continuously. The result is stored numerically
and also displayed graphically with a warning color if tilt is
above a predefined threshold. In addition each MEMS sensor
includes  a  built-in  reference  accelerometer  that  provides  a
continuous tracking of such factors as distortion, gain, phase,
and  cross-talk.  During  the  recording,  the  data  may  be
visualized  component  by  component  (Figure  7);  several
attributes (e.g., signal, noise, frequency content, faulty trace)
are available on a trace-by-trace or shot-by-shot basis which
allows continuous monitoring of the acquisition process.

Since MEMS sensors record acceleration and not velocity,
real time integration from one domain to the other has been
made  available.  To  provide  a  one-to-one  comparison

0000

THE LEADING EDGE MARCH 2004

MARCH 2004 THE LEADING EDGE

249

both good PP-wave data as well as good PS-wave data.

In some surveys, crews are deploying lines of 3C MEMS-
based  sensors  strategically  within  a  3D  layout  of  analog
phones (1C) recorded on the same system at the same time.
In this way P-wave sampling and S-wave sampling can be
different  on  the  same  survey,  moving  closer  to  optimum
spacing for specific wavefields. This is only one example of
the creativity of system manufacturers, their customers, and
their customer’s clients when new technology offers new
solutions to pressing exploration and production problems.
So, is it time for MEMS-based sensors? Why not! In this
industry  we  have  always  had  exploration  or  production
problems that we couldn’t solve with existing technology.
So we look for the next technology with which we can push
the envelope. Successful and efficient use of MEMS-based
sensors is a reality. TLE

Acknowledgments:  We  thank  CGG,  Veritas  DGC,  Devon,  and
BatchNeftGeofisika for having acquired and processed the digital sensor
data shown in this article. We thank Sercel’s R&D department for useful
information, and Sercel’s engineers who supervised the field tests. Final
review by Bob Albers and George Wood was very helpful.

Corresponding author: denis.mougenot@sercel.fr

between  analog  and  digital  sensors,  MEMS  broadband
seismic data may be filtered to resemble geophone data (10
Hz low cut filtering and damping, Figure 10).

Conclusion. Is it time to use digital sensors? MEMS-based
single digital sensors offer new capabilities compared with
conventional arrays of geophones. The sensor itself (MEMS
+ ASIC) should provide better vector fidelity thanks to its
accurate  and  stable  calibration  (amplitude  and
orthogonality), and its broadband linear response (from dc
to 800 Hz). Tight integration of the sensor with the station
electronics allows size/weight reduction and lower power
consumption.

Such a sensor will provide, for the first time, complete
digital  transmission,  from  the  sensor  to  the  central  unit,
which is less sensitive to electromagnetic pick-up, cross-talk,
and leakage. Overall MEMS technology offers the potential
to  reduce  costs  while  improving  data  quality.  However,
there are two limitations to the use of MEMS sensors: one
is geophysical (digital sensors are recorded as single sensors)
and the other is economic (manufacturing costs of MEMS
compared to coiled geophones).

If single-sensor recording provides obvious advantages
for deployment and signal preservation, these benefits are
strongly  balanced  by  the  inability  of  single  sensors  to
attenuate  any  ambient  or  shot-related  noise.  Records  by
single digital sensors will be dominated by noise, and this
domination will be even worse if point receivers are used
in conjunction with point source (i.e., without any source
array filtering). In noisy areas with strong, dispersive, and
backscattered ground roll and with high ambient noise this
may prevent recording any usable signal.

To  be  able  to  recover  signal,  all  this  noise  should  be
attenuated during processing. For ambient noise reduction,
the  fold  coverage  should  increase.  This  is  possible  by
decreasing the spacing and increasing the number of single
digital  sensors.  For  coherent  noise  attenuation,  the  point
receiver spacing should also decrease, perhaps not down to
the  geophone  spacing,  but  at  least  down  to  the  Nyquist
distance necessary to keep the corresponding ground-roll
unaliased. For both ambient and coherent noise, this implies
increasing  the  number  of  point  receivers  and  channel
capabilities (which will increase the cost of acquiring data).
Thus  a  question  arises:  Does  it  make  sense  to  invest  and
operate  single  digital  sensors  instead  of  conventional
geophone arrays?

Is it time? In all realms of seismic recording, single sensor
acquisition, done properly, has the potential to increase data
resolution to the levels required for the definition of subtle
targets  and  detection  of  small  changes.  When  120  dB
recording became a reality there was a lot of talk about the
geophysical benefits of this new range of seismic data. There
is also a lot of discussion that up to now we have really not
ever  used  this  breakthrough  in  the  actual  processing  and
interpretation of the data. In the single sensor world, we will
now require dynamic ranges every bit as wide as these new
systems allow.

We have discussed sampling for single sensor acquisition
and know that better sampling with higher channel counts
will  be  required.  When  we  consider  the  different
wavelengths associated with P-wave data and S-wave data,
the sampling requirements of the recording layout become
more complicated than when we strictly consider a P-wave
survey. At this time there are crews in the field using single
sensor MEMS-based systems to record 3D-3C with improved
but still practical spatial sampling. These crews are recording

250

THE LEADING EDGE MARCH 2004

MARCH 2004 THE LEADING EDGE

0000

