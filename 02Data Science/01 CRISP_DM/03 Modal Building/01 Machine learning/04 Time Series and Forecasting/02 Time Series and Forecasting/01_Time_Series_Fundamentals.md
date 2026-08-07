# 01_Time_Series_Fundamentals.md

# Time Series & Forecasting — Fundamentals

## 1. Introduction

A **Time Series** is a sequence of observations recorded in chronological order at specific time intervals.

Examples:

* Daily sales
* Monthly revenue
* Hourly electricity demand
* Stock prices
* Weekly website traffic
* Monthly production
* Daily temperature
* Quarterly GDP

Example:

| Date | Sales |
| ---- | ----: |
| Jan  |   100 |
| Feb  |   120 |
| Mar  |   115 |
| Apr  |   140 |
| May  |   150 |

The key characteristic of time-series data is:

> **Time order matters.**

---

# 2. Time Series vs Regular Data

In regular machine-learning datasets, observations are often assumed to be independent.

In time series:

```text
Past → Present → Future
```

The current observation may depend on previous observations.

Example:

```text
Sales(t)
   ↓
Sales(t-1)
Sales(t-2)
Sales(t-3)
```

Therefore, time-series data requires special preprocessing, validation, and modeling techniques.

---

# 3. Time Series Analysis

**Time Series Analysis** is the process of analyzing historical observations to understand patterns and relationships over time.

Main objectives:

* Understand historical behavior
* Identify trends
* Detect seasonality
* Identify cycles
* Detect anomalies
* Check stationarity
* Understand autocorrelation
* Build forecasting models

---

# 4. Forecasting

**Forecasting** is the process of predicting future values using historical observations and potentially other explanatory variables.

Example:

```text
Historical Sales
       ↓
Time Series Analysis
       ↓
Forecasting Model
       ↓
Future Sales
```

Example:

```text
2024 Sales → Historical
2025 Sales → Historical
2026 Sales → Forecast
```

---

# 5. Components of a Time Series

A time series can contain several components:

```text
Time Series
│
├── Trend
├── Seasonality
├── Cyclical Pattern
├── Irregular / Random Component
└── Noise
```

A common conceptual representation is:

$$
Y_t = T_t + S_t + C_t + R_t
$$

Where:

* `Yₜ` = observed value
* `Tₜ` = trend
* `Sₜ` = seasonal component
* `Cₜ` = cyclical component
* `Rₜ` = irregular/random component

---

# 6. Trend

A **Trend** represents the long-term direction of a time series.

It can be:

* Increasing
* Decreasing
* Constant
* Nonlinear

Example:

```text
Sales

|
|                 *
|             *
|          *
|       *
|    *
| *
+----------------------> Time
```

This indicates an upward trend.

---

# 7. Types of Trend

### Increasing Trend

Values generally increase over time.

```text
100 → 120 → 140 → 160
```

### Decreasing Trend

Values generally decrease.

```text
200 → 180 → 150 → 130
```

### Constant Trend

Values fluctuate around a stable level.

```text
100 → 102 → 98 → 101
```

### Nonlinear Trend

The rate of change itself changes over time.

Example:

```text
100 → 105 → 115 → 135 → 170
```

---

# 8. Seasonality

**Seasonality** is a pattern that repeats at a fixed and known frequency.

Examples:

* Ice cream sales increase every summer
* Retail sales increase every December
* Electricity demand changes by day of week
* Hotel bookings increase every holiday season

Example:

```text
Jan ↓
Feb ↓
Mar ↑
Apr ↑
May ↑
...
Next year:
Jan ↓
Feb ↓
Mar ↑
...
```

---

# 9. Seasonal Period

The **seasonal period** is the number of observations between repeated seasonal patterns.

Examples:

| Data Frequency |    Common Seasonal Period |
| -------------- | ------------------------: |
| Hourly         |  24 for daily seasonality |
| Daily          |  7 for weekly seasonality |
| Weekly         | 52 for yearly seasonality |
| Monthly        | 12 for yearly seasonality |
| Quarterly      |  4 for yearly seasonality |

### Important

The seasonal period depends on the pattern you want to model, not only on the data frequency.

---

# 10. Seasonality vs Trend

### Trend

Long-term movement.

### Seasonality

Repeating pattern at a fixed frequency.

Example:

```text
Trend:
Sales increase over 5 years.

Seasonality:
Sales increase every December.
```

A time series can have both.

---

# 11. Cyclical Pattern

A **Cycle** represents long-term fluctuations that do not necessarily repeat at a fixed frequency.

Examples:

* Economic expansion and recession
* Business cycles
* Long-term demand cycles

### Difference

```text
Seasonality
→ Fixed and known frequency

Cycle
→ Duration may vary
```

---

# 12. Trend vs Seasonality vs Cycle

| Component   | Pattern                | Frequency             |
| ----------- | ---------------------- | --------------------- |
| Trend       | Long-term direction    | No fixed frequency    |
| Seasonality | Repeating pattern      | Fixed                 |
| Cycle       | Long-term fluctuations | Not necessarily fixed |
| Noise       | Random variation       | Irregular             |

---

# 13. Noise

**Noise** represents random variation that cannot be explained by systematic patterns.

Example:

```text
Expected Sales = 100
Actual Sales = 103
```

The difference may be random noise.

Noise can come from:

* Measurement errors
* Random customer behavior
* Unexpected events
* Data collection errors
* External factors not included in the model

---

# 14. White Noise

A **White Noise** time series has:

* Mean approximately zero or constant
* Constant variance
* No autocorrelation
* Random observations

Conceptually:

$$
Y_t = \epsilon_t
$$

where:

$$
E(\epsilon_t)=0
$$

and:

$$
Cov(\epsilon_t,\epsilon_{t-k})=0
$$

for:

$$
k \neq 0
$$

---

# 15. Why White Noise Is Important

A good forecasting model should ideally leave residuals that behave approximately like white noise.

Workflow:

```text
Time Series
     ↓
Forecasting Model
     ↓
Residuals
     ↓
Residual Diagnostics
     ↓
Approximately White Noise?
```

If residuals still contain systematic patterns:

> The model may not have captured all useful information.

---

# 16. Stationarity

A time series is **stationary** when its statistical properties remain stable over time.

Important properties include:

* Mean
* Variance
* Autocovariance

A weakly stationary series generally has:

$$
E(Y_t)=\mu
$$

where mean is constant over time.

And:

$$
Var(Y_t)=\sigma^2
$$

where variance is constant.

Autocovariance depends on the lag rather than the actual time point.

---

# 17. Why Stationarity Matters

Many classical time-series models work better when the series is stationary.

Examples:

* AR
* MA
* ARMA
* ARIMA

A non-stationary series can lead to:

* Misleading relationships
* Poor model estimation
* Unstable forecasts
* Spurious regression

---

# 18. Types of Stationarity

### Strict Stationarity

The entire joint probability distribution remains unchanged under a shift in time.

It is a strong theoretical condition.

### Weak / Covariance Stationarity

The main conditions are:

```text
Constant Mean
Constant Variance
Autocovariance depends only on lag
```

This is the form commonly discussed in practical time-series modeling.

---

# 19. Non-Stationary Time Series

A series can be non-stationary because of:

* Trend
* Changing variance
* Seasonality
* Structural changes
* Unit roots

Example:

```text
100
120
150
190
240
300
```

The mean changes over time, indicating non-stationarity.

---

# 20. Random Walk

A random walk is a common example of a non-stationary time series.

Basic form:

$$
Y_t = Y_{t-1} + \epsilon_t
$$

where:

$$
\epsilon_t \sim White\ Noise
$$

The current value depends on the previous value plus a random shock.

---

# 21. Random Walk with Drift

A random walk can include drift:

$$
Y_t = c + Y_{t-1} + \epsilon_t
$$

Where:

* `c` = drift
* `εₜ` = random error

Example:

```text
Previous value
      +
Average movement
      +
Random shock
      =
Current value
```

---

# 22. Differencing

**Differencing** is commonly used to remove trend and make a time series more stationary.

First difference:

$$
\Delta Y_t = Y_t - Y_{t-1}
$$

Example:

| Time | Value | Difference |
| ---- | ----: | ---------: |
| 1    |   100 |          - |
| 2    |   110 |         10 |
| 3    |   125 |         15 |
| 4    |   130 |          5 |

---

# 23. First-Order Differencing

If:

$$
Y_t
$$

is non-stationary, calculate:

$$
Y'*t=Y_t-Y*{t-1}
$$

This removes many types of trend.

Example:

```text
Original:
100 → 110 → 125 → 130

Differenced:
10 → 15 → 5
```

---

# 24. Second-Order Differencing

If first differencing is insufficient:

$$
\Delta^2Y_t
===========

\Delta Y_t-\Delta Y_{t-1}
$$

Example:

```text
Original Series
      ↓
First Difference
      ↓
Second Difference
```

However:

> Avoid unnecessary differencing.

Excessive differencing can remove useful structure and make the series unnecessarily noisy.

---

# 25. Lag

A **Lag** represents a previous observation.

For lag 1:

$$
Y_{t-1}
$$

For lag 2:

$$
Y_{t-2}
$$

Example:

| Month | Sales | Lag 1 |
| ----- | ----: | ----: |
| Jan   |   100 |     - |
| Feb   |   120 |   100 |
| Mar   |   130 |   120 |
| Apr   |   150 |   130 |

---

# 26. Lag Features

Lag variables are commonly used in machine-learning forecasting.

Example:

```text
Sales_t-1
Sales_t-2
Sales_t-3
Sales_t-7
Sales_t-12
```

For monthly sales:

```text
Lag 1
→ Previous month

Lag 12
→ Same month last year
```

---

# 27. Lead

A **Lead** represents a future observation.

For example:

$$
Y_{t+1}
$$

In forecasting, future values are generally the target rather than features.

Example:

```text
X_t → Predict Y_(t+1)
```

---

# 28. Autocorrelation

**Autocorrelation** measures the relationship between a time series and its lagged values.

For lag `k`:

$$
\rho_k
======

Corr(Y_t,Y_{t-k})
$$

Example:

```text
Sales today
      ↕
Sales yesterday
```

If strongly related:

> High autocorrelation at lag 1.

---

# 29. Positive Autocorrelation

If:

```text
High → High
Low → Low
```

then consecutive values tend to move in the same direction.

This produces positive autocorrelation.

Example:

```text
100 → 105 → 110 → 108 → 115
```

---

# 30. Negative Autocorrelation

If high values tend to be followed by low values and vice versa:

```text
High → Low
Low → High
```

then autocorrelation can be negative.

Example:

```text
100 → 80 → 105 → 85 → 110
```

---

# 31. ACF

**ACF = Autocorrelation Function**

It measures correlation between:

```text
Y_t
```

and:

```text
Y_(t-k)
```

for different lag values `k`.

ACF is commonly used to identify:

* Serial dependence
* Seasonality
* MA order
* Residual autocorrelation

---

# 32. Partial Autocorrelation

**PACF = Partial Autocorrelation Function**

PACF measures the relationship between:

$$
Y_t
$$

and:

$$
Y_{t-k}
$$

after removing the effects of intermediate lags.

Example:

For lag 3, PACF measures the relationship between:

```text
Y_t
```

and:

```text
Y_(t-3)
```

after accounting for:

```text
Y_(t-1)
Y_(t-2)
```

---

# 33. ACF vs PACF

| ACF                               | PACF                             |
| --------------------------------- | -------------------------------- |
| Total correlation                 | Direct correlation               |
| Includes intermediate lag effects | Removes intermediate lag effects |
| Useful for MA identification      | Useful for AR identification     |
| Helps detect seasonality          | Helps identify AR order          |

### Rule of Thumb

```text
AR Model → PACF
MA Model → ACF
```

This is a practical identification guideline, not an absolute rule.

---

# 34. Autocovariance

Autocovariance measures how observations at different time lags vary together.

For lag `k`:

$$
\gamma_k
========

Cov(Y_t,Y_{t-k})
$$

Autocorrelation is the standardized version:

$$
\rho_k
======

\frac{\gamma_k}{\gamma_0}
$$

---

# 35. Seasonality and ACF

Strong seasonal patterns often create significant autocorrelation at seasonal lags.

For monthly data with yearly seasonality:

```text
Lag 12
Lag 24
Lag 36
...
```

may show strong autocorrelation.

For daily data with weekly seasonality:

```text
Lag 7
Lag 14
Lag 21
...
```

may be important.

---

# 36. Time Series Decomposition

Decomposition separates a time series into components.

Common components:

```text
Observed
   ↓
Trend
Seasonality
Residual
```

For additive decomposition:

$$
Y_t=T_t+S_t+R_t
$$

For multiplicative decomposition:

$$
Y_t=T_t\times S_t\times R_t
$$

---

# 37. Additive Model

Additive decomposition is appropriate when the magnitude of seasonal fluctuations is relatively constant.

$$
Y_t=T_t+S_t+R_t
$$

Example:

```text
Trend = 100
Seasonal effect = +20
Residual = +5

Observed = 125
```

---

# 38. Multiplicative Model

Multiplicative decomposition is useful when seasonal fluctuations increase with the level of the series.

$$
Y_t=T_t\times S_t\times R_t
$$

Example:

```text
Trend = 100
Seasonal factor = 1.20
Residual = 1.05

Observed ≈ 126
```

---

# 39. Additive vs Multiplicative

| Additive                               | Multiplicative                               |
| -------------------------------------- | -------------------------------------------- |
| `Y = T + S + R`                        | `Y = T × S × R`                              |
| Seasonal variation roughly constant    | Seasonal variation changes with level        |
| Suitable for stable seasonal amplitude | Suitable for proportional seasonal amplitude |

### Example

If sales increase from:

```text
100 → 200
```

and seasonal variation changes from:

```text
±10 → ±20
```

multiplicative behavior may be appropriate.

---

# 40. Log Transformation

A logarithmic transformation can sometimes stabilize increasing variance and convert multiplicative relationships into additive ones.

For example:

$$
Y'_t=\log(Y_t)
$$

If:

$$
Y_t=T_t\times S_t\times R_t
$$

then:

$$
\log(Y_t)
=========

\log(T_t)+\log(S_t)+\log(R_t)
$$

This can make modeling easier.

---

# 41. Moving Average

A moving average smooths a time series by calculating averages over a rolling window.

For window size `k`:

$$
MA_t=
\frac{1}{k}
\sum_{i=0}^{k-1}Y_{t-i}
$$

Example with window 3:

```text
Values:
10, 20, 30

MA = (10 + 20 + 30) / 3
   = 20
```

---

# 42. Rolling Mean

In Python:

```python
df["rolling_mean"] = df["sales"].rolling(window=7).mean()
```

This can help identify:

* Trend
* Smoothing
* Local behavior
* Noise reduction

---

# 43. Rolling Standard Deviation

Rolling standard deviation measures local variability.

```python
df["rolling_std"] = (
    df["sales"]
    .rolling(window=7)
    .std()
)
```

If rolling variance changes significantly over time:

> The series may have non-constant variance.

---

# 44. Time-Based Features

Time series models can use calendar-based features.

Examples:

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

For retail forecasting:

```text
Month
Holiday
Festival
Weekend
Promotion
```

can be useful predictors.

---

# 45. Lag-Based Features

Common features:

```text
Lag 1
Lag 2
Lag 3
Lag 7
Lag 12
Lag 24
```

Depending on data frequency.

Example:

### Daily data

```text
Lag 1  → Yesterday
Lag 7  → Same weekday last week
Lag 365 → Approximately same day last year
```

### Monthly data

```text
Lag 1  → Previous month
Lag 12 → Same month previous year
```

---

# 46. Forecast Horizon

The **Forecast Horizon** is how far into the future we want to predict.

Examples:

```text
Next 1 day
Next 7 days
Next 12 months
Next 4 quarters
```

Notation:

```text
Forecast horizon = h
```

---

# 47. One-Step Forecast

Predict only the next time point.

```text
Y₁ Y₂ Y₃ Y₄ Y₅
         ↓
       Predict Y₆
```

Example:

> Predict tomorrow's sales.

---

# 48. Multi-Step Forecast

Predict multiple future time points.

```text
Y₁ Y₂ Y₃ Y₄ Y₅
         ↓
Predict:
Y₆
Y₇
Y₈
Y₉
```

Example:

> Forecast sales for the next 12 months.

---

# 49. Recursive Forecasting

In recursive forecasting:

```text
Predict Y(t+1)
      ↓
Use prediction as input
      ↓
Predict Y(t+2)
      ↓
Use prediction
      ↓
Predict Y(t+3)
```

Example:

```text
Actual → Actual → Forecast
                    ↓
                  Forecast
                    ↓
                  Forecast
```

### Risk

Forecast errors can accumulate over multiple steps.

---

# 50. Direct Forecasting

In direct forecasting, separate models can be trained for different forecast horizons.

Example:

```text
Model 1 → Predict Y(t+1)
Model 2 → Predict Y(t+2)
Model 3 → Predict Y(t+3)
```

### Advantage

Errors from previous predictions are not recursively propagated.

### Disadvantage

More models need to be trained.

---

# 51. Forecasting Approaches

Three common approaches:

```text
1. Statistical Models
2. Machine Learning Models
3. Deep Learning Models
```

### Statistical

* Naive
* Moving Average
* Exponential Smoothing
* Holt
* Holt-Winters
* AR
* MA
* ARMA
* ARIMA
* SARIMA
* VAR

### Machine Learning

* Linear Regression
* Random Forest
* Gradient Boosting
* XGBoost
* LightGBM

### Deep Learning

* RNN
* LSTM
* GRU
* Transformer-based models

---

# 52. Naive Forecast

The simplest forecasting method.

The next prediction equals the most recent observation.

$$
\hat{Y}_{t+1}=Y_t
$$

Example:

```text
Today's sales = 500

Tomorrow forecast = 500
```

---

# 53. Seasonal Naive Forecast

The forecast equals the value from the corresponding previous season.

For monthly data with yearly seasonality:

$$
\hat{Y}*{t}=Y*{t-12}
$$

Example:

```text
January 2026 forecast
=
January 2025 actual
```

This is a very useful baseline for seasonal forecasting.

---

# 54. Why Baselines Matter

Before using complex models, create a baseline.

Example:

```text
Naive Model
      ↓
ARIMA
      ↓
XGBoost
      ↓
LSTM
```

If a complex model cannot outperform the baseline:

> The complexity may not be justified.

---

# 55. Train-Test Split for Time Series

Normal random train-test splitting should generally be avoided.

Incorrect:

```python
train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

Why?

Because random splitting can allow future information to enter the training set.

---

# 56. Correct Time-Based Split

Example:

```text
Past ------------------------> Future

Train          Validation     Test
|--------------|--------------|
```

Example:

```text
2019–2023 → Train
2024       → Validation
2025       → Test
```

The model should be trained using past information to predict future observations.

---

# 57. Data Leakage in Time Series

**Data Leakage** occurs when information from the future is unintentionally used to train the model.

Example:

```text
Predict:
Sales in March

Feature:
Average Sales calculated using March, April, May
```

This uses future information.

Incorrect.

Correct:

```text
Features available before March
→ Predict March
```

---

# 58. Temporal Validation

A forecasting model should be evaluated using a realistic temporal setup.

Example:

```text
Train:
Jan 2020 → Dec 2022

Validation:
Jan 2023 → Jun 2023

Test:
Jul 2023 → Dec 2023
```

This mimics real-world forecasting.

---

# 59. Rolling Forecast Validation

Rolling validation repeatedly trains on past data and predicts future observations.

Example:

```text
Train: Jan–Jun
Test:  Jul

Train: Jan–Jul
Test:  Aug

Train: Jan–Aug
Test:  Sep
```

This is also called:

* Rolling-origin evaluation
* Walk-forward validation
* Expanding-window validation

---

# 60. Expanding Window

Training data continuously grows.

```text
Fold 1:
Train → Jan–Jun
Test  → Jul

Fold 2:
Train → Jan–Jul
Test  → Aug

Fold 3:
Train → Jan–Aug
Test  → Sep
```

---

# 61. Sliding Window

The training window moves forward while maintaining a fixed size.

Example:

```text
Fold 1:
Train → Jan–Jun
Test  → Jul

Fold 2:
Train → Feb–Jul
Test  → Aug

Fold 3:
Train → Mar–Aug
Test  → Sep
```

### Difference

```text
Expanding Window
→ Training size increases

Sliding Window
→ Training size remains approximately constant
```

---

# 62. Time Series Cross-Validation

A common strategy is:

```text
Past → Future
```

rather than:

```text
Random → Random
```

Example:

```text
Fold 1:
Train █████
Test  ██

Fold 2:
Train ███████
Test  ██

Fold 3:
Train █████████
Test  ██
```

This preserves temporal ordering.

---

# 63. Forecast Error

Forecast error is:

$$
e_t=Y_t-\hat{Y}_t
$$

Where:

* `Yₜ` = actual value
* `Ŷₜ` = forecast

Example:

```text
Actual = 100
Forecast = 90

Error = 100 - 90
      = 10
```

---

# 64. Residual vs Forecast Error

In forecasting, these terms are closely related but can be distinguished.

### Forecast Error

Difference between actual and forecast:

$$
e_t=Y_t-\hat{Y}_t
$$

### Residual

Difference between observed values and fitted values in the training/modeling context.

For a well-specified model, residuals should ideally contain little systematic information.

---

# 65. Good Forecasting Model

A good forecasting model should generally have:

```text
Low Forecast Error
       +
No Systematic Residual Pattern
       +
Good Generalization
       +
Stable Future Performance
```

---

# 66. Important Time Series Concepts

```text
Time Series
    ↓
Trend
    ↓
Seasonality
    ↓
Cycle
    ↓
Noise
    ↓
Stationarity
    ↓
Lag
    ↓
Autocorrelation
    ↓
ACF / PACF
    ↓
Differencing
    ↓
Forecasting
    ↓
Temporal Validation
```

---

# 67. Python: Basic Time-Series Setup

```python
import pandas as pd
import matplotlib.pyplot as plt

df = pd.read_csv("sales.csv")

df["date"] = pd.to_datetime(df["date"])

df = df.sort_values("date")

df = df.set_index("date")
```

---

# 68. Plot Time Series

```python
df["sales"].plot(figsize=(12, 5))

plt.title("Sales Over Time")
plt.xlabel("Date")
plt.ylabel("Sales")
plt.show()
```

Always visualize the series before modeling.

Look for:

* Trend
* Seasonality
* Outliers
* Structural breaks
* Missing periods
* Changing variance

---

# 69. Check Missing Dates

Time series datasets should be checked for missing timestamps.

Example:

```python
df.index.to_series().diff().value_counts()
```

For daily data, unexpected gaps may indicate missing observations.

---

# 70. Resampling

Resampling changes the frequency of a time series.

Example:

Daily → Monthly:

```python
monthly_sales = df["sales"].resample("M").sum()
```

Daily → Weekly:

```python
weekly_sales = df["sales"].resample("W").sum()
```

Monthly → Quarterly:

```python
quarterly_sales = df["sales"].resample("Q").sum()
```

---

# 71. Aggregation During Resampling

The aggregation depends on the business meaning.

### Sales

```python
.resample("M").sum()
```

### Average Temperature

```python
.resample("M").mean()
```

### Closing Stock Price

```python
.resample("M").last()
```

Choosing the wrong aggregation can distort the time series.

---

# 72. Outliers in Time Series

Outliers can be caused by:

* Data errors
* Promotions
* Holidays
* Pandemics
* Supply disruptions
* Weather events
* Sudden market changes

Do not automatically remove every outlier.

First determine:

> Is it a data error or a genuine business event?

---

# 73. Structural Break

A **Structural Break** occurs when the underlying behavior of a time series changes.

Example:

```text
Before:
Sales ≈ 100 units/day

After:
Sales ≈ 180 units/day
```

Possible causes:

* New product
* Pricing change
* New market
* Regulation
* Pandemic
* Major competitor
* Business strategy change

---

# 74. Concept Drift

In forecasting, **concept drift** occurs when the relationship between predictors and the target changes over time.

Example:

```text
Before:
Promotion → Strong increase in sales

After:
Promotion → Small increase in sales
```

The model may become less accurate because the underlying relationship has changed.

---

# 75. Time Series Workflow

```text
Business Problem
      ↓
Define Target
      ↓
Define Forecast Horizon
      ↓
Collect Time-Series Data
      ↓
Sort by Time
      ↓
Check Frequency
      ↓
Handle Missing Dates
      ↓
EDA
      ↓
Trend / Seasonality / Cycles
      ↓
Outlier Analysis
      ↓
Check Stationarity
      ↓
Transform / Difference if Required
      ↓
Create Baseline
      ↓
Feature Engineering
      ↓
Train Forecasting Models
      ↓
Time-Based Validation
      ↓
Evaluate Forecast
      ↓
Residual Diagnostics
      ↓
Final Model
      ↓
Future Forecast
      ↓
Monitor Performance
```

---

# 76. Important Interview Questions

## Q1. What is a time series?

A sequence of observations recorded chronologically over time.

---

## Q2. What is forecasting?

Predicting future values using historical time-dependent information and potentially external variables.

---

## Q3. What are the main components of a time series?

* Trend
* Seasonality
* Cyclical component
* Irregular/random component

---

## Q4. Difference between trend and seasonality?

**Trend** is long-term direction.

**Seasonality** is a repeating pattern at a fixed frequency.

---

## Q5. Difference between seasonality and cyclic behavior?

Seasonality has a fixed and known frequency, while cycles generally have variable duration.

---

## Q6. What is stationarity?

A stationary time series has stable statistical properties over time, particularly constant mean, constant variance, and autocovariance dependent primarily on lag.

---

## Q7. Why is stationarity important?

Many classical time-series models rely on stationary behavior for reliable estimation and interpretation.

---

## Q8. How can you make a time series stationary?

Common approaches:

* Differencing
* Log transformation
* Box-Cox transformation
* Removing trend
* Seasonal differencing

---

## Q9. What is differencing?

Subtracting a previous observation from the current observation:

$$
\Delta Y_t=Y_t-Y_{t-1}
$$

---

## Q10. What is autocorrelation?

The correlation between a time series and its lagged values.

---

## Q11. What is ACF?

ACF measures autocorrelation at different lag values.

---

## Q12. What is PACF?

PACF measures the direct relationship between a value and a particular lag after accounting for intermediate lags.

---

## Q13. Why are ACF and PACF important?

They help identify temporal dependencies and are useful when selecting AR and MA components.

---

## Q14. Why should random train-test split generally be avoided?

Because it can allow future observations to influence training and cause data leakage.

---

## Q15. What is walk-forward validation?

A validation approach where the model is repeatedly trained on historical data and tested on the next future period.

---

## Q16. What is a naive forecast?

The next forecast equals the most recent observed value.

$$
\hat{Y}_{t+1}=Y_t
$$

---

## Q17. What is seasonal naive forecasting?

The forecast equals the value from the corresponding previous seasonal period.

For monthly yearly seasonality:

$$
\hat{Y}*t=Y*{t-12}
$$

---

## Q18. What is white noise?

A random process with approximately constant mean and variance and no meaningful autocorrelation.

---

## Q19. What should good model residuals look like?

They should ideally:

* Have mean near zero
* Show approximately constant variance
* Have little/no autocorrelation
* Contain no obvious systematic pattern

---

## Q20. What is forecast horizon?

The number of future time periods for which forecasts are required.

---

# 77. Scenario-Based Interview Questions

## Scenario 1

Your sales data has strong yearly seasonality.

What would you do?

### Answer

Identify the seasonal period, visualize the seasonal pattern, consider seasonal decomposition and seasonal forecasting models such as Holt-Winters or SARIMA, and use a seasonal-naive baseline for comparison.

---

## Scenario 2

Your time series has an upward trend.

Is it stationary?

### Answer

Not necessarily. A persistent trend usually indicates non-stationarity in the mean.

---

## Scenario 3

Your ACF shows strong spikes at lag 12, 24, and 36 for monthly data.

What could this indicate?

### Answer

It strongly suggests yearly seasonality.

---

## Scenario 4

Your model performs very well on random train-test split but poorly in production.

What could be wrong?

### Answer

Potential causes include temporal data leakage, unrealistic validation, concept drift, distribution changes, or future information accidentally entering the training features.

---

## Scenario 5

Your residuals show strong autocorrelation.

What does it indicate?

### Answer

The model may not have captured all temporal structure, suggesting that additional lag/seasonal components or a different forecasting model may be required.

---

# 78. Quick Revision

```text
TIME SERIES
│
├── Time-ordered observations
│
├── Trend
│
├── Seasonality
│
├── Cycle
│
├── Noise
│
├── Stationarity
│
├── Lag
│
├── Autocorrelation
│
├── ACF
│
├── PACF
│
├── Differencing
│
├── Decomposition
│
├── Forecast Horizon
│
├── One-Step Forecast
│
├── Multi-Step Forecast
│
├── Naive Forecast
│
├── Seasonal Naive
│
└── Temporal Validation
```

---

# 79. Must Remember

```text
Time Series
→ Observations ordered by time

Forecasting
→ Predict future values

Trend
→ Long-term direction

Seasonality
→ Repeating fixed-frequency pattern

Cycle
→ Long-term non-fixed fluctuations

Noise
→ Random variation

Stationarity
→ Stable statistical properties over time

Lag
→ Previous observation

Autocorrelation
→ Relationship with lagged observations

ACF
→ Overall lag correlation

PACF
→ Direct lag correlation

Differencing
→ Y(t) - Y(t-1)

Naive Forecast
→ Last observed value

Seasonal Naive
→ Previous seasonal value

Forecast Error
→ Actual - Forecast

Walk-Forward Validation
→ Train on past → predict future

Data Leakage
→ Future information enters training

Good Residuals
→ Approximately white noise
```

---

# 80. One-Minute Interview Explanation

> Time-series forecasting deals with predicting future values from time-ordered historical data. The important components of a time series are trend, seasonality, cycles, and noise. Before modeling, I check the time frequency, missing timestamps, outliers, trend, seasonality, autocorrelation, and stationarity. For classical models, I may use differencing or transformations when required to achieve stationarity. I also use ACF and PACF to understand temporal dependencies. For validation, I avoid random train-test splits and use time-based or walk-forward validation to prevent future data leakage. I start with simple baselines such as naive and seasonal-naive forecasts and then compare them with statistical, machine-learning, or deep-learning models based on the business problem and forecast horizon.
