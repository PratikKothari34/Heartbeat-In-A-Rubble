IIS2ICLX
Datasheet
High-accuracy, high-resolution, low-power, 2-axis digital inclinometer with
embedded machine learning core
Features
• 2-axis linear accelerometer
• Selectable full scale: ±0.5/±1/±2/±3 g
• Ultralow noise performance: 15 µg/√Hz
• Superior stability over temperature (<0.075 mg/°C) and repeatability
• Embedded compensation for high stability over temperature
• I²C/SPI digital output interface
• Low power: 0.42 mA with 2 axes delivering full performance
• Sensor hub feature to efficiently collect data from additional external sensors
• Smart embedded FIFO up to 3 KB
• Programmable high-pass and low-pass digital filters
Product status link • Programmable machine learning core to integrate AI algorithms and reduce
IIS2ICLX power consumption at system level
• Programmable finite state machine to process data from accelerometer and one
external sensor
Product summary
• Extended operating temperature range (-40 °C to +105 °C)
Order code IIS2ICLXTR • Embedded temperature sensor
Temp. range [°C] -40 to +105 • Analog supply voltage: 1.71 V to 3.6 V
CCLGA-16 • High shock survivability
Package
(5 x 5 x 1.7 mm)
• ECOPACK and RoHS compliant
Packing Tape and reel
Applications
Product resources
• Precision inclinometers
AN5509 (IIS2ICLX)
• Antenna pointing and platform leveling
AN5536 (machine learning core)
• Structural health monitoring
AN5542 (finite state machine)
• Precise leveling instruments
AN5551 (tilt sensing)
• Installation and monitoring of equipment
TN0018 (design and soldering)
• Robotics and industrial automation
Product labels Description
The IIS2ICLX is a high-accuracy (ultralow noise, high stability, and repeatability) and
low-power, two-axis linear accelerometer with digital output.
The IIS2ICLX has a selectable full scale of ±0.5/±1/±2/±3 g and is capable of
providing the measured accelerations to the application over an I²C or SPI digital
interface.
Its high accuracy, stability over temperature, and repeatability make IIS2ICLX
particularly suitable for inclination measurement applications (inclinometers).
The sensing element is manufactured using a dedicated micromachining process
developed by STMicroelectronics to produce inertial sensors and actuators on silicon
wafers.
The IC interface is manufactured using a CMOS process that allows a high level
of integration to design a dedicated circuit, which is trimmed to better match the
characteristics of the sensing element.
DS13005 - Rev 7 - August 2022 www.st.com
For further information contact your local STMicroelectronics sales office.

IIS2ICLX
The IIS2ICLX has an unmatched set of embedded features (programmable FSM, machine learning core, sensor
hub, FIFO, event decoding, and interrupts), which are enablers for implementing smart and complex sensor
nodes that deliver high accuracy and performance at very low power.
The IIS2ICLX is available in a high-performance (low-stress) ceramic cavity land grid array (CCLGA) package and
can operate within a temperature range of -40 °C to +105 °C.
DS13005 - Rev 7 page 2/119

IIS2ICLX
Overview
1 Overview
The IIS2ICLX is a high-accuracy (ultralow noise, high stability, and repeatability) and ultralow-power two-axis
digital accelerometer specifically recommended for inclination measurements (inclinometers) in Industry 4.0
applications.
All design aspects and the testing and calibration of the IIS2ICLX have been optimized to reach superior
accuracy, stability, repeatability, and extremely low noise.
The IIS2ICLX has a selectable full scale of ±0.5/±1/±2/±3 g and is capable of providing the measured
accelerations to the application over an I²C or SPI digital interface.
Its unique set of embedded features (programmable FSM, machine learning core, sensor hub, FIFO, event
decoding, and interrupts) facilitates the implementation of smart and complex sensor nodes that deliver high
accuracy at very low power.
Like the entire portfolio of ST MEMS sensors, the IIS2ICLX leverages the robust and mature in-house
manufacturing processes already used for the production of micromachined accelerometers and gyroscopes. The
various sensing elements are manufactured using specialized micromachining processes, while the IC interfaces
are developed using CMOS technology that allows the design of a dedicated circuit, which is trimmed to better
match the characteristics of the sensing element.
The IIS2ICLX is available in a high-performance (low-stress) ceramic cavity land grid array (CCLGA) package and
can operate within a temperature range of -40 °C to +105 °C.
Note: Due to the use of epoxy glue for lid sealing, hermeticity of the package is not guaranteed. Processing or use of
this package in a harsh environment should be assessed by the customer.
DS13005 - Rev 7 page 3/119

IIS2ICLX
Embedded low-power features
2 Embedded low-power features
The IIS2ICLX features the following on-chip functions:
• 3 KB data buffering
– 100% efficiency with flexible configurations and partitioning
– Possibility to store timestamp and external sensors
• Event-detection interrupts (fully configurable)
– Wake-up
– Click and double-click sensing
– Stationary/motion detection
• Specific IP blocks with negligible power consumption and high-performance
– Finite state machine for accelerometer and external sensors
– Machine learning core
• Sensor hub
– Up to 5 total sensors: internal accelerometer and 4 external sensors
DS13005 - Rev 7 page 4/119

IIS2ICLX
Finite state machine
2.1 Finite state machine
The IIS2ICLX can be configured to generate interrupt signals activated by user-defined motion patterns. To
do this, up to 16 embedded finite state machines can be programmed independently for motion detection and
decoding.
Definition of finite state machine
A state machine is a mathematical abstraction used to design logic connections. It is a behavioral model
composed of a finite number of states and transitions between states, similar to a flow chart in which one can
inspect the way logic runs when certain conditions are met. The state machine begins with a start state, goes to
different states through transitions dependent on the inputs, and can finally end in a specific state (called stop
state). The current state is determined by the past states of the system. The following figure shows a generic
state machine.
Figure 1. Generic state machine
Finite state machine in the IIS2ICLX
The IIS2ICLX works as an accelerometer sensor, generating acceleration output data. It is also possible to
connect an external sensor (an accelerometer, a gyroscope, a pressure sensor, and so forth) by using the sensor
hub feature (mode 2). These data can be used as input of up to 16 programs in the embedded finite state
machine (Figure 2. State machine in the IIS2ICLX).
All 16 finite state machines are independent: each one has its dedicated memory area and it is independently
executed. An interrupt is generated when the end state is reached or when some specific command is performed.
Figure 2. State machine in the IIS2ICLX
IIS2ICLX ACC [LSB]
SIGNAL FSM Output
FSM
CONDITIONING
EXT. SENSOR (GYRO)[LSB]
(optional)
DS13005 - Rev 7 page 5/119

IIS2ICLX
Machine learning core
2.2 Machine learning core
The IIS2ICLX embeds a dedicated core for machine learning processing that provides system flexibility, allowing
some algorithms run in the application processor to be moved to the MEMS sensor with the advantage of
consistent reduction in power consumption.
Machine learning core logic allows identifying if a data pattern (for example motion, pressure, temperature,
magnetic data, and so forth) matches a user-defined set of classes. Typical examples of applications could be
anomalous vibration recognition, complex movement, or condition identification, activity detection, and so forth.
The IIS2ICLX machine learning core works on data patterns coming from the accelerometer, but it is also possible
to connect and process external sensor data (from a gyroscope or additional external inclinometer/accelerometer,
temperature or pressure sensors) by using the sensor hub feature (mode 2).
The input data can be filtered using a dedicated configurable computation block containing filters and features
computed in a fixed time window defined by the user.
Machine learning processing is based on logical processing composed of a series of configurable nodes
characterized by "if-then-else" conditions where the "feature" values are evaluated against defined thresholds.
Figure 3. Machine learning core in the IIS2ICLX
Machine
INPUT OUTPUT Machine
Learning Core
Sensor Data & Hub Learning Core
Logicalprocessing
Accelerometer Filters Results
External Sensor Features Interrupts
The IIS2ICLX can be configured to run up to 8 flows simultaneously and independently and every flow can
generate up to 256 results. The total number of nodes can be up to 512.
The results of the machine learning processing are available in dedicated output registers readable from the
application processor at any time.
The IIS2ICLX machine learning core can be configured to generate an interrupt when a change in the result
occurs.
DS13005 - Rev 7 page 6/119

IIS2ICLX
Pin description
3 Pin description
Figure 4. Pin connections
Y
|     | 14 13 12 | 11  |
| --- | -------- | --- |
X
|     | 15  | 10  |
| --- | --- | --- |
|     | 16  | 9   |
TOP
VIEW
|     | 1   | 8   |
| --- | --- | --- |
1
|     | 2   | 7   |
| --- | --- | --- |
(TOP VIEW)
| DIRECTION OF THE  | 3 4 5 | 6   |
| ----------------- | ----- | --- |
DETECTABLE
ACCELERATIONS
3.1 Pin connections
The IIS2ICLX offers flexibility to connect the pins in order to have two different mode connections and
functionalities. In detail:
• Mode 1: I²C slave interface or SPI (3- and 4-wire) serial interface is available.
• Mode 2: I²C slave interface or SPI (3- and 4-wire) serial interface and I²C interface master for external
sensor connections are available.
Figure 5. IIS2ICLX connection modes
Mode 2
Mode 1
HOST
HOST
| I2C/ | I2C/ |     |
| ---- | ---- | --- |

|     | SPI (3/4-w) |     |
| --- | ----------- | --- |
SPI (3/4-w)
| IIS2ICLX | IIS2ICLX |     |
| -------- | -------- | --- |
Master I2C
|     | ELxStMer6nDalS  | M   |
| --- | --------------- | --- |
LSM6DSM
sensors
DS13005 - Rev 7 page 7/119

IIS2ICLX
Pin connections
In the following table, each mode is described for the pin connections and function.
Table 1. Pin description
| Pin number | Name | Mode 1 function | Mode 2 function |
| ---------- | ---- | --------------- | --------------- |
1 VDD_IO Power supply for I/O pins (recommended 100 nF filter capacitor)
I²C/SPI mode selection
| 2   | CS  | (1: SPI idle mode / I²C communication enabled; |     |
| --- | --- | ---------------------------------------------- | --- |
0: SPI communication mode / I²C disabled and reset)
| 3   | GND                               | 0 V supply |                                   |
| --- | --------------------------------- | ---------- | --------------------------------- |
|     | Programmable interrupt 2 (INT2) / |            | Programmable interrupt 2 (INT2) / |
| 4   | INT2                              |            |                                   |
Data enable (DEN) Data enable (DEN)/I²C master external synchronization signal (MDRDY)
SPI 4-wire serial data output (SDO)
| 5   | SDO/SA0 |     |     |
| --- | ------- | --- | --- |
I²C least significant bit of the device address (SA0)
| 6   | INT1 | Programmable Interrupt 1 (INT1)                    |                               |
| --- | ---- | -------------------------------------------------- | ----------------------------- |
| 7   | SDx  | Connect to GND or VDD_IO                           | I²C serial data master (MSDA) |
| 8   | VDD  | Power supply (recommended 100 nF filter capacitor) |                               |
| 9   | VDD  | Power supply (recommended 100 nF filter capacitor) |                               |
I²C serial clock (SCL)
| 10  | SCL |     |     |
| --- | --- | --- | --- |
SPI serial port clock (SPC)
I²C serial data (SDA)
| 11  | SDA/SDI | SPI serial data input (SDI) |     |
| --- | ------- | --------------------------- | --- |
3-wire interface serial data output (SDO)
12 SCx Connect to GND or VDD_IO I²C serial clock master (MSCL)
| 13  | GND | GND                                 |     |
| --- | --- | ----------------------------------- | --- |
| 14  | NC  | Connect to GND or leave unconnected |     |
| 15  | NC  | Connect to GND or leave unconnected |     |
| 16  | NC  | Connect to GND or leave unconnected |     |
DS13005 - Rev 7 page 8/119

IIS2ICLX
Module specifications
4 Module specifications
4.1 Mechanical characteristics
@ Vdd = 3.0 V, T = 25 °C, unless otherwise noted.
Table 2. Mechanical characteristics
Symbol Parameter Test conditions Min.(1) Typ.(2) Max.(1) Unit
±0.5
±1.0
FS Measurement range g
±2.0
±3.0
|                                        | FS = ±0.5 | 0.015       |            |
| -------------------------------------- | --------- | ----------- | ---------- |
|                                        | FS = ±1.0 | 0.031       |            |
| So Sensitivity(3)                      |           | -2%         | +2% mg/LSB |
|                                        | FS = ±2.0 | 0.061       |            |
|                                        | FS = ±3.0 | 0.122       |            |
| So_acc Sensitivity change over life(4) |           | -0.25 ±0.07 | +0.25 %    |
TCSo Sensitivity change vs. temperature From -40° to +105°C,delta from 25 °C -0.012 ±0.01 +0.012 %/°C
| Off Zero-g level offset accuracy(5)      |     | -8      | +8 mg   |
| ---------------------------------------- | --- | ------- | ------- |
| Off_acc Zero-g level change over life(4) |     | -2.5 ±1 | +2.5 mg |
TCOff Zero-g level change vs. temperature From -40° to +105°C, delta from 25 °C -0.075 ±0.020 +0.075 mg/°C
| NL Non-linearity        | Best-fit straight line | 0.1 | % FS      |
| ----------------------- | ---------------------- | --- | --------- |
| An Zero-g noise density |                        | 15  | 30 µg/√Hz |
12.5
26
52
| ODR Digital output data rate |     | 104 | Hz  |
| ---------------------------- | --- | --- | --- |
208
416
833
| Bw Bandwidth | @ODR 833 Hz | 260 | Hz  |
| ------------ | ----------- | --- | --- |
FS = ±2 g; ODR = 50 Hz;
| VRE Vibration rectification error |     | 1   | mg  |
| --------------------------------- | --- | --- | --- |
2.5 grms vibration in 50 - 2000 Hz band
| F0 Sensor resonant frequency    |            | 900 | Hz      |
| ------------------------------- | ---------- | --- | ------- |
| ST Self-test                    | @FS = ±2 g | 1   | 15 mg   |
| Top Operating temperature range |            | -40 | +105 °C |

1. Min/Max values are based on characterization results at 3σ on a limited number of samples, not tested in production and not guaranteed.
2. Typical specifications are not guaranteed.
3. Sensitivity range after MSL3 preconditioning.
4. Drift over life assessed based on behavior after 1000h of THS (Temperature Humidity Storage) at T=+85°C / RH = 85%.
5. Typical zero-g level offset value after MSL3 preconditioning.

| DS13005 - Rev 7 |     |     | page 9/119 |
| --------------- | --- | --- | ---------- |

IIS2ICLX
Electrical characteristics
4.2 Electrical characteristics
@ Vdd = 3.0 V, T = 25 °C, unless otherwise noted.
Table 3. Electrical characteristics
|                                             |     |           |                 | Min.(1)      | Typ.(2) | Max.(1)     |      |
| ------------------------------------------- | --- | --------- | --------------- | ------------ | ------- | ----------- | ---- |
| Symbol                                      |     | Parameter | Test conditions |              |         |             | Unit |
| Vdd Supply voltage                          |     |           |                 | 1.71         | 1.8     | 3.6         | V    |
| Vdd_IO I/O pins supply voltage              |     |           |                 | 1.62         |         | 3.6         | V    |
| Idd Current consumption                     |     |           |                 |              | 420     |             | µA   |
| IddPD Current consumption during power-down |     |           |                 |              | 3       |             | µA   |
| Ton Turn-on time                            |     |           |                 |              | 15      |             | ms   |
| VIH Digital high-level input voltage        |     |           |                 | 0.7 *Vdd_IO  |         |             | V    |
| VIL Digital low-level input voltage         |     |           |                 |              |         | 0.3 *Vdd_IO | V    |
| VOH High-level output voltage               |     |           | IOH = 4 mA(3)   | VDD_IO - 0.2 |         |             | V    |
| VOL Low-level output voltage                |     |           | IOL = 4 mA(3)   |              |         | 0.2         | V    |
| Top Operating temperature range             |     |           |                 | -40          |         | +105        | °C   |

1. Min/Max values are based on characterization results at 3σ on a limited number of samples, not tested in production and not
guaranteed.
2. Typical specifications are not guaranteed.
3. 4 mA is the maximum driving capability, that is, the maximum DC current that can be sourced/sunk by the digital pad in
order to guarantee the correct digital output voltage levels VOH and VOL.

4.3 Temperature sensor characteristics
@ Vdd = 3.0 V, T = 25 °C unless otherwise noted.
Table 4. Temperature sensor characteristics
| Symbol |                          | Parameter | Test conditions | Min. | Typ.(1) | Max. | Unit |
| ------ | ------------------------ | --------- | --------------- | ---- | ------- | ---- | ---- |
| TODR   | Temperature refresh rate |           |                 |      | 52      |      | Hz   |
Temperature offset(2)
| Toff      |                                   |     |     | -15 |     | +15  | °C     |
| --------- | --------------------------------- | --- | --- | --- | --- | ---- | ------ |
| Tsens     | Temperature sensitivity           |     |     |     | 256 |      | LSB/°C |
| TST       | Temperature stabilization time(3) |     |     |     |     | 500  | µs     |
| T_ADC_res | Temperature ADC resolution        |     |     |     | 16  |      | bit    |
| Top       | Operating temperature range       |     |     | -40 |     | +105 | °C     |

1. Typical specifications are not guaranteed.
2. The output of the temperature sensor is 0 LSB (typ.) at 25 °C. Absolute temperature accuracy can be improved (reducing
the effect of temperature offset) by performing OPC (one-point calibration) at room temperature (25 °C).
3. Time from power ON to valid data based on characterization data.

DS13005 - Rev 7 page 10/119

IIS2ICLX
Communication interface characteristics
4.4 Communication interface characteristics
4.4.1 SPI - serial peripheral interface
Subject to general operating conditions for Vdd and Top.
Table 5. SPI slave timing values (in mode 3)
Value(1)
| Symbol  |                      | Parameter |     |     | Unit |
| ------- | -------------------- | --------- | --- | --- | ---- |
|         |                      |           | Min | Max |      |
| tc(SPC) | SPI clock cycle      |           | 100 |     | ns   |
| fc(SPC) | SPI clock frequency  |           |     | 10  | MHz  |
| tsu(CS) | CS setup time        |           | 5   |     |      |
| th(CS)  | CS hold time         |           | 20  |     |      |
| tsu(SI) | SDI input setup time |           | 5   |     |      |
| th(SI)  | SDI input hold time  |           | 15  |     | ns   |
tv(SO)
|          | SDO valid output time   |     |     | 50  |     |
| -------- | ----------------------- | --- | --- | --- | --- |
| th(SO)   | SDO output hold time    |     | 5   |     |     |
| tdis(SO) | SDO output disable time |     |     | 50  |     |

1. Values are evaluated at 10 MHz clock frequency for SPI with both 4 and 3 wires, based on characterization results, not
tested in production.

Figure 6. SPI slave timing diagram (in mode 3)
Note: Measurement points are done at 0.3·Vdd_IO and 0.7·Vdd_IO for both input and output ports.
DS13005 - Rev 7 page 11/119

IIS2ICLX
Communication interface characteristics
4.4.2 I²C - inter-IC control interface
Subject to general operating conditions for Vdd and Top.
Table 6. I²C slave timing values
|                             |           | I²C standard mode(1) |     | I²C fast mode(1) |      |
| --------------------------- | --------- | -------------------- | --- | ---------------- | ---- |
| Symbol                      | Parameter |                      |     |                  | Unit |
|                             |           | Min                  | Max | Min Max          |      |
| f(SCL) SCL clock frequency  |           | 0                    | 100 | 0 400            | kHz  |
| tw(SCLL) SCL clock low time |           | 4.7                  |     | 1.3              |      |
µs
tw(SCLH)
| SCL clock high time                         |     | 4.0 |      | 0.6   |     |
| ------------------------------------------- | --- | --- | ---- | ----- | --- |
| tsu(SDA) SDA setup time                     |     | 250 |      | 100   | ns  |
| th(SDA) SDA data hold time                  |     | 0   | 3.45 | 0 0.9 |     |
| th(ST) START condition hold time            |     | 4   |      | 0.6   |     |
| tsu(SR) Repeated START condition setup time |     | 4.7 |      | 0.6   | µs  |
| tsu(SP) STOP condition setup time           |     | 4   |      | 0.6   |     |
tw(SP:SR) Bus free time between STOP and START condition 4.7 1.3

1. Data based on standard I²C protocol requirement, not tested in production.

Figure 7. I²C slave timing diagram
REPEATED
START
START
t
su(SR)
START
SDA t w(SP:SR)
t t
su(SDA) h(SDA)
|     |     |     |     | t STOP |     |
| --- | --- | --- | --- | ------ | --- |
su(SP)
SCL
t t t
h(ST) w(SCLL) w(SCLH)
Note: Measurement points are done at 0.3·Vdd_IO and 0.7·Vdd_IO for both ports.
| DS13005 - Rev 7 |     |     |     |     | page 12/119 |
| --------------- | --- | --- | --- | --- | ----------- |

IIS2ICLX
Absolute maximum ratings
4.5 Absolute maximum ratings
Stresses above those listed as “absolute maximum ratings” may cause permanent damage to the device. This
is a stress rating only and functional operation of the device under these conditions is not implied. Exposure to
maximum rating conditions for extended periods may affect device reliability.
Table 7. Absolute maximum ratings
| Symbol         |                                          | Ratings | Maximum value | Unit |
| -------------- | ---------------------------------------- | ------- | ------------- | ---- |
| Vdd and Vdd_IO | Supply voltage                           |         | -0.3 to 4.8   | V    |
| TSTG           | Storage temperature range                |         | -40 to +125   | °C   |
| Sg             | Acceleration g for 0.1 ms                |         | 10000         | g    |
| ESD            | Electrostatic discharge protection (HBM) |         | 2             | kV   |
Input voltage on any control pin
| Vin |     |     | -0.3 to Vdd_IO +0.3 | V   |
| --- | --- | --- | ------------------- | --- |
(including CS, SPC, SDI, SDO)
Note: Supply voltage on any pin should never exceed 4.8 V.
This device is sensitive to mechanical shock, improper handling can cause permanent damage to the part.
This device is sensitive to electrostatic discharge (ESD), improper handling can cause permanent damage to the part.
DS13005 - Rev 7 page 13/119

IIS2ICLX
Digital interfaces
5 Digital interfaces
5.1 I²C/SPI interface
The registers embedded inside the IIS2ICLX may be accessed through both the I²C and SPI serial interfaces. The
latter may be software-configured to operate either in 3-wire or 4-wire interface mode. The device is compatible
with SPI modes 0 and 3.
The serial interfaces are mapped to the same pins. To select/exploit the I²C interface, the CS line must be tied
high (that is, connected to Vdd_IO).
Table 8. Serial interface pin description
Pin name Pin description
Enable SPI
CS I²C/SPI mode selection (1: SPI idle mode / I²C communication enabled;
0: SPI communication mode / I²C disabled)
I²C serial clock (SCL)
SCL/SPC
SPI serial port clock (SPC)
I²C serial data (SDA)
SDA/SDI/SDO SPI serial data input (SDI)
3-wire interface serial data output (SDO)
SPI serial data output (SDO)
SDO/SA0
I²C less significant bit of the device address
5.2 I²C serial interface
The IIS2ICLX I²C is a bus slave. The I²C is employed to write the data to the registers, whose content can also be
read back.
The relevant I²C terminology is provided in the table below.
Table 9. I²C terminology
Term Description
Transmitter The device that sends data to the bus
Receiver The device that receives data from the bus
Master The device that initiates a transfer, generates clock signals, and terminates a transfer
Slave The device addressed by the master
There are two signals associated with the I²C bus: the serial clock line (SCL) and the serial data line (SDA). The
latter is a bidirectional line used for sending and receiving the data to/from the interface. Both the lines must be
connected to Vdd_IO through external pull-up resistors. When the bus is free, both the lines are high.
The I²C interface is implemented with fast mode (400 kHz) I²C standards as well as with the standard mode.
In order to disable the I²C block, (I2C_disable) = 1 must be written in CTRL4_C (13h).
5.2.1 I²C operation
The transaction on the bus is started through a start (ST) signal. A START condition is defined as a high to low
transition on the data line while the SCL line is held high. After this has been transmitted by the master, the bus
is considered busy. The next byte of data transmitted after the start condition contains the address of the slave in
the first 7 bits and the eighth bit tells whether the master is receiving data from the slave or transmitting data to
the slave. When an address is sent, each device in the system compares the first seven bits after a start condition
with its address. If they match, the device considers itself addressed by the master.
DS13005 - Rev 7 page 14/119

IIS2ICLX
I²C serial interface
The slave address (SAD) associated to the IIS2ICLX is 110101xb. The SDO/SA0 pin can be used to modify the
less significant bit of the device address. If the SDO/SA0 pin is connected to the supply voltage, LSb is 1 (address
1101011b); else if the SDO/SA0 pin is connected to ground, the LSb value is 0 (address 1101010b). This solution
permits to connect and address two different inertial modules to the same I²C bus.
Data transfer with acknowledge is mandatory. The transmitter must release the SDA line during the acknowledge
pulse. The receiver must then pull the data line LOW so that it remains stable low during the high period of the
acknowledge clock pulse. A receiver that has been addressed is obliged to generate an acknowledge after each
byte of data received.
The I²C embedded inside the IIS2ICLX behaves like a slave device and the following protocol must be adhered
to. After the start condition (ST) a slave address is sent, once a slave acknowledge (SAK) has been returned, an
8-bit subaddress (SUB) is transmitted. The increment of the address is configured by CTRL3_C (12h) (IF_INC).
The slave address is completed with a read/write bit. If the bit is 1 (read), a repeated start (SR) condition
must be issued after the two subaddress bytes; if the bit is 0 (write) the master transmits to the slave with
direction unchanged. Table 10 explains how the SAD+read/write bit pattern is composed, listing all the possible
configurations.
Table 10. SAD+read/write patterns
|     | Command |     |     | SAD[6:1] |     |     | SAD[0] = SA0 |     |     | R/W |     |     | SAD+R/W        |     |
| --- | ------- | --- | --- | -------- | --- | --- | ------------ | --- | --- | --- | --- | --- | -------------- | --- |
|     | Read    |     |     | 110101   |     |     |              | 0   |     | 1   |     |     | 11010101 (D5h) |     |
|     | Write   |     |     | 110101   |     |     |              | 0   |     | 0   |     |     | 11010100 (D4h) |     |
|     | Read    |     |     | 110101   |     |     |              | 1   |     | 1   |     |     | 11010111 (D7h) |     |
|     | Write   |     |     | 110101   |     |     |              | 1   |     | 0   |     |     | 11010110 (D6h) |     |
Table 11. Transfer when master is writing one byte to slave
|     | Master |     | ST  | SAD + W |     |     |     | SUB |     |     | DATA |     |     | SP  |
| --- | ------ | --- | --- | ------- | --- | --- | --- | --- | --- | --- | ---- | --- | --- | --- |
|     | Slave  |     |     |         |     |     | SAK |     | SAK |     |      |     | SAK |     |
Table 12. Transfer when master is writing multiple bytes to slave
| Master |     | ST  | SAD + W |     |     |     | SUB |     | DATA |     | DATA |     |     | SP  |
| ------ | --- | --- | ------- | --- | --- | --- | --- | --- | ---- | --- | ---- | --- | --- | --- |
| Slave  |     |     |         |     | SAK |     |     | SAK |      | SAK |      |     | SAK |     |
Table 13. Transfer when master is receiving (reading) one byte of data from slave
| Master |     | ST  | SAD + W |     |     | SUB |     | SR  | SAD + R |     |          |     | NMAK | SP  |
| ------ | --- | --- | ------- | --- | --- | --- | --- | --- | ------- | --- | -------- | --- | ---- | --- |
| Slave  |     |     |         |     | SAK |     | SAK |     |         |     | SAK DATA |     |      |     |
Table 14. Transfer when master is receiving (reading) multiple bytes of data from slave
| Master | ST  | SAD+W |     | SUB |     | SR  | SAD+R |     | MAK  |     | MAK  |      | NMAK | SP  |
| ------ | --- | ----- | --- | --- | --- | --- | ----- | --- | ---- | --- | ---- | ---- | ---- | --- |
| Slave  |     |       | SAK |     | SAK |     |       | SAK | DATA |     | DATA | DATA |      |     |
Data are transmitted in byte format (DATA). Each data transfer contains 8 bits. The number of bytes transferred
per transfer is unlimited. Data is transferred with the most significant bit (MSb) first. If a slave receiver does not
acknowledge the slave address (that is, it is not able to receive because it is performing some real-time function)
the data line must be left high by the slave. The master can then abort the transfer. A low to high transition on the
SDA line while the SCL line is high is defined as a stop condition. Each data transfer must be terminated by the
generation of a stop (SP) condition.
In the presented communication format MAK is master acknowledge and NMAK is no master acknowledge.
| DS13005 - Rev 7 |     |     |     |     |     |     |     |     |     |     |     |     |     | page 15/119 |
| --------------- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | ----------- |

IIS2ICLX
SPI bus interface
5.3 SPI bus interface
The IIS2ICLX SPI is a bus slave. The SPI allows writing to and reading from the registers of the device.
The serial interface communicates to the application using 4 wires: CS, SPC, SDI, and SDO.
Figure 8. Read and write protocol (in mode 3)
CS
SPC
SDI
RW DI7 DI6 DI5 DI4 DI3 DI2 DI1 DI0
AD6AD5 AD4AD3AD2AD1AD0
SDO
DO7DO6DO5DO4DO3DO2DO1DO0
CS enables the serial port and it is controlled by the SPI master. It goes low at the start of the transmission and
goes back high at the end. SPC is the serial port clock and it is controlled by the SPI master. It is stopped high
when CS is high (no transmission). SDI and SDO are, respectively, the serial port data input and output. Those
lines are driven at the falling edge of SPC and should be captured at the rising edge of SPC.
Both the read register and write register commands are completed in 16 clock pulses or in multiples of 8 in case
of multiple read/write bytes. Bit duration is the time between two falling edges of SPC. The first bit (bit 0) starts at
the first falling edge of SPC after the falling edge of CS while the last bit (bit 15, bit 23, ...) starts at the last falling
edge of SPC just before the rising edge of CS.
bit 0: RW bit. When 0, the data DI(7:0) is written into the device. When 1, the data DO(7:0) from the device is
read. In the latter case, the chip drives SDO at the start of bit 8.
bit 1-7: address AD(6:0). This is the address field of the indexed register.
bit 8-15: data DI(7:0) (write mode). This is the data that is written into the device (MSb first).
bit 8-15: data DO(7:0) (read mode). This is the data that is read from the device (MSb first).
In multiple read/write commands, further blocks of 8 clock periods are added. When the CTRL3_C (12h) (IF_INC)
bit is 0, the address used to read/write data remains the same for every block. When the CTRL3_C (12h)
(IF_INC) bit is 1, the address used to read/write data is increased at every block.
The function and the behavior of SDI and SDO remain unchanged.
DS13005 - Rev 7 page 16/119

IIS2ICLX
SPI bus interface
5.3.1 SPI read
Figure 9. SPI read protocol (in mode 3)
CS
SPC
SDI
RW
AD6AD5AD4AD3AD2AD1AD0
SDO
DO7DO6DO5DO4DO3DO2DO1DO0
The SPI read command is performed with 16 clock pulses. A multiple byte read command is performed by adding
blocks of 8 clock pulses to the previous one.
bit 0: READ bit. The value is 1.
bit 1-7: address AD(6:0). This is the address field of the indexed register.
bit 8-15: data DO(7:0) (read mode). This is the data that are read from the device (MSb first).
bit 16-...: data DO(...-8). Further data in multiple byte reads.
Figure 10. Multiple byte SPI read protocol (2-byte example) (in mode 3)
CS
SPC
SDI
RW
AD6AD5AD4AD3AD2AD1AD0
SDO
DO7DO6DO5DO4DO3DO2DO1DO0DO15 DO14D O13D O12 DO11DO10 DO9DO8
DS13005 - Rev 7 page 17/119

IIS2ICLX
SPI bus interface
5.3.2 SPI write
Figure 11. SPI write protocol (in mode 3)
CS
SPC
SDI
RW DI7 DI6 DI5 DI4 DI3 DI2 DI1 DI0
AD6AD5 AD4AD3 AD2 AD1 AD0
The SPI Write command is performed with 16 clock pulses. A multiple byte write command is performed by
adding blocks of 8 clock pulses to the previous one.
bit 0: WRITE bit. The value is 0.
bit 1-7: address AD(6:0). This is the address field of the indexed register.
bit 8-15: data DI(7:0) (write mode). This is the data that is written inside the device (MSb first).
bit 16-... : data DI(...-8). Further data in multiple byte writes.
Figure 12. Multiple byte SPI write protocol (2-byte example) (in mode 3)
CS
SPC
SDI
DI7 DI6 DI5 DI4 DI3 DI2 DI1 DI0 DI15 DI14 DI13 DI12 DI11 DI10 DI9 DI8
RW
AD6AD5AD4AD3AD2AD1AD0
5.3.3 SPI read in 3-wire mode
A 3-wire mode is entered by setting the CTRL3_C (12h) (SIM) bit equal to 1 (SPI serial interface mode selection).
Figure 13. SPI read protocol in 3-wire mode (in mode 3)
CS
SPC
SDI/O
RW DO7 DO6 DO5 DO4 DO3 DO2 DO1 DO0
AD6 AD5 AD4 AD3 AD2 AD1 AD0
The SPI read command is performed with 16 clock pulses:
bit 0: READ bit. The value is 1.
bit 1-7: address AD(6:0). This is the address field of the indexed register.
bit 8-15: data DO(7:0) (read mode). This is the data that is read from the device (MSb first).
A multiple read command is also available in 3-wire mode.
DS13005 - Rev 7 page 18/119

IIS2ICLX
Master I²C interface
5.4 Master I²C interface
If the IIS2ICLX is configured in mode 2, a master I²C line is available. The master serial interface is mapped to the
following dedicated pins.
Table 15. Master I²C pin details
Pin name Pin description
MSCL I²C serial clock master
MSDA I²C serial data master
MDRDY I²C master external synchronization signal
DS13005 - Rev 7 page 19/119

IIS2ICLX
Functionality
6 Functionality
6.1 Block diagram of filters
Figure 14. Block diagram of filters
CS
|     |     |     |     | I2C/SPI  | SCL/SPC |
| --- | --- | --- | --- | -------- | ------- |
XL
| S         |     |          | Composite | Interface | S D A /SDIO |
| --------- | --- | -------- | --------- | --------- | ----------- |
| front-end |     |          |           |           | S D O       |
| M E       |     |          | Filter    |           |             |
| E N       |     | Low Pass |           |           |             |
Filter
ADC
| M S |     | (LPF1)  | Digital     |     |     |
| --- | --- | ------- | ----------- | --- | --- |
| S O |     |         | Processing  |     |     |
INT1
| R Temperature  |     |     | and | Interrupt |     |
| -------------- | --- | --- | --- | --------- | --- |
functions
sensor
Mng
INT2
Voltage and
|          | Trimming Circuit  | Clock & Phase  | Power      |     |     |
| -------- | ----------------- | -------------- | ---------- | --- | --- |
| current  |                   |                |            | FTP |     |
|          | &Test Interface   | Generator      | Management |     |     |
reference
6.1.1 Block diagrams of the accelerometer filters
In the IIS2ICLX, the filtering chain for the accelerometer part is composed of the following:
• Digital filter (LPF1)
• Composite filter
Details of the block diagram appear in the following figure.
Figure 15. Accelerometer UI chain
Digital
LP Filter
LPF1
Composite
ADC
Filter
ODR_XL[3:0]
DS13005 - Rev 7 page 20/119

IIS2ICLX
Block diagram of filters
Figure 16. Accelerometer composite filter
LPF2_XL_EN
USR_OFF_ON_OUT
HP_SLOPE_XL_EN
0 0
Digital 0
USER
LP Filter 1
OFFSET
LPF2
1 USR_OFF_W
OFS_USR[7:0]
LPF1 FIFO
output HPCF_XL[2:0]
1 1
Wake-up
0 0
Digital
HP Filter USR_OFF_ON_WU SLOPE_FDS I2C/ SPI
001
010
…
111
1
HPCF_XL[2:0]
SLOPE
000
FILTER
HPCF_XL[2:0]
S/D Tap
DS13005 - Rev 7 page 21/119

IIS2ICLX
FIFO
6.2 FIFO
The presence of a FIFO buffer allows consistent power saving for the system since the host processor does not
need to continuously poll data from the sensor, but it can wake up only when needed and burst the significant
data out from the FIFO.
The IIS2ICLX embeds 3 KB of data in FIFO to store the following data:
• Accelerometer
• External sensors (up to 4)
• Timestamp
• Temperature
The applications have maximum flexibility in choosing the rate of batching for physical sensors with FIFO-
dedicated configurations: accelerometer and temperature sensor batch rates can be selected by the user. Writing
external sensor data in FIFO can be triggered by the accelerometer data-ready signal or by an external sensor
interrupt. It is possible to select decimation for timestamp batching in FIFO with a factor of 1, 8, or 32.
The reconstruction of a FIFO stream is a simple task thanks to the FIFO_DATA_OUT_TAG byte that allows
recognizing the meaning of a word in FIFO.
FIFO allows correct reconstruction of the timestamp information for each sensor stored in FIFO. If a change in the
ODR or BDR (batch data rate) configuration is performed, the application can correctly reconstruct the timestamp
and know exactly when the change was applied without disabling FIFO batching. FIFO stores information of the
new configuration and timestamp in which the change was applied in the device.
The programmable FIFO watermark threshold can be set in FIFO_CTRL1 (07h) and FIFO_CTRL2 (08h) using the
WTM[8:0] bits. To monitor the FIFO status, dedicated registers (FIFO_STATUS1 (3Ah), FIFO_STATUS2 (3Bh))
can be read to detect FIFO overrun events, FIFO full status, FIFO empty status, FIFO watermark status, and the
number of unread samples stored in the FIFO. To generate dedicated interrupts on the INT1 and INT2 pins of
these status events, the configuration can be set in INT1_CTRL (0Dh) and INT2_CTRL (0Eh).
The FIFO buffer can be configured according to six different modes:
• Bypass mode
• FIFO mode
• Continuous mode
• Continuous-to-FIFO mode
• Bypass-to-continuous mode
• Bypass-to-FIFO mode
Each mode is selected by the FIFO_MODE_[2:0] bits in the FIFO_CTRL4 (0Ah) register.
6.2.1 Bypass mode
In bypass mode (FIFO_CTRL4 (0Ah)(FIFO_MODE_[2:0] = 000), the FIFO is not operational and it remains empty.
Bypass mode is also used to reset the FIFO when in FIFO mode.
6.2.2 FIFO mode
In FIFO mode (FIFO_CTRL4 (0Ah)(FIFO_MODE_[2:0] = 001) data from the output channels are stored in the
FIFO until it is full.
To reset FIFO content, bypass mode should be selected by writing FIFO_CTRL4 (0Ah)(FIFO_MODE_[2:0])
to 000. After this reset command, it is possible to restart FIFO mode by writing FIFO_CTRL4 (0Ah)
(FIFO_MODE_[2:0]) to 001.
The FIFO buffer memorizes up to 3 KB of data but the depth of the FIFO can be resized by setting the WTM[8:0]
bits in FIFO_CTRL1 (07h) and FIFO_CTRL2 (08h). If the STOP_ON_WTM bit in FIFO_CTRL2 (08h) is set to 1,
FIFO depth is limited up to the WTM[8:0] bits inFIFO_CTRL1 (07h) and FIFO_CTRL2 (08h).
DS13005 - Rev 7 page 22/119

IIS2ICLX
FIFO
6.2.3 Continuous mode
Continuous mode (FIFO_CTRL4 (0Ah)(FIFO_MODE_[2:0] = 110) provides a continuous FIFO update: as new
data arrives, the older data is discarded.
A FIFO threshold flag FIFO_STATUS2 (3Bh)(FIFO_WTM_IA) is asserted when the number of unread samples in
FIFO is greater than or equal to FIFO_CTRL1 (07h) and FIFO_CTRL2 (08h) (WTM[8:0]).
It is possible to route the FIFO_WTM_IA flag to the INT1 pin by writing in register INT1_CTRL (0Dh)
(INT1_FIFO_TH) = 1 or to the INT2 pin by writing in register INT2_CTRL (0Eh)(INT2_FIFO_TH) = 1.
A full-flag interrupt can be enabled, INT1_CTRL (0Dh)(INT1_FIFO_FULL) = 1 or INT2_CTRL (0Eh)
(INT2_FIFO_FULL) = 1, in order to indicate FIFO saturation and eventually read its content all at once.
If an overrun occurs, at least one of the oldest samples in FIFO has been overwritten and the FIFO_OVR_IA flag
in FIFO_STATUS2 (3Bh) is asserted.
In order to empty the FIFO before it is full, it is also possible to pull from FIFO the number of unread samples
available in FIFO_STATUS1 (3Ah) and FIFO_STATUS2 (3Bh)(DIFF_FIFO_[9:0]).
6.2.4 Continuous-to-FIFO mode
In continuous-to-FIFO mode (FIFO_CTRL4 (0Ah)(FIFO_MODE_[2:0] = 011), FIFO behavior changes according to
the trigger event detected in one of the following interrupt events:
• Single tap
• Double tap
• Wake-up
When the selected trigger bit is equal to 1, FIFO operates in FIFO mode.
When the selected trigger bit is equal to 0, FIFO operates in continuous mode.
6.2.5 Bypass-to-continuous mode
In bypass-to-continuous mode (FIFO_CTRL4 (0Ah)(FIFO_MODE_[2:0] = 100), data measurement storage inside
FIFO operates in continuous mode when selected triggers are equal to 1, otherwise FIFO content is reset (bypass
mode).
FIFO behavior changes according to the trigger event detected in one of the following interrupt events:
• Single tap
• Double tap
• Wake-up
6.2.6 Bypass-to-FIFO mode
In bypass-to-FIFO mode (FIFO_CTRL4 (0Ah)(FIFO_MODE_[2:0] = 111), data measurement storage inside FIFO
operates in FIFO mode when selected triggers are equal to 1, otherwise FIFO content is reset (bypass mode).
FIFO behavior changes according to the trigger event detected in one of the following interrupt events:
• Single tap
• Double tap
• Wake-up
DS13005 - Rev 7 page 23/119

IIS2ICLX
FIFO
6.2.7 FIFO reading procedure
The data stored in FIFO are accessible from dedicated registers and each FIFO word is composed of 7
bytes: one tag byte (FIFO_DATA_OUT_TAG (78h), in order to identify the sensor, and 6 bytes of fixed data
(FIFO_DATA_OUT registers from (79h) to (7Eh)).
The DIFF_FIFO_[9:0] field in the FIFO_STATUS1 (3Ah) and FIFO_STATUS2 (3Bh) registers contains the number
of words (1 byte TAG + 6 bytes DATA) collected in FIFO.
In addition, it is possible to configure a counter of the batch events of the accelerometer sensor. The
flag COUNTER_BDR_IA in FIFO_STATUS2 (3Bh) alerts that the counter reaches a selectable threshold
(CNT_BDR_TH_[10:0] field in COUNTER_BDR_REG1 (0Bh) and COUNTER_BDR_REG2 (0Ch)). This allows
triggering the reading of FIFO with the desired latency of one single sensor. As for the other FIFO status
events, the flag COUNTER_BDR_IA can be routed on the INT1 or INT2 pins by asserting the corresponding bits
(INT1_CNT_BDR of INT1_CTRL (0Dh) and INT2_CNT_BDR of INT2_CTRL (0Eh)).
Meta information about the accelerometer sensor configuration changes can be managed by enabling the
ODR_CHG_EN bit in FIFO_CTRL2 (08h).
DS13005 - Rev 7 page 24/119

IIS2ICLX
Frequency response
7 Frequency response
The IIS2ICLX filtering chain and frequency response are detailed in the following figures.
Figure 17. Filtering chain
Analog
|     |     | Low-Pass  | Composite  |
| --- | --- | --------- | ---------- |
Front-end+
|          |     | Filter | Filter           |
| -------- | --- | ------ | ---------------- |
| f0=900Hz | ADC |        |                  |
| MEMS     | ADC | LPF1   | Composite Filter |
The output of the ADC converter is filtered with a digital low-pass filter to ensure the intended sensor’s frequency
response.
The frequency response at the output of the LPF1 filter is indicated in the following figure.
Figure 18. Frequency response at the output of LPF1 filter at different ODR configurations
The frequency response is determined by CAD simulation.
DS13005 - Rev 7 page 25/119

IIS2ICLX
Typical performance characteristics
8 Typical performance characteristics
8.1 Frequency response measurements
The frequency response of the IIS2ICLX, measured on a mechanical shaker, is indicated in the following figures.
Measurements have been performed with the IIS2ICLX configured with the digital composite filter bypassed.
Figure 19. Frequency response- X-axis ODR = 833 Hz, BW = ODR/2
Figure 20. Frequency response - Y-axis ODR = 833 Hz, BW = ODR/2
Figure 21. Frequency response - X-axis ODR = 104 Hz, BW = ODR/2
DS13005 - Rev 7 page 26/119

IIS2ICLX
Frequency response measurements
Figure 22. Frequency response - Y-axis ODR = 104 Hz, BW = ODR/2
Figure 23. Frequency response - X-axis ODR = 12.5 Hz, BW = ODR/2
Figure 24. Frequency response - Y-axis ODR = 12.5 Hz, BW = ODR/2
Note: Characterization data on a few parts. Not measured in production and not guaranteed.
DS13005 - Rev 7 page 27/119

9 Application hints
9.1 IIS2ICLX electrical connections in mode 1
Figure 25. IIS2ICLX electrical connections in mode 1
VDDIO
C2
100nF CS
GND
DNG 2TNI 0AS/ODS 1TNI
SCL
Vdd
VDD
C1
SDx 100nF
GND
GND or VddIO
ADS
GND or VddIO
)1(CN DNG xCS
IIS2ICLX
Application hints
Mode 1
HOST
I2C/SPI (3/4-w)
NC(1)
IIS2ICLX
NC(1)
I2C configuration
Vdd_IO
R R pu pu
SCL
SDA
Pull-up to be added
(1) Leave pin electrically unconnected and soldered to PCB.
R =10kOhm
pu
The device core is supplied through the Vdd line. Power supply decoupling capacitors (C1, C2 = 100 nF ceramic)
should be placed as near as possible to the supply pin of the device (common design practice).
The functionality of the device and the measured acceleration data are selectable and accessible through the
I²C/SPI interface.
The functions, the threshold, and the timing of the two interrupt pins for each sensor can be completely
programmed by the user through the I²C/SPI interface.
DS13005 - Rev 7 page 28/119

9.2 IIS2ICLX electrical connections in mode 2
Figure 26. IIS2ICLX electrical connections in mode 2
VDDIO
C2
100nF CS
GND
DNG 2TNI/YDRDM 0AS/ODS 1TNI
SCL
Vdd
VDD
C1
MSDA 100nF
GND
DNG
LCSM
ADS
Mode 2
HOST
I2C/SPI (3/4-w)
IIS2ICLX
NC(1)
NC(1) Master I2C
External
sensors
I2C configuration
Vdd_IO
R R
pu pu
SCL
SDA
Pull-up to be added
R =10kOhm
pu
)1(CN
IIS2ICLX
IIS2ICLX electrical connections in mode 2
(1) Leave pin electrically unconnected and soldered to PCB.
The device core is supplied through the Vdd line. Power supply decoupling capacitors (C1, C2 = 100 nF ceramic)
should be placed as near as possible to the supply pin of the device (common design practice).
The functionality of the device and the measured acceleration data are selectable and accessible through the
I²C/SPI primary interface.
The functions, the threshold, and the timing of the two interrupt pins for each sensor can be completely
programmed by the user through the I²C/SPI primary interface.
DS13005 - Rev 7 page 29/119

IIS2ICLX
IIS2ICLX electrical connections in mode 2
The procedure to correctly initialize the device is as follows:
1. INT1: Leave unconnected or connect with external pull-down during power-on. Pull-up must be avoided on
this pin.
2. INT2: Recommend to not connect with external pull-up.
3. Properly configure the device:
a. SPI interface: I2C_disable = 1 in CTRL4_C (13h) and DEVICE_CONF = 1 in CTRL9_XL (18h).
b. I²C interface: I2C_disable = 0 (default) in CTRL4_C (13h) and DEVICE_CONF = 1 in CTRL9_XL (18h).
Table 16. Internal pin status
Pin # Name Mode 1 function Mode 2 function Pin status mode 1 Pin status mode 2
Power supply for I/O pins
1 VDD_IO
(recommended 100 nF filter capacitor)
I²C/SPI mode selection Default: input with pull-up. Default: input with pull-up.
2 CS (1:SPI idle mode / I²C communication enabled; Pull-up is disabled if bit Pull-up is disabled if bit
|     |     |     | I2C_disable = 1 in reg 13h and | I2C_disable = 1 in reg 13h and |
| --- | --- | --- | ------------------------------ | ------------------------------ |
0: SPI communication mode / I²C disabled) DEVICE_CONF = 1 in reg 18h. DEVICE_CONF = 1 in reg 18h.
| 3 GND | 0 V supply |     |     |     |
| ----- | ---------- | --- | --- | --- |
Programmable interrupt 2 (INT2)/
|     | Programmable interrupt 2 | Data enable (DEN)/ I²C master |     |     |
| --- | ------------------------ | ----------------------------- | --- | --- |
4 INT2 Default: output forced to ground Default: output forced to ground
|     | (INT2) / Data enable (DEN) | external synchronization signal |     |     |
| --- | -------------------------- | ------------------------------- | --- | --- |
(MDRDY)
SDO SPI 4-wire interface serial data output (SDO) Default: input without pull-up. Default: input without pull-up.
| 5   |     |     | Pull-up is enabled if bit | Pull-up is enabled if bit |
| --- | --- | --- | ------------------------- | ------------------------- |
SA0 I²C least significant bit of the device address (SA0) SDO_PU_EN = 1 in reg 02h. SDO_PU_EN = 1 in reg 02h.
6 INT1 Programmable Interrupt 1 (INT1) Default: input with pull-down(1) Default: input with pull-down(1)
|     |     |     | Default: input without pull-up. | Default: input without pull-up. |
| --- | --- | --- | ------------------------------- | ------------------------------- |
7 SDx Connect to GND or VDD_IO I²C serial data master (MSDA) Pull-up is enabled if bit Pull-up is enabled if bit
|       |                                                    |     | SHUB_PU_EN = 1 in reg 14h in | SHUB_PU_EN = 1 in reg 14h in |
| ----- | -------------------------------------------------- | --- | ---------------------------- | ---------------------------- |
|       |                                                    |     | sensor hub registers.        | sensor hub registers.        |
| 8 VDD | Power supply (recommended 100 nF filter capacitor) |     |                              |                              |
| 9 VDD | Power supply (recommended 100 nF filter capacitor) |     |                              |                              |
10 SCL I²C serial clock (SCL) / SPI serial port clock (SPC) Default: input without pull-up Default: input without pull-up
I²C serial data (SDA)
11 SDA/SDI SPI serial data input (SDI) Default: input without pull-up Default: input without pull-up
3-wire interface serial data output (SDO)
|        |                          |                                | Default: input without pull-up. | Default: input without pull-up. |
| ------ | ------------------------ | ------------------------------ | ------------------------------- | ------------------------------- |
|        |                          |                                | Pull-up is enabled if bit       | Pull-up is enabled if bit       |
| 12 SCx | Connect to GND or VDD_IO | I²C serial clock master (MSCL) |                                 |                                 |
|        |                          |                                | SHUB_PU_EN = 1 in reg 14h in    | SHUB_PU_EN = 1 in reg 14h in    |
|        |                          |                                | sensor hub registers.           | sensor hub registers.           |
| 13 GND |                          | GND                            |                                 |                                 |
14 NC Connect to GND or leave unconnected
15 NC Connect to GND or leave unconnected
16 NC Connect to GND or leave unconnected

1. INT1 must be set to 0 or left unconnected during power-on.

DS13005 - Rev 7 page 30/119

IIS2ICLX
Register map
10 Register map
The table given below provides a list of the 8/16-bit registers embedded in the device and the corresponding
addresses.
Table 17. Registers address map
Register address
| Name | Type |     | Default | Comment |
| ---- | ---- | --- | ------- | ------- |
Hex Binary
| FUNC_CFG_ACCESS          | R/W 01  | 00000001 | 00000000 |             |
| ------------------------ | ------- | -------- | -------- | ----------- |
| PIN_CTRL                 | R/W 02  | 00000010 | 00111111 |             |
| RESERVED                 | - 03-06 |          |          | Reserved    |
| FIFO_CTRL1               | R/W 07  | 00000111 | 00000000 |             |
| FIFO_CTRL2               | R/W 08  | 00001000 | 00000000 |             |
| FIFO_CTRL3               | R/W 09  | 00001001 | 00000000 |             |
| FIFO_CTRL4               | R/W 0A  | 00001010 | 00000000 |             |
| COUNTER_BDR_REG1         | R/W 0B  | 00001011 | 00000000 |             |
| COUNTER_BDR_REG2         | R/W 0C  | 00001100 | 00000000 |             |
| INT1_CTRL                | R/W 0D  | 00001101 | 00000000 |             |
| INT2_CTRL                | R/W 0E  | 00001110 | 00000000 |             |
| WHO_AM_I                 | R 0F    | 00001111 | 01101011 |             |
| CTRL1_XL                 | R/W 10  | 00010000 | 00000000 |             |
| RESERVED                 | - 11    |          |          | Reserved    |
| CTRL3_C                  | R/W 12  | 00010010 | 00000100 |             |
| CTRL4_C                  | R/W 13  | 00010011 | 00000000 |             |
| CTRL5_C                  | R/W 14  | 00010100 | 00000000 |             |
| CTRL6_C                  | R/W 15  | 00010101 | 00000000 |             |
| CTRL7_XL                 | R/W 16  | 00010110 | 00000000 |             |
| CTRL8_XL                 | R/W 17  | 00010111 | 00000000 |             |
| CTRL9_XL                 | R/W 18  | 00011000 | 11100000 |             |
| CTRL10_C                 | R/W 19  | 00011001 | 00000000 |             |
| ALL_INT_SRC              | R 1A    | 00011010 | output   |             |
| WAKE_UP_SRC              | R 1B    | 00011011 | output   |             |
| TAP_SRC                  | R 1C    | 00011100 | output   |             |
| DEN_SRC                  | R 1D    | 00011101 | output   |             |
| STATUS_REG               | R 1E    | 00011110 | output   |             |
| RESERVED                 | - 1F    |          |          | Reserved    |
| OUT_TEMP_L               | R 20    | 00100000 | output   |             |
| OUT_TEMP_H               | R 21    | 00100001 | output   |             |
| RESERVED                 | - 22-27 |          |          | Reserved    |
| OUTX_L_A                 | R 28    | 00101000 | output   |             |
| OUTX_H_A                 | R 29    | 00101001 | output   |             |
| OUTY_L_A                 | R 2A    | 00101010 | output   |             |
| OUTY_H_A                 | R 2B    | 00101011 | output   |             |
| RESERVED                 | - 2C-34 |          |          | Reserved    |
| EMB_FUNC_STATUS_MAINPAGE | R 35    | 00110101 | output   |             |
| DS13005 - Rev 7          |         |          |          | page 31/119 |

IIS2ICLX
Register map
Register address
| Name | Type |     | Default | Comment |
| ---- | ---- | --- | ------- | ------- |
Hex Binary
| FSM_STATUS_A_MAINPAGE  | R 36    | 00110110 | output   |          |
| ---------------------- | ------- | -------- | -------- | -------- |
| FSM_STATUS_B_MAINPAGE  | R 37    | 00110111 | output   |          |
| MLC_STATUS_MAINPAGE    | R 38    | 00111000 | output   |          |
| STATUS_MASTER_MAINPAGE | R 39    | 00111001 | output   |          |
| FIFO_STATUS1           | R 3A    | 00111010 | output   |          |
| FIFO_STATUS2           | R 3B    | 00111011 | output   |          |
| RESERVED               | - 3C-3F |          |          | Reserved |
| TIMESTAMP0             | R 40    | 01000000 | output   |          |
| TIMESTAMP1             | R 41    | 01000001 | output   |          |
| TIMESTAMP2             | R 42    | 01000010 | output   |          |
| TIMESTAMP3             | R 43    | 01000011 | output   |          |
| RESERVED               | - 44-55 |          |          | Reserved |
| TAP_CFG0               | R/W 56  | 01010110 | 00000000 |          |
| TAP_CFG1               | R/W 57  | 01010111 |          |          |
| TAP_CFG2               | R/W 58  | 01011000 | 00000000 |          |
| RESERVED               | - 59    |          |          | Reserved |
| INT_DUR2               | R/W 5A  | 01011010 | 00000000 |          |
| WAKE_UP_THS            | R/W 5B  | 01011011 | 00000000 |          |
| WAKE_UP_DUR            | R/W 5C  | 01011100 | 00000000 |          |
| RESERVED               | - 5D    |          |          | Reserved |
| MD1_CFG                | R/W 5E  | 01011110 | 00000000 |          |
| MD2_CFG                | R/W 5F  | 01011111 | 00000000 |          |
| RESERVED               | - 60-62 |          |          | Reserved |
| INTERNAL_FREQ_FINE     | R 63    | 01100011 | output   |          |
| RESERVED               | - 64-72 |          |          | Reserved |
| X_OFS_USR              | R/W 73  | 01110011 | 00000000 |          |
| Y_OFS_USR              | R/W 74  | 01110100 | 00000000 |          |
| RESERVED               | - 75-77 |          |          | Reserved |
| FIFO_DATA_OUT_TAG      | R 78    | 01111000 | output   |          |
| FIFO_DATA_OUT_X_L      | R 79    | 01111001 | output   |          |
| FIFO_DATA_OUT_X_H      | R 7A    | 01111010 | output   |          |
| FIFO_DATA_OUT_Y_L      | R 7B    | 01111011 | output   |          |
| FIFO_DATA_OUT_Y_H      | R 7C    | 01111100 | output   |          |
| FIFO_DATA_OUT_Z_L      | R 7D    | 01111101 | output   |          |
| FIFO_DATA_OUT_Z_H      | R 7E    | 01111110 | output   |          |
Reserved registers must not be changed. Writing to those registers may cause permanent damage to the device.
The content of the registers that are loaded at boot should not be changed. They contain the factory calibration
values. Their content is automatically restored when the device is powered up.
| DS13005 - Rev 7 |     |     |     | page 32/119 |
| --------------- | --- | --- | --- | ----------- |

IIS2ICLX
Register description
11 Register description
The device contains a set of registers that are used to control its behavior and to retrieve linear acceleration and
temperature data. The register addresses, made up of 7 bits, are used to identify them and to write the data
through the serial interface.
11.1 FUNC_CFG_ACCESS (01h)
Enable embedded functions register (R/W)
Table 18. FUNC_CFG_ACCESS register
FUNC_CFG_ SHUB_REG_
0(1) 0(1) 0(1) 0(1) 0(1) 0(1)
ACCESS ACCESS
1. This bit must be set to 0 for the correct operation of the device.
Table 19. FUNC_CFG_ACCESS register description
Enable access to the embedded functions configuration registers.
FUNC_CFG_ACCESS
Default value: 0(1)
Enable access to the sensor hub (I²C master) registers.
SHUB_REG_ACCESS
Default value: 0(2)
1. Details concerning the embedded functions configuration registers are available in Section 12 Embedded functions register
map and Section 13 Embedded functions register description.
2. Details concerning the sensor hub registers are available in Section 16 Sensor hub register map and Section 17 Sensor
hub register description.
11.2 PIN_CTRL (02h)
SDO pin pull-up enable/disable register (R/W)
Table 20. PIN_CTRL register
SDO_
0(1) 1(2) 1(2) 1(2) 1(2) 1(2) 1(2)
PU_EN
1. This bit must be set to 0 for the correct operation of the device.
2. This bit must be set to 1 for the correct operation of the device.
Table 21. PIN_CTRL register description
Enable pull-up on SDO pin. Default value: 0
SDO_PU_EN
(0: SDO pin pull-up disconnected (default); 1: SDO pin with pull-up)
DS13005 - Rev 7 page 33/119

IIS2ICLX
FIFO_CTRL1 (07h)
11.3 FIFO_CTRL1 (07h)
FIFO control register 1 (R/W)
Table 22. FIFO_CTRL1 register
| WTM7 | WTM6 | WTM5 | WTM4 | WTM3 | WTM2 | WTM1 | WTM0 |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
Table 23. FIFO_CTRL1 register description
FIFO watermark threshold, in conjunction with WTM8 in FIFO_CTRL2 (08h)
WTM[7:0] 1 LSB = 1 sensor (6 bytes) + TAG (1 byte) written in FIFO
Watermark flag rises when the number of bytes written in the FIFO is greater than or equal to the threshold level.
11.4 FIFO_CTRL2 (08h)
FIFO control register 2 (R/W)
Table 24. FIFO_CTRL2 register
| STOP_ON |      |     | ODRCHG |      |      |      |      |
| ------- | ---- | --- | ------ | ---- | ---- | ---- | ---- |
|         | 0(1) | 0   |        | 0(1) | 0(1) | 0(1) | WTM8 |
| _WTM    |      |     | _EN    |      |      |      |      |

1. This bit must be set to 0 for the correct operation of the device.

Table 25. FIFO_CTRL2 register
Sensing chain FIFO stop values memorization at threshold level
| STOP_ON_WTM | (0: FIFO depth is not limited (default); |     |     |     |     |     |     |
| ----------- | ---------------------------------------- | --- | --- | --- | --- | --- | --- |
1: FIFO depth is limited to the threshold level, defined in FIFO_CTRL1 (07h) and FIFO_CTRL2 (08h)
| ODRCHG_EN | Enables ODR CHANGE virtual sensor to be batched in FIFO |     |     |     |     |     |     |
| --------- | ------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
FIFO watermark threshold, in conjunction with WTM[7:0] in FIFO_CTRL1 (07h)
1 LSB = 1 sensor (6 bytes) + TAG (1 byte) written in FIFO
WTM8
Watermark flag rises when the number of bytes written in FIFO is greater than or equal to the threshold
level.
DS13005 - Rev 7 page 34/119

IIS2ICLX
FIFO_CTRL3 (09h)
11.5 FIFO_CTRL3 (09h)
FIFO control register 3 (R/W)
Table 26. FIFO_CTRL3 register
0(1) 0(1) 0(1) 0(1) BDR_XL_3 BDR_XL_2 BDR_XL_1 BDR_XL_0
1. This bit must be set to 0 for the correct operation of the device.
Table 27. FIFO_CTRL3 register description
Selects batch data rate (write frequency in FIFO) for accelerometer data.
(0000: accelerometer not batched in FIFO (default);
0001: 12.5 Hz;
0010: 26 Hz;
0011: 52 Hz;
0100: 104 Hz;
0101: 208 Hz;
BDR_XL_[3:0]
0110: 417 Hz;
0111: 833 Hz;
1000: not allowed;
1001: not allowed;
1010: not allowed;
1011: 1.6 Hz;
1100-1111: not allowed)
DS13005 - Rev 7 page 35/119

IIS2ICLX
FIFO_CTRL4 (0Ah)
11.6 FIFO_CTRL4 (0Ah)
FIFO control register 4 (R/W)
Table 28. FIFO_CTRL4 register
DEC_TS_ DEC_TS_ ODR_T_ ODR_T_ FIFO_ FIFO_ FIFO_
0(1)
BATCH_1 BATCH_0 BATCH_1 BATCH_0 MODE2 MODE1 MODE0
1. This bit must be set to 0 for the correct operation of the device.
Table 29. FIFO_CTRL4 register description
Selects decimation for timestamp batching in FIFO. The write rate is the rate of the accelerometer
divided by the decimation decoder.
(00: timestamp not batched in FIFO (default);
DEC_TS_BATCH_[1:0]
01: decimation 1;
10: decimation 8;
11: decimation 32)
Selects batch data rate (write frequency in FIFO) for temperature data
(00: temperature not batched in FIFO (default);
ODR_T_BATCH_[1:0] 01: 1.6 Hz;
10: 12.5 Hz;
11: 52 Hz)
FIFO mode selection
(000: bypass mode: FIFO disabled;
001: FIFO mode: stops collecting data when FIFO is full;
010: reserved;
FIFO_MODE[2:0] 011: continuous-to-FIFO mode: continuous mode until trigger is deasserted, then FIFO mode;
100: bypass-to-continuous mode: bypass mode until trigger is deasserted, then continuous mode;
101: reserved;
110: continuous mode: if the FIFO is full, the new sample overwrites the older one;
111: bypass-to-FIFO mode: bypass mode until trigger is deasserted, then FIFO mode.)
DS13005 - Rev 7 page 36/119

IIS2ICLX
COUNTER_BDR_REG1 (0Bh)
11.7 COUNTER_BDR_REG1 (0Bh)
Counter batch data rate register 1 (R/W)
Table 30. COUNTER_BDR_REG1 register
dataready_ RST_COUNTER CNT_BDR_
0(1) 0 (1) 0(1) 0(1) 0(1)
pulsed _BDR TH_8
1. This bit must be set to 0 for the correct operation of the device.
Table 31. COUNTER_BDR_REG1 register description
Enables pulsed data-ready mode
dataready_pulsed (0: data-ready latched mode (returns to 0 only after an interface reading) (default);
1: data-ready pulsed mode (the data ready pulses are 75 µs long)
Resets the internal counter of batch events for a single sensor.
RST_COUNTER_BDR
This bit is automatically reset to zero if it was set to 1.
In conjunction with CNT_BDR_TH_[7:0] in COUNTER_BDR_REG2 (0Ch), sets the threshold for the
CNT_BDR_TH_8 internal counter of batch events. When this counter reaches the threshold, the counter is reset and
the COUNTER_BDR_IA flag in FIFO_STATUS2 (3Bh) is set to 1.
11.8 COUNTER_BDR_REG2 (0Ch)
Counter batch data rate register 2 (R/W)
CNT_BDR_ CNT_BDR_ CNT_BDR_ CNT_BDR_ CNT_BDR_ CNT_BDR_ CNT_BDR_ CNT_BDR_
TH_7 TH_6 TH_5 TH_4 TH_3 TH_2 TH_1 TH_0
Table 32. COUNTER_BDR_REG2 register description
In conjunction with CNT_BDR_TH_[10:8] in COUNTER_BDR_REG1 (0Bh), sets the threshold for the
CNT_BDR_TH_[7:0] internal counter of batch events. When this counter reaches the threshold, the counter is reset and the
COUNTER_BDR_IA flag in FIFO_STATUS2 (3Bh) is set to 1.
DS13005 - Rev 7 page 37/119

IIS2ICLX
INT1_CTRL (0Dh)
11.9 INT1_CTRL (0Dh)
INT1 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT1. The output of the pin is the OR combination of
the signals selected here and in MD1_CFG (5Eh).
| DEN_DRDY | INT1_   | INT1_     | INT1_    | INT1_   | INT1_ | 0(1) | INT1_   |
| -------- | ------- | --------- | -------- | ------- | ----- | ---- | ------- |
| _flag    | CNT_BDR | FIFO_FULL | FIFO_OVR | FIFO_TH | BOOT  |      | DRDY_XL |

1. This bit must be set to 0 for the correct operation of the device.

Table 33. INT1_CTRL register description
DEN_DRDY_flag Sends DEN_DRDY (DEN stamped on sensor data flag) to INT1 pin
| INT1_CNT_BDR   |     | Enables COUNTER_BDR_IA interrupt on INT1                |     |     |     |     |     |
| -------------- | --- | ------------------------------------------------------- | --- | --- | --- | --- | --- |
| INT1_FIFO_FULL |     | Enables FIFO full flag interrupt on INT1 pin            |     |     |     |     |     |
| INT1_FIFO_OVR  |     | Enables FIFO overrun interrupt on INT1 pin              |     |     |     |     |     |
| INT1_FIFO_TH   |     | Enables FIFO threshold interrupt on INT1 pin            |     |     |     |     |     |
| INT1_BOOT      |     | Enables boot status on INT1 pin.                        |     |     |     |     |     |
| INT1_DRDY_XL   |     | Enables accelerometer data-ready interrupt on INT1 pin. |     |     |     |     |     |
11.10 INT2_CTRL (0Eh)
INT2 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT2. The output of the pin is the OR combination of
the signals selected here and in MD2_CFG (5Fh).
Table 34. INT2_CTRL register
|      | INT2_   | INT2_     | INT2_    | INT2_   | INT2_     |      | INT2_   |
| ---- | ------- | --------- | -------- | ------- | --------- | ---- | ------- |
| 0(1) |         |           |          |         |           | 0(1) |         |
|      | CNT_BDR | FIFO_FULL | FIFO_OVR | FIFO_TH | DRDY_TEMP |      | DRDY_XL |

1. This bit must be set to 0 for the correct operation of the device.

Table 35. INT2_CTRL register description
| INT2_CNT_BDR   |     | Enables COUNTER_BDR_IA interrupt on INT2 pin |     |     |     |     |     |
| -------------- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
| INT2_FIFO_FULL |     | Enables FIFO full flag interrupt on INT2 pin |     |     |     |     |     |
| INT2_FIFO_OVR  |     | Enables FIFO overrun interrupt on INT2 pin   |     |     |     |     |     |
| INT2_FIFO_TH   |     | Enables FIFO threshold interrupt on INT2 pin |     |     |     |     |     |
INT2_DRDY_TEMP Enables temperature sensor data-ready interrupt on INT2 pin
| INT2_DRDY_XL |     | Enables accelerometer data-ready interrupt on INT2 pin |     |     |     |     |     |
| ------------ | --- | ------------------------------------------------------ | --- | --- | --- | --- | --- |
11.11 WHO_AM_I (0Fh)
WHO_AM_I register (R). This is a read-only register. Its value is fixed at 6Bh.
Table 36. Who_Am_I register
| 0   | 1   | 1   | 0   | 1   | 0   | 1   | 1   |
| --- | --- | --- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 38/119

IIS2ICLX
CTRL1_XL (10h)
11.12 CTRL1_XL (10h)
Accelerometer control register 1 (R/W)
ODR_XL3 ODR_XL2 ODR_XL1 ODR_XL0 FS1_XL FS0_XL LPF2_XL_EN 0(1)

1. This bit must be set to 0 for the correct operation of the device.

Table 37. CTRL1_XL register description
| ODR_XL[3:0] | Accelerometer ODR selection (see Table 38)        |     |     |     |
| ----------- | ------------------------------------------------- | --- | --- | --- |
| FS[1:0]_XL  | Accelerometer full-scale selection (see Table 39) |     |     |     |
Accelerometer high-resolution selection
| LPF2_XL_EN | (0: output from first stage digital filtering selected (default); |     |     |     |
| ---------- | ----------------------------------------------------------------- | --- | --- | --- |
1: output from LPF2 second filtering stage selected)
Table 38. Accelerometer ODR selection
| ODR_XL3 | ODR_XL2 | ODR_XL1 | ODR_XL0 | ODR selection [Hz] |
| ------- | ------- | ------- | ------- | ------------------ |
| 0       | 0       | 0       | 0       | Power-down         |
| 0       | 0       | 0       | 1       | 12.5 Hz            |
| 0       | 0       | 1       | 0       | 26 Hz              |
| 0       | 0       | 1       | 1       | 52 Hz              |
| 0       | 1       | 0       | 0       | 104 Hz             |
| 0       | 1       | 0       | 1       | 208 Hz             |
| 0       | 1       | 1       | 0       | 416 Hz             |
| 0       | 1       | 1       | 1       | 833 Hz             |
| 1       | x       | x       | x       | RESERVED           |
Table 39. Accelerometer full-scale selection
|     | FS[1:0]_XL |     |     | XL_FS  |
| --- | ---------- | --- | --- | ------ |
|     | 00         |     |     | ±0.5 g |
|     | 01         |     |     | ±3 g   |
|     | 10         |     |     | ±1 g   |
|     | 11         |     |     | ±2 g   |
DS13005 - Rev 7 page 39/119

IIS2ICLX
CTRL3_C (12h)
11.13 CTRL3_C (12h)
Control register 3 (R/W)
Table 40. CTRL3_C register
BOOT BDU H_LACTIVE PP_OD SIM IF_INC 0(1) SW_RESET
1. This bit must be set to 0 for the correct operation of the device.
Table 41. CTRL3_C register description
Reboots memory content. Default value: 0
BOOT (0: normal mode; 1: reboot memory content)
This bit is automatically cleared.
Block data update. Default value: 0
BDU (0: continuous update;
1: output registers are not updated until MSB and LSB have been read)
Interrupt activation level. Default value: 0
H_LACTIVE
(0: interrupt output pins active high; 1: interrupt output pins active low
Push-pull/open-drain selection on INT1 and INT2 pins. This bit must be set to 0 when H_LACTIVE is set to 1.
PP_OD Default value: 0
(0: push-pull mode; 1: open-drain mode)
SPI serial interface mode selection. Default value: 0
SIM
(0: 4-wire interface; 1: 3-wire interface)
Register address automatically incremented during a multiple byte access with a serial interface (I²C or SPI).
IF_INC Default value: 1
(0: disabled; 1: enabled)
Software reset. Default value: 0
SW_RESET (0: normal mode; 1: reset device)
This bit is automatically cleared.
DS13005 - Rev 7 page 40/119

IIS2ICLX
CTRL4_C (13h)
11.14 CTRL4_C (13h)
Control register 4 (R/W)
Table 42. CTRL4_C register
| 0(1) | 0(1) | INT2_on | 0(1) | DRDY_MASK | I2C_disable | 0(1) | 0(1) |
| ---- | ---- | ------- | ---- | --------- | ----------- | ---- | ---- |
_INT1

1. This bit must be set to 0 for the correct operation of the device.

Table 43. CTRL4_C register description
All interrupt signals available on INT1 pin enable. Default value: 0
| INT2_on_INT1 | (0: interrupt signals divided between INT1 and INT2 pins; |     |     |     |     |     |     |
| ------------ | --------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
1: all interrupt signals in logic or on INT1 pin)
Enables data available
| DRDY_MASK | (0: disabled; |     |     |     |     |     |     |
| --------- | ------------- | --- | --- | --- | --- | --- | --- |
1: mask DRDY on pin until filter settling ends )
Disables I²C interface. Default value: 0
I2C_disable
(0: SPI and I²C interfaces enabled (default); 1: I²C interface disabled)
11.15 CTRL5_C (14h)
Control register 5 (R/W)
Table 44. CTRL5_C register
| 0(1) | 0(1) | 0(1) | 0(1) | 0(1) | 0(1) |        |        |
| ---- | ---- | ---- | ---- | ---- | ---- | ------ | ------ |
|      |      |      |      |      |      | ST1_XL | ST0_XL |

1. This bit must be set to 0 for the correct operation of the device.

Table 45. CTRL5_C register description
Linear acceleration sensor self-test enable. Default value: 00
ST[1:0]_XL
(00: self-test disabled; other: refer to Table 46)
Table 46. Linear acceleration sensor self-test mode selection
| ST1_XL |     | ST0_XL |                         |     | Self-test mode |     |     |
| ------ | --- | ------ | ----------------------- | --- | -------------- | --- | --- |
| 0      |     | 0      | Normal mode             |     |                |     |     |
| 0      |     | 1      | Positive sign self-test |     |                |     |     |
| 1      |     | 0      | Negative sign self-test |     |                |     |     |
| 1      |     | 1      | Not allowed             |     |                |     |     |
DS13005 - Rev 7 page 41/119

IIS2ICLX
CTRL6_C (15h)
11.16 CTRL6_C (15h)
Control register 6 (r/w)
Table 47. CTRL6_C register
| TRIG_EN | LVL1_EN | LVL2_EN | 0(1) | USR_ | 0(1) | 0(1) | 0(1) |
| ------- | ------- | ------- | ---- | ---- | ---- | ---- | ---- |
OFF_W

1. This bit must be set to 0 for the correct operation of the device.

Table 48. CTRL6_C register description
| TRIG_EN | Enables DEN data edge-sensitive trigger mode. Refer to Table 49 . |     |     |     |     |     |     |
| ------- | ----------------------------------------------------------------- | --- | --- | --- | --- | --- | --- |
| LVL1_EN | Enables DEN data level-sensitive trigger mode. Refer to Table 49. |     |     |     |     |     |     |
| LVL2_EN | Enables DEN level-sensitive latched mode. Refer toTable 49.       |     |     |     |     |     |     |
Weight of XL user offset bits of registers X_OFS_USR (73h), Y_OFS_USR (74h).
| USR_OFF_W | (0: 2-10 g/LSB; |     |     |     |     |     |     |
| --------- | --------------- | --- | --- | --- | --- | --- | --- |
1: 2-6 g/LSB)
Table 49. Trigger mode selection
| TRIG_EN, LVL1_EN, LVL2_EN |     |     |                                              |     | Trigger mode |     |     |
| ------------------------- | --- | --- | -------------------------------------------- | --- | ------------ | --- | --- |
|                           | 100 |     | Edge-sensitive trigger mode is selected      |     |              |     |     |
|                           | 010 |     | Level-sensitive trigger mode is selected     |     |              |     |     |
|                           | 011 |     | Level-sensitive latched mode is selected     |     |              |     |     |
|                           | 110 |     | Level-sensitive FIFO enable mode is selected |     |              |     |     |
11.17 CTRL7_XL (16h)
Control register 7 (R/W)
Table 50. CTRL7_XL register
USR_OFF_
| 0(1) | 0(1) | 0(1) | 0(1) | 0 (1) | 0(1) |     | 0(1) |
| ---- | ---- | ---- | ---- | ----- | ---- | --- | ---- |
ON_OUT

1. This bit must be set to 0 for the correct operation of the device.

Table 51. CTRL7_XL register description
Enables accelerometer user offset correction block; it's valid for the low-pass path - see Figure 16. Accelerometer
composite filter . Default value: 0
USR_OFF_ON_OUT
(0: accelerometer user offset correction block bypassed;
1: accelerometer user offset correction block enabled)
DS13005 - Rev 7 page 42/119

IIS2ICLX
CTRL8_XL (17h)
11.18 CTRL8_XL (17h)
Control register 8 (R/W)
Table 52. CTRL8_XL register
HPCF_XL_2 HPCF_XL_1 HPCF_XL_0 HP_REF_ FASTSETTL_ HP_SLOPE_ 0(1) 0(1)
|     |     | MODE_XL | MODE_XL | XL_EN |     |
| --- | --- | ------- | ------- | ----- | --- |

1. This bit must be set to 0 for the correct operation of the device.

HPCF_XL_[2:0] Accelerometer LPF2 and HP filter configuration and cutoff setting. Refer to Table 53.
Enables accelerometer high-pass filter reference mode (valid for high-pass path -
| HP_REF_MODE_XL | HP_SLOPE_XL_EN bit must be 1). Default value: 0(1)(2) |     |     |     |     |
| -------------- | ----------------------------------------------------- | --- | --- | --- | --- |
(0: disabled, 1: enabled)
Enables accelerometer LPF2 and HPF fast-settling mode. The filter sets the second samples after
FASTSETTL_MODE_XL writing this bit. Active only during device exit from power-down mode. Default value: 0
(0: disabled, 1: enabled)
Accelerometer slope filter / high-pass filter selection. Refer to Figure 16. Accelerometer composite
HP_SLOPE_XL_EN
filter.

1. HPCF_XL_[2:0] must be set to 111 before enabling this bit.
2. When enabled, the first output data have to be discarded.

Table 53. Accelerometer bandwidth configurations
Filter type HP_SLOPE_XL_EN LPF2_XL_EN HPCF_XL_[2:0] Bandwidth
|          |     | 0   |     | -   | ODR/2  |
| -------- | --- | --- | --- | --- | ------ |
|          |     |     |     | 000 | ODR/4  |
|          |     |     |     | 001 | ODR/10 |
|          |     |     |     | 010 | ODR/20 |
| Low pass | 0   |     |     | 011 | ODR/45 |
1
|                 |     |     |     | 100 | ODR/100       |
| --------------- | --- | --- | --- | --- | ------------- |
|                 |     |     |     | 101 | ODR/200       |
|                 |     |     |     | 110 | ODR/400       |
|                 |     |     |     | 111 | ODR/800       |
|                 |     |     |     | 000 | SLOPE (ODR/4) |
|                 |     |     |     | 001 | ODR/10        |
|                 |     |     |     | 010 | ODR/20        |
|                 |     |     |     | 011 | ODR/45        |
| High pass       | 1   | -   |     |     |               |
|                 |     |     |     | 100 | ODR/100       |
|                 |     |     |     | 101 | ODR/200       |
|                 |     |     |     | 110 | ODR/400       |
|                 |     |     |     | 111 | ODR/800       |
| DS13005 - Rev 7 |     |     |     |     | page 43/119   |

IIS2ICLX
CTRL9_XL (18h)
11.19 CTRL9_XL (18h)
Control register 9 (R/W)
Table 54. CTRL9_XL register
DEVICE
DEN_X DEN_Y 1(1) 1(1) DEN_EN DEN_LH 0(2)
_CONF
1. This bit must be set to 1 to properly use the DEN feature.
2. This bit must be set to 0 for the correct operation of the device.
Table 55. CTRL9_XL register description
DEN value stored in LSB of X-axis. Default value: 1
DEN_X
(0: DEN not stored in X-axis LSB; 1: DEN stored in X-axis LSB)
DEN value stored in LSB of Y-axis. Default value: 1
DEN_Y
(0: DEN not stored in Y-axis LSB; 1: DEN stored in Y-axis LSB)
Enable DEN functionality. Default value: 0
DEN_EN
(0: disabled; 1: enabled)
DEN active level configuration. Default value: 0
DEN_LH
(0: active low; 1: active high)
Enables the proper device configuration. Default value: 0
(0: default; 1: enabled)
DEVICE_CONF
It is recommended to set this bit to 1 at initialization phase (and after any software reset) and always keep it
to 1 afterwards.
11.20 CTRL10_C (19h)
Control register 10 (R/W)
Table 56. CTRL10_C register
TIMESTAMP
0(1) 0(1) 0(1) 0(1) 0(1) 0(1) 0(1)
_EN
1. This bit must be set to 0 for the correct operation of the device.
Table 57. CTRL10_C register description
Enables timestamp counter. Default value: 0
(0: disabled; 1: enabled)
TIMESTAMP_EN
The counter is readable in TIMESTAMP0 (40h), TIMESTAMP1 (41h), TIMESTAMP2 (42h), and
TIMESTAMP3 (43h).
DS13005 - Rev 7 page 44/119

IIS2ICLX
ALL_INT_SRC (1Ah)
11.21 ALL_INT_SRC (1Ah)
Source register for all interrupts (R)
Table 58. ALL_INT_SRC register
TIMESTAMP SLEEP_ DOUBLE_ SINGLE_
0 0 WU_IA 0
_ENDCOUNT CHANGE TAP TAP
Table 59. ALL_INT_SRC register description
TIMESTAMP_ENDCOUNT Alerts timestamp overflow within 6.4 ms
Detects change event in stationary/motion status. Default value: 0
SLEEP_CHANGE
(0: change status not detected; 1: change status detected)
Double-tap event status. Default value: 0
DOUBLE_TAP
(0:event not detected, 1: event detected)
Single-tap event status. Default value: 0
SINGLE_TAP
(0:event not detected, 1: event detected)
Wake-up event status. Default value: 0
WU_IA
(0: event not detected, 1: event detected)
11.22 WAKE_UP_SRC (1Bh)
Wake-up interrupt source register (R)
Table 60. WAKE_UP_SRC register
SLEEP_ SLEEP_
0 0 WU_IA X_WU Y_WU 0
CHANGE_IA STATE
Table 61. WAKE_UP_SRC register description
Detects change event in stationary/motion status. Default value: 0
SLEEP_CHANGE_IA
(0: change status not detected; 1: change status detected)
Sleep status bit. Default value: 0
SLEEP_STATE
(0: sleep event not detected; 1: sleep event detected)
Wake-up event detection status. Default value: 0
WU_IA
(0: wake-up event not detected; 1: wake-up event detected.)
Wake-up event detection status on X-axis. Default value: 0
X_WU
(0: wake-up event on X-axis not detected; 1: wake-up event on X-axis detected)
Wake-up event detection status on Y-axis. Default value: 0
Y_WU
(0: wake-up event on Y-axis not detected; 1: wake-up event on Y-axis detected)
DS13005 - Rev 7 page 45/119

IIS2ICLX
TAP_SRC (1Ch)
11.23 TAP_SRC (1Ch)
Tap source register (R)
Table 62. TAP_SRC register
SINGLE_ DOUBLE
0 TAP_IA TAP_SIGN X_TAP Y_TAP 0
TAP TAP
Table 63. TAP_SRC register description
Tap event detection status. Default: 0
TAP_IA
(0: tap event not detected; 1: tap event detected)
Single-tap event status. Default value: 0
SINGLE_TAP
(0: single tap event not detected; 1: single tap event detected)
Double-tap event detection status. Default value: 0
DOUBLE_TAP
(0: double-tap event not detected; 1: double-tap event detected)
Sign of acceleration detected by tap event. Default: 0
TAP_SIGN (0: positive sign of acceleration detected by tap event;
1: negative sign of acceleration detected by tap event)
Tap event detection status on X-axis. Default value: 0
X_TAP
(0: tap event on X-axis not detected; 1: tap event on X-axis detected)
Tap event detection status on Y-axis. Default value: 0
Y_TAP
(0: tap event on Y-axis not detected; 1: tap event on Y-axis detected)
11.24 DEN_SRC (1Dh)
DEN data-ready register (R)
Table 64. DEN_SRC register
DEN_DRDY 0 0 0 0 0 0 0
Table 65. DEN_SRC register description
DEN data-ready signal. It is set high when data output is related to the data coming from a DEN active
DEN_DRDY
condition. (1)
1. The DEN data-ready signal can be latched or pulsed depending on the value of the dataready_pulsed bit of the
COUNTER_BDR_REG1 (0Bh) register.
DS13005 - Rev 7 page 46/119

IIS2ICLX
STATUS_REG (1Eh)
11.25 STATUS_REG (1Eh)
Status register (R)
Table 66. STATUS_REG register
0 0 0 0 0 TDA 0 XLDA
Table 67. STATUS_REG register description
Temperature new data available. Default: 0
TDA (0: no set of data is available at temperature sensor output;
1: a new set of data is available at temperature sensor output)
Accelerometer new data available. Default value: 0
XLDA (0: no set of data available at accelerometer output;
1: a new set of data is available at accelerometer output)
11.26 OUT_TEMP_L (20h), OUT_TEMP_H (21h)
Temperature data output register (R). L and H registers together express a 16-bit word in two’s complement.
Table 68. OUT_TEMP_L register
Temp7 Temp6 Temp5 Temp4 Temp3 Temp2 Temp1 Temp0
Table 69. OUT_TEMP_H register
Temp15 Temp14 Temp13 Temp12 Temp11 Temp10 Temp9 Temp8
Table 70. OUT_TEMP register description
Temp[15:0] Temperature sensor output data. The value is expressed as two’s complement.
DS13005 - Rev 7 page 47/119

IIS2ICLX
OUTX_L_A (28h) and OUTX_H_A (29h)
11.27 OUTX_L_A (28h) and OUTX_H_A (29h)
Linear acceleration sensor X-axis output register (R). The value is expressed as a 16-bit word in two’s
complement.
Table 71. OUTX_L_A register
| D7  | D6  | D5  | D4  | D3  | D2  | D1  | D0  |
| --- | --- | --- | --- | --- | --- | --- | --- |
Table 72. OUTX_H_A register
| D15 | D14 | D13 | D12 | D11 | D10 | D9  | D8  |
| --- | --- | --- | --- | --- | --- | --- | --- |
Table 73. OUTX_H_A register description
| D[15:0] X-axis linear acceleration value. D[15:0] expressed in two’s complement. |     |     |     |     |     |     |     |
| -------------------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
11.28 OUTY_L_A (2Ah) and OUTY_H_A (2Bh)
Linear acceleration sensor Y-axis output register (R). The value is expressed as a 16-bit word in two’s
complement.
Table 74. OUTY_L_A register
| D7  | D6  | D5  | D4  | D3  | D2  | D1  | D0  |
| --- | --- | --- | --- | --- | --- | --- | --- |
Table 75. OUTY_H_A register
| D15 | D14 | D13 | D12 | D11 | D10 | D9  | D8  |
| --- | --- | --- | --- | --- | --- | --- | --- |
Table 76. OUTY_H_A register description
| D[15:0] Y-axis linear acceleration value. D[15:0] expressed in two’s complement. |     |     |     |     |     |     |     |
| -------------------------------------------------------------------------------- | --- | --- | --- | --- | --- | --- | --- |
11.29 EMB_FUNC_STATUS_MAINPAGE (35h)
Embedded function status register (R)
Table 77. EMB_FUNC_STATUS_MAINPAGE register
| IS_FSM_LC | 0   | 0   | 0   | 0   | 0   | 0   | 0   |
| --------- | --- | --- | --- | --- | --- | --- | --- |
Table 78. EMB_FUNC_STATUS_MAINPAGE register description
Interrupt status bit for FSM long counter timeout interrupt event.
IS_FSM_LC
(1: interrupt detected; 0: no interrupt)
DS13005 - Rev 7 page 48/119

IIS2ICLX
FSM_STATUS_A_MAINPAGE (36h)
11.30 FSM_STATUS_A_MAINPAGE (36h)
Finite state machine status register (R)
Table 79. FSM_STATUS_A_MAINPAGE register
IS_FSM8 IS_FSM7 IS_FSM6 IS_FSM5 IS_FSM4 IS_FSM3 IS_FSM2 IS_FSM1
Table 80. FSM_STATUS_A_MAINPAGE register description
IS_FSM8 Interrupt status bit for FSM8 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM7 Interrupt status bit for FSM7 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM6 Interrupt status bit for FSM6 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM5 Interrupt status bit for FSM5 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM4 Interrupt status bit for FSM4 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM3 Interrupt status bit for FSM3 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM2 Interrupt status bit for FSM2 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM1 Interrupt status bit for FSM1 interrupt event. (1: interrupt detected; 0: no interrupt)
11.31 FSM_STATUS_B_MAINPAGE (37h)
Finite state machine status register (R)
Table 81. FSM_STATUS_B_MAINPAGE register
IS_FSM16 IS_FSM15 IS_FSM14 IS_FSM13 IS_FSM12 IS_FSM11 IS_FSM10 IS_FSM9
Table 82. FSM_STATUS_B_MAINPAGE register description
IS_FSM16 Interrupt status bit for FSM16 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM15 Interrupt status bit for FSM15 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM14 Interrupt status bit for FSM14 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM13 Interrupt status bit for FSM13 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM12 Interrupt status bit for FSM12 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM11 Interrupt status bit for FSM11 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM10 Interrupt status bit for FSM10 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM9 Interrupt status bit for FSM9 interrupt event. (1: interrupt detected; 0: no interrupt)
DS13005 - Rev 7 page 49/119

IIS2ICLX
MLC_STATUS_MAINPAGE (38h)
11.32 MLC_STATUS_MAINPAGE (38h)
Machine learning core status register (R)
Table 83. MLC_STATUS_MAINPAGE register
IS_MLC8 IS_MLC7 IS_MLC6 IS_MLC5 IS_MLC4 IS_MLC3 IS_MLC2 IS_MLC1
Table 84. MLC_STATUS_MAINPAGE register description
| IS_MLC8 | Interrupt status bit for MLC8 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
| ------- | --------------------------------------------------------------------------------------- | --- | --- | --- | --- |
| IS_MLC7 | Interrupt status bit for MLC7 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
| IS_MLC6 | Interrupt status bit for MLC6 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
| IS_MLC5 | Interrupt status bit for MLC5 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
| IS_MLC4 | Interrupt status bit for MLC4 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
| IS_MLC3 | Interrupt status bit for MLC3 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
| IS_MLC2 | Interrupt status bit for MLC2 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
| IS_MLC1 | Interrupt status bit for MLC1 interrupt event. (1: interrupt detected; 0: no interrupt) |     |     |     |     |
11.33 STATUS_MASTER_MAINPAGE (39h)
Sensor hub source register (R)
Table 85. STATUS_MASTER_MAINPAGE register
| WR_ONCE_ | SLAVE3_ | SLAVE2_ | SLAVE1_ | SLAVE0_ | SENS_HUB_ |
| -------- | ------- | ------- | ------- | ------- | --------- |
0 0
| DONE | NACK | NACK | NACK | NACK | ENDOP |
| ---- | ---- | ---- | ---- | ---- | ----- |
Table 86. STATUS_MASTER_MAINPAGE register description
When the bit WRITE_ONCE in MASTER_CONFIG (14h) is configured as 1, this bit is set to 1 when the
WR_ONCE_DONE
write operation on slave 0 has been performed and completed. Default value: 0
SLAVE3_NACK This bit is set to 1 if Not acknowledge occurs on slave 3 communication. Default value: 0
SLAVE2_NACK This bit is set to 1 if Not acknowledge occurs on slave 2 communication. Default value: 0
SLAVE1_NACK This bit is set to 1 if Not acknowledge occurs on slave 1 communication. Default value: 0
SLAVE0_NACK This bit is set to 1 if Not acknowledge occurs on slave 0 communication. Default value: 0
Sensor hub communication status. Default value: 0
| SENS_HUB_ENDOP | (0: sensor hub communication not concluded; |     |     |     |     |
| -------------- | ------------------------------------------- | --- | --- | --- | --- |
1: sensor hub communication concluded)
DS13005 - Rev 7 page 50/119

IIS2ICLX
FIFO_STATUS1 (3Ah)
11.34 FIFO_STATUS1 (3Ah)
FIFO status register 1 (R)
Table 87. FIFO_STATUS1 register
DIFF_FIFO_7 DIFF_FIFO_6 DIFF_FIFO_5 DIFF_FIFO_4 DIFF_FIFO_3 DIFF_FIFO_2 DIFF_FIFO_1 DIFF_FIFO_0
Table 88. FIFO_STATUS1 register description
Number of unread sensor data (TAG + 6 bytes) stored in FIFO
DIFF_FIFO_[7:0]
In conjunction with DIFF_FIFO[9:8] in FIFO_STATUS2 (3Bh).
11.35 FIFO_STATUS2 (3Bh)
FIFO status register 2 (R)
Table 89. FIFO_STATUS2 register
FIFO_ FIFO_ FIFO_ COUNTER_ FIFO_OVR_
0 DIFF_FIFO_9 DIFF_FIFO_8
WTM_IA OVR_IA FULL_IA BDR_IA LATCHED
Table 90. FIFO_STATUS2 register description
FIFO watermark status. Default value: 0
(0: FIFO filling is lower than WTM;
FIFO_WTM_IA
1: FIFO filling is equal to or greater than WTM)
Watermark is set through bits WTM[8:0] in FIFO_CTRL2 (08h) and FIFO_CTRL1 (07h).
FIFO overrun status. Default value: 0
FIFO_OVR_IA
(0: FIFO is not completely filled; 1: FIFO is completely filled)
Smart FIFO full status. Default value: 0
FIFO_FULL_IA
(0: FIFO is not full; 1: FIFO will be full at the next ODR)
Counter BDR reaches the CNT_BDR_TH_[10:0] threshold set in COUNTER_BDR_REG1 (0Bh) and
COUNTER_BDR_IA COUNTER_BDR_REG2 (0Ch). Default value: 0
This bit is reset when these registers are read.
Latched FIFO overrun status. Default value: 0
FIFO_OVR_LATCHED
This bit is reset when this register is read.
Number of unread sensor data (TAG + 6 bytes) stored in FIFO. Default value: 00
DIFF_FIFO_[9:8]
In conjunction with DIFF_FIFO[7:0] in FIFO_STATUS1 (3Ah)
DS13005 - Rev 7 page 51/119

IIS2ICLX
TIMESTAMP0 (40h), TIMESTAMP1 (41h), TIMESTAMP2 (42h), and TIMESTAMP3 (43h)
11.36 TIMESTAMP0 (40h), TIMESTAMP1 (41h), TIMESTAMP2 (42h), and TIMESTAMP3
(43h)
Timestamp first data output register (R). The value is expressed as a 32-bit word and the bit resolution is 25 µs.
Table 91. TIMESTAMP output registers
| D31 | D30 | D29 | D28 | D27 | D26 | D25 | D24 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| D23 | D22 | D21 | D20 | D19 | D18 | D17 | D16 |
| D15 | D14 | D13 | D12 | D11 | D10 | D9  | D8  |
| D7  | D6  | D5  | D4  | D3  | D2  | D1  | D0  |
Table 92. TIMESTAMP output register description
| D[31:0] | Timestamp output registers: 1LSB = 25 µs |     |     |     |     |     |     |
| ------- | ---------------------------------------- | --- | --- | --- | --- | --- | --- |
The formula below can be used to calculate a better estimation of the actual timestamp resolution:
TS_Res = 1 / (40000 + (0.0015 * INTERNAL_FREQ_FINE * 40000))
where INTERNAL_FREQ_FINE is the content of INTERNAL_FREQ_FINE (63h).
DS13005 - Rev 7 page 52/119

IIS2ICLX
TAP_CFG0 (56h)
11.37 TAP_CFG0 (56h)
Configuration of filtering and tap recognition functions (R/W)
Table 93. TAP_CFG0 register
INT_CLR_ SLEEP_STATUS
0 SLOPE_FDS TAP_X_EN TAP_Y_EN 0 LIR
ON_READ _ON_INT
Table 94. TAP_CFG0 register description
This bit allows immediately clearing the latched interrupts of an event detection upon the read of
the corresponding status register. It must be set to 1 together with LIR. Default value: 0
INT_CLR_ON_READ
(0: latched interrupt signal cleared at the end of the ODR period;
1: latched interrupt signal immediately cleared)
Motion/stationary interrupt mode configuration.
If INT1_SLEEP_CHANGE or INT2_SLEEP_CHANGE bits are enabled, drives the sleep status or
SLEEP_STATUS_ON_INT
sleep change on the INT pins. Default value: 0
(0: sleep change notification on INT pins; 1: sleep status reported on INT pins)
HPF or SLOPE filter selection on wake-up function. Default value: 0 (
SLOPE_FDS
0: SLOPE filter applied; 1: HPF applied)
Enable X direction in tap recognition. Default value: 0
TAP_X_EN
(0: X direction disabled; 1: X direction enabled)
Enable Y direction in tap recognition. Default value: 0
TAP_Y_EN
(0: Y direction disabled; 1: Y direction enabled)
Latched interrupt. Default value: 0
LIR
(0: interrupt request not latched; 1: interrupt request latched)
11.38 TAP_CFG1 (57h)
Tap configuration register (R/W)
Table 95. TAP_CFG1 register
TAP_ TAP_THS TAP_THS TAP_THS TAP_THS TAP_THS
0 0
PRIORITY _X_4 _X_3 _X_2 _X_1 _X_0
Table 96. TAP_CFG1 register description
(0: X max, Y min;
TAP_PRIORITY
1: Y max, X min)
X-axis tap recognition threshold. Default value: 0
TAP_THS_X_[4:0] 1 LSB = FS_XL / (25)
Note: If selecting FS_XL = ±3 g, 1 LSB = 4 / 25 g.
DS13005 - Rev 7 page 53/119

IIS2ICLX
TAP_CFG2 (58h)
11.39 TAP_CFG2 (58h)
Enables interrupt and tap recognition functions (R/W)
Table 97. TAP_CFG2 register
INTERRUPTS TAP_THS_ TAP_THS_ TAP_THS_ TAP_THS_ TAP_THS_
0 0
_ENABLE _Y_4 _Y_3 _Y_2 _Y_1 _Y_0
Table 98. TAP_CFG2 register description
Enable basic interrupts (wake-up, tap). Default value: 0
INTERRUPTS_ENABLE
(0: interrupt disabled; 1: interrupt enabled)
Y-axis tap recognition threshold. Default value: 0
TAP_THS_Y_[4:0] 1 LSB = FS_XL / (25)
Note: If selecting FS_XL = ±3 g, 1 LSB = 4 / 25 g.
11.40 INT_DUR2 (5Ah)
Tap recognition function setting register (R/W)
Table 99. INT_DUR2 register
DUR3 DUR2 DUR1 DUR0 QUIET1 QUIET0 SHOCK1 SHOCK0
Table 100. INT_DUR2 register description
Duration of maximum time gap for double tap recognition. Default: 0000
DUR[3:0] When double tap recognition is enabled, this register expresses the maximum time between two consecutive
detected taps to determine a double tap event. The default value of these bits is 0000 which corresponds to
16/ODR_XL time. If the DUR[3:0] bits are set to a different value, 1LSB corresponds to 32/ODR_XL time.
Expected quiet time after a tap detection. Default value: 00
QUIET[1:0] Quiet time is the time after the first detected tap in which there must not be any overthreshold event. The default
value of these bits is 00 which corresponds to 2/ODR_XL time. If the QUIET[1:0] bits are set to a different value,
1LSB corresponds to 4/ODR_XL time.
Maximum duration of overthreshold event. Default value: 00
SHOCK[1:0] Maximum duration is the maximum time of an overthreshold signal detection to be recognized as a tap event.
The default value of these bits is 00 which corresponds to 4/ODR_XL time. If the SHOCK[1:0] bits are set to a
different value, 1LSB corresponds to 8/ODR_XL time.
DS13005 - Rev 7 page 54/119

IIS2ICLX
WAKE_UP_THS (5Bh)
11.41 WAKE_UP_THS (5Bh)
Single/double-tap selection and wake-up configuration (R/W)
Table 101. WAKE_UP_THS register
SINGLE_ USR_OFF_
WK_THS5 WK_THS4 WK_THS3 WK_THS2 WK_THS1 WK_THS0
DOUBLE_TAP ON_WU
Table 102. WAKE_UP_THS register description
Single/double-tap event enable. Default: 0
SINGLE_DOUBLE_TAP (0: only single-tap event enabled;
1: both single and double-tap events enabled)
Drives the low-pass filtered data with user offset correction (instead of high-pass filtered data) to the
USR_OFF_ON_WU
wakeup function.
Threshold for wakeup: 1 LSB weight depends on WAKE_THS_W in WAKE_UP_DUR (5Ch).
WK_THS[5:0]
Default value: 000000
11.42 WAKE_UP_DUR (5Ch)
Wake-up and sleep mode functions duration setting register (R/W)
Table 103. WAKE_UP_DUR register
WAKE_ WAKE_ WAKE_ SLEEP_ SLEEP_ SLEEP_ SLEEP_
0
DUR1 DUR0 THS_W DUR3 DUR2 DUR1 DUR0
Table 104. WAKE_UP_DUR register description
Wake-up duration event. Default: 00
WAKE_DUR[1:0]
1LSB = 1 ODR_time
Weight of 1 LSB of wakeup threshold. Default: 0
(0: 1 LSB = FS_XL / (26);
WAKE_THS_W 1: 1 LSB = FS_XL / (28))
Note: If selecting FS_XL = ±3 g then:
if WAKE_THS_W = 0, 1 LSB = 4 / 26 g; if WAKE_THS_W = 1, 1 LSB = 4 / 28 g.
Duration to go in sleep mode. Default value: 0000 (this corresponds to 16 ODR)
SLEEP_DUR[3:0]
1 LSB = 512 ODR
DS13005 - Rev 7 page 55/119

IIS2ICLX
MD1_CFG (5Eh)
11.43 MD1_CFG (5Eh)
Functions routing to INT1 pin register (R/W)
Table 105. MD1_CFG register
INT1_SLEEP INT1_ INT1_ INT1_
INT1_WU 0(1) 0(1) INT1_SHUB
_CHANGE SINGLE_TAP DOUBLE_TAP EMB_FUNC
1. This bit must be set to 0 for the correct operation of the device.
Table 106. MD1_CFG register description
Routing stationary/motion recognition event to INT1. Default: 0
INT1_SLEEP_CHANGE(1) (0: routing stationary/motion event to INT1 disabled;
1: routing stationary/motion event to INT1 enabled)
Routing single-tap recognition event to INT1. Default: 0
INT1_SINGLE_TAP (0: routing single-tap event to INT1 disabled;
1: routing single-tap event to INT1 enabled)
Routing wake-up event to INT1. Default value: 0
INT1_WU (0: routing wake-up event to INT1 disabled;
1: routing wake-up event to INT1 enabled)
Routing double-tap event to INT1. Default value: 0
INT1_DOUBLE_TAP (0: routing double-tap event to INT1 disabled;
1: routing double-tap event to INT1 enabled)
Routing embedded functions event to INT1. Default value: 0
INT1_EMB_FUNC (0: routing embedded functions event to INT1 disabled;
1: routing embedded functions event to INT1 enabled)
Routing sensor hub communication concluded event to INT1.
Default value: 0
INT1_SHUB
(0: routing sensor hub communication concluded event to INT1 disabled; 1: routing sensor hub
communication concluded event to INT1 enabled)
1. Stationary/motion interrupt mode (sleep change or sleep status) depends on the SLEEP_STATUS_ON_INT bit in the
TAP_CFG0 (56h) register.
DS13005 - Rev 7 page 56/119

IIS2ICLX
MD2_CFG (5Fh)
11.44 MD2_CFG (5Fh)
Functions routing to INT2 pin register (R/W)
Table 107. MD2_CFG register
| INT2_SLEEP | INT2_      | INT2_WU | 0(1) | INT2_      | 0(1) | INT2_    | INT2_     |
| ---------- | ---------- | ------- | ---- | ---------- | ---- | -------- | --------- |
| _CHANGE    | SINGLE_TAP |         |      | DOUBLE_TAP |      | EMB_FUNC | TIMESTAMP |

1. This bit must be set to 0 for the correct operation of the device.

Table 108. MD2_CFG register description
Routing stationary/motion recognition event to INT2. Default: 0
| INT2_SLEEP_CHANGE(1) |     | (0: routing stationary/motion event to INT2 disabled; |     |     |     |     |     |
| -------------------- | --- | ----------------------------------------------------- | --- | --- | --- | --- | --- |
1: routing stationary/motion event to INT2 enabled)
Single-tap recognition routing to INT2. Default: 0
| INT2_SINGLE_TAP |     | (0: routing single-tap event to INT2 disabled; |     |     |     |     |     |
| --------------- | --- | ---------------------------------------------- | --- | --- | --- | --- | --- |
1: routing single-tap event to INT2 enabled)
Routing wake-up event to INT2. Default value: 0
| INT2_WU |     | (0: routing wake-up event to INT2 disabled; |     |     |     |     |     |
| ------- | --- | ------------------------------------------- | --- | --- | --- | --- | --- |
1: routing wake-up event to INT2 enabled)
Routing double-tap event to INT2. Default value: 0
| INT2_DOUBLE_TAP |     | (0: routing double-tap event to INT2 disabled; |     |     |     |     |     |
| --------------- | --- | ---------------------------------------------- | --- | --- | --- | --- | --- |
1: routing double-tap event to INT2 enabled)
Routing embedded functions event to INT2. Default value: 0
| INT2_EMB_FUNC |     | (0: routing embedded functions event to INT2 disabled; |     |     |     |     |     |
| ------------- | --- | ------------------------------------------------------ | --- | --- | --- | --- | --- |
1: routing embedded functions event to INT2 enabled)
INT2_TIMESTAMP Enables routing the alert for timestamp overflow within 6.4 ms to the INT2 pin.

1. Stationary/motion interrupt mode (sleep change or sleep status) depends on the SLEEP_STATUS_ON_INT bit in the
TAP_CFG0 (56h) register.

DS13005 - Rev 7 page 57/119

IIS2ICLX
INTERNAL_FREQ_FINE (63h)
11.45 INTERNAL_FREQ_FINE (63h)
Internal frequency register (R)
Table 109. INTERNAL_FREQ_FINE register
FREQ_FINE7 FREQ_FINE6 FREQ_FINE5 FREQ_FINE4 FREQ_FINE3 FREQ_FINE2 FREQ_FINE1 FREQ_FINE0
Table 110. INTERNAL_FREQ_FINE register description
Difference in percentage of the effective ODR (and timestamp rate) with respect to the typical. Step: 0.15%.
FREQ_FINE[7:0]
8-bit format, two's complement.
The formula below can be used to calculate a better estimation of the actual ODR:
ODR_Actual = (6667 + ((0.0015 * INTERNAL_FREQ_FINE) * 6667)) / ODR_Coeff
Selected_ODR ODR_Coeff
12.5 512
26 256
52 128
104 64
208 32
416 16
833 8
The Selected_ODR parameter has to be derived from the ODR_XL selection (Table 38. Accelerometer ODR
selection) in order to estimate the accelerometer ODR.
DS13005 - Rev 7 page 58/119

IIS2ICLX
X_OFS_USR (73h)
11.46 X_OFS_USR (73h)
Accelerometer X-axis user offset correction (R/W). The offset value set in the X_OFS_USR offset register is
internally subtracted from the acceleration value measured on the X-axis.
Table 111. X_OFS_USR register
X_OFS_ X_OFS_ X_OFS_ X_OFS_ X_OFS_ X_OFS_ X_OFS_ X_OFS_
USR_7 USR_6 USR_5 USR_4 USR_3 USR_2 USR_1 USR_0
Table 112. X_OFS_USR register description
Accelerometer X-axis user offset correction expressed in two’s complement, weight depends on
X_OFS_USR_[7:0]
USR_OFF_W in CTRL6_C (15h). The value must be in the range [-127 127].
11.47 Y_OFS_USR (74h)
Accelerometer Y-axis user offset correction (R/W). The offset value set in the Y_OFS_USR offset register is
internally subtracted from the acceleration value measured on the Y-axis.
Table 113. Y_OFS_USR register
Y_OFS_ Y_OFS_ Y_OFS_ Y_OFS_ Y_OFS_ Y_OFS_ Y_OFS_ Y_OFS_
USR_7 USR_6 USR_5 USR_4 USR_3 USR_2 USR_1 USR_0
Table 114. Y_OFS_USR register description
Accelerometer Y-axis user offset calibration expressed in two’s complement, weight depends on
Y_OFS_USR_[7:0]
USR_OFF_W in CTRL6_C (15h). The value must be in the range [-127, +127].
DS13005 - Rev 7 page 59/119

IIS2ICLX
FIFO_DATA_OUT_TAG (78h)
11.48 FIFO_DATA_OUT_TAG (78h)
FIFO tag register (R)
Table 115. FIFO_DATA_OUT_TAG register
| TAG_     | TAG_     | TAG_     | TAG_     | TAG_ TAG_CNT_1 | TAG_CNT_0 | TAG_   |
| -------- | -------- | -------- | -------- | -------------- | --------- | ------ |
| SENSOR_4 | SENSOR_3 | SENSOR_2 | SENSOR_1 | SENSOR_0       |           | PARITY |
Table 116. FIFO_DATA_OUT_TAG register description
Identifies the sensor in:
TAG_SENSOR_[4:0] FIFO_DATA_OUT_X_L (79h) and FIFO_DATA_OUT_X_H (7Ah), FIFO_DATA_OUT_Y_L (7Bh) and
FIFO_DATA_OUT_Y_H (7Ch), and FIFO_DATA_OUT_Z_L (7Dh) and FIFO_DATA_OUT_Z_H (7Eh)
For details, refer to Table 117.
| TAG_CNT_[1:0] | 2-bit counter which identifies sensor time slot |     |     |     |     |     |
| ------------- | ----------------------------------------------- | --- | --- | --- | --- | --- |
| TAG_PARITY    | Parity check of TAG content                     |     |     |     |     |     |
Table 117. FIFO tag
|     | TAG_SENSOR_[4:0] |      |     | Sensor name   |     |     |
| --- | ---------------- | ---- | --- | ------------- | --- | --- |
|     |                  | 0x02 |     | Accelerometer |     |     |
|     |                  | 0x03 |     | Temperature   |     |     |
|     |                  | 0x04 |     | Timestamp     |     |     |
|     |                  | 0x05 |     | CFG_Change    |     |     |
0x06
0x07
0x08
0x09
Reserved
0x0A
0x0B
0x0C
0x0D
|     |     | 0x0E |     | Sensor Hub Slave 0 |     |     |
| --- | --- | ---- | --- | ------------------ | --- | --- |
|     |     | 0x0F |     | Sensor Hub Slave 1 |     |     |
|     |     | 0x10 |     | Sensor Hub Slave 2 |     |     |
|     |     | 0x11 |     | Sensor Hub Slave 3 |     |     |
|     |     | 0x19 |     | Sensor Hub Nack    |     |     |
DS13005 - Rev 7 page 60/119

IIS2ICLX
FIFO_DATA_OUT_X_L (79h) and FIFO_DATA_OUT_X_H (7Ah)
11.49 FIFO_DATA_OUT_X_L (79h) and FIFO_DATA_OUT_X_H (7Ah)
FIFO data output X (R)
Table 118. FIFO_DATA_OUT_X_H and FIFO_DATA_OUT_X_L registers
| D15 | D14 | D13 | D12 | D11 | D10 | D9  | D8  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| D7  | D6  | D5  | D4  | D3  | D2  | D1  | D0  |
Table 119. FIFO_DATA_OUT_X_H and FIFO_DATA_OUT_X_L register description
| D[15:0] |     | FIFO X-axis output |     |     |     |     |     |
| ------- | --- | ------------------ | --- | --- | --- | --- | --- |
11.50 FIFO_DATA_OUT_Y_L (7Bh) and FIFO_DATA_OUT_Y_H (7Ch)
FIFO data output Y (R)
Table 120. FIFO_DATA_OUT_Y_H and FIFO_DATA_OUT_Y_L registers
| D15 | D14 | D13 | D12 | D11 | D10 | D9  | D8  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| D7  | D6  | D5  | D4  | D3  | D2  | D1  | D0  |
Table 121. FIFO_DATA_OUT_Y_H and FIFO_DATA_OUT_Y_L register description
| D[15:0] |     | FIFO Y-axis output |     |     |     |     |     |
| ------- | --- | ------------------ | --- | --- | --- | --- | --- |
11.51 FIFO_DATA_OUT_Z_L (7Dh) and FIFO_DATA_OUT_Z_H (7Eh)
FIFO data output Z (R)
Table 122. FIFO_DATA_OUT_Z_H and FIFO_DATA_OUT_Z_L registers
| D15 | D14 | D13 | D12 | D11 | D10 | D9  | D8  |
| --- | --- | --- | --- | --- | --- | --- | --- |
| D7  | D6  | D5  | D4  | D3  | D2  | D1  | D0  |
Table 123. FIFO_DATA_OUT_Z_H and FIFO_DATA_OUT_Z_L register description
| D[15:0] |     | FIFO Z-axis output |     |     |     |     |     |
| ------- | --- | ------------------ | --- | --- | --- | --- | --- |
Note: Fields related to the Z-axis are intended for usage in conjunction with an external sensor.
DS13005 - Rev 7 page 61/119

IIS2ICLX
Embedded functions register map
12 Embedded functions register map
The table given below provides a list of the registers for the embedded functions available in the device and
the corresponding addresses. Embedded functions registers are accessible when FUNC_CFG_EN is set to 1 in
FUNC_CFG_ACCESS (01h).
Table 124. Register address map - embedded functions
Register address
| Name | Type |     | Default | Comment |
| ---- | ---- | --- | ------- | ------- |
Hex Binary
| PAGE_SEL               | R/W 02  | 00000010 | 00000001 |             |
| ---------------------- | ------- | -------- | -------- | ----------- |
| EMB_FUNC_EN_B          | R/W 05  | 00000101 | 00000000 |             |
| PAGE_ADDRESS           | R/W 08  | 00001000 | 00000000 |             |
| PAGE_VALUE             | R/W 09  | 00001001 | 00000000 |             |
| EMB_FUNC_INT1          | R/W 0A  | 00001010 | 00000000 |             |
| FSM_INT1_A             | R/W 0B  | 00001011 | 00000000 |             |
| FSM_INT1_B             | R/W 0C  | 00001100 | 00000000 |             |
| MLC_INT1               | R/W 0D  | 00001101 | 00000000 |             |
| EMB_FUNC_INT2          | R/W 0E  | 00001110 | 00000000 |             |
| FSM_INT2_A             | R 0F    | 00001111 | 01101011 |             |
| FSM_INT2_B             | R/W 10  | 00010000 | 00000000 |             |
| MLC_INT2               | R/W 11  | 00010001 | 00000000 |             |
| EMB_FUNC_STATUS        | R 12    | 00010010 | output   |             |
| FSM_STATUS_A           | R 13    | 00010011 | output   |             |
| FSM_STATUS_B           | R 14    | 00010100 | output   |             |
| MLC_STATUS             | R 15    | 00010101 | output   |             |
| PAGE_RW                | R/W 17  | 00010111 | 00000000 |             |
| RESERVED               | - 18-45 |          |          | Reserved    |
| FSM_ENABLE_A           | R/W 46  | 01000110 | 00000000 |             |
| FSM_ENABLE_B           | R/W 47  | 01000111 | 00000000 |             |
| FSM_LONG_COUNTER_L     | R/W 48  | 01001000 | 00000000 |             |
| FSM_LONG_COUNTER_H     | R/W 49  | 01001001 | 00000000 |             |
| FSM_LONG_COUNTER_CLEAR | R/W 4A  | 01001010 | 00000000 |             |
| FSM_OUTS1              | R 4C    | 01001100 | output   |             |
| FSM_OUTS2              | R 4D    | 01001101 | output   |             |
| FSM_OUTS3              | R 4E    | 01001110 | output   |             |
| FSM_OUTS4              | R 4F    | 01001111 | output   |             |
| FSM_OUTS5              | R 50    | 01010000 | output   |             |
| FSM_OUTS6              | R 51    | 01010001 | output   |             |
| FSM_OUTS7              | R 52    | 01010010 | output   |             |
| FSM_OUTS8              | R 53    | 01010011 | output   |             |
| FSM_OUTS9              | R 54    | 01010100 | output   |             |
| FSM_OUTS10             | R 55    | 01010101 | output   |             |
| FSM_OUTS11             | R 56    | 01010110 | output   |             |
| DS13005 - Rev 7        |         |          |          | page 62/119 |

IIS2ICLX
Embedded functions register map
Register address
| Name | Type |     | Default | Comment |
| ---- | ---- | --- | ------- | ------- |
Hex Binary
| FSM_OUTS12         | R 57    | 01010111 | output   |          |
| ------------------ | ------- | -------- | -------- | -------- |
| FSM_OUTS13         | R 58    | 01011000 | output   |          |
| FSM_OUTS14         | R 59    | 01011001 | output   |          |
| FSM_OUTS15         | R 5A    | 01011010 | output   |          |
| FSM_OUTS16         | R 5B    | 01011011 | output   |          |
| RESERVED           | - 5C-5E |          |          | Reserved |
| EMB_FUNC_ODR_CFG_B | R/W 5F  | 01011111 | 01001011 |          |
| EMB_FUNC_ODR_CFG_C | R/W 60  | 01100000 | 00010101 |          |
| RESERVED           | - 61-66 |          |          | Reserved |
| EMB_FUNC_INIT_B    | RW 67   | 01100111 | 00000000 |          |
| MLC0_SRC           | R 70    | 01110000 | output   |          |
| MLC1_SRC           | R 71    | 01110001 | output   |          |
| MLC2_SRC           | R 72    | 01110010 | output   |          |
| MLC3_SRC           | R 73    | 01110011 | output   |          |
| MLC4_SRC           | R 74    | 01110100 | output   |          |
| MLC5_SRC           | R 75    | 01110101 | output   |          |
| MLC6_SRC           | R 76    | 01110110 | output   |          |
| MLC7_SRC           | R 77    | 01110111 | output   |          |
Reserved registers must not be changed. Writing to those registers may cause permanent damage to the device.
The content of the registers that are loaded at boot should not be changed. They contain the factory calibration
values. Their content is automatically restored when the device is powered up.
| DS13005 - Rev 7 |     |     |     | page 63/119 |
| --------------- | --- | --- | --- | ----------- |

IIS2ICLX
Embedded functions register description
13 Embedded functions register description
13.1 PAGE_SEL (02h)
Enable advanced features dedicated page (R/W)
Table 125. PAGE_SEL register
PAGE_SEL3 PAGE_SEL2 PAGE_SEL1 PAGE_SEL0 0(1) 0(1) 0(1) 1(2)
1. This bit must be set to 0 for the correct operation of the device.
2. This bit must be set to 1 for the correct operation of the device.
Table 126. PAGE_SEL register description
PAGE_SEL[3:0] Selects the advanced features dedicated page. Default value: 0000
13.2 EMB_FUNC_EN_B (05h)
Enable embedded functions register (R/W)
Table 127. EMB_FUNC_EN_B register
0(1) 0(1) 0(1) MLC_EN 0(1) 0(1) 0(1) FSM_EN
1. This bit must be set to 0 for the correct operation of the device.
Table 128. EMB_FUNC_EN_B register description
Enables machine learning core feature. Default value: 0
MLC_EN (0: machine learning core feature disabled;
1: machine learning core feature enabled)
Enables finite state machine (FSM) feature. Default value: 0
FSM_EN
(0: FSM feature disabled; 1: FSM feature enabled)
13.3 PAGE_ADDRESS (08h)
Page address register (R/W)
Table 129. PAGE_ADDRESS register
PAGE_ PAGE_ PAGE_ PAGE_ PAGE_ PAGE_ PAGE_ PAGE_
ADDR7 ADDR6 ADDR5 ADDR4 ADDR3 ADDR2 ADDR1 ADDR0
Table 130. PAGE_ADDRESS register description
After setting the bit PAGE_WRITE / PAGE_READ in register PAGE_RW (17h), this register is used to set
PAGE_ADDR[7:0] the address of the register to be written/read in the advanced features page selected through the bits
PAGE_SEL[3:0] in register PAGE_SEL (02h).
DS13005 - Rev 7 page 64/119

IIS2ICLX
PAGE_VALUE (09h)
13.4 PAGE_VALUE (09h)
Page value register (R/W)
Table 131. PAGE_VALUE register
PAGE_ PAGE_ PAGE_ PAGE_ PAGE_ PAGE_ PAGE_ PAGE_
VALUE7 VALUE6 VALUE5 VALUE4 VALUE3 VALUE2 VALUE1 VALUE0
Table 132. PAGE_VALUE register description
These bits are used to write (if the bit PAGE_WRITE = 1 in register PAGE_RW (17h)) or read (if the bit
PAGE_VALUE[7:0] PAGE_READ = 1 in register PAGE_RW (17h)) the data at the address PAGE_ADDR[7:0] of the selected
advanced features page.
13.5 EMB_FUNC_INT1 (0Ah)
INT1 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT1. The pin's output supplies the OR combination of
the selected signals.
Table 133. EMB_FUNC_INT1 register
INT1_
0(1) 0(1) 0(1) 0(1) 0(1) 0(1) 0(1)
FSM_LC
1. This bit must be set to 0 for the correct operation of the device.
Table 134. EMB_FUNC_INT1 register description
Routing FSM long counter timeout interrupt event to INT1. Default value: 0
INT1_FSM_LC(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
1. This bit is activated if the INT1_EMB_FUNC bit of MD1_CFG (5Eh) is set to 1.
DS13005 - Rev 7 page 65/119

IIS2ICLX
FSM_INT1_A (0Bh)
13.6 FSM_INT1_A (0Bh)
INT1 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT1. The pin's output supplies the OR combination of
the selected signals.
Table 135. FSM_INT1_A register
INT1_FSM8 INT1_FSM7 INT1_FSM6 INT1_FSM5 INT1_FSM4 INT1_FSM3 INT1_FSM2 INT1_FSM1
Table 136. FSM_INT1_A register description
Routing FSM8 interrupt event to INT1. Default value: 0
INT1_FSM8(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM7 interrupt event to INT1. Default value: 0
INT1_FSM7(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM6 interrupt event to INT1. Default value: 0
INT1_FSM6(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM5 interrupt event to INT1. Default value: 0
INT1_FSM5(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM4 interrupt event to INT1. Default value: 0
INT1_FSM4(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM3 interrupt event to INT1. Default value: 0
INT1_FSM3(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM2 interrupt event to INT1. Default value: 0
INT1_FSM2(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM1 interrupt event to INT1. Default value: 0
INT1_FSM1(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
1. This bit is activated if the INT1_EMB_FUNC bit of MD1_CFG (5Eh) is set to 1.
DS13005 - Rev 7 page 66/119

IIS2ICLX
FSM_INT1_B (0Ch)
13.7 FSM_INT1_B (0Ch)
INT1 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT1. The pin's output supplies the OR combination of
the selected signals.
Table 137. FSM_INT1_B register
INT1_FSM16 INT1_FSM15 INT1_FSM14 INT1_FSM13 INT1_FSM12 INT1_FSM11 INT1_FSM10 INT1_FSM9
Table 138. FSM_INT1_B register description
Routing FSM16 interrupt event to INT1. Default value: 0
INT1_FSM16(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM15 interrupt event to INT1. Default value: 0
INT1_FSM15(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM14 interrupt event to INT1. Default value: 0
INT1_FSM14(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM13 interrupt event to INT1. Default value: 0
INT1_FSM13(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM12 interrupt event to INT1. Default value: 0
INT1_FSM12(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM11 interrupt event to INT1. Default value: 0
INT1_FSM11(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM10 interrupt event to INT1. Default value: 0
INT1_FSM10(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM9 interrupt event to INT1. Default value: 0
INT1_FSM9(1)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
1. This bit is activated if the INT1_EMB_FUNC bit of MD1_CFG (5Eh) is set to 1.
DS13005 - Rev 7 page 67/119

IIS2ICLX
MLC_INT1 (0Dh)
13.8 MLC_INT1 (0Dh)
INT1 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT1. The pin's output supplies the OR combination of
the selected signals.
Table 139. MLC_INT1 register
INT1_MLC8 INT1_MLC7 INT1_MLC6 INT1_MLC5 INT1_MLC4 INT1_MLC3 INT1_MLC2 INT1_MLC1
Table 140. MLC_INT1 register description
Routing MLC8 interrupt event to INT1. Default value: 0
INT1_MLC8
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing MLC7 interrupt event to INT1. Default value: 0
INT1_MLC7
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing MLC6 interrupt event to INT1. Default value: 0
INT1_MLC6
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing MLC5 interrupt event to INT1. Default value: 0
INT1_MLC5
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing MLC4 interrupt event to INT1. Default value: 0
INT1_MLC4
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing MLC3 interrupt event to INT1. Default value: 0
INT1_MLC3
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing MLC2 interrupt event to INT1. Default value: 0
INT1_MLC2
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing MLC1 interrupt event to INT1. Default value: 0
INT1_MLC1
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
13.9 EMB_FUNC_INT2 (0Eh)
INT2 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT2. The pin's output supplies the OR combination of
the selected signals.
Table 141. EMB_FUNC_INT2 register
INT2_
0(1) 0(1) 0(1) 0(1) 0(1) 0(1) 0(1)
FSM_LC
1. This bit must be set to 0 for the correct operation of the device.
Table 142. EMB_FUNC_INT2 register description
Routing FSM long counter timeout interrupt event to INT2. Default value: 0
INT2_FSM_LC(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
1. This bit is activated if the INT2_EMB_FUNC bit of MD2_CFG (5Fh) is set to 1.
DS13005 - Rev 7 page 68/119

IIS2ICLX
FSM_INT2_A (0Fh)
13.10 FSM_INT2_A (0Fh)
INT2 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT2. The pin's output supplies the OR combination of
the selected signals.
Table 143. FSM_INT2_A register
INT2_FSM8 INT2_FSM7 INT2_FSM6 INT2_FSM5 INT2_FSM4 INT2_FSM3 INT2_FSM2 INT2_FSM1
Table 144. FSM_INT2_A register description
Routing FSM8 interrupt event to INT2. Default value: 0
INT2_FSM8(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM7 interrupt event to INT2. Default value: 0
INT2_FSM7(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM6 interrupt event to INT2. Default value: 0
INT2_FSM6(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM5 interrupt event to INT2. Default value: 0
INT2_FSM5(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM4 interrupt event to INT2. Default value: 0
INT2_FSM4(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM3 interrupt event to INT2. Default value: 0
INT2_FSM3(1) (0: routing to INT2 disabled; 1: routing to INT2 enabled)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM2 interrupt event to INT2. Default value: 0
INT2_FSM2(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM1 interrupt event to INT2. Default value: 0
INT2_FSM1(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
1. This bit is activated if the INT2_EMB_FUNC bit of MD2_CFG (5Fh) is set to 1.
DS13005 - Rev 7 page 69/119

IIS2ICLX
FSM_INT2_B (10h)
13.11 FSM_INT2_B (10h)
INT2 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT2. The pin's output supplies the OR combination of
the selected signals.
Table 145. FSM_INT2_B register
INT2_FSM16 INT2_FSM15 INT2_FSM14 INT2_FSM13 INT2_FSM12 INT2_FSM11 INT2_FSM10 INT2_FSM9
Table 146. FSM_INT2_B register description
Routing FSM16 interrupt event to INT2. Default value: 0
INT2_FSM16(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM15 interrupt event to INT2. Default value: 0
INT2_FSM15(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM14 interrupt event to INT2. Default value: 0
INT2_FSM14(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM13 interrupt event to INT2. Default value: 0
INT2_FSM13(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM12 interrupt event to INT2. Default value: 0
INT2_FSM12(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM11 interrupt event to INT2. Default value: 0
INT2_FSM11(1) (0: routing to INT2 disabled; 1: routing to INT2 enabled)
(0: routing to INT1 disabled; 1: routing to INT1 enabled)
Routing FSM10 interrupt event to INT2. Default value: 0
INT2_FSM10(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing FSM9 interrupt event to INT2. Default value: 0
INT2_FSM9(1)
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
1. This bit is activated if the INT2_EMB_FUNC bit of MD2_CFG (5Fh) is set to 1.
DS13005 - Rev 7 page 70/119

IIS2ICLX
MLC_INT2 (11h)
13.12 MLC_INT2 (11h)
INT2 pin control register (R/W)
Each bit in this register enables a signal to be carried over INT2. The pin's output supplies the OR combination of
the selected signals.
Table 147. MLC_INT2 register
INT2_MLC8 INT2_MLC7 INT2_MLC6 INT2_MLC5 INT2_MLC4 INT2_MLC3 INT2_MLC2 INT2_MLC1
Table 148. MLC_INT2 register description
Routing MLC8 interrupt event to INT2. Default value: 0
INT2_MLC8
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing MLC7 interrupt event to INT2. Default value: 0
INT2_MLC7
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing MLC6 interrupt event to INT2. Default value: 0
INT2_MLC6
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing MLC5 interrupt event to INT2. Default value: 0
INT2_MLC5
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing MLC4 interrupt event to INT2. Default value: 0
INT2_MLC4
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing MLC3 interrupt event to INT2. Default value: 0
INT2_MLC3
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing MLC2 interrupt event to INT2. Default value: 0
INT2_MLC2
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
Routing MLC1 interrupt event to INT2. Default value: 0
INT2_MLC1
(0: routing to INT2 disabled; 1: routing to INT2 enabled)
13.13 EMB_FUNC_STATUS (12h)
Embedded function status register (R)
Table 149. EMB_FUNC_STATUS register
IS_FSM_LC 0 0 0 0 0 0 0
Table 150. EMB_FUNC_STATUS register description
Interrupt status bit for FSM long counter timeout interrupt event
IS_FSM_LC
(1: interrupt detected; 0: no interrupt)
DS13005 - Rev 7 page 71/119

IIS2ICLX
FSM_STATUS_A (13h)
13.14 FSM_STATUS_A (13h)
Finite state machine status register (R)
Table 151. FSM_STATUS_A register
IS_FSM8 IS_FSM7 IS_FSM6 IS_FSM5 IS_FSM4 IS_FSM3 IS_FSM2 IS_FSM1
Table 152. FSM_STATUS_A register description
IS_FSM8 Interrupt status bit for FSM8 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM7 Interrupt status bit for FSM7 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM6 Interrupt status bit for FSM6 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM5 Interrupt status bit for FSM5 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM4 Interrupt status bit for FSM4 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM3 Interrupt status bit for FSM3 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM2 Interrupt status bit for FSM2 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM1 Interrupt status bit for FSM1 interrupt event. (1: interrupt detected; 0: no interrupt)
13.15 FSM_STATUS_B (14h)
Finite state machine status register (R)
Table 153. FSM_STATUS_B register
IS_FSM16 IS_FSM15 IS_FSM14 IS_FSM13 IS_FSM12 IS_FSM11 IS_FSM10 IS_FSM9
Table 154. FSM_STATUS_B register description
IS_FSM16 Interrupt status bit for FSM16 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM15 Interrupt status bit for FSM15 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM14 Interrupt status bit for FSM14 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM13 Interrupt status bit for FSM13 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM12 Interrupt status bit for FSM12 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM11 Interrupt status bit for FSM11 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM10 Interrupt status bit for FSM10 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_FSM9 Interrupt status bit for FSM9 interrupt event. (1: interrupt detected; 0: no interrupt)
DS13005 - Rev 7 page 72/119

IIS2ICLX
MLC_STATUS (15h)
13.16 MLC_STATUS (15h)
Machine learning core status register (R)
Table 155. MLC_STATUS register
IS_MLC8 IS_MLC7 IS_MLC6 IS_MLC5 IS_MLC4 IS_MLC3 IS_MLC2 IS_MLC1
Table 156. MLC_STATUS register description
IS_MLC8 Interrupt status bit for MLC8 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_MLC7 Interrupt status bit for MLC7 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_MLC6 Interrupt status bit for MLC6 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_MLC5 Interrupt status bit for MLC5 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_MLC4 Interrupt status bit for MLC4 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_MLC3 Interrupt status bit for MLC3 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_MLC2 Interrupt status bit for MLC2 interrupt event. (1: interrupt detected; 0: no interrupt)
IS_MLC1 Interrupt status bit for MLC1 interrupt event. (1: interrupt detected; 0: no interrupt)
13.17 PAGE_RW (17h)
Enable read and write mode of advanced features dedicated page (R/W)
Table 157. PAGE_RW register
EMB_ PAGE_ PAGE_
0(1) 0(1) 0(1) 0(1) 0(1)
FUNC_LIR WRITE READ
1. This bit must be set to 0 for the correct operation of the device.
Table 158. PAGE_RW register description
Latched interrupt mode for embedded functions. Default value: 0
EMB_FUNC_LIR (0: embedded functions interrupt request not latched;
1: embedded functions interrupt request latched)
Enable writes to the selected advanced features dedicated page.(1) Default value: 0
PAGE_WRITE
(1: enable; 0: disable)
Enable reads from the selected advanced features dedicated page.(1) Default value: 0
PAGE_READ
(1: enable; 0: disable)
1. Page selected by PAGE_SEL[3:0] in PAGE_SEL (02h) register.
DS13005 - Rev 7 page 73/119

IIS2ICLX
FSM_ENABLE_A (46h)
13.18 FSM_ENABLE_A (46h)
Enable FSM register (R/W)
Table 159. FSM_ENABLE_A register
FSM8_EN FSM7_EN FSM6_EN FSM5_EN FSM4_EN FSM3_EN FSM2_EN FSM1_EN
Table 160. FSM_ENABLE_A register description
FSM8_EN Enables FSM8. Default value: 0 (0: FSM8 disabled; 1: FSM8 enabled)
FSM7_EN Enables FSM7. Default value: 0 (0: FSM7 disabled; 1: FSM7 enabled)
FSM6_EN Enables FSM6. Default value: 0 (0: FSM6 disabled; 1: FSM6 enabled)
FSM5_EN Enables FSM5. Default value: 0 (0: FSM5 disabled; 1: FSM5 enabled)
FSM4_EN Enables FSM4. Default value: 0 (0: FSM4 disabled; 1: FSM4 enabled)
FSM3_EN Enables FSM3. Default value: 0 (0: FSM3 disabled; 1: FSM3 enabled)
FSM2_EN Enables FSM2. Default value: 0 (0: FSM2 disabled; 1: FSM2 enabled)
FSM1_EN Enables FSM1. Default value: 0 (0: FSM1 disabled; 1: FSM1 enabled)
13.19 FSM_ENABLE_B (47h)
Enable FSM register (R/W)
Table 161. FSM_ENABLE_B register
FSM16_EN FSM15_EN FSM14_EN FSM13_EN FSM12_EN FSM11_EN FSM10_EN FSM9_EN
Table 162. FSM_ENABLE_B register description
FSM16_EN Enables FSM16. Default value: 0 (0: FSM16 disabled; 1: FSM16 enabled)
FSM15_EN Enables FSM15. Default value: 0 (0: FSM15 disabled; 1: FSM15 enabled)
FSM14_EN Enables FSM14. Default value: 0 (0: FSM14 disabled; 1: FSM14 enabled)
FSM13_EN Enables FSM13. Default value: 0 (0: FSM13 disabled; 1: FSM13 enabled)
FSM12_EN Enables FSM12. Default value: 0 (0: FSM12 disabled; 1: FSM12 enabled)
FSM11_EN Enables FSM11. Default value: 0 (0: FSM11 disabled; 1: FSM11 enabled)
FSM10_EN Enables FSM10. Default value: 0 (0: FSM10 disabled; 1: FSM10 enabled)
FSM9_EN Enables FSM9. Default value: 0 (0: FSM9 disabled; 1: FSM9 enabled)
DS13005 - Rev 7 page 74/119

IIS2ICLX
FSM_LONG_COUNTER_L (48h) and FSM_LONG_COUNTER_H (49h)
13.20 FSM_LONG_COUNTER_L (48h) and FSM_LONG_COUNTER_H (49h)
FSM long counter status register (R/W)
Long counter value is an unsigned integer value (16-bit format); this value can be reset using the LC_CLEAR bit
in the FSM_LONG_COUNTER_CLEAR (4Ah) register.
Table 163. FSM_LONG_COUNTER_L register
FSM_LC_7 FSM_LC_6 FSM_LC_5 FSM_LC_4 FSM_LC_3 FSM_LC_2 FSM_LC_1 FSM_LC_0
Table 164. FSM_LONG_COUNTER_L register description
FSM_LC_[7:0] Long counter current value (LSbyte). Default value: 00000000
Table 165. FSM_LONG_COUNTER_H register
FSM_LC_15 FSM_LC_14 FSM_LC_13 FSM_LC_12 FSM_LC_11 FSM_LC_10 FSM_LC_9 FSM_LC_8
Table 166. FSM_LONG_COUNTER_H register description
FSM_LC_[15:8] Long counter current value (MSbyte). Default value: 00000000
13.21 FSM_LONG_COUNTER_CLEAR (4Ah)
FSM long counter reset register (R/W)
Table 167. FSM_LONG_COUNTER_CLEAR register
FSM_LC_ FSM_LC_
0(1) 0(1) 0(1) 0(1) 0(1) 0(1)
CLEARED CLEAR
1. This bit must be set to 0 for the correct operation of the device.
Table 168. FSM_LONG_COUNTER_CLEAR register description
FSM_LC_CLEARED This read-only bit is automatically set to 1 when the long counter reset is done. Default value: 0
FSM_LC_CLEAR Clears FSM long counter value. Default value: 0
DS13005 - Rev 7 page 75/119

IIS2ICLX
FSM_OUTS1 (4Ch)
13.22 FSM_OUTS1 (4Ch)
FSM1 output register (R)
Table 169. FSM_OUTS1 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 170. FSM_OUTS1 register description
P_X FSM1 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM1 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM1 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM1 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM1 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM1 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.23 FSM_OUTS2 (4Dh)
FSM2 output register (R)
Table 171. FSM_OUTS2 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 172. FSM_OUTS2 register description
P_X FSM2 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM2 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM2 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM2 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM2 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM2 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 76/119

IIS2ICLX
FSM_OUTS3 (4Eh)
13.24 FSM_OUTS3 (4Eh)
FSM3 output register (R)
Table 173. FSM_OUTS3 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 174. FSM_OUTS3 register description
P_X FSM3 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM3 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM3 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM3 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM3 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM3 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.25 FSM_OUTS4 (4Fh)
FSM4 output register (R)
Table 175. FSM_OUTS4 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 176. FSM_OUTS4 register description
P_X FSM4 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM4 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM4 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM4 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM4 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM4 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 77/119

IIS2ICLX
FSM_OUTS5 (50h)
13.26 FSM_OUTS5 (50h)
FSM5 output register (R)
Table 177. FSM_OUTS5 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 178. FSM_OUTS5 register description
P_X FSM5 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM5 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM5 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM5 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM5 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM5 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.27 FSM_OUTS6 (51h)
FSM6 output register (R)
Table 179. FSM_OUTS6 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 180. FSM_OUTS6 register description
P_X FSM6 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM6 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM6 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM6 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM6 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM6 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 78/119

IIS2ICLX
FSM_OUTS7 (52h)
13.28 FSM_OUTS7 (52h)
FSM7 output register (R)
Table 181. FSM_OUTS7 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 182. FSM_OUTS7 register description
P_X FSM7 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM7 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM7 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM7 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM7 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM7 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.29 FSM_OUTS8 (53h)
FSM8 output register (R)
Table 183. FSM_OUTS8 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 184. FSM_OUTS8 register description
P_X FSM8 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM8 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM8 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM8 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM8 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM8 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 79/119

IIS2ICLX
FSM_OUTS9 (54h)
13.30 FSM_OUTS9 (54h)
FSM9 output register (R)
Table 185. FSM_OUTS9 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 186. FSM_OUTS9 register description
P_X FSM9 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM9 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM9 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM9 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM9 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM9 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.31 FSM_OUTS10 (55h)
FSM10 output register (R)
Table 187. FSM_OUTS10 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 188. FSM_OUTS10 register description
P_X FSM10 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM10 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM10 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM10 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM10 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM10 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 80/119

IIS2ICLX
FSM_OUTS11 (56h)
13.32 FSM_OUTS11 (56h)
FSM11 output register (R)
Table 189. FSM_OUTS11 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 190. FSM_OUTS11 register description
P_X FSM11 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM11 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM11 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM11 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM11 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM11 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.33 FSM_OUTS12 (57h)
FSM12 output register (R)
Table 191. FSM_OUTS12 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 192. FSM_OUTS12 register description
P_X FSM12 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM12 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM12 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM12 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM12 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM12 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 81/119

IIS2ICLX
FSM_OUTS13 (58h)
13.34 FSM_OUTS13 (58h)
FSM13 output register (R)
Table 193. FSM_OUTS13 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 194. FSM_OUTS13 register description
P_X FSM13 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM13 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM13 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM13 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM13 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM13 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.35 FSM_OUTS14 (59h)
FSM14 output register (R)
Table 195. FSM_OUTS14 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 196. FSM_OUTS14 register description
P_X FSM14 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM14 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM14 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM14 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM14 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM14 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 82/119

IIS2ICLX
FSM_OUTS15 (5Ah)
13.36 FSM_OUTS15 (5Ah)
FSM15 output register (R)
Table 197. FSM_OUTS15 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 198. FSM_OUTS15 register description
P_X FSM15 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM15 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM15 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM15 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM15 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM15 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
13.37 FSM_OUTS16 (5Bh)
FSM16 output register (R)
Table 199. FSM_OUTS16 register
P_X N_X P_Y N_Y P_Z N_Z 0 0
Table 200. FSM_OUTS16 register description
P_X FSM16 output: positive event detected on the X-axis. (0: event not detected; 1: event detected)
N_X FSM16 output: negative event detected on the X-axis. (0: event not detected; 1: event detected)
P_Y FSM16 output: positive event detected on the Y-axis. (0: event not detected; 1: event detected)
N_Y FSM16 output: negative event detected on the Y-axis. (0: event not detected; 1: event detected)
P_Z FSM16 output: positive event detected on the Z-axis. (0: event not detected; 1: event detected)
N_Z FSM16 output: negative event detected on the Z-axis. (0: event not detected; 1: event detected)
Note: Fields related to the Z-axis are intended for use in conjunction with an external sensor.
DS13005 - Rev 7 page 83/119

IIS2ICLX
EMB_FUNC_ODR_CFG_B (5Fh)
13.38 EMB_FUNC_ODR_CFG_B (5Fh)
Finite state machine output data rate configuration register (R/W)
Table 201. EMB_FUNC_ODR_CFG_B register
0(1) 1(2) 0(1) FSM_ODR1 FSM_ODR0 0(1) 1(2) 1(2)
1. This bit must be set to 0 for the correct operation of the device.
2. This bit must be set to 1 for the correct operation of the device
Table 202. EMB_FUNC_ODR_CFG_B register description
Finite state machine ODR configuration:
(00: 12.5 Hz;
FSM_ODR[1:0] 01: 26 Hz (default);
10: 52 Hz;
11: 104 Hz)
13.39 EMB_FUNC_ODR_CFG_C (60h)
Machine learning core output data rate configuration register (R/W)
Table 203. EMB_FUNC_ODR_CFG_C register
0(1) 0(1) MLC_ODR1 MLC_ODR0 0(1) 1(2) 0(1) 1(2)
1. This bit must be set to 0 for the correct operation of the device.
2. This bit must be set to 1 for the correct operation of the device.
Table 204. EMB_FUNC_ODR_CFG_C register description
Machine learning core ODR configuration:
(00: 12.5 Hz;
MLC_ODR[1:0] 01: 26 Hz (default);
10: 52 Hz;
11: 104 Hz)
13.40 EMB_FUNC_INIT_B (67h)
Embedded functions initialization register (R/W)
Table 205. EMB_FUNC_INIT_B register
0(1) 0(1) 0(1) MLC_INIT 0(1) 0(1) 0(1) FSM_INIT
1. This bit must be set to 0 for the correct operation of the device.
Table 206. EMB_FUNC_INIT_B register description
MLC_INIT Machine learning core initialization request. Default value: 0
FSM_INIT FSM initialization request. Default value: 0
DS13005 - Rev 7 page 84/119

IIS2ICLX
MLC0_SRC (70h)
13.41 MLC0_SRC (70h)
Machine learning core source register (R)
Table 207. MLC0_SRC register
| MLC0_ | MLC0_ | MLC0_ | MLC0_ | MLC0_ | MLC0_ | MLC0_ | MLC0_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 208. MLC0_SRC register description
| MLC0_SRC_[7:0] |     | Output value of MLC0 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
13.42 MLC1_SRC (71h)
Machine learning core source register (R)
Table 209. MLC1_SRC register
| MLC1_ | MLC1_ | MLC1_ | MLC1_ | MLC1_ | MLC1_ | MLC1_ | MLC1_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 210. MLC1_SRC register description
| MLC1_SRC_[7:0] |     | Output value of MLC1 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
13.43 MLC2_SRC (72h)
Machine learning core source register (R)
Table 211. MLC2_SRC register
| MLC2_ | MLC2_ | MLC2_ | MLC2_ | MLC2_ | MLC2_ | MLC2_ | MLC2_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 212. MLC2_SRC register description
| MLC2_SRC_[7:0] |     | Output value of MLC2 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
13.44 MLC3_SRC (73h)
Machine learning core source register (R)
Table 213. MLC3_SRC register
| MLC3_ | MLC3_ | MLC3_ | MLC3_ | MLC3_ | MLC3_ | MLC3_ | MLC3_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 214. MLC3_SRC register description
| MLC3_SRC_[7:0] |     | Output value of MLC3 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 85/119

IIS2ICLX
MLC4_SRC (74h)
13.45 MLC4_SRC (74h)
Machine learning core source register (R)
Table 215. MLC4_SRC register
| MLC4_ | MLC4_ | MLC4_ | MLC4_ | MLC4_ | MLC4_ | MLC4_ | MLC4_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 216. MLC4_SRC register description
| MLC4_SRC_[7:0] |     | Output value of MLC4 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
13.46 MLC5_SRC (75h)
Machine learning core source register (R)
Table 217. MLC5_SRC register
| MLC5_ | MLC5_ | MLC5_ | MLC5_ | MLC5_ | MLC5_ | MLC5_ | MLC5_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 218. MLC5_SRC register description
| MLC5_SRC_[7:0] |     | Output value of MLC5 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
13.47 MLC6_SRC (76h)
Machine learning core source register (R)
Table 219. MLC6_SRC register
| MLC6_ | MLC6_ | MLC6_ | MLC6_ | MLC6_ | MLC6_ | MLC6_ | MLC6_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 220. MLC6_SRC register description
| MLC6_SRC_[7:0] |     | Output value of MLC6 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
13.48 MLC7_SRC (77h)
Machine learning core source register (R)
Table 221. MLC7_SRC register
| MLC7_ | MLC7_ | MLC7_ | MLC7_ | MLC7_ | MLC7_ | MLC7_ | MLC7_ |
| ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| SRC_7 | SRC_6 | SRC_5 | SRC_4 | SRC_3 | SRC_2 | SRC_1 | SRC_0 |
Table 222. MLC7_SRC register description
| MLC7_SRC_[7:0] |     | Output value of MLC7 decision tree |     |     |     |     |     |
| -------------- | --- | ---------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 86/119

IIS2ICLX
Embedded advanced features
14 Embedded advanced features
The following table provides a list of the registers for the embedded advanced features page 1. These registers
are accessible when PAGE_SEL[3:0] are set to 0001 in PAGE_SEL (02h).
Table 223. Register address map - embedded advanced features page 1
Register address
|     | Name | Type |     | Default | Comment |
| --- | ---- | ---- | --- | ------- | ------- |
Hex Binary
| FSM_LC_TIMEOUT_L |     | RW 7A | 01111010 | 00000000 |     |
| ---------------- | --- | ----- | -------- | -------- | --- |
| FSM_LC_TIMEOUT_H |     | RW 7B | 01111011 | 00000000 |     |
| FSM_PROGRAMS     |     | RW 7C | 01111100 | 00000000 |     |
| FSM_START_ADD_L  |     | RW 7E | 01111110 | 00000000 |     |
| FSM_START_ADD_H  |     | RW 7F | 01111111 | 00000000 |     |
Reserved registers must not be changed. Writing to those registers may cause permanent damage to the device.
The content of the registers that are loaded at boot should not be changed. They contain the factory calibration
values. Their content is automatically restored when the device is powered up.
Write procedure example:
Example: write value 01h of register at address 7Ch (FSM_PROGRAMS) in page 1
1. Write bit FUNC_CFG_EN = 1 in FUNC_CFG_ACCESS (01h) // Enable access to embedded functions registers
2. Write bit PAGE_WRITE = 1 in PAGE_RW (17h) register // Select write operation mode
| 3. Write 0001 in PAGE_SEL[3:0] field of register PAGE_SEL (02h) |     |     | // Select page 1 |     |     |
| --------------------------------------------------------------- | --- | --- | ---------------- | --- | --- |
| 4. Write 7Ch in PAGE_ADDR register (08h)                        |     |     | // Set address   |     |     |
5. Write 06h in PAGE_DATA register (09h) // Set value to be written
6. Write bit PAGE_WRITE = 0 in PAGE_RW (17h) register // Write operation disabled
7. Write bit FUNC_CFG_EN = 0 in FUNC_CFG_ACCESS (01h) // Disable access to embedded functions registers
Read procedure example:
Example: read value of register at address 7Ch (FSM_PROGRAMS) in page 1
1. Write bit FUNC_CFG_EN = 1 in FUNC_CFG_ACCESS (01h) // Enable access to embedded functions registers
2. Write bit PAGE_READ = 1 in PAGE_RW (17h) register // Select read operation mode
| 3. Write 0001 in PAGE_SEL[3:0] field of register PAGE_SEL (02h) |     |     | // Select page 1 |     |     |
| --------------------------------------------------------------- | --- | --- | ---------------- | --- | --- |
| 4. Write 7Ch in PAGE_ADDR register (08h)                        |     |     | // Set address   |     |     |
5. Read value of PAGE_DATA register (09h) // Get register value
6. Write bit PAGE_READ = 0 in PAGE_RW (17h) register // Read operation disabled
7. Write bit FUNC_CFG_EN = 0 in FUNC_CFG_ACCESS (01h) // Disable access to embedded functions registers
Note: Steps 1 and 2 of both procedures are intended to be performed at the beginning of the procedure. Steps
6 and 7 of both procedures are intended to be performed at the end of the procedure. If the procedure involves
multiple operations, only steps 3, 4 and 5 must be repeated for each operation. If, in particular, the multiple
operations involve consecutive registers, only step 5 can be performed.
DS13005 - Rev 7 page 87/119

IIS2ICLX
Embedded advanced features register description
15 Embedded advanced features register description
15.1 Page 1 - embedded advanced features registers
15.1.1 FSM_LC_TIMEOUT_L (7Ah) and FSM_LC_TIMEOUT_H (7Bh)
FSM long counter timeout register (R/W)
The long counter timeout value is an unsigned integer value (16-bit format). When the long counter value reaches
this value, the FSM generates an interrupt.
Table 224. FSM_LC_TIMEOUT_L register
FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_
TIMEOUT7 TIMEOUT6 TIMEOUT5 TIMEOUT4 TIMEOUT3 TIMEOUT2 TIMEOUT1 TIMEOUT0
Table 225. FSM_LC_TIMEOUT_L register description
FSM_LC_TIMEOUT[7:0] FSM long counter timeout value (LSbyte). Default value: 00000000
Table 226. FSM_LC_TIMEOUT_H register
FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_ FSM_LC_
TIMEOUT15 TIMEOUT14 TIMEOUT13 TIMEOUT12 TIMEOUT11 TIMEOUT10 TIMEOUT9 TIMEOUT8
Table 227. FSM_LC_TIMEOUT_H register description
FSM_LC_TIMEOUT[15:8] FSM long counter timeout value (MSbyte). Default value: 00000000
15.1.2 FSM_PROGRAMS (7Ch)
FSM number of programs register (R/W)
Table 228. FSM_PROGRAMS register
FSM_N_ FSM_N_ FSM_N_ FSM_N_ FSM_N_ FSM_N_ FSM_N_ FSM_N_
PROG7 PROG6 PROG5 PROG4 PROG3 PROG2 PROG1 PROG0
Table 229. FSM_PROGRAMS register description
FSM_N_PROG[7:0] Number of FSM programs; must be less than or equal to 16. Default value: 00000000
DS13005 - Rev 7 page 88/119

IIS2ICLX
Page 1 - embedded advanced features registers
15.1.3 FSM_START_ADD_L (7Eh) and FSM_START_ADD_H (7Fh)
FSM start address register (R/W). First available address is 0x033C.
Table 230. FSM_START_ADD_L register
| FSM_   | FSM_   | FSM_   | FSM_   | FSM_   | FSM_   | FSM_   | FSM_   |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| START7 | START6 | START5 | START4 | START3 | START2 | START1 | START0 |
Table 231. FSM_START_ADD_L register description
| FSM_START[7:0] |     | FSM start address value (LSbyte). Default value: 00000000 |     |     |     |     |     |
| -------------- | --- | --------------------------------------------------------- | --- | --- | --- | --- | --- |
Table 232. FSM_START_ADD_H register
| FSM_ | FSM_ | FSM_ | FSM_ | FSM_ | FSM_ | FSM_ | FSM_ |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
START15 START14 START13 START12 START11 START10 START9 START8
Table 233. FSM_START_ADD_H register description
| FSM_START[15:8] |     | FSM start address value (MSbyte). Default value: 00000000 |     |     |     |     |     |
| --------------- | --- | --------------------------------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 89/119

IIS2ICLX
Sensor hub register map
16 Sensor hub register map
The table given below provides a list of the registers for the sensor hub functions available in the device and the
corresponding addresses. The sensor hub registers are accessible when bit SHUB_REG_ACCESS is set to 1 in
FUNC_CFG_ACCESS (01h).
Table 234. Registers address map
Register address
| Name           | Type |     |          | Default  | Comment |
| -------------- | ---- | --- | -------- | -------- | ------- |
|                |      | Hex | Binary   |          |         |
| SENSOR_HUB_1   | R    | 02  | 00000010 | output   |         |
| SENSOR_HUB_2   | R    | 03  | 00000011 | output   |         |
| SENSOR_HUB_3   | R    | 04  | 00000100 | output   |         |
| SENSOR_HUB_4   | R    | 05  | 00000101 | output   |         |
| SENSOR_HUB_5   | R    | 06  | 00000110 | output   |         |
| SENSOR_HUB_6   | R    | 07  | 00000111 | output   |         |
| SENSOR_HUB_7   | R    | 08  | 00001000 | output   |         |
| SENSOR_HUB_8   | R    | 09  | 00001001 | output   |         |
| SENSOR_HUB_9   | R    | 0A  | 00001010 | output   |         |
| SENSOR_HUB_10  | R    | 0B  | 00001011 | output   |         |
| SENSOR_HUB_11  | R    | 0C  | 00001100 | output   |         |
| SENSOR_HUB_12  | R    | 0D  | 00001101 | output   |         |
| SENSOR_HUB_13  | R    | 0E  | 00001110 | output   |         |
| SENSOR_HUB_14  | R    | 0F  | 00001111 | output   |         |
| SENSOR_HUB_15  | R    | 10  | 00010000 | output   |         |
| SENSOR_HUB_16  | R    | 11  | 00010001 | output   |         |
| SENSOR_HUB_17  | R    | 12  | 00010010 | output   |         |
| SENSOR_HUB_18  | R    | 13  | 00010011 | output   |         |
| MASTER_CONFIG  | RW   | 14  | 00010100 | 00000000 |         |
| SLV0_ADD       | R/W  | 15  | 00010101 | 00000000 |         |
| SLV0_SUBADD    | R/W  | 16  | 00010110 | 00000000 |         |
| SLV0_CONFIG    | R/W  | 17  | 00010111 | 00000000 |         |
| SLV1_ADD       | RW   | 18  | 00011000 | 00000000 |         |
| SLV1_SUBADD    | R/W  | 19  | 00011001 | 00000000 |         |
| SLV1_CONFIG    | R/W  | 1A  | 00011010 | 00000000 |         |
| SLV2_ADD       | R/W  | 1B  | 00011011 | 00000000 |         |
| SLV2_SUBADD    | R/W  | 1C  | 00011100 | 00000000 |         |
| SLV2_CONFIG    | R/W  | 1D  | 00011101 | 00000000 |         |
| SLV3_ADD       | R/W  | 1E  | 00011110 | 00000000 |         |
| SLV3_SUBADD    | R/W  | 1F  | 00011111 | 00000000 |         |
| SLV3_CONFIG    | R/W  | 20  | 00100000 | 00000000 |         |
| DATAWRITE_SLV0 | R/W  | 21  | 00100001 | 00000000 |         |
| STATUS_MASTER  | R    | 22  | 00100010 | output   |         |
Reserved registers must not be changed. Writing to those registers may cause permanent damage to the device.
The content of the registers that are loaded at boot should not be changed. They contain the factory calibration
values. Their content is automatically restored when the device is powered up.
| DS13005 - Rev 7 |     |     |     |     | page 90/119 |
| --------------- | --- | --- | --- | --- | ----------- |

IIS2ICLX
Sensor hub register description
17 Sensor hub register description
17.1 SENSOR_HUB_1 (02h)
Sensor hub output register (R)
First byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG number
of read operation configurations (for external sensors from x = 0 to x = 3).
Table 235. SENSOR_HUB_1 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub1_7 | Hub1_6 | Hub1_5 | Hub1_4 | Hub1_3 | Hub1_2 | Hub1_1 | Hub1_0 |
Table 236. SENSOR_HUB_1 register description
| SensorHub1_[7:0] |     | First byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ----------------------------------------- | --- | --- | --- | --- | --- |
17.2 SENSOR_HUB_2 (03h)
Sensor hub output register (R)
Second byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 237. SENSOR_HUB_2 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub2_7 | Hub2_6 | Hub2_5 | Hub2_4 | Hub2_3 | Hub2_2 | Hub2_1 | Hub2_0 |
Table 238. SENSOR_HUB_2 register description
| SensorHub2_[7:0] |     | Second byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ------------------------------------------ | --- | --- | --- | --- | --- |
17.3 SENSOR_HUB_3 (04h)
Sensor hub output register (R)
Third byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 239. SENSOR_HUB_3 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub3_7 | Hub3_6 | Hub3_5 | Hub3_4 | Hub3_3 | Hub3_2 | Hub3_1 | Hub3_0 |
Table 240. SENSOR_HUB_3 register description
| SensorHub3_[7:0] |     | Third byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ----------------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 91/119

IIS2ICLX
SENSOR_HUB_4 (05h)
17.4 SENSOR_HUB_4 (05h)
Sensor hub output register (R)
Fourth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 241. SENSOR_HUB_4 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub4_7 | Hub4_6 | Hub4_5 | Hub4_4 | Hub4_3 | Hub4_2 | Hub4_1 | Hub4_0 |
Table 242. SENSOR_HUB_4 register description
| SensorHub4_[7:0] |     | Fourth byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ------------------------------------------ | --- | --- | --- | --- | --- |
17.5 SENSOR_HUB_5 (06h)
Sensor hub output register (R)
Fifth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG number
of read operation configurations (for external sensors from x = 0 to x = 3).
Table 243. SENSOR_HUB_5 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub5_7 | Hub5_6 | Hub5_5 | Hub5_4 | Hub5_3 | Hub5_2 | Hub5_1 | Hub5_0 |
Table 244. SENSOR_HUB_5 register description
| SensorHub5_[7:0] |     | Fifth byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ----------------------------------------- | --- | --- | --- | --- | --- |
17.6 SENSOR_HUB_6 (07h)
Sensor hub output register (R)
Sixth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 245. SENSOR_HUB_6 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub6_7 | Hub6_6 | Hub6_5 | Hub6_4 | Hub6_3 | Hub6_2 | Hub6_1 | Hub6_0 |
Table 246. SENSOR_HUB_6 register description
| SensorHub6_[7:0] |     | Sixth byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ----------------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 92/119

IIS2ICLX
SENSOR_HUB_7 (08h)
17.7 SENSOR_HUB_7 (08h)
Sensor hub output register (R)
Seventh byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 247. SENSOR_HUB_7 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub7_7 | Hub7_6 | Hub7_5 | Hub7_4 | Hub7_3 | Hub7_2 | Hub7_1 | Hub7_0 |
Table 248. SENSOR_HUB_7 register description
| SensorHub7_[7:0] |     | Seventh byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ------------------------------------------- | --- | --- | --- | --- | --- |
17.8 SENSOR_HUB_8 (09h)
Sensor hub output register (R)
Eighth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 249. SENSOR_HUB_8 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub8_7 | Hub8_6 | Hub8_5 | Hub8_4 | Hub8_3 | Hub8_2 | Hub8_1 | Hub8_0 |
Table 250. SENSOR_HUB_8 register description
| SensorHub8_[7:0] |     | Eighth byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ------------------------------------------ | --- | --- | --- | --- | --- |
17.9 SENSOR_HUB_9 (0Ah)
Sensor hub output register (R)
Ninth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 251. SENSOR_HUB_9 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
| Hub9_7 | Hub9_6 | Hub9_5 | Hub9_4 | Hub9_3 | Hub9_2 | Hub9_1 | Hub9_0 |
Table 252. SENSOR_HUB_9 register description
| SensorHub9_[7:0] |     | Ninth byte associated to external sensors |     |     |     |     |     |
| ---------------- | --- | ----------------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 93/119

IIS2ICLX
SENSOR_HUB_10 (0Bh)
17.10 SENSOR_HUB_10 (0Bh)
Sensor hub output register (R)
Tenth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 253. SENSOR_HUB_10 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub10_7 Hub10_6 Hub10_5 Hub10_4 Hub10_3 Hub10_2 Hub10_1 Hub10_0
Table 254. SENSOR_HUB_10 register description
| SensorHub10_[7:0] |     | Tenth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | ----------------------------------------- | --- | --- | --- | --- | --- |
17.11 SENSOR_HUB_11 (0Ch)
Sensor hub output register (R)
Eleventh byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 255. SENSOR_HUB_11 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub11_7 Hub11_6 Hub11_5 Hub11_4 Hub11_3 Hub11_2 Hub11_1 Hub11_0
Table 256. SENSOR_HUB_11 register description
| SensorHub11_[7:0] |     | Eleventh byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | -------------------------------------------- | --- | --- | --- | --- | --- |
17.12 SENSOR_HUB_12 (0Dh)
Sensor hub output register (R)
Twelfth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 257. SENSOR_HUB_12 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub12_7 Hub12_6 Hub12_5 Hub12_4 Hub12_3 Hub12_2 Hub12_1 Hub12_0
Table 258. SENSOR_HUB_12 register description
| SensorHub12_[7:0] |     | Twelfth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | ------------------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 94/119

IIS2ICLX
SENSOR_HUB_13 (0Eh)
17.13 SENSOR_HUB_13 (0Eh)
Sensor hub output register (R)
Thirteenth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 259. SENSOR_HUB_13 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub13_7 Hub13_6 Hub13_5 Hub13_4 Hub13_3 Hub13_2 Hub13_1 Hub13_0
Table 260. SENSOR_HUB_13 register description
| SensorHub13_[7:0] |     | Thirteenth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | ---------------------------------------------- | --- | --- | --- | --- | --- |
17.14 SENSOR_HUB_14 (0Fh)
Sensor hub output register (R)
Fourteenth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 261. SENSOR_HUB_14 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub14_7 Hub14_6 Hub14_5 Hub14_4 Hub14_3 Hub14_2 Hub14_1 Hub14_0
Table 262. SENSOR_HUB_14 register description
| SensorHub14_[7:0] |     | Fourteenth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | ---------------------------------------------- | --- | --- | --- | --- | --- |
17.15 SENSOR_HUB_15 (10h)
Sensor hub output register (R)
Fifteenth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 263. SENSOR_HUB_15 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub15_7 Hub15_6 Hub15_5 Hub15_4 Hub15_3 Hub15_2 Hub15_1 Hub15_0
Table 264. SENSOR_HUB_15 register description
| SensorHub15_[7:0] |     | Fifteenth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | --------------------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 95/119

IIS2ICLX
SENSOR_HUB_16 (11h)
17.16 SENSOR_HUB_16 (11h)
Sensor hub output register (R)
Sixteenth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 265. SENSOR_HUB_16 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub16_7 Hub16_6 Hub16_5 Hub16_4 Hub16_3 Hub16_2 Hub16_1 Hub16_0
Table 266. SENSOR_HUB_16 register description
| SensorHub16_[7:0] |     | Sixteenth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | --------------------------------------------- | --- | --- | --- | --- | --- |
17.17 SENSOR_HUB_17 (12h)
Sensor hub output register (R)
Seventeenth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 267. SENSOR_HUB_17 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub17_7 Hub17_6 Hub17_5 Hub17_4 Hub17_3 Hub17_2 Hub17_1 Hub17_0
Table 268. SENSOR_HUB_17 register description
| SensorHub17_[7:0] |     | Seventeenth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | ----------------------------------------------- | --- | --- | --- | --- | --- |
17.18 SENSOR_HUB_18 (13h)
Sensor hub output register (R)
Eighteenth byte associated to external sensors. The content of the register is consistent with the SLVx_CONFIG
number of read operation configurations (for external sensors from x = 0 to x = 3).
Table 269. SENSOR_HUB_18 register
| Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor | Sensor |
| ------ | ------ | ------ | ------ | ------ | ------ | ------ | ------ |
Hub18_7 Hub18_6 Hub18_5 Hub18_4 Hub18_3 Hub18_2 Hub18_1 Hub18_0
Table 270. SENSOR_HUB_18 register description
| SensorHub18_[7:0] |     | Eighteenth byte associated to external sensors |     |     |     |     |     |
| ----------------- | --- | ---------------------------------------------- | --- | --- | --- | --- | --- |
DS13005 - Rev 7 page 96/119

IIS2ICLX
MASTER_CONFIG (14h)
17.19 MASTER_CONFIG (14h)
Master configuration register (R/W)
Table 271. MASTER_CONFIG register
RST_MASTER WRITE_ START_ PASS_THROUGH SHUB_ MASTER AUX_SENS AUX_SENS
_REGS ONCE CONFIG _MODE PU_EN _ON _ON1 _ON0
Table 272. MASTER_CONFIG register description
RST_MASTER_REGS Resets master logic and output registers. Must be set to 1 and then set it to 0. Default value: 0
Slave 0 write operation is performed only at the first sensor hub cycle.
Default value: 0
WRITE_ONCE
(0: write operation for each sensor hub cycle;
1: write operation only for the first sensor hub cycle)
Sensor hub trigger signal selection. Default value: 0
START_CONFIG (0: sensor hub trigger signal is the accelerometer data-ready;
1: sensor hub trigger signal external from INT2 pin)
I²C interface pass-through. Default value: 0
PASS_THROUGH_MODE (0: pass-through disabled;
1: pass-through enabled, main I²C line is short-circuited with the auxiliary line)
Master I²C pull-up enable. Default value: 0
SHUB_PU_EN (0: internal pull-up on auxiliary I²C line disabled;
1: internal pull-up on auxiliary I²C line enabled)
Sensor hub I²C master enable. Default: 0
MASTER_ON
(0: master I²C of sensor hub disabled; 1: master I²C of sensor hub enabled)
Number of external sensors to be read by the sensor hub.
(00: one sensor (default);
AUX_SENS_ON[1:0] 01: two sensors;
10: three sensors;
11: four sensors)
DS13005 - Rev 7 page 97/119

IIS2ICLX
SLV0_ADD (15h)
17.20 SLV0_ADD (15h)
I²C slave address of the first external sensor (sensor 1) register (R/W)
Table 273. SLV0_ADD register
| slave0_ | slave0_ | slave0_ | slave0_ | slave0_ | slave0_ | slave0_ | rw_0 |
| ------- | ------- | ------- | ------- | ------- | ------- | ------- | ---- |
| add6    | add5    | add4    | add3    | add2    | add1    | add0    |      |
Table 274. SLV0_ADD register description
slave0_add[6:0] I²C slave address of sensor 1 that can be read by the sensor hub. Default value: 0000000
Read/write operation on sensor 1. Default value: 0
rw_0
(0: write operation; 1: read operation)
17.21 SLV0_SUBADD (16h)
Address of register on the first external sensor (sensor 1) register (R/W)
Table 275. SLV0_SUBADD register
slave0_ slave0_ slave0_ slave0_ slave0_ slave0_ slave0_ slave0_
| reg7 | reg6 | reg5 | reg4 | reg3 | reg2 | reg1 | reg0 |
| ---- | ---- | ---- | ---- | ---- | ---- | ---- | ---- |
Table 276. SLV0_SUBADD register description
Address of register on sensor 1 that has to be read/written according to the rw_0 bit value in SLV0_ADD
slave0_reg[7:0]
(15h). Default value: 00000000
17.22 SLV0_CONFIG (17h)
First external sensor (sensor 1) configuration and sensor hub settings register (R/W)
Table 277. SLV0_CONFIG register
| SHUB_ | SHUB_ |      |      | BATCH_EXT_ | Slave0_ | Slave0_ | Slave0_ |
| ----- | ----- | ---- | ---- | ---------- | ------- | ------- | ------- |
|       |       | 0(1) | 0(1) |            |         |         |         |
| ODR_1 | ODR_0 |      |      | SENS_0_EN  | numop2  | numop1  | numop0  |

1. This bit must be set to 0 for the correct operation of the device.

Table 278. SLV0_CONFIG register description
Rate at which the master communicates. Default value: 00
(00: 104 Hz (or the accelerometer ODR if it is less than 104 Hz);
SHUB_ODR_[1:0] 01: 52 Hz (or the accelerometer ODR if it is less than 52 Hz);
10: 26 Hz (or the accelerometer ODR if it is less than 26 Hz);
11: 12.5 Hz (or the accelerometer ODR if it is less than 12.5 Hz)
| BATCH_EXT_SENS_0_EN |     | Enables FIFO data batching of first slave. Default value: 0 |     |     |     |     |     |
| ------------------- | --- | ----------------------------------------------------------- | --- | --- | --- | --- | --- |
| Slave0_numop[2:0]   |     | Number of read operations on sensor 1. Default value: 000   |     |     |     |     |     |
DS13005 - Rev 7 page 98/119

IIS2ICLX
SLV1_ADD (18h)
17.23 SLV1_ADD (18h)
I²C slave address of the second external sensor (sensor 2) register (R/W)
Table 279. SLV1_ADD register
Slave1_ Slave1_ Slave1_ Slave1_ Slave1_ Slave1_ Slave1_
r_1
add6 add5 add4 add3 add2 add1 add0
Table 280. SLV1_ADD register description
I²C slave address of sensor 2 that can be read by the sensor hub.
Slave1_add[6:0]
Default value: 0000000
Enables read operation on sensor 2. Default value: 0
r_1
(0: read operation disabled; 1: read operation enabled)
17.24 SLV1_SUBADD (19h)
Address of register on the second external sensor (sensor 2) register (R/W)
Table 281. SLV1_SUBADD register
Slave1_ Slave1_ Slave1_ Slave1_ Slave1_ Slave1_ Slave1_ Slave1_
reg7 reg6 reg5 reg4 reg3 reg2 reg1 reg0
Table 282. SLV1_SUBADD register description
Slave1_reg[7:0] Address of register on sensor 2 that has to be read/written according to the r_1 bit value in SLV1_ADD (18h).
17.25 SLV1_CONFIG (1Ah)
Second external sensor (sensor 2) configuration register (R/W)
Table 283. SLV1_CONFIG register
BATCH_EXT_ Slave1_ Slave1_ Slave1_
0(1) 0(1) 0(1) 0(1)
SENS_1_EN numop2 numop1 numop0
1. This bit must be set to 0 for the correct operation of the device.
Table 284. SLV1_CONFIG register description
BATCH_EXT_SENS_1_EN Enables FIFO data batching of second slave. Default value: 0
Slave1_numop[2:0] Number of read operations on sensor 2. Default value: 000
DS13005 - Rev 7 page 99/119

IIS2ICLX
SLV2_ADD (1Bh)
17.26 SLV2_ADD (1Bh)
I²C slave address of the third external sensor (sensor 3) register (R/W)
Table 285. SLV2_ADD register
Slave2_ Slave2_ Slave2_ Slave2_ Slave2_ Slave2_ Slave2_
r_2
add6 add5 add4 add3 add2 add1 add0
Table 286. SLV2_ADD register description
Slave2_add[6:0] I²C slave address of sensor 3 that can be read by the sensor hub.
Enables read operation on sensor 3. Default value: 0
r_2
(0: read operation disabled; 1: read operation enabled)
17.27 SLV2_SUBADD (1Ch)
Address of register on the third external sensor (sensor 3) register (R/W)
Table 287. SLV2_SUBADD register
Slave2_ Slave2_ Slave2_ Slave2_ Slave2_ Slave2_ Slave2_ Slave2_
reg7 reg6 reg5 reg4 reg3 reg2 reg1 reg0
Table 288. SLV2_SUBADD register description
Address of register on sensor 3 that has to be read/written according to the r_2 bit value in SLV2_ADD
Slave2_reg[7:0]
(1Bh).
17.28 SLV2_CONFIG (1Dh)
Third external sensor (sensor 3) configuration register (R/W)
Table 289. SLV2_CONFIG register
BATCH_EXT_ Slave2_ Slave2_ Slave2_
0(1) 0(1) 0(1) 0(1)
SENS_2_EN numop2 numop1 numop0
1. This bit must be set to 0 for the correct operation of the device.
Table 290. SLV2_CONFIG register description
BATCH_EXT_SENS_2_EN Enables FIFO data batching of third slave. Default value: 0
Slave2_numop[2:0] Number of read operations on sensor 3. Default value: 000
DS13005 - Rev 7 page 100/119

IIS2ICLX
SLV3_ADD (1Eh)
17.29 SLV3_ADD (1Eh)
I²C slave address of the fourth external sensor (sensor 4) register (R/W)
Table 291. SLV3_ADD register
Slave3_ Slave3_ Slave3_ Slave3_ Slave3_ Slave3_ Slave3_
r_3
add6 add5 add4 add3 add2 add1 add0
Table 292. SLV3_ADD register description
Slave3_add[6:0] I²C slave address of sensor 4 that can be read by the sensor hub.
Enables read operation on sensor 4. Default value: 0
r_3
(0: read operation disabled; 1: read operation enabled)
17.30 SLV3_SUBADD (1Fh)
Address of register on the fourth external sensor (sensor 4) register (R/W)
Table 293. SLV3_SUBADD register
Slave3_ Slave3_ Slave3_ Slave3_ Slave3_ Slave3_ Slave3_ Slave3_
reg7 reg6 reg5 reg4 reg3 reg2 reg1 reg0
Table 294. SLV3_SUBADD register description
Slave3_reg[7:0] Address of register on sensor 4 that has to be read according to the r_3 bit value in SLV3_ADD (1Eh).
17.31 SLV3_CONFIG (20h)
Fourth external sensor (sensor 4) configuration register (R/W)
Table 295. SLV3_CONFIG register
BATCH_EXT_ Slave3_ Slave3_ Slave3_
0(1) 0(1) 0(1) 0(1)
SENS_3_EN numop2 numop1 numop0
1. This bit must be set to 0 for the correct operation of the device.
Table 296. SLV3_CONFIG register description
BATCH_EXT_SENS_3_EN Enables FIFO data batching of fourth slave. Default value: 0
Slave3_numop[2:0] Number of read operations on sensor 4. Default value: 000
DS13005 - Rev 7 page 101/119

IIS2ICLX
DATAWRITE_SLV0 (21h)
17.32 DATAWRITE_SLV0 (21h)
Data to be written into the slave device register (R/W)
Table 297. DATAWRITE_SLV0 register
Slave0_ Slave0_ Slave0_ Slave0_ Slave0_ Slave0_ Slave0_ Slave0_
dataw7 dataw6 dataw5 dataw4 dataw3 dataw2 dataw1 dataw0
Table 298. DATAWRITE_SLV0 register description
Data to be written into the slave 0 device according to the rw_0 bit in register SLV0_ADD (15h).
Slave0_dataw[7:0]
Default value: 00000000
17.33 STATUS_MASTER (22h)
Sensor hub source register (R)
Table 299. STATUS_MASTER register
WR_ONCE SLAVE3_ SLAVE2_ SLAVE1_ SLAVE0_ SENS_HUB
0 0
_DONE NACK NACK NACK NACK _ENDOP
Table 300. STATUS_MASTER register description
When the bit WRITE_ONCE in MASTER_CONFIG (14h) is configured as 1, this bit is set to 1 when the
WR_ONCE_DONE
write operation on slave 0 has been performed and completed. Default value: 0
SLAVE3_NACK This bit is set to 1 if not acknowledge occurs on slave 3 communication. Default value: 0
SLAVE2_NACK This bit is set to 1 if not acknowledge occurs on slave 2 communication. Default value: 0
SLAVE1_NACK This bit is set to 1 if not acknowledge occurs on slave 1 communication. Default value: 0
SLAVE0_NACK This bit is set to 1 if not acknowledge occurs on slave 0 communication. Default value: 0
Sensor hub communication status. Default value: 0
SENS_HUB_ENDOP (0: sensor hub communication not concluded;
1: sensor hub communication concluded)
DS13005 - Rev 7 page 102/119

IIS2ICLX
Soldering information
18 Soldering information
The LGA package is compliant with the ECOPACK and RoHS standard.
It is qualified for soldering heat resistance according to JEDEC J-STD-020.
For the land pattern and soldering recommendations, consult technical note TN0018 available on www.st.com.
DS13005 - Rev 7 page 103/119

19 Package information
In order to meet environmental requirements, ST offers these devices in different grades of ECOPACK packages,
depending on their level of environmental compliance. ECOPACK specifications, grade definitions and product
status are available at: www.st.com. ECOPACK is an ST trademark.
19.1 LGA-16L package information
The IIS2ICLX is available in a high-performance (low-stress) ceramic cavity land grid array (CCLGA) package.
Due to the use of epoxy glue for lid sealing, hermeticity is not guaranteed. Processing or use of this package in a
harsh environment should be assessed by the customer.
Figure 27. Ceramic cavity LGA-16: package outline and mechanical data
H
L
Pin 1
indicator
W
IIS2ICLX
Package information
8535893_A
Note: Top and bottom view: dimensions are expressed in mm.
Table 301. Outer dimensions
Item Dimension [mm] Tolerance [mm]
Length [L] 5 ±0.15
Width [W] 5 ±0.15
Height [H] 1.7 typ ±0.15
Pad size 0.7 x 0.5 ±0.15
Note: General tolerance is ±0.1 mm unless otherwise specified.
DS13005 - Rev 7 page 104/119

IIS2ICLX
Revision history
Table 302. Document revision history
Date Version Changes
27-May-2020 1 Initial release
09-Jun-2020 2 Updated title of datasheet
Updated CS pin in Table 16. Internal pin status and added procedure to
initialize the device
Added DEVICE_CONF bit to CTRL9_XL
18-Jun-2020 3 Updated description of X-axis tap recognition threshold in TAP_CFG1 (57h)
Updated description of Y-axis tap recognition threshold in TAP_CFG2 (58h)
Updated description of weight of 1 LSB of wakeup threshold in
WAKE_UP_DUR (5Ch)
Updated description of BDR_XL_[3:0] in FIFO_CTRL3 (09h)
20-Aug-2020 4 Updated description of ODR_T_BATCH_[1:0] in FIFO_CTRL4 (0Ah)
Updated Table 48. CTRL6_C register description
Updated Table 38. Accelerometer ODR selection
Updated description of BDR_XL_[3:0] in FIFO_CTRL3 (09h), adding 1.6 Hz
18-Sep-2020 5
Updated description of ODR_T_BATCH_[1:0] in FIFO_CTRL4 (0Ah), adding
1.6 Hz
Added Product resources
Updated sensitivity change over life in Table 2. Mechanical characteristics
24-Aug-2021 6 Updated Note below Figure 6 and Figure 7
Updated bits 0 and 1 of registers FSM_OUTS1 (4Ch) through FSM_OUTS16
(5Bh)
Corrected range for Vin in Table 7. Absolute maximum ratings
01-Aug-2022 7
Minor textual updates
DS13005 - Rev 7 page 105/119

IIS2ICLX
Contents
Contents
1 Overview ..........................................................................3
2 Embedded low-power features.....................................................4
2.1 Finite state machine ............................................................5
2.2 Machine learning core ..........................................................6
3 Pin description ....................................................................7
3.1 Pin connections................................................................7
4 Module specifications .............................................................9
4.1 Mechanical characteristics.......................................................9
4.2 Electrical characteristics........................................................10
4.3 Temperature sensor characteristics ..............................................10
4.4 Communication interface characteristics ..........................................11
4.4.1 SPI - serial peripheral interface............................................. 11
4.4.2 I²C - inter-IC control interface .............................................. 12
4.5 Absolute maximum ratings......................................................13
5 Digital interfaces .................................................................14
5.1 I²C/SPI interface ..............................................................14
5.2 I²C serial interface.............................................................14
5.2.1 I²C operation........................................................... 14
5.3 SPI bus interface..............................................................16
5.3.1 SPI read .............................................................. 17
5.3.2 SPI write.............................................................. 18
5.3.3 SPI read in 3-wire mode .................................................. 18
5.4 Master I²C interface ...........................................................19
6 Functionality .....................................................................20
6.1 Block diagram of filters.........................................................20
6.1.1 Block diagrams of the accelerometer filters.................................... 20
6.2 FIFO ........................................................................22
6.2.1 Bypass mode .......................................................... 22
6.2.2 FIFO mode ............................................................ 22
6.2.3 Continuous mode ....................................................... 23
6.2.4 Continuous-to-FIFO mode................................................. 23
6.2.5 Bypass-to-continuous mode ............................................... 23
6.2.6 Bypass-to-FIFO mode.................................................... 23
6.2.7 FIFO reading procedure .................................................. 24
7 Frequency response..............................................................25
DS13005 - Rev 7 page 106/119

IIS2ICLX
Contents
8 Typical performance characteristics ..............................................26
8.1 Frequency response measurements .............................................26
9 Application hints .................................................................28
9.1 IIS2ICLX electrical connections in mode 1.........................................28
9.2 IIS2ICLX electrical connections in mode 2.........................................29
10 Register map .....................................................................31
11 Register description ..............................................................33
11.1 FUNC_CFG_ACCESS (01h)....................................................33
11.2 PIN_CTRL (02h) ..............................................................33
11.3 FIFO_CTRL1 (07h)............................................................34
11.4 FIFO_CTRL2 (08h)............................................................34
11.5 FIFO_CTRL3 (09h)............................................................35
11.6 FIFO_CTRL4 (0Ah)............................................................36
11.7 COUNTER_BDR_REG1 (0Bh) ..................................................37
11.8 COUNTER_BDR_REG2 (0Ch)..................................................37
11.9 INT1_CTRL (0Dh).............................................................38
11.10 INT2_CTRL (0Eh).............................................................38
11.11 WHO_AM_I (0Fh).............................................................38
11.12 CTRL1_XL (10h)..............................................................39
11.13 CTRL3_C (12h)...............................................................40
11.14 CTRL4_C (13h)...............................................................41
11.15 CTRL5_C (14h)...............................................................41
11.16 CTRL6_C (15h)...............................................................42
11.17 CTRL7_XL (16h)..............................................................42
11.18 CTRL8_XL (17h)..............................................................43
11.19 CTRL9_XL (18h)..............................................................44
11.20 CTRL10_C (19h)..............................................................44
11.21 ALL_INT_SRC (1Ah) ..........................................................45
11.22 WAKE_UP_SRC (1Bh).........................................................45
11.23 TAP_SRC (1Ch) ..............................................................46
11.24 DEN_SRC (1Dh)..............................................................46
11.25 STATUS_REG (1Eh)...........................................................47
11.26 OUT_TEMP_L (20h), OUT_TEMP_H (21h)........................................47
11.27 OUTX_L_A (28h) and OUTX_H_A (29h)..........................................48
11.28 OUTY_L_A (2Ah) and OUTY_H_A (2Bh) .........................................48
DS13005 - Rev 7 page 107/119

IIS2ICLX
Contents
11.29 EMB_FUNC_STATUS_MAINPAGE (35h) .........................................48
11.30 FSM_STATUS_A_MAINPAGE (36h) .............................................49
11.31 FSM_STATUS_B_MAINPAGE (37h) .............................................49
11.32 MLC_STATUS_MAINPAGE (38h)................................................50
11.33 STATUS_MASTER_MAINPAGE (39h)............................................50
11.34 FIFO_STATUS1 (3Ah) .........................................................51
11.35 FIFO_STATUS2 (3Bh) .........................................................51
11.36 TIMESTAMP0 (40h), TIMESTAMP1 (41h), TIMESTAMP2 (42h), and TIMESTAMP3 (43h) 52
11.37 TAP_CFG0 (56h)..............................................................53
11.38 TAP_CFG1 (57h)..............................................................53
11.39 TAP_CFG2 (58h)..............................................................54
11.40 INT_DUR2 (5Ah)..............................................................54
11.41 WAKE_UP_THS (5Bh).........................................................55
11.42 WAKE_UP_DUR (5Ch) ........................................................55
11.43 MD1_CFG (5Eh)..............................................................56
11.44 MD2_CFG (5Fh) ..............................................................57
11.45 INTERNAL_FREQ_FINE (63h)..................................................58
11.46 X_OFS_USR (73h)............................................................59
11.47 Y_OFS_USR (74h)............................................................59
11.48 FIFO_DATA_OUT_TAG (78h)...................................................60
11.49 FIFO_DATA_OUT_X_L (79h) and FIFO_DATA_OUT_X_H (7Ah) .....................61
11.50 FIFO_DATA_OUT_Y_L (7Bh) and FIFO_DATA_OUT_Y_H (7Ch).....................61
11.51 FIFO_DATA_OUT_Z_L (7Dh) and FIFO_DATA_OUT_Z_H (7Eh) .....................61
12 Embedded functions register map ................................................62
13 Embedded functions register description .........................................64
13.1 PAGE_SEL (02h) .............................................................64
13.2 EMB_FUNC_EN_B (05h).......................................................64
13.3 PAGE_ADDRESS (08h)........................................................64
13.4 PAGE_VALUE (09h)...........................................................65
13.5 EMB_FUNC_INT1 (0Ah) .......................................................65
13.6 FSM_INT1_A (0Bh) ...........................................................66
13.7 FSM_INT1_B (0Ch) ...........................................................67
13.8 MLC_INT1 (0Dh)..............................................................68
13.9 EMB_FUNC_INT2 (0Eh) .......................................................68
13.10 FSM_INT2_A (0Fh)............................................................69
13.11 FSM_INT2_B (10h)............................................................70
DS13005 - Rev 7 page 108/119

IIS2ICLX
Contents
13.12 MLC_INT2 (11h) ..............................................................71
13.13 EMB_FUNC_STATUS (12h) ....................................................71
13.14 FSM_STATUS_A (13h).........................................................72
13.15 FSM_STATUS_B (14h).........................................................72
13.16 MLC_STATUS (15h)...........................................................73
13.17 PAGE_RW (17h)..............................................................73
13.18 FSM_ENABLE_A (46h) ........................................................74
13.19 FSM_ENABLE_B (47h) ........................................................74
13.20 FSM_LONG_COUNTER_L (48h) and FSM_LONG_COUNTER_H (49h)...............75
13.21 FSM_LONG_COUNTER_CLEAR (4Ah) ..........................................75
13.22 FSM_OUTS1 (4Ch) ...........................................................76
13.23 FSM_OUTS2 (4Dh) ...........................................................76
13.24 FSM_OUTS3 (4Eh)............................................................77
13.25 FSM_OUTS4 (4Fh)............................................................77
13.26 FSM_OUTS5 (50h)............................................................78
13.27 FSM_OUTS6 (51h)............................................................78
13.28 FSM_OUTS7 (52h)............................................................79
13.29 FSM_OUTS8 (53h)............................................................79
13.30 FSM_OUTS9 (54h)............................................................80
13.31 FSM_OUTS10 (55h)...........................................................80
13.32 FSM_OUTS11 (56h)...........................................................81
13.33 FSM_OUTS12 (57h)...........................................................81
13.34 FSM_OUTS13 (58h)...........................................................82
13.35 FSM_OUTS14 (59h)...........................................................82
13.36 FSM_OUTS15 (5Ah) ..........................................................83
13.37 FSM_OUTS16 (5Bh) ..........................................................83
13.38 EMB_FUNC_ODR_CFG_B (5Fh)................................................84
13.39 EMB_FUNC_ODR_CFG_C (60h)................................................84
13.40 EMB_FUNC_INIT_B (67h)......................................................84
13.41 MLC0_SRC (70h) .............................................................85
13.42 MLC1_SRC (71h) .............................................................85
13.43 MLC2_SRC (72h) .............................................................85
13.44 MLC3_SRC (73h) .............................................................85
13.45 MLC4_SRC (74h) .............................................................86
13.46 MLC5_SRC (75h) .............................................................86
13.47 MLC6_SRC (76h) .............................................................86
DS13005 - Rev 7 page 109/119

IIS2ICLX
Contents
13.48 MLC7_SRC (77h) .............................................................86
14 Embedded advanced features.....................................................87
15 Embedded advanced features register description ................................88
15.1 Page 1 - embedded advanced features registers...................................88
15.1.1 FSM_LC_TIMEOUT_L (7Ah) and FSM_LC_TIMEOUT_H (7Bh).................... 88
15.1.2 FSM_PROGRAMS (7Ch) ................................................. 88
15.1.3 FSM_START_ADD_L (7Eh) and FSM_START_ADD_H (7Fh) ..................... 89
16 Sensor hub register map..........................................................90
17 Sensor hub register description...................................................91
17.1 SENSOR_HUB_1 (02h)........................................................91
17.2 SENSOR_HUB_2 (03h)........................................................91
17.3 SENSOR_HUB_3 (04h)........................................................91
17.4 SENSOR_HUB_4 (05h)........................................................92
17.5 SENSOR_HUB_5 (06h)........................................................92
17.6 SENSOR_HUB_6 (07h)........................................................92
17.7 SENSOR_HUB_7 (08h)........................................................93
17.8 SENSOR_HUB_8 (09h)........................................................93
17.9 SENSOR_HUB_9 (0Ah)........................................................93
17.10 SENSOR_HUB_10 (0Bh).......................................................94
17.11 SENSOR_HUB_11 (0Ch).......................................................94
17.12 SENSOR_HUB_12 (0Dh).......................................................94
17.13 SENSOR_HUB_13 (0Eh).......................................................95
17.14 SENSOR_HUB_14 (0Fh).......................................................95
17.15 SENSOR_HUB_15 (10h).......................................................95
17.16 SENSOR_HUB_16 (11h).......................................................96
17.17 SENSOR_HUB_17 (12h).......................................................96
17.18 SENSOR_HUB_18 (13h).......................................................96
17.19 MASTER_CONFIG (14h).......................................................97
17.20 SLV0_ADD (15h)..............................................................98
17.21 SLV0_SUBADD (16h)..........................................................98
17.22 SLV0_CONFIG (17h) ..........................................................98
17.23 SLV1_ADD (18h)..............................................................99
17.24 SLV1_SUBADD (19h)..........................................................99
17.25 SLV1_CONFIG (1Ah)..........................................................99
17.26 SLV2_ADD (1Bh) ............................................................100
17.27 SLV2_SUBADD (1Ch) ........................................................100
DS13005 - Rev 7 page 110/119

IIS2ICLX
Contents
17.28 SLV2_CONFIG (1Dh).........................................................100
17.29 SLV3_ADD (1Eh) ............................................................101
17.30 SLV3_SUBADD (1Fh).........................................................101
17.31 SLV3_CONFIG (20h) .........................................................101
17.32 DATAWRITE_SLV0 (21h)......................................................102
17.33 STATUS_MASTER (22h)......................................................102
18 Soldering information........................................................... 103
19 Package information............................................................ 104
19.1 LGA-16L package information..................................................104
Revision history ..................................................................... 105
List of tables ........................................................................ 112
List of figures........................................................................ 118
DS13005 - Rev 7 page 111/119

IIS2ICLX
List of tables
List of tables
Table 1. Pin description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 8
Table 2. Mechanical characteristics . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 9
Table 3. Electrical characteristics. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 10
Table 4. Temperature sensor characteristics . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 10
Table 5. SPI slave timing values (in mode 3) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 11
Table 6. I²C slave timing values . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 12
Table 7. Absolute maximum ratings . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 13
Table 8. Serial interface pin description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 14
Table 9. I²C terminology . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 14
Table 10. SAD+read/write patterns. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 15
Table 11. Transfer when master is writing one byte to slave. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 15
Table 12. Transfer when master is writing multiple bytes to slave. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 15
Table 13. Transfer when master is receiving (reading) one byte of data from slave. . . . . . . . . . . . . . . . . . . . . . . . . . . . . 15
Table 14. Transfer when master is receiving (reading) multiple bytes of data from slave . . . . . . . . . . . . . . . . . . . . . . . . . 15
Table 15. Master I²C pin details. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 19
Table 16. Internal pin status . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 30
Table 17. Registers address map. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 31
Table 18. FUNC_CFG_ACCESS register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 33
Table 19. FUNC_CFG_ACCESS register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 33
Table 20. PIN_CTRL register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 33
Table 21. PIN_CTRL register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 33
Table 22. FIFO_CTRL1 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 34
Table 23. FIFO_CTRL1 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 34
Table 24. FIFO_CTRL2 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 34
Table 25. FIFO_CTRL2 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 34
Table 26. FIFO_CTRL3 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 35
Table 27. FIFO_CTRL3 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 35
Table 28. FIFO_CTRL4 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 36
Table 29. FIFO_CTRL4 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 36
Table 30. COUNTER_BDR_REG1 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 37
Table 31. COUNTER_BDR_REG1 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 37
Table 32. COUNTER_BDR_REG2 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 37
Table 33. INT1_CTRL register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 38
Table 34. INT2_CTRL register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 38
Table 35. INT2_CTRL register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 38
Table 36. Who_Am_I register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 38
Table 37. CTRL1_XL register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 39
Table 38. Accelerometer ODR selection . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 39
Table 39. Accelerometer full-scale selection . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 39
Table 40. CTRL3_C register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 40
Table 41. CTRL3_C register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 40
Table 42. CTRL4_C register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 41
Table 43. CTRL4_C register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 41
Table 44. CTRL5_C register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 41
Table 45. CTRL5_C register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 41
Table 46. Linear acceleration sensor self-test mode selection . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 41
Table 47. CTRL6_C register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 42
Table 48. CTRL6_C register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 42
Table 49. Trigger mode selection. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 42
Table 50. CTRL7_XL register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 42
Table 51. CTRL7_XL register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 42
Table 52. CTRL8_XL register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 43
Table 53. Accelerometer bandwidth configurations. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 43
DS13005 - Rev 7 page 112/119

IIS2ICLX
List of tables
Table 54. CTRL9_XL register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 44
Table 55. CTRL9_XL register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 44
Table 56. CTRL10_C register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 44
Table 57. CTRL10_C register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 44
Table 58. ALL_INT_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 45
Table 59. ALL_INT_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 45
Table 60. WAKE_UP_SRC register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 45
Table 61. WAKE_UP_SRC register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 45
Table 62. TAP_SRC register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 46
Table 63. TAP_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 46
Table 64. DEN_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 46
Table 65. DEN_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 46
Table 66. STATUS_REG register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 47
Table 67. STATUS_REG register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 47
Table 68. OUT_TEMP_L register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 47
Table 69. OUT_TEMP_H register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 47
Table 70. OUT_TEMP register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 47
Table 71. OUTX_L_A register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 72. OUTX_H_A register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 73. OUTX_H_A register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 74. OUTY_L_A register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 75. OUTY_H_A register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 76. OUTY_H_A register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 77. EMB_FUNC_STATUS_MAINPAGE register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 78. EMB_FUNC_STATUS_MAINPAGE register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 48
Table 79. FSM_STATUS_A_MAINPAGE register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 49
Table 80. FSM_STATUS_A_MAINPAGE register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 49
Table 81. FSM_STATUS_B_MAINPAGE register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 49
Table 82. FSM_STATUS_B_MAINPAGE register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 49
Table 83. MLC_STATUS_MAINPAGE register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 50
Table 84. MLC_STATUS_MAINPAGE register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 50
Table 85. STATUS_MASTER_MAINPAGE register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 50
Table 86. STATUS_MASTER_MAINPAGE register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 50
Table 87. FIFO_STATUS1 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 51
Table 88. FIFO_STATUS1 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 51
Table 89. FIFO_STATUS2 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 51
Table 90. FIFO_STATUS2 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 51
Table 91. TIMESTAMP output registers . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 52
Table 92. TIMESTAMP output register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 52
Table 93. TAP_CFG0 register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 53
Table 94. TAP_CFG0 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 53
Table 95. TAP_CFG1 register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 53
Table 96. TAP_CFG1 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 53
Table 97. TAP_CFG2 register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 54
Table 98. TAP_CFG2 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 54
Table 99. INT_DUR2 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 54
Table 100. INT_DUR2 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 54
Table 101. WAKE_UP_THS register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 55
Table 102. WAKE_UP_THS register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 55
Table 103. WAKE_UP_DUR register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 55
Table 104. WAKE_UP_DUR register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 55
Table 105. MD1_CFG register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 56
Table 106. MD1_CFG register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 56
Table 107. MD2_CFG register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 57
Table 108. MD2_CFG register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 57
DS13005 - Rev 7 page 113/119

IIS2ICLX
List of tables
Table 109. INTERNAL_FREQ_FINE register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 58
Table 110. INTERNAL_FREQ_FINE register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 58
Table 111. X_OFS_USR register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 59
Table 112. X_OFS_USR register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 59
Table 113. Y_OFS_USR register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 59
Table 114. Y_OFS_USR register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 59
Table 115. FIFO_DATA_OUT_TAG register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 60
Table 116. FIFO_DATA_OUT_TAG register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 60
Table 117. FIFO tag. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 60
Table 118. FIFO_DATA_OUT_X_H and FIFO_DATA_OUT_X_L registers. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 61
Table 119. FIFO_DATA_OUT_X_H and FIFO_DATA_OUT_X_L register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . 61
Table 120. FIFO_DATA_OUT_Y_H and FIFO_DATA_OUT_Y_L registers. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 61
Table 121. FIFO_DATA_OUT_Y_H and FIFO_DATA_OUT_Y_L register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . 61
Table 122. FIFO_DATA_OUT_Z_H and FIFO_DATA_OUT_Z_L registers. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 61
Table 123. FIFO_DATA_OUT_Z_H and FIFO_DATA_OUT_Z_L register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . 61
Table 124. Register address map - embedded functions. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 62
Table 125. PAGE_SEL register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
Table 126. PAGE_SEL register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
Table 127. EMB_FUNC_EN_B register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
Table 128. EMB_FUNC_EN_B register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
Table 129. PAGE_ADDRESS register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
Table 130. PAGE_ADDRESS register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 64
Table 131. PAGE_VALUE register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 65
Table 132. PAGE_VALUE register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 65
Table 133. EMB_FUNC_INT1 register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 65
Table 134. EMB_FUNC_INT1 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 65
Table 135. FSM_INT1_A register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 66
Table 136. FSM_INT1_A register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 66
Table 137. FSM_INT1_B register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 67
Table 138. FSM_INT1_B register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 67
Table 139. MLC_INT1 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 68
Table 140. MLC_INT1 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 68
Table 141. EMB_FUNC_INT2 register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 68
Table 142. EMB_FUNC_INT2 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 68
Table 143. FSM_INT2_A register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 69
Table 144. FSM_INT2_A register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 69
Table 145. FSM_INT2_B register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 70
Table 146. FSM_INT2_B register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 70
Table 147. MLC_INT2 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 71
Table 148. MLC_INT2 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 71
Table 149. EMB_FUNC_STATUS register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 71
Table 150. EMB_FUNC_STATUS register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 71
Table 151. FSM_STATUS_A register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 72
Table 152. FSM_STATUS_A register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 72
Table 153. FSM_STATUS_B register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 72
Table 154. FSM_STATUS_B register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 72
Table 155. MLC_STATUS register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
Table 156. MLC_STATUS register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
Table 157. PAGE_RW register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
Table 158. PAGE_RW register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 73
Table 159. FSM_ENABLE_A register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74
Table 160. FSM_ENABLE_A register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74
Table 161. FSM_ENABLE_B register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74
Table 162. FSM_ENABLE_B register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 74
Table 163. FSM_LONG_COUNTER_L register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75
DS13005 - Rev 7 page 114/119

IIS2ICLX
List of tables
Table 164. FSM_LONG_COUNTER_L register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75
Table 165. FSM_LONG_COUNTER_H register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75
Table 166. FSM_LONG_COUNTER_H register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75
Table 167. FSM_LONG_COUNTER_CLEAR register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75
Table 168. FSM_LONG_COUNTER_CLEAR register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 75
Table 169. FSM_OUTS1 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 76
Table 170. FSM_OUTS1 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 76
Table 171. FSM_OUTS2 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 76
Table 172. FSM_OUTS2 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 76
Table 173. FSM_OUTS3 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
Table 174. FSM_OUTS3 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
Table 175. FSM_OUTS4 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
Table 176. FSM_OUTS4 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 77
Table 177. FSM_OUTS5 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 78
Table 178. FSM_OUTS5 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 78
Table 179. FSM_OUTS6 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 78
Table 180. FSM_OUTS6 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 78
Table 181. FSM_OUTS7 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 79
Table 182. FSM_OUTS7 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 79
Table 183. FSM_OUTS8 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 79
Table 184. FSM_OUTS8 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 79
Table 185. FSM_OUTS9 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 80
Table 186. FSM_OUTS9 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 80
Table 187. FSM_OUTS10 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 80
Table 188. FSM_OUTS10 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 80
Table 189. FSM_OUTS11 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 81
Table 190. FSM_OUTS11 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 81
Table 191. FSM_OUTS12 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 81
Table 192. FSM_OUTS12 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 81
Table 193. FSM_OUTS13 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 82
Table 194. FSM_OUTS13 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 82
Table 195. FSM_OUTS14 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 82
Table 196. FSM_OUTS14 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 82
Table 197. FSM_OUTS15 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 83
Table 198. FSM_OUTS15 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 83
Table 199. FSM_OUTS16 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 83
Table 200. FSM_OUTS16 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 83
Table 201. EMB_FUNC_ODR_CFG_B register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84
Table 202. EMB_FUNC_ODR_CFG_B register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84
Table 203. EMB_FUNC_ODR_CFG_C register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84
Table 204. EMB_FUNC_ODR_CFG_C register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84
Table 205. EMB_FUNC_INIT_B register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84
Table 206. EMB_FUNC_INIT_B register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 84
Table 207. MLC0_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 208. MLC0_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 209. MLC1_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 210. MLC1_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 211. MLC2_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 212. MLC2_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 213. MLC3_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 214. MLC3_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 85
Table 215. MLC4_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
Table 216. MLC4_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
Table 217. MLC5_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
Table 218. MLC5_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
DS13005 - Rev 7 page 115/119

IIS2ICLX
List of tables
Table 219. MLC6_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
Table 220. MLC6_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
Table 221. MLC7_SRC register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
Table 222. MLC7_SRC register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 86
Table 223. Register address map - embedded advanced features page 1. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 87
Table 224. FSM_LC_TIMEOUT_L register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 88
Table 225. FSM_LC_TIMEOUT_L register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 88
Table 226. FSM_LC_TIMEOUT_H register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 88
Table 227. FSM_LC_TIMEOUT_H register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 88
Table 228. FSM_PROGRAMS register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 88
Table 229. FSM_PROGRAMS register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 88
Table 230. FSM_START_ADD_L register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 89
Table 231. FSM_START_ADD_L register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 89
Table 232. FSM_START_ADD_H register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 89
Table 233. FSM_START_ADD_H register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 89
Table 234. Registers address map. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 90
Table 235. SENSOR_HUB_1 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 91
Table 236. SENSOR_HUB_1 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 91
Table 237. SENSOR_HUB_2 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 91
Table 238. SENSOR_HUB_2 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 91
Table 239. SENSOR_HUB_3 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 91
Table 240. SENSOR_HUB_3 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 91
Table 241. SENSOR_HUB_4 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
Table 242. SENSOR_HUB_4 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
Table 243. SENSOR_HUB_5 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
Table 244. SENSOR_HUB_5 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
Table 245. SENSOR_HUB_6 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
Table 246. SENSOR_HUB_6 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 92
Table 247. SENSOR_HUB_7 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93
Table 248. SENSOR_HUB_7 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93
Table 249. SENSOR_HUB_8 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93
Table 250. SENSOR_HUB_8 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93
Table 251. SENSOR_HUB_9 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93
Table 252. SENSOR_HUB_9 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 93
Table 253. SENSOR_HUB_10 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94
Table 254. SENSOR_HUB_10 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94
Table 255. SENSOR_HUB_11 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94
Table 256. SENSOR_HUB_11 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94
Table 257. SENSOR_HUB_12 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94
Table 258. SENSOR_HUB_12 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 94
Table 259. SENSOR_HUB_13 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
Table 260. SENSOR_HUB_13 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
Table 261. SENSOR_HUB_14 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
Table 262. SENSOR_HUB_14 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
Table 263. SENSOR_HUB_15 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
Table 264. SENSOR_HUB_15 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 95
Table 265. SENSOR_HUB_16 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
Table 266. SENSOR_HUB_16 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
Table 267. SENSOR_HUB_17 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
Table 268. SENSOR_HUB_17 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
Table 269. SENSOR_HUB_18 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
Table 270. SENSOR_HUB_18 register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 96
Table 271. MASTER_CONFIG register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 97
Table 272. MASTER_CONFIG register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 97
Table 273. SLV0_ADD register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
DS13005 - Rev 7 page 116/119

IIS2ICLX
List of tables
Table 274. SLV0_ADD register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
Table 275. SLV0_SUBADD register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
Table 276. SLV0_SUBADD register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
Table 277. SLV0_CONFIG register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
Table 278. SLV0_CONFIG register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 98
Table 279. SLV1_ADD register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
Table 280. SLV1_ADD register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
Table 281. SLV1_SUBADD register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
Table 282. SLV1_SUBADD register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
Table 283. SLV1_CONFIG register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
Table 284. SLV1_CONFIG register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 99
Table 285. SLV2_ADD register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
Table 286. SLV2_ADD register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
Table 287. SLV2_SUBADD register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
Table 288. SLV2_SUBADD register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
Table 289. SLV2_CONFIG register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
Table 290. SLV2_CONFIG register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 100
Table 291. SLV3_ADD register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
Table 292. SLV3_ADD register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
Table 293. SLV3_SUBADD register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
Table 294. SLV3_SUBADD register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
Table 295. SLV3_CONFIG register . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
Table 296. SLV3_CONFIG register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 101
Table 297. DATAWRITE_SLV0 register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
Table 298. DATAWRITE_SLV0 register description . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
Table 299. STATUS_MASTER register. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
Table 300. STATUS_MASTER register description. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 102
Table 301. Outer dimensions. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 104
Table 302. Document revision history. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 105
DS13005 - Rev 7 page 117/119

IIS2ICLX
List of figures
List of figures
Figure 1. Generic state machine. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 5
Figure 2. State machine in the IIS2ICLX . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 5
Figure 3. Machine learning core in the IIS2ICLX. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 6
Figure 4. Pin connections . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 7
Figure 5. IIS2ICLX connection modes. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 7
Figure 6. SPI slave timing diagram (in mode 3) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 11
Figure 7. I²C slave timing diagram . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 12
Figure 8. Read and write protocol (in mode 3) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 16
Figure 9. SPI read protocol (in mode 3). . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 17
Figure 10. Multiple byte SPI read protocol (2-byte example) (in mode 3) . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 17
Figure 11. SPI write protocol (in mode 3). . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 18
Figure 12. Multiple byte SPI write protocol (2-byte example) (in mode 3). . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 18
Figure 13. SPI read protocol in 3-wire mode (in mode 3). . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 18
Figure 14. Block diagram of filters . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 20
Figure 15. Accelerometer UI chain. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 20
Figure 16. Accelerometer composite filter . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 21
Figure 17. Filtering chain. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 25
Figure 18. Frequency response at the output of LPF1 filter at different ODR configurations . . . . . . . . . . . . . . . . . . . . . . 25
Figure 19. Frequency response- X-axis ODR = 833 Hz, BW = ODR/2. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 26
Figure 20. Frequency response - Y-axis ODR = 833 Hz, BW = ODR/2 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 26
Figure 21. Frequency response - X-axis ODR = 104 Hz, BW = ODR/2 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 26
Figure 22. Frequency response - Y-axis ODR = 104 Hz, BW = ODR/2 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 27
Figure 23. Frequency response - X-axis ODR = 12.5 Hz, BW = ODR/2. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 27
Figure 24. Frequency response - Y-axis ODR = 12.5 Hz, BW = ODR/2. . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 27
Figure 25. IIS2ICLX electrical connections in mode 1 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 28
Figure 26. IIS2ICLX electrical connections in mode 2 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 29
Figure 27. Ceramic cavity LGA-16: package outline and mechanical data . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 104
DS13005 - Rev 7 page 118/119

IIS2ICLX
IMPORTANT NOTICE – READ CAREFULLY
STMicroelectronics NV and its subsidiaries (“ST”) reserve the right to make changes, corrections, enhancements, modifications, and improvements to ST
products and/or to this document at any time without notice. Purchasers should obtain the latest relevant information on ST products before placing orders. ST
products are sold pursuant to ST’s terms and conditions of sale in place at the time of order acknowledgment.
Purchasers are solely responsible for the choice, selection, and use of ST products and ST assumes no liability for application assistance or the design of
purchasers’ products.
No license, express or implied, to any intellectual property right is granted by ST herein.
Resale of ST products with provisions different from the information set forth herein shall void any warranty granted by ST for such product.
ST and the ST logo are trademarks of ST. For additional information about ST trademarks, refer to www.st.com/trademarks. All other product or service names
are the property of their respective owners.
Information in this document supersedes and replaces information previously supplied in any prior versions of this document.
© 2022 STMicroelectronics – All rights reserved
DS13005 - Rev 7 page 119/119