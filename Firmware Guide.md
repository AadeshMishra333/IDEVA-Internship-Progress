# Firmware Guide

A comprehensive learning roadmap covering the firmware development volumes for battery management and charging logic.

---

## 📌 Core Learning Objectives

### 🎯 Must Learn
* **Charging Modes:** Constant Current (CC) & Constant Voltage (CV) charging logic
* **BMS Basics:** Battery Management System fundamentals, telemetry reports (voltage, temperature, current limits, State of Charge (SOC)), and CAN bus communication
* **State of Charge (SOC):** Estimation and tracking
* **Battery Thermal Dynamics:** Temperature monitoring and management

### 💡 Nice to Know
* Li-ion chemistry characteristics
* Cell balancing methods
* Internal resistance measurements
* Battery aging mechanisms & degradation

---

## 📚 Volume Breakdown

### **Volume 1: Reliable Embedded System Software Base**
> **Goal:** Build a robust and reliable embedded software baseline.

* **Development Setup:**
  * Code Composer Studio (CCS)
  * C2000Ware library integration
  * Project structure and architecture
* **Hardware Interfaces:**
  * GPIO, UART, ADC, PWM
* **Task Scheduler:**
  * Multi-rate periodic execution (`1ms`, `10ms`, `100ms`, `1s` intervals)
* **Fault Handling:**
  * Over-current, over-voltage, over-temperature protection
  * CAN communication timeout monitoring

---

### **Volume 2: Real Charger Logic & AI Feature Engineering**
> **Goal:** Implement control algorithms, state machines, and firmware-level feature generation for embedded AI models.

* **State Machine States:**
  * `BOOT` ➔ `SELFTEST` ➔ `WAIT_BMS` ➔ `PRECHARGE` ➔ `START_PFC` ➔ `START_PSFB` ➔ `CC` ➔ `CV` ➔ `COMPLETE` ➔ `FAULT`
* **Power Stage Control:**
  * **PFC (Power Factor Correction):** Regulates DC bus voltage between 390V – 410V
  * **PSFB (Phase-Shifted Full-Bridge):** Controls charging output to the battery
* **Battery Interaction:**
  * CAN handshake protocols
  * Reading telemetry (status, maximum current limits, target voltage, temperature)
* **Charging Algorithms & Thermal Control:**
  * CC and CV state execution
  * Dynamic thermal derating (reducing charging current as temperature rises)
* **AI Integration:**
  * Firmware periodically generates relevant telemetry features to feed an embedded AI model.

---

### **Volume 3: Commercial Product Layer & On-Device AI**
> **Goal:** Add production-grade hardware features, diagnostics, and on-device AI integration.

* **Display UI:**
  * Real-time status, temperature readings, and charge data output
* **EEPROM Storage:**
  * Calibration data, system logs, runtime statistics, and AI parameters
* **Diagnostics:**
  * Self-test routines, manufacturing testing mode, and service mode
* **On-Device AI Layer:**
  * Persistent storage support for **AI Parameters**, **AI Model Version**, and **AI Risk Scores**
  * *Note:* Indicates a lightweight, embedded on-device AI implementation rather than cloud dependency.
