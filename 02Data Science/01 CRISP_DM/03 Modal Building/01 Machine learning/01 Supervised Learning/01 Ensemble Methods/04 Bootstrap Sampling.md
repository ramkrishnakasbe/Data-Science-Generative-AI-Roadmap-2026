# Bootstrap Sampling

> **Level:** Beginner → Intermediate  
> **Prerequisites:** Statistics, Sampling Techniques, Ensemble Learning Basics  
> **Goal:** Understand Bootstrap Sampling, Sampling with Replacement, Out-of-Bag (OOB) Samples, and why Bootstrap is the foundation of Bagging and Random Forest.

---

# Table of Contents

1. Introduction
2. What is Sampling?
3. Why Sampling is Required?
4. Types of Sampling
5. What is Bootstrap Sampling?
6. Sampling with Replacement
7. Sampling without Replacement
8. Bootstrap vs Random Sampling
9. Bootstrap Algorithm
10. Mathematical Intuition
11. Probability of Selection
12. Out-of-Bag (OOB) Samples
13. Why Approximately 36.8% OOB?
14. Bootstrap in Bagging
15. Bootstrap in Random Forest
16. Advantages
17. Disadvantages
18. Applications
19. Python Implementation
20. Interview Questions
21. Summary

---

# 1. Introduction

Bootstrap Sampling is one of the most important concepts in Ensemble Learning.

Algorithms like

- Bagging
- Random Forest

cannot work without Bootstrap Sampling.

It is a statistical resampling technique that creates multiple datasets from a single dataset.

Each dataset is slightly different, allowing multiple models to learn different patterns.

---

# 2. What is Sampling?

## Definition

Sampling is the process of selecting a subset of observations from a larger dataset (population).

Instead of using the entire population, we work with a representative sample.

---

## Example

Population

```
100,000 Customers
```

Sample

```
10,000 Customers
```

Machine Learning models are usually trained on samples instead of the entire population.

---

# 3. Why Sampling is Required?

Using the complete dataset is not always practical.

Reasons include:

- Large datasets require more memory.
- Training takes longer.
- Computational cost increases.
- Some algorithms become slower.
- Sampling helps estimate population characteristics efficiently.

In Ensemble Learning, sampling also creates **diversity** among models.

---

# 4. Types of Sampling

There are several sampling techniques.

| Sampling Type | Replacement | Duplicate Records |
|---------------|-------------|-------------------|
| Random Sampling | No | No |
| Bootstrap Sampling | Yes | Yes |
| Stratified Sampling | Usually No | No |
| Systematic Sampling | No | No |
| Cluster Sampling | No | No |

For Ensemble Learning, **Bootstrap Sampling** is the most important.

---

# 5. What is Bootstrap Sampling?

## Definition

Bootstrap Sampling is a resampling technique in which observations are selected **randomly with replacement**.

The size of the bootstrap sample is generally equal to the size of the original dataset.

---

## Example

Original Dataset

```
A
B
C
D
E
```

Bootstrap Sample 1

```
A
B
B
D
E
```

Bootstrap Sample 2

```
C
A
C
D
D
```

Bootstrap Sample 3

```
E
A
B
E
C
```

Notice

- Some records appear multiple times.
- Some records are missing.

This is expected behavior.

---

# 6. Sampling with Replacement

Sampling with replacement means that after selecting an observation, it is placed back into the dataset before the next draw.

Therefore,

the same observation can be selected multiple times.

---

## Example

Original Dataset

```
1
2
3
4
5
```

Bootstrap Sample

```
2
5
2
1
4
```

Observation **2** appears twice.

Observation **3** does not appear at all.

---

## Characteristics

- Duplicate observations are allowed.
- Sample size remains the same.
- Every draw is independent.
- Creates different datasets.

---

# 7. Sampling without Replacement

In sampling without replacement,

once an observation is selected,

it cannot be selected again.

---

## Example

Original Dataset

```
1
2
3
4
5
```

Random Sample

```
2
5
1
4
3
```

Every observation appears exactly once.

---

## Characteristics

- No duplicate observations.
- Every record is unique.
- Used in traditional random sampling.

---

# 8. Bootstrap vs Random Sampling

| Feature | Bootstrap Sampling | Random Sampling |
|----------|-------------------|----------------|
| Replacement | Yes | No |
| Duplicate Records | Allowed | Not Allowed |
| Missing Records | Yes | No |
| Used in Bagging | Yes | No |
| Used in Random Forest | Yes | No |
| Sample Size | Usually Same as Original Dataset | Variable |

---

# 9. Bootstrap Algorithm

Step 1

Start with the original dataset.

↓

Step 2

Randomly select one observation.

↓

Step 3

Return it to the dataset.

↓

Step 4

Repeat until the bootstrap sample reaches the desired size.

↓

Step 5

Generate multiple bootstrap datasets.

---

## Workflow

```
Original Dataset

      │
      ▼

Bootstrap Sampling

      │
      ▼

Sample 1

Sample 2

Sample 3

Sample 4

...

Sample N

      │
      ▼

Train One Model Per Sample
```

---

# 10. Mathematical Intuition

Suppose the original dataset contains

```
N observations
```

Each bootstrap sample also contains

```
N observations
```

Each observation has a probability of

```
1/N
```

of being selected during one draw.

Since sampling is performed with replacement,

every draw is independent.

---

# 11. Probability of Selection

Probability that an observation is **selected** in one draw:

```
P(Selected)

=

1/N
```

Probability that an observation is **not selected** in one draw:

```
P(Not Selected)

=

1 - 1/N
```

Since we perform **N draws**, the probability that a particular observation is never selected is

```
(1 - 1/N)^N
```

As

```
N → ∞
```

```
(1 - 1/N)^N

≈ e^-1

≈ 0.368
```

---

# 12. Out-of-Bag (OOB) Samples

Some observations are never selected during Bootstrap Sampling.

These observations are called

> **Out-of-Bag (OOB) Samples**

---

## Example

Original Dataset

```
A
B
C
D
E
```

Bootstrap Sample

```
A
A
B
D
E
```

Observation

```
C
```

was never selected.

Therefore,

```
C

↓

Out-of-Bag Sample
```

---

# 13. Why Approximately 36.8% OOB?

For a dataset containing

```
N observations
```

approximately

```
63.2%
```

appear in a bootstrap sample.

The remaining

```
36.8%
```

are Out-of-Bag observations.

---

## Illustration

Suppose

```
1000 Records
```

Approximately

```
632 Records

↓

Selected
```

Approximately

```
368 Records

↓

OOB Samples
```

These OOB samples are used as a validation dataset.

---

# 14. Bootstrap in Bagging

Bagging follows these steps:

```
Original Dataset

↓

Bootstrap Sample 1

↓

Decision Tree 1

-------------------

Bootstrap Sample 2

↓

Decision Tree 2

-------------------

Bootstrap Sample 3

↓

Decision Tree 3

-------------------

Combine Predictions
```

Every model receives a different bootstrap sample.

This diversity improves performance.

---

# 15. Bootstrap in Random Forest

Random Forest extends Bagging by adding

**Random Feature Selection**.

Workflow

```
Original Dataset

↓

Bootstrap Sampling

↓

Random Feature Selection

↓

Decision Tree

↓

Repeat

↓

Majority Voting

↓

Final Prediction
```

Thus,

Random Forest =

```
Bootstrap Sampling

+

Random Feature Selection
```

---

# 16. Advantages

- Simple to implement.
- Creates diverse datasets.
- Reduces overfitting in ensemble models.
- Improves model stability.
- Works well for variance estimation.
- Enables Out-of-Bag validation.
- Supports parallel model training.
- Does not require additional data collection.

---

# 17. Disadvantages

- Duplicate records reduce the number of unique observations in each sample.
- Not effective for very small datasets.
- Increases computational cost due to multiple models.
- Does not directly reduce model bias.
- Some information is repeated across bootstrap samples.

---

# 18. Applications

Bootstrap Sampling is widely used in

- Bagging
- Random Forest
- Model Validation
- Confidence Interval Estimation
- Statistical Resampling
- Feature Importance Estimation
- Uncertainty Quantification
- Medical Research
- Finance
- Survey Analysis

---

# 19. Python Implementation

## Creating a Bootstrap Sample

```python
from sklearn.utils import resample

bootstrap_sample = resample(
    X,
    replace=True,
    n_samples=len(X),
    random_state=42
)
```

---

## Simple Example

```python
from sklearn.utils import resample

data = [1,2,3,4,5]

sample = resample(
    data,
    replace=True,
    n_samples=5,
    random_state=42
)

print(sample)
```

Possible Output

```
[4, 5, 3, 5, 5]
```

Notice that duplicates are allowed.

---

# 20. Interview Questions

## Beginner

1. What is Bootstrap Sampling?
2. Why is sampling performed with replacement?
3. What is the difference between Bootstrap and Random Sampling?
4. Why are duplicate observations allowed?
5. What is an Out-of-Bag sample?

---

## Intermediate

1. Why is Bootstrap Sampling important in Bagging?
2. Why does Bootstrap increase diversity among models?
3. Explain OOB Error.
4. Why are bootstrap samples the same size as the original dataset?
5. What is the probability that a record is never selected?

---

## Advanced

1. Derive why approximately 36.8% of observations are Out-of-Bag.
2. Can Bootstrap Sampling reduce bias? Explain.
3. How does Bootstrap Sampling improve generalization?
4. What happens if sampling is performed without replacement in Bagging?
5. Why does Random Forest require Bootstrap Sampling?

---

# 21. Summary

- **Bootstrap Sampling** is a resampling technique that selects observations **with replacement**.
- Each bootstrap sample is usually the **same size as the original dataset**.
- Duplicate observations are expected, while some observations may not be selected at all.
- The unselected observations are called **Out-of-Bag (OOB) samples**.
- Approximately **63.2%** of unique observations appear in a bootstrap sample, while **36.8%** remain OOB.
- Bootstrap Sampling creates diverse training datasets, making it the foundation of **Bagging** and **Random Forest**.
- OOB samples provide a convenient way to estimate model performance without requiring a separate validation dataset.

---

# Key Takeaways

- **Bootstrap = Sampling with Replacement**
- **Duplicates are allowed.**
- **Each bootstrap sample is typically the same size as the original dataset.**
- **~63.2%** of observations are included in a bootstrap sample.
- **~36.8%** become **Out-of-Bag (OOB)** samples.
- **Bootstrap Sampling is the core technique behind Bagging and Random Forest.**
- **Bootstrap increases model diversity, leading to better ensemble performance.**
