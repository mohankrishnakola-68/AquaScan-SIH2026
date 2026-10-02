# 🌊 Prototyping & SIH Defense Strategy: AquaScan-OBS

This document details the core technical context, problem alignment, and defense strategy for **Team AquaScan** in **Smart India Hackathon 2026**.

---

## 🎯 Theme & Problem Statement Alignment

* **Problem Statement ID**: 26064
* **Problem Statement Title**: Low-Cost Deployable Seafloor Metal Detection Sensor for Ocean Resource Exploration
* **Organization**: Ministry of Earth Sciences (MoES)
* **Department**: National Centre for Polar and Ocean Research (NCPOR)
* **Category**: Hardware
* **Theme**: Robotics and Drones

### Strategic National Importance:
India has been allocated a 75,000 sq. km exploration area in the **Central Indian Ocean Basin (CIOB)** by the **International Seabed Authority (ISA)**. The Government of India’s **Deep Ocean Mission (Samudrayaan)** requires rapid, scalable prospecting tools to detect:
1. **Polymetallic Nodules (PMN)**: Abundant in Nickel, Copper, Cobalt, and Manganese.
2. **Hydrothermal Massive Sulphides (SMS)**: Copper-Zinc-Gold sea-vent deposits along the Central Indian Ridge.
3. **Cobalt-Rich Ferromanganese Crusts**: High-grade Rare Earth Elements (REEs) and Platinum-group metals.

---

## 🔬 Core Technological Innovation: Multi-Physics Fusion

### 1. The Seawater Electrical Attenuation Barrier
* **The Problem**: Seawater has a high electrical conductivity ($\sigma \approx 3.8 \text{ to } 5.2\ \text{S/m}$), causing severe attenuation for standard continuous-wave metal detectors.
* **The AquaScan Solution**: **Transient Electromagnetics (TEM) with Delayed-Gate Sampling**.
  - A primary current pulse is abruptly shut off ($di/dt \to \infty$).
  - Fast-diffusing eddy currents in conductive seawater dissipate within $t < 15\ \mu\text{s}$.
  - The high internal conductivity of metallic nodules sustains secondary eddy currents for $>50\ \mu\text{s}$.
  - Integrating the receiver signal between $35\ \mu\text{s} - 1.2\ \text{ms}$ effectively eliminates saltwater noise.

### 2. Natural Self-Potential (SP) Redox Detection
* Hydrothermal sulfide deposits act as natural geobatteries, setting up negative electrical dipole potentials ($-20\text{ to }-250\ \text{mV}$).
* A pair of non-polarizable **$Ag/AgCl$ electrodes** passively logs these anomalies without consuming active battery power.

### 3. Low-Cost Galvanic Burn-Wire Release Mechanism
* Commercial Ocean Bottom Seismographs/Nodes rely on **\$15,000 – \$35,000 acoustic release transponders**.
* AquaScan uses a **₹250 electrolytic sacrificial link**: applying a $3.3\text{V}, 350\text{ mA}$ DC current causes rapid anodic dissolution of a 0.4 mm Nichrome wire in 150 seconds, dropping the ballast plate for positive buoyancy ascent.

---

## 🛠️ Prototyping & Demonstration Roadmap

1. **Benchtop Proof-of-Concept (Current Stage)**:
   - Operating in a 35 PSU saltwater test tank using real metallic ore simulants.
   - ESP32 controller generating 100 Hz pulses and logging ADC waveforms.
   - Demonstration video linked in submission deck.
2. **Hyperbaric Chamber Testing (Phase 2)**:
   - Pressure housing hydrostatic test up to 50 bar (equivalent to 500 m depth).
3. **Coastal Sea Trials (Phase 3)**:
   - Shallow continental shelf deployment and recovery off Goa coast with oceanographic institutes.

---

## 👥 Hackathon Repository Structure
* `README.md` — Project Overview, System Architecture & Specifications
* `docs/SIH_Presentation_Deck.md` — Slide-by-slide pitch and presenter script
* `docs/Hardware_BOM_and_Circuit_Design.md` — Complete BOM with part numbers & schematics
* `docs/Scientific_Principles_and_Physics.md` — Theoretical equations & Maxwell modeling
* `firmware/aquascan_core.cpp` — Embedded FSM, TEM pulse generation & LoRa telemetry
* `simulation/seafloor_sensor_sim.py` — Python geophysical simulation engine
* `dashboard/index.html` — Interactive vessel mission control and seabed anomaly visualizer
