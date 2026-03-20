# Real-Time Weather Forecasting Using Machine Learning Techniques

## 1. Introduction

This project implements an end-to-end **real-time weather forecasting system** that combines:

- Historical NOAA weather data
- Time-series feature engineering
- Machine learning regression models
- Model interpretability (SHAP)
- Live weather data integration via API

The system predicts **daily maximum (TMAX)** and **minimum (TMIN)** temperatures and generates **short-term forecasts** using a hybrid ML + API approach.

---

## 2. Dataset Description

- Source: NOAA Global Historical Climatology Network (GHCN-Daily)
- Station: JFK International Airport, New York
- Time Period: January 2010 – December 2025 :contentReference[oaicite:0]{index=0}

### Key Features

| Category        | Variables |
|----------------|----------|
| Temperature    | TMAX, TMIN |
| Precipitation  | PRCP |
| Snow           | SNOW, SNWD |
| Wind           | AWND, WSF2, WSF5 |
| Weather Events | WT01–WT22 |

---

## 3. System Architecture

The project follows a structured machine learning pipeline:

### 3.1 Exploratory Data Analysis
- Time series visualization
- Seasonal trend analysis
- Distribution and outlier detection
- Correlation analysis

### 3.2 Data Preprocessing
- Datetime conversion and indexing
- Missing value treatment:
  - Event flags → 0
  - Precipitation/snow → 0
  - Remaining values → forward fill
- Removal of:
  - Target leakage (TAVG)
  - Sparse/non-informative columns

### 3.3 Feature Engineering

#### Time-Based Features
- Year, Month, Day
- Day of year, Week of year

#### Cyclical Encoding
- sin(day_of_year), cos(day_of_year)

#### Lag Features
- 1, 3, 7, 14 day lags for TMAX and TMIN

#### Rolling Features
- Rolling mean (7-day, 30-day)
- Rolling standard deviation

---

## 4. Model Development

### Models Used
- Ridge Regression (baseline linear model)
- Random Forest Regressor (ensemble learning)
- XGBoost Regressor (gradient boosting)

### Evaluation Metrics
- Mean Absolute Error (MAE)
- Root Mean Squared Error (RMSE)
- R² Score

The best-performing model is automatically selected and saved.

---

## 5. Model Interpretability

SHAP (SHapley Additive exPlanations) is used for:

- Feature importance ranking
- Global interpretation (summary plots)
- Local interpretation (dependence plots)

---

## 6. Real-Time Forecasting System

### API Integration
- OpenWeatherMap API used for live weather data

### Forecasting Strategy
- Combine:
  - ML predictions
  - Real-time API values
- Weighted blending:
  - 60% ML prediction
  - 40% API forecast

### Output
- Daily predictions for:
  - Maximum temperature (TMAX)
  - Minimum temperature (TMIN)
- 5-day rolling forecast saved
