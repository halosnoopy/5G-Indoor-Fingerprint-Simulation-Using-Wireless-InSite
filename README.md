# 5G-Indoor-Fingerprint-Simulation-Using-Wireless-InSite

## Overview
This project presents a simulation-based framework for generating **5G fingerprint datasets** using **Wireless InSite**, a high-fidelity ray-tracing simulator.  
The goal is to build realistic datasets for indoor positioning and localization research by modeling multipath propagation, antenna patterns, and 3D indoor structures under realistic 5G scenarios.

The repository includes:
- **Wireless InSite simulation setups** for dataset generation,  
- **Processed fingerprint data** (RSRP, RSSI, AoD, etc.),  
- **MATLAB scripts** for extracting, loading, and transforming data for machine learning algorithms.

---

## Motivation
Accurate indoor positioning is essential for emerging **5G-enabled IoT and smart-building systems**.  
Real-world fingerprint collection is expensive and inconsistent due to environmental changes and multipath fading.  
This work proposes a **simulation-driven method** to overcome these challenges by using **Wireless InSite** to generate realistic radio fingerprints under controlled parameters, ensuring reproducibility and scalability.

---

## Simulation Framework (Wireless InSite)
The dataset was generated using **Wireless InSite 3D ray-tracing** with the following configuration:

| Parameter | Description |
|------------|-------------|
| **Scenario** | Multi-floor indoor office environment |
| **Carrier frequency** | 3.5 GHz |
| **Transmitter (TX)** | 8×8 MIMO array, directional beamforming |
| **Receiver (RX)** | Half-wave dipole antenna |
| **Reflections / Transmissions / Diffractions** | 6 / 4 / 1 |
| **Diffuse Scattering** | Enabled |
| **Receiver grid spacing** | ≈ 3 m |
| **Simulation output** | RSRP, RSSI, AoD, CIR, delay spread |

Each simulation exports **Receiver Summary Statistics** and **MIMO Channel Data** as CSV/TSV files, forming the raw dataset for further processing.

---

## Dataset Description
Two primary datasets are provided:

1. **Single-Slot Fingerprint Dataset**  
   Each record represents one receiver location’s fingerprint at a single time slot.

2. **Time-Series Fingerprint Dataset**  
   Contains sequences of fingerprints for each receiver location across multiple time steps, capturing signal fluctuations and temporal dynamics.

### Key Features
| Feature | Description |
|----------|-------------|
| `x, y, z` | Receiver coordinates (m) |
| `RSRP_i` | Reference signal received power from TX_i |
| `RSSI_i` | Received signal strength indicator |
| `AoD_i` | Angle of departure |
| `DelaySpread` | Channel delay spread |
| `PowerDelayProfile` | Aggregated power-delay features |

---
## Simulation and Data Description

### Simulation Files (`simulation/`)
The `simulation/` folder contains all necessary files and settings to run the **Wireless InSite** simulation.  
It is a **ready-to-run setup** for generating 5G indoor fingerprints.

- The configuration includes the full study area, transmitter/receiver placement, antenna parameters, and propagation settings.
- To execute the simulation, you must have **Wireless InSite installed** and a **valid software license**.
- Once opened in Wireless InSite, simply run the project to regenerate the raw signal data.

> Note: Wireless InSite is a licensed software by Remcom. A valid license is required to modify or re-run the simulation.

---

### Data Files (`data/`)
The `data/` folder contains datasets generated from the Wireless InSite simulation.  
It is organized as follows:

├── sim1/ # Raw data directly exported from the simulation

├── sim2/, sim3/, ... # Additional runs (for building time-series fingerprints)

├── AoD/ # Files extracted by getaod.m

├── features/ # Feature data extracted by getfeatures.m

├── getaod.m # Extracts the AoD data from raw simulation results.

├── getfeatures.m # Extracts the signal features (e.g., RSRP, RSSI, path delay) from simulation files.

├── aodprocess.m # Utility function used by `getaod.m` for processing AoD-related parameters.

├── rsprocess.m # Utility function used by `getfeatures.m` for RSS/RSRP data transformation. 

├── fulldata.m # Assembles the full dataset for machine learning

