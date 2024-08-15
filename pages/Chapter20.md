# Chapter: Pearson Correlation

## Introduction

Pearson correlation is a statistical measure that quantifies the linear relationship between two continuous variables. It is a widely used method to assess the strength and direction of the linear association between two variables. The Pearson correlation coefficient, denoted as \( r \), ranges from -1 to 1, where:

- $ r = 1 $ indicates a perfect positive linear relationship.
- \( r = -1 \) indicates a perfect negative linear relationship.
- \( r = 0 \) indicates no linear relationship.

## Key Concepts

1. **Pearson Correlation Coefficient (\( r \))**: The formula for calculating the Pearson correlation coefficient between two variables \( X \) and \( Y \) is:
   \[
   r = \frac{\sum{(X_i - \bar{X})(Y_i - \bar{Y})}}{\sqrt{\sum{(X_i - \bar{X})^2} \sum{(Y_i - \bar{Y})^2}}}
   \]
   where:
   - \( X_i \) and \( Y_i \) are the individual data points,
   - \( \bar{X} \) and \( \bar{Y} \) are the means of the \( X \) and \( Y \) variables.

2. **Interpretation**:
   - **Positive Correlation**: As \( X \) increases, \( Y \) tends to increase.
   - **Negative Correlation**: As \( X \) increases, \( Y \) tends to decrease.
   - **No Correlation**: There is no apparent relationship between \( X \) and \( Y \).

3. **Assumptions**:
   - **Linearity**: The relationship between the variables is linear.
   - **Continuous Variables**: Both variables are continuous.
   - **Normality**: The variables are normally distributed (for significance testing).

## Example in Python

Let's explore how to calculate and interpret the Pearson correlation coefficient using Python.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
from scipy.stats import pearsonr

# Sample data: hours studied and test scores
np.random.seed(42)
data = pd.DataFrame({
    'Hours_Studied': np.random.rand(100) * 10,
    'Test_Score': 3 + 2.5 * np.random.rand(100) * 10 + np.random.randn(100) * 2
})

# Calculate Pearson correlation coefficient
correlation_coefficient, p_value = pearsonr(data['Hours_Studied'], data['Test_Score'])

print(f"Pearson Correlation Coefficient (r): {correlation_coefficient:.2f}")
print(f"P-value: {p_value:.4f}")

# Scatter plot with regression line
plt.figure(figsize=(8, 6))
plt.scatter(data['Hours_Studied'], data['Test_Score'], color='blue')
plt.title('Scatter Plot with Regression Line')
plt.xlabel('Hours Studied')
plt.ylabel('Test Score')

# Fit a regression line
m, b = np.polyfit(data['Hours_Studied'], data['Test_Score'], 1)
plt.plot(data['Hours_Studied'], m * data['Hours_Studied'] + b, color='red')

plt.show()
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied and test scores.
- **Pearson Correlation Calculation**: We use the `pearsonr()` function from `scipy.stats` to calculate the Pearson correlation coefficient and the associated p-value.
- **Scatter Plot with Regression Line**: We plot the data and fit a regression line to visualize the relationship between hours studied and test scores.

## Example in R

Let's perform the same Pearson correlation analysis using R.

### R Code

```r
# Sample data: hours studied and test scores
set.seed(42)
Hours_Studied <- runif(100, min=0, max=10)
Test_Score <- 3 + 2.5 * runif(100, min=0, max=10) + rnorm(100, mean=0, sd=2)

# Calculate Pearson correlation coefficient
correlation_coefficient <- cor(Hours_Studied, Test_Score)
p_value <- cor.test(Hours_Studied, Test_Score)$p.value

cat("Pearson Correlation Coefficient (r):", round(correlation_coefficient, 2), "\n")
cat("P-value:", round(p_value, 4), "\n")

# Scatter plot with regression line
plot(Hours_Studied, Test_Score, main="Scatter Plot with Regression Line",
     xlab="Hours Studied", ylab="Test Score", pch=19, col="blue")
abline(lm(Test_Score ~ Hours_Studied), col="red", lwd=2)
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied and test scores using `runif()` and `rnorm()` functions.
- **Pearson Correlation Calculation**: We use the `cor()` function to calculate the Pearson correlation coefficient and the `cor.test()` function to obtain the p-value.
- **Scatter Plot with Regression Line**: We plot the data and fit a regression line using `abline()` to visualize the relationship between hours studied and test scores.

## Interpretation of Results

### Pearson Correlation Coefficient (\( r \))

- **\( r > 0 \)**: Indicates a positive linear relationship between the variables. As one variable increases, the other tends to increase.
- **\( r < 0 \)**: Indicates a negative linear relationship between the variables. As one variable increases, the other tends to decrease.
- **\( r = 0 \)**: Indicates no linear relationship between the variables.

### P-value

The p-value indicates the significance of the correlation:
- **Low p-value (\( p \leq \alpha \))**: Suggests that the observed correlation is statistically significant (commonly, \( \alpha = 0.05 \)).
- **High p-value (\( p > \alpha \))**: Suggests that the observed correlation is not statistically significant.

### Scatter Plot with Regression Line

The scatter plot with a regression line provides a visual representation of the relationship between the two variables. The closer the data points are to the regression line, the stronger the linear relationship.

## Applications

Pearson correlation is widely used in various fields:

- **Healthcare**: To assess the relationship between two health indicators, such as blood pressure and cholesterol levels.
- **Economics**: To evaluate the correlation between economic indicators, such as GDP growth and unemployment rates.
- **Education**: To analyze the relationship between study time and academic performance.

## Conclusion

Pearson correlation is a fundamental tool for assessing the strength and direction of the linear relationship between two continuous variables. By calculating the Pearson correlation coefficient, interpreting the results, and visualizing the relationship with scatter plots, researchers and analysts can gain valuable insights into the relationships within their data. Whether in healthcare, economics, education, or other fields, Pearson correlation provides a straightforward and effective method for exploring linear associations.
