# 03_Time_Series_Forecasting_Models.md

# Time Series & Forecasting — Models

## 1. Time Series Model Categories

Time-series forecasting models can be broadly divided into:

```text
Time Series Forecasting
│
├── Naive Methods
│
├── Moving Average
│
├── Exponential Smoothing
│   ├── Simple Exponential Smoothing
│   ├── Holt's Method
│   └── Holt-Winters
│
├── Statistical Models
│   ├── AR
│   ├── MA
│   ├── ARMA
│   ├── ARIMA
│   ├── SARIMA
│   └── SARIMAX
│
├── Multivariate Models
│   └── VAR
│
├── Machine Learning
│   ├── Linear Regression
│   ├── Random Forest
│   ├── XGBoost
│   └── LightGBM
│
└── Deep Learning
    ├── RNN
    ├── LSTM
    ├── GRU
    └── Transformer
```

---

# 2. Naive Forecasting

The naive method uses the most recent observation as the next forecast.

Formula:

```text
Y_hat(t+1) = Y(t)
```

Example:

```text
Today's Sales = 500

Tomorrow's Forecast = 500
```

Python:

```python
forecast = train["sales"].iloc[-1]
```

### Advantages

* Very simple
* Fast
* No training required
* Excellent baseline

### Disadvantages

* Cannot model trend
* Cannot model seasonality
* Cannot capture complex patterns

---

# 3. Seasonal Naive Forecast

Seasonal naive forecasting uses the value from the previous seasonal cycle.

Formula:

```text
Y_hat(t) = Y(t-m)
```

Where:

```text
m = Seasonal Period
```

Example:

For monthly data with yearly seasonality:

```text
m = 12
```

Therefore:

```text
Y_hat(t) = Y(t-12)
```

Python:

```python
forecast = df["sales"].shift(12)
```

Useful when strong seasonality exists.

---

# 4. Moving Average Model

A moving average forecast uses the average of recent observations.

For window size `k`:

```text
Y_hat(t+1) =
[Y(t) + Y(t-1) + ... + Y(t-k+1)]
-----------------------------------
k
```

Example with `k = 3`:

```text
Sales:

100
110
120

Forecast:

(100 + 110 + 120) / 3
= 110
```

Python:

```python
forecast = (
    df["sales"]
    .rolling(3)
    .mean()
)
```

---

# 5. Weighted Moving Average

More recent observations can receive greater weight.

Formula:

```text
Y_hat(t+1) =
w1Y(t) + w2Y(t-1) + ... + wkY(t-k+1)
```

Subject to:

```text
w1 + w2 + ... + wk = 1
```

Example:

```text
Today's value      → Weight 0.5
Yesterday's value  → Weight 0.3
2 days ago         → Weight 0.2
```

Recent observations have more influence.

---

# 6. Exponential Smoothing

Exponential smoothing gives greater weight to recent observations.

Basic idea:

```text
Recent observations
        ↓
Higher weight

Older observations
        ↓
Lower weight
```

The major methods are:

```text
Simple Exponential Smoothing
Holt's Method
Holt-Winters
```

---

# 7. Simple Exponential Smoothing

Simple Exponential Smoothing is appropriate when the series has:

* No significant trend
* No significant seasonality

Formula:

```text
L(t) = αY(t) + (1-α)L(t-1)
```

Where:

```text
L(t) = Current level
Y(t) = Actual observation
α = Smoothing parameter
```

`α` ranges from:

```text
0 < α < 1
```

---

# 8. Effect of Alpha

### High Alpha

```text
α → 1
```

The model gives more importance to recent observations.

Result:

```text
More responsive
More sensitive to noise
```

### Low Alpha

```text
α → 0
```

The model gives more importance to historical values.

Result:

```text
Smoother
Less responsive
```

---

# 9. Simple Exponential Smoothing in Python

```python
from statsmodels.tsa.holtwinters import (
    SimpleExpSmoothing
)

model = SimpleExpSmoothing(
    train["sales"]
)

fit = model.fit()

forecast = fit.forecast(
    len(test)
)
```

---

# 10. Holt's Linear Trend Method

Holt's method extends exponential smoothing to handle trend.

It maintains:

```text
Level
Trend
```

Equations:

```text
L(t) =
αY(t) + (1-α)[L(t-1) + B(t-1)]
```

```text
B(t) =
β[L(t) - L(t-1)] + (1-β)B(t-1)
```

Forecast:

```text
Y_hat(t+h) =
L(t) + hB(t)
```

Where:

```text
L(t) = Level
B(t) = Trend
α = Level smoothing parameter
β = Trend smoothing parameter
h = Forecast horizon
```

---

# 11. Holt's Method in Python

```python
from statsmodels.tsa.holtwinters import Holt

model = Holt(
    train["sales"]
)

fit = model.fit()

forecast = fit.forecast(
    len(test)
)
```

Use Holt when:

```text
Trend exists
Seasonality is absent
```

---

# 12. Holt-Winters Method

Holt-Winters extends Holt's method by incorporating seasonality.

It models:

```text
Level
Trend
Seasonality
```

Two major forms:

```text
Additive Seasonality
Multiplicative Seasonality
```

---

# 13. Holt-Winters Additive Seasonality

Use when seasonal variation is approximately constant.

Example:

```text
January  → +100
February → +80
March    → +120
```

Seasonal effect remains approximately similar over time.

---

# 14. Holt-Winters Multiplicative Seasonality

Use when seasonal variation changes with the level.

Example:

```text
Year 1:
Base = 1000
Seasonal increase = 200

Year 2:
Base = 2000
Seasonal increase = 400
```

The seasonal effect increases with the level.

---

# 15. Holt-Winters in Python

```python
from statsmodels.tsa.holtwinters import (
    ExponentialSmoothing
)

model = ExponentialSmoothing(
    train["sales"],
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

# 16. AR Model — Autoregressive

AR means **AutoRegressive**.

The current value depends on its previous values.

AR(p):

```text
Y(t) =
c
+
φ1Y(t-1)
+
φ2Y(t-2)
+
...
+
φpY(t-p)
+
ε(t)
```

Where:

```text
p = Number of lags
φ = Model coefficients
ε(t) = Error
```

---

# 17. AR(1)

AR(1) uses only one previous observation.

```text
Y(t) =
c
+
φ1Y(t-1)
+
ε(t)
```

Example:

```text
Today's Sales
     ↑
Yesterday's Sales
```

The current value depends on the previous value.

---

# 18. AR(2)

AR(2) uses two previous observations.

```text
Y(t) =
c
+
φ1Y(t-1)
+
φ2Y(t-2)
+
ε(t)
```

Conceptually:

```text
Today
 ↑
Yesterday
 ↑
2 Days Ago
```

---

# 19. MA Model — Moving Average

The MA model uses previous forecast errors.

MA(q):

```text
Y(t) =
c
+
ε(t)
+
θ1ε(t-1)
+
θ2ε(t-2)
+
...
+
θqε(t-q)
```

Where:

```text
q = Number of previous errors
θ = Model coefficients
ε(t) = Error
```

Important:

> MA in ARIMA is different from a simple moving-average smoothing method.

---

# 20. AR vs MA

| AR                                | MA                               |
| --------------------------------- | -------------------------------- |
| Uses previous observations        | Uses previous errors             |
| AR(p)                             | MA(q)                            |
| Uses lagged Y values              | Uses lagged residuals/errors     |
| PACF is useful for identification | ACF is useful for identification |

---

# 21. ARMA Model

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
+
φ1Y(t-1)
+
...
+
φpY(t-p)
+
ε(t)
+
θ1ε(t-1)
+
...
+
θqε(t-q)
```

ARMA is generally used for stationary time series.

---

# 22. ARIMA Model

ARIMA stands for:

```text
AutoRegressive
Integrated
Moving Average
```

Written as:

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

# 23. Meaning of ARIMA Parameters

Example:

```text
ARIMA(2,1,1)
```

Means:

```text
p = 2
→ Two AR terms

d = 1
→ First-order differencing

q = 1
→ One MA term
```

---

# 24. ARIMA Workflow

```text
Original Time Series
        ↓
Check Stationarity
        ↓
Differencing
        ↓
Stationary Series
        ↓
ACF / PACF
        ↓
Select p and q
        ↓
Fit ARIMA
        ↓
Check Residuals
        ↓
Forecast
```

---

# 25. ARIMA Equation Concept

ARIMA applies ARMA modeling to a differenced series.

If:

```text
W(t) = Δ^d Y(t)
```

then ARMA can be applied to `W(t)`.

Conceptually:

```text
Original Series
      ↓
Differencing
      ↓
Stationary Series
      ↓
AR + MA
```

---

# 26. ARIMA in Python

```python
from statsmodels.tsa.arima.model import ARIMA

model = ARIMA(
    train["sales"],
    order=(2, 1, 1)
)

fit = model.fit()

forecast = fit.forecast(
    steps=len(test)
)
```

---

# 27. How to Select ARIMA p, d, q

### `d`

Determine using:

* Stationarity tests
* Visual inspection
* Amount of differencing required

### `p`

PACF can provide diagnostic information.

### `q`

ACF can provide diagnostic information.

Then compare candidate models using:

```text
AIC
BIC
Validation Error
Residual Diagnostics
```

---

# 28. AIC

AIC means:

**Akaike Information Criterion**

It balances:

```text
Model Fit
+
Model Complexity
```

General form:

```text
AIC = 2k - 2ln(L)
```

Where:

```text
k = Number of estimated parameters
L = Maximum likelihood
```

Lower AIC is generally preferred when comparing models fit to the same data and objective.

---

# 29. BIC

BIC means:

**Bayesian Information Criterion**

General form:

```text
BIC =
k ln(n)
-
2ln(L)
```

Where:

```text
k = Number of parameters
n = Number of observations
L = Maximum likelihood
```

BIC generally penalizes model complexity more strongly than AIC.

Lower BIC is generally preferred.

---

# 30. AIC vs BIC

| AIC                                       | BIC                         |
| ----------------------------------------- | --------------------------- |
| Penalizes complexity                      | Stronger complexity penalty |
| Often favors slightly more complex models | Often favors simpler models |
| Useful for model comparison               | Useful for model comparison |

Neither should replace out-of-sample validation.

---

# 31. SARIMA

SARIMA extends ARIMA to handle seasonality.

Written as:

```text
SARIMA(p,d,q)(P,D,Q,m)
```

Where:

```text
p = Non-seasonal AR order
d = Non-seasonal differencing
q = Non-seasonal MA order

P = Seasonal AR order
D = Seasonal differencing
Q = Seasonal MA order
m = Seasonal period
```

---

# 32. Example SARIMA

```text
SARIMA(1,1,1)(1,1,1,12)
```

For monthly data:

```text
m = 12
```

Meaning:

```text
Non-seasonal:
AR = 1
Differencing = 1
MA = 1

Seasonal:
AR = 1
Differencing = 1
MA = 1
Seasonal period = 12
```

---

# 33. Seasonal Differencing in SARIMA

Seasonal differencing:

```text
Y'(t) =
Y(t) - Y(t-m)
```

For monthly yearly seasonality:

```text
Y'(t) =
Y(t) - Y(t-12)
```

---

# 34. SARIMA in Python

```python
from statsmodels.tsa.statespace.sarimax import (
    SARIMAX
)

model = SARIMAX(
    train["sales"],
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

# 35. SARIMAX

SARIMAX means:

```text
SARIMA
+
Exogenous Variables
```

It can incorporate external variables.

Example:

```text
Sales
  ↑
  ├── Historical Sales
  ├── Seasonality
  ├── Price
  ├── Promotion
  └── Holiday
```

---

# 36. SARIMAX Example

Suppose:

```text
Target:
Sales

Exogenous variables:
Price
Promotion
Temperature
```

Python:

```python
model = SARIMAX(
    train["sales"],
    exog=train[
        ["price", "promotion", "temperature"]
    ],
    order=(1, 1, 1),
    seasonal_order=(1, 1, 1, 12)
)
```

For future forecasting, future values of the exogenous variables generally need to be known or forecasted.

---

# 37. SARIMA vs SARIMAX

| SARIMA                 | SARIMAX                                     |
| ---------------------- | ------------------------------------------- |
| Uses historical target | Uses historical target + external variables |
| Univariate             | Can incorporate exogenous variables         |
| No external regressors | Supports external regressors                |

---

# 38. VAR — Vector Autoregression

VAR is used for multivariate time series.

Suppose we have:

```text
Sales
Price
Production
```

VAR allows each variable to depend on lagged values of all variables.

Conceptually:

```text
Sales(t)
   ↑
Sales(t-1)
Price(t-1)
Production(t-1)
```

And:

```text
Price(t)
   ↑
Sales(t-1)
Price(t-1)
Production(t-1)
```

---

# 39. When to Use VAR

Use VAR when:

* Multiple time-series variables exist
* Variables may influence each other
* Relationships among variables are important

Examples:

```text
GDP
Inflation
Interest Rate
```

or:

```text
Sales
Price
Production
```

---

# 40. Machine Learning for Forecasting

Time-series forecasting can also be converted into a supervised-learning problem.

Example:

```text
Features:
lag_1
lag_7
lag_14
rolling_mean_7
month
day_of_week
promotion

Target:
sales(t)
```

Then use:

```text
Linear Regression
Random Forest
XGBoost
LightGBM
CatBoost
```

---

# 41. Machine Learning Forecasting Pipeline

```text
Time Series
    ↓
Feature Engineering
    ↓
Lag Features
    ↓
Rolling Features
    ↓
Calendar Features
    ↓
External Variables
    ↓
Train/Test Split
    ↓
ML Model
    ↓
Forecast
```

---

# 42. Linear Regression for Forecasting

Example:

```text
Sales(t) =
β0
+
β1 Sales(t-1)
+
β2 Sales(t-7)
+
β3 Promotion(t)
+
β4 Price(t)
+
ε(t)
```

Python:

```python
from sklearn.linear_model import LinearRegression

model = LinearRegression()

model.fit(
    X_train,
    y_train
)
```

---

# 43. Tree-Based Models

Common models:

```text
Decision Tree
Random Forest
XGBoost
LightGBM
CatBoost
```

They can learn nonlinear relationships between:

```text
Lag Features
Calendar Features
External Variables
```

and the target.

---

# 44. XGBoost for Forecasting

XGBoost does not inherently understand temporal order.

Therefore, create time-based features.

Example:

```text
lag_1
lag_7
lag_28
rolling_mean_7
rolling_mean_28
month
day_of_week
holiday
promotion
```

Then train XGBoost as a supervised-learning model.

---

# 45. Important Difference

Statistical models such as:

```text
ARIMA
SARIMA
```

explicitly model temporal dependence.

Machine-learning models such as:

```text
XGBoost
Random Forest
```

learn temporal patterns indirectly through engineered features.

---

# 46. LSTM

LSTM stands for:

**Long Short-Term Memory**

It is a type of Recurrent Neural Network.

LSTM is designed to learn dependencies over sequences.

Conceptually:

```text
Past Sequence
     ↓
LSTM
     ↓
Future Prediction
```

---

# 47. LSTM Architecture

An LSTM contains:

```text
Forget Gate
Input Gate
Output Gate
Cell State
Hidden State
```

The gates control information flow through the network.

---

# 48. Why LSTM for Time Series?

LSTM can model:

* Nonlinear relationships
* Sequential dependencies
* Complex temporal patterns
* Long-term dependencies

But:

> LSTM is not automatically better than statistical or tree-based models.

For smaller datasets, classical models or gradient boosting can often be more effective.

---

# 49. GRU

GRU stands for:

**Gated Recurrent Unit**

GRU is another recurrent neural-network architecture.

Compared with LSTM, GRU has a simpler architecture.

Common gates:

```text
Update Gate
Reset Gate
```

GRU can be faster and use fewer parameters than an equivalent LSTM in some situations.

---

# 50. LSTM vs GRU

| LSTM                        | GRU                              |
| --------------------------- | -------------------------------- |
| More complex                | Simpler                          |
| More gates                  | Fewer gates                      |
| More parameters             | Fewer parameters                 |
| Can model long dependencies | Can also model long dependencies |
| Potentially slower          | Often faster                     |

Actual performance depends on the dataset and architecture.

---

# 51. Transformer for Time Series

Transformers use attention mechanisms to model relationships between different positions in a sequence.

Conceptually:

```text
Time 1 ─┐
Time 2 ─┤
Time 3 ─┼──→ Attention → Forecast
Time 4 ─┤
Time 5 ─┘
```

Advantages can include:

* Parallel processing during training
* Modeling long-range relationships
* Flexible multivariate inputs

They can be computationally expensive and require sufficient data and careful validation.

---

# 52. Statistical vs ML vs Deep Learning

| Approach              | Examples               | Strength                         |
| --------------------- | ---------------------- | -------------------------------- |
| Statistical           | ARIMA, SARIMA          | Interpretable temporal structure |
| Exponential Smoothing | Holt-Winters           | Trend + seasonality              |
| ML                    | XGBoost, Random Forest | Nonlinear feature relationships  |
| Deep Learning         | LSTM, GRU              | Complex sequential patterns      |
| Transformer           | Temporal Transformers  | Long-range dependencies          |

---

# 53. Choosing a Forecasting Model

A practical approach:

```text
Start
  ↓
Naive / Seasonal Naive
  ↓
Exponential Smoothing
  ↓
ARIMA / SARIMA / SARIMAX
  ↓
Machine Learning
  ↓
Deep Learning
```

Do not automatically choose the most complex model.

Choose based on:

```text
Data Size
Seasonality
Trend
External Variables
Forecast Horizon
Interpretability
Latency
Computational Cost
Business Requirements
Validation Performance
```

---

# 54. Model Selection Example

### Case 1

Small dataset:

```text
500 observations
Strong seasonality
```

Possible starting models:

```text
Seasonal Naive
Holt-Winters
SARIMA
```

### Case 2

Large dataset:

```text
Millions of observations
Many external variables
Complex nonlinear relationships
```

Possible candidates:

```text
XGBoost
LightGBM
Deep Learning
```

---

# 55. Forecasting Workflow

```text
Business Problem
      ↓
Understand Data
      ↓
Define Forecast Horizon
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
Candidate Models
      ↓
Time-Based Validation
      ↓
Hyperparameter Tuning
      ↓
Residual Diagnostics
      ↓
Final Model
      ↓
Forecast
      ↓
Monitoring
```

---

# 56. Model Evaluation

Important metrics:

```text
MAE
RMSE
MAPE
WAPE
MASE
sMAPE
```

Example:

```python
from sklearn.metrics import (
    mean_absolute_error,
    mean_squared_error
)

mae = mean_absolute_error(
    y_test,
    forecast
)

rmse = mean_squared_error(
    y_test,
    forecast
) ** 0.5
```

---

# 57. Residual Diagnostics

After fitting a model:

```text
Actual
  ↓
Forecast
  ↓
Residuals
```

Residuals should ideally have:

```text
Mean ≈ 0
No trend
No seasonality
No significant autocorrelation
Stable variance
```

---

# 58. Residual ACF

Plotting ACF of residuals can reveal remaining temporal structure.

If residual ACF shows significant autocorrelation:

```text
Residuals
    ↓
Pattern remains
    ↓
Model may be missing information
```

A good model should leave residuals approximately uncorrelated.

---

# 59. Ljung-Box Test

The Ljung-Box test checks whether autocorrelations in a series are jointly significant up to specified lags.

Typical null hypothesis:

```text
H0:
No autocorrelation up to the tested lags
```

A small p-value provides evidence against this null.

Python:

```python
from statsmodels.stats.diagnostic import acorr_ljungbox

result = acorr_ljungbox(
    residuals,
    lags=[10],
    return_df=True
)
```

---

# 60. Confidence vs Prediction Intervals

### Confidence Interval

Represents uncertainty around an estimated quantity such as the mean forecast.

### Prediction Interval

Represents uncertainty around a future observation.

Prediction intervals are generally wider because they include both:

```text
Parameter / forecast uncertainty
+
Future observation noise
```

For forecasting, prediction intervals are often the more relevant concept.

---

# 61. Multi-Step Forecasting

There are three common approaches:

```text
1. Recursive
2. Direct
3. Multi-output
```

### Recursive

```text
t+1
 ↓
t+2
 ↓
t+3
```

### Direct

```text
Model 1 → t+1
Model 2 → t+2
Model 3 → t+3
```

### Multi-output

```text
One model
    ↓
t+1, t+2, t+3
```

---

# 62. Forecasting Example — Demand

Suppose we need to forecast milk demand.

Available data:

```text
Historical Demand
Price
Promotion
Holiday
Temperature
Day of Week
```

Feature engineering:

```text
lag_1
lag_7
lag_14
lag_28
rolling_mean_7
rolling_mean_28
day_of_week
month
holiday
price
promotion
temperature
```

Candidate models:

```text
Seasonal Naive
Holt-Winters
SARIMAX
XGBoost
LSTM
```

Evaluate using:

```text
MAE
RMSE
WAPE
MASE
```

---

# 63. Interview Question — Explain ARIMA

A strong answer:

> ARIMA stands for AutoRegressive Integrated Moving Average. It is represented as ARIMA(p,d,q), where p represents the autoregressive order, d represents the number of differences applied to achieve stationarity, and q represents the moving-average error order. I first analyze stationarity, determine appropriate differencing, use ACF and PACF as diagnostics for candidate orders, fit the model, validate it using time-based data, and then check residuals before using it for forecasting.

---

# 64. Interview Question — Explain SARIMA

> SARIMA extends ARIMA by adding seasonal autoregressive, differencing, and moving-average components. It is represented as SARIMA(p,d,q)(P,D,Q,m), where the second set represents the seasonal components and m represents the seasonal period.

---

# 65. Interview Question — AR vs MA

> AR uses previous values of the time series, while MA uses previous forecast errors. In practice, PACF provides diagnostic information for AR order and ACF provides diagnostic information for MA order.

---

# 66. Interview Question — ARIMA vs SARIMA

> ARIMA models non-seasonal temporal patterns, while SARIMA extends ARIMA to explicitly model recurring seasonal patterns.

---

# 67. Interview Question — SARIMA vs SARIMAX

> SARIMAX extends SARIMA by allowing exogenous variables such as price, promotion, holidays, or weather to influence the forecast.

---

# 68. Interview Question — Why XGBoost for Time Series?

> XGBoost can model nonlinear relationships between engineered temporal features such as lag values, rolling statistics, calendar variables, and external variables. However, XGBoost itself does not inherently understand chronological order, so the features and validation strategy must preserve temporal structure.

---

# 69. Interview Question — Why Not Always Use LSTM?

A good answer:

> LSTM can model complex sequential relationships, but it requires more data, computation, and tuning. For smaller datasets or problems with strong trend and seasonality, simpler models such as seasonal naive, exponential smoothing, SARIMA, or gradient boosting may perform equally well or better. I would select the model based on out-of-sample performance and business requirements rather than complexity.

---

# 70. Interview Question — How Do You Select the Final Model?

> I start with simple baselines and then compare statistical, machine-learning, or deep-learning approaches depending on the data. I use chronological or walk-forward validation, select appropriate forecasting metrics, analyze residuals, consider computational and business requirements, and choose the simplest model that provides reliable out-of-sample performance.

---

# 71. Common Mistakes

## Mistake 1 — Random Train-Test Split

```text
Wrong:
Random Split

Correct:
Chronological Split
```

---

## Mistake 2 — Data Leakage

Using:

```text
Future values
```

to create:

```text
Current features
```

is leakage.

---

## Mistake 3 — Ignoring Baselines

Always compare against:

```text
Naive
Seasonal Naive
```

when appropriate.

---

## Mistake 4 — Over-Differencing

Too much differencing can add unnecessary noise.

---

## Mistake 5 — Blind Outlier Removal

An unusual observation may represent a real business event.

---

## Mistake 6 — Choosing Model Only by AIC

AIC is useful for model comparison, but final selection should consider:

```text
Out-of-sample performance
Residual diagnostics
Business requirements
```

---

## Mistake 7 — Using Future Exogenous Variables Without Availability

For SARIMAX or ML models, ask:

> Will the external variable be known when the forecast is generated?

If not, it must itself be forecasted or otherwise handled appropriately.

---

# 72. Model Comparison

| Model          | Trend                        | Seasonality      | External Variables | Main Use                      |
| -------------- | ---------------------------- | ---------------- | ------------------ | ----------------------------- |
| Naive          | No                           | No               | No                 | Baseline                      |
| Seasonal Naive | No                           | Yes              | No                 | Seasonal baseline             |
| Moving Average | Limited                      | Limited          | No                 | Smoothing                     |
| SES            | Level                        | No               | No                 | Stable series                 |
| Holt           | Yes                          | No               | No                 | Trend                         |
| Holt-Winters   | Yes                          | Yes              | No                 | Trend + Seasonality           |
| AR             | Yes/depends on specification | No               | No                 | Lag dependence                |
| MA             | Error dependence             | No               | No                 | Error structure               |
| ARIMA          | Yes after differencing       | No               | No                 | Non-seasonal series           |
| SARIMA         | Yes                          | Yes              | No                 | Seasonal series               |
| SARIMAX        | Yes                          | Yes              | Yes                | Seasonal + external variables |
| VAR            | Yes/depends on model         | Not explicit     | Multivariate       | Interacting series            |
| XGBoost        | Learned from features        | Through features | Yes                | Nonlinear forecasting         |
| LSTM           | Learned                      | Learned          | Yes                | Complex sequences             |
| GRU            | Learned                      | Learned          | Yes                | Sequential data               |
| Transformer    | Learned                      | Learned          | Yes                | Long-range dependencies       |

---

# 73. Quick Revision

```text
NAIVE
→ Last value

SEASONAL NAIVE
→ Previous seasonal value

MOVING AVERAGE
→ Average recent observations

SES
→ Level

HOLT
→ Level + Trend

HOLT-WINTERS
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

XGBOOST
→ Feature-based nonlinear forecasting

LSTM
→ Recurrent deep-learning model

GRU
→ Simplified recurrent architecture

TRANSFORMER
→ Attention-based sequence modeling
```

---

# 74. ARIMA Parameter Cheat Sheet

```text
ARIMA(p,d,q)

p → AR order
d → Differencing order
q → MA order
```

Example:

```text
ARIMA(2,1,1)

2 → AR terms
1 → First differencing
1 → MA term
```

---

# 75. SARIMA Parameter Cheat Sheet

```text
SARIMA(p,d,q)(P,D,Q,m)

Non-seasonal:
p → AR
d → Differencing
q → MA

Seasonal:
P → Seasonal AR
D → Seasonal Differencing
Q → Seasonal MA
m → Seasonal Period
```

Example:

```text
SARIMA(1,1,1)(1,1,1,12)
```

For monthly data with yearly seasonality.

---

# 76. Final Interview Framework

When asked:

**"How would you build a forecasting model?"**

Use this structure:

```text
1. Business Understanding
        ↓
2. Define Forecast Horizon
        ↓
3. Data Quality Checks
        ↓
4. Time-Series EDA
        ↓
5. Trend / Seasonality
        ↓
6. Stationarity
        ↓
7. Baseline Model
        ↓
8. Feature Engineering
        ↓
9. Candidate Models
        ↓
10. Time-Based Validation
        ↓
11. Hyperparameter Tuning
        ↓
12. Evaluate Metrics
        ↓
13. Residual Diagnostics
        ↓
14. Select Final Model
        ↓
15. Forecast + Prediction Interval
        ↓
16. Deployment
        ↓
17. Monitoring
```

---

# 77. One-Minute Interview Answer

> I would first understand the business objective, forecast horizon, frequency, and target variable. Then I would clean and validate the time index, analyze trend and seasonality, and check stationarity where relevant. I would establish a naive or seasonal-naive baseline before trying more complex models. Depending on the data, I would evaluate exponential smoothing, ARIMA/SARIMA/SARIMAX, or machine-learning models such as XGBoost. For ML models, I would create leakage-safe lag, rolling, calendar, and external-variable features. I would use chronological or walk-forward validation rather than random splitting, compare models using business-appropriate metrics such as MAE, RMSE, WAPE, or MASE, and perform residual diagnostics. Finally, I would select the simplest model that provides reliable out-of-sample performance and deploy it with monitoring.

---

# 78. Core Mental Model

```text
                  FORECASTING
                       │
                       ↓
                 Baseline
                       │
           ┌───────────┼───────────┐
           ↓           ↓           ↓
      Exponential   Statistical     ML
       Smoothing      Models         │
           │           │             │
      Holt-Winters   ARIMA        XGBoost
                      │             │
                   SARIMA       LightGBM
                      │
                  SARIMAX
                       │
                       ↓
                 Deep Learning
                       │
                ┌──────┼──────┐
                ↓      ↓      ↓
               LSTM   GRU  Transformer
                       │
                       ↓
                Time-Based Validation
                       │
                       ↓
                  Residual Check
                       │
                       ↓
                  Final Forecast
```

---

# 79. Most Important Interview Concepts

Prioritize these topics:

```text
1. Time-Series Components
2. Stationarity
3. ADF / KPSS
4. Differencing
5. ACF
6. PACF
7. Naive Forecast
8. Seasonal Naive
9. Exponential Smoothing
10. Holt-Winters
11. AR
12. MA
13. ARMA
14. ARIMA
15. SARIMA
16. SARIMAX
17. AIC / BIC
18. Residual Diagnostics
19. Walk-Forward Validation
20. Time-Series Feature Engineering
21. Temporal Leakage
22. XGBoost Forecasting
23. LSTM / GRU
24. Forecast Metrics
25. Model Selection
```
