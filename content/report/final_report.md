---
title: "Development of a Compact Power Distribution System for Unmanned Surface Vehicle (USV)" 
date: 2025-11-14
lastmod: 2025-11-16
author: ["Chen Jiawei"]
description: "This report documents the work done on developing a compact power distribution system for ST Engineering's Unmanned Surface Vehicle (USV)."
summary: "This report documents the work done on developing a compact power distribution system for ST Engineering's Unmanned Surface Vehicle (USV)."
editPost:
    URL: "https://www.stengg.com/"
    Text: "ST Engineering Company Website"
showToc: true
disableAnchoredHeadings: false
---

## Acknowledgements

Firstly, I would like to thank ST Engineering for giving me the opportunity to work on this project. This project would not have been possible without the support of many dedicated ST Engineering members. I am especially grateful to Ang Ming Xiang, my ST Engineering supervisor and  Nathanel Tan, the Head of ST engineering Unmaned & Integrated System Department for providing the guidance and technical input for this project.

I also wish to acknowledge the support provided by the NUS College of Engineering, particularly Mr Royston, and Mr Graham from the Engineering Design and Innovation Centre. I would also like to thank Mr Eugene Ee for taking the time to review my project and provide valuable advice.

----
## List of Common Acronyms

<div align="center">

| **Acronym** |        **Definition**         |
| :---------: | :---------------------------: |
|   **USV**   |    Unmanned Surface Vessel    |
|   **PLC**   |    Programmable Logic Controller   |
|   **DC**   |    Direct Current    |
|   **MTBF**   |    Mean Time Before Failure    |
|   **MTTR**   |    Mean Time To Repair    |
|   **CAN**   |    Controller Area Network    |
|   **PCB**   |     Printed Circuit Board     |
|   **PDB**   |    Power Distribution Board     |
|   **PG**   |    Power Good     |

</div>

---

## 1. Summary

This project focuses on developing a compact Power Distribution System for ST Engineering's Unmanned Surface Vehicle. The PDS is a critical component of the vehicle’s electrical system, designed to distribute and control the power to different parts of the vehicle. 

The new Power Distribution System developed mainly consists of a compact and robust power switching PCB solution with a backplane design for the ease of modularity and integration. The system also includes key features such as power line protection and accurate power status monitoring and reporting, to ensure its critical functionality even when a power line fault has occured.

---

## 2. Background

### 2.1 Introduction
Unmanned Surface Vehicle (USV) is defined as a boat or ship that operates on the surface of the water without a crew.

USV market is a fast growing market recent years in the maritime industry, especially around the Asia Pacific Region. The most common way to classify USV is based on their sizes, where they are divided into 3 different size categories. Among the three, the medium size category USV, with a length of 2 to 24 meters, is the target vehicle of this project

Within the USV market, more than half of the vessel is developed for defence purpose and most of the them fall below the weight of 2000 kg, which often classified as small and medium USV.

![USV Market Size and Distribution](USV_Market_1.png)
##### Figure 1: USV Market Size and Distribution

To achieve autonomous operation, USV is often equipped with various sensors and equipment which are powered by an engine/batteries and supplied through an on board power distribution system, which is the focus of this project.

![Common USV On-board Devices](USV_Market_2.png)
##### Figure 2: Common USV On-board Devices

### 2.2 Existing Solutions
Most of the USVs nowadays still adapts a similar power distribution system as those used in the conventional boats.

Common components implemented are Transformer, DC convertors, Programmable Logic Controllers (PLCs), relays, fuse and circuit breaker. They are joint together using cables and terminal blocks

![Conventional Power Distribution System Architecture](conventional.png)
##### Figure 3: Conventional Marine DC Power Distribution System Architecture

## 3. Problem Analysis    
In order to understand further how problems may arised from applying conventional power distribution system in medium sized USV, I have carried out analysis on two signature case studies, the first one is a literature review on a marine power system product (onboard DC grid&trade;) developed by ABB, a key power system provider in the marine industry, as well as a real life product analysis on the power distribution system of ST Engineering’s medium size USVs. 

### 3.1 Onboard DC Grid&trade;
Onboard DC Grid™ is an advanced DC power distribution system developed by ABB, a leading global technology company renowned for its expertise in electrification, automation, and digital solutions. The system is designed to efficiently manage the generation, storage, and distribution of direct current (DC) power on ships, industrial platforms, and other onboard applications.

In 2020, ABB has published the report, _Unmanned Surface Vehicles/Vessel (USV) 
Reliable Power and Propulsion Architecture Characterization_, in response for a Request for Information (RFI) from the US government. In the report, the company introduce this product and highlight some problems on the current USV power architecture 

The primary concern identified in this report regarding the current power distribution solution for USV, is its negative impact on the vehicle's mission success rate. Compared to its application in conventional manned vessel, the conventioanl power distribution system used in USV has same power subsystems' Mean Time Before Failure (MTBF) but much higher Mean Time To Repair (MTTR). This is because unlike manned vehicle, faults happened during the mission of the vehicle cannot be identified and fixed on the spot due to the absence of on-board crew for USV. These faults may not be fatal for the mission at the begining, but may subsequently lead to faults in  parts of the boat that are crtical for its operation. As a result, USV has a shorter overall system MTBF compared to conventioanl vehicle, leading to more frequent failure of mission.

![USV Power System Reliability Comparison](usvpower.png)
##### Figure 4: USV Power System Reliability Comparison with Conventional Manned Vessel

### 3.2 ST Engineering USV Power Distribution System

In this project, I have the hornor to work on ST Engineering's USV and examine its power distribution system in real life.

![Discharge Voltage Curve](voltagecapacity.webp)
##### Figure 7: ST Engineering's USV Current Power Distribution System Architecture

The current system consists mainly of commercial fuses and relays, controlled by a specific power system PLC. The switching of the power channel is controlled by a continuous digital signals from the PLC. The power switching functionality of the system enables a sequential start of the main compute stacks at boat start-up as well as the shutdown of unneccessary devices for power effeciency during mission

Two main problems exists in the current system:

**Size Constraint**:
Currently, the power distribution system is housed within the equipment racks of the USV. However, due to the bulky nature of the conventional power distribution components, the system occupies a significant portion of the rack's internal volume. This oversizing poses challenges during integration, as it limits the available space for other essential components and makes maintenance tasks more cumbersome. The oversized system also complicates cable management within the rack, leading to potential issues with airflow and accessibility.

What is more, ST Engineering is designing USVs for 3 different sizes with the following dimension statistics:
| **USV Model Name** | **Length (m)** | **Width (m)** |
| :----------: | :------------: | :----------: |
|   Goldfish      |      10       |     2.5      |
|   Bellagio     |      15        |     4     |
|   Puma         |      17.5        |     5.2      |
##### Table 1: ST Engineering's USV Size Statistics

With the current power distribution system being already oversized in medium size vehicle Puma and Bellagio, it is foreseeable that the system will be even more ill-suited for the smaller USV models like Goldfish. Therefore, there is a pressing need to redesign the power distribution system to be more compact and efficient, ensuring it can fit seamlessly within the spatial constraints of all USV models while still delivering reliable performance.

**Existance of Single Pont of Failure**:
The current power distribution system lacks redundancy and fault tolerance, making it susceptible to single points of failure. 

For example, if the PLC for the power distribution system fails, due to the control logic where the ON state of power channel is maintained by a continuous digital high signal from PLC, the loss of its control signal can lead to a shutdown of all relays controlled by the PLC and a complete loss of power to all systems onboard the USV. This vulnerability poses a significant risk to the mission success rate of the USV and even the loss of the vehicle itself on the sea.  

---

## 4. Design Statement
Targeting the above identified problems, the design statement of this project are derived and summarised as:

<div align="center">
    <b>
      Design a power distribution system, to reduce the size of the current medium USV power system while increase vehicle mission success rate by improving its fault tolerance and power system monitoring
    </b>
</div>

## 4. Value Proposition

### 4.1 Stakeholders
The first stakeholders for this project is the ST Engineering USV Team members, including boat designers, manufacturers and testing engineers who will directly interact with and benefit from the improved power distribution system. Additionally, the broader ST Engineering Unmanned & Integrated Systems Department stands to gain from the advancements made in this project, as the developed technologies and methodologies can be applied to other USV projects within the department.

The second stakeholders include end-users of the USV, such as maritime security agencies and research institutions, who will benefit from the enhanced reliability and performance of the USV enabled by the new power distribution system. Improving mission success rate can greatly enhance the operational effectiveness of their tasks and reduce the extra cost of maintaining the USV from faulty situations.

### 4.2 Benefits
The new Power Distribution System offers several key benefits to its stakeholders:

| **Benefits**                                      |                  **Rationale**                   |
| :------------------------------------- | :----------------------------------------------: |
| Compact Design                        | Reduces the spatial footprint of the power distribution system, allowing for more efficient use of space within the USV's equipment racks; Increase design flexibility and scalarbility for USVs with different size requirements |
| Enhanced Fault Tolerance              | Improves the reliability of the USV by incorporating features that mitigate the impact of component failures, thereby increasing the overall mission success rate. |
| Advanced Power Monitoring and Reporting | Provides real-time insights into the power system's status, enabling proactive maintenance and informed decision-making during operations. |

---

## 5. Design Requirments

### 5.1 Technical Specifications
To begin, the new power distribution system must meet or exceed the technical performance of its predecessor. The following functional requirements were defined following the capability of the current system

| **Technical Capabilities** | **Specifications**                                                                |
| :------------------------- | :-------------------------------------------------------------------------------- |
| Maximum Physical Dimension         |  445mm x 600mm x 133mm                                                                              |
| Application Voltage             | 12V and 24V DC                                                               |
| Maximum Continuous Current         | 30A                                                                               |
| Maximum Transient Current     | 100A                                                                            |
| Fault Protection     | Overvoltage/Undervoltage/Overcurrent/Short Circuit                                                                            |
| Fault Reponse Time     |  <10ms                                                                          |                                                                           |
| Power System Monitoring                  | Current, Internal Temperature, Power Good(PG), Fault Status |
| Communication Protocol     | Digital/Analog/CAN 2.0      |

##### Table 7: Core Functional Requirements for the New Power Distribution System

The 30A current specification is based on the maximum continuous current draw possible from one channel of the current ST power distribution system (20A). This provides sufficient headroom. CAN Bus is used for communication between backplane and PLC, whose design will be explained further in the sections below.

### 5.2 Functional Sub-goals
Three main functionalities need to be achived in the new power distribution system, with each sub-goal detailed in its respective section.

| **Key Functionalities**                          |                  **Section Number**                   |
| :------------------------------------- | :---------------------------------------------------: |
| Compact & robust power switching solutions for each power channel | [Section 7](#7-Power-Switching) |
| Implement power line protection features for transient/fault situation |   [Section 8](#8-Power-Protection)    |
| Monitor and report power status and power(current) consumptions in each channel|       [Section 6](#6-Power-Monitoring)       |
##### Table 5: Key System Functionalities and Corresponding Report Section

### 5.3 Environmental Requirments

Other than functional requirements, as this product may eventually be applied to a product used in marinetime environments, proper industrial standrads has to be followed. The below design standrad requirements is derivate fro the _IEEE Recommended Practice for the Design and Application of Power Electronics in Electrical Power Systems_ and are the most relevant to this project.


| **Characteristics**  | **Constraints**                                                                        |
| :------------------- | :------------------------------------------------------------------------------------- |
| Ambient Tempreature           | ≤50°C |
| Vibration |          not less than 22Hz          |
| Humidity              | around 80% |

##### Table 6: Design Constraints for Backward Compatibility

---  

## 5. System Overview

This section presents the summarised architectures to provide a high-level overview of the systems. Subsequent sections will explain how the design choices support the overall project goals.

![Summarised Power Architecture of PMB](powerarch.png)
##### Figure 11: Summarised System Architecture of the developed power distribution system

---

## 6. Power Switching 
The new Power Distribution System is designed to provide compact and robust power switching solutions for each power channel. And this is achieved through two main improvements, moving from traditional relay + PLC combination towards PCB backplane system as well as improving the power switching logic.

### 6.1 Moving towards PCB 

#### 6.1.1 Comparison of PLC + Relay vs MCU + PCB System

As mentioned in the case study above, the current power distribution system adapted in ST Engineering USV relies on a combination of a Programmable Logic Controller (PLC) and SSR relays to manage power switching. This is also the common approach used in conventioanl power distribution system in marine industry. Another possibl approach is to use a MCU + PCB system, which involves a substantial amount of customisation and design efforts.

The below table summarises the key advantages and disadvntages between the two approaches:

| **Aspect**               | **PLC + Relay**                                                | **MCU + PCB System**                                                                                                                                   |
| ------------------------ | -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Size and Weight          | - Bulky and heavy due to discrete components<br>- Requires additional space for wiring and terminal blocks<br> | - Compact and lightweight due to integrated design<br>- Reduces wiring complexity and space requirements<br>                                           |
| Reliability and Durability | - Mechanical parts prone to wear and failure over time<br>- Susceptible to vibration and shock<br> | - Solid-state components with higher reliability<br>- Better resistance to vibration and shock<br>                                                       |
| Customisability and Scalability | - Limited customisation options<br>- Scaling up requires additional components and wiring<br> | - Highly customisable to specific requirements<br>- Easily scalable by adding or modifying PCB modules<br>                                           |

#### 6.1.2 Targeting limitations in MCU + PCB System
While the MCU + PCB system offers significant advantages in terms of size, reliability, and customisability, it also presents certain challenges that need to be addressed to ensure successful implementation.

### 6.2 Power Switching Logic Modification
As mentioned in [Section](#232-limited-capabilities-of-battery-fuel-gauge), the current control logics relied on a continous signal from PLC. This approach means that if there is any signal loss from the PLC, be it PLC failure or loose connection, the power supply maybe disturbed. In this project, I would like to introduce a new user-customisable control logic using a latching PCB design to mitigate this risk.

#### 6.2.1 Comparison Between New and Old Control Logic
The diagram below illustrates the current control logic flow and the proposed new control logic. 

![TI's Forum Search Result](forum.png)
##### Figure 18: Current Control Logic in ST Engineering USV Power Distribution System

![TI's YouTube Playlist on Battery Management](youtube.png)
##### Figure 19: New Control Logic proposed

The key difference between the two control logics is that in the current system, the ON state of power channel is maintained by a continuous digital high signal from PLC. In contrast, the new control logic uses a latching mechanism where a momentary high signal from the MCU would be able to toggles the power channel ON and only with a subsequent continous high signal , will the cahnnel be turn OFF. This means that once the power channel is turned ON, it will remain ON even if there is a loss of signal from the MCU.

#### 6.2.3 User-customisability with latching PCB Design
Although the latching PCB design improves fault tolerance, it may introduce some inconveniences during operation. For instance, if the MCU fails while the power channel is ON, the user will not be able to turn OFF the power channel remotely even if they are unneccssary to be ON during mission operation (e.g. on-board lights that are only needed during maintainence work). To address this, a seperate PCB is designed to achieve the latching mechanism while remain pluggable from the main MOSFET relay board. This makes the control logic user-customisable, allowing them to choose between the new latching control logic or revert to the old continuous signal control logic based on their operational needs.

![Latching PCB](latchingpcb_pcb.png)
##### Figure 20: Latching PCB Schematic and Layout

![Relay_Latching_PCB Combination ](Integration.png)
##### Figure 21: 3D model of the MOSFET Relay Board with Latching PCB Integrated

---

## 7. Power Protection

Power protection is crucial in ensuring the safety and reliability of the power distribution system. Current power distribution system in ST Engineering USV lacks adequate protection features, making it vulnerable to transient and fault situations. 

### 7.1 Protection Requirements
The type of faults the power protection feature of the new power distribution system should be able to handle are derivate from the design standrads mentioned in [Section 5.3](#53-environmental-requirments). The faults are overvoltage, undervoltage, overcurrent and short circuit.

#### 7.2 Choice of MOSFET Gate Driver IC - TPS4800

As a result, the MOSFET gate driver IC TPS4800 from Texas Instruments is selected among all other MOSFET gate driver IC for its ability to achieve all the above protection features and at the same time, satisy the technical specifications mentioned in [Section 5.1](#51-technical-specifications). The key features of the TPS4800 are summarised in the table below:

| **Key Features**                | **Specifications**                                                                 |
| :------------------------------ | :-------------------------------------------------------------------------------- |
| Operating Voltage               | 8V to 60V DC                                                                      |
| Maximum Continuous Current      | 30A                                                                               |
| Overvoltage Protection Threshold | Adjustable between 10V to 60V DC                                                  |
| Undervoltage Protection Threshold | Adjustable between 6V to 54V DC                                                   |
| Overcurrent Protection Response Time | <10ms                                                                          |
##### Table 13: Key Features of TPS4800 MOSFET Gate Driver IC

![Using resistors and capacitors to configure Protection Settings](protection.png)
##### Figure 37: Configuring TPS4800 Protection Parameters

Besides the gate driver IC, the IPTC014N10NM5 MOSFET was chosen as it has a top side cooling package. This allows the use of thermal pads to conduct the heat from the MOSFET to the top of the battery hull [6].

![MOSFET Highlighted on The New PMB](pcbmosfet.png)
##### Figure 40: MOSFET Highlighted on The New PMB

A test was conducted to compare the new MOSFET with the old MOSFET and its thermal conducting capabilities. The PMB is placed within the enclosed battery hull with starting temperature of 28 degree Celsius. A continuous current draw of 40A was carried out for 10 minutes. A thermal camera was then used to measure the temperature of the PCB.

![Thermal Image of the New PMB](newpmbthermal.jpg)
##### Figure 41: Thermal Image of the New PMB after Load Test

![Thermal Image of the Old PMB](thermaloldpmb.jpg)
##### Figure 42: Thermal Image of the Old PMB after Load Test

It can be observed that the old PMB has a higher temperature after the load test, indicating that the MOSFETs on the new PMB are better at conducting thermal heat away.

To ensure reliable power supply, a power consumption chart was drawn up to verify that the selected voltage regulators are able to supply enough power.

![PMB's Power Consumption Chart](pmbpowerconsume.png)
##### Figure 43: PMB's Power Consumption Chart

### 8.3 PCB Design for Power and Signal Integrity

#### 8.3.1 Design for High Power Handling
The PMB is designed to handle 40A of continuous current. Hence, 2oz copper was used on the outer layers of the PCB, where the power path are, to reduce temperature rise. The traces are also made as wide as possible to reduce resistance.

![3D Model of Power Path](3dpower.png)
##### Figure 38: 3D Model of Power Path

![Power Path on the Top Layer](toppower.png)
##### Figure 39: Power Path on the Top Layer

#### 8.3.2 Design for Signal Integrity
Ensuring that the signals transmitted on the data lines are not degraded by noise is critical to creating a reliable PMB.

Firstly, the board was split into high-power and low-power zones to minimise interference.

![Split between Higher and Lower Power Section of the PMB](highlowsplit.png)
##### Figure 44: Split between Higher and Lower Power Sections of the PMB (Red Line Divides the Sections)

Due to the variation in current drawn from the battery, it is likely that there would be noise if the low power components were powered from the same source. Hence, an Isolated DC-DC regulator was used to isolate the Battery and AUV power from the microcontroller's components. A low-dropout regulator (LDO) was used to step down to 3.3V for 3.3V components.

The BQ40Z50 communicates via SMBus, which spans both the high-power low-power sections. Therefore an I2C isolator is used. To protect the SMBus lines from electrostatic discharge and voltage spikes, TVS and Zener diodes are connected to the lines

The various power and ground nets are summarised in the table below:


| **Power and Ground Nets**    | **Description**                                                                        |
| :--------------------------- | :------------------------------------------------------------------------------------- |
| +3V3, +5, GND                | Isolated power and ground to power the components associated with the microcontroller. |
| Batt_Pos, Batt_Neg           | Positive and negative input from the battery.                                          |
| AUV_Pos, +3V3_UnIso, AUV_Neg | Positive and negative output to the AUV, and a 3V3 that references the AUV_Neg.        |

##### Table 22: Table of Power and Ground Nets with Its Description

This can be further seen in the division of the Power and Ground Plane within the PMB. 

![PMB Power Plane](pcbpowerplane.png)
##### Figure 45: PMB Power Plane

![PMB Ground Plane](pmbgndplane.png)
##### Figure 46: PMB Ground Plane
---

## 8. Power Monitoring
The power monitoring system is responsible for monitoring and reporting power status and power(current) consumptions in each channel. This section will detail the various features implemented to achieve this functionality.

### 8.1 Power Good Status
The Power Good (PG) status is a critical indicator of the health and stability of the power supply. It provides real-time feedback on whether the power supply is operating within acceptable parameters, allowing for proactive management of the power system.

To achieve the PG monitoring functionality, a TPS3711DDCR voltage supervisor from Texas Instruments is selected for its simplicity and reliability. The TPS3711 monitors the output voltage of the power channel and asserts the PG signal when the voltage is within the specified range.

### 8.2 Fault Reporting
As mentioned in [Section 7.1](#71-protection-requirements), the MOSFET gate driver IC TPS4800 is selected for its built-in protection features which collectively protect the vehicle from electrical fault, improving the reliability of the system. At the same time, the TPS4800 is also able to report fault status via its FAULT pin. This pin goes LOW when any of the protection features are triggered, allowing the microcontroller to log and report the fault event.

### 8.3 Power(Current) Consumption Statistics
Accurate power(current) consumption monitoring is essential for effective power management and optimization. The AMC1301DWVR, a precision isolated delta-sigma modulator from Texas Instruments, is selected for its high accuracy and isolation capabilities.

### 8.4 Fault Analysis Logics

The diagram below illustrates the fault analysis logic flow implemented in the new power distribution system.

![Fault Analysis Logic Flow](faultlogic.png)
##### Figure 32: Fault Analysis Logic Flow

### 8.5 Overall Dat Collection and Reporting

#### 8.5.1 Chosen Method
Telegram was selected as the alert platform due to its prior success and team-wide adoption. Furthermore, as it is used for internal communications, it provides a low-barrier of entry and high-visibility for any fault notification. 

### 7.3 Remote Status Monitoring
As discussed in in [Section 2.3.3](#233-challenges-with-tracking-battery-hulls-pressure-and-temperature), the team currently relies on manual logging to monitor the battery hull’s internal pressure and temperature. This lack of historical data makes it difficult to determine if a slow leak is present. Additionally, telemetry such as individual cell voltages and state of health is not consistently recorded, limiting the ability to track battery degradation over time.

To address these limitations, a remote status monitoring system was proposed. The requirements for the system and its rationale are summarised below.

| **Requirements**                     | **Rationale**                                                                                                                  |
| :----------------------------------- | :----------------------------------------------------------------------------------------------------------------------------- |
| Automated Reporting                  | Minimises human error by eliminating manual data entry.                                                                        |
| Wireless Data Upload                 | Avoids the need to unseal the hull to retrieve the data.                                                                       |
| Database with A Low-Barrier of Entry | As members from different sub-teams have to maintain the battery hulls, the storage database should be easy to access and use. |
##### Table 14: “Requirements and Rationale for Remote Status Monitoring

### 7.2.1 Design Concept 1 - Microcontroller with Wireless Capabilities
The initial design involved using a microcontroller with built-in WiFi capabilities (STM32Wx, Espressif MCUs), allowing it to connect to the internet whenever the battery hull is powered on. However, this approach is not ideal as the PMB is placed within a metal hull, which would act as a Faraday cage. This would weaken the WiFi signal leading to unreliable connections.

Given that the battery is already connected to the internet when it is attached to the AUV (Figure 28), wireless capabilities are only necessary when the battery hull is charging in the BCB. 

![Diagram of Data Flow from PMB to the Internet](pmbtointernetauv.png)
##### Figure 29: Diagram of Data Flow from PMB to the Internet

## 9. Prototyping and Testing 

### 9.1 Testing of Power Protection Features
Several key safety features were configured and tested:

| **Feature**                             | **Test Result**                                                                                                                       |
| :-------------------------------------- | :------------------------------------------------------------------------------------------------------------------------------------ |
| Overcurrent in Discharge (OCD)          | Used a load tester to verify that discharging above the set current value for the specified time would turn off the discharge MOSFET. |
| Overload in Discharge Protection (AOLD) | Almost instantaneous cut off when discharging above the set current limit.                                                            |
| Over Charging Current Protection (OCC)  | When the charging current is higher than the preset threshold, the charging MOSFET is turned off.                                     |

##### Table 21: Test Results for TPS4800 Protection Features


---

## 11. Future Project Timeline 

The following timeline outlines the proposed development plan for holiday time and the next semester. Key milestones include hardware revisions, Subsystem integration and testing phases to ensure continued reliability and performance enhancements.

![Future Project Timeline](futuretimeline.png)
##### Figure 53: Future Project Timeline

---

## References

1. Texas Instruments, “bq34110 Multi-Chemistry CEDV Battery Gas Gauge for Rarely Discharged Applications,” bq34110 datasheet, Aug. 2015 [Revised Nov. 2016]
2. “Complete Guide to Lipo Battery Voltage,” Ufine Battery [Official], https://www.ufinebattery.com/blog/useful-overview-of-lipo-battery-voltage/ (accessed Apr. 2, 2025). 
3. “LiPo vs Lithium Ion Batteries for Unmanned & Robotics Applications | Unmanned Systems Technology,” Unmanned Systems Technology, Jan. 26, 2023. https://www.unmannedsystemstechnology.com/feature/lipo-vs-lithium-ion-batteries-for-unmanned-robotics-applications/
4. “Gas Laws,” Gas laws, https://www.chem.fsu.edu/chemlab/chm1045/gas_laws.html (accessed Apr. 2, 2025). 
5. Texas Instruments, “bq40z50 Advanced Gas Gauge Circuit Design,” Application Report, Nov. 2012 [Revised Sep. 2014]
6. Infineon, "Recommendations for Board Assembly of Infineon Packages with Dual Row Gullwing Leads," Nov 2020
7. “Subconn low profile - 9 contacts,” Underwater Technology, https://www.macartney.com/connectivity/subconn/subconn-low-profile-series/subconn-low-profile-9-contacts/ (accessed Apr. 2, 2025). 
8. A. Fink et al., "Design, Implementation, and Strategy of the Polaris and Sirius AUVs," Cornell Univ. Autonomous Underwater Vehicles, Tech. Rep., Jul. 2024. [Online]. Available: https://robonation.org/app/uploads/sites/4/2024/07/RS24_TDR_Cornell-compressed.pdf
9. [1] N. Becker, A. Dellacqua, B. Knutson, M. Oinonen, R. Pafford, and C. Tucker, "Design Review of Talos: An Autonomous Underwater Vehicle by The Ohio State University’s Underwater Robotics Team," The Ohio State Univ., Tech. Rep., Jun. 2023. [Online]. Available: https://robonation.org/app/uploads/sites/4/2023/06/TDR_THEOhioStateUniversity_RS2023-compressed.pdf
10. Texas Instruments, “Battery Gauging Algorithm Comparison,” Application Report, Dec. 2023
11. Texas Instruments, “Achieving The Successful Learning Cycle,” Application Report, Jul. 2018

---

## Appendix A: PCB Schematics
+ [Power Monitoring Board Schematic](PMB4.5-2Schematics.pdf)
+ [Battery Telemetry Board Schematic](btpschematic.pdf)

## Appendix B: Individual Layers of Power Monitoring Board

![PMB Top Layer](pmbtoponly.png)
##### Top Layer of PMB

![PMB Power Plane](pmbpwronly.png)
##### Power Plane of PMB

![PMB Ground Plane](pmbgndonly.png)
##### Ground Plane of PMB

![PMB Bottom Layer](pmbbottomonly.png)
##### Bottom Layer of PMB

## Appendix C: Relay Circuit Calculation

![Relay Circuit Calculation](relaycircuitcalc.png)
##### Relay Circuit Calculation

## Appendix D: Battery Specification
+ [AUV4.1 LiPo Battery](lipobatt.pdf)
+ [AUV4.5 Li-Ion Battery](liionbatt.pdf)

## Appendix E: 3D Model of AUV4.5 Power Monitoring Board

<div style="display: flex; justify-content: center;">
  <div class="sketchfab-embed-wrapper" style="width: 100%; max-width: 900px;">
    <iframe title="AUV4.5 Power Monitoring Board 3D Model"
            frameborder="0"
            allowfullscreen
            mozallowfullscreen="true"
            webkitallowfullscreen="true"
            allow="autoplay; fullscreen; xr-spatial-tracking"
            xr-spatial-tracking
            execution-while-out-of-viewport
            execution-while-not-rendered
            web-share
            style="width: 100%; height: 480px;"
            src="https://sketchfab.com/models/1ba9f9a1e7d0487896ffd8acb5602e95/embed">
    </iframe>
    <p style="font-size: 13px; font-weight: normal; margin: 5px; color: #4A4A4A; text-align: center;">
      <a href="https://sketchfab.com/3d-models/step-no-variations-for-auv4-5-2-pmb-pcbdoc-1ba9f9a1e7d0487896ffd8acb5602e95?utm_medium=embed&utm_campaign=share-popup&utm_content=1ba9f9a1e7d0487896ffd8acb5602e95"
         target="_blank"
         rel="nofollow"
         style="font-weight: bold; color:black;">
        AUV4.5 Power Management Board 3D Model
      </a>
    </p>
  </div>
</div>