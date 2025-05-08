
# a14g-final-submission

    * Team Number: 29
    * Team Name: Strawhats
    * Team Members: Sidddharth Ramanathan and Komalika Gaikwad
    * Github Repository URL: https://github.com/ese5160/a14g-final-submission-s25-t29-straw-hats.git
    * Description of test hardware: acbook Air M1, Dell G15, Windows, SAMW25, SD Card Module, Micss 5524 sensor, 

## 1. Video Presentation

**Click on the image below**

[![Watch the video](https://github.com/ese5160/a14g-final-submission-s25-t29-straw-hats/blob/main/Images/CO.jpg?raw=true)](https://drive.google.com/drive/folders/17WcglImkKmd4xaHWco-ZTRyiMJsDFJ4c?usp=sharing)

## 2. Project Summary

### Device Description
CO Away! - Toxic gas Detector and Filtering system

CO Away is designed to enhance indoor safety by detecting and mitigating carbon monoxide (CO) presence in apartment units. Inhaling CO is hazardous, often leading to severe health risks. Unlike conventional CO detectors that simply trigger an alarm when CO is detected, CO GO takes a proactive approach by removing and filtering the harmful gas as soon as a small amount of increase is observed. If and only if there is a continuious increase in the level of CO in a unit will the Alarms and LED lights go off, waking up the residents of the unit. 

During cold winters, prolonged use of heaters and poor ventilation can lead to CO buildup, posing respiratory and health risks to residents. CO GO ensures rapid detection and removal of the gas, maintaining indoor air quality and safety, Sometimes without even disturbing the residents. People with different health conditions have different limits of CO they can tolerate, CO Go helps us change the alarm limits based on the specific needs of the residents. 

CO GO can be installed in individual apartments, closed public spaces and also as an add on to HVAC systems to monitor and address CO accumulation. Each device uses a MiCS-5524 MEMS sensor for detecting indoor carbon monoxide and natural gas leaks. Upon detecting hazardous CO levels, the system:
* Activates an exhaust system to remove CO from the space.
* Filters the expelled gas through a filter, ensuring clean air circulation.
* Triggers an alarm system with an audible buzzer and LED lights for immediate notification once the CO levels are over a certain PPM.
* Sends real-time alerts via a Wi-Fi-enabled SAMW25 microcontroller to building managers and residents, detailing the specific unit affected and the duration of the event.

### Device Functionality:
The MiCS-5524 sensor constantly monitors the CO gas level and reports to the decision making stack of the project, which controls what actuators need to be triggered. There are three modes in this decision making stack:
- Safe mode: When the detected ppm < 10, the environment is considered safe. The green status LED will turn ON and the OLED display will display the ppm value and a "safe" message.
- Detection mode: When the detected ppm is between 10 and 20, there is a mild threat in the environment. The red status LED will turn ON, the exhaust fan turns ON with 50% speed and the OLED display will display the ppm value and a "Mild threat" message.
- Danger mode: When the detected ppm > 20, there is a critical threat in the environment. The red status LED and the buzzer will turn ON, the exhaust fan turns ON with 100% speed and the OLED display will display the ppm value and a "Critical threat, evacuate" message.

Along with the product level changes, the CO gas values will be updated on the node-red dashboard, and basic statistics of high CO threshold will also be tabulated. From the admin side, we are able to run over the air firmware updates, making the device a true IoT Edge device. The project leverages the synchronization capabilities of FreeRTOS, and has designated tasks for each of these functionalities. Here is a state diagram of the device functionality:

<div align=center>
<img src="Images\StateDiagram.drawio.png" width="600">  
</div>

### Challenges
Over the course of this project, we faced several technical and logistical challenges that significantly influenced our development timeline and outcomes:

* Custom Component Design in Altium: The MiCS-5524 CO sensor did not have a predefined footprint in Altium Designer. This required us to manually create a custom footprint, ensuring accurate pad dimensions and pin mappings to meet design specifications.

* Board Bring-Up Issues: Upon receiving our fabricated PCBs, we encountered multiple hardware issues. On PCB A, the FTDI chip failed to function, which impeded USB-to-serial communication. On PCB B, excessive heat buildup was observed due to a voltage regulation flaw, which necessitated manual debugging and circuit modification.

* J-Link Connector Flaw: A critical design oversight led to reversed pad orientation for the J-Link debugger header. As a result, we had to physically reroute the J-Link connector wires through direct soldering to establish the correct signal paths.

* Power Dependency for Wi-Fi Handler: The Wi-Fi communication module failed to initialize properly when powered via USB alone. It only functioned correctly when powered through the onboard Li-Po battery, highlighting an issue with power rail stability or insufficient startup current.

* I2C Display Communication: Establishing I2C communication with the OLED display proved time-consuming due to the limited clarity of the datasheet. We had to reverse-engineer much of the configuration by referring to Arduino examples and implementing display commands incrementally.


### Prototype Learnings
The most critical learning from this prototype phase was understanding the impact of hardware and firmware integration errors. Although our initial plan was to have all three boards operate in sync, manufacturing limitations and debugging complexity constrained our implementation. If given the opportunity to revisit this project, we would focus on system-level integration earlier in the design cycle to catch such issues early on.


### Next Steps & Takeaways

* HVAC System Integration: A natural next step for this project is to scale the system to interface with HVAC systems in commercial buildings, where centralized CO monitoring and control could improve occupant safety and energy efficiency.

* MQTT Communication Debugging: Currently, MQTT protocol communication between the device and Node-RED remains unreliable, only basic mqtt publish functions work. Further investigation into task prioritization, broker connectivity, and buffer handling within the FreeRTOS environment is necessary.

* Sensor Upgrade: Replacing the MiCS-5524 with a more reliable CO sensor—with higher accuracy, better linearity, and a comprehensive datasheet—would enhance the robustness of the system.

* Display Improvements: Transitioning from I2C to SPI communication for the display would reduce latency and improve refresh rates, especially as the system scales or includes graphical data.

* Sensor Calibration Protocol: Proper sensor calibration remains a high priority. We aim to use a controlled calibration tank with known CO concentrations (e.g., 1850 ppm) for durations exceeding five minutes to ensure accurate and repeatable sensor behavior.

## 3. Hardware & Software Requirements

### Hardware Requirements 

| **HRS ID** | **Requirement** | **Status** |
| --- | --- | --- |
| HRS-01 | Li-ion battery's o/p voltage shall be boosted to 5V using a boost converter. | Satisfied |
| HRS-02 | A Switch shall turn on/Off the system. | Satisfied |
| HRS-03 | MiCS-5524 MEMS sensor shall send readings every one sec to the MCU | Satisfied |
| HRS-04 | Exhaust Fan shall start and run at 100% of its speed when the carbon monoxide reaches to Toxicity level 2 (over 15 ppm)| Satisfied |
| HRS-05 | Buzzer shall turn on when the CO level rise up to toxicity level 2 | Satisfied |
| HRS-06 | Buzzer and exhaust fan and the LED shall turn off once the CO levels go down to non toxic level i.e below 15 ppm | Satisfied |

### Software Requirements 

| **SRS ID** | **Requirement** |  **Status** |
| --- | --- | --- |
| SRS-01 | The gas sensor shall measure CO levels and communicate with the SAMW25 MCU over ADC. | Satisfied |
| SRS-02 | Sensor data shall be read every 500 milliseconds ±10 milliseconds.| Satisfied |
| SRS-03 | The CO sensor shall have the accuracy of ± 5%  | Satisfied |
| SRS-04 | The sensor shall aqquire new sample data every 3 seconds. | Satisfied |
| SRS-05 | System shall register different levels of CO that get classified as Level 1 - safe, Level 2 - toxicity over 10 PPM. | Satisfied |
| SRS-06 | Sensor shall give a resistance value which can later be converted to gas part per million using a relation between Ideal resistance and observed resistance.  | Satisfied |

#### Display 

| **SRS ID** | **Requirement** |  **Status** |
| --- | --- | --- |
| SRS-07 | The system shall display on the LCD, the CO levels in the units of parts per million and the room status based on the level of toxicity. | Satisfied |
| SRS-08 | The LCD display will be connected via i2c to the MCU. | Satisfied |
| SRS-09  | When the first reading is registered by the MCU, the Display screen should display - "Carbon Monoxide Level __ PPM " | Satisfied |
| SRS-10  | On the second page of the display the text printed out shall show the Current Toxicity level text.  | Satisfied |
| SRS-11  | When Level 1 toxicity is observed, the displayed text shall be "Toxicity Level- 1, You are safe." | Satisfied |
| SRS-12 | When Level 2 toxicity is observed, the displayed text shall be "Toxicity Level- 2, Danger! Please evacuate."  | Satisfied |
| SRS-13 | The LCD display shall be refreshed every 3 seconds with new CO readings Observed from the sensor.  | Satisfied |

### Operations

| **SRS ID** | **Requirement** |  **Status** |
| --- | --- | --- |
| SRS-14 | The system shall have different modes of operations based on the toxicity level that are classified based on the CO detected ppm. | Satisfied |
| SRS-15 | At level 1 toxicity, i.e negligible CO presence, the system shall have the Exhaust fan off. | Satisfied |
| SRS-16 | At level 2 toxicity, i.e CO presence detected, the system shall have the Exhaust fan on with 100% of its speed | Satisfied |
| SRS-17 | The speed of the fan shall be controlled by PWM mode. | Satisfied |


### Indicators 

| **SRS ID** | **Requirement** |  **Status** |
| --- | --- | --- |
| SRS-18 | The buzzer shall go off when the toxicity level 2 is detected. | Satisfied |
| SRS-19 | The LEDs on the box shall indicate the level of toxicity based on the input CO reading PPM; green at level 1, Red at level 2. | Satisfied |


### Web Interface

| **SRS ID** | **Requirement** |  **Status** |
| --- | --- |--- |
| SRS-20 | The system shall support communication between the MCU and a web interface via WiFi.  | Satisfied |
| SRS-21 | The web interface shall display the CO levels in the units of parts per million and the room status based on the level of toxicity | Partially Satisfied as we have the node red display established to work how we intended when we recieve the MQTT values |
| SRS-22 | The Display text on the Node red shall include data from all the three units that is transfered over the MQTT protocol. | Unsatisfied - Although we were able to get the wifi handler updates, We were not able to able to Update new readings via MQTT |
| SRS-23 | The display on the Node red shall Display the level of CO detected on the dashboard and another dashboard that logs in the time when toxic level 2 was detected on the system along with the Past measured readings | Satisfied |
| SRS-24 | The display on the Node red shall refresh every second after we get the input reading.  | Satisfied |


## 4. Project Photos & Screenshots

##### Demo Setup

<div align=center>
<img src="Images\Setup.jpg" width="600">  
</div>

##### Manufactured PCB 

<div align=center>
<img src="Images\PCB_1.jpg" width="600">  
</div>



##### Altium_Design

<div align=center>
<img src="Images\Altium_Design.png" width="600">  
</div>

<div align=center>
<img src="Images\3D.png" width="600">  
</div>


##### Thermal Image

<div align=center>
<img src="Images\Thermal_image.jpeg" width="600">  
</div>

##### Node-RED dashboard
###### Frontend Dashboard 1
<div align=center>
<img src="Images\Nodered1.png" width="600">  
</div>

######  Frontend Dashboard 2
<div align=center>
<img src="Images\Nodered2.png" width="600">  
</div>


###### Backend Flow
<div align=center>
<img src="Images\Nodered_flow.png" width="600">  
</div>

<div align=center>
<img src="Images\Nodered_flow2.png" width="600">  
</div>

##### Enclosure design on Solidworks

<div align=center>
<img src="Images\Enclosure_design.png" width="600">  
</div>

##### Block Diagram

<div align=center>
<img src="Images\Detailed_diagram.drawio.png" width="600">  
</div>


## 5. Reworks 

Out of the three PCBs we recieved,
* PCB A had manufacturing issues with the FTDI chip, an Inductor was poorly soldered.  
* PCB B had bad power architecture in the power line for 5 Volts, the Voltage kept increasing over 5 Volts constantly resulting the board to heat up.
* PCB C - Mostly perfect, but trace for the reset button was faulty and needed rework, but the code would not go the wifi handler task without the Battery connected to the board. 


## Codebase

- <a href="https://github.com/ese5160/final-project-t29-straw-hats.git">GitHub_Codebase</a>
- <a href="http://172.172.174.245:1880/ui/#!/0?socketid=MjuhaxfJVJHE7yXFAAE1">NodeRed</a>


