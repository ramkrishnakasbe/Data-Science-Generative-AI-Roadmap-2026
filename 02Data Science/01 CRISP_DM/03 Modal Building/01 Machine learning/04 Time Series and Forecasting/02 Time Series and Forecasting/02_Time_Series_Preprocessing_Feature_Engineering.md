# 02_Time_Series_Preprocessing_Feature_Engineering.md

# Time Series — Preprocessing & Feature Engineering

## 1. Why Preprocessing is Important in Time Series

Time-series data requires special preprocessing because observations are ordered chronologically.

The main goals are:

* Correct date/time handling
* Correct frequency
* Missing-value treatment
* Missing timestamp detection
* Outlier handling
* Trend and seasonality analysis
* Stationarity transformation
* Lag feature creation
* Rolling feature creation
* Calendar feature creation
* Avoiding temporal data leakage

General workflow:

```text
Raw Time Series
      ↓
Date/Time Processing
      ↓
Sort Chronologically
      ↓
Frequency Check
      ↓
Missing Dates
      ↓
Missing Values
      ↓
Outliers
      ↓
Transformations
      ↓
Feature Engineering
      ↓
Modeling
```

---

# 2. Date/Time Processing

The first step is converting the date column into a proper datetime format.

```python
import pandas as pd

df["date"] = pd.to_datetime(df["date"])
```

Check:

```python
df["date"].dtype
```

Expected:

```text
datetime64[ns]
```

---

# 3. Sort Data Chronologically

Always sort the data by the time column.

```python
df = df.sort_values("date")
```

Then reset the index:

```python
df = df.reset_index(drop=True)
```

Correct order:

```text
2024-01-01
2024-01-02
2024-01-03
2024-01-04
```

---

# 4. Set Date as Index

For many time-series operations, the date can be used as the index.

```python
df = df.set_index("date")
```

Example:

```text
            sales
date
2024-01-01   100
2024-01-02   110
2024-01-03   105
```

---

# 5. Check Time Frequency

Frequency tells us how often observations occur.

Examples:

```text
Hourly
Daily
Weekly
Monthly
Quarterly
Yearly
```

Check the gaps between timestamps:

```python
df.index.to_series().diff().value_counts()
```

For regular daily data, the dominant difference should generally be:

```text
1 day
```

---

# 6. Missing Timestamps

Missing values and missing timestamps are different problems.

Example:

```text
2024-01-01
2024-01-02
2024-01-04
```

Here:

```text
2024-01-03
```

is missing completely.

There is no row for that date.

---

# 7. Detect Missing Dates

For daily data:

```python
full_range = pd.date_range(
    start=df.index.min(),
    end=df.index.max(),
    freq="D"
)

missing_dates = full_range.difference(df.index)

print(missing_dates)
```

For hourly data:

```python
full_range = pd.date_range(
    start=df.index.min(),
    end=df.index.max(),
    freq="H"
)
```

---

# 8. Reindexing

We can create a complete time index using:

```python
df = df.asfreq("D")
```

This creates missing rows for missing dates.

Example:

```text
Before:

Jan 1 → 100
Jan 2 → 110
Jan 4 → 120

After:

Jan 1 → 100
Jan 2 → 110
Jan 3 → NaN
Jan 4 → 120
```

Now the missing timestamp becomes explicit.

---

# 9. Missing Values

After establishing the correct frequency, check missing values.

```python
df.isnull().sum()
```

Common approaches:

```text
Forward Fill
Backward Fill
Interpolation
Mean/Median
Model-based Imputation
Business-rule-based Imputation
```

The correct method depends on the meaning of the data.

---

# 10. Forward Fill

Forward filling uses the previous available value.

```python
df["sales"] = df["sales"].ffill()
```

Example:

```text
100
110
NaN
NaN
130
```

After forward fill:

```text
100
110
110
110
130
```

Useful when the latest known value reasonably persists until a new observation arrives.

---

# 11. Backward Fill

Backward fill uses the next available value.

```python
df["sales"] = df["sales"].bfill()
```

Example:

```text
100
110
NaN
NaN
130
```

After backward fill:

```text
100
110
130
130
130
```

Use carefully because it uses future information.

For forecasting model training, careless backward filling can introduce temporal leakage.

---

# 12. Time-Based Interpolation

Interpolation estimates missing values using neighboring observations.

```python
df["sales"] = df["sales"].interpolate(
    method="time"
)
```

Example:

```text
100
110
NaN
130
```

Approximate result:

```text
100
110
120
130
```

---

# 13. Missing Value Strategy

There is no universally correct imputation method.

Consider:

```text
1. Why is the value missing?
2. How long is the missing period?
3. Is the variable continuous?
4. Is seasonality present?
5. Is the data causal/business-driven?
6. Could the imputation use future information?
```

For long missing periods, simple interpolation may be inappropriate.

---

# 14. Duplicate Timestamps

Check duplicate timestamps:

```python
df.index.duplicated().sum()
```

Or:

```python
df["date"].duplicated().sum()
```

Duplicate timestamps can cause problems in:

* Aggregation
* Resampling
* Rolling calculations
* Forecasting models

---

# 15. Handling Duplicate Timestamps

First understand why duplicates exist.

Example:

```text
2024-01-01 → Store A → 100
2024-01-01 → Store B → 150
```

These are not necessarily errors.

If the desired series is total sales:

```python
df = (
    df.groupby("date")["sales"]
      .sum()
      .to_frame()
)
```

Never blindly delete duplicates.

---

# 16. Resampling

Resampling changes the frequency of a time series.

Examples:

```text
Hourly → Daily
Daily → Weekly
Daily → Monthly
Monthly → Quarterly
```

Example:

```python
daily_sales = df["sales"].resample("D").sum()
```

Monthly:

```python
monthly_sales = df["sales"].resample("ME").sum()
```

---

# 17. Aggregation Depends on Business Meaning

For sales:

```python
df["sales"].resample("D").sum()
```

For temperature:

```python
df["temperature"].resample("D").mean()
```

For inventory:

```python
df["inventory"].resample("D").last()
```

For maximum temperature:

```python
df["temperature"].resample("D").max()
```

The aggregation function must match the variable's meaning.

---

# 18. Upsampling

Upsampling means increasing the frequency.

Example:

```text
Daily → Hourly
```

This creates additional timestamps but does not magically create real observations.

```python
df.resample("H").asfreq()
```

The new values may be missing and require appropriate interpolation or domain-based treatment.

---

# 19. Downsampling

Downsampling reduces the frequency.

Example:

```text
Hourly → Daily
```

```python
daily = df["sales"].resample("D").sum()
```

This is common when high-frequency data is too noisy or when the business operates at a daily level.

---

# 20. Outliers in Time Series

An outlier is an observation that differs significantly from expected behavior.

Example:

```text
100
105
110
108
5000
112
115
```

The value:

```text
5000
```

may be an outlier.

But in time series, an extreme value may be a legitimate event.

---

# 21. Types of Time-Series Outliers

Common types:

```text
Point Outlier
Temporary Change
Level Shift
Trend Change
Seasonal Anomaly
Collective Anomaly
```

---

# 22. Point Outlier

A single observation is unusually high or low.

```text
100
105
110
500
115
120
```

The value 500 is a point outlier.

---

# 23. Level Shift

The entire series suddenly moves to a new level.

```text
Before:

100
102
98
101

After:

150
152
148
151
```

Possible causes:

* Price change
* Business expansion
* New policy
* Structural change

This should not automatically be treated as an outlier.

---

# 24. Temporary Change

The series temporarily changes and then returns to its previous behavior.

```text
100
105
110
300
115
120
```

Possible cause:

```text
Temporary promotion
Festival
Supply disruption
Weather event
```

---

# 25. Outlier Detection Using IQR

The Interquartile Range method:

```text
IQR = Q3 - Q1
```

Lower bound:

```text
Q1 - 1.5 × IQR
```

Upper bound:

```text
Q3 + 1.5 × IQR
```

Values outside these limits may be considered outliers.

However, blindly applying IQR to trending or seasonal time-series data can produce misleading results.

---

# 26. Rolling Z-Score

A rolling z-score can detect observations that are unusual relative to recent history.

Conceptually:

```text
Z(t) =
[Y(t) - Rolling Mean]
---------------------
Rolling Std
```

Large absolute values can indicate potential anomalies.

---

# 27. Outlier Treatment

Possible approaches:

```text
Keep
Cap/Winsorize
Replace
Interpolate
Transform
Create Anomaly Flag
Remove
```

Best practice:

> Investigate the business reason before removing a time-series outlier.

---

# 28. Log Transformation

Log transformation is useful when:

* Values are highly right-skewed
* Variance increases with level
* Growth is multiplicative

Formula:

```text
Y' = log(Y)
```

Python:

```python
import numpy as np

df["sales_log"] = np.log(df["sales"])
```

If zeros are present:

```python
df["sales_log"] = np.log1p(df["sales"])
```

---

# 29. Box-Cox Transformation

Box-Cox can transform positive-valued data to stabilize variance and make the distribution more suitable for some models.

General form:

```text
Y(λ) =
(Y^λ - 1) / λ        if λ ≠ 0

log(Y)               if λ = 0
```

Box-Cox generally requires positive values.

---

# 30. Yeo-Johnson Transformation

Yeo-Johnson is similar to Box-Cox but can handle zero and negative values.

It is useful when the time-series variable contains:

```text
Positive values
Zero
Negative values
```

---

# 31. Trend Removal

A trend can sometimes be removed before modeling.

For a simple linear trend:

```text
Y(t) = Trend(t) + Residual(t)
```

Detrending can help isolate short-term fluctuations.

However, many forecasting models can model the trend directly, so manual detrending is not always necessary.

---

# 32. Differencing

First-order differencing:

```text
Y'(t) = Y(t) - Y(t-1)
```

Python:

```python
df["diff_1"] = (
    df["sales"].diff(1)
)
```

Purpose:

```text
Remove trend
↓
Help achieve stationarity
```

---

# 33. Seasonal Differencing

Seasonal differencing:

```text
Y'(t) = Y(t) - Y(t-m)
```

For monthly data with yearly seasonality:

```text
m = 12
```

Python:

```python
df["seasonal_diff"] = (
    df["sales"].diff(12)
)
```

---

# 34. Avoid Excessive Differencing

Too much differencing can create:

* Unnecessary noise
* Over-differencing
* Difficult interpretation
* Poor forecasts

General principle:

> Use the minimum differencing needed to achieve an appropriate level of stationarity.

---

# 35. Calendar Features

Calendar features can be very useful in machine-learning forecasting.

Common features:

```text
Year
Month
Quarter
Week
Day
Day of Week
Day of Month
Day of Year
Weekend
Holiday
```

Example:

```python
df["year"] = df.index.year
df["month"] = df.index.month
df["quarter"] = df.index.quarter
df["day_of_week"] = df.index.dayofweek
df["day_of_month"] = df.index.day
```

---

# 36. Weekend Feature

```python
df["is_weekend"] = (
    df.index.dayofweek >= 5
).astype(int)
```

Interpretation:

```text
0 → Weekday
1 → Weekend
```

---

# 37. Month-End and Month-Start Features

```python
df["is_month_start"] = (
    df.index.is_month_start.astype(int)
)

df["is_month_end"] = (
    df.index.is_month_end.astype(int)
)
```

These can be useful when business activity changes around month boundaries.

---

# 38. Holiday Features

Holiday information can be extremely important for demand forecasting.

Example:

```text
Diwali
Christmas
New Year
Eid
Independence Day
Republic Day
```

Create:

```text
is_holiday
days_before_holiday
days_after_holiday
holiday_type
```

Holiday effects should be created using information that would actually be known at forecast time.

---

# 39. Lag Features

Lag features use previous observations.

```python
df["lag_1"] = df["sales"].shift(1)

df["lag_7"] = df["sales"].shift(7)

df["lag_30"] = df["sales"].shift(30)
```

Interpretation:

```text
lag_1
→ Previous period

lag_7
→ 7 periods ago

lag_30
→ 30 periods ago
```

---

# 40. Why Lag Features are Important

Lag features allow machine-learning models to learn temporal relationships.

Example:

```text
Today's Sales
      ↑
Yesterday's Sales
      ↑
Sales 7 Days Ago
      ↑
Sales 30 Days Ago
```

A model can learn relationships such as:

```text
Today's Sales
≈ f(
    Yesterday's Sales,
    Last Week's Sales,
    Last Month's Sales
)
```

---

# 41. Seasonal Lag Features

If weekly seasonality exists in daily data:

```python
df["lag_7"] = df["sales"].shift(7)
```

If yearly seasonality exists in monthly data:

```python
df["lag_12"] = df["sales"].shift(12)
```

These features capture recurring seasonal patterns.

---

# 42. Multiple Lag Features

Example:

```python
lags = [1, 2, 3, 7, 14, 28]

for lag in lags:
    df[f"lag_{lag}"] = (
        df["sales"].shift(lag)
    )
```

Do not create hundreds of arbitrary lags without a reason.

Choose lags based on:

* Business frequency
* Seasonality
* ACF
* Domain knowledge
* Model performance

---

# 43. Rolling Mean

Rolling mean smooths short-term fluctuations.

```python
df["rolling_mean_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .mean()
)
```

The `shift(1)` is important because the feature should use information available before the forecast time.

---

# 44. Rolling Standard Deviation

```python
df["rolling_std_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .std()
)
```

It captures recent volatility.

---

# 45. Rolling Minimum and Maximum

```python
df["rolling_min_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .min()
)

df["rolling_max_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .max()
)
```

These can capture the recent range of the target.

---

# 46. Rolling Sum

Useful for quantities such as:

* Sales
* Orders
* Transactions
* Production

Example:

```python
df["rolling_sales_7"] = (
    df["sales"]
    .shift(1)
    .rolling(7)
    .sum()
)
```

This represents total sales over the previous 7 periods.

---

# 47. Expanding Features

An expanding statistic uses all available historical observations up to that point.

Example:

```python
df["expanding_mean"] = (
    df["sales"]
    .shift(1)
    .expanding()
    .mean()
)
```

Difference:

```text
Rolling:
Fixed-size window

Expanding:
Growing historical window
```

---

# 48. Rolling vs Expanding

| Rolling                   | Expanding                  |
| ------------------------- | -------------------------- |
| Fixed window              | Increasing window          |
| Focuses on recent history | Uses all previous history  |
| Example: last 7 days      | Example: all previous days |

---

# 49. Exponentially Weighted Features

Recent observations can be given more importance using exponentially weighted statistics.

```python
df["ewm_mean"] = (
    df["sales"]
    .shift(1)
    .ewm(span=7)
    .mean()
)
```

Recent observations receive greater weight.

---

# 50. Temporal Data Leakage

Temporal leakage occurs when future information is used during model training or feature creation.

Example:

```python
df["rolling_mean"] = (
    df["sales"]
    .rolling(7)
    .mean()
)
```

This can include the current target.

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

# 51. Example of Leakage

Suppose we want to predict:

```text
Sales on January 10
```

We can use:

```text
January 9
January 8
January 7
...
```

We cannot use:

```text
January 11
January 12
```

because these values were not available at prediction time.

---

# 52. Feature Engineering Rule

For predicting time `t`:

```text
Features
=
Information available before t
```

Conceptually:

```text
              Prediction Time
                     ↓
Past ────────────────|──────── Future
                     ↑
                Prediction
```

Features must come from the left side.

---

# 53. Target Construction

Suppose we want to predict tomorrow's sales.

```python
df["target"] = (
    df["sales"].shift(-1)
)
```

This creates:

```text
Today's Features
        ↓
Tomorrow's Sales
```

For a 7-day-ahead target:

```python
df["target_7"] = (
    df["sales"].shift(-7)
)
```

---

# 54. One-Step Supervised Dataset

Original:

| Date  | Sales |
| ----- | ----: |
| Jan 1 |   100 |
| Jan 2 |   110 |
| Jan 3 |   120 |
| Jan 4 |   130 |

Create:

```text
lag_1
target
```

Result:

| Date  | lag_1 | target |
| ----- | ----: | -----: |
| Jan 2 |   100 |    120 |
| Jan 3 |   110 |    130 |
| Jan 4 |   120 |    140 |

The exact target values depend on the forecasting horizon and original data.

---

# 55. Direct Multi-Step Forecasting

Suppose we want:

```text
t+1
t+2
t+3
```

We can create separate targets:

```python
df["target_1"] = df["sales"].shift(-1)
df["target_2"] = df["sales"].shift(-2)
df["target_3"] = df["sales"].shift(-3)
```

Then train separate models or a multi-output model.

---

# 56. Recursive Forecasting

In recursive forecasting:

```text
Forecast t+1
     ↓
Use forecast t+1
     ↓
Forecast t+2
     ↓
Use forecast t+2
     ↓
Forecast t+3
```

Potential problem:

> Forecast errors can accumulate across multiple steps.

---

# 57. Direct vs Recursive Forecasting

| Direct                               | Recursive                     |
| ------------------------------------ | ----------------------------- |
| Separate prediction for each horizon | One model repeatedly predicts |
| Can reduce error propagation         | Error can accumulate          |
| More models/outputs                  | Simpler setup                 |

---

# 58. Time-Based Train/Test Split

Example:

```python
train = df.loc[
    df.index < "2025-01-01"
]

test = df.loc[
    df.index >= "2025-01-01"
]
```

This preserves temporal order.

---

# 59. Validation Set

A three-way split can be used:

```text
Train
  ↓
Validation
  ↓
Test
```

Example:

```text
2022 ───── 2023 ───── 2024 ───── 2025
  Train      Validation     Test
```

The exact periods depend on the forecasting problem.

---

# 60. Scaling Time-Series Features

Scaling may be required for models such as:

```text
Linear Regression
KNN
Neural Networks
LSTM
GRU
```

Common methods:

```text
StandardScaler
MinMaxScaler
RobustScaler
```

Tree-based models generally do not require feature scaling.

---

# 61. Important Scaling Rule

Fit the scaler only on training data.

Correct:

```python
scaler.fit(X_train)

X_train_scaled = scaler.transform(X_train)
X_test_scaled = scaler.transform(X_test)
```

Do not:

```python
scaler.fit(X)
```

before splitting, because this allows information from the test period to influence preprocessing.

---

# 62. Handling Categorical Variables

Time-series models can also use categorical variables such as:

```text
Store
Product
Region
Holiday Type
Day Type
Promotion Type
```

Possible encoding:

```text
One-Hot Encoding
Target Encoding
Ordinal Encoding
Embeddings
```

Encoding must also be performed without leaking future information.

---

# 63. Fourier Features

Fourier terms can represent smooth seasonal patterns.

Conceptually:

```text
sin(2πkt/m)
cos(2πkt/m)
```

Where:

```text
k = Harmonic number
m = Seasonal period
t = Time
```

Useful for complex or long seasonal patterns.

---

# 64. Why Fourier Features?

Suppose data has yearly seasonality.

Instead of creating:

```text
Month = 1
Month = 2
...
Month = 12
```

we can represent cyclical behavior using sine and cosine terms.

This allows models to understand the circular nature of time.

---

# 65. Cyclical Encoding

Month is cyclical:

```text
December → January
```

Treating:

```text
December = 12
January = 1
```

makes them appear far apart numerically.

Instead:

```text
month_sin =
sin(2π × month / 12)

month_cos =
cos(2π × month / 12)
```

Python:

```python
import numpy as np

df["month_sin"] = np.sin(
    2 * np.pi * df.index.month / 12
)

df["month_cos"] = np.cos(
    2 * np.pi * df.index.month / 12
)
```

---

# 66. Feature Engineering Example

Suppose we forecast daily sales.

Useful features:

```text
Calendar Features
    ↓
Day of Week
Month
Quarter
Holiday

Lag Features
    ↓
lag_1
lag_7
lag_14
lag_28

Rolling Features
    ↓
rolling_mean_7
rolling_mean_28
rolling_std_7

External Variables
    ↓
Price
Promotion
Temperature
```

---

# 67. Example Feature Pipeline

```python
df["day_of_week"] = df.index.dayofweek
df["month"] = df.index.month
df["quarter"] = df.index.quarter

df["lag_1"] = df["sales"].shift(1)
df["lag_7"] = df["sales"].shift(7)
df["lag_28"] = df["sales"].shift(28)

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

df["target"] = (
    df["sales"].shift(-1)
)
```

---

# 68. Feature Selection for Time Series

Not every feature is useful.

Consider:

```text
1. Business relevance
2. Availability at prediction time
3. Correlation
4. ACF/PACF
5. Feature importance
6. Cross-validation performance
7. Multicollinearity
```

Most importantly:

> The feature must be available when the forecast is actually generated.

---

# 69. Data Leakage Checklist

Before training, ask:

```text
Can this feature be known at prediction time?

Does it contain future observations?

Was scaling fitted using test data?

Was imputation based on future values?

Was rolling calculation shifted?

Were train and test split chronologically?

Were hyperparameters selected using the test set?
```

If the answer is wrong to any of these, there may be leakage.

---

# 70. Preprocessing Workflow — Interview Answer

A good interview response:

```text
First, I convert the timestamp into a proper datetime
format and sort the data chronologically.

Then I check the expected frequency and identify missing
timestamps separately from missing values.

I handle missing values based on the business context and
avoid using future information during imputation.

Next, I investigate outliers, trend, seasonality, and
stationarity.

Depending on the model, I may apply transformations,
differencing, or scaling.

For machine-learning forecasting, I create lag,
rolling, calendar, holiday, and external-variable features.

Finally, I make sure every feature is available at the
forecast generation time and perform a chronological
train-validation-test split to prevent temporal leakage.
```

---

# 71. Quick Revision

```text
DATETIME
→ Convert timestamp properly

SORT
→ Always maintain chronological order

FREQUENCY
→ Hourly / Daily / Weekly / Monthly

MISSING TIMESTAMP
→ Missing row in the time index

MISSING VALUE
→ Existing timestamp with missing target/value

RESAMPLING
→ Change time frequency

UPSAMPLING
→ Increase frequency

DOWNSAMPLING
→ Decrease frequency

LAG
→ Previous observation

ROLLING
→ Fixed-size moving window

EXPANDING
→ Increasing historical window

DIFFERENCING
→ Current value - previous value

SEASONAL DIFFERENCING
→ Current value - previous seasonal value

CALENDAR FEATURES
→ Month / Day / Quarter / Weekend

CYCLICAL ENCODING
→ sin/cos representation of cyclic time

OUTLIER
→ Unusual observation

TEMPORAL LEAKAGE
→ Future information enters training/features

TRAIN/TEST
→ Chronological split

SCALING
→ Fit only on training data

TARGET
→ Future value to predict
```

---

# 72. Key Interview Questions

## Q1. How do you preprocess time-series data?

Answer:

> I first convert and validate the datetime column, sort chronologically, verify the expected frequency, detect missing timestamps and missing values, handle duplicates and outliers based on business context, investigate trend and seasonality, apply transformations if required, and then create leakage-safe features such as lags, rolling statistics, calendar features, and external variables.

---

## Q2. How do you handle missing timestamps?

> I first establish the expected frequency, create a complete date range, compare it with the existing timestamps, and identify missing periods. Depending on the business context, I then reindex and decide whether to impute, aggregate, or leave the periods missing.

---

## Q3. How do you handle missing values in time series?

> I choose the method based on the data-generating process. Common approaches include forward fill, interpolation, model-based imputation, or business-rule-based methods. I make sure the method does not introduce future information into the training data.

---

## Q4. Why is `shift(1)` important before rolling features?

> Without shifting, the rolling calculation may include the current target value. That can cause data leakage. `shift(1)` ensures the feature uses only information available before the prediction time.

---

## Q5. How do you create lag features?

```python
df["lag_1"] = df["sales"].shift(1)
df["lag_7"] = df["sales"].shift(7)
```

> I select lags based on the forecasting frequency, seasonality, ACF, and business knowledge.

---

## Q6. What is temporal leakage?

> Temporal leakage occurs when information from the future relative to the prediction time is used to train the model or construct features.

---

## Q7. How do you prevent temporal leakage?

```text
Chronological split
        ↓
Shift lag features
        ↓
Shift rolling features
        ↓
Fit scaler only on training data
        ↓
Avoid future-based imputation
        ↓
Use time-based validation
```

---

## Q8. What is the difference between rolling and expanding windows?

> A rolling window has a fixed size and moves through time, while an expanding window starts with an initial training period and continuously includes more historical observations.

---

## Q9. How do you handle outliers in time-series data?

> I first investigate whether the extreme observation represents an actual business event, data error, temporary anomaly, or structural change. I don't automatically remove it. Depending on the cause, I may keep it, transform it, cap it, flag it, or replace it.

---

## Q10. What features would you create for demand forecasting?

A good answer:

```text
Lag Features
    lag_1
    lag_7
    lag_14
    lag_28

Rolling Features
    rolling_mean_7
    rolling_mean_28
    rolling_std_7

Calendar
    day_of_week
    month
    quarter
    weekend

Business
    promotion
    price
    holiday

External
    weather
    events
```

---

# 73. Final Mental Model

```text
                 TIME SERIES DATA
                       │
                       ↓
                DateTime Handling
                       │
                       ↓
                Frequency Check
                       │
                       ↓
              Missing Timestamps
                       │
                       ↓
               Missing Values
                       │
                       ↓
                  Outliers
                       │
                       ↓
             Trend / Seasonality
                       │
                       ↓
             Transformation
                       │
                       ↓
              Feature Engineering
                       │
        ┌──────────────┼──────────────┐
        ↓              ↓              ↓
      Lags          Rolling       Calendar
        │              │              │
        └──────────────┼──────────────┘
                       ↓
                 Target Creation
                       │
                       ↓
              Temporal Split
                       │
                       ↓
             Leakage Prevention
                       │
                       ↓
                    MODEL
```
