# 02_Kaplan_Meier_and_Log_Rank_Test.md

# Kaplan-Meier Estimator & Log-Rank Test

## 1. Introduction

The **Kaplan-Meier estimator** is a non-parametric statistical method used to estimate the **survival function** from time-to-event data.

It is mainly used to answer:

> What is the probability that an individual survives beyond a particular time?

The **Log-Rank Test** is used to compare the survival distributions of two or more groups.

### Example

Suppose we want to compare customer retention between:

```text
Group A → Basic Plan
Group B → Premium Plan
```

Kaplan-Meier can estimate the survival curve for each group.

The Log-Rank Test can determine whether the survival curves are statistically significantly different.

---

# 2. Kaplan-Meier Estimator

The Kaplan-Meier estimator estimates the probability of surviving beyond time `t`.

It is especially useful when the dataset contains **censored observations**.

### Key Characteristics

* Non-parametric
* Handles right-censored data
* Does not assume a specific probability distribution
* Produces a survival curve
* Can estimate median survival time
* Can compare survival between groups

---

# 3. Why Kaplan-Meier?

Suppose we have:

| Customer | Time | Event |
| -------- | ---: | ----: |
| A        |    2 |     1 |
| B        |    4 |     1 |
| C        |    5 |     0 |
| D        |    7 |     1 |
| E        |    9 |     0 |

Some customers churned and some were censored.

A normal average cannot properly represent the survival pattern because censored customers have unknown actual event times.

Kaplan-Meier uses the available information while correctly accounting for censoring.

---

# 4. Kaplan-Meier Formula

The Kaplan-Meier survival estimator is:

$$
\hat{S}(t)
==========

\prod_{t_i \leq t}
\left(
1-\frac{d_i}{n_i}
\right)
$$

Equivalent form:

$$
\hat{S}(t)
==========

\prod_{t_i \leq t}
\frac{n_i-d_i}{n_i}
$$

Where:

* `t_i` = time at which an event occurs
* `d_i` = number of events at time `t_i`
* `n_i` = number of individuals at risk immediately before `t_i`

---

# 5. Understanding `nᵢ` and `dᵢ`

### `nᵢ` — Number at Risk

Number of individuals who are still being observed and have not experienced the event immediately before time `tᵢ`.

### `dᵢ` — Number of Events

Number of events occurring at time `tᵢ`.

Therefore:

$$
\frac{d_i}{n_i}
$$

represents the proportion of individuals at risk who experience the event at that time.

---

# 6. Simple Kaplan-Meier Example

Consider:

| Person | Time | Event |
| ------ | ---: | ----: |
| A      |    2 |     1 |
| B      |    4 |     1 |
| C      |    5 |     0 |
| D      |    7 |     1 |
| E      |    9 |     0 |

Initially:

```text
n = 5
```

At time 2:

```text
d = 1
n = 5
```

Therefore:

$$
S(2)=\frac{5-1}{5}
$$

$$
S(2)=0.8
$$

So survival probability after time 2 is:

```text
80%
```

---

# 7. Kaplan-Meier Step-by-Step

Suppose:

| Time | At Risk `n` | Events `d` |
| ---: | ----------: | ---------: |
|    2 |           5 |          1 |
|    4 |           4 |          1 |
|    7 |           2 |          1 |

### At time 2

$$
S(2)=\frac{5-1}{5}=0.8
$$

### At time 4

$$
S(4)
====

0.8
\times
\frac{4-1}{4}
$$

$$
S(4)=0.8 \times 0.75
$$

$$
S(4)=0.60
$$

### At time 7

$$
S(7)
====

0.60
\times
\frac{2-1}{2}
$$

$$
S(7)=0.30
$$

Therefore:

| Time | Survival Probability |
| ---: | -------------------: |
|    0 |                 1.00 |
|    2 |                 0.80 |
|    4 |                 0.60 |
|    7 |                 0.30 |

---

# 8. Why Is the Kaplan-Meier Curve a Step Function?

The Kaplan-Meier survival curve changes only when an **event occurs**.

If no event occurs between two time points:

```text
Survival probability remains constant
```

When an event occurs:

```text
Survival probability drops
```

Therefore the curve has a step-like shape.

```text
Survival
1.0 |──────────
    |          |
0.8 |          └────────
    |                   |
0.6 |                   └──────
    |                           |
0.4 |                           └──
    |
0.0 +-------------------------------> Time
```

---

# 9. Effect of Censoring on Kaplan-Meier Curve

A censored observation does **not directly cause a drop** in the survival curve.

Instead, it reduces the number of individuals remaining at risk for future event times.

Example:

```text
Event      → Curve drops
Censoring  → Usually no drop
```

Censored observations are commonly shown using small marks on the survival curve.

---

# 10. Kaplan-Meier Curve Interpretation

Suppose:

$$
S(12)=0.70
$$

Interpretation:

> The estimated probability of remaining event-free beyond time 12 is 70%.

For customer churn:

> There is an estimated 70% probability that a customer remains active beyond 12 months.

---

# 11. Median Survival Time

The median survival time is the time at which:

$$
S(t)=0.5
$$

Example:

| Time | Survival |
| ---: | -------: |
|    5 |     0.85 |
|   10 |     0.72 |
|   15 |     0.58 |
|   20 |     0.49 |

The median survival time is approximately:

```text
20 time units
```

### Important

If the survival curve never reaches 0.5:

> Median survival time cannot be estimated from the observed data.

This is an important interview point.

---

# 12. Comparing Kaplan-Meier Curves

Suppose we have two groups:

```text
Treatment A
Treatment B
```

We can estimate:

```text
KM Curve A
KM Curve B
```

and visually compare them.

Example:

```text
Survival
1.0 |──────────── Group A
    |       \
0.8 |        \────────
    |
0.6 |──────────── Group B
    |       \
0.4 |        \──────
    |
0.0 +----------------------> Time
```

If one curve consistently remains higher:

> That group has better observed survival.

However, visual difference alone does not establish statistical significance.

For that, we commonly use the **Log-Rank Test**.

---

# 13. Log-Rank Test

The **Log-Rank Test** is a statistical hypothesis test used to compare survival distributions between groups.

It answers:

> Are the survival curves of the groups statistically different?

### Example

Compare:

```text
Group A → Treatment A
Group B → Treatment B
```

Hypotheses:

### Null Hypothesis `H₀`

The survival distributions are the same.

```text
H₀: S₁(t) = S₂(t)
```

### Alternative Hypothesis `H₁`

The survival distributions are different.

```text
H₁: S₁(t) ≠ S₂(t)
```

---

# 14. Log-Rank Test Intuition

At each observed event time:

1. Determine the number of individuals at risk in each group.
2. Determine how many events actually occurred in each group.
3. Calculate the expected number of events under the assumption that the groups have equal survival.
4. Compare observed vs expected events across all event times.
5. Calculate a test statistic.

The test combines information across the entire follow-up period.

---

# 15. Log-Rank Test Statistic

The Log-Rank Test is commonly based on a chi-square statistic.

For two groups, conceptually:

$$
\chi^2
======

\frac{(O-E)^2}{E}
$$

Where:

* `O` = observed number of events
* `E` = expected number of events

For multiple groups, the calculation uses the corresponding vector/matrix form.

---

# 16. P-Value Interpretation

Suppose the Log-Rank Test produces:

```text
p-value = 0.03
```

Using:

```text
α = 0.05
```

Since:

```text
0.03 < 0.05
```

we reject the null hypothesis.

Conclusion:

> There is statistically significant evidence that the survival distributions differ between the groups.

---

# 17. Non-Significant Result

Suppose:

```text
p-value = 0.40
```

Since:

```text
0.40 > 0.05
```

we fail to reject the null hypothesis.

Conclusion:

> There is insufficient statistical evidence to conclude that the survival distributions are different.

### Important

Do not say:

> The two groups are definitely identical.

Instead say:

> We do not have sufficient evidence to conclude that they differ.

---

# 18. Kaplan-Meier vs Log-Rank Test

| Kaplan-Meier                  | Log-Rank Test                       |
| ----------------------------- | ----------------------------------- |
| Estimates survival function   | Tests survival distributions        |
| Produces survival curve       | Produces test statistic and p-value |
| Descriptive/estimation method | Hypothesis test                     |
| Shows survival probability    | Determines whether groups differ    |
| Handles censoring             | Handles censoring                   |
| Non-parametric                | Non-parametric                      |

### Easy Interview Explanation

> Kaplan-Meier tells us **what the survival looks like**, while the Log-Rank Test tells us **whether the survival curves are statistically different**.

---

# 19. Kaplan-Meier Workflow

```text
Survival Dataset
      ↓
Identify Duration
      ↓
Identify Event Indicator
      ↓
Fit Kaplan-Meier Estimator
      ↓
Estimate Survival Function
      ↓
Plot Survival Curve
      ↓
Calculate Median Survival
      ↓
Compare Groups
      ↓
Perform Log-Rank Test
      ↓
Interpret P-value
```

---

# 20. Python Library

The most commonly used Python library for basic survival analysis is:

```python
lifelines
```

Installation:

```bash
pip install lifelines
```

Import:

```python
from lifelines import KaplanMeierFitter
```

---

# 21. Basic Kaplan-Meier Implementation

```python
from lifelines import KaplanMeierFitter

kmf = KaplanMeierFitter()

kmf.fit(
    durations=df["duration"],
    event_observed=df["event"]
)

kmf.plot()
```

Where:

```text
duration → observed survival time
event    → event indicator
```

---

# 22. Getting Survival Probabilities

```python
kmf.survival_function_
```

Example output:

```text
          KM_estimate
timeline
0.0            1.00
2.0            0.80
4.0            0.60
7.0            0.30
```

---

# 23. Predicting Survival Probability

To estimate survival probability at time 12:

```python
kmf.predict(12)
```

Example:

```text
0.72
```

Interpretation:

> Estimated probability of surviving beyond time 12 is 72%.

---

# 24. Median Survival Using Python

```python
kmf.median_survival_time_
```

Example:

```text
20.0
```

Interpretation:

> Estimated median survival time is 20 time units.

---

# 25. Confidence Intervals

Kaplan-Meier estimates can be accompanied by confidence intervals.

```python
kmf.confidence_interval_
```

A confidence interval provides a range of plausible values for the estimated survival function.

Example:

```text
Survival at t = 12

Estimate = 0.72
95% CI = [0.64, 0.79]
```

Interpretation:

> The estimated survival probability is 72%, with a 95% confidence interval from 64% to 79%.

---

# 26. Kaplan-Meier by Groups

Suppose the dataset contains:

```text
treatment = A / B
```

We can fit separate survival curves.

```python
from lifelines import KaplanMeierFitter

kmf_a = KaplanMeierFitter()
kmf_b = KaplanMeierFitter()

group_a = df["treatment"] == "A"
group_b = df["treatment"] == "B"

kmf_a.fit(
    df.loc[group_a, "duration"],
    df.loc[group_a, "event"],
    label="Treatment A"
)

kmf_b.fit(
    df.loc[group_b, "duration"],
    df.loc[group_b, "event"],
    label="Treatment B"
)

ax = kmf_a.plot()
kmf_b.plot(ax=ax)
```

This produces separate Kaplan-Meier curves.

---

# 27. Log-Rank Test in Python

The `lifelines` library provides:

```python
from lifelines.statistics import logrank_test
```

Example:

```python
from lifelines.statistics import logrank_test

results = logrank_test(
    df.loc[group_a, "duration"],
    df.loc[group_b, "duration"],
    event_observed_A=df.loc[group_a, "event"],
    event_observed_B=df.loc[group_b, "event"]
)

print(results.summary)
```

---

# 28. Accessing the P-Value

```python
results.p_value
```

Example:

```text
0.021
```

Using:

```text
α = 0.05
```

Since:

```text
0.021 < 0.05
```

we reject the null hypothesis.

Conclusion:

> The survival distributions are statistically significantly different.

---

# 29. Log-Rank Test with More Than Two Groups

For multiple groups, the Log-Rank Test can be extended to compare survival distributions across multiple groups.

Example:

```text
Group A
Group B
Group C
```

The null hypothesis becomes:

> All groups have the same survival distribution.

If the overall test is significant, additional pairwise comparisons may be needed to determine which groups differ.

---

# 30. Important Assumption of Log-Rank Test

The Log-Rank Test is most appropriate when the primary interest is in comparing survival distributions over the follow-up period.

It works particularly well when the hazard functions are reasonably proportional.

### Important Limitation

If survival curves cross substantially, the standard Log-Rank Test may have reduced power or may not reflect the specific difference of interest.

---

# 31. Kaplan-Meier Assumptions

Important assumptions include:

### 1. Independent Censoring

The censoring mechanism should not be strongly related to the future event risk, conditional on relevant information.

### 2. Independent Survival Times

Observations are generally assumed to be independent.

### 3. Correct Event Definition

The event indicator must correctly identify whether the event occurred.

### 4. Accurate Time Measurement

The duration should correctly represent the observation period.

---

# 32. Advantages of Kaplan-Meier

* Simple to understand
* Non-parametric
* Handles right censoring
* No distributional assumption
* Easy visual interpretation
* Estimates survival probabilities
* Estimates median survival
* Useful for comparing groups visually

---

# 33. Limitations of Kaplan-Meier

* Primarily univariate/group-based analysis
* Does not directly model multiple predictors simultaneously
* Cannot easily adjust for confounding variables
* Survival curves can become unstable with very few subjects remaining
* Standard KM does not directly provide individual-level covariate effects
* Does not explain why survival differs between groups

For multiple covariates, models such as **Cox Proportional Hazards** are more appropriate.

---

# 34. Kaplan-Meier vs Cox Regression

| Kaplan-Meier                                   | Cox PH                              |
| ---------------------------------------------- | ----------------------------------- |
| Non-parametric                                 | Semi-parametric                     |
| Mainly descriptive                             | Predictive/inferential              |
| Usually one grouping variable                  | Multiple covariates                 |
| Produces survival curve                        | Estimates hazard ratios             |
| Does not require baseline hazard specification | Baseline hazard left unspecified    |
| Good for visualizing survival                  | Good for studying covariate effects |

---

# 35. Example: Customer Churn

Suppose we have 1,000 customers.

We want to compare:

```text
Basic Plan
Premium Plan
```

### Step 1

Calculate customer survival time:

```text
Time from subscription → churn/censoring
```

### Step 2

Create event indicator:

```text
1 → Churned
0 → Still active
```

### Step 3

Fit Kaplan-Meier curves.

```text
Basic Plan → KM Curve
Premium Plan → KM Curve
```

### Step 4

Compare curves.

### Step 5

Perform Log-Rank Test.

Suppose:

```text
p-value = 0.01
```

Conclusion:

> There is statistically significant evidence that customer survival differs between Basic and Premium customers.

---

# 36. Example Interpretation

Suppose:

```text
Premium Plan:
Median Survival = 24 months

Basic Plan:
Median Survival = 15 months
```

Interpretation:

> The estimated median time until churn is longer for Premium customers.

If the Log-Rank Test gives:

```text
p-value < 0.05
```

we also have statistical evidence that the survival distributions differ.

---

# 37. Important Interview Questions

## Q1. What is Kaplan-Meier?

Kaplan-Meier is a non-parametric estimator used to estimate the survival function from time-to-event data, including censored observations.

---

## Q2. Why is Kaplan-Meier called non-parametric?

Because it does not assume a specific probability distribution for survival times.

---

## Q3. What does the Kaplan-Meier curve represent?

It represents the estimated probability of surviving beyond each point in time.

---

## Q4. Why is the Kaplan-Meier curve a step function?

Because the estimated survival probability changes at observed event times and remains constant between events.

---

## Q5. Does censoring cause the Kaplan-Meier curve to drop?

No.

An event causes the survival curve to drop. Censoring typically changes the number of subjects at risk for subsequent event times.

---

## Q6. What happens when multiple events occur at the same time?

The Kaplan-Meier estimator accounts for the number of events occurring at that time when calculating the survival probability.

---

## Q7. What is the Log-Rank Test?

It is a non-parametric hypothesis test used to determine whether survival distributions differ between groups.

---

## Q8. What is the null hypothesis of the Log-Rank Test?

The survival distributions of the groups are the same.

---

## Q9. What does a p-value < 0.05 indicate?

Under the chosen significance level of 0.05, there is statistically significant evidence against the null hypothesis.

---

## Q10. What does a p-value > 0.05 mean?

There is insufficient evidence to conclude that the survival distributions differ.

---

## Q11. Can Kaplan-Meier handle censored data?

Yes. Handling censored observations is one of its major advantages.

---

## Q12. Can Kaplan-Meier handle multiple predictors?

Not in the same way as a regression model.

Kaplan-Meier is primarily used for estimating survival curves and comparing groups. For multiple predictors, Cox regression is commonly used.

---

## Q13. What is median survival?

The time at which the estimated survival probability reaches 50%.

---

## Q14. What if the Kaplan-Meier curve never reaches 50%?

The median survival time is not estimable from the observed follow-up period.

---

## Q15. Kaplan-Meier vs Log-Rank Test?

> Kaplan-Meier estimates and visualizes survival curves, while the Log-Rank Test statistically compares survival distributions between groups.

---

## Q16. Why shouldn't we use a t-test to compare survival times?

Because survival data may be censored and often violate the assumptions required for standard methods. Survival-specific methods account for censoring.

---

## Q17. Why can't we calculate the simple average survival time?

Because censored observations do not provide the complete event time.

For example:

```text
Customer observed for 10 months
Event not observed
```

The actual event time could be:

```text
11 months
20 months
50 months
```

The exact value is unknown.

---

# 38. Coding Interview Questions

### Question 1

Fit a Kaplan-Meier model.

```python
from lifelines import KaplanMeierFitter

kmf = KaplanMeierFitter()

kmf.fit(
    durations=df["duration"],
    event_observed=df["event"]
)

kmf.plot()
```

---

### Question 2

Find median survival time.

```python
kmf.median_survival_time_
```

---

### Question 3

Predict survival probability at 12 months.

```python
kmf.predict(12)
```

---

### Question 4

Compare two survival groups.

```python
from lifelines.statistics import logrank_test

results = logrank_test(
    group_a_duration,
    group_b_duration,
    event_observed_A=group_a_event,
    event_observed_B=group_b_event
)

print(results.p_value)
```

---

# 39. Common Interview Traps

### Trap 1

**"Event = 0 means the person never experienced the event."**

Incorrect.

It generally means the event was not observed during the available observation period.

---

### Trap 2

**"Censoring causes the survival curve to decrease."**

Incorrect.

Events cause the survival estimate to decrease. Censoring affects the risk set.

---

### Trap 3

**"Kaplan-Meier predicts individual survival time."**

Not directly.

Kaplan-Meier estimates the population/group-level survival function.

---

### Trap 4

**"Log-Rank Test tells which group is better."**

Not by itself.

It tests whether survival distributions differ statistically.

You still need the survival curves and/or survival estimates to understand the direction and practical meaning of the difference.

---

### Trap 5

**"p-value > 0.05 proves the groups are identical."**

Incorrect.

It means there is insufficient evidence to reject the null hypothesis.

---

### Trap 6

**"Kaplan-Meier requires normally distributed survival times."**

Incorrect.

Kaplan-Meier is non-parametric and does not assume a particular survival-time distribution.

---

# 40. Quick Revision

```text
KAPLAN-MEIER
│
├── Non-parametric
│
├── Estimates Survival Function
│
├── Handles Right Censoring
│
├── Produces Survival Curve
│
├── Estimates Median Survival
│
└── Can Compare Groups


LOG-RANK TEST
│
├── Hypothesis Test
│
├── Compares Survival Distributions
│
├── H₀ → Same Survival Distribution
│
├── H₁ → Different Survival Distribution
│
└── Uses P-value for Statistical Evidence
```

## Must Remember

```text
Kaplan-Meier
→ Estimates survival probability over time

Survival Function
→ S(t) = P(T > t)

KM Estimator
→ Product of conditional survival probabilities

Event
→ Causes survival curve to drop

Censoring
→ Does not directly cause a drop

Median Survival
→ S(t) = 0.5

Log-Rank Test
→ Compares survival distributions

H₀
→ Survival distributions are the same

p-value < α
→ Reject H₀

p-value > α
→ Fail to reject H₀
```
