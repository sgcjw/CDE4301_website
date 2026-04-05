---
title: "Development of a Compact Power Distribution System (PDS) for Unmanned Surface Vehicle (USV)" 
date: 2026-03-29
lastmod: 2026-03-29
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

Firstly, I would like to thank ST Engineering for giving me the opportunity to work on this project. This project would not have been possible without the support of many dedicated ST Engineering members. I am especially grateful to Ang Ming Xiang and Teo Xuen, my ST Engineering supervisors and Nathanel Tan, the Head of ST engineering Unmaned & Integrated System Department for providing the guidance and technical input for this project.

I also wish to acknowledge the support provided by the NUS College of Engineering, particularly Mr Royston, and Mr Graham from the Engineering Design and Innovation Centre. I would also like to thank Mr Eugene Ee for taking the time to review my project and provide valuable advices.

## List of Common Acronyms

<div align="center">

| **Acronym** |        **Definition**         |
| :---------: | :---------------------------: |
|   **USV**   |    Unmanned Surface Vessel    |
|   **PDS**   |    Power Distribution System     |
|   **PCB**   |     Printed Circuit Board     |
|   **PLC**   |    Programmable Logic Controller   |
|   **SSR**   |    Solid State Relay    |
|   **MCU**   |    Microcontroller   |
|   **DC**   |    Direct Current    |
|   **MTBF**   |    Mean Time Before Failure    |
|   **MTTR**   |    Mean Time To Repair    |
|   **MOSFET**   |      Metal-Oxide-Semiconductor Field-Effect Transistor     |
|   **TI**   |    Texas Instruments     |   
|   **PG**   |    Power Good     |
|   **IC**   |    Integrated Circuit     |
|  **GPIO**   |    General Purpose Input/Output     |
|  **ADC**   |    Analog to Digital Converter     |
|   **I2C**   |    Inter-Integrated Circuit     |
|   **CAN**   |    Controller Area Network    |

</div>


## 1. Abstract

This project focuses on developing a compact Power Distribution System (PDS) for ST Engineering's Unmanned Surface Vehicle. The PDS is a critical component of the vehicle’s electrical system, designed to distribute and control the power to different parts of the vehicle. 

The new PDS developed mainly consists of serveral compact and robust printed circuit board (PCB) solutions as well as the firmware associated with them. The solutions includes key features such as power line switching, protection and accurate power status monitoring and reporting, to ensure its functionality even after a power line fault has occured.

## 2. Background

### 2.1 Introduction

**For a more detailed introduction to the background of this project, please refer to the interim report. Below is a brief summary of the key points:*

- **Unmanned Surface Vehicles (USVs)** are boats or ships that operate on the water surface without an onboard crew.

- **Medium-sized USVs**, typically 2 to 24 meters in length, are the target vehicle of this project.

- These USV's **Power Distribution System (PDS)** is the central focus of this project.

### 2.2 Existing Solutions
Most USVs today still adopt PDS designs similar to those used in conventional manned vessels. Common components found in such PDS setups include transformers, DC converters, Programmable Logic Controllers (PLCs), Relays Module, Fuses, and Circuit Breakers. These components are interconnected using cables, terminal blocks, and wiring harnesses to form the overall electrical network.

![Conventional PDS Architecture](conventional.png)
##### Figure 3: Conventional Marinetime Direct Current (DC) PDS Architecture

## 3. Literature Review  
As mentioned above, conventional USV PDS usually follow a similar design as those in conventional manned vessels. To better understand how this approach has performed in medium-sized USVs, analysis on two representative case studies will be discussed in this project. The first is a literature review of Onboard DC Grid™, a marinetime power system developed by ABB, one of the leading power system providers in the maritime industry. The second is a real-world examination of the PDS currently used in ST Engineering’s medium-sized USVs. 

**Please refer to the interim report for the detailed literature review of the above mentioned case studys. Below is a brief summary of the existing problems identified from the literature review:*

- **Lower Autonomous Mission Success Rate**: The components in the PDS of manned vehicles are designed to work with manual maintenance and repairment, which makes them unsuitable for autonomous operations. This results in them having a smaller mean time between failures (MTBF), which can significantly disrupt the USV's operations and reduce its mission success rates.

- **Size Constraint**: The bulky design of the current USV PDS components (e.g. Relay Modules, PLCs) reduces the onboard space available for other essential components used in unmanned operations such as sensors and servers. They also make maintenance tasks more cumbersome.

- **Existence of Single Point of Failure**: Using ST Engineering’s USV Power architecture as an example, the loss of PLC signal will immediately de-energises all relays in its PDS, cutting power to the entire boat and hence presenting a significant operational risk to the USV.

- **Lack of power line monitoring and reporting**: Due to the lack of real-time power consumption monitoring and fault reporting capabilities, early signs of degradation or minor malfunctions can easily be neglected and gradually escalate, eventually developing into critical failures that threaten the safety and mission success of the USV.


## 4. Design Statement
Targeting the above identified problems, the design statement of this project are summarised as:

<div align="center">
    <b>
      Design a Power Distribution System, to reduce the size of the current ST Engineering USV power system while increasing the vehicle's mission success rate by improving its fault tolerance and power system monitoring
    </b>
</div>

## 5. Value Proposition

**For a detailed discussion on the value proposition of this project, please refer to the interim report. Below is a brief summary of the key points.*

The proposed new PDS of this project will offer several key benefits to its stakeholders::

| **Benefits**                                      |                  **Rationale**                   |
| :------------------------------------- | :----------------------------------------------: |
| **Compact Design**                        |  A smaller PDS footprint allows more efficient use of space within the USV’s equipment racks. This increases design flexibility and scalability across different USV sizes and configurations.  |
| **Enhanced Fault Tolerance**              | A more robust PDS reduces the impact of component failures, improving overall system reliability and increasing mission success rates. |
| **Advanced Power Monitoring and Reporting** | Real-time power-status insights   support early detection of abnormal conditions. This enables proactive maintenance, prevents minor issues from escalating into critical faults, and reduces repair costs and downtime. |

##### Table 3: Key Benefits of the Proposed PDS to Stakeholders

## 6. Design Requirements

### 6.1 Design Standards
To ensure the new PDS meets industry best practices and regulatory requirements, the following design standards were referenced in the design process of this project:

*IEEE Recommended Practice for the Design and Application of Power Electronics in Electrical Power Systems*
(IEEE Std 1709-2010) [4].

This standard provides comprehensive guidelines for designing power electronic systems in maritime applications, covering aspects such as electrical safety, electromagnetic compatibility, thermal management, and environmental considerations.

### 6.2 Technical Specifications
As a starting point, the new PDS must at least match the technical performance of the existing system. Based on an evaluation of the current PDS capabilities as well as suggestions given by the ST USV engineering team, the following technical requirements were identified:

| **Technical Capabilities** | **Specifications**                                                                |
| :------------------------- | :-------------------------------------------------------------------------------- |
| Physical Dimension         |  < 445mm x 600mm x 133mm                                                                              |
| Number of Channels | 26
| Application Voltage             | 12V and 24V DC                                                               |
| Maximum Continuous Current  per channel      | 20A                                                                               |
| Maximum Transient Current   per channel  | 30A                                                                            |
| Fault Protection     | Overvoltage/Undervoltage/Overcurrent                                                                            |
| Power System Monitoring                  | Power Consumption, Power Good(PG), Fault Status |
| Communication Protocol     | Digital/I2C/CAN 2.0      |

##### Table 4: Core Technical Requirements for the New PDS

The rationale for choosing these technical specifications will be discussed in the corresponding sections below.

### 6.3 Functional Sub-goals
In addition to meeting the technical specifications, the new PDS must achieve three key functionalities to satisfy user requirements.

| **Key Functionalities**                          |                  **Section Number**                   |
| :------------------------------------- | :---------------------------------------------------: |
| Compact and robust power-switching solutions for each channel | [Section 8.1](#81-Power-Switching) |
| Integrated power-line protection for transient and fault conditions |   [Section 8.2](#82-Power-Protection)    |
| Real-time monitoring and reporting of power status and current consumption for each channel |       [Section 8.3](#83-Power-Monitoring)     |
##### Table 5: New PDS System Functionalities and the Corresponding Report Sections

### 6.4 Environmental Conditions

Since this product is intended for use in maritime environments, the following environmental parameters were identified from the design standard mentioned above and will be referenced in the design and testing of the new PDS. 

| **Parameters**     | **Conditions**                         |
|------------------------|-----------------------------------------|
| Ambient Temperature    | ≤ 50°C                                  |
| Vibration frequency    | ≥ 22 Hz                                 |
| Humidity               | Approximately 80%                       |

##### Table 6: Operational Conditions for the New PDS

### 6.5 Performance Criteria

<!--[Define the measurable targets the solution must achieve. Be precise about target values and measurement methods -- these will be assessed directly in Chapter 5.]-->

The following performance criteria are defined to evaluate the new PDS against the technical specifications and functional sub-goals outlined above. These criteria will be directly assessed during the prototyping and testing phases of the project.

| Type   | Performance Criterion | Target Value | Measurement Method     |
|------|-----------------------|--------------|-------------------------|
| Power Distribution Stability | Ability to maintain stable power supply under varying load conditions | Uninterrupted continuous power supply of 20A, voltage ripple < 100mV | Supply 20A current through all channels for 30 minutes and measure the voltage ripple |
| Power Switching Capability |         Ability to response to power channel control signal (ON/OFF) from the vehicle's control system              |  Correct switching behaviour; Response time < 1ms            |          Conduct repeated switching tests under various load conditions and record the results               |
| Power Monitoring Accuracy |    |  Details in [Section 10.3](#103-power-consumption-statistics)  |
| Power Protection Effectiveness |     Ability to effectively protect the power lines from transient fault conditions; Ability to identify the type of fault (e.g., overcurrent, short circuit)                  | Correct fault type identification; Protection trigger time < 1ms             |           Stimulate various fault conditions (Undervoltage, Overvoltage, Overcurrent) using electronic loads and record the results              |

##### Table 7: Performance Criteria for Evaluating the New PDS

## 7. System Overview

The proposed new PDS consists of three main subsystems of PCBs: the Relay PCB system, the MCU PCB, and the Power Backplane PCB. Each subsystem is designed to address specific functional requirements while ensuring seamless integration with the overall system architecture.

![Summarised Power Architecture of PDS](powerarch.png)
##### Figure 6: Summarised System Architecture of the developed PDS

## 8. Relay PCB System
The Relay PCB system is the core of the proposed PDS. It consists of 26 individual relay PCBs, each controls and monitors a single DC power channel. This section of the report will introduce the design of the this PCB system based on its contribution to the three key functionalities mentioned in [Section 6.3](#63-functional-sub-goals)

### 8.1. Power Switching 

One important feature of the relay PCB is to provide compact and robust power switching control for each power channel. This is achieved through two main solutions: **Moving from PLC and relay module system to relay PCB backplane system** & **Modifying the existing power switching logic**.

#### 8.1.1 Moving towards PCBs 

As mentioned in [Section 3.2](#32-st-engineering-usv-pds), the current PDS adapted in ST Engineering USV consists of a combination of PLC and multiple SSR modules to perform power switching. This is also the common approach used in many conventioanl USV in the marintime industry. In this project, a MCU and relay PCB backplane system was explored as an alternative to this traditional approach.

The below table summarises the key advantages and disadvntages between the two approaches:

| **Aspect**               | **PLC + Relay Modules**                                                | **MCU + Relay PCB**                                                                                                                                   |
| ------------------------ | -------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Size and Weight          | - Bulky and heavy due to discrete components<br>- Requires additional space for wiring and terminal blocks<br> | - Compact and lightweight with integrated circuit design<br>- Reduces wiring complexity and space requirements<br>                                           |
| Reliability and Durability | - Certified for maritime usage<br> - proper insulation and protection done based on industrial standards<br>   | - Large efforts are required to design for robustness
| Customisability and Scalability | - Limited customisation <br>- Easily scalable by adding or modifying Relay/PLC modules<br> | - Highly customisable to specific requirements<br>- More difficult to change/scale up                                          |

##### Table 7: Comparison Between PLC + Relay and MCU + Relay PCB System

While the MCU + Relay PCB system offers significant advantages in achieving size reduction, it also presents the above mentioned limitations that need to be addressed. As a result, several design considerations were made in this project to target them:

**Customisability and Scalability:**

To address this challenge, a PCB backplane architecture was adopted for the system, in which the MCU and Relay PCBs are implemented as modular plug-in cards while the base backplane contains only the connectors and copper traces for power transmission purposes. This modular approach enables easy replacement and upgrading of individual relay PCB cards, allowing users to customise and scale the PDS based on their specific requirements without undertaking a full redesign.

![PCB Backplane System](Backplane.png)
##### Figure 7: Example of a PCB backplane system in my past developed project 

**Reliability and Durability:**

To enhance system reliability and durability, the PLC will not be removed from the proposed PDS; instead, it will remain as the switching controller for the relay PCBs while the MCU handles only the power monitoring and data collection. This hybrid approach leverages the strengths of both PLCs and MCUs, ensuring robustness in completing the critical power control tasks without compromising the compactness of the PCB design.

![Control Signal Flow](CSF.png)
##### Figure 8: Control Signal Flow in the new PDS

#### 8.1.2 Improved Power Switching Logic
As mentioned in [Section 3.2](#32-st-engineering-usv-pds), the current PDS control of the ST Engineering USV relies on a continuous signal from the PLC, which creates a risk of complete power-line disconnection in the event of a PLC failure or loose connection. In this project, a new control logic using an ON signal latching design is introduced to solved this problem.

The diagrams below illustrate the current control logic flow and the proposed new control logic. 

![Current Control Logic](CCL.png)
##### Figure 8: Current Control Logic in the PDS

![New Control Logic](NCL.png)
##### Figure 9: New Control Logic proposed

The key difference between the two control logics lies in how the power channel’s ON state is maintained. In the current system, the ON state is sustained by a continuous digital HIGH signal from the PLC. In contrast, the new control logic employs a latching mechanism: a momentary HIGH signal from the MCU toggles and latch the power channel ON at startup, and subsequent continuous HIGH signal will keep the channel OFF. This design ensures that a signal loss from PLC will only turn existing OFF power channel to ON instead of ON power channel to OFF. This significantly enhances fault tolerance, as transient or permanant PLC/MCU failures will not disrupt power delivery to critical subsystems during missions.

In the interim report, it is mentioned that a separate PCB will be designed to implement this latching mechanism while remaining pluggable from the  Relay PCB. However, after further review and consultation with the ST Engineering USV team, the latching circuit will be integrated into the Relay PCB, which is a more compact and cost-effective approach. The schematic and layout of the latching circuit is shown below.

![Latching Circuit](latching_circuit.png)
##### Figure 10: Latch section Schematic and Layout

An LTspice simulation has also been conducted with the designed circuit to validate its functionality. The simulation results are included in the appendix section of this report.

### 8.2 Power Protection

Power protection features are crucial in ensuring the safety and reliability of PDS. Current PDS in ST Engineering USV lacks adequate protection features, making it vulnerable to transient and fault situations. The Relay PCB design explained below will target this issue.

#### 8.2.1 Protection Requirements
Before detailing the protection mechanisms, it is important to identify the types of faults that the new PDS should be able to protect against. Refered to the design standards outlined in [Section 6.1](#61-design-standards), the new PDS should be able to protect against **Overvoltage (OV)**, **Undervoltage (UV)** and **Overcurrent (OC)** faults.

#### 8.2.2 Choice of MOSFET Gate Driver IC - TPS4800
**MOSFET gate driver** is an electronic device designed to efficiently control the gate terminal of a MOSFET, enabling rapid switching between its ON and OFF states. It is the main compnent that enables the power channel switching functionality in the Relay PCB.

In this project, the MOSFET gate driver IC **TPS4800** from Texas Instruments (TI) is selected for its ability to achieve all the above required fault protection while satisfying the technical specifications mentioned in [Section 6.2](#62-technical-specifications). The key features of the TPS4800 are summarised in the appendix section.

![TPS4800 MOSFET Gate Driver IC](TPS4800.png)
##### Figure 11: TPS4800 MOSFET Gate Driver IC Operation Circuit

Besides, during the design of the circuit associated with the MOSFET gate driver, multiple considerations were taken to meet its operational requirements. These considerations are also highlighted in the appendix section. 

#### 8.2.3 User Configurable Protection Thresholds
To further enhance the capabilities and modularity of the Relay PCB, the protection thresholds for OC condition is made user-configurable in the design

This threshold can be configured through a DIP switch interface on the PCB, providng a simple and intuitive way for users to adjust the setting without needing to modify the hardware and refabricate. The avaliable threshold options are 5A, 10A, 20A and 30A, which are the 4 most common current ratings of the devices connected to the system. During PCB operation, the state of this DIP switch will be read by the MCU to identify the OC threshold setting on each channel. This information will then be used to identify the type of fault triggered in that power channel (explained further in [Section 8.4](#84-fault-analysis-logic)).

### 8.3 Power Monitoring
The power monitoring section of the Relay PCB is responsible for monitoring and reporting power status and consumptions statistics in each channel. This section will detail the various features implemented to achieve this functionality.

#### 8.3.1 Power Good Status
Power Good (PG) status provides the most direct feedback on the power condition of each channel, allowing the system to quickly identify the occurance of any power loss issues.

A **TPS3711DDCR** voltage supervisor from TI is installed on the Relay PCB for this purpose. The IC monitors the output voltage and asserts the PG signal high when the voltage is within a specified range. In this project, the range is set to 10 - 30V which is the acceptable operating voltage range of the PDS.

![Voltage Supervisor IC](TPS3711.png)
##### Figure 13: TPS3711DDCR Voltage Supervisor IC Operation Circuit

#### 8.3.2 Fault Reporting
As mentioned in [Section 8.2.1](#821-protection-requirements), the MOSFET gate driver IC TPS4800 is selected for its built-in protection features. Besides, when these protection features are triggered, the IC will assert a fault signal low, which can then be used to report the fault status of each channel.

However, this fault signal is a simple digital signal that only indicates whether a fault has occurred, without providing specific information about the type of fault. TI's **INA228** current shunt monitor is used to address this limitation, which will be explained with more detail in the following sections.

![Current Shunt Monitor IC](INA228.png)
##### Figure 14: INA228 Current Shunt Monitor IC Operation Circuit

#### 8.3.3 Power Consumption Statistics
Accurate power consumption monitoring is essential for identifying abnormal power situations in each channel. Here are some measurement requirements for the power consumption monitoring system in the new PDS:

| **Parameter**           | **Requirement**                                                                 |
|-------------------------|---------------------------------------------------------------------------------|
| Current/Voltage Measurement Accuracy     | ±10% of the actual value or better                                           |
| Voltage Measurement Resolution   | 100mV or better                                                                 |
| Voltage Measurement Range        | 0V to 30V (to cover both 12V and 24V systems)                                  |
| Current Measurement Resolution   | 0.01A or better                                                                 |
| Current Measurement Range        | 0A to 30A (to cover the maximum transient current)                                  |

##### Table 8: Power Consumption Monitoring Requirements

As mentioned above, the INA228 current monitoring IC from TI is the choice for this functionality. The IC provides high-precision power statistics measurements with an integrated 20-bit ADC that satisfy the above resolution and accuracy requirements. At the same time, it supports I2C communication which can be used for real-time data reporting to the MCU

What is more, the IC also features programmable alert thresholds for abnormal power conditions, which can coordinate with the fault signals coming from TPS4800 to provide more detailed insights into the nature of any faults that occur.

#### 8.3.4 Fault Analysis Logic
To make use of the above mentioned alert signals, a fault analysis logic, illustrated in the figure below, is implemented in the new PDS. With this logic, the system can distinguish between the types of faults occurred and report this information to the USV's power PLC for further investigations

![Fault Analysis Logic Flow](faultlogic.png)
##### Figure 12: Fault Analysis Logic Flow

#### 8.3.5 Overcurrent Protection Thresholds Sensing

## 9. MCU PCB System
The MCU PCB serves as the processing unit in the new PDS, responsible for collecting power monitoring data and facilitating communication with the USV’s power PLC. 

The remaining part of this section will explain in detail some features in this MCU PCB, including the choice of MCU and the data reporting peripheral design.

### 9.1 Choice of MCU - STM32G474QET6
The MCU selected for this PCB is from the STMicroelectronics STM32G4 series, in particular the **STM32G474QET6**, which offers a powerful ARM Cortex-M4 core, ample memory resources, and most importantly, a wide range of peripherals sufficient for the new PDS requirements. 

The MCU contains up to 107 fast GPIOs, 5 ADC Channels, and 5 I2C buses, making it enough for collecting data from the 26 relay PCB channels, which outputs in total 78 digital signals, 26 analog signals, and 26 I2C signals. What is more, the MCU also features a built-in CAN controller, which help to reduces the overall PCB footprint by avoiding the need for a separate CAN controller implementation.

### 9.2 Data Reporting Peripheral Design
The communication of this MCU PCB with the USV’s power PLC is carried out via the Controller Area Network (CAN) bus. This communication protocol is chosen here because of its robustness, reliability, and suitability for high-speed data transmission in noisy environments, making it ideal for the maritime environment of this project. This approach also reduces overall wiring complexity, as only two wires are required for CAN communication.

Below is an overall data flow diagram showing how the power monitoring data is collected and reported in the new PDS.
![Power Data Flow](PDF.png)
##### Figure 13: Power Data Flow in the new PDS

## 10. Power Backplane
As mentioned in [Section 8.1.1](#811-moving-towards-pcbs), the power backplane is designed to provide a robust and scalable platform for integrating the Relay PCBs, the MCU PCB and other components in the new PDS (e.g. fuses, power convertors). The backplane includes high-current connectors for power delivery, as well as signal connectors for CAN communication between the MCU PCB and the USV’s power PLC.

#### 10.1 Vibration Simulation for Board to Board Connectors Selection

To ensure the mechanical integrity of the board-to-board connectors used in the power backplane, a vibration simulation using SolidWorks was conducted to evaluate the mechanical stress exerted on the connector chosen, which is the TE Connectivity **MULTI-BEAM Connector 6450120-2** (*more detailed on the selection process please refer to the interim report*). The vibration profile used in this simulation is obtained from the on-board IMU data of ST Engineering’s USV during a sea trail happened on March 10th 2026.

![Vibration Simulation Results](vibration.png)
##### Figure 15: Vibration Simulation Results

The simulation results showed that the connector can withstand the expected vibration levels without experiencing significant mechanical stress or failure, making it a suitable choice for the PCB connectors.

Other considerations regarding the design of the power backplane such as current carrying capacity, thermal management and mechanical robustness will be provided in the appendix of this report.

## 11. Firmware Development

Other than the hardware design mentioned above, the firmware development for the Relay PCB and the MCU PCB is also a critical part of this project. This section will provide an overview of the firmware design for both PCBs.

### 11.1 Relay PCB Firmware
The firmware on Relay PCB is designed to interface the MCU and the current shunt monitor INA228AIDGSR to adjust the various settings of the power monitoring system.

Key features of the design involves:
 - Configuring the conversion time of INA228 to response to transient faults 
 - Setting the sensor sampling rate to ensure accuracy in continuous power monitoring
 - Allocating the I2C static address for multiple channels to allow the MCU to identify the data source of each channel

### 11.2 MCU Firmware
The firmware for the MCU PCB is responsible for collecting data from the Relay PCB and communicating with the USV’s power PLC via CAN bus. Detailed tasks of the MCU firmware include:

- Reading the PG status, fault status, and power consumption data from the Relay PCB.
- Processing the collected data to determine the fault types if any faults are detected.
- Sending the processed data to the USV’s power PLC via CAN communication.

**The detailed design considerations of the above mentioned firmware tasks will be illustrated in the appendix section of this report*.

## 12. Subsystem Prototyping and Testing 

Before integrating the MOSFET PCB, MCU PCB, and Power backplane into a complete PDS, each subsystem were prototyped and tested separately to validate their functionality and performance. The below sections outline these processes and summarize the results which proven the functionality of each subsystem based on the performance criteria defined in [Section 6.5](#65-performance-criteria).

### 12.1 Relay PCB Subsystem Prototyping and Testing
In this project, the Relay PCB has gone through 3 major iterations, which was designed to be tested alone, with T&C PCB and with the power backplane resepctively.This report will go through briefly the design achievments in all 3 iterations and focus on discussing the test result of the final iteration, which best reflects the performance of this series of PCB prototypes.

**For more detailed test processes and results of the Relay PCB iterations, please refer to the appendix section of this report*.

#### 12.1.1 1<sup>st</sup> Iteration Relay PCB

The 1<sup>st</sup> iteration of the Relay PCB is designed with **Wago 221-412** terminal blocks as power input and output connectors, which allow it to be tested seperately through cable connections. The testing of this iteration includes basic power channel switching testing, power protection testing and power monitoring testing. The results has validated the functionalities of MOSFET gate driver IC TPS4800 selected and the latching circuit designed. However, it is also identified from this iteration that the initial power monitoring IC choice AMC1301DWVR was not suitable for this application due to it having a common mode input voltage limit smaller than required, which led to the change of the dedicated IC to INA228 in the later iterations. 

**This iteration of the PCB is also discussed in the Interim Report, refer to it if more detailed design information is needed.*

![1st Iteration Relay PCB](1st_Relay_PCB.jpg)
##### Figure 15: 1<sup>st</sup> Iteration of the Relay PCB

![Test Setup for 1st Iteration](1st_test_setup.jpg)
##### Figure 16: Test Setup for 1<sup>st</sup> Iteration of the Relay PCB

#### 12.1.2 Testing and Commissioning (T&C) PCB

Before carrying out the design of a full Power Backplane. a single channel T&C PCB was designed and tested to validate the integration of the relay PCB with the MCU PCB. This prototype will serve as a proof of concept for the overall PCB subsystem design and allow for iterative improvements before scaling up to the full 26-channel implementation. Below is the designed T&C PCB:

![Testing and Commissioning PCB](Testing_PCB.jpg)
##### Figure 16: Testing and Commissioning PCB

Besides, the T&C PCB is also used to conduct a commissioning check on the Relay PCB produced and configured before their actual deployment. The check involves verifying all intended functionalities of the connected Relay PCB as well as validating the correct setting of the overcurrent threshold and static I2C ID for communication with the MCU, which are important preventive measures to reduce production errors. Below is a figure showing the commissioning test procedures and their intended outcomes:

![Relay PCB Commissioning Test Procedures](commissioning.png)
##### Figure 17: Relay PCB Commissioning Test Procedures and Intended Outcomes

<video width="800" controls>
  <source src="/videos/demo.mp4" type="video/mp4">
</video>

##### Figure 18: Video Demonstration of the Relay PCB Commissioning Test Procedures

**More detailed information about the design of the T&C PCB and the commissioning test procedures can be found in the appendix section of this report*.

#### 12.1.3 2<sup>nd</sup> Iteration Relay PCB and its Integration with T&C PCB
Developing upon the 1st iteration, the 2nd iteration of the relay PCB has replaced the terminal blocks with the high-current PCB board to board **MULTI-BEAM Connector 6450120-2** to examine its functionality. This means that the PCB cannot be powered using cable connections. Instead, the T&C PCB is used for its testing. Other than what is conducted in the previous iteration, additional tests performed on this iteration includes board commissioning procedure testing and the testing on the interaction of MCU with Relay PCB for power monitoring data collection and reporting.

The results of these tests have shown the capability of the chosen PCB connectors in handling the maximum continuous current of 20A as well as the transient current of 30A. Besides, the new power monitoring IC choice INA228 is also first introduced in this iteration and validated through these test results. The integration of the Relay PCB with the T&C PCB has further served as a platform for developing the firmware for the various PCB subsystem as mentioned in [Section 11](#11-firmware-development)


![2nd Iteration Relay PCB Front View](2nd_Relay_PCB_Front.jpg)
##### Figure 17: Front view of the 2<sup>nd</sup> Iteration Relay PCB

![2nd Iteration Relay PCB Back View](2nd_Relay_PCB_Back.jpg)
##### Figure 18: Back view of the 2<sup>nd</sup> Iteration Relay PCB

![2nd Iteration Relay PCB Integrated with T&C PCB](2nd_Relay_PCB_Integrated.jpg)
##### Figure 19: 2<sup>nd</sup> Iteration of the Relay PCB Integrated with T&C PCB

![Test Setup for 2nd Iteration](2nd_test_setup.jpg)
##### Figure 20: Test Setup for the Integrated PCBs

Although the main components of the Relay PCB were finalised and validated in this iteration, several issues were identified during testing:

- **PLC input signal compatibility**: The switching signal circuit on this PCB revision is unable to tolerate the 24 V control signal from the PLC. A 24 V-to-3.3 V signal level-shifting stage will therefore be added in the next revision.
- **Overcurrent threshold accuracy**: The user-configurable overcurrent threshold does not accurately match the actual protection trigger point. This discrepancy is caused by the MOSFET-based resistor selection method used to switch between threshold resistors. To improve reliability and accuracy, the design will be revised to use a mechanical DP3T slide switch for resistor selection.

#### 12.1.4 Final Iteration Relay PCB
This iteration of the PCB mainly focus on improving issues identified in the previous iteration mentioned above. After the fabrication and assembly of this iteration, a throughout testing and evaluation with the Power Backplane and MCU Board is conducted on this iteration, which will be discussed in the "Overall System Integration and Testing" section of this report ([Section 13](#13-overall-system-integration-and-testing)).

![Final Iteration Relay PCB](final_relay_PCB.png)
##### Figure 19: Final Iteration of the Relay PCB

**Due to the PCB manufacturing delay, the production of this iteration of the Relay PCB is still ongoing at the time of this report submission. Most latest picture will be updated once the production is complete.*

### 12.2 Other PCB Subsystem Prototyping and Testing

Other than the Relay PCBs, two more PCB subsystems are prototyped in this project: the MCU PCB and the Power Backplane PCB. 

The MCU PCB is prototyped with reference to the MCU section of the T&C PCB. The testing of the MCU PCB focuses on validating its data collection and reporting functionalities, especially its measuremnet accuracy and resolution under multi-channel operation. 

![MCU PCB Prototype](MCU_PCB.png)
##### Figure 20: MCU PCB Prototype

Similar to the MCU PCB, the power backplane is prototyped by expanding the single channel Relay PCB connector section of the T&C PCB to a full 26 channels backplane design. The testing of the power backplane focuses on validating its power transmission capabilities. 

![Power Backplane Prototype](Backplane_PCB.jpg)
##### Figure 21: Power Backplane Prototype

Due to the nature of these PCBs, it is not feasible to test them separately without the integration of the whole system. As a result, the testing of these two PCB subsystems is conducted together with the final iteration of the Relay PCB, which, as mentioned above, will be discussed in the next section.

## 13. Overall System Integration and Testing
After separate testing of the individual subsystems, the next step is to integrate them on the power backplane and conduct comprehensive testing to validate the overall functionality and performance of the new PDS against the performance criteria defined in [Section 6.5](#65-performance-criteria).

However, due to time constraint, this project will only cover the initial integration testing phases, which include an in lab functionality testing and a thermal testing with 5 operating Relay PCB channels and the MCU PCB on the Power Backplane. Further testing phases will be carried out by the ST Engineering USV team after the completion of this project.

### 13.1 Functionality Testing
Functionality testing was conducted to verify whether that the new PDS meets all technical specifications and functional requirements outlined in [Section 5](#5-Design-Requirments). This will involve testing the power switching capabilities, fault protection features, and power monitoring functionalities under various load conditions and fault scenarios. The testing will be performed in a controlled laboratory environment using power supply and electronic load tester. Below is a summary of the functionality testing procedures and their results:

| **Tested Functionality** | **Test Procedures** |**Expected Outcome**|**Actual Outcome** | **Pass/Fail** |
|-------------------------|---------------------|----------------|-------------------|---------------|
| Power Channel Switching at no load         |      With no current drawn by electronic load tester, turn on each power channel for 30s then turn off the power channel                |        Power ON/OFF on all power channels successfully with a response time <1ms           |   Power ON/OFF on all power channels successfully with a response time of 750us measured on the oscilloscope   |      PASS         |
| Power Channel Switching at 20A continuous current drawn     |      With a constant current of 20A drawn by the electronic load tester, turn on each power channel for 30s then turn off the power channel                |       Same as above           |   Power ON/OFF on all power channels successfully with a response time of 750us measured on the oscilloscope    |      PASS         |
| Power Channel Protection at 32A transient current drawn     |      With a transient current of 32A drawn by the electronic load tester at one specific channel, observe the response of all power channels (OC threshold configured to 30A)               |       Only the affected Power channel trips and protects within an acceptable delay (<1ms)                |   Only the affected power channel trips and protects with a delay of approximately 850us measured on the oscilloscope              |      PASS         |
| Power Channel Protection at 9V undervoltage input     |      Apply a 9V input voltage to all power channel and observe the response                |        All power channel trips and protects against undervoltage within an acceptable delay (<1ms)                 |   All power channel trips and protects against undervoltage with a delay of approximately 850us measured on the oscilloscope               |      PASS         |
| Power Channel Protection at 32V overvoltage input     |      Apply a 32V input voltage to all power channel and observe the response                |        All power channel trips and protects against overvoltage within an acceptable delay (<1ms)               |   All power channel trips and protects against overvoltage with a delay of approximately 850us measured on the oscilloscope              |   PASS         |
| Power Channel Monitoring at 24V 0.06A continuous current drawn (smallest load in ST Engineering USV)     |      With a constant current of 0.06A drawn by the electronic load tester, observe the power channel monitoring message on the MCU PCB               |        Power channel monitoring functions as specified in [Section 8.3.3](#833-power-consumption-statistics)           |   Voltage & Current reading accuracy within 10% of the expected value (0.066 - 0.054A)    |      PASS         |
| Power Channel Monitoring at 24V 20A continuous current drawn     |      With a constant current of 20A drawn by the electronic load tester, monitor the power channel monitoring message on the MCU PCB               |        Same as above           |   Voltage & Current reading accuracy within 10% of the expected value (20.2 - 19.8A)    |      PASS         |

##### Table 16: Functionality Test Results Summary for 5 Operating Channels

![Test Setup for Functionality Testing](functionality_test_setup.png)
##### Figure 18: Test Setup for functionality testing of 5 Operating Channels

Other than the above mentioned tests, more tests were also conducted to validate features such as the detection of the fault types  and the identification of the overcurrent threshold setting at each power channel. These will be summaries in the appendix section of this report.

**Due to PCB manufacturing delay, the above mentioned test results comes from the testing of only 1 operating relay PCB on the T&C PCB. The final results of the testing with 5 operating relay PCB on the Power Backplane will be updated after the submission of this report but before the completion of this project.*

### 13.2 Thermal Testing
Thermal testing was conducted to evaluate the heat generation of the new Power Distribution System (PDS) under different load conditions. The objective of this test was to ensure that the system operates within safe temperature limits during continuous operation.

The overall system thermal test was performed by monitoring the temperature of five loaded channels under two conditions and last until a steady state temperature is reached:
- No-load condition
- Maximum continuous load of 20 A

The test procedure consisted of two stages:

Hot-spot identification – A thermal imaging camera was used to scan the system and identify components with the highest temperature rise.

Temperature monitoring – Temperature probes were then placed at the identified hot spots to continuously record temperature throughout the test duration.

The following table summarises the thermal testing results.

| **Load Condition** | **Component** || **Hotest Spot Steady State Temperature** | **Within Accepted Range?** |
|--------------------|---------------|-------------------------------|-----------------------------|---------------|
| 0A             | MOSFETs       |                               |                             |               |
| 0A            | Shunt Resistor |                               |                             |               |
| 20A            | MOSFETs       |                               |                             |               |
| 20A            | Shunt Resistor |                               |                             |               |

##### Table 18: Thermal Testing Results Summary for 5 Loaded Channels

![Test Setup for Thermal Testing](thermal_test_setup.png)
##### Figure 19: Test Setup for thermal testing of 5 Loaded Channels

**Due to PCB manufacturing delay, the above mentioned thermal testing were unable to be conducted until the point of report submission. The final results will be updated here before the completion of this project.*

## 14. Conclusion
### 14.1 Limitations
<!-- [What aspects of the system were not tested? What conditions were not representative of real deployment? What technical constraints remain?] -->

The first limitation of this project is the lack of testing under actual operational conditions. While the functionality and thermal testing conducted in the laboratory provide valuable insights into the performance of the new PDS, they may not fully capture the complexities and challenges of real-world maritime environments, such as exposure to saltwater, temperature fluctuations, and mechanical vibrations. As a result, the system's performance and reliability under these conditions remain unverified. This limitation hopefully will be solved by more follow-up testing after the completion of this project.

Another limitation is associated with the technical constraints of the design. The current PDS PCBs are only suitable for DC power operation but not functional under AC load. This is a significant limitation, as many maritime system components (e.g. Servers/Switches, Induction motors) still operate on AC power. This limitation highlights the need for future iterations of the PDS to expand its capabilities to support a wider range of power types and applications.

### 14.2 Possible Future Improvements

<!-- [What are some potential improvements that could be made to the system? What are some possible future directions for this project?] -->
As mentioned in the limitations section, one potential improvement for the new PDS is to expand its capabilities to support AC power loads. This would involve redesigning the power switching components to handle AC currents, implementing appropriate protection features for AC faults, and modifying the monitoring system to accurately measure AC power consumption. This improvement would significantly enhance the versatility and applicability of the PDS in maritime environments, allowing it to support a wider range of systems and components.

Other than more hardware developments, possible improvements can also be made in the software aspect of the PDS. For example, the data collected by the MCU can be further processed using machine learning algorithms to predict potential faults before they occur, enabling proactive maintenance and reducing downtime. Additionally, the user interface for monitoring the PDS could be enhanced to provide more intuitive and actionable insights for operators.


## References

1. Abraham Sachin, "Marine Electrical Distribution," 22 June 2018. [Online] Avaliable: teckhmarine.blogspot.com/2018/06/marine-electrical-distribution.html.
2. ABB, "Unmanned Surface Vehicles/Vessel (USV) Reliable Power and Propulsion Architecture Characterization," 2020. [Online]. Available: https://new.abb.com/docs/librariesprovider15/gov/usv-abb-white-paper-20200830.pdf?sfvrsn=6369e809_2
3. ST Engineering, "Unmanned Surface Vehicle (USV) Solutions," [Online]. Available: https://www.stengg.com/en/solutions/unmanned-surface-vehicle-usv-solutions.html
4. IEEE Std 1709-2010, "IEEE Recommended Practice for the Design and Application of Power Electronics in Electrical Power Systems," pp.1-50, 2010.
5. Omron, "G3NA-210B-UTU DC5-24 Solid State Relay Datasheet," [Online]. Available: https://www.ia.omron.com/product/item/7692/
6. Texas Instruments, "TPS4800-Q1 High-Side and Low-Side N-Channel MOSFET Driver with Integrated Protection Features," [Online]. Available: https://www.ti.com/product/TPS4800-Q1
7. Texas Instruments, "TPS3711 Voltage Supervisor with Power-Good Output," [Online]. Available: https://www.ti.com/product/TPS3711
8. Texas Instruments, "AMC1301 Isolated Delta-Sigma Modulator for Current Sensing," [Online]. Available: https://www.ti.com/product/AMC1301
9. IPC-2152, "Standard for Determining Current-Carrying Capacity in Printed Board Design," pp.1-60, 2017.

---
## Appendix A: Technical Specifications Rationale
The 30 A transient current limit is derived from the maximum expected per-channel transient DC load — 24 A as specified in the searchlight datasheet — with an additional 50% design margin to provide sufficient headroom for short-duration overloads. A power-consumption chart was also prepared to verify that these power-level specifications are adequate for all required loads; this chart is included in the Appendix.

The fault-response requirement is selected to match the operating characteristics of the G3NA-210B-UTU DC5–24 relay used in the current PDS, which has a specified operation time of up to 1 ms.

## Appendix B: TPS4800 Key Features
| **Key Features**                | **Specifications**                                                                 |
| :------------------------------ | :-------------------------------------------------------------------------------- |
| Operating Voltage               | 3.5V to 95V DC                                                                      |
| Overvoltage Protection Threshold | Adjustable between 10V to 60V DC                                                  |
| Undervoltage Protection Threshold | Adjustable between 6V to 54V DC                                                   |
| Overcurrent Protection Threshold | Adjustable between 5A to 50A                                                      |
| Overcurrent Protection Response Time | <1ms (adjustable)                                                                          |
##### Key Features of TPS4800 MOSFET Gate Driver IC

## Appendix C: Design MOSFET PCB to Meet Technical and Protection Specifications
Several design considerations were taken during the MOSFET PCB design to ensure that the technical specifications and protection requirements mentioned in [Section 5.2](#52-technical-specifications) and [Section 7.1](#71-protection-requirements) are met:

**Current Tolerance:** To handle the maximum continuous current of 20 A and transient current of 30 A, the MOSFET PCB adopts a 4-layer design, with the middle layers dedicated entirely to power and ground. Additionally, the PCB traces are designed with sufficient width and thickness to minimize resistance and heat generation (Calculation done based on design standrad _IPC-2152_). Thermal vias and copper pours are also incorporated to improve heat dissipation.

![MOSFET PCB Dedicated Power Plane](Players.png)
![MOSFET PCB Dedicated Ground Plane](Glayers.png)  
##### Dedicated Power and Ground Plane in the MOSFET PCB

![MOSFET PCB Trace Width Calculation](tracecalc.png)  
##### Trace Width and Plane Area Calculation for the MOSFET PCB using online IPC-2152 Trace Width Calculator

![MOSFET PCB Thermal Vias and Copper pours](thermalvias.png)
##### Thermal Vias and Copper Pours in the MOSFET PCB

**Fault Protection Thresholds:** The TPS4800 gate driver IC allows for adjustable fault protection thresholds. Below is a table showing the overvoltage, undervoltage, and overcurrent protection thresholds set for the the most recent prototype, according to the specifications outlined. Resistor dividers and charging capacitors are used to configure these thresholds accurately. 

| **Protection Type**     | **Threshold Setting**                         |
|------------------------|----------------------------------------------| 
| Overvoltage Protection    | 30V DC                                       |
| Undervoltage Protection   | 10V DC                                       |
| Overcurrent Protection    | 30A                                          |
| Fault Response Time        |  50μs                                       |
##### Table 8: Protection Threshold Settings on the MOSFET PCB

![Protection Threshold Configuration Circuit](protectioncircuit.png)
##### Example of the Protection Threshold Configuration Circuit in the MOSFET PCB


## Appendix D: MOSFET and Latch PCB Schematics
+ [MOSFET PCB Schematics](mosfetschem.pdf)
+ [Latch PCB Schematics](latchschem.png)

## Appendix E: MOSFET and Latch PCB Layouts
+ [MOSFET PCB Layouts](mosfetlayout.pdf)
+ [Latch PCB Layouts](latchlayout.pdf)

## Appendix F: Latch PCB Simulation
![Latching PCB Simulation](latchsim.png)  
##### Latch PCB Simulation Results

## Appendix G: Power Consumption Chart
![Power Consumption Chart](powerchart.png)  
##### Power Consumption Chart of the USV DC Systems