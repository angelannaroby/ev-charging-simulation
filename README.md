# EV Charging Demand Simulator

A simulation and visualization tool for modeling **electric vehicle (EV) charging demand** and analyzing power usage patterns over time.

🔗 **Live Demo:** https://angelannaroby.github.io/reonic-ev-charging-simulation/

---

## Overview

This project simulates the behavior of multiple EV charging stations over time to estimate:

- Total energy consumption (kWh)
- Theoretical maximum power demand (kW)
- Actual peak demand (kW)
- Concurrency factor (utilization efficiency)

The simulation is based on probabilistic models of:
- Vehicle arrival patterns throughout the day  
- Charging demand distributions  

These inputs allow analysis of **realistic load behavior vs theoretical capacity**, which is critical for infrastructure planning and grid optimization.

---

## Simulation Logic

The core simulation is implemented in:

```
src/lib/simulation.ts
```

### Key characteristics:

- Simulates **N chargepoints** (default: 20)
- Charging power per point: **11 kW**
- Time resolution: **15-minute intervals**
- Duration: **1 year (35,040 ticks)**

### Behavior modeled:

- Probabilistic EV arrivals based on time-of-day distributions  
- Charging demand sampled from predefined probability distributions  
- Each chargepoint handles one vehicle at a time  
- Vehicles leave immediately after charging completes  

### Outputs computed:

- Total energy consumption  
- Theoretical max demand (`chargepoints × power`)  
- Actual peak demand  
- Concurrency factor (actual / theoretical)

---

## Approach & Assumptions

### Time-based probability handling

The input distribution defines **hourly arrival probabilities**, while the simulation runs in **15-minute steps**.

To maintain consistency:
- Hourly probabilities are converted into **per-tick probabilities**
- This ensures the expected number of arrivals remains statistically correct

### Deterministic simulation

The simulation optionally supports:
- **Seeded randomness** for reproducibility
- Enables consistent results across runs (useful for testing and comparison)

---

## Frontend Visualization

A lightweight UI is provided to interact with the simulation and explore results.

### Features:

- Configure simulation parameters:
  - Number of chargepoints  
  - Charging power  
  - Energy consumption  
  - Arrival probability multiplier  

- Visualize:
  - Load profiles over time  
  - Peak demand behavior  
  - Aggregate energy consumption  

- Interactive charts built using **Recharts**

---

## Tech Stack

- **React + TypeScript**
- **Vite**
- **Tailwind CSS**
- **Recharts**

The UI is intentionally kept **simple and minimal**, focusing on clarity and usability rather than heavy abstractions.

---

## Running Locally

```bash
npm install
npm run dev
```

---

## What This Project Demonstrates

- Modeling real-world systems using **probabilistic simulation**
- Translating domain requirements into **scalable TypeScript logic**
- Building **interactive data visualizations**
- Designing clean, maintainable frontend architecture

---

## Future Improvements

- Support multiple charger types (e.g., 11kW, 22kW, fast chargers)
- Persist simulation scenarios (backend integration)
- Compare multiple simulation runs
- Advanced analytics (distribution insights, variance, trends)
