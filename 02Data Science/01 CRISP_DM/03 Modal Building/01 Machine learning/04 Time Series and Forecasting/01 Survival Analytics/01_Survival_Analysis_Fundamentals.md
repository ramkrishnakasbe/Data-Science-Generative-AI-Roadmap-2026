# Survival Analysis Fundamentals

## 1. Introduction to Survival Analysis

Survival Analysis is a statistical technique used to analyze **time-to-event data**.

The main objective is to understand:

* How long it takes for an event to occur
* Probability of surviving beyond a particular time
* Risk of experiencing an event at a particular time
* Factors that influence the time until an event
* How to handle observations where the event has not yet occurred

### Examples

| Domain             | Entity   | Event        |
| ------------------ | -------- | ------------ |
| Healthcare         | Patient  | Death        |
| Customer Analytics | Customer | Churn        |
| Manufacturing      | Machine  | Failure      |
| Banking            | Customer | Loan Default |
| HR                 | Employee | Resignation  |
| Insurance          | Policy   | Claim        |

### Key Idea

Normal regression asks:

> **What will happen?**

Classification asks:

> **Will the event happen?**

Survival Analysis asks:

> **When will the event happen?**

---

# 2. Why Survival Analysis?

A major challenge in time-to-event data is that the exact event time may not always be observed.

### Example

Suppose a company wants to analyze customer churn.

| Customer | Observation                  |
| -------- | ---------------------------- |
| A        | Churned after 8 months       |
| B        | Churned after 12 months      |
| C        | Still active after 15 months |

For Customer C, we do not know the actual churn time.

We only know:

```text
Churn Time > 15 months
```

This is called **right censoring**.

Survival analysis is specifically designed to handle such observations.

---

# 3. Survival Data

A typical survival dataset contains:

1. **Duration / Time**
2. **Event Indicator**
3. **Covariates / Features**

Example:

| Customer | Duration | Event | Age | Plan    |
| -------- | -------: | ----: | --: | ------- |
| A        |        8 |     1 |  25 | Basic   |
| B        |       12 |     1 |  35 | Premium |
| C        |       15 |     0 |  42 | Basic   |
| D        |       20 |     1 |  31 | Premium |
| E        |       18 |     0 |  50 | Basic   |

### Duration

The amount of time for which the subject was observed.

### Event

Usually:

```text
1 → Event occurred
0 → Event did not occur during observation / censored
```

### Covariates

Variables that may influence survival.

Examples:

* Age
* Gender
* Treatment
* Income
* Customer segment
* Machine type
* Loan amount

---

# 4. Event

An **event** is the outcome whose occurrence we want to study.

Examples:

```text
Patient      → Death
Customer     → Churn
Machine      → Failure
Employee     → Resignation
Loan         → Default
Policy       → Claim
```

The event does not necessarily have to be negative.

It can represent any measurable occurrence.

---

# 5. Survival Time

Survival time is the time from the beginning of observation until:

* The event occurs, or
* The observation becomes censored.

### Uncensored Example

```text
Customer joined → January 2024
Customer churned → September 2024
```

Therefore:

```text
Survival Time = 8 months
Event = 1
```

### Censored Example

```text
Customer joined → January 2024
Study ended → September 2024
Customer still active
```

Therefore:

```text
Observed Time = 8 months
Event = 0
```

The actual churn time is unknown.

---

# 6. Censoring

**Censoring** occurs when the exact event time is not observed.

However, we still have partial information about the event time.

### Example

A study runs for 12 months.

```text
Patient A → Death at month 5
Patient B → Death at month 8
Patient C → Alive at month 12
```

For Patient C:

```text
Death Time > 12 months
```

Patient C is therefore **right-censored**.

---

# 7. Types of Censoring

## 7.1 Right Censoring

The event has not occurred by the end of observation.

Example:

```text
Observation:
0 ---------------------- 12
                         ↑
                    Study ends
                    Event unknown
```

We know:

```text
T > 12
```

but we do not know the exact value of `T`.

### Common examples

* Customer has not churned by study end
* Patient is still alive when study ends
* Machine has not failed during monitoring

---

## 7.2 Left Censoring

The event has already occurred before observation began, but the exact time is unknown.

Example:

A patient enters a study and is already infected.

We know:

```text
Infection occurred before study entry
```

but the exact infection time is unknown.

---

## 7.3 Interval Censoring

The event is known to have occurred within a specific interval.

Example:

```text
Month 3 → Disease not detected
Month 6 → Disease detected
```

Therefore:

```text
3 < Event Time <= 6
```

The exact event time is unknown.

---

# 8. Censoring Summary

| Type               | Meaning                           |
| ------------------ | --------------------------------- |
| Right Censoring    | Event occurs after observed time  |
| Left Censoring     | Event occurred before observation |
| Interval Censoring | Event occurred within an interval |

For most introductory survival analysis problems, **right censoring** is the most common.

---

# 9. Censored vs Uncensored Observations

## Uncensored

The event occurred and the event time is known.

```text
Duration = 10
Event = 1
```

Meaning:

> Event occurred at time 10.

## Censored

The event was not observed during the observation period.

```text
Duration = 10
Event = 0
```

Meaning:

> The subject was observed for 10 time units without observing the event.

### Important Interview Point

```text
Event = 0
```

does **not** necessarily mean:

> The event will never happen.

It usually means:

> The event was not observed during the available observation period.

---

# 10. Survival Function

The **survival function** represents the probability that an individual survives beyond a particular time.

It is defined as:

$$
S(t) = P(T > t)
$$

Where:

* `T` = random survival time
* `t` = specific time
* `S(t)` = probability of surviving beyond time `t`

### Example

If:

```text
S(12) = 0.80
```

then:

> There is an estimated 80% probability that the subject survives beyond 12 time units.

---

# 11. Properties of Survival Function

### At Time 0

Normally:

$$
S(0) = 1
$$

Meaning:

> At the beginning of observation, survival probability is 100%.

### As Time Increases

Survival probability generally decreases.

Example:

| Time | Survival Probability |
| ---: | -------------------: |
|    0 |                 1.00 |
|    5 |                 0.90 |
|   10 |                 0.78 |
|   15 |                 0.65 |
|   20 |                 0.50 |
|   25 |                 0.35 |

Therefore:

```text
S(t) decreases as t increases
```

### Range

Usually:

$$
0 \leq S(t) \leq 1
$$

---

# 12. Survival Curve

A survival curve plots:

```text
X-axis → Time
Y-axis → Survival Probability
```

A typical survival curve looks like:

```text
Survival
Probability
1.0 |───────────
    |           \
0.8 |            \──────
    |                   \
0.6 |                    \────
    |                         \
0.4 |                          \───
    |
0.2 |
    |
0.0 +------------------------------> Time
```

Important characteristics:

* Starts near 1
* Generally decreases
* Can contain flat regions
* Drops when events occur
* Censored observations can be marked on the curve

---

# 13. Hazard Function

The **hazard function** represents the instantaneous risk of experiencing the event at time `t`, given that the subject has survived up to time `t`.

It is represented as:

$$
h(t)
$$

Conceptually:

> Among individuals who have survived until time `t`, how high is the risk that the event occurs immediately after `t`?

### Important

Hazard is **not simply the probability of failure**.

It represents an instantaneous event rate conditional on survival up to that time.

---

# 14. Hazard Function Intuition

Consider machine failure.

At an early age:

```text
Machine Age = 1 year
Hazard = Low
```

At an old age:

```text
Machine Age = 10 years
Hazard = High
```

The hazard function can therefore change over time.

Possible patterns include:

```text
Increasing Hazard
Decreasing Hazard
Constant Hazard
Bathtub-shaped Hazard
```

---

# 15. Common Hazard Shapes

## Increasing Hazard

Risk increases over time.

Example:

> Aging machines become more likely to fail.

```text
Hazard
  |
  |        /
  |      /
  |    /
  |  /
  |_/____________ Time
```

## Decreasing Hazard

Risk decreases over time.

Example:

> Early failures occur frequently, but surviving machines become more reliable.

## Constant Hazard

Risk remains approximately constant.

This is an important assumption of the **Exponential Survival Model**.

## Bathtub Hazard

Commonly used for machine reliability.

Three phases:

```text
Early failures
      ↓
Useful life
      ↓
Wear-out failures
```

---

# 16. Cumulative Hazard Function

The cumulative hazard function represents the accumulated hazard up to time `t`.

It is represented by:

$$
H(t)
$$

The relationship between hazard and cumulative hazard is:

$$
H(t) = \int_0^t h(u),du
$$

The relationship between survival and cumulative hazard is:

$$
S(t) = e^{-H(t)}
$$

Therefore:

$$
H(t) = -\log S(t)
$$

### Important Relationships

```text
Hazard
   ↓
Cumulative Hazard
   ↓
Survival Function
```

Mathematically:

$$
H(t) = -\log S(t)
$$

and:

$$
S(t) = e^{-H(t)}
$$

---

# 17. Survival Function vs Hazard Function

| Concept        | Survival Function                 | Hazard Function             |
| -------------- | --------------------------------- | --------------------------- |
| Symbol         | `S(t)`                            | `h(t)`                      |
| Meaning        | Probability of surviving beyond t | Instantaneous event risk    |
| Range          | 0 to 1                            | 0 to ∞                      |
| Interpretation | "How likely is survival?"         | "How high is current risk?" |
| Time dependent | Yes                               | Yes                         |
| Can increase?  | Generally no                      | Yes                         |
| Used for       | Survival probability              | Risk analysis               |

---

# 18. Survival Probability vs Event Probability

Survival function:

$$
S(t) = P(T > t)
$$

The probability that the event has occurred by time `t` is:

$$
P(T \leq t) = 1 - S(t)
$$

This is the **Cumulative Distribution Function (CDF)**.

Therefore:

$$
F(t) = 1 - S(t)
$$

### Example

Suppose:

$$
S(10) = 0.75
$$

Then:

$$
F(10) = 1 - 0.75 = 0.25
$$

Therefore:

> There is a 25% probability that the event has occurred by time 10.

---

# 19. Median Survival Time

The **median survival time** is the time at which the survival probability reaches 50%.

Therefore:

$$
S(t) = 0.5
$$

### Example

| Time | Survival |
| ---: | -------: |
|   10 |     0.80 |
|   20 |     0.65 |
|   30 |     0.52 |
|   35 |     0.48 |

The median survival time is approximately between:

```text
30 and 35 time units
```

### Interpretation

Approximately 50% of the population is expected to experience the event by the median survival time.

---

# 20. Mean vs Median Survival

### Mean Survival

Average time until the event.

### Median Survival

Time at which survival probability reaches 50%.

Median survival is often more useful when survival times are skewed or heavily censored.

---

# 21. Survival Analysis Dataset

A typical dataset looks like:

| ID | Duration | Event | Age | Treatment |
| -- | -------: | ----: | --: | --------- |
| 1  |       10 |     1 |  45 | A         |
| 2  |       15 |     0 |  52 | B         |
| 3  |        7 |     1 |  38 | A         |
| 4  |       20 |     0 |  61 | B         |
| 5  |       12 |     1 |  49 | A         |

### Core Variables

```text
Duration → Observed time
Event    → Whether event occurred
Features → Variables influencing survival
```

---

# 22. Survival Analysis Workflow

```text
Define Event
      ↓
Collect Time-to-Event Data
      ↓
Identify Censored Observations
      ↓
Data Cleaning
      ↓
Exploratory Data Analysis
      ↓
Kaplan-Meier Analysis
      ↓
Compare Survival Groups
      ↓
Statistical Testing
      ↓
Survival Model
      ↓
Model Evaluation
      ↓
Interpret Results
```

---

# 23. Common Applications

## Healthcare

* Time until death
* Time until disease recurrence
* Time until recovery
* Time until relapse

## Customer Analytics

* Time until churn
* Customer retention

## Manufacturing

* Time until machine failure
* Equipment reliability

## Banking

* Time until loan default
* Time until credit event

## HR

* Time until employee resignation
* Employee retention

## Insurance

* Time until claim
* Time until policy termination

---

# 24. Survival Analysis vs Regression

| Feature        | Regression               | Survival Analysis        |
| -------------- | ------------------------ | ------------------------ |
| Target         | Numeric value            | Time-to-event            |
| Censoring      | Usually not handled      | Explicitly handled       |
| Output         | Predicted value          | Survival/risk over time  |
| Time component | Not necessarily required | Fundamental              |
| Example        | Predict sales            | Predict time until churn |
| Common Models  | Linear Regression        | Cox PH, KM, AFT          |

---

# 25. Survival Analysis vs Classification

Classification predicts:

```text
Will the event happen?
YES / NO
```

Survival Analysis predicts:

```text
When will the event happen?
```

It can also estimate:

```text
Probability of surviving until a specific time
```

### Example

Classification:

> Will this customer churn?

Survival Analysis:

> What is the probability that this customer remains active for the next 12 months?

---

# 26. Important Terminology

| Term               | Meaning                                     |
| ------------------ | ------------------------------------------- |
| Survival Time      | Time until event or censoring               |
| Event              | Outcome being studied                       |
| Censoring          | Exact event time is not observed            |
| Right Censoring    | Event not observed by end of observation    |
| Left Censoring     | Event occurred before observation           |
| Interval Censoring | Event occurred within an interval           |
| Survival Function  | Probability of surviving beyond `t`         |
| Hazard Function    | Instantaneous event risk                    |
| Cumulative Hazard  | Accumulated hazard                          |
| Survival Curve     | Survival probability plotted over time      |
| Median Survival    | Time where survival probability reaches 50% |
| CDF                | Probability event has occurred by time `t`  |

---

# 27. Important Mathematical Relationships

### Survival Function

$$
S(t) = P(T > t)
$$

### CDF

$$
F(t) = P(T \leq t)
$$

### Relationship

$$
F(t) = 1 - S(t)
$$

### Cumulative Hazard

$$
H(t) = -\log S(t)
$$

### Survival from Cumulative Hazard

$$
S(t) = e^{-H(t)}
$$

### Median Survival

$$
S(t) = 0.5
$$

---

# 28. Key Interview Questions

## Q1. What is Survival Analysis?

Survival Analysis is a statistical approach for analyzing **time-to-event data**, particularly when some observations are censored.

---

## Q2. Why is Survival Analysis required?

Because normal regression/classification methods do not naturally handle censored observations and time-to-event information.

---

## Q3. What is censoring?

Censoring occurs when the exact event time is unknown, but we know some information about the event time.

---

## Q4. What is right censoring?

Right censoring occurs when the event has not occurred by the end of the observation period.

---

## Q5. What is the difference between censored and uncensored data?

**Uncensored:**

The event occurred and the event time is known.

**Censored:**

The event was not observed during the available observation period.

---

## Q6. Does Event = 0 mean the event will never happen?

No.

It usually means the event was not observed during the observation period.

---

## Q7. What is the survival function?

The survival function gives the probability that the event time is greater than a specific time:

$$
S(t) = P(T > t)
$$

---

## Q8. What is the hazard function?

The hazard function represents the instantaneous risk of experiencing the event at time `t`, conditional on surviving up to time `t`.

---

## Q9. What is the difference between survival and hazard?

**Survival:**

> Probability of surviving beyond a particular time.

**Hazard:**

> Instantaneous risk of experiencing the event at that time, given survival up to that time.

---

## Q10. What is cumulative hazard?

Cumulative hazard represents the total accumulated hazard up to time `t`.

$$
H(t) = \int_0^t h(u)du
$$

---

## Q11. What is the relationship between survival and cumulative hazard?

$$
S(t) = e^{-H(t)}
$$

or:

$$
H(t) = -\log S(t)
$$

---

## Q12. What is median survival time?

The time at which the estimated survival probability equals 50%.

$$
S(t)=0.5
$$

---

## Q13. Why can't we simply remove censored observations?

Because censored observations contain valuable information.

For example, if a customer is observed for 15 months without churning, we know:

```text
Churn Time > 15 months
```

Removing that customer would discard this information and can introduce bias.

---

## Q14. Can survival analysis be used for customer churn?

Yes.

Instead of simply predicting whether a customer will churn, survival analysis can estimate:

> The probability that the customer remains active beyond a particular time.

---

## Q15. What are the most common survival analysis models?

Important models include:

* Kaplan-Meier Estimator
* Cox Proportional Hazards Model
* Exponential Model
* Weibull Model
* Accelerated Failure Time Model
* Random Survival Forest

---

# 29. Quick Revision

```text
SURVIVAL ANALYSIS
│
├── Time-to-Event
│
├── Event
│
├── Censoring
│   ├── Right
│   ├── Left
│   └── Interval
│
├── Survival Function
│   └── S(t) = P(T > t)
│
├── CDF
│   └── F(t) = 1 - S(t)
│
├── Hazard Function
│   └── Instantaneous Event Risk
│
├── Cumulative Hazard
│   └── H(t) = -log(S(t))
│
└── Median Survival
    └── S(t) = 0.5
```

## Must Remember

```text
Event = 1
→ Event occurred

Event = 0
→ Usually censored

S(t)
→ Probability of surviving beyond t

F(t)
→ Probability event occurred by t

h(t)
→ Instantaneous event risk

H(t)
→ Cumulative hazard

H(t) = -log(S(t))

S(t) = exp(-H(t))

Median Survival
→ S(t) = 0.5
```
