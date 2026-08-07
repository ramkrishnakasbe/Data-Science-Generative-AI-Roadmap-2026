# 03_Time_Series_Forecasting_Models.md

# Time Series & Forecasting — Forecasting Models

## 1. Overview

Forecasting is the process of predicting future values using historical observations and, when available, external variables.

```text
Historical Data
      ↓
Data Preparation
      ↓
EDA
      ↓
Trend / Seasonality
      ↓
Stationarity
      ↓
Model Selection
      ↓
Train Model
      ↓
Forecast
      ↓
Evaluate
      ↓
Deploy & Monitor
```

This file covers the major forecasting models required for Data Science interviews:

* Naive Forecast
* Seasonal Naive
* Moving Average
* Simple Exponential Smoothing
* Holt's Method
* Holt-Winters
* AR
* MA
* ARMA
* ARIMA
* SARIMA
* SARIMAX
* VAR
* Prophet
* ML-based Forecasting
* Deep Learning Forecasting
* Forecast Evaluation
* Walk-Forward Validation
* Forecast Intervals
* Model Selection
* Interview Questions

---

# 2. Forecasting Problem

Suppose we have:

| Date     | Sales |
| -------- | ----: |
| Jan 2025 |   100 |
| Feb 2025 |   110 |
| Mar 2025 |   125 |
| Apr 2025 |   130 |

We want to predict future values:

```text
Jan 2026
Feb 2026
Mar 2026
...
```

General notation:

```text
Forecast = Ŷ(t+h)
```

Where:

* `t` = current time
* `h` = forecast horizon
* `Ŷ(t+h)` = predicted value h steps into the future

---

# 3. Forecast Horizon

Forecast horizon defines how far into the future we predict.

### Short-Term

```text
Next hour
Next day
Next week
```

### Medium-Term

```text
Next month
Next quarter
```

### Long-Term

```text
Next year
Next 5 years
```

The appropriate model and validation strategy depend heavily on the forecast horizon.

---

# 4. Major Forecasting Approaches

```text
Forecasting
│
├── Statistical
│   ├── Naive
│   ├── Moving Average
│   ├── Exponential Smoothing
│   ├── AR
│   ├── MA
│   ├── ARMA
│   ├── ARIMA
│   └── SARIMA
│
├── Regression / Machine Learning
│   ├── Linear Regression
│   ├── Random Forest
│   ├── XGBoost
│   └── LightGBM
│
├── Deep Learning
│   ├── RNN
│   ├── LSTM
│   ├── GRU
│   └── Transformer
│
└── Specialized / Hybrid
    ├── SARIMAX
    ├── Prophet
    └── Ensemble Models
```

---

# 5. Naive Forecast

The simplest forecasting method.

The next forecast equals the most recent observed value.

```text
Ŷ(t+1) = Y(t)
```

Example:

```text
Monday    = 100
Tuesday   = 120
Wednesday = 130
```

Forecast:

```text
Thursday = 130
```

---

# 6. Why Naive Forecast Is Important

Naive forecasting is an important baseline.

A sophisticated forecasting model should ideally outperform a reasonable naive benchmark.

```text
Naive Model
     ↓
Baseline
     ↓
Advanced Model
     ↓
Compare Performance
```

If a complex model does not outperform the baseline, the added complexity may not be justified.

---

# 7. Seasonal Naive Forecast

For seasonal data, forecast using the value from the previous season.

General formula:

```text
Ŷ(t) = Y(t-m)
```

Where:

* `m` = seasonal period

For monthly data with yearly seasonality:

```text
m = 12
```

Therefore:

```text
January 2026 Forecast
=
January 2025 Actual
```

Seasonal naive is often a strong baseline for seasonal business data.

---

# 8. Moving Average Forecast

Moving Average forecasting uses the average of recent observations.

For a 3-period moving average:

```text
Ŷ(t+1) = [Y(t) + Y(t-1) + Y(t-2)] / 3
```

Example:

```text
100, 110, 120

Forecast
= (100 + 110 + 120) / 3
= 110
```

---

# 9. Limitations of Moving Average

Advantages:

* Simple
* Easy to understand
* Smooths random noise

Limitations:

* Can lag behind trends
* Equal weight is assigned to observations
* Does not naturally handle seasonality
* Can perform poorly when the underlying process changes rapidly

---

# 10. Exponential Smoothing

Exponential smoothing assigns more weight to recent observations.

Basic formula:

```text
S(t) = αY(t) + (1-α)S(t-1)
```

Where:

* `S(t)` = smoothed value
* `Y(t)` = current observation
* `α` = smoothing parameter
* `0 < α < 1`

---

# 11. Interpretation of Alpha

### High Alpha

```text
α → 1
```

More weight is given to recent observations.

The model reacts quickly to changes.

### Low Alpha

```text
α → 0
```

More smoothing occurs.

The model reacts more slowly to changes.

---

# 12. Simple Exponential Smoothing

Simple Exponential Smoothing is suitable when the series has:

```text
No strong trend
No strong seasonality
```

Model:

```text
S(t) = αY(t) + (1-α)S(t-1)
```

Forecast:

```text
Ŷ(t+h) = S(t)
```

for future horizons `h`.

---

# 13. Python — Simple Exponential Smoothing

```python
from statsmodels.tsa.holtwinters import SimpleExpSmoothing

model = SimpleExpSmoothing(train)

fit = model.fit()

forecast = fit.forecast(
    steps=len(test)
)
```

---

# 14. Holt's Linear Trend Method

Simple Exponential Smoothing cannot explicitly model trend.

Holt's method adds a trend component.

Level:

```text
l(t) = αY(t) + (1-α)[l(t-1) + b(t-1)]
```

Trend:

```text
b(t) = β[l(t) - l(t-1)] + (1-β)b(t-1)
```

Forecast:

```text
Ŷ(t+h) = l(t) + h × b(t)
```

Where:

* `l(t)` = level
* `b(t)` = trend
* `α` = level smoothing parameter
* `β` = trend smoothing parameter

---

# 15. When to Use Holt's Method

Use Holt's method when the series has:

```text
Trend
+
No strong seasonality
```

Example:

```text
100
110
120
130
140
150
```

Holt's method can capture the upward trend.

---

# 16. Holt-Winters Method

Holt-Winters extends exponential smoothing to handle:

```text
Level
Trend
Seasonality
```

Therefore:

```text
Holt-Winters
=
Level
+
Trend
+
Seasonality
```

It is useful for data with repeated seasonal patterns.

---

# 17. Holt-Winters Components

Holt-Winters can use:

```text
Trend:
Additive / Multiplicative

Seasonality:
Additive / Multiplicative
```

Example:

```python
from statsmodels.tsa.holtwinters import ExponentialSmoothing

model = ExponentialSmoothing(
    train,
    trend="add",
    seasonal="add",
    seasonal_periods=12
)

fit = model.fit()

forecast = fit.forecast(
    len(test)
)
```

---

# 18. Additive vs Multiplicative Seasonality

## Additive Seasonality

Seasonal effect is approximately constant.

```text
Y(t) = Trend(t) + Seasonality(t) + Error(t)
```

Example:

```text
Every December:
+500 units
```

The seasonal effect is approximately constant.

---

## Multiplicative Seasonality

Seasonal effect is proportional to the level.

```text
Y(t) = Trend(t) × Seasonality(t) × Error(t)
```

Example:

```text
December sales are approximately 20% higher
than the normal level.
```

---

# 19. Autoregressive Model — AR

AR models use previous observations to predict the current observation.

AR(p):

```text
Y(t) =
c
+ φ1Y(t-1)
+ φ2Y(t-2)
+ ...
+ φpY(t-p)
+ ε(t)
```

Where:

* `p` = number of lagged observations
* `φ` = AR coefficients
* `c` = constant
* `ε(t)` = error term

---

# 20. AR(1)

AR(1) uses one previous observation.

```text
Y(t) = c + φ1Y(t-1) + ε(t)
```

Conceptually:

```text
Today's Value
      ↑
Yesterday's Value
```

The current value depends on the previous value.

---

# 21. AR(p)

AR(p) uses multiple lagged observations.

For AR(3):

```text
Y(t) =
c
+ φ1Y(t-1)
+ φ2Y(t-2)
+ φ3Y(t-3)
+ ε(t)
```

---

# 22. Moving Average Model — MA

The MA model uses previous forecast errors.

MA(q):

```text
Y(t) =
c
+ ε(t)
+ θ1ε(t-1)
+ θ2ε(t-2)
+ ...
+ θqε(t-q)
```

Where:

* `q` = number of previous errors
* `θ` = MA coefficients
* `ε(t)` = current error

Important:

> MA in time-series modeling is different from a simple moving average used for smoothing.

---

# 23. ARMA

ARMA combines:

```text
AR
+
MA
```

ARMA(p,q):

```text
Y(t) =
c
+ φ1Y(t-1)
+ ...
+ φpY(t-p)
+ ε(t)
+ θ1ε(t-1)
+ ...
+ θqε(t-q)
```

ARMA is generally applied to stationary time series.

---

# 24. ARIMA

ARIMA stands for:

```text
AutoRegressive
Integrated
Moving Average
```

Notation:

```text
ARIMA(p,d,q)
```

Where:

```text
p = AR order
d = Differencing order
q = MA order
```

---

# 25. Meaning of ARIMA Parameters

```text
ARIMA(p,d,q)
       │ │ │
       │ │ └── MA order
       │ └──── Differencing order
       └────── AR order
```

Example:

```text
ARIMA(2,1,1)
```

means:

```text
p = 2
d = 1
q = 1
```

---

# 26. ARIMA Concept

ARIMA handles non-stationary data by applying differencing.

General workflow:

```text
Original Series
      ↓
Differencing
      ↓
Stationary Series
      ↓
AR + MA
      ↓
Forecast
```

---

# 27. Differencing

First-order differencing:

```text
Y'(t) = Y(t) - Y(t-1)
```

Example:

```text
Original:
100 → 110 → 125 → 140

First Difference:
10 → 15 → 15
```

If one difference makes the series appropriately stationary:

```text
d = 1
```

---

# 28. ARIMA in Python

```python
from statsmodels.tsa.arima.model import ARIMA

model = ARIMA(
    train,
    order=(2, 1, 1)
)

fit = model.fit()

forecast = fit.forecast(
    steps=len(test)
)
```

---

# 29. Choosing AR Order

ACF and PACF can provide initial guidance.

For an AR process:

```text
ACF  → tails off
PACF → cuts off around p
```

Example:

```text
PACF:

Lag 1 → Significant
Lag 2 → Significant
Lag 3 → Insignificant
Lag 4 → Insignificant
```

Possible starting point:

```text
p = 2
```

ACF/PACF are diagnostic guides, not absolute rules.

---

# 30. Choosing MA Order

For an MA process:

```text
ACF  → cuts off around q
PACF → tails off
```

Example:

```text
ACF:

Lag 1 → Significant
Lag 2 → Significant
Lag 3 → Insignificant
```

Possible starting point:

```text
q = 2
```

---

# 31. Choosing Differencing Order

`d` represents the number of regular differences.

Workflow:

```text
Original Series
      ↓
Check Stationarity
      ↓
Non-Stationary?
      ↓
First Difference
      ↓
Check Again
      ↓
Repeat only if necessary
```

Avoid unnecessary differencing because excessive differencing can introduce additional noise and make the model harder to interpret.

---

# 32. SARIMA

SARIMA stands for:

```text
Seasonal AutoRegressive
Integrated Moving Average
```

Notation:

```text
SARIMA(p,d,q)(P,D,Q,m)
```

Where:

```text
p = non-seasonal AR order
d = non-seasonal differencing
q = non-seasonal MA order

P = seasonal AR order
D = seasonal differencing
Q = seasonal MA order

m = seasonal period
```

---

# 33. Example of SARIMA

For monthly data with yearly seasonality:

```text
SARIMA(1,1,1)(1,1,1,12)
```

Meaning:

```text
Non-seasonal:
p = 1
d = 1
q = 1

Seasonal:
P = 1
D = 1
Q = 1

Seasonal Period:
m = 12
```

---

# 34. Why SARIMA?

Use SARIMA when the series has:

```text
Non-seasonal dynamics
+
Seasonal dynamics
```

Example:

```text
Monthly Sales
+
Yearly Seasonality
+
Trend
```

---

# 35. SARIMA Workflow

```text
Time Series
     ↓
EDA
     ↓
Identify Seasonality
     ↓
Check Stationarity
     ↓
Regular Differencing
     ↓
Seasonal Differencing
     ↓
ACF / PACF
     ↓
Candidate SARIMA Models
     ↓
Validation
     ↓
Final Model
```

---

# 36. SARIMA in Python

```python
from statsmodels.tsa.statespace.sarimax import SARIMAX

model = SARIMAX(
    train,
    order=(1, 1, 1),
    seasonal_order=(1, 1, 1, 12)
)

fit = model.fit(
    disp=False
)

forecast = fit.forecast(
    steps=len(test)
)
```

---

# 37. SARIMAX

SARIMAX stands for:

```text
Seasonal ARIMA
+
Exogenous Variables
```

It allows external variables to influence the forecast.

Example:

```text
                 ┌── Price
                 │
Sales Forecast ←─┼── Promotion
                 │
                 ├── Holiday
                 │
                 └── Weather
```

---

# 38. Exogenous Variables

Exogenous variables are external predictors.

Examples:

### Demand Forecasting

```text
Price
Discount
Promotion
Holiday
Weather
```

### Energy Forecasting

```text
Temperature
Humidity
Wind Speed
```

### Financial Forecasting

```text
Interest Rate
Exchange Rate
Economic Indicators
```

---

# 39. SARIMAX Example

```python
model = SARIMAX(
    train["sales"],
    exog=train[["price", "promotion"]],
    order=(1, 1, 1),
    seasonal_order=(1, 1, 1, 12)
)

fit = model.fit()

forecast = fit.get_forecast(
    steps=len(test),
    exog=test[["price", "promotion"]]
)
```

Important:

> Future values of exogenous variables must be known or separately forecasted.

---

# 40. ARIMA vs SARIMA vs SARIMAX

| Model   | Non-Seasonal Dynamics | Seasonality                    | External Variables |
| ------- | --------------------- | ------------------------------ | ------------------ |
| ARIMA   | Yes                   | No explicit seasonal structure | No                 |
| SARIMA  | Yes                   | Yes                            | No                 |
| SARIMAX | Yes                   | Yes                            | Yes                |

---

# 41. VAR

VAR stands for:

```text
Vector Autoregression
```

It is used when multiple time series influence one another.

Example:

```text
Sales
Price
Advertising
```

These variables may influence each other over time.

Instead of modeling:

```text
Sales
```

alone, VAR models multiple variables jointly.

---

# 42. VAR Concept

For multiple variables:

```text
Y(t) =
A1Y(t-1)
+ A2Y(t-2)
+ ...
+ ApY(t-p)
+ ε(t)
```

Here `Y(t)` is a vector containing multiple time series.

Example:

```text
Y(t) =
[
    Sales
    Price
]
```

---

# 43. When to Use VAR

Use VAR when:

* Multiple time series are available
* Variables may influence one another
* Variables need to be modeled jointly
* The data satisfies the assumptions/transformations required by the VAR model

Example:

```text
Sales
Price
Advertising
```

---

# 44. Prophet

Prophet is a forecasting framework designed for business time series.

It can model:

* Trend
* Seasonality
* Holidays
* Special events
* External regressors
* Missing observations

Conceptually:

```text
y(t) = g(t) + s(t) + h(t) + ε(t)
```

Where:

```text
g(t) = Trend
s(t) = Seasonality
h(t) = Holiday Effects
ε(t) = Error
```

---

# 45. Prophet Components

```text
Prophet
│
├── Trend
├── Seasonality
├── Holiday Effects
└── Error
```

Prophet can automatically model common:

```text
Daily Seasonality
Weekly Seasonality
Yearly Seasonality
```

---

# 46. Prophet Data Format

Prophet generally expects two columns:

```text
ds
y
```

Example:

| ds         |   y |
| ---------- | --: |
| 2025-01-01 | 100 |
| 2025-01-02 | 105 |
| 2025-01-03 | 110 |

Where:

```text
ds = Date/Time
y  = Target
```

---

# 47. Prophet Example

```python
from prophet import Prophet

model = Prophet(
    yearly_seasonality=True,
    weekly_seasonality=True
)

model.fit(train)

future = model.make_future_dataframe(
    periods=30
)

forecast = model.predict(
    future
)
```

---

# 48. Prophet vs ARIMA

| Feature          | ARIMA                                | Prophet             |
| ---------------- | ------------------------------------ | ------------------- |
| Autocorrelation  | Strong focus                         | Less direct focus   |
| Trend            | Through model structure/differencing | Explicit trend      |
| Seasonality      | SARIMA extension                     | Built-in components |
| Holidays         | External setup                       | Built-in support    |
| Missing dates    | More sensitive                       | More flexible       |
| Interpretability | Statistical                          | Component-based     |

Neither model is universally better.

Model selection should be based on validation performance and business requirements.

---

# 49. Machine Learning for Time Series

Traditional ML models can be used for forecasting by converting time-series data into supervised learning data.

Original:

```text
Time → Sales
```

Transform into:

```text
Features:

Lag_1
Lag_2
Lag_3
Rolling_Mean
Month
Day_of_Week
Holiday

Target:

Sales
```

---

# 50. Lag Features

Lag features represent previous observations.

```python
df["lag_1"] = df["sales"].shift(1)
df["lag_7"] = df["sales"].shift(7)
df["lag_12"] = df["sales"].shift(12)
```

For daily data:

```text
lag_1
→ Yesterday

lag_7
→ Same weekday last week
```

For monthly data:

```text
lag_12
→ Same month last year
```

---

# 51. Rolling Features

Rolling statistics capture local patterns.

```python
df["rolling_mean_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .mean()
)

df["rolling_std_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .std()
)
```

Important:

> Shift before calculating the rolling feature when predicting the current observation, so the feature does not include the target's actual value.

---

# 52. Calendar Features

Useful calendar features include:

```text
Year
Month
Quarter
Week
Day
Day of Week
Weekend
Holiday
Financial Year
```

Example:

```python
df["month"] = df.index.month
df["quarter"] = df.index.quarter
df["day_of_week"] = df.index.dayofweek
```

---

# 53. Cyclical Encoding

Calendar variables such as month and day-of-week are cyclical.

For month:

```text
Month_Sin = sin(2π × Month / 12)

Month_Cos = cos(2π × Month / 12)
```

This helps the model understand:

```text
December → January
```

as neighboring points in a cycle.

---

# 54. ML Forecasting Pipeline

```text
Raw Time Series
      ↓
Create Lag Features
      ↓
Create Rolling Features
      ↓
Create Calendar Features
      ↓
Add External Variables
      ↓
Time-Based Split
      ↓
Train ML Model
      ↓
Forecast
      ↓
Evaluate
```

---

# 55. XGBoost for Forecasting

XGBoost can model nonlinear relationships among:

```text
Lag Features
Rolling Features
Calendar Features
External Variables
```

Example:

```python
from xgboost import XGBRegressor

model = XGBRegressor(
    n_estimators=500,
    learning_rate=0.05,
    max_depth=6
)

model.fit(
    X_train,
    y_train
)

pred = model.predict(
    X_test
)
```

---

# 56. Random Forest for Forecasting

Random Forest can also be used after converting the time series into supervised learning data.

```python
from sklearn.ensemble import RandomForestRegressor

model = RandomForestRegressor(
    n_estimators=300,
    random_state=42
)

model.fit(
    X_train,
    y_train
)

pred = model.predict(
    X_test
)
```

Random Forest does not inherently understand temporal order.

Temporal information must be encoded through:

```text
Lag Features
Rolling Features
Calendar Features
```

---

# 57. Statistical vs ML Forecasting

| Feature                 | Statistical Models | ML Models       |
| ----------------------- | ------------------ | --------------- |
| Autocorrelation         | Explicit           | Feature-based   |
| External Variables      | SARIMAX            | Easy            |
| Nonlinear Relationships | Limited            | Strong          |
| Feature Engineering     | Lower              | Higher          |
| Large Feature Sets      | Limited            | Strong          |
| Interpretability        | Often strong       | Model-dependent |
| Complex Interactions    | Limited            | Strong          |

---

# 58. Deep Learning Forecasting

Common deep-learning models:

```text
RNN
LSTM
GRU
Transformer
Temporal CNN
```

These models can be useful for:

* Large datasets
* Complex temporal relationships
* Nonlinear patterns
* Multiple interacting features
* Long sequences

However:

> Deep learning is not automatically better than classical forecasting models.

---

# 59. LSTM Forecasting

LSTM can learn temporal dependencies.

Conceptually:

```text
Previous Observations
        ↓
      LSTM
        ↓
    Prediction
```

Example:

```text
[100, 105, 110, 120, 125]
              ↓
            LSTM
              ↓
            130
```

LSTM is more appropriate when the data volume and problem complexity justify deep learning.

---

# 60. Direct vs Recursive Forecasting

Suppose we need:

```text
t+1
t+2
t+3
```

## Recursive Forecasting

```text
Predict t+1
    ↓
Use t+1 prediction
    ↓
Predict t+2
    ↓
Use t+2 prediction
    ↓
Predict t+3
```

## Direct Forecasting

Train separate models:

```text
Model 1 → t+1
Model 2 → t+2
Model 3 → t+3
```

---

# 61. Recursive Forecasting

Advantages:

* One model
* Simple implementation

Disadvantages:

* Errors can accumulate
* Later predictions depend on earlier predictions

```text
Error at t+1
      ↓
Affects t+2
      ↓
Affects t+3
      ↓
Potentially larger forecast error
```

---

# 62. Direct Forecasting

Advantages:

* Avoids recursive error propagation
* Each forecast horizon can have its own model

Disadvantages:

* Requires multiple models
* More computationally expensive
* More maintenance
* Different horizons may learn different relationships

---

# 63. Multi-Step Forecasting

Common approaches:

```text
Recursive
Direct
Direct-Recursive
Multi-Output
```

Choice depends on:

* Forecast horizon
* Data size
* Model type
* Error propagation
* Computational resources

---

# 64. Forecast Evaluation

Common forecasting metrics:

```text
MAE
MSE
RMSE
MAPE
sMAPE
WAPE
MASE
```

---

# 65. MAE

Mean Absolute Error:

```text
MAE = (1/n) × Σ|yᵢ - ŷᵢ|
```

Where:

```text
yᵢ  = Actual value
ŷᵢ  = Forecast value
n   = Number of observations
```

Advantages:

* Easy to interpret
* Same units as target
* Less sensitive to large errors than MSE/RMSE

---

# 66. MSE

Mean Squared Error:

```text
MSE = (1/n) × Σ(yᵢ - ŷᵢ)²
```

Large errors receive disproportionately higher penalties.

---

# 67. RMSE

Root Mean Squared Error:

```text
RMSE = √[(1/n) × Σ(yᵢ - ŷᵢ)²]
```

Advantages:

* Same units as target
* Penalizes large errors more strongly than MAE

---

# 68. MAPE

Mean Absolute Percentage Error:

```text
MAPE = (100/n) × Σ |(yᵢ - ŷᵢ) / yᵢ|
```

Problem:

> MAPE becomes problematic when actual values are zero or close to zero.

---

# 69. sMAPE

Symmetric Mean Absolute Percentage Error:

```text
sMAPE =
(100/n) × Σ
[
  |yᵢ - ŷᵢ|
  /
  ((|yᵢ| + |ŷᵢ|) / 2)
]
```

It reduces some asymmetry issues of MAPE but still has limitations around zero.

---

# 70. WAPE

Weighted Absolute Percentage Error:

```text
WAPE =
[Σ|yᵢ - ŷᵢ| / Σ|yᵢ|] × 100
```

Useful for aggregate demand and sales forecasting.

---

# 71. MASE

Mean Absolute Scaled Error compares forecast error against a naive benchmark.

```text
MASE =
MAE of Forecast
----------------
MAE of Naive Forecast
```

Interpretation:

```text
MASE < 1
→ Better than naive benchmark

MASE = 1
→ Same as naive benchmark

MASE > 1
→ Worse than naive benchmark
```

---

# 72. Choosing Forecast Metrics

| Situation                    | Useful Metrics        |
| ---------------------------- | --------------------- |
| General forecasting          | MAE, RMSE             |
| Large errors are important   | RMSE                  |
| Percentage interpretation    | MAPE                  |
| Zeros present                | MAE, RMSE, WAPE, MASE |
| Comparing different scales   | MASE                  |
| Aggregate demand forecasting | WAPE, MASE            |

No single metric is universally best.

---

# 73. Time-Based Train-Test Split

Never randomly shuffle ordinary time-series data for forecasting evaluation.

Incorrect:

```text
Random Train/Test Split
```

Preferred:

```text
Past
 ↓
Train
 ↓
Validation
 ↓
Test
 ↓
Future
```

Example:

```text
2022 ───────── 2023 ───────── 2024 ───────── 2025
|--------------|--------------|--------------|
    Train          Validation       Test
```

---

# 74. Why Random Split Is Dangerous

Suppose:

```text
Train:
Jan 2024
Mar 2024
May 2024
```

Test:

```text
Feb 2024
Apr 2024
```

The model can indirectly learn information from future observations.

This creates:

```text
Temporal Leakage
```

and produces overly optimistic evaluation.

---

# 75. Walk-Forward Validation

Walk-forward validation repeatedly trains using historical observations and evaluates on future observations.

```text
Fold 1:
Train → Test

Fold 2:
Train + New Data → Test

Fold 3:
More Historical Data → Test
```

This better simulates real forecasting.

---

# 76. Expanding Window

Example:

```text
Train:
[1 2 3]
Test:
[4]

Train:
[1 2 3 4]
Test:
[5]

Train:
[1 2 3 4 5]
Test:
[6]
```

Training data continuously expands.

---

# 77. Rolling Window

Example:

```text
Train:
[1 2 3]
Test:
[4]

Train:
[2 3 4]
Test:
[5]

Train:
[3 4 5]
Test:
[6]
```

The training window remains fixed.

Useful when old observations become less representative of current behavior.

---

# 78. TimeSeriesSplit

Scikit-learn provides:

```python
from sklearn.model_selection import TimeSeriesSplit

tscv = TimeSeriesSplit(
    n_splits=5
)
```

It creates sequential train/test splits.

For real forecasting, custom walk-forward validation may be preferable when you need:

```text
Fixed Forecast Horizon
Gap Between Train and Test
Rolling Window
Expanding Window
```

---

# 79. Forecast Intervals

A point forecast provides one value:

```text
Forecast = 150
```

An interval forecast provides a range:

```text
95% Prediction Interval:
[130, 172]
```

A prediction interval represents uncertainty around a future observation under the model's assumptions and interval construction.

---

# 80. Point Forecast vs Interval Forecast

### Point Forecast

```text
Ŷ(t+h)
```

### Interval Forecast

```text
[L(t+h), U(t+h)]
```

Where:

```text
L = Lower Bound
U = Upper Bound
```

Business decisions often benefit from intervals rather than point forecasts alone.

---

# 81. Forecast Bias

Forecast bias measures systematic overprediction or underprediction.

A simple mean signed error is:

```text
Bias = (1/n) × Σ(yᵢ - ŷᵢ)
```

Interpretation depends on the sign convention.

Using:

```text
Actual - Forecast
```

then:

```text
Positive Bias
→ Model tends to underestimate

Negative Bias
→ Model tends to overestimate
```

---

# 82. Forecast Residuals

Residual:

```text
e(t) = Y(t) - Ŷ(t)
```

Good residuals should ideally show:

```text
No obvious trend
No obvious seasonality
No significant autocorrelation
Stable variance
Mean close to zero
```

If residuals contain strong structure, the model may not have captured all available information.

---

# 83. Residual Diagnostics

Important diagnostics:

```text
Residual Plot
ACF of Residuals
Histogram
Q-Q Plot
Ljung-Box Test
```

### Ljung-Box Test

Used to test whether residual autocorrelations are collectively significant.

A good forecasting model should generally leave residuals that are approximately uncorrelated.

---

# 84. Model Selection

Do not select a forecasting model only because it has the lowest training error.

Use:

```text
Business Understanding
        ↓
Baseline
        ↓
Candidate Models
        ↓
Time-Series Validation
        ↓
Forecast Metrics
        ↓
Residual Diagnostics
        ↓
Business Constraints
        ↓
Final Model
```

---

# 85. AIC

AIC stands for:

```text
Akaike Information Criterion
```

AIC balances model fit and model complexity.

Formula:

```text
AIC = 2k - 2ln(L)
```

Where:

```text
k = Number of estimated parameters
L = Likelihood
```

Lower AIC is generally preferred when comparing suitable models fitted to the same data.

---

# 86. BIC

BIC stands for:

```text
Bayesian Information Criterion
```

Formula:

```text
BIC = k × ln(n) - 2ln(L)
```

Where:

```text
k = Number of parameters
n = Number of observations
L = Likelihood
```

BIC penalizes model complexity more strongly than AIC as sample size grows.

---

# 87. AIC vs BIC

| AIC                                 | BIC                         |
| ----------------------------------- | --------------------------- |
| Complexity penalty                  | Stronger complexity penalty |
| Often favors predictive flexibility | Often favors simpler models |
| Useful for model comparison         | Useful for model comparison |

Important:

> AIC and BIC should not replace proper out-of-sample forecasting validation.

---

# 88. Forecasting Workflow — Interview Ready

```text
1. Understand Business Problem
        ↓
2. Define Forecast Horizon
        ↓
3. Prepare Time Index
        ↓
4. Handle Missing Values
        ↓
5. Explore Trend / Seasonality
        ↓
6. Build Naive Baseline
        ↓
7. Check Stationarity
        ↓
8. Create Candidate Models
        ↓
9. Time-Based Validation
        ↓
10. Compare Metrics
        ↓
11. Residual Diagnostics
        ↓
12. Select Final Model
        ↓
13. Retrain
        ↓
14. Forecast Future
        ↓
15. Monitor Performance
```

---

# 89. Practical Model Selection

## No Trend, No Seasonality

```text
Naive
Simple Exponential Smoothing
```

## Trend, No Seasonality

```text
Holt
ARIMA
```

## Trend + Seasonality

```text
Holt-Winters
SARIMA
Prophet
```

## External Variables

```text
SARIMAX
XGBoost
LightGBM
```

## Multiple Interacting Time Series

```text
VAR
```

## Complex Nonlinear Patterns + Large Dataset

```text
XGBoost
LSTM
Transformer
```

This is a starting point, not a rigid rule.

---

# 90. Sales Forecasting Example

Suppose a company wants to forecast monthly sales.

Available data:

```text
Date
Sales
Price
Promotion
Holiday
```

Possible approach:

```text
Sales
 ↓
EDA
 ↓
Trend + Seasonality
 ↓
Naive Baseline
 ↓
SARIMA
 ↓
SARIMAX
 ↓
XGBoost
 ↓
Compare
 ↓
Select
```

---

# 91. Feature Engineering for Sales Forecasting

Possible features:

```text
Lag 1
Lag 3
Lag 6
Lag 12

Rolling Mean 3
Rolling Mean 6
Rolling Mean 12

Month
Quarter
Holiday
Promotion
Price
```

Example:

```python
df["lag_1"] = df["sales"].shift(1)
df["lag_12"] = df["sales"].shift(12)

df["rolling_3"] = (
    df["sales"]
    .shift(1)
    .rolling(3)
    .mean()
)
```

Important:

```text
shift(1)
```

ensures the rolling feature uses only historical information when predicting the current period.

---

# 92. Data Leakage in Forecasting

Data leakage occurs when information unavailable at prediction time is used to create features or train the model.

Bad:

```python
df["rolling_mean"] = (
    df["sales"]
    .rolling(7)
    .mean()
)
```

If used to predict the current value, this may include the current actual value.

Better:

```python
df["rolling_mean"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .mean()
)
```

---

# 93. Forecasting with Known Future Variables

Suppose:

```text
Sales ← Promotion
```

If future promotions are already planned, they can be used.

If future promotions are unknown:

```text
Forecast Promotion
        ↓
Use Promotion Forecast
        ↓
Forecast Sales
```

Uncertainty in future exogenous variables adds uncertainty to the final sales forecast.

---

# 94. Intermittent Demand

Some products have many zero-demand periods.

Example:

```text
0
0
5
0
0
0
10
0
```

Examples:

```text
Spare Parts
Slow-Moving Inventory
Rare Product Sales
```

Standard forecasting approaches and metrics may perform poorly.

Specialized methods include:

```text
Croston
SBA
TSB
```

---

# 95. Hierarchical Forecasting

Forecasts can exist at multiple levels.

Example:

```text
Company
│
├── Region
│   ├── State
│   │   ├── City
│   │   └── City
│   │
│   └── State
│
└── Region
```

Forecasts should ideally be coherent across levels.

Example:

```text
Total Sales
=
North Sales
+
South Sales
+
West Sales
+
East Sales
```

This is called:

```text
Hierarchical Forecasting
```

and forecast reconciliation can be used to make forecasts coherent.

---

# 96. Univariate vs Multivariate Forecasting

## Univariate

Uses only historical values of the target.

```text
Sales → Sales Forecast
```

Examples:

```text
ARIMA
SARIMA
ETS
```

## Multivariate

Uses multiple variables.

```text
Sales
Price
Promotion
Weather
Holiday
```

Examples:

```text
SARIMAX
VAR
XGBoost
LSTM
```

---

# 97. ARIMA vs XGBoost — Interview Question

### Question

When would you prefer ARIMA over XGBoost?

### Answer

I would consider ARIMA when the forecasting problem is primarily driven by temporal autocorrelation and the dataset is relatively focused on the target series.

I would consider XGBoost when I have multiple explanatory variables, nonlinear relationships, complex feature interactions, or a feature-rich dataset.

The final choice should be based on time-series validation performance.

---

# 98. ARIMA vs LSTM — Interview Question

### Question

Is LSTM always better than ARIMA?

### Answer

No.

LSTM requires sufficient data and careful tuning. For smaller datasets or relatively simple temporal structures, ARIMA, SARIMA, or exponential smoothing can perform as well as or better than LSTM.

Model selection should depend on:

```text
Data Size
Pattern Complexity
Validation Performance
Forecast Horizon
Computational Cost
Interpretability
```

---

# 99. Why Is Naive Forecast Important?

### Interview Answer

A naive forecast provides a simple benchmark.

If a complex model cannot consistently outperform a reasonable naive or seasonal-naive model on proper out-of-sample validation, the added complexity may not be justified.

---

# 100. Why Can't We Use Random Train-Test Split?

### Interview Answer

Time-series observations are ordered.

Random splitting can allow information from the future to enter the training set.

This causes:

```text
Temporal Leakage
```

and results in overly optimistic performance estimates.

---

# 101. What Is Walk-Forward Validation?

### Interview Answer

Walk-forward validation repeatedly trains a model using historical observations and evaluates it on future observations.

The training window can either:

```text
Expand
```

or:

```text
Roll Forward
```

This better represents how the model will operate in production.

---

# 102. What Is Forecast Horizon?

The forecast horizon is the number of future periods being predicted.

Example:

```text
Forecast next 12 months

Forecast Horizon = 12
```

---

# 103. What Is Recursive Forecasting?

The model predicts one future step and then uses that prediction as input for the next step.

```text
t+1 Prediction
      ↓
t+2 Prediction
      ↓
t+3 Prediction
```

Main problem:

```text
Prediction errors can accumulate.
```

---

# 104. What Is Direct Forecasting?

A separate model is trained for each forecast horizon.

```text
Model 1 → t+1
Model 2 → t+2
Model 3 → t+3
```

Advantage:

```text
Reduced recursive error propagation
```

Disadvantage:

```text
More models
More computation
More maintenance
```

---

# 105. What Is SARIMAX?

SARIMAX is:

```text
Seasonal ARIMA
+
Exogenous Variables
```

Example:

```text
Sales
 ↑
 ├── Historical Sales
 ├── Price
 ├── Promotion
 └── Holiday
```

It is useful when external variables contain information that improves the target forecast.

---

# 106. What Is Seasonality Period?

The seasonality period is the number of observations in one complete seasonal cycle.

Examples:

| Data Frequency |      Seasonal Period |
| -------------- | -------------------: |
| Hourly         |   24 for daily cycle |
| Daily          |   7 for weekly cycle |
| Weekly         | ~52 for yearly cycle |
| Monthly        |  12 for yearly cycle |
| Quarterly      |   4 for yearly cycle |

Multiple seasonalities can exist.

Example:

```text
Hourly Data
├── Daily Seasonality = 24
└── Weekly Seasonality = 168
```

---

# 107. Forecasting Model Cheat Sheet

```text
Naive
→ Last observed value

Seasonal Naive
→ Same season from previous cycle

Simple Exponential Smoothing
→ Level

Holt
→ Level + Trend

Holt-Winters
→ Level + Trend + Seasonality

AR
→ Previous values

MA
→ Previous errors

ARMA
→ AR + MA

ARIMA
→ AR + Differencing + MA

SARIMA
→ ARIMA + Seasonality

SARIMAX
→ SARIMA + External Variables

VAR
→ Multiple interacting time series

Prophet
→ Trend + Seasonality + Holidays

XGBoost
→ Lag + Rolling + Calendar + External Features

LSTM
→ Neural Sequence Modeling
```

---

# 108. Complete Interview Revision Table

| Model          | Trend                         | Seasonality                    | External Variables            | Stationarity                       |
| -------------- | ----------------------------- | ------------------------------ | ----------------------------- | ---------------------------------- |
| Naive          | Implicit                      | No                             | No                            | No                                 |
| Seasonal Naive | Implicit                      | Yes                            | No                            | No                                 |
| SES            | Level                         | No                             | No                            | No                                 |
| Holt           | Yes                           | No                             | No                            | No                                 |
| Holt-Winters   | Yes                           | Yes                            | No                            | No                                 |
| AR             | Through dynamics              | Not explicit                   | No                            | Generally yes                      |
| MA             | Through errors                | Not explicit                   | No                            | Generally yes                      |
| ARMA           | Through dynamics              | Not explicit                   | No                            | Yes                                |
| ARIMA          | Through differencing          | No explicit seasonal structure | No                            | Stationary after differencing      |
| SARIMA         | Yes                           | Yes                            | No                            | Stationary representation          |
| SARIMAX        | Yes                           | Yes                            | Yes                           | Stationary representation          |
| VAR            | Through multivariate dynamics | Not inherently seasonal        | Multiple endogenous variables | Usually stationary or transformed  |
| Prophet        | Yes                           | Yes                            | Regressors / holidays         | No strict stationarity requirement |
| XGBoost        | Feature-based                 | Feature-based                  | Yes                           | No strict stationarity requirement |
| LSTM           | Learned                       | Learned                        | Yes                           | No strict stationarity requirement |

---

# 109. Important Formula Cheat Sheet

## Naive

```text
Ŷ(t+1) = Y(t)
```

## Seasonal Naive

```text
Ŷ(t) = Y(t-m)
```

## Moving Average

```text
Ŷ(t+1)
=
[Y(t) + Y(t-1) + ... + Y(t-k+1)] / k
```

## Simple Exponential Smoothing

```text
S(t) = αY(t) + (1-α)S(t-1)
```

## Holt

```text
Level:
l(t) = αY(t) + (1-α)[l(t-1) + b(t-1)]

Trend:
b(t) = β[l(t)-l(t-1)] + (1-β)b(t-1)

Forecast:
Ŷ(t+h) = l(t) + h × b(t)
```

## AR(p)

```text
Y(t) =
c
+ φ1Y(t-1)
+ φ2Y(t-2)
+ ...
+ φpY(t-p)
+ ε(t)
```

## MA(q)

```text
Y(t) =
c
+ ε(t)
+ θ1ε(t-1)
+ θ2ε(t-2)
+ ...
+ θqε(t-q)
```

## Differencing

```text
Y'(t) = Y(t) - Y(t-1)
```

## Seasonal Differencing

```text
Y'(t) = Y(t) - Y(t-m)
```

## MAE

```text
MAE = (1/n) × Σ|yᵢ - ŷᵢ|
```

## MSE

```text
MSE = (1/n) × Σ(yᵢ - ŷᵢ)²
```

## RMSE

```text
RMSE = √[(1/n) × Σ(yᵢ - ŷᵢ)²]
```

## MAPE

```text
MAPE = (100/n) × Σ |(yᵢ - ŷᵢ) / yᵢ|
```

## WAPE

```text
WAPE =
[Σ|yᵢ - ŷᵢ| / Σ|yᵢ|] × 100
```

## MASE

```text
MASE =
MAE(Forecast)
------------
MAE(Naive)
```

## Bias

```text
Bias = (1/n) × Σ(yᵢ - ŷᵢ)
```

## AIC

```text
AIC = 2k - 2ln(L)
```

## BIC

```text
BIC = k × ln(n) - 2ln(L)
```

---

# 110. Final Interview Checklist

Before saying a forecasting model is ready:

```text
☑ Business objective defined
☑ Forecast horizon defined
☑ Forecast frequency defined
☑ Time index correct
☑ Missing dates checked
☑ Missing values handled
☑ Outliers investigated
☑ Trend analyzed
☑ Seasonality analyzed
☑ Stationarity checked where relevant
☑ Naive baseline created
☑ Seasonal baseline created when appropriate
☑ Candidate models evaluated
☑ Time-based validation used
☑ Temporal leakage prevented
☑ Forecast metrics calculated
☑ Residual diagnostics performed
☑ Prediction intervals considered
☑ Model compared against baseline
☑ Business constraints considered
☑ Model monitoring planned
```

---

# 111. One-Minute Interview Answer

> I start a forecasting problem by understanding the business objective, forecast horizon, data frequency, and available historical and external variables. I perform time-series EDA to identify trend, seasonality, outliers, missing values, and structural changes. I establish a naive or seasonal-naive baseline and then evaluate suitable statistical and machine-learning models such as exponential smoothing, ARIMA, SARIMA, SARIMAX, Prophet, or tree-based models using lag, rolling, calendar, and external features. I use time-based or walk-forward validation rather than random splitting, evaluate models using metrics such as MAE, RMSE, WAPE, or MASE depending on the business problem, and perform residual diagnostics. Finally, I select the model based on out-of-sample performance, stability, interpretability, operational requirements, and business impact.
