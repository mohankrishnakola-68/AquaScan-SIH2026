# 🛠️ AquaScan-OBS: Hardware Bill of Materials (BOM) & Circuit Design

**Project**: Low-Cost Deployable Seafloor Metal Detection Sensor (PS ID: 26064)  
**Target Ministry**: Ministry of Earth Sciences (MoES) / NCPOR  
**Revision**: v1.2 — Prototype Proof-of-Concept & Production Architecture  

---

## 1. Complete Bill of Materials (BOM)

### Subsystem 1: Core Processing & Signal Acquisition
| Component Description | Exact Part Number | Key Specifications | Qty | Unit Cost (INR) | Supplier / Source |
| :--- | :--- | :--- | :---: | :---: | :--- |
| Main Controller MCU Board | **STM32H743VIT6** (Dev Board) | 480 MHz ARM Cortex-M7, 2MB Flash, 1MB RAM, Low Power Modes | 1 | ₹2,200 | DigiKey / Robu.in |
| Ultra-Precision 24-Bit ADC | **ADS1256** | 8-Ch, 30 kSPS Delta-Sigma ADC, SPI, Ultra-low noise (PGA up to 64x) | 1 | ₹1,450 | Texas Instruments |
| Precision Instrumentation Amp | **INA128P / AD8221** | Ultra-high input impedance ($10\ \text{G}\Omega$), $120\ \text{dB}$ CMRR, Low offset drift ($0.5\ \mu\text{V}/^\circ\text{C}$) | 2 | ₹900 | Analog Devices |
| High-Speed Op-Amp (TEM Buffer)| **OPA350 / AD8605** | 38 MHz Rail-to-rail, $5\ \text{pA}$ bias current, $<50\ \text{ns}$ settling | 2 | ₹480 | Texas Instruments |
| Fast Damping / Clamping Diodes | **1N4148W / BAS70** | Fast switching ($<4\ \text{ns}$ reverse recovery), Schottky barrier | 4 | ₹40 | Mouser / local |

### Subsystem 2: Sensor Payload
| Component Description | Exact Part Number | Key Specifications | Qty | Unit Cost (INR) | Supplier / Source |
| :--- | :--- | :--- | :---: | :---: | :--- |
| Custom Transient EM Coil | **AquaScan-TEM-Coil-100** | 32-gauge marine-grade enameled Cu wire, 150 turns, $L \approx 1.2\ \text{mH}$, $R \approx 3.8\ \Omega$, epoxy encapsulated | 1 | ₹1,200 | Custom In-House Fabrication |
| Non-Polarizable SP Electrodes | **Ag/AgCl Pellets (E206)** | Sintered Silver/Silver-Chloride, Ceramic porous liquid junction, $<0.5\ \text{mV}$ baseline drift | 2 | ₹2,800 | World Precision Instruments / E-store |
| High-Sensitivity Magnetometer | **PNI RM3100 / QMC5883L** | 3-Axis Geomagnetic Sensor, $13\ \text{nT}$ resolution, Low hysteresis | 1 | ₹1,850 | PNI Sensor Corp |
| Digital Ocean Depth / Pressure | **MS5837-30BA** | 30 bar ($300\ \text{m}$ depth), $0.2\ \text{mbar}$ resolution, Gel protection for saltwater | 1 | ₹3,200 | TE Connectivity / BlueRobotics |
| Water Temperature & Conductivity| **Analog EC-Probe v2** | Graphite/Titanium electrodes, NTC 10k thermistor, 0–50,000 µS/cm | 1 | ₹1,950 | DFRobot |
| Redox / ORP Industrial Electrode | **Industrial ORP-Pro** | Platinum ring sensor, $-2000\ \text{mV to }+2000\ \text{mV}$ range | 1 | ₹2,400 | DFRobot / Robu |

### Subsystem 3: Ballast Release Mechanism (Galvanic Burn-Wire)
| Component Description | Exact Part Number | Key Specifications | Qty | Unit Cost (INR) | Supplier / Source |
| :--- | :--- | :--- | :---: | :---: | :--- |
| Power N-Channel MOSFET | **IRLZ44N / IRFB3077** | Logic-level gate, $60\ \text{V}, 50\ \text{A}, R_{DS(on)} < 0.02\ \Omega$ | 1 | ₹75 | Infineon |
| Optocoupler Isolator | **PC817 / 4N35** | 5 kV galvanic isolation between MCU and burn-wire current loop | 1 | ₹30 | Sharp / Vishay |
| Sacrificial Burn-Wire Element | **Nichrome 80 (0.4 mm)** | Tensile strength $>15\ \text{kg}$, electrolytic dissolution in seawater $<180\ \text{s}$ at $350\ \text{mA}$ | 50 m spool | ₹350 | Local Metallurgy |
| Current Sense Shunt Resistor | **WSL2512 $0.1\ \Omega\ 1\%$** | Low inductance current monitoring for burn-wire confirmation | 1 | ₹65 | Vishay Dale |
| Fail-Safe Magnesium Anode | **Mg Galvanic Timed Link** | Passive electrolytic dissolution (12-hour fail-safe backup release) | 1 | ₹150 | Marine Zinc/Mg Co. |

### Subsystem 4: Recovery Beacon & Surface Telemetry
| Component Description | Exact Part Number | Key Specifications | Qty | Unit Cost (INR) | Supplier / Source |
| :--- | :--- | :--- | :---: | :---: | :--- |
| Long-Range LoRa Transceiver | **EBYTE E22-900T22D** | Semtech SX1262, $868/915\ \text{MHz}, +22\ \text{dBm}$, up to 12 km range | 1 | ₹1,100 | EBYTE |
| High-Sensitivity GNSS Receiver | **u-blox NEO-M8N** | Concurrent GPS/GLONASS/Galileo, $-167\ \text{dBm}$ tracking, active patch antenna | 1 | ₹1,250 | u-blox |
| High-Intensity Recovery Strobe | **Cree XP-L V6 + Constant Current Driver** | 1000 Lumens white flash, visible up to 4 nautical miles at night | 1 | ₹650 | Cree LED |

### Subsystem 5: Power Management & Enclosure
| Component Description | Exact Part Number | Key Specifications | Qty | Unit Cost (INR) | Supplier / Source |
| :--- | :--- | :--- | :---: | :---: | :--- |
| Deep-Cycle Battery Pack | **LiFePO4 4S 12.8V 6000mAh** | Safe chemistry, 2000+ cycles, BMS included, operating temp $0^\circ\text{C}$ to $45^\circ\text{C}$ | 1 | ₹3,400 | E-bike battery makers |
| High-Efficiency Step-Down Buck | **LM2596 / MP2307** | Step-down 12.8V to 5V (System Rail), 92% efficiency | 1 | ₹180 | Texas Instruments |
| Ultra-Low-Noise LDO Regulator | **TPS7A4700 / LM3940** | Ultra-clean $\pm 5\text{V}$ and $3.3\text{V}$ for 24-bit ADC ($4.17\ \mu\text{V}_{RMS}$ noise) | 2 | ₹350 | Texas Instruments |
| PoC Pressure Hull Assembly | **Hard Anodized 6061-T6** | $110\ \text{mm}$ OD, $8\ \text{mm}$ wall thickness, O-ring dual seal face, rated for 50 bar | 1 | ₹9,500 | CNC Machine Shop |
| Buoyancy Collar & Syntactic Foam| **Closed-Cell PVC / Polyurethane**| High density buoyancy ring ($+3.5\ \text{kg}$ positive net displacement) | 1 | ₹3,200 | Marine Composite |
| Connectors & Penetrator Ports | **M10 SubConn Compatible** | 4-pin & 6-pin wet-mate penetrators with nitrile O-rings | 3 | ₹2,400 | BlueRobotics / SubConn |

### 💰 Total System BOM Cost
* **Proof-of-Concept (PoC) Unit Cost**: **₹38,240 (~$455 USD)**  
* **Production Run (Batch of 50 units)**: **₹22,500 (~$270 USD)**  
*(Compared to commercial ocean landers at ₹50,00,000+, AquaScan achieves >99% capex reduction).*

---

## 2. Circuit Schematics & Operational Principles

### 1. Transient Electromagnetic (TEM) Induction Driver
```
 +12.8V Rail
     │
     ├───[ Flyback Clamping Diode: Fast Schottky ]────┐
     │                                                │
     ├───[ Damping Resistor: Rd = 470 Ω ]─────────────┤
     │                                                │
     └───[ Transmitter Coil: 150 Turns, 1.2 mH ]──────┤
                                                      │ (Drain)
                                                ┌─────┴─────┐
                                                │  IRLZ44N  │ (N-MOSFET)
                                                │   Switch  │
     Gate Drive Signal (MCU GPIO) ──[100 Ω]─────┤           │
                                                └─────┬─────┘
                                                      │ (Source)
                                                     GND
     
     Decay Signal Pick-up:
     Coil Tap ──[ Clamping Diodes to ±3.3V ]──► [ OPA350 Buffer ] ──► [ ADS1256 24-bit ADC ]
```
* **How it works**:
  1. The MCU pulses the MOSFET gate ON for $10\ \text{ms}$, charging the coil with a stable magnetic field.
  2. The MOSFET is snapped OFF in $<2\ \mu\text{s}$.
  3. The sudden collapse induces eddy currents in the surrounding medium.
  4. Saltwater eddy currents dissipate within $0\text{ to }15\ \mu\text{s}$.
  5. The ADC samples from $t = 30\ \mu\text{s}\text{ to }10\ \text{ms}$. If metallic nodules are present, their high internal electrical conductivity causes an exponential voltage decay whose amplitude and decay time constant $\tau$ are proportional to nodule density.

---

### 2. Self-Potential (SP) Redox Anomaly Detector
```
  [ Seafloor Ag/AgCl Electrode ] ────────[ 10k LPF ]─────(+) IN
                                                              │   [ INA128P ]
                                                              ├─── Instrumentation Amp ──► ADS1256
                                                              │   (Gain = 50x)
  [ Reference Ag/AgCl Electrode ] ───────[ 10k LPF ]─────(-) IN
  (Positioned 1.0 m higher on pod)
```
* **Why this is critical for MoES/NCPOR**:
  - Hydrothermal massive sulphide bodies act as spontaneous natural geobatteries, generating vertical dipole electrical currents.
  - The potential difference between seafloor sediment and ambient seawater reaches up to $-200\ \text{mV}$ near active or relict sulfide deposits.
  - The INA128 instrumentation amplifier provides $>10\ \text{G}\Omega$ input impedance, preventing any current drain on the electrodes and measuring microvolt-level anomalies cleanly.

---

### 3. Galvanic Burn-Wire Ballast Release Circuit
```
 +12.8V Power Rail
     │
     └───[ Current Limiting Power Resistor: 25 Ω, 20W ]───┐
                                                          │
                                         [ Nichrome 80 Burn-Wire Link ]
                                         (Holding Ballast Plate in Sea)
                                                          │
                                                          │ (Cathode in Seawater)
                                                    ┌─────┴─────┐
                                                    │  IRLZ44N  │
  MCU Trigger Pin ──[ Optocoupler PC817 ]───────────┤  MOSFET   │
                                                    └─────┬─────┘
                                                          │
                                                  [ 0.1 Ω Shunt ]
                                                          │
                                                         GND
```
* **Operational Cycle**:
  1. During the survey, the ballast weight (8 kg cast iron) is held mechanically by the loop of Nichrome wire.
  2. Once the mission timer expires (e.g., 2 hours on seabed), the MCU energizes the optocoupler, turning on the MOSFET.
  3. Current flows from the wire through the conductive seawater electrolyte to the titanium cathode.
  4. Rapid anodic oxidation dissolves the 0.4 mm wire within 150 seconds.
  5. The ballast drops away, and positive net buoyancy ascends the pod to the surface.
