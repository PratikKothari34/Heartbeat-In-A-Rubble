QuietSeisTM
An Ultra-low noise MEMS accelerometer for
Seismology
aurelien.fougerat@sercel.com
laurent.guerineau@sercel.com
April 10th, 2018

Introduction
SERCEL
| • French company |                   | founded | in 1956, subsidiary         |     | of CGG |
| ---------------- | ----------------- | ------- | --------------------------- | --- | ------ |
| • More than      | 1500 employees    |         | in 8 countries and 14 sites |     |        |
| • Market         | leader in seismic |         | instrumentation for O&G     |     |        |
exploration in marine, land and transition zones
| • Longstanding |     | culture of technological |     | innovation |     |
| -------------- | --- | ------------------------ | --- | ---------- | --- |
2

Introduction
Context
| • Sensors                      | for low | frequency    | seismic | applications (<2Hz): |     |     |     |
| ------------------------------ | ------- | ------------ | ------- | -------------------- | --- | --- | --- |
| - Geophones                    |         | (10Hz, ~5Hz) |         |                      |     |     |     |
| - Seismometers                 |         | (1-2Hz)      |         |                      |     |     |     |
| - Force Balance Accelerometers |         |              |         | (FBA)                |     |     |     |
(cid:1)
| bulky, costly, power consuming, not deemed |     |     |     |     | industrial..  |     |     |
| ------------------------------------------ | --- | --- | --- | --- | ------------- | --- | --- |
(cid:1)
phase rotation at low frequency, manufacturing tolerances, aging,
environmental conditions: amplitude & phase distortions detrimental to
| the fidelity | of the signal |     |     |     |     |     |     |
| ------------ | ------------- | --- | --- | --- | --- | --- | --- |
Phase response
2Hz seismometer (damping 0,7)
0
)seerged( esahP
-30
-60
-90
-120
-150
-180
|     |     |     | 0,01 | 0,1 | 1   | 10  | 100 |
| --- | --- | --- | ---- | --- | --- | --- | --- |
Frequency (Hz)
3

Introduction
Context
• MEMS accelerometers often perceived as too noisy at low frequency
| because | of 1/f noise |                |                    |
| ------- | ------------ | -------------- | ------------------ |
| - True  | for most     | of the seismic | MEMS on the market |
• Latest generation of digital closed-loop MEMS accelerometer, initially
designed for seismic imaging, exhibits very good noise performances
| at low frequency. |     |     |     |
| ----------------- | --- | --- | --- |
4

MEMS accelerometer
| Some | benefits | of MEMS accelerometer |     |     |     |     |
| ---- | -------- | --------------------- | --- | --- | --- | --- |
• No sensor leveling required, can be used in any orientation
| • Measures            | its | own tilt (DC response) |     |     |     |     |
| --------------------- | --- | ---------------------- | --- | --- | --- | --- |
| • Compact and very    |     | low power              |     |     |     |     |
| • Digital closed-loop |     | architecture:          |     |     |     |     |
- Frequency response flat and highly stable in amplitude and
phase (down to DC):
|     | ≫ Perfect           | time synchronization |      | of events | between | sensors |
| --- | ------------------- | -------------------- | ---- | --------- | ------- | ------- |
| -   | Very low distortion |                      |      |           |         |         |
| -   | Very fast           | clip recovery        | time |           |         |         |
5

MEMS Noise measurements
| Noise floor            | for seismic |           | imaging              | (Lainé, 2014) |
| ---------------------- | ----------- | --------- | -------------------- | ------------- |
| • Noise measured       |             | above     | 1Hz in LSBB (France) |               |
| • <15ng/sqrt(Hz) above |             |           | 10Hz                 |               |
| • 1/f noise at low     |             | frequency | not characterized    |               |
6

MEMS Noise measurements
| Low | frequency                    |      | noise measurement           |             |
| --- | ---------------------------- | ---- | --------------------------- | ----------- |
| •   | Basement                     |      | of office building in peri- |             |
|     | urban                        | area |                             |             |
| •   | Vibration isolation platform |      |                             | (f ~2,7Hz)  |
0
| •   | Soundproof    |                | acoustic                  | chamber |
| --- | ------------- | -------------- | ------------------------- | ------- |
| •   | Data acquired |                | at night over the course  |         |
|     | of several    | months         |                           |         |
| •   | Raw           | data processed |                           | using   |
ANSS/USGS Matlab script:
ANSS_noise_rms_rev4.m
7

MEMS Noise measurements
| Low | frequency                                | noise measurement  |     |
| --- | ---------------------------------------- | ------------------ | --- |
| •   | 2 QS-DB boards: Vertical and horizontal  |                    |     |
|     | – QuietSeis                              | MEMS accelerometer |     |
– UART serial data transmission to external device
| •   | 10 Hz and 5Hz geophone    |                | channels        |
| --- | ------------------------- | -------------- | --------------- |
|     | – low noise 24 bits / ADC |                |                 |
|     | – Velocity                | data converted | in acceleration |
QS-DB
8

MEMS Noise measurements
| Low | frequency | noise measurement |     |     |               |     |
| --- | --------- | ----------------- | --- | --- | ------------- | --- |
|     | 5Hz       |                   |     |     | Noise limited | by  |
10Hz
ambient vibrations
above ~2Hz
|     |     |     | MEMS 1/f                    | noise lower | than : |     |
| --- | --- | --- | --------------------------- | ----------- | ------ | --- |
|     |     |     | • 10Hz-geophone noise below |             | ~2Hz   |     |
|     |     |     | 5Hz-geophone noise below    |             | ~0,1Hz |     |
•
• NHNM down to ~0,1Hz
9

MEMS Noise measurements
Low frequency Dynamic Range
Full scale
+/- 5 m/s² pk
Dyn. Range
(3,5m/s² rms)
133dB
Dyn. Range
126dB
0,02-2Hz
Full scale @ +/-13m/s² pk :
• Vertical MEMS Dyn. Range ~131dB
10

MEMS Noise measurements
Comparative testing vs. Trillium Compact broadband seismometer
in a low noise test site is being scheduled with a French seismology
institution.
Test site Noise PPSD (vertical)
Trillium Compact QS-DB
11

Earthquake detection
IRAN-IRAK border M7.4 earthquake
• Nov 12th,2017
• 18:18:19 (UTC)
12

Earthquake detection
Earthquakeground acceleration
(Clinton, 2002)
MEMS Full scale
5m/s² pk
VVVVeeeerrrrttttiiiiccccaaaallll aaaaxxxxiiiissss MMMMEEEEMMMMSSSS aaaacccccccceeeelllleeeerrrroooommmmeeeetttteeeerrrr
MEMS Noise ((((PPPPoooowwwweeeerrrr ssssppppeeeeccccttttrrrruuuummmm))))
floor(typ.)
Natural frequency
of isolation platform
13

Earthquake detection
(cid:1)
t=180s 18:25:09 in NANTES
P-wave @ 18:25:06 in CLF
(cid:1)
t=515s 18:30:24 in NANTES
S-wave @ 18:30:35 in CLF
Good correlation with
CLF seismic station!

Conclusion
A new MEMS accelerometer with improved noise floor and
reduced 1/f noise contribution has been evaluated for very
weak signals and very low frequency measurements. A noise
floor below NHNM down to 0.1 Hz has been demonstrated.
New possibilities for low frequency, weak signal applications:
• Ambient seismic noise imaging and monitoring
• Seismology
- Replacement of Force Balance Accelerometers,
seismometers,…
• Structural Health Monitoring of large structures
- Operational Modal Analysis using ambient vibrations
• Active stabilization platforms in low noise
or low-g environments
15

Bibliography
References
• Clinton J.F., Heaton T.H., 2002, Potential Advantages of a Strong-motion
Velocity Meter over a Strong-motion Accelerometer: Seismological Research
Letters Volume 73, Number 3, 332-342.
• Lainé J., 2014, A high-sensitivity MEMS-based accelerometer: The Leading
Edge 33/11, 1234-1242
• Observatoire GEOSCOPE (doi: 10.18715/GEOSCOPE.G), Centre de Données
de l'Institut de Physique du Globe de Paris.
http://geoscope.ipgp.fr/index.php/fr/catalogue/description-d-un-seisme?seis=us2000bmcg
16