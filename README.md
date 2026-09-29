#  SAIROS – AI-Powered Underground Mine Safety, Monitoring and Rescue Rover

**Smart India Hackathon 2026**  
**Problem Statement ID:** SIH26039

---

##  About the Project

SAIROS is a six-wheel ground rover being developed for underground mine safety, monitoring and rescue support.

The main idea is to send the rover into a mine area where it may not be safe for a person to enter immediately. The rover collects information about the surroundings using gas sensors, environmental sensors, cameras, ultrasonic sensors and LiDAR. The collected information is processed on the rover and sent to a base station through a wireless mesh network.

The rescue team can use the information from the rover to understand the underground situation, monitor hazardous conditions, detect people and observe the path taken by the rover.

---

##  Problem Statement

Underground coal mines can have hazardous conditions such as toxic gases, low oxygen levels, poor visibility, high temperature, obstacles, flooding and mine collapses. During an emergency, the rescue team may not have enough information about the affected area before entering it.

Entering an unknown mine section can expose rescue personnel to additional risks. It can also take time to understand what has happened inside the mine.

The problem statement therefore requires a system that can operate in hazardous underground environments, monitor mine conditions, provide visual information, detect hazards, assist in locating trapped workers and help rescue teams make better decisions.

SAIROS focuses on the ground-rover approach to this problem.

---

##  Our Proposed Solution

SAIROS is designed as a six-wheel mine-rescue rover that can be remotely operated in underground mine passages.

The rover combines:

* Gas monitoring
* Temperature and humidity monitoring
* Low-light video
* Thermal imaging
* Person detection using AI
* Obstacle detection
* LiDAR-based scanning
* Mapping and navigation
* Wireless mesh communication
* Remote monitoring

The system is divided into sensing, processing, navigation, communication and monitoring parts.

---

##  How SAIROS Works

The basic working flow is:

**Mine Environment → Sensors & Cameras → ESP32 / Raspberry Pi 4B → AI & Navigation Processing → Wi-Fi Mesh → MQTT → Base Station Dashboard**

The rover moves through the mine and collects information from its sensors and cameras.

The ESP32 is used for sensor interfacing and rover-control functions. The Raspberry Pi 4B is used for the main processing tasks, including camera processing, AI inference and navigation-related processing.

The camera feed is processed using OpenCV and YOLOv8. YOLOv8 is used to assist with person detection.

The YDLIDAR X2 provides 2D scanning information for mapping and navigation. Ultrasonic sensors provide additional information about nearby obstacles.

The collected data is transmitted through Archer Wi-Fi mesh nodes. MQTT is used for lightweight telemetry and alert communication. The information is finally displayed at the base station dashboard.

---

#  System Architecture

The SAIROS system can be understood through five main parts:

###  1. Sensing Layer

The rover collects information from the mine using:

* Gas sensors
* Temperature and humidity sensor
* Thermal camera
* Low-light camera
* Ultrasonic sensors
* LiDAR

These sensors provide information about the environment and the rover's surroundings.

###  2. Control and Processing Layer

The **ESP32** handles sensor interfacing and rover-control functions.

The **Raspberry Pi 4B** acts as the main processing unit. It handles camera processing, AI inference, LiDAR-related processing and communication with the other system components.

###  3. AI and Vision Layer

The camera provides the visual input.

**OpenCV** is used for image and video processing.

**YOLOv8** is used for person detection from the camera feed. The detection result can be sent to the monitoring station as part of the rover's situational information.

###  4. Navigation Layer

The **YDLIDAR X2** scans the surrounding area and provides 2D distance information.

The LiDAR data can be used for mapping, obstacle awareness and navigation-related functions through SLAM/navigation software.

The ultrasonic sensors provide additional short-range obstacle information.

###  5. Communication and Monitoring Layer

**TP-Link Archer Wi-Fi nodes** are used to build the wireless mesh network.

**OpenWrt** provides the networking platform on supported routers.

**BATMAN-adv** is used for the multi-hop mesh networking layer.

**MQTT** is used to transfer telemetry and alerts.

The base station dashboard displays the information received from the rover.

---

#  Hardware

The main hardware planned for the SAIROS rover includes:

| Component | Purpose |
| -------------------------- | ------------------------------------- |
| Raspberry Pi 4B | Main processing, AI and data handling |
| ESP32 | Sensor interfacing and rover control |
| Six-wheel chassis | Rover mobility |
| RHINO 24V DC 60 RPM geared motor | Drive system |
| BTS7960 motor drivers | Motor control |
| 24 V LiFePO4 battery | Main power source |
| MQ/TGS gas sensors | Gas monitoring |
| SHT31 | Temperature and humidity monitoring |
| MLX90640 | Thermal imaging |
| Caddx Baby Ratel 2 | Visual monitoring in dark areas |
| HC-SR04 | Short-range obstacle detection |
| YDLIDAR X2 | 2D scanning and navigation |
| TP-Link Archer Wi-Fi nodes | Wireless mesh communication |

The final hardware configuration may be updated as the prototype is tested.

---

#  Software and Technologies

##  Python

Python is used for system programming, data processing and integration between different software components.

##  YOLOv8

YOLOv8 is used for AI-based person detection from the rover's camera feed.

##  OpenCV

OpenCV is used to capture and process camera frames and prepare visual data for further processing.

##  OpenWrt

OpenWrt is used as the customizable operating system/networking platform on supported Wi-Fi routers.

##  BATMAN-adv

BATMAN-adv is used to create the multi-hop wireless mesh network between the communication nodes.

##  MQTT

MQTT is used for lightweight communication of sensor values, status information and alerts.

##  SLAM / Navigation Software

SLAM and navigation software use LiDAR and rover movement information to support mapping, localization and navigation inside the mine where GPS is not available.

##  Monitoring Dashboard

The dashboard provides the rescue team with a common place to view sensor readings, alerts, video, person detections and navigation information.

---

#  Communication System

Communication is an important part of the SAIROS design because underground mine passages may not provide a direct wireless path to the base station.

SAIROS uses **TP-Link Archer Wi-Fi nodes** as communication nodes. The nodes are positioned at suitable locations inside the mine to extend the communication path.

The network uses:

**Archer Router → Archer Router → Archer Router → Base Station**

The mesh approach allows data to travel through multiple nodes instead of depending only on one direct connection.

OpenWrt is used as the router platform and BATMAN-adv provides the mesh networking layer.

MQTT is used for transferring sensor telemetry and alerts.

The system is intended to support low-resolution live video together with sensor and AI information rather than high-definition video transmission.

---

#  AI and Person Detection

One of the important functions of SAIROS is assisting in the detection of people inside the mine.

The camera provides the input video. OpenCV handles the video frames and YOLOv8 processes the frames for person detection.

The basic process is:

**Camera → OpenCV → YOLOv8 → Person Detection → Alert/Data → Dashboard**

The detected person information can help the rescue team understand whether a person is present in the area being inspected.

AI detection is intended as a rescue-support function and should be used together with human judgement and other sensor information.

---

#  Navigation and Mapping

Underground mines do not provide reliable GPS coverage. Therefore, the rover needs another method to understand its surroundings.

SAIROS uses the **YDLIDAR X2** for 2D scanning.

The LiDAR measures distances around the rover and provides scan data that can be used by SLAM/navigation software.

This can help the system:

* Build a 2D representation of the surroundings
* Detect obstacles
* Understand the rover's position relative to the map
* Support navigation
* Record the route taken during inspection

The communication nodes can also be associated with known mine sections to provide useful reference information about where the rover is operating.

---

#  Monitoring Dashboard

The base station dashboard is designed to give the rescue team a simple view of the information coming from the rover.

The dashboard can include:

* Live low-resolution video
* Gas readings
* Temperature
* Humidity
* Person-detection results
* Hazard alerts
* Rover status
* Communication/node information
* Map/navigation information

The goal is to bring the important information into one place instead of requiring the rescue team to check each sensor separately.

---

#  Key Features

* Six-wheel ground rover for underground inspection
* Gas monitoring
* Temperature and humidity monitoring
* Thermal imaging
* Low-light visual monitoring
* AI-based person detection
* LiDAR-based 2D scanning
* Obstacle detection
* Mapping and navigation support
* Archer-based Wi-Fi mesh communication
* MQTT telemetry and alerts
* Remote monitoring dashboard
* Modular hardware and software design

---

#  Innovation

The main idea behind SAIROS is the combination of several functions in one underground rescue-support rover.

The system brings together:

**Environmental Monitoring + AI Person Detection + Thermal/Low-Light Vision + LiDAR Navigation + Wi-Fi Mesh + Remote Dashboard**

The communication design is also important. Instead of depending on a single Wi-Fi connection, multiple Archer nodes can be positioned along mine sections to provide a multi-hop communication path.

The modular design also makes it possible to change or improve individual parts of the system as testing continues.

---

#  Feasibility

SAIROS is being developed using commercially available components and commonly used software technologies.

The Raspberry Pi 4B and ESP32 provide the processing and control platforms. Sensors, cameras, motor drivers and communication devices can be integrated using standard interfaces.

The communication system can be expanded by adding more mesh nodes according to the mine layout.

The software stack also uses widely available technologies such as Python, OpenCV, YOLOv8, OpenWrt, BATMAN-adv and MQTT.

This makes the prototype suitable for step-by-step development and testing.

---

#  Expected Impact

SAIROS is intended to support rescue teams during underground mine emergencies.

The system can help by:

* Providing information before rescuers enter a hazardous area
* Monitoring underground environmental conditions
* Assisting in locating people
* Providing visual information from dark areas
* Supporting underground navigation and mapping
* Giving rescue teams a remote view of the rover's surroundings
* Reducing unnecessary exposure of rescuers to unknown conditions

SAIROS is a rescue-support system and is not intended to replace trained rescue personnel.

---

#  Current Development Status

The project is being developed in stages.

Current development areas include:

* Rover hardware integration
* Sensor interfacing
* Camera setup
* YOLOv8 person detection
* LiDAR-based navigation
* Wi-Fi mesh communication
* MQTT telemetry
* Monitoring dashboard
* System integration and testing

As development continues, this section will be updated with actual testing results, prototype photographs, maps, detection results and communication measurements.

---

#  Repository Structure

```text
SAIROS/
│
├── README.md
│
├── docs/
│   ├── project-report/
│   ├── architecture/
│   └── references/
│
├── hardware/
│   ├── circuits/
│   ├── schematics/
│   └── components/
│
├── software/
│   ├── esp32/
│   └── raspberry-pi/
│
├── ai/
│   ├── dataset/
│   ├── training/
│   └── inference/
│
├── navigation/
│   ├── lidar/
│   ├── slam/
│   └── maps/
│
├── communication/
│   ├── openwrt/
│   ├── batman-adv/
│   └── mqtt/
│
└── dashboard/
