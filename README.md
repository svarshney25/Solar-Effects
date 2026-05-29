# CME and Proton Temperature Analysis
Overview
I worked on this project in a team for my NASA STEM Enhancement in Earth Sciences (SEES) Research Internship. My group analyzed the effects of Coronal Mass Ejections (CMEs) and solar flares on Earth and Mars.

This notebook detects and characterizes Coronal Mass Ejection (CME) events by identifying simultaneous anomalies across multiple solar wind parameters such as proton density, velocity, temperature, flux, and geomagnetic activity (Kp index). It covers both Earth-based and Mars-based observations, enabling a multi-planet view of the same CME events.

## Data Sources
Mars (MAVEN/SWIA)
- MAVEN_SWIA_Mars.csv for proton number density, velocity, and temperature at Mars

Earth
- DSCOVR_temperature_Earth.csv - solar wind proton temperature (DSCOVR satellite)
- GOES_flux_Earth.csv - proton flux (GOES satellite)
- ACE_density_Earth.csv - proton density (ACE satellite)
- NOAA_KP_Earth.csv - Kp geomagnetic index (NOAA)

## Notebook Structure

1. Setup & Data Loading - Mounts Google Drive, reads Mars CSV, parses timestamps
2. Mars CME Detection - Flags time steps where ≥2 of 3 parameters (density, velocity, temperature) exceed 2.5σ above their mean
3. Earth Data Loading & Cleaning - Reads all four Earth datasets, removes negative values and outliers beyond 3–3.5σ
4. Earth Time-Series Plots - Raw and smoothed (30-point rolling average) plots of all four Earth parameters with CME windows overlaid
5. Histogram Analysis - Distributions of each parameter split into three periods: pre-CME, during CME, and post-CME
6. Helper Functions - local_average() for smoothing; create_histograms() for multi-panel histogram plots

Requirements
- pandas
- numpy
- matplotlib
- scipy

The notebook is designed to run in Google Colab with data files stored in Google Drive.
Notes
- fillna(method='ffill') is used to forward-fill sporadic gaps in all datasets.
- The Mars detection uses an OR-style threshold (≥2 of 3 parameters), while the Earth detection uses an AND-style threshold requiring all four parameters to exceed their thresholds simultaneously. The Earth version is therefore more conservative.
- The get_variable_name() helper function uses Python frame inspection to auto-label histogram axes; it may not work reliably in all environments.
- Unit conversion from eV to Kelvin (factor: 11604.525) is applied where column names contain 'eV'.
