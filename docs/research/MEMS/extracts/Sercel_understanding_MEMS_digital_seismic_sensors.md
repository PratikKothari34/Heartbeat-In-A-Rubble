> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> Sercel, *Understanding MEMS digital seismic sensors*. Source PDF (7.76 MB) deleted after
> conversion (gitignored).
>
> Cited as **supporting** material in `docs/research/MEMS/03-literature.md` line 69 and logged in
> `05-verification-log.md` line 116. Vendor-authored explainer on MEMS digital seismic sensors,
> companion to `Sercel_MEMS_3C_accelerometers_land_seismic` (which has its own extract).
>
> **Vendor material: treat its comparisons as marketing, not as an independent benchmark.**
> Note the MEMS-vs-geophone conclusion in this project is **reversed** from the earlier research
> pass - at the correct 5-40 Hz band the **SM-24 geophone** is selected and the ADXL355 cannot do
> the job. See the SUPERSEDED banner at the top of `docs/research/MEMS/README.md`.

Understanding MEMS-based digital seismic sensors

Nicolas Tellier1* and Jérôme Lainé1 explain how to understand operating characteristics of
Digital Sensor Units (DSU) and discuss the quality and cost issues in the light of experience
gained after more than a decade of field operations.

Introduction
Over the last few decades almost all the electronic devices we use
in our daily lives have switched from analog to digital owing to the
numerous  benefits  they  offer,  such  as  miniaturization,  enhanced
functionalities or reduced power consumption, etc. This revolution
also  reached  the  seismic  industry,  primarily  when  fully  digital
recorders  and  telemetries  became  available  in  the  late  1970s.
However,  measurement  of  the  Earth’s  displacement  by  sensors
remained analog. The last step towards full digital recording was
made in the early 2000s with the launch of digital seismic sensors
based on MEMS (Micro Electro Mechanical Systems) accelerom-
eters that had the potential to replace analog geophones that had
been used since the early days of seismic dating back to the 1930s.
However, although digital sensors have established a foothold
and  indeed  even  become  a  reference  for  a  number  of  different
applications, the anticipated revolution has however not lived up
to the expectations of the seismic industry, the current situation
being perhaps analogous to using audio cassette tapes alongside
MP3 music files. More than a decade after the release of the first
digital seismic sensors, several explanations for such a situation
have become clear:
•   the operating principles of digital sensors are somehow per-

ceived to be more complicated than those of geophones, and
trickier to understand;

•   the quality of data acquired with digital sensors is sometimes
judged to be no better than equivalent to data acquired with

geophones (more often than not, this is owing to a comparison
of single digital sensors with strings of geophones at the same
trace interval);

•   the cost of digital sensors is often seen to be higher (at least

for one-component – 1C – acquisition) than the cost of a con-
ventional Field Digitizing Unit (FDU) connected to a string of
geophones.

This article aims firstly to review the main operating character-
istics  of  MEMS-based  Digital  Sensor  Units  (DSU),  especially
when  compared  to  geophones,  and  then  discuss  the  quality  and
cost  issues  in  the  light  of  experience  gained  after  more  than  a
decade  of  field  operations.  We  conclude  that  their  use  with  an
adapted high-density geometry makes it possible to achieve much
better imaging than with geophone arrays, for an equivalent cost.

Operating characteristics of digital
seismic sensors
What do we measure with MEMS digital sensors?
Both  geophones  and  MEMS  technology-based  accelerometers
operate  on  the  principle  of  a  damped  mass-spring  system
(Figure 1).

For  geophones,  the  resonant  frequency  [Fresonance  =  √(spring
stiffness  /  mass)]  is  low:  this  is  due  to  the  fact  that  the  spring
stiffness is weak (when compared to the ‘heavy’ mass of the coil
driven by the spring). This means that for any signal of interest
(above  resonant  frequency)  the  proof  mass  (i.e.,  the  coil)  is

Figure 1 Geophone (left): the sensor casing (blue) is
attached to a spike (grey) and to the magnet (yellow).
All these components move with ground motion,
while the coil (red) connected to the casing by a soft
spring (black), remains motionless. Digital sensors
(right): the principle is the same as for geophones
on a microscopic scale, with a MEMS casing (blue)
attached to a sensor casing (not represented). The
inertial mass (green) is maintained by stiff springs
(black) and then moves with casing/ground motions.
When subjected to an acceleration, the small
displacements of the inertial mass are measured by
electrodes (red).

9 3

1 Sercel

* Corresponding author: nicolas.tellier@sercel.com

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017the  reference  point.  When  the  ground  shakes,  the  coil  remains
motionless  while  the  geophone  casing  and  the  magnet  moves
relatively to the coil. As a geophone is an electromagnetic device,
the output voltage signal produced by the coil is proportional to
the  relative  displacement  rate  (velocity)  of  the  magnet  attached
to  the  casing.  Geophones  act  then  as  velocimeters  above  their
resonant  frequency  (commonly  10  Hz)  and  deliver  an  analog
voltage proportional to ground velocity.

For  MEMS  accelerometers,  it  is  even  simpler:  resonant
frequency is high because the spring stiffness is strong (compared
with the associated ‘light’ mass). This resonant frequency is high-
er than the frequency bandwidth of interest for seismic imaging.
As  a  result,  when  subjected  to  a  seismic  wave,  the  proof  mass
(i.e.  the  inertial  silicon  mass)  moves  in  phase  with  the  casing.
Consequently, when the velocity is constant, there is no relative
force  applied  to  the  mass  (as  is  the  case  for  a  passenger  inside
a  car  on  a  freeway).  When  the  sensor  casing  is  subjected  to  a
variation in speed, i.e., an acceleration, then a force is applied to
the mass that moves from its resting position by a value dx given
by Equation (1):

(1)

Digital  sensors  act  then  as  accelerometers  below  their  resonant
frequency  (around  1  kHz)  and  deliver  digits  proportionally  to
ground acceleration.

Computation  of  the  MEMS  acceleration  output  depends  on
the  way  in  which  the  MEMS  is  controlled.  Two  ways  can  be
distinguished:
1.   Open-loop MEMS accelerometers (no control of the inertial
mass oscillation): dx is measured by a capacitive position
sensing interface. The ground acceleration is obtained from
the measured displacement and the known spring stiffness
and mass:

2.

 Closed-loop MEMS accelerometers (a feedback force is
applied so that the mass displacement remains close to
null): the ground acceleration is obtained by measuring the
force applied to the inertial mass to maintain it at its resting
position, this force being produced by applying a voltage on
the electrodes (Figure 1).

(3)

The feedback force can be generated by an analog controller (as
for the first generations of digital sensors); on modern sensors it
is now digitally controlled.

Understanding the specifications of MEMS
digital sensors
Several  concepts  are  reviewed  here  with  relevant  examples.
These  concepts  can  usually  be  found  in  the  specifications  of
digital sensors, and allow a comparison of their performances:

Noise  Floor  is  the  output  of  the  sensor  in  the  absence  of  any
external perturbations (i.e., if we consider the sensor to be ideally
isolated from its environment). This non-null output corresponds
to the noise produced by the sensor itself, mainly as a result of:
•   The collision of gas molecules in the sensing cell (i.e.,

the MEMS depicted, right, in Figure 1). This noise, called
Brownian noise, is mitigated by a high vacuum maintained
by a device called ‘getter’ that traps any residual gas
molecules.

•   The noise produced by electronic components when operating.
Electronic noise has various origins, the main one being the
agitation of the charge carriers in electrical conductors, known
as thermal noise.

There are two ways to express a noise floor (Figure 2):
•   For temporal analysis, RMS (Root value of the Mean of the

(2)

Squared values) is preferred. The noise floor is then expressed
in the same unit as the signal (for example Volt, m/s or m/s²).
The RMS noise value is the sum of all the noise sources

Figure 2 Spectra of a 1 V signal having two rays at 10 and 100 Hz, with white noise of 1 mV. (Left): spectrum is expressed in amplitude: the noise floor is dependent on the
frequency resolution. Increasing the number of computation points ‘spreads’ the noise: each point represents a smaller bandwidth (bin size) that consequently has lower
amplitude. In this example, the noise floor seems to be divided by 10 when the number of points is multiplied by 10. (Right): Expressing noise in power density avoids this
artifact: comparing the noise floor performance of different systems should then be done in power density.

9 4

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017

within the Nyquist bandwidth, i.e., from 0 Hz up to Fs/2, with
Fs being the sampling frequency.

Example 1: for a 6-180 Hz seismic signal of interest, 2 ms

sampling rate is used (Fs = 500 Hz to record data without
aliasing up to 250 Hz), then the noise RMS will be expressed
on the 0-250 Hz bandwidth.

Example 2: if the noise floor is ‘flat’, the noise floor RMS
of an acquisition system increases by a factor of ~√2 (+3 dB)
when the frequency bandwidth considered is doubled.

•   For spectral analysis, Noise Density is preferred. The unit
is x/√Hz with x being the unit of the signal. Only one
value is then sufficient to fully specify noise performance,
irrespective of the sampling rate, the length of acquisition and
the frequency resolution of the spectral analysis. Moreover,
when comparing the noise spectra between two systems, it is
mandatory to display spectra in noise density (in V/√Hz) or in
PSD (Power Spectral Density, in V2/Hz) as the noise density
value does not depend on the frequency resolution.

Note  that  noise  RMS  can  be  computed  from  Noise  Density  by
multiplying the latter by the square root of the bandwidth that is
defined by the sampling frequency, the digital antialiasing filter
and the low-cut filter, if any.

Example: with a sampling rate = 2 ms, a 0.8 Nyquist digital
filter and a 3 Hz low-cut filter, the bandwidth is [3 200 Hz]. With
this  configuration,  the  RMS  noise  of  a  digital  accelerometer
having a noise density of 15ng/√Hz is:

The  noise  floor  level  depends  on  the  MEMS  construction
(Moreau  et  al.,  2014).  As  an  example,  the  noise  floor  of  the
latest  generation  of  digital  sensors  (<  15  ng/√Hz)  is  divided  by
~3  compared  to  the  previous  generation  (<  40  ng/√Hz). This  is
of  particular  importance  when  recording  very  low  frequencies
(< 5 Hz) for which MEMS noise floor increases.

Full  scale  is  the  maximum  signal  amplitude  that  can  be
measured. For an FDU, this limitation is due to the  maximum
input  voltage  of  the  Analog-to-Digital  Converter  (ADC)  that
is allowed (that is dependent on the selected gain). For a DSU

operating  in  closed-loop,  this  limitation  is  owing  to  the  maxi-
mum feedback force that can be applied to the seismic mass. It
can be expressed either in peak value, or RMS value (assuming
the  signal  is  a  sine  wave,  the  latter  is  equal  to  the  full  scale
(peak) divided by √2).

Example: an FDU having a peak full scale at 2.26 V / 0.565 V
(low/high gain) has a RMS full scale at 1.6 V / 400 mV. These
values can be converted into velocities by applying the geophone
string sensitivity. For digital sensors, a typical full scale value is
5 m/s² peak.

Figure 3 (top) compared instrument noise and (bottom) full scale of a DSU and FDU
with two different gains. The FDU full scale is derived to enable comparison.

Figure 4 Comparison of DSU and FDU sensitivity:
(top) With an FDU having a full scale of 2.26V
(digital output +223), the maximum recordable
signal when using a 22.8 V/m/s geophone
will be 2.26/22.8=0.1 m/s; (bottom) to enable
comparison, the DSU can be split into an ADC
and a virtual sensor with a pseudo sensitivity of
2.26 V / 5 m.s-² = 0.452 V/m/s².

9 5

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017

Dynamic range is the ratio of the full scale over the RMS noise,
expressed in decibels. It is the most important signal specification
of a sensing unit as it describes its capability to record simultane-
ously large and very weak signal amplitudes.

each connected to a single geophone (or to bunched phones if sin-
gle ones are not available). For 3C (three-component) recording,
a  single  3C  digital  sensor  must  be  compared  to  three  digitizers
connected to a triphone.

Example:  for  a  system  having  a  full  scale  of  1.6  V  RMS
(±2.26 V peak) and a noise of 450 nV RMS at a 2 ms sample rate,

Sensitivity  is  the  factor  used  to  convert  the  analog  or  digital
signal  produced  by  the  sensor  into  the  physical  quantity  we
wish  to  measure.  Such  a  conversion  is  mandatory  to  compare
seismic data recorded by analog and digital sensors. The output
of a geophone is a voltage. This is then expressed as a velocity
by dividing by the geophone sensitivity (in V/m/s). The issue is
different for digital sensors, as a digital output ranges from -223
to  +223 (for  a  24-bit  system).  The  DSU’s  maximum  recordable
signal of 5 m/s² corresponds then to +223. DSUs can be compared
with FDUs by introducing a pseudo sensitivity to convert input
acceleration  into  voltage:  the  pseudo  sensitivity  is  the  ratio
between the full scale of an FDU of reference with the full scale
of the DSU (Figure 4).

Note that the FDU ADC noise RMS, when converted in veloc-

ity, will appear lower when using high-sensitivity geophones.

Comparing acceleration data sets with velocity
data sets
The  motion  shown  by  both  geophone  and  digital  sensors  is  the
ground particle motion at the location of measurement. However,
velocity (output from the geophone above its resonant frequency)
and  acceleration  (output  from  the  MEMS  digital  sensor  below
its  resonant  frequency)  are  90  degrees  apart.  In  addition,  the
amplitude response of both types of sensor displays a difference
of +6 dB/octave (high frequencies are boosted by digital sensors).
As a result, seismic data recorded by digital sensors seem to have
a higher frequency/vertical resolution, but this is mainly because
we are in a different domain. If we had derived geophone data in
the  acceleration  domain,  we  would  also  have  boosted  the  high
frequencies.

It is therefore mandatory to apply a conversion to compare
both data sets. This conversion is always performed from accel-
eration to velocity which is the reference domain for interpreters
to pick reflectors at their exact time location: zero-phase wave-
lets  are  aligned  with  the  contrasts  in  acoustic  impedance  only
in  the  velocity  domain.  This  conversion  is  often  performed  by
applying an integration operator that boosts the low frequencies
but also boosts the associated noise. To avoid introducing noisy
data  into  data  processing,  zero-phase  deconvolution  may  be
applied  directly  to  acceleration  data.  It  is  often  stated  that  the
output is in the velocity domain irrespective of the type of sensor.

Geophysical benefits and operational advantages of
MEMS digital sensors
Digital sensors must be used as single sensors since they must be
recorded individually. This means that the benefits for operations
have to be found when comparing digital sensors with digitizers,

9 6

The  original  technology  behind  digital  seismic  sensors
provides  a  wide  range  of  geophysical  benefits  that  ultimately
ensure  the  higher  fidelity  and  stability  of  seismic  measure-
ments:
•   Geophone specifications are given with tolerances (e.g., for
sensitivity or natural frequency) and for a given operating
temperature. As a consequence, the geophone output will be
dependent on the temperature, the unit manufactured, but also
on the ageing of the miscellaneous components. This is not
the case for digital sensors, the output of which is insensitive
to ageing and temperature. As a result, seismic amplitudes are
better preserved, which makes such sensors highly suitable
for miscellaneous applications (e.g., AVO) (Mougenot, 2013);
and wavelet phase is also more stable, particularly in low
frequencies.

•   Electromagnetic noise is not picked up owing to the fact that

there is no coil; the full digital transmission avoids picking up
other external noise through the line.

•   The digital sensor’s amplitude and phase response remains
linear and flat from 0 to around 1 kHz in the acceleration
domain. Moving to the velocity domain, digital sensor
amplitudes increase by 6 dB per octave compared with the
geophone’s flat response above its natural frequency – this
makes digital sensors particularly suitable for high-frequency
recording. At low frequencies, below the geophone’s natural
frequency, the digital sensors are only attenuated by 6 dB/
octave compared with the 12 dB/octave attenuation of
geophones, while the latest generation of MEMS significantly
reduced the low-frequency instrument noise (Moreau et al.,
2014).

•   MEMS noise fits better with field noise, i.e., with noise

decreasing towards the high frequencies.

•   Finally, the 3C digital sensors enable high vector fidelity

since they are capable of detecting the gravity field and then
measuring the tilt angle and correcting it.

Field  operations  are  also  simplified  when  operating  with  dig-
ital  seismic  sensors.  Firstly,  one  digital  channel  is  smaller
and  lighter  (~30%)  than  an  FDU  with  its  string  of  geophones,
and  uses  less  power  (~20%).  Secondly,  the  sensor’s  tight
integration  with  the  telemetry  makes  the  line  more  robust
(less  connectors)  and  easier  to  manage,  particularly  for
cable  lay-out,  pick-up  and  repairs.  As  a  result,  operations
are  significantly  facilitated  by  the  deployment  of  less  field
equipment,  and  less  staff  and  technical  resources  to  manage
this equipment.

Data quality
The  second,  but  surely  most  important  question,  concerns  the
quality  of  data  acquired  with  digital  sensors.  The  literature
abounds  with  examples  of  successful  deployment  of  digital
sensors  for  mining  (e.g.,  Meisheng  et  al.,  2008),  3C  applica-
tions  (e.g.,  Stotter,  2011),  thin  gas  reservoir  identification  from
preserved  far  offset AVO  (e.g.,  Shi  et  al.,  2008,  2009),  or  tight

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017

oil exploration (Xuming et al., 2014), and they are widely used
for any application in regions such as China or North and South
America.

Two new tests acquired with digital sensors were conducted
in  2016  to  assess  the  benefits  of  digital  sensors  for  broadband
recording,  particularly  on  the  low-frequency  side.  The  first  test
(Figure 5) was commissioned by Ritek, the technology division
of Lukoil, and acquired in February 2016 by Geotech SeismoRaz-
vedka  in  the  Samara  region  (South  Russia). The  initial  purpose
of  the  test  was  to  compare  low-frequency  sweeps  starting  from
2  Hz  with  linear  sweeps  starting  from  7  Hz,  but  digital  sensors
available  at  the  time  of  the  tests  enabled  the  comparison  with
10 Hz geophones.

As  digital  sensor  evaluation  was  not  the  main  purpose  of
these  tests,  the  parameters  chosen  were  actually  quite  unfa-
vourable  for  this  type  of  sensor:  one  digital  sensor  was  indeed
compared  to  a  string  of  12  geophones,  with  the  latter  offering
important  source-generated  noise  attenuation  directly  in  the
field.  The  theoretical  benefit  on  the  raw  shot’s  signal-to-ambi-
ent-noise ratio is then of √12 for the geophone array, which can
be  more  realistically  reduced  to  √6  if  considering  a  minimum
decorrelation  distance  between  receivers  of  5  m.  The  datasets
were  nonetheless  processed  identically  to  allow  unbiased  com-
parisons, apart from a mandatory integration for the DSU data.
The  digital  sensors  showed  a  data  quality  that  outstripped  the
data quality obtained with the geophone strings, particularly in
terms  of  data  bandwidth.  This  produced  an  imaging  that  was
richer  in  low  frequencies  that  are  particularly  visible  at  great
depths (Figure 6). Even better results could have been expected
from  digital  sensors  if  used  with  a  suitable  geometry  and  a
dedicated processing flow.

The second test was acquired in December 2015 in Manitoba,
Canada, with the purpose of comparing three types of sensors laid
out  side-by-side  on  three  2900  m  parallel  lines  (290  RPs  with
10-m group intervals each):
•   Line 1 = Single 5 Hz geophone in marsh casing.
•   Line 2 = 3x2 10 Hz geophones in land casing podded in a 4 ft

diameter circle.

•   Line 3 = Single DSU QuietSeis.
The DSU QuietSeis sensor is the latest generation of digital sen-
sors, designed to enhance even further the capability to record
low frequencies, particularly as a result of an ultra-low sensor
noise floor, lower than the noise floor of a geophone connected
to a digitizer (Moreau 2014) thus enabling the characterization
of  even  deeper  and  weaker  events.  The  three  receiver  lines
were  acquired  by  a  single  40,000  lbs  Mertz  18  vibrator,  using
a  single  low-dwell  sweep  of  2-90  Hz,  30  s  length,  on  a  20  m
VP  grid.  Here  again,  a  clear  deeper  penetration  of  the  low
frequencies is visible on the stack after amplitude compensation
and  denoising,  and  these  results  are  confirmed  on  the  corre-
sponding spectra with an advantage in terms of signal amplitude
around  5  dB  below  6  Hz  when  compared  to  geophones
(Figure 7).

The cost issue
Designing  an  ideal  survey  that  would  provide  at  a  reasonable
cost  all  the  required  information  to  understand  the  subsurface
and all its features (from large-scale structures to the most subtle
fault) without any compromises has long been the dream of land
seismic  designers  and  interpreters.  Current  thinking  revolves
around the concept of obtaining dramatically more field data (of
individually lower quality) that fits the Big Data motto of ‘more

Figure 5 Test overview: sweep parameters (top left), geometry (bottom left), sources (top right), DSU-428 digital accelerometers (middle right) and the test area (bottom right).

9 7

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017data  is  better  data’,  the  information  acquired  on  such  projects
being  rich  enough  to  perform  adequately  any  analysis,  ranging
from accurate velocity models to seismic attribute analysis, and
make the interpretation less subjective.

Land project designs have therefore gradually evolved in this

direction, principally with:
•   Adapted 3D geometries (dense and wide-azimuth, and also

enabling the long offset recording), with high-channel-count
spreads and reduced source and receiver arrays;

•   High-productivity shooting methodologies, such as slip-
sweep, DS3, DS4 or Free Vibrator, producing more than
10,000 VPs per day;

•   Processing resources and technologies able to cope with

enormous quantities of noisy data.

This logic remains true provided the field data is not affected by
acquisition artifacts that cannot be addressed at the processing
stage,  such  as  the  use  of  source  or  receiver  arrays:  they  have
proven  to  be  an  effective  way  of  attenuating  powerful  surface
waves  directly  in  the  field,  but  at  the  cost  of  high-frequency
attenuation  because  of  the  intra-array  filtering.  While  source
fleets  have  significantly  decreased  in  recent  years,  commonly
down  to  a  single  or  dual  vibrator  in  the  Middle  East,  the  still
widespread  use  of  strings  of  geophones  (even  with  a  clear
tendency  to  reduce  the  quantity  of  geophones  per  channel)

Figure 6 PSTM of the 2-Hz geophone data
(top left) and 2-Hz DSU data (middle left), with
their respective band-pass filter 1-2-4-6 (right).
Bottom: spectra in logarithmic scale of PSTM for
the four sets of data. On the 2 Hz dataset at a
-6 dB level, the DSU data offer one extra octave
of signal when compared to geophones.

9 8

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017Figure 7 Stacks after amplitude compensation and denoising on a 150-1000 ms time window, and corresponding spectra. The same processing flow was applied, apart from
the integration for DSU data.

remains by far the less mature approach towards performing a
high-quality acquisition without compromise. This is confirmed
by  the  fact  that  the  number  of  crews  using  single  sensors
represents only a very small percentage of the total active crews
worldwide,  and  among  these  crews,  analog  single  sensors  are
used  as  often  as  digital  MEMS.  Therefore,  whereas  the  tech-
nical and geophysical advantages of MEMS have been largely
demonstrated,  how  can  we  explain  the  limited  commercial
success of this technology?

The  last  obstacle  appears  to  be  chiefly  economic  (Postel,
2016),  mainly  owing  to  the  fact  that  when  compared  to  a  FDU
with  a  string  of  geophones,  a  DSU  configuration  remains
more  expensive  as  a  result  of  the  higher  density  required.  The
usual  ‘rule  of  thumb’  when  substituting  DSU’s  for  geophones
(Mougenot, 2011) is to use a DSU spacing that is:
•   Larger than twice the geophone interval
•   Smaller than half the channel interval
However, when analysing the cost of seismic sensors it is neces-
sary to take a holistic approach and distinguish between capital
expenditure  for  equipment  (Capex)  and  operational  expenditure
(Opex)  to  operate  this  equipment.  For  Opex,  the  comparison
is  clearly  unfavourable  for  geophone  strings,  if  we  take  into
account the effort needed to transport, deploy, retrieve, maintain
and repair large quantities of equipment – in addition to the staff
required for these tasks and the subsequent logistics (accommo-
dation,  catering,  laundry,  transportation  etc.).  HSE  exposure  is
also correspondingly increased.

Reducing the cost of DSU deployment in terms of Capex and

Opex is currently an ongoing process:
•   The cost of manufacturing this equipment is steadily declining

with mass production.

•   The cost of deployment logistics is also declining as the field

process is streamlined.

As  for  marine  seismic  acquisition,  another  major  step  forward
concerning Capex and Opex would come with a standardization
of the group interval. This will drastically simplify manufactur-
ers’ stocks and contractors’ inventories and accelerate the global
worldwide deployment of this type of equipment.

Conclusion
After more than a decade of existence in the market, digital seis-
mic  sensors  have  proven  their  technical  and  geophysical  effec-
tiveness for a wide range of applications, and their performance
continues to improve at a regular pace. Their acceptance remains
limited, however, as they represent only ~10% of the market in
terms of channels (300,000 digital RPs compared with 3 million
analog ones) and much less in terms of sensors (compared with
about 50 million geophones). In low SNR areas subject to strong
low-velocity source-generated noise, noise filtering with receiver
arrays remains the preferred option for survey operators who rely
only on shot displays for quality control.

We  can  expect  digital  sensors  to  replace  these  arrays  once
they  can  be  deployed  with  a  trace  interval  (both  inline  and
crossline) that is small enough to record the full wavefield with-
out aliasing and thus manage efficiently any type of noise at the
processing stage. The key factor will then be the cost, especially
in  an  industry  facing  a  seemingly  endless  troubled  period. That
notwithstanding, the significant reduction in operational expenses
offered by downsized seismic crews when operating with single
sensors – a downsizing that will be probably driven even further
by  the  mechanization  of  sensor  layout  and  pick-up  –  and  the
constant progress being made in denoising algorithms will most

9 9

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017likely  be  the  primary  factors  that  will  convince  operators  to
finally make the leap. This will make it possible to achieve much
better imaging than with arrays, for an equivalent cost.

Mougenot  D.  and  Shuying  L.  [2013].  Do  digital  sensors  preserve

amplitude better? Case studies. Geohorizons, 18 (2), 38-42.

Postel  J.J.  and  Tellier  N.  [2016].  MEMS:  A  cost-effective  solution

Acknowledgments
The authors would like to thank PanAmerican Geophysical and
Ritek for granting show rights for the test data, the CGG Vostok
team  for  Russian  test  processing  and  Sercel  management  for
granting permission to present this work. Special thanks to Denis
Mougenot for his advice and review, and more generally for his
work and contribution to MEMS-based digital sensor technology.

References
Meisheng W., Hong L., Zhensheng Z., Peiming L. [2008]. The application
of DSU1 high density 3-D in coal field exploration. 78th SEG Annual
Meeting, Expanded abstracts.

Moreau  M.,  Lainé  J.,  Serrut  M.  [2014].  MEMS-based  accelerometers
– The  quest  for  low  frequencies  and  weak  signals.  76th  EAGE
Conference & Exhibition, Expanded Abstracts.

Mougenot  D.  [2004].  How  digital  sensors  compare  to  geophones?

74th SEG Annual Meeting, Expanded Abstracts.

Mougenot  D.,  Cherepovskiy A.,  JunJie  L.  [2011].  MEMS-based  accel-

erometers: expectations and practical achievements. First Break, 29

(2), 85-90.

for  3D  broadband  vibroseis  acquisition  with  high  trace  density.
2nd broadband point source point receiver acquisition and process-
ing, Expanded Abstracts.

Shi,  S.,  Du,  Y.,  Yao,  Z.,  Wang,  D.,  Zhang,  M.,  Cheng,  S.,  Gan,  L.,

Gao, L., Li, M. and Qin, Z. [2008]. Digital point receiver seismic

acquisition  and  pre-stack  reservoir  characterization  at  Sulige
gas  field,  China.  70th  EAGE  Conference  &  Exhibition,  Expanded
Abstracts.

Shi,  S.,  Du,  Y.,  Zhang,  M.,  Cheng,  S.,  Gan,  L.,  Gao,  L,  Yao,  Z.  and

Li,  M.  [2009].  Seismic  acquisition  with  digital  point  receiver  and

prestack reservoir characterization at China’s Sulige gas field. The

Leading Edge, 28 (3), 324-331.

Stotter,  C.  and  Angerer,  E.  [2011].  Evaluation  of  3C  microelectro-

mechanical  system  data  on  a  2D  line:  Direct  comparison  with

conventional  vertical-component  geophone  arrays  and  PS-wave

analysis. Geophysics 76 (3), B79-B87.

Xuming, B., Shenglui, Y., Zedan, W., Jingguo, C., Xiaodong, W., Qing
H. [2014]. Digital geophones and exploration of tight oil. 84th SEG
Annual Meeting, Expanded Abstracts.

NAPEC FB17 Jan.indd   1

1 0 0

08/12/16   08:47

SPECIAL TOPIC: LAND SEISMIC FIRST BREAK I VOLUME 35 I JANUARY 2017