# Air Quality Prediction System - Bhopal

## Overview
An end-to-end data pipeline for air quality forecasting using real-world CPCB pollution data and meteorological analysis for Bhopal, India.

## Project Details

**Duration:** November 2024 - Present (analyzing historical 2019-2023 data + 2024 validation)

**Location:** Bhopal, Madhya Pradesh, India

## Objectives
- Forecast air quality trends using time-series modeling
- Identify pollution patterns and seasonal variations
- Correlate meteorological factors with pollutant dispersion
- Build a scalable, reproducible data pipeline

## Dataset

### Air Quality Data
- **Source:** Central Pollution Control Board (CPCB)
- **Historical Data:** 5 years (2019-2023) with daily frequency
- **Historical Records:** 1,826+ daily measurements
- **Validation Data:** 2024 actual measurements for comparison and model validation
- **Resolution:** Daily aggregated values
- **Pollutants Tracked:**
  - PM2.5 (Fine Particulate Matter)
  - PM10 (Coarse Particulate Matter)
  - NO₂ (Nitrogen Dioxide)
  - O₃ (Ozone)
  - CO (Carbon Monoxide)
  - SO₂ (Sulfur Dioxide)

### Meteorological Data
- **Source:** NOAA ISD (Integrated Surface Database)
- **Station:** Raja Bhoj Airport (Station 42667)
- **Historical Period:** 2019-2023 (daily frequency)
- **Parameters:** Wind speed, wind direction, temperature, pressure, humidity

## Key Findings

- **5-Year Average PM2.5 (2019-2023):** ~85 µg/m³ (well above NAAQS standard limit of 30 µg/m³)
- **2024 Validation:** Annual PM2.5 mean of ~90 µg/m³, showing consistent pollution levels year-over-year
- **Trend Analysis:** Identified increasing PM2.5 concentrations during winter months (Nov-Jan) across all 5 years
- **Diwali Effect:** Recurring pollution spike pattern observed annually, with PM2.5 reaching 250+ µg/m³
- **AQI Distribution (2024):** Zero "Good" category days recorded
- **Seasonal Pattern:** Winter months consistently show highest pollution; monsoon season shows lowest concentrations
- **Model Validation:** 2024 actual data compared against predictions shows model capturing seasonal trends effectively

## Technical Implementation

### Data Processing
- Cleaned and validated 5-year historical dataset (2019-2023) with Pandas
- Integrated 2024 actual measurements for model validation and comparative analysis
- Handled missing values and outliers using statistical methods
- Normalized features for model compatibility
- Performed seasonal decomposition and trend analysis across 5-year period

### Forecasting Model
- **Algorithm:** Holt-Winters Exponential Smoothing
- **Training Data:** 2019-2023 (1,826+ daily observations)
- **Validation Data:** 2024 actual measurements
- **Performance:** 12-15% MAPE on 2024 holdout data
- **Forecast Horizon:** Year-ahead and month-ahead predictions
- **Validation:** Time-series cross-validation comparing predictions to 2024 actuals

### Feature Engineering
- Lag features (1, 7, 30-day rolling windows)
- Temporal features (hour, day, month, season)
- Meteorological interaction terms
- Wind direction and speed correlation analysis

### Geospatial Analysis
- Wind rose analysis using WRPLOT View
- Correlation between wind patterns and pollutant dispersion
- Receptor-based dispersion modeling preparation

## Technologies & Tools

### Languages
- Python 3.x

### Libraries
- **Data Processing:** Pandas, NumPy
- **Machine Learning:** Scikit-learn, Statsmodels
- **Visualization:** Matplotlib, Seaborn
- **Environment:** Google Colab

### Tools
- WRPLOT View (wind rose analysis)
- AERMOD (dispersion modeling framework)
- Jupyter Notebooks

## Project Structure

```
Air Quality Prediction System/
├── data/
│   ├── raw_cpcb_data.csv
│   ├── noaa_meteorological_data.csv
│   └── processed_dataset.csv
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   ├── 02_data_cleaning.ipynb
│   ├── 03_feature_engineering.ipynb
│   └── 04_forecasting_model.ipynb
├── src/
│   ├── data_pipeline.py
│   ├── preprocessing.py
│   ├── forecasting.py
│   └── visualization.py
├── results/
│   ├── model_predictions.csv
│   ├── performance_metrics.txt
│   └── visualizations/
├── reports/
│   └── Air_Quality_Presentation.pptx
└── README.md
```

## Pipeline Workflow

1. **Data Ingestion:** Fetch CPCB and NOAA ISD data
2. **Cleaning:** Remove duplicates, handle missing values, validate ranges
3. **Feature Engineering:** Create temporal and meteorological features
4. **Exploratory Analysis:** Identify patterns, correlations, seasonal trends
5. **Model Training:** Fit Holt-Winters with optimal parameters
6. **Validation:** Evaluate with MAPE and visual residual analysis
7. **Forecasting:** Generate month-ahead and year-ahead predictions
8. **Reporting:** Create visualizations and technical reports

## Model Performance

| Metric | Value |
|--------|-------|
| MAPE (Test Set) | 12-15% |
| MAE | 8-12 µg/m³ |
| RMSE | 15-20 µg/m³ |
| R² Score | 0.78-0.82 |

## Sample Code

### Data Loading and Preprocessing

```python
import pandas as pd
import numpy as np
from sklearn.preprocessing import StandardScaler

# Load historical data
df_cpcb = pd.read_csv('raw_cpcb_data.csv')
df_meteorology = pd.read_csv('noaa_meteorological_data.csv')

# Merge datasets
df_combined = pd.merge(df_cpcb, df_meteorology, on='date')

# Handle missing values
df_combined.fillna(df_combined.mean(), inplace=True)

# Normalize features
scaler = StandardScaler()
df_scaled = scaler.fit_transform(df_combined)
```

### Forecasting Model

```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing

# Fit Holt-Winters model on 2019-2023 data
model = ExponentialSmoothing(
    train_data, 
    seasonal_periods=365, 
    trend='add', 
    seasonal='add'
)

fitted_model = model.fit()

# Generate predictions for 2024
predictions_2024 = fitted_model.forecast(steps=365)

# Calculate MAPE
mape = np.mean(np.abs((actual_2024 - predictions_2024) / actual_2024)) * 100
print(f"MAPE: {mape:.2f}%")
```

## Deliverables

- ✅ Complete Python/Colab data pipeline
- ✅ Holt-Winters forecasting model with 12-15% MAPE
- ✅ 10-slide PowerPoint presentation with findings
- ✅ Temporal trend and seasonal heatmap visualizations
- ✅ Technical documentation for non-specialist audiences
- ✅ AERMOD dispersion model input dataset

## Future Enhancements

- Implement LSTM/GRU deep learning models for better long-term forecasting
- Integrate real-time data streaming from CPCB API
- Deploy web dashboard for stakeholder access
- Add AERMOD dispersion modeling for source attribution
- Implement multi-step ahead forecasting with confidence intervals

