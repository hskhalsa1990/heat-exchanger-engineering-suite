# Heat Exchanger Complete Engineering Suite (Upgraded)

**Shell-and-Tube · Plate · Finned-Tube · Transient · Fouling (Kern–Seaton) · ML · Uncertainty · Sensitivity · Optimization · Predictive Maintenance · Fleet · Nanofluids · Economics · PDF Reports**

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Fully self-contained industrial Jupyter notebook for thermal design, fouling prediction, predictive maintenance and economic optimization of heat exchangers.

**Flat structure** – all files in one folder (easy on phone).

---

## Quick Start

```bash
pip install -r requirements.txt
jupyter notebook Heat_Exchanger_Complete_Suite_Executed.ipynb
```

Or just open the executed notebook – all results and figures are already inside.

---

## System Architecture

```mermaid
flowchart TB
    subgraph INPUT["📥 Inputs"]
        A[Process Conditions<br/>m, cp, T_in]
        B[Geometry<br/>n_tubes, L, OD]
        C[Sensor / Historian CSV<br/>Rf, ΔP, U, efficiency]
    end

    subgraph CORE["⚙️ Core HX Models"]
        D[Shell-Tube HX]
        E[Plate HX]
        F[Finned-Tube HX]
        G[LMTD / ε-NTU<br/>Overall U]
    end

    subgraph ANALYSIS["📊 Analysis Modules"]
        H[Transient Response]
        I[Monte-Carlo Uncertainty]
        J[Sensitivity Ranking]
        K[Design Optimization]
    end

    subgraph FOULING["🧪 Fouling & ML"]
        L[Kern–Seaton Model]
        M[Random Forest]
        N[XGBoost]
        O[1d / 7d / 30d Forecast]
    end

    subgraph PM["🛡️ Predictive Maintenance"]
        P[Anomaly Detection<br/>Isolation Forest]
        Q[Health Index 0–100]
        R[RUL Estimation]
        S[Early Warnings<br/>GREEN / YELLOW / RED]
    end

    subgraph OUTPUT["📤 Outputs"]
        T[Fleet Dashboard]
        U[What-If Simulator]
        V[Economic Cleaning Interval]
        W[PDF Management Report]
        X[Nanofluid Impact]
        Y[ΔP · Pumping · CAPEX · Exergy]
        Z[TEMA Helper]
    end

    A --> CORE
    B --> CORE
    C --> FOULING
    CORE --> G
    G --> ANALYSIS
    G --> FOULING
    FOULING --> PM
    ANALYSIS --> OUTPUT
    PM --> OUTPUT
```

---

## Predictive Maintenance Workflow

```mermaid
flowchart LR
    A[Daily Sensors<br/>Rf · ΔP · U · Eff] --> B[Feature Engineering<br/>lags · dRf]
    B --> C{ML Ensemble<br/>RF + XGBoost}
    C --> D[1-day Rf]
    C --> E[7-day Rf]
    C --> F[30-day Rf]
    D --> G[Health Index]
    E --> G
    F --> G
    G --> H{Status}
    H -->|≥ 80| I[🟢 GREEN<br/>Normal]
    H -->|55–80| J[🟡 YELLOW<br/>Plan cleaning]
    H -->|< 55| K[🔴 RED<br/>Clean ASAP]
    G --> L[RUL days]
    L --> M[Recommended Actions]
```

---

## Fouling → Decision Logic

```mermaid
stateDiagram-v2
    [*] --> Clean: Start / After cleaning
    Clean --> MildFouling: Rf rising
    MildFouling --> Elevated: Rf > 70% critical
    Elevated --> NearCritical: Rf > 90% critical
    NearCritical --> Critical: Rf ≥ Rf_CRIT
    Critical --> Clean: Chemical / mechanical cleaning

    MildFouling --> Clean: Early intervention
    Elevated --> Clean: Planned maintenance
    NearCritical --> Clean: Urgent window

    note right of Critical
        ΔP high
        Efficiency low
        Health Index < 40
    end note
```

---

## Data Flow (Plant → Report)

```mermaid
flowchart TD
    A[Plant Historian / SCADA] -->|CSV export| B[hx_fleet_sample.csv]
    B --> C[load_hx_csv]
    C --> D[Per-asset Health Index<br/>RUL · Status]
    D --> E[Fleet Ranking<br/>worst first]
    E --> F[PDF Report]
    E --> G[Operator Dashboard]
    C --> H[ML Retrain optional]
    H --> D
```

---

## Module Overview

```mermaid
mindmap
  root((HX Suite))
    Core Models
      Shell-Tube
      Plate
      Finned-Tube
      LMTD / ε-NTU
    Dynamics
      Transient lag
      Step response
    Fouling
      Kern–Seaton
      Synthetic data
      RF + XGBoost
    Uncertainty
      Monte-Carlo
      Sensitivity
    Optimization
      Max Q
      Constraints
    Predictive Maint.
      Anomaly
      Health Index
      RUL
      Warnings
    Fleet
      Multi-asset
      Priority ranking
    Extras
      Nanofluids
      Economics
      What-If
      PDF Report
```

---

## Files in this folder

| File | Description |
|------|-------------|
| `Heat_Exchanger_Complete_Suite_Upgraded.ipynb` | Clean source notebook |
| `Heat_Exchanger_Complete_Suite_Executed.ipynb` | Fully executed notebook (all outputs) |
| `01_…09_….png` | All diagrams, charts & 3D schematic |
| `hx_fleet_sample.csv` | Sample multi-asset historian data |
| `HX_Predictive_Maintenance_Report.pdf` | Auto-generated management report |
| `requirements.txt` | Python dependencies |
| `LICENSE` | MIT |
| `USAGE.md` | Short usage notes |
| `hx_results_summary.csv` | Quick numeric summary export |
| `hx_design_summary.txt` | Text design sheet |
| `17_…18_….png` | Parametric sweeps, cleaning strategies |
| `12_…16_….png` | F-chart, axial profiles, TEMA Rf, Q–A curve, tube layout |

---

## Diagrams & Charts

### 1. 3D Shell-and-Tube Schematic
![3D Shell-and-Tube](06_3d_shell_tube_schematic.png)

### 2. Steady-State Performance Comparison
![Steady-State Comparison](01_steady_state_comparison.png)

Heat duty, effectiveness (ε) and overall heat-transfer coefficient (U) for three industrial configurations under identical process conditions.

### 3. Transient Step Response
![Transient Response](02_transient_response.png)

First-order lag response of hot-fluid outlet temperature after a step change in inlet temperature.

### 4. ML Fouling Prediction (Random Forest)
![Fouling ML](03_fouling_ml_prediction.png)

Parity plot, feature importance and fouling resistance growth curves vs water hardness.

### 5. Monte-Carlo Uncertainty Propagation
![Monte-Carlo](04_monte_carlo_uncertainty.png)

Distributions of heat duty and effectiveness under parameter uncertainty (±10 % on U, flows, temperatures, area).

### 6. Local Sensitivity Ranking
![Sensitivity](05_sensitivity_analysis.png)

Percentage change in heat duty for a ±10 % variation of each design / process parameter.

### 7. Degradation & Pressure-Drop Tracking (180 days)
![Degradation Tracking](07_degradation_tracking.png)

Evolution of fouling resistance (Rf), thermal efficiency, pressure drop (ΔP) and overall U.

### 8. Composite Equipment Health Index (0–100)
![Health Index](08_health_index.png)

Single operator-friendly score combining fouling, ΔP, efficiency and anomaly score.

### 9. Multi-HX Fleet Monitoring
![Fleet Monitoring](09_fleet_monitoring.png)

Side-by-side fouling trends, health-index snapshot and remaining useful life (RUL) for the fleet.

### 10. Multi-Objective Snapshot (Q vs CAPEX vs ΔP + Exergy)
![Multi-Objective](10_multiobjective_snapshot.png)

Heat duty versus equipment cost and pressure drop, plus second-law (exergy) efficiency comparison.

### 11. Nanofluid Pumping Power Impact
![Nanofluid Pumping](11_nanofluid_pumping.png)

How increasing nanoparticle volume fraction raises viscosity and therefore pumping power.

### 12. LMTD Correction Factor F Chart
![F Chart](12_LMTD_F_chart.png)

1 shell-pass / 2 tube-pass F-chart approximation (Bowman-style).

### 13. Axial Temperature Profiles
![Axial Profiles](13_axial_temperature_profiles.png)

Counter-flow vs parallel-flow temperature profiles along the exchanger length.

### 14. TEMA Recommended Fouling Factors
![TEMA Rf](14_TEMA_fouling_factors.png)

Selected TEMA fouling resistances by fluid service.

### 15. Q–Area Design Curve
![Q vs Area](15_Q_vs_Area_design_curve.png)

Heat duty versus required area at different overall U values.

### 16. Tube-Sheet Layout Sketch
![Tube Layout](16_tube_sheet_layout.png)

Simple 2-D triangular-pitch tube-sheet visualisation.

### 17. Parametric Sweeps
![Parametric Sweeps](17_parametric_sweeps.png)

Heat duty vs hot-side flow, inlet temperature and overall U.

### 18. Cleaning Strategy Comparison
![Cleaning Strategies](18_cleaning_strategies.png)

Annual energy-loss + cleaning cost for different cleaning intervals.

### 19. ε–NTU Design Charts
![eps-NTU](19_eps_NTU_charts.png)

Effectiveness vs NTU for counter-flow, parallel-flow and cross-flow at several capacity ratios.

### 20. Off-Design Performance Map
![Off-design](20_offdesign_map.png)

Heat duty map vs hot mass flow and hot inlet temperature (design point marked).

### 21. Fouling Energy & CO₂ Footprint
![Footprint](21_fouling_footprint.png)

Extra daily energy cost and CO₂ emissions as fouling resistance grows.

### 22. Fixed-Duty Sizing Comparison
![Sizing](22_fixed_duty_sizing.png)

Required area for Shell-Tube / Plate / Finned-Tube to meet the same heat-duty target.

### 23. Typical Overall U by Service
![Typical U](23_typical_U_values.png)

Rule-of-thumb overall heat-transfer coefficient ranges for common process pairs.

### 24. Air-Cooled Seasonal Derate
![Seasonal](24_aircooled_seasonal_derate.png)

Available duty vs ambient temperature for an air-cooled unit.

### 25. Approach Temperature vs U
![Approach](25_approach_vs_U.png)

Minimum approach temperature as overall U increases (fixed geometry).

### 26. Heat Recovery vs Minimum Approach
![Heat Recovery](26_heat_recovery_vs_approach.png)

Maximum recoverable heat duty as a function of allowable approach.

### 27. Life-Cycle Energy Loss from Fouling
![Lifecycle](27_lifecycle_energy_loss.png)

Cumulative lost energy over 10 years without intermediate cleaning.






---


### 10. Axial Temperature Profiles
![Axial Profiles](10_axial_temperature_profiles.png)

Hot and cold fluid temperature evolution along the normalised length of a counter-flow shell-and-tube exchanger.

---

## Features

- **Core HX models** – LMTD / ε-NTU for Shell-Tube, Plate, Finned-Tube
- **Transient** – First-order lag response to step changes
- **Fouling** – Kern–Seaton asymptotic model + synthetic data generation
- **ML Prediction** – Random Forest + XGBoost (1-day / 7-day / 30-day horizons)
- **Uncertainty** – Monte-Carlo propagation on U, Q, effectiveness
- **Sensitivity** – Local (one-at-a-time ±10 %) parameter ranking
- **Optimization** – Maximize heat duty under area & velocity constraints
- **Predictive Maintenance** – Anomaly detection, RUL estimation, health index 0–100, early warnings
- **Fleet Monitoring** – Multi-asset ranking from CSV historian data
- **Nanofluids** – Maxwell conductivity + mixture rules (Al₂O₃, CuO, hybrid)
- **Economics** – Cleaning cost vs energy-loss trade-off; optimal cleaning interval
- **What-If Simulator** – Instant scenario analysis (hardness, velocity, temperature)
- **PDF Report** – One-click management / maintenance report
- **Pressure Drop** – Tube-side (Darcy) + shell-side (Kern) ΔP
- **LMTD Correction F** – Multipass correction factor for 1-2 exchangers
- **Capital Cost** – Approximate purchased equipment cost (material factors)
- **Axial T Profiles** – 1-D hot/cold temperature profiles along length
- **Vibration Screening** – Simple flow-induced vibration risk indicator
- **Maintenance Calendar** – Recommended cleaning & inspection dates
- **Excel Export** – One-click summary workbook (`HX_Summary_Export.xlsx`)

---

## Sample Results (default conditions)

| HX Type       | Q [kW] | ε    | U [W/m²K] | Area [m²] |
|---------------|--------|------|-----------|-----------|
| Shell-Tube    | 673    | 0.68 | 800       | 23.6      |
| Plate         | 806    | 0.81 | 2381      | 14.3      |
| Finned-Tube   | 430    | 0.43 | 40        | 204       |

- Transient time constant τ ≈ 80–100 s → settling ~4τ  
- Fouling ML model R² typically > 0.95 on held-out data  
- Most sensitive parameters: hot-side flow / inlet temperature / U  
- Suggested cleaning interval (default economics): often 45–90 days  

---

## Using your own plant data

1. Put your CSV in this same folder (or replace `hx_fleet_sample.csv`).
2. Expected columns (flexible mapping exists):  
   `timestamp, asset_id, operating_hours, water_hardness, velocity, T_hot_in, Rf, U, Q_kW, efficiency_pct, delta_P_kPa`
3. Open the notebook and run the CSV / fleet cells.
4. Adjust `Rf_CRIT`, `dP_CRIT`, energy price and cleaning cost to match your site.

---

## License

MIT – free for academic, commercial and industrial use.
