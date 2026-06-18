# UNIVARIATE ANALYSIS - GRAPHICAL REPRESENTATION (DETAILED STUDY NOTES)

---

# 1. INTRODUCTION

Univariate analysis studies **one variable at a time** using graphs and statistics.

It helps in understanding:
- Distribution
- Outliers
- Patterns
- Skewness
- Data type behavior

It is the **foundation of Exploratory Data Analysis (EDA)**.

---

# 2. HISTOGRAM

## 📌 Purpose
Used to understand the **distribution of numerical data**.

## 📊 Example Graph Representation
- Age distribution of employees
- Salary distribution in a company

## 📈 What it shows
- Frequency of data
- Shape of distribution
- Skewness

## 🔍 Interpretation
- Bell shaped → Normal distribution
- Right skew → long right tail
- Left skew → long left tail

## 📌 Use Case
- Understanding salary distribution
- Customer age distribution

## 🎯 Interview Questions
- What is histogram used for?
- Difference between histogram and bar chart?
- What does bin mean in histogram?

---

# 3. BAR PLOT

## 📌 Purpose
Used for **categorical data comparison**.

## 📊 Example Graph Representation
- Gender distribution
- Product category sales

## 📈 What it shows
- Count of categories
- Comparison between groups

## 🔍 Interpretation
- Taller bar = higher frequency
- Helps ranking categories

## 📌 Use Case
- Top selling products
- City-wise customer count

## 🎯 Interview Questions
- Difference between bar chart and histogram?
- When do we use bar plot?
- Can bar chart show numerical data?

---

# 4. DENSITY PLOT (KDE)

## 📌 Purpose
Smooth version of histogram showing probability distribution.

## 📊 Example Graph Representation
- Age distribution curve
- Salary distribution smooth curve

## 📈 What it shows
- Density of data
- Peaks and concentration

## 🔍 Interpretation
- High peak = high concentration
- Flat curve = uniform distribution

## 📌 Use Case
- Comparing distributions
- Checking normality

## 🎯 Interview Questions
- Difference between histogram and KDE?
- Why KDE is used?
- What smoothing means in KDE?

---

# 5. BOX PLOT

## 📌 Purpose
Used to detect **outliers and spread of data**.

## 📊 Example Graph Representation
- Salary boxplot showing outliers
- Age distribution spread

## 📈 What it shows
- Median
- Quartiles (Q1, Q3)
- IQR
- Outliers

## 🔍 Interpretation
- Points outside whiskers = outliers
- Wide box = high variation

## 📌 Use Case
- Detect salary anomalies
- Identify extreme values in data

## 🎯 Interview Questions
- What is IQR?
- How do you detect outliers using boxplot?
- What are whiskers in boxplot?

---

# 6. Q-Q PLOT

## 📌 Purpose
Used to check **normal distribution assumption**.

## 📊 Example Graph Representation
- Checking if salary data is normally distributed

## 📈 What it shows
- Data quantiles vs theoretical quantiles

## 🔍 Interpretation
- Straight line → Normal distribution
- Curve → Not normal

## 📌 Use Case
- Statistical modeling assumption check

## 🎯 Interview Questions
- What is Q-Q plot used for?
- How do you check normality?
- What happens if points deviate from line?

---

# 7. STRIP PLOT

## 📌 Purpose
Shows **individual data points distribution**.

## 📊 Example Graph Representation
- Salary per department
- Age per gender

## 📈 What it shows
- Spread of data points
- Clusters

## 🔍 Interpretation
- Dense area = more values
- Spread = variation

## 📌 Use Case
- Small datasets visualization
- Category-wise distribution

## 🎯 Interview Questions
- What is strip plot?
- Difference between strip plot and box plot?
- When to use strip plot?

---

# 8. CANDLE (OHLC) PLOT

## 📌 Purpose
Used in **financial data analysis**.

## 📊 Example Graph Representation
- Stock price movement

## 📈 What it shows
- Open price
- High price
- Low price
- Close price

## 🔍 Interpretation
- Green candle → price increase
- Red candle → price decrease

## 📌 Use Case
- Stock market analysis
- Trading patterns

## 🎯 Interview Questions
- What does OHLC mean?
- Why candle chart is used in finance?
- What does green/red candle indicate?

---

# 9. TIME SERIES PLOT

## 📌 Purpose
Used to analyze **data over time**.

## 📊 Example Graph Representation
- Monthly sales trend
- Temperature over time

## 📈 What it shows
- Trend
- Seasonality
- Pattern changes

## 🔍 Interpretation
- Upward trend → growth
- Downward trend → decline

## 📌 Use Case
- Sales forecasting
- Weather analysis

## 🎯 Interview Questions
- What is time series data?
- Difference between time series and normal data?
- What is seasonality?

---

# 10. PIE CHART

## 📌 Purpose
Shows **percentage distribution of categories**.

## 📊 Example Graph Representation
- Market share
- Gender distribution

## 📈 What it shows
- Part-to-whole relationship

## 🔍 Interpretation
- Larger slice = higher proportion

## 📌 Use Case
- Business revenue breakdown
- Market share analysis

## 🎯 Interview Questions
- When should you not use pie chart?
- Difference between pie chart and bar chart?
- Why pie chart is limited?

---

# 11. SUMMARY TABLE

| Graph | Type | Purpose |
|------|------|--------|
| Histogram | Numerical | Distribution |
| Bar Plot | Categorical | Comparison |
| KDE | Numerical | Smooth distribution |
| Box Plot | Numerical | Outliers |
| Q-Q Plot | Numerical | Normality check |
| Strip Plot | Both | Data points |
| Candle Plot | Time/Finance | OHLC movement |
| Time Series | Time | Trend analysis |
| Pie Chart | Categorical | Percentage |

---

# 12. FINAL CONCLUSION

Univariate graphical analysis is essential for:

- Understanding data distribution
- Detecting outliers
- Checking normality
- Identifying patterns
- Preparing data for ML models

It is the **first and most important step in EDA**.
