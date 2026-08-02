# 05_Python_Implementation.md

> **Level:** Beginner → Advanced
>
> **Prerequisites:** Pandas, NumPy, Scikit-learn, Multiple Linear Regression Fundamentals
>
> **Goal:** Learn how to build, evaluate, diagnose, and improve a Multiple Linear Regression model using Python. This file focuses only on concepts and implementation specific to Multiple Linear Regression.

---

# Table of Contents

1. Required Libraries
2. Load Dataset
3. Separate Features & Target
4. Train-Test Split
5. Train Multiple Linear Regression Model
6. Model Coefficients
7. Prediction
8. Feature Importance using Coefficients
9. Handling Categorical Variables
10. Correlation Matrix
11. VIF Calculation
12. Feature Selection using RFE
13. Sequential Feature Selection
14. Polynomial Features
15. Interaction Features
16. Statsmodels Summary
17. Ridge Regression
18. Lasso Regression
19. Elastic Net
20. Model Comparison
21. Complete Workflow
22. Best Practices
23. Interview Questions
24. Summary

---

# 1. Required Libraries

```python
import numpy as np
import pandas as pd

from sklearn.model_selection import train_test_split

from sklearn.linear_model import (
    LinearRegression,
    Ridge,
    Lasso,
    ElasticNet
)

from sklearn.preprocessing import (
    OneHotEncoder,
    PolynomialFeatures,
    StandardScaler
)

from sklearn.compose import ColumnTransformer

from sklearn.pipeline import Pipeline

from sklearn.feature_selection import (
    RFE,
    SequentialFeatureSelector
)

from sklearn.metrics import (
    r2_score,
    mean_absolute_error,
    mean_squared_error
)

import statsmodels.api as sm

import seaborn as sns
import matplotlib.pyplot as plt
```

---

# 2. Load Dataset

```python
df = pd.read_csv("house_price.csv")
```

Basic Inspection

```python
df.head()

df.info()

df.describe()
```

---

# 3. Separate Features & Target

```python
X = df.drop("Price", axis=1)

y = df["Price"]
```

Multiple features

```
Area

Bedrooms

Age

Parking

Location Score
```

Target

```
Price
```

---

# 4. Train-Test Split

```python
X_train, X_test, y_train, y_test = train_test_split(
    X,
    y,
    test_size=0.2,
    random_state=42
)
```

---

# 5. Train Multiple Linear Regression Model

```python
model = LinearRegression()

model.fit(X_train, y_train)
```

Prediction

```python
y_pred = model.predict(X_test)
```

---

# 6. Model Coefficients

Intercept

```python
model.intercept_
```

Coefficients

```python
model.coef_
```

Feature Names

```python
X.columns
```

Create Coefficient Table

```python
coef = pd.DataFrame({
    "Feature": X.columns,
    "Coefficient": model.coef_
})

coef.sort_values(
    by="Coefficient",
    ascending=False
)
```

---

# 7. Prediction

Single Prediction

```python
new_house = [[1200,3,5,1,8]]

prediction = model.predict(new_house)
```

Multiple Predictions

```python
model.predict(X_test)
```

---

# 8. Feature Importance using Coefficients

Higher absolute coefficient

↓

Greater influence

```python
importance = pd.DataFrame({

"Feature":X.columns,

"Importance":abs(model.coef_)

})

importance.sort_values(

"Importance",

ascending=False

)
```

**Note**

Coefficient comparison is meaningful only after feature scaling or when variables are on comparable scales.

---

# 9. Handling Categorical Variables

Example

```
City

↓

Pune

Mumbai

Delhi
```

Using OneHotEncoder

```python
categorical = ["City"]

numeric = ["Area","Age"]

preprocessor = ColumnTransformer(

[
("cat",
OneHotEncoder(drop="first"),
categorical),

("num",
"passthrough",
numeric)

]
)
```

Pipeline

```python
pipeline = Pipeline([

("preprocess",preprocessor),

("model",LinearRegression())

])

pipeline.fit(X_train,y_train)
```

---

# 10. Correlation Matrix

```python
corr = df.corr(
    numeric_only=True
)

corr
```

Heatmap

```python
plt.figure(figsize=(8,6))

sns.heatmap(

corr,

annot=True,

cmap="coolwarm"

)

plt.show()
```

Look for

```
Correlation > 0.80
```

Possible multicollinearity.

---

# 11. VIF Calculation

```python
from statsmodels.stats.outliers_influence import variance_inflation_factor
```

```python
X_vif = sm.add_constant(X)

vif = pd.DataFrame()

vif["Feature"] = X_vif.columns

vif["VIF"] = [

variance_inflation_factor(

X_vif.values,

i

)

for i in range(X_vif.shape[1])

]

print(vif)
```

Interpretation

```
VIF < 5

Good
```

```
VIF > 10

Investigate
```

---

# 12. Feature Selection using RFE

```python
model = LinearRegression()

rfe = RFE(

model,

n_features_to_select=5

)

rfe.fit(X,y)
```

Selected Features

```python
selected = X.columns[rfe.support_]

selected
```

Ranking

```python
rfe.ranking_
```

---

# 13. Sequential Feature Selection

```python
from sklearn.feature_selection import SequentialFeatureSelector
```

Forward Selection

```python
sfs = SequentialFeatureSelector(

LinearRegression(),

n_features_to_select=5,

direction="forward"

)

sfs.fit(X,y)
```

Selected Features

```python
X.columns[sfs.get_support()]
```

Backward Selection

```python
direction="backward"
```

---

# 14. Polynomial Features

```python
poly = PolynomialFeatures(

degree=2,

include_bias=False

)
```

Transform

```python
X_poly = poly.fit_transform(X)
```

Feature Names

```python
poly.get_feature_names_out()
```

---

# 15. Interaction Features

Only interaction terms

```python
PolynomialFeatures(

degree=2,

interaction_only=True,

include_bias=False

)
```

Generated Features

```
Area × Bedrooms

Area × Age

Bedrooms × Parking
```

Useful when one feature modifies another feature's effect.

---

# 16. Statsmodels Summary

```python
X_sm = sm.add_constant(X)

model = sm.OLS(

y,

X_sm

).fit()
```

Summary

```python
print(model.summary())
```

Important Outputs

- Coefficients
- p-values
- t-statistics
- F-statistic
- R²
- Adjusted R²
- Confidence Interval
- AIC
- BIC

---

# 17. Ridge Regression

```python
ridge = Ridge(

alpha=1.0

)

ridge.fit(

X_train,

y_train

)
```

Prediction

```python
ridge.predict(X_test)
```

---

# 18. Lasso Regression

```python
lasso = Lasso(

alpha=0.1

)

lasso.fit(

X_train,

y_train

)
```

Coefficients

```python
lasso.coef_
```

Some coefficients may become

```
0
```

---

# 19. Elastic Net

```python
elastic = ElasticNet(

alpha=0.1,

l1_ratio=0.5

)

elastic.fit(

X_train,

y_train

)
```

Prediction

```python
elastic.predict(X_test)
```

---

# 20. Model Comparison

| Model | Advantages | Best Use Case |
|--------|------------|---------------|
| Linear Regression | Simple & Interpretable | Baseline Model |
| Ridge | Handles Multicollinearity | Correlated Features |
| Lasso | Feature Selection | High-Dimensional Data |
| Elastic Net | L1 + L2 | Many Correlated Features |

Compare Scores

```python
print(r2_score(y_test,y_pred))
```

Compare RMSE

```python
np.sqrt(

mean_squared_error(

y_test,

y_pred

))
```

---

# 21. Complete Workflow

```
Load Dataset

↓

EDA

↓

Identify Numeric & Categorical Features

↓

Encode Categorical Variables

↓

Train-Test Split

↓

Train Multiple Linear Regression

↓

Check VIF

↓

Remove Multicollinearity

↓

Feature Selection

↓

Evaluate Model

↓

Compare Ridge, Lasso & Elastic Net

↓

Select Best Model

↓

Save Model

↓

Deployment
```

---

# 22. Best Practices

- Remove duplicate features.
- Check multicollinearity using VIF.
- Use `drop='first'` for One-Hot Encoding.
- Standardize data before Ridge/Lasso/Elastic Net.
- Compare multiple regression models.
- Validate using Cross Validation.
- Interpret coefficients carefully.
- Keep the model as simple as possible.

---

# 23. Interview Questions

## Beginner

1. How do you build a Multiple Linear Regression model in Scikit-learn?
2. How do you retrieve regression coefficients?
3. How do you encode categorical variables?
4. Why use `drop='first'` in OneHotEncoder?
5. How do you predict new observations?

---

## Intermediate

1. How do you calculate VIF in Python?
2. Explain RFE.
3. Explain Sequential Feature Selection.
4. Why use Statsmodels with Scikit-learn?
5. How do you compare multiple regression models?

---

## Advanced

1. How would you build a complete regression pipeline?
2. Why standardize features before Ridge Regression?
3. How would you identify insignificant variables?
4. Explain coefficient interpretation after One-Hot Encoding.
5. How would you deploy a Multiple Linear Regression model?

---

# 24. Summary

- Multiple Linear Regression in Python follows the same workflow as Simple Linear Regression but supports multiple predictors.
- Categorical variables must be encoded before training.
- **VIF**, **Correlation Matrix**, and **Statsmodels** are essential tools for diagnosing regression models.
- Feature selection techniques such as **RFE** and **Sequential Feature Selection** help improve model simplicity and generalization.
- **Ridge**, **Lasso**, and **Elastic Net** extend Multiple Linear Regression by addressing multicollinearity and overfitting.
- Pipelines simplify preprocessing and model deployment while ensuring reproducibility.

---

# Key Takeaways

- **Use `LinearRegression()` for the baseline model.**
- **Encode categorical variables using `OneHotEncoder(drop="first")`.**
- **Always check multicollinearity using VIF.**
- **Use Statsmodels for statistical interpretation and Scikit-learn for machine learning workflows.**
- **RFE and Sequential Feature Selection help identify important predictors.**
- **Standardize features before applying Ridge, Lasso, or Elastic Net.**
- **Compare multiple models before choosing the final solution.**
- **A well-designed preprocessing pipeline is essential for production-ready regression models.**
