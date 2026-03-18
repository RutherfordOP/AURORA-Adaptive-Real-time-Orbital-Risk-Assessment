# AURORA : Adaptive Real Time Orbital Risk Assesment 🛰️

**End-to-end TLE pipeline for satellite classification, orbit propagation, and collision risk detection**

I built this because I got tired of seeing space debris news and not having my own tool to actually analyse it. Started with raw Two-Line Elements, ended up with a full production-grade system: UKF state refinement, proper ML classification (no leakage!), common-epoch propagation, real conjunction detection, and a beautiful 3D dashboard.

## What it actually does

- Refines noisy TLEs using an **Adaptive Unscented Kalman Filter** (full 6×6 covariance output)
- Classifies every object as **PAYLOAD / DEBRIS / ROCKET BODY** with CatBoost (macro F1 0.8637 on time-series CV)
- Propagates **all satellites to the exact same epochs** (fixed the original bug where everything was at different times)
- Detects real debris-payload conjunctions (yes, we finally have some at <10 km)
- Generates an interactive 3D Earth dashboard + summary report

## Results from the 50k TLE dataset (Oct 2025)

- 18,851 unique objects processed
- 56,855 refined states
- Classification: 12,966 PAYLOAD | 5,885 DEBRIS
- 3 prediction horizons (D+1, D+3, D+7) at common epochs
- 38 conjunctions found (17 real debris-payload risks)
- Dashboard: 4.9 MB interactive HTML

## Repository Structure
orbital-sentinel/
├── notebooks/
│   ├── 01_tle_refinement_ukf.ipynb          # Phase 1 core
│   ├── 02_classification_pipeline.ipynb     # ML part
│   └── 03_propagation_conjunctions.ipynb    # Fixed propagator
├── data/                                    # (add your CSV here)
├── output/
│   ├── refined_states_full.csv
│   ├── FINAL_CLASSIFIED.csv
│   ├── orbit_predictions_fixed.parquet
│   └── dashboard.html
├── src/                                     # clean Python modules (coming soon)
└── README.md

## How to run it

1. Clone the repo
2. Drop your TLE CSV (same format as the Kaggle one) into `data/`
3. Run the notebooks in order (they're self-contained and heavily commented)
4. Open `output/dashboard.html` in any browser — it works offline

**Requirements** (tested on Kaggle + local):
- Python 3.11
- `sgp4`, `skyfield`, `catboost`, `tensorflow`, `plotly` (exact versions in the notebooks)

## Why this is actually useful

Most public TLE tools either:
- Just plot orbits, or
- Use outdated propagation, or
- Classify without covariance

This one does **all three** correctly, with proper time alignment so conjunction detection actually works.

## Repository Name Suggestions (pick one)

1. **orbital-sentinel** ← my favourite (clean, professional, memorable)
2. **debris-radar**
3. **tle-guardian**
4. **space-traffic-ai**
5. **conjunction-hunter**
6. **astro-sentinel**
7. **leo-debris-tracker**

## Short GitHub Descriptions (use any)

- "AI-powered satellite tracking & collision prediction pipeline using TLE data"
- "From raw TLE → classified objects → propagated orbits → real conjunction alerts"
- "UKF + CatBoost + Skyfield = production-grade space situational awareness"
- "End-to-end orbital debris monitoring system I actually trust"

## Want to contribute?

Open issues for:
- Adding Starlink/OneWeb bulk propagation
- Real-time API version
- Better visualisation (Plotly Dash version)
- Integration with Celestrak API

Feel free to fork and go wild — just credit the original if you use the UKF+classification core.

---

Made with ☕ in Bengaluru. Star if you find it useful!
