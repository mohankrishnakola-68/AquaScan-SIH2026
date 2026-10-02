# 🔬 AquaScan-OBS: Scientific Principles, Geophysics & Mathematical Modeling

**Project**: Low-Cost Deployable Seafloor Metal Detection Sensor (PS ID: 26064)  
**Target Ministry**: Ministry of Earth Sciences (MoES) / NCPOR  
**Scope**: Theoretical validation for SIH Jury & Scientific Evaluators  

---

## 1. The Seawater Attenuation Problem & Why Standard Detectors Fail

In terrestrial metal detectors, air has an electrical conductivity $\sigma \approx 0\ \text{S/m}$. Consequently, electromagnetic signals travel without conductive dissipation. 

However, ocean water has an average salinity of $35\ \text{PSU}$, resulting in an electrolyte electrical conductivity of:
$$\sigma_{\text{seawater}} \approx 3.8 \text{ to } 5.2\ \text{S/m}$$

For a time-harmonic electromagnetic field of frequency $f = \frac{\omega}{2\pi}$, the skin depth $\delta$ (the depth at which field amplitude drops to $1/e \approx 37\%$) in a conductive medium is given by:

$$\delta = \sqrt{\frac{2}{\omega \mu \sigma}} = \frac{1}{\sqrt{\pi f \mu_0 \sigma}}$$

Where:
* $\mu_0 = 4\pi \times 10^{-7}\ \text{H/m}$ (Magnetic permeability of seawater, equal to free space)
* $\sigma = 4.5\ \text{S/m}$

### Skin Depth vs. Frequency in Seawater:
* At $f = 100\ \text{kHz}$ (typical terrestrial metal detector frequency):
  $$\delta \approx \frac{1}{\sqrt{\pi \times 10^5 \times (4\pi \times 10^{-7}) \times 4.5}} \approx 0.75\ \text{m}$$
  *Severe attenuation and immense phase shift prevent seabed penetration.*
* At $f = 100\ \text{Hz}$ (AquaScan TEM fundamental pulse repetition):
  $$\delta \approx \frac{1}{\sqrt{\pi \times 100 \times (4\pi \times 10^{-7}) \times 4.5}} \approx 23.7\ \text{m}$$

### The Transient Time-Domain Breakthrough
Rather than continuous AC waves, AquaScan uses **Transient Electromagnetics (TEM)**:
1. Current is driven through the transmitter loop to establish a steady magnetic field.
2. The current is abruptly shut off ($di/dt \to \infty$).
3. By Faraday's Law ($\nabla \times \mathbf{E} = -\frac{\partial \mathbf{B}}{\partial t}$), eddy currents are induced in both the seawater and the seabed deposits.
4. **Decay Separation**:
   - The seawater eddy current response diffuses outwards rapidly, decaying according to a fast power law:
     $$V_{\text{water}}(t) \propto t^{-5/2}$$
   - Metallic polymetallic nodules and sulfide ores have high internal conductivity ($\sigma_{\text{ore}} \sim 10^3 \text{ to } 10^6\ \text{S/m}$), creating an exponential decay with characteristic relaxation time:
     $$\tau = \frac{L_{\text{nodule}}}{R_{\text{nodule}}} \propto \mu_0 \sigma_{\text{nodule}} r^2$$
   - By beginning ADC integration after $t_{\text{delay}} > 35\ \mu\text{s}$, the seawater response has dropped below the noise floor, leaving **only the mineral deposit response**.

---

## 2. Geobattery Physics of Seafloor Massive Sulfides (Self-Potential)

Hydrothermal Massive Sulfide (SMS) deposits form at tectonic spreading centers (such as the Central and Southwest Indian Ridges, monitored by NCPOR). They consist of pyrite, chalcopyrite, and sphalerite.

### The Self-Potential (SP) Mechanism:
1. **Redox Gradient**:
   - The upper seafloor boundary contains cold, oxygen-saturated seawater ($E_h \approx +300\text{ to }+400\ \text{mV}$).
   - The underlying seabed sediment is anoxic and reducing ($E_h \approx -100\text{ to }-300\ \text{mV}$).
2. **Electronic Conduction through Ore**:
   - The massive sulfide body acts as a low-resistance electronic conductor bridging these two distinct chemical zones.
   - Electrons flow upward through the mineral body from the reducing sediment to the oxygenated ocean water.
3. **Electric Field in Seawater**:
   - Return ionic currents flow downward through the conductive seawater, establishing a negative dipolar electric potential on the seabed directly above the deposit:
     $$\Delta V_{\text{SP}} = V_{\text{seabed}} - V_{\text{reference}} = -20\ \text{mV to } -250\ \text{mV}$$

**AquaScan's SP Sensor**:
A vertical pair of non-polarizable $Ag/AgCl$ electrodes directly samples this potential difference:
$$\mathbf{E}_{\text{vertical}} \approx -\frac{\Delta V_{\text{SP}}}{\Delta z}$$
Because this signal is continuous, passive, and requires $0\ \text{W}$ to excite, AquaScan consumes minimal battery while logging massive sulfide anomalies.

---

## 3. Hydrodynamics & Ballast Release Mechanics

### 1. Terminal Descent Velocity:
During descent, the pod with ballast accelerates until hydrodynamic drag equals net submerged weight:
$$W_{\text{net}} = (m_{\text{pod}} + m_{\text{ballast}}) g - \rho_{\text{sw}} V_{\text{total}} g$$
$$F_D = \frac{1}{2} \rho_{\text{sw}} C_d A v_{\text{descent}}^2$$
Setting $W_{\text{net}} = F_D$:
$$v_{\text{descent}} = \sqrt{\frac{2 W_{\text{net}}}{\rho_{\text{sw}} C_d A}}$$
* With $m_{\text{total}} = 16\ \text{kg}$, $V_{\text{total}} = 11.2\ \text{L}$, $\rho_{\text{sw}} = 1025\ \text{kg/m}^3$, $C_d \approx 0.85$, $A = 0.038\ \text{m}^2$:
  $$v_{\text{descent}} \approx 1.35\ \text{m/s}$$
  *Descent to 500 m takes ~6 minutes; descent to 3,000 m takes ~37 minutes.*

### 2. Ascent Velocity Post-Ballast Release:
Upon releasing the 8 kg ballast:
$$B_{\text{net}} = \rho_{\text{sw}} V_{\text{pod}} g - m_{\text{pod}} g \approx +3.2\ \text{kgf} \approx 31.4\ \text{N}$$
$$v_{\text{ascent}} = \sqrt{\frac{2 B_{\text{net}}}{\rho_{\text{sw}} C_d A}} \approx 0.98\ \text{m/s}$$

---

## 4. Electrolytic Galvanic Dissolution Rate (Faraday's Law of Electrolysis)

The mass $m$ of sacrificial wire dissolved anodically is given by Faraday's Law:
$$m = \frac{I \cdot t \cdot M}{z \cdot F}$$

Where:
* $I = 0.35\ \text{A}$ (Trigger current applied by MCU circuit)
* $M = 58.69\ \text{g/mol}$ (Molar mass of Nickel in Nichrome)
* $z = 2$ (Valence state $\text{Ni} \to \text{Ni}^{2+} + 2e^-$)
* $F = 96485\ \text{C/mol}$ (Faraday constant)

For a wire diameter $d = 0.4\ \text{mm}$ and active exposed length $L = 5\ \text{mm}$:
* Mass required to breach critical tensile failure ($>80\%$ dissolution):
  $$m_{\text{crit}} \approx 0.042\ \text{g}$$
* Theoretical dissolution time $t$:
  $$t = \frac{m_{\text{crit}} \cdot z \cdot F}{I \cdot M} = \frac{0.042 \times 2 \times 96485}{0.35 \times 58.69} \approx 157\ \text{seconds (}\approx 2.6\ \text{minutes)}$$

This proves the physical feasibility of using a controlled low-current galvanic burn-wire to release an ocean-bottom lander rapidly and reliably.
