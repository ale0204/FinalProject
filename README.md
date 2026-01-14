# Wireless Study Hourglass  
**Introduction to Robotics – Final Project**

Student: Alexandra Neamtu  
Faculty of Mathematics and Computer Science, University of Bucharest  
Academic Year: 2025–2026  

---

## 1. General Description

**Wireless Study Hourglass** is a distributed embedded system designed to help users manage and analyze their focus sessions using a physical gesture and a mobile interface.

The system is built around **two ESP32 microcontrollers**:

- A **mobile Hourglass Cube** that contains an ESP32, an IMU (motion sensor), and a battery. When the user flips the cube, a focus session starts. When it is flipped back, the session stops.
- A **Display Station** that contains a second ESP32, a screen, and environmental sensors. It receives data wirelessly from the cube and acts as a gateway between the cube and the user’s phone.

The two ESP32 boards communicate using **ESP-NOW**, a low-latency peer-to-peer wireless protocol.  
The Display Station also runs a **Wi-Fi web server** that allows a phone to connect and view detailed statistics, session history, and environmental data.

The station measures **air temperature and humidity**, allowing the system to evaluate comfort conditions and generate warnings when the environment is not suitable for focused work.

All focus sessions are logged, summarized, and made available both on the local display and on the phone.

---

## 2. GitHub Repository

A dedicated GitHub repository will contain:
- Firmware for both ESP32 devices
- Wireless communication and state logic
- Display, logging, and web interface code
- Documentation and wiring diagrams

---

## 3. Bill of Materials (BOM)

### Hourglass Cube (mobile node)

| Component | Quantity | Purpose |
|--------|---------|---------|
| ESP32 development board | 1 | Main controller and wireless communication |
| IMU (e.g., MPU6050) | 1 | Detects orientation (flip gesture) |
| Li-Po battery (3.7V) | 1 | Powers the cube |
| TP4056 charging module | 1 | Safely charges the battery via USB |
| Enclosure (cube) | 1 | Houses all components |

### Display Station (fixed node)

| Component | Quantity | Purpose |
|--------|---------|---------|
| ESP32 development board | 1 | Receives data from the cube and hosts the web interface |
| OLED or LCD display | 1 | Shows focus state, time, and summaries |
| Temperature & humidity sensor (e.g., DHT22 or SHT31) | 1 | Measures environmental comfort |
| USB power cable | 1 | Powers the station |

### General

| Component | Quantity | Purpose |
|--------|---------|---------|
| Jumper wires, connectors | — | Electrical connections |
| Breadboard or PCB (optional) | — | Prototyping and mounting |

---

## 4. Tutorial Source

The project is not based on a single end-to-end tutorial.  
Individual references will be used for:
- IMU data acquisition
- ESP-NOW communication
- Display control
- Temperature and humidity sensing
- ESP32 Wi-Fi web servers  

These sources are combined into a new and original system.

---

## 5. What Will Be Changed Compared to Tutorials

Most tutorials cover only one component or one communication method.  
This project integrates multiple subsystems into a **coherent distributed system** with:
- Two communicating ESP32 boards
- A physical gesture-based interface
- Wireless synchronization
- Data logging and statistics
- A phone-based user interface

---

## 6. Q1 – What is the system boundary?

**Inside the system:**
- Hourglass Cube (ESP32, IMU, battery)
- Display Station (ESP32, display, temperature & humidity sensor, storage, Wi-Fi server)

**Outside the system:**
- The user
- The phone, used as a visualization and control interface

---

## 7. Q2 – Where does intelligence live?

The primary intelligence lives in the **Hourglass Cube ESP32**, which:
- Detects the flip gesture
- Manages focus and break states
- Controls session timing  

The Display Station processes, stores, and presents this information.

---

## 8. Q3 – What is the hardest technical problem?

The hardest technical problem is:

**Reliable detection of cube orientation combined with low-latency wireless synchronization between two embedded devices and a phone interface.**

---

## 9. Q4 – What is the minimum demo?

The minimum valid demo is:

> Flipping the cube starts a focus session.  
> Flipping it back stops the session.  
> The Display Station and phone interface immediately show the correct state and time.

---

## 10. Q5 – Why is this not just a tutorial?

This project:
- Uses two embedded nodes
- Uses two wireless protocols (ESP-NOW and Wi-Fi)
- Implements a state machine
- Logs and analyzes data over time
- Combines physical interaction with digital visualization  

It requires system-level design, not just module assembly.

---

## 11. Do you need an ESP32?

**Yes — two ESP32 boards are required.**

One ESP32 is used in the Hourglass Cube, and one is used in the Display Station to handle the display, sensors, and Wi-Fi connection to the phone.
