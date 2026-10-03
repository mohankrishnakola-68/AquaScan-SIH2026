# 📘 AquaScan-OBS: Complete Technical Documentation & System Specification
### Low-Cost Deployable Seafloor Metal Detection Sensor for Ocean Resource Exploration

**Smart India Hackathon (SIH) 2026 | Hardware Edition**  
* **Problem Statement ID**: 26064  
* **Organization**: Ministry of Earth Sciences (MoES)  
* **Department**: National Centre for Polar and Ocean Research (NCPOR)  
* **Category**: Hardware  
* **Theme**: Robotics and Drones  
* **Team**: AquaScan  
* **Project Name**: AquaScan-OBS (*Ocean-Bottom Sensor*)  

---

# TABLE OF CONTENTS
1. [Executive Summary & Problem Statement](#1-executive-summary--problem-statement)
2. [Deep Ocean Exploration Challenges & Bottlenecks](#2-deep-ocean-exploration-challenges--bottlenecks)
3. [Proposed Solution Architecture (AquaScan-OBS)](#3-proposed-solution-architecture-aquascan-obs)
4. [Target Marine Mineral Deposits & Geology](#4-target-marine-mineral-deposits--geology)
5. [Multi-Modal Geophysical Sensing Principles](#5-multi-modal-geophysical-sensing-principles)
6. [Hardware & Circuit Design Breakdown](#6-hardware--circuit-design-breakdown)
7. [Failsafe Ballast Release Mechanism (Galvanic Burn-Wire)](#7-failsafe-ballast-release-mechanism-galvanic-burn-wire)
8. [Embedded Firmware & Autonomous State Machine](#8-embedded-firmware--autonomous-state-machine)
9. [Mathematical & Physical Validation Equations](#9-mathematical--physical-validation-equations)
10. [Step-by-Step Video Demonstration & Testing Protocol](#10-step-by-step-video-demonstration--testing-protocol)
11. [Itemized Bill of Materials (BOM) & Cost Comparison](#11-itemized-bill-of-materials-bom--cost-comparison)
12. [Strategic Alignment & National Impact](#12-strategic-alignment--national-impact)
13. [Jury Defense & Frequently Asked Questions (FAQ)](#13-jury-defense--frequently-asked-questions-faq)

---

## 1. Executive Summary & Problem Statement

### The Problem Statement (PS ID: 26064)
> *"Design and develop a low-cost deployable ocean-bottom sensor that can be released from a research vessel during surveys to detect and map metal-rich seabed deposits, including polymetallic nodules, hydrothermal sulphides, cobalt-rich crusts and rare-earth-element-bearing sediments, providing a rapid and cost-effective tool for deep-ocean mineral exploration."*

### The Solution: AquaScan-OBS
**AquaScan-OBS** is an autonomous, deployable **"Drop-and-Pop" Seafloor Metal Detection Lander**. Designed to be released directly from oceanographic research vessels (such as *ORV Sagar Nidhi* or *RV Bharati*) during normal transit, AquaScan:
1. Free-falls to the seabed at **$1.4\ \text{m/s}$** anchored by an expendable ballast plate.
2. Conducts multi-modal geophysical sensing using **Transient Electromagnetic (TEM) Pulse Induction** and **Self-Potential (SP) Redox Electrochemistry**.
3. Employs onboard **time-gated signal processing** to eliminate conductive saltwater interference.
4. Releases its expendable ballast plate via a low-cost **electrolytic galvanic burn-wire link** in under 3 minutes.
5. Ascends to the surface under positive buoyancy at **$1.0\ \text{m/s}$** and broadcasts GPS coordinates and survey telemetry over **LoRa** to the vessel for rapid retrieval.

---

## 2. Deep Ocean Exploration Challenges & Bottlenecks

| Existing Method | Operational Constraint | Financial Cost |
| :--- | :--- | :--- |
| **Deep-Sea ROVs** (Remotely Operated Vehicles) | Requires vessel to remain stationary (dynamic positioning); tether cables snag easily on rugged hydrothermal chimneys; covers only a few hundred square meters per dive. | **₹35–₹50 Lakhs/day** in vessel charter costs. |
| **Deep-Rated AUVs** (Autonomous Underwater Vehicles) | Extremely high purchase price; limited battery life when fighting strong bottom currents; risk of total vehicle loss in complex seamounts. | **₹15–₹30 Crore** per vehicle. |
| **Commercial Ocean Bottom Nodes** (OBS / OBN) | Single-point recording; relies on expensive acoustic release transponders ($20k–$40k each); limited to small deployment numbers. | **₹50 Lakhs–₹1.2 Crore** per node. |
| **Surface Sonar / Bathymetry** | Can map seabed depth topography, but **cannot detect sub-bed metallic composition or ore grade**. | Blind to metal content beneath silt. |

### The Physical Challenge: Conductive Seawater Shielding
In air, electrical conductivity is $\sigma \approx 0\ \text{S/m}$. In the ocean, high salinity ($35\ \text{PSU}$) makes seawater an electrical electrolyte with conductivity:
$$\sigma_{\text{seawater}} \approx 3.8 \text{ to } 5.2\ \text{S/m}$$
Standard continuous-frequency metal detectors induce eddy currents in the surrounding seawater, which generate an overwhelming false signal that masks any underlying metallic deposits.

---

## 3. Proposed Solution Architecture (AquaScan-OBS)

### Operational Lifecycle:
```
[ 1. VESSEL DROP ]
  └── Ship drops AquaScan pods at 1–2 km intervals along survey transects without stopping.

[ 2. FREE-FALL DESCENT ]
  └── Pod descends at 1.4 m/s stabilized by hydrodynamic tail fins and an 8 kg cast-iron ballast plate.

[ 3. SEAFLOOR LOGGING ]
  └── Pressure transducer detects landing (velocity drops to zero).
  └── Controller executes survey routines:
      • 100 Hz Transient EM Pulse Induction excitation.
      • Delayed-gate sampling (captures metallic eddy current decay curve).
      • Differential Self-Potential (Ag/AgCl non-polarizable electrodes).
      • In-situ feature extraction & preliminary deposit classification.
      • Data logged to non-volatile SPI Flash / MicroSD.

[ 4. CONTROLLED BALLAST SEPARATION ]
  └── Mission timer expires (1 to 24 hours).
  └── MOSFET delivers 3.3V / 350 mA through sacrificial Nichrome 80 burn-wire link.
  └── Anodic dissolution severs the wire in ~150 seconds.
  └── Ballast plate drops away; pod achieves +3.2 kgf positive net buoyancy.

[ 5. ASCENT & TELEMETRY ]
  └── Pod rises at ~1.0 m/s to the ocean surface.
  └── Hydrostatic sensor detects surface atmospheric pressure (depth < 0.5 m).
  └── GPS acquires satellite fix; SX1262 LoRa broadcasts coordinates & survey summary.
  └── High-intensity Cree LED strobe flashes for visual night recovery by vessel crew.
```

---

## 4. Target Marine Mineral Deposits & Geology

AquaScan-OBS specifically targets the **three primary deep-sea mineral classes** prioritized by the **Ministry of Earth Sciences (MoES)** and **International Seabed Authority (ISA)**:

### 1. Polymetallic Nodules (PMN)
* **Occurrence**: Abyssal sediment plains at depths of 4,000 to 6,000 meters (specifically the **Central Indian Ocean Basin - CIOB**, where India holds a 75,000 sq. km exploration contract).
* **Composition**: Nickel ($\text{Ni}$), Copper ($\text{Cu}$), Cobalt ($\text{Co}$), and Manganese ($\text{Mn}$).
* **Physical Signature**: High internal electrical conductivity ($\sigma \sim 10^3\ \text{S/m}$) and moderate magnetic susceptibility.
* **Detection Method**: **Transient Electromagnetic (TEM) Inductive Decay**. Dense nodule fields prolong the secondary magnetic field relaxation time ($\tau > 50\ \mu\text{s}$).

### 2. Seafloor Massive Sulphides (SMS)
* **Occurrence**: Hydrothermal vents, volcanic arcs, and tectonic spreading ridges (such as the **Central and Southwest Indian Ridges**).
* **Composition**: Copper ($\text{Cu}$), Zinc ($\text{Zn}$), Gold ($\text{Au}$), Silver ($\text{Ag}$), and Lead ($\text{Pb}$).
* **Physical Signature**: Massive electronic conduction body bridging reducing seabed fluid and oxygenated ocean water, acting as a natural **geobattery**.
* **Detection Method**: **Self-Potential (SP) Redox Sensing**. Generates a spontaneous negative electric dipole anomaly of **$-20\text{ to }-250\text{ mV}$** relative to background seawater.

### 3. Cobalt-Rich Ferromanganese Crusts
* **Occurrence**: Flanks of underwater seamounts and guyots at depths of 800 to 3,000 meters.
* **Composition**: Cobalt ($\text{Co}$), Platinum ($\text{Pt}$), Tellurium ($\text{Te}$), and **Rare Earth Elements (REEs)** like Neodymium, Dysprosium, and Europium.
* **Physical Signature**: High remnant magnetization and distinct magnetic susceptibility contrast against host ocean basalt.
* **Detection Method**: **3-Axis Fluxgate Magnetometer** + TEM inductive response.

---

## 5. Multi-Modal Geophysical Sensing Principles

### A. Transient Electromagnetics (TEM) with Delayed-Gate Sampling
* **Why it works**:
  1. A low-resistance transmitter loop is energized with a steady direct current ($I_0 \approx 2.5\ \text{A}$), establishing a static magnetic dipole field.
  2. The current is abruptly shut off ($di/dt \to \infty$) within $<2\ \mu\text{s}$.
  3. By Faraday's Law, eddy currents are induced in both the surrounding seawater and the seabed mineral deposits.
  4. **The Time-Domain Separation**:
     * In seawater ($\sigma \approx 4.5\ \text{S/m}$), the eddy currents diffuse outward rapidly and dissipate within **$t < 15\ \mu\text{s}$**.
     * In metallic mineral nodules ($\sigma \gg 10^3\ \text{S/m}$), eddy currents circulate inside the conductive mineral matrices and decay exponentially:
       $$V_{\text{nodule}}(t) = V_0 e^{-t/\tau} \quad \text{where } \tau = \frac{L}{R} \propto \mu_0 \sigma r^2$$
  5. By initiating ADC integration after a **$35\ \mu\text{s}$ delay cutoff**, the seawater response has completely dropped below the noise floor, leaving **only the genuine metallic mineral signature**.

### B. Passive Self-Potential (SP) Redox Sensing
* Hydrothermal sulfide deposits act as natural geobatteries:
  * Upper zone (contact with cold, oxygenated ocean bottom water): **Cathodic reduction** ($O_2 + 4H^+ + 4e^- \to 2H_2O$).
  * Lower zone (anoxic, reducing hydrothermal fluid): **Anodic oxidation** ($FeS_2 + 8H_2O \to Fe^{2+} + 2SO_4^{2-} + 16H^+ + 14e^-$).
  * Electrons flow upward through the metallic sulfide ore body.
  * Ionic return current flows downward through the seawater, establishing a measurable negative potential at the seabed:
    $$\Delta V_{\text{SP}} = V_{\text{bottom}} - V_{\text{reference}} = -20\ \text{to } -250\ \text{mV}$$
* **Instrumentation**: Measured using two non-polarizable **sintered $Ag/AgCl$ electrodes** connected to an ultra-high input impedance ($>10\ \text{G}\Omega$) instrumentation amplifier. This process consumes **zero active electrical power**.

---

## 6. Hardware & Circuit Design Breakdown

### Subsystems Architecture:
1. **Processing Subsystem**:
   * Controller: **ESP32-S3 / STM32H743** (ARM Cortex-M7 at 480 MHz).
   * Functions: Generates microsecond pulse gates, samples 24-bit ADC over SPI, manages system state machine, and logs records to SD flash.
2. **Transient EM Analog Front-End**:
   * Power Switch: **IRLZ44N / IRFB3077 Power MOSFET** (logic-level gate drive, $R_{DS(on)} < 0.015\ \Omega$).
   * Clamping Circuit: Ultra-fast Schottky diodes (**1N4148 / BAS70**) clamp back-EMF inductive flyback spikes to safe logic rails ($\pm 3.3\text{V}$).
   * Preamplifier: **OPA350 / AD8605** high-speed rail-to-rail op-amp ($38\ \text{MHz}$ bandwidth, $<50\ \text{ns}$ settling).
   * Analog-to-Digital Converter: **ADS1256** (24-bit Delta-Sigma, up to $30\ \text{kSPS}$, SPI interface).
3. **Self-Potential Analog Front-End**:
   * Sensor: Dual **$Ag/AgCl$ sintered pellet electrodes** with porous ceramic liquid junctions.
   * Amplifier: **INA128P / AD8221** Precision Instrumentation Amplifier ($10\ \text{G}\Omega$ input impedance, $120\ \text{dB}$ CMRR, Gain = 50x).
4. **Hydrostatic Depth & Environmental Sensing**:
   * Depth Sensor: **TE Connectivity MS5837-30BA** (30 bar / 300 m rated, $0.2\ \text{mbar}$ resolution, gel-sealed titanium diaphragm).
5. **Surface Telemetry & Recovery Beacon**:
   * LoRa Transceiver: **EBYTE E22-900T22D (Semtech SX1262)**, $868/915\ \text{MHz}$, $+22\ \text{dBm}$ output, up to 15 km line-of-sight range.
   * GNSS: **u-blox NEO-M8N** concurrent GPS/GLONASS receiver with active patch antenna.
   * Visual Strobe: **Cree XP-L V6** high-intensity 1000-lumen LED flashing at 1 Hz.
6. **Pressure Hull & Enclosure**:
   * Material: **Hard-anodized 6061-T6 marine aluminum** or heavy-wall Borosilicate glass sphere.
   * Sealing: Dual radial Buna-N O-rings on machined end-caps, rated for 50 bar hydrostatic pressure for benchtop/shelf PoC testing.

---

## 7. Failsafe Ballast Release Mechanism (Galvanic Burn-Wire)

The #1 reason conventional ocean landers cost ₹50+ Lakhs is their reliance on acoustic release transponders ($20k–$40k USD) and ship-mounted hydrophone transceivers. 

AquaScan solves this using a **Controlled Electrolytic Burn-Wire Link**:

### Mechanism:
1. The 8 kg cast-iron ballast plate is held by a mechanical clamp secured under tension by a thin **0.4 mm Nichrome 80 / Copper sacrificial wire loop**.
2. When the survey cycle expires, the ESP32 activates an optocoupler-isolated MOSFET switch.
3. A direct current of **$3.3\ \text{V}$ and $350\ \text{mA}$** passes from the wire (anode) through the ambient seawater electrolyte to a cathode plate.
4. **Anodic Dissolution**: By Faraday's Law of Electrolysis, the metallic wire undergoes accelerated corrosion ($\text{Ni} \to \text{Ni}^{2+} + 2e^-$).
5. Within **$150\ \text{seconds}$**, the cross-sectional area of the wire decreases below the tensile yield point, snapping the link cleanly.
6. The ballast drops away, and the pod surfaces naturally.
7. **Passive Fail-Safe**: A secondary magnesium timed link dissolves naturally after 12 hours in seawater, guaranteeing recovery even if the battery dies.

---

## 8. Embedded Firmware & Autonomous State Machine

The firmware is implemented in C++ ([`firmware/aquascan_core.cpp`](firmware/aquascan_core.cpp)) using a deterministic Finite State Machine (FSM):

```
       [ STATE_BOOT_INIT ]
               │ (Hardware self-test & baseline calibration)
               ▼
     [ STATE_DESCENT_MONITOR ]
               │ (Monitors depth pressure; detects seafloor contact)
               ▼
      [ STATE_SEAFLOOR_SURVEY ] ◄────┐
               │                     │ (5-second bursts)
               ├──► Fire TEM Pulse   │
               ├──► Sample SP mV     │
               ├──► Classify Deposit │
               │                     │
               └──► Timer expired? ──┘
               │ (YES)
               ▼
     [ STATE_BALLAST_RELEASE ]
               │ (Energize burn-wire MOSFET for ~150s)
               ▼
      [ STATE_ASCENT_MONITOR ]
               │ (Depth decreasing; detects surface atmospheric pressure)
               ▼
      [ STATE_SURFACE_BEACON ]
               │
               ├──► Flash Cree Strobe LED at 1 Hz
               └──► Broadcast LoRa NMEA Telemetry every 10 seconds
```

---

## 9. Mathematical & Physical Validation Equations

### 1. Seawater Skin Depth vs. Frequency:
$$\delta = \sqrt{\frac{2}{\omega \mu_0 \sigma}} = \frac{1}{\sqrt{\pi f \mu_0 \sigma}}$$
* At $f = 100\ \text{kHz}$ (continuous metal detector): $\delta \approx 0.75\ \text{m}$ (*Severe dissipation*).
* At $f = 100\ \text{Hz}$ (AquaScan TEM repetition): $\delta \approx 23.7\ \text{m}$ (*High seabed penetration*).

### 2. Time-Gated Dissipation Separation:
* Seawater / Silt Eddy Response:
  $$V_{\text{water}}(t) \propto t^{-5/2} \quad (\text{decays below noise within } 15\ \mu\text{s})$$
* Conductive Nodule Response:
  $$V_{\text{nodule}}(t) = V_0 e^{-t/\tau} \quad (\tau > 50\ \mu\text{s})$$

### 3. Faraday Electrolytic Wire Dissolution Time:
$$t = \frac{m_{\text{crit}} \cdot z \cdot F}{I \cdot M}$$
* $m_{\text{crit}} = 0.042\ \text{g}$ (tensile failure threshold for 0.4 mm wire).
* $z = 2$, $F = 96485\ \text{C/mol}$, $I = 0.35\ \text{A}$, $M = 58.69\ \text{g/mol}$.
* **Theoretical Release Time**: **$t \approx 157\ \text{seconds (}\approx 2.6\ \text{minutes)}$**.

---

## 10. Step-by-Step Video Demonstration & Testing Protocol

When filming your working prototype demonstration:

### 1. Benchtop Equipment Setup:
* Transparent container filled with **saltwater ($35\ \text{g/L}$ NaCl)** representing marine salinity.
* Pulse Induction sensor coil submerged or positioned directly beneath the container.
* Metallic ore simulants (ferrous rocks, manganese nodule surrogates, brass/copper specimens).
* ESP32 controller with status LEDs and wiring connected to laptop via USB.

### 2. The Demonstration Sequence:
1. **Baseline Phase (Saltwater Only)**:
   * Show the coil running in the saltwater container.
   * Point to the Serial Monitor / Plotter: the decay signal drops to zero within the first sampling gate. **Zero false triggers from salt water!**
2. **Detection Phase (Introducing Ore Simulant)**:
   * Submerge the metallic ore sample near the coil in the saline tank.
   * Show the Serial Plotter: the decay waveform jumps and stretches into the delayed sampling window.
   * The ESP32 LED triggers indicating: **`VALID ORE ANOMALY CONFIRMED`**.
3. **Burn-Wire Mechanism Demonstration**:
   * Show a close-up of the thin sacrificial wire holding a small weight.
   * Apply the trigger: show tiny electrolytic bubbling on the wire in saline water until the weight releases.
4. **Mission Dashboard Ingestion**:
   * Show [`dashboard/index.html`](dashboard/index.html) running in Chrome.
   * Click **`+ Deploy New Node`** and display the real-time bathymetry heatmap and GeoJSON data export.

---

## 11. Itemized Bill of Materials (BOM) & Cost Comparison

| Subsystem Component | Commercial Ocean Lander / OBS | **AquaScan-OBS (Our Solution)** |
| :--- | :--- | :--- |
| **Acoustic Release Transponder** | ₹20,00,000 (\$24,000 USD) | **₹450** (Controlled Electrolytic Burn-Wire) |
| **Metal & Sulfide Sensors** | ₹18,00,000 (Commercial Fluxgate/TEM) | **₹8,450** (Custom Coil + Ag/AgCl SP Electrodes) |
| **Pressure Enclosure & Buoyancy**| ₹12,00,000 (Titanium Shell) | **₹12,700** (Anodized 6061-T6 + Syntactic Foam) |
| **Controller & Telemetry** | ₹5,00,000 (Proprietary Datalogger) | **₹6,000** (ESP32-S3 + ADS1256 + LoRa/GPS) |
| **Battery & Power Conditioning** | ₹3,00,000 (Pressure-balanced pack) | **₹3,800** (LiFePO4 4S 12.8V with BMS) |
| **Total System Cost** | **₹58,00,000+ (\$70,000+)** | **₹31,400 – ₹38,240 (~$450 USD)** |

**Cost Reduction**: **> 98.5% Capex Savings**, enabling oceanographic vessels to drop **150+ AquaScan pods** for the cost of a single commercial ocean-bottom lander!

---

## 12. Strategic Alignment & National Impact

* **Deep Ocean Mission (MoES / NCPOR)**: Directly accelerates exploration in the 75,000 sq. km Central Indian Ocean Basin (CIOB) allocated by the International Seabed Authority (ISA).
* **Critical Minerals & EV Revolution**: Pinpoints domestic reserves of Nickel, Cobalt, Copper, and Manganese, eliminating reliance on foreign supply chains.
* **Atmanirbhar Bharat**: Indigenous design, fabrication, and software eliminate dependence on imported deep-sea scientific hardware.
* **Minimal Environmental Impact**: Non-invasive passive and electromagnetic logging creates zero benthic sediment destruction compared to exploratory dredging.

---

## 13. Jury Defense & Frequently Asked Questions (FAQ)

### ❓ Q1: "Why does standard metal detection fail in seawater?"
> **Answer**: *"Seawater contains dissolved salts making it an electrical conductor ($\sigma \approx 4.5\ \text{S/m}$). In continuous AC detectors, seawater generates massive eddy current noise that masks mineral signals. AquaScan solves this using **Transient Electromagnetics with delayed time-gate sampling**: when our pulse shuts off, seawater eddy currents die down within $15\ \mu\text{s}$, while metallic nodules continue ringing past $50\ \mu\text{s}$. Sampling only in the delayed window makes seawater invisible."*

### ❓ Q2: "How do you recover the sensor without expensive acoustic releases or cables?"
> **Answer**: *"Commercial landers use acoustic releases costing ₹20+ Lakhs. AquaScan uses an **electrolytic galvanic burn-wire link**. An onboard circuit delivers a small $3.3\text{V}, 350\text{ mA}$ DC current into seawater, dissolving the sacrificial wire in under 3 minutes via anodic oxidation. The ballast weight drops, positive buoyancy surfaces the pod, and our GPS/LoRa beacon broadcasts its position for vessel net recovery."*

### ❓ Q3: "Can an ESP32 handle microsecond decay sampling?"
> **Answer**: *"The ESP32 runs dual cores at 240 MHz. For microsecond transient sampling, we interface a dedicated 24-bit Delta-Sigma ADC (ADS1256) running at 30 kSPS over high-speed hardware SPI with DMA, while an analog peak-detector/integrator circuit captures early-gate decay dynamics before MCU handoff."*
