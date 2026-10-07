Low Noise, Low Drift, Low Power,
3-Axis MEMS Accelerometers

| Data Sheet  |     |     |     |     |     | ADXL354/ADXL355 |     |
| ----------- | --- | --- | --- | --- | --- | --------------- | --- |

| FEATURES  |     |     |     | FUNCTIONAL BLOCK DIAGRAMS  |         |               |     |
| --------- | --- | --- | --- | -------------------------- | ------- | ------------- | --- |
|           |     |     |     |                            | V1P8ANA | V1P8DIG RANGE |     |
Hermetic package offers excellent long-term stability
0 g offset vs. temperature (all axes): 0.15 mg/°C maximum
Ultralow noise density (all axes): 20 μg/√Hz (ADXL354)  VSUPPLY LDO LDO P O W E R
MAN A G E M ENT
| Low power, V                           | SUPPLY  (LDO enabled)  |     |     | XOUT |         |     |     |
| -------------------------------------- | ---------------------- | --- | --- | ---- | ------- | --- | --- |
| ADXL354 in measurement mode: 150 μA    |                        |     |     |      | A N A L | O G |     |
|                                        |                        |     |     | YOUT | F IL T  | E R | ST1 |
3-AXIS
| ADXL355 in measurement mode: 200 μA     |     |     |     |     |     | SENSOR  | ST2 |
| --------------------------------------- | --- | --- | --- | --- | --- | ------- | --- |
|                                         |     |     |     | OUT |     | CONTROL |     |
| ADXL354/ADXL355 in standby mode: 21 μA  |     |     |     |     |     | LOGIC   |     |
STBY
ADXL354 has user adjustable analog output bandwidth  TEMP T EM P ADXL354
|                                  |     |     |     |     | SE N SO | R   | VDDIO     |
| -------------------------------- | --- | --- | --- | --- | ------- | --- | --------- |
| ADXL355 digital output features  |     |     |     |     |         |     | 200-50241 |
Digital serial peripheral interface (SPI)/I2C interfaces  VSSIO VSS

20-bit analog-to-digital converter (ADC)  Figure 1. ADXL354 Functional Block Diagram
Data interpolation routine for synchronous sampling
|     |     |     |     | V1P8ANA | V1P8DIG | VDDIO |     |
| --- | --- | --- | --- | ------- | ------- | ----- | --- |
Programmable high- and low-pass digital filters
POWER
| Electromechanical self test  |     |     |     | VSUPPLY LDO |     | ADXL355 MANAGEMENT |     |
| ---------------------------- | --- | --- | --- | ----------- | --- | ------------------ | --- |
LDO
Integrated temperature sensor
ADC
INT1
| Voltage range options  |     |     |     |     |        | DIGITAL CO NT R OL | INT2 |
| ---------------------- | --- | --- | --- | --- | ------ | ------------------ | ---- |
|                        |     |     |     |     | ANALOG | ADC LO G IC        |      |
V  with internal regulators: 2.25 V to 3.6 V  FILTER FILTER DRDY
| SUPPLY |                                                 |     |     | 3-AXIS |      | ADC             | CS/SCL     |
| ------ | ----------------------------------------------- | --- | --- | ------ | ---- | --------------- | ---------- |
| V      | , V  with internal low dropout regulator (LDO)  |     |     | SENSOR |      |                 |            |
| 1P8ANA | 1P8DIG                                          |     |     |        |      |                 | SCLK/VSSIO |
|        |                                                 |     |     |        | TEMP | ADC FIFO SERIAL | MOSI/SDA   |
bypassed: 1.8 V typical ± 10%  SENSOR I/O MISO/ASEL 100-50241
Operating temperature range: −40°C to +125°C
|     |     |     |     |     |     | VSSIO VSS |     |
| --- | --- | --- | --- | --- | --- | --------- | --- |
14-terminal, 6 mm × 6 mm × 2.1 mm, LCC package,  Figure 2. ADXL355 Functional Block Diagram
0.26 grams
APPLICATIONS
Inertial measurement units (IMUs)/altitude and heading
reference systems (AHRSs)
Platform stabilization systems
Structural health monitoring
Seismic imaging
Tilt sensing
Robotics
Condition monitoring
GENERAL DESCRIPTION
The analog output ADXL354 and the digital output ADXL355  Highly integrated in a compact form factor, the low power
are low noise density, low 0 g offset drift, low power, 3-axis  ADXL355 is ideal in an Internet of Things (IoT) sensor node
accelerometers with selectable measurement ranges. The  and other wireless product designs.
ADXL354B supports the ±2 g and ±4 g ranges, the ADXL354C
The ADXL355 multifunction pin names may be referenced by
supports the ±2 g and ±8 g ranges, and the ADXL355 supports  their relevant function only for either the SPI or I2C interfaces.
the ±2.048 g, ±4.096 g, and ±8.192 g ranges. The ADXL354/

ADXL355 offer industry leading noise, minimal offset drift over
temperature, and long term stability enabling precision
applications with minimal calibration.

1 Protected by U.S. Patents 8,472,270; 9,041,462; 8,665,627; 8,917,099; 6,892,576; 9,297,825; and 7,956,621.
| Rev. 0  |     | Document Feedback  |     |     |     |     |     |
| ------- | --- | ------------------ | --- | --- | --- | --- | --- |
Information furnished by Analog Devices is believed to be accurate and reliable. However, no

responsibility is assumed by Analog Devices for its use, nor for any infringements of patents or other
rights of third parties that may result from its use. Specifications subject to change without notice. No  One Technology Way, P.O. Box 9106, Norwood, MA 02062-9106, U.S.A.
|     |     |     | Tel: 781.329.4700  |     | ©2016 Analog Devices, Inc. All rights reserved.  |     |     |
| --- | --- | --- | ------------------ | --- | ------------------------------------------------ | --- | --- |
license is granted by implication or otherwise under any patent or patent rights of Analog Devices.
Trademarks and registered trademarks are the property of their respective owners.    Technical Support  www.analog.com

ADXL354/ADXL355 Data Sheet
TABLE OF CONTENTS
Features .............................................................................................. 1 NVM_BUSY ............................................................................... 28
Applications ....................................................................................... 1 External Synchronization and Interpolation .......................... 29
Functional Block Diagrams ............................................................. 1 ADXL355 Register Map ................................................................. 31
General Description ......................................................................... 1 Register Definitions........................................................................ 32
Revision History ............................................................................... 2 Analog Devices ID Register ...................................................... 32
Specifications ..................................................................................... 3 Analog Devices MEMS ID Register ......................................... 32
Analog Output for the ADXL354 ............................................... 3 Device ID Register ..................................................................... 32
Digital Output for the ADXL355 ............................................... 4 Product Revision ID Register ................................................... 32
SPI Digital Interface Characteristics for the ADXL355 .......... 5 Status Register ............................................................................. 32
I2C Digital Interface Characteristics for the ADXL355 ........... 6 FIFO Entries Register ................................................................ 33
Absolute Maximum Ratings ............................................................ 8 Temperature Data Registers ...................................................... 33
Thermal Resistance ...................................................................... 8 X-Axis Data Registers ................................................................ 33
ESD Caution .................................................................................. 8 Y-Axis Data Registers ................................................................ 34
Pin Configurations and Function Descriptions ........................... 9 Z-Axis Data Registers ................................................................ 34
Typical Performance Characteristics ........................................... 11 FIFO Access Register ................................................................. 35
Root Allan Variance (RAV) ADXL355 Characteristics ......... 19 X-Axis Offset Trim Registers .................................................... 35
Theory of Operation ...................................................................... 20 Y-Axis Offset Trim Registers .................................................... 35
Analog Output ............................................................................ 20 Z-Axis Offset Trim Registers .................................................... 36
Digital Output ............................................................................. 21 Activity Enable Register ............................................................ 36
Axes of Acceleration Sensitivity ............................................... 21 Activity Threshold Registers ..................................................... 36
Power Sequencing ...................................................................... 22 Activity Count Register ............................................................. 36
Power Supply Description ......................................................... 22 Filter Settings Register ............................................................... 37
Overrange Protection ................................................................. 22 FIFO Samples Register .............................................................. 37
Self Test ........................................................................................ 22 Interrupt Pin (INTx) Function Map Register......................... 37
Filter ............................................................................................. 23 Data Synchronization ................................................................ 38
Serial Communications ................................................................. 25 I2C Speed, Interrupt Polarity, and Range Register ................. 38
SPI Protocol ................................................................................. 25 Power Control Register ............................................................. 38
I2C Protocol ................................................................................. 26 Self Test Register ......................................................................... 39
Reading Acceleration or Temperature Data from the Interface Reset Register .............................................................................. 39
....................................................................................................... 26
Recommended Soldering Profile ................................................. 40
FIFO ................................................................................................. 27
PCB Footprint Pattern ............................................................... 41
Interrupts ......................................................................................... 28
Packaging and Ordering Information ......................................... 42
DATA_RDY ................................................................................. 28
Outline Dimensions ................................................................... 42
DRDY Pin .................................................................................... 28
Branding Information ................................................................ 42
FIFO_FULL ................................................................................. 28
Ordering Guide .......................................................................... 42
FIFO_OVR .................................................................................. 28
Activity ......................................................................................... 28
REVISION HISTORY
9/2016—Revision 0: Initial Version
Rev. 0 | Page 2 of 42

| Data Sheet  |     |     |     | ADXL354/ADXL355  |     |
| ----------- | --- | --- | --- | ---------------- | --- |

SPECIFICATIONS
ANALOG OUTPUT FOR THE ADXL354
T  = 25°C, V  = 3.3 V, x-axis acceleration and y-axis acceleration = 0 g, and z-axis acceleration = 1 g, unless otherwise noted.
A SUPPLY
Table 1.
| Parameter     | Test Conditions/Comments  |     | Min  Typ  | Max  | Unit  |
| ------------- | ------------------------- | --- | --------- | ---- | ----- |
| SENSOR INPUT  | Each axis                 |     |           |      |       |
Output Full-Scale Range (FSR)  ADXL354B, supports two ranges    ±2/±4    g
|                         | ADXL354C, supports two ranges  |     |   ±2/±8  |     | g    |
| ----------------------- | ------------------------------ | --- | -------- | --- | ---- |
| Resonant Frequency1     |                                |     |   2.4    |     | kHz  |
| Nonlinearity            | ±2 g                           |     |   0.1    |     | %    |
| Cross Axis Sensitivity  |                                |     |   1      |     | %    |
| SENSITIVITY             | Ratiometric to V               |     |          |     |      |
1P8ANA
Sensitivity at X OUT , Y OUT , Z OUT    ±2 g  368  400  432  mV/g
|     | ±4 g  |     | 184  200  | 216  | mV/g  |
| --- | ----- | --- | --------- | ---- | ----- |
|     | ±8 g  |     | 92  100   | 108  | mV/g  |
Sensitivity Change due to Temperature  −40°C to +125°C    ±0.01    %/°C
| 0 g OFFSET  | Each axis, ±2 g   |     |     |     |     |
| ----------- | ----------------- | --- | --- | --- | --- |
0 g Output for X , Y , Z   Referred to V /2  −75  ±25  +75  mg
OUT OUT OUT 1P8ANA
0 g Offset vs. Temperature (X-Axis, Y-Axis, and Z-Axis)2  −40°C to +125°C  −0.15  ±0.1  +0.15  mg/°C
| Repeatability3  | X-axis and y-axis  |     |   ±3.5  |     | mg  |
| --------------- | ------------------ | --- | ------- | --- | --- |
|                 | Z-axis             |     |   ±9    |     | mg  |
Vibration Rectification Error (VRE)4  ±2 g range, in a 1 g orientation,     <0.4    g
offset due to 2.5 g rms vibration
| NOISE DENSITY               | ±2 g               |     |       |     |             |
| --------------------------- | ------------------ | --- | ----- | --- | ----------- |
| X-Axis, Y-Axis, and Z-Axis  |                    |     |   20  |     | µg/√Hz      |
| Velocity Random Walk        | X-axis and y-axis  |     |   9   |     | µm/sec/√Hr  |
|                             | Z-axis             |     |   13  |     | µm/sec/√Hr  |
| BANDWIDTH                   |                    |     |       |     |             |
Internal Low-Pass Filter Frequency  Fixed frequency, 50% response     1500    Hz
attenuation
|     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- |
SELF TEST
| Output Change  |     |     |            |      |     |
| -------------- | --- | --- | ---------- | ---- | --- |
| X-Axis         |     |     |   0.3      |      | g   |
| Y-Axis         |     |     |   0.3      |      | g   |
| Z-Axis         |     |     |   1.5      |      | g   |
| POWER SUPPLY   |     |     |            |      |     |
| Voltage Range  |     |     |            |      |     |
| V SUPPLY 5     |     |     | 2.25  2.5  | 3.6  | V   |
| V              |     |     | V   2.5    | 3.6  | V   |
| DDIO           |     |     | 1P8DIG     |      |     |
V 1P8ANA , V 1P8DIG  with Internal Low Dropout   V SUPPLY  = 0 V  1.62  1.8  1.98  V
Regulator (LDO) Bypassed
| Current            |     |     |        |     |     |
| ------------------ | --- | --- | ------ | --- | --- |
| Measurement Mode   |     |     |        |     |     |
| V  (LDO Enabled)   |     |     |   150  |     | µA  |
SUPPLY
| V  (LDO Disabled)   |     |     |   138  |     | µA  |
| ------------------- | --- | --- | ------ | --- | --- |
1P8ANA
| V 1P8DIG  (LDO Disabled)  |     |     |   12  |     | µA  |
| ------------------------- | --- | --- | ----- | --- | --- |
| Standby Mode              |     |     |       |     |     |
| V SUPPLY  (LDO Enabled)   |     |     |   21  |     | µA  |
| V  (LDO Disabled)         |     |     |   7   |     | µA  |
1P8ANA
| V 1P8DIG  (LDO Disabled)  |                       |     |   10   |     | µA  |
| ------------------------- | --------------------- | --- | ------ | --- | --- |
| Turn On Time6             | 2 g range             |     |   <10  |     | ms  |
|                           | Power-off to standby  |     |   <10  |     | ms  |
Rev. 0 | Page 3 of 42

| ADXL354/ADXL355  |     |     | Data Sheet  |     |
| ---------------- | --- | --- | ----------- | --- |

| Parameter         | Test Conditions/Comments  | Min  Typ  | Max        | Unit  |
| ----------------- | ------------------------- | --------- | ---------- | ----- |
| OUTPUT AMPLIFIER  |                           |           |            |       |
| Swing             | No load                   | 0.03      | V  − 0.03  | V     |
1P8ANA
| Output Series Resistance     |     |   32     |       | kΩ     |
| ---------------------------- | --- | -------- | ----- | ------ |
| TEMPERATURE SENSOR           |     |          |       |        |
| Output at 25°C               |     |   892.2  |       | mV     |
| Scale Factor                 |     |   3.0    |       | mV/°C  |
| TEMPERATURE                  |     |          |       |        |
| Operating Temperature Range  |     | −40      | +125  | °C     |

1 The resonant frequency is a sensor characteristic. An integrated analog 1.5 kHz (−6 dB) sinc low-pass filter that cannot be bypassed limits the actual output response.
2 The temperature change is −40°C to +25°C or +25°C to +125°C.
3 Repeatability is predicted for a 10 year life and includes shifts due to the high temperature operating life test (HTOL) (TA = 150°C, VSUPPLY = 3.6 V, and 1000 hours),
temperature cycling (−55°C to +125°C and 1000 cycles), velocity random walk, broadband noise, and temperature hysteresis.
4 The VRE measurement is the shift in dc offset while the device is subject to 2.5 g rms of random vibration from 50 Hz to 2 kHz. The device under test (DUT) is
configured for the ±2 g range and an output data rate of 4 kHz. The VRE scales with the range setting.
5 When V1P8ANA and V1P8DIG are generated internally, VSUPPLY is valid. To disable the LDO and drive V1P8ANA and V1P8DIG externally, connect VSUPPLY to VSS.
6 Standby to measurement mode; valid when the output is within 1 mg of the final value.

DIGITAL OUTPUT FOR THE ADXL355
T  = 25°C, V  = 3.3 V, x-axis acceleration and y-axis acceleration = 0 g, and z-axis acceleration = 1 g, and output data rate (ODR) =
A SUPPLY
500 Hz, unless otherwise noted. Note that multifunction pin names may be referenced by their relevant function only.
Table 2.
| Parameter     | Test Conditions/Comments  | Min  Typ  | Max  | Unit  |
| ------------- | ------------------------- | --------- | ---- | ----- |
| SENSOR INPUT  | Each axis                 |           |      |       |
Output Full Scale Range (FSR)  User selectable    ±2.048    g
|                         |            |   ±4.096  |     | g     |
| ----------------------- | ---------- | --------- | --- | ----- |
|                         |            |   ±8.192  |     | g     |
| Nonlinearity            | ±2 g       |   0.1     |     | % FS  |
| Cross Axis Sensitivity  |            |   1       |     | %     |
| SENSITIVITY             | Each axis  |           |     |       |
X-Axis, Y-Axis, and Z-Axis Sensitivity   ±2 g  235,520  256,000  276,480  LSB/g
|     | ±4 g  | 117,760  128,000  | 138,240  | LSB/g  |
| --- | ----- | ----------------- | -------- | ------ |
|     | ±8 g  | 58,880  64,000    | 69,120   | LSB/g  |
X-Axis, Y-Axis, and Z-Axis Scale Factor   ±2 g    3.9    µg/LSB
|     | ±4 g  |   7.8   |     | µg/LSB  |
| --- | ----- | ------- | --- | ------- |
|     | ±8 g  |   15.6  |     | µg/LSB  |
Sensitivity Change due to Temperature  −40°C to +125°C    ±0.01    %/°C
| 0 g OFFSET                              | Each axis, ±2 g   |           |      |     |
| --------------------------------------- | ----------------- | --------- | ---- | --- |
| X-Axis, Y-Axis, and Z-Axis 0 g Output   |                   | −75  ±25  | +75  | mg  |
0 g Offset vs. Temperature (X-Axis, Y-Axis, and Z-Axis)1  −40°C to +125°C  −0.15  ±0.02  +0.15  mg/°C
| Repeatability2            | X-axis and y-axis                   |   ±3.5  |     | mg  |
| ------------------------- | ----------------------------------- | ------- | --- | --- |
|                           | Z-axis                              |   ±9    |     | mg  |
| Vibration Rectification3  |                                     |         |     | g   |
|                           | ±2 g range, in a 1 g orientation,   | <0.4    |     |     |
offset due to 2.5 g rms vibration
| NOISE DENSITY                   | ±2 g               |       |     |             |
| ------------------------------- | ------------------ | ----- | --- | ----------- |
| X-Axis, Y-Axis, and Z-Axis      |                    |   25  |     | µg/√Hz      |
| Velocity Random Walk            | X-axis and y-axis  |   9   |     | µm/sec/√Hr  |
|                                 | Z-axis             |   13  |     | µm/sec/√Hr  |
| OUTPUT DATA RATE AND BANDWIDTH  |                    |       |     |             |
Low-Pass Filter Passband Frequency  User programmable, Register 0x28  1    1000  Hz
High-Pass Filter Passband Frequency When Enabled  User programmable, Register 0x28  0.0095    10  Hz
| (Disabled by Default)  | for 4 kHz ODR  |     |     |     |
| ---------------------- | -------------- | --- | --- | --- |
Rev. 0 | Page 4 of 42

| Data Sheet  |     |     |     | ADXL354/ADXL355  |     |     |
| ----------- | --- | --- | --- | ---------------- | --- | --- |

| Parameter      |     | Test Conditions/Comments  | Min   | Typ  Max  |     | Unit  |
| -------------- | --- | ------------------------- | ----- | --------- | --- | ----- |
| SELF TEST      |     |                           |       |           |     |       |
| Output Change  |     |                           |       |           |     |       |
| X-Axis         |     |                           |       | 0.3       |     | g     |
| Y-Axis         |     |                           |       | 0.3       |     | g     |
| Z-Axis         |     |                           |       | 1.5       |     | g     |
| POWER SUPPLY   |     |                           |       |           |     |       |
| Voltage Range  |     |                           |       |           |     |       |
| V  Operating4  |     |                           | 2.25  | 2.5  3.6  |     | V     |
SUPPLY
| V    |     |     | V      | 2.5  3.6  |     | V   |
| ---- | --- | --- | ------ | --------- | --- | --- |
| DDIO |     |     | 1P8DIG |           |     |     |
V  and V  with Internal LDO Bypassed  V  = 0 V  1.62  1.8  1.98  V
| 1P8ANA 1P8DIG      |     | SUPPLY |     |        |     |     |
| ------------------ | --- | ------ | --- | ------ | --- | --- |
| Current            |     |        |     |        |     |     |
| Measurement Mode   |     |        |     |        |     |     |
| V  (LDO Enabled)   |     |        |     | 200    |     | µA  |
SUPPLY
| V 1P8ANA  (LDO Disabled)   |     |     |     | 160     |     | µA  |
| -------------------------- | --- | --- | --- | ------- | --- | --- |
| V  (LDO Disabled)          |     |     |     | 35.5    |     | µA  |
1P8DIG
| Standby Mode       |     |     |     |       |     |     |
| ------------------ | --- | --- | --- | ----- | --- | --- |
| V  (LDO Enabled)   |     |     |     | 21    |     | µA  |
SUPPLY
| V  (LDO Disabled)   |     |     |     | 7    |     | µA  |
| ------------------- | --- | --- | --- | ---- | --- | --- |
1P8ANA
| V 1P8DIG  (LDO Disabled)     |     |                       |      | 10       |     | µA      |
| ---------------------------- | --- | --------------------- | ---- | -------- | --- | ------- |
| Turn On Time5                |     | 2 g range             |      | <10      |     | ms      |
|                              |     | Power-off to standby  |      | <10      |     | ms      |
| TEMPERATURE SENSOR           |     |                       |      |          |     |         |
| Output at 25°C               |     |                       |      | 1852     |     | LSB     |
| Scale Factor                 |     |                       |      | −9.05    |     | LSB/°C  |
| TEMPERATURE                  |     |                       |      |          |     |         |
| Operating Temperature Range  |     |                       | −40  |   +125   |     | °C      |

1 The temperature change is −40°C to +25°C or +25°C to +125°C.
2 Repeatability is predicted for a 10 year life and includes shifts due to the HTOL (TA = 150°C, VSUPPLY = 3.6 V, and 1000 hours), temperature cycling (−55°C to +125°C and
1000 cycles), velocity random walk, broadband noise, and temperature hysteresis.
3 The VRE measurement is the shift in dc offset while the device is subject to 2.5 g rms random vibration from 50 Hz to 2 kHz. The DUT is configured for the ±2 g range
and an output data rate of 4 kHz. The VRE scales with the range setting.
4 When V1P8ANA and V1P8DIG are generated internally, VSUPPLY is valid. To disable the LDO and drive V1P8ANA and V1P8DIG externally, connect VSUPPLY to VSS.
5 Standby to measurement mode; valid when the output is within 1 mg of final value.

SPI DIGITAL INTERFACE CHARACTERISTICS FOR THE ADXL355
Note that multifunction pin names may be referenced by their relevant function only.
Table 3.
Parameter  Symbol  Test Conditions/Comments  Min  Typ  Max  Unit
| DC INPUT LEVELS    |        |                     |           |           |        |     |
| ------------------ | ------ | ------------------- | --------- | --------- | ------ | --- |
| Input Voltage      |        |                     |           |           |        |     |
| Low Level          | V IL   |                     |           |   0.3 × V | DDIO   | V   |
| High Level         | V      |                     | 0.7 × V   |           |        | V   |
|                    | IH     |                     | DDIO      |           |        |     |
| Input Current      |        |                     |           |           |        |     |
| Low Level          | I      | V  = 0 V            | −0.1      |           |        | µA  |
|                    | IL     | IN                  |           |           |        |     |
| High Level         | I      | V  = V              |           |   0.1     |        | µA  |
|                    | IH     | IN DDIO             |           |           |        |     |
| DC OUTPUT LEVELS   |        |                     |           |           |        |     |
| Output Voltage     |        |                     |           |           |        |     |
| Low Level          | V OL   | I OL  = I OL, MIN   |           |   0.2 × V | DDIO   | V   |
| High Level         | V      | I  = I              | 0.8 × V   |           |        | V   |
|                    | OH     | OH OH, MAX          | DDIO      |           |        |     |
| Output Current     |        |                     |           |           |        |     |
| Low Level          | I      | V  = V              | −10       |           |        | mA  |
|                    | OL     | OL OL, MAX          |           |           |        |     |
| High Level         | I OH   | V OH  = V OH, MIN   |           |   4       |        | mA  |
Rev. 0 | Page 5 of 42

| ADXL354/ADXL355  |     |     |     |     |     |     |     |     |     |     | Data Sheet |     |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---------- | --- |

Parameter  Symbol  Test Conditions/Comments  Min  Typ  Max  Unit
| AC INPUT LEVELS  |     |           |     |     |     |     |      |     |     |     |     |      |
| ---------------- | --- | --------- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | ---- |
| SCLK Frequency   |     |           |     |     |     |     | 0.1  |     |     | 10  |     | MHz  |
| SCLK High Time   |     | t HIGH    |     |     |     |     | 40   |     |     |     |     | ns   |
| SCLK Low Time    |     | t         |     |     |     |     | 40   |     |     |     |     | ns   |
LOW
| CS Setup Time  |     | t CSS    |     |     |     |     | 20  |     |     |     |     | ns  |
| -------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| CS Hold Time   |     | t        |     |     |     |     | 20  |     |     |     |     | ns  |
CSH
| CS Disable Time         |     | t CSD    |     |     |     |     | 40  |     |     |     |     | ns  |
| ----------------------- | --- | -------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Rising SCLK Setup Time  |     | t        |     |     |     |     | 20  |     |     |     |     | ns  |
SCLKS
| MOSI Setup Time  |     | t    |     |     |     |     | 20  |     |     |     |     | ns  |
| ---------------- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
SU
| MOSI Hold Time  |     | t    |     |     |     |     | 20  |     |     |     |     | ns  |
| --------------- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
HD
| AC OUTPUT LEVELS   |     |         |             |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | ------- | ----------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Propagation Delay  |     | t       | C  = 30 pF  |     |     |     |     |     |     | 30  |     | ns  |
|                    |     | P       | LOAD        |     |     |     |     |     |     |     |     |     |
| Enable MISO Time   |     | t EN    |             |     |     |     | 30  |     |     |     |     | ns  |
| Disable MISO Time  |     | t       |             |     |     |     |     |     |     | 20  |     | ns  |
DIS

t
CSD
CS
|     |       |     |     |     |        |       |     | t CSH |     | t     |     |     |
| --- | ----- | --- | --- | --- | ------ | ----- | --- | ----- | --- | ----- | --- | --- |
|     | t CSS |     |     |     | t HIGH | t LOW |     |       |     | SCLKS |     |     |
SCLK
t
|     |     |     | SU t HD |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | ------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
MOSI
|     |     |     |     |     |     | t   |     | t   |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | t   |     |     |     | P   |     | DIS |     |     |     |     |
EN
300-50241
MISO

Figure 3. SPI Interface Timing Diagram

I2C DIGITAL INTERFACE CHARACTERISTICS FOR THE ADXL355
Note that multifunction pin names may be referenced by their relevant function only.
Table 4.
    Test Conditions/  I2C_HS = 0 (Fast Mode)  I2C_HS = 1 (High Speed Mode)
Parameter  Symbol  Comments  Min  Typ  Max  Min  Typ  Max  Unit
| DC INPUT LEVELS  |        |     |     |         |      |     |              |         |      |           |      |      |
| ---------------- | ------ | --- | --- | ------- | ---- | --- | ------------ | ------- | ---- | --------- | ---- | ---- |
| Input Voltage    |        |     |     |         |      |     |              |         |      |           |      |      |
| Low Level        | V IL   |     |     |         |      |     | 0.3 × V DDIO |         |      |   0.3 × V | DDIO |   V  |
| High Level       | V      |     |     | 0.7 × V |      |     |              | 0.7 × V |      |           |      | V    |
|                  | IH     |     |     |         | DDIO |     |              |         | DDIO |           |      |      |
Hysteresis of Schmitt   V HYS     0.05 × V DDIO       0.1 × V DDIO       μA
Trigger Inputs
| Input Current  | I   | 0.1 × V |  < V  <   | −10  |     |     | +10  |     |     |     |     | μA  |
| -------------- | --- | ------- | --------- | ---- | --- | --- | ---- | --- | --- | --- | --- | --- |
|                | IL  |         | DDIO IN   |      |     |     |      |     |     |     |     |     |
|                |     | 0.9 × V |           |      |     |     |      |     |     |     |     |     |
DDIO
| DC OUTPUT LEVELS   |     |            |     |     |     |     |     |     |     |     |     |     |
| ------------------ | --- | ---------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Output Voltage     |     | I  = 3 mA  |     |     |     |     |     |     |     |     |     |     |
OL
| Low Level       | V OL1 |   V DD  > 2 V  |     |     |     |     | 0.4     |     |     |     |     | V   |
| --------------- | ----- | -------------- | --- | --- | --- | --- | ------- | --- | --- | --- | --- | --- |
|                 | V     |   V  ≤ 2 V     |     |     |     |     | 0.2 × V |     |     |     |     | V   |
|                 | OL2   | DD             |     |     |     |     | DDIO    |     |     |     |     |     |
| Output Current  |       |                |     |     |     |     |         |     |     |     |     |     |
| Low Level       | I     | V  = 0.4 V     |     | 20  |     |     |         |     |     |     |     | mA  |
|                 | OL    | OL             |     |     |     |     |         |     |     |     |     |     |
|                 |       | V  = 0.6 V     |     | 6   |     |     |         |     |     |     |     | mA  |
OL
Rev. 0 | Page 6 of 42

| Data Sheet  |     |     |     |     |     |     |     | ADXL354/ADXL355 |     |     |
| ----------- | --- | --- | --- | --- | --- | --- | --- | --------------- | --- | --- |

    Test Conditions/  I2C_HS = 0 (Fast Mode)  I2C_HS = 1 (High Speed Mode)
Parameter  Symbol  Comments  Min  Typ  Max  Min  Typ  Max  Unit
| AC INPUT LEVELS  |     |     |      |     |      |      |     |     |      |      |
| ---------------- | --- | --- | ---- | --- | ---- | ---- | --- | --- | ---- | ---- |
| SCLK Frequency   |     |     |      |     | 0    |   1  | 0   |     | 3.4  | MHz  |
| SCL High Time    |     | t   |      |     | 260  |      | 60  |     |      | ns   |
HIGH
| SCL Low Time      |     | t LOW    |      |     | 500  |     | 160  |     |     | ns  |
| ----------------- | --- | -------- | ---- | --- | ---- | --- | ---- | --- | --- | --- |
| Start Setup Time  |     | t        |      |     | 260  |     | 160  |     |     | ns  |
SUSTA
| Start Hold Time  |     | t   |      |     | 260  |     | 160  |     |     | ns  |
| ---------------- | --- | --- | ---- | --- | ---- | --- | ---- | --- | --- | --- |
HDSTA
| SDA Setup Time  |     | t   |     |     | 50  |     | 10  |     |     | ns  |
| --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
SUDAT
| SDA Hold Time  |     | t   |     |     | 0   |     | 0   |     |     | ns  |
| -------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
HDDAT
| Stop Setup Time  |     | t SUSTO |      |     | 260  |     | 160  |     |     | ns  |
| ---------------- | --- | ------- | ---- | --- | ---- | --- | ---- | --- | --- | --- |
| Bus Free Time    |     | t       |      |     | 500  |     |      |     |     | ns  |
BUF
| SCL Input Rise Time  |     | t RCL    |     |     |     |   120  |     |     | 80  | ns  |
| -------------------- | --- | -------- | --- | --- | --- | ------ | --- | --- | --- | --- |
| SCL Input Fall Time  |     | t        |     |     |     |   120  |     |     | 80  | ns  |
FCL
| SDA Input Rise Time  |     | t    |     |     |     |   120  |     |     | 160  | ns  |
| -------------------- | --- | ---- | --- | --- | --- | ------ | --- | --- | ---- | --- |
RDA
| SDA Input Fall Time  |     | t   |     |     |     |   120  |     |     | 160  | ns  |
| -------------------- | --- | --- | --- | --- | --- | ------ | --- | --- | ---- | --- |
FDA
Width of Spikes to   t   Not shown in Figure 4      50      10  ns
SP
Suppress
| AC OUTPUT LEVELS   |     |     |              |     |     |     |     |     |     |     |
| ------------------ | --- | --- | ------------ | --- | --- | --- | --- | --- | --- | --- |
| Propagation Delay  |     |     | C  = 500 pF  |     |     |     |     |     |     |     |
LOAD
| Data         |     | t VDDAT |      |     | 97  |   450  | 27  |     | 135  | ns  |
| ------------ | --- | ------- | ---- | --- | --- | ------ | --- | --- | ---- | --- |
| Acknowledge  |     | t       |      |     |     |   450  |     |     |      | ns  |
VDACK
Output Fall Time  t   F Not shown in Figure 4  20 × (V DD /5.5)    120        ns

|     |     | t   |     |     |     |     |     | t   | t   |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
|     |     | FDA |     |     |     |     |     | RDA | BUF |     |
SDA
|     | t             |     |       |       |     | t     |         |         | t     |     |
| --- | ------------- | --- | ----- | ----- | --- | ----- | ------- | ------- | ----- | --- |
|     | t SUSTA HDSTA |     |       |       |     | VDDAT | t VDACK | t SUSTO | SUSTA |     |
|     |               |     | t     | t     | t   | t     | t       |         |       |     |
|     |               |     | SUDAT | HDDAT | LOW | HIGH  | FCL     |         |       |     |
t RCL
|     |     |     |     |     |     | t VDDAT |     |     |     | 400-50241 |
| --- | --- | --- | --- | --- | --- | ------- | --- | --- | --- | --------- |
SCL

Figure 4. I2C Interface Timing Diagram

Rev. 0 | Page 7 of 42

| ADXL354/ADXL355  |     |     |     | Data Sheet |
| ---------------- | --- | --- | --- | ---------- |

ABSOLUTE MAXIMUM RATINGS
THERMAL RESISTANCE
Table 5.
Parameter  Rating  Thermal performance is directly linked to printed circuit board
(PCB) design and operating environment. Careful attention to
| Acceleration (Any Axis, 0.1 ms)  |     |     |     |     |
| -------------------------------- | --- | --- | --- | --- |
PCB thermal design is required.
| Unpowered                    | 5,000 g  |     |                              |           |
| ---------------------------- | -------- | --- | ---------------------------- | --------- |
| V SUPPLY , V DDIO            | 5.4 V    |     | Table 6. Thermal Resistance  |           |
| V , V  Configured as Inputs  | 1.98 V   |     |                              |           |
| 1P8ANA 1P8DIG                |          |     | Package Type                 | θ   Unit  |
JA
| ADXL354   |     |     | E-14-11   |     |
| --------- | --- | --- | --------- | --- |
42  °C/W
| Digital Inputs (RANGE, ST1, ST2, STBY)  | −0.3 V to V |  + 0.3 V  |                                                                         |     |
| --------------------------------------- | ----------- | --------- | ----------------------------------------------------------------------- | --- |
|                                         |             | DDIO      | 1 Thermal impedance simulated values are based on a JEDEC 2S2P thermal  |     |
Analog Outputs (X OUT , Y OUT , Z OUT , TEMP)   −0.3 V to V 1P8ANA  + 0.3 V  test board with four thermal vias. See JEDEC JESD51.
| ADXL355   |     |     |     |     |
| --------- | --- | --- | --- | --- |

| Digital Pins (CS, SCLK, MOSI, MISO,   | −0.3 V to V | DDIO  + 0.3 V  |     |     |
| ------------------------------------- | ----------- | -------------- | --- | --- |
ESD CAUTION
INT1, INT2, DRDY)
| Operating Temperature Range  | −40°C to +125°C  |     |     |     |
| ---------------------------- | ---------------- | --- | --- | --- |
| Storage Temperature Range    | −55°C to +150°C  |     |     |     |
Stresses at or above those listed under Absolute Maximum
Ratings may cause permanent damage to the product. This is a

stress rating only; functional operation of the product at these
or any other conditions above those indicated in the operational

section of this specification is not implied. Operation beyond

the maximum operating conditions for extended periods may
affect product reliability.

Rev. 0 | Page 8 of 42

Data Sheet  ADXL354/ADXL355

PIN CONFIGURATIONS AND FUNCTION DESCRIPTIONS

TUOZ TUOY TUOX
41 31 21
Y
|     |     |     | RANGE 1 |         | 11 VSUPPLY |     |     |     |
| --- | --- | --- | ------- | ------- | ---------- | --- | --- | --- |
|     |     |     | ST1 2   | ADXL354 | 10V1P8ANA  |     |     |     |
TOP VIEW
|     |     |     | ST2 3  | (Not to Scale) | 9 VSS     |     | X   |     |
| --- | --- | --- | ------ | -------------- | --------- | --- | --- | --- |
|     |     |     | TEMP 4 |                | 8 V1P8DIG |     |     |     |
Z
5 6 7
|     |     |     |     | OIDDV OISSV YBTS |     |     | 700-50241 |     |
| --- | --- | --- | --- | ---------------- | --- | --- | --------- | --- |

Figure 5. ADXL354 Pin Configuration

Table 7. ADXL354 Pin Function Descriptions
| Pin No.  | Mnemonic  | Description  |     |     |     |     |     |     |
| -------- | --------- | ------------ | --- | --- | --- | --- | --- | --- |
1  RANGE  Range Selection Pin. Set this pin to ground to select the ±2 g range, or set this pin to V DDIO  to select the ±4 g
or ±8 g range. This pin is model dependent (see the Ordering Guide section).
| 2   | ST1  | Self Test Pin 1. This pin enables self test mode.  |     |     |     |     |     |     |
| --- | ---- | -------------------------------------------------- | --- | --- | --- | --- | --- | --- |
3  ST2  Self Test Pin 2. This pin activates the electromechanical self test actuation.
| 4   | TEMP     | Temperature Sensor Output.         |     |     |     |     |     |     |
| --- | -------- | ---------------------------------- | --- | --- | --- | --- | --- | --- |
| 5   | V DDIO   | Digital Interface Supply Voltage.  |     |     |     |     |     |     |
| 6   | V        | Digital Ground.                    |     |     |     |     |     |     |
SSIO
7  STBY  Standby or Measurement Mode Selection Pin. Set this pin to ground to enter standby mode, or set this pin
to V  to enter measurement mode.
DDIO
8  V 1P8DIG   Digital Supply. This pin requires a decoupling capacitor. If V  connects to V , supply the voltage to this
SUPPLY SS
pin externally.
| 9   | V   | Analog Ground.  |     |     |     |     |     |     |
| --- | --- | --------------- | --- | --- | --- | --- | --- | --- |
SS
10  V 1P8ANA   Analog Supply. This pin requires a decoupling capacitor. If V SUPPLY  connects to V SS , supply the voltage to this
pin externally.
11  V   Supply Voltage. When V  equals 2.25 V to 3.6 V, V  enables the internal LDOs to generate V  and
|     | SUPPLY  |                 |        | SUPPLY     |                            | SUPPLY |     | 1P8DIG |
| --- | ------- | --------------- | ------ | ---------- | -------------------------- | ------ | --- | ------ |
|     |         | V . For V       |  = V   | , V  and V |  are externally supplied.  |        |     |        |
|     |         | 1P8ANA          | SUPPLY | SS 1P8DIG  | 1P8ANA                     |        |     |        |
| 12  | X OUT   | X-Axis Output.  |        |            |                            |        |     |        |
| 13  | Y       | Y-Axis Output.  |        |            |                            |        |     |        |
OUT
| 14  | Z OUT   | Z-Axis Output.  |     |     |     |     |     |     |
| --- | ------- | --------------- | --- | --- | --- | --- | --- | --- |

Rev. 0 | Page 9 of 42

| ADXL354/ADXL355  |     |     |     |     |     | Data Sheet |     |
| ---------------- | --- | --- | --- | --- | --- | ---------- | --- |

YDRD41
2TNI31 1TNI21
|     |     |            | CS/SCL 1  | 11 VSUPPLY | Y   |     |     |
| --- | --- | ---------- | --------- | ---------- | --- | --- | --- |
|     |     | SCLK/VSSIO | 2 ADXL355 | 10V1P8ANA  |     |     |     |
TOP VIEW
|     |     | MOSI/SDA  | 3 (Not to Scale) | 9 VSS     |     | X   |     |
| --- | --- | --------- | ---------------- | --------- | --- | --- | --- |
|     |     | MISO/ASEL | 4                | 8 V1P8DIG |     |     |     |
Z
|     |     |     | 5 6         | 7        |     |     |     |
| --- | --- | --- | ----------- | -------- | --- | --- | --- |
|     |     |     | OIDDV OISSV | DEVRESER |     |     |     |
600-50241

Figure 6. ADXL355 Pin Configuration

Table 8. ADXL355 Pin Function Descriptions
| Pin No.  | Mnemonic      | Description                                  |                 |     |     |     |     |
| -------- | ------------- | -------------------------------------------- | --------------- | --- | --- | --- | --- |
| 1        | CS/SCL        | Chip Select for SPI (CS).                    |                 |     |     |     |     |
|          |               | Serial Communications Clock for I2C (SCL).   |                 |     |     |     |     |
| 2        | SCLK/V SSIO   | Serial Communications Clock for SPI (SCLK).  |                 |     |     |     |     |
|          |               | Connect to V                                 |  for I2C (V ).  |     |     |     |     |
SSIO SSIO
| 3   | MOSI/SDA   | Master Output, Slave Input for SPI (MOSI).    |     |     |     |     |     |
| --- | ---------- | --------------------------------------------- | --- | --- | --- | --- | --- |
|     |            | Serial Data for I2C (SDA).                    |     |     |     |     |     |
| 4   | MISO/ASEL  | Master Input, Slave Output for SPI (MISO).    |     |     |     |     |     |
|     |            | Alternate I2C Address Select for I2C (ASEL).  |     |     |     |     |     |
| 5   | V          | Digital Interface Supply Voltage.             |     |     |     |     |     |
DDIO
| 6   | V SSIO   | Digital Ground.  |     |     |     |     |     |
| --- | -------- | ---------------- | --- | --- | --- | --- | --- |
7  RESERVED  Reserved. This pin can be connected to ground or left open.
8  V 1P8DIG   Digital Supply. This pin requires a decoupling capacitor. If V SUPPLY  connects to V SS , supply the voltage to this
pin externally.
| 9   | V   | Analog Ground.  |     |     |     |     |     |
| --- | --- | --------------- | --- | --- | --- | --- | --- |
SS
10  V 1P8ANA   Analog Supply. This pin requires a decoupling capacitor. If V SUPPLY  connects to V SS , supply the voltage to this
pin externally.
11  V   Supply Voltage. When V  equals 2.25 V to 3.6 V, V  enables the internal LDOs to generate V  and
|     | SUPPLY |                   | SUPPLY           |                            | SUPPLY |     | 1P8DIG |
| --- | ------ | ----------------- | ---------------- | -------------------------- | ------ | --- | ------ |
|     |        | V . For V         |  = V , V  and V  |  are externally supplied.  |        |     |        |
|     |        | 1P8ANA            | SUPPLY SS 1P8DIG | 1P8ANA                     |        |     |        |
| 12  | INT1   | Interrupt Pin 1.  |                  |                            |        |     |        |
| 13  | INT2   | Interrupt Pin 2.  |                  |                            |        |     |        |
| 14  | DRDY   | Data Ready Pin.   |                  |                            |        |     |        |

Rev. 0 | Page 10 of 42

| Data Sheet  |     |     |     |     | ADXL354/ADXL355  |     |     |
| ----------- | --- | --- | --- | --- | ---------------- | --- | --- |

TYPICAL PERFORMANCE CHARACTERISTICS
All figures include data for multiple devices and multiple lots, and they were taken in the ±2 g range, unless otherwise noted.
| 10  |     |     |     | 1   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
1
)g( TUOX
0.1
0.1
| 0.01 |                |      | 702-50241 | 0.01 |                |      |           |
| ---- | -------------- | ---- | --------- | ---- | -------------- | ---- | --------- |
| 10   | 100            | 1000 |           |      |                |      | 012-50241 |
|      |                |      |           | 10   | 100            | 1000 |           |
|      | FREQUENCY (Hz) |      |           |      |                |      |           |
|      |                |      |           |      | FREQUENCY (Hz) |      |           |
Figure 7. ADXL354 Frequency Response for X-Axis
Figure 10. ADXL355 Normalized Frequency Response for X-Axis at 4 kHz ODR

| 10  |     |     |     | 1   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
1
| )g( TUOY |     |     |     | )g( SIXA-Y |     |     |     |
| -------- | --- | --- | --- | ---------- | --- | --- | --- |
0.1
0.1
| 0.01 |                |      | 802-50241 |      |                |      |           |
| ---- | -------------- | ---- | --------- | ---- | -------------- | ---- | --------- |
| 10   | 100            | 1000 |           | 0.01 |                |      |           |
|      |                |      |           | 10   | 100            | 1000 | 112-50241 |
|      | FREQUENCY (Hz) |      |           |      |                |      |           |
|      |                |      |           |      | FREQUENCY (Hz) |      |           |
Figure 8. ADXL354 Frequency Response for Y-Axis
Figure 11. ADXL355 Normalized Frequency Response for Y-Axis at 4 kHz ODR

10
1
)g( TUOZ
)g( SIXA-Z
1
0.1
| 0.1 |                |      | 902-50241 |      |     |      |           |
| --- | -------------- | ---- | --------- | ---- | --- | ---- | --------- |
| 10  | 100            | 1000 |           |      |     |      |           |
|     |                |      |           | 0.01 |     |      | 212-50241 |
|     | FREQUENCY (Hz) |      |           | 10   | 100 | 1000 |           |
Figure 9. ADXL354 Frequency Response for Z-Axis  FREQUENCY (Hz)
  Figure 12. ADXL355 Normalized Frequency Response for Z-Axis at 4 kHz ODR

Rev. 0 | Page 11 of 42

| ADXL354/ADXL355  |     |     |     |     |     |     | Data Sheet  |
| ---------------- | --- | --- | --- | --- | --- | --- | ----------- |

| 15.00                   |     |     |     | 1.00                   |     |     |     |
| ----------------------- | --- | --- | --- | ---------------------- | --- | --- | --- |
| MAXIMUM CHANGE = 1.69mg |     |     |     | MAXIMUM CHANGE = 0.60% |     |     |     |
| AVERAGE CHANGE = 1.18mg |     |     |     | AVERAGE CHANGE = 0.34% |     |     |     |
10.00
)%( YTIVITISNES EVITALER
)gm( TESFFO EVITALER
0.50
5.00
| 0   |     |     |     | 0   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
–5.00
–0.50
| –9.75 |                  |     |               | –0.65 |                  |     |               |
| ----- | ---------------- | --- | ------------- | ----- | ---------------- | --- | ------------- |
| –45   | 5                | 55  | 105 312-50241 | –45   | 5                | 55  | 105 612-50241 |
|       | TEMPERATURE (°C) |     |               |       | TEMPERATURE (°C) |     |               |
Figure 13. ADXL354 X-Axis Zero g Offset Relative to 25°C vs. Temperature  Figure 16. ADXL354 X-Axis Sensitivity Relative to 25°C vs. Temperature
|       |     |     |     |      |     |     |     |
| ----- | --- | --- | --- | ---- | --- | --- | --- |
| 15.00 |     |     |     | 1.00 |     |     |     |
MAXIMUM CHANGE = 3.12mg
MAXIMUM CHANGE = 0.54%
| AVERAGE CHANGE = 1.85mg |     |     |     | AVERAGE CHANGE = 0.28% |     |     |     |
| ----------------------- | --- | --- | --- | ---------------------- | --- | --- | --- |
10.00
)%( YTIVITISNES EVITALER
)gm( TESFFO EVITALER
0.50
5.00
0
0
–5.00
–0.50
| –9.75 |                  |     | 412-50241 | –0.65 |                  |     | 712-50241 |
| ----- | ---------------- | --- | --------- | ----- | ---------------- | --- | --------- |
| –45   | 5                | 55  | 105       | –45   | 5                | 55  | 105       |
|       | TEMPERATURE (°C) |     |           |       | TEMPERATURE (°C) |     |           |
Figure 14. ADXL354 Y-Axis Zero g Offset Relative to 25°C vs. Temperature  Figure 17. ADXL354 Y-Axis Sensitivity Relative to 25°C vs. Temperature
|                         |     |     |     |                        |     |     |     |
| ----------------------- | --- | --- | --- | ---------------------- | --- | --- | --- |
| 15.00                   |     |     |     | 1.00                   |     |     |     |
| MAXIMUM CHANGE = 3.12mg |     |     |     | MAXIMUM CHANGE = 0.99% |     |     |     |
| AVERAGE CHANGE = 1.85mg |     |     |     | AVERAGE CHANGE = 0.51% |     |     |     |
10.00
| )gm( TESFFO EVITALER |     |     |     | )%( YTIVITISNES EVITALER |     |     |     |
| -------------------- | --- | --- | --- | ------------------------ | --- | --- | --- |
0.50
5.00
| 0   |     |     |     | 0   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
–5.00
–0.50
| –9.75 |                  |     |               | –0.65 |                  |     |           |
| ----- | ---------------- | --- | ------------- | ----- | ---------------- | --- | --------- |
| –45   | 5                | 55  | 105 512-50241 |       |                  |     | 812-50241 |
|       |                  |     |               | –40   | 10               | 60  | 110       |
|       | TEMPERATURE (°C) |     |               |       | TEMPERATURE (°C) |     |           |
Figure 15. ADXL354 Z-Axis Zero g Offset Relative to 25°C vs. Temperature  Figure 18. ADXL354 Z-Axis Sensitivity Relative to 25°C vs. Temperature
|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
Rev. 0 | Page 12 of 42

Data Sheet ADXL354/ADXL355
70
60
50
40
30
20
10
0
Rev. 0 | Page 13 of 42
570.0 070.0 560.0 060.0 550.0 050.0 540.0 040.0– 530.0– 030.0– 520.0– 020.0– 510.0– 010.0– 500.0– 0 500.0 010.0 510.0 020.0 520.0 030.0 530.0 040.0 540.0 050.0 550.0 060.0 560.0 070.0 570.0
ADXL354 2g OFFSET X-AXIS (g)
)tnuoC(
NIB
REP
STIH
912-50241
Figure 19. ADXL354 Zero g Offset Histogram at 25°C, X-Axis
80
70
60
50
40
30
20
10
0
570.0 070.0 560.0 060.0 550.0 050.0 540.0 040.0– 530.0– 030.0– 520.0– 020.0– 510.0– 010.0– 500.0– 0 500.0 010.0 510.0 020.0 520.0 030.0 530.0 040.0 540.0 050.0 550.0 060.0 560.0 070.0 570.0
ADXL354 2g OFFSETY-AXIS (g)
)tnuoC(
NIB
REP
STIH
022-50241
Figure 20. ADXL354 Zero g Offset Histogram at 25°C, Y-Axis
45
40
35
30
25
20
15
10
5
0
ADXL354 2g OFFSET Z-AXIS (g)
)tnuoC(
NIB
REP
STIH
122-50241
80
70
60
50
40
30
20
10
0
Figure 21. ADXL354 Zero g Offset Histogram at 25°C, Z-Axis
863.0 073.0 273.0 473.0 673.0 873.0 083.0 283.0 483.0 683.0 883.0 093.0 293.0 493.0 693.0 893.0 004.0 204.0 404.0 604.0 804.0 014.0 214.0 414.0 614.0 814.0 024.0 224.0 424.0 624.0 824.0 034.0 234.0
ADXL354 2g SENSITIVITY X-AXIS (V/g)
)tnuoC(
NIB
REP
STIH
222-50241
Figure 22. ADXL354 Sensitivity Histogram at 25°C, X-Axis
80
70
60
50
40
30
20
10
0
ADXL354 2g SENSITIVITYY-AXIS (V/g)
)tnuoC(
NIB
REP
STIH
863.0 073.0 273.0 473.0 673.0 873.0 083.0 283.0 483.0 683.0 883.0 093.0 293.0 493.0 693.0 893.0 004.0 204.0 404.0 604.0 804.0 014.0 214.0 414.0 614.0 814.0 024.0 224.0 424.0 624.0 824.0 034.0 234.0
322-50241
Figure 23. ADXL354 Sensitivity Histogram at 25°C, Y-Axis
70
60
50
40
30
20
10
0
573.0 773.0 973.0 183.0 383.0 583.0 783.0 983.0 193.0 393.0 593.0 793.0 993.0 104.0 304.0 504.0 704.0 904.0
ADXL354 2g SENSITIVITY Z-AXIS (V/g)
)tnuoC(
NIB
REP
STIH
863.0 073.0 273.0 473.0 673.0 873.0 614.0 814.0 024.0 224.0 424.0 624.0 824.0 034.0 234.0
422-50241
Figure 24. ADXL354 Sensitivity Histogram at 25°C, Z-Axis

| ADXL354/ADXL355  |     |     |     |     | Data Sheet  |     |
| ---------------- | --- | --- | --- | --- | ----------- | --- |

| 0.7              |                         |           | 0.68             |                         |     |           |
| ---------------- | ----------------------- | --------- | ---------------- | ----------------------- | --- | --------- |
| 0.6              |                         |           | 0.58             |                         |     |           |
| 0.5              |                         |           | 0.48             |                         |     |           |
| )g( TFIHS TESFFO |                         |           | )g( TFIHS TESFFO |                         |     |           |
| 0.4              |                         |           | 0.38             |                         |     |           |
| 0.3              |                         |           | 0.28             |                         |     |           |
| 0.2              |                         |           | 0.18             |                         |     |           |
| 0.1              |                         |           | 0.08             |                         |     |           |
| 0                |                         | 522-50241 | –0.02            |                         |     | 822-50241 |
| 0                | 1 2 3                   | 4         | 0                | 2 4 6                   | 8   | 10        |
|                  | INPUT VIBRATION (g rms) |           |                  | INPUT VIBRATION (g rms) |     |           |
Figure 25. ADXL354 Vibration Rectification Error (VRE),   Figure 28. ADXL354 Vibration Rectification Error (VRE),
X-Axis Offset from +1 g, ±2 g Range, X-Axis Orientation = −1 g   X-Axis Offset from +1 g, ±8 g Range, X-Axis Orientation = −1 g
0
0
–0.1
–0.1
–0.2
)g( TFIHS TESFFO –0.2
)g( TFIHS TESFFO
–0.3
–0.3
–0.4
–0.4
–0.5
–0.5
–0.6
–0.6
–0.7
| –0.7 |                         | 622-50241 | 0   | 2 4 6                   | 8   | 10 922-50241 |
| ---- | ----------------------- | --------- | --- | ----------------------- | --- | ------------ |
| 0    | 1 2 3                   | 4         |     |                         |     |              |
|      | INPUT VIBRATION (g rms) |           |     | INPUT VIBRATION (g rms) |     |              |

Figure 26. ADXL354 Vibration Rectification Error (VRE),   Figure 29. ADXL354 Vibration Rectification Error (VRE),
Y-Axis Offset from +1 g, ±2 g Range, Y-Axis Orientation = +1 g  Y-Axis Offset from +1 g, ±8 g Range, Y-Axis Orientation = +1 g
| 0                |                         |             | 0                |                         |     |           |
| ---------------- | ----------------------- | ----------- | ---------------- | ----------------------- | --- | --------- |
| –0.1             |                         |             | –0.1             |                         |     |           |
| –0.2             |                         |             | –0.2             |                         |     |           |
| )g( TFIHS TESFFO |                         |             | )g( TFIHS TESFFO |                         |     |           |
| –0.3             |                         |             | –0.3             |                         |     |           |
| –0.4             |                         |             | –0.4             |                         |     |           |
| –0.5             |                         |             | –0.5             |                         |     |           |
| –0.6             |                         |             | –0.6             |                         |     |           |
| –0.7             |                         |             | –0.7             |                         |     |           |
| 0                | 1 2 3                   | 4 722-50241 |                  |                         |     | 032-50241 |
|                  |                         |             | 0                | 2 4 6                   | 8   | 10        |
|                  | INPUT VIBRATION (g rms) |             |                  | INPUT VIBRATION (g rms) |     |           |
Figure 27. ADXL354 Vibration Rectification Error (VRE),   Figure 30. ADXL354 Vibration Rectification Error (VRE),
Z-Axis Offset from +1 g, ±2 g Range, Z-Axis Orientation = +1 g  Z-Axis Offset from +1 g, ±8 g Range, Z-Axis Orientation = +1 g
Rev. 0 | Page 14 of 42

| Data Sheet  |     |     |     |     |     | ADXL354/ADXL355  |     |
| ----------- | --- | --- | --- | --- | --- | ---------------- | --- |

| 15.00                 |     |     |     | 1.00                   |     |     |     |
| --------------------- | --- | --- | --- | ---------------------- | --- | --- | --- |
| MAXIMUM DELTA = 6.5mg |     |     |     | MAXIMUM CHANGE = 0.78% |     |     |     |
| AVERAGE DELTA = 1.7mg |     |     |     | AVERAGE CHANGE = 0.72% |     |     |     |
10.00
)%( YTIVITISNES EVITALER
)gm( TESFFO EVITALER
0.50
5.00
| 0   |     |     |     | 0   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
–5.00
–0.50
| –9.75 |                  |     |               | –0.65 |                  |     |               |
| ----- | ---------------- | --- | ------------- | ----- | ---------------- | --- | ------------- |
| –45   | 5                | 55  | 105 132-50241 | –45   | 5                | 55  | 105 432-50241 |
|       | TEMPERATURE (°C) |     |               |       | TEMPERATURE (°C) |     |               |
|       |                  |     |               |       |                  |     |               |
Figure 31. ADXL355 X-Axis Zero g Offset Relative to 25°C vs. Temperature  Figure 34. ADXL355 X-Axis Sensitivity Relative to 25°C vs. Temperature
|                       |     |     |     |                        |     |     |     |
| --------------------- | --- | --- | --- | ---------------------- | --- | --- | --- |
| 15.00                 |     |     |     | 1.00                   |     |     |     |
| MAXIMUM DELTA = 3.2mg |     |     |     | MAXIMUM CHANGE = 0.78% |     |     |     |
AVERAGE CHANGE = 0.72%
AVERAGE DELTA = 1.4mg
10.00
)%( YTIVITSNES EVITALER
)gm( TESFFO EVITALER
0.50
5.00
0
0
–5.00
–0.50
| –9.75 |                  |     | 232-50241 | –0.65 |                  |     | 532-50241 |
| ----- | ---------------- | --- | --------- | ----- | ---------------- | --- | --------- |
| –45   | 5                | 55  | 105       | –45   | 5                | 55  | 105       |
|       | TEMPERATURE (°C) |     |           |       | TEMPERATURE (°C) |     |           |
Figure 32. ADXL355 Y-Axis Zero g Offset Relative to 25°C vs. Temperature  Figure 35. ADXL355 Y-Axis Sensitivity Relative to 25°C vs. Temperature
|                        |     |     |     |                        |     |     |     |
| ---------------------- | --- | --- | --- | ---------------------- | --- | --- | --- |
| 15.00                  |     |     |     | 1.00                   |     |     |     |
| MAXIMUM DELTA = 10.6mg |     |     |     | MAXIMUM CHANGE = 0.47% |     |     |     |
| AVERAGE DELTA = 5.3mg  |     |     |     | AVERAGE CHANGE = 0.3%  |     |     |     |
10.00
| )gm( TESFFO EVITALER |     |     |     | )%( YTIVITSNES EVITALER |     |     |     |
| -------------------- | --- | --- | --- | ----------------------- | --- | --- | --- |
0.50
5.00
| 0   |     |     |     | 0   |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |
–5.00
–0.50
| –9.75 |     |     |               | –0.65 |     |     |               |
| ----- | --- | --- | ------------- | ----- | --- | --- | ------------- |
| –45   | 5   | 55  | 105 332-50241 | –45   | 5   | 55  | 105 632-50241 |
TEMPERATURE (°C)
|     |     |     |     |     | TEMPERATURE (°C) |     |     |
| --- | --- | --- | --- | --- | ---------------- | --- | --- |
Figure 33. ADXL355 Z-Axis Zero g Offset Relative to 25°C vs. Temperature  Figure 36. ADXL355 Z-Axis Sensitivity Relative to 25°C vs. Temperature

Rev. 0 | Page 15 of 42

ADXL354/ADXL355 Data Sheet
Rev. 0 | Page 16 of 42
732-50241
80
70
60
50
40
30
20
10
0
)tnuoC(
NIB
REP
STIH
57– 96– 36– 75– 15– 54– 93– 33– 72– 12– 51– 9– 3– 3 9 51 12 72 33 93 54 15 75 36 96 57
OFFSET (mg)
Figure 37. ADXL355 Zero g Offset Histogram at 25°C, X-Axis
)tnuoC(
NIB
REP
STIH
832-50241
80
70
60
50
40
30
20
10
0 57– 96– 36– 75– 15– 54– 93– 33– 72– 12– 51– 9– 3– 3 9 51 12 72 33 93 54 15 75 36 96 57
OFFSET (mg)
Figure 38. ADXL355 Zero g Offset Histogram at 25°C, Y-Axis
932-50241
45
40
35
30
25
20
15
10
5
0
)tnuoC(
NIB
REP
STIH
57– 96– 36– 75– 15– 54– 93– 33– 72– 12– 51– 9– 3– 3 9 51 12 72 33 93 54 15 75 36 96 57
OFFSET (mg)
Figure 39. ADXL355 Zero g Offset Histogram at 25°C, Z-Axis
042-50241
60
50
40
30
20
10
0
)tnuoC(
NIB
REP
STIH
025532 851732 797832 534042 470242 217342 053542 989642 726842 662052 409152 245352 181552 918652 854852 690062 437162 373362 110562 056662 882862 629962 565172 302372 248472 084672
SENSITIVITY (lsb/g)
Figure 40. ADXL355 Sensitivity Histogram at 25°C, X-Axis
)tnuoC(
NIB
REP
STIH
142-50241
60
50
40
30
20
10
0
SENSITIVITY (LSB/g)
025532 851732 797832 534042 470242 217342 053542 989642 726842 662052 409152 245352 181552 918652 854852 690062 437162 373362 110562 056662 882862 629962 565172 302372 248472 084672
Figure 41. ADXL355 Sensitivity Histogram at 25°C, Y-Axis
)tnuoC(
NIB
REP
STIH
242-50241
SENSITIVITY (LSB/g)
025532 851732 797832 534042 470242 217342 053542 989642 726842 662052 409152 245352 181552 918652 854852 690062 437162 373362 110562 056662 882862 629962 565172 302372 248472 084672
60
50
40
30
20
10
0
Figure 42. ADXL355 Sensitivity Histogram at 25°C, Z-Axis

Data Sheet  ADXL354/ADXL355

| 0.7                   |     |     | 0.68 |     |     |     |
| --------------------- | --- | --- | ---- | --- | --- | --- |
| 0.6                   |     |     | 0.58 |     |     |     |
| )g( EGNAHC TESFFO 0.5 |     |     | 0.48 |     |     |     |
)g( TFIHS TESFFO
| 0.4 |                         |           | 0.38  |                         |     |           |
| --- | ----------------------- | --------- | ----- | ----------------------- | --- | --------- |
| 0.3 |                         |           | 0.28  |                         |     |           |
| 0.2 |                         |           | 0.18  |                         |     |           |
| 0.1 |                         |           | 0.08  |                         |     |           |
| 0   |                         | 342-50241 | –0.02 |                         |     | 642-50241 |
| 0   | 1 2 3                   | 4         | 0     | 2 4 6                   | 8   | 10        |
|     | INPUT VIBRATION (g rms) |           |       | INPUT VIBRATION (g rms) |     |           |
Figure 43. ADXL355 Vibration Rectification Error (VRE),   Figure 46. ADXL355 Vibration Rectification Error (VRE),
X-Axis Offset from +1 g, ±2 g Range, X-Axis Orientation = −1 g   X-Axis Offset from +1 g, ±8 g Range, X-Axis Orientation = −1 g
0
0
–0.1
–0.1
)g( EGNAHC TESFFO –0.2
)g( TFIHS TESFFO –0.2
–0.3
–0.3
| –0.4 |                         |           | –0.4 |                         |     |           |
| ---- | ----------------------- | --------- | ---- | ----------------------- | --- | --------- |
| –0.5 |                         |           | –0.5 |                         |     |           |
| –0.6 |                         |           | –0.6 |                         |     |           |
| –0.7 |                         | 442-50241 | –0.7 |                         |     | 742-50241 |
| 0    | 1 2 3                   | 4         | 0    | 2 4 6                   | 8   | 10        |
|      | INPUT VIBRATION (g rms) |           |      | INPUT VIBRATION (g rms) |     |           |
Figure 44. ADXL355 Vibration Rectification Error (VRE),   Figure 47. ADXL355 Vibration Rectification Error (VRE),
Y-Axis Offset from +1 g, ±2 g Range, Y-Axis Orientation = +1 g  Y-Axis Offset from +1 g, ±8 g Range, Y-Axis Orientation = +1 g
| 0                      |     |     | 0    |     |     |     |
| ---------------------- | --- | --- | ---- | --- | --- | --- |
| –0.1                   |     |     | –0.1 |     |     |     |
| )g( EGNAHC TESFFO –0.2 |     |     | –0.2 |     |     |     |
)g( TFIHS TESFFO
| –0.3 |                         |           | –0.3 |                         |     |              |
| ---- | ----------------------- | --------- | ---- | ----------------------- | --- | ------------ |
| –0.4 |                         |           | –0.4 |                         |     |              |
| –0.5 |                         |           | –0.5 |                         |     |              |
| –0.6 |                         |           | –0.6 |                         |     |              |
| –0.7 |                         | 542-50241 | –0.7 |                         |     |              |
| 0    | 1 2 3                   | 4         | 0    | 2 4 6                   | 8   | 10 842-50241 |
|      | INPUT VIBRATION (g rms) |           |      | INPUT VIBRATION (g rms) |     |              |

Figure 45. ADXL355 Vibration Rectification Error (VRE),
Figure 48. ADXL355 Vibration Rectification Error (VRE),
Z-Axis Offset from +1 g, ±2 g Range, Z-Axis Orientation = +1 g   Z-Axis Offset from +1 g, ±8 g Range, Z-Axis Orientation = +1 g
Rev. 0 | Page 17 of 42

| ADXL354/ADXL355  |     |     |     |     |     |     |     |     | Data Sheet  |     |     |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | --- | ----------- | --- | --- |

| 1.35 |     |     |     | 0.006 |     | )BSL( TUPTUO ROSNES ERUTAREPMET 553LXDA 2300 |     |     |     | 6   |     |
| ---- | --- | --- | --- | ----- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
)V( TUPTUO ROSNES ERUTAREPMET 453LXDA TEMPERATURE SENSOR OUTPUT
LINEARITY
2100
1.25 0.004 ROSNES ERUTAREPMET 453LXDA 4 ROSNES ERUTAREPMET 553LXDA
|      |     |     |     |       |                    | 1900 |     |     |     |     | )BSL( TESFFO RAENIL  |
| ---- | --- | --- | --- | ----- | ------------------ | ---- | --- | --- | --- | --- | -------------------- |
|      |     |     |     |       | )V( TESFFO RAENIL  |      |     |     |     | 2   |                      |
| 1.15 |     |     |     | 0.002 |                    |      |     |     |     |     |                      |
1700
0
| 1.05 |     |     |     | 0   |     | 1500 |     |     |     |     |     |
| ---- | --- | --- | --- | --- | --- | ---- | --- | --- | --- | --- | --- |
–2
| 0.95 |     |     |     | –0.002 |     | 1300 |     |     |     |     |     |
| ---- | --- | --- | --- | ------ | --- | ---- | --- | --- | --- | --- | --- |
–4
1100
| 0.85 |     |     |     | –0.004 |     |     |     |     |     |     |     |
| ---- | --- | --- | --- | ------ | --- | --- | --- | --- | --- | --- | --- |
–6
|      |                  |     |     |        |           | 900 TEMPERATURE SENSOR OUTPUT |                  |     |     |     |           |
| ---- | ---------------- | --- | --- | ------ | --------- | ----------------------------- | ---------------- | --- | --- | --- | --------- |
|      |                  |     |     |        |           | LINEARITY                     |                  |     |     |     | 052-50241 |
| 0.75 |                  |     |     | –0.006 | 942-50241 | 700                           |                  |     |     | –8  |           |
| –40  | 10               | 60  | 110 |        |           | –40                           | 10               | 60  | 110 |     |           |
|      | TEMPERATURE (°C) |     |     |        |           |                               | TEMPERATURE (°C) |     |     |     |           |
Figure 49. ADXL354 Temperature Sensor Output and Linearity Offset vs.  Figure 52. ADXL355 Temperature Sensor Output and Linearity Offset vs.
|     | Temperature   |     |     |     |     |     | Temperature   |     |     |     |     |
| --- | ------------- | --- | --- | --- | --- | --- | ------------- | --- | --- | --- | --- |
| 80  |               |     |     |     |     | 100 |               |     |     |     |     |
| 70  |               |     |     |     |     | 90  |               |     |     |     |     |
80
60
| )tnuoC( NIB REP STIH |     |     |     |     |     | )tnuoC( NIB REP STIH 70 |     |     |     |     |     |
| -------------------- | --- | --- | --- | --- | --- | ----------------------- | --- | --- | --- | --- | --- |
50
60
| 40  |     |     |     |     |     | 50  |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
40
30
30
20
20
| 10  |     |     |     |     |           | 10  |     |     |     |     |           |
| --- | --- | --- | --- | --- | --------- | --- | --- | --- | --- | --- | --------- |
|     |     |     |     |     | 152-50241 | 0   |     |     |     |     | 352-50241 |
0 125 129 133 137 141 145 149 153 157 161 165 169 173 180 184 188 192 196 200 204 208 212 216 220 224 228
|     | TOTAL SUPPLY CURRENT (µA) |     |     |     |     |     | TOTAL SUPPLY CURRENT (µA) |     |     |     |     |
| --- | ------------------------- | --- | --- | --- | --- | --- | ------------------------- | --- | --- | --- | --- |
Figure 50. ADXL354 Total Supply Current, 3.3 V  Figure 53. ADXL355 Total Supply Current, 3.3 V
|     |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 35  |     |     |     |     |     |     |     |     |     |     |     |

30

)tnuoC( NIB REP STIH 25

20

| 15  |     |     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 10  |     |     |     |     |     |     |     |     |     |     |     |

5

| 0         |                              |           |                | 252-50241 |     |     |     |     |     |     |     |
| --------- | ---------------------------- | --------- | -------------- | --------- | --- | --- | --- | --- | --- | --- | --- |
| 3800 3840 | 3880 3920 3960               | 4000 4040 | 4080 4120 4160 | 4200      |     |     |     |     |     |     |     |
|           | ADXL355 CLOCK FREQUENCY (Hz) |           |                |           |     |     |     |     |     |     |     |

Figure 51. ADXL355 Internal Clock Frequency Histogram

Rev. 0 | Page 18 of 42

Data Sheet ADXL354/ADXL355
ROOT ALLAN VARIANCE (RAV) ADXL355 CHARACTERISTICS
All figures include data for multiple devices and multiple lots, and they were taken in the ±2 g range, unless otherwise noted.
1000
100
10
1
0.01 0.1 1 10 100 1000
Rev. 0 | Page 19 of 42
)gµ(
VAR
INTEGRATION TIME (Seconds)
452-50241
Figure 54. ADXL355 Root Allan Variance (RAV), X-Axis
1000
100
10
1
0.01 0.1 1 10 100 1000
)gµ(
VAR
INTEGRATION TIME (Seconds)
552-50241
1000
100
10
1
0.01 0.1 1 10 100 1000
Figure 55. ADXL355 Root Allan Variance (RAV), Y-Axis
)gµ(
VAR
INTEGRATION TIME (Seconds)
652-50241
Figure 56. ADXL355 Root Allan Variance (RAV), Z-Axis

ADXL354/ADXL355 Data Sheet
THEORY OF OPERATION
The ADXL354 is a complete 3-axis, ultralow noise and ultrastable ANALOG OUTPUT
offset MEMS accelerometer with outputs ratiometric to the analog
Figure 57 shows the ADXL354 application circuit. The analog
1.8 V supply, V . The ADXL355 adds three high resolution
1P8ANA outputs (X , Y , and Z ) are ratiometric to the 1.8 V
OUT OUT OUT
ADCs that use the analog 1.8 V supply as a reference to provide
analog voltage from the V pin. V can be powered
1P8ANA 1P8ANA
digital outputs insensitive to the supply voltage. The ADXL354B
with an on-chip LDO that is powered from V . V can
SUPPLY 1P8ANA
is pin selectable for ±2 g or ±4 g full scale, the ADXL354C is pin
also be supplied externally by forcing V to V , which
SUPPLY SS
selectable for ±2 g or ±8 g full scale, and the ADXL355 is
disables the LDO. Due to the ratiometric response, the analog
programmable for ±2.048 g, ±4.096 g, and ±8.192 g full scale.
output requires referencing to the V supply when
1P8ANA
The ADXL355 offers both SPI and I2C communications ports.
digitizing to achieve the inherent noise and offset performance
The micromachined, sensing elements are fully differential, of the ADXL354. The 0 g bias output is nominally equal to
comprising the lateral x-axis and y-axis sensors and the vertical, V /2. The recommended option is to use the ADXL354
1P8ANA
teeter totter z-axis sensors. The x-axis and y-axis sensors and with a ratiometric ADC (for example, the Analog Devices, Inc.,
the z-axis sensors go through separate signal paths that minimize AD7682) with V providing the voltage reference. This
1P8ANA
offset drift and noise. The signal path is fully differential, except configuration results in self cancellation of errors due to minor
for a differential to single-ended conversion at the analog supply variations.
outputs of the ADXL354.
The ADXL354 outputs two forms of filtering: internal anti-
The analog accelerometer outputs of the ADXL354 are ratiometric aliasing filtering with a cutoff frequency of approximately 1.5 kHz,
to V 1P8ANA ; therefore, carefully digitize them correctly. The and external filtering. The external filter uses a fixed, on-chip,
temperature sensor output is not ratiometric. The X OUT , Y OUT , 32 kΩ resistance in series with each output in conjunction with
and Z analog outputs are filtered internally with an anti- the external capacitors to implement the low-pass filter antialiasing
OUT
aliasing filter. These analog outputs also have an internal 32 kΩ and noise reduction prior to the external ADC. The antialias
series resistor that can be used with an external capacitor to set filter cutoff frequency must be significantly higher than the
the bandwidth of the output. desired signal bandwidth. If the antialias filter corner is too low,
ratiometricity can be degraded where the signal attenuation is
The ADXL355 includes antialias filters before and after the high
different than the reference attenuation.
resolution Σ-Δ ADC. User-selectable output data rates and filter
corners are provided. The temperature sensor is digitized with a
12-bit successive approximation register (SAR) ADC.
VDDIO (±4g, ±8g)
GND ( ± 2g)
RANGE 11VSUPPLY
ST1
10V1P8ANA ADC VREF
ST2
ADXL354 9 VSS
TEMP
V1P8DIG
VDDIO (MEASUREMENT)
GND (STANDBY)
Rev. 0 | Page 20 of 42
TUOZ41 TUOY31 TUOX21
1
2
3
8
5
OIDDV
6
OISSV
7
YBTS
2.25VTO 3.6V
0.1µF 1µF
0.1µF 1µF
4
1µF 1µF
2.25VTO 3.6V
0.1µF 0.1µF
220-50241
Figure 57. ADXL354 Application Circuit

Data Sheet ADXL354/ADXL355
DIGITAL OUTPUT AXES OF ACCELERATION SENSITIVITY
Figure 59 shows the ADXL355 application circuit with the Figure 58 shows the axes of acceleration sensitivity. Note that
recommended bypass capacitors. The communications interface the output voltage increases when accelerated along the
is either SPI or I2C (see the Serial Communications section for sensitive axis.
additional information). Z
The ADXL355 includes an internal configurable digital band- Y
pass filter. Both the high-pass and low-pass poles of the filter
are adjustable, as detailed in the Filter Settings Register section
and Table 43. At power-up, the default conditions for the filters
are as follows:
 High-pass filter (HPF) = dc (off)
 Low-pass filter (LPF) = 1000 Hz
 Output data rate = 4000 Hz
X
Rev. 0 | Page 21 of 42
500-50241
Figure 58. Axes of Acceleration Sensitivity
11 VSUPPLY
10V1P8ANA
ADXL355
TOP VIEW 9 VSS
(Not to Scale)
V1P8DIG
YDRD
41
2TNI
31
1TNI
21
1
2
3
8
5
OIDDV
6
OISSV
7
DEVRESER
2.25VTO 3.6V
0.1µF 1µF
0.1µF 1µF
4
1µF 1µF
2.25VTO 3.6V
0.1µF 0.1µF
C2I/IPS
ECAFRETNI
120-50241
CS/SCL
SCLK/VSSIO
MOSI/SDA
MISO/ASEL
Figure 59. ADXL355 Application Circuit

| ADXL354/ADXL355  |     |     |     |     |     | Data Sheet  |     |
| ---------------- | --- | --- | --- | --- | --- | ----------- | --- |

| POWER SEQUENCING  |     |     |     |     | V   |     |     |
| ----------------- | --- | --- | --- | --- | --- | --- | --- |
DDIO
The V  value determines the logic high levels. On the analog
| There are two methods for applying power to the device.  |     |     |     |     | DDIO |     |     |
| -------------------------------------------------------- | --- | --- | --- | --- | ---- | --- | --- |
Typically, internal LDO regulators generate the 1.8 V power for  output ADXL354, V DDIO  sets the logic high level for the self test
pins, ST1 and ST2, as well as the STBY pin. On the digital output
| the analog and digital supplies, V |     | 1P8ANA  and V | 1P8DIG , respectively.  |     |     |     |     |
| ---------------------------------- | --- | ------------- | ----------------------- | --- | --- | --- | --- |
Optionally, connecting V  to V  and driving V  and  ADXL355, V DDIO  sets the logic high level for communications
|     |     | SUPPLY SS | 1P8ANA |     |     |     |     |
| --- | --- | --------- | ------ | --- | --- | --- | --- |
V  with an external supply can supply V  and V .  interface ports, as well as the interrupt and DRDY outputs.
| 1P8DIG |     | 1P8ANA | 1P8DIG |     |     |     |     |
| ------ | --- | ------ | ------ | --- | --- | --- | --- |
When using the internal LDO regulators, connect V SUPPLY  to a  The LDO regulators are operational when V SUPPLY  is between
voltage source between 2.25 V to 3.6 V. In this case, V  and  2.25 V and 3.6 V. V  and V  are the regulator outputs in
|     |     |     | DDIO |     | 1P8ANA 1P8DIG |     |     |
| --- | --- | --- | ---- | --- | ------------- | --- | --- |
V  can be powered in parallel. V  must not exceed the  this mode. Alternatively, when tying V  to V , V  and
| SUPPLY |     | SUPPLY |     |     |     | SUPPLY | SS 1P8ANA |
| ------ | --- | ------ | --- | --- | --- | ------ | --------- |
V DDIO  voltage by greater than 0.5 V. If necessary, V DDIO  can be  V 1P8DIG  are supply voltage inputs with a 1.62 V to 1.98 V range.
| powered before V | .      |     |     |     |                       |     |     |
| ---------------- | ------ | --- | --- | --- | --------------------- | --- | --- |
|                  | SUPPLY |     |     |     | OVERRANGE PROTECTION  |     |     |
When disabling the internal LDO regulators and using an external  To avoid electrostatic capture of the proof mass when the
| 1.8 V supply to power V |     |  and V , tie V |  to ground,  |     |     |     |     |
| ----------------------- | --- | -------------- | ------------ | --- | --- | --- | --- |
1P8ANA 1P8DIG SUPPLY accelerometer is subject to input acceleration beyond its full-
| and set V |  and V |  to the same final voltage level. In the  |     |     |     |     |     |
| --------- | ------ | ----------------------------------------- | --- | --- | --- | --- | --- |
1P8ANA 1P8DIG scale range, all sensor drive clocks turn off for 0.5 ms. In the
case of bypassing the LDOs, the recommended power sequence is
±2 g/±2.048 g range setting, the overrange protection activates
| to apply power to V | , followed by applying power to V |     |     |     |     |     |     |
| ------------------- | --------------------------------- | --- | --- | --- | --- | --- | --- |
DDIO 1P8DIG for input signals beyond approximately ±8 g/±8.192 g (±25%),
approximately 10 µs later, and then applying power to V 1P8ANA   and for the ±4 g/±4.096 g and ±8 g/±8.192 g range setting, the
| approximately 10 µs later. If necessary, V |     |        |  and V  can be  |     |                                                |     |     |
| ------------------------------------------ | --- | ------ | --------------- | --- | ---------------------------------------------- | --- | --- |
|                                            |     | 1P8DIG | DDIO            |     | threshold corresponds to about ±16 g (±25%).   |     |     |
powered from the same 1.8 V supply, which can also be tied to
|     |     |     |     |     | When overrange protection occurs, the X | , Y | , and Z  pins  |
| --- | --- | --- | --- | --- | --------------------------------------- | --- | -------------- |
V  with proper isolation. In this case, proper decoupling  OUT OUT OUT
1P8ANA
and low frequency isolation is important to maintain the noise  on the ADXL354 begin to drive to midscale. The ADXL355
floats toward zero, and first in, first out (FIFO) begins filling
performance of the sensor.
with this data.
POWER SUPPLY DESCRIPTION
SELF TEST
The ADXL354/ADXL355 have four different power supply
The ADXL354 and ADXL355 incorporate a self test feature
| domains: V | SUPPLY , V 1P8ANA | , V 1P8DIG , and V DDIO . The internal  |     |     |     |     |     |
| ---------- | ----------------- | --------------------------------------- | --- | --- | --- | --- | --- |
that effectively tests their mechanical and electronic systems
analog and digital circuitry operates at 1.8 V nominal.
|     |     |     |     |     | simultaneously. In ADXL354, drive the ST1 pin to V |     | DDIO  to  |
| --- | --- | --- | --- | --- | -------------------------------------------------- | --- | --------- |
V
SUPPLY invoke self test mode. Then, by driving the ST2 pin to V ,
DDIO
V  is 2.25 V to 3.6 V, which is the input range to the two
SUPPLY the ADXL354 applies an electrostatic force to the mechanical
LDO regulators that generate the nominal 1.8 V outputs for  sensor and induces a change in output in response to the force.
| V  and V | . Connect V |  to V  to disable the LDO  |     |     |     |     |     |
| -------- | ----------- | -------------------------- | --- | --- | --- | --- | --- |
1P8ANA 1P8DIG SUPPLY SS The self test delta (or response) is the difference in output
regulators, which allows driving V 1P8ANA  and V 1P8DIG  from an  voltages between when ST2 is high and ST2 is low, both when
external source.  ST1 is asserted. After the self test measurement is complete,
| V   |     |     |     |     | bring both pins low to resume normal operation.  |     |     |
| --- | --- | --- | --- | --- | ------------------------------------------------ | --- | --- |
1P8ANA
All sensor and analog signal processing circuitry operates in  The self test operation is similar in the ADXL355, except ST1
and ST2 can be accessed through the SELF_TEST register
this domain. Offset and sensitivity of the analog output
ADXL354 are ratiometric to this supply voltage. When using  (Register 0x2E).
external ADCs, use V 1P8ANA  as the reference voltage. The digital  The self test feature rejects externally applied acceleration and
| output ADXL355 includes ADCs that are ratiometric to V |     |     |     | ,      |                                                                 |     |     |
| ------------------------------------------------------ | --- | --- | --- | ------ | --------------------------------------------------------------- | --- | --- |
|                                                        |     |     |     | 1P8ANA | only responds to the self test force, which allows an accurate  |     |     |
thereby rendering offset and sensitivity insensitive to the value  measurement of the self test, even in the presence of external
of V . V  can be an input or an output as defined by the  mechanical noise.
| 1P8ANA         | 1P8ANA      |     |     |     |     |     |     |
| -------------- | ----------- | --- | --- | --- | --- | --- | --- |
| state of the V |  voltage.   |     |     |     |     |     |     |
SUPPLY

V
1P8DIG

V 1P8DIG  is the supply voltage for the internal logic circuitry. A

separate LDO regulator decouples the digital supply noise from

| the analog signal path. V            |     | 1P8ANA  can be an input or an output as  |             |     |     |     |     |
| ------------------------------------ | --- | ---------------------------------------- | ----------- | --- | --- | --- | --- |
| defined by the state of the V        |     |  voltage. If driven externally,          |             |     |     |     |     |
|                                      |     | SUPPLY                                   |             |     |     |     |     |
| V  must be the same voltage as the V |     |                                          |  voltage.   |     |     |     |     |
| 1P8DIG                               |     | 1P8ANA                                   |             |     |     |     |     |

Rev. 0 | Page 22 of 42

| Data Sheet  |     |     |     |     |     | ADXL354/ADXL355 |
| ----------- | --- | --- | --- | --- | --- | --------------- |

FILTER  ADXL355. Note that Figure 60 does not include the fixed
The ADXL354/ADXL355 use an analog, low-pass, antialiasing  frequency analog, low-pass, antialiasing filter with a fixed
bandwidth of approximately 1.5 kHz.
filter to reduce out of band noise and to limit bandwidth. The
| ADXL355 provides further digital filtering options to maintain  |     |     |     |     | 0   |     |
| --------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
excellent noise performance at various ODRs.
–10
| The analog, low-pass antialiasing filter in the ADXL354/  |     |     |     |     | )Bd( ESNOPSER FPL LATIGID |     |
| --------------------------------------------------------- | --- | --- | --- | --- | ------------------------- | --- |
| ADXL355 provides a fixed bandwidth of approximately       |     |     |     |     | –20                       |     |
1.5 kHz, which is where the output response is attenuated by
–30
approximately 50%. The shape of the filter response in the
| frequency domain is that of a sinc3 filter.   |     |     |     |     | –40 |     |
| --------------------------------------------- | --- | --- | --- | --- | --- | --- |
The ADXL354 x-axis, y-axis, and z-axis analog outputs include
–50
an amplifier followed by a series 32 kΩ resistor and output to
| the X OUT , the Y | OUT , and the Z | OUT  pins, respectively.   |     |     | –60 |     |
| ----------------- | --------------- | -------------------------- | --- | --- | --- | --- |
The ADXL355 provides an internal 20-bit, Σ-Δ ADC to digitize
–70
the filtered analog signal. Additional digital filtering (beyond the  1 10 100 1k 10k 320-50241
analog, low-pass, antialiasing filter) consists of a low-pass digital  INPUT FREQUENCY (Hz)
decimation filter and a bypassable high-pass filter that supports  Figure 60. ADXL355 Digital Low-Pass Filter (LPF) Response for 4 kHz ODR
output data rates between 4 kHz and 3.9 Hz. The decimation  The ADXL355 pass band of the signal path relates to the
filter consists of two stages. The first stage is fixed decimation  combined filter responses, including the analog filter previously
with a 4 kHz ODR with a low-pass filter cutoff (50% reduction  discussed, and the digital decimation filter/ODR setting. Table 9
in output response) at about 1 kHz. A variable second stage  shows the delay associated with the decimation filter for each
decimation filter is used for the 2 kHz output data rate and below
setting and provides the attenuation at the ODR/4 corner.
(it is bypassed for 4 kHz ODR). Figure 60 shows the low-pass
filter response with a 1 kHz corner (4 kHz ODR) for the
Table 9. Digital Filter Group Delay and Profile
|     |     |     | Delay  |     |     | Attenuation  |
| --- | --- | --- | ------ | --- | --- | ------------ |
Programmed ODR (Hz)  ODR (Cycles)  Time (ms)  Decimator at ODR/4 (dB)  Full Path at ODR/4 (dB)
| 4000            |     |     | 2.52  | 0.63    | −3.44  | −3.63  |
| --------------- | --- | --- | ----- | ------- | ------ | ------ |
| 4000/2 = 2000   |     |     | 2.00  | 1.00    | −2.21  | −2.26  |
| 4000/4 = 1000   |     |     | 1.78  | 1.78    | −1.92  | −1.93  |
| 4000/8 = 500    |     |     | 1.63  | 3.26    | −1.83  | −1.83  |
| 4000/16 = 250   |     |     | 1.57  | 6.27    | −1.83  | −1.83  |
| 4000/32 = 125   |     |     | 1.54  | 12.34   | −1.83  | −1.83  |
| 4000/64 = 62.5  |     |     | 1.51  | 24.18   | −1.83  | −1.83  |
| 4000/128 ~ 31   |     |     | 1.49  | 47.59   | −1.83  | −1.83  |
| 4000/256 ~ 16   |     |     | 1.50  | 96.25   | −1.83  | −1.83  |
| 4000/512 ~ 8    |     |     | 1.50  | 189.58  | −1.83  | −1.83  |
| 4000/1024 ~ 4   |     |     | 1.50  | 384.31  | −1.83  | −1.83  |

|     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- |
Rev. 0 | Page 23 of 42

ADXL354/ADXL355  Data Sheet

The ADXL355 also includes an optional digital high-pass filter  Group delay is the digital filter delay from the input to the ADC
with a programmable corner frequency. By default, the high- until data is available at the interface (see the Filter section).
pass filter is disabled. The high pass corner frequency, where  This delay is the largest component of the total delay from
the output is attenuated by 50%, is related to the ODR, and the  sensor to serial interface.
| HPF_CORNER setting in the filter register (Register 0x28,  |     |     | 40  |     |
| ---------------------------------------------------------- | --- | --- | --- | --- |
Bits[6:4]). Table 10 shows the HPF_CORNER response. Figure 61
and Figure 62 show the simulated high-pass filter response and
32.2122
delay for a 10 Hz cutoff.
30
)SELCYC RDO( YALED
The ADXL355 also includes an interpolation filter after the
decimation filters to produce oversampled/upconverted data
| that provides an external synchronization option. See the Data  |     |     | 20  |     |
| --------------------------------------------------------------- | --- | --- | --- | --- |
Synchronization section for more details. Table 11 shows the
delay and attenuation relative to the programmed ODR.
10
)Bd( ELACS LLUF OTEVITALER EDUTILPMA
0
–3
1
0 520-50241
| –10 |     |     | 0 9.8801 |     |
| --- | --- | --- | -------- | --- |
FREQUENCY (kHz)
Figure 62. High-Pass Filter Delay Response for a 4 kHz ODR and an
–20
HPF_CORNER Setting of 001 (Register 0x28, Bits[6:4])

–30

| –40 |     |     |     |     |
| --- | --- | --- | --- | --- |

| –50      |     | 420-50241 |     |     |
| -------- | --- | --------- | --- | --- |
| 0 9.8801 |     | 100       |     |     |
FREQUENCY (kHz)

Figure 61. High-Pass Filter Pass-Band Response for a 4 kHz ODR and an
HPF_CORNER Setting of 001 (Register 0x28, Bits[6:4])
Table 10. Digital High-Pass Filter Response
HPF_CORNER Register Setting
(Register 0x28, Bits[6:4])  HPF_CORNER Frequency, −3 dB Point Relative to ODR Setting   −3 dB at 4 kHz ODR (Hz)
| 000  | Not applicable, no high-pass filter enabled  |     |     | Off      |
| ---- | -------------------------------------------- | --- | --- | -------- |
| 001  | 24.7 × 10−4 × ODR                            |     |     | 9.88     |
| 010  | 6.2084 × 10−4 × ODR                          |     |     | 2.48     |
| 011  | 1.5545 × 10−4 × ODR                          |     |     | 0.62     |
| 100  | 0.3862 × 10−4 × ODR                          |     |     | 0.1545   |
| 101  | 0.0954 × 10−4 × ODR                          |     |     | 0.03816  |
| 110  | 0.0238 × 10−4 × ODR                          |     |     | 0.00952  |
Table 11. Combined Digital Interpolation Filter and Decimation Filter Response
Interpolator Data Rate Resolution  Combined Interpolator/  Combined Interpolator/  Combined Interpolator/Decimator
Relative to 64 × ODR (Hz)  Decimator Delay (ODR Cycles)  Decimator Delay (ms)  Output Attenuation at ODR/4 (dB)
| 64 × 4000 = 256000  | 3.51661  |     | 0.88    | −6.18  |
| ------------------- | -------- | --- | ------- | ------ |
| 64 × 2000 = 128000  | 3.0126   |     | 1.51    | −4.93  |
| 64 × 1000 = 64000   | 2.752    |     | 2.75    | −4.66  |
| 64 × 500 = 32000    | 2.6346   |     | 5.27    | −4.58  |
| 64 × 250 = 16000    | 2.5773   |     | 10.31   | −4.55  |
| 64 × 125 = 8000     | 2.5473   |     | 20.38   | −4.55  |
| 64 × 62.5 = 4000    | 2.53257  |     | 40.52   | −4.55  |
| 64 × 31.25 = 2000   | 2.52452  |     | 80.78   | −4.55  |
| 64 × 15.625 = 1000  | 2.52045  |     | 161.31  | −4.55  |
| 64 × 7.8125 = 500   | 2.5194   |     | 322.48  | −4.55  |
| 64 × 3.90625 = 250  | 2.51714  |     | 644.39  | −4.55  |

Rev. 0 | Page 24 of 42

Data Sheet  ADXL354/ADXL355

SERIAL COMMUNICATIONS
The 4-wire serial interface communicates in either the SPI or
|     |     |     |     |     |     |     |     |     | ADXL355 | PROCESSOR |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ------- | --------- | --- |
I2C protocol. It affectively autodetects the format being used,
|     |     |     |     |     |     |     |     |     | CS  | DOUT |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- |
requiring no configuration control to select the format.
|     |     |     |     |     |     |     |     |     | MOSI | DOUT |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | ---- | --- |
SPI PROTOCOL
|     |     |     |     |     |     |     |     |     | MISO | DIN |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | --- | --- |
Wire the ADXL355 for SPI communication as shown in the  620-50241
|     |     |     |     |     |     |     |     |     | SCLK | DOUT |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | ---- | ---- | --- |
connection diagram in Figure 63. The SPI protocol timing is

shown in Figure 64 to Figure 67. The timing scheme follows the
Figure 63. 4-Wire SPI Connection
clock polarity (CPOL) = 0 and clock phase (CPHA) = 0. The
SPI clock speed ranges from 100 kHz to 10 MHz.

CS
|     |     |     | 1   | 2 3 | 4 5 | 6 7 | 8 9 | 10 11 12 | 13 14 15 16 |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ----------- | --- | --- |
SCLK
|     |     | MOSI | A6  | A5 A4 | A3 A2 | A1 A0 | RW  |     |     |     |     |
| --- | --- | ---- | --- | ----- | ----- | ----- | --- | --- | --- | --- | --- |
720-50241
|     |     | MISO |     |     |     |     | D7 D6 | D5 D4 | D3 D2 D1 D0 |     |     |
| --- | --- | ---- | --- | --- | --- | --- | ----- | ----- | ----------- | --- | --- |
Figure 64. SPI Timing Diagram—Single-Byte Read

CS
|     |     |     | 1   | 2 3 | 4 5 | 6 7 | 8 9 | 10 11 12 | 13 14 15 16 |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | -------- | ----------- | --- | --- |
SCLK
|     |     | MOSI | A6  | A5 A4 | A3 A2 | A1 A0 | RW D7 D6 | D5 D4 | D3 D2 D1 D0 |     |     |
| --- | --- | ---- | --- | ----- | ----- | ----- | -------- | ----- | ----------- | --- | --- |
820-50241
|     |     | MISO |     |     |     |     |     |     |     |     |     |
| --- | --- | ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Figure 65. SPI Timing Diagram—Single-Byte Write

CS
|     | 1 2 | 3 4 | 5 6 7 | 8 9 | 10 11 | 12 13 | 14 15 | 16 17 |     |     |     |
| --- | --- | --- | ----- | --- | ----- | ----- | ----- | ----- | --- | --- | --- |
SCLK
| MOSI | A6 A5 | A4 A3 | A2 A1 A0 | RW  |     |     |     |     |     |     |     |
| ---- | ----- | ----- | -------- | --- | --- | --- | --- | --- | --- | --- | --- |
920-50241
|      |     |     |     |     |       | BYTE 1 |       |       |             | BYTE n         |     |
| ---- | --- | --- | --- | --- | ----- | ------ | ----- | ----- | ----------- | -------------- | --- |
| MISO |     |     |     | D7  | D6 D5 | D4 D3  | D2 D1 | D0 D7 | D0 D7 D6 D5 | D4 D3 D2 D1 D0 |     |
Figure 66. SPI Timing Diagram—Multibyte Read

CS
|     | 1 2 | 3 4 | 5 6 7 | 8 9 | 10 11 | 12 13 | 14 15 | 16 17 |     |     |     |
| --- | --- | --- | ----- | --- | ----- | ----- | ----- | ----- | --- | --- | --- |
SCLK
|     |     |     |     |     |     | BYTE 1 |     |     |     | BYTE n |     |
| --- | --- | --- | --- | --- | --- | ------ | --- | --- | --- | ------ | --- |
MOSI A6 A5 A4 A3 A2 A1 A0 RW D7 D6 D5 D4 D3 D2 D1 D0 D7 D0 D7 D6 D5 D4 D3 D2 D1 D0
030-50241
| MISO |     |     |     |     |     |     |     |     |     |     |     |
| ---- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
Figure 67. SPI Timing Diagram—Multibyte Write

Rev. 0 | Page 25 of 42

ADXL354/ADXL355 Data Sheet
I2C PROTOCOL recent available. It is not guaranteed that XDATA, YDATA, and
ZDATA form a set corresponding to one sample point in time.
Figure 68 to Figure 70 detail the I2C protocol timing. The I2C
The routine used to retrieve the data from the device controls
interface can be used on most buses operating in I2C standard
this data set continuity. If data transfers are initiated when the
mode (100 kHz), fast mode (400 kHz), fast mode plus (1 MHz),
DATA_RDY bit goes high and completes in a time
and high speed mode (3.4 MHz). The ADXL355 I2C device ID
approximately equal to 1/ODR, XDATA, YDATA, and ZDATA
is as follows:
apply to the same data set.
 ASEL (pin) = 0, device address = 0x1D
For multibyte read or write transactions through either serial
 ASEL (pin) = 1, device address = 0x53
interface, the internal register address autoincrements. When
READING ACCELERATION OR TEMPERATURE the top of the register address range, 0x3FF, is reached the auto-
DATA FROM THE INTERFACE increment stops and does not wrap back to Hex Address 0x00.
Acceleration data is left justified and has a register address The address autoincrement function disables when the FIFO
order of most significant data to least significant data, which address is used, so that data can be read continuously from the
allows the user to use multibyte transfers and to take only as FIFO as a multibyte transaction. In cases where the starting
much data as required—either 8 bits, 16 bits, or 20 bits plus the address of a multibyte transaction is less than the FIFO address,
marker. Temperature data is 12 bits unsigned, right justified. the address autoincrements until reaching the FIFO address,
The data in XDATA, YDATA, and ZDATA is always the most and then stops at the FIFO address.
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29 30 31 32 33 34 35 36 37
SCL
REPEAT
START DEVICE ADDRESS REGISTER ADDRESS START DEVICE ADDRESS DATA BYTE STOP
SDA A6 A5 A4 A3 A2 A1 A0 RW AK 0 A6 A5 A4 A3 A2 A1 A0 AK A6 A5 A4 A3 A2 A1 A0 RW AK 0 D6 D5 D4 D3 D2 D1 D0 AK
SINGLE BYTE READ INDICATE SDA IS
CONTROLLED BYADXL355
Rev. 0 | Page 26 of 42
130-50241
Figure 68. I2C Timing Diagram—Single-Byte Read
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27
SCL
START DEVICE ADDRESS REGISTER ADDRESS DATA BYTE STOP
SDA A6 A5 A4 A3 A2 A1 A0 RW AK 0 A6 A5 A4 A3 A2 A1 A0 AK D7 D6 D5 D4 D3 D2 D1 D0 AK
230-50241
Figure 69. I2C Timing Diagram—Single-Byte Write
1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 19
SCL
START DEVICE ADDRESS REGISTER ADDRESS DATA BYTE 1 DATA BYTE n
SDA A6 A5 A4 A3 A2 A1 A0 RW AK 0 A6 A5 A4 A3 A2 A1 A0 AK D7 D6 D5 D4 D3 D2 D1 D0 AK D7 D0 AK D7 D6 D5 D4 D3 D2 D1 D0 AK
330-50241
Figure 70. I2C Timing Diagram—Multibyte Write

Data Sheet ADXL354/ADXL355
FIFO
FIFO operates in a stream mode, that is, when the FIFO Figure 71 shows the organization of the data in the FIFO. The
overruns new data overwrites the oldest data in the FIFO. A acceleration data is twos complement, 20-bit data. The FIFO
read from the FIFO address guarantees that the three bytes control logic inserts the two LSB reads on the interface. Bit 1
associated with the acceleration measurement on an axis all indicates that an attempt was made to read an empty FIFO, and
pertain to the same measurement. The FIFO never overruns, that the data is not valid acceleration data. Bit 0 is a marker bit
and data is always taken out in sets (multiples of three data to identify the x-axis, which allows a user to verify that the
points). FIFO data was correctly read. An acceleration data point for a
given axis occupies one FIFO location. The read pointer, RD_PTR,
There are 96 21-bit locations in the FIFO. Each location
points to the oldest stored data that was not read already from
contains 20 bits of data and a marker bit for the x-axis data. A
the interface (see Figure 71). There are no physical x-acceleration,
single-byte read from the FIFO address pops one location from
y-acceleration, or z-acceleration data registers. This data also comes
the FIFO. A multibyte read to the FIFO location pops the FIFO
directly from the most recent data set in the FIFO, which points
on the read of the first byte and every third byte read thereafter.
to by the z pointer, Z_PTR, (see Figure 71).
Z17 Z16 Z15 Z14 Z13 Z12 Z11 Z10 Z9 Z8 Z7 Z6 Z5 Z4 Z3 Z2 Z1 Z0 0
Y3 Y2 Y1 Y0 0
Rev. 0 | Page 27 of 42
TNIOP
ELPMAS
.TES
ATAD
SSORCAEMAS
EHT
SI
,SIXA-Y,SIXA-X
ELGNIS
A
.TES
ATAD
SIXA-Z
DNA
Z_PTR + 1 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 0 1 1
Z_PTR Z19 Z18 0
Z_PTR – 1 Y19 Y18 Y17 Y16 Y15 Y14 Y13 Y12 Y11 Y10 Y9 Y8 Y7 Y6 Y5 Y4 0
Z_PTR – 2
RD_PTR
VIRTUAL BITS
ACCELERATION DATA (NOTALLOCATED IN THE FIFO)
EMPTY INDICATOR
X-AXIS MARKER
ASCENDING SPIADDRESSES
SESSERDDAOFIF
GNIDNECSA
GNIDNECSA
SESSERDDAIPS
530-50241
Figure 71. FIFO Data Organization

ADXL354/ADXL355 Data Sheet
INTERRUPTS
The status register (Register 0x04) contains five individual bits, FIFO_FULL
four of which can be mapped to either the INT1 pin, the INT2 pin,
The FIFO_FULL bit is set when the entries in the FIFO are
or both. The polarity of the interrupt, active high or active low,
equal to the setting of the FIFO_SAMPLES bits. It clears as
is also selectable via the INT_POL bit in the range (Register 0x2C)
follows:
register. In general, the status register clears when read, but this
is not the case if the condition that caused the interrupt persists • If the entries in the FIFO fall below the FIFO_SAMPLES,
after the read of the register. The definition of persist varies which is only the case if sufficient data is read from the
slightly in each case, but it is described in the following sections. FIFO.
The DRDY pin is similar to an interrupt pins (INTx) but clears • On a read of the status register, but only if the entries in the
very differently. This case is also described. FIFO are less than the FIFO_SAMPLES bits.
DATA_RDY FIFO_OVR
The DATA_RDY bit is set when new acceleration data is The FIFO_OVR bit is set when the FIFO is so far overrange that
available to the interface. It clears on a read of the status register. data is lost. The specified size of the FIFO is 96 locations. There
It is not set again until acceleration data that is newer than the is an additional three location buffer to compensate for delays
status register read is available. in the synchronization of the clock domains. It is only when
there is an attempt to write past this 99 location limit that
Special logic on the clear of the DATA_RDY bit covers the
FIFO_OVR is set.
corner case where new data arrives during the read of the status
register. In this case, the data ready condition may be missed A read of the status register clears FIFO_OVR. It is not set again
completely. This logic results in a delay of the clearing of until data is lost subsequent to this data register read.
DATA_RDY of up to four 512 kHz cycles. ACTIVITY
DRDY PIN
The activity bit (Register 0x04, Bit 3) is set when the measured
DATA is not a status register bit; it instead behaves similar to an acceleration on any axis is above the ACT_THRESH bits for
unmaskable interrupt. DRDY is set when new acceleration data ACT_COUNT consecutive measurements. An over threshold
is available to the interface. It clears on a read of the FIFO, on a condition can shift from one axis to another on successive
read of XDATA, YDATA, or ZDATA, or by an autoclear measurements and is still counted toward the consecutive
function that occurs approximately halfway between output ACT_COUNT count.
acceleration data sets.
A read of the status register clears the activity bit (Register 0x04,
DRDY is always active high. The INT_POL bit does not affect Bit 3), but it sets again at the end of the next measurement if the
DRDY. In EXT_SYNC modes, the first few DRDY pulses after activity bit (Register 0x04, Bit 3) conditions are still satisfied.
initial synchronization can be lost or corrupted. The length of NVM_BUSY
this potential corruption is less than the group delay.
The NVM_BUSY bit indicates that the nonvolatile memory
(NVM) controller is busy, and it cannot be accessed to read,
write, or generate an interrupt.
A status register read that occurs after the NVM controller is no
longer busy clears NVM_BUSY.
Rev. 0 | Page 28 of 42

Data Sheet ADXL354/ADXL355
EXTERNAL SYNCHRONIZATION AND The advantage of this mode is that data is available at a user
INTERPOLATION defined sample rate and is asynchronous to the internal oscillator.
The disadvantage of this mode is that the group delay is increased,
There are three possible synchronization options for the ADXL355,
and there is increased attenuation at the band edge. Additionally,
shown in Figure 72 to Figure 74. For clarity, the clock frequencies
because there is a limit to the time resolution, there is some
and delays are drawn to scale. The labels in Figure 72 to Figure 74
distortion related to the mismatch of the external sync relative
are defined as follows:
to the internal oscillator. This mismatch degrades spectral
• Internal ODR is the alignment of the decimated output performance. The group delay is based on the decimation setting
data based on the internal clock. and interpolation setting (see Table 11). Table 13 shows the delay
• ADC clock shows the internal master clock rate between the SYNC signal (input) to DRDY (output).
• DRDY is an output indicator signaling a sample is ready.
EXT_SYNC = 01—External Sync and External Clock
The three modes are include as follows: In this case, an external source provides an external clock at a
• No external synchronization (internal clocks used) frequency of 4 × 64 × ODR. The external clock becomes the
• Synchronization with interpolation filter enabled master clock source for the device. In addition, an external
synchronization signal is needed to align the decimation filter
• Sync with an external sync and clock signals, no
output to a specific clock edge, which provides full external
interpolation filter
synchronization and is commonly used when a fixed external
EXT_SYNC = 00—No External Sync or Interpolation clock captures and processes data, and asynchronous clock(s) are
For this case, an internal clock that serves as the synchronization not allowed. When using multiple sensors, synchronization with an
master generates the data. No external signals are required, and external master clock is beneficial and requires time alignment.
this is used commonly when the external processor retrieves When configured for EXT_SYNC = 01 with an ODR of 4 kHz,
data from the device asynchronously and absolute synchronization the user must supply an external clock at 1.024 MHz (64 × 4 ×
to an external source is not required. Use Register 0x28 to program 4 kHz) on the INT2 pin (Pin 13), and an external synchronization
the ODR. on DRDY pin (Pin 14), as shown in Table 12.
The device outputs a DRDY (active high) to signal that a new Special restrictions when using this mode include the following:
sample is available, and data is retrieved from the real-time
• An external clock (EXT_CLK) must be provided as well as
registers or the FIFO. The group delay is based on the
an external sync.
decimation setting as shown in Table 9.
• The frequency of EXT_CLK must be exactly 4 × 64 × ODR.
EXT_SYNC = 10—External Sync with Interpolation
• The width of sync must be a minimum of four EXT_CLK
In this case, the internal clock generates data; however, an periods.
interpolation filter provides additional time resolution of 64 • The phase of sync must meet an approximate 25 ns setup
times the programmed ODR. Synchronization using interpolation time to the EXT_CLK rising edge.
filters and an external ODR clock is commonly used when the
When using the EXT_SYNC mode and without providing sync,
external processor can provide a synchronization signal (which
the device runs on its own synchronization. Similarly, after
is asynchronous to the internal clock) at the desired ODR.
synchronization, the device continues to run synchronized to
Synchronization with the interpolation filter enabled
the last sync pulse it received, which means that EXT_SYNC = 01
(EXT_SYNC = 10) allows the nonsynchronous external clock to
mode can be used with only a single synchronization pulse.
output data most closely associated with the external clock
rising edge. The interpolation filter provides a frequency The interpolation filter provides a frequency resolution related to
resolution related to ODR (see Table 11). the ODR (see Table 11). In this case, the data provided corresponds
to the external signal, which can be greater than the set ODR,
but the output pass band remains the same it was prior to the
interpolation filter.
Table 12. Multiplexing of INT2 and DRDY
Register or Bit Fields Pins
EXT_CLK EXT_SYNC[1:0] INT_MAP[7:4] INT2 (Pin 13) DRDY (Pin 14) Comments
0 00 0000 Low DRDY Synchronization is to the internal clocks, and there is
0 00 Not 0000 INT2 DRDY no external clock synchronization.
1 00 0000 EXT_CLK DRDY
1 00 Not 00002 EXT_CLK DRDY
0 01 0000 DRDY SYNC These options reset the digital filters on every
0 011 Not 0000 INT2 SYNC synchronization pulse and are not recommended.
Rev. 0 | Page 29 of 42

ADXL354/ADXL355  Data Sheet

| Register or Bit Fields  |     |     | Pins  |     |
| ----------------------- | --- | --- | ----- | --- |
EXT_CLK  EXT_SYNC[1:0]  INT_MAP[7:4]  INT2 (Pin 13)  DRDY (Pin 14)  Comments
1  011  0000  EXT_CLK  SYNC  External synchronization, no interpolation filter, and
DRDY (active high) signals that data is ready. Data
| 1  011  | Not 00002  | EXT_CLK  | SYNC  |     |
| ------- | ---------- | -------- | ----- | --- |
represents a sample point group delay earlier in time.
0  10  0000  DRDY  SYNC  External synchronization, interpolation filter, and
0  101  Not 0000  INT2  SYNC  DRDY (active high) signals that data is ready. Data
sample group delay earlier in time.
| 1  101  | 0000      | EXT_CLK  | SYNC  |     |
| ------- | --------- | -------- | ----- | --- |
| 1  101  | Not 0000  | EXT_CLK  | SYNC  |     |
1 No DRDY.
2 No INT2, even though it is enabled.

|     |     | SAMPLE POINT |     | GROUPDELAY |
| --- | --- | ------------ | --- | ---------- |
(FIXED RELATIVETO DRDY)
INTERNAL ODR
ADC MOD. CLK.
64× ODR 630-50241
DRDY
Figure 72. External Synchronization Option—EXT_SYNC = 00, Internal Sync

GROUPDELAY
SAMPLE POINT (FIXED RELATIVETO SYNC) INTERFACE SYNCHRONIZATION DELAY
INTERNAL ODR
INTERPOLATOR
64× ODR
SYNC
110% ODR 730-50241
DRDY
Figure 73. External Synchronization Option—EXT_SYNC = 10, External Sync, External Clock, Interpolation Filter

GROUPDELAY
|     |     | SAMPLE POINT | (FIXED RELATIVETO SYNC) |     |
| --- | --- | ------------ | ----------------------- | --- |
INTERNAL ODR
EXT_CLK
(4 × 64) × SYNC
SYNC SYNCHRONIZE
LOST SAMPLE 830-50241
DRDY

Figure 74. External Synchronization Option—EXT_SYNC = 01, External Sync, No Interpolation Filter
Table 13. EXT_SYNC = 10, DRDY Delay
| ODR_LPF  |     |     | Delay (OSC Cycles)  |     |
| -------- | --- | --- | ------------------- | --- |
| 0x0      |     |     | 8                   |     |
| 0x1      |     |     | 10                  |     |
| 0x2      |     |     | 14                  |     |
| 0x3      |     |     | 22                  |     |
| 0x4      |     |     | 38                  |     |
| 0x5      |     |     | 70                  |     |
| 0x6      |     |     | 134                 |     |
| 0x7      |     |     | 262                 |     |
| 0x8      |     |     | 1031                |     |
| 0x9      |     |     | 2054                |     |
| 0x10     |     |     | 4102                |     |

Rev. 0 | Page 30 of 42

| Data Sheet  |     |     |     |     |     |     |     | ADXL354/ADXL355  |     |     |
| ----------- | --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- |

ADXL355 REGISTER MAP
Note that while configuring the ADXL355 in an application, all configuration registers must be programmed before enabling measurement mode
in the POWER_CTL register. When the ADXL355 is in measurement mode, only the following configurations can change: the HPF_CORNER
bits in the filter register, the INT_MAP register, the ST1 and ST2 bits in the SELF_TEST register, and the reset register.
Table 14. ADXL355 Register Map
Hex. Addr. Register Name  Bit 7  Bit 6  Bit 5  Bit 4  Bit 3  Bit 2  Bit 1  Bit 0  Reset  R/W
| 0x00  DEVID_AD   |     |     |     |     | DEVID_AD   |     |     |     | 0xAD  | R   |
| ---------------- | --- | --- | --- | --- | ---------- | --- | --- | --- | ----- | --- |
| 0x01  DEVID_MST  |     |     |     |     | DEVID_MST  |     |     |     | 0x1D  | R   |
| 0x02  PARTID     |     |     |     |     | PARTID     |     |     |     | 0xED  | R   |
| 0x03  REVID      |     |     |     |     | REVID      |     |     |     | 0x01  | R   |
0x04  Status  Reserved  NVM_BUSY  Activity  FIFO_OVR  FIFO_FULL  DATA_RDY  0x00  R
| 0x05  FIFO_ENTRIES  | Reserved  |                   |             |                         | FIFO_ENTRIES       |                          |           |        | 0x00  | R    |
| ------------------- | --------- | ----------------- | ----------- | ----------------------- | ------------------ | ------------------------ | --------- | ------ | ----- | ---- |
| 0x06  TEMP2         |           | Reserved          |             |                         |                    | Temperature, Bits[11:8]  |           |        | 0x00  | R    |
| 0x07  TEMP1         |           |                   |             | Temperature, Bits[7:0]  |                    |                          |           |        | 0x00  | R    |
| 0x08  XDATA3        |           |                   |             | XDATA, Bits[19:12]      |                    |                          |           |        | 0x00  | R    |
| 0x09  XDATA2        |           |                   |             |                         | XDATA, Bits[11:4]  |                          |           |        | 0x00  | R    |
| 0x0A  XDATA1        |           | XDATA, Bits[3:0]  |             |                         |                    |                          | Reserved  |        | 0x00  | R    |
| 0x0B  YDATA3        |           |                   |             | YDATA, Bits[19:12]      |                    |                          |           |        | 0x00  | R    |
| 0x0C  YDATA2        |           |                   |             |                         | YDATA, Bits[11:4]  |                          |           |        | 0x00  | R    |
| 0x0D  YDATA1        |           | YDATA, Bits[3:0]  |             |                         |                    |                          | Reserved  |        | 0x00  | R    |
| 0x0E  ZDATA3        |           |                   |             | ZDATA, Bits[19:12]      |                    |                          |           |        | 0x00  | R    |
| 0x0F  ZDATA2        |           |                   |             |                         | ZDATA, Bits[11:4]  |                          |           |        | 0x00  | R    |
| 0x10  ZDATA1        |           | ZDATA, Bits[3:0]  |             |                         |                    |                          | Reserved  |        | 0x00  | R    |
| 0x11  FIFO_DATA     |           |                   |             |                         | FIFO_DATA          |                          |           |        | 0x00  | R    |
| 0x1E  OFFSET_X_H    |           |                   |             | OFFSET_X, Bits[15:8]    |                    |                          |           |        | 0x00  | R/W  |
| 0x1F  OFFSET_X_L    |           |                   |             | OFFSET_X, Bits[7:0]     |                    |                          |           |        | 0x00  | R/W  |
| 0x20  OFFSET_Y_H    |           |                   |             | OFFSET_Y, Bits[15:8]    |                    |                          |           |        | 0x00  | R/W  |
| 0x21  OFFSET_Y_L    |           |                   |             | OFFSET_Y, Bits[7:0]     |                    |                          |           |        | 0x00  | R/W  |
| 0x22  OFFSET_Z_H    |           |                   |             | OFFSET_Z, Bits[15:8]    |                    |                          |           |        | 0x00  | R/W  |
| 0x23  OFFSET_Z_L    |           |                   |             | OFFSET_Z, Bits[7:0]     |                    |                          |           |        | 0x00  | R/W  |
| 0x24  ACT_EN        |           |                   | Reserved    |                         |                    | ACT_Z                    | ACT_Y     | ACT_X  | 0x00  | R/W  |
| 0x25  ACT_THRESH_H  |           |                   |             | ACT_THRESH, Bits[15:8]  |                    |                          |           |        | 0x00  | R/W  |
| 0x26  ACT_THRESH_L  |           |                   |             | ACT_THRESH, Bits[7:0]   |                    |                          |           |        | 0x00  | R/W  |
| 0x27  ACT_COUNT     |           |                   |             |                         | ACT_COUNT          |                          |           |        | 0x01  | R/W  |
| 0x28  Filter        | Reserved  |                   | HPF_CORNER  |                         |                    |                          | ODR_LPF   |        | 0x00  | R/W  |
| 0x29  FIFO_SAMPLES  | Reserved  |                   |             |                         | FIFO_SAMPLES       |                          |           |        | 0x60  | R/W  |
0x2A  INT_MAP  ACT_EN2  OVR_EN2  FULL_EN2  RDY_EN2  ACT_EN1  OVR_EN1  FULL_EN1  RDY_EN1  0x00  R/W
| 0x2B  Sync   |         |          | Reserved  |     |           | EXT_CLK  |     | EXT_SYNC  | 0x00  | R/W  |
| ------------ | ------- | -------- | --------- | --- | --------- | -------- | --- | --------- | ----- | ---- |
| 0x2C  Range  | I2C_HS  | INT_POL  |           |     | Reserved  |          |     | Range     | 0x81  | R/W  |
0x2D  POWER_CTL  Reserved  DRDY_OFF  TEMP_OFF  STANDBY  0x01  R/W
| 0x2E  SELF_TEST  |     |     | Reserved  |     |        |     | ST2  | ST1  | 0x00  | R/W  |
| ---------------- | --- | --- | --------- | --- | ------ | --- | ---- | ---- | ----- | ---- |
| 0x2F  Reset      |     |     |           |     | Reset  |     |      |      | 0x00  | W    |

Rev. 0 | Page 31 of 42

| ADXL354/ADXL355  |     |     |     |     |     |     | Data Sheet  |
| ---------------- | --- | --- | --- | --- | --- | --- | ----------- |

REGISTER DEFINITIONS
This section describes the functions of the ADXL355 registers. The ADXL355 powers up with the default register values, as shown in the
Reset column of Table 14.
ANALOG DEVICES ID REGISTER
This register contains the Analog Devices ID, 0xAD.
Address: 0x00, Reset: 0xAD, Name: DEVID_AD
Table 15. Bit Descriptions for DEVID_AD
| Bits   | Bit Name  |     | Settings  | Description          |     | Reset  | Access  |
| ------ | --------- | --- | --------- | -------------------- | --- | ------ | ------- |
| [7:0]  | DEVID_AD  |     |           |   Analog Devices ID  |     | 0xAD   | R       |

ANALOG DEVICES MEMS ID REGISTER
This register contains the Analog Devices MEMS ID, 0x1D.
Address: 0x01, Reset: 0x1D, Name: DEVID_MST
Table 16. Bit Descriptions for DEVID_MST
| Bits   | Bit Name   | Settings  |     | Description             |     | Reset  | Access  |
| ------ | ---------- | --------- | --- | ----------------------- | --- | ------ | ------- |
| [7:0]  | DEVID_MST  |           |     | Analog Devices MEMS ID  |     | 0x1D   | R       |

DEVICE ID REGISTER
This register contains the device ID, 0xED (355 octal).
Address: 0x02, Reset: 0xED, Name: PARTID
Table 17. Bit Descriptions for PARTID
| Bits   | Bit Name  | Settings  |     | Description              |     | Reset  | Access  |
| ------ | --------- | --------- | --- | ------------------------ | --- | ------ | ------- |
| [7:0]  | PARTID    |           |     |   Device ID (355 octal)  |     | 0xED   | R       |

PRODUCT REVISION ID REGISTER
This register contains the product revision ID, beginning with 0x00 and incrementing for each subsequent revision.
Address: 0x03, Reset: 0x00, Name: REVID
Table 18. Bit Descriptions for REVID
| Bits   | Bit Name  |     | Settings  |     | Description    | Reset  | Access  |
| ------ | --------- | --- | --------- | --- | -------------- | ------ | ------- |
| [7:0]  | REVID     |     |           |     | Mask revision  | 0x01   | R       |

STATUS REGISTER
This register includes bits that describe the various conditions of the ADXL355.
Address: 0x04, Reset: 0x00, Name: STATUS
Table 19. Bit Descriptions for STATUS
| Bits  Bit Name   | Settings  | Description  |     |     |     |     | Reset  Access  |
| ---------------- | --------- | ------------ | --- | --- | --- | --- | -------------- |
| [7:5]  Reserved  |           |   Reserved.  |     |     |     |     | 0x0  R         |
4  NVM_BUSY    NVM controller is busy with either refresh, programming, or built-in, self test (BIST).  0x0  R
3  Activity    Activity, as defined in the THRESH_ACT and COUNT_ACT registers, is detected.  0x0  R
2  FIFO_OVR    FIFO has overrun, and the oldest data is lost.  0x0  R
| 1  FIFO_FULL  |     |   FIFO watermark is reached.  |     |     |     |     | 0x0  R  |
| ------------- | --- | ----------------------------- | --- | --- | --- | --- | ------- |
0  DATA_RDY    A complete x-axis, y-axis, and z-axis measurement was made and results can be read.  0x0  R

Rev. 0 | Page 32 of 42

| Data Sheet  |     |     |     |     |     |     | ADXL354/ADXL355  |     |
| ----------- | --- | --- | --- | --- | --- | --- | ---------------- | --- |

FIFO ENTRIES REGISTER
This register indicates the number of valid data samples present in the FIFO buffer. This number ranges from 0 to 96.
Address: 0x05, Reset: 0x00, Name: FIFO_ENTRIES
Table 20. Bit Descriptions for FIFO_ENTRIES
| Bits  | Bit Name  | Settings  | Description  |     |     |     | Reset  | Access  |
| ----- | --------- | --------- | ------------ | --- | --- | --- | ------ | ------- |
| 7     | Reserved  |           |   Reserved   |     |     |     | 0x0    | R       |
[6:0]  FIFO_ENTRIES    Number of data samples stored in the FIFO  0x0  R

TEMPERATURE DATA REGISTERS
These two registers contain the uncalibrated temperature data. The nominal intercept is 1852 LSB at 25°C and the nominal slope is
−9.05 LSB/°C. TEMP2 contains the four most significant bits, and TEMP1 contains the eight least significant bits of the 12-bit value.
Address: 0x06, Reset: 0x00, Name: TEMP2
Table 21. Bit Descriptions for TEMP2
| Bits   | Bit Name  |     | Settings  | Description  |     |     | Reset  | Access  |
| ------ | --------- | --- | --------- | ------------ | --- | --- | ------ | ------- |
| [7:4]  | Reserved  |     |           |   Reserved.  |     |     |        |         |
[3:0]  Temperature, Bits[11:8]    Uncalibrated temperature data  0x0  R

Address: 0x07, Reset: 0x00, Name: TEMP1
Table 22. Bit Descriptions for TEMP1
| Bits  | Bit Name  |     | Settings  | Description  |     |     | Reset  | Access  |
| ----- | --------- | --- | --------- | ------------ | --- | --- | ------ | ------- |
[7:0]  Temperature, Bits[7:0]    Uncalibrated temperature data  0x0  R

X-AXIS DATA REGISTERS
These three registers contain the x-axis acceleration data. Data is left justified and formatted as twos complement.
Address: 0x08, Reset: 0x00, Name: XDATA3
Table 23. Bit Descriptions for XDATA3
| Bits   | Bit Name            |     | Settings  |     | Description    | Reset  |     | Access  |
| ------ | ------------------- | --- | --------- | --- | -------------- | ------ | --- | ------- |
| [7:0]  | XDATA, Bits[19:12]  |     |           |     |   X-axis data  | 0x0    |     | R       |

Address: 0x09, Reset: 0x00, Name: XDATA2
Table 24. Bit Descriptions for XDATA2
| Bits   | Bit Name           |     | Settings  |     | Description    | Reset  | Access  |     |
| ------ | ------------------ | --- | --------- | --- | -------------- | ------ | ------- | --- |
| [7:0]  | XDATA, Bits[11:4]  |     |           |     |   X-axis data  | 0x0    | R       |     |

Address: 0x0A, Reset: 0x00, Name: XDATA1
Table 25. Bit Descriptions for XDATA1
| Bits   | Bit Name          |     | Settings  |     | Description    | Reset  | Access  |     |
| ------ | ----------------- | --- | --------- | --- | -------------- | ------ | ------- | --- |
| [7:4]  | XDATA, Bits[3:0]  |     |           |     |   X-axis data  | 0x0    | R       |     |
| [3:0]  | Reserved          |     |           |     |   Reserved     | 0x0    | R       |     |

Rev. 0 | Page 33 of 42

| ADXL354/ADXL355  |     |     |     |     | Data Sheet  |
| ---------------- | --- | --- | --- | --- | ----------- |

Y-AXIS DATA REGISTERS
These three registers contain the y-axis acceleration data. Data is left justified and formatted as twos complement.
Address: 0x0B, Reset: 0x00, Name: YDATA3
Table 26. Bit Descriptions for YDATA3
| Bits   | Bit Name            | Settings  | Description    | Reset  | Access  |
| ------ | ------------------- | --------- | -------------- | ------ | ------- |
| [7:0]  | YDATA, Bits[19:12]  |           |   Y-axis data  | 0x0    | R       |

Address: 0x0C, Reset: 0x00, Name: YDATA2
Table 27. Bit Descriptions for YDATA2
| Bits   | Bit Name           | Settings  | Description    | Reset  | Access  |
| ------ | ------------------ | --------- | -------------- | ------ | ------- |
| [7:0]  | YDATA, Bits[11:4]  |           |   Y-axis data  | 0x0    | R       |

Address: 0x0D, Reset: 0x00, Name: YDATA1
Table 28. Bit Descriptions for YDATA1
| Bits   | Bit Name          | Settings  | Description    | Reset  | Access  |
| ------ | ----------------- | --------- | -------------- | ------ | ------- |
| [7:4]  | YDATA, Bits[3:0]  |           |   Y-axis data  | 0x0    | R       |
| [3:0]  | Reserved          |           |   Reserved     | 0x0    | R       |

Z-AXIS DATA REGISTERS
These three registers contain the z-axis acceleration data. Data is left justified and formatted as twos complement.
Address: 0x0E, Reset: 0x00, Name: ZDATA3
Table 29. Bit Descriptions for ZDATA3
| Bits   | Bit Name            | Settings  | Description    | Reset  | Access  |
| ------ | ------------------- | --------- | -------------- | ------ | ------- |
| [7:0]  | ZDATA, Bits[19:12]  |           |   Z-axis data  | 0x0    | R       |

Address: 0x0F, Reset: 0x00, Name: ZDATA2
Table 30. Bit Descriptions for ZDATA2
| Bits   | Bit Name           | Settings  | Description    | Reset  | Access  |
| ------ | ------------------ | --------- | -------------- | ------ | ------- |
| [7:0]  | ZDATA, Bits[11:4]  |           |   Z-axis data  | 0x0    | R       |

Address: 0x10, Reset: 0x00, Name: ZDATA1
Table 31. Bit Descriptions for ZDATA1
| Bits   | Bit Name          | Settings  | Description    | Reset  | Access  |
| ------ | ----------------- | --------- | -------------- | ------ | ------- |
| [7:4]  | ZDATA, Bits[3:0]  |           |   Z-axis data  | 0x0    | R       |
| [3:0]  | Reserved          |           |   Reserved     | 0x0    | R       |

Rev. 0 | Page 34 of 42

Data Sheet ADXL354/ADXL355
FIFO ACCESS REGISTER
Address: 0x11, Reset: 0x00, Name: FIFO_DATA
Read this register to access data stored in the FIFO.
Table 32. Bit Descriptions for FIFO_DATA
Bits Bit Name Settings Description Reset Access
[7:0] FIFO_DATA FIFO data is formatted to 24 bits, 3 bytes, most significant byte first. A read to this 0x0 R
address pops an effective three equal byte words of axis data from the FIFO. Two
subsequent reads or a multibyte read completes the transaction of this data onto the
interface. Continued reading or a sustained multibyte read of this field continues to
pop the FIFO every third byte. Multibyte reads to this address do not increment the
address pointer. If this address is read due to an autoincrement from the previous
address, it does not pop the FIFO. Instead, it returns zeros and increments on to the
next address.
X-AXIS OFFSET TRIM REGISTERS
Address: 0x1E, Reset: 0x00, Name: OFFSET_X_H
Table 33. Bit Descriptions for OFFSET_X_H
Bits Bit Name Settings Description Reset Access
[7:0] OFFSET_X, Offset added to x-axis data after all other signal processing. Data is in twos complement 0x0 R/W
Bits[15:8] format. The significance of OFFSET_X[15:0] matches the significance of XDATA[19:4].
Address: 0x1F, Reset: 0x00, Name: OFFSET_X_L
Table 34. Bit Descriptions for OFFSET_X_L
Bits Bit Name Settings Description Reset Access
[7:0] OFFSET_X, Offset added to x-axis data after all other signal processing. Data is in twos complement 0x0 R/W
Bits[7:0] format. The significance of OFFSET_X[15:0] matches the significance of XDATA[19:4].
Y-AXIS OFFSET TRIM REGISTERS
Address: 0x20, Reset: 0x00, Name: OFFSET_Y_H
Table 35. Bit Descriptions for OFFSET_Y_H
Bits Bit Name Settings Description Reset Access
[7:0] OFFSET_Y, Offset added to y-axis data after all other signal processing. Data is in twos complement 0x0 R/W
Bits[15:8] format. The significance of OFFSET_Y[15:0] matches the significance of YDATA[19:4].
Address: 0x21, Reset: 0x00, Name: OFFSET_Y_L
Table 36. Bit Descriptions for OFFSET_Y_L
Bits Bit Name Settings Description Reset Access
[7:0] OFFSET_Y, Offset added to y-axis data after all other signal processing. Data is in twos complement 0x0 R/W
Bits[7:0] format. The significance of OFFSET_Y[15:0] matches the significance of YDATA[19:4].
Rev. 0 | Page 35 of 42

ADXL354/ADXL355 Data Sheet
Z-AXIS OFFSET TRIM REGISTERS
Address: 0x22, Reset: 0x00, Name: OFFSET_Z_H
Table 37. Bit Descriptions for OFFSET_Z_H
Bits Bit Name Settings Description Reset Access
[7:0] OFFSET_Z, Offset added to z-axis data after all other signal processing. Data is in twos complement 0x0 R/W
Bits[15:8] format. The significance of OFFSET_Z[15:0] matches the significance of ZDATA[19:4].
Address: 0x23, Reset: 0x00, Name: OFFSET_Z_L
Table 38. Bit Descriptions for OFFSET_Z_L
Bits Bit Name Settings Description Reset Access
[7:0] OFFSET_Z, Offset added to z-axis data after all other signal processing. Data is in twos complement 0x0 R/W
Bits[7:0] format. The significance of OFFSET_Z[15:0] matches the significance of ZDATA[19:4].
ACTIVITY ENABLE REGISTER
Address: 0x24, Reset: 0x00, Name: ACT_EN
Table 39. Bit Descriptions for ACT_EN
Bits Bit Name Settings Description Reset Access
[7:3] Reserved Reserved. 0x0 R
2 ACT_Z Z-axis data is a component of the activity detection algorithm. 0x0 R/W
1 ACT_Y Y-axis data is a component of the activity detection algorithm. 0x0 R/W
0 ACT_X X-axis data is a component of the activity detection algorithm. 0x0 R/W
ACTIVITY THRESHOLD REGISTERS
Address: 0x25, Reset: 0x00, Name: ACT_THRESH_H
Table 40. Bit Descriptions for ACT_THRESH_H
Bits Bit Name Settings Description Reset Access
[7:0] ACT_THRESH[15:8] Threshold for activity detection. Acceleration magnitude must be above 0x0 R/W
ACT_THRESH to trigger the activity counter. ACT_THRESH is an unsigned
magnitude. The significance of ACT_TRESH[15:0] matches the significance of
XDATA, YDATA, and ZDATA[18:3].
Address: 0x26, Reset: 0x00, Name: ACT_THRESH_L
Table 41. Bit Descriptions for THRESH_ACT_X_L
Bits Bit Name Settings Description Reset Access
[7:0] ACT_THRESH[7:0] Threshold for activity detection. Acceleration magnitude must be above 0x0 R/W
ACT_THRESH to trigger the activity counter. ACT_THRESH is an unsigned
magnitude. The significance of ACT_TRESH[15:0] matches the significance of
XDATA, YDATA, and ZDATA[18:3].
ACTIVITY COUNT REGISTER
Address: 0x27, Reset: 0x01, Name: ACT_COUNT
Table 42. Bit Descriptions for ACT_COUNT
Bits Bit Name Settings Description Reset Access
[7:0] ACT_COUNT Number of consecutive events above threshold required to detect activity 0x1 R/W
Rev. 0 | Page 36 of 42

| Data Sheet  |     |     |     | ADXL354/ADXL355  |     |
| ----------- | --- | --- | --- | ---------------- | --- |

FILTER SETTINGS REGISTER
Address: 0x28, Reset: 0x00, Name: Filter
Use this register to specify parameters for the internal high-pass and low-pass filters.
Table 43. Bit Descriptions for Filter
| Bits  Bit Name  | Settings  | Description  |     | Reset  | Access  |
| --------------- | --------- | ------------ | --- | ------ | ------- |
| 7  Reserved     |           |   Reserved   |     | 0x0    | R       |
[6:4]  HPF_CORNER    −3 dB filter corner for the first-order, high-pass filter relative to the ODR  0x0  R/W
|                 |     | 000  Not applicable, no high-pass filter enabled   |     |      |      |
| --------------- | --- | -------------------------------------------------- | --- | ---- | ---- |
|                 |     | 001  247 × 10−3 × ODR                              |     |      |      |
|                 |     | 010  62.084 × 10−3 × ODR                           |     |      |      |
|                 |     | 011  15.545 × 10−3 × ODR                           |     |      |      |
|                 |     | 100  3.862 × 10−3 × ODR                            |     |      |      |
|                 |     | 101  0.954 × 10−3 × ODR                            |     |      |      |
|                 |     | 110  0.238 × 10−3 × ODR                            |     |      |      |
| [3:0]  ODR_LPF  |     |   ODR and low-pass filter corner                   |     | 0x0  | R/W  |
|                 |     | 0000  4000 Hz and 1000 Hz                          |     |      |      |
|                 |     | 0001  2000 Hz and 500 Hz                           |     |      |      |
|                 |     | 0010  1000 Hz and 250 Hz                           |     |      |      |
|                 |     | 0011  500 Hz and 125 Hz                            |     |      |      |
|                 |     | 0100  250 Hz and 62.5 Hz                           |     |      |      |
|                 |     | 0101  125 Hz and 31.25 Hz                          |     |      |      |
|                 |     | 0110  62.5 Hz and 15.625 Hz                        |     |      |      |
|                 |     | 0111  31.25 Hz and 7.813 Hz                        |     |      |      |
|                 |     | 1000  15.625 Hz and 3.906 Hz                       |     |      |      |
|                 |     | 1001  7.813 Hz and 1.953 Hz                        |     |      |      |
|                 |     | 1010  3.906 Hz and 0.977 Hz                        |     |      |      |

FIFO SAMPLES REGISTER
Address: 0x29, Reset: 0x60, Name: FIFO_SAMPLES
Use the FIFO_SAMPLES value to specify the number of samples to store in the FIFO. The default value of this register is 0x60 to avoid
triggering the FIFO watermark interrupt.
Table 44. Bit Descriptions for FIFO_SAMPLES
| Bits  Bit Name  | Settings  | Description  |     |     | Reset  Access  |
| --------------- | --------- | ------------ | --- | --- | -------------- |
| 7  Reserved     |           |   Reserved.  |     |     | 0x0  R         |
[6:0]  FIFO_SAMPLES    Watermark number of samples stored in the FIFO that triggers a FIFO_FULL condition.  0x60  R/W
Values range from 1 to 96.

INTERRUPT PIN (INTx) FUNCTION MAP REGISTER
Address: 0x2A, Reset: 0x00, Name: INT_MAP
The INT_MAP register configures the interrupt pins. Bits[7:0] select which function(s) generate an interrupt on the INT1 and INT2 pins.
Multiple events can be configured. If the corresponding bit is set to 1, the function generates an interrupt on the interrupt pins.
Table 45. Bit Descriptions for INT_MAP
| Bits  Bit Name  |     | Settings  | Description                           | Reset  | Access  |
| --------------- | --- | --------- | ------------------------------------- | ------ | ------- |
| 7  ACT_EN2      |     |           |   Activity interrupt enable on INT2   | 0x0    | R/W     |
| 6  OVR_EN2      |     |           |   FIFO_OVR interrupt enable on INT2   | 0x0    | R/W     |
| 5  FULL_EN2     |     |           |   FIFO_FULL interrupt enable on INT2  | 0x0    | R/W     |
| 4  RDY_EN2      |     |           |   DATA_RDY interrupt enable on INT2   | 0x0    | R/W     |
| 3  ACT_EN1      |     |           |   Activity interrupt enable on INT1   | 0x0    | R/W     |
| 2  OVR_EN1      |     |           |   FIFO_OVR interrupt enable on INT1   | 0x0    | R/W     |
| 1  FULL_EN1     |     |           |   FIFO_FULL interrupt enable on INT1  | 0x0    | R/W     |
| 0  RDY_EN1      |     |           |   DATA_RDY interrupt enable on INT1   | 0x0    | R/W     |
Rev. 0 | Page 37 of 42

| ADXL354/ADXL355  |     |     |     | Data Sheet  |
| ---------------- | --- | --- | --- | ----------- |

DATA SYNCHRONIZATION
Address: 0x2B, Reset: 0x00, Name: Sync
Use this register to control the external timing triggers.
Table 46. Bit Descriptions for Sync
| Bits  Bit Name   | Settings  Description            |     |     | Reset  Access  |
| ---------------- | -------------------------------- | --- | --- | -------------- |
| [7:3]  Reserved  |   Reserved.                      |     |     | 0x0  R         |
| 2  EXT_CLK       |   Enable external clock.         |     |     | 0x0  R/W       |
| [1:0]  EXT_SYNC  |   Enable external sync control.  |     |     | 0x0  R/W       |
|                  | 00  Internal sync.               |     |     |                |
    01  External sync, no interpolation filter. After synchronization, and for EXT_SYNC within
specification, DATA_RDY occurs on EXT_SYNC.
    10  External sync, interpolation filter, next available data indicated by DATA_RDY 14 to
8204 oscillator cycles later (longer delay for higher ODR_LPF setting), data represents
a sample point group delay earlier in time.
|     | 11  Reserved.  |     |     |     |
| --- | -------------- | --- | --- | --- |

I2C SPEED, INTERRUPT POLARITY, AND RANGE REGISTER
Address: 0x2C, Reset: 0x81, Name: Range
Table 47. Bit Descriptions for Range
| Bits  Bit Name   | Settings  | Description                        | Reset  | Access  |
| ---------------- | --------- | ---------------------------------- | ------ | ------- |
| 7  I2C_HS        |           |   I2C speed.                       | 0x1    | R/W     |
|                  |           |   1 = high speed mode.             |        |         |
|                  |           |   0 = fast mode.                   |        |         |
| 6  INT_POL       |           |   Interrupt polarity.              | 0x0    | R/W     |
|                  |           | 0  INT1 and INT2 are active low.   |        |         |
|                  |           | 1  INT1 and INT2 are active high.  |        |         |
| [5:2]  Reserved  |           |   Reserved.                        | 0x0    | R       |
| [1:0]  Range     |           |   Range.                           | 0x1    | R/W     |
|                  |           | 01  ±2 g.                          |        |         |
|                  |           | 10  ±4 g.                          |        |         |
|                  |           | 11  ±8 g.                          |        |         |

POWER CONTROL REGISTER
Address: 0x2D, Reset: 0x01, Name: POWER_CTL
Table 48. Bit Descriptions for POWER_CTL
| Bits  Bit Name   | Settings  Description  |     |     | Reset  Access  |
| ---------------- | ---------------------- | --- | --- | -------------- |
| [7:3]  Reserved  |   Reserved.            |     |     | 0x0  R         |
2  DRDY_OFF    Set to 1 to force the DRDY output to 0 in modes where it is normally signal data ready.  0x0  R/W
1  TEMP_OFF    Set to 1 to disable temperature processing. Temperature processing is also disabled  0x0  R/W
when STANDBY = 1.
| 0  STANDBY  |   Standby or measurement mode.  |     |     | 0x1  R/W  |
| ----------- | ------------------------------- | --- | --- | --------- |
    1  Standby mode. In standby mode, the device is in a low power state, and the
temperature and acceleration datapaths are not operating. In addition, digital
functions, including FIFO pointers, reset. Changes to the configuration setting of the
device must be made when STANDBY = 1. An exception is a high-pass filter that can
be changed when the device is operating.
|     | 0  Measurement mode.  |     |     |     |
| --- | --------------------- | --- | --- | --- |

Rev. 0 | Page 38 of 42

| Data Sheet  |     |     |     | ADXL354/ADXL355  |     |
| ----------- | --- | --- | --- | ---------------- | --- |

SELF TEST REGISTER
Address: 0x2E, Reset: 0x00, Name: SELF_TEST
Refer to the Self Test section for more information on the operation of the self test feature.
Table 49. Bit Descriptions for SELF_TEST
| Bits  Bit Name   |     | Settings  | Description                           | Reset  | Access  |
| ---------------- | --- | --------- | ------------------------------------- | ------ | ------- |
| [7:2]  Reserved  |     |           |   Reserved.                           | 0x0    | R       |
| 1  ST2           |     |           |   Set to 1 to enable self test force  | 0x0    | R/W     |
| 0  ST1           |     |           |   Set to 1 to enable self test mode   | 0x0    | R/W     |

RESET REGISTER
Address: 0x2F, Reset: 0x00, Name: Reset
Table 50. Bit Descriptions for Reset
| Bits  Bit Name  | Settings  | Description  |     |     | Reset  Access  |
| --------------- | --------- | ------------ | --- | --- | -------------- |
[7:0]  Reset    Write Code 0x52 to resets the device, similar to a power-on reset (POR)  0x0  W

Rev. 0 | Page 39 of 42

| ADXL354/ADXL355  |     |     | Data Sheet |
| ---------------- | --- | --- | ---------- |

RECOMMENDED SOLDERING PROFILE
Figure 75 and Table 51 provide details about the recommended soldering profile.

CRITICAL ZONE
t
TP P TL TO TP
RAMP-UP
ERUTAREPMET TL
TSMAX t L
TSMIN
t
S RAMP-DOWN
PREHEAT
930-50241
t 25°CTO PEAK
TIME
Figure 75. Recommended Soldering Profile

Table 51. Recommended Soldering Profile
|                  |     | Condition  |          |
| ---------------- | --- | ---------- | -------- |
| Profile Feature  |     | Sn63/Pb37  | Pb-Free  |
Average Ramp Rate from Liquid Temperature (T) to Peak Temperature (T)  L P 3°C/sec maximum  3°C/sec maximum
| Preheat                |         |        |        |
| ---------------------- | ------- | ------ | ------ |
| Minimum Temperature (T | SMIN )  | 100°C  | 150°C  |
| Maximum Temperature (T | )       | 150°C  | 200°C  |
SMAX
Time from T  to T  (t)  60 sec to 120 sec  60 sec to 180 sec
SMIN SMAX S
| T  to T Ramp-Up Rate  |     | 3°C/sec maximum  | 3°C/sec maximum  |
| --------------------- | --- | ---------------- | ---------------- |
SMAX L
| Liquid Temperature (T)   |     | 183°C  | 217°C  |
| ------------------------ | --- | ------ | ------ |
L
Time Maintained Above T (t)  L L 60 sec to 150 sec  60 sec to 150 sec
| Peak Temperature (T)  |     | 240°C + 0°C/−5°C  | 260°C + 0°C/−5°C  |
| --------------------- | --- | ----------------- | ----------------- |
P
Time of Actual T − 5°C (t)  P P 10 sec to 30 sec  20 sec to 40 sec
| Ramp-Down Rate  |     | 6°C/sec maximum  | 6°C/sec maximum  |
| --------------- | --- | ---------------- | ---------------- |
Time from 25°C to Peak Temperature (t 25°C TO PEAK )  6 minutes maximum  8 minutes maximum

Rev. 0 | Page 40 of 42

Data Sheet ADXL354/ADXL355
PCB FOOTPRINT PATTERN
Figure 76 shows the PCB footprint pattern and dimensions in millimeters.
3.22mm
3.80mm
Rev. 0 | Page 41 of 42
mm08.3
0.68mm
0.70mm 0.70mm
14 PLCS
1.8mm × 0.68mm
mm5.4
040-50241
Figure 76. PCB Footprint Pattern and Dimensions in Millimeters

| ADXL354/ADXL355  |     |     |     |     |     |     |     | Data Sheet |     |
| ---------------- | --- | --- | --- | --- | --- | --- | --- | ---------- | --- |

PACKAGING AND ORDERING INFORMATION
OUTLINE DIMENSIONS
DETAIL A
0.80
|     |     | 6.25    |     | 2.25 |     |           |     | BSC |     |
| --- | --- | ------- | --- | ---- | --- | --------- | --- | --- | --- |
|     |     | 6.00 SQ |     | 2.05 |     | 1.674 BSC |     |     |     |
|     |     | 5.85    |     | 1.85 |     |           |     |     |     |
0.510REF
0.30 SQ
|     |     |     |     |     |     | 12  | 14 (PIN 1 INDEX) |     |     |
| --- | --- | --- | --- | --- | --- | --- | ---------------- | --- | --- |
|     |     |     |     |     |     | 11  | 1                |     |     |
DETAIL A
5.60
|     | R 0.103 |     |     | SQ  | 3.81 |     |     |     |     |
| --- | ------- | --- | --- | --- | ---- | --- | --- | --- | --- |
REF
|     | (14 PLCS) |     |     |     |     |     | 0.508 |     |     |
| --- | --------- | --- | --- | --- | --- | --- | ----- | --- | --- |
BSC
|     |     |     |     |     |     | 8 7 | 5 4 |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
R 0.25
|     |          | TOP VIEW |          | SIDE VIEW |         | BOTTOM VIEW | 0.914 |              |     |
| --- | -------- | -------- | -------- | --------- | ------- | ----------- | ----- | ------------ | --- |
|     | (4 PLCS) |          |          | 0.15      |         | 2.54REF     | BSC   |              |     |
|     |          |          | 0.10 BSC | BSC       | 2.20REF |             |       |              |     |
|     |          | R 0.203  |          |           |         |             |       | B-6102-72-50 |     |
(14 PLCS)
455400-GKP

Figure 77. 14-Terminal Ceramic Leadless Chip Carrier [LCC]
(E-14-1)
Dimensions shown in millimeters
BRANDING INFORMATION
|     |     | NO BRAND ON THIS LINE |     | PIN ONE LOCATOR, NO OTHER BRAND ON THIS LINE |     |     |           |     |     |
| --- | --- | --------------------- | --- | -------------------------------------------- | --- | --- | --------- | --- | --- |
|     |     | PART NUMBER           |     | ADXL354B,ADXL354C, ORADXL355B                |     |     |           |     |     |
|     |     | #YYWW                 |     | TWO DIGITYEAR, TWO DIGIT WEEK ID             |     |     |           |     |     |
|     |     | 6 DIGIT LOT NUMBER    |     | SIX DIGIT LOT NUMBER                         |     |     | 870-50241 |     |     |

Figure 78. Branding Information

ORDERING GUIDE
|     | Output   Measurement   |     | Specified   |     |     |     |     |     | Package  |
| --- | ---------------------- | --- | ----------- | --- | --- | --- | --- | --- | -------- |
Model1  Mode  Range (g)  Voltage (V)  Temperature Range  Package Description  Option
ADXL354BEZ  Analog  ±2, ±4  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
ADXL354BEZ-RL  Analog  ±2, ±4  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
ADXL354BEZ-RL7  Analog  ±2, ±4  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
ADXL354CEZ  Analog  ±2, ±8  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
ADXL354CEZ-RL  Analog  ±2, ±8  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
ADXL354CEZ-RL7  Analog  ±2, ±8  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
ADXL355BEZ  Digital  ±2.048, ±4.096,  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
±8.192
ADXL355BEZ-RL  Digital  ±2.048, ±4.096,  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
±8.192
ADXL355BEZ-RL7  Digital  ±2.048, ±4.096,  3.3  −40°C to +125°C  14-Terminal LCC  E-14-1
±8.192
| EVAL-ADXL354BZ  |     |     |     |     |     | Evaluation Board for ADXL354BEZ  |     |     |     |
| --------------- | --- | --- | --- | --- | --- | -------------------------------- | --- | --- | --- |
| EVAL-ADXL354CZ  |     |     |     |     |     | Evaluation Board for ADXL354CEZ  |     |     |     |
| EVAL-ADXL355Z   |     |     |     |     |     | Evaluation Board for ADXL355BEZ  |     |     |     |

1 Z = RoHS-Compliant Part.

©2016 Analog Devices, Inc. All rights reserved. Trademarks and
 registered trademarks are the property of their respective owners.
|     |     | D14205-0-9/16(0)   |     |     |     |     |     |     |     |
| --- | --- | ------------------ | --- | --- | --- | --- | --- | --- | --- |
Rev. 0 | Page 42 of 42