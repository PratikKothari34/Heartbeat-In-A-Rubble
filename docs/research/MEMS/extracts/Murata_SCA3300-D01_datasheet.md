|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |         |
| --- | --- | --- | --- | --- | ------- |
|     |     |     |     |     | 1 (42)  |

Data Sheet

SCA3300-D01
3-axis industrial accelerometer with
digital SPI interface

Features
| •  3-axis (XYZ) accelerometer          |     |     |     |     |     |
| -------------------------------------- | --- | --- | --- | --- | --- |
| •  User selectable measurement modes:  |     |     |     |     |     |
± 1.5g, ± 3g, ± 6g with 70 Hz measurement bandwidth
± 1.5g with 10 Hz measurement bandwidth
| •  −40°C…+125°C operating range               |     |     |     |     |     |
| --------------------------------------------- | --- | --- | --- | --- | --- |
| •  3.0V…3.6V supply voltage                   |     |     |     |     |     |
| •  SPI digital interface                      |     |     |     |     |     |
| •  Extensive self-diagnostics features        |     |     |     |     |     |
| •  Ultra-low 37 µg/√Hz noise density          |     |     |     |     |     |
| •  Excellent offset stability                 |     |     |     |     |     |
| •  Size 8.6 x 7.6 x 3.3 mm (l × w × h)        |     |     |     |     |     |
| •  RoHS compliant robust DFL plastic package  |     |     |     |     |     |
suitable for lead free soldering process and SMD
mounting
| •  Proven capacitive 3D-MEMS technology  |     |     |     |     |     |
| ---------------------------------------- | --- | --- | --- | --- | --- |

Applications
SCA3300-D01 is targeted at applications demanding high
stability with tough environmental requirements.
Typical applications include:
| •  Leveling                           |     |     |     |     |     |
| ------------------------------------- | --- | --- | --- | --- | --- |
| •  Angle measurement                  |     |     |     |     |     |
| •  Tilt compensation                  |     |     |     |     |     |
| •  Inertial Measurement Units (IMUs)  |     |     |     |     |     |
| •  Motion analysis and control        |     |     |     |     |     |
| •  Navigation systems                 |     |     |     |     |     |
Overview
The SCA3300-D01 is a high-performance accelerometer sensor. It is a three-axis accelerometer sensor based on
Murata's proven capacitive 3D-MEMS technology. Signal processing is done in a mixed-signal ASIC with flexible SPI
digital interface. The sensor element and ASIC are packaged into 12-pin pre-molded plastic housing that guarantees
reliable operation over the product's lifetime.
The SCA3300-D01 is designed, manufactured and tested for high stability, reliability and quality requirements. The
component has extremely stable output over a wide range of temperature and vibration. The component has several
advanced self-diagnostics features, is suitable for SMD mounting, and is compatible with the RoHS and ELV
directives.
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | www.murata.com         |     |              | Rev. 3        |     |

2 (42)
TABLE OF CONTENTS
1 Introduction ................................................................................................................................. 4
2 Specifications ............................................................................................................................. 4
2.1 Abbreviations ......................................................................................................................... 4
2.2 General Specifications ........................................................................................................... 4
2.3 Performance Specifications for Accelerometer....................................................................... 5
2.4 Performance Specification for Temperature Sensor ............................................................... 6
2.5 Absolute Maximum Ratings ................................................................................................... 6
2.6 AEC-Q100 Testing ................................................................................................................. 7
2.7 Pin Description....................................................................................................................... 8
2.8 Typical performance characteristics ....................................................................................... 9
2.9 Digital I/O Specification ........................................................................................................ 13
2.9.1 DC Characteristics .......................................................................................................... 13
2.9.2 SPI AC Characteristics ................................................................................................... 14
2.10 Measurement Axis and Directions........................................................................................ 15
2.11 Package Characteristics ...................................................................................................... 16
2.11.1 Package Outline Drawing ............................................................................................ 16
2.12 PCB Footprint ...................................................................................................................... 17
3 General Product Description.................................................................................................... 17
3.1 Factory Calibration ............................................................................................................... 18
4 Component Operation, Reset and Power Up .......................................................................... 18
4.1 Component Operation .......................................................................................................... 18
4.2 Start-up sequence ............................................................................................................... 19
4.3 Operation modes ................................................................................................................. 20
5 Component Interfacing ............................................................................................................. 21
5.1.1 General ........................................................................................................................... 21
5.1.2 Protocol .......................................................................................................................... 21
5.1.3 SPI frame ....................................................................................................................... 22
5.1.4 Operations ...................................................................................................................... 24
5.1.5 Return Status .................................................................................................................. 25
5.2 Checksum (CRC) ................................................................................................................. 25
6 Register Definition .................................................................................................................... 26
6.1 Sensor Data Block ............................................................................................................... 28
6.1.1 Example of Acceleration Data Conversion ...................................................................... 28
6.1.2 Example of Temperature Data Conversion ..................................................................... 29
6.2 STO ..................................................................................................................................... 29
6.2.1 Example of Self-Test Analysis ........................................................................................ 30
Murata Electronics Oy SCA3300-D01 Doc.No. 3165
www.murata.com Rev. 3

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |         |
| --- | --- | --- | --- | --- | ------- |
|     |     |     |     |     | 3 (42)  |

6.3  STATUS .............................................................................................................................. 31
6.3.1  Example of STATUS summary reset ................................................................................... 33
6.4  Error Flag Block ................................................................................................................... 33
6.4.1  ERR_FLAG1 ........................................................................................................................ 34
6.4.2  ERR_FLAG2 ........................................................................................................................ 35
6.5  CMD .................................................................................................................................... 36
6.6  WHOAMI ............................................................................................................................. 37
6.7  Serial Block .......................................................................................................................... 37
6.7.1  Example of Resolving Serial Number.............................................................................. 38
6.8  SELBANK ............................................................................................................................ 39
7  Application information ............................................................................................................ 39
7.1  Application Circuitry and External Component Characteristics ............................................. 39
7.2  Assembly Instructions .......................................................................................................... 41
8  Traceability ................................................................................................................................ 41
9  Frequently Asked Questions.................................................................................................... 41
10  Order Information ..................................................................................................................... 42
|     |                        |     |              |               |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
|     | www.murata.com         |     |              | Rev. 3        |     |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |         |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- |
|     |     |     |     |     |     |     | 4 (42)  |     |

1  Introduction
This document contains essential technical information about the SCA3300-D01 sensor
including  specifications,  SPI  interface  descriptions,  user  accessible  register  details,
electrical properties and application information. This document should be used as a
reference when designing the SCA3300-D01 component into a system.
2  Specifications
2.1  Abbreviations
|     | ASIC   | Application Specific Integrated Circuit   |     |     |     |     |     |     |
| --- | ------ | ----------------------------------------- | --- | --- | --- | --- | --- | --- |
|     | SPI    | Serial Peripheral Interface               |     |     |     |     |     |     |
|     | RT     | Room Temperature, +23 °C                  |     |     |     |     |     |     |
|     | FS     | Full Scale                                |     |     |     |     |     |     |
|     | CSB    | Chip Select                               |     |     |     |     |     |     |
|     | SCK    | Serial Clock                              |     |     |     |     |     |     |
|     | MOSI   | Master Out Slave In                       |     |     |     |     |     |     |
|     | MISO   | Master In Slave Out                       |     |     |     |     |     |     |
|     | MCU    | Microcontroller                           |     |     |     |     |     |     |
|     | STO    | Self-test Output                          |     |     |     |     |     |     |
|     | EMI    | Electromagnetic Interference              |     |     |     |     |     |     |
|     | ODR    | Output Data Rate                          |     |     |     |     |     |     |
2.2  General Specifications
General specifications for the SCA3300-D01 component are presented in Table 1. All
analog voltages are referenced to the potential at AVSS, and all digital voltages are
referenced to the potential at DVSS.
Table 1 General specifications
|     | Parameter            |     | Condition  |     |     | Min  Nom  | Max  | Units  |
| --- | -------------------- | --- | ---------- | --- | --- | --------- | ---- | ------ |
|     | Supply voltage: VDD  |     |            |     |     | 3.0  3.3  | 3.6  | V      |
SPI supply voltage: DVIO  Must never be higher than VDD  3.0  3.3  3.6  V
Temperature range -40 ... +125 °C
|     | Current consumption: I_VDD  |     |     |     |     |   1.2  |     | mA  |
| --- | --------------------------- | --- | --- | --- | --- | ------ | --- | --- |
Standard operation
Temperature range -40 ... +125 °C
|     | Current consumption: I_VDD in  |     | Power down mode                       |     |     |      |     |     |
| --- | ------------------------------ | --- | ------------------------------------- | --- | --- | ---- | --- | --- |
|     |                                |     |                                       |     |     |   3  | 10  | µA  |
|     | power down mode                |     | Typical value is at room temperature  |     |     |      |     |     |
(+23°C)
|     |                        |     |              |     |     |               |     |     |
| --- | ---------------------- | --- | ------------ | --- | --- | ------------- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |
|     | www.murata.com         |     |              |     |     | Rev. 3        |     |     |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |         |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- |
|     |     |     |     |     |     |     | 5 (42)  |     |

2.3  Performance Specifications for Accelerometer
Table 2 Accelerometer performance specifications. Supply voltage  VDD = 3.3 V and room
temperature (RT) +23 °C unless otherwise specified. Definition of gravitational acceleration:
g = 9.819 m/s2.
|     | Parameter                          |     | Condition             |     | Min    | Nom  | Max    | Unit  |
| --- | ---------------------------------- | --- | --------------------- | --- | ------ | ---- | ------ | ----- |
|     |                                    |     | Measurement axes XYZ  |     |        |      |        |       |
|     |                                    |     | Mode 1                |     | -3     |      | +3     |       |
|     | Measurement range                  |     |                       |     |        |      |        | g     |
|     |                                    |     | Mode 2                |     | -6     |      | +6     |       |
|     |                                    |     | Mode 3, 4             |     | -1.5   |      | +1.5   |       |
|     | Offset (zero acceleration output)  |     |                       |     |        | 0    |        | LSB   |
|     |                                    |     |                       |     | -20    |      | +20    | mg    |
|     | Offset error (A                    |     | -40°C ... +125°C      |     |        |      |        |       |
|     |                                    |     |                       |     | -1.15  |      | +1.15  | °     |
|     |                                    |     | -40°C ... +125°C      |     | -10    |      | +10    | mg    |

|     |     |     | X and Y axes  |     | -0.57  |     | +0.57  | °   |
| --- | --- | --- | ------------- | --- | ------ | --- | ------ | --- |
Offset temperature dependency (B
|     |     |     | -40°C ... +125°C  |     | -15  |     | +15  | mg  |
| --- | --- | --- | ----------------- | --- | ---- | --- | ---- | --- |

|     |              |     | Z axis             |     | -0.86  |       | +0.86  | °      |
| --- | ------------ | --- | ------------------ | --- | ------ | ----- | ------ | ------ |
|     |              |     | ±3g    Mode 1      |     |        | 2700  |        |        |
|     | Sensitivity  |     | ±6g    Mode 2      |     |        | 1350  |        | LSB/g  |
|     |              |     | ±1.5g Modes 3, 4   |     |        | 5400  |        |        |
-40°C ... +125°C
|     | Sensitivity error (A  |     |     |     | -0.7  |     | +0.7  | %   |
| --- | --------------------- | --- | --- | --- | ----- | --- | ----- | --- |
Mode 1
|     | Sensitivity temperature    |     | -40°C ... +125°C                |     |       |       |       |        |
| --- | -------------------------- | --- | ------------------------------- | --- | ----- | ----- | ----- | ------ |
|     |                            |     |                                 |     | -0.3  |       | +0.3  | %      |
|     | dependency (B              |     | Mode 1                          |     |       |       |       |        |
|     |                            |     | -1g ... +1g range, Modes 1 - 4  |     | -1    |       | +1    | mg     |
|     | Linearity error (C         |     |                                 |     |       |       |       |        |
|     |                            |     | -6g ... +6g range, Mode 2       |     | -15   |       | +15   | mg     |
|     |                            |     | Mode 1                          |     |       | 0.5   | 0.7   |        |
|     |                            |     | Mode 2                          |     |       | 0.7   | 1.0   |        |
|     | Integrated noise (RMS) (E  |     |                                 |     |       |       |       | mgRMS  |
|     |                            |     | Mode 3                          |     |       | 0.4   | 0.6   |        |
|     |                            |     | Mode 4                          |     |       | 0.15  | 0.2   |        |
|     |                            |     | Mode 1                          |     |       | 44    | 49    |        |
|     |                            |     | Mode 2                          |     |       | 68    | 76    |        |
|     | Noise density (E           |     |                                 |     |       |       |       | Hz     |
|     |                            |     | Mode 3                          |     |       | 35    | 40    | µg/    |
|     |                            |     | Mode 4                          |     |       | 35    | 40    |        |
|     | Cross axis sensitivity (D  |     | Mode 1, per axis                |     | -1    |       | +1    | %      |
|     |                            |     | Modes 1, 2, 3                   |     |       | 70    |       | Hz     |
Amplitude response,
|     | -3dB frequency            |     | Mode 4         |     |     | 10  |     | Hz  |
| --- | ------------------------- | --- | -------------- | --- | --- | --- | --- | --- |
|     | Power on start-up time(F  |     |                |     |     | 3   |     | ms  |
|     |                           |     | Modes 1, 2, 3  |     |     | 15  |     | ms  |
Output settling time
|     |       |     | Mode 4  |     |     | 100   |     | ms  |
| --- | ----- | --- | ------- | --- | --- | ----- | --- | --- |
|     | ODR   |     |         |     |     | 2000  |     | Hz  |
Min/Max values are ±3 sigma variation limits at the minimum from the original product validation (PV) test population. Min and Max values
are not guaranteed. Nominal values are mean values from validation test population.
A)  Includes calibration error, temperature, supply voltage and drift over lifetime (HTOL +125°C/1000h,
TC -50°C/+150°C 1000cy, UHST 110°C/85%RH 264h, and THB 85°C/85%RH 1000h tests).
B)  Deviation from value at room temperature (RT).
C)  Straight line through specified measurement range end points.
D)  Cross axis sensitivity is the effect of a signal from orthogonal axes to the measured axis.
E)  SPI communication and EMI may affect the noise level. Used SPI clock and EMI conditions should be
carefully validated. Recommended SPI clock is 2 MHz - 4 MHz to achieve the best performance; see
section 2.9.2 SPI AC Characteristics for details.
F)  Power on start-up time does not include output settling time.
|     | Murata Electronics Oy  |     | SCA3300-D01  |     | Doc.No. 3165  |     |     |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | --- | --- | --- |
|     | www.murata.com         |     |              |     | Rev. 3        |     |     |     |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |         |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- |
|     |     |     |     |     |     |     | 6 (42)  |     |

2.4  Performance Specification for Temperature Sensor
Table 3 Temperature sensor performance specifications.
|     | Parameter                 |     | Condition  |     | Min.  | Typ  | Max.  | Unit  |
| --- | ------------------------- | --- | ---------- | --- | ----- | ---- | ----- | ----- |
|     | Temperature signal range  |     |            |     | -50   |      | +150  | °C    |
Temperature signal sensitivity  Direct 16-bit word    18.9    LSB/°C
|     | Temperature signal offset  |     | °C output  |     | -10  |     | 10  | °C  |
| --- | -------------------------- | --- | ---------- | --- | ---- | --- | --- | --- |

Temperature is converted to °C with following equation:

Temperature [°C] = -273 + (TEMP / 18.9),

where TEMP is temperature sensor output register content in decimal format.
2.5  Absolute Maximum Ratings
Within  the  maximum  ratings  (Table  4),  no  damage  to  the  component  shall  occur.
Parametric values may deviate from specification, yet no functional failure shall occur.
Table 4. Absolute maximum ratings.
|     | Symbol  | Description                      |     |     | Min.  | Typ  | Max.  | Unit  |
| --- | ------- | -------------------------------- | --- | --- | ----- | ---- | ----- | ----- |
|     | VDD     | Supply voltage analog circuitry  |     |     | -0.3  |      | 4.3   | V     |
|     | DVIO    | Supply voltage SPI               |     |     | -0.3  |      | 4.3   | V     |
DIN/DOUT  Maximum voltage at digital input and output pins  -0.3    DVIO+0.3  V
|     | Topr     | Operating temperature range                |     |     | -40    |     | +125  | °C  |
| --- | -------- | ------------------------------------------ | --- | --- | ------ | --- | ----- | --- |
|     | Tstg     | Storage temperature range                  |     |     | -40    |     | +150  | °C  |
|     |          | ESD according Human Body Model (HBM)       |     |     |        |     |       |     |
|     | ESD_HBM  |                                            |     |     |        |     |       | V   |
|     |          | Q100-002                                   |     |     | -2000  |     | 2000  |     |
|     |          | ESD according Charged Device Model (CDM)   |     |     |        |     |       |     |
|     | ESD_CDM  |                                            |     |     |        |     |       | V   |
|     |          | Q100-011                                   |     |     | -1000  |     | 1000  |     |
US  Ultrasonic agitation (cleaning, welding, etc.)  Prohibited

|     |                        |     |              |     |               |     |     |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | --- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     | Doc.No. 3165  |     |     |     |
|     | www.murata.com         |     |              |     | Rev. 3        |     |     |     |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |         |     |
| --- | --- | --- | --- | --- | --- | --- | ------- | --- |
|     |     |     |     |     |     |     | 7 (42)  |     |

2.6  AEC-Q100 Testing
The SCA3300-D01 is tested according to AEC-Q100 Grade 1, revision H. Deviations to
the requirements are presented in Table 5.
Table 5. Deviations to AEC-Q100 requirements.
|     | Stress  | ABV  |     | Requirement  |     | Deviation  |     |     |
| --- | ------- | ---- | --- | ------------ | --- | ---------- | --- | --- |
Drop part on each of 6 axes once
10 Drops, random orientation, drop
|     | Package Drop  | DROP  | from a height of 1.2m onto a concrete  |     |     |     |     |     |
| --- | ------------- | ----- | -------------------------------------- | --- | --- | --- | --- | --- |
height 0.8m1
surface.

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

1 Shocks may cause mechanical damage to the internal structures of MEMS sensor, causing malfunction of
sensor, therefore mechanical shocks should be avoided. The level depends heavily on the pulse width and
shape and should be evaluated case by case. As a general guideline, the lighter assembly or part, the higher
shock levels will be generated on sensor component. Dropped components shall not be used and shall be
scrapped.
|     | Murata Electronics Oy  |     |     | SCA3300-D01  | Doc.No. 3165  |     |     |     |
| --- | ---------------------- | --- | --- | ------------ | ------------- | --- | --- | --- |
|     | www.murata.com         |     |     |              | Rev. 3        |     |     |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |         |
| --- | --- | --- | --- | --- | ------- |
|     |     |     |     |     | 8 (42)  |

2.7  Pin Description
The pinout for SCA3300-D01 is presented in Figure 1.

Figure 1 Pinout for SCA3300-D01.
Table 6 SCA3300-D01 pin descriptions.
|     | Pin#  Name  | Type  | Description  |     |     |
| --- | ----------- | ----- | ------------ | --- | --- |
1  AVSS  GND  Analog Reference Ground, connect externally to GND
|     | 2  A_EXTC    | AOUT    | External capacitor connection for analog core  |     |     |
| --- | ------------ | ------- | ---------------------------------------------- | --- | --- |
|     | 3  RESERVED  | -       | Factory use only, connect externally to GND    |     |     |
|     | 4  VDD       | SUPPLY  | Analog Supply Voltage                          |     |     |
Chip Select of SPI Interface, 3.3V logic compatible Schmitt-trigger
|     | 5  CSB  | DIN  |     |     |     |
| --- | ------- | ---- | --- | --- | --- |
input
|     | 6  MISO  | DOUT  | Data Out of SPI Interface  |     |     |
| --- | -------- | ----- | -------------------------- | --- | --- |
7  MOSI  DIN  Data In of SPI Interface, 3.3V logic compatible Schmitt-trigger input
|     | 8  SCK      | DIN     | Clock Signal of SPI                              |     |     |
| --- | ----------- | ------- | ------------------------------------------------ | --- | --- |
|     | 9  DVIO     | SUPPLY  | SPI Supply Voltage                               |     |     |
|     | 10  D_EXTC  | AOUT    | External capacitor connection for digital core   |     |     |
Digital Reference Ground, connect externally to GND. Must never be
|     | 11  DVSS  | GND  |     |     |     |
| --- | --------- | ---- | --- | --- | --- |
left floating when component is powered.
|     | 12  EMC_GND            | EMC GND  | EMC Ground pin, connect externally to GND  |               |     |
| --- | ---------------------- | -------- | ------------------------------------------ | ------------- | --- |
|     |                        |          |                                            |               |     |
|     | Murata Electronics Oy  |          | SCA3300-D01                                | Doc.No. 3165  |     |
|     | www.murata.com         |          |                                            | Rev. 3        |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |         |
| --- | --- | --- | --- | --- | ------- |
|     |     |     |     |     | 9 (42)  |

2.8  Typical performance characteristics

Figure 2 Accelerometer typical offset temperature behavior.

|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | www.murata.com         |     |              | Rev. 3        |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |
| --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     | 10 (42)  |

Figure 3 Example of accelerometer long term stability during 1000h HTOL. HTOL test conditions:
temperature = +125 °C, Vsupply=3.6 V. Example data measurement condition = +25 °C.
|     |                        |     |              |               |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
|     | www.murata.com         |     |              | Rev. 3        |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |
| --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     | 11 (42)  |

Figure 4 Accelerometer typical sensitivity temperature error in %

Figure  5  Left:  Vibration  rectification  error;  Sine  sweep  500...5 KHz  with  4 g  amplitude  and
5 kHz...25 kHz with 2 g amplitude. Right: Accelerometer typical linearity behavior.

|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | www.murata.com         |     |              | Rev. 3        |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |
| --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     | 12 (42)  |

Figure 6 Left: Accelerometer typical noise density. Right: Typical Allan deviation.
|     |                        |     |              |               |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
|     | www.murata.com         |     |              | Rev. 3        |     |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     | 13 (42)  |     |

2.9  Digital I/O Specification
2.9.1  DC Characteristics
Table 7 describes the DC characteristics of SCA3300-D01 sensor SPI I/O pins. Supply
voltage is 3.3 V unless otherwise specified. Current flowing into the circuit has a positive
value.
Table 7 SPI DC Characteristics
|     | Symbol  | Remark  |     |     | Min.  | Typ  | Max.  | Unit  |
| --- | ------- | ------- | --- | --- | ----- | ---- | ----- | ----- |

Serial Clock SCK (Pull Down)
IPD  Pull-down current  Vin = 3.0 - 3.6 V  7.5  16.5  36  uA
|     | VIH  | Input voltage '1'  |     |     | 0.67*DVIO  |      | DVIO       | V   |
| --- | ---- | ------------------ | --- | --- | ---------- | ---- | ---------- | --- |
|     | VIL  | Input voltage '0'  |     |     |            | 0    | 0.33*DVIO  | V   |

Chip Select CSB (Pull Up), low active
|     | IPU  | Pull-up current    | Vin = 0  |     |            | 7.5  16.5  | 36         | uA  |
| --- | ---- | ------------------ | -------- | --- | ---------- | ---------- | ---------- | --- |
|     | VIH  | Input voltage '1'  |          |     | 0.67*DVIO  |            | DVIO       | V   |
|     | VIL  | Input voltage '0'  |          |     |            | 0          | 0.33*DVIO  | V   |

Serial Data Input MOSI (Pull Down)
IPD  Pull-down current  Vin = 3.0 - 3.6 V  7.5  16.5  36  uA
|     | VIH  | Input voltage '1'  |     |     | 0.67*DVIO  |      | DVIO       | V   |
| --- | ---- | ------------------ | --- | --- | ---------- | ---- | ---------- | --- |
|     | VIL  | Input voltage '0'  |     |     |            | 0    | 0.33*DVIO  | V   |

Serial Data Output MISO (Tri State)
|     | VOH                    | Output high voltage      | I > -1 mA           |     | DVIO-0.5V  |               |      | V   |
| --- | ---------------------- | ------------------------ | ------------------- | --- | ---------- | ------------- | ---- | --- |
|     | VOL                    | Output low voltage       | I < 1 mA            |     |            |               | 0.5  | V   |
|     | ILEAK                  | Tri-state leakage        | 0 <  VMISO < 3.3 V  |     |            | -1  0         | 1    | uA  |
|     |                        | Maximum Capacitive load  |                     |     |            |               | 50   | pF  |
|     |                        |                          |                     |     |            |               |      |     |
|     | Murata Electronics Oy  |                          | SCA3300-D01         |     |            | Doc.No. 3165  |      |     |
|     | www.murata.com         |                          |                     |     |            | Rev. 3        |      |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     | 14 (42)  |     |

2.9.2  SPI AC Characteristics
The AC characteristics of SCA3300-D01 are defined in Figure 7 and Table 8.

Figure 7 Timing diagram of SPI communication.
Table 8 SPI AC electrical characteristics.
|     | Symbol         | Description                       |     | Min.  Typ  | Max.  | Unit  |
| --- | -------------- | --------------------------------- | --- | ---------- | ----- | ----- |
|     | TLS1           | Time from CSB (10%) to SCK (90%)  |     | 63         |       | ns    |
|     | TLS2           | Time from SCK (10%) to CSB (90%)  |     | 63         |       | ns    |
|     | TCL            | SCK low time                      |     | 25         |       | ns    |
|     | TCH            | SCK high time                     |     | 25         |       | ns    |
|     | fSCK = 1/Tper  | SCK Frequency *                   |     | 0.1  2     | 8     | MHz   |
Time from changing MOSI (10%, 90%) to SCK
|     | TSET  |     |     | 32    |     | ns  |
| --- | ----- | --- | --- | ----- | --- | --- |
(90%). Data setup time
Time from SCK (90%) to changing MOSI (10%,
|     | THOL  |     |     | 32    |     | ns  |
| --- | ----- | --- | --- | ----- | --- | --- |
90%). Data hold time
TVAL1  Time from CSB (10%) to stable MISO (10%, 90%)  4  10  16  ns
Time from CSB (90%) to high impedance state of
|     | TLZ  |     |     |   10  |     | ns  |
| --- | ---- | --- | --- | ----- | --- | --- |
MISO
TVAL2  Time from SCK (10%) to stable MISO (10%, 90%)  4  10  16  ns
TLH  Time between SPI cycles, CSB at high level (90%)  10      us
* SPI communication may affect the noise level. Used SPI clock should be carefully validated. Recommended SPI clock is
2 MHz - 4 MHz to achieve the best performance.
|     |                        |     |              |               |     |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |     |
|     | www.murata.com         |     |              | Rev. 3        |     |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     | 15 (42)  |

2.10  Measurement Axis and Directions

Figure 8 SCA3300-D01 measurement directions.
Table 9 SCA3300-D01 accelerometer measurement directions.

|     |     | x: +1g  | x:  0g  |     | x:  0g  |     |
| --- | --- | ------- | ------- | --- | ------- | --- |
|     |     | y:  0g  | y: +1g  |     | y:  0g  |     |
|     |     | z:  0g  | z:  0g  |     | z: +1g  |     |

|     |                        | x: -1g  | x:  0g       |               | x:  0g  |     |
| --- | ---------------------- | ------- | ------------ | ------------- | ------- | --- |
|     |                        | y:  0g  | y: -1g       |               | y:  0g  |     |
|     |                        | z:  0g  | z:  0g       |               | z: -1g  |     |
|     |                        |         |              |               |         |     |
|     | Murata Electronics Oy  |         | SCA3300-D01  | Doc.No. 3165  |         |     |
|     | www.murata.com         |         |              | Rev. 3        |         |     |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     |     |     | 16 (42)  |

2.11  Package Characteristics
2.11.1 Package Outline Drawing

Figure 9 Package outline. The tolerances are according to ISO2768-f (see Table 10).
Table 10 Limits for linear measures (ISO2768-f).
Limits in mm for nominal size in mm
Tolerance class
|     |                        |     | 0.5 to 3     |     | Above 3 to 6  |               | Above 6 to 30  |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | ------------- | -------------- | --- |
|     | f (fine)               |     | ±0.05        |     | ±0.05         |               | ±0.1           |     |
|     |                        |     |              |     |               |               |                |     |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     |               | Doc.No. 3165  |                |     |
|     | www.murata.com         |     |              |     |               | Rev. 3        |                |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |
| --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     | 17 (42)  |

2.12  PCB Footprint

Figure 10 Recommended PWB pad layout for SCA3300-D01. All dimensions are in mm. The
tolerances are according to ISO2768-f (see Table 10).
3  General Product Description
The  SCA3300-D01  sensor  includes  acceleration  sensing  element  and  Application-
Specific Integrated Circuit (ASIC). Figure 11 contains an upper level block diagram of the
component.

Figure 11. SCA3300-D01 component block diagram.
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | www.murata.com         |     |              | Rev. 3        |     |

18 (42)
The sensing elements are manufactured using Murata proprietary High Aspect Ratio
(HAR) 3D-MEMS process, which enables making robust, extremely stable and low noise
capacitive sensors.
The acceleration sensing element consists of four acceleration sensitive masses.
Acceleration causes capacitance change that is converted into a voltage change in the
signal conditioning ASIC.
3.1 Factory Calibration
SCA3300-D01 sensors are factory calibrated. No separate calibration is required in the
application. Calibration parameters are stored in non-volatile memory during
manufacturing. The parameters are read automatically from the internal non-volatile
memory during start-up.
Assembly can cause offset/bias errors to the sensor output. If best possible accuracy is
required, system level offset/bias calibration (zeroing) after assembly is recommended.
Offset calibration is recommended to be performed not earlier than 12 hours after reflow.
It should be noted that accuracy can be improved with longer stabilization time.
4 Component Operation, Reset and Power Up
4.1 Component Operation
The sensor ODR in normal operation mode is 2000 Hz. Registers are updated every
0.5 ms.
In order to achieve optimal performance, it is recommended that during normal operation
acceleration outputs ACCX, ACCY, ACCZ are read in every cycle using sensor ODR. It is
necessary to read STATUS register only if return status (RS) indicates error.
Murata Electronics Oy SCA3300-D01 Doc.No. 3165
www.murata.com Rev. 3

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |
| --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     | 19 (42)  |

4.2  Start-up sequence
Table 11 Start-Up Sequence.
|     | Step  Procedure  | RS*  | Function  | Note                          |     |
| --- | ---------------- | ---- | --------- | ----------------------------- | --- |
|     | Set              |      |           | Procedure for normal startup  |     |

VDD and DVIO don't need to rise at the
same time, but DVIO must never be
|     | 1                    | - -  | Startup the device  |                   |     |
| --- | -------------------- | ---- | ------------------- | ----------------- | --- |
|     | VDD  3.0 - 3.6 V     |      |                     | higher than VDD.  |     |
|     | DVIO    3.0 - 3.6 V  |      |                     |                   |     |
Supply voltages must be settled until
proceeding to the next step.
OR
Procedure if device is in power down
|     | Write Wake up from  |      |     | mode                               |     |
| --- | ------------------- | ---- | --- | ---------------------------------- | --- |
|     | 1  power down mode  | - -  |     |                                    |     |
|     | command             |      |     | See Table 15 Operations and their  |     |
equivalent SPI frames
Memory reading
|     | 1.2  Wait 3 ms  | - -  |     | Minimum wait time  |     |
| --- | --------------- | ---- | --- | ------------------ | --- |
Settling of signal path
Always continue from here
|     | Write SW Reset  |     |                            | See Table 15 Operations and their  |     |
| --- | --------------- | --- | -------------------------- | ---------------------------------- | --- |
|     | 2               | --  | Software reset the device  |                                    |     |
|     | command         |     |                            | equivalent SPI frames.             |     |
Memory reading
|     | 3  Wait 3 ms  | - -  |     | Minimum wait time  |     |
| --- | ------------- | ---- | --- | ------------------ | --- |
Settling of signal path
3g full-scale
Mode1
70 Hz measurement
(default)
bandwidth
6g full-scale
Mode2  70 Hz measurement
bandwidth
Set Measurement
|     | 4   | ‘11’  | Select operation mode  |     |     |
| --- | --- | ----- | ---------------------- | --- | --- |
mode**
1.5g full-scale
Mode3  70 Hz measurement
bandwidth
1.5g full-scale
Mode4  10 Hz measurement
bandwidth
|     | Wait 15 ms  | - -  | Settling of signal path  | Modes 1, 2, and 3  |     |
| --- | ----------- | ---- | ------------------------ | ------------------ | --- |
5
|     | OR Wait 100ms  | --  | Settling of signal path  | Mode 4  |     |
| --- | -------------- | --- | ------------------------ | ------- | --- |
6  Read STATUS   ‘11’  Clear status summary  Reset status summary
SPI response to step 6.

7  Read STATUS   ‘11’  Read status summary  Read status summary.  Due to SPI off-
frame protocol response is before
STATUS has been cleared.
SPI response to step 7.

|     | Read STATUS  |     |     | First response where STATUS has been  |     |
| --- | ------------ | --- | --- | ------------------------------------- | --- |
8  (or any other valid  ‘01’  Ensure successful start-up  cleared. RS bits should be ‘01’ to indicate
|     | SPI command)  |     |     | proper start-up. Otherwise, start-up has  |     |
| --- | ------------- | --- | --- | ----------------------------------------- | --- |
not been done correctly. See 6.3
STATUS for more information.
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | www.murata.com         |     |              | Rev. 3        |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     | 20 (42)  |

* RS bits in returned SPI response during normal start-up. See 5.1.5 Return Status for
more information.
** if not set, mode1 is used.
4.3  Operation modes
SCA3300-D01 provides four user selectable operation modes. Default operation mode is
mode 1: ± 3 g full-scale with 70 Hz 1st order low pass filter. After power-off, reset (SW or
HW), power down mode or unintentional power-off, operation mode will be set to mode1.
Current operation mode can be read with “read CMD” SPI command, see sections 5.1.4
Operations and 6.5 CMD.
Table 12 Operation mode description
Mode  Full-scale  Sensitivity LSB/g  1st order low pass filter
|     | 1   | ± 3 g    | 2700   |     | 70 Hz  |     |
| --- | --- | -------- | ------ | --- | ------ | --- |
|     | 2   | ± 6 g    | 1350   |     | 70 Hz  |     |
|     | 3   | ± 1.5 g  | 5400   |     | 70 Hz  |     |
|     | 4   | ± 1.5 g  | 5400   |     | 10 Hz  |     |

|     |                        |     |              |     |               |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     | Doc.No. 3165  |     |
|     | www.murata.com         |     |              |     | Rev. 3        |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     | 21 (42)  |

5  Component Interfacing
5.1.1  General
SPI communication transfers data between the SPI master and registers of the SCA3300-
D01  ASIC.  The  SCA3300-D01  always  operates  as  a  slave  device  in  master-slave
operation mode. 3-wire SPI connection is not supported.
Table 13 SPI interface pins
|     | Pin  | Pin Name                  |     | Communication  |     |          |
| --- | ---- | ------------------------- | --- | -------------- | --- | -------- |
|     | CSB  | Chip Select (active low)  |     | MCU            |     | SCA3300  |
→
|     | SCK   | Serial Clock         |     | MCU      | →   | SCA3300  |
| --- | ----- | -------------------- | --- | -------- | --- | -------- |
|     | MOSI  | Master Out Slave In  |     | MCU      | →   | SCA3300  |
|     | MISO  | Master In Slave Out  |     | SCA3300  | →   | MCU      |
5.1.2  Protocol
The SPI is a 32-bit 4-wire slave configured bus. Off-frame protocol is used so each transfer
consists of two phases. A response to the request is sent within next request frame. The
response  concurrent  to  the  request  contains  the  data  requested  by  the  previous
command. The first bit in a sequence is the MSB.
SPI transmission is always started with the falling edge of chip select, CSB. The data bits
are sampled at the rising edge of the SCK signal. The data is captured on the rising edge
(MOSI line) of the SCK and it is propagated on the falling edge (MISO line) of the SCK.
This equals to SPI Mode 0 (CPOL = 0 and CPHA = 0).

NOTE: For sensor operation, time between consecutive SPI requests (i.e. CSB high)
must be at least 10 µs. If less than 10 µs is used, output data will be corrupted.
CSB
SCK
MOSI
|     |     | Request 1 | Request 2 | Request 3 |     |     |
| --- | --- | --------- | --------- | --------- | --- | --- |
MISO
|     |     | * Undefined | Response 1 | Response 2 |     |     |
| --- | --- | ----------- | ---------- | ---------- | --- | --- |
* The first response after reset is
undefined and shall be discarded
Figure 12 SPI Protocol
|     |                        |     |              |               |     |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |     |
|     | www.murata.com         |     |              | Rev. 3        |     |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |
| --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     | 22 (42)  |

5.1.3  SPI frame
The SPI Frame is divided into four parts:
1.  Operation Code (OP), consisting of Read/Write (RW) and Address (ADDR)
2.  Return Status (RS, in MISO)
3.  Data (D)
4.  Checksum (CRC)

See Figure 13 and Table 14 Table 14 SPI Frame Specification for more details. For
allowed SPI operating commands see Table 15.

Figure 13 SPI Frame
|     |                        |     |              |               |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
|     | www.murata.com         |     |              | Rev. 3        |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     | 23 (42)  |

Table 14 SPI Frame Specification
|     | Name  | Bits  Description  |     | MISO / MOSI                 |                       |       |
| --- | ----- | ------------------ | --- | --------------------------- | --------------------- | ----- |
|     |       | Operation code     |     | OP   [5] =   RW             | Read = 0 / Write = 1  |       |
|     | OP    | [31:26]            |     |                             |                       |       |
|     |       | RW + ADDR          |     | OP [4:0] = ADDR             | Register address      |       |
|     |       |                    |     | MISO                        |                       | MOSI  |
|     |       |                    |     | '00' - Startup in progress  |                       |       |
RS  [25:24] Return status  '01' - Normal operation, no flags  ‘00’ – Always
|     |      |                  |     | '10' - (Not in use)            |     |     |
| --- | ---- | ---------------- | --- | ------------------------------ | --- | --- |
|     |      |                  |     | '11' - Error                   |     |     |
|     | D    | [23:8]  Data     |     | Returned data / data to write  |     |     |
|     | CRC  | [7:0]  Checksum  |     | See section 5.2                |     |     |

Return Status (RS) shows error (i.e. '11') when an error flag (or flags) is active in, or if
previous MOSI-command had incorrect CRC.
|     |                        |     |              |     |               |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     | Doc.No. 3165  |     |
|     | www.murata.com         |     |              |     | Rev. 3        |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     | 24 (42)  |     |

5.1.4  Operations
Allowed operation commands are shown in Table 15. No other commands are allowed.
Table 15 Operations and their equivalent SPI frames
|     | Operation  | Bank  | SPI Frame  |     | SPI Frame Hex  |     |
| --- | ---------- | ----- | ---------- | --- | -------------- | --- |
Read ACC_X  0 1  0000 0100 0000 0000 0000 0000 1111 0111  040000F7h
Read ACC_Y  0 1  0000 1000 0000 0000 0000 0000 1111 1101  080000FDh
Read ACC_Z  0 1  0000 1100 0000 0000 0000 0000 1111 1011  0C0000FBh
Read STO (self-test output)  0 1  0001 0000 0000 0000 0000 0000 1110 1001  100000E9h
Read Temperature  0 1  0001 0100 0000 0000 0000 0000 1110 1111  140000EFh
Read Status Summary  0 1  0001 1000 0000 0000 0000 0000 1110 0101  180000E5h
Read ERR_FLAG1  0  0001 1100 0000 0000 0000 0000 1110 0011  1C0000E3
Read ERR_FLAG2  0  0010 0000 0000 0000 0000 0000 1100 0001  200000C1h
Read CMD  0  0011 0100 0000 0000 0000 0000 1101 1111  340000DFh
Change to mode1  0  1011 0100 0000 0000 0000 0000 0001 1111  B400001Fh
Change to mode2  0  1011 0100 0000 0000 0000 0001 0000 0010  B4000102h
Change to mode3  0  1011 0100 0000 0000 0000 0010 0010 0101  B4000225h
Change to mode4  0  1011 0100 0000 0000 0000 0011 0011 1000  B4000338h
Set power down mode  0  1011 0100 0000 0000 0000 0100 0110 1011  B400046Bh
Wake up from power down
|     |     | 0   | 1011 0100 0000 0000 0000 0000 0001 1111  |     | B400001Fh  |     |
| --- | --- | --- | ---------------------------------------- | --- | ---------- | --- |
mode
SW Reset  0  1011 0100 0000 0000 0010 0000 1001 1000  B4002098h
Read WHOAMI  0  0100 0000 0000 0000 0000 0000 1001 0001  40000091h
Read SERIAL1  1  0110 0100 0000 0000 0000 0000 1010 0111  640000A7h
Read SERIAL2  1  0110 1000 0000 0000 0000 0000 1010 1101  680000ADh
Read current bank  0 1  0111 1100 0000 0000 0000 0000 1011 0011  7C0000B3h
Switch to bank #0  0 1  1111 1100 0000 0000 0000 0000 0111 0011  FC000073h
Switch to bank #1  0 1  1111 1100 0000 0000 0000 0001 0110 1110  FC00016Eh
|     |                        |     |              |               |     |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |     |
|     | www.murata.com         |     |              | Rev. 3        |     |     |

|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |
| --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     | 25 (42)  |

5.1.5  Return Status
SPI frame Return Status bits (RS bits) indicate the functional status of the sensor. See
Table 16 for RS definitions.
Table 16 Return Status definitions
|     | RS [1]  | RS [0]  Description            |     |     |     |
| --- | ------- | ------------------------------ | --- | --- | --- |
|     | 0       | 0  Startup in progress         |     |     |     |
|     | 0       | 1  Normal operation, no flags  |     |     |     |
|     | 1       | 0  Reserved                    |     |     |     |
|     | 1       | 1  Error                       |     |     |     |
The priority of the return status states is from high to low: 00 → 11 → 01
Return Status (RS) shows error (i.e. '11') when an error flag (or flags) is active in Status Summary
register, or if previous MOSI-command had incorrect frame CRC. If the Status Summary register
is read immediately after a shock event, the RS bits may indicate an error (RS = '11'), even though
the STATUS register data content is '0000'. In the subsequent frame, if the STATUS register data
content remains '0000', this indicates that the cause was a CRC error. In the case of a saturation
error, the data content will indicate that. For example, STATUS = '0040'.
See 6.3 STATUS for more information.
5.2  Checksum (CRC)
For SPI transmission error detection a Cyclic Redundancy Check (CRC) is implemented,
for details see Table 17.
Table 17 SPI CRC definition
|     | Parameter  Value                              |     |     |     |     |
| --- | --------------------------------------------- | --- | --- | --- | --- |
|     | Name  CRC-8                                   |     |     |     |     |
|     | Width  8 bit                                  |     |     |     |     |
|     | Poly  1Dh (generator polynom: X8+X4+X3+X2+1)  |     |     |     |     |
|     | Init  FFh (initialization value)              |     |     |     |     |
|     | XOR out  FFh (inversion of CRC result)        |     |     |     |     |

The CRC value used in system level software has to be initialized with FFh to ensure a
CRC failure in case of stuck-at-0 and stuck-at-1 error on the SPI bus. C-programming
language example for CRC calculation is presented in Figure 14. It can be used as is in
an appropriate programming context.
|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- |
|     | www.murata.com         |     |              | Rev. 3        |     |

26 (42)
// Calculate CRC for 24 MSB's of the 32 bit dword
// (8 LSB's are the CRC field and are not included in CRC calculation)
uint8_t CalculateCRC(uint32_t Data)
{
uint8_t BitIndex;
uint8_t BitValue;
uint8_t CRC;
CRC = 0xFF;
for (BitIndex = 31; BitIndex > 7; BitIndex--)
{
BitValue = (uint8_t)((Data >> BitIndex) & 0x01);
CRC = CRC8(BitValue, CRC);
}
CRC = (uint8_t)~CRC;
return CRC;
}
static uint8_t CRC8(uint8_t BitValue, uint8_t CRC)
{
uint8_t Temp;
Temp = (uint8_t)(CRC & 0x80);
if (BitValue == 0x01)
{
Temp ^= 0x80;
}
CRC <<= 1;
if (Temp > 0)
{
CRC ^= 0x1D;
}
return CRC;
}
Figure 14 C-programming language example for CRC calculation
In case of wrong CRC in MOSI write/read, RS bits “11” are set in the next SPI response,
STATUS register is not changed, and write command is discarded. If CRC in MISO SPI
response is incorrect, communication failure occurred.
CRC calculation example:
Read ACC_X register (04h)
SPI [31:8] = 040000h → CRC = F7h
SPI [7:0] = F7h
SPI frame = 040000F7h
6 Register Definition
SCA3300-D01 contains two user switchable register banks. Default register bank is #0.
One should have register bank #0 always active, unless data from bank #1 is required.
After reading data from bank #1 is finished, one should switch back to bank #0 to ensure
no accidental read / writes in unwanted registers. See 6.8 SELBANK for more information
for selecting active register bank. Table 18 shows overview of register banks and register
addresses.
Murata Electronics Oy SCA3300-D01 Doc.No. 3165
www.murata.com Rev. 3

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     | 27 (42)  |     |

Table 18 Register address space overview
|     | Addr  |     | Register Bank  |     |     |     |     |     |
| --- | ----- | --- | -------------- | --- | --- | --- | --- | --- |
Read/
Description
|     | (hex)  | Write  | #0  | #1  |     |     |     |     |
| --- | ------ | ------ | --- | --- | --- | --- | --- | --- |
01h
R  ACC_X  ACC_X  X-axis acceleration output in 2’s complement format
02h  R  ACC_Y  ACC_Y  Y-axis acceleration output in 2’s complement format
03h  R  ACC_Z  ACC_Z  Z-axis acceleration output in 2’s complement format
04h
|     |     | R   | STO   | STO  | Self-test output in 2’s complement format  |     |     |     |
| --- | --- | --- | ----- | ---- | ------------------------------------------ | --- | --- | --- |
05h  R  TEMPERATURE  TEMPERATURE  Temperature sensor output in 2’s complement format
06h  R  STATUS  STATUS  Status Summary combining ERR_FLAG1 and ERR_FLAG2
|     | 07h  | R   | ERR_FLAG1  | reserved  | Error flags group1  |     |     |     |
| --- | ---- | --- | ---------- | --------- | ------------------- | --- | --- | --- |
|     | 08h  | R   | ERR_FLAG2  | reserved  | Error flags group2  |     |     |     |
|     | 09h  | -   | reserved   | reserved  | -                   |     |     |     |
|     | 0Ah  | -   | reserved   | reserved  | -                   |     |     |     |
|     | 0Bh  | -   | reserved   | reserved  | -                   |     |     |     |
|     | 0Ch  | -   | reserved   | reserved  | -                   |     |     |     |
0Dh  R / W  MODE  reserved  Sets operation mode, SW Reset and Power down mode
|     | 0Eh  | -   | reserved  | reserved  | -   |     |     |     |
| --- | ---- | --- | --------- | --------- | --- | --- | --- | --- |
|     | 0Fh  | -   | reserved  | reserved  | -   |     |     |     |
10h  R  WHOAMI  reserved  8-bit register for component identification
|     | 11h  | -   | reserved  | reserved  | -   |     |     |     |
| --- | ---- | --- | --------- | --------- | --- | --- | --- | --- |
|     | 12h  | -   | reserved  | reserved  | -   |     |     |     |
|     | 13h  | -   | reserved  | reserved  | -   |     |     |     |
14h
|     |      | -   | reserved  | reserved  | -   |     |     |     |
| --- | ---- | --- | --------- | --------- | --- | --- | --- | --- |
|     | 15h  | -   | reserved  | reserved  | -   |     |     |     |
|     | 16h  | -   | reserved  | reserved  | -   |     |     |     |
17h
|     |      | -   | reserved  | reserved  | -                        |     |     |     |
| --- | ---- | --- | --------- | --------- | ------------------------ | --- | --- | --- |
|     | 18h  | -   | reserved  | reserved  | -                        |     |     |     |
|     | 19h  | R   | reserved  | SERIAL1   | Component serial part 1  |     |     |     |
1Ah
|     |      | R   | reserved  | SERIAL2      | Component serial part 2  |     |     |     |
| --- | ---- | --- | --------- | ------------ | ------------------------ | --- | --- | --- |
|     | 1Bh  | -   | reserved  | Factory Use  | -                        |     |     |     |
|     | 1Ch  | -   | reserved  | Factory Use  | -                        |     |     |     |
|     | 1Dh  |     |           |              | -                        |     |     |     |
|     |      | -   | reserved  | Factory Use  |                          |     |     |     |
|     | 1Eh  | -   | reserved  | reserved     | -                        |     |     |     |
1Fh  R / W  SELBANK  SELBANK  Switch between active register banks

User should not access Reserved nor Factory Use registers. Power-cycle, reset and
power down mode will reset all written settings.
|     | Murata Electronics Oy  |     |     | SCA3300-D01  |     | Doc.No. 3165  |     |     |
| --- | ---------------------- | --- | --- | ------------ | --- | ------------- | --- | --- |
|     | www.murata.com         |     |     |              |     | Rev. 3        |     |     |

|     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     |     | 28 (42)  |     |

6.1  Sensor Data Block
Table 19 Sensor data block description
|     |             |       |     | No. of  | Read /       |     |     |     |     |     |
| --- | ----------- | ----- | --- | ------- | ------------ | --- | --- | --- | --- | --- |
|     | Bank  Addr  | Name  |     |         | Description  |     |     |     |     |     |
|     |             |       |     | bits    | Write        |     |     |     |     |     |
0 1  01h
ACC_X  16  R  X-axis acceleration output in 2’s complement format
0 1  02h  ACC_Y  16  R  Y-axis acceleration output in 2’s complement format
0 1  03h  ACC_Z  16  R  Z-axis acceleration output in 2’s complement format
Temperature sensor output in 2’s complement format.
|     | 0 1  05h  | TEMPERATURE  |     | 16  | R   |     |     |     |     |     |
| --- | --------- | ------------ | --- | --- | --- | --- | --- | --- | --- | --- |
See section 2.4 for conversion equation.
Table 20 Sensor data block operations
|     | Operation  |     |     | SPI Frame  |     |     |     | SPI Frame Hex  |     |     |
| --- | ---------- | --- | --- | ---------- | --- | --- | --- | -------------- | --- | --- |
Read ACC_X  0000 0100 0000 0000 0000 0000 1111 0111  040000F7h
Read ACC_Y  0000 1000 0000 0000 0000 0000 1111 1101  080000FDh
Read ACC_Z  0000 1100 0000 0000 0000 0000 1111 1011  0C0000FBh
Read Temperature  0001 0100 0000 0000 0000 0000 1110 1111  140000EFh
6.1.1  Example of Acceleration Data Conversion
For example, if ACC_X register read results: ACC_X = 0500DC1Ch, the register content
is converted to acceleration rate as follows:

OP[31:26]
|     |     | +   |     | Data[23:8]  |     | CRC[7:0]  |     |     |     |     |
| --- | --- | --- | --- | ----------- | --- | --------- | --- | --- | --- | --- |
RS[25:24]
|     |     | 0  5  | 0   | 0   | D  C  | 1   | C   |     |     |     |
| --- | --- | ----- | --- | --- | ----- | --- | --- | --- | --- | --- |

OP + RS
05h = 0000 0101b
|     |     | 0000 01b    |     |     | = OP code = Read ACC_X                |     |     |     |     |     |
| --- | --- | ----------- | --- | --- | ------------------------------------- | --- | --- | --- | --- | --- |
|     |     | 01b         |     |     | = return status (RS bits) = no error  |     |     |     |     |     |

Data = ACC_X register content
   00DCh
|     |     | 00DCh → 220d  |     |     | = in 2's complement format  |     |     |     |     |     |
| --- | --- | ------------- | --- | --- | --------------------------- | --- | --- | --- | --- | --- |
Acceleration:
= 220 LSB / sensitivity(mode1)
= 220 LSB / 2700 LSB/g
= 0.081 g

|     | CRC                    |                                  |     |              |     |     |               |     |     |     |
| --- | ---------------------- | -------------------------------- | --- | ------------ | --- | --- | ------------- | --- | --- | --- |
|     |       1Ch              |                                  |     |              |     |     |               |     |     |     |
|     |                        | CRC of 0500DCh, see section 5.2  |     |              |     |     |               |     |     |     |
|     |                        |                                  |     |              |     |     |               |     |     |     |
|     | Murata Electronics Oy  |                                  |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |     |
|     | www.murata.com         |                                  |     |              |     |     | Rev. 3        |     |     |     |

|     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     |     | 29 (42)  |     |

6.1.2  Example of Temperature Data Conversion
For example, if TEMPERATURE register read results: TEMPERATURE = 15161E0Ah,
the register content is converted to temperature as follows:

OP[31:26]
|     |     | +   |     | Data[23:8]  |     | CRC[7:0]  |     |     |     |     |
| --- | --- | --- | --- | ----------- | --- | --------- | --- | --- | --- | --- |
RS[25:24]
|     |     | 1  5  | 1   | 6   | 1  E  | 0   | A   |     |     |     |
| --- | --- | ----- | --- | --- | ----- | --- | --- | --- | --- | --- |

OP + RS
15h = 0001 0101b
|     |     | 0001 01b    |     |     | = OP code = Read TEMP                 |     |     |     |     |     |
| --- | --- | ----------- | --- | --- | ------------------------------------- | --- | --- | --- | --- | --- |
|     |     | 01b         |     |     | = return status (RS bits) = no error  |     |     |     |     |     |

Data = TEMPERATURE register content
   161Eh
|     |     | 161Eh → 5662d  |     |     | = in 2's complement format  |     |     |     |     |     |
| --- | --- | -------------- | --- | --- | --------------------------- | --- | --- | --- | --- | --- |
Temperature:
= -273 + (5662 / 18.9)
= +26.6°C

|     | CRC        |                                  |     |     |     |     |     |     |     |     |
| --- | ---------- | -------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |       0Ah  |                                  |     |     |     |     |     |     |     |     |
|     |            | CRC of 15161Eh, see section 5.2  |     |     |     |     |     |     |     |     |
6.2  STO
Table 21 STO (self-test output) description
|     |             |       |     | No. of  Read /  |              |     |     |     |     |     |
| --- | ----------- | ----- | --- | --------------- | ------------ | --- | --- | --- | --- | --- |
|     | Bank  Addr  | Name  |     |                 | Description  |     |     |     |     |     |
|     |             |       |     | bits            | Write        |     |     |     |     |     |
0 1  04h  STO  16  R  Self-test output in 2’s complement format
Table 22 STO operation
|     | Operation  |     |     | SPI Frame  |     |     |     | SPI Frame Hex  |     |     |
| --- | ---------- | --- | --- | ---------- | --- | --- | --- | -------------- | --- | --- |
Read STO (self-test output)  0001 0000 0000 0000 0000 0000 1110 1001  100000E9h

If self-test option is desired in application, following guidelines should be taken into
account. STO is used to monitor if accelerometer is functioning correctly. It provides
information on signal saturation during vibration and shock events. STO should be read
continuously in the normal operation sequence after XYZ acceleration readings.
STO  threshold  monitoring  should  be  implemented  on  application  software.  Failure
thresholds and failure tolerant time of the system are application specific and should be
carefully validated. Monitoring can be implemented by counting the subsequent “STO
signal exceeding threshold” –events. Examples for STO thresholds are shown in Table
23.
|     | Murata Electronics Oy  |     |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |     |
| --- | ---------------------- | --- | --- | ------------ | --- | --- | ------------- | --- | --- | --- |
|     | www.murata.com         |     |     |              |     |     | Rev. 3        |     |     |     |

|     |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     |     |     | 30 (42)  |     |

STO
threshold
Failure-tolerant time, e.g. event counter
how many times threshold is exceeded
Component failure can be suspected if the STO signal exceeds the threshold level
continuously after performing component hard reset in static (no vibration) condition.
Table 23 Examples for STO Thresholds
|     |     | Mode  |     | Full-scale  |     | Examples for STO thresholds  |     |     |     |     |     |
| --- | --- | ----- | --- | ----------- | --- | ---------------------------- | --- | --- | --- | --- | --- |
|     |     | 1     |     | ± 3 g       |     | ±800 LSB                     |     |     |     |     |     |
|     |     | 2     |     | ± 6 g       |     | ±400 LSB                     |     |     |     |     |     |
|     |     | 3     |     | ± 1.5 g     |     | ±1600 LSB                    |     |     |     |     |     |
|     |     | 4     |     | ± 1.5 g     |     | ±1600 LSB                    |     |     |     |     |     |
6.2.1  Example of Self-Test Analysis
For example, if STO register read results: STO = 1100017Bh, the register value can be
converted as follows:

OP[31:26]
|     |     |     |     | +   |     | Data[23:8]  |     | CRC[7:0]  |     |     |     |
| --- | --- | --- | --- | --- | --- | ----------- | --- | --------- | --- | --- | --- |
RS[25:24]
|     |     |     |     | 1  1  |     | 0  0  | 0  1  | 7   | B   |     |     |
| --- | --- | --- | --- | ----- | --- | ----- | ----- | --- | --- | --- | --- |

OP + RS
11h = 0001 0001b
|     |     |     | 0001 00b    |     |     |     | = OP code = Read STO                  |     |     |     |     |
| --- | --- | --- | ----------- | --- | --- | --- | ------------------------------------- | --- | --- | --- | --- |
|     |     |     | 01b         |     |     |     | = return status (RS bits) = no error  |     |     |     |     |

Data = STO register content
   0001h
|     |     |     | 0001h → 1d  |     |     |     | = in 2's complement format  |     |     |     |     |
| --- | --- | --- | ----------- | --- | --- | --- | --------------------------- | --- | --- | --- | --- |
Self-test reading:
= 1
See Table 12 for recommended STO threshold values
|     | CRC                    |                 |                                  |     |     |              |     |     |               |     |     |
| --- | ---------------------- | --------------- | -------------------------------- | --- | --- | ------------ | --- | --- | ------------- | --- | --- |
|     |       7Bh              |                 |                                  |     |     |              |     |     |               |     |     |
|     |                        |                 | CRC of 110001h, see section 5.2  |     |     |              |     |     |               |     |     |
|     | Murata Electronics Oy  |                 |                                  |     |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |
|     |                        | www.murata.com  |                                  |     |     |              |     |     | Rev. 3        |     |     |

|     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     | 31 (42)  |     |

6.3  STATUS
Table 24 STATUS description
No. of  Read /
|     | Bank  Addr  | Name  |     | Description  |     |     |     |     |     |
| --- | ----------- | ----- | --- | ------------ | --- | --- | --- | --- | --- |
bits  Write
|     | 0 1  06h  |         |     | Status Summary combining ERR_FLAG1 and  |     |     |     |     |     |
| --- | --------- | ------- | --- | --------------------------------------- | --- | --- | --- | --- | --- |
|     |           | STATUS  | 16  | R                                       |     |     |     |     |     |
ERR_FLAG2
Table 25 STATUS operation
|     | Operation  |     | SPI Frame  |     |     |     | SPI Frame Hex  |     |     |
| --- | ---------- | --- | ---------- | --- | --- | --- | -------------- | --- | --- |
Read Status Summary  0001 1000 0000 0000 0000 0000 1110 0101  180000E5h
Table 26 STATUS register
D15  D14  D13  D12  D11  D10  D9  D8  D7  D6  D5  D4  D3  D2  D1  D0  Bit
|     |     |     | D   | D C  | S T | P M | P M | P   |     |
| --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- |
|     |     |     | IG  | IG L | A E | W   | D   | IN  |     |
|     |     |     |     | K    | T M | E   | O   |     |     |
|     |     |     | I1  | I2   |     | R M |   D | _   |     |
|     |     |     |     |      |   P |     | E   | C   |     |
|     |     |     |     |      |     |     | _   | O   |     |
C
N
|     |     | Reserved  |     |     |     |     | H   | T Read  |     |
| --- | --- | --------- | --- | --- | --- | --- | --- | ------- | --- |
|     |     |           |     |     |     |     | A   | IN      |     |
N
U
|     |     |     |     |     |     |     | G   | IT  |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
E
|     |     |     |     |     |     |     |     | Y   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |                        |     |              |     |     |               |     |     |     |
| --- | ---------------------- | --- | ------------ | --- | --- | ------------- | --- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |     |
|     | www.murata.com         |     |              |     |     | Rev. 3        |     |     |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     | 32 (42)  |

Table 27 STATUS register bit description
|     | Bit  | Name   | Description                 |     | Required action/explanation  |     |
| --- | ---- | ------ | --------------------------- | --- | ---------------------------- | --- |
|     | 9    | DIGI1  | Digital block error type 1  |     | SW or HW reset needed        |     |
|     | 8    | DIGI2  | Digital block error type 2  |     | SW or HW reset needed        |     |
|     | 7    | CLK    | Clock error                 |     | SW or HW reset needed        |     |
Acceleration too high and
acceleration reading not usable.
6  SAT  Signal saturated in signal path  Component failure possible. All
acceleration and STO output data
is invalid.
Error in temperature sensor.
Temperature reading and
acceleration reading not usable.
|     | 5   | TEMP  | Temperature signal path error  |     |     |     |
| --- | --- | ----- | ------------------------------ | --- | --- | --- |
All acceleration and STO output
data is invalid.
Component failure possible.
[After start-up or reset]
This flag is set high. No actions
needed.
|     |     |      | Start-up indication or voltage level  |     | [During normal operation]           |     |
| --- | --- | ---- | ------------------------------------- | --- | ----------------------------------- | --- |
|     | 4   | PWR  |                                       |     |                                     |     |
|     |     |      | failure                               |     | External voltages too high or low.  |     |
Component failure possible.

SW or HW reset needed.
Memory check failed. Possible
component failure
|     | 3   | MEM  | Error in non-volatile memory  |     |     |     |
| --- | --- | ---- | ----------------------------- | --- | --- | --- |

SW or HW reset needed.
If power down is not requested.
|     | 2   | PD  | Device in power down mode  |     |     |     |
| --- | --- | --- | -------------------------- | --- | --- | --- |
SW or HW reset needed
Bit is set high if operation mode
has been changed.
|     | 1  MODE_CHANGE  |     | Operation mode changed  |     |     |     |
| --- | --------------- | --- | ----------------------- | --- | --- | --- |
If mode change is not requested.
SW or HW reset needed
0  PIN_CONTINUITY  Component internal connection error  Possible component failure

Status register indicates saturation or failure in component. Failure is indicated by setting
the status flag to 1.

Software (SW) reset is done with SPI operation (see 5.1.4). Hardware (HW) reset is done
by power cycling the sensor. If these do not reset the error, then possible component error
has occurred and system needs to be shut down and part returned to supplier.
|     |                        |     |              |     |               |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     | Doc.No. 3165  |     |
|     | www.murata.com         |     |              |     | Rev. 3        |     |

|     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     |     |     | 33 (42)  |

6.3.1  Example of STATUS summary reset
The STATUS summary is cleared by reading the register. The example below shows the
MOSI commands and corresponding MISO responses for the “Read STATUS summary”
command when the SAT bit is set in the STATUS summary (data = 0x0040).
Step #1: Due to the SPI off‑frame protocol, the first MISO response corresponds to the
previous MOSI command and is therefore not relevant in this example (“don’t care”).
Step #2: The Return Status (RS) bits indicate an error (b'11) in the response to the MOSI
command.
Step #3: After the MOSI command, the Return Status (RS) bits are cleared (b'01).
Step #4: After the MOSI command, the SAT bit is also cleared, and the returned STATUS
data is 0x0000.
The definition of the Return Status bits is provided in Chapter 5.1.5.
|     | Step #  | MOSI command  | MISO response  |     | Return  | Status  | Data  |     |
| --- | ------- | ------------- | -------------- | --- | ------- | ------- | ----- | --- |
bits (RS)
|     | 1   | 0x180000E5  | don't care  |     | b'11  |     | don't care  |     |
| --- | --- | ----------- | ----------- | --- | ----- | --- | ----------- | --- |
|     | 2   | 0x180000E5  | 0x1b00407a  |     | b'11  |     | 0x0040      |     |
|     | 3   | 0x180000E5  | 0x19004079  |     | b'01  |     | 0x0040      |     |
|     | 4   | 0x180000E5  | 0x1900006a  |     | b'01  |     | 0x0000      |     |
6.4  Error Flag Block
Table 28 Error flag block description
No. of  Read /
|     | Bank  Addr  | Register Name  |     | Description  |     |     |     |     |
| --- | ----------- | -------------- | --- | ------------ | --- | --- | --- | --- |
bits  Write
|     | 0  07h  | ERR_FLAG1  | 16  | R  Error flags  |     |     |     |     |
| --- | ------- | ---------- | --- | --------------- | --- | --- | --- | --- |
0  08h
|     |     | ERR_FLAG2  | 16  | R  Error flags  |     |     |     |     |
| --- | --- | ---------- | --- | --------------- | --- | --- | --- | --- |

Table 29 Error flag block operations
|     | Operation  |     | SPI Frame                                |     |     |     | SPI Frame Hex  |     |
| --- | ---------- | --- | ---------------------------------------- | --- | --- | --- | -------------- | --- |
|     |            |     | 0001 1100 0000 0000 0000 0000 1110 0011  |     |     |     | 1C0000E3       |     |
Read ERR_FLAG1
Read ERR_FLAG2  0010 0000 0000 0000 0000 0000 1100 0001  200000C1h

ERR_FLAG registers indicate saturation or failure in the component. Failure is indicated
by setting the error flag to 1.
STATUS  register  contains  combination  of  the  information  in  the  ERR_FLAG1  and
ERR_FLAG2 registers; if there is an error, it is reflected in STATUS. ERR_FLAG registers
can be used to further assess reason for error. Note that reading ERR_FLAG registers
does not reset error flags in STATUS register nor reset RS bits.
|     |                        |     |              |     |     |               |     |     |
| --- | ---------------------- | --- | ------------ | --- | --- | ------------- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |
|     | www.murata.com         |     |              |     |     | Rev. 3        |     |     |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     | 34 (42)  |

6.4.1  ERR_FLAG1
Table 30 ERR_FLAG1 register
D15  D14  D13  D12  D11  D10  D9  D8  D7  D6  D5  D4  D3  D2  D1  D0  Bit
A
D
|     |           | C   |     |          |     | M       |
| --- | --------- | --- | --- | -------- | --- | ------- |
|     | Reserved  | _   |     | AFE_SAT  |     | E Read  |
|     |           | S   |     |          |     | M       |
|     |           | A   |     |          |     |         |
T

Table 31 ERR_FLAG1 register bit description
|     | Bit  Name        |     | Description  |     |     |     |
| --- | ---------------- | --- | ------------ | --- | --- | --- |
|     | 15:12  Reserved  |     | Reserved     |     |     |     |
11  ADC_SAT  Signal saturated at analog-to-digital converter (A2D)
10:1
AFE_SAT  Signal saturated at analog front-end circuitry (C2V)
|     | 0  MEM  |     | Error in non-volatile memory  |     |     |     |
| --- | ------- | --- | ----------------------------- | --- | --- | --- |

|     |                        |     |              |     |               |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     | Doc.No. 3165  |     |
|     | www.murata.com         |     |              |     | Rev. 3        |     |

|     |     |     |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     |     |     |     |     | 35 (42)  |     |

6.4.2  ERR_FLAG2
Table 32 ERR_FLAG2 register
D15  D14  D13  D12  D11  D10  D9  D8  D7  D6  D5  D4  D3  D2  D1  D0  Bit
|     |     |     |     |     |     | M   | M   |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
O
|     |     |     | A   |     |     |     | E   |      |     |     |     |         |     |
| --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | ------- | --- |
|     | R   | D   |     |     | R   | D   | M   | R    |     | A   |     |         |     |
|     | e   |     | _   | A   | e   | E   |     | e A  | D   | P   | T   |         |     |
|     | s   | _   | A   | V   | s   | _   | O   | s P  | P   | R   |     | C       |     |
|     | e   | E   | E   | G D | e   | C   | P R | e    |     | E W | E   | L Read  |     |
|     | rv  | X   | X   | N   | rv  |     | D Y | rv W | W   | F R | M   | K       |     |
|     |     | T   | T   | D D |     | H   |   _ | R    | R   | V   | P   |         |     |
|     | e   | C   | _   |     | e   | A   | C   | e    |     |   _ |     |         |     |
|     | d   |     | C   |     | d   | N   |     | d    |     | 2   |     |         |     |
|     |     |     |     |     |     | G   | R   |      |     |     |     |         |     |
|     |     |     |     |     |     |     | C   |      |     |     |     |         |     |
|     |     |     |     |     |     | E   |     |      |     |     |     |         |     |

Table 33 ERR_FLAG2 register bit description
|     | Bit  |     | Name      |     |     |     | Description                          |     |     |     |     |     |     |
| --- | ---- | --- | --------- | --- | --- | --- | ------------------------------------ | --- | --- | --- | --- | --- | --- |
|     | 15   |     | Reserved  |     |     |     | Reserved                             |     |     |     |     |     |     |
|     | 14   |     | D_EXT_C   |     |     |     | External capacitor connection error  |     |     |     |     |     |     |
|     | 13   |     | A_EXT_C   |     |     |     | External capacitor connection error  |     |     |     |     |     |     |
|     | 12   |     | AGND      |     |     |     | Analog ground connection error       |     |     |     |     |     |     |
11
|     |     |     | VDD          |     |     |     | Supply voltage error            |     |     |     |     |     |     |
| --- | --- | --- | ------------ | --- | --- | --- | ------------------------------- | --- | --- | --- | --- | --- | --- |
|     | 10  |     | Reserved     |     |     |     | Reserved                        |     |     |     |     |     |     |
|     |     | 9   | MODE_CHANGE  |     |     |     | Operation mode changed by user  |     |     |     |     |     |     |
8
|     |     |     | PD          |     |     |     | Device in power down mode  |     |     |     |     |     |     |
| --- | --- | --- | ----------- | --- | --- | --- | -------------------------- | --- | --- | --- | --- | --- | --- |
|     |     | 7   | MEMORY_CRC  |     |     |     | Memory CRC check failed    |     |     |     |     |     |     |
|     |     | 6   | Reserved    |     |     |     | Reserved                   |     |     |     |     |     |     |
|     |     | 5   | APWR        |     |     |     | Analog power error         |     |     |     |     |     |     |
[After start-up or reset]
This flag is set high. No actions needed.
[During normal operation]
|     |     | 4   | DPWR  |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | ----- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Digital power error. Component failure possible.

SW or HW reset needed.
|     |                        | 3               | VREF    |     |     |              | Reference voltage error        |     |     |               |     |     |     |
| --- | ---------------------- | --------------- | ------- | --- | --- | ------------ | ------------------------------ | --- | --- | ------------- | --- | --- | --- |
|     |                        | 2               | APWR_2  |     |     |              | Analog power error             |     |     |               |     |     |     |
|     |                        | 1               | TEMP    |     |     |              | Temperature signal path error  |     |     |               |     |     |     |
|     |                        | 0               | CLK     |     |     |              | Clock error                    |     |     |               |     |     |     |
|     |                        |                 |         |     |     |              |                                |     |     |               |     |     |     |
|     | Murata Electronics Oy  |                 |         |     |     | SCA3300-D01  |                                |     |     | Doc.No. 3165  |     |     |     |
|     |                        | www.murata.com  |         |     |     |              |                                |     |     | Rev. 3        |     |     |     |

|     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     | 36 (42)  |     |

6.5  CMD
Table 34 CMD description
No. of  Read /
|     | Bank  Addr  | Register Name  |     | Description  |     |     |     |     |     |
| --- | ----------- | -------------- | --- | ------------ | --- | --- | --- | --- | --- |
bits  Write
0  0Dh  CMD  16  R / W  Sets operation mode, SW Reset and Power down mode
Table 35 CMD operations
|     | Command  |     | SPI Frame  |     |     |     | SPI Frame hex  |     |     |
| --- | -------- | --- | ---------- | --- | --- | --- | -------------- | --- | --- |
Read CMD  0011 0100 0000 0000 0000 0000 1101 1111  340000DFh
Change to mode1  1011 0100 0000 0000 0000 0000 0001 1111  B400001Fh
Change to mode2  1011 0100 0000 0000 0000 0001 0000 0010  B4000102h
Change to mode3  1011 0100 0000 0000 0000 0010 0010 0101  B4000225h
Change to mode4  1011 0100 0000 0000 0000 0011 0011 1000  B4000338h
Set power down mode  1011 0100 0000 0000 0000 0100 0110 1011  B400046Bh
Wake up from power down mode  1011 0100 0000 0000 0000 0000 0001 1111  B400001Fh
SW Reset  1011 0100 0000 0000 0010 0000 1001 1000  B4002098h
Table 36 CMD register
D15  D14  D13  D12  D11  D10  D9  D8  D7  D6  D5  D4  D3  D2  D1  D0  Bit
|     |     |     |     | F F   |     | F F   |     |         |     |
| --- | --- | --- | --- | ----- | --- | ----- | --- | ------- | --- |
|     |     | R   |     | a a   | S   | a a   |     |         |     |
|     |     | e   |     | c c   | W   | c c   |     | M       |     |
|     |     | s   |     | to to |     | to to |     |         |     |
|     |     | e   |     |       | _   |       | P   | O Read  |     |
|     |     | rv  |     | ry ry | R   | ry ry | D   | D       |     |
|     |     |     |     |  u  u | S   |  u  u |     |         |     |
|     |     | e   |     |       |     |       |     | E       |     |
|     |     | d   |     | s s   | T   | s s   |     |         |     |
|     |     |     |     | e e   |     | e e   |     |         |     |
|     |     |     |     |       |     |       |     |         |     |
Table 37 CMD register bit description
|     | Bit  Name       |     |     | Description          |     |     |     |     |     |
| --- | --------------- | --- | --- | -------------------- | --- | --- | --- | --- | --- |
|     | 15:8  Reserved  |     |     | Reserved             |     |     |     |     |     |
|     | 7  Factory use  |     |     | Factory use          |     |     |     |     |     |
|     | 6  Factory use  |     |     | Factory use          |     |     |     |     |     |
|     | 5  SW_RST       |     |     | Software (SW) Reset  |     |     |     |     |     |
|     | 4  Factory use  |     |     | Factory use          |     |     |     |     |     |
|     | 3  Factory use  |     |     | Factory use          |     |     |     |     |     |
|     | 2  PD           |     |     | Power Down           |     |     |     |     |     |
|     | 1:0  MODE       |     |     | Operation Mode       |     |     |     |     |     |

Sets operation mode of the SCA3300-D01. After power-off, reset (SW or HW), power
down mode or unintentional power-off, normal start-up sequence must be followed. Note:
mode will be set to default mode1.
Operation modes are described in section 4.3.
Changing mode will set Status Summary bit 1 to high, setting / waking up from power
down mode will set Status Summary bit 2 to high (see 6.3.) Thus RS bits will show ‘11’
(see 5.1.5.)
|     | Murata Electronics Oy  |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |     |
| --- | ---------------------- | --- | ------------ | --- | --- | ------------- | --- | --- | --- |
|     | www.murata.com         |     |              |     |     | Rev. 3        |     |     |     |

|     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     | 37 (42)  |     |

Note: User must not configure other than given valid commands, otherwise power-off,
reset or power down is required.
6.6  WHOAMI
Table 38 WHOAMI description
No. of  Read /
|     | Bank  Addr  | Register Name  |     | Description  |     |     |     |     |     |
| --- | ----------- | -------------- | --- | ------------ | --- | --- | --- | --- | --- |
bits  Write
0  10h  WHOAMI  8  R  8-bit register for component identification
Table 39 WHOAMI operations
|     | Operation  |     | SPI Frame  |     |     |     | SPI Frame Hex  |     |     |
| --- | ---------- | --- | ---------- | --- | --- | --- | -------------- | --- | --- |
Read WHOAMI  0100 0000 0000 0000 0000 0000 1001 0001  40000091h
Table 40 WHOAMI register
D15  D14  D13  D12  D11  D10  D9  D8  D7  D6  D5  D4  D3  D2  D1  D0  Bit
|     |     |                  |     |   -  | -  -                      | -  -  | -   | -  -  Write  |     |
| --- | --- | ---------------- | --- | ---- | ------------------------- | ----- | --- | ------------ | --- |
|     |     | Not Used [15:8]  |     |      | Component ID [7:0] = 51h  |       |     | Read         |     |

WHOAMI is an 8-bit register for component identification. Returned value is 51h.
Note: as returned value is fixed, this can be used to ensure SPI communication is working
correctly.
6.7  Serial Block
Table 41 Serial block description
No. of  Read /
|     | Bank  Addr  | Register Name  |     | Description  |     |     |     |     |     |
| --- | ----------- | -------------- | --- | ------------ | --- | --- | --- | --- | --- |
bits  Write
|     | 1  19h  | SERIAL1  | 16  | R  Component serial part 1  |     |     |     |     |     |
| --- | ------- | -------- | --- | --------------------------- | --- | --- | --- | --- | --- |
|     | 1  1Ah  | SERIAL2  | 16  | R  Component serial part 2  |     |     |     |     |     |
Table 42 Serial block operations
|     | Operation  |     | SPI Frame  |     |     |     | SPI Frame Hex  |     |     |
| --- | ---------- | --- | ---------- | --- | --- | --- | -------------- | --- | --- |
Read SERIAL1  0110 0100 0000 0000 0000 0000 1010 0111  640000A7h
Read SERIAL2  0110 1000 0000 0000 0000 0000 1010 1101  680000ADh

Serial Block contains sensor serial number in two 16 bit registers in register bank #1, see
6.8 SELBANK for information how to switch register banks. The same serial number is
also written on top of the sensor.
|     |                        |     |              |     |     |               |     |     |     |
| --- | ---------------------- | --- | ------------ | --- | --- | ------------- | --- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     |     | Doc.No. 3165  |     |     |     |
|     | www.murata.com         |     |              |     |     | Rev. 3        |     |     |     |

38 (42)
The following procedure is recommended when reading serial number:
1. Change active register bank to #1
2. Read registers 19h and 1Ah
3. Change active register back to bank #0
4. Resolve serial number:
1. Combine result data from 1Ah[16:31] and 19h[0:15]
2. Convert HEX to DEC
3. Add letters “B33” to end
6.7.1 Example of Resolving Serial Number
1 Change active register bank to #1
SPI Request SWITCH_TO_BANK_1
Request: FC00016E
Response: XXXXXXXX, response to previous command
2. Read registers 19h and 1Ah
SPI Request READ_SERIAL1:
Request: 640000A7
Response: FD0001E1, response to switch command
SPI Request READ_SERIAL2:
Request: 680000AD
Response: 65F7DA19, response to serial1, data: F7DA
3. Change active register back to bank #0
SPI Request SWITCH_TO_BANK_0
Request: FC000073
Response: 693CE54F, response to serial2, data: 3CE5
4. Resolve serial number
1. Combined Serial number: 3CE5F7DA
2. HEX to DEC: 1021704154
3. Add “B33”: 1021704154B33
➔ Full Serial number: 1021704154B33
Murata Electronics Oy SCA3300-D01 Doc.No. 3165
www.murata.com Rev. 3

|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |          |
| --- | --- | --- | --- | --- | --- | --- | -------- |
|     |     |     |     |     |     |     | 39 (42)  |

6.8  SELBANK
Table 43 SELBANK description
No. of  Read /
|     | Bank  Addr  | Register Name  |     | Description  |     |     |     |
| --- | ----------- | -------------- | --- | ------------ | --- | --- | --- |
bits  Write
0 1  1Fh  SELBANK  16  R  Switch between active register banks
Table 44 SELBANK operations
|     | Command  |     | SPI Frame  |     |     | SPI Frame hex  |     |
| --- | -------- | --- | ---------- | --- | --- | -------------- | --- |
Read current bank  0111 1100 0000 0000 0000 0000 1011 0011  7C0000B3h
Switch to bank #0  1111 1100 0000 0000 0000 0000 0111 0011  FC000073h
Switch to bank #1  1111 1100 0000 0000 0000 0001 0110 1110  FC00016Eh

SELBANK is used to switch between memory banks #0 and #1. It’s recommended to keep
memory bank #0 selected unless register from bank #1 is required, for example, reading
serial number of sensor. After using bank #1 user should switch back to bank #0.
7  Application information
7.1  Application Circuitry and External Component Characteristics
See Figure 15 and Table 45 for specification of the external components. The PCB layout
example is shown in Figure 16.

|     | VDD |     |     |     |     | DVIO |     |
| --- | --- | --- | --- | --- | --- | ---- | --- |
1 12
|     |     |     | AVSS | EMC_GND |     |     |     |
| --- | --- | --- | ---- | ------- | --- | --- | --- |
2 11
|     |     |     | A_EXTC     | DVSS      |     |     |     |
| --- | --- | --- | ---------- | --------- | --- | --- | --- |
|     |     |     | 3 RESERVED | D_EXTC 10 |     |     |     |
|     |     |     | 4 VDD      | DVIO 9    |     |     |     |
5 8
|     |     | CSB | CSB | SCK SCK |     |     |     |
| --- | --- | --- | --- | ------- | --- | --- | --- |
6 7
|     |     | MISO | MISO | MOSI MOSI |     |     |     |
| --- | --- | ---- | ---- | --------- | --- | --- | --- |
|     | C1  | C2   |      |           |     | C3  | C4  |
100 nF 100 nF
|     | 100 nF | 100 nF |     |     |     |     |     |
| --- | ------ | ------ | --- | --- | --- | --- | --- |

Figure 15 Application schematic.
|     |                        |     |              |     |               |     |     |
| --- | ---------------------- | --- | ------------ | --- | ------------- | --- | --- |
|     | Murata Electronics Oy  |     | SCA3300-D01  |     | Doc.No. 3165  |     |     |
|     | www.murata.com         |     |              |     | Rev. 3        |     |     |

|     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     |     |     |     | 40 (42)  |     |

Table 45 External component description for SCA3300-D01.
|     | Symbol  | Description  |     |     |     | Min.  | Nom.  | Max.  | Unit  |
| --- | ------- | ------------ | --- | --- | --- | ----- | ----- | ----- | ----- |
Decoupling capacitor between VDD and GND

|     |     | Recommended component:                    |     |     |      | 70  | 100  |     | nF  |
| --- | --- | ----------------------------------------- | --- | --- | ---- | --- | ---- | --- | --- |
|     | C1  |                                           |     |     |      |     |      |     |     |
|     |     | Murata GCM155R71C104KA55, 0402, 16V, X7R  |     |     | ESR  |     |      |     | m  |
Capacitor availability should be confirmed from
www.murata.com
Decoupling capacitor between A_EXTC and GND

|     |     |     |     |     |     | 70  | 100  | 130  | nF  |
| --- | --- | --- | --- | --- | --- | --- | ---- | ---- | --- |
C2  Recommended component:
|     |     | Murata GCM155R71C104KA55, 0402, 16V, X7R  |     |     | ESR  |     |     | 100  | m  |
| --- | --- | ----------------------------------------- | --- | --- | ---- | --- | --- | ---- | --- |
Capacitor availability should be confirmed from
www.murata.com
Decoupling capacitor between D_EXTC and GND

|     |     |     |     |     |     | 70  | 100  | 130  | nF  |
| --- | --- | --- | --- | --- | --- | --- | ---- | ---- | --- |
Recommended component:
C3
|     |     | Murata GCM155R71C104KA55, 0402, 16V, X7R  |     |     | ESR  |     |     | 100  | m  |
| --- | --- | ----------------------------------------- | --- | --- | ---- | --- | --- | ---- | --- |
Capacitor availability should be confirmed from
www.murata.com
Decoupling capacitor between DVIO and GND

|     |     | Recommended component:                    |     |     |      | 70  | 100  |     | nF  |
| --- | --- | ----------------------------------------- | --- | --- | ---- | --- | ---- | --- | --- |
|     | C4  |                                           |     |     |      |     |      |     |     |
|     |     | Murata GCM155R71C104KA55, 0402, 16V, X7R  |     |     | ESR  |     |      |     | m  |
Capacitor availability should be confirmed from
www.murata.com

Figure 16. Application PCB layout.

General circuit diagram and PCB layout recommendations for SCA3300-D01:
1.  Connect decoupling SMD capacitors (C1 - C4) right next to respective component
pins.
2.  Place ground plate under component.
3.  Do not route signals or power supplies under the component on top layer.
4.  Ensure good ground connection of DVSS, AVSS and EMC_GND pins
|     | Murata Electronics Oy  |                 |     | SCA3300-D01  |     | Doc.No. 3165  |     |     |     |
| --- | ---------------------- | --------------- | --- | ------------ | --- | ------------- | --- | --- | --- |
|     |                        | www.murata.com  |     |              |     | Rev. 3        |     |     |     |

41 (42)
7.2 Assembly Instructions
The Moisture Sensitivity Level of the component is Level 3 according to the IPC/JEDEC
JSTD-020C. The part is delivered in a dry pack. The manufacturing floor time (out of bag)
at the customer’s end is 168 hours.
Usage of PCB coating materials may penetrate component lid and affect component
performance. PCB coating is not allowed.
Sensor components shall not be exposed to chemicals that are known to react with
silicones, such as solvents. Sensor components shall not be exposed to chemicals with
high impurity levels, such as Cl-, Na+, NO3-, SO4-, NH4+ in excess of >10 ppm. Flame
retardants such as Br or P containing materials shall be avoided in close vicinity of sensor
component. Materials with high amount of volatile content should also be avoided.
If heat stabilized polymers are used in application, user should check that no iodine, or
other halogen, containing additives are used.
For additional assembly related details please refer to technical note Assembly
instructions of Dual Flat Lead Package (DFL).
APP 2702 Assembly_Instructions_for_DFL_Package
8 Traceability
Each sensor is assigned a unique serial number at the assembly line, which is printed on
the component housing and stored in the ASIC's internal memory. This serial number
allows full traceability of the entire bill of materials. Test data can be traced from final
component tests down to individual MEMS and ASIC level test data. Traceability data also
enables tracking of consumables and production equipment.
9 Frequently Asked Questions
• How can I be sure SPI communication is working?
o Read register WHOAMI (10h), the response should be 51h.
• Why do I get wrong results when I read data?
o SCA3300-D01 uses off-frame protocol (see 5.1.2 Protocol), make sure to
utilize this correctly.
o Confirm time between SPI requests (CSB high) is at least 10 µs.
o Ensure SCA3300-D01 is correctly started (see 4.2 Start-up sequence).
o Read RS bits (see 5.1.5 Return Status), if error is shown read Status
Summary (see 6.3 STATUS) for further information.
o Confirm correct sensitivity is used for current operation mode (see 4.3
Operation modes)
Murata Electronics Oy SCA3300-D01 Doc.No. 3165
www.murata.com Rev. 3

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |

|     |     |     |     |     |          |     |
| --- | --- | --- | --- | --- | -------- | --- |
|     |     |     |     |     | 42 (42)  |     |

10  Order Information
Measurement
|     | Order Code  | Description  |     |     | Packing  Qty  |     |
| --- | ----------- | ------------ | --- | --- | ------------- | --- |
Range (g)
3-axis accelerometer with digital SPI interface

|     | SCA3300-D01-004  |     |     | ±1.5g, ±3g, ±6g  | Bulk  4pcs  |     |
| --- | ---------------- | --- | --- | ---------------- | ----------- | --- |
This order code is only for samples. Not for
production.
SCA3300-D01-1  3-axis accelerometer with digital SPI interface  ±1.5g, ±3g, ±6g  T&R  100pcs
SCA3300-D01-10  3-axis accelerometer with digital SPI interface  ±1.5g, ±3g, ±6g  T&R  1000pcs

Murata reserves all rights to modify this document without prior notice.

|     | Murata Electronics Oy  |     | SCA3300-D01  | Doc.No. 3165  |     |     |
| --- | ---------------------- | --- | ------------ | ------------- | --- | --- |
|     | www.murata.com         |     |              | Rev. 3        |     |     |