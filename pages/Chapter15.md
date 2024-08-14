# Chapter: Simple Linear Regression

## Introduction

Simple linear regression is a statistical method used to model the relationship between two continuous variables. One variable, known as the independent variable (or predictor), is used to predict the value of the other variable, known as the dependent variable (or response). The relationship is modeled as a linear equation, and the goal is to find the best-fitting line that minimizes the difference between the observed and predicted values.

## Key Concepts

1. **Independent Variable (X)**: The variable used to predict the dependent variable. It is also known as the predictor or explanatory variable.
2. **Dependent Variable (Y)**: The variable being predicted. It is also known as the response or outcome variable.
3. **Linear Equation**: The relationship between X and Y is modeled by the linear equation:
   
   $Y = \beta_0 + \beta_1 X + \epsilon$
   
   where:
   - $\beta_0$ is the intercept (the value of Y when X = 0),
   - $\beta_1$ is the slope (the change in Y for a one-unit change in X),
   - $\epsilon$ is the error term (the difference between the observed and predicted values).

5. **Objective**: The objective of simple linear regression is to estimate the values of \(\beta_0\) and \(\beta_1\) that minimize the sum of squared errors (SSE) between the observed and predicted values of Y.

## Example in Python

Let's explore how to perform simple linear regression using Python's `scikit-learn` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
import matplotlib.pyplot as plt
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Sample data: hours studied (X) and test scores (Y)
np.random.seed(42)
X = np.random.rand(100, 1) * 10  # Hours studied
Y = 2.5 * X + np.random.randn(100, 1) * 2 + 20  # Test scores with some noise

# Create a linear regression model
model = LinearRegression()

# Fit the model to the data
model.fit(X, Y)

# Make predictions
Y_pred = model.predict(X)

# Model parameters
intercept = model.intercept_[0]
slope = model.coef_[0][0]

# Calculate metrics
mse = mean_squared_error(Y, Y_pred)
r2 = r2_score(Y, Y_pred)

print(f"Intercept (β₀): {intercept:.2f}")
print(f"Slope (β₁): {slope:.2f}")
print(f"Mean Squared Error (MSE): {mse:.2f}")
print(f"R-squared (R²): {r2:.2f}")

# Plot the data and the regression line
plt.scatter(X, Y, color='blue', label='Observed data')
plt.plot(X, Y_pred, color='red', label='Regression line')
plt.title("Simple Linear Regression")
plt.xlabel("Hours Studied")
plt.ylabel("Test Score")
plt.legend()
plt.show()
```

### Explanation

- **Sample Data**: We generate 100 data points representing hours studied (X) and test scores (Y). The relationship between X and Y is linear, with some added noise.
- **Model Fitting**: We fit a simple linear regression model using `LinearRegression` from `scikit-learn`.
- **Model Parameters**: The intercept (\(\beta_0\)) and slope (\(\beta_1\)) are printed, representing the estimated values of the linear equation.
- **Model Evaluation**: We calculate the mean squared error (MSE) and R-squared (R²) to assess the model's performance.
- **Plotting**: We plot the observed data and the fitted regression line to visualize the relationship.

## Example in R

Let's perform the same simple linear regression analysis using R.

### R Code

```r
# Sample data: hours studied (X) and test scores (Y)
set.seed(42)
X <- runif(100, min=0, max=10)  # Hours studied
Y <- 2.5 * X + rnorm(100, mean=0, sd=2) + 20  # Test scores with some noise

# Fit a linear regression model
model <- lm(Y ~ X)

# Model summary
summary(model)

# Extract model parameters
intercept <- coef(model)[1]
slope <- coef(model)[2]

# Calculate Mean Squared Error (MSE) and R-squared (R²)
mse <- mean(model$residuals^2)
r_squared <- summary(model)$r.squared

cat("Intercept (β₀):", round(intercept, 2), "\n")
cat("Slope (β₁):", round(slope, 2), "\n")
cat("Mean Squared Error (MSE):", round(mse, 2), "\n")
cat("R-squared (R²):", round(r_squared, 2), "\n")

# Plot the data and the regression line
plot(X, Y, main="Simple Linear Regression", xlab="Hours Studied", ylab="Test Score", pch=19, col="blue")
abline(model, col="red", lwd=2)
```

### Explanation

- **Sample Data**: We generate 100 data points representing hours studied (X) and test scores (Y) using `runif()` and `rnorm()` functions.
- **Model Fitting**: We fit a simple linear regression model using the `lm()` function.
- **Model Summary**: The `summary()` function provides detailed information about the model, including the coefficients, R-squared value, and significance of the model.
- **Model Parameters**: The intercept (\(\beta_0\)) and slope (\(\beta_1\)) are extracted and printed.
- **Model Evaluation**: We calculate the mean squared error (MSE) and R-squared (R²) to assess the model's performance.
- **Plotting**: We plot the observed data and the fitted regression line to visualize the relationship.

## Interpreting the Results

### Model Parameters

- **Intercept (\(\beta_0\))**: The intercept represents the predicted value of the dependent variable (Y) when the independent variable (X) is zero. In the context of the example, it represents the predicted test score when no hours are studied.
- **Slope (\(\beta_1\))**: The slope represents the change in the dependent variable (Y) for a one-unit change in the independent variable (X). In the example, it indicates how much the test score increases for each additional hour studied.

### Model Evaluation

- **Mean Squared Error (MSE)**: MSE measures the average squared difference between the observed and predicted values. A lower MSE indicates a better fit.
- **R-squared (R²)**: R² represents the proportion of the variance in the dependent variable that is explained by the independent variable. An R² value closer to 1 indicates a better fit.

### Visualization

The scatter plot with the regression line provides a visual representation of the relationship between the independent and dependent variables. The closer the data points are to the regression line, the stronger the linear relationship.

## Applications

Simple linear regression is widely used in various fields:

- **Economics**: To predict consumption based on income, or housing prices based on square footage.
- **Healthcare**: To estimate the effect of a drug dosage on patient recovery time.
- **Marketing**: To assess the impact of advertising spend on sales revenue.

## Conclusion

Simple linear regression is a powerful tool for modeling the relationship between two continuous variables. By understanding the model parameters, evaluating model performance, and visualizing the results, researchers and analysts can make informed predictions and decisions based on their data. Whether in business, science, or social research, simple linear regression provides a foundation for understanding and analyzing linear relationships.
