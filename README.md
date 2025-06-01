# 🏎️ F1 Barcelona GP 2025 Winner Prediction

This project uses historical F1 data from the 2024 Spanish Grand Prix (Barcelona) to build a machine learning model that predicts the results of the 2025 Barcelona GP. The primary focus is on leveraging historical race data, qualifying performance, and various contextual feature to forecast race outcomes using Scikit-Learn's SVR (Support Vector Regression), which yielded the best prediction accuracy among tested models.

## Data Sources

- **FastF1 API**: Used to collect session data (laps, weather, car telemetry, etc.)
- **OpenWeatherMap API**: fetched race-day weather forecasts.
- **2024 Spanish Grand Prix**: Used as the training dataset
- **2025 Qualifying Session Data**: Used for inference

## Key Technologies

- Python 
- [FastF1](https://theoehrly.github.io/Fast-F1/) API
- Scikit-Learn
- Pandas, NumPy

## Project Highlights

- Processed telemetry and session data from the 2024 Barcelona GP.
- Engineered features such as sector times, tyre compounds, weather conditions, and driver/team metadata.
- Built multiple regression models to predict 2025 finishing positions.
- **SVR (Support Vector Regression)** showed the best performance in terms of RMSE and ranking accuracy.

## Features Used

The feature set reflects a blend of performance, environmental, and historical metrics:

- `QualifyingTime`: Time set by the driver in Q3 of the 2025 session.
- `RainProbability`: Forecasted rain chance (from OpenWeatherMap).
- `Temperature`: Ambient temperature at forecasted race time.
- `TeamPerformanceScore`: Normalized constructor points from the 2025 standings.
- `TireDegradation`: Median tire degradation per driver from 2024 race stint data.
- `RecentForm`: Recent performance metric calculated using past race points.
- `TotalSectorTime`: Aggregated average sector times from the 2024 race.

## Models Trained

Three regression models were tested for predicting average race lap time (proxy for race performance):

1. **SVR (Support Vector Regression)** *(Best Performance)*
   - Kernel: RBF
   - C: 1.5, Epsilon: 0.1

2. **KNeighborsRegressor**
   - n_neighbors: 3
   - Distance-weighted voting

3. **XGBRegressor (Extreme Gradient Boosting)**
   - Used for training + feature importance plotting.
   - Revealed `QualifyingTime` and `TeamPerformanceScore` as dominant factors.

### Feature Importance (XGBoost)

A plot was generated showing feature importance using XGBoost, indicating that:

- `QualifyingTime` had the strongest predictive power.
- `TeamPerformanceScore`, `RecentForm`, and `TireDegradation` followed.
- Several features used in the model, such as `TeamPerformanceScore`, `RecentForm`, and `TireDegradation`, were derived by combining and interpreting various elements available through the FastF1 API. This feature engineering was carried out by aggregating and interpreting multiple raw metrics such as stint lengths, lap times, tire compounds, constructor standings, and driver performance trends, helping the model capture underlying patterns in race dynamics and ultimately improving its predictive accuracy.
<img width="787" alt="image" src="https://github.com/user-attachments/assets/61458856-21de-45b0-97df-da7afb9eb51f" />


## Results

- Predictions showed high correlation with actual results, with notable success in predicting podium finishes.
- However, **Max Verstappen**, who was predicted to finish **3rd**, ended up in **10th** due to **a 10-second penalty**, an unforeseen race event that the model could not account for.
  1. Oscar Piastri
  2. Lando Norris
  3. Max Verstappen *(actual: 10th due to penalty)*

## Limitations

- **External Race Factors**: The model does not account for:
  - On-track incidents (crashes, penalties)
  - Strategic miscalculations (pit stops, tyre choices)
  - Mechanical failures
- **Qualifying-Based Prediction**: Since predictions are based on qualifying performance, in-race dynamics are simplified.


