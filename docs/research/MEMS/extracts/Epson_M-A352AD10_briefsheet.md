| Sensing Device             |     |     |     |     |     |     |     |     |     |
| -------------------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 3 Axis Acceleration Sensor |     |     |     |     |     |     |     |     |     |

|     |     |     |     |     |     |     | Product number  |     |     |
| --- | --- | --- | --- | --- | --- | --- | --------------- | --- | --- |

| M-A352AD10  |     |     |     |     |     |     | M-A352AD10 : X2F0000110001  |     |     |
| ----------- | --- | --- | --- | --- | --- | --- | --------------------------- | --- | --- |

• Ultra-low noise：0.2µG/√Hz typ.

• Frequency response characteristics: DC to 460 Hz (-6dB)

• Low jitter external trigger function for synchronous sampling

• High dynamic range: ±15 G (148 dB at fc = 16 Hz / 512 Tap)

• 3-axis digital output SPI / UART

• Power consumption : 20 mA Typ. (Output data rate 200 Hz)

Recommended Application
  • SHM (Structural Health Monitoring)  • seismic observation

• Vibration analysis, control and stabilization  • Motion analysis and control
  Recommended Operating Condition

|            | Parameter  |     | Conditions  |     | Min.  | Typ.  |      | Max.  | Unit  |
| ---------- | ---------- | --- | ----------- | --- | ----- | ----- | ---- | ----- | ----- |
| V  to GND  |            |     |             |     | 3.15  |       | 3.3  | 3.45  | V     |
CC
| Digital input voltage to GND  |     |     |     |     | GND  |     |     | V   | V   |
| ----------------------------- | --- | --- | --- | --- | ---- | --- | --- | --- | --- |
CC
| Digital output voltage to GND  |     |     |     |     | -0.3  |     |     | V  +0.3  | V   |
| ------------------------------ | --- | --- | --- | --- | ----- | --- | --- | -------- | --- |
CC

| Operating temperature range  |     |                            |     |     | -30  |     |     | +85  | °C  |
| ---------------------------- | --- | -------------------------- | --- | --- | ---- | --- | --- | ---- | --- |
| Startup time                 |     | Power-on to start output.  |     |     |      |     |     | 900  | ms  |

  Specifications

  T
|  = -30 °C to +85 °C, V |  = 3.15 V to 3.45 V, ≤ ±1 G, unless otherwise noted.  |     |     |     |     |     |     |     |     |
| ---------------------- | ----------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- | --- |
| A                      | CC                                                    |     |     |     |     |     |     |     |     |
Parameter  Test conditions / Comments  Min.  Typ.  Max.  Unit
| ACCELERATION          |     |                   |     |     |      |       |     |                |     |
| --------------------- | --- | ----------------- | --- | --- | ---- | ----- | --- | -------------- | --- |
| Sensitivity           |     |                   |     |     |      |       |     |                |     |
| Output dynamic range  |     | f = DC to 460 Hz  |     |     | -15  |       |     | +15  G         |     |
| Scale factor          |     | 2-24 G / LSB      |     |     |      | 0.06  |     |   µG / LSB     |     |
| Sensitivity error     |     | +25 °C, ≤ 1 G     |     |     |      | ±500  |     |   ×10-6 (ppm)  |     |
Nonlinearity  ≤ 1 G, Best fit straight line, +25 °C  -0.03    +0.03  % of FS
| Cross axis sensitivity  |     |                     |                              |     |     | ±0.2  |     |   %     |     |
| ----------------------- | --- | ------------------- | ---------------------------- | --- | --- | ----- | --- | ------- | --- |
| Bias                    |     |                     |                              |     |     |       |     |         |     |
| Initial error           |     | +25 °C              |                              |     | -2  |       |     | +2  mG  |     |
|                         |     | T A   =   + 2 5 ° C |  a n d  V C C   =   3. 3 V   |     |     |       |     |         |     |
Bias repeatability  fo r   o n e   y e ar  a f te r  s h i p m e n t    3    mG
| Bias temperature error   |     | +25 °C  |     |     | -2  |       |     | +2  mG     |     |
| ------------------------ | --- | ------- | --- | --- | --- | ----- | --- | ---------- | --- |
| Temperature sensitivity  |     |         |     |     |     | ±0.1  |     |   mG / °C  |     |
| Noise                    |     |         |     |     |     |       |     |            |     |
Noise density   +25 °C, Avg, f = 0.5 Hz to 6 Hz    0.2  0.7  µG / √Hz, rms
Cantilever
| resonance frequency*1  |     | +25 °C, V        | CC  3.3 V  |     |     | 850  |     | Hz       |     |
| ---------------------- | --- | ---------------- | ---------- | --- | --- | ---- | --- | -------- | --- |
| Frequency property     |     |                  |            |     |     |      |     |          |     |
| -6 dB bandwidth        |     | User selectable  |            |     | 9   |      |     | 460  Hz  |     |
| FUNCTION               |     |                  |            |     |     |      |     |          |     |
Built-in LPF cut off  -6 dB at +25 °C, selectable  9    460  Hz
|                          |     |                  |     |     |     | 4, 64, 128, 512  |     | Tap        |     |
| ------------------------ | --- | ---------------- | --- | --- | --- | ---------------- | --- | ---------- | --- |
| User LPF                 |     |                  |     |     |     |                  |     |            |     |
| Output data rate         |     | User selectable  |     |     | 50  |                  |     | 1,000  Hz  |     |
| Ext.trigger input cycle  |     |                  |     |     | 1   |                  |     | 20  ms     |     |
Ext.trigger jitter  ADC's completion to Ext.trigger input  0    5  µs
| TEMPERATURE SENSOR   |     |     |     |     |      |     |     |          |     |
| -------------------- | --- | --- | --- | --- | ---- | --- | --- | -------- | --- |
| Output range         |     |     |     |     | -30  |     |     | +85  °C  |     |
Scale factor *2
|              |     | Output = 2634 (0x0A4A) at +25 °C   |     |     |     | -0.0037918  |     | °C / LSB  |     |
| ------------ | --- | ---------------------------------- | --- | --- | --- | ----------- | --- | --------- | --- |
| RELIABILITY  |     |                                    |     |     |     |             |     |           |     |
MTBF*3
|     |     | JIS-C5003 T | A  = +25 °C  |     | 87,600  |     |     | hour  |     |
| --- | --- | ----------- | ------------ | --- | ------- | --- | --- | ----- | --- |
*1) Please make sure that a vibration on this product around the resonance frequency does not exceed 100 mG. Please take an appropriate
action (e.g. installing a damper mechanism) if it exceeds 100 mG.
*2) This is a reference value used for the internal temperature correction, and is not guaranteed to accurately output the interior temperature.
*3) The MTBF is an estimated value derived from the result of high temperature operation with a system requirement of TA=25℃
and a 60% reliability level.
Note) The values in the specifications are based on the data calibrated at the factory. The values may change according to the way
the product is used.
Note) The Max/Min value is the maximum/minimum value of the design or factory shipment examination, unless otherwise specified.
Note) The calibrated standard 1G gravitational acceleration value is 9.80665 m/s2
|     |     |     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |

Sensor
Outline Dimentions Block Diagram
48
B1 3 42 B2
2 2
16
.2 15
3-φ2.5
24. 19 7
.9 85
.2 15 ( ) 2.15 19 1 .7 4.65 24 (2.15) Unit：mm
Noise Density (Acceleration Output) Frequency Response (Acceleration Output)
fc 460 Hz (512 Tap)
The product characteristics shown above are just examples and are not guaranteed as specifications
Notice of the Document
NOTICE：PLEASE READ CAREFULLY BELOW BEFORE THE USE OF THIS DOCUMENT ©Seiko Epson Corporation 2020
1.The content of this document is subject to change without notice. Before purchasing or using Epson products, please contact with sales representative of Seiko Epson Corporation
(“Epson”) for the latest information and be always sure to check the latest information published on Epson’s official web sites and resources.
2.This document may not be copied, reproduced, or used for any other purposes, in whole or in part, without Epson’s prior consent.
3.Information provided in this document including, but not limited to application circuits, programs and usage, is for reference purpose only. Epson makes no guarantees against any
infringements or damages to any third parties’ intellectual property rights or any other rights resulting from the information. This document does not grant you any licenses, any
intellectual property rights or any other rights with respect to Epson products owned by Epson or any third parties.
4.Using Epson products, you shall be responsible for safe design in your products; that is, your hardware, software, and/or systems shall be designed enough to prevent any critical harm
or damages to life, health or property, even if any malfunction or failure might be caused by Epson products. In designing your products with Epson products, please be sure to check and
comply with the latest information regarding Epson products (including, but not limited to this document, specifications, data sheets, manuals, and Epson’s web site). Using technical
contents such as product data, graphic and chart, and technical information, including programs, algorithms and application circuit examples under this document, you shall evaluate
your products thoroughly both in stand-alone basis and within your overall systems. You shall be solely responsible for deciding whether to adopt/use Epson products with your products.
5.Epson has prepared this document carefully to be accurate and dependable, but Epson does not guarantee that the information is always accurate and complete. Epson assumes no
responsibility for any damages you incurred due to any misinformation in this document.
6.No dismantling, analysis, reverse engineering, modification, alteration, adaptation, reproduction, etc., of Epson products is allowed.
7.Epson products have been designed, developed and manufactured to be used in general electronic applications and specifically designated applications (“Anticipated Purpose”).
Epson products are NOT intended for any use beyond the Anticipated Purpose that requires particular quality or extremely high reliability in order to refrain from causing any malfunction
or failure leading to critical harm to life and health, serious property damage, or severe impact on society, including, but not limited to listed below (“Specific Purpose”).
Therefore, you are strongly advised to use Epson products only for the Anticipated Purpose.
Should you desire to purchase and use Epson products for Specific Purpose, Epson makes no warranty and disclaims with respect to Epson products, whether express or implied,
including without limitation any implied warranty of merchantability or fitness for any Specific Purpose. Please be sure to contact our sales representative in advance, if you desire Epson
products for Specific Purpose:
Space equipment (artificial satellites, rockets, etc.)/Transportation vehicles and their control equipment (automobiles, aircraft, trains, ships, etc.)/Medical equipment/Relay equipment to
be placed on sea floor/ Power station control equipment/Disaster or crime prevention equipment/Traffic control equipment/Financial equipment.
Other applications requiring similar levels of reliability as the above
8.Epson products listed in this document and our associated technologies shall not be used in any equipment or systems that laws and regulations in Japan or any other countries
prohibits to manufacture, use or sell. Furthermore, Epson products and our associated technologies shall not be used for the purposes of military weapons development (e.g. mass
destruction weapons), military use, or any other military applications. If exporting Epson products or our associated technologies, please be sure to comply with the Foreign Exchange
and Foreign Trade Control Act in Japan, Export Administration Regulations in the U.S.A (EAR) and other export-related laws and regulations in Japan and any other countries and to
follow their required procedures.
9.Epson assumes no responsibility for any damages (whether direct or indirect) caused by or in relation with your non-compliance with the terms and conditions in this document or for
any damages (whether direct or indirect) incurred by any third party that you give, transfer or assign Epson products.
10.For more details or other concerns about this document, please contact our sales representative.
11.Company names and product names listed in this document are trademarks or registered trademarks of their respective companies.
DEVICE SALES & MARKETING DEPT. https://global.epson.com/products_and_drivers/sensing_system/