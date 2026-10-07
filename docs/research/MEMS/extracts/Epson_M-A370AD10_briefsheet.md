| Sensing Device  |     |     |     |     |     |     |     |
| --------------- | --- | --- | --- | --- | --- | --- | --- |

  3 Axis Acceleration Sensor
|     |     |     |     |     |     | 製品型番  |     |
| --- | --- | --- | --- | --- | --- | ----- | --- |

M-A370AD10 : X2F000091000000
M-A370AD10

  • Ultra-low noise, surpassing USGS New High Noise Model [1]  0.02 µG/√Hz typ. (1 Hz ~ 10 Hz)
• High-precision  Amplitude Response : ±0.4 dB, Phase Response : ± 0.1 °, Sensitivity Error : ± 500 × 10-6

• High dynamic range  ± 10 G (170 dB)

• High bias stability  Temperature Error : ± 0.5 mG Max., Bias Repeatability for 1 year : ± 0.1 mG Typ.

• GNSS synchronization by 1 PPS (Pulse Per Second)

• 3-axis digital output SPI / UART that is not easily affected by noise

  Recommended Application
• Seismic measurement • Resource exploration • Tilt measurement

  • Structural Health Monitoring (SHM)  • Vibration analysis / control / stabilization

  [1] Peterson, J., “Observations and Modeling of Seismic Background Noise”, USGS Open-File Report 93-322, 1993
|   Recommended Operating Condition  |     |     |     |     |     |     |     |
| ---------------------------------- | --- | --- | --- | --- | --- | --- | --- |

|            | Parameter  |     | Conditions  | Min.  | Typ.  | Max.  | Unit  |
| ---------- | ---------- | --- | ----------- | ----- | ----- | ----- | ----- |
| V  to GND  |            |     |             | 3.15  | 3.3   | 3.45  | V     |
CC
| Digital input voltage to GND  |     |     |     | GND  |     | V   | V   |
| ----------------------------- | --- | --- | --- | ---- | --- | --- | --- |
CC
| Digital output voltage to GND  |     |     |     | - 0.3  |     | V  + 0.3  | V   |
| ------------------------------ | --- | --- | --- | ------ | --- | --------- | --- |
CC
| Operating temperature range  |     |     |                            | - 30  |     | + 85  | °C  |
| ---------------------------- | --- | --- | -------------------------- | ----- | --- | ----- | --- |
| Startup time                 |     |     | Power-on to start output.  |       |     | 900   | ms  |

  Specifications
|   T  = - 30 °C to + 85 °C, V |     |  = 3.15 V to 3.45 V, ≤ ± 1 G, unless otherwise noted.  |     |     |     |     |     |
| ---------------------------- | --- | ------------------------------------------------------ | --- | --- | --- | --- | --- |
| A                            |     | CC                                                     |     |     |     |     |     |
 P a rameter
|                    |     | Test Conditions / Comments  |     | Min.  | Typ.   | Max.  | Unit    |
| ------------------ | --- | --------------------------- | --- | ----- | ------ | ----- | ------- |
| ACCELERATION       |     |                             |     |       |        |       |         |
| Sensitivity        |     |                             |     |       |        |       |         |
| Output Range       |     | f = DC ~ 210 Hz             |     | - 10  |        | + 10  | G       |
| Scale Factor       |     | 2-24 G/LSB                  |     |       | 0.06   |       | µG/LSB  |
| Sensitivity Error  |     | 25 °C, -1 G ~ 1 G           |     |       | ± 500  |       | x10-6   |
Nonlinearity  25 °C, -1 G ~ 1 G, Best fit straight line      ± 0.03  %
Cross Axis Sensitivity  No alignment correction     ± 0.2    %
Bias
| Initial Error          |     | 25°C                              |     |     |        | ± 2.0  | mG  |
| ---------------------- | --- | --------------------------------- | --- | --- | ------ | ------ | --- |
| Bias Repeatability *4  |     | One year after shipment, 25 °C,   |     |     |        |        |     |
|                        |     |                                   |     |     | ± 0.1  |        | mG  |
V  = 3.3 V, Average
CC
Bias Temperature Error  Bias offset change from 25°C reference      ± 0.5  mG
| Temperature sensitivity  |     |     |     |     | ± 0.1  |     | mG/°C  |
| ------------------------ | --- | --- | --- | --- | ------ | --- | ------ |
| Noise                    |     |     |     |     |        |     |        |
Noise Density   25 °C, Average, f = 1 Hz ~ 10 Hz    0.02  0.04  µG/√Hz, rms
Cantilever
|                         |     | 25 °C, V |  = 3.3 V  |     | 450  |     | Hz  |
| ----------------------- | --- | -------- | --------- | --- | ---- | --- | --- |
| Resonance Frequency *1  |     |          | CC        |     |      |     |     |
|  FUNCTION               |     |          |           |     |      |     |     |
Built-in LPF cut off  -6 dB at +25 °C, selectable  9    210  Hz
| User LPF           |     |                  |     |           | 4, 64, 128, 512  |           | Tap  |
| ------------------ | --- | ---------------- | --- | --------- | ---------------- | --------- | ---- |
| Output data rate   |     | User selectable  |     | 50        |                  | 1,000     | Hz   |
| 1 PPS Input Cycle  |     |                  |     | 1 - 10-5  | 1                | 1 + 10-5  | s    |
Ext.trigger jitter  ADC's completion to Ext.trigger input  0    5  µs
| TEMPERATURE SENSOR   |     |     |     |       |     |       |     |
| -------------------- | --- | --- | --- | ----- | --- | ----- | --- |
| Output Range         |     |     |     | - 30  |     | + 85  | °C  |
16-bit Scale Factor *2  Output = 2634 (0x0A4A) at 25 °C    - 0.0037918    °C/LSB
| RELIABILITY  |     |        |     |         |     |     |     |
| ------------ | --- | ------ | --- | ------- | --- | --- | --- |
| MTTF*3       |     | 25 °C  |     | 87,600  |     |     | h   |
*1) Please make sure that a vibration on this product around the resonance frequency does not exceed 5 mG. Please take an appropriate action (e.g. installing
a damper mechanism) if it exceeds 5 mG.
*2) This is a reference value used for the internal temperature correction, and is not guaranteed to accurately output the interior temperature.
*3) Based on the test results, the estimated value is determined under the condition of an 80 % reliability level.
*4) Estimated value from accelerated testing results.
Note) The values in the specifications are based on the data calibrated at the factory. The values may change according to the way the product is used.
Note) The Max/Min value is the maximum/minimum value of the design or factory shipment examination, unless otherwise specified.
Note) The calibrated standard 1 G gravitational acceleration value is 9.80665 m/s2.
|     |     |     |     |     |     |     |     |
| --- | --- | --- | --- | --- | --- | --- | --- |

Sensor
Outline Dimensions Block Diagram
Unit：mm
Noise Density Frequency Response
ASD：Amplitude Spectral Density fc 210 Hz (512 Tap)
Note) The product characteristics shown above are just examples and are not guaranteed as specifications.
Note) This product is subject to export regulations as defined by the "Foreign Exchange and Foreign Trade Act."
When exporting, please follow the relevant laws and regulations of the region and complete the necessary procedures.
Notice of the Document
NOTICE：PLEASE READ CAREFULLY BELOW BEFORE THE USE OF THIS DOCUMENT ©Seiko Epson Corporation 2025
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
including without limitation any implied warranty of merchantability or fitness for any Specific Purpose.
Space equipment (artificial satellites, rockets, etc.)/Transportation vehicles and their control equipment (automobiles, aircraft, trains, ships, etc.)/Medical equipment/Relay equipment to
be placed on sea floor/ Power station control equipment/Disaster or crime prevention equipment/Traffic control equipment/Financial equipment
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
MD SALES DEPT. https://global.epson.com/products_and_drivers/sensing_system/contact/