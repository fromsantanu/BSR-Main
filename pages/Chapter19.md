# Chapter: Assumptions and Diagnostics of Regression Models

## Introduction

Regression models are powerful tools for understanding relationships between variables and making predictions. However, to ensure the validity of a regression model, certain assumptions must be met. Violations of these assumptions can lead to biased or misleading results. Therefore, it is essential to perform diagnostics to check whether the assumptions hold for a given model.

## Key Assumptions of Regression Models

1. **Linearity**: The relationship between the independent variables and the dependent variable is linear.
2. **Independence**: The residuals (errors) are independent of each other.
3. **Homoscedasticity**: The residuals have constant variance (i.e., the spread of residuals is consistent across all levels of the independent variables).
4. **Normality**: The residuals are normally distributed.
5. **No Multicollinearity**: In multiple regression, the independent variables should not be highly correlated with each other.

## Diagnostics to Check Assumptions

1. **Residual Plots**: Used to check linearity, homoscedasticity, and independence of residuals.
2. **Q-Q Plot (Quantile-Quantile Plot)**: Used to check the normality of residuals.
3. **Variance Inflation Factor (VIF)**: Used to check for multicollinearity among independent variables.

## Example in Python

Let's perform regression diagnostics on a multiple linear regression model using Python.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from sklearn.linear_model import LinearRegression
from sklearn.metrics import mean_squared_error
from statsmodels.stats.outliers_influence import variance_inflation_factor
import statsmodels.api as sm

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

# Fit the regression model
model = LinearRegression()
model.fit(X, Y)
Y_pred = model.predict(X)

# Calculate residuals
residuals = Y - Y_pred

# Linearity and Homoscedasticity Check: Residual Plot
plt.figure(figsize=(10, 6))
plt.scatter(Y_pred, residuals, color='blue')
plt.axhline(y=0, color='red', linestyle='--')
plt.title('Residual Plot')
plt.xlabel('Predicted Values')
plt.ylabel('Residuals')
plt.show()

# Normality Check: Q-Q Plot
sm.qqplot(residuals, line='s')
plt.title('Q-Q Plot')
plt.show()

# Independence Check: Durbin-Watson Test
dw_statistic = sm.stats.durbin_watson(residuals)
print(f'Durbin-Watson Statistic: {dw_statistic:.2f}')

# Multicollinearity Check: VIF
vif_data = pd.DataFrame()
vif_data['Feature'] = X.columns
vif_data['VIF'] = [variance_inflation_factor(X.values, i) for i in range(len(X.columns))]
print(vif_data)
```

### Explanation

- **Residual Plot**: The residual plot is used to check for linearity and homoscedasticity. If the residuals are randomly scattered around the horizontal axis (y=0), it indicates that the assumptions of linearity and homoscedasticity are met.
- **Q-Q Plot**: The Q-Q plot compares the distribution of residuals to a normal distribution. If the points lie along the reference line, it suggests that the residuals are normally distributed.
- **Durbin-Watson Test**: The Durbin-Watson statistic is used to detect the presence of autocorrelation in the residuals. Values close to 2 indicate no autocorrelation.
- **Variance Inflation Factor (VIF)**: VIF values greater than 5 or 10 indicate multicollinearity among the independent variables, which can be problematic for the model.

## Example in R

Let's perform the same regression diagnostics in R.

### R Code

```r
# Load necessary libraries
library(ggplot2)
library(car)
library(MASS)

# Sample data: hours studied, hours slept, and test scores
set.seed(42)
data <- data.frame(
  Hours_Studied = runif(100, min=0, max=10),
  Hours_Slept = runif(100, min=2, max=10)
)
data$Test_Score <- 3 + 2.5 * data$Hours_Studied + 1.5 * data$Hours_Slept + rnorm(100, mean=0, sd=2)

# Fit the regression model
model <- lm(Test_Score ~ Hours_Studied + Hours_Slept, data=data)

# Residual Plot: Linearity and Homoscedasticity
residuals <- model$residuals
fitted_values <- model$fitted.values
ggplot(data, aes(x=fitted_values, y=residuals)) +
  geom_point(color="blue") +
  geom_hline(yintercept=0, color="red", linetype="dashed") +
  labs(title="Residual Plot", x="Predicted Values", y="Residuals") +
  theme_minimal()

# Q-Q Plot: Normality Check
qqnorm(residuals)
qqline(residuals, col = "red", lwd = 2)

# Durbin-Watson Test: Independence Check
dw_test <- durbinWatsonTest(model)
print(dw_test)

# VIF: Multicollinearity Check
vif_values <- vif(model)
print(vif_values)
```

### Explanation

- **Residual Plot**: The residual plot is generated using `ggplot2` to check for linearity and homoscedasticity. A random scatter of residuals around the horizontal line indicates that these assumptions are met.
- **Q-Q Plot**: The `qqnorm()` and `qqline()` functions are used to create a Q-Q plot to check the normality of residuals.
- **Durbin-Watson Test**: The `durbinWatsonTest()` function from the `car` package is used to test for autocorrelation in the residuals.
- **VIF**: The `vif()` function from the `car` package calculates the Variance Inflation Factor to check for multicollinearity among the independent variables.

## Interpretation of Diagnostics

### Linearity and Homoscedasticity

- **Residual Plot**: If the residuals are randomly scattered around the horizontal line (y=0) without any clear pattern, the assumptions of linearity and homoscedasticity are likely met. If there is a clear pattern (e.g., a funnel shape), it may indicate non-linearity or heteroscedasticity (non-constant variance).

### Normality

- **Q-Q Plot**: If the points on the Q-Q plot closely follow the reference line, the residuals are approximately normally distributed. Deviations from this line suggest non-normality, which may affect the validity of the regression model.

### Independence

- **Durbin-Watson Test**: The Durbin-Watson statistic ranges from 0 to 4. A value close to 2 indicates no autocorrelation in the residuals. Values closer to 0 indicate positive autocorrelation, while values closer to 4 indicate negative autocorrelation.

### Multicollinearity

- **VIF**: VIF values greater than 5 or 10 indicate high multicollinearity, which can inflate the variance of the coefficient estimates and make the model unstable. If high VIF values are detected, consider removing or combining highly correlated predictors.

## Applications

Performing regression diagnostics is crucial in various fields:

- **Economics**: To ensure the validity of models predicting economic indicators, such as GDP growth or inflation rates.
- **Healthcare**: To validate models predicting patient outcomes based on multiple health indicators, ensuring accurate and reliable predictions.
- **Social Sciences**: To assess the relationships between social factors and outcomes, such as education level and income, while ensuring the assumptions of regression are met.

## Conclusion

Regression diagnostics are essential for validating the assumptions of regression models. By checking for linearity, independence, homoscedasticity, normality, and multicollinearity, researchers and analysts can ensure the reliability and validity of their models. Proper diagnostics lead to more accurate predictions and better decision-making across various fields, from economics and healthcare to social sciences and beyond.
