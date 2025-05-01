[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/AlBFWSQg)
# a14g-final-submission

    * Team Number: 29
    * Team Name: Strawhats
    * Team Members: Sidddharth Ramanathan and Komalika Gaikwad
    * Github Repository URL: 
    * Description of test hardware: acbook Air M1, Dell G15, Windows, SAMW25, SD Card Module, Micss 5524 sensor, 

## 1. Video Presentation

<a href="(https://drive.google.com/drive/folders/17WcglImkKmd4xaHWco-ZTRyiMJsDFJ4c?usp=sharing)">Project Demonstration</a>
(New Video will be updated)

## 2. Project Summary

CO Away! - Toxic gas Detector and Filtering system

CO Away is designed to enhance indoor safety by detecting and mitigating carbon monoxide (CO) presence in apartment units. Inhaling CO is hazardous, often leading to severe health risks. Unlike conventional CO detectors that simply trigger an alarm when CO is detected, CO GO takes a proactive approach by removing and filtering the harmful gas as soon as Even a small amount of increase is observed. If and only if there is an continuious increase in the level of CO in a unit will the, Alarms and LED lights go off waking up the residents of the unit. 
CO GO can be installed in individual apartment units to monitor and address CO accumulation. Each device uses a MiCS-5524 MEMS sensor for detecting indoor carbon monoxide and natural gas leaks. Upon detecting hazardous CO levels, the system:
* Activates an exhaust system to remove CO from the space.
* Filters the expelled gas through a filter, ensuring clean air circulation.
* Triggers an alarm system with an audible buzzer and LED lights for immediate notification once the CO levels are over a certain PPM.
* Sends real-time alerts via a Wi-Fi-enabled SAMW25 microcontroller to building managers and residents, detailing the specific unit affected and the duration of the event.

### Use Case:
During cold winters, prolonged use of heaters and poor ventilation can lead to CO buildup, posing respiratory and health risks to residents. CO GO ensures rapid detection and removal of the gas, maintaining indoor air quality and safety, Sometimes without even disturbing the residents. People with different health conditions have different limits of CO they can tolerate, CO Go helps us change the alarm limits based on the specific needs of the residents. 

### Implementation:
For this project, three prototype units will be developed, each with its own CO GO kit connected to separate exhaust and filtration systems. The devices will communicate via I2C to the SAMD21 microcontroller and integrate with Node-RED, allowing comprehensive monitoring of all units, including timestamps for each incident.
By addressing both detection and mitigation, CO GO offers a robust solution for CO safety in residential apartments, promoting health and peace of mind for occupant based on their needs and health conditions. 


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
| SRS-22 | The Display text on the Node red shall include data from all the three units that is transfered over the MQTT protocol. | Unsatisfied - Although we were able to get the wifi handler updates, We were not able to able to Update new readings via MQTT | Unsatisfied |
| SRS-23 | The display on the Node red shall Display the level of CO detected on the dashboard and another dashboard that logs in the time when toxic level 2 was detected on the system along with the Past measured readings | Satisfied |
| SRS-24 | The display on the Node red shall refresh every second after we get the input reading.  | Satisfied |


## 4. Project Photos & Screenshots



## Codebase

- <a href="(https://github.com/ese5160/final-project-t29-straw-hats.git)">GitHub_Codebase</a>
- <a href="(http://172.172.174.245:1880/ui/#!/0?socketid=MjuhaxfJVJHE7yXFAAE1)">NodeRed</a>


