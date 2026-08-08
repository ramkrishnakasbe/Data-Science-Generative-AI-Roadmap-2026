# 04_Time_Series_Advanced_Interview.md

# Time Series & Forecasting — Advanced Concepts & Interview Questions

---

## 1. Forecast Horizon

Forecast horizon is the number of future time periods we want to predict.

```text
Historical Data
      ↓
Train Data
      ↓
Forecast
      ↓
t+1  t+2  t+3  t+4
```

Example:

```text
Forecast next 7 days
→ Forecast Horizon = 7
```

---

## 2. Forecasting Strategies

### Recursive Forecasting

One model predicts one step at a time.

```text
t+1 → t+2 → t+3 → t+4
```

The previous prediction becomes an input for the next prediction.

### Direct Forecasting

Separate models are trained for each horizon.

```text
Model 1 → t+1
Model 2 → t+2
Model 3 → t+3
```

### Multi-Output Forecasting

One model predicts multiple future values.

```text
Model
 ↓
[t+1, t+2, t+3, t+4]
```

---

## 3. Recursive vs Direct Forecasting

| Recursive              | Direct                                |
| ---------------------- | ------------------------------------- |
| One model              | Multiple models                       |
| Easier to maintain     | More models to maintain               |
| Errors can accumulate  | Less recursive error accumulation     |
| Good for many horizons | Good when horizons behave differently |

---

# 4. Walk-Forward Validation

Walk-forward validation simulates real-world forecasting.

```text
Fold 1

Train: ███████
Test:         █


Fold 2

Train: ████████
Test:          █


Fold 3

Train: █████████
Test:           █
```

The model is repeatedly trained using past data and tested on future data.

---

# 5. Expanding Window

Training data continuously increases.

```text
Train → Test

██████ → █

███████ → █

████████ → █

█████████ → █
```

Useful when old historical data remains relevant.

---

# 6. Rolling Window

The training window moves forward.

```text
██████ → █

 ██████ → █

  ██████ → █

   ██████ → █
```

Useful when recent observations are more relevant than older observations.

---

# 7. Time Series Cross-Validation

Standard K-Fold cross-validation should generally not be used directly for forecasting because it can violate temporal ordering.

Instead use:

```text
TimeSeriesSplit
Walk-Forward Validation
Rolling Validation
Expanding Window
```

Python:

```python
from sklearn.model_selection import TimeSeriesSplit

tscv = TimeSeriesSplit(n_splits=5)

for train_index, test_index in tscv.split(X):
    X_train = X.iloc[train_index]
    X_test = X.iloc[test_index]

    y_train = y.iloc[train_index]
    y_test = y.iloc[test_index]
```

---

# 8. Forecast Error

Forecast error:

```text
e(t) = Y(t) - Y_hat(t)
```

Where:

```text
Y(t) = Actual value
Y_hat(t) = Forecast value
```

---

# 9. MAE

Mean Absolute Error:

```text
MAE =
Σ |Y(t) - Y_hat(t)|
---------------------
n
```

Advantages:

* Easy to understand
* Same unit as target
* Less sensitive to outliers than RMSE

Lower MAE is better.

---

# 10. MSE

Mean Squared Error:

```text
MSE =
Σ [Y(t) - Y_hat(t)]²
---------------------
n
```

Large errors receive much larger penalties.

---

# 11. RMSE

Root Mean Squared Error:

```text
RMSE =
√[
Σ [Y(t) - Y_hat(t)]²
---------------------
n
]
```

RMSE has the same unit as the target.

---

# 12. MAPE

Mean Absolute Percentage Error:

```text
MAPE =
100 × (1/n) ×
Σ
|
(Y(t) - Y_hat(t))
------------------
Y(t)
|
```

Problem:

MAPE becomes problematic when actual values are zero or close to zero.

---

# 13. WAPE

Weighted Absolute Percentage Error:

```text
WAPE =
Σ |Y(t) - Y_hat(t)|
--------------------
Σ |Y(t)|
```

Useful for business forecasting where total volume matters.

---

# 14. MASE

Mean Absolute Scaled Error:

```text
MASE =
Forecast MAE
----------------
Naive Forecast MAE
```

Interpretation:

```text
MASE < 1
→ Better than naive model

MASE > 1
→ Worse than naive model
```

---

# 15. Forecast Bias

Forecast bias:

```text
Bias =
Mean(Y(t) - Y_hat(t))
```

If:

```text
Bias > 0
```

The model is generally under-forecasting.

If:

```text
Bias < 0
```

The model is generally over-forecasting.

---

# 16. Prediction Interval

A point forecast gives:

```text
Forecast = 1000
```

A prediction interval gives:

```text
Forecast = 1000

Lower Bound = 900
Upper Bound = 1120
```

Prediction intervals communicate forecast uncertainty.

---

# 17. Forecast Uncertainty

Generally:

```text
Forecast Horizon ↑
        ↓
Uncertainty ↑
```

Therefore:

```text
t+1
→ relatively lower uncertainty

t+30
→ higher uncertainty
```

---

# 18. Residual Analysis

Residual:

```text
Residual = Actual - Forecast
```

Good residuals should ideally have:

```text
Mean ≈ 0
No significant autocorrelation
Stable variance
No obvious trend
No obvious seasonality
```

---

# 19. Residual Autocorrelation

If residuals are autocorrelated:

```text
Residual
   ↓
ACF
   ↓
Significant correlation
```

This suggests the model has not captured all temporal structure.

---

# 20. Ljung-Box Test

Ljung-Box test checks whether residual autocorrelations are jointly significant.

Hypotheses:

```text
H0:
No significant autocorrelation

H1:
Significant autocorrelation exists
```

Interpretation:

```text
p-value > 0.05
→ Fail to reject H0
→ Residuals may be uncorrelated

p-value < 0.05
→ Reject H0
→ Evidence of autocorrelation
```

---

# 21. White Noise Residuals

A good forecasting model should leave residuals that resemble white noise.

```text
Actual
  ↓
Model
  ↓
Residual
  ↓
White Noise
```

If residuals contain predictable structure, the model can potentially be improved.

---

# 22. Heteroscedasticity

Heteroscedasticity means that residual variance changes over time.

Example:

```text
Early Period
→ Small errors

Later Period
→ Large errors
```

This indicates non-constant variance.

Possible approaches:

```text
Log Transformation
Box-Cox Transformation
Model Variance Explicitly
Robust Methods
```

---

# 23. Log Transformation

For positive data:

```text
Y' = log(Y)
```

Useful when:

* Variance increases with level
* Data is highly right-skewed
* Multiplicative patterns exist

Python:

```python
import numpy as np

df["log_sales"] = np.log1p(df["sales"])
```

---

# 24. Box-Cox Transformation

Box-Cox transformation can stabilize variance.

For λ ≠ 0:

```text
Y(λ) =
[Y^λ - 1]
----------
λ
```

For λ = 0:

```text
Y(λ) = log(Y)
```

Box-Cox generally requires positive values.

---

# 25. Concept Drift

Concept drift occurs when the relationship between variables changes over time.

Example:

```text
Before:
Price ↑ → Demand ↓

After:
Price ↑ → Demand changes differently
```

A previously trained model may degrade.

---

# 26. Data Drift vs Concept Drift

### Data Drift

Input distribution changes.

```text
P(X)
changes
```

### Concept Drift

Relationship between input and target changes.

```text
P(Y | X)
changes
```

---

# 27. Handling Concept Drift

Possible approaches:

```text
Rolling Training Window
Frequent Retraining
Recent Data Weighting
Model Monitoring
Drift Detection
Champion-Challenger Models
```

---

# 28. Hierarchical Forecasting

Example:

```text
Company
│
├── North
│   ├── Product A
│   └── Product B
│
└── South
    ├── Product A
    └── Product B
```

Forecasts exist at multiple levels.

---

# 29. Forecast Reconciliation

Suppose:

```text
Total = 1000

North = 600
South = 400
```

Then:

```text
600 + 400 = 1000
```

Reconciliation ensures forecasts at different hierarchy levels are coherent.

---

# 30. Univariate Forecasting

Only one target series is modeled.

```text
Historical Sales
      ↓
Forecast Sales
```

Examples:

```text
ARIMA
SARIMA
ETS
Holt-Winters
```

---

# 31. Multivariate Forecasting

Multiple variables are used.

Example:

```text
Sales
Price
Promotion
Holiday
Weather
```

Models:

```text
SARIMAX
VAR
XGBoost
LightGBM
Neural Networks
```

---

# 32. Exogenous Variables

External variables that influence the target are called exogenous variables.

Examples:

```text
Price
Promotion
Weather
Holiday
Economic Indicators
Competitor Price
```

SARIMAX can incorporate such variables.

---

# 33. Lag Features

Lag features represent previous observations.

```text
lag_1  = Y(t-1)

lag_7  = Y(t-7)

lag_14 = Y(t-14)

lag_28 = Y(t-28)
```

Python:

```python
df["lag_1"] = df["sales"].shift(1)
df["lag_7"] = df["sales"].shift(7)
df["lag_28"] = df["sales"].shift(28)
```

---

# 34. Rolling Features

Rolling statistics summarize recent history.

```python
df["rolling_mean_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .mean()
)
```

The `shift(1)` is important because it prevents the current target from entering the feature.

---

# 35. Temporal Leakage

Temporal leakage occurs when future information is used during model training.

Incorrect:

```text
Current Sales
     ↓
Rolling Mean
     ↓
Feature
```

Correct:

```text
Previous Sales
     ↓
Rolling Mean
     ↓
Feature
```

Rule:

> Every feature must be available at the exact time when the forecast is generated.

---

# 36. Calendar Features

Common features:

```text
Year
Month
Quarter
Week
Day of Week
Day of Month
Weekend
Holiday
```

Python:

```python
df["month"] = df.index.month
df["day_of_week"] = df.index.dayofweek
df["quarter"] = df.index.quarter
```

---

# 37. Cyclical Encoding

Months are cyclical.

December and January are close in time.

Use:

```text
month_sin =
sin(2π × month / 12)
```

```text
month_cos =
cos(2π × month / 12)
```

Python:

```python
import numpy as np

df["month_sin"] = np.sin(
    2 * np.pi * df["month"] / 12
)

df["month_cos"] = np.cos(
    2 * np.pi * df["month"] / 12
)
```

---

# 38. Baseline Models

Always create a simple baseline.

Common baselines:

```text
Naive Forecast
Seasonal Naive
Moving Average
Drift Method
```

Example:

```text
Naive Forecast:

Y_hat(t+1) = Y(t)
```

If an advanced model cannot beat the baseline, reconsider using the complex model.

---

# 39. Seasonal Naive Forecast

Seasonal naive forecasting uses the value from the previous seasonal cycle.

For monthly data with yearly seasonality:

```text
Y_hat(t) = Y(t-12)
```

For daily data with weekly seasonality:

```text
Y_hat(t) = Y(t-7)
```

---

# 40. ARIMA vs Machine Learning

### ARIMA

Best when:

```text
Strong temporal dependence
Limited external variables
Relatively structured series
```

### Machine Learning

Useful when:

```text
Many features
Nonlinear relationships
External variables
Large datasets
Complex interactions
```

---

# 41. XGBoost for Time Series

XGBoost does not inherently understand time.

We convert time-series data into supervised learning.

Example:

```text
Features:

lag_1
lag_7
lag_14
rolling_mean_7
rolling_mean_28
month
day_of_week
holiday
price

Target:

sales(t)
```

Then train:

```python
from xgboost import XGBRegressor

model = XGBRegressor()

model.fit(X_train, y_train)

prediction = model.predict(X_test)
```

---

# 42. LSTM for Time Series

LSTM stands for:

**Long Short-Term Memory**

It is a recurrent neural network architecture designed to model sequential dependencies.

Architecture:

```text
Input Sequence
      ↓
LSTM
      ↓
Dense Layer
      ↓
Forecast
```

Useful when:

```text
Large datasets
Complex nonlinear patterns
Long sequential dependencies
```

But LSTM should not automatically be preferred over simpler models.

---

# 43. Transformer for Time Series

Transformers use attention mechanisms to capture relationships across sequence positions.

Conceptually:

```text
Historical Sequence
        ↓
Attention
        ↓
Representation
        ↓
Forecast
```

They can be powerful for large and complex forecasting problems.

---

# 44. Forecasting Pipeline

```text
Raw Data
   ↓
Data Cleaning
   ↓
Datetime Processing
   ↓
EDA
   ↓
Trend / Seasonality
   ↓
Stationarity
   ↓
Baseline
   ↓
Feature Engineering
   ↓
Model Training
   ↓
Time-Based Validation
   ↓
Hyperparameter Tuning
   ↓
Evaluation
   ↓
Residual Analysis
   ↓
Forecast
   ↓
Deployment
   ↓
Monitoring
```

---

# 45. Forecasting Interview Questions

## Q1. What is time-series forecasting?

Time-series forecasting is predicting future observations using historical time-dependent data and potentially external variables.

---

## Q2. What are the major components of a time series?

```text
Trend
Seasonality
Cyclical Component
Residual
```

---

## Q3. What is stationarity?

A stationary series has statistical properties such as mean, variance, and autocovariance structure that remain stable over time.

---

## Q4. How do you make a series stationary?

```text
Differencing
Seasonal Differencing
Log Transformation
Box-Cox Transformation
Detrending
```

---

## Q5. What is the difference between ACF and PACF?

ACF measures correlation between observations at different lags.

PACF measures the correlation at a particular lag after accounting for intermediate lags.

---

## Q6. What is ARIMA?

ARIMA combines:

```text
AR → Autoregression
I  → Integration / Differencing
MA → Moving Average
```

It is represented as:

```text
ARIMA(p,d,q)
```

---

## Q7. What is SARIMA?

SARIMA extends ARIMA with seasonal components.

```text
SARIMA(p,d,q)(P,D,Q,m)
```

Where:

```text
p = AR order
d = Differencing order
q = MA order

P = Seasonal AR order
D = Seasonal differencing
Q = Seasonal MA order
m = Seasonal period
```

---

## Q8. What is SARIMAX?

SARIMAX is SARIMA with exogenous variables.

```text
SARIMA
   +
External Variables
   =
SARIMAX
```

---

## Q9. Why should random train-test splitting be avoided?

Because future observations can enter the training dataset, causing temporal leakage.

---

## Q10. What is walk-forward validation?

A validation strategy where the model is trained using historical observations and tested on subsequent future observations repeatedly.

---

## Q11. How would you evaluate a forecasting model?

I would use:

```text
MAE
RMSE
WAPE
MASE
MAPE / sMAPE when appropriate
```

and also examine:

```text
Forecast Bias
Residual Autocorrelation
Business Impact
```

---

## Q12. What is temporal leakage?

Temporal leakage happens when information that would not have been available at prediction time is used in training or feature engineering.

---

## Q13. What is concept drift?

Concept drift occurs when the relationship between predictors and target changes over time.

---

## Q14. What is the difference between rolling and expanding windows?

```text
Rolling:
Fixed-size training window

Expanding:
Training window continuously grows
```

---

## Q15. How do you handle seasonality?

Possible approaches:

```text
Seasonal Naive
Holt-Winters
SARIMA
SARIMAX
Seasonal Features
Fourier Features
Machine Learning
```

---

# 46. Scenario-Based Interview Questions

## Scenario 1

### Problem

You have 5 years of monthly sales data with strong yearly seasonality.

### Approach

```text
1. Validate data
2. Sort by date
3. Check missing values
4. Analyze trend
5. Analyze 12-month seasonality
6. Create seasonal-naive baseline
7. Test stationarity
8. Try Holt-Winters
9. Try SARIMA
10. Try SARIMAX if external variables exist
11. Use walk-forward validation
12. Compare MAE / WAPE / RMSE
13. Check residuals
14. Select final model
15. Monitor after deployment
```

---

## Scenario 2

### Problem

The model performs very well during testing but poorly after deployment.

### Possible Causes

```text
Temporal Leakage
Data Drift
Concept Drift
Incorrect Feature Generation
Production Data Issues
Incorrect Validation
Future Information Used During Training
```

---

## Scenario 3

### Problem

Forecasts consistently underestimate demand.

### Investigate

```text
Forecast Bias
Recent Trend
Seasonality
Promotions
Price
External Variables
Concept Drift
Outdated Training Data
Loss Function
```

---

## Scenario 4

### Problem

You have daily sales data with weekly seasonality.

### Approach

```text
Seasonal Period = 7

Create:
lag_1
lag_7
lag_14
rolling_mean_7
rolling_mean_28
day_of_week
holiday
promotion
```

Then compare:

```text
Seasonal Naive
SARIMA
SARIMAX
XGBoost
```

using time-based validation.

---

# 47. Important Model Selection Framework

```text
                Time Series
                     ↓
             Understand Data
                     ↓
          Trend + Seasonality
                     ↓
              Build Baseline
                     ↓
         ┌───────────┴───────────┐
         ↓                       ↓
 Statistical                  ML / DL
 Models                        Models
         ↓                       ↓
 ARIMA                       XGBoost
 SARIMA                      LightGBM
 SARIMAX                     LSTM
 ETS                         Transformer
         ↓                       ↓
         └───────────┬───────────┘
                     ↓
           Time-Based Validation
                     ↓
               Error Metrics
                     ↓
             Residual Analysis
                     ↓
              Model Selection
                     ↓
                 Forecast
                     ↓
               Deployment
                     ↓
                Monitoring
```

---

# 48. Production Monitoring

Monitor:

```text
Forecast Accuracy
Forecast Bias
Data Quality
Missing Values
Feature Drift
Prediction Drift
Concept Drift
Business KPIs
```

Example:

```text
Actual Sales
     ↓
Forecast
     ↓
Error
     ↓
Monitoring
     ↓
Performance Degradation?
     ↓
Retrain
```

---

# 49. Retraining Strategies

### Scheduled Retraining

```text
Daily
Weekly
Monthly
Quarterly
```

### Trigger-Based Retraining

Retrain when:

```text
Accuracy drops
Data drift detected
Concept drift detected
Business behavior changes
```

---

# 50. Important Interview Cheat Sheet

```text
TREND
→ Long-term direction

SEASONALITY
→ Repeating pattern at fixed intervals

CYCLICAL
→ Long-term fluctuations without fixed periodicity

STATIONARITY
→ Stable statistical properties

ADF
→ H0: Unit root / non-stationary

KPSS
→ H0: Stationary

ACF
→ Autocorrelation

PACF
→ Partial autocorrelation

AR
→ Previous observations

MA
→ Previous errors

ARIMA
→ AR + Differencing + MA

SARIMA
→ ARIMA + Seasonality

SARIMAX
→ SARIMA + Exogenous Variables

ETS
→ Error + Trend + Seasonality

WALK-FORWARD
→ Time-aware validation

MAE
→ Average absolute error

RMSE
→ Penalizes large errors

WAPE
→ Business-oriented percentage error

MASE
→ Comparison against naive forecast

LAG FEATURES
→ Previous observations

ROLLING FEATURES
→ Recent historical statistics

TEMPORAL LEAKAGE
→ Future information entering the model

CONCEPT DRIFT
→ Relationship changes over time

BASELINE
→ Simple benchmark

RESIDUALS
→ Actual - Forecast
```

---

# 51. Final Interview Preparation Checklist

```text
[ ] Understand Trend
[ ] Understand Seasonality
[ ] Understand Cyclicality
[ ] Understand Stationarity
[ ] ADF Test
[ ] KPSS Test
[ ] Differencing
[ ] ACF
[ ] PACF
[ ] AR
[ ] MA
[ ] ARIMA
[ ] SARIMA
[ ] SARIMAX
[ ] Holt-Winters
[ ] ETS
[ ] Naive Forecast
[ ] Seasonal Naive
[ ] Lag Features
[ ] Rolling Features
[ ] Calendar Features
[ ] Exogenous Variables
[ ] Temporal Leakage
[ ] Time-Based Split
[ ] Walk-Forward Validation
[ ] Rolling Window
[ ] Expanding Window
[ ] MAE
[ ] RMSE
[ ] MAPE
[ ] WAPE
[ ] MASE
[ ] Forecast Bias
[ ] Prediction Intervals
[ ] Residual Analysis
[ ] Ljung-Box Test
[ ] Concept Drift
[ ] Hierarchical Forecasting
[ ] XGBoost Forecasting
[ ] LSTM
[ ] Production Monitoring
[ ] Retraining
```

---

# 52. Most Important Topics for a Data Scientist

Focus most on:

```text
★★★★★

Stationarity
ADF / KPSS
ACF / PACF
Differencing
ARIMA
SARIMA
SARIMAX
Holt-Winters
Time-Based Validation
Walk-Forward Validation
Temporal Leakage
Lag Features
Rolling Features
Forecast Metrics
Residual Diagnostics
Forecast Bias
```

Then:

```text
★★★★

XGBoost Forecasting
Prediction Intervals
Concept Drift
Hierarchical Forecasting
VAR
LSTM
```

---

# 53. Final Mental Model

```text
                    TIME SERIES
                         ↓
                Understand Data
                         ↓
               Trend + Seasonality
                         ↓
                   Stationarity
                         ↓
                  Build Baseline
                         ↓
             Feature Engineering
                         ↓
        ┌────────────────┴────────────────┐
        ↓                                 ↓
 Statistical Models                 ML / Deep Learning
        ↓                                 ↓
 ARIMA / SARIMA                     XGBoost / LSTM
 SARIMAX / ETS                      Transformers
        ↓                                 ↓
        └────────────────┬────────────────┘
                         ↓
                Time-Based Validation
                         ↓
                  Error Metrics
                         ↓
                 Residual Analysis
                         ↓
                  Model Selection
                         ↓
                      Forecast
                         ↓
                Prediction Interval
                         ↓
                    Deployment
                         ↓
                    Monitoring
                         ↓
                     Retraining
```
