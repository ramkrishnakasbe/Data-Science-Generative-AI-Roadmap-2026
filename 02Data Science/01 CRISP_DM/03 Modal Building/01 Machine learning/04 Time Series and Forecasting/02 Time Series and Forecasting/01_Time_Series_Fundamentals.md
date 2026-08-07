# 01_Time_Series_Fundamentals.md

# Time Series & Forecasting — Fundamentals

## 1. What is Time Series?

A **time series** is a sequence of observations collected over time in chronological order.

Examples:

* Daily sales
* Monthly revenue
* Hourly electricity consumption
* Daily stock prices
* Monthly production
* Weekly demand

Example:

| Date  | Sales |
| ----- | ----: |
| Jan 1 |   100 |
| Jan 2 |   110 |
| Jan 3 |   105 |
| Jan 4 |   120 |

The most important characteristic of time-series data is:

> **Time/order matters.**

---

# 2. Time Series vs Normal Data

In normal machine-learning data, observations are often assumed to be independent.

In time-series data, observations can depend on previous observations.

Example:

```text
Today's Sales
      ↑
Yesterday's Sales
      ↑
Day Before Yesterday's Sales
```

Therefore, we cannot blindly shuffle time-series data before training a forecasting model.

---

# 3. What is Forecasting?

**Forecasting** means predicting future values using historical information.

Example:

```text
Historical Sales
      ↓
Time Series Model
      ↓
Future Sales
```

If we have:

```text
Jan → 100
Feb → 110
Mar → 120
Apr → 130
```

we may forecast:

```text
May → 140
```

---

# 4. Time Series vs Forecasting

### Time Series Analysis

Focuses on understanding the historical data.

It studies:

* Trend
* Seasonality
* Cycles
* Autocorrelation
* Stationarity
* Noise

### Forecasting

Focuses on predicting future values.

```text
Time Series Analysis
        ↓
Understand historical patterns
        ↓
Forecasting
        ↓
Predict future values
```

---

# 5. Components of Time Series

A time series commonly contains:

```text
Time Series
│
├── Level
├── Trend
├── Seasonality
├── Cyclicity
└── Noise
```

The important components for interviews are:

1. Level
2. Trend
3. Seasonality
4. Noise

---

# 6. Level

**Level** represents the average or baseline value of the series.

Example:

```text
100
105
98
102
101
```

The series is approximately centered around:

```text
100
```

So the level is approximately 100.

---

# 7. Trend

**Trend** represents the long-term direction of the time series.

### Increasing Trend

```text
100
110
120
130
140
```

The series is increasing.

### Decreasing Trend

```text
140
130
120
110
100
```

The series is decreasing.

Trend can be:

* Increasing
* Decreasing
* Approximately constant
* Nonlinear

---

# 8. Seasonality

**Seasonality** is a pattern that repeats at a known and fixed frequency.

Examples:

### Retail Sales

```text
December → High Sales
December → High Sales
December → High Sales
```

### Weekly Pattern

```text
Monday    → High
Tuesday   → Medium
...
Sunday    → Low
```

### Monthly Data

A yearly seasonal pattern usually has:

```text
12 months
```

---

# 9. Examples of Seasonality

| Data Frequency | Possible Seasonality |
| -------------- | -------------------- |
| Hourly         | Daily                |
| Daily          | Weekly               |
| Weekly         | Yearly               |
| Monthly        | Yearly               |
| Quarterly      | Yearly               |

Example:

```text
Monthly Sales

Jan → 100
Feb → 110
...
Dec → 200

Next Year:

Jan → 105
Feb → 115
...
Dec → 210
```

The repeated yearly pattern is seasonality.

---

# 10. Cyclicity

A **cycle** is a long-term rise and fall in a time series.

The important difference is:

> A cycle does not necessarily have a fixed and known frequency.

Example:

```text
Economic Growth
      ↓
Economic Peak
      ↓
Economic Decline
      ↓
Economic Recovery
```

---

# 11. Seasonality vs Cyclicity

| Seasonality                | Cyclicity                                     |
| -------------------------- | --------------------------------------------- |
| Repeats at known frequency | No fixed frequency                            |
| Usually predictable period | Duration can vary                             |
| Often calendar-related     | Often related to business/economic conditions |
| Christmas sales            | Economic cycle                                |

### Interview Answer

> Seasonality is a repeating pattern with a known frequency, while cyclicity represents longer-term fluctuations whose duration is not necessarily fixed.

---

# 12. Noise

**Noise** represents random variation that cannot be explained by the systematic patterns in the data.

Example:

```text
100
105
101
108
103
```

Some variation may simply be random.

Conceptually:

```text
Observed Data
=
Pattern
+
Noise
```

---

# 13. Time Series Decomposition

Decomposition means breaking a time series into different components.

A simple conceptual representation is:

```text
Time Series
    ↓
Trend
+
Seasonality
+
Noise
```

There are two common decomposition approaches:

1. Additive
2. Multiplicative

---

# 14. Additive Time Series

In an additive model:

```text
Y(t) = T(t) + S(t) + E(t)
```

Where:

```text
Y(t) = Observed value
T(t) = Trend
S(t) = Seasonal component
E(t) = Error / Noise
```

Use additive decomposition when the seasonal effect is approximately constant.

Example:

```text
Normal Sales = 1000

December effect = +200

Next year:

Normal Sales = 1500
December effect = +200
```

The seasonal effect remains approximately constant.

---

# 15. Multiplicative Time Series

In a multiplicative model:

```text
Y(t) = T(t) × S(t) × E(t)
```

Use multiplicative decomposition when seasonal variation changes with the level of the series.

Example:

```text
Normal Sales = 1000
December = 1200

Next year:

Normal Sales = 2000
December = 2400
```

The seasonal effect is proportional to the level.

---

# 16. Additive vs Multiplicative

| Additive                         | Multiplicative                        |
| -------------------------------- | ------------------------------------- |
| `Y(t) = T(t) + S(t) + E(t)`      | `Y(t) = T(t) × S(t) × E(t)`           |
| Seasonal effect roughly constant | Seasonal effect proportional to level |
| Constant seasonal amplitude      | Increasing seasonal amplitude         |
| Example: +100 every December     | Example: +20% every December          |

### Easy Rule

```text
Constant seasonal variation
        ↓
Additive

Seasonal variation increases with level
        ↓
Multiplicative
```

---

# 17. Time Series Frequency

Frequency tells us how often observations are recorded.

Examples:

```text
Hourly
Daily
Weekly
Monthly
Quarterly
Yearly
```

Example:

```text
Date        Sales

01-Jan      100
02-Jan      105
03-Jan      110
```

Frequency:

```text
Daily
```

---

# 18. Seasonal Period

The **seasonal period** is the number of observations required to complete one seasonal cycle.

Examples:

### Hourly Data

If there is daily seasonality:

```text
24 observations
```

So:

```text
m = 24
```

### Daily Data

If there is weekly seasonality:

```text
7 observations
```

So:

```text
m = 7
```

### Monthly Data

If there is yearly seasonality:

```text
12 observations
```

So:

```text
m = 12
```

### Quarterly Data

Yearly seasonality:

```text
m = 4
```

---

# 19. Univariate Time Series

A **univariate time series** contains one main variable measured over time.

Example:

```text
Date → Sales
```

Data:

| Date | Sales |
| ---- | ----: |
| Jan  |   100 |
| Feb  |   120 |
| Mar  |   130 |

Common models include:

* AR
* MA
* ARMA
* ARIMA
* SARIMA
* Exponential Smoothing

---

# 20. Multivariate Time Series

A **multivariate time series** contains multiple variables observed over time.

Example:

| Date | Sales | Price | Promotion | Temperature |
| ---- | ----: | ----: | --------: | ----------: |
| Jan  |   100 |    50 |         1 |          25 |
| Feb  |   120 |    48 |         1 |          28 |
| Mar  |   130 |    47 |         0 |          32 |

Here:

```text
Target:
Sales

Other variables:
Price
Promotion
Temperature
```

These additional variables can help forecast sales.

---

# 21. Exogenous Variables

An **exogenous variable** is an external variable that can help explain or predict the target.

Example:

```text
Sales
  ↑
  |
  ├── Price
  ├── Promotion
  ├── Holiday
  └── Weather
```

For example:

```text
Sales = f(
    Historical Sales,
    Price,
    Promotion,
    Holiday
)
```

Models such as SARIMAX can incorporate external variables.

---

# 22. Lag

A **lag** means using a previous value of a time series.

Suppose:

```text
Date    Sales

Day 1   100
Day 2   110
Day 3   120
Day 4   130
```

Lag 1 means:

```text
Day 4 prediction
        ↓
Previous Day Sales
        ↓
130 → 120
```

Mathematically:

```text
Lag 1 = Y(t-1)
```

Lag 2:

```text
Lag 2 = Y(t-2)
```

---

# 23. Lag Features

Lag features are commonly used in machine-learning forecasting.

Example:

```python
df["lag_1"] = df["sales"].shift(1)

df["lag_7"] = df["sales"].shift(7)

df["lag_30"] = df["sales"].shift(30)
```

Meaning:

```text
lag_1
→ Yesterday's sales

lag_7
→ Sales 7 periods ago

lag_30
→ Sales 30 periods ago
```

---

# 24. Rolling Statistics

Rolling statistics calculate statistics over a moving window.

Example:

```python
df["rolling_mean_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .mean()
)
```

This calculates the average of the previous 7 observations.

Common rolling features:

```text
Rolling Mean
Rolling Median
Rolling Standard Deviation
Rolling Minimum
Rolling Maximum
Rolling Sum
```

---

# 25. Why Use `shift()` Before Rolling?

Suppose we want to predict today's sales.

If we calculate:

```python
df["sales"].rolling(7).mean()
```

the current sales value can be included in the feature.

That can create **data leakage**.

Instead:

```python
df["sales"].shift(1).rolling(7).mean()
```

uses only information available before the prediction time.

---

# 26. Autocorrelation

**Autocorrelation** measures the relationship between a time series and its previous values.

Example:

```text
Today's Sales
      ↕
Yesterday's Sales
```

If today's sales are strongly related to yesterday's sales, there is autocorrelation.

Formula:

```text
ACF(k) = Corr(Y(t), Y(t-k))
```

Where:

```text
k = Lag
```

---

# 27. Positive Autocorrelation

Example:

```text
Yesterday → 100
Today     → 105

Yesterday → 200
Today     → 205
```

High values tend to follow high values.

Low values tend to follow low values.

This indicates positive autocorrelation.

---

# 28. Negative Autocorrelation

Negative autocorrelation means high values tend to be followed by low values and vice versa.

Example:

```text
100
50
110
45
120
```

The series alternates between high and low values.

---

# 29. Autocorrelation Function — ACF

The **Autocorrelation Function (ACF)** measures autocorrelation at different lag values.

Example:

```text
Lag 1 → Correlation
Lag 2 → Correlation
Lag 3 → Correlation
Lag 4 → Correlation
...
```

ACF is commonly used for:

* Understanding temporal dependence
* Detecting seasonality
* Identifying possible MA order

---

# 30. Partial Autocorrelation — PACF

PACF measures the direct relationship between the current value and a particular lag after accounting for intermediate lags.

Example:

```text
Y(t-3)
  ↓
Y(t-2)
  ↓
Y(t-1)
  ↓
Y(t)
```

PACF attempts to isolate the direct relationship between:

```text
Y(t)
```

and:

```text
Y(t-3)
```

after accounting for lags 1 and 2.

PACF is commonly useful for identifying possible AR order.

---

# 31. ACF vs PACF

| ACF                                     | PACF                             |
| --------------------------------------- | -------------------------------- |
| Measures correlation with lagged values | Measures direct lag relationship |
| Includes indirect relationships         | Controls for intermediate lags   |
| Useful for MA identification            | Useful for AR identification     |

Easy interview rule:

```text
ACF → MA

PACF → AR
```

This is a common diagnostic rule, not an absolute law.

---

# 32. Stationarity

A time series is **stationary** when its statistical properties remain reasonably stable over time.

For weak stationarity, commonly:

```text
Mean → Stable
Variance → Stable
Covariance → Depends on lag
```

Simple interview definition:

> A stationary time series has statistical properties that do not systematically change over time.

---

# 33. Why is Stationarity Important?

Several classical time-series models rely on stationarity or on transformations that produce a stationary series.

Examples:

```text
AR
MA
ARMA
ARIMA
VAR
```

If a series is non-stationary, we may need:

```text
Differencing
Transformation
Detrending
```

---

# 34. Example of Non-Stationary Series

Consider:

```text
100
120
140
160
180
```

The average level keeps increasing.

Therefore, the series is likely non-stationary because the mean changes over time.

---

# 35. Example of Stationary Series

Consider:

```text
100
95
103
98
102
97
101
```

The series fluctuates around a relatively stable level.

This may be stationary.

---

# 36. Causes of Non-Stationarity

Common causes:

```text
Trend
Seasonality
Changing Variance
Structural Changes
```

Example:

```text
Sales
  ↑
  |
  |       /
  |     /
  |   /
  | /
  +----------------→ Time
```

The increasing trend can cause non-stationarity.

---

# 37. How to Check Stationarity?

Common approaches:

```text
1. Visual inspection
2. Rolling mean
3. Rolling standard deviation
4. ADF test
5. KPSS test
```

Do not depend only on one statistical test.

---

# 38. Rolling Mean

Rolling mean calculates the mean over a moving window.

Example:

```python
df["rolling_mean"] = (
    df["sales"]
    .rolling(12)
    .mean()
)
```

If the rolling mean changes significantly over time, it may indicate non-stationarity.

---

# 39. Rolling Standard Deviation

Rolling standard deviation measures changing variability.

```python
df["rolling_std"] = (
    df["sales"]
    .rolling(12)
    .std()
)
```

If the variance changes significantly over time, the series may not be stationary.

---

# 40. Augmented Dickey-Fuller Test — ADF

ADF is one of the most commonly used stationarity tests.

### Null Hypothesis

```text
H0:
Series has a unit root
→ Non-stationary
```

### Alternative Hypothesis

```text
H1:
Series does not have a unit root
→ Stationary
```

Decision:

```text
p-value < 0.05
→ Reject H0
→ Evidence of stationarity

p-value >= 0.05
→ Fail to reject H0
→ Evidence is insufficient to claim stationarity
```

---

# 41. ADF Test in Python

```python
from statsmodels.tsa.stattools import adfuller

result = adfuller(
    df["sales"].dropna()
)

print("ADF Statistic:", result[0])
print("p-value:", result[1])
```

---

# 42. KPSS Test

KPSS is another stationarity test.

For the common level-stationarity version:

### Null Hypothesis

```text
H0:
Series is stationary
```

### Alternative Hypothesis

```text
H1:
Series is non-stationary
```

Decision:

```text
p-value < 0.05
→ Reject H0
→ Evidence of non-stationarity
```

---

# 43. ADF vs KPSS

The null hypotheses are opposite.

| Test | Null Hypothesis |
| ---- | --------------- |
| ADF  | Non-stationary  |
| KPSS | Stationary      |

Using both tests can provide stronger evidence.

A common pattern:

```text
ADF:
Reject H0

KPSS:
Fail to reject H0

        ↓

Evidence supporting stationarity
```

---

# 44. Differencing

Differencing is used to remove changes such as trend and help make a series stationary.

First-order differencing:

```text
Y'(t) = Y(t) - Y(t-1)
```

Example:

```text
Original:

100
110
125
140

First Difference:

10
15
15
```

---

# 45. Second-Order Differencing

If first-order differencing is not sufficient:

```text
Y''(t) = Y'(t) - Y'(t-1)
```

However:

> Avoid unnecessary differencing because excessive differencing can introduce unnecessary noise.

---

# 46. Seasonal Differencing

Seasonal differencing compares the current value with the value from the previous seasonal cycle.

Formula:

```text
Y'(t) = Y(t) - Y(t-m)
```

Where:

```text
m = Seasonal period
```

For monthly data with yearly seasonality:

```text
m = 12
```

Therefore:

```text
Y'(t) = Y(t) - Y(t-12)
```

---

# 47. Log Transformation

Log transformation can help stabilize variance.

Formula:

```text
Y' = log(Y)
```

Python:

```python
import numpy as np

df["sales_log"] = np.log(
    df["sales"]
)
```

For data containing zeros:

```python
df["sales_log"] = np.log1p(
    df["sales"]
)
```

---

# 48. White Noise

White noise is a random process with approximately:

```text
Mean ≈ 0
Constant variance
No meaningful autocorrelation
```

Example:

```text
2
-1
0
1
-2
0
1
```

A good forecasting model should ideally leave residuals that behave approximately like white noise.

---

# 49. Random Walk

A basic random walk is:

```text
Y(t) = Y(t-1) + E(t)
```

Where:

```text
E(t) = Random error
```

Example:

```text
100
105
103
110
108
115
```

The next value depends on the previous value plus random movement.

A basic random walk is generally non-stationary.

---

# 50. Residual

Residual is the difference between actual and predicted values.

Formula:

```text
Residual = Actual - Forecast
```

Or:

```text
E(t) = Y(t) - Y_hat(t)
```

Example:

```text
Actual   = 120
Forecast = 110

Residual = 120 - 110
         = 10
```

---

# 51. Good Residuals

Ideally, residuals should have:

```text
Mean ≈ 0
No trend
No seasonality
No significant autocorrelation
Stable variance
```

If residuals still contain patterns:

```text
Model
  ↓
Missed Pattern
```

The model may need improvement.

---

# 52. Forecasting Horizon

Forecast horizon means how far into the future we want to predict.

Example:

```text
Forecast next 1 day
→ Horizon = 1

Forecast next 7 days
→ Horizon = 7

Forecast next 12 months
→ Horizon = 12
```

---

# 53. One-Step Forecast

Predict only the next observation.

```text
Historical Data
       ↓
Predict t+1
```

Example:

```text
Jan
Feb
Mar
Apr
 ↓
Forecast May
```

---

# 54. Multi-Step Forecast

Predict multiple future observations.

```text
Historical Data
       ↓
May
June
July
August
```

Example:

```text
Forecast Horizon = 4
```

---

# 55. Baseline Forecast

Before using a complex model, create a simple baseline.

Common baselines:

```text
Naive Forecast
Seasonal Naive
Moving Average
```

The complex model should outperform a reasonable baseline on out-of-sample data.

---

# 56. Naive Forecast

The naive method predicts the next value using the most recent observed value.

Formula:

```text
Y_hat(t+1) = Y(t)
```

Example:

```text
Today's Sales = 500

Tomorrow's Forecast = 500
```

Very simple, but extremely important as a benchmark.

---

# 57. Seasonal Naive Forecast

Seasonal naive forecasting uses the value from the previous seasonal cycle.

Formula:

```text
Y_hat(t) = Y(t-m)
```

For monthly data with yearly seasonality:

```text
Y_hat(t) = Y(t-12)
```

Example:

```text
December 2025 Sales = 10,000

Forecast December 2026
≈ December 2025 Sales
```

---

# 58. Train-Test Split for Time Series

For time-series forecasting, data should normally be split chronologically.

Correct:

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

Incorrect for ordinary forecasting evaluation:

```text
Random Shuffle
      ↓
Random Train/Test
```

---

# 59. Why Random Train-Test Split is Dangerous?

Suppose:

```text
2024 Data → Training
2023 Data → Testing
```

The model has effectively learned from the future relative to the test period.

This creates temporal leakage.

Correct:

```text
2023 → Train
2024 → Test
```

---

# 60. Walk-Forward Validation

Walk-forward validation simulates real forecasting.

Example:

```text
Train:  Jan Feb Mar
Test:   Apr

Train:  Jan Feb Mar Apr
Test:   May

Train:  Jan Feb Mar Apr May
Test:   Jun
```

This is also called:

* Walk-forward validation
* Rolling-origin evaluation
* Backtesting

---

# 61. Expanding Window

Training data keeps increasing.

```text
Fold 1:
[1 2 3] → [4]

Fold 2:
[1 2 3 4] → [5]

Fold 3:
[1 2 3 4 5] → [6]
```

Useful when old historical data remains relevant.

---

# 62. Rolling Window

The training window moves forward.

```text
Fold 1:
[1 2 3] → [4]

Fold 2:
[2 3 4] → [5]

Fold 3:
[3 4 5] → [6]
```

Useful when recent history is more relevant than very old history.

---

# 63. Forecast Error

Forecast error is:

```text
Error = Actual - Forecast
```

Example:

```text
Actual   = 500
Forecast = 450

Error = 50
```

---

# 64. Common Forecasting Metrics

Important metrics:

```text
MAE
MSE
RMSE
MAPE
WAPE
MASE
sMAPE
```

The correct metric depends on the business problem.

---

# 65. MAE

Mean Absolute Error:

```text
MAE = (1/n) × Σ |Y(t) - Y_hat(t)|
```

Advantages:

* Easy to understand
* Same unit as target
* Less sensitive to large errors than RMSE

Example:

```text
MAE = 20

```

means the average absolute forecast error is 20 units.

---

# 66. RMSE

Root Mean Squared Error:

```text
RMSE = √[(1/n) × Σ(Y(t) - Y_hat(t))²]
```

RMSE penalizes large errors more strongly than MAE.

Use RMSE when large errors are particularly important.

---

# 67. MAPE

Mean Absolute Percentage Error:

```text
MAPE = (100/n) × Σ |(Y(t) - Y_hat(t)) / Y(t)|
```

Main problem:

```text
Actual = 0
```

causes division by zero.

MAPE can also become unstable when actual values are very close to zero.

---

# 68. WAPE

Weighted Absolute Percentage Error:

```text
WAPE =
Σ|Y(t) - Y_hat(t)|
-------------------
Σ|Y(t)|
× 100
```

WAPE is commonly useful for aggregate sales or demand forecasting.

---

# 69. MASE

Mean Absolute Scaled Error:

```text
MASE =
MAE of Forecast
----------------
MAE of Naive Forecast
```

Interpretation:

```text
MASE < 1
→ Better than naive forecast

MASE = 1
→ Same as naive forecast

MASE > 1
→ Worse than naive forecast
```

---

# 70. Prediction Interval

A point forecast gives only one value.

Example:

```text
Forecast = 500
```

A prediction interval communicates uncertainty.

Example:

```text
Forecast = 500

95% Prediction Interval:
450 – 550
```

This means the forecast is uncertain, and the interval represents a range for a future observation under the model's assumptions.

---

# 71. Important Time Series Models

At a high level:

```text
Naive
Seasonal Naive
Moving Average
Simple Exponential Smoothing
Holt
Holt-Winters
AR
MA
ARMA
ARIMA
SARIMA
SARIMAX
VAR
Prophet
Machine Learning
LSTM
GRU
Transformers
```

These models will be covered in the later modeling file.

---

# 72. Time Series Analysis Workflow

Use this workflow in interviews:

```text
1. Understand Business Problem
        ↓
2. Define Target
        ↓
3. Define Forecast Horizon
        ↓
4. Check Date Column
        ↓
5. Sort Chronologically
        ↓
6. Check Frequency
        ↓
7. Check Missing Values
        ↓
8. Check Missing Dates
        ↓
9. Visualize Time Series
        ↓
10. Identify Trend
        ↓
11. Identify Seasonality
        ↓
12. Check Stationarity
        ↓
13. ACF / PACF
        ↓
14. Create Baseline
        ↓
15. Build Models
        ↓
16. Time-Based Validation
        ↓
17. Evaluate Metrics
        ↓
18. Check Residuals
        ↓
19. Forecast Future
        ↓
20. Monitor Model
```

---

# 73. Important Interview Questions

## Q1. What is a time series?

A time series is a sequence of observations recorded in chronological order where temporal relationships may exist between observations.

---

## Q2. What is forecasting?

Forecasting is the process of predicting future values using historical observations and potentially external variables.

---

## Q3. What are the main components of a time series?

```text
Level
Trend
Seasonality
Noise
```

Cycles may also be present.

---

## Q4. What is trend?

Trend is the long-term direction of a time series.

---

## Q5. What is seasonality?

Seasonality is a repeating pattern occurring at a known frequency.

---

## Q6. What is the difference between seasonality and cyclicity?

Seasonality repeats at a known frequency, while cycles have variable duration and do not necessarily follow a fixed period.

---

## Q7. What is stationarity?

Stationarity means that the statistical behavior of the time series remains stable over time.

---

## Q8. How do you check stationarity?

I would use:

```text
Visual Analysis
Rolling Statistics
ADF Test
KPSS Test
```

---

## Q9. What is differencing?

Differencing subtracts the previous observation from the current observation:

```text
Y'(t) = Y(t) - Y(t-1)
```

It is commonly used to remove trend and help achieve stationarity.

---

## Q10. What is ACF?

ACF measures correlation between a time series and its lagged values.

---

## Q11. What is PACF?

PACF measures the direct relationship between a time series and a specific lag after accounting for intermediate lags.

---

## Q12. Why do we use ACF and PACF?

They help understand temporal dependence and provide diagnostic information for selecting AR and MA orders.

---

## Q13. Why should we not randomly split time-series data?

Because random splitting can mix future observations into the training data and cause temporal leakage.

---

## Q14. What is walk-forward validation?

Walk-forward validation sequentially trains on historical data and evaluates on later observations, simulating real-world forecasting.

---

## Q15. What is a naive forecast?

A naive forecast uses the latest observed value as the next forecast.

```text
Y_hat(t+1) = Y(t)
```

---

## Q16. Why is a baseline model important?

It provides a simple benchmark. A complex model should demonstrate that it provides meaningful improvement over the baseline.

---

## Q17. What is residual?

Residual is:

```text
Actual - Forecast
```

---

## Q18. What should good residuals look like?

Ideally:

```text
Mean ≈ 0
No trend
No seasonality
No significant autocorrelation
Stable variance
```

---

## Q19. What is forecast horizon?

Forecast horizon is the number of future periods we want to predict.

---

## Q20. What is temporal leakage?

Temporal leakage occurs when information that would not have been available at prediction time is used to create features, train the model, or evaluate the forecast.

---

# 74. Quick Revision

```text
TIME SERIES
→ Ordered observations over time

FORECASTING
→ Predict future values

LEVEL
→ Baseline value

TREND
→ Long-term direction

SEASONALITY
→ Repeating fixed-frequency pattern

CYCLE
→ Long-term fluctuation without fixed frequency

NOISE
→ Random variation

LAG
→ Previous observation

ACF
→ Correlation with lagged values

PACF
→ Direct correlation with a lag

STATIONARITY
→ Stable statistical behavior

ADF
→ Null: Unit root / non-stationary

KPSS
→ Null: Stationary

DIFFERENCING
→ Current value - previous value

SEASONAL DIFFERENCING
→ Current value - value from previous season

NAIVE
→ Last value as forecast

SEASONAL NAIVE
→ Previous season's value as forecast

MAE
→ Average absolute error

RMSE
→ Penalizes large errors

MAPE
→ Percentage error; problematic around zero

WAPE
→ Aggregate percentage error

MASE
→ Error relative to naive benchmark

RESIDUAL
→ Actual - Forecast

WALK-FORWARD
→ Sequential time-based validation
```

---

# 75. One-Minute Interview Summary

If an interviewer asks:

**"How would you approach a time-series forecasting problem?"**

Answer:

```text
First, I would understand the business objective,
target variable, forecast horizon, and required frequency.

Then I would validate the time index, sort the data
chronologically, check missing timestamps, missing values,
duplicates, and outliers.

Next, I would perform time-series EDA to identify trend,
seasonality, cycles, and autocorrelation.

I would check stationarity using visual analysis,
rolling statistics, ADF, and KPSS tests where appropriate.

Then I would create a simple baseline such as naive or
seasonal-naive forecasting.

After that, I would engineer appropriate lag, rolling,
calendar, and external-variable features while preventing
temporal leakage.

I would evaluate candidate models using time-based or
walk-forward validation rather than random splitting.

Finally, I would compare models using appropriate
forecasting metrics, analyze residuals, generate forecasts
with uncertainty intervals where appropriate, and monitor
the model after deployment.
```

---

# 76. Core Concepts to Remember

```text
Time Order Matters
        ↓
Understand Trend
        ↓
Understand Seasonality
        ↓
Check Stationarity
        ↓
Understand ACF / PACF
        ↓
Create Baseline
        ↓
Avoid Temporal Leakage
        ↓
Use Time-Based Validation
        ↓
Evaluate Forecast Error
        ↓
Check Residuals
        ↓
Forecast Future
```
