# Remote-Sensing and Machine-Learning Crop Yield Prediction

## Overview
This repository contains a research-grade machine learning pipeline for pre-harvest corn yield forecasting across Iowa's 99 counties (2019–2024)[cite: 1]. By integrating satellite remote sensing and global climate reanalysis, the pipeline predicts yield anomalies (deviations from historical county baselines) to establish an interpretable, biophysically grounded forecasting model[cite: 1].

## Data & Architecture
*   **Target Variable:** USDA NASS County-Level Corn Yield (Bushels/Acre)[cite: 1].
*   **Remote Sensing:** Sentinel-2 Level-2A (Monthly median composites of NDVI, NDRE, and NDWI)[cite: 1].
*   **Environmental Data:** ERA5-Land Reanalysis (Monthly aggregates of Temperature, Precipitation, and Soil Water)[cite: 1].
*   **Masking:** USDA Cropland Data Layer (CDL) applied dynamically to isolate active corn pixels[cite: 1].
*   **Modeling Framework:** Residual/Anomaly Modeling utilizing Ridge Regression, Random Forest, and XGBoost[cite: 1].

## Key Findings & Visualizations

### 1. Model Evaluation & Out-of-Sample Generalization
Evaluated on a strictly held-out 2024 test set, the Ridge-based multimodal fusion model achieved an RMSE of 15.22 bu/ac and an MAE of 12.31 bu/ac, significantly outperforming the baseline historical county average (RMSE: 25.18 bu/ac)[cite: 6]. Leave-One-Year-Out (LOYO) cross-validation across the training window demonstrated strong predictive capability in standard weather years ($R^2 = 0.583$ in 2022)[cite: 6]. The architecture also successfully isolated severe mechanical shock events, such as a +18.77 bu/ac overprediction during the catastrophic 2020 Iowa Derecho windstorm, which destroyed crops via lodging without impacting early-season canopy greenness[cite: 6].

### 2. Agronomic Explainability (SHAP)
Tree SHAP analysis isolated late-season moisture (`precip_Aug`), early-season thermal accumulation (`temp_May`), and late-season canopy chlorophyll density (`NDRE_mean_Aug`) as the primary biophysical drivers of final harvest volume[cite: 7].

![SHAP Beeswarm Plot](SHAP.png)

### 3. Spatial Diagnostics & Geographic Error
Geographic mapping of 2024 residuals revealed regional error clustering[cite: 8]. The model overpredicted yields in northern counties like Winnebago (+27.07 bu/ac) and Worth (+20.02 bu/ac), while underestimating localized bumper crops in southeastern counties like Lee (-45.35 bu/ac) and Henry (-33.73 bu/ac)[cite: 9].

![Spatial Error Map](spatial error.png)

### 4. Precision Agriculture Downscaling
By extracting high-resolution (10-meter) vegetation anomalies specifically within Lee County, the pipeline successfully traced macro-level county underpredictions to hyper-localized surges in field-level vigor, effectively bridging regional forecasting with precision agriculture diagnostics[cite: 10].

![Lee County Stress Map](lee_county_stress_map.png)

### 5. Forecasting Lead-Time
Chronological feature ablation proved that forecast error plummets substantially at the end of July (Silking stage), successfully locking in predictive accuracy months before the October physical harvest[cite: 11].

![Lead-Time Trajectory](lead_time_curve.png)

## Repository Organization
* `/notebooks`: Sequential Jupyter notebooks detailing Google Earth Engine extraction, preprocessing, model training, and spatial error mapping.
* `/src`: Utility scripts for automated cloud masking, CDL application, and evaluation metrics.
* `/results/Figures`: High-resolution outputs of SHAP attributions, spatial tri-maps, and lead-time forecast trajectories.
* `/data`: Directory template for raw and processed datasets (data excluded from version control for size limitations).

## Requirements
To execute this pipeline, ensure the following dependencies are installed:
```bash
pip install numpy pandas scikit-learn xgboost shap geopandas matplotlib geemap earthengine-api
