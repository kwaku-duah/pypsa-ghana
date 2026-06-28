# 🇬🇭 PyPSA-Ghana

**Open-source power system research model for Ghana — vanilla PyPSA, real data, reproducible science.**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PyPSA](https://img.shields.io/badge/built%20with-PyPSA-blue)](https://pypsa.org)
[![Data: WEM Bulletins](https://img.shields.io/badge/data-WEM%20Bulletins-green)](https://energycom.gov.gh)

---

## What this is

PyPSA-Ghana is a research-grade power system model for Ghana, built on vanilla [PyPSA](https://pypsa.org). It uses real hourly demand data constructed from Ghana's Wholesale Electricity Market (WEM) bulletins and a validated generator fleet from the Energy Commission's National Energy Statistical Bulletin.

This repository is the **research layer** of a two-repo Ghana modelling framework:

| Repo                                                  | Purpose                                                                                                             |
| ----------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- |
| **[pypsa-gh](https://github.com/kwakuduah/pypsa-gh)** | Ghana configuration for PyPSA-Earth — automated network building, ERA5 renewable potential, infrastructure planning |
| **pypsa-ghana** ← you are here                        | Vanilla PyPSA research analysis — real WEM demand, validated dispatch, contingencies, LEAP integration, paper       |

---

## What it does

```
pypsa-gh (PyPSA-Earth)              pypsa-ghana (this repo)
──────────────────────              ───────────────────────
ERA5 solar/wind profiles    ──────► Renewable capacity factors
Network topology (6 nodes)  ──────► Transmission constraints
                                    Real WEM hourly demand (2024)
                                    Validated generator fleet
                                    Baseline dispatch optimisation
                                    SCOPF contingency analysis
                                    Emissions tracking
                                    LEAP demand scenarios 2030-2070
                                    Least-cost capacity expansion
                                    ▼
                            ──────► Validated results feed back to pypsa-gh
```

---

## Research programme

### Phase 1 — 2024 Baseline (current)

- 8,760-hour demand profile constructed from WEM Bulletins Issues 91–102
- Generator fleet: 20+ plants, real marginal costs from fuel prices and heat rates
- Dispatch optimisation validated against Energy Commission Statistical Bulletin 2025
- Grid emission factor validation (target: 0.35 tCO₂/MWh)

### Phase 2 — Contingency Analysis

- N-1: Akosombo derating (Volta Lake water level risk)
- N-1: West African Gas Pipeline (WAGP) disruption
- N-1: Floating power plant exit (Karpower)
- Output: hours of unmet demand, cost of resilience, corrective dispatch

### Phase 3 — 2030 Scenarios

- Business as Usual (BAU): 4.6% demand CAGR
- Accelerated Transition: aggressive electrification + EV uptake
- Climate Ambition: demand-side management + near-zero carbon
- Least-cost generation mix per scenario
- Solar, storage and transmission investment recommendations

### Phase 4 — LEAP Integration (2030–2070)

- LEAP models sectoral demand: residential, industrial, commercial, transport
- Connector script converts LEAP annual GWh → 8,760-hour timeseries
- PyPSA optimises least-cost supply to meet LEAP demand scenarios
- Results feed back to LEAP for emissions accounting
- First open-source LEAP–PyPSA integrated framework for West Africa

---

## Data sources

| Data                       | Source                                                       |
| -------------------------- | ------------------------------------------------------------ |
| Hourly demand profile      | WEM Bulletins Issues 91–102 (EMOPS, Energy Commission Ghana) |
| Generator fleet            | National Energy Statistical Bulletin 2025, Table 3.2         |
| Fuel prices & heat rates   | WEM Bulletin Issue 102, Economic & Operational Fact Sheets   |
| Renewable capacity factors | ERA5 via pypsa-gh / PyPSA-Earth                              |
| Emissions factors          | National Energy Statistical Bulletin 2025, Table 6.3         |

---

## Repository structure

```
pypsa-ghana/
├── data/
│   ├── demand/
│   │   ├── Ghana_2024_Hourly_Demand_MW.csv    # 8,760-hour profile
│   │   └── Ghana_2024_Daily_Summary.csv
│   └── generators/
│       └── ghana_fleet_2024.csv               # validated generator fleet
├── scripts/
│   ├── 01_build_network.py                    # network construction
│   ├── 02_baseline_2024.py                    # dispatch optimisation
│   ├── 03_contingencies_scopf.py              # N-1 contingency analysis
│   ├── 04_emissions.py                        # emissions tracking
│   ├── 05_scenarios_2030.py                   # demand scaling + investment
│   └── 06_leap_connector.py                   # LEAP → PyPSA pipeline
├── results/                                   # model outputs (gitignored)
├── notebooks/                                 # analysis and visualisation
├── paper/                                     # research paper drafts
├── README.md
├── LICENSE
├── .gitignore
└── requirements.txt
```

---

## Quick start

```bash
git clone https://github.com/yourusername/pypsa-ghana.git
cd pypsa-ghana
pip install -r requirements.txt
python scripts/01_build_network.py
python scripts/02_baseline_2024.py
```

---

## Requirements

```
pypsa>=0.26
pandas>=2.0
numpy>=1.24
highspy
matplotlib
```

---

## Related work

- **pypsa-gh**: Ghana configuration for PyPSA-Earth → [github.com/kwakuduah/pypsa-gh](https://github.com/kwakuduah/pypsa-gh)
- **PyPSA-Earth**: Global power system model → [github.com/pypsa-meets-earth/pypsa-earth](https://github.com/pypsa-meets-earth/pypsa-earth)
- **LEAP**: Long-range Energy Alternatives Planning → [leap.sei.org](https://leap.sei.org)

---

## Author

**Kwaku Duah**  
Independent Energy Systems Researcher & Modeller | Ghana  
Lead Researcher, PyPSA-Ghana | Founder, KWD Power Systems  
[LinkedIn](https://linkedin.com/in/kwaku-duah-262543202) · [Zenodo](https://zenodo.org/record/19109707)

---

## Citation

If you use this work please cite:

```bibtex
@software{duah2024pypsa_ghana,
  author    = {Duah, Kwaku},
  title     = {PyPSA-Ghana: Open-source power system research model for Ghana},
  year      = {2024},
  publisher = {GitHub},
  url       = {https://github.com/yourusername/pypsa-ghana}
}
```

---

## License

MIT License. See [LICENSE](LICENSE).
