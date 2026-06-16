# 01_Continuous_vs_Discrete_Data.md

# 1. Data Classification

```text
Data
│
├── 1. Numerical Data
│   │
│   ├── 1.1 Continuous Data
│   │   ├── 1.1.1 Interval Scale
│   │   └── 1.1.2 Ratio Scale
│   │
│   └── 1.2 Discrete Data
│       └── 1.2.1 Count Data
│
└── 2. Categorical Data
    │
    ├── 2.1 Binary Data
    │
    └── 2.2 Multiple Categories
         ├── 2.2.1 Nominal Data
         └── 2.2.2 Ordinal Data
```

---

# 1. Numerical Data

Numerical Data consists of values that can be measured or counted and can be used in mathematical calculations.

### Examples

* Age
* Height
* Weight
* Salary
* Number of Orders

---

# 1.1 Continuous Data

## Definition

Continuous Data can take any value within a given range.

These values are obtained through measurement.

### Examples

* Height
* Weight
* Temperature
* Distance
* Salary

### Characteristics

* Infinite possible values
* Decimal values allowed
* Measured rather than counted

---

# 1.1.1 Interval Scale

## Definition

Interval Data has equal intervals between values but no true zero.

### Examples

* Temperature (°C)
* Temperature (°F)
* IQ Score

### Characteristics

* Equal intervals
* No absolute zero
* Addition and subtraction are meaningful
* Ratios are not meaningful

### Example

```text
20°C - 10°C = 10°C ✔

20°C is twice 10°C ✘
```

---

# 1.1.2 Ratio Scale

## Definition

Ratio Data has equal intervals and a true zero value.

### Examples

* Age
* Height
* Weight
* Salary
* Distance

### Characteristics

* True zero exists
* All mathematical operations are valid
* Ratios are meaningful

### Example

```text
100 kg is twice 50 kg ✔

Salary ₹100,000 is twice ₹50,000 ✔
```

### Important Note

Ratio Scale is the most preferred scale in Statistics and Machine Learning.

---

# 1.2 Discrete Data

## Definition

Discrete Data contains countable numerical values.

These values usually appear as whole numbers.

### Examples

* Number of Students
* Number of Orders
* Number of Employees
* Number of Cars

### Characteristics

* Countable values
* Usually integers
* Finite or countably infinite values

---

# 1.2.1 Count Data

## Definition

Count Data is obtained by counting occurrences of an event.

### Examples

```text
Orders per Day = 50

Website Visits = 1000

Number of Customers = 350
```

### Characteristics

* Non-negative integers
* Cannot have fractions
* Common in Business Analytics

---

# 2. Categorical Data

## Definition

Categorical Data represents labels, classes, or groups.

### Examples

* Gender
* Country
* Department
* Product Category

### Characteristics

* Non-numeric meaning
* Used for classification
* Requires encoding for ML models

---

# 2.1 Binary Data

## Definition

Binary Data contains only two categories.

### Examples

```text
Yes / No

Pass / Fail

Fraud / Non-Fraud

True / False
```

---

# 2.2 Multiple Categories

Data containing more than two categories.

Examples:

* Country
* Education Level
* Product Category

---

# 2.2.1 Nominal Data

## Definition

Nominal Data consists of categories without any order.

### Examples

* Country
* Blood Group
* Color
* City

### Characteristics

* No ranking
* No order
* Categories only

---

# 2.2.2 Ordinal Data

## Definition

Ordinal Data consists of categories having meaningful order.

### Examples

```text
Low
Medium
High
```

```text
Poor
Average
Good
Excellent
```

```text
1 Star
2 Star
3 Star
4 Star
5 Star
```

### Characteristics

* Ordered categories
* Ranking exists
* Difference between ranks may not be equal

---

# 3. Summary Table

| Category    | Type                  | Examples           |
| ----------- | --------------------- | ------------------ |
| Numerical   | Continuous (Interval) | Temperature        |
| Numerical   | Continuous (Ratio)    | Salary             |
| Numerical   | Discrete (Count)      | Number of Students |
| Categorical | Binary                | Yes/No             |
| Categorical | Nominal               | Country            |
| Categorical | Ordinal               | Low/Medium/High    |

---

# 4. Top 10 Interview Questions & Answers

## Q1. What is the difference between Continuous and Discrete Data?

### Answer

| Continuous Data          | Discrete Data               |
| ------------------------ | --------------------------- |
| Measured                 | Counted                     |
| Decimal values allowed   | Whole numbers usually       |
| Infinite values possible | Countable values            |
| Example: Height          | Example: Number of Students |

---

## Q2. What is Continuous Data?

### Answer

Continuous Data can take any value within a range and is obtained through measurement.

Examples:

* Height
* Weight
* Salary
* Temperature

---

## Q3. What is Discrete Data?

### Answer

Discrete Data contains countable values and is obtained through counting.

Examples:

* Number of Employees
* Number of Orders
* Number of Customers

---

## Q4. What is the difference between Interval and Ratio Data?

### Answer

| Interval         | Ratio            |
| ---------------- | ---------------- |
| No true zero     | True zero exists |
| Ratios invalid   | Ratios valid     |
| Temperature (°C) | Weight           |
| IQ Score         | Salary           |

---

## Q5. Why is Ratio Scale preferred?

### Answer

Because:

* True zero exists
* Ratios are meaningful
* Supports all mathematical operations
* Widely used in Machine Learning and Statistics

---

## Q6. Is Temperature Interval or Ratio Data?

### Answer

Temperature in Celsius and Fahrenheit is Interval Data because zero does not represent the absence of temperature.

Temperature in Kelvin is Ratio Data because absolute zero exists.

---

## Q7. What is Count Data?

### Answer

Count Data is a type of Discrete Data obtained by counting events or objects.

Examples:

* Number of Orders
* Website Visits
* Customer Count

---

## Q8. Difference between Nominal and Ordinal Data?

### Answer

| Nominal     | Ordinal            |
| ----------- | ------------------ |
| No order    | Order exists       |
| Country     | Satisfaction Level |
| Color       | Ratings            |
| Blood Group | Education Level    |

---

## Q9. What is Binary Data?

### Answer

Binary Data contains only two categories.

Examples:

* Yes / No
* Fraud / Non-Fraud
* Pass / Fail

---

## Q10. Is Age Interval or Ratio Data?

### Answer

Age is Ratio Data.

Reason:

* True zero exists
* Ratios are meaningful

Example:

```text
40 years is twice 20 years
```

which is a valid comparison.

---

# Key Takeaways

* Data is broadly classified into Numerical and Categorical Data.
* Continuous Data is measured; Discrete Data is counted.
* Interval Scale has no true zero.
* Ratio Scale has a true zero and is most preferred.
* Binary, Nominal, and Ordinal are important types of Categorical Data.
* Understanding data types is essential before EDA, Feature Engineering, and Machine Learning.
