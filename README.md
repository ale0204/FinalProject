# Wireless Study Hourglass  
**Introduction to Robotics – Final Project**

Student: Alexandra Neamtu  
Faculty of Mathematics and Computer Science, University of Bucharest  
Academic Year: 2025–2026  

---

## 1. General Description

**Wireless Study Hourglass** is a distributed embedded system designed to help users manage and track their focus sessions using a physical gesture instead of buttons or mobile apps.  

The system consists of two ESP32-based devices:

- A **mobile hourglass cube** containing an ESP32, an IMU (motion sensor), and a battery. When the user flips the cube, a focus session starts. When it is flipped back, the session stops.
- A **display station** powered by USB that receives data wirelessly from the cube and shows the current state, remaining time, and statistics on a small screen.

The cube communicates with the display station using **ESP-NOW**, a low-latency peer-to-peer wireless protocol.  
All focus sessions are logged, and daily totals and trends are computed and displayed, allowing the user to track productivity over time.

The project combines physical interaction, real-time embedded control, wireless communication, and persistent data logging into a single coherent system.

---

## 2. GitHub Repository

A dedicated GitHub repository will contain:
- All firmware for both ESP32 boards
- Display and communication logic
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
| ESP32 development board | 1 | Receives data from the cube |
| OLED or LCD display | 1 | Shows focus state, time, and statistics |
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
- Reading an IMU (MPU6050)
- Using ESP-NOW on ESP32
- Driving OLED/LCD displays  

These will be combined into a new system with custom logic and architecture.

---

## 5. What Will Be Changed Compared to Tutorials

Existing tutorials usually demonstrate:
- How to read an IMU
- How to send a message via ESP-NOW
- How to display text on a screen  

This project combines all of them into:
- A two-node distributed system  
- A real-time state machine (focus / break / idle)  
- Persistent logging and statistics  
- A physical gesture-based user interface  

The system behavior, architecture, and integration are original.

---

## 6. Q1 – What is the system boundary?

**Inside the system:**
- Hourglass Cube (ESP32, IMU, battery)
- Display Station (ESP32, display, storage)

**Outside the system:**
- The user
- (Optionally) a phone for viewing statistics via Wi-Fi

The two ESP32 devices and their wireless link form a single well-defined system.

---

## 7. Q2 – Where does intelligence live?

The **Hourglass Cube ESP32** is the primary brain:
- It detects orientation
- Decides when a session starts or stops
- Manages timing and state transitions

The Display Station only displays, stores, and exposes the data.

---

## 8. Q3 – What is the hardest technical problem?

The hardest technical problem is:

**Reliable detection of cube orientation combined with real-time wireless synchronization between two embedded devices.**

This requires filtering noisy IMU data, debouncing physical movement, and ensuring that the display always stays synchronized with the cube.

---

## 9. Q4 – What is the minimum demo?

The minimum valid demo is:

> Flipping the cube starts a focus session.  
> Flipping it back stops the session.  
> The display station immediately shows the correct state and elapsed time.

---

## 10. Q5 – Why is this not just a tutorial?

This project:
- Uses multiple devices
- Uses wireless communication
- Implements a state machine
- Logs and processes data over time
- Provides a physical user interface

It requires architectural and design decisions, not just wiring known modules together.

---

## 11. Do you need an ESP32?

**Yes.**

The project requires:
- ESP-NOW wireless communication
- Low-power operation
- Built-in Wi-Fi radio

These features are specific to the ESP32 platform.
