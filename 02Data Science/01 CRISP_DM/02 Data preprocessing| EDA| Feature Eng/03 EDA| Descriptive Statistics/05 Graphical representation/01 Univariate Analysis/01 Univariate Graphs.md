# Univariate Graphs and Plots

## Overview

Univariate Analysis focuses on analyzing a single variable at a time. Graphs and plots help understand the distribution, spread, frequency, and patterns of the data.

---

# Numerical Data Visualizations

## 1. Histogram

### Definition

A Histogram displays the frequency distribution of numerical data by grouping values into intervals called bins.

### Purpose

* Understand data distribution
* Identify skewness
* Detect gaps and unusual patterns
* Check normality

### Example Use Case

Analyzing customer age distribution.

### Interpretation

* Bell-shaped → Normal Distribution
* Right Tail Longer → Positive Skew
* Left Tail Longer → Negative Skew

### Example Image

```md
![Histogram](images/histogram.png)
```

---

## 2. Box Plot

### Definition

A Box Plot summarizes data using quartiles and helps identify outliers.

### Components

* Minimum
* Q1 (25th Percentile)
* Median (50th Percentile)
* Q3 (75th Percentile)
* Maximum
* Outliers

### Purpose

* Detect outliers
* Understand spread
* Compare distributions

### Example Use Case

Analyzing salary distribution.

### Example Image

```md
![Box Plot](images/boxplot.png)
```

---

## 3. Density Plot (KDE Plot)

### Definition

A Density Plot provides a smooth representation of data distribution.

### Purpose

* Visualize distribution shape
* Compare multiple distributions
* Identify peaks and clusters

### Example Use Case

Studying exam score distribution.

### Example Image

```md
![Density Plot](images/density_plot.png)
```

---

## 4. Violin Plot

### Definition

A Violin Plot combines a Box Plot and Density Plot.

### Purpose

* Show distribution shape
* Display spread and central tendency
* Identify multimodal distributions

### Example Use Case

Comparing salary distributions across departments.

### Example Image

```md
![Violin Plot](images/violin_plot.png)
```

---

## 5. Frequency Distribution Plot

### Definition

Displays the frequency of observations across value ranges.

### Purpose

* Understand data concentration
* Identify common value ranges

### Example Use Case

Product sales distribution.

### Example Image

```md
![Frequency Distribution](images/frequency_distribution.png)
```

---

# Categorical Data Visualizations

## 6. Bar Chart

### Definition

A Bar Chart displays the count or frequency of categories using rectangular bars.

### Purpose

* Compare categories
* Identify dominant categories
* Understand category distribution

### Example Use Case

Number of customers by city.

### Example Image

```md
![Bar Chart](images/bar_chart.png)
```

---

## 7. Count Plot

### Definition

A Count Plot shows the frequency count of each category.

### Purpose

* Visualize category frequencies
* Detect class imbalance

### Example Use Case

Gender distribution.

### Example Image

```md
![Count Plot](images/count_plot.png)
```

---

## 8. Pie Chart

### Definition

A Pie Chart represents category proportions as slices of a circle.

### Purpose

* Show percentage contribution
* Visualize part-to-whole relationships

### Example Use Case

Market share analysis.

### Example Image

```md
![Pie Chart](images/pie_chart.png)
```

---

# Choosing the Right Plot

| Data Type   | Recommended Plots                              |
| ----------- | ---------------------------------------------- |
| Numerical   | Histogram, Box Plot, Density Plot, Violin Plot |
| Categorical | Bar Chart, Count Plot, Pie Chart               |

---

# Summary

Univariate visualizations help understand the characteristics of a single variable before moving to Bivariate or Multivariate Analysis. Selecting the correct plot depends on whether the variable is numerical or categorical and on the analytical objective.
