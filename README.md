# Productivity Bloom  
**Introduction to Robotics - Final Project**

Student: Alexandra Neamtu  
Faculty of Mathematics and Computer Science, University of Bucharest  
Academic Year: 2025-2026  

---

## 1. Project Overview

Productivity Bloom is a standalone smart productivity device designed as a tangible, interactive cube that transforms time management into a physical and gamified experience.

Instead of relying on traditional mobile applications that can be easily ignored, this project encourages users to engage with their productivity in a concrete, meaningful way. The system allows users to configure Focus and Break cycles through a web interface hosted directly on the device. These cycles are then controlled through physical interaction with the cube, creating a direct connection between real-world actions and digital feedback.

Progress is visualized through a virtual plant displayed on the integrated OLED screen. The plant grows whenever the user completes tasks and stays consistent with their Focus cycles. If daily goals are not met, the plant withers as a natural consequence. To bring it back to life, the user must perform a deliberate physical action: opening a small door in the cube to reveal a hidden photoresistor and shining a strong light on it. This design ensures that recovery requires real-world effort rather than a simple digital reset, reinforcing accountability in a tangible and engaging way.

---

## 2. Concept of Operation

The user interacts with Productivity Bloom in a continuous workflow rather than through isolated tasks.

Through the built-in web dashboard, the user sets two main parameters: Focus duration and Break duration. Once configured, the workflow is controlled entirely through the physical cube. Flipping the cube starts a Focus session, and the system automatically alternates between Focus and Break periods based on the chosen configuration.

The cycle repeats as many times as needed until the user decides that their work is finished. When a task is completed, the user must explicitly confirm it in the interface by checking a confirmation box next to that task. Only after this confirmation does the system allow the “Water Plant” action, which rewards the user by visually growing the virtual plant on the OLED display.

If the user does not complete all scheduled tasks for the current day, the virtual plant will wither automatically. This evaluation is synchronized using NTP (Network Time Protocol) to ensure accurate real-world timing. Every night at precisely 00:00, the system checks whether all tasks have been completed. If any remain unfinished, the firmware triggers the withered state, and this state is saved in non-volatile memory so that it persists even after a restart.

---

## 3. System Components and Their Roles

The entire system is built around a single ESP32 microcontroller that coordinates all hardware and software elements.

The ESP32 acts as the central brain of the device. It manages Wi-Fi communication, hosts the web interface, processes sensor data, renders animations on the OLED display, and executes the internal state machine. Its dual-core architecture allows networking tasks to run in parallel with real-time graphics and sensor monitoring.

An MPU6050 accelerometer and gyroscope module enables physical interaction with the cube. It detects orientation changes and allows the user to start or stop sessions simply by flipping the device.

A 1.5-inch OLED display with 128x128 resolution provides visual feedback. It shows the virtual plant, countdown timers, animations, and status messages, acting as the main emotional and informational interface of the system.

A light-dependent resistor (LDR) is used as a physical “revival mechanism.” If the plant has withered due to missed goals, the user must expose the sensor to a strong light source to bring the plant back to life. This design ensures that recovering from failure requires a real-world action.

The system is powered by a rechargeable Li-Po battery and a TP4056 charging module, making the cube completely portable and independent.

---

## 4. Bill of Materials (BOM)

| Component | Quantity | Notes |
|---------|---------|------|
| ESP32 DevKit V1 | 1 | Main microcontroller |
| Li-Po Battery 3.7V 2500mAh | 1 | Portable power source |
| TP4056 Charging Module (with protection) | 1 | Battery charging and protection |
| OLED Display 1.5" (128x128) | 1 | Main visual interface |
| MPU6050 Sensor | 1 | Motion detection |
| LDR Photoresistor | 1 | Light-based interaction |
| Buzzer | 1 | Audio feedback to notify the user when a Focus or Break session ends |
| Resistors | as needed | Exact quantity determined during prototyping |
| Capacitors | as needed | For power stabilization |
| Wires | as needed | Connections between components |
| ON/OFF Switch | 1 | Physical power control |
| Custom Cube Enclosure | 1 | Constructed from cardboard |

---

## 5. Weekly Productivity Analytics

In addition to real-time interaction, Productivity Bloom includes a long-term analytics component.

The system records every completed session and confirmed task locally on the ESP32. After seven days from the first recorded use, the dashboard generates a weekly report. This report calculates the user’s average productivity, displays performance trends across the week, and highlights the day on which the user was most productive.

This feature transforms the device from a simple timer into a personal habit-tracking assistant.

---

## Q1 - What is the system boundary?

The boundary of the system is local and physical. Productivity Bloom is designed as a completely self-contained embedded device that operates within the limits of the cube itself and the user’s local Wi-Fi network. All computation, decision-making, data storage, and visualization occur directly on the hardware. The user interacts with the system either through the physical cube or through the web dashboard served by the ESP32. No external cloud services are required for operation. The only outside interaction is an optional connection to an NTP server used solely for accurate timekeeping. From a functional perspective, the system begins and ends with the cube and the user interacting with it.

---

## Q2 - Where does intelligence live?

All intelligence in Productivity Bloom lives inside the ESP32 microcontroller. The firmware implements a complete internal state machine responsible for managing timers, evaluating task completion, processing sensor input, controlling animations, and making daily decisions about the plant’s state. Every important action and calculation is performed locally on the device. The web interface acts only as a presentation and configuration layer, allowing the user to send commands and visualize information. This edge-based architecture ensures privacy, responsiveness, and full functionality even without an internet connection.

---

## Q3 - What is the hardest technical problem?

The most challenging technical problem is coordinating multiple real-time responsibilities on a limited embedded platform. The ESP32 must handle sensor monitoring, OLED rendering, timing logic, WebSocket communication, and HTTP requests at the same time while running on battery power. These tasks compete for processing time and memory, and must be carefully scheduled to avoid blocking or instability. Achieving smooth animations without interrupting network communication, preventing brownout resets during Wi-Fi activity, and maintaining accurate timing across reboots all require careful architectural design. Balancing concurrency, power efficiency, and reliability represents the core engineering difficulty of the project.

---

## Q4 - What is the minimum demo?

A meaningful demonstration of Productivity Bloom focuses on its continuous Focus and Break cycle workflow. The user first opens the built-in dashboard and sets the desired Focus and Break durations. The cube is then flipped to begin the first Focus session. The OLED display immediately shows the active timer and the current state of the virtual plant. When the Focus period ends, the system automatically enters a Break period, and this alternating sequence continues repeatedly.

At any time, the user can decide that a task has been completed. To do this, they mark the confirmation checkbox next to that task in the interface. Only after this explicit confirmation does the system allow the “Water Plant” action. Pressing this button visibly grows the plant on the OLED display, rewarding the user for real progress.

To demonstrate the accountability mechanism, Demo Mode can be used to force the plant into a withered state. The plant can then be revived only through physical interaction with the LDR light sensor, proving the full loop between user behavior, hardware interaction, and software logic.

---

## Q5 - Why is this not just a tutorial project?

Productivity Bloom is a complete integrated system rather than a simple electronics exercise. It combines embedded firmware development, real-time multitasking, wireless networking, graphical rendering, persistent storage, and human-centered interaction design. Unlike typical tutorials that demonstrate an isolated sensor or module, this project implements a functional product intended for daily use. It requires careful system-level design, power management, data integrity, and user experience considerations. The result is not a basic demonstration but a cohesive device that meaningfully supports productivity habits.

---

## Do you need an ESP32?

Yes. The project fundamentally depends on the capabilities of the ESP32 platform. Hosting a web interface, maintaining WebSocket communication, processing sensor data, and rendering real-time graphics simultaneously require significantly more memory and processing power than basic microcontrollers can provide. The dual-core architecture, integrated Wi-Fi, and sufficient resources of the ESP32 make it the only practical choice for implementing Productivity Bloom as designed.
