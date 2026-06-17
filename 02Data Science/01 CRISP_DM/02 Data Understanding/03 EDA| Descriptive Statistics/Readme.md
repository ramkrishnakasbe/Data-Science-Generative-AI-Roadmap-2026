# EDA Roadmap

```text
EDA / Descriptive Analysis
│
├── 1. First Moment Business
│   ├── Mean
│   ├── Median
│   └── Mode
│
├── 2. Second Moment Business
│   ├── Variance
│   ├── Standard Deviation
│   └── Range
│
├── 3. Third Moment Business
│   └── Skewness
│
├── 4. Fourth Moment Business
│   └── Kurtosis
│
├── 5. Graphical Representation
│   │
│   ├── 5.1 Univariate Analysis
│   │   ├── Histogram
│   │   ├── Density Plot (KDE)
│   │   ├── Box Plot
│   │   ├── Violin Plot
│   │   ├── Bar Chart
│   │   └── Pie Chart
│   │
│   ├── 5.2 Bivariate Analysis
│   │   ├── Scatter Plot
│   │   ├── Grouped Bar Chart
│   │   ├── Stacked Bar Chart
│   │   ├── Line Plot
│   │   ├── Box Plot by Category
│   │   └── Correlation Plot
│   │
│   └── 5.3 Multivariate Analysis
│       ├── Pair Plot
│       ├── Heatmap
│       ├── Bubble Plot
│       ├── 3D Scatter Plot
│       ├── Parallel Coordinates Plot
│       └── Cluster Visualization
│
├── 6. Auto EDA
│   ├── Pandas Profiling
│   ├── Sweetviz
│   ├── AutoViz
│   └── DTale
│
└── 7. Key Documents
    │
    ├── 7.1 Business Insights
    └── 7.2 Statistical Insights
```

---

# 5. Graphical Representation

Graphical Representation helps visualize data patterns, distributions, trends, relationships, and anomalies.

---

## 5.1 Univariate Analysis

### Definition

Analysis of a single variable.

### Objective

- Understand distribution
- Identify outliers
- Check skewness
- Study frequency patterns

### Common Charts

- Histogram
- Density Plot (KDE)
- Box Plot
- Violin Plot
- Bar Chart
- Pie Chart

### Example

```text
Salary Distribution
```

Analyze only one column:

```text
Salary
```

---

## 5.2 Bivariate Analysis

### Definition

Analysis of two variables simultaneously.

### Objective

- Identify relationships
- Compare groups
- Measure correlation
- Study dependency

### Common Charts

- Scatter Plot
- Grouped Bar Chart
- Stacked Bar Chart
- Line Plot
- Box Plot by Category
- Correlation Plot

### Example

```text
Salary vs Experience
```

Variables:

```text
Salary
Experience
```

---

## 5.3 Multivariate Analysis

### Definition

Analysis involving three or more variables.

### Objective

- Discover complex relationships
- Feature interaction analysis
- Pattern identification
- Segment discovery

### Common Charts

- Pair Plot
- Heatmap
- Bubble Plot
- 3D Scatter Plot
- Parallel Coordinates Plot
- Cluster Visualization

### Example

```text
Salary vs Experience vs Education
```

Variables:

```text
Salary
Experience
Education
```

---

# 7. Key Documents

## 7.1 Business Insights

Business-focused findings generated from EDA.

Examples:

- Customers aged 25–35 generate the highest revenue.
- Employee attrition is highest in the Sales department.
- Premium customers contribute 70% of profits.

---

## 7.2 Statistical Insights

Data-driven findings generated using statistical analysis.

Examples:

- Salary is positively skewed.
- Experience and Salary have a correlation of 0.82.
- Dataset contains 4.5% missing values.
- Kurtosis indicates presence of extreme outliers.
