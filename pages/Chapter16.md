# Chapter: Multiple Linear Regression

## Introduction

Multiple linear regression is an extension of simple linear regression that models the relationship between a dependent variable and two or more independent variables. This technique is used to understand how multiple predictors influence the outcome variable and to make predictions based on the combined effect of these predictors.

## Key Concepts

1. **Dependent Variable (Y)**: The variable that you are trying to predict or explain, also known as the response or outcome variable.
2. **Independent Variables (X1, X2, ..., Xn)**: The variables used to predict the dependent variable, also known as predictors, features, or explanatory variables.
3. **Linear Equation**: The relationship between the dependent and independent variables is modeled by the linear equation:
   
   $Y = \beta_0 + \beta_1 X_1 + \beta_2 X_2 + \ldots + \beta_n X_n + \epsilon$
   
   where:
   - $\beta_0$ is the intercept (the value of Y when all \(X_i\) = 0),
   - $\beta_1, \beta_2, \ldots, \beta_n$ are the coefficients (the change in Y for a one-unit change in \(X_i\)),
   - $\epsilon$ is the error term (the difference between the observed and predicted values).

4. **Objective**: The objective of multiple linear regression is to estimate the values of \(\beta_0, \beta_1, \ldots, \beta_n\) that minimize the sum of squared errors (SSE) between the observed and predicted values of Y.

## Example in Python

Let's explore how to perform multiple linear regression using Python's `scikit-learn` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Sample data: hours studied, hours slept, and test scores
np.random.seed(42)
data = pd.DataFrame({
    'Hours_Studied': np.random.rand(100) * 10,
    'Hours_Slept': np.random.rand(100) * 8 + 2
})
data['Test_Score'] = 3 + 2.5 * data['Hours_Studied'] + 1.5 * data['Hours_Slept'] + np.random.randn(100) * 2

# Independent variables (X) and dependent variable (Y)
X = data[['Hours_Studied', 'Hours_Slept']]
Y = data['Test_Score']

# Create a multiple linear regression model
model = LinearRegression()

# Fit the model to the data
model.fit(X, Y)

# Make predictions
Y_pred = model.predict(X)

# Model parameters
intercept = model.intercept_
coefficients = model.coef_

# Calculate metrics
mse = mean_squared_error(Y, Y_pred)
r2 = r2_score(Y, Y_pred)

print(f"Intercept (β₀): {intercept:.2f}")
print(f"Coefficients (β₁, β₂): {coefficients}")
print(f"Mean Squared Error (MSE): {mse:.2f}")
print(f"R-squared (R²): {r2:.2f}")

# Plotting actual vs predicted values
plt.scatter(Y, Y_pred, color='blue')
plt.plot([Y.min(), Y.max()], [Y.min(), Y.max()], 'k--', lw=2)
plt.xlabel("Actual Test Score")
plt.ylabel("Predicted Test Score")
plt.title("Actual vs Predicted Test Scores")
plt.show()
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied, hours slept, and test scores. The test scores are modeled as a linear combination of hours studied and hours slept, with some added noise.
- **Model Fitting**: We fit a multiple linear regression model using `LinearRegression` from `scikit-learn`.
- **Model Parameters**: The intercept (\(\beta_0\)) and coefficients (\(\beta_1, \beta_2\)) are printed, representing the estimated values of the linear equation.
- **Model Evaluation**: We calculate the mean squared error (MSE) and R-squared (R²) to assess the model's performance.
- **Visualization**: We plot the actual vs. predicted test scores to visualize the model's accuracy.

## Example in R

Let's perform the same multiple linear regression analysis using R.

### R Code

```r
# Load necessary library
library(ggplot2)

# Sample data: hours studied, hours slept, and test scores
set.seed(42)
data <- data.frame(
  Hours_Studied = runif(100, min=0, max=10),
  Hours_Slept = runif(100, min=2, max=10)
)
data$Test_Score <- 3 + 2.5 * data$Hours_Studied + 1.5 * data$Hours_Slept + rnorm(100, mean=0, sd=2)

# Fit a multiple linear regression model
model <- lm(Test_Score ~ Hours_Studied + Hours_Slept, data=data)

# Model summary
summary(model)

# Extract model parameters
intercept <- coef(model)[1]
coefficients <- coef(model)[-1]

# Calculate Mean Squared Error (MSE) and R-squared (R²)
mse <- mean(model$residuals^2)
r_squared <- summary(model)$r.squared

cat("Intercept (β₀):", round(intercept, 2), "\n")
cat("Coefficients (β₁, β₂):", round(coefficients, 2), "\n")
cat("Mean Squared Error (MSE):", round(mse, 2), "\n")
cat("R-squared (R²):", round(r_squared, 2), "\n")

# Plotting actual vs predicted values
data$Predicted_Score <- predict(model, data)
ggplot(data, aes(x=Test_Score, y=Predicted_Score)) +
  geom_point(color="blue") +
  geom_abline(slope=1, intercept=0, linetype="dashed", color="red") +
  labs(title="Actual vs Predicted Test Scores", x="Actual Test Score", y="Predicted Test Score") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied, hours slept, and test scores using `runif()` and `rnorm()` functions.
- **Model Fitting**: We fit a multiple linear regression model using the `lm()` function.
- **Model Summary**: The `summary()` function provides detailed information about the model, including the coefficients, R-squared value, and significance of the model.
- **Model Parameters**: The intercept (\(\beta_0\)) and coefficients (\(\beta_1, \beta_2\)) are extracted and printed.
- **Model Evaluation**: We calculate the mean squared error (MSE) and R-squared (R²) to assess the model's performance.
- **Visualization**: We plot the actual vs. predicted test scores using `ggplot2` to visualize the model's accuracy.

## Interpreting the Results

### Model Parameters

- **Intercept (\(\beta_0\))**: The intercept represents the predicted value of the dependent variable (Y) when all independent variables (X) are zero. In the context of the example, it represents the predicted test score when no hours are studied or slept.
- **Coefficients (\(\beta_1, \beta_2\))**: The coefficients represent the change in the dependent variable (Y) for a one-unit change in each independent variable (X), holding all other variables constant. In the example, \(\beta_1\) indicates how much the test score increases for each additional hour studied, and \(\beta_2\) indicates how much the test score increases for each additional hour slept.

### Model Evaluation

- **Mean Squared Error (MSE)**: MSE measures the average squared difference between the observed and predicted values. A lower MSE indicates a better fit.
- **R-squared (R²)**: R² represents the proportion of the variance in the dependent variable that is explained by the independent variables. An R² value closer to 1 indicates a better fit.

### Visualization

The plot of actual vs. predicted values provides a visual representation of the model's accuracy. If the model fits the data well, the points should lie close to the diagonal line where the actual and predicted values are equal.

## Applications

Multiple linear regression is widely used in various fields:

- **Economics**: To predict economic outcomes based on multiple factors, such as income, education, and age.
- **Healthcare**: To estimate the effect of multiple factors, such as diet, exercise, and medication, on patient outcomes.
- **Marketing**: To assess the impact of various marketing strategies, such as advertising spend, price, and distribution channels, on sales revenue.

## Conclusion

Multiple linear regression is a powerful tool for modeling the relationship between a dependent variable and multiple independent variables. By understanding the model parameters, evaluating model performance, and visualizing the results, researchers and analysts can make informed predictions and decisions based on their data. Whether in business, science, or social research, multiple linear regression provides a comprehensive framework for understanding and analyzing complex relationships between variables.
