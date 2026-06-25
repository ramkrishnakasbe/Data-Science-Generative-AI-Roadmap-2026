# Multivariate Graphs and Plots

## Overview

Multivariate Analysis studies relationships among three or more variables simultaneously. It helps uncover complex patterns, interactions, and dependencies within data.

---

# Common Multivariate Visualizations

## 1. Pair Plot

### Definition

A Pair Plot displays pairwise relationships among multiple numerical variables.

### Purpose

* Explore relationships
* Detect trends
* Identify correlations
* Find outliers

### Example Use Case

Analyzing relationships among Age, Income, Spending Score, and Savings.

### Example Image

```md
![Pair Plot](images/pair_plot.png)
```

---

## 2. Correlation Heatmap

### Definition

A Heatmap showing correlation values among multiple numerical variables.

### Purpose

* Identify strong correlations
* Detect multicollinearity
* Support feature selection

### Example Use Case

Analyzing relationships among financial variables.

### Example Image

```md
![Correlation Heatmap](images/correlation_heatmap.png)
```

---

## 3. Bubble Chart

### Definition

A Scatter Plot where bubble size represents an additional variable.

### Purpose

* Analyze three variables simultaneously
* Visualize magnitude differences

### Example Use Case

Sales vs Profit with Customer Count as bubble size.

### Example Image

```md
![Bubble Chart](images/bubble_chart.png)
```

---

## 4. 3D Scatter Plot

### Definition

A Scatter Plot that displays three numerical variables in three-dimensional space.

### Purpose

* Visualize relationships among three variables
* Identify clusters and patterns

### Example Use Case

Age, Income, and Spending Score analysis.

### Example Image

```md
![3D Scatter Plot](images/3d_scatter_plot.png)
```

---

## 5. Parallel Coordinates Plot

### Definition

Displays multiple variables using parallel vertical axes.

### Purpose

* Compare observations across many variables
* Identify patterns and clusters

### Example Use Case

Customer segmentation analysis.

### Example Image

```md
![Parallel Coordinates Plot](images/parallel_coordinates.png)
```

---

## 6. Cluster Map

### Definition

Combines hierarchical clustering with a heatmap.

### Purpose

* Identify similar groups
* Discover hidden patterns

### Example Use Case

Customer behavior analysis.

### Example Image

```md
![Cluster Map](images/cluster_map.png)
```

---

## 7. Treemap

### Definition

Represents hierarchical data using nested rectangles.

### Purpose

* Visualize proportions
* Compare hierarchical categories

### Example Use Case

Revenue contribution by product categories.

### Example Image

```md
![Treemap](images/treemap.png)
```

---

## 8. PCA Visualization

### Definition

Visualizes high-dimensional data in two or three dimensions using Principal Component Analysis (PCA).

### Purpose

* Reduce dimensionality
* Visualize clusters
* Detect patterns

### Example Use Case

Machine Learning feature exploration.

### Example Image

```md
![PCA Plot](images/pca_plot.png)
```

---

# Choosing the Right Plot

| Objective                    | Recommended Plot              |
| ---------------------------- | ----------------------------- |
| Correlation Analysis         | Correlation Heatmap           |
| Multiple Relationships       | Pair Plot                     |
| Three Numerical Variables    | Bubble Chart, 3D Scatter Plot |
| High-Dimensional Data        | PCA Plot                      |
| Clustering Analysis          | Cluster Map                   |
| Hierarchical Data            | Treemap                       |
| Multiple Variable Comparison | Parallel Coordinates Plot     |

---

# Summary

Multivariate Analysis helps analyze interactions among multiple variables simultaneously. It is widely used in advanced EDA, feature engineering, dimensionality reduction, clustering, and machine learning workflows.
