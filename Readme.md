<div align="center">

![header](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,20&height=220&section=header&text=Rapido%20Revenue%20Leak%20Analysis&fontSize=42&fontAlignY=38&animation=fadeIn&fontColor=ffffff&desc=Uncovering%20hidden%20losses%20across%2050%2C000%20Bangalore%20rides&descAlignY=60&descSize=17)

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&size=20&duration=2800&pause=900&color=F7B731&center=true&vCenter=true&width=800&lines=49%2C801+rides+analysed+across+Bangalore;%E2%82%B96%2C837%2C929+in+total+revenue+mapped;10.4%25+cancellation+rate+driving+revenue+loss;%E2%82%B91%2C20%2C000%2Fmo+recoverable+with+targeted+fixes;Python+%E2%80%A2+Pandas+%E2%80%A2+Tableau+%E2%80%A2+Statistics)](https://github.com/vedant-valid/rapido-revenue-leak-analysis)

</div>

---

## The Problem

Rapido loses revenue silently — not from pricing, but from **cancellations**. When a ride is booked and cancelled, the fare disappears. Multiply that across thousands of peak-hour rides in high-demand zones, and the loss becomes structural.

> **Core question:** Where, when, and why do rides cancel — and how much revenue does Rapido bleed as a result?

This project processes **49,801 Bangalore ride transactions** to answer that question with numbers, not guesses.

---

## Impact at a Glance

<div align="center">

| Metric | Value |
|:---|:---|
| Total Revenue Mapped | **₹ 68,37,929** |
| Rides Analysed | **49,801** |
| Cancellation Rate | **10.4%** — 5,180 lost rides |
| Avg Revenue per Ride | **₹ 153.24** |
| Peak-Hour Cancel Spike | **+15–20%** above baseline |
| Monthly Recovery Potential | **₹ 1,20,000** from top 5 zones alone |
| Revenue Hotspot Share | **40%** of revenue from 2 zones |

</div>

---

## What the Data Revealed

**1. High demand = more cancellations, not fewer**
Zones with demand z-score > 1.0 show disproportionately higher cancellation rates — driver supply isn't scaling with demand.

**2. Two windows account for most of the damage**
Cancellations spike **15–20%** during 8–10 AM and 5–7 PM. `cab_economy` and `auto` are the worst hit — both high-volume, high-margin services.

**3. ₹1,20,000/month sitting on the table**
Reducing cancellations in just the **top 5 high-demand zones by 10%** recovers ~₹1.2L monthly. This is a surgical fix, not a platform overhaul.

**4. Bikes are the floor, not the ceiling**
`bike` and `bike_lite` maintain **92%+ completion rates** even during peak hours — they're the most operationally resilient service type.

**5. Koramangala & HSR Layout carry the revenue**
Two zones generate **40% of total revenue** but suffer inconsistent driver availability — the highest-ROI targets for supply intervention.

---

## Pipeline — How the Data Was Transformed

```
Raw CSV (51,000 rows, 13 cols)
        │
        ▼
[01] Extraction & Inspection   → dtype audit, shape check, nulls mapped
        │
        ▼
[02] Cleaning & ETL            → business-logic nulls, dedup on ride_id,
        │                         category standardisation, anomaly removal
        ▼
[03] EDA                       → distributions, heatmaps, peak-hour patterns
        │
        ▼
[04] Statistical Analysis      → z-score demand intensity, correlation tests,
        │                         revenue leakage simulation
        ▼
[05] Load Prep                 → final schema, export to cleaned_rides.csv

Cleaned Output: 49,801 rows · 30 engineered columns
```

**Key engineering decisions:**
- Cancelled rides → fare set to `0` (not dropped) — preserves cancellation signal
- `total_fare` recomputed as `ride_charge + misc_charge` to fix source inconsistencies
- 17 new features built: `peak_hour`, `demand_intensity`, `fare_per_km`, `ride_efficiency`, `avg_speed_kmh`, and more

---

## Live Dashboard

<div align="center">

[![Open Tableau Dashboard](https://img.shields.io/badge/Tableau-Open%20Interactive%20Dashboard-%23E97627?style=for-the-badge&logo=tableau&logoColor=white)](https://public.tableau.com/views/Rapido_Rides_Analysis_17780461220670/Overview?:language=en-US&:display_count=n&:origin=viz_share_link)

</div>

The dashboard covers:
- **Overview** — Revenue KPIs, cancellation rate, ride volume by service
- **Demand vs. Cancellation** — Zone-level scatter: where supply fails demand
- **Peak Hour Breakdown** — Hour-by-hour cancellation heatmap by service type
- **Revenue Recovery** — Simulated impact of targeted driver allocation

Dashboard screenshots → [`tableau/screenshots/`](tableau/screenshots/)

---

## Tech Stack

<div align="center">

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-150458?style=for-the-badge&logo=pandas&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-F37626?style=for-the-badge&logo=jupyter&logoColor=white)
![Tableau](https://img.shields.io/badge/Tableau-E97627?style=for-the-badge&logo=tableau&logoColor=white)
![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)

</div>

| Tool | What it did |
|:---|:---|
| **Python + Pandas** | ETL pipeline, cleaning, feature engineering |
| **Jupyter Notebooks** | Step-by-step analysis with inline documentation |
| **SciPy / NumPy** | Statistical testing, z-score demand modelling |
| **Tableau Public** | Interactive 4-view dashboard for business stakeholders |
| **GitHub** | Version control, structured project delivery |

---

## Repository Structure

```
rapido-revenue-leak-analysis/
├── data/
│   ├── raw/                    ← Original 51,000-row dataset
│   └── processed/              ← Cleaned 49,801-row output
├── notebooks/
│   ├── 01_extraction.ipynb     ← Load & inspect
│   ├── 02_cleaning.ipynb       ← ETL & feature engineering
│   ├── 03_EDA.ipynb            ← Exploratory analysis
│   ├── 04_statistical_analysis.ipynb  ← Demand modelling & leakage sim
│   └── 05_final_load_prep.ipynb
├── tableau/
│   ├── dashboard_links.md      ← Live dashboard link + previews
│   └── screenshots/            ← Dashboard images
├── reports/
│   └── Rapido-Ride-Analysis.pdf
└── docs/
    └── data_dictionary.md
```

---

## Dataset

| Attribute | Value |
|:---|:---|
| Source | [Kaggle — Bangalore Rapido Ride Services](https://www.kaggle.com/datasets/vishaldeoprasad/bangalore-rapido-ride-services-dataset/data) |
| Raw rows | 51,000 |
| Cleaned rows | 49,801 |
| Raw columns | 13 |
| Engineered columns | 30 |
| Period covered | April 10 – April 29 |

---

<div align="center">

![footer](https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,12,20&height=120&section=footer&animation=fadeIn)

**Built by [Vedant Madne](https://github.com/vedant-valid) — turning raw ride data into revenue decisions**

</div>
