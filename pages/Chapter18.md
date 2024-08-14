# Chapter: Polynomial Regression

## Introduction

Polynomial regression is a type of regression analysis in which the relationship between the independent variable \(X\) and the dependent variable \(Y\) is modeled as an nth degree polynomial. Unlike simple linear regression, which assumes a linear relationship, polynomial regression can capture non-linear relationships between variables by fitting a curve to the data.

## Key Concepts

1. **Polynomial Equation**: In polynomial regression, the relationship between the dependent variable \(Y\) and the independent variable \(X\) is represented by a polynomial equation of degree \(n\):

   $Y = \beta_0 + \beta_1 X + \beta_2 X^2 + \ldots + \beta_n X^n + \epsilon$

   where:
   - $\beta_0, \beta_1, \ldots, \beta_n$ are the coefficients of the polynomial,
   - $X^2, X^3, \ldots, X^n$ are the higher-order terms of the independent variable,
   - $\epsilon$ is the error term.

2. **Non-linear Relationships**: Polynomial regression is used when the data shows a curvilinear relationship, which cannot be adequately captured by a simple linear model.

3. **Overfitting**: One of the challenges of polynomial regression is overfitting, especially when using higher-degree polynomials. Overfitting occurs when the model fits the training data very well but fails to generalize to new data.

## Example in Python

Let's explore how to perform polynomial regression using Python's `scikit-learn` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
import matplotlib.pyplot as plt
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error, r2_score

# Sample data: X values and Y values with a quadratic relationship
np.random.seed(42)
X = np.random.rand(100, 1) * 10  # Independent variable
Y = 2 + 1.5 * X + 0.5 * X**2 + np.random.randn(100, 1) * 2  # Dependent variable

# Transform the original features to polynomial features
poly = PolynomialFeatures(degree=2)
X_poly = poly.fit_transform(X)

# Create a linear regression model
model = LinearRegression()

# Fit the model to the polynomial features
model.fit(X_poly, Y)

# Make predictions
Y_pred = model.predict(X_poly)

# Model parameters
intercept = model.intercept_[0]
coefficients = model.coef_[0]

# Calculate metrics
mse = mean_squared_error(Y, Y_pred)
r2 = r2_score(Y, Y_pred)

print(f"Intercept (β₀): {intercept:.2f}")
print(f"Coefficients (β₁, β₂): {coefficients[1:]}")
print(f"Mean Squared Error (MSE): {mse:.2f}")
print(f"R-squared (R²): {r2:.2f}")

# Plot the data and the polynomial regression curve
plt.scatter(X, Y, color='blue', label='Observed data')
plt.plot(X, Y_pred, color='red', label='Polynomial regression curve')
plt.title("Polynomial Regression (Degree 2)")
plt.xlabel("X")
plt.ylabel("Y")
plt.legend()
plt.show()
```

### Explanation

- **Sample Data**: We generate 100 data points with a quadratic relationship between the independent variable \(X\) and the dependent variable \(Y\), with some added noise.
- **Polynomial Transformation**: We transform the original features \(X\) into polynomial features using `PolynomialFeatures` from `scikit-learn`.
- **Model Fitting**: We fit a linear regression model to the transformed polynomial features.
- **Model Parameters**: The intercept (\(\beta_0\)) and coefficients (\(\beta_1, \beta_2\)) of the polynomial are printed.
- **Model Evaluation**: We calculate the mean squared error (MSE) and R-squared (R²) to assess the model's performance.
- **Visualization**: We plot the observed data and the polynomial regression curve to visualize the relationship.

## Example in R

Let's perform the same polynomial regression analysis using R.

### R Code

```r
# Load necessary libraries
library(ggplot2)

# Sample data: X values and Y values with a quadratic relationship
set.seed(42)
X <- runif(100, min=0, max=10)  # Independent variable
Y <- 2 + 1.5 * X + 0.5 * X^2 + rnorm(100, mean=0, sd=2)  # Dependent variable

# Fit a polynomial regression model (degree 2)
model <- lm(Y ~ poly(X, 2, raw=TRUE))

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

# Plot the data and the polynomial regression curve
data <- data.frame(X=X, Y=Y, Y_pred=predict(model))
ggplot(data, aes(x=X, y=Y)) +
  geom_point(color="blue", size=2) +
  geom_line(aes(y=Y_pred), color="red", size=1) +
  labs(title="Polynomial Regression (Degree 2)", x="X", y="Y") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We generate 100 data points with a quadratic relationship between the independent variable \(X\) and the dependent variable \(Y\) using `runif()` and `rnorm()` functions.
- **Model Fitting**: We fit a polynomial regression model (degree 2) using the `lm()` function.
- **Model Summary**: The `summary()` function provides detailed information about the model, including the coefficients, R-squared value, and significance of the model.
- **Model Parameters**: The intercept (\(\beta_0\)) and coefficients (\(\beta_1, \beta_2\)) are extracted and printed.
- **Model Evaluation**: We calculate the mean squared error (MSE) and R-squared (R²) to assess the model's performance.
- **Visualization**: We plot the observed data and the polynomial regression curve using `ggplot2` to visualize the relationship.

## Interpreting the Results

### Model Parameters

- **Intercept ($\beta_0$)**: The intercept represents the predicted value of the dependent variable $Y$ when the independent variable $X$ is zero.
- **Coefficients ($\beta_1, \beta_2$)**: The coefficients represent the change in the dependent variable \(Y\) for a one-unit change in the corresponding power of the independent variable $X$. In the context of the example, $\beta_1$ is the coefficient for $X$, and $\beta_2$ is the coefficient for $X^2$.

### Model Evaluation

- **Mean Squared Error (MSE)**: MSE measures the average squared difference between the observed and predicted values. A lower MSE indicates a better fit.
- **R-squared (R²)**: R² represents the proportion of the variance in the dependent variable that is explained by the independent variables. An R² value closer to 1 indicates a better fit.

### Visualization

The plot of the polynomial regression curve provides a visual representation of the relationship between the independent and dependent variables. The curve captures the non-linear pattern in the data that a simple linear regression model would miss.

## Applications

Polynomial regression is widely used in various fields where relationships between variables are not linear:

- **Economics**: To model relationships such as diminishing returns to scale or the Kuznets curve.
- **Healthcare**: To estimate the effect of dosage on patient outcomes, where the relationship may not be linear.
- **Engineering**: To model physical phenomena, such as stress-strain relationships, that exhibit non-linear behavior.

## Conclusion

Polynomial regression is a powerful tool for modeling non-linear relationships between variables. By understanding the model parameters, evaluating model performance, and visualizing the results, researchers and analysts can make informed predictions and decisions based on their data. Whether in economics, healthcare, engineering, or other fields, polynomial regression provides a flexible framework for capturing complex relationships between variables.
