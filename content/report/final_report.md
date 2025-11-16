---
title: "Development of a Compact PDS for Unmanned Surface Vehicle (USV)" 
date: 2025-11-14
lastmod: 2025-11-16
author: ["Chen Jiawei"]
description: "This report documents the work done on developing a compact PDS for ST Engineering's Unmanned Surface Vehicle (USV)."
summary: "This report documents the work done on developing a compact PDS for ST Engineering's Unmanned Surface Vehicle (USV)."
editPost:
    URL: "https://www.stengg.com/"
    Text: "ST Engineering Company Website"
showToc: true
disableAnchoredHeadings: false
---

## Acknowledgements

Firstly, I would like to thank ST Engineering for giving me the opportunity to work on this project. This project would not have been possible without the support of many dedicated ST Engineering members. I am especially grateful to Ang Ming Xiang, my ST Engineering supervisor and Nathanel Tan, the Head of ST engineering Unmaned & Integrated System Department for providing the guidance and technical input for this project.

I also wish to acknowledge the support provided by the NUS College of Engineering, particularly Mr Royston, and Mr Graham from the Engineering Design and Innovation Centre. I would also like to thank Mr Eugene Ee for taking the time to review my project and provide valuable advice.

----
## List of Common Acronyms

<div align="center">

| **Acronym** |        **Definition**         |
| :---------: | :---------------------------: |
|   **USV**   |    Unmanned Surface Vessel    |
|   **PDS**   |    Power Distribution System     |
|   **PCB**   |     Printed Circuit Board     |
|   **PLC**   |    Programmable Logic Controller   |
|   **MCU**   |    Microcontroller   |
|   **DC**   |    Direct Current    |
|   **MTBF**   |    Mean Time Before Failure    |
|   **MTTR**   |    Mean Time To Repair    |
|   **MOSFET**   |      Metal-Oxide-Semiconductor Field-Effect Transistor     |
|   **PG**   |    Power Good     |
|   **CAN**   |    Controller Area Network    |

</div>

---

## 1. Summary

This project focuses on developing a compact Power Distribution System (PDS) for ST Engineering's Unmanned Surface Vehicle. The PDS is a critical component of the vehicle’s electrical system, designed to distribute and control the power to different parts of the vehicle. 

The new PDS developed mainly consists of a compact and robust power switching printed circuit board (PCB) solution with a backplane system for the ease of modularity and integration. The system also includes key features such as power line protection and accurate power status monitoring and reporting, to ensure its functionality even after a power line fault has occured.

---

## 2. Background

### 2.1 Introduction
**Unmanned Surface Vehicles (USVs)** are boats or ships that operate on the water surface without an onboard crew. In recent years, the USV market has grown rapidly, particularly within the Asia-Pacific region.

USVs are commonly classified by size, with three main categories used in the maritime industry. Among these, medium-sized USVs—typically 2 to 24 meters in length—are the target vehicle of this project.

Within the overall USV market, more than half of all vessels are developed for defence applications. Most of these defence-oriented USVs weigh under 2,000 kg, placing them within the small or medium-size categories.

![USV Market Size and Distribution](USV_Market_1.png)
##### Figure 1: USV Market Size and Distribution

To enable autonomous operation, USVs rely on a suite of sensors and onboard equipment usually powered by engines or batteries. These power sources supply energy through an integrated Power Distribution System — the central focus of this project.

![Common USV On-board Devices](USV_Market_2.png)
##### Figure 2: Common USV On-board Devices

### 2.2 Existing Solutions
Most USVs today still adopt PDS design similar to those used in conventional manned vessels. These systems typically rely on traditional marine electrical architectures that were not specifically designed for autonomous or highly integrated operations.

Common components found in such PDS setups include transformers, DC converters, Programmable Logic Controllers (PLCs), relays, fuses, and circuit breakers. These components are interconnected using cables, terminal blocks, and wiring harnesses to form the overall electrical network.

![Conventional PDS Architecture](conventional.png)
##### Figure 3: Conventional Marine Direct Current (DC) PDS Architecture

## 3. Problem Analysis    
To better understand the challenges that may arise when conventional power distribution systems (PDS) are applied to medium-sized USVs, I conducted an analysis of two representative case studies. The first is a literature review of Onboard DC Grid™, a marine power system developed by ABB, one of the leading power system providers in the maritime industry. The second is a real-world examination of the PDS used in ST Engineering’s medium-sized USVs. 

### 3.1 Onboard DC Grid&trade;
Onboard DC Grid™ is an advanced power distribution system designed to manage the generation, storage, and distribution of direct current (DC) power across onboard applications.

In 2020, ABB has published the report, _Unmanned Surface Vehicles/Vessel (USV) 
Reliable Power and Propulsion Architecture Characterization_, in response for a Request for Information (RFI) from the US government. In the report, the company introduce this product and highlight some problems on the current USV power architecture 

The primary concern identified in this report regarding the current power distribution solutions used in USVs is their negative impact on mission success rates. Although USVs use many of the same power subsystem components as conventional manned vessels, these components exhibit the same Mean Time Between Failures (MTBF) but a much higher Mean Time To Repair (MTTR). This difference arises because, unlike manned vessels, faults that occur during a USV’s mission cannot be immediately detected, diagnosed, or repaired due to the absence of onboard crew.

While initial faults may not be mission-critical, they can propagate into secondary failures affecting systems essential for the vehicle's operation. Consequently, the overall effective MTBF of the USV system becomes shorter than that of a conventional vessel, resulting in a higher likelihood of mission failure.

![USV Power System Reliability Comparison](usvpower.png)
##### Figure 4: USV Power System Reliability Comparison with Conventional Manned Vessel

### 3.2 ST Engineering USV PDS

In this project, I had the opportunity to work directly with ST Engineering’s USVs and examine their PDS in a real operational setting.

![ST Engineering USV PDS Architecture](stpds.png)
##### Figure 5: ST Engineering's USV Current PDS Architecture

The current system conists primarily of commercial fuses and relays, coordinated through a dedicated power-system PLC. Power channel switching is controlled by continuous digital signals from the PLC, which govern when individual subsystems are energised or disconnected. This switching capability enables the sequential start-up of the main compute stacks during vessel initialization, as well as the selective shutdown of non-essential devices to improve power efficiency during missions.

Two main problems exists in the current system:

**Size Constraint**:
Currently, the PDS is housed within the equipment racks of the USV. However, due to the bulky nature of the conventional power distribution components, the system occupies a significant portion of the rack's internal volume. This oversizing poses challenges during integration, as it limits the available space for other essential components and makes maintenance tasks more cumbersome. The oversized system also complicates cable management within the rack, leading to potential issues with accessibility.

Here are the dimension statistics of the current PDS used in ST Engineering USV and a estimation of the equipment rack space it occupies:

| **PDS Sections** | **Length (mm)** | **Width (mm)** | **Height (mm)** | **Equipment Rack Space Occupied (%)** |
| :----------: | :------------: | :----------: | :----------: | :----------: |
|   Auxilary Power Box      |      750       |     570      |    150      |    10     |
|   Main Power Distribution Unit     |      890       |     1200      |    266      |   15     |
##### Table 1: Current PDS Size Statistics

What is more, ST Engineering is designing USVs for 3 different sizes with the following dimension statistics:

| **USV Model Name** | **Length (m)** | **Width (m)** |
| :----------: | :------------: | :----------: |
|   Goldfish      |      10       |     2.5      |
|   Bellagio     |      15        |     4     |
|   Puma         |      17.5        |     5.2      |
##### Table 2: ST Engineering's USV Size Statistics

With the current PDS being already oversized in medium size vehicle Puma and Bellagio, it is foreseeable that the system will be even more ill-suited for the smaller USV models like Goldfish. Therefore, there is a pressing need to redesign the PDS to be more compact and efficient, ensuring it can fit within the constraints of all USV models while still delivering reliable performance.

**Existance of Single Pont of Failure**:
The current PDS lacks both redundancy and fault-tolerance, making it highly susceptible to single points of failure.

For instance, if the PLC of PDS fails, the consequences can be severe. Because the system’s control logic requires each power channel to remain continuously energised by a digital HIGH signal from the PLC, the loss of this signal immediately de-energises all PLC-controlled relays. This results in a complete shutdown of all subsystems powered through these channels. Such a failure mode presents a significant operational risk to the USV and may even lead to the total loss of the vessel while at sea. 

**Lack of power status indications**:
ST Engineering’s USVs currently operate under the principle that if a fault is not classified as critical, the vehicle will continue its mission. However, the existing PDS lacks adequate power-status monitoring and reporting capabilities. This limitation makes it difficult to assess the health and performance of the power distribution system in real time and to detect early signs of degradation or malfunction. As a result, non-critical issues may go unnoticed and remain unisolated from the main power network, allowing them to propagate into critical failures that ultimately reduce the overall mission success rate.

---

## 4. Design Statement
Targeting the above identified problems, the design statement of this project are summarised as:

<div align="center">
    <b>
      Design a PDS, to reduce the size of the current medium USV power system while increase vehicle mission success rate by improving its fault tolerance and power system monitoring
    </b>
</div>

## 4. Value Proposition

### 4.1 Stakeholders
The first group of stakeholders in this project are the members of the ST Engineering USV Team, who will directly involve in the design, integration, and testing of the new USV. Their primary task is to ensure that the new platform meets all technical and operational requirements set by users.

The second group of stakeholders are the end-users of the USVs, such as maritime security agencies, port authorities, and research institutions. These organisations deploy the vehicles for operational tasks and are also responsible for performing maintenance and repair activities when faults occur.

### 4.2 Benefits
The new PDS offers several key benefits to its stakeholders::

| **Benefits**                                      |                  **Rationale**                   |
| :------------------------------------- | :----------------------------------------------: |
| Compact Design                        |  **To ST Engineering USV Team** - A smaller PDS footprint allows more efficient use of space within the USV’s equipment racks. This increases design flexibility and scalability across different USV sizes and configurations.  |
| Enhanced Fault Tolerance              | **To USV Users** - A more robust PDS reduces the impact of component failures, improving overall system reliability and increasing mission success rates. |
| Advanced Power Monitoring and Reporting | **To USV Users** - Real-time power-status insights support early detection of abnormal conditions. This enables proactive maintenance, prevents minor issues from escalating into critical faults, and reduces repair costs and downtime. |

##### Table 3: Key Benefits of the New PDS to Stakeholders

---

## 5. Design Requirments

### 5.1 Design Standards
To ensure the new PDS meets industry best practices and regulatory requirements, the following design standards were adopted:
*IEEE Recommended Practice for the Design and Application of Power Electronics in Electrical Power Systems*
(IEEE Std 1709-2010) [4]. This standard provides comprehensive guidelines for designing power electronic systems in maritime applications, covering aspects such as electrical safety, electromagnetic compatibility, thermal management, and environmental considerations.

### 5.2 Technical Specifications
To begin, the new PDS must match or exceed the technical performance of the existing system. Based on an evaluation of the current PDS capabilities as well as suggestions given by the ST USV engineering team, the following technical requirements were identified:

| **Technical Capabilities** | **Specifications**                                                                |
| :------------------------- | :-------------------------------------------------------------------------------- |
| Physical Dimension         |  < 445mm x 600mm x 133mm                                                                              |
| Application Voltage             | 12V and 24V DC                                                               |
| Maximum Continuous Current        | 20A                                                                               |
| Maximum Transient Current     | 30A                                                                            |
| Fault Protection     | Overvoltage/Undervoltage/Overcurrent/Short Circuit                                                                            |
| Fault Reponse Time     |  <10ms                                                                          |                                                                           |
| Power System Monitoring                  | Current, Internal Temperature, Power Good(PG), Fault Status |
| Communication Protocol     | Digital/Analog/CAN 2.0      |

##### Table 4: Core Technical Requirements for the New PDS

The 30 A transient current specification is based on the maximum transient current of the existing PDS — 24 A, as measured during the operation of the searchlight according to its datasheet — augmented with a 50% design margin. This additional margin ensures sufficient headroom to handle transient overloads without compromising system reliability.

A power consumption chart was also drawn up to verify that the above technical specifications are able to supply enough power which will be attached in the Appendix section.


### 5.3 Functional Sub-goals
In addition to meeting the technical specifications, the new PDS must achieve three key functionalities to satisfy user requirements. Each of these is described in detail in the corresponding section below.

| **Key Functionalities**                          |                  **Section Number**                   |
| :------------------------------------- | :---------------------------------------------------: |
| Compact and robust power-switching solutions for each channel | [Section 6](#6-Power-Switching) |
| Integrated power-line protection for transient and fault conditions |   [Section 7](#7-Power-Protection)    |
| Real-time monitoring and reporting of power status and current consumption for each channel |       [Section 8](#8-Power-Monitoring)     |
##### Table 5: PDS System Functionalities and the Corresponding Report Sections

### 5.4 Environmental Requirments

Since this product is intended for use in maritime environments, the following environmental parameters were selected from the design standrad mentioned above. These parameters represent the most relevant constraints for this project.

| **Parameters**     | **Constraint**                         |
|------------------------|-----------------------------------------|
| Ambient Temperature    | ≤ 50°C                                  |
| Vibration              | ≥ 22 Hz                                 |
| Humidity               | Approximately 80%                       |

##### Table 6: Environmental Design Constraints for Backward Compatibility

---  

## 5. System Overview

This section presents the summarised architectures to provide a high-level overview of the systems. Subsequent sections will explain how the design choices support the overall project goals.

![Summarised Power Architecture of PDS](powerarch.png)
##### Figure 6: Summarised System Architecture of the developed PDS

---

## 6. Power Switching 
The new PDS is designed to provide compact and robust power switching solutions for each power channel. And this is achieved through two main improvements, moving from traditional relay + PLC combination towards PCB backplane system as well as improving the power switching logic.

### 6.1 Moving towards PCB 

#### 6.1.1 PLC + Relay vs MCU + MOSFET PCB System

As mentioned in [Section 3.2](#32-st-engineering-usv-pds), the current PDS adapted in ST Engineering USV consists of a combination of a Programmable Logic Controller (PLC) and Solid State Relays to achieve power switching. This is also the common approach used in conventioanl PDS in marine industry. Another possibl approach is to use a MCU + MOSFET PCB system, which involves a substantial amount of customisation and design efforts.

The below table summarises the key advantages and disadvntages between the two approaches:

| **Aspect**               | **PLC + Relay**                                                | **MCU + PCB System**                                                                                                                                   |
| ------------------------ | -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Size and Weight          | - Bulky and heavy due to discrete components<br>- Requires additional space for wiring and terminal blocks<br> | - Compact and lightweight due to integrated design<br>- Reduces wiring complexity and space requirements<br>                                           |
| Reliability and Durability | - Certified for maritime usage<br> - proper insulation and protection done based on industrial standards<br>   | - Larger efforts are required to design for robustness
| Customisability and Scalability | - Limited customisation <br>- Easily scalable by adding or modifying Relay/PLC modules<br> | - Highly customisable to specific requirements<br>- More difficult to replace/scale up                                           |

##### Table 7: Comparison Between PLC + Relay and MCU + MOSFET PCB System

#### 6.1.2 Targeting limitations in MCU + MOSFET PCB System
While the MCU + MOSFET PCB system offers significant advantages in achieving size reduction, it also presents the above mentioned limitations that need to be addressed to ensure successful implementation. As such, the following design improvements were made in this project to mitigate these limitations:

* **Customisability and Scalability:** To address the challenges of customisability and scalability, a backplane system architecture was adopted where MCU + MOSFET PCBs will be in the form of cards and only connectors and copper traces exists on the base backplane. This modular design allows for easy replacement and upgrading of individual PCB modules, enabling users to tailor the PDS to their specific needs without requiring a complete redesign.

* **Reliability and Durability:** To improve the reliability and durability, PLC will still be used as the primary source of switching while MCU will be used as a redundancy and for monitoring data collections. This hybrid approach leverages the strengths of both PLCs and MCUs, ensuring robust performance while maintaining the compactness of the PCB design.

![New Switching Signal Flow](SSF.png)
##### Figure 7: Switching Signal Flow in the PDS

### 6.2 Customisable Power Switching Logic
As mentioned in [Section 3.2](#32-st-engineering-usv-pds), the current control logic of the ST Engineering USV PDS relies on a continuous signal from the PLC, which creates a risk of power-line disconnection in the event of a PLC failure or loose connection. In this project, I would like to introduce a new user-customisable control logic using a latching PCB design to mitigate this risk.

#### 6.2.1 Comparison Between New and Old Control Logic
The diagrams below illustrate the current control logic flow and the proposed new control logic. 

![Current Control Logic](CCL.png)
##### Figure 8: Current Control Logic in the PDS

![New Control Logic](NCL.png)
##### Figure 9: New Control Logic proposed

The key difference between the two control logics lies in how the power channel’s ON state is maintained. In the current system, the ON state is sustained by a continuous digital HIGH signal from the PLC. In contrast, the new control logic employs a latching mechanism: a momentary HIGH signal from the MCU toggles the power channel ON at startup, and the channel is only turned OFF when a subsequent continuous HIGH signal is applied. This design ensures that once a power channel is turned ON, it remains ON even if the MCU signal is lost. This significantly enhances fault tolerance, as transient or permanant PLC/MCU failures will not inadvertently disrupt power delivery to critical subsystems during missions.

#### 6.2.2 User-customisability with latching PCB Design
Although the latching logic enhances fault tolerance, it may introduce certain operational limitations. For example, if the MCU fails while a power channel is ON, the user cannot remotely turn off that channel, even for systems that are not required during mission operation (e.g., onboard lights used only for maintenance), which could reduce overall power efficiency. 

To address this, a separate PCB was designed to implement the latching mechanism while remaining pluggable from the main MOSFET board. This modular design makes the control logic user-customisable, allowing operators to choose between the new latching mechanism or revert to the traditional continuous-signal control logic according to their operational requirements.

![Latching PCB](latching_pcb.png)
##### Figure 10: Latch PCB Schematic and Layout

![MOSFET_Latching_PCB Combination ](integration.png)
##### Figure 11: 3D model of the MOSFET Board with Latch PCB Integrated

---

## 7. Power Protection

Power protection is crucial in ensuring the safety and reliability of the PDS. Current PDS in ST Engineering USV lacks adequate protection features, making it vulnerable to transient and fault situations. 

### 7.1 Protection Requirements
The types of faults that the new PDS should be able to protect against are identified from the design standards outlined in [Section 5.1](#51-design-standards)
. These include overvoltage, undervoltage, overcurrent, and short-circuit faults.

#### 7.2 Choice of MOSFET Gate Driver IC - TPS4800
**MOSFET gate driver** is an electronic device designed to efficiently control the gate terminal of a MOSFET, enabling rapid switching between its ON and OFF states. 

In this project, the MOSFET gate driver IC TPS4800 from Texas Instruments is selected among all other MOSFET gate driver IC for its ability to achieve all the above protection features while satisfying the technical specifications mentioned in [Section 5.1](#51-technical-specifications). The key features of the TPS4800 are summarised in the appendix section.

---

## 8. Power Monitoring
The power monitoring system is responsible for monitoring and reporting power status and power(current) consumptions in each channel. This section will detail the various features implemented to achieve this functionality.

### 8.1 Power Good Status
The Power Good (PG) status is a critical indicator of the health and stability of the power supply. It provides real-time feedback on whether the power supply is operating within acceptable parameters.

To achieve the PG monitoring functionality, a TPS3711DDCR voltage supervisor from Texas Instruments is selected for its simplicity and reliability. The TPS3711 monitors the output voltage of the power channel and asserts the PG signal when the voltage is within the specified range.

### 8.2 Fault Reporting
As mentioned in [Section 7.1](#71-protection-requirements), the MOSFET gate driver IC TPS4800 is selected for its built-in protection features. At the same time, the TPS4800 is also able to report fault status via its FAULT pins. These pins goes LOW when any of the protection features are triggered, allowing the MCU to log and report the fault event.

### 8.3 Power(Current) Consumption Statistics
Accurate power(current) consumption monitoring is essential in this project to identify abnormal power situation in each channel. The AMC1301DWVR, a precision isolated delta-sigma modulator from Texas Instruments, is selected for its high accuracy and isolation capabilities.

### 8.4 Fault Analysis Logics

The diagram below illustrates the fault analysis logic flow implemented in the new PDS. With this logic, the system can differentiate between critical and non-critical faults for the vehicle's operation and respond accordingly.

![Fault Analysis Logic Flow](faultlogic.png)
##### Figure 12: Fault Analysis Logic Flow

### 8.5 Overall Data Collection and Reporting

#### 8.5.1 Digital/Analog from MOSFET PCBs to MCU
The MOSFET PCB with all the above mentioned devices will output a combination of digital and analog signals to communicate power status and consumption data to MCU. The digital signals include the Power Good (PG) status and fault status, while the analog signals represent the current consumption data.

#### 8.5.2 CAN Bus from MCU to PLC 
The Controller Area Network (CAN) bus is employed for communication between the MCU on the Backplane and the power PLC of the USV. CAN bus is chosen for its robustness, reliability, and ability to handle high-speed data transmission in noisy environments, making it ideal for maritime applications. This also reduce the wiring complexity between the PDS and the USV main computer stack as only two wires are required for CAN communication.

## 9. Prototyping and Testing 

Prototypes developed before the submission of this report are provided in the appendix section below.

Testing will first be carries out with the MOSFET PCB standalone using power supply and a electronic load tester. Here are some of the features that will be tested and recorded:

![Continous Current Test](CCT.png)
##### Figure 13: Continous Current Test

![Fault Protection Test](FPT.png)
##### Figure 14: Fault Protection Test 

After the standalone testing, the MOSFET PCB will replace one of the existing relay modules in the current ST Engineering USV PDS for overnight integration testing. 

---

## 11. Future Project Timeline 

The following timeline outlines the proposed development plan for holiday time and the next semester. Key milestones include hardware revisions, Subsystem integration and on-boat testing phases to ensure continued reliability and performance enhancements.

![Future Project Timeline](futuretimeline.png)
##### Figure 13: Future Project Timeline

---

## References

1. Abraham Sachin, "Marine Electrical Distribution," 22 June 2018. [Online] Avaliable: teckhmarine.blogspot.com/2018/06/marine-electrical-distribution.html.
2. ABB, "Unmanned Surface Vehicles/Vessel (USV) Reliable Power and Propulsion Architecture Characterization," 2020. [Online]. Available: https://new.abb.com/docs/librariesprovider15/gov/usv-abb-white-paper-20200830.pdf?sfvrsn=6369e809_2
3. IEEE Std 1709-2010, "IEEE Recommended Practice for the Design and Application of Power Electronics in Electrical Power Systems," pp.1-50, 2010.
4. Texas Instruments, "TPS4800-Q1 High-Side and Low-Side N-Channel MOSFET Driver with Integrated Protection Features," [Online]. Available: https://www.ti.com/product/TPS4800-Q1
5. Texas Instruments, "TPS3711 Voltage Supervisor with Power-Good Output," [Online]. Available: https://www.ti.com/product/TPS3711
6. Texas Instruments, "AMC1301 Isolated Delta-Sigma Modulator for Current Sensing," [Online]. Available: https://www.ti.com/product/AMC1301

---

## Appendix A: TPS4800 Key Features
| **Key Features**                | **Specifications**                                                                 |
| :------------------------------ | :-------------------------------------------------------------------------------- |
| Operating Voltage               | 8V to 60V DC                                                                      |
| Overvoltage Protection Threshold | Adjustable between 10V to 60V DC                                                  |
| Undervoltage Protection Threshold | Adjustable between 6V to 54V DC                                                   |
| Overcurrent Protection Threshold | Adjustable between 5A to 50A                                                      |
| Overcurrent Protection Response Time | <10ms (adjustable)                                                                          |
| Short-Circuit Protection Response Time | <1µs                                                                           |
##### Key Features of TPS4800 MOSFET Gate Driver IC

## Appendix B: MOSFET and Latch PCB Schematics
+ [MOSFET PCB Schematics]
+ [Latch PCB Schematics]

## Appendix C: MOSFET and Latch PCB Layouts
+ [MOSFET PCB Layouts] 
+ [Latch PCB Layouts]

## Appendix D: Latch PCB Simulation
![Latching PCB Simulation](latchsim.png)  
##### Latch PCB Simulation Results

## Appendix D: Power Consumption Chart
![Power Consumption Chart](powerchart.png)  
##### Power Consumption Chart of the USV DC Systems