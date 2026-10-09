# Remote-Sensing and Machine-Learning Crop Yield Prediction

## Overview
A machine learning pipeline designed to forecast pre-harvest corn yields across Iowa's 99 counties (2019–2024). By integrating satellite remote sensing and global climate reanalysis, this project predicts yield anomalies to establish a highly interpretable, biophysically grounded agricultural forecasting model.

## Features
* **Multimodal Data Fusion:** Combines Sentinel-2 surface reflectance (NDVI, NDWI, NDRE) with ERA5-Land climate data (temperature, precipitation, soil water).
* **Crop Masking:** Dynamically applies the USDA Cropland Data Layer (CDL) to isolate active corn pixels prior to feature extraction.
* **Residual Modeling:** Uses Ridge Regression and XGBoost to predict yield deviations from historical county baselines, improving model stability and out-of-sample generalization.
* **Explainable AI:** Utilizes Tree SHAP to identify and visualize the primary agronomic drivers of crop yield (e.g., late-season moisture, early-season thermal accumulation).
* **Precision Diagnostics:** Maps county-level spatial prediction errors and downscales regional anomalies to 10-meter field-level vegetative stress maps.

## Data Sources
* **USDA NASS:** County-level historical corn yield data (target variable).
* **Sentinel-2 (Level-2A):** Monthly median vegetation and moisture indices.
* **ERA5-Land:** Monthly aggregates of climate and weather metrics.



