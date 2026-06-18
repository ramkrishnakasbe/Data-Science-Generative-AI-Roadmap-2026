# Data Understanding

## What is Data Understanding?

Data Understanding is the process of examining, exploring, and understanding available data before performing cleaning, transformation, or machine learning.

The goal is to answer:

- What data do we have?
- What type of data is it?
- Is the data useful?
- Is the data reliable?
- Are there quality issues?
- Is additional data required?

---

# Data Types

Understanding data types is one of the most important skills in Data Science.

---

## Continuous Data

Continuous data can take any value within a range.

### Examples

- Height = 175.5 cm
- Weight = 68.2 kg
- Temperature = 36.7°C
- Salary = ₹57,845.50

### Characteristics

- Infinite possible values
- Decimal values allowed
- Measured, not counted

---

## Discrete Data

Discrete data consists of countable values.

### Examples

- Number of Employees
- Number of Customers
- Number of Cars
- Number of Defects

### Characteristics

- Countable
- Whole numbers
- No fractions

---

## Qualitative vs Quantitative Data

### Qualitative Data

Categorical information.

#### Examples

- Gender
- City
- Product Category
- Color

### Quantitative Data

Numerical information.

#### Examples

- Age
- Salary
- Revenue
- Weight

| Qualitative | Quantitative |
|------------|------------|
| Categories | Numbers |
| Non-numeric | Numeric |
| Descriptive | Measurable |

---

## Structured vs Semi-Structured vs Unstructured Data

### Structured Data

Stored in rows and columns.

#### Examples

- SQL Databases
- Excel Files
- CSV Files

| Employee_ID | Name | Salary |
|------------|------|--------|
| 101 | Ram | 50000 |

---

### Semi-Structured Data

Has partial structure.

#### Examples

- JSON
- XML
- Log Files

Example:

```json
{
  "name":"Ram",
  "salary":50000
}
```

---

### Unstructured Data

No predefined format.

#### Examples

- Images
- Audio
- Video
- Emails
- Documents
- Social Media Posts

---

## Big Data vs Non-Big Data

### Non-Big Data

Traditional datasets manageable by a single machine.

Examples:

- Excel Dataset
- Customer Records
- Employee Database

---

### Big Data

Extremely large datasets.

Examples:

- Facebook Data
- YouTube Videos
- Amazon Transactions

### 5 V's of Big Data

- Volume
- Velocity
- Variety
- Veracity
- Value

---

## Cross-Sectional vs Time Series vs Longitudinal Data

### Cross-Sectional Data

Collected at one point in time.

Example:

Employee salaries in 2025.

| Employee | Salary |
|----------|--------|
| A | 50000 |
| B | 60000 |

---

### Time Series Data

Collected over time.

Example:

Monthly Sales.

| Month | Sales |
|--------|--------|
| Jan | 1000 |
| Feb | 1200 |

---

### Longitudinal / Panel Data

Same subjects observed repeatedly over time.

| Employee | Year | Salary |
|----------|------|--------|
| A | 2023 | 50000 |
| A | 2024 | 55000 |
| A | 2025 | 60000 |

---

## Balanced vs Imbalanced Data

### Balanced Data

Target classes are nearly equal.

Example:

| Class | Count |
|---------|---------|
| Yes | 500 |
| No | 500 |

---

### Imbalanced Data

One class dominates.

Example:

Fraud Detection

| Class | Count |
|---------|---------|
| Fraud | 100 |
| Non-Fraud | 10000 |

### Problems

- Model becomes biased
- Poor minority prediction

### Solutions

- SMOTE
- Oversampling
- Undersampling
- Class Weights

---

## Rare Events Data

Events occurring very infrequently.

Examples:

- Fraud Transactions
- Disease Detection
- Equipment Failure

---

## Offline (Batch) Data vs Live Streaming Data

### Offline / Batch Data

Processed at scheduled intervals.

Examples:

- Daily Sales Report
- Monthly Revenue Data

---

### Live Streaming Data

Processed continuously in real time.

Examples:

- Stock Market Prices
- IoT Sensor Data
- UPI Transactions
- Uber Location Tracking

---

# Data Collection

## What is Data Collection?

Process of gathering data from different sources.

### Internal Sources

- CRM
- ERP
- Databases

### External Sources

- APIs
- Government Data
- Kaggle
- Web Scraping

---

# Exploratory Data Analysis (EDA)

## What is EDA?

Process of exploring datasets before model building.

Purpose:

- Understand patterns
- Detect outliers
- Find missing values
- Generate insights

---

## Descriptive Statistics

### Central Tendency

- Mean
- Median
- Mode

### Dispersion

- Range
- Variance
- Standard Deviation

### Shape

- Skewness
- Kurtosis

---

# Key Takeaways

- Understand the data before cleaning it.
- Identify data types correctly.
- Detect imbalance and quality issues early.
- Perform EDA before model building.
- Good models start with good data understanding.
