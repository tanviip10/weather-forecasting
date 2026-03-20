# Real-Time Weather Forecasting Using Machine Learning Techniques

## 1. Introduction

This project implements an end-to-end real-time weather forecasting system that integrates:

- Historical NOAA weather data
- Time-series feature engineering
- Machine learning regression models
- Model interpretability using SHAP
- Live weather data integration via API

The system predicts daily maximum (TMAX) and minimum (TMIN) temperatures and generates short-term forecasts using a hybrid machine learning and API-based approach.

---

## 2. Dataset Description

- Source: NOAA Global Historical Climatology Network (GHCN-Daily)
- Station: JFK International Airport, New York
- Time Period: January 2010 – December 2025

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
- Distribution analysis and outlier detection
- Correlation analysis between variables

### 3.2 Data Preprocessing
- Datetime conversion and indexing for time-series modeling
- Missing value handling:
  - Weather event flags replaced with 0
  - Precipitation and snow values filled with 0
  - Remaining missing values handled using forward fill
- Removal of:
  - Target leakage feature (TAVG)
  - Sparse or non-informative columns

### 3.3 Feature Engineering

#### Time-Based Features
- Year, month, day
- Day of year
- Week of year

#### Cyclical Encoding
- Sine and cosine transformation of day_of_year to preserve seasonality

#### Lag Features
- Lag values at 1, 3, 7, and 14 days for TMAX and TMIN

#### Rolling Features
- Rolling mean (7-day and 30-day windows)
- Rolling standard deviation to capture variability

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

The best-performing model is selected based on RMSE and saved for deployment.

---

## 5. Model Interpretability

SHAP (SHapley Additive exPlanations) is used to:

- Identify important features influencing predictions
- Provide global interpretability through summary plots
- Analyze feature impact using dependence plots

---

## 6. Real-Time Forecasting System

### API Integration
- OpenWeatherMap API is used to fetch real-time weather data

### Forecasting Strategy
- Combines:
  - Machine learning predictions
  - Real-time API observations
- Weighted blending approach:
  - 60% machine learning prediction
  - 40% API-based values

### Output
- Daily predictions:
  - Maximum temperature (TMAX)
  - Minimum temperature (TMIN)
- 5-day rolling forecast saved as: forecast_output.csv

---

## 7. Key Highlights

- Time-series aware feature engineering
- Multi-model training and comparison
- Hybrid forecasting approach (ML + API)
- Model interpretability using SHAP
- Real-time prediction capability

---

## 8. Future Work

- Implementation of deep learning models (LSTM, GRU, Transformers)
- Hyperparameter optimization using Optuna
- Deployment via FastAPI or Streamlit
- Multi-location forecasting capability
- Automated model retraining pipeline
