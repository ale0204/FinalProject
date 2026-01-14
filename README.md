# Wireless Study Hourglass  
**Introduction to Robotics – Final Project**

Student: Alexandra Neamtu  
Faculty of Mathematics and Computer Science, University of Bucharest  
Academic Year: 2025–2026  

---

## 1. General Description

**Wireless Study Hourglass** is a distributed embedded system designed to help users manage and track their focus sessions using a physical gesture instead of buttons or mobile apps.

The system is built around **two ESP32 microcontrollers**:

- A **mobile Hourglass Cube** that contains an ESP32, an IMU (motion sensor), and a battery. When the user flips the cube, a focus session starts. When it is flipped back, the session stops.
- A **Display Station** that contains a second ESP32, a screen, and environmental sensors. It receives data wirelessly from the cube and displays the current focus state, remaining time, and productivity statistics.

The two ESP32 boards communicate using **ESP-NOW**, a low-latency peer-to-peer wireless protocol that does not require a Wi-Fi network or Bluetooth pairing.  
The Display Station also measures **air temperature and humidity**, allowing the system to evaluate environmental comfort and show warnings when conditions are not suitable for focused work.

All focus sessions are logged, and daily totals and trends are computed and displayed, giving the user feedback about their productivity over time.

---

## 2. GitHub Repository

A dedicated GitHub repository will contain:
- Firmware for both ESP32 devices
- Wireless communication and state logic
- Display and logging code
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
| ESP32 development board | 1 | Receives data from the cube and hosts the display |
| OLED or LCD display | 1 | Shows focus state, time, and statistics |
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
- Reading IMU data (MPU6050 or similar)
- Using ESP-NOW on ESP32
- Driving OLED/LCD displays
- Reading temperature and humidity sensors  

These sources are combined into a new system with custom logic and architecture.

---

## 5. What Will Be Changed Compared to Tutorials

Most tutorials focus on a single topic (IMU reading, ESP-NOW messaging, or display output).  
This project integrates them into a **distributed system** with:
- Two communicating embedded nodes
- A real-time state machine (focus / break)
- Persistent logging and statistics
- Environmental awareness

The behavior and system architecture are original.

---

## 6. Q1 – What is the system boundary?

**Inside the system:**
- Hourglass Cube (ESP32, IMU, battery)
- Display Station (ESP32, display, temperature & humidity sensor, storage)

**Outside the system:**
- The user
- (Optionally) a phone used only for viewing data via Wi-Fi

The two ESP32 devices and their wireless link form a single well-defined system.

---

## 7. Q2 – Where does intelligence live?

The primary intelligence lives in the **Hourglass Cube ESP32**, which:
- Detects the flip gesture
- Manages focus and break states
- Tracks session timing

The Display Station processes and presents this information but does not control the core logic.

---

## 8. Q3 – What is the hardest technical problem?

The hardest technical problem is:

**Reliable detection of cube orientation combined with real-time wireless synchronization between two embedded devices.**

This involves filtering noisy IMU data, debouncing physical motion, and keeping both ESP32 boards in a consistent state.

---

## 9. Q4 – What is the minimum demo?

The minimum valid demo is:

> Flipping the cube starts a focus session.  
> Flipping it back stops the session.  
> The Display Station immediately shows the correct state and elapsed time.

---

## 10. Q5 – Why is this not just a tutorial?

This project:
- Uses two embedded devices
- Uses wireless peer-to-peer communication
- Implements a state machine
- Logs and processes data over time
- Combines physical interaction with digital feedback  

It requires design and architectural decisions, not just following wiring instructions.

---

## 11. Do you need an ESP32?

**Yes — two ESP32 boards are required.**

One ESP32 is used in the Hourglass Cube (mobile node), and one is used in the Display Station (fixed node) to handle display, sensors, and Wi-Fi connectivity.
