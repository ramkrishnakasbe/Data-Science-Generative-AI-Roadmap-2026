# Data Types

## Mind Map

```text
Data Types
│
├── Continuous Data
│   │
│   ├── Ratio Scale
│   │   └── Most Preferred Scale
│   │
│   ├── Decimal Values Allowed
│   │
│   ├── Infinite Possibilities
│   │
│   └── Examples
│       ├── Height
│       ├── Weight
│       ├── Age
│       ├── Salary
│       ├── Revenue
│       └── Temperature
│
└── Discrete Data
    │
    ├── Count Data
    │
    ├── Finite Values
    │
    ├── Decimal Values Not Meaningful
    │
    └── Categorical Data
        │
        ├── Binary
        │   ├── Yes / No
        │   ├── True / False
        │   ├── Fraud / Non-Fraud
        │   └── Pass / Fail
        │
        └── Multiple Categories
            │
            ├── Nominal
            │   ├── Country
            │   ├── Blood Group
            │   ├── Product Category
            │   └── City
            │
            └── Ordinal
                ├── Poor
                ├── Average
                ├── Good
                ├── Excellent
                └── Education Levels
```

---

# Introduction

Data is the foundation of Data Science, Machine Learning, Artificial Intelligence, Business Analytics, and Statistics.

Before performing:

* Data Cleaning
* Data Analysis
* Data Visualization
* Feature Engineering
* Machine Learning

we must first understand the nature and type of data.

Different data types require different preprocessing techniques, statistical methods, visualizations, and machine learning algorithms.

---

# What is Data?

Data refers to raw facts, measurements, observations, or information collected from various sources.

Examples:

| Customer_ID | Name | Age | Salary |
| ----------- | ---- | --- | ------ |
| 101         | Ram  | 28  | 50000  |
| 102         | John | 32  | 70000  |

In Data Science, every column is considered a variable (feature).

---

# Classification of Data

Data can be broadly classified into:

```text
Data
│
├── Continuous Data
│
└── Discrete Data
    │
    └── Categorical Data
        │
        ├── Binary
        ├── Nominal
        └── Ordinal
```

---

# Continuous Data

## Definition

Continuous data represents measurements that can take any value within a range.

The values are not restricted to whole numbers.

Continuous data can contain decimal points and fractions.

---

## Characteristics

* Measured rather than counted
* Infinite possible values
* Supports arithmetic operations
* Usually numerical
* Most statistical techniques work best with continuous data

---

## Examples

### Height

```text
170.5 cm
171.8 cm
172.35 cm
```

### Weight

```text
65.2 kg
72.45 kg
85.12 kg
```

### Salary

```text
₹55,000.50
₹87,350.75
```

### Revenue

```text
₹15,67,845.75
```

### Temperature

```text
36.7°C
37.2°C
```

---

## Why Continuous Data is Important

Most Machine Learning algorithms perform better when features are continuous.

Examples:

* Linear Regression
* Logistic Regression
* Random Forest
* XGBoost
* Neural Networks

---

# Ratio Scale

The screenshot specifically highlights Ratio Scale under Continuous Data.

---

## Definition

Ratio Scale is the highest level of measurement.

It contains:

* Order
* Equal Intervals
* True Zero

---

## Examples

| Feature  | Ratio Scale |
| -------- | ----------- |
| Height   | Yes         |
| Weight   | Yes         |
| Salary   | Yes         |
| Revenue  | Yes         |
| Distance | Yes         |
| Age      | Yes         |

---

## Why Ratio Scale is Preferred

All mathematical operations are valid.

### Addition

```text
50 + 100 = 150
```

### Subtraction

```text
100 - 50 = 50
```

### Multiplication

```text
50 × 2 = 100
```

### Division

```text
100 / 50 = 2
```

---

## True Zero

A true zero means complete absence.

Examples:

```text
0 kg weight
0 revenue
0 distance
```

Because of true zero:

```text
100kg is twice 50kg
```

This statement is mathematically correct.

---

## Why Data Scientists Prefer Ratio Scale

Supports:

* Mean
* Median
* Mode
* Standard Deviation
* Variance
* Correlation
* Regression
* Hypothesis Testing
* Machine Learning Algorithms

---

# Infinite Possibilities

Continuous variables have infinite possible values.

Example:

Between:

```text
10 and 11
```

We have:

```text
10.1
10.01
10.001
10.0001
```

and infinitely more values.

---

# Discrete Data

## Definition

Discrete data represents countable quantities.

Values occur as distinct, separate numbers.

Usually represented using whole numbers.

---

## Characteristics

* Counted not measured
* Finite values
* Usually integers
* Decimal values generally do not make practical sense

---

## Examples

### Number of Employees

```text
10
20
100
```

Not:

```text
10.5 Employees
```

---

### Number of Cars

```text
5 Cars
15 Cars
```

---

### Number of Orders

```text
100 Orders
250 Orders
```

---

### Number of Students

```text
35 Students
```

---

# Count Data

Discrete data is often called Count Data.

Examples:

* Number of Customers
* Number of Orders
* Number of Employees
* Number of Transactions
* Number of Products

---

# Finite Values

Unlike continuous data, discrete data has limited possible outcomes.

Example:

Number of children in a family:

```text
0
1
2
3
4
5
```

Not:

```text
2.5 children
```

---

# Categorical Data

Categorical Data represents labels or groups.

It answers:

```text
Which Category?
```

instead of:

```text
How Much?
```

---

# Binary Data

Binary Data contains only two possible outcomes.

---

## Examples

### Gender

```text
Male
Female
```

---

### Fraud Detection

```text
Fraud
Not Fraud
```

---

### Medical Diagnosis

```text
Disease
No Disease
```

---

### Student Result

```text
Pass
Fail
```

---

# Nominal Data

## Definition

Nominal data consists of categories without any order.

---

## Examples

### Country

```text
India
USA
Canada
Australia
```

---

### Blood Group

```text
A
B
AB
O
```

---

### Product Category

```text
Electronics
Fashion
Food
Books
```

---

## Characteristics

* No ranking
* No order
* Purely labels

---

## Machine Learning Handling

Common Encoding:

* One Hot Encoding
* Label Encoding

---

# Ordinal Data

## Definition

Ordinal data consists of categories with meaningful order.

---

## Examples

### Customer Satisfaction

```text
Poor
Average
Good
Excellent
```

---

### Education Level

```text
High School
Bachelor's
Master's
PhD
```

---

### Salary Band

```text
Low
Medium
High
```

---

## Characteristics

* Order exists
* Distance between categories unknown

Example:

```text
Excellent > Good > Average > Poor
```

But we do not know how much better.

---

# Nominal vs Ordinal

| Feature                 | Nominal        | Ordinal             |
| ----------------------- | -------------- | ------------------- |
| Order                   | No             | Yes                 |
| Ranking                 | No             | Yes                 |
| Example                 | Country        | Satisfaction Rating |
| Mathematical Difference | Not Meaningful | Not Meaningful      |

---

# Continuous vs Discrete

| Feature        | Continuous | Discrete           |
| -------------- | ---------- | ------------------ |
| Nature         | Measured   | Counted            |
| Values         | Infinite   | Finite             |
| Decimal Values | Allowed    | Not Meaningful     |
| Example        | Height     | Number of Students |
| Example        | Salary     | Number of Orders   |

---

# Real Data Science Examples

## Customer Churn Dataset

Continuous:

* Age
* Salary
* Account Balance

Categorical:

* Gender
* Geography

Binary:

* Churn
* Not Churn

---

## Employee Attrition Dataset

Continuous:

* Monthly Income
* Age

Categorical:

* Department
* Job Role

Binary:

* Leave Company
* Stay Company

---

# Interview Questions

## What is Continuous Data?

Data that can take any value within a range and is usually measured.

---

## What is Discrete Data?

Data that consists of countable values.

---

## What is Binary Data?

Data having exactly two categories.

---

## Difference Between Nominal and Ordinal?

Nominal has no order.

Ordinal has order.

---

## Difference Between Continuous and Discrete Data?

Continuous is measured.

Discrete is counted.

---

## Why is Ratio Scale Most Preferred?

Because it supports all statistical and mathematical operations and contains a true zero.

---

## Is Age Continuous or Discrete?

Technically Continuous.

In business datasets it is often stored as Discrete.

---

## Is Salary Continuous?

Yes.

Salary can contain decimal values.

---

# Key Takeaways

✅ Continuous Data = Measured Values

✅ Discrete Data = Counted Values

✅ Binary Data = Two Categories

✅ Nominal Data = Categories Without Order

✅ Ordinal Data = Categories With Order

✅ Ratio Scale = Most Powerful Measurement Scale

✅ Understanding Data Types is the first step of Data Science, Statistics, Machine Learning, and AI
