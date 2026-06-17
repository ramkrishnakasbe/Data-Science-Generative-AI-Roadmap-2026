# Exploratory Data Analysis (EDA) / Descriptive Analysis

## What is EDA?

Exploratory Data Analysis (EDA) is the process of understanding, summarizing, visualizing, and investigating data before applying statistical models or machine learning algorithms.

EDA helps discover:

- Patterns
- Trends
- Relationships
- Outliers
- Data Quality Issues
- Business Insights

EDA is one of the most important phases in Data Science because better understanding of data leads to better decisions and better models.

---

# Why EDA is Important

EDA helps to:

- Understand data characteristics
- Detect missing values
- Identify outliers
- Study distributions
- Understand relationships between variables
- Generate business insights
- Generate statistical insights
- Improve model performance

---

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

# 1. First Moment Business

## Definition

First Moment measures the central tendency of data.

It helps answer:

```text
What is the typical value in the dataset?
```

### Topics Covered

- Mean
- Median
- Mode

### Example

Employee Salaries:

```text
25000
30000
35000
40000
45000
```

Mean Salary:

```text
35000
```

### Business Usage

- Average Revenue
- Average Sales
- Average Salary
- Average Customer Spend

---

# 2. Second Moment Business

## Definition

Second Moment measures data variability or dispersion.

It helps answer:

```text
How spread out is the data?
```

### Topics Covered

- Variance
- Standard Deviation
- Range

### Example

Two classes may have the same average score but different variability.

### Business Usage

- Risk Analysis
- Demand Variability
- Revenue Stability
- Customer Spending Variation

---

# 3. Third Moment Business

## Definition

Third Moment measures asymmetry in the distribution.

### Topic Covered

- Skewness

It helps answer:

```text
Is data leaning left or right?
```

### Types

#### Positive Skew

```text
Long Tail →
```

Examples:

- Salary
- Income
- House Prices

---

#### Negative Skew

```text
← Long Tail
```

Examples:

- Easy Exam Scores

---

#### Symmetric Distribution

```text
Balanced Distribution
```

Examples:

- Normal Distribution

---

# 4. Fourth Moment Business

## Definition

Fourth Moment measures tail heaviness and peakedness.

### Topic Covered

- Kurtosis

It helps answer:

```text
Are extreme values present?
```

### Types

#### Mesokurtic

Normal Distribution

---

#### Leptokurtic

Heavy Tails

More Outliers

---

#### Platykurtic

Light Tails

Fewer Outliers

---

# 5. Graphical Representation

Visualization is used to understand patterns and relationships in data.

---

# 5.1 Univariate Analysis

## Definition

Analysis of a single variable.

### Objective

- Understand distribution
- Detect outliers
- Identify skewness
- Understand frequency

### Common Graphs

#### Histogram

Shows frequency distribution.

#### Density Plot (KDE)

Shows smooth distribution curve.

#### Box Plot

Shows:

- Median
- Quartiles
- Outliers

#### Violin Plot

Shows:

- Distribution
- Density

#### Bar Chart

Used for categorical variables.

#### Pie Chart

Shows category proportions.

### Example

```text
Salary Distribution
```

---

# 5.2 Bivariate Analysis

## Definition

Analysis involving two variables.

### Objective

- Study relationships
- Compare variables
- Measure dependency

### Common Graphs

#### Scatter Plot

Example:

```text
Experience vs Salary
```

---

#### Grouped Bar Chart

Compare categories.

Example:

```text
Department vs Attrition
```

---

#### Stacked Bar Chart

Shows composition.

---

#### Line Plot

Shows trend between two variables.

---

#### Box Plot by Category

Compare numerical distributions across groups.

---

#### Correlation Plot

Visualize strength of relationships.

---

### Example

```text
Salary vs Experience
```

---

# 5.3 Multivariate Analysis

## Definition

Analysis involving three or more variables.

### Objective

- Study complex relationships
- Feature interaction analysis
- Pattern identification

### Common Graphs

#### Pair Plot

Relationship among multiple variables.

---

#### Heatmap

Correlation matrix visualization.

---

#### Bubble Plot

Adds third variable using bubble size.

---

#### 3D Scatter Plot

Visualizes three numerical variables.

---

#### Parallel Coordinates Plot

Used for high-dimensional datasets.

---

#### Cluster Visualization

Used in clustering analysis.

---

### Example

```text
Salary
Experience
Education
```

Analyze all together.

---

# 6. Auto EDA

## Definition

Automated tools that generate EDA reports with minimal coding.

### Benefits

- Faster analysis
- Automated insights
- Data quality checks
- Visualization generation

---

## Popular Tools

### Pandas Profiling (YData Profiling)

Provides:

- Missing values
- Correlations
- Summary statistics

---

### Sweetviz

Provides:

- Visual reports
- Feature comparisons

---

### AutoViz

Creates charts automatically.

---

### DTale

Interactive browser-based EDA.

---

# 7. Key Documents

EDA findings are generally summarized into two major reports.

---

# 7.1 Business Insights

## Definition

Business-oriented findings that help stakeholders make decisions.

### Questions Answered

- What is happening?
- Why is it happening?
- What action should be taken?

### Examples

- Customers aged 25-35 contribute 60% of revenue.
- Sales increase during festive seasons.
- Premium customers generate highest profits.
- Employee attrition is highest in Sales department.

### Audience

- CEO
- Managers
- Business Teams
- Stakeholders

---

# 7.2 Statistical Insights

## Definition

Data-driven findings obtained using statistical techniques.

### Questions Answered

- What does the data tell us?
- How is the data distributed?
- Are variables correlated?

### Examples

- Salary distribution is positively skewed.
- Correlation between experience and salary is 0.82.
- Dataset contains 3.5% missing values.
- High kurtosis indicates extreme outliers.

### Audience

- Data Scientists
- Analysts
- ML Engineers

---

# Learning Outcome

After completing EDA, you should understand:

- Central Tendency
- Data Dispersion
- Skewness
- Kurtosis
- Data Visualization
- Univariate Analysis
- Bivariate Analysis
- Multivariate Analysis
- Auto EDA Tools
- Business Insights
- Statistical Insights

---

# Folder Structure

```text
04_EDA
│
├── README.md
│
├── 01_First_Moment_Business.md
├── 02_Second_Moment_Business.md
├── 03_Third_Moment_Business.md
├── 04_Fourth_Moment_Business.md
├── 05_Graphical_Representation.md
├── 06_Auto_EDA.md
├── 07_Business_Insights.md
└── 08_Statistical_Insights.md
```

---

# Key Takeaways

- EDA is the heart of Data Science.
- First Moment explains central tendency.
- Second Moment explains variability.
- Third Moment explains skewness.
- Fourth Moment explains kurtosis.
- Visualizations reveal hidden patterns.
- Auto EDA speeds up analysis.
- Business Insights drive decisions.
- Statistical Insights validate findings.
- EDA should always be performed before Machine Learning.
