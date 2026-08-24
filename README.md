# PVIRI: Photovoltaic Installation Risk Index

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.20180215.svg)](https://doi.org/10.5281/zenodo.20180215)

Source code and processed data for:

> Alkaf ZZ, Lenggana BW, Arifin RRN, Sastyawan MWR, Putera RD, Hurun'in, Wisudawati T, Akhmad Yani ARSP, Muhammad K (2026) **Photovoltaic Installation Risk Index (PVIRI): A climate-based scheduling framework for solar PV deployment in high-rainfall tropical regions of Indonesia.** *Theoretical and Applied Climatology* (under review).

PVIRI is a composite 0–1 risk index for scheduling solar PV installation work in tropical, high-rainfall regions, integrating monthly rainfall volume, rainy-day frequency, and global horizontal irradiance (GHI). It is validated at three Indonesian sites representing equatorial, monsoonal, and orographic rainfall regimes: Mimika, Luwu Utara, and Padang Pariaman.

## Versions

This repository has two tagged releases, corresponding to the two stages of peer review.

| Version | Tag | Corresponds to | Summary |
|---|---|---|---|
| v1.0.0 | [`v1.0.0`](../../releases/tag/v1.0.0) | Original submission | 10-year NASA POWER baseline (2016–2025); bias-correction factors computed but not propagated to the full record; entropy-weighting verification reported. |
| v2.0.0 | [`v2.0.0`](../../releases/tag/v2.0.0) | Revision 1 | 30-year baseline (1996–2025); bias-correction factors applied to the full record; wind and heat screening added; entropy-weighting claim withdrawn (see Changelog). |

**If you are trying to reproduce a number from the paper, check which version you need.** The manuscript under review cites the DOI of v2.0.0 specifically, not the concept DOI, so that the archived code always matches the reported results.

## Repository structure

```
PVIRI_Notebook_REV2.ipynb        Main analysis notebook (v2.0.0)
data/
  NASA_daily_30y_Mimika.csv           NASA POWER daily reanalysis, 1996–2025
  NASA_daily_30y_Luwu_Utara.csv       NASA POWER daily reanalysis, 1996–2025
  NASA_daily_30y_Padang_Pariaman.csv  NASA POWER daily reanalysis, 1996–2025
  README_data.md                      Column definitions and provenance
LICENSE
README.md
```

The v1.0.0 release retains the original notebook and is preserved unmodified under its own tag for anyone auditing what was originally reviewed.

## Data availability

**NASA POWER** (public domain). The three files in `data/` are the daily reanalysis product (`PRECTOTCORR`, `ALLSKY_SFC_SW_DWN`, `T2M`, `T2M_MAX`, `T2M_MIN`, `RH2M`, `WS10M`, `WS10M_MAX`) for 1996–2025, downloaded from the [NASA POWER API](https://power.larc.nasa.gov/). No restrictions apply to redistribution.

**BMKG station observations** (restricted). The ground-truth station data used for bias correction and cross-validation are **not redistributed in this repository**, per BMKG's data policy. They are available on official request via [dataonline.bmkg.go.id](https://dataonline.bmkg.go.id). `README_data.md` documents the station identifiers and the exact request parameters (period, variables) needed to reproduce our request.

## Requirements

```
python >= 3.10
pandas == 2.3.3
numpy == 2.0.2
scipy == 1.16.3
scikit-learn == 1.6.1
statsmodels
pymannkendall
matplotlib
seaborn
openpyxl
```

Install with:

```bash
pip install -r requirements.txt
```

## Running the analysis

1. Place the BMKG station files (obtained per **Data availability** above) alongside the NASA files listed in `data/`, or point `DATA_DIR_OVERRIDE` in the notebook's configuration cell at their location.
2. Open `PVIRI_Notebook_REV2.ipynb` and run all cells in order. The notebook auto-detects its runtime (local / Colab / Kaggle) and locates the data directory automatically; see the configuration cell for `BASELINE_MODE`, `BASELINE_Y0`/`BASELINE_Y1`, and `APPLY_BIAS_CORRECTION` if you want to reproduce the v1.0.0 behaviour (10-year, uncorrected) for comparison.
3. Figures are written to the working directory as PNG at 300 dpi; a final cell archives all of them into `PV_Research_Figures_FINAL.zip` and prints a map from each file to its figure number in the manuscript.

## Changelog (v1.0.0 → v2.0.0)

- **Baseline extended from 10 to 30 years** (2016–2025 → 1996–2025), meeting the WMO climate-normal minimum for SPI and extreme-value analysis.
- **Bias-correction bug fixed.** In v1.0.0, monthly Linear Scaling factors were estimated and used only to compute validation metrics; they were never applied to the full reanalysis record, so the climatology and PVIRI in v1.0.0 were in fact uncorrected. v2.0.0 applies the correction throughout.
- **Wind and heat screening added**, evaluating and explicitly justifying their exclusion from the monthly index.
- **Entropy-weighting claim withdrawn.** We were unable to reproduce the entropy-derived weights reported in v1.0.0 from this pipeline; the weighting is justified on operational grounds instead, with robustness shown by one-at-a-time sensitivity analysis.
- Station elevation metadata and MERRA-2 grid-cell elevation added for all three sites.

See the manuscript's Response to Reviewers for full details.

## License

Code and NASA POWER-derived data are released under the [MIT License](LICENSE). BMKG station data are third-party and are not covered by this license; see **Data availability**.

## Citation

If you use this code or data, please cite the paper above and this repository:

```
Alkaf ZZ et al. (2026) PVIRI analysis code and data (v2.0.0) [Software].
Zenodo. https://doi.org/10.5281/zenodo.20180215
```
