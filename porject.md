# Voyager 1 and 2: Mission Analysis

## Overview
The twin Voyager spacecraft were launched in 1977 to explore the outer Solar System. Their primary mission was to study Jupiter and Saturn, including their rings and moons ([NASA](https://science.nasa.gov)). Using gravity-assist flybys, Voyager 2 later explored Uranus and Neptune. Together, the Voyagers returned data from four giant planets and 48 moons, discovering new moons, planetary rings, active volcanism on Io, Titan’s dense atmosphere, and strong magnetic fields. 

Voyager 1’s trajectory after Saturn placed it ~35° above the ecliptic, eventually making it the first human-made object to enter interstellar space (crossing the heliopause in 2012).

---

## 1. Spacecraft Structure and Specifications

### 1.1 Physical Design
- **Bus:** Ten-sided box carrying electronics, instruments, and subsystems.
- **Stabilization:** Three-axis stabilized using celestial references and gyros.
- **High-Gain Antenna (HGA):** 3.7 m diameter, aligned along z-axis for Earth communication.
- **Scan Platform:** Movable platform for pointing instruments independently of bus.

![Voyager Bus and Instrument Layout](https://science.nasa.gov/wp-content/uploads/2024/03/instruments-3.jpg)

#### 1.1.1 Dimensions and Mass
- Launch mass: ~722 kg (including fuel)
- Hydrazine for attitude control: 100 kg (75% used by 2012)
- RTGs mounted on a boom for thermal and radiation isolation

### 1.2 High-Gain Antenna (HGA)
- **Downlink Channels:**  
  - X-band (~8.4 GHz) for science and engineering data  
  - S-band (~2.3 GHz) for engineering telemetry  
- **Data Rates:** 7.2 kbps (X-band high-rate), 40 bps (S-band low-rate)

### 1.3 Command & Attitude Control Subsystems
- **CCS (Command Computer Subsystem):** Sequences operations, decodes commands, performs fault detection, manages antenna pointing.
- **AACS (Attitude and Articulation Control Subsystem):** Maintains orientation, controls maneuvers, positions scan platform. Uses hydrazine thrusters.

### 1.4 Power Subsystem: RTGs
- **Type:** 3 Radioisotope Thermoelectric Generators (RTGs)
- **Fuel:** Plutonium-238 dioxide (PuO₂)
- **Power Output:** ~225 W (2023)
- **Decay:** Exponential; selective instrument shutdown to conserve energy
- **Mounted on boom:** Reduces thermal/radiation interference

### 1.5 Optical Calibration Target
- Fixed flat target for in-flight calibration of cameras and instruments.

---

## 2. Payload and Scientific Instruments

### 2.1 Active Instruments (2025)
| Instrument | Voyager 1 | Voyager 2 | Principal Investigator |
|------------|-----------|-----------|----------------------|
| Cosmic Ray Subsystem (CRS) | Off (Feb 25, 2025) | On | Alan C. Cummings, Caltech |
| Low-Energy Charged Particles (LECP) | On | Off (Mar 24, 2025) | Stamatios M. Krimigis, JHU/APL |
| Magnetometer (MAG) | On | On | Adam Szabo, NASA GSFC |
| Plasma Wave Subsystem (PWS) | On | On | William Kurth, Univ. of Iowa |

### 2.2 Inactive Instruments (2025)
| Instrument | Voyager 1 | Voyager 2 |
|------------|-----------|-----------|
| Plasma Science (PLS) | Off (Feb 1, 2007) | Off (Sept 26, 2024) |
| Imaging Science Subsystem (ISS) | Off (Feb 14, 1990) | Off (Oct/Dec 1989) |
| Infrared Interferometer Spectrometer (IRIS) | Off (Jun 3, 1998) | Off (Feb 1, 2007) |
| Photopolarimeter Subsystem (PPS) | Off (Jan 29, 1980) | Off (Apr 3, 1991) |
| Planetary Radio Astronomy (PRA) | Off (Jan 15, 2008) | Off (Feb 21, 2008) |
| Ultraviolet Spectrometer (UVS) | Off (Apr 19, 2016) | Off (Nov 12, 1998) |

### 2.3 Instrument Objectives
- **CRS:** Energetic particle spectrum and cosmic ray origin/transport  
- **LECP:** Low-energy particle spectra, solar wind, planetary magnetospheres  
- **MAG:** Magnetic field measurements (planets, interplanetary)  
- **PWS:** Plasma waves and electric/magnetic fluctuations (10 Hz – 56 kHz)  
- **ISS:** Imaging planetary surfaces, rings, atmospheres  
- **IRIS:** Thermal mapping, elemental/compound composition  
- **PPS:** Light polarization to characterize particles in atmospheres and rings  
- **PRA:** Planetary radio emissions (20.4 kHz – 40.5 MHz)  
- **UVS:** UV spectroscopy to study atmospheric and interstellar composition  

---

## 3. Orbit and Trajectory

Voyagers are on **hyperbolic escape trajectories** following gravity assists:

\[
E = \frac{v^2}{2} - \frac{\mu}{r}
\]

- \(E>0\): Hyperbolic, unbound from the Sun  
- Escape velocity: \(v_\text{esc} = \sqrt{\frac{2\mu}{r}}\)  
  - 1 AU: 42.1 km/s  
  - 130 AU: 3.7 km/s  
- Voyager 1 speed: 17 km/s → confirms escape trajectory  
- Vis-viva equation: \(v^2 = \mu \left( \frac{2}{r} - \frac{1}{a} \right)\)  

### 3.1 Current Trajectories
- Voyager 1: ~164 AU, 35° inclination  
- Voyager 2: ~133 AU, 48° inclination  
- Hyperbolic, no fixed orbital period (period → ∞)

---

## 4. Communications and Earth-Space Link

- **Uplink:** S-band (~2.3 GHz)  
- **Downlink:** X-band (~8.4 GHz, nominal 160 bps)  
- **Ground Segment:** NASA Deep Space Network (DSN) – California, Spain, Australia

### 4.1 Link Budget
- **Friis Transmission Equation:**
\[
P_r = P_t \cdot G_t \cdot G_r \left( \frac{\lambda}{4 \pi R} \right)^2
\]
- Free-space path loss (dB):  
\[
L_\text{fs} = 20 \log_{10}\left( \frac{4 \pi R}{\lambda} \right)
\]

---

## 5. Power and Thermal Subsystems

### 5.1 Power Decay
\[
P(t) = P_0 e^{-\lambda t}, \quad \lambda = \frac{\ln 2}{T_\text{half}}
\]

### 5.2 Thermal Management
- Passive thermal control using multi-layer insulation
- Electrically-controlled louvers regulate heat radiation
- Stefan-Boltzmann law:
\[
Q = \epsilon \sigma A T^4
\]

---

## 6. Attitude and Orbit Control (AOCS)
- Three-axis stabilization
- Hydrazine thrusters for roll, pitch, yaw
- Angular momentum:
\[
H = I \cdot \omega
\]

---

## References
1. NASA Voyager Mission Overview: [https://science.nasa.gov/missions/voyager](https://science.nasa.gov/missions/voyager)  
2. Voyager Science Instruments: [NASA/JPL](https://voyager.jpl.nasa.gov/assets/images/galleries/voyager-spacecraft-diagram.jpg)  
3. Deep Space Network: [https://deepspace.jpl.nasa.gov](https://deepspace.jpl.nasa.gov)  

