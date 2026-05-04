# Air_Quality
Built time-series forecasting pipeline processing 366 days of CPCB air quality data (6 pollutants). Implemented Holt-Winters model (12-15% MAPE) with automated data ingestion from NOAA ISD meteorological API. Performed feature engineering, seasonal decomposition, and geospatial wind pattern analysis using Python, Pandas, NumPy, Scikit-learn.
Air Quality Prediction System - Bhopal
Overview
An end-to-end data pipeline for air quality forecasting using real-world CPCB pollution data and meteorological analysis for Bhopal, India.
Project Details
Duration: November 2024 - Present
Location: Bhopal, Madhya Pradesh, India
Objectives

Forecast air quality trends using time-series modeling
Identify pollution patterns and seasonal variations
Correlate meteorological factors with pollutant dispersion
Build a scalable, reproducible data pipeline

Dataset
Air Quality Data

Source: Central Pollution Control Board (CPCB)
Duration: 366 days (2024)
Resolution: Hourly measurements
Pollutants Tracked:

PM2.5 (Fine Particulate Matter)
PM10 (Coarse Particulate Matter)
NO₂ (Nitrogen Dioxide)
O₃ (Ozone)
CO (Carbon Monoxide)
SO₂ (Sulfur Dioxide)



Meteorological Data

Source: NOAA ISD (Integrated Surface Database)
Station: Raja Bhoj Airport (Station 42667)
Records: 50,000+ hourly observations
Parameters: Wind speed, wind direction, temperature, pressure, humidity

Key Findings

Annual PM2.5 Mean: ~90 µg/m³ (3× NAAQS standard limit of 30 µg/m³)
Diwali Pollution Spike: PM2.5 reached 250+ µg/m³
AQI Distribution: Zero "Good" category days recorded in 2024
Seasonal Pattern: Winter months show highest pollution concentrations

Technical Implementation
Data Processing

Cleaned and validated 366-day dataset with Pandas
Handled missing values and outliers using statistical methods
Normalized features for model compatibility
Performed seasonal decomposition and trend analysis

Forecasting Model

Algorithm: Holt-Winters Exponential Smoothing
Performance: 12-15% MAPE (Mean Absolute Percentage Error)
Forecast Horizon: Month-ahead predictions
Validation: Time-series cross-validation with walk-forward testing

Feature Engineering

Lag features (1, 7, 30-day rolling windows)
Temporal features (hour, day, month, season)
Meteorological interaction terms
Wind direction and speed correlation analysis

Geospatial Analysis

Wind rose analysis using WRPLOT View
Correlation between wind patterns and pollutant dispersion
Receptor-based dispersion modeling preparation

Technologies & Tools
Languages

Python 3.x

Libraries

Data Processing: Pandas, NumPy
Machine Learning: Scikit-learn, Statsmodels
Visualization: Matplotlib, Seaborn
Environment: Google Colab

Tools

WRPLOT View (wind rose analysis)
AERMOD (dispersion modeling framework)
Jupyter Notebooks
