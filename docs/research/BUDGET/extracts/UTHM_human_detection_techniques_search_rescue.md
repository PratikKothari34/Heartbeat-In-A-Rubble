> **EXTRACT - full text, converted from PDF 2026-10-08 (markitdown).**
> *Human Detection Techniques for Search and Rescue* (UTHM) - a survey of victim-detection
> modalities. Source PDF deleted after conversion (gitignored).
>
> Listed in `docs/research/BUDGET/01-literature.md` row 9 as **HELD**, no figure quoted.
> Useful as a **survey-level map of the incumbent modality space** (acoustic, seismic, radar,
> thermal, CO2) for the related-work section of the proposal.
>
> A survey is not a measurement: cite it for *what approaches exist*, never for a performance
> number. Any figure wanted from here must be chased to its primary source first.

Evolution of Information, Communication and Computing Systems (EICCS)
https://publisher.uthm.edu.my/bookseries/index.php/eiccs
Human Detection Techniques for Search and
Rescue of Trapped Victims Under Debris: A
Review
Sajjad Ahmed1,2*, Ariffuddin Joret2, Norshidah Katiran2, and Muhammad
Suhaimi Sulong3
1Quaid-e-Awam University of Engineering, Science and Technology (QUEST) Nawabshah, PAKISTAN
2Faculty of Electrical and Electronic Engineering,
Universiti Tun Hussein Onn Malaysia, Johor, MALAYSIA
3Faculty of Technical and Vocational Education,
Universiti Tun Hussein Onn Malaysia, Johor, MALAYSIA
*Corresponding Author
Abstract:
This study presents a comparative review study on human detection techniques for search and rescue
of trapped victims under debris. Natural calamities are increasingly common as climate change
becomes more serious. Search and rescue missions become more and more important to humanity
worldwide. Often, time is a crucial factor for an optimistic result of search and rescue operations.
Different technology-based techniques are used for human detection, including radar techniques,
robotics techniques, drone techniques, gas sensor techniques, optical acoustic/seismic techniques,
and infrared techniques. Furthermore, analyzing of advantages and disadvantages of the different
types of human detection techniques and the development direction of human detection techniques
is presented in this review. At present, there is a need for advanced human detection systems that
can support rescue operations, while improving location accuracy and speed in a short period of time.
Keywords:
Radar  Robotics  Drone  Gas sensor  Optical  Acoustic/Seismic  Infrared  Trapped victims 
Human detection technique  Debris
1. Introduction
Every year, thousands of humans experience their last breath under the rubble of collapsed
buildings due to natural disasters such as earthquakes, flooding, hurricane, and other incidents that turn
buildings infrastructure into piles of debris. Among all the operations carried out in natural disasters,
such as earthquakes, fires and building collapses, the search and rescue of entrapped victims has priority
[1]. Survival rates decline after 72 hours of being trapped under the rubble of the collapsed buildings,
and without access to water, most victims are unlikely to survive longer than 120 hours [2]. Human
detection techniques and tools find and locate humans under debris based on the victim's senses, such
as sight, hearing and smell. The history of revolutionary systems to detect human survivors trapped
under the debris starts with the work of Kun-Mu Chen [3] that carries out the concept of detection of
buried humans using microwave beams in 1985. The researcher had put their efforts time by time to
*Corresponding author: sajjadbhatti@quest.edu.pk
2022 UTHM Publisher. All rights reserved.

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
develop various human detection technologies for disaster situations. These human detection systems
are based on many technologies which are discussed here.
2. Human Detection Systems
The signal such as radio frequency reflection, heartbeat, and pulses of humans buried under rubble
would become into energy sources like radio waves, light waves, sound waves, infrared rays, and video
images. Human detection systems are a kind of acquisition system for different forms of a wave through
which signal data is analyzed through sensors and different technologies tools to determine the location
of victims buried under rubble.
2.1 Radar Human Detection System
Radar technology has recently gained much attention for detecting survivors under debris [4]. Radar
has the ability to penetrate through debris to detect the signal of vital signs or non-invasive techniques
such as breathing rate, heartbeat, and pulse rate of the targeted victim. Types of radar detection systems
are discussed here.
2.1.1 Continuous Wave (CW) Radar Human Detection System
The approach of continuous wave radar detection system instigates continuous microwave beam
on a human body, in result system obtains returned echo signal in form of heart rate, pulse rate, etc.
which further process through signal processing technique for extracting of the parameters of the body
of life signals. This type of radar is used to measure distance in the frequency domain and the resolution
range depends on the frequency domain resolution that can be altered as preferred [5]. The received
signal to recognize humans under the ruins from the antenna affects the time variation of the radar to
detect the survivor [6]. CW radar based on radar vital signs monitor (RVSM) technology for vital sign
detection was discussed in [7].
CW radar with the dual-frequency operation was presented in [8]. The proposed human detection
system with low and high-frequency combinations indicated a good potential application for search
operations because it exhibited effective carrier interference suppression. The work in [9] developed a
human-detection system based on CW radar for the detection of several human targets buried under
wreckage. The author developed the Blind Source Separation (BSS) signal processing technique along
with a multiple-antenna MIMO configuration for the detection of several human targets simultaneously.
2.1.2 Frequency Modulated Continuous Wave (FMCW) Radar Human Detection System
FMCW radar works on the principle of beat frequency which is a difference of transmitted and
reflected signals of the target. Further FMCW techniques achieve the velocity, range measurement with
less power [10]. FMCW radar technology has broad applications in the field of search and rescue of
human beings in disaster conditions. The experimental work of FMCW radar with a frequency range of
1.2-2.2GHz started for detection of targets under snowpack by Y. Yamaguchi, et. al. in the 1990s [11],
[12], and [13]. Further in [14], an FMCW radar system was developed for the detection of human targets
through the wall structure. Maaref et. al. [15] used FMCW radar equipped with an antenna system for
through the wall detection of human subjects.
Non-contact detection of vital signs has rising importance for human localization in disaster rescue,
in such case, FMCW radar technology is also considered a fine solution for vital signs detection. FMCW
radar technology has previously been presented in the earlier for numerous applications associated to
vital signs detection. In [16] and [17] FMCW radar was used for the detection of heartbeat rate with a
frequency range of 24 GHz and 9.6 GHz respectively. While in [18] FMCW radar prototype was designed
Page | 55

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
along with a patch antenna system for monitoring of non-contact vital signs. Different systems have
been developed by researchers for bringing improvement in vital sign detection. A study in [19] showed
the FMCW radar has been used in small displacement detection systems and projection matrix methods
for the detection of human vital signs. Another work in [20] also used a small-displacement detection
system for monitoring human respiration through FMCW radar.
2.1.3 Stepped Frequency Continuous Wave (SFCW) Radar Human Detection System
The working principle of SFCW radar is simple, it transmits a series of discrete frames linearly to the
direction of the target. Furthermore, it offers good target detection accuracy with simple calibration
procedures and post-processing techniques [21]. The work in [22] was performed through wall
experiments for the detection of human activities by SFCW radar with 93% to 98 % accuracy. Gumbmann
et. al. [21] developed a short-range imaging system based on the SFCW approach for the detection of
targets with high sweep rates and low ambiguity level. In addition, physical experiments for the
detection of human survivors under debris through the SFCW radar approach have been conducted in
[23]. The proposed radar system used 100MHz - 1GHz frequency and showed the ability to detect a
victim buried under thick debris of one meter.
As this radar system has fine range resolution and Doppler sensitivity for monitoring several human
vital signs [24], it has been widely studied for applications such as vital signs monitoring, and object
detection behind obstacles [25], [26]. The work in [27] performed real-time experiments for the
detection and localization of multiple stationary human targets behind walls based on dual-station
SFCW radars. The cross-correlation algorithm was introduced in this work to effectively detect multiple
targets and to provide a range pairing mechanism for dual radars.
2.1.4 Ground Penetrating Radar (GPR) Human Detection System
Ground penetrating radar (GPR) is known as a geophysical technique for imaging the earth's
subsurface and detecting buried objects. GPR has the ability to resolve many problems where the
answers are buried in the earth subsurface. The GPR technique works by transmitting antenna sends
radio waves into ground surface or rubble and strike the hidden target, when these waves touch targets
with different electromagnetic characteristics, these waves reflected back and received by the receiver
antenna. The first patent for a GPR system for tracking hidden objects was filled in 1910 [28] and then
the first survey was conducted by using the system for mapping glaciers in 1929 [29]. Nowadays GPR
techniques are in focus for research in many applications such as, detection of buried objects, locating
of utility, fault detection in the concrete structure, and human trapped detection in the rubble [30], [31].
Locating of humans buried or trapped under debris is a developing field of GPR application. The
work in [32] showed GPR-based detection and localization of objects under voids in the rubble of
disaster conditions during search and rescue operation. The proposed method with the developed
algorithm achieved overall good results considering both real and simulated GPR scans with 93%
accuracy. Yuan et. al. [33] developed GPR based new drop–flow algorithm for the detection of
underground utilities with a detection rate of 84% and a precision of 78%. In [34] demonstrated GPR
numerical modeling and estimations of target response magnitude when buried in a complex
subsurface such as encountered in search and rescue situations. In addition, the GPR approach was used
for the detection of buried human bodies [35] in order to increase the effectiveness and efficiency of
natural disaster victims by conducting simulation and measurement methods.
Page | 56

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
2.2 Robotics Human Detection System
Nowadays search and rescue using robotics technology is a huge and active field in both academia
and industry. Robots are the perfect choice for when it is dangerous to send in humans in search and
rescue including disaster situations such as earthquakes, fires, avalanches, minefields, and floods. Rescue
robots are based on different sensors technologies such as vision sensors, ultrasonic sensors, heat
sensors, laser range finders, electromagnetic wave sensors, and GPS sensors. The robot for rescue
purposes is made with a long and thin structure through different tracked vehicles in series, so it can
pass through narrow and small spaces. The disaster robot system consists of four structural parts, such
as robot, sensor, communication network, and monitoring unit. When humans are trapped inside the
rubble, it will be difficult to search and rescue them quickly, in these circumstances mobile robots are
used that can enter the building and find if there is any victim there and then send a signal to the rescue
team to call for help [36].
According to the work in [37] and [38], the purpose of using robots is to help the first-aid workers
by providing them an image of a place that they cannot reach for rescuing of victims if any. The first
attempt at real-time robots was used during the World Trade Center disaster rescue mission in New
York in 2001 [39]. Since then, worldwide attention in robots for search and rescue operations has grown
rapidly. Six remotely-controlled rescue robots were used during the World Trade Center by the rescue
team for tracking human victims trapped under rubble. Robots can be easily used and controlled in
dangerous situations such as bomb disposal, mining fields, and also for cleaning toxic wastes. In 2019,
the development of a human detection robot for rescue operations in natural calamities was presented
[40]. The robot model used a radar technique which is based on electromagnetic wave signal reflection
for detection of targets which can be controlled through mobile application with Bluetooth module.
Nowadays different technologies are integrated into robots for search and rescue purposed in
natural calamities. Cao Xin et. al. [41] presented a robot system based on Internet of Things technology
for human detection under debris. Another robot based on image processing and neural networks
system was proposed in [42] for human detection in the operation of urban search and rescue. In 2018,
a research work was presented [43] where the main focus was on live human detection in battle fields
and earthquake site using robots. The robot system was integrated with GPS, GSM, sensors, and
camouflage technologies for effective detection. Furthermore, referring to the work in [44] and [45], a
robot system had been designed for the detection of survivors during a disaster situation.
2.3 Gas Sensor Human Detection System
The gas sensor is the smallest and cheapest device for detecting people by smell, which could be
used in the search for people buried under the rubble of an earthquake or any disaster. Further, gas
sensors are considered as tiny electronic rescue dogs which are the size of small computer chips. These
gas sensors emit in low concentrations via human breath or skin, whereas it has also been confirmed
that the use of gas sensors for human sensing is possible through analysis of changes in carbon dioxide
(CO2) and oxygen (O2) in the environment due to human respiration [46]. The gas sensor is capable to
determine CO2, propane, and methane. CO2 measurements are used to detect the breathing of living
trapped victims. Additionally, CO2, propane, and methane are also used to detect dangerous gas
concentrations for human rescuers [47]. The ChemPro chemical detector was used for the detection of
selected volatile organic compounds known to be possible signs of human presence under debris [48].
The work in [49] proposes to use a CO2 detector to detect survivors based on particular thresholds.
In 2018, Güntner et. al. [50] developed novel gas sensor arrays to detect acetone, ammonia,
isoprene, CO2, and relative humidity (RH) from metabolic tracers emitted from breath and skin, all jointly
working as signs of life for tracking entrapped humans. This pilot study shows that such sensor arrays
Page | 57

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
could be quite effective during natural calamity situations for rescuers teams. In the same year, another
study was proposed by Zhang et. al. [51]. A CO2 sensor was proposed and tested for detecting living
victims trapped under debris. The efficiency of the sensor was evaluated and confirmed through
experiments. The gas sensor's performance in detecting living victims under debris was tested in a high-
fidelity simulated disaster area. The results show that the CO2 sensor can provide useful information to
locate a victim in a disaster. Furthermore, an experimental study on the evolution of chemical plumes
created by trapped inside collapsed buildings was conducted in [47]. The results show that gases such
as NH3, acetone and CO2 are reliable indicators of active metabolism and these compounds quickly
pass through the construction debris with a column of metabolites.
2.4 Drone Human Detection System
During natural disasters one of the key challenges faced by rescue teams is finding live humans as
early as possible, in such conditions drone human detection system is very useful to help first responders
in their search to find survivors in the disaster areas. Avalanches, floods, and wildfire are among the
most common natural calamities which make search and rescue operations extremely hard for rescue
workers [52], in such situations drone system has an advantage over other detection systems. Drone
human detection system uses different technologies such as sensors, high-definition cameras, and
wireless technology to detect human victims in disasters zone. In 2019, Naji et. al. [53] presented a drone
system equipped with standard cameras for life sign detection in disaster zones. The proposed system
uses a drone-based computer vision system to detect cardiopulmonary motion caused by periodic chest
movement in survivors. The experiment was conducted on eight human subjects and one mannequin
at distances of 4-8 meters in different positions where the results obtained have reached 100% accuracy.
Another drone system based on the passive infrared sensor (PIR), radio frequency technique, and
microcontroller for earthquake rescue operation was reported in [54].
The use of drone technology has made it possible to find survivors at high altitude areas where
another detection system was insufficient to find live humans in less response time. A study by Tariq et.
al. [55] presented a drone system named “DronAID” for human rescue purposes in natural calamities.
The drone system used a monitoring unit integrated with a camera and sensor to detect the presence
of human subjects buried under the rubble. Another study by Lee et. al. [56] developed a drone system
based on an infrared camera and lidar sensor for human rescue in disaster situations. The experiment
was conducted in limited lighting and unknown building structure to highlight the real-world issues that
may occur in practical search and rescue operations.
2.5 Optical Human Detection System
An optical system for human subject detection under debris can be referred to as a system that
helps rescuers visually search the location and the vital status of a victim inside the rubble. To be capable
of reaching further into void space, the optical camera is generally fixed on a telescopic rod. The rescue
team then tries, as with the search camera, to access the void with the fiber optic camera through holes
and openings in the debris. Information on the inside of the rubble can then be vision by the operator
on the video screen. The dimension of a fiber optic search camera is compact in relation to other visual
rod-based detection systems which makes the fiber optic system able in accessing smaller voids and
openings. Additionally, for a better vision in darkness, the optical camera is often offered with a light
source and the system gets no interference from other sources.
The key features related to the design of optical detection systems are sensor sensitivity, sensor
size, and image processing algorithm. In [57], researchers have developed a prototype of an optical
sensor network for rescue operations for urban search and rescue (USAR). The proposed devices use
the positioning of visible (VIS) and infrared (IR) range cameras to obtain images of signs of life and
Page | 58

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
detection of dangers. At the time of the design and development of the prototype, special care has
been taken to select the appropriate optical components and image processing algorithms.
Furthermore, the development of optical sensors in 2017 has been reported for detection applications
[58]. In addition, Zarco et. al. [59] developed an electro-optical detector to rescue humans during natural
calamities. The designed optical detection system consists of commercial pyloric quantum sensors and
a Cassegrain antenna which detect humans on the basis of the infrared radiation discharged by the
human body under debris.
2.6 Acoustic / Seismic Human Detection System
An acoustic/seismic system works as an amplifier of seismic activity, this system consists of sensors
that are capable to detect vibrations and sounds that are not detectable by the rescuer. These sensors
are connected through a cable to an amplifier with special indicators. The rescue team place the sensors
in the rubble and observe the sensor's response by listening in their earphone to determine the
happening of sound and seismic activity, if there is a live victim there must be some kind of sound or
motion that causes vibrations in the rubble. These vibrations are detected by an acoustic system for the
localization of live victims. Nowadays many commercial acoustic/seismic detection systems are available
in the market; one of them is delsar human detector system which is worldwide used by rescue teams
for trapped victims under the rubble of collapsed structures.
The work in [60] has shown an efficient technique based on passive acoustic sensors for the
detection of human vital signs in concealed structures. The proposed method used a geophones
network and a signal processing algorithm for detecting and recognizing vital signs. A series of
experiments have been carried out as preliminary results, confirming the promising performance of the
proposed method. Furthermore, Cao Hui et. al. [61] proposed acoustic/seismic human detection and
position system for trapped victims in earthquakes. The positioning method is the basis of the research
and development of the acoustic vibration life search and positioning system. Considering the
difficulties and time requirements of on-site rescue, a fast search method for energy tracking is
proposed.
2.7 Infrared Human Detection System
An infrared human detection system can be used in searching for sunless and hazy situations, and
help rescuers quickly and accurately detect living things buried in debris or hidden in cloudy dust with
vision capabilities in the darkness. The working principle of the infrared human detection system is very
simple when an infrared beam is directed at some part of the earthquake debris covering a victim, the
beam penetrates the debris to reach the victim. Infrared (IR) systems are widely used to measure
distances for different applications. It uses a reflected light signal to calculate the distance from an
object [62]. Snake eye detector and visual detector are commercially available human-detection systems
that are widely used in rescue missions. These devices based on infrared sensors on the outgoing and
flexible cable, gather the information from the rescue location and convert it into video images, which
will aid the rescuers to rapidly inspect whether there is a victim alive or not. An IR detection system for
the detection of humans buried under debris has been developed in [63]. The designed IR detection
system can detect and measure the heartbeat signals of the trapped victim. An experimental result
shows that the developed prototype is economical and effective and not only detects signs of human,
but also the identification of trapped victims. The work in [64] and [65] shows a passive infrared (PIR)
sensor-based detection system is developed for the detection of live human subjects. Both detection
systems are cost-effective, user-friendly, and semi-autonomous with robotics support.
Page | 59

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review

3.  Advantages and Disadvantages of Human Detection Systems
Table 1 shows a comparison of human detection systems that can be applied in search and rescue
operations. Based on this table the technique can be divided into 7 categories where all the techniques
applied are based on an electromagnetic wave, sound wave, gas, or optical signals.
Table 1: Human detection system technique comparison
| Technique  | Human  | Advantages  | Disadvantages  |
| ---------- | ------ | ----------- | -------------- |
Detection
Systems
| 1   | Radar       | UWB, deep               | Limited detection in long  |
| --- | ----------- | ----------------------- | -------------------------- |
|     | human       | penetration capability  | range and poor in multi-   |
|     | detection   | and target accurately   | target detection           |
|     | system      | inspecting              |                            |
|     | Continuous  | Simple design, low      | Low resolution range and   |
|     | Wave (CW)   | cost                    | sensitivity to outside     |
|     | Radar       |                         | interference               |
|     | FMCW radar  | Simple design, solid-   | Poor in long range target  |
|     |             | state transmitters and  | detection and external     |
|     |             | good in short range     | interference from power    |
|     |             | resolution              | source                     |
|     | SFCW radar  | It has quality of low-  | Require more acquisition   |
|     |             | probability-of-         | time and poor in long      |
|     |             | intercept radar (LPIR)  | range target detection     |
and good in
resolution
|     | GPR  | Deep penetration    | Difficulty in linear scan due  |
| --- | ---- | ------------------- | ------------------------------ |
|     |      | capability and low  | to piles of debris and         |
|     |      | cost                | rubble material has            |
cluttered heterogeneous
nature it makes difficult to
recognize victim
| 2   | Robotics    | Robots can get into     | Costly, more improvement      |
| --- | ----------- | ----------------------- | ----------------------------- |
|     | human       | locations that humans   | required in design, sensor,   |
|     | detection   | cannot because of       | decoding behavior,            |
|     | system      | small size, high heat,  | algorithms and                |
|     |             | and environmental       | communications links          |
|     |             | toxicity                |                               |
| 3   | Gas sensor  | High sensitivity,       | It has increased airflow      |
|     | human       | compact size and low    | which makes difficult to use  |
|     | detection   | cost                    | in open environment, still    |
|     | system      |                         | no commercial product is      |
|     |             |                         | lunched. Experiments are      |
|     |             |                         | only conducted in             |
|     |             |                         | laboratory                    |
| 4   | Drone       | Reduce the rescue       | Limited communication         |
|     | human       | time, search a larger   | range, not enough             |
  detection  area in a shorter time  precision in navigation
|     | system  | period and reach at     |     |
| --- | ------- | ----------------------- | --- |
|     |         | high altitude and hard  |     |
areas
Page | 60

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review

| 5   | Optical    | Inexpensive, low   | Image visibility is narrow,  |
| --- | ---------- | ------------------ | ---------------------------- |
|     | human      | power consumption  | skilled operators are        |
|     | detection  |                    | required and cannot be       |
|     | system     |                    | used in inaccessible         |
location
| 6   | Acoustic /  | Penetration through    | Limited range,                |
| --- | ----------- | ---------------------- | ----------------------------- |
|     | Seismic     | metal objects and      | ineffectiveness in concrete,  |
|     | human       | sensitivity to detect  | and inability to detect       |
|     | detection   | slow motion            | unconscious victims           |
system
| 7   | Infrared   | Rescue victim in    | Low penetration, to know      |
| --- | ---------- | ------------------- | ----------------------------- |
|     | human      | narrow spaces, low  | the condition of the victim,  |
|     | detection  | cost and            | holes are needed to place     |
|     | system     | portable            | the probe at the disaster     |
|     |            |                     | site                          |

4.  Conclusion
A comparative review-based study into human detection techniques for search and rescue of
trapped victims under debris has been performed in this paper. A detailed summary of a Radar human
detection system, Robotics human detection system, Drone human detection system, Gas sensor human
detection system, Optical human detection system, Acoustic/Seismic human detection system, and
Infrared human detection system, with different research techniques have been presented. At present,
the research of human detection systems is mainly based on integrated sensor technology. Human
detection-based search and rescue needs a wide range of information because of difficult and changing
environmental conditions such as high altitude zones, hot weather, low visibility, loud sound, power
failure, and other sceneries that happen during natural calamities. In search and rescue operations, time
is considered a critical factor as lives are in danger. To handle such scenarios human detection system
must base on multi-sensor technology which can search a huge area within a very short spell of time
with better accuracy, measurement, and fine resolution. In order to acquire the entire information of
live human subjects within the environment of the disasters zone, the drone technique is brought into
the human-detection system. Drone technology can be integrated with other modern techniques such
as swarm intelligence, machine learning, and 5G networks for gathering comprehensive and secure
information of survivors during natural calamities.
References
[1]   Manaseer, S., Alawneh, A.: A New Mobility Model for Ad Hoc Networks in Disaster Recovery
Areas. Int. J. Online Eng., 13(6), 113–120, 2017.
[2]   Varanasi, V.K.: Detection of Human Activity after a Natural Disaster. Journal of Geography &
Natural Disasters, 1(1), 1–2, 2011. https://doi.org/10.4172/2167-0587.1000
[3]   Chen, K.M. et al: An X-Band Microwave Life-Detection System. 7, 697–701, 1986.
[4]   Van, N.T.P., Tang, L., Demir, V., Hasan, S.F., Minh, N.D., Mukhopadhyay, S.: Review-microwave
radar sensing systems for search and rescue purposes. Sensors (Switzerland), 19(13), 1–24, 2019.
https://doi.org/10.3390/s19132879.
[5]  Zhao, G., Liang, Q., Durrani, T.S.: UWB Radar Target Detection Based on Hidden Markov Models.
IEEE Access, 6(c), 28702–28711, 2018. https://doi.org/10.1109/ACCESS.2018.2839690
Page | 61

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
[6] Akiyama, I., Yoshizumi, N., Ohya, A., Aoki, Y., Matsuno, F.: Search for survivors buried in rubble
by rescue radar with array antennas - Extraction of respiratory fluctuation -. SSRR2007 - IEEE
International Workshop on Safety, Security and Rescue Robotics Proceedings, (September), 0–
5, 2007. https://doi.org/10.1109/SSRR.2007.4381292
[7] Geisheimer: Origins of RVsm. IEEE Potentials, 21–24, 1999.
[8] Zhang, Y., Jiao, T., Lv, H., Li, S., Li, C.: An Interference Suppression Technique for Life Detection
Using 5.75- and 35-GHz Dual-Frequency Continuous-Wave Radar 12(3), 482–486, 2015.
[9] Indu, S., Gupta, A., Kaw, A., Gehi, S.: Life detection system using continuous wave Doppler radar
and blind source separation. Proceedings of 2nd International Conference on 2017 Devices for
Integrated Circuit, DevIC 2017, 711–715, 2017. https://doi.org/10.1109/DEVIC.2017.8074043
[10] Li, C., Xiao, Y., Lin, J.: Experiment and spectral analysis of a low-power K a-band heartbeat
detector measuring from four sides of a human body. IEEE Transactions on Microwave Theory
and Techniques, 54(12), 4464–4471, 2006. https://doi.org/10.1109/TMTT.2006.884652
[11] Yamaguchi, Y., Mitsumoto, M.: Synthetic Aperture FM-CW Radar Applied to the Detection of
Objects Buried in Snowpack. 32(1), 11–18, 1994.
[12] Yamaguchi, Y., Maruyama, Y., Kawakami, A., Sengoko, M., Abe, T.: Detection of objects buried in
wet snowpack by an FM-CW radar. 29(2), 0–208, 1991. doi:10.1109/36.73660
[13] Yamaguchi, Y., Maruyama, Y., Kawakami, A., Sengoko, M., Abe, T.: Human body detection in wet
snowpack by an FM-CW radar, IEEE Transactions on Geoscience and Remote Sensing, vol. 30,
no. 1, pp. 186-189, 1992.
[14] Ritchie, M., Ash, M., Chen, Q., Chetty, K.: Through wall radar classification of human micro-
doppler using singular value decomposition analysis. Sensors (Switzerland), 16(9), 2016.
https://doi.org/10.3390/s16091401.
[15] Maaref, N., Millot, P., Pichot, C., Picon, O.: FMCW ultra-wideband radar for through-the- wall
detection of human beings. 2009 International Radar Conference “Surveillance for a Safer
World”, RADAR 2009.
[16] Lee, H., Kim, B., Park, J.: A Novel Vital-Sign Sensing Algorithm for Multiple Subjects Basedon 24-
GHz FMCW Doppler Radar. 2019. https://doi.org/10.3390/rs11101237
[17] Anitori, L., Jong, A., De, Nennie, F.: FMCW radar for life-sign detection. rated Circuit, DevIC 2017,
711–715, 2017. https://doi.org/10.1109/DEVIC.2017.8074043.
[18] Wang, J., Peng, Z., Gómez-garcía, R., Li, C.: From Doppler to FMCW Radars for Non-Contact
Vital-Sign Monitoring 1 Introduction 2 Theoretical Foundations. (June), 2–5, 2018.
[19] Zhang, D., Kurata, M., Inaba, T.: FMCW Radar for Small Displacement Detection of Vital Signal
Using Projection Matrix Method. 2013(1), 1–6, 2013.
[20] Pramudita, A. A., Suratman, F. Y., Arseno, D.: Modified FMCW system for non-contact sensing of
human respiration. Journal of Medical Engineering & Technology, 1–11, 2020.
https://doi.org/10.1080/03091902.2020.1753835
[21] Gumbmann, F., Schiessl, A.: Short-Range Imaging System With a Nonuniform SFCW Approach.
1–10, 2017.
Page | 62

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
[22] Qi, F. et al; Detection and Classification of Finer-Grained Human Activities Based on Stepped-
Frequency Continuous-Wave Through-Wall Radar, 2016. https://doi.org/10.3390/s16060885
[23] Grazzini, G., Pieraccini, M., Parrini, F., Spinetti, A., Macaluso, G., Dei, D., Atzeni, C.: An Ultra-
Wideband High-Dynamic Range GPR for detecting buried people after collapse of buildings.
June, 2010. https://doi.org/10.1109/ICGPR.2010.5550259
[24] Su, W., Tang, M., Arif, R. El, Wang, F.: Stepped-Frequency Continuous-Wave Radar With Self-
Injection-Locking Technology for Monitoring Multiple Human Vital Signs. IEEE Transactions on
Microwave Theory and Techniques, PP, 1–10, 2019.
https://doi.org/10.1109/TMTT.2019.2933199
[25] Liu, L., Liu, S.: Remote Detection of Human Vital Sign With Stepped-Frequency Continuous Wave
Radar. August, 2014. https://doi.org/10.1109/JSTARS.2014.2306995
[26] Nigam, A.N.G.D.S.M.J.: Application of clutter reduction techniques for detection of metallic and
low dielectric target behind the brick wall by stepped frequency continuous wave radar in ultra-
wideband range. 416–425, 2011. https://doi.org/10.1049/iet-rsn.2010.0059
[27] Jia, Y., Guo, Y., Yan, C., Sheng, H., Cui, G., Zhong, X.: Detection and Localization for Multiple
Stationary Human Targets Based on Cross-Correlation of Dual-Station SFCW Radars. Remote
Sens. 2019, 11, 1428, 2019. https://doi.org/10.3390/rs11121428
[28] Webster, J.: GROUND-PENETRATING RADAR : OPERATION PRINCIPLE AND DATA PROCESSING.
Willy Encyclop. Of El. & Elec.Eng. 2019) https://doi.org/10.1002/047134608X.W8383
[29] Modroo, J., Olhoeft, R.G., Gound Penetrating Radar Location of Buried Avalanche Victims.
Colorado School of Mines- Department of Geophysics. 1988.
[30] Li, L., Tan, A. E., Jhamb, K., Rambabu, K.: Buried Object Characterization Using Ultra-Wideband
Ground Penetrating Radar. 1–11, 2012.
[31] Hu, D., Li, S., Chen, J., & Kamat, V.R.: Advanced Engineering Informatics Detecting , locating ,
and characterizing voids in disaster rubble for search and rescue. 42, 2019.
https://doi.org/10.1016/j.aei.2019.100974
[32] Li, S., Cai, H., Asce, M., Abraham, D. M., Asce, M., Mao, P.: Estimating Features of Underground
Utilities : Hybrid GPR / GPS Approach. 1–12, 2007. https://doi.org/10.1061/(ASCE)CP.1943-
5487.0000443.
[33] Yuan, C., Li, S., Cai, H., Asce, M., Kamat, V. R., Asce, M.: GPR Signature Detection and
Decomposition for Mapping Buried Utilities with Complex Spatial Configuration. 32(4), 1–15,
2018. https://doi.org/10.1061/(ASCE)CP.1943-5487.0000764
[34] Diamanti, N., Annan, A. P. (n.d.). Predicting GPR Performance for Buried Victim Search & Rescue.
[35] Bagaskara, A., Wafi, A., Setiawan, N. S.: Detection of buried human bodies using ground-
penetrating radar method Detection of buried human bodies using ground-penetrating radar
method, 2021. https://doi.org/10.1088/1742-6596/1876/1/012014
[36] Bhondve,T; Mukhedkar, M.: Mobile Rescue Robot for Human Body Detection in Rescue
Operation of Disaster. International Journal of Advanced Research in Electrical,Electronics and
Instrumentation Engineering ,(An ISO 3297: 2007 Certified Organization) Vol. 3, Issue 6, June,
2014.
Page | 63

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
[37] Cubber, G. D. et al; Introduction to the Use of Robotic Tools for Search and Rescue. Intechopen,
2017. DOI: 10.5772/intechopen.69489
[38] Ko, A. W. Y. & Lau, H.Y. K.: Intelligent Robot-assisted Humanitarian Search and Rescue System.
International Journal of Advanced Robotic Systems, Vol. 6, No. 2, pp. 121-128, 2009.
[39] Casper, J., & Murphy, R. R.: Human – Robot Interactions During the Robot-Assisted Urban
Search and Rescue Response at the World Trade Center. IEEE Transactions on Systems, Man,
and Cybernetics, Part B (Cybernetics), 33(3), 367–385, 2003.
https://doi.org/10.1109/TSMCB.2003.811794
[40] Joseph, A. Design of Human Detection Robot for Natural calamity Rescue Operation. 1–5, 2019.
[41] Neusoft, D.: Design and Implementation of Debris Search and Rescue Robot System Based on
Internet of Things. 2018 International Conference on Smart Grid and Electrical Automation
(ICSGEA), 303–307, 2018. https://doi.org/10.1109/ICSGEA.2018.00082
[42] Vijay, K. M. A., Purustut, S., Suhas, R., Pavan, C. G., Pradhan, P.: A Live Human Being Detector in
War Fields and Earthquake Location Using Robot with Camouflage Technology. 2018 3rd IEEE
International Conference on Recent Trends in Electronics, Information & Communication
Technology (RTEICT), 2244–2249, 2018.
[43] Awad, F., & Shamroukh, R.: Human Detection by Robotic Urban Search and Rescue Using Image
Processing and Neural Networks. (April), 39–53, 2014.
[44] Vijayaragavan, S. P.: Live Human Detecting Robot for Earthquake Rescue Operation. 02(01), 83–
87, 2013.
[45] Aoyama, H., & Sumrall, T.: Micro Hopping Robot with IR Sensor for Disaster Survivor Detection.
(June), 189–194, 2005.
[46] Huo, R. et.al; The trapped human experiment. J. Breath Res. 2011, 5, 046006.
https://doi.org/10.1088/1752-7155/5/4/046006
[47] Imlauer, S., Lassnig, K; Maurer. J., Steinbauer, G.: Life Sign Detection Based on Sound and Gas
Measurements. Proceedings of the Austrian Robotics Workshop 2014 -22-23 May, Linz, Austria.
[48] Final report summary, SGL f USA (Second Generation Locator for Urban Search and Rescue
Operations. Project reference: 217967, Funded under: FP7-Security, European Commission.
[49] Maggu, A., Rana, K., Kumar, M., Dahiya, M., Chaurasia, S.: Life detecting robot for rescue
operations. International Journal of Information Technology, vol. 4, no. 2, pp. 653–657, 2014.
[50] Gu, A. T., Pineau, N. J., Mochalski, P., Wiesenhofer, H., Agapiou, A., Mayhew, C. A., Pratsinis, S. E.:
Sni ffi ng Entrapped Humans with Sensor Arrays, 2018.
https://doi.org/10.1021/acs.analchem.8b00237
[51] Zhang, D., Sessa, S., Kasai, R., Cosentino, S., Giacomo, C.: Evaluation of a Sensor System for
Detecting Humans Trapped under Rubble : A Pilot Study. 1–13, 2018.
https://doi.org/10.3390/s18030852
[52] Mayer, S., Lischke, L., Woźniak, P. W., Mayer, S., Lischke, L., Woźniak, P. W., International, R.
Drones for Search and Rescue To cite this version : HAL Id : hal-02128385. May 2019.
Page | 64

Chapter 5: Human Detection Techniques for Search and Rescue of Trapped Victims Under Debris: A Review
[53] Al-naji, A., Perera, A. G., Mohammed, S. L., Chahl, J.: Life Signs Detector Using a Drone in Disaster
Zones. 1–12, 2019.
[54] Tariq, R., Rahim, M., Aslam, N., Bawany, N., Faseeha, U.: DronAID : A Smart Human Detection
Drone for Rescue. 2018 15th International Conference on Smart Cities: Improving Quality of Life
Using ICT & IoT (HONET-ICT), 33–37, 2018.
[55] Shobika, A., Thenkuzhali, N., Suganya, S., Nivedha, G. R., Hiemaja, R.: Human Detection System
Using Drone For Earthquake Rescue Operation. 154–160, 2018.
https://doi.org/10.17148/IJARCCE.2018.7432
[56] Lee, S., Har, D., Kum, D.: Drone-Assisted Disaster Management : Finding Victims via Infrared
Camera and Lidar Sensor Fusion. (D), 84–89, 2016.
https://doi.org/10.1109/APWC.on.CSE.2016.23
[57] Ojala, K. M., Hildebrand, L.: Optical Sensors and Algorithms for Life-Sign Detection in USaR-
Operations. (May), 1–8, 2013. https://doi.org/10.1063/1.4809690
[58] Tahir, M. W., Zaidi, N. A., Blank, R., Vinayaka, P. P., Vellekoop, M. J., Lang, W.: Fungus Detection
through Optical Sensor System using Two Different kind of Feature Vectors for the
Classification. IEEE Sensors, 1–9, 2017. https://doi.org/10.1109/JSEN.2017.2723052
[59] Nacional, I., Óptica, D. A., Postal, A.: Infrared electro-optical detector to rescue humans . 5563,
174–181, 2004. https://doi.org/10.1117/12.558933
[60] Ascione, M., Buonanno, A., Urso, M. D., Vinetti, P., Claudio, V.: A method based on passive
acoustic sensors for detection of vital signs in closed structures, 2012.
[61] Hui, C; et al; Research on the position technology of the acoustic/seismic life detection and
position system. College of information engineering; chengdu university of technology;
chengdu 610059; China, 2007.
[62] Colla,V., Sabatini, M.: A composite proximity sensor for target location and color estimation.
IMEKO Sixth International Symposium on Measurement and Control in Robotics, Brussels, pp.
134–139, 1996.
[63] Ashutosh, G., Thomas, B.: A NEW R EVOLUTIONARY INFRARED LIFE D ETECTION SYSTEM USING
ATM EGA. International Journal of Embedded Systems and applications, (IJESA) Vol.2, No.3, 168.
April 2015.
[64] Karthikeyan, S., Karthick, C., Prasath, V. S.: HUMAN TRACKING SYSTEM FOR VICTIMS TRAPPED
FROM COLLAPSED BUILDING. ARPN Journal of Engineering and Applied Sciences, 11(1), 497–
501, 2016.
[65] Uthra, B., Adchiya, D., Anupriya. K.: Live Human Detection System for Earthquake Rescue
Operation. J. of Computation in Biosciences And Engineering, 2(3), 2–4, 2015.
Page | 65