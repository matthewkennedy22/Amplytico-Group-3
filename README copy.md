# Amplytico Group 3 (Final Submission Repo)

This repository contains the **analysis assets** for Team 3’s project:
**Climate-Aware Optimization of Hyperscale Data Center Cooling Systems**.

It is intentionally “lean” for GitHub submission:
- excludes multi-GB raw weather and full county-level simulation CSVs
- includes the **latest, report-relevant scripts** and **compact derived datasets** (so the key metrics can still be reproduced)

## What’s included (folder map)
- `01_weather_api_and_pue_wue_simulation/`  
  Weather retrieval (Open-Meteo) + AE/WEC PUE/WUE simulation pipeline scripts
- `02_drought_risk/`  
  U.S. Drought Monitor API integration + drought data cleaning scripts
- `03_utility_pricing/`  
  State-level electricity & water pricing inputs used in the project
- `04_analysis_data/`  
  Precomputed rollups + compact derived tables used for the report figures/tables
- `05_tableau_visuals/`  
  Tableau workbooks and small supporting images
- `06_climate_zone_analysis/`  
  Zone-level datasets/scripts/workbooks for IECC climate zone analysis + sensitivity
- `scripts/`  
  Builders that turn the large drought weekly file into compact summaries and then into water-stress/effective-cost tables
- `docs/`  
  Project blueprints and pipeline documentation
- `PUE_WUE_SIM/` (repo root)  
  The simulator core + COP model pickles used by `county_pipeline.py`

## Key derived outputs (already generated)
- `04_analysis_data/drought_summary_by_county.csv`
- `04_analysis_data/water_stress_by_county_system.csv`
- `04_analysis_data/effective_utility_cost_by_county_system.csv`

## Weather scripts (submission-friendly defaults)
To let the weather+PUE/WUE scripts run without the full multi-GB DuckDB exports, the submission repo includes:
`01_weather_api_and_pue_wue_simulation/weather_hourly_with_counties_sample.csv`
which is generated from Open-Meteo using:
`python scripts/build_weather_hourly_with_counties_sample.py`

## Reproduce the compact outputs (recommended)
This submission includes the newest **week52only** drought weekly file compressed as:
`02_drought_risk/drought_weekly_by_county_2015_2024_week52only_fixed_2.0.csv.gz`

To regenerate the compact outputs from scratch:
1. Build county drought summary (uses the included week52only file by default):
   ```bash
   python scripts/build_drought_summary_by_county.py
   ```
2. Build water stress + effective utility cost tables:
   ```bash
   python scripts/build_water_stress_and_effective_costs.py
   ```

## Tableau note
The included `*.twb` workbooks were exported from the original workspace and still reference larger extracts / absolute local paths. If you open them and Tableau asks to reconnect data sources, simply re-link them to the files you have (especially the compact CSVs in `04_analysis_data/`).

