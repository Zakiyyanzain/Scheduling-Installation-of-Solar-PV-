# PVIRI: Photovoltaic Installation Risk Index (Scheduling Installation)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

This repository contains the source code (Jupyter Notebook) used to calculate and analyze the installation schedule of Solar Photovoltaic (PV) power plants based on weather parameters and associated risks, as discussed in our paper: **"[Your Paper Title Here]"**.

## 📌 Description
This program performs weather risk analysis (including rainfall, Consecutive Dry Days/CDD, and Global Horizontal Irradiance/GHI) specifically targeted at the construction and installation phases of PV systems. The outputs of this script include data visualizations and an exported file (`PV_Installation_Results.xlsx`) containing comparative summaries and the most robust scheduling recommendations.

## 📂 Repository Structure
* `11_05_26_PVIRI_Notebook_EN.ipynb`: The main script to run the PVIRI analysis.
* `data/`: Folder containing the climatology/weather dataset (ensure this contains sample data if the original dataset is too large or confidential).
* `requirements.txt`: List of required Python libraries.

## ⚙️ System Requirements
Please ensure you are using Python 3.x. The main libraries used in this analysis are:
* `pandas` == 2.2.2
* `scipy` == 1.16.3
* `scikit-learn` == 1.6.1
* `numpy` == 2.0.2

You can easily install all dependencies by running the following command:
```bash
pip install -r requirements.txt
