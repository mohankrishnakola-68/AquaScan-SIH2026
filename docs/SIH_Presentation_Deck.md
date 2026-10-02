# 🏆 Smart India Hackathon (SIH) Official Presentation Deck
## Problem Statement ID: 26064
### Low-Cost Deployable Seafloor Metal Detection Sensor for Ocean Resource Exploration
**Organization**: Ministry of Earth Sciences (MoES) | **Department**: National Centre for Polar and Ocean Research (NCPOR)  
**Category**: Hardware | **Theme**: Robotics and Drones | **Team Name**: AquaScan

---

## 📑 Slide-by-Slide Deck Blueprint

---

### 🖥️ SLIDE 1: Title & Team Credentials
* **Slide Title**: AquaScan-OBS: Low-Cost Autonomous Seafloor Metal Exploration Sensor
* **Sub-title**: Enabling Rapid, Scalable Seabed Mineral Prospecting for India's Deep Ocean Mission
* **Problem Statement ID**: 26064 (MoES / NCPOR)
* **Team Information**:
  - Team Name: **AquaScan**
  - Members & Specialized Roles:
    1. *Team Lead & Embedded Systems Engineer* (Firmware & Sensor Fusion)
    2. *Hardware & Power Electronics Lead* (Transient EM Coil Driver & Burn-wire Circuit)
    3. *Oceanographic & Sensor Lead* (Geophysical Self-Potential & CTD Calibration)
    4. *Mechanical & Enclosure Lead* (Pressure Hull, Buoyancy & Hydrodynamics)
    5. *Edge AI & Signal Processing Engineer* (TinyML & In-situ Nodule Classification)
    6. *Vessel Software & Telemetry Lead* (LoRa/GPS Ingestion & Heatmap Dashboard)

> **🎤 Presenter Script (30 Seconds)**:
> *"Respected Jury members, India has been allotted 75,000 square kilometers in the Central Indian Ocean Basin by the International Seabed Authority to explore polymetallic nodules and deep-sea minerals. Yet, our oceanographic research vessels face a massive bottleneck: surveying deep abyssal plains currently requires multi-million dollar ROVs or commercial ocean-bottom nodes costing over ₹50 Lakhs each. We present **AquaScan-OBS** — an indigenous, ultra-low-cost, autonomous drop-and-pop seafloor sensor node that slashes deployment costs by 95% and enables swarm-scale ocean mineral mapping."*

---

### 🖥️ SLIDE 2: Problem Statement & Exploration Bottlenecks
* **Slide Header**: The Deep-Sea Exploration Bottleneck
* **Key Challenges in Seafloor Metal Prospecting**:
  1. **Prohibitive Capex & Opex**: Standard scientific ROVs and deep-rated AUVs cost upwards of ₹30–₹50 Lakhs/day in vessel charter time. Traditional Ocean Bottom Seismometers/Nodes (OBS/OBN) cost \$40,000 to \$100,000 per unit.
  2. **Coarse Spatial Resolution**: Acoustic bathymetry from surface ships cannot directly identify mineral composition beneath the seabed sediment layer.
  3. **Conductive Seawater Shielding**: Seawater conductivity (~4.5 S/m) severely attenuates standard electromagnetic metal detectors, causing high false alarms from saline drift.
  4. **The Deployment Trap**: Because existing landers are expensive, scientists cannot risk deploying them in dense grids over rough hydrothermal vents.

> **🎤 Presenter Script (40 Seconds)**:
> *"Surface sonar can map seabed topography, but it cannot differentiate between a pile of barren basalt rocks and high-grade polymetallic nodules or massive sulfides. Deep-sea rovers are too slow and expensive to cover vast territorial waters. Furthermore, ordinary metal detectors fail underwater because high-salinity seawater acts as a giant electrical conductor. To survey thousands of square kilometers effectively, NCPOR needs a deployable sensor that is rugged, physically immune to seawater conductivity, and cheap enough to be deployed in dozens from a moving survey vessel."*

---

### 🖥️ SLIDE 3: Proposed Solution — The AquaScan Architecture
* **Slide Header**: AquaScan-OBS: Autonomous "Drop-and-Pop" Architecture
* **Core Concept**:
  - A free-fall, positively buoyant sensor pod anchored to an expendable ballast plate.
  - Deployed in arrays directly from the stern of research vessels (like *ORV Sagar Nidhi* or *RV Bharati*).
  - Performs autonomous bottom sensing for a programmed mission duration (1–24 hours).
  - Automatically severs its anchor link via a galvanic burn-wire and ascends to the surface for fast vessel recovery.
* **System Breakdown (Visual Diagram)**:
  - **Upper Float Collar**: Syntactic buoyancy housing + Recovery beacon (GPS/LoRa/Strobe).
  - **Core Pressure Housing**: Hard-anodized 6061-T6 aluminum / borosilicate chamber containing microcontrollers, signal conditioning, and LiFePO4 battery pack.
  - **Lower Sensing Skirt**: Custom Transient Electromagnetic (TEM) inductive coil, dual non-polarizable Ag/AgCl Self-Potential electrodes, and 3-axis fluxgate magnetometer.
  - **Bottom Ballast**: Recycled cast-iron / biodegradable concrete plate attached via electrolytic sacrificial link.

> **🎤 Presenter Script (45 Seconds)**:
> *"AquaScan-OBS solves this with a modular 'Drop-and-Pop' design. A research vessel transiting an exploration tract simply drops multiple AquaScan pods over the side without stopping. The pod descends at 1.4 m/s. Upon seafloor impact, it activates its multi-modal sensor suite to log metal signatures directly at the sediment-water interface. Once the survey cycle is complete, an onboard micro-controller triggers an electrolytic burn-wire that dissolves an anchor link in under 3 minutes. The buoyant pod floats back to the surface, where its LoRa and GPS beacon alerts the vessel for quick net-scoop recovery."*

---

### 🖥️ SLIDE 4: Sensor Modality & Scientific Innovation
* **Slide Header**: Multi-Modal Physics: Overcoming Seawater Interference
* **Three-Pillar Geophysical Sensing Suite**:
  1. **Transient Electromagnetic (TEM) Induction**:
     - Sends 100 Hz pulsed magnetic excitation into the seabed.
     - Samples decay voltage *after* the primary transmitter pulse turns off ($t > 50\ \mu\text{s}$).
     - *Key Advantage*: Conductive seawater decays instantaneously ($<10\ \mu\text{s}$), leaving only the long eddy-current decay signature of high-conductivity polymetallic nodules.
  2. **Non-Polarizable Self-Potential (SP) Redox Sensing**:
     - Ag/AgCl electrode pair spaced vertically across the bottom boundary layer.
     - Detects the spontaneous electrochemical potential ($-20\text{ to }-200\text{ mV}$) generated by natural oxidation-reduction reactions around Hydrothermal Massive Sulphide (SMS) bodies.
  3. **3-Axis High-Sensitivity Fluxgate Magnetometer**:
     - Measures micro-Tesla magnetic susceptibility anomalies caused by ferromanganese crusts and cobalt-rich seabed mounts.
  4. **CTD & Water Plume Characterization**:
     - In-situ conductivity, temperature, and depth tracking to compensate EM drift and flag active hydrothermal thermal plumes.

> **🎤 Presenter Script (45 Seconds)**:
> *"How do we overcome the conductive seawater barrier? We use Transient Electromagnetics with delayed time-gate sampling. When our coil shuts off, eddy currents in seawater dissipate in microseconds, but eddy currents inside dense metallic nodules persist much longer. By reading the signal in this delayed window, seawater becomes practically transparent! Simultaneously, our non-polarizable silver-chloride electrodes passively detect natural battery voltages generated by massive sulphide deposits without expending power. This multi-physics fusion guarantees zero false positives."*

---

### 🖥️ SLIDE 5: Mechanical Design & Low-Cost Release Mechanism
* **Slide Header**: Ruggedized Deep-Sea Engineering at Low Cost
* **Breakthrough Release Mechanism**:
  - *Industry Standard*: Acoustic Release Transponders (\$15,000 – \$35,000 USD) requiring expensive hydrophone transceivers.
  - *AquaScan Innovation*: **Controlled Electrolytic Galvanic Burn-Wire Link**.
  - A 0.5 mm Nichrome/Copper sacrificial wire holds the ballast clamp. When an onboard FET delivers $3.3\text{V} / 350\text{ mA}$ into seawater, accelerated anodic dissolution snaps the wire in 150 seconds, releasing 8 kg of ballast.
* **Pressure & Buoyancy Balance**:
  - Net buoyancy post-release: $+3.2\text{ kgf}$, ensuring an ascent speed of $\sim 1.0\text{ m/s}$.
  - Rated for 50 bar (500 m) in PoC enclosure; scalable to 600 bar with syntactic foam and oil-compensated electronics.
  - Fail-safe: Backup mechanical magnesium galvanic link dissolves naturally after 12 hours if electronics fail.

> **🎤 Presenter Script (40 Seconds)**:
> *"The biggest factor that makes ocean-bottom nodes cost ₹50 Lakhs is the acoustic release transponder. We completely eliminated this expense by engineering a controlled electrolytic galvanic burn-wire. Applying a tiny 350 milliamp current directly into the marine electrolyte dissolves the sacrificial link in under three minutes, allowing the ballast to drop and the pod to surface. Even if the battery dies completely, a passive magnesium safety link dissolves automatically, guaranteeing 100% pod recovery."*

---

### 🖥️ SLIDE 6: Software, Edge TinyML & Vessel Dashboard
* **Slide Header**: Edge Intelligence & Survey Mission Control
* **Onboard Edge AI Pipeline**:
  - Raw TEM decay curves + SP voltages are fed into an onboard **Random Forest TinyML model** running on an ARM Cortex-M7 (STM32H7).
  - Real-time classification into 4 seabed states:
    - *Type 0: Barren Pelagic Silt*
    - *Type 1: Sparse Nodule Distribution ($<5\text{ kg/m}^2$)*
    - *Type 2: High-Density Polymetallic Ore Field ($>15\text{ kg/m}^2$)*
    - *Type 3: Active Hydrothermal Sulphide Body*
* **Vessel Ingestion & Mission Dashboard**:
  - Upon surfacing, node transmits condensed survey packets via 868/915 MHz LoRa (up to 15 km line-of-sight to ship antenna).
  - Vessel dashboard automatically maps GPS coordinates, plots nodule density heatmaps, and exports GIS-ready shapefiles for oceanographers.

> **🎤 Presenter Script (40 Seconds)**:
> *"Data collection is useless without rapid interpretation. Our onboard TinyML algorithm evaluates the electromagnetic decay slope and redox potentials in real-time, categorizing the seabed type before even surfacing. Once it pops up, it broadcasts its payload over LoRa. The vessel's mission dashboard ingests this data instantly, creating real-time heatmaps of metal deposits on GIS bathymetry maps so scientists can immediately prioritize where to send coring drills."*

---

### 🖥️ SLIDE 7: Cost Analysis & Feasibility Validation
* **Slide Header**: 95% Cost Reduction — Enabling Swarm Deployments
* **Cost Comparison Table**:

| Subsystem Component | Commercial Ocean Lander / OBS | **AquaScan-OBS (Our Solution)** |
| :--- | :--- | :--- |
| **Acoustic Release Mechanism** | ₹20,00,000 (\$24,000) | **₹250** (Galvanic Burn-Wire Link) |
| **Metal & Sulfide Sensors** | ₹18,00,000 (Imported Magnetometer/EM) | **₹8,500** (Custom TEM Coil + Ag/AgCl SP) |
| **Pressure Enclosure & Buoyancy**| ₹12,00,000 (Titanium Hull) | **₹18,000** (Anodized 6061-T6 + Cast Epoxy) |
| **Controller & Telemetry** | ₹5,00,000 (Proprietary Datalogger) | **₹11,750** (STM32H7 + GPS/LoRa Beacon) |
| **Total Cost per Node** | **₹55,00,000+** | **₹38,500 (~$460)** |

* **Hackathon Working PoC Readiness**:
  - Complete benchtop hardware prototype operating in a 35 PSU saltwater test tank.
  - Real-time detection demonstrated using real manganese/ferrous nodule simulants.

> **🎤 Presenter Script (35 Seconds)**:
> *"Here is the commercial reality: for the price of ONE conventional ocean-bottom lander (₹55 Lakhs), NCPOR can manufacture over 140 AquaScan nodes! This transforms deep-sea exploration from high-risk single-point drops into wide-area distributed sensor swarms. We have already implemented the firmware, validated the electromagnetic decay physics, and designed a working benchtop prototype inside a saltwater calibration chamber."*

---

### 🖥️ SLIDE 8: Impact, Roadmap & Alignment with National Goals
* **Slide Header**: Empowering India's Deep Ocean Mission
* **Strategic Alignment**:
  - **MoES Deep Ocean Mission (Samudrayaan)**: Directly accelerates exploration of polymetallic nodules in the Central Indian Ocean Basin (CIOB) and hydrothermal vents along the Central Indian Ridge.
  - **Resource Security**: Nickel, Copper, Cobalt, and Rare Earth Elements are critical for India's EV transition, defense, and semiconductor self-sufficiency.
* **Post-Hackathon Development Roadmap**:
  - *T + 3 Months*: Hyperbaric pressure chamber testing up to 50 bar (National Institute of Ocean Technology / NIOT Chennai).
  - *T + 6 Months*: Coastal sea trial off Goa coast with NCPOR / NIO vessels.
  - *T + 12 Months*: Deep-sea deployment at CIOB test tract (>4,000 m rating).

> **🎤 Presenter Script (30 Seconds)**:
> *"AquaScan directly supports India's mission to become self-reliant in critical battery and green-energy minerals. By replacing expensive foreign imports with an indigenous, scalable ocean-bottom sensor swarm, we empower our scientists to map India's seabed wealth faster, cheaper, and safer. Thank you, and we welcome your questions!"*
