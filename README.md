# Smart IoT Datalogger

## 1. Project Overview

This project is a **proof-of-concept ESP32-based modular datalogger** designed to demonstrate end-to-end IoT system development, from embedded hardware to cloud data handling.

The system targets **field data acquisition scenarios**, where sensor data must be reliably collected, stored locally, and transmitted wirelessly for monitoring and analysis.  
It emphasizes **modularity**, allowing different sensors and communication methods to be integrated depending on deployment requirements.

Key objectives of this project include:
- Designing a flexible embedded platform based on ESP32
- Supporting both **local data logging** and **remote data transmission**
- Demonstrating structured firmware design for real-world IoT use
- Understanding hardware, power, and communication trade-offs

This project is **not production-ready** and is documented as a learning-focused proof-of-concept.  
Some implementation details are intentionally generalized to respect confidentiality.

---

## 📸 Hardware & Prototype

<img width="2160" height="1141" alt="3D_SDL_GW_REV1 0_2026-01-17 (1)" src="https://github.com/user-attachments/assets/0fc514fb-9cb0-40a2-b652-c031a025355c" />

<img width="794" height="588" alt="image" src="https://github.com/user-attachments/assets/42a7ae66-f00d-4e16-9dce-94fc359e5d13" />

## 2. System Architecture

The ESP32 Modular Datalogger is designed using a **layered architecture**, separating sensing, processing, storage, communication, and backend components.  
This structure improves modularity, simplifies debugging, and allows individual components to be replaced or extended with minimal changes.

At a high level, the system flow is:

**Sensors → ESP32 MCU → Local Storage (SD Card) → Wireless Communication → Server / Dashboard**

---

### 📐 Architecture Diagram

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/80d4cef5-7f4f-41ea-854f-7288d37b0943" />

## 3. Hardware Design

The hardware design of the ESP32 Modular Datalogger focuses on **flexibility, reliability, and ease of integration** for different sensing and communication requirements.  
The system is designed as a **core controller with modular peripherals**, allowing sensors and communication modules to be added or changed with minimal redesign.

---

### 🧠 Core Controller

- **MCU:** ESP32  
- Selected for its integrated Wi-Fi, multiple peripheral interfaces, and strong community support  
- Provides sufficient processing capability for sensor polling, data logging, and communication handling  

Key reasons for choosing ESP32:
- Multiple UART, I2C, and SPI interfaces
- Adequate flash and RAM for IoT applications
- Low-power modes suitable for battery-operated systems

---

### 🔌 Sensor & I/O Interfaces

The hardware supports multiple **sensor and control interfaces** to maintain modularity
and compatibility with industrial devices.

- **Analog Inputs**  
  Used for sensors requiring ADC measurements such as voltage, current,
  or analog transducers.

- **Digital Inputs (DI)**  
  Designed for status or event detection, such as dry contacts,
  switches, or alarm signals.

- **Digital Outputs (DO)**  
  Used for simple control actions, including relay activation
  or external device triggering.

- **I2C Interface**  
  Shared digital bus for sensors such as environmental,
  pressure, or industrial monitoring modules.

- **RS-485 (Modbus RTU)**  
  Supported via UART for communication with industrial
  sensors and devices using Modbus RTU protocol.

- **UART Interface**  
  Reserved for serial-based peripherals or communication modules
  when RS-485 is not required.

---

### 📸 Hardware Design Images

<img width="901" height="642" alt="image" src="https://github.com/user-attachments/assets/8874f59f-1682-433d-82f1-90873ce634fc" />

<img width="986" height="720" alt="image" src="https://github.com/user-attachments/assets/84949710-4717-4d11-b529-e5673780f28f" />

## 5. Communication & Backend Integration

The ESP32 Modular Datalogger supports **remote data transmission** to a backend system for monitoring, storage, and basic visualization.  
The communication design focuses on **reliability, simplicity, and flexibility**, allowing different connectivity options depending on deployment constraints.

---

### 📡 Communication Methods

The system is designed to support multiple communication technologies, selectable based on use case:

- **LoRa**
  - Used for long-range, low-power data transmission
  - Suitable for remote or low-bandwidth deployments
  - Payload size optimized for sensor data

- **GSM (Cellular)**
  - Used where LoRa infrastructure is unavailable
  - Enables direct communication with cloud servers via mobile networks

- **Wi-Fi**
  - Primarily used for development, testing, or local deployments

Only one communication method is active per configuration to reduce complexity and power consumption.

---

### 🌐 Backend Integration

The backend system receives data using lightweight and commonly adopted protocols:

- **HTTP POST**
  - Simple REST-based data submission
  - Easy integration with custom servers or IoT platforms

- **MQTT**
  - Publish-based data delivery
  - Suitable for near real-time monitoring applications

Received data is:
- Parsed on the server
- Stored in a simple database structure
- Used for basic visualization and analysis

---

### 📊 Data Storage & Visualization

- Sensor data is stored in a **structured database format**
- Time-series data enables historical analysis
- A lightweight dashboard provides:
  - Basic charts
  - Status monitoring
  - Data inspection for debugging and validation

#### Database View (phpMyAdmin)
<img width="1624" height="458" alt="image" src="https://github.com/user-attachments/assets/5105491e-9e17-4193-866e-064929a766de" />


#### Simple Dashboard View
<img width="1307" height="361" alt="image" src="https://github.com/user-attachments/assets/bd925805-650f-498e-972f-6b066ae1fe30" />

> Dashboard implementation is intentionally kept simple and is not production-grade.

---

### 📸 Communication & Dashboard Images

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/1e86970c-4f0d-414e-8915-5b0430bb8f81" />

Overall, this project reinforced the importance of **building reliable foundations** before optimizing for performance or scalability in IoT applications.
