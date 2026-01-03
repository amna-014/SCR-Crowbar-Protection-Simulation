# Design & Simulation of SCR Crowbar Protection

> **Analysis of High-Speed Overvoltage Protection Mechanisms using Multisim.**

[![Simulation](https://img.shields.io/badge/Tool-NI_Multisim-blue)]()
[![Component](https://img.shields.io/badge/Switch-SCR_C106D-red)]()
[![Threshold](https://img.shields.io/badge/Zener-7.5V-yellow)]()

## Project Abstract
This project focuses on the **Circuit Design and Simulation** of a Crowbar Circuit—a failsafe mechanism used to protect sensitive biomedical loads (like microcontrollers) from power surges.

While the physical prototype verified the concept, this repository documents the **Theoretical Validation** and **Threshold Analysis**. Using **NI Multisim**, we modeled the transient response of a Zener-triggered SCR system to ensure it isolates the load before damage occurs.

## Circuit Design Parameters
[cite_start]The design was calculated to protect a 14.4Ω Load (Bulb) from voltages exceeding 7.5V[cite: 393, 410].

| Component | Selected Value | Design Rationale |
| :--- | :--- | :--- |
| **Zener Diode** | 7.5V | [cite_start]Sets the precise breakdown voltage for the trigger[cite: 395]. |
| **Thyristor (SCR)** | C106D (4A Max) | [cite_start]Chosen to handle the short-circuit surge current (>1A)[cite: 404]. |
| **Fuse** | 1 Amp | [cite_start]Selected to blow immediately when SCR shorts the rail[cite: 387]. |
| **Pull-Down Resistor** | 1 kΩ | [cite_start]Prevents false triggering of the Gate pin[cite: 406]. |

## Simulation Analysis (Multisim)
[cite_start]The circuit was simulated under three voltage conditions to verify the "Crowbar" effect[cite: 413, 426].

### 1. Normal Operation (< 7.5V)
* **Input:** 5V DC
* **Status:** The Zener diode acts as an open circuit. The SCR Gate is pulled Low (0V).
* **Result:** Current flows normally to the load.

### 2. Threshold Breached (> 7.5V)
* **Input:** 10V DC (Simulated Surge)
* **Status:** Zener breakdown occurs. Voltage at SCR Gate exceeds trigger threshold.
* **Result:** SCR latches ON, creating a low-impedance path to Ground.

### Simulation Screenshots
| Normal Condition | Fault Condition (Before Fuse) | Fault Condition (Safe State) |
| :---: | :---: | :---: |
| ![Normal](https://github.com/amna-014/SCR-Crowbar-Protection-Simulation/blob/main/normal%20condition.jpg?raw=true) | ![Overvoltage 1](https://github.com/amna-014/SCR-Crowbar-Protection-Simulation/blob/main/overvoltage%20condition%201.jpg?raw=true) | ![Overvoltage 2](https://github.com/amna-014/SCR-Crowbar-Protection-Simulation/blob/main/overvoltage%20condition%202.jpg?raw=true) |
| *Input: 5V (System Active)* | *Input: 10V (SCR Triggered)* | *Fuse Blown (Load 0V)* |

> [cite_start]*Figure 1: Multisim results showing Voltage Drop across the load falling to near-zero (0.27V) during a fault condition[cite: 472].*

## Threshold Verification Results
[cite_start]Based on simulation and hardware comparison[cite: 427]:

| Input Voltage ($V_{in}$) | Fuse Status | Load State |
| :--- | :--- | :--- |
| **4.0 V** | Intact | ON (Protected) |
| **5.0 V** | Intact | ON (Protected) |
| **7.2 V** | **BLOWN** | **OFF (Safe)** |

> [cite_start]*"The simulation confirmed that the C106D SCR successfully shunts the current within milliseconds, protecting the 14.4Ω load from high-voltage transients[cite: 477]."*

## Project Team
This project was a collaborative effort for the **Power Electronics** module.

* **Amna Yousuf** (@amna-014) - *Circuit Analysis & Simulation Lead*
* **Shahmeer Hussain** (@shahmeeerx) - *Hardware Prototyping & Assembly*

---
*© 2026 Dept. of Biomedical Engineering, SSUET.*
