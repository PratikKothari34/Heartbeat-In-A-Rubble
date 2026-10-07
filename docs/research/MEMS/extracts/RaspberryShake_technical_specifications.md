Watch the Earth Move

Raspberry Shake Technical
Speciﬁcations

Website: raspberryshake.org

Contact us: sales@raspberryshake.org

RS1D

Specifications for:
The Original (1D) Raspberry Shake
- Your Personal Seismograph -
An IoT home automation device
Born on: October, 2016
https://shop.raspberryshake.org/
sales@raspberryshake.org

Last updated: 5-aug-2021

Unit

The Raspberry Shake Personal Seismograph is an all-in-one, IoT plug-and-go solution for

personal seismology that integrates a vertical (1D) velocity sensor, the digitizer, the hyper

damper, and the computer into a single box. The Raspberry Shake Personal Seismograph is

manufactured in China using cutting-edge 3D printing and laser-cutting technology.

Warranty: 1 year from ship date

Specifications subject to change without notice.

Parameter

Value

Raspberry Shake Version

All versions

Dimensions (estimated)

Standard enclosure: 135x110x50 mm

IP67 enclosure: 160x90x90 mm

Weight (estimated)

0.35 kg

Immersion rating

Standard enclosure: IP10

IP67 enclosure available upon request at

additional cost

Connectors

Standard enclosure: Ethernet (RJ45), Power

Micro USB (5V, 2.5 Amps), USB 2 ports x4,

RS1D

HDMi, Micro SD, CSI Camera port,

Composite video and audio output jack

IP 67 enclosure: Ethernet (RJ45), Power. Note:
the supported standard for the IP67 LAN
connector is 100 Mbit/s (4-wired LAN cable).

Installation Considerations

Designed for plug-and-go installation

Operating Temperature

0 to 60 C (limited by RPi, the Raspberry

Shake itself can go to -20C)

On Board Computer

Raspberry Pi 3 Model B

The Raspberry Shake board/ Software is also

compatible with:

00[10,13],900032: Model B+

a[01040,01041,21041,22042]: 2 Model B

9000[92,93],9200[92,93]: Zero

a[02082,22082,32082,52082]: 3 Model B

a020d3: 3 Model B+

4 Model B

9000c1: Zero W(H)

Storage Device

8 Gb or + micro SD card

Est. # days of disk space:

OS/ software: ~3 Gb
Remaining space for data: ~5 Gb

V5/ V4 (50 sps):

# days (7.5 Mb/ day/ channel [x1]):

~660, more if you use a bigger SD

V6+ (100 sps):

Timing

Timing Quality

RS1D

# days (15 Mb/ day/ channel): ~320,

more if you use a bigger SD

Network Timing Protocol, NTP (default)

GPS timing supported

NTP timing quality remains within 1 sample of

accuracy versus startup accuracy:

V6+: +/- 10 ms or better @ 100 sps

V5 / V4: +/- 20 ms or better @ 50 sps

RS1D

Seismograph

Parameter

Value

Type

Single-component 4.5 Hz 395 Ohm vertical Racotech

RGI-20DX geophone with electronic extension to lower

Samples per second

frequencies (<1 Hz)

V6+: 100 sps

V5 / V4: 50 sps

Earthquake Early Warning (EEW) compatible*
V6: data packets shipped across serial port at a rate of 4 packets/ second (250 ms/ packet)

V5/ V4: data packets shipped across serial port at a rate of 1 packet/ second (1000 ms/ packet)

Bandwidth (estimated)

V7+: -3dB points at 0.7 and 44 Hz

V6: -3dB points at 0.8 and 29 Hz

V5/V4: -3dB points at 0.8 and 23 Hz

Poles (estimate,

radians/ second)

V7+:

-1 (0.16 Hz, single pole high pass filter)

-3.03 x2 (0.48 Hz, double pole high pass filter)

-666.67 (106 Hz, single pole low pass filter)

V6: -4.88+/-3.06E+02, -2.22+/-1.18E+02, -3.33+/-1.98E+02

V5/V4: -4.21, -2.33, -1.30

Zeros (estimate,

radians/ second)

V7+: 0; 0; 0

V6: -4.51+/-3.08E+02, 0, 0

RS1D

V5/V4: -6.75, 0, 0, 0

Sensitivity (estimated)

V7+: 3.996500E+08 counts/ meter/ second +/- 10%

precision

V6: 3.81E+08 counts/ meter/ second +/- 10% precision

V5/V4: 4.69E+08 counts/ meter/ second +/- 10% precision

Clip Level (estimated)

+/- 8,388,608 counts (24-bits)

V7+: 21 mm/s peak-to-peak from 0.1 to 10 Hz

V6: 22 mm/s peak-to-peak from 0.1 to 10 Hz

V5/V4: 18 mm/s peak-to-peak from 0.1 to 10 Hz

Minimum Detection

Threshold (estimate)

V7+: 0.08 µm/ s RMS from 1 to 20 Hz @ 100 sps

V6: 0.03 µm/ s RMS from 1 to 20 Hz @ 100 sps

V5/V4: 0.14 µm/ s RMS from 1 to 20 Hz @ 50 sps

Note: The minimum detectable level is considered to be 10

dB above the noise RMS. Dynamic range is the full scale

sinusoid RMS over the noise RMS in dB.

Digitizer

24-bit ADC Sigma-Delta

Dynamic range

144 dB (24 bits)

Effective bits

(estimated)

V6+: 21 bits (126 dB) from 1 to 20 Hz @ 100 sps

V5/V4: 18.5 bits (110.5 dB) from 1 to 20 Hz @ 50 sps (for

the entire analog to digital hardware chain).

Note: Whereas most manufacturers report this for their

digitizer only, we are reporting it for the entire sensor + ADC

RS1D

hardware chain. The effective bits of the digitizer itself are

necessarily better.

This parameter is also commonly known as “Dynamic

Range”; “RMS to RMS noise"; or "noise free bits".

*Applies to firmware versions 2.X.X and higher and units shipped purchased after July, 2017

Velocity Channel Instrument Response:

Sleeman Self-Noise:

RS1D

(same as 4Dv6)

RS1D

Software

Software installed on Raspberry Shake's RPi computer

100% SeisComP3 compatible

Also: AQMS, Antelope, Earlybird, Earthworm, Hydra, ObsPy, SEISAN, …

Native SeedLink Server (source: GEOFON) with Raspberry Shake’s Data Flow Message

Router

Tight and automatic integration with SeisComP

Web-interface (HTML) for easy configuration

Software to store continuous seismic data in miniSEED format

Web-based helicorder plot generator (source: USGS)

Swarm (source: USGS)

Software distributed with Docker

Automatic updates

Operating System: Debian 8 (Linux)

RS1D

Communications

Parameter

Digital bandwidth consumption at 100

Hz, per channel

Value

Average:

820 bytes/ second

71 megabytes/ day

Max:

1420 bytes/ second

123 megabytes/ day

TCP/IP compatible

Compatible with Ethernet, Cell, GPRS, Satellite modems. The supported standard for the
IP67 LAN connector is 100 Mbit/s (4-wired LAN cable).

Power

Parameter

Value

Power Supply Voltage

5 Volts DC (2.5 Amp supply)

Power Consumption (RPi +

Raspberry Shake, estimated)

Startup: 5 Volts x 0.550 A = 2.8 Watts

Run-time: 5 Volts x 0.290 A = 1.5 Watts

Calibration Mechanism: Calibration not required over time but can be verified using the OSOP
Calibration Table. All seismographs are verified prior to shipping to ensure that their gain is
within 10% of the nominal instrument response (up to 10% variation attributable to geophones
and capacitors).

RS3D

Specifications for: Raspberry Shake 3D
- Your 3D Personal Seismograph -
An IoT home-automation device
Born on: February, 2017
https://shop.raspberryshake.org/
sales@raspberryshake.org

Last updated: 21-sept-2020

Unit

The Raspberry Shake 3D Personal Seismograph is an all-in-one, IoT plug-and-go solution for

personal seismology that integrates a 3 orthogonal velocity sensors, the digitizers, the hyper

dampers, and the computer into a single box. The Raspberry Shake 3D Personal Seismograph

is manufactured in China using cutting-edge 3D printing and laser-cutting technology.

Warranty: 1 year from ship date

Specifications subject to change without notice.

Parameter

Value

Raspberry Shake 3D Version

All versions

Dimensions (estimated)

Standard enclosure: 140x135x60 mm

IP67 enclosure: 160x90x90 mm

Weight (estimated)

0.6 kg

Immersion rating

Standard enclosure: IP10

Connectors

IP67 enclosure available upon request at

additional cost

Standard enclosure: Ethernet (RJ45), Power

Micro USB (5V, 2.5 Amps), USB 2 ports x4,

HDMi, Micro SD, CSI Camera port,

Composite video and audio output jack

RS3D

IP 67 enclosure: Ethernet (RJ45), Power. Note:
the supported standard for the IP67 LAN
connector is 100 Mbit/s (4-wired LAN cable).

Installation Considerations

Designed for plug-and-go installation

Operating Temperature

0 to 60 C (limited by RPi, the Raspberry

Shake itself can go to -20C)

On Board Computer

Raspberry Pi 3 Model B

The Raspberry Shake board/ Software is also

compatible with:

00[10,13],900032: Model B+

a[01040,01041,21041,22042]: 2 Model B

a[02082,22082,32082,52082]: 3 Model B

a020d3: 3 Model B+

4 Model B

Storage Device

8 Gb or + micro SD card

Est. # days of disk space:

OS/ software: ~3 Gb

Remaining space for data: ~5 Gb

# days (15 Mb/ day/ channel [x3]): ~110, more

if you use a bigger SD

Network Timing Protocol, NTP (default)

GPS timing supported

NTP timing quality remains within 1 sample of

accuracy versus startup accuracy: +/- 10 ms

or better @ 100 sps

Timing

Timing Quality

RS3D

Seismograph

Parameter

Value

Type

3-component, orthogonally placed 4.5 Hz (electronically

extended down to 2 seconds) Sunfull PS-4.5B geophones,

375 Ohm

Note: These are not the same geophones used in the 1D and 4D

versions of Raspberry Shake

Samples per second

100

Earthquake Early Warning (EEW) compatible

data packets shipped across serial port at a rate of 4 packets/ second (250 ms/ packet)

Bandwidth (estimate)

V5+: -3dB points at 0.7 to 39 Hz

V3: -3dB points at 0.6 to 34 Hz

Poles (estimate,

radians/ second)

V5+:

-1 (0.16 Hz, single pole high pass filter)

-3.03 x2 (0.48 Hz, double pole high pass filter)
-666.67 (106 Hz, single pole low pass filter)

V3: 2.23E+02 +/- 2.95E+02; 3.76E-01; 0

Zeros (estimate,

radians/ second)

V5+: 0, 0, 0

Sensitivity (estimate)

V3: -1.96E+02 +/- 1.55E+02; 2.65 +/- 6.83E-01

V5+: 3.60E+08 counts/ meter/ second +/- 10% precision

V3: 3.53E+08 counts/ meter/ second +/- 10% precision

RS3D

Clip Level (estimate)

+/- 8,388,608 counts (24-bits)

Minimum Detection

Threshold (estimate)

V5+/ V3: 24 mm/s peak-to-peak from 0.1 to 10 Hz

V5+: 0.03 µm/ s RMS from 1 to 20 Hz @ 100 sps

V3: 0.06 µm/ s RMS from 1 to 20 Hz @ 100 sps

Note: The minimum detectable level is considered to be 10

dB above the noise RMS. Dynamic range is the full scale

sinusoid RMS over the noise RMS in dB.

Digitizer

24-bit ADC Sigma-Delta

Dynamic range

144 dB (24 bits)

Effective bits (estimate)

V5+: 21 bits (124 dB) from 1 to 20 Hz @ 100 sps (for the

entire analog to digital hardware chain).

V3: 20 bits (120 dB) from 1 to 20 Hz @ 100 sps (for the

entire analog to digital hardware chain).

Note: Whereas most manufacturers report this for their

digitizer only, we are reporting it for the entire sensor + ADC

hardware chain. The effective bits of the digitizer itself are

necessarily better.

This parameter is also commonly known as “Dynamic

Range”; “RMS to RMS noise"; or "noise free bits".

RS3D

Velocity Channel Instrument Response:

RS3D

Sleeman Self-noise:

RS3D

Software

Software installed on Raspberry Shake's RPi computer

100% SeisComP3 compatible

Also: AQMS, Antelope, Earlybird, Earthworm, Hydra, ObsPy, SEISAN, …

Native SeedLink Server (source: GEOFON) with Raspberry Shake’s Data Flow Message

Router

Tight and automatic integration with SeisComP

Web-interface (HTML) for easy configuration

Software to store continuous seismic data in miniSEED format

Web-based helicorder plot generator (source: USGS)

Swarm (source: USGS)

Software distributed with Docker

Automatic updates

Operating System: Debian 8 (Linux)

RS3D

Communications

Parameter

Digital bandwidth consumption at 100

Hz, per channel

Value

Average:

820 bytes/ second

71 megabytes/ day

Max:

1420 bytes/ second

123 megabytes/ day

TCP/IP compatible

Compatible with Ethernet, Cell, GPRS, Satellite modems. The supported standard for the
IP67 LAN connector is 100 Mbit/s (4-wired LAN cable).

Power

Parameter

Value

Power Supply Voltage

5 Volts DC (2.5 Amp supply)

Power Consumption (RPi +

Raspberry Shake, estimated)

Startup: 5 Volts x 0.550 A = 2.8 Watts

Run-time: 5 Volts x 0.320 A = 1.6 Watts

Calibration Mechanism: Calibration not required over time but can be verified using the OSOP
Calibration Table. All seismographs are verified prior to shipping to ensure that their gain is
within 10% of the nominal instrument response (up to 10% variation attributable to geophones
and capacitors).

RS4D

Specifications for: Raspberry Shake RS4D
- Your RS4D Personal Seismograph & Accelerograph -
An IoT home-automation device
Born on: February, 2017
https://shop.raspberryshake.org/

sales@raspberryshake.org
Last updated: 1-feb-2021

Unit

The “Raspberry Shake RS4D” Personal Seismograph & Accelerograph is an all-in-one, IoT

plug-and-go solution for personal seismology that integrates a single vertical velocity sensors

with a 2G orthogonal MEMS accelerometer, the digitizers, the hyper dampers, and the computer

into a single box. The Raspberry Shake RS4D is manufactured in China using cutting-edge  3D

printing and laser-cutting technology.

Warranty: 1 year from ship date

Parameter

Value

Raspberry Shake 4D Version

All versions

Specifications subject to change without notice.

Dimensions (estimated)

Standard enclosure: 135x110x50 mm

IP67 enclosure: 160x90x90 mm

Weight (estimated)

0.35 kg

Immersion rating

Standard enclosure: IP10

IP67 enclosure available upon request at

additional cost

Connectors

Standard enclosure: Ethernet (RJ45), Power

Micro USB (5V, 2.5 Amps), USB 2 ports x4,

RS4D

HDMi, Micro SD, CSI Camera port,

Composite video and audio output jack

IP 67 enclosure: Ethernet (RJ45), Power. Note:
the supported standard for the IP67 LAN
connector is 100 Mbit/s (4-wired LAN cable).

Designed for plug-and-go installation

Mounting screw anchor slot provided

Alignment: with axis of building or magnetic.

North arrow provided.

Installation Considerations

Operating Temperature

0 to 60 C (limited by RPi, the Raspberry

Shake itself can go to -20C)

On Board Computer

Raspberry Pi 3 Model B

The Raspberry Shake board/ Software is also

compatible with:

00[10,13],900032: Model B+

a[01040,01041,21041,22042]: 2 Model B

a[02082,22082,32082,52082]: 3 Model B

a020d3: 3 Model B+

4 Model B

Storage Device

8 Gb or + micro SD card

Est. # days of disk space:

OS/ software: ~3 Gb

Remaining space for data: ~5 Gb

# days (15 Mb/ day/ channel [x4]): ~80, more

if you use a bigger SD

Timing

Network Timing Protocol, NTP (default)

RS4D

Timing Quality

GPS timing supported

NTP timing quality remains within 1 sample of

accuracy versus startup accuracy: +/- 10 ms

or better @ 100 sps

RS4D

Seismograph

Parameter

Value

Type

Single-component 4.5 Hz 395 Ohm vertical Racotech

RGI-20DX geophone with electronic extension to lower

frequencies (<1 Hz)

Samples per second

100

Earthquake Early Warning (EEW) compatible

data packets shipped across serial port at a rate of 4 packets/ second (250 ms/ packet)

Bandwidth (estimate)

V6+: -3dB points at 0.7 and 44 Hz
V5: -3dB points at 0.7 and 26 Hz, possibly higher

V4: -3dB points at 0.7 and 40 Hz

Poles (estimate,

radians/ second)

V6+:

-1 (0.16 Hz, single pole high pass filter)

-3.03 x2 (0.48 Hz, double pole high pass filter)
-666.67 (106 Hz, single pole low pass filter)

V5: -1.63E+02 +/- 1.02E+02; -3.61; -1.41 +/- 4.11E-01

V4: 1.82E+02 +/- 3.43E+02; 4.56E-01; 0

Zeros (estimate,

radians/ second)

V6+: 0; 0; 0

V5: -5.78E+03; 0; 0; 0

V4: -3.60E+02 +/- 8.29E+02; -3.04 +/- 8.48E-01

RS4D

Sensitivity (estimate)

V6+: 3.996500E+08 counts/ meter/ second +/- 10%

precision

V5: 3.36E+08 counts/ meter/ second +/- 10% precision

V4: 4.05E+08 counts/ meter/ second +/- 10% precision

Clip Level (estimate)

+/- 8,388,608 counts (24-bits)

V4+: 21 mm/s peak-to-peak from 0.1 to 10 Hz

Minimum Detection

Threshold (estimate)

V5+: 0.08 µm/ s RMS from 1 to 20 Hz @ 100 sps

V4: 0.16 µm/ s RMS from 1 to 20 Hz @ 100 sps

Note: The minimum detectable level is considered to be 10

dB above the noise RMS. Dynamic range is the full scale

sinusoid RMS over the noise RMS in dB.

Digitizer

24-bit ADC Sigma-Delta

Dynamic range

144 dB (24 bits)

Effective bits (estimate)

V5+: 21 bits (126 dB) from 1 to 20 Hz @ 100 sps (for the

entire analog to digital hardware chain).

V4: 18 bits (109 dB) from 1 to 20 Hz @ 100 sps (for the

entire analog to digital hardware chain).

Note: Whereas most manufacturers report this for their

digitizer only, we are reporting it for the entire sensor + ADC

hardware chain. The effective bits of the digitizer itself are

necessarily better.

This parameter is also commonly known as “Dynamic

Range”; “RMS to RMS noise"; or "noise free bits".

RS4D

Velocity Channel Instrument Response:

Sleeman Self-Noise:

RS4D

RS4D

Accelerograph: MEMs

Think of the addition of the MEMs sensor as your insurance plan to guarantee that the

Raspberry Shake remains on-scale for big earthquakes or smaller, local ones where the

Raspberry Shake is located near the source, as often happens in settings like Oklahoma.

Parameter

Value

Sensor

3-component, orthogonally placed +/- 2g MEMs sensor

(Class C)

Samples per second

100

Earthquake Early Warning (EEW) compatible

data packets shipped across serial port at a rate of 5 packets/ second (200 ms/ packet)

Flat Frequency Range

(estimate, -3dB points)

V6+: DC to 44 Hz
V5: DC to 23 Hz, possibly higher

V4: DC to 29 Hz, possibly higher

Poles (estimate)

V6+:

-459.56 (73 Hz, single pole low pass filter)
-1785.71 (284 Hz, single pole low pass filter)

V5: 6.57E+02 +/- 1.20E+03; 0

V4: 5.06E+01 +/- 2.86E+02; 0

Zeros (estimate)

V6+: None

V5: -1.26E+02 +/- 1.02E+-02; -6.24E-05

V4: -4.33E+02; -1.45E+02 +/- 2.78E+02; 3.94E-02

RS4D

Sensitivity (estimate)

V6+: 3.845E+05 counts/ meter/ second squared +/- 10%

precision

V5: 3.87E+05 counts/ meter/ second squared +/- 10%

precision

V4: 3.96E+05 counts/ meter/ second squared +/- 10%

precision

Clip Level (estimate)

V5+/ V4: +/-2G (21-22 m/s^2 peak-to-peak from 0.1 to 10

Hz)

Digitizer

Dynamic range

24-bit ADC Sigma-Delta

144 dB (24 bits)

Effective bits (estimate)

V4+: 14 bits (84 dB) from 1 to 10 Hz @ 100 sps (for the

entire analog to digital hardware chain).

Note: Whereas most manufacturers report this for their

digitizer only, we are reporting it for the entire sensor +

ADC hardware chain. The effective bits of the digitizer itself

are necessarily better.

This parameter is also commonly known as “Dynamic

Range”; “RMS to RMS noise"; or "noise free bits".

Noise Level

V4+: 3000 µm/ s (0.3 Gal, 0.0003 g) RMS from 1 to 10 Hz

@ 100 sps

RS4D

Acceleration Channel Instrument Response:

Sleeman Self-Noise:

RS4D

RS4D

Software

Software installed on Raspberry Shake's RPi computer

100% SeisComP3 compatible

Also: AQMS, Antelope, Earlybird, Earthworm, Hydra, ObsPy, SEISAN, …

Native SeedLink Server (source: GEOFON) with Raspberry Shake’s Data Flow Message

Router

Tight and automatic integration with SeisComP

Web-interface (HTML) for easy configuration

Software to store continuous seismic data in miniSEED format

Web-based helicorder plot generator (source: USGS)

Swarm (source: USGS)

Software distributed with Docker

Automatic updates

Operating System: Debian 8 (Linux)

RS4D

Communications

Parameter

Digital bandwidth consumption at 100

Hz, per channel

Value

Average:

820 bytes/ second

71 megabytes/ day

Max:

1420 bytes/ second

123 megabytes/ day

TCP/IP compatible

Compatible with Ethernet, Cell, GPRS, Satellite modems. The supported standard for the
IP67 LAN connector is 100 Mbit/s (4-wired LAN cable).

Power

Parameter

Value

Power Supply Voltage

5 Volts DC (2.5 Amp supply)

Power Consumption (RPi +

Raspberry Shake, estimated)

Startup: 5 Volts x 0.550 A = 2.8 Watts

Run-time: 5 Volts x 0.460 A = 2.3 Watts

Calibration Mechanism: Calibration not required over time but can be verified using the OSOP
Calibration Table. All seismographs are verified prior to shipping to ensure that their gain is
within 10% of the nominal instrument response (up to 10% variation attributable to geophones
and capacitors).

RBOOM-RS&BOOM

Specifications for:
Raspberry Boom (RBOOM) and 'Shake and Boom'
(RS&BOOM)
- Your Personal Acoustic and Seismo-Acoustic Home Science Monitors -
An IoT home-automation device
Born on: July, 2017
https://shop.raspberryshake.org/

sales@raspberryshake.org
Last updated: 9-February-2022

Unit

The “Raspberry Boom” (RBOOM) personal infrasound and "Raspberry Shake and Boom"

(RS&BOOM) personal seismo-acoustic monitors are all-in-one, IoT plug-and-go solutions for

personal infrasonics and seismology that integrates a single vertical velocity sensors with an

acoustic pressure transducer, the digitizers, the hyper dampers, and the computer into a single

box. These monitors are manufactured in China using cutting-edge 3D printing and

laser-cutting technology.

Warranty: 1 year from ship date

Parameter

Versioning

Value

All versions

Specifications subject to change without notice.

Dimensions (estimated)

Standard enclosure: 135x110x70 mm

IP67 enclosure: 160x90x90 mm

Weight (estimated)

0.4 kg

Immersion rating

Standard enclosure: IP10

Connectors

Standard enclosure: Ethernet (RJ45), Power

Micro USB (5V, 2.5 Amps), USB 2 ports x4,

RBOOM-RS&BOOM

HDMi, Micro SD, CSI Camera port,

Composite video and audio output jack

IP 67 enclosure: Ethernet (RJ45), Power. Note:
the supported standard for the IP67 LAN
connector is 100 Mbit/s (4-wired LAN cable).

Installation Considerations

Designed for plug-and-go installation

Mounting screw anchor slot provided (for

RBOOM)

Alignment: no alignment required (the

infrasound sensor is omnidirectional and the

velocity sensor, vertical)

Operating Temperature

0 to 60 C (limited by RPi, the Raspberry Boom

itself can go to -20C)

On Board Computer

Raspberry Pi 3 Model B

The Raspberry Shake board/ Software is also

compatible with:

00[10,13],900032: Model B+

a[01040,01041,21041,22042]: 2 Model B

9000[92,93],9200[92,93]: Zero

a[02082,22082,32082,52082]: 3 Model B

a020d3: 3 Model B+

4 Model B

9000c1: Zero W(H)

Storage Device

8 Gb or + micro SD card

Est. # days of disk space:

OS/ software: ~3 Gb

Remaining space for data: ~5 Gb

RBOOM-RS&BOOM

# days Raspberry Boom (15 Mb/ day/

channel): ~320, more if you use a bigger SD

# days Raspberry Shake and Boom (15 Mb/

day/ channel): ~160, more if you use a bigger

SD

Network Timing Protocol, NTP (default)

GPS timing supported

NTP timing quality remains within 1 sample of

accuracy versus startup accuracy: +/- 10 ms

or better @ 100 sps

Timing

Timing Quality

RBOOM-RS&BOOM

Microbarograph (Infrasound)
Applies to both Raspberry Boom & Raspberry Shake and Boom

Parameter

Value

Type

MEMS temperature compensated differential pressure

transducer

Samples per second

100

Data packet transmission

Data packets shipped across serial port at a rate of 4

rate

packets/ second (250 ms/ packet)

Bandwidth (estimate)

-3dB points at 1 Hertz (1 seconds) to 44 Hertz (for 1s

mechanical filter, default).

-3dB points at 0.08 Hertz (13 seconds) to 44 Hertz (for 20s

mechanical filter, not included by default with order,

available upon special request only).

Rolloff past low frequency corners: 2 poles or 40dB/decade

Poles (estimate, radians/

There is a hardware single-pole high-pass filter with a -3

second)

dB point around 0.05 Hz.

With 1s mechanical filter attached (default):

-0.312 (20 seconds, single pole high pass filter,

from hardware)

-6.289 (1 Hz, single pole high pass filter, from

mechanical filter)

With 20s mechanical filter attached (not included by default

with order, available upon special request only):

RBOOM-RS&BOOM

-0.312 (20 seconds, single pole high-pass filter,

from hardware)

-0.312 (20 seconds, single pole high pass

filter,  from mechanical filter)

Zeros (estimate, radians/

0,0

second)

Sensitivity (estimate)

56,000 counts/ Pascal +/- 10% precision

Clip Level (estimate)

+/- 8,388,608 counts (24-bits)

0.5 inches of water, corresponding to +/- 125 Pa

Digitizer

Dynamic range

24-bit ADC Sigma-Delta

144 dB (24 bits)

Effective bits (estimate)

21 bits (126 dB) from 1 to 20 Hz @ 100 sps (for the entire

analog to digital hardware chain).

Note: Whereas most manufacturers report this for their

digitizer only, we are reporting it for the entire sensor +

ADC hardware chain. The effective bits of the digitizer itself

are necessarily better.

This parameter is also commonly known as “Dynamic

Range”; “RMS to RMS noise"; or "noise free bits".

Error band

Linearity of the pressure
measurement (included in
total error band
measurement)

Gain Calibration

~1%

<0.5%

Automatic

RBOOM-RS&BOOM

Mechanical filter High Pass
filter options

1s (default, included with order), 20s (available upon

special request only)

Operating Temperature of

sensor

Compensated operating range: 0 to 50 C

Max. operating range: -25 to 85 C (though the rest of the

electronics are limited to 0-60C)

The Raspberry Boom infrasound sensor was based on Jeffrey Johnson’s InfraBSU sensor and the work published in (1) Marcillo, O., Johnson, J.B., and Hart, D. (2012)

Implementation, Characterization, and Evaluation of an Inexpensive Low-Power, Low-Noise Infrasound Sensor Based on a Micromachined Differential Pressure Transducer and

a Mechanical Filter, Journal of Atmospheric and Oceanic Technology 29:1275-1284; and (2) Johnson, J.B. and Ripepe, M. (2011) Volcano Infrasound: A review, Journal of

Volcanology and Geothermal Research 206:61-69.

RBOOM-RS&BOOM

Microbarograph: Acoustic Channel Instrument Response

Microbarograph: Sleeman Self-Noise

RBOOM-RS&BOOM

RBOOM-RS&BOOM

Seismograph
Raspberry "Shake and Boom" only

Parameter

Value

Type

Single-component 4.5 Hz 395 Ohm vertical Racotech

RGI-20DX geophone with electronic extension to lower

frequencies (<1 Hz)

Samples per second

100

Earthquake Early Warning (EEW) compatible

data packets shipped across serial port at a rate of 4 packets/ second (250 ms/ packet)

Bandwidth (estimate)

-3dB points at 0.7 to 44 Hz

Poles (estimate,

radians/ second)

-1 (0.16 Hz, single pole high pass filter)

-3.03 x2 (0.48 Hz, double pole high pass filter)

-666.67 (106 Hz, single pole low pass filter)

Zeros (estimate,

radians/ second)

0; 0; 0

Sensitivity (estimate)

3.996500E+08 counts/ meter/ second +/- 10% precision

Clip Level (estimate)

+/- 8,388,608 counts (24-bits)

21 mm/s peak-to-peak from 0.1 to 10 Hz

Minimum Detection

Threshold (estimate)

0.08 µm/ s RMS from 1 to 20 Hz @ 100 sps

RBOOM-RS&BOOM

Note: The minimum detectable level is considered to be 10

dB above the noise RMS. Dynamic range is the full scale

sinusoid RMS over the noise RMS in dB.

Digitizer

24-bit ADC Sigma-Delta

Dynamic range

144 dB (24 bits)

Effective bits (estimate)

21 bits (126 dB) from 1 to 20 Hz @ 100 sps (for the entire

analog to digital hardware chain).

Note: Whereas most manufacturers report this for their

digitizer only, we are reporting it for the entire sensor + ADC

hardware chain. The effective bits of the digitizer itself are

necessarily better.

This parameter is also commonly known as “Dynamic

Range”; “RMS to RMS noise"; or "noise free bits".

RBOOM-RS&BOOM

Seismograph: Velocity Channel Instrument Response

RBOOM-RS&BOOM

Seismograph: Sleeman Self-Noise

RBOOM-RS&BOOM

Software

Software installed on Raspberry Shake's RPi computer

100% SeisComP3 compatible

Also: AQMS, Antelope, Earlybird, Earthworm, Hydra, ObsPy, SEISAN, …

Native SeedLink Server (source: GEOFON) with Raspberry Shake’s Data Flow Message

Router

Tight and automatic integration with SeisComP

Web-interface (HTML) for easy configuration

Software to store continuous seismic data in miniSEED format

Web-based helicorder plot generator (source: USGS)

Swarm (source: USGS)

Software distributed with Docker

Automatic updates

Operating System: Debian 8 (Linux)

RBOOM-RS&BOOM

Communications

Parameter

Digital bandwidth consumption at 100

Hz, per channel

Value

Average:

820 bytes/ second

71 megabytes/ day

Max:

1420 bytes/ second

123 megabytes/ day

TCP/IP compatible

Compatible with Ethernet, Cell, GPRS, Satellite modems. The supported standard for the
IP67 LAN connector is 100 Mbit/s (4-wired LAN cable).

Power

Parameter

Value

Power Supply Voltage

5 Volts DC (2.5 Amp supply)

Power Consumption (RPi +

Raspberry Shake, estimated)

Raspberry Boom:

Startup: 5 Volts x 0.550 A = 3.0

Watts

Run-time: 5 Volts x 0.290 A = 1.8

Watts

RBOOM-RS&BOOM

Raspberry Shake and Boom:

Startup: 5 Volts x 0.550 A = 3.1

Watts

Run-time: 5 Volts x 0.290 A = 1.9

Watts

Calibration Mechanism: Calibration not required over time but can be verified using the OSOP
Calibration Table. All seismographs are verified prior to shipping to ensure that their gain is
within 10% of the nominal instrument response (up to 10% variation attributable to geophones
and capacitors).

