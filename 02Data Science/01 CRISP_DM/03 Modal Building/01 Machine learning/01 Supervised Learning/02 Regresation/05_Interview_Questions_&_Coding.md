# 05_Interview_Questions_&_Coding.md

> **Level:** Beginner → Advanced
>
> **Purpose:** Complete interview preparation for Simple Linear Regression covering theory, coding, mathematics, statistics, business scenarios, SQL integration, and frequently asked company questions.

---

# Table of Contents

1. Beginner Interview Questions
2. Intermediate Interview Questions
3. Advanced Interview Questions
4. Mathematical Questions
5. Statistics Questions
6. Business Scenario Questions
7. Coding Questions
8. Python Coding Questions
9. SQL + Regression Questions
10. Case Studies
11. Frequently Asked Company Questions
12. Rapid Fire Questions
13. Quick Revision

---

# 1. Beginner Interview Questions

## Fundamentals

1. What is Machine Learning?
2. What is Supervised Learning?
3. What is Regression?
4. Difference between Regression and Classification.
5. What is Simple Linear Regression?
6. What is the objective of Linear Regression?
7. Give real-world applications of Linear Regression.
8. What are dependent and independent variables?
9. What is the target variable?
10. What is a feature?
11. What is a regression line?
12. What is the Best Fit Line?
13. What is prediction?
14. Explain slope.
15. Explain intercept.
16. Write the equation of Simple Linear Regression.
17. Can Linear Regression work with categorical variables?
18. How many independent variables are present in Simple Linear Regression?
19. What type of output does Linear Regression predict?
20. What is a continuous variable?

---

# 2. Intermediate Interview Questions

## Model Building

1. How does Linear Regression work?
2. How is the Best Fit Line calculated?
3. What is Ordinary Least Squares (OLS)?
4. Why do we minimize SSE?
5. Why are errors squared?
6. What is a cost function?
7. Explain Mean Squared Error.
8. What is Gradient Descent?
9. Why is Gradient Descent used?
10. Explain learning rate.
11. What happens if the learning rate is too high?
12. What happens if it is too low?
13. Difference between Batch GD, SGD and Mini-Batch GD.
14. What is the Normal Equation?
15. Difference between OLS and Gradient Descent.

---

# 3. Advanced Interview Questions

1. Explain the mathematical derivation of OLS.
2. Why is Linear Regression sensitive to outliers?
3. Explain the Gauss-Markov theorem.
4. What is Maximum Likelihood Estimation (MLE)?
5. Difference between OLS and MLE.
6. Explain Bias-Variance Tradeoff.
7. Why does Linear Regression fail for non-linear data?
8. Explain residual analysis.
9. Why should residuals be normally distributed?
10. Explain heteroscedasticity.
11. Explain homoscedasticity.
12. Explain autocorrelation.
13. Explain multicollinearity.
14. Why doesn't multicollinearity affect Simple Linear Regression?
15. What happens when assumptions are violated?
16. Explain confidence intervals.
17. Explain prediction intervals.
18. Explain p-value.
19. Explain t-test.
20. Explain F-test.

---

# 4. Mathematical Questions

1. Derive the equation of the regression line.
2. Derive the OLS solution.
3. Derive the cost function.
4. Calculate SSE manually.
5. Calculate MSE manually.
6. Calculate RMSE manually.
7. Calculate MAE manually.
8. Calculate R² manually.
9. Calculate Adjusted R².
10. Find the regression equation from a dataset.
11. Calculate slope manually.
12. Calculate intercept manually.
13. Explain why squared error is used.
14. Explain gradient calculation.
15. Derive Gradient Descent update rule.

---

# 5. Statistics Questions

1. What are LINE assumptions?
2. Explain Linearity.
3. Explain Independence.
4. Explain Normality.
5. Explain Equal Variance.
6. What are residuals?
7. What is residual variance?
8. Explain QQ Plot.
9. Explain Residual Plot.
10. Explain Cook's Distance.
11. Explain Leverage Points.
12. Explain Influential Points.
13. Explain Durbin-Watson Test.
14. Explain VIF.
15. Explain hypothesis testing.

---

# 6. Business Scenario Questions

### Scenario 1

Sales increase every month with increasing advertisement budget.

Would you use Linear Regression?

Why?

---

### Scenario 2

House prices increase exponentially.

Will Linear Regression perform well?

What would you use instead?

---

### Scenario 3

The model has

```
Training R² = 0.99

Testing R² = 0.58
```

What is happening?

---

### Scenario 4

Residual plot shows a curve.

What assumption is violated?

---

### Scenario 5

Residual variance increases continuously.

Identify the problem.

---

### Scenario 6

One observation changes the regression line significantly.

What is this observation called?

---

### Scenario 7

The p-value of a feature is

```
0.78
```

Should it remain in the model?

---

### Scenario 8

Your dataset has missing values and outliers.

Describe your preprocessing pipeline.

---

### Scenario 9

The business wants predictions that are easy to explain to management.

Would you choose Linear Regression?

Why?

---

### Scenario 10

You have only one predictor but the relationship is curved.

Which model would you recommend?

---

# 7. Coding Questions

## Easy

1. Load a CSV file.
2. Display first five rows.
3. Find missing values.
4. Remove duplicates.
5. Create a scatter plot.
6. Find correlation.
7. Split dataset.
8. Train Linear Regression model.
9. Predict new values.
10. Print slope and intercept.

---

## Intermediate

11. Calculate MAE.
12. Calculate MSE.
13. Calculate RMSE.
14. Calculate R².
15. Plot regression line.
16. Plot residuals.
17. Perform Cross Validation.
18. Save model using Joblib.
19. Load saved model.
20. Predict using loaded model.

---

## Advanced

21. Implement Linear Regression without Scikit-learn.
22. Implement Gradient Descent from scratch.
23. Implement OLS manually.
24. Build a regression pipeline.
25. Compare Linear Regression with Polynomial Regression.
26. Detect outliers using IQR.
27. Detect leverage points.
28. Generate residual plots.
29. Calculate confidence intervals.
30. Perform complete model diagnostics.

---

# 8. Python Coding Questions

### NumPy

1. Create arrays.
2. Matrix multiplication.
3. Matrix transpose.
4. Mean calculation.
5. Variance calculation.

---

### Pandas

1. Read CSV.
2. Handle missing values.
3. Drop duplicates.
4. Rename columns.
5. GroupBy operations.

---

### Matplotlib

1. Scatter Plot
2. Line Plot
3. Histogram
4. Box Plot
5. Residual Plot

---

### Scikit-learn

1. Train model
2. Predict values
3. Evaluate model
4. Cross Validation
5. Pipeline

---

# 9. SQL + Regression Questions

1. Find duplicate records.
2. Remove duplicate rows.
3. Replace NULL values.
4. Calculate average salary.
5. Find maximum salary.
6. Find minimum salary.
7. Calculate yearly growth.
8. Rank employees by salary.
9. Write INNER JOIN queries.
10. Write LEFT JOIN queries.
11. Explain Window Functions.
12. Explain CTE.
13. Find top 5 records.
14. Aggregate sales by month.
15. Prepare data for regression analysis.

---

# 10. Case Studies

## Salary Prediction

Predict salary based on years of experience.

---

## House Price Prediction

Predict price using area.

---

## Sales Prediction

Predict sales using advertising budget.

---

## Demand Forecasting

Predict future demand using historical sales.

---

## Temperature Prediction

Predict temperature using historical weather data.

---

## Fuel Consumption

Predict fuel usage using distance traveled.

---

## Insurance Cost Prediction

Predict insurance premium using age.

---

# 11. Frequently Asked Company Questions

## TCS

- Explain Linear Regression.
- Explain OLS.
- Difference between MAE and RMSE.
- Explain R².

---

## Infosys

- Cost Function
- Gradient Descent
- Regression Equation
- Cross Validation

---

## Capgemini

- Residual Analysis
- Train-Test Split
- Overfitting
- Underfitting

---

## Cognizant

- Linear Regression Assumptions
- p-value
- t-Test
- F-Test

---

## Deloitte

- Business Interpretation
- Feature Engineering
- Model Evaluation
- Regression Metrics

---

## Accenture

- Cross Validation
- Feature Selection
- Outlier Handling
- Practical Case Study

---

## EY

- Regression Diagnostics
- Confidence Interval
- Prediction Interval
- Business Scenarios

---

## Walmart Global Tech

- Large Dataset Regression
- Feature Engineering
- Deployment
- Explainability

---

## Amazon

- OLS Derivation
- Gradient Descent
- Coding from Scratch
- Bias-Variance Tradeoff
- Statistical Interpretation

---

## Microsoft

- Regression Mathematics
- Optimization
- Residual Analysis
- System Design around ML Models

---

# 12. Rapid Fire Questions

1. Difference between regression and classification.
2. Difference between MAE and RMSE.
3. Difference between MSE and RMSE.
4. Difference between R² and Adjusted R².
5. Difference between OLS and Gradient Descent.
6. Difference between Confidence Interval and Prediction Interval.
7. Difference between Homoscedasticity and Heteroscedasticity.
8. Difference between Training Error and Testing Error.
9. Difference between Bias and Variance.
10. Difference between Underfitting and Overfitting.
11. Difference between Correlation and Regression.
12. Difference between Covariance and Correlation.
13. Difference between Scatter Plot and Regression Plot.
14. Difference between Residual and Error.
15. Difference between Cross Validation and Train-Test Split.

---

# 13. Quick Revision

## Important Formulae

### Regression Equation

```
Ŷ = β₀ + β₁X
```

---

### Residual

```
Residual = Actual − Predicted
```

---

### MAE

```
Σ|Actual − Predicted| / n
```

---

### MSE

```
Σ(Actual − Predicted)² / n
```

---

### RMSE

```
√MSE
```

---

### R²

```
1 − (RSS / TSS)
```

---

## Remember

- Linear Regression predicts **continuous values**.
- OLS minimizes the **Sum of Squared Errors (SSE)**.
- Lower **MAE**, **MSE**, and **RMSE** indicate better performance.
- Higher **R²** and **Adjusted R²** indicate a better fit.
- Residuals should be **random**, **independent**, and **normally distributed**.
- Always verify the **LINE assumptions** before interpreting the model.
- Use **Cross Validation** to estimate generalization performance.
- Handle **missing values**, **outliers**, and **data quality issues** before model training.
- Interpret results in the context of the business problem, not just the evaluation metrics.
