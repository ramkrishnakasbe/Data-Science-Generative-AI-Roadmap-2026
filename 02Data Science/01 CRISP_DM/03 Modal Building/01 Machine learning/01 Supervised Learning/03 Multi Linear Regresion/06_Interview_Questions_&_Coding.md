# 06_Interview_Questions_&_Coding.md

> **Level:** Beginner → Advanced
>
> **Goal:** Prepare for Data Scientist, ML Engineer, Data Analyst, AI Engineer, and MLE interviews covering **Multiple Linear Regression**. This file focuses only on concepts **not already covered in the Simple Linear Regression Interview Notes**.

---

# Table of Contents

1. Beginner Interview Questions
2. Intermediate Interview Questions
3. Advanced Interview Questions
4. Feature Engineering Questions
5. Multicollinearity Questions
6. Model Selection Questions
7. Regularization Questions
8. Business Scenario Questions
9. Coding Questions
10. Python Coding Questions
11. SQL Scenario Questions
12. Case Studies
13. Company-wise Interview Questions
14. Rapid Fire Questions
15. Quick Revision

---

# 1. Beginner Interview Questions

1. What is Multiple Linear Regression?
2. Difference between Simple and Multiple Linear Regression.
3. Why do we use Multiple Linear Regression?
4. What is a predictor variable?
5. What is a regression coefficient?
6. Explain the regression equation.
7. What is an intercept?
8. Why does Multiple Linear Regression usually perform better than Simple Linear Regression?
9. Can Multiple Linear Regression handle categorical variables?
10. What is the meaning of "holding other variables constant"?
11. What is a partial regression coefficient?
12. What is a hyperplane?
13. How many independent variables are required for Multiple Linear Regression?
14. Explain matrix representation.
15. Give some real-world applications of Multiple Linear Regression.

---

# 2. Intermediate Interview Questions

1. What is Multicollinearity?
2. Why is Multicollinearity a problem?
3. How do you detect Multicollinearity?
4. What is VIF?
5. What is Tolerance?
6. Explain the Dummy Variable Trap.
7. Difference between Label Encoding and One-Hot Encoding.
8. What is the reference category?
9. Explain interaction terms.
10. Explain polynomial features.
11. Difference between correlation and multicollinearity.
12. Why is Adjusted R² preferred over R²?
13. Explain Forward Selection.
14. Explain Backward Elimination.
15. Explain Stepwise Regression.
16. Explain Recursive Feature Elimination.
17. Explain Sequential Feature Selection.
18. What is Best Subset Selection?
19. Explain Condition Number.
20. Explain Eigenvalues in Multicollinearity.

---

# 3. Advanced Interview Questions

1. Why does Multicollinearity affect coefficients but not always predictions?
2. Explain the mathematical intuition behind VIF.
3. What happens if two variables are perfectly correlated?
4. How do interaction terms affect coefficient interpretation?
5. Explain nested models.
6. Explain Partial F-Test.
7. Difference between AIC and BIC.
8. Explain Mallows' Cp.
9. Explain PRESS Statistic.
10. Why does Lasso perform feature selection?
11. Why does Ridge not eliminate features?
12. Explain Elastic Net mathematically.
13. Explain Bias-Variance Tradeoff in MLR.
14. Why is feature scaling important for Regularization?
15. How would you build an interpretable regression model?

---

# 4. Feature Engineering Questions

1. How do you create interaction features?
2. What are polynomial features?
3. When should polynomial features be used?
4. Difference between Feature Selection and Feature Extraction.
5. Difference between Feature Engineering and Feature Selection.
6. How do you identify redundant features?
7. How do you handle high-cardinality categorical variables?
8. Why should ID columns be removed?
9. Explain feature construction with examples.
10. When should you transform variables?

---

# 5. Multicollinearity Questions

1. Explain VIF with an example.
2. What VIF value is acceptable?
3. Can a high correlation always imply Multicollinearity?
4. How do you reduce Multicollinearity?
5. Should every variable with high VIF be removed?
6. Explain Correlation Matrix vs VIF.
7. Explain Tolerance.
8. Explain Condition Number.
9. Explain Dummy Variable Trap using VIF.
10. Explain Multicollinearity in business terms.

---

# 6. Model Selection Questions

1. Why isn't R² enough?
2. Difference between R² and Adjusted R².
3. Difference between AIC and BIC.
4. Explain Partial F-Test.
5. What is a nested model?
6. How do you compare two regression models?
7. Which metric would you use in production?
8. What is overfitting in regression?
9. How do you detect overfitting?
10. Explain model complexity.

---

# 7. Regularization Questions

1. Why is Regularization required?
2. Difference between Ridge and Lasso.
3. Difference between L1 and L2 penalty.
4. Explain Elastic Net.
5. Why does Ridge reduce coefficient values?
6. Why does Lasso perform feature selection?
7. What is lambda (λ)?
8. What happens when lambda becomes very large?
9. What happens when lambda becomes zero?
10. When should Elastic Net be preferred?

---

# 8. Business Scenario Questions

## Scenario 1

You have **35 predictors**.

Many have

```
VIF > 15
```

What would you do?

---

## Scenario 2

Adding five new features increases

```
Adjusted R²

↓

decreases
```

Would you keep them?

Why?

---

## Scenario 3

OneHotEncoding creates

```
Gender

↓

Male

Female
```

Why should one column be removed?

---

## Scenario 4

Two regression models

```
Model A

Adj R² = 0.91

AIC = 540
```

```
Model B

Adj R² = 0.90

AIC = 510
```

Which model would you choose?

---

## Scenario 5

Lasso removed

```
Experience
```

Should you always accept the result?

---

## Scenario 6

A business manager asks

> Which variable impacts salary the most?

How would you answer?

---

## Scenario 7

You have

```
500 Features

5000 Records
```

Which feature-selection technique would you use?

---

## Scenario 8

Training Accuracy

```
98%
```

Testing Accuracy

```
79%
```

What is happening?

---

## Scenario 9

The model performs well,

but coefficients keep changing after every retraining.

What is the likely cause?

---

## Scenario 10

The dataset contains

```
1000 Cities
```

Would you use One-Hot Encoding?

Why?

---

# 9. Coding Questions

## Beginner

1. Train a Multiple Linear Regression model.
2. Print coefficients.
3. Predict new observations.
4. Display feature importance.
5. Calculate Adjusted R².
6. Perform One-Hot Encoding.
7. Drop the first dummy variable.
8. Calculate Correlation Matrix.
9. Build a regression pipeline.
10. Save the trained model.

---

## Intermediate

11. Calculate VIF.
12. Perform RFE.
13. Perform Forward Selection.
14. Perform Backward Selection.
15. Build Polynomial Features.
16. Create Interaction Features.
17. Compare Ridge and Lasso.
18. Use Elastic Net.
19. Print Statsmodels summary.
20. Compare AIC and BIC.

---

## Advanced

21. Build a complete regression pipeline.
22. Detect Multicollinearity automatically.
23. Implement feature selection pipeline.
24. Optimize alpha using GridSearchCV.
25. Compare four regression models.
26. Interpret coefficients automatically.
27. Build reusable preprocessing functions.
28. Perform Cross Validation.
29. Deploy the regression model.
30. Build an end-to-end prediction system.

---

# 10. Python Coding Questions

### Pandas

- Detect categorical variables.
- Encode categories.
- Create interaction columns.
- Remove highly correlated variables.
- Create polynomial features.

---

### NumPy

- Matrix multiplication.
- Matrix inversion.
- Dot product.
- Transpose.
- Vectorized prediction.

---

### Scikit-learn

- LinearRegression
- Ridge
- Lasso
- ElasticNet
- RFE
- Pipeline
- ColumnTransformer
- PolynomialFeatures

---

### Statsmodels

- OLS
- Summary
- p-values
- Confidence Interval
- AIC
- BIC

---

# 11. SQL Scenario Questions

1. Find highly correlated business features.
2. Create interaction features using SQL.
3. Convert categorical variables.
4. Aggregate monthly sales by city.
5. Prepare regression-ready datasets.
6. Remove duplicate features.
7. Calculate average customer value.
8. Handle missing values.
9. Create feature tables.
10. Build a dataset for regression.

---

# 12. Case Studies

## House Price Prediction

Features

- Area
- Bedrooms
- Bathrooms
- Parking
- Location

---

## Salary Prediction

Features

- Experience
- Education
- Skill Score
- Certifications
- Company Rating

---

## Loan Amount Prediction

Features

- Income
- Age
- Credit Score
- Employment
- Existing Loans

---

## Medical Insurance Cost

Features

- Age
- BMI
- Smoking
- Region
- Children

---

## Sales Prediction

Features

- TV Ads
- Radio Ads
- Social Media Spend
- Festival
- Discounts

---

## Manufacturing Cost Prediction

Features

- Raw Material Cost
- Labor Cost
- Machine Hours
- Electricity
- Transportation

---

# 13. Company-wise Interview Questions

## Amazon

- Explain VIF mathematically.
- Ridge vs Lasso.
- Feature Engineering.
- Regression Pipeline.
- High-dimensional datasets.

---

## Microsoft

- Matrix Representation.
- Feature Selection.
- Regularization.
- Model Comparison.
- Production Deployment.

---

## Google

- Multicollinearity.
- AIC/BIC.
- Polynomial Features.
- Cross Validation.
- End-to-End ML Pipeline.

---

## Deloitte

- Business interpretation.
- Regression diagnostics.
- Dummy Variable Trap.
- Feature Engineering.
- Client explanation.

---

## Accenture

- OneHotEncoding.
- Feature Selection.
- Ridge Regression.
- Model Evaluation.
- Business Scenarios.

---

## TCS / Infosys / Cognizant

- VIF
- RFE
- Adjusted R²
- Ridge vs Lasso
- Practical Coding

---

# 14. Rapid Fire Questions

1. R² vs Adjusted R²
2. Ridge vs Lasso
3. Ridge vs Elastic Net
4. AIC vs BIC
5. Correlation vs Multicollinearity
6. Feature Selection vs Feature Engineering
7. Label Encoding vs One-Hot Encoding
8. Forward vs Backward Selection
9. Wrapper vs Filter Methods
10. Dummy Variable vs One-Hot Encoding
11. VIF vs Tolerance
12. PRESS vs Cross Validation
13. Polynomial Features vs Interaction Features
14. Nested Model vs Full Model
15. L1 vs L2 Penalty

---

# 15. Quick Revision

## Important Thresholds

| Metric | Good Value |
|---------|------------|
| Correlation | < 0.80 |
| VIF | < 5 |
| Tolerance | > 0.20 |
| Condition Number | < 30 |
| p-value | < 0.05 |
| Adjusted R² | Higher |
| AIC | Lower |
| BIC | Lower |

---

## Remember

- Multiple Linear Regression extends Simple Linear Regression by using **multiple predictors**.
- Interpret each coefficient **while holding all other variables constant**.
- **Always check VIF before interpreting coefficients.**
- Use **One-Hot Encoding** for nominal variables and **Label Encoding** for ordinal variables.
- Avoid the **Dummy Variable Trap** by dropping one dummy column.
- Use **Adjusted R²**, **AIC**, and **BIC** for model comparison.
- **Ridge** handles multicollinearity, **Lasso** performs feature selection, and **Elastic Net** combines both.
- A good regression model is **accurate, simple, interpretable, and generalizes well**.
