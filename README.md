# Remote-Sensing and Machine-Learning Crop Yield Prediction

## Project Overview
An end-to-end, reproducible machine learning pipeline that fuses satellite multispectral imagery (Sentinel-2) with environmental climate data (ERA5-Land) to predict pre-harvest county-level corn yield in the U.S. Corn Belt. 

This project demonstrates the transition from raw geospatial raster data to a tabular machine-learning dataset, evaluated with strict temporal cross-validation and Explainable AI (SHAP).

## Data Architecture
* **Target Variable:** USDA NASS county-level corn yield (bushels/acre).
* **Crop Mask:** USDA NASS Cropland Data Layer (30m).
* **Vegetation Metrics:** Sentinel-2 Surface Reflectance (NDVI, extracted via Google Earth Engine).
* **Climate Metrics:** ERA5-Land Monthly Aggregated reanalysis (Temperature, Soil Moisture).

## Key Results
* **In-Season Forecasting:** Predictive skill improved as the season progressed. 
  * June 30 (Vegetative): RMSE 11.60 bu/ac
  * July 31 (Peak Pollination): RMSE 10.84 bu/ac
  * August 31 (Maturation): RMSE 10.72 bu/ac | R² = 0.689
* **Explainability (SHAP):** The Random Forest model independently identified July thermal stress (approximately 297.5 K / 24.4°C) as the critical threshold for yield collapse, aligning with known agronomic limits for corn pollination.
* **Spatial Diagnostics:** Residual error mapping confirmed the model generalizes well geographically without heavy spatial clustering of errors.

## Repository Structure
* `/notebooks`: Numbered Google Colab notebooks (00 to 04) detailing the pipeline from Earth Engine extraction to ML evaluation.
* `/results/figures`: SHAP beeswarm plots, forecast progression curves, and spatial error maps.
* `data_dictionary.csv`: Definitions and units for all engineered features.
