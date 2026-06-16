
# Exploratory Data Analysis (EDA) / Descriptive Analysis

## What is EDA?

Exploratory Data Analysis (EDA) is the process of understanding, summarizing, visualizing, and investigating data before applying statistical models or machine learning algorithms.

EDA helps answer questions such as:

- What does the data look like?
- Are there missing values?
- Are there outliers?
- What patterns exist in the data?
- Which variables are important?
- Are there relationships between variables?

EDA is often considered the most important phase of a Data Science project because it helps uncover hidden insights and data quality issues.

---

# Why EDA is Important

EDA helps to:

- Understand the dataset
- Identify data quality issues
- Detect missing values
- Detect outliers
- Understand feature distributions
- Discover patterns and trends
- Validate business assumptions
- Improve feature engineering
- Improve model performance

---

# EDA Roadmap

```text
EDA / Descriptive Analysis
│
├── 1. Data Understanding
│
├── 2. Data Profiling
│
├── 3. Descriptive Statistics
│
├── 4. Missing Value Analysis
│
├── 5. Duplicate Data Analysis
│
├── 6. Outlier Analysis
│
├── 7. Univariate Analysis
│
├── 8. Bivariate Analysis
│
├── 9. Multivariate Analysis
│
├── 10. Correlation Analysis
│
├── 11. Distribution Analysis
│
├── 12. Feature Relationships
│
├── 13. Data Visualization
│
└── 14. Business Insights
```

---

# Topics Covered

## 1. Data Understanding

Understanding:

- Dataset structure
- Number of rows
- Number of columns
- Feature names
- Target variable
- Data types

---

## 2. Data Profiling

Creating a summary of the dataset.

Includes:

- Total records
- Missing values
- Unique values
- Data types
- Summary statistics

---

## 3. Descriptive Statistics

Summarizing data using statistics.

Examples:

- Mean
- Median
- Mode
- Range
- Variance
- Standard Deviation
- Quartiles
- Percentiles

---

## 4. Missing Value Analysis

Finding:

- Missing records
- Null values
- Empty values

Understanding:

- Why values are missing
- Impact on analysis

---

## 5. Duplicate Analysis

Checking:

- Duplicate rows
- Duplicate records

Purpose:

- Improve data quality
- Avoid biased analysis

---

## 6. Outlier Analysis

Identifying unusual observations.

Examples:

- Extremely high salary
- Abnormally large transaction

Common Techniques:

- IQR Method
- Z-Score Method
- Box Plot

---

## 7. Univariate Analysis

Analyzing one variable at a time.

Examples:

- Age Distribution
- Salary Distribution
- Customer Count

Common Visualizations:

- Histogram
- Bar Chart
- Pie Chart
- Density Plot

---

## 8. Bivariate Analysis

Analyzing relationships between two variables.

Examples:

- Salary vs Experience
- Sales vs Advertising

Common Visualizations:

- Scatter Plot
- Grouped Bar Chart
- Correlation Matrix

---

## 9. Multivariate Analysis

Analyzing more than two variables simultaneously.

Examples:

- Salary vs Experience vs Education
- Sales vs Marketing vs Region

---

## 10. Correlation Analysis

Measures relationships between numerical variables.

Questions:

- Does Salary increase with Experience?
- Does Advertising impact Sales?

Common Methods:

- Pearson Correlation
- Spearman Correlation

---

## 11. Distribution Analysis

Understanding how data is distributed.

Examples:

- Normal Distribution
- Skewed Distribution
- Uniform Distribution

Important for:

- Statistical Analysis
- Machine Learning Assumptions

---

## 12. Feature Relationships

Understanding interactions among variables.

Examples:

- Customer Age and Spending
- Experience and Salary

---

## 13. Data Visualization

Graphical representation of data.

Common Charts:

- Histogram
- Bar Chart
- Pie Chart
- Box Plot
- Scatter Plot
- Line Chart
- Heatmap

---

## 14. Business Insights

Final objective of EDA.

Convert findings into actionable insights.

Example:

```text
Customers aged 25-35
generate 60% of revenue.
```

---

# EDA Deliverables

After EDA, you should have:

- Dataset Summary
- Data Quality Report
- Missing Value Report
- Outlier Report
- Correlation Report
- Visualizations
- Business Insights
- Recommendations

---

# Real-World Example

## Employee Attrition Project

### During EDA

Investigate:

- Employee Age
- Salary
- Experience
- Department
- Attrition Status

### Findings

- Younger employees leave more frequently
- Low salary employees have higher attrition
- Certain departments show high turnover

### Business Insight

Improve retention programs for high-risk employees.

---

# Learning Outcome

After completing EDA, you should be able to:

- Understand any dataset quickly
- Identify data quality issues
- Detect outliers and anomalies
- Analyze distributions
- Study feature relationships
- Generate business insights
- Prepare data for Machine Learning

---

# Folder Structure

```text
04_EDA
│
├── README.md
│
├── 01_Data_Understanding.md
├── 02_Data_Profiling.md
├── 03_Descriptive_Statistics.md
├── 04_Missing_Value_Analysis.md
├── 05_Duplicate_Analysis.md
├── 06_Outlier_Analysis.md
├── 07_Univariate_Analysis.md
├── 08_Bivariate_Analysis.md
├── 09_Multivariate_Analysis.md
├── 10_Correlation_Analysis.md
├── 11_Distribution_Analysis.md
├── 12_Data_Visualization.md
└── 13_Business_Insights.md
```

---

# Key Takeaways

- EDA is the heart of Data Science.
- Most business insights come from EDA.
- Always perform EDA before Machine Learning.
- EDA helps identify data quality issues.
- Visualization is a critical part of EDA.
- Good EDA leads to better models and better decisions.
