# 02_Time_Series_Decomposition_and_Stationarity.md

# Time Series — Decomposition & Stationarity

## 1. Overview

Before building a forecasting model, we need to understand the underlying structure of the time series.

The major tasks are:

```text
Time Series
     ↓
Decomposition
     ↓
Trend Analysis
     ↓
Seasonality Analysis
     ↓
Stationarity Check
     ↓
Transformation / Differencing
     ↓
Modeling
```

This file covers:

* Time-series decomposition
* Additive decomposition
* Multiplicative decomposition
* Trend
* Seasonality
* Residual component
* Moving averages
* Rolling statistics
* Stationarity
* Unit root
* Differencing
* Seasonal differencing
* Log transformation
* Box-Cox transformation
* ADF test
* KPSS test
* ACF
* PACF
* White noise
* Residual diagnostics

---

# 2. Time Series Decomposition

Time-series decomposition separates an observed series into meaningful components.

A basic decomposition is:

```text
Observed Series
      │
      ├── Trend
      ├── Seasonality
      └── Residual
```

Mathematically:

### Additive

$$
Y_t = T_t + S_t + R_t
$$

### Multiplicative

$$
Y_t = T_t \times S_t \times R_t
$$

Where:

* `Yₜ` = observed value
* `Tₜ` = trend
* `Sₜ` = seasonal component
* `Rₜ` = residual/remainder

---

# 3. Additive Decomposition

The additive model is:

$$
Y_t = T_t + S_t + R_t
$$

Use it when the magnitude of seasonal fluctuations is approximately constant over time.

Example:

```text
Trend = 100
Seasonality = +20
Residual = +5

Observed = 100 + 20 + 5
         = 125
```

Another period:

```text
Trend = 150
Seasonality = +20
Residual = -5

Observed = 150 + 20 - 5
         = 165
```

The seasonal amplitude remains approximately constant.

---

# 4. Multiplicative Decomposition

The multiplicative model is:

$$
Y_t = T_t \times S_t \times R_t
$$

It is useful when seasonal variation changes proportionally with the level of the series.

Example:

```text
Trend = 100
Seasonal factor = 1.20
Residual factor = 1.05

Observed = 100 × 1.20 × 1.05
         = 126
```

As the trend increases, the seasonal effect can also increase.

---

# 5. Additive vs Multiplicative

| Characteristic     | Additive            | Multiplicative      |
| ------------------ | ------------------- | ------------------- |
| Formula            | `Y = T + S + R`     | `Y = T × S × R`     |
| Seasonal amplitude | Roughly constant    | Changes with level  |
| Seasonal effect    | Absolute            | Proportional        |
| Suitable for       | Stable variance     | Increasing variance |
| Log transformation | Usually unnecessary | Often useful        |

---

# 6. Example: Choosing Decomposition

Suppose monthly sales are:

```text
Year 1:
100, 120, 100, 80

Year 2:
200, 240, 200, 160
```

Seasonal difference:

```text
Year 1 amplitude ≈ 40
Year 2 amplitude ≈ 80
```

The seasonal fluctuation increases with the level.

This suggests:

> Multiplicative seasonality may be more appropriate.

---

# 7. Trend Component

Trend represents the long-term movement of a time series.

Example:

```text
100 → 110 → 125 → 140 → 160
```

This series has an upward trend.

Trend can be:

* Linear
* Nonlinear
* Increasing
* Decreasing
* Piecewise
* Changing over time

---

# 8. Seasonal Component

Seasonality represents a pattern that repeats at a known frequency.

Examples:

```text
Monthly:
12-month yearly pattern

Daily:
7-day weekly pattern

Hourly:
24-hour daily pattern
```

For monthly sales:

```text
January → Low
February → Low
...
December → High

Next year:
January → Low
...
December → High
```

---

# 9. Residual Component

After removing trend and seasonality, the remaining component is the residual/remainder.

For additive decomposition:

$$
R_t=Y_t-T_t-S_t
$$

Ideally, residuals should contain mostly random variation.

A good forecasting model should leave residuals with:

```text
Mean ≈ 0
No strong trend
No obvious seasonality
No significant autocorrelation
Approximately constant variance
```

---

# 10. Moving Average Smoothing

Moving averages smooth short-term fluctuations.

For a window size `k`:

$$
MA_t=
\frac{1}{k}
\sum_{i=0}^{k-1}Y_{t-i}
$$

Example:

```text
Sales:
100, 110, 120

3-period MA:

(100 + 110 + 120) / 3
= 110
```

---

# 11. Simple Moving Average

For a 3-period moving average:

$$
MA_t=
\frac{Y_t+Y_{t-1}+Y_{t-2}}{3}
$$

Example:

| Month | Sales | 3-Month MA |
| ----- | ----: | ---------: |
| Jan   |   100 |          - |
| Feb   |   120 |          - |
| Mar   |   140 |        120 |
| Apr   |   130 |        130 |
| May   |   150 |        140 |

Moving averages reduce short-term noise.

---

# 12. Centered Moving Average

A centered moving average uses observations around the current time point.

For a 3-period centered moving average:

$$
CMA_t=
\frac{Y_{t-1}+Y_t+Y_{t+1}}{3}
$$

It is useful for estimating trend during decomposition.

However, because it uses future observations relative to `t`, it is generally not directly suitable for real-time forecasting.

---

# 13. Rolling Mean

A rolling mean calculates the average over a moving window.

```python
df["rolling_mean"] = (
    df["sales"]
    .rolling(window=12)
    .mean()
)
```

For monthly data:

```text
window = 12
```

can help visualize yearly-scale movement.

---

# 14. Rolling Standard Deviation

Rolling standard deviation measures local variability.

```python
df["rolling_std"] = (
    df["sales"]
    .rolling(window=12)
    .std()
)
```

If rolling standard deviation changes significantly:

> The variance may not be constant.

This can indicate heteroscedasticity or non-stationarity.

---

# 15. Classical Decomposition

Using `statsmodels`:

```python
from statsmodels.tsa.seasonal import seasonal_decompose

result = seasonal_decompose(
    df["sales"],
    model="additive",
    period=12
)

result.plot()
```

For multiplicative decomposition:

```python
result = seasonal_decompose(
    df["sales"],
    model="multiplicative",
    period=12
)
```

---

# 16. STL Decomposition

**STL = Seasonal-Trend decomposition using Loess**

STL is a flexible decomposition method based on LOESS smoothing.

```python
from statsmodels.tsa.seasonal import STL

result = STL(
    df["sales"],
    period=12
).fit()

result.plot()
```

Components:

```text
Observed
Trend
Seasonal
Residual
```

---

# 17. Advantages of STL

STL is useful because it can handle:

* Changing trend
* Complex seasonal behavior
* Robust decomposition
* Outliers

A robust STL decomposition can reduce the influence of extreme observations.

```python
result = STL(
    df["sales"],
    period=12,
    robust=True
).fit()
```

---

# 18. Stationarity

A time series is stationary when its important statistical properties remain stable over time.

For weak stationarity:

### Constant Mean

$$
E(Y_t)=\mu
$$

### Constant Variance

$$
Var(Y_t)=\sigma^2
$$

### Autocovariance

Depends on lag rather than absolute time.

---

# 19. Intuition Behind Stationarity

Non-stationary:

```text
Mean changes
Variance changes
Trend exists
Seasonality exists
```

Stationary:

```text
Mean approximately constant
Variance approximately constant
Dependence structure stable
```

Conceptually:

```text
Non-Stationary
100 → 120 → 150 → 190 → 240

Stationary
100 → 95 → 103 → 98 → 101
```

---

# 20. Why Stationarity Matters

Stationarity is important for many classical time-series models.

Especially:

* AR
* MA
* ARMA
* ARIMA

If a series is strongly non-stationary, model assumptions may be violated.

Potential problems include:

* Unstable parameter estimates
* Poor forecasts
* Spurious relationships
* Misleading statistical inference

---

# 21. Strict vs Weak Stationarity

## Strict Stationarity

The joint probability distribution remains unchanged after shifting the time origin.

Formally:

$$
(Y_{t_1},Y_{t_2},...,Y_{t_n})
$$

has the same distribution as:

$$
(Y_{t_1+k},Y_{t_2+k},...,Y_{t_n+k})
$$

for any time shift `k`.

This is a strong theoretical condition.

---

## Weak Stationarity

A process is weakly stationary when:

```text
Mean is constant
Variance is constant
Covariance depends only on lag
```

Weak stationarity is commonly used in practical classical forecasting.

---

# 22. Non-Stationarity

Common causes:

```text
Trend
Seasonality
Changing Variance
Structural Breaks
Unit Root
```

A time series can contain more than one source of non-stationarity.

---

# 23. Trend-Induced Non-Stationarity

Example:

```text
100
120
140
160
180
200
```

The mean changes over time.

Possible solutions:

```text
Differencing
Detrending
Transformation
```

---

# 24. Variance-Induced Non-Stationarity

Example:

```text
Low values:
100 ± 5

High values:
500 ± 50
```

The variance increases with the level.

Possible solutions:

```text
Log transformation
Square-root transformation
Box-Cox transformation
```

---

# 25. Seasonality-Induced Non-Stationarity

A seasonal series can have a repeating pattern:

```text
Jan → Low
Feb → Low
...
Dec → High

Jan → Low
...
Dec → High
```

Possible solution:

> Seasonal differencing.

---

# 26. Unit Root

A unit root is a major cause of non-stationarity.

Consider:

$$
Y_t=\phi Y_{t-1}+\epsilon_t
$$

If:

$$
\phi=1
$$

then:

$$
Y_t=Y_{t-1}+\epsilon_t
$$

This is a random walk.

It is non-stationary.

---

# 27. Random Walk

A random walk is:

$$
Y_t=Y_{t-1}+\epsilon_t
$$

where:

$$
\epsilon_t
$$

is white noise.

Characteristics:

* Non-stationary
* Strong persistence
* Variance grows over time
* Often requires differencing

First difference:

$$
\Delta Y_t=Y_t-Y_{t-1}
$$

Therefore:

$$
\Delta Y_t=\epsilon_t
$$

which can be stationary if the errors are white noise.

---

# 28. Differencing

Differencing removes changes in level.

First difference:

$$
\Delta Y_t=Y_t-Y_{t-1}
$$

Example:

| Time | Value | Difference |
| ---- | ----: | ---------: |
| Jan  |   100 |          - |
| Feb  |   110 |         10 |
| Mar  |   125 |         15 |
| Apr  |   130 |          5 |

---

# 29. First-Order Differencing

Formula:

$$
\Delta Y_t=(1-B)Y_t
$$

where `B` is the backshift operator.

Example:

```text
Original:
100 → 110 → 125 → 130

Difference:
10 → 15 → 5
```

---

# 30. Second-Order Differencing

If first differencing is not sufficient:

$$
\Delta^2Y_t
===========

\Delta(\Delta Y_t)
$$

or:

$$
\Delta^2Y_t
===========

Y_t-2Y_{t-1}+Y_{t-2}
$$

Use second differencing only when necessary.

---

# 31. Over-Differencing

Over-differencing occurs when we difference a series more than necessary.

Possible consequences:

* Excessive noise
* Loss of useful information
* Negative autocorrelation
* Poor model performance

### Rule

> Use the minimum amount of differencing needed to achieve an appropriate stationary representation.

---

# 32. Seasonal Differencing

For seasonal period `m`:

$$
\Delta_mY_t
===========

Y_t-Y_{t-m}
$$

Example for monthly data with yearly seasonality:

$$
\Delta_{12}Y_t
==============

Y_t-Y_{t-12}
$$

Example:

```text
January 2026
-
January 2025
```

---

# 33. Regular vs Seasonal Differencing

| Regular Differencing       | Seasonal Differencing          |
| -------------------------- | ------------------------------ |
| `Yₜ - Yₜ₋₁`                | `Yₜ - Yₜ₋ₘ`                    |
| Removes non-seasonal trend | Removes seasonal pattern       |
| Lag = 1                    | Lag = seasonal period          |
| Example: monthly change    | Example: year-over-year change |

---

# 34. Combining Differencing

Sometimes both are required:

$$
\Delta\Delta_mY_t
$$

Conceptually:

```text
Original
   ↓
Seasonal Differencing
   ↓
Regular Differencing
   ↓
Stationary Series
```

The exact order depends on the modeling context.

---

# 35. Log Transformation

Log transformation can stabilize variance.

$$
Y'_t=\log(Y_t)
$$

Example:

```text
Original:
100
200
400
800

Log:
4.61
5.30
5.99
6.68
```

The transformation compresses large values.

---

# 36. Why Log Transformation Helps

Suppose:

```text
Sales level increases
        ↓
Seasonal variation increases
        ↓
Variance increases
```

Log transformation can reduce this relationship.

It is especially useful when:

> Seasonal fluctuations are proportional to the level.

---

# 37. Important Log Transformation Rule

Log transformation requires positive values.

For:

$$
\log(Y)
$$

we need:

$$
Y>0
$$

If zeros exist, a common transformation is:

$$
\log(1+Y)
$$

But the choice should be based on the data-generating process rather than applied automatically.

---

# 38. Box-Cox Transformation

The Box-Cox transformation is:

$$
Y^{(\lambda)}
=============

\begin{cases}
\frac{Y^\lambda-1}{\lambda}, & \lambda\neq0\
\log(Y), & \lambda=0
\end{cases}
$$

The parameter `λ` controls the transformation.

Common values:

|   λ | Transformation    |
| --: | ----------------- |
|   1 | No transformation |
| 0.5 | Square-root-like  |
|   0 | Log               |
|  -1 | Reciprocal-like   |

Box-Cox generally requires positive data.

---

# 39. ADF Test

**ADF = Augmented Dickey-Fuller Test**

It tests for the presence of a unit root.

### Hypotheses

**H₀:**

> The series has a unit root and is non-stationary.

**H₁:**

> The series does not have a unit root.

### Decision

If:

$$
p < 0.05
$$

Reject `H₀`.

This provides evidence that the series is stationary under the test specification.

---

# 40. ADF Test in Python

```python
from statsmodels.tsa.stattools import adfuller

result = adfuller(df["sales"].dropna())

print("ADF Statistic:", result[0])
print("p-value:", result[1])
```

Interpretation:

```text
p < 0.05
→ Reject H₀
→ Evidence against unit root
→ Series can be treated as stationary under the test
```

If:

```text
p >= 0.05
```

we fail to reject `H₀`.

---

# 41. ADF Test Interpretation

Example:

```text
ADF Statistic = -4.25
p-value = 0.001
```

Since:

$$
0.001 < 0.05
$$

we reject the null hypothesis.

Conclusion:

> There is statistical evidence against a unit root.

---

# 42. KPSS Test

**KPSS = Kwiatkowski-Phillips-Schmidt-Shin Test**

It provides a complementary stationarity test.

### Null Hypothesis

The series is stationary around:

* A level, or
* A deterministic trend

depending on the test specification.

### Alternative

The series is non-stationary.

---

# 43. KPSS in Python

```python
from statsmodels.tsa.stattools import kpss

result = kpss(
    df["sales"].dropna(),
    regression="c",
    nlags="auto"
)

print("KPSS Statistic:", result[0])
print("p-value:", result[1])
```

For `regression="c"`:

> The null is level stationarity.

---

# 44. ADF vs KPSS

The tests have opposite null hypotheses.

| Test | Null Hypothesis            |
| ---- | -------------------------- |
| ADF  | Non-stationary / unit root |
| KPSS | Stationary                 |

This makes them useful together.

---

# 45. ADF + KPSS Decision Table

| ADF               | KPSS              | Interpretation                             |
| ----------------- | ----------------- | ------------------------------------------ |
| Reject H₀         | Fail to reject H₀ | Strong evidence for stationarity           |
| Fail to reject H₀ | Reject H₀         | Strong evidence for non-stationarity       |
| Reject H₀         | Reject H₀         | Could indicate trend/structural complexity |
| Fail to reject H₀ | Fail to reject H₀ | Tests may be inconclusive                  |

Always interpret test results together with plots and domain knowledge.

---

# 46. Visual Stationarity Check

Statistical tests should not be the only method.

Check:

```text
Time-Series Plot
Rolling Mean
Rolling Standard Deviation
ACF
```

Example:

```python
rolling_mean = df["sales"].rolling(12).mean()
rolling_std = df["sales"].rolling(12).std()
```

Plot them to inspect whether the level and variability remain reasonably stable.

---

# 47. ACF

ACF measures correlation between:

$$
Y_t
$$

and:

$$
Y_{t-k}
$$

for different lags.

Python:

```python
from statsmodels.graphics.tsaplots import plot_acf

plot_acf(
    df["sales"].dropna(),
    lags=40
)
```

---

# 48. PACF

PACF measures the direct relationship between `Yₜ` and `Yₜ₋ₖ` after accounting for shorter lags.

Python:

```python
from statsmodels.graphics.tsaplots import plot_pacf

plot_pacf(
    df["sales"].dropna(),
    lags=40
)
```

---

# 49. ACF Pattern for Non-Stationarity

A non-stationary series often shows:

> Slowly decaying ACF.

Example:

```text
Lag:
1   █████████
2   ████████
3   ███████
4   ██████
5   █████
6   ████
...
```

A very slow decay can indicate strong persistence or non-stationarity.

---

# 50. ACF Pattern for Stationary Series

A stationary series often has an ACF that decreases more quickly.

Example:

```text
Lag:
1   █████
2   ██
3   █
4
5
```

The exact pattern depends on the underlying process.

---

# 51. ACF and Seasonality

For monthly data with yearly seasonality:

```text
Lag 12
Lag 24
Lag 36
```

may show significant spikes.

This indicates repeated dependence at seasonal intervals.

---

# 52. PACF and AR Identification

For an AR process:

```text
ACF → Gradual decay
PACF → Sharp cutoff
```

Example:

For AR(2):

```text
PACF:
Lag 1 → Significant
Lag 2 → Significant
Lag 3+ → Approximately insignificant
```

This is a practical identification rule.

---

# 53. ACF and MA Identification

For an MA process:

```text
ACF → Sharp cutoff
PACF → Gradual decay
```

Example:

For MA(2):

```text
ACF:
Lag 1 → Significant
Lag 2 → Significant
Lag 3+ → Approximately insignificant
```

---

# 54. ACF/PACF Identification Summary

| Model | ACF               | PACF              |
| ----- | ----------------- | ----------------- |
| AR(p) | Tails off         | Cuts off around p |
| MA(q) | Cuts off around q | Tails off         |
| ARMA  | Tails off         | Tails off         |

These are identification guidelines and should be confirmed using model diagnostics and validation.

---

# 55. White Noise

A white-noise process has:

* Constant mean
* Constant variance
* No serial correlation

Example:

```text
2, -1, 0.5, -2, 1.3, 0, -0.7
```

The observations are not systematically related over time.

---

# 56. White Noise in Forecasting

After fitting a forecasting model:

```text
Actual
  ↓
Model
  ↓
Residuals
  ↓
Residual diagnostics
```

If residuals behave like white noise:

> The model has captured most predictable temporal structure.

---

# 57. Ljung-Box Test

The Ljung-Box test checks whether a group of autocorrelations is jointly different from zero.

### Null Hypothesis

> The residuals have no autocorrelation up to the tested lags.

Python:

```python
from statsmodels.stats.diagnostic import acorr_ljungbox

result = acorr_ljungbox(
    residuals,
    lags=[10, 20],
    return_df=True
)

print(result)
```

---

# 58. Ljung-Box Interpretation

If:

$$
p > 0.05
$$

we fail to reject the null hypothesis.

This provides no strong statistical evidence of residual autocorrelation at the tested lags.

If:

$$
p < 0.05
$$

there is evidence that residual autocorrelation remains.

---

# 59. Residual Diagnostics

After fitting a forecasting model, examine:

```text
Residual Mean
Residual Variance
Residual ACF
Residual Distribution
Ljung-Box Test
```

Ideal residual behavior:

```text
Mean ≈ 0
Constant variance
No autocorrelation
No obvious structure
```

---

# 60. Residual Diagnostic Workflow

```text
Forecasting Model
       ↓
Calculate Residuals
       ↓
Plot Residuals
       ↓
Check Mean
       ↓
Check Variance
       ↓
Check ACF
       ↓
Ljung-Box Test
       ↓
White Noise?
```

---

# 61. Structural Breaks

A structural break occurs when the underlying behavior of the series changes.

Example:

```text
Before 2020:
Sales ≈ 100/day

After 2020:
Sales ≈ 180/day
```

Possible causes:

* New product
* Pricing change
* New competitor
* Pandemic
* Regulation
* Economic shock
* Business strategy

---

# 62. Why Structural Breaks Matter

A model trained entirely on old behavior may perform poorly after a structural break.

Example:

```text
Historical Pattern
       ↓
Structural Break
       ↓
New Pattern
```

Possible responses:

* Add relevant external variables
* Retrain the model
* Use recent data
* Add regime indicators
* Use models capable of adapting to changes

---

# 63. Outliers vs Structural Breaks

### Outlier

A temporary unusual observation.

```text
100
105
102
250  ← Outlier
103
101
```

### Structural Break

A persistent change.

```text
100
105
102

180
185
190
```

The distinction is important for preprocessing.

---

# 64. Time Series Decomposition in Practice

Example:

```python
from statsmodels.tsa.seasonal import seasonal_decompose

result = seasonal_decompose(
    df["sales"],
    model="additive",
    period=12
)

trend = result.trend
seasonal = result.seasonal
residual = result.resid
```

Inspect:

```python
trend.plot()
seasonal.plot()
residual.plot()
```

---

# 65. STL in Practice

```python
from statsmodels.tsa.seasonal import STL

stl = STL(
    df["sales"],
    period=12,
    robust=True
)

result = stl.fit()

trend = result.trend
seasonal = result.seasonal
residual = result.resid
```

---

# 66. Stationarity Workflow

```text
Original Series
      ↓
Plot Series
      ↓
Check Trend / Seasonality
      ↓
Rolling Mean / Std
      ↓
ADF Test
      ↓
KPSS Test
      ↓
Stationary?
   ↙       ↘
 Yes       No
  ↓         ↓
Model    Transform /
         Difference
              ↓
       Re-test Stationarity
```

---

# 67. Example: Making a Series Stationary

Suppose:

```text
ADF p-value = 0.60
```

The null hypothesis cannot be rejected.

Possible approach:

```python
df["diff"] = (
    df["sales"]
    .diff()
)
```

Then:

```python
adfuller(
    df["diff"].dropna()
)
```

If the transformed series is stationary under the chosen diagnostics, it can be used for models requiring stationarity.

---

# 68. Seasonal Stationarity

Suppose monthly sales have strong yearly seasonality.

Use:

```python
df["seasonal_diff"] = (
    df["sales"] -
    df["sales"].shift(12)
)
```

Then test the transformed series again.

---

# 69. Transformation + Differencing

Sometimes both variance stabilization and differencing are required.

Example:

```text
Original
   ↓
Log Transformation
   ↓
First Differencing
   ↓
Stationary Series
```

Example:

```python
df["log_sales"] = np.log(df["sales"])

df["diff_log_sales"] = (
    df["log_sales"].diff()
)
```

---

# 70. Important Distinction: Differencing vs Detrending

### Differencing

Uses changes between observations:

$$
Y_t-Y_{t-1}
$$

### Detrending

Explicitly estimates and removes a trend function.

Example:

$$
Y_t=T_t+R_t
$$

Then:

$$
R_t=Y_t-T_t
$$

Both can help with non-stationarity, but they are not identical approaches.

---

# 71. Important Distinction: Seasonality vs Stationarity

A series can be:

```text
Non-stationary
+
Seasonal
```

Seasonality is a pattern.

Stationarity is a property of the statistical behavior of the series.

They are related but not the same concept.

---

# 72. Important Distinction: ACF vs PACF

### ACF

Answers:

> How correlated is the series with its past at different lags?

### PACF

Answers:

> What is the direct relationship with a particular lag after accounting for shorter lags?

---

# 73. Interview Scenario

### Question

Your monthly sales series has strong seasonality and an increasing trend. What would you do?

### Answer

I would first visualize the series and decompose it to understand trend and seasonality. I would check whether variance increases with the level and consider a log or Box-Cox transformation if appropriate. I would assess stationarity using plots and tests such as ADF/KPSS. If necessary, I would apply regular and/or seasonal differencing, then re-check stationarity before fitting an appropriate forecasting model.

---

# 74. Interview Scenario

### Question

ADF p-value is 0.80. What does it mean?

### Answer

The ADF null hypothesis of a unit root cannot be rejected at conventional significance levels. This provides insufficient evidence that the series is stationary.

---

# 75. Interview Scenario

### Question

KPSS p-value is 0.01. What does it mean?

### Answer

The KPSS null hypothesis of stationarity is rejected at the 5% significance level, providing evidence of non-stationarity under the selected test specification.

---

# 76. Interview Scenario

### Question

ADF says stationary but KPSS says non-stationary. What would you do?

### Answer

I would not rely on a single test. I would inspect the time-series plot, rolling statistics, ACF/PACF, possible trend or structural breaks, and the exact specifications of both tests before deciding whether transformation or differencing is required.

---

# 77. Interview Scenario

### Question

Why should you not blindly difference until ADF p-value becomes less than 0.05?

### Answer

Because excessive differencing can remove useful information, increase noise, introduce strong negative autocorrelation, and produce a worse model. Differencing should be based on statistical evidence, plots, domain knowledge, and model performance.

---

# 78. Interview Scenario

### Question

Your residuals still have significant autocorrelation after fitting ARIMA. What does it indicate?

### Answer

It indicates that the model has not captured all of the temporal dependence. I would inspect the residual ACF/PACF, reconsider the model order or seasonal terms, check for missing variables or structural changes, and compare alternative models.

---

# 79. Interview Questions

## Q1. What is time-series decomposition?

Breaking a time series into components such as trend, seasonality, and residual.

---

## Q2. What is additive decomposition?

$$
Y_t=T_t+S_t+R_t
$$

It is suitable when seasonal variation is approximately constant.

---

## Q3. What is multiplicative decomposition?

$$
Y_t=T_t\times S_t\times R_t
$$

It is suitable when seasonal variation changes proportionally with the level.

---

## Q4. What is STL?

Seasonal-Trend decomposition using LOESS.

It provides flexible trend and seasonal decomposition and can be made robust to outliers.

---

## Q5. What is stationarity?

A time series whose important statistical properties remain stable over time.

---

## Q6. Why is stationarity important?

Many classical models such as AR, MA, ARMA, and ARIMA rely on stationary representations.

---

## Q7. What causes non-stationarity?

Common causes include:

* Trend
* Seasonality
* Changing variance
* Unit roots
* Structural breaks

---

## Q8. What is differencing?

Subtracting a previous observation from the current observation.

$$
\Delta Y_t=Y_t-Y_{t-1}
$$

---

## Q9. What is seasonal differencing?

Subtracting the observation from the previous seasonal cycle.

$$
\Delta_mY_t=Y_t-Y_{t-m}
$$

---

## Q10. What is over-differencing?

Applying more differencing than necessary.

---

## Q11. What is ADF?

A unit-root test where the null hypothesis is that the series has a unit root.

---

## Q12. What is KPSS?

A stationarity test where the null hypothesis is stationarity under the specified deterministic component.

---

## Q13. Why use ADF and KPSS together?

Their null hypotheses are complementary, providing a stronger diagnostic than relying on one test alone.

---

## Q14. What is a unit root?

A unit root occurs when an autoregressive process has a characteristic root at 1, commonly producing non-stationary behavior.

---

## Q15. What is white noise?

A random process with approximately constant mean and variance and no serial correlation.

---

## Q16. What is Ljung-Box test?

A test for whether a group of autocorrelations is jointly significant.

---

## Q17. What should residuals look like?

Ideally:

```text
Mean ≈ 0
Constant variance
No autocorrelation
No systematic pattern
```

---

# 80. Quick Revision

```text
TIME SERIES DECOMPOSITION
│
├── Observed
│
├── Trend
│
├── Seasonality
│
└── Residual
```

```text
ADDITIVE
Y = T + S + R
```

```text
MULTIPLICATIVE
Y = T × S × R
```

```text
STATIONARITY
│
├── Constant Mean
├── Constant Variance
└── Autocovariance depends on Lag
```

```text
NON-STATIONARITY
│
├── Trend
├── Seasonality
├── Changing Variance
├── Unit Root
└── Structural Break
```

```text
MAKE STATIONARY
│
├── Differencing
├── Seasonal Differencing
├── Log Transformation
├── Box-Cox Transformation
└── Detrending
```

```text
STATIONARITY TESTS
│
├── ADF
│   └── H₀: Unit Root / Non-Stationary
│
└── KPSS
    └── H₀: Stationary
```

```text
MODEL DIAGNOSTICS
│
├── Residual Plot
├── Residual ACF
├── Residual Variance
└── Ljung-Box
```

---

# 81. Must Remember

```text
Additive:
Y = T + S + R

Multiplicative:
Y = T × S × R

First Difference:
ΔYₜ = Yₜ - Yₜ₋₁

Seasonal Difference:
ΔₘYₜ = Yₜ - Yₜ₋ₘ

ADF:
H₀ → Unit Root / Non-Stationary

KPSS:
H₀ → Stationary

ADF p < 0.05:
Reject unit-root null

KPSS p < 0.05:
Reject stationarity null

ACF:
Correlation with lagged values

PACF:
Direct lag relationship

Ljung-Box:
Checks residual autocorrelation

Good Residuals:
Approximately white noise
```

---

# 82. One-Minute Interview Explanation

> Before building a forecasting model, I first analyze the time series components such as trend, seasonality, and residual behavior. I can use classical decomposition or STL to separate these components. I then check stationarity using visual analysis, rolling statistics, ADF, and KPSS tests. If the series is non-stationary, I consider appropriate transformations, regular differencing, or seasonal differencing while avoiding over-differencing. I use ACF and PACF to understand temporal dependencies and help identify model structures. After fitting a forecasting model, I analyze residuals and use tools such as residual ACF and the Ljung-Box test to verify that the remaining errors do not contain significant predictable temporal structure.
