# 04_Python_Implementation_&_Practical.md

> **Level:** Beginner → Advanced
>
> **Prerequisites:** Python, NumPy, Pandas, Matplotlib, Scikit-learn
>
> **Goal:** Learn how to implement Simple Linear Regression from data loading to model deployment using Python.

---

# Table of Contents

1. Required Libraries
2. Dataset
3. Import Dataset
4. Exploratory Data Analysis (EDA)
5. Data Visualization
6. Correlation Analysis
7. Train-Test Split
8. Building Simple Linear Regression Model
9. Model Parameters
10. Prediction
11. Regression Line
12. Model Evaluation
13. Residual Analysis
14. Confidence & Prediction Interval
15. Cross Validation
16. Saving & Loading Model
17. Pipeline
18. Complete Project
19. Common Errors
20. Best Practices
21. Interview Questions
22. Summary

---

# 1. Required Libraries

```python
import numpy as np
import pandas as pd

import matplotlib.pyplot as plt

from sklearn.model_selection import train_test_split
from sklearn.linear_model import LinearRegression
from sklearn.metrics import (
    mean_absolute_error,
    mean_squared_error,
    r2_score
)

import joblib
```

---

# 2. Dataset

Example Dataset

| Experience | Salary |
|------------|--------|
| 1 | 30000 |
| 2 | 35000 |
| 3 | 40000 |
| 4 | 47000 |
| 5 | 52000 |

Independent Variable

```
Experience
```

Dependent Variable

```
Salary
```

---

# 3. Import Dataset

```python
df = pd.read_csv("salary.csv")
```

View Dataset

```python
df.head()
```

Dataset Information

```python
df.info()
```

Summary Statistics

```python
df.describe()
```

---

# 4. Exploratory Data Analysis (EDA)

Check Missing Values

```python
df.isnull().sum()
```

Check Duplicate Records

```python
df.duplicated().sum()
```

Check Data Types

```python
df.dtypes
```

Remove Duplicates

```python
df.drop_duplicates(inplace=True)
```

---

# 5. Data Visualization

Scatter Plot

```python
plt.scatter(df["Experience"], df["Salary"])
plt.xlabel("Experience")
plt.ylabel("Salary")
plt.title("Experience vs Salary")
plt.show()
```

Purpose

- Check linear relationship
- Detect outliers
- Understand trend

---

# 6. Correlation Analysis

```python
df.corr(numeric_only=True)
```

Only for two variables

```python
df["Experience"].corr(df["Salary"])
```

Interpretation

| Correlation | Meaning |
|-------------|----------|
| 1 | Perfect Positive |
| 0 | No Relation |
| -1 | Perfect Negative |

---

# 7. Train-Test Split

Separate Features and Target

```python
X = df[["Experience"]]

y = df["Salary"]
```

Split Dataset

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

Common Split

- 80 : 20
- 70 : 30

---

# 8. Building Simple Linear Regression Model

Create Model

```python
model = LinearRegression()
```

Train Model

```python
model.fit(X_train, y_train)
```

Model learns

```
Intercept

Coefficient
```

---

# 9. Model Parameters

Slope

```python
model.coef_
```

Intercept

```python
model.intercept_
```

Regression Equation

```
Y = Intercept + Coefficient × X
```

Example

```
Salary

=

25000

+

7000 × Experience
```

---

# 10. Prediction

Predict Test Data

```python
y_pred = model.predict(X_test)
```

Predict New Data

```python
salary = model.predict([[6]])
print(salary)
```

Multiple Predictions

```python
new_data = [[2], [4], [7]]

pred = model.predict(new_data)
```

---

# 11. Regression Line

Scatter Plot

```python
plt.scatter(X_train, y_train)
```

Regression Line

```python
plt.plot(
    X_train,
    model.predict(X_train),
    color="red"
)

plt.show()
```

Output

```
•

•

•

------------ Regression Line
```

---

# 12. Model Evaluation

### MAE

```python
mae = mean_absolute_error(
    y_test,
    y_pred
)
```

### MSE

```python
mse = mean_squared_error(
    y_test,
    y_pred
)
```

### RMSE

```python
rmse = np.sqrt(mse)
```

### R² Score

```python
r2 = r2_score(
    y_test,
    y_pred
)
```

Print Results

```python
print("MAE :", mae)
print("MSE :", mse)
print("RMSE :", rmse)
print("R2 :", r2)
```

---

# 13. Residual Analysis

Residual

```python
residual = y_test - y_pred
```

Residual Plot

```python
plt.scatter(y_pred, residual)

plt.axhline(
    y=0,
    color="red"
)

plt.xlabel("Predicted")

plt.ylabel("Residual")

plt.show()
```

Good Plot

Random scatter around zero.

Bad Plot

Visible pattern.

---

# 14. Confidence & Prediction Interval

Using **statsmodels**

```python
import statsmodels.api as sm

X = sm.add_constant(X)

model = sm.OLS(y, X).fit()

print(model.summary())
```

Useful Information

- Coefficients
- p-value
- Confidence Interval
- F-statistic
- R²
- Adjusted R²

---

# 15. Cross Validation

```python
from sklearn.model_selection import cross_val_score
```

Perform 5-Fold Cross Validation

```python
scores = cross_val_score(
    LinearRegression(),
    X,
    y,
    cv=5,
    scoring="r2"
)
```

Average Score

```python
scores.mean()
```

---

# 16. Saving & Loading Model

Save Model

```python
joblib.dump(
    model,
    "linear_model.pkl"
)
```

Load Model

```python
loaded_model = joblib.load(
    "linear_model.pkl"
)
```

Prediction

```python
loaded_model.predict([[8]])
```

---

# 17. Pipeline

```python
from sklearn.pipeline import Pipeline

pipeline = Pipeline([
    ("model", LinearRegression())
])

pipeline.fit(X_train, y_train)
```

Benefits

- Cleaner code
- Easy deployment
- Reproducible workflow

---

# 18. Complete Project Workflow

```
Load Dataset

↓

EDA

↓

Data Cleaning

↓

Visualization

↓

Correlation Analysis

↓

Train-Test Split

↓

Model Training

↓

Prediction

↓

Model Evaluation

↓

Residual Analysis

↓

Cross Validation

↓

Save Model

↓

Deployment
```

---

# 19. Common Errors

### Missing Values

```
ValueError
```

Solution

```
Handle missing values first.
```

---

### Wrong Shape

Wrong

```python
model.predict([5])
```

Correct

```python
model.predict([[5]])
```

---

### Categorical Data

Linear Regression only accepts numerical values.

Convert categorical variables using:

- One-Hot Encoding
- Label Encoding

---

### Overfitting

Possible Causes

- Data Leakage
- Small Dataset
- Outliers

---

### Poor Accuracy

Possible Reasons

- Non-linear relationship
- Missing features
- Incorrect assumptions
- Poor data quality

---

# 20. Best Practices

- Perform EDA before modeling.
- Remove duplicates.
- Handle missing values.
- Detect outliers.
- Check correlation.
- Visualize data.
- Validate assumptions.
- Use Train-Test Split.
- Perform Cross Validation.
- Evaluate with multiple metrics.
- Save trained models.
- Document experiments.

---

# 21. Interview Questions

## Beginner

1. Which library is used for Linear Regression in Python?
2. What does `fit()` do?
3. What does `predict()` return?
4. How do you obtain slope and intercept?
5. What is Train-Test Split?

---

## Intermediate

1. Why is `random_state` used?
2. Difference between `fit()` and `transform()`?
3. How do you calculate RMSE?
4. How do you evaluate a regression model?
5. Why use Cross Validation?

---

## Advanced

1. Why use `statsmodels` instead of `scikit-learn`?
2. How do you interpret regression coefficients?
3. How do you deploy a trained regression model?
4. How would you build an end-to-end regression pipeline?
5. What preprocessing steps would you perform before training?

---

# 22. Summary

- **scikit-learn** provides an easy implementation of Simple Linear Regression through the `LinearRegression` class.
- A typical workflow includes data loading, EDA, visualization, train-test split, model training, prediction, evaluation, and deployment.
- Model performance should be evaluated using **MAE**, **MSE**, **RMSE**, and **R² Score**.
- Residual analysis and Cross Validation help verify that the model generalizes well.
- Save trained models using **joblib** for reuse in production.
- Building reproducible pipelines simplifies deployment and maintenance.

---

# Key Takeaways

- **Load → Explore → Clean → Train → Predict → Evaluate → Save**
- **LinearRegression()** is the primary regression model in Scikit-learn.
- **fit()** learns the regression parameters.
- **predict()** estimates target values for new observations.
- **coef_** returns the slope, **intercept_** returns the intercept.
- **Residual plots** should show random scatter around zero.
- **Cross Validation** provides a more reliable estimate than a single train-test split.
- **joblib** is commonly used to save and load trained regression models.
- **Pipelines** improve reproducibility and simplify production workflows.
