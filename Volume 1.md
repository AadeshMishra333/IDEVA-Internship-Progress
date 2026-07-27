# Volume 1: Reliable Embedded System Software Base

**Goal:** Blank laptop ➔ Working embedded charger foundation

---

## 📌 Technical Prerequisites & Core Concepts

* **Programming Language:** C Programming
* **Digital Electronics:** Basic GPIO logic
* **Target Hardware Architecture:** Texas Instruments (TI) F28379D microcontroller
* **Interrupt Model:** Interrupt Service Routines (ISR) execution flow

---

## 🏗️ Stage 1: Hardware Blocks & Data Flow

### 1. Microcontroller (TI F28379D)
A system-on-chip that interacts directly with power hardware. Executes compiled C code (`main()`), manages internal peripherals, and processes hardware interrupts.

### 2. General Purpose Input/Output (GPIO)
Controllable digital pins for signal switching:
* **Output Mode:** High (3.3V) / Low (0V) — e.g., `GPIO_WritePin(LED, 1);`
* **Input Mode:** Digital state sensing (Buttons, Switch status)
* **Application in Charger:** Relay control, cooling fan control, status/debug LEDs, fault signal lines.

### 3. Universal Asynchronous Receiver-Transmitter (UART)
Serial communication protocol used primarily for logging, firmware debugging, and telemetry output to a PC terminal.

### 4. Analog-to-Digital Converter (ADC)
Converts continuous real-world analog signals into discrete digital values for firmware processing (e.g., $1.65\text{ V} \rightarrow 2048$ digital counts on a 12-bit ADC).
* **Application:** Measures critical system parameters including voltage, current, and temperature telemetry (serves as the primary data feed for AI feature extraction).

### 5. Pulse-Width Modulation (PWM)
High-speed digital pulse generation used to drive power electronics components.
* **Application:** Controls MOSFET gate signals, power converters, output charging current, and charging voltage levels.

### 6. Timers & Task Scheduler
* **Timers:** On-chip hardware clocks generating precise tick intervals.
* **Scheduler:** Deterministic task manager executing firmware functions at dedicated periodic slots (`1ms`, `10ms`, `100ms`, `1s`).

### 7. Interrupt Service Routine (ISR)
High-priority event handler.
* **ADC ISR Rule:** Must remain extremely short and deterministic. Collect data, store values to memory, and exit immediately. **Avoid blocking calls like UART prints within the ISR.**

### 8. Fault System & Safety Interlocks
Emergency protection logic triggered upon safety threshold violations:
* **Fault Types:** Over-Voltage Protection (OVP), Over-Current Protection (OCP), Over-Temperature Protection (OTP), CAN Timeout, Sensor Failures.
* **Safety Sequence:** $\text{Fault Detected} \longrightarrow \text{Disable PWM} \longrightarrow \text{Open Relays} \longrightarrow \text{Safe State}$

### 9. Controller Area Network (CAN)
High-reliability differential communication bus managing data exchange between the charger firmware and the Battery Management System (BMS).

---

### 🔄 Telemetry & Control Data Flow

```text
[ Sensor ] ──> [ ADC ] ──> [ Firmware ] ──> [ Scheduler ] ──> [ Control Logic ] ──> [ PWM ] ──> [ Charger ]
```
---

## 🛠️ Stage 2: Development Environment

*(To be documented)*

---

## 🔌 Stage 3: Peripheral Understanding

*(To be documented)*

---

## ⏱️ Stage 4: Scheduler Architecture

*(To be documented)*

---

## 🛡️ Stage 5: Fault Protection System

*(To be documented)*
