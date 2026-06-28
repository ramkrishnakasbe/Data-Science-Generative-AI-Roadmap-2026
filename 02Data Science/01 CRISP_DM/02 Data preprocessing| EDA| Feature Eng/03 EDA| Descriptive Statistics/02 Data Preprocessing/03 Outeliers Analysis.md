# 03. Outlier Analysis

# Overview

Outlier Analysis is the process of identifying and handling observations that are significantly different from the majority of the data.

Outliers may occur due to:

* Data entry errors
* Measurement errors
* Sampling errors
* Natural variation
* Fraudulent activities
* Rare events

Proper outlier treatment improves data quality and model performance.

---

# Why Outlier Analysis?

Outliers can:

* Distort statistical measures
* Affect the mean and standard deviation
* Reduce machine learning model accuracy
* Influence regression models significantly
* Produce misleading insights

However, not all outliers are bad. Some may contain valuable business information.

---

# What is an Outlier?

An outlier is an observation that lies unusually far away from the rest of the data.

### Example

```text id="4ld1vb"
Marks

45
48
52
50
47
49
51
250
```

Here, **250** is an outlier.

---

# Common Methods for Detecting Outliers

## Graphical Methods

* Box Plot
* Scatter Plot
* Histogram
* Density Plot

---

## Statistical Methods

* IQR (Interquartile Range)
* Z-Score
* Modified Z-Score (MAD)
* Percentile / Quantile Method

---

# 3R Technique

After detecting outliers, three common approaches are used.

---

## 1. Rectify

Rectify means correcting the outlier if it is caused by a data entry or measurement error.

### Example

Age recorded as:

```text id="gskm3v"
250
```

Actual value:

```text id="cnxtth"
25
```

The value should be corrected instead of removed.

---

## 2. Retain

Retain means keeping the outlier because it represents a genuine observation.

### Example

Luxury car prices:

```text id="m1n55y"
250000
300000
280000
5000000
```

The value **5,000,000** may represent a luxury sports car, so it should be retained.

---

## 3. Remove

Remove the outlier when it is clearly incorrect or negatively impacts analysis.

### Example

Employee Salary

```text id="ejdr0d"
35000
40000
45000
5000000
```

If **5,000,000** is due to a typing mistake, it should be removed.

---

# Masking

## Definition

Masking occurs when **actual outliers exist but fail to be detected** because other extreme values hide them.

This is a **False Negative** situation.

### Meaning

```text id="0nmkvh"
Outlier Exists
↓

Detection Method Fails
↓

Not Detected
```

### Example

Dataset

```text id="bjtwvv"
5
6
7
8
9
150
170
```

Because both extreme values influence the statistical calculations, one or both outliers may remain undetected.

---

# Swamping

## Definition

Swamping occurs when **normal observations are incorrectly identified as outliers**.

This is a **False Positive** situation.

### Meaning

```text id="7kktdb"
Normal Observation
↓

Detected as Outlier
```

### Example

Dataset

```text id="jlwm9y"
20
21
22
23
24
35
```

Due to extreme neighboring values or unsuitable thresholds, **35** may incorrectly be classified as an outlier.

---

# Winsorization

## Definition

Winsorization is an outlier treatment technique where extreme values are **replaced** instead of removed.

The observations remain in the dataset, but their values are capped at specified limits.

---

# Why Winsorization?

* Preserves dataset size
* Reduces effect of extreme values
* Improves model stability
* Prevents loss of information

---

# Winsorization Using IQR

## Step 1

Calculate:

```text id="4kk2na"
IQR = Q3 - Q1
```

## Step 2

Compute limits:

```text id="mujlwm"
Lower Limit = Q1 - 1.5 × IQR

Upper Limit = Q3 + 1.5 × IQR
```

## Step 3

Replace values outside the limits with the corresponding boundary values.

---

# Winsorization Using MAD

MAD stands for **Median Absolute Deviation**.

It is more robust than standard deviation because it is less affected by extreme values.

### Steps

1. Calculate Median
2. Compute absolute deviations
3. Calculate MAD
4. Replace values outside the acceptable range

Used when data contains many outliers.

---

# Winsorization Using Percentiles / Quantiles

Extreme values are capped using percentile limits.

Example:

```text id="gdb4ba"
Lower = 5th Percentile

Upper = 95th Percentile
```

Values:

```text id="rl55vs"
Below 5th Percentile
```

are replaced by the 5th percentile value.

Values:

```text id="hrv6ru"
Above 95th Percentile
```

are replaced by the 95th percentile value.

---

# Example of Winsorization

Original Data

```text id="jlwmt8"
10
12
15
18
20
200
```

After Winsorization

```text id="sb2hhx"
10
12
15
18
20
25
```

The extreme value **200** is replaced with the upper limit.

---

# Trimming

## Definition

Trimming removes observations that lie beyond specified limits.

Unlike Winsorization, the observations are completely deleted.

---

# Alpha (α) Trimming

Suppose:

```text id="9q12w6"
α = 5%
```

Then:

* Lowest 5% observations are removed.
* Highest 5% observations are removed.

Total removed observations:

```text id="g8jlsj"
10%
```

---

# Example

Original Data

```text id="jlwmq3"
5
7
8
10
12
15
18
20
150
```

After 5% trimming

```text id="ijyffr"
7
8
10
12
15
18
20
```

The extreme observations are removed.

---

# Trimming vs Winsorization

| Feature           | Trimming       | Winsorization           |
| ----------------- | -------------- | ----------------------- |
| Outliers          | Removed        | Replaced                |
| Number of Records | Decreases      | Remains Same            |
| Information Loss  | Higher         | Lower                   |
| Suitable For      | Large Datasets | Small & Medium Datasets |
| Extreme Values    | Deleted        | Capped                  |

---

# Choosing the Right Method

| Situation                | Recommended Technique |
| ------------------------ | --------------------- |
| Data Entry Error         | Rectify               |
| Genuine Rare Observation | Retain                |
| Incorrect Observation    | Remove                |
| Preserve Dataset Size    | Winsorization         |
| Very Large Dataset       | Trimming              |

---

# Advantages of Outlier Analysis

* Improves model performance
* Reduces statistical bias
* Produces reliable insights
* Improves regression models
* Enhances data quality

---

# Disadvantages

* Genuine observations may be removed
* Incorrect thresholds may misclassify data
* Different detection methods may produce different results
* Domain knowledge is often required

---

# Real-World Applications

## Banking

Detect fraudulent transactions.

---

## Healthcare

Identify abnormal patient readings.

---

## Manufacturing

Detect defective products.

---

## Retail

Identify unusual purchasing behavior.

---

## Finance

Detect stock market anomalies.

---

# Summary

Outlier Analysis is an essential preprocessing step used to detect and treat extreme observations. Once identified, outliers can be **Rectified**, **Retained**, or **Removed** using the **3R Technique**. Incorrect detection can lead to **Masking (False Negative)** or **Swamping (False Positive)**. Common treatment methods include **Winsorization**, which replaces extreme values using **IQR**, **MAD**, or **Percentiles**, and **Trimming**, which removes extreme observations. The choice of method depends on the nature of the data, business requirements, and the machine learning model being used.
