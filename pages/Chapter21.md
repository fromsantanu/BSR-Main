# Chapter: Spearman Rank Correlation

## Introduction

Spearman rank correlation is a non-parametric measure of the strength and direction of association between two ranked variables. Unlike Pearson correlation, which assesses linear relationships, Spearman rank correlation evaluates the monotonic relationship between two variables. It is particularly useful when the data does not meet the assumptions of Pearson correlation, such as when the data is ordinal or not normally distributed.

## Key Concepts

1. **Spearman Rank Correlation Coefficient ( $\rho$)**: The formula for calculating Spearman's rank correlation coefficient between two variables $X$ and $Y$ is:
   
   $\rho = 1 - \frac{6 \sum d_i^2}{n(n^2 - 1)}$
   
   where:
   - $d_i$ is the difference between the ranks of corresponding values of \( X \) and \( Y \),
   - $n$ is the number of observations.

2. **Monotonic Relationship**: Spearman rank correlation assesses whether the relationship between two variables is monotonic, meaning that as one variable increases, the other either consistently increases or decreases, but not necessarily at a constant rate.

3. **Non-parametric**: Spearman correlation does not assume a specific distribution for the data, making it suitable for ordinal data or data that does not meet the assumptions required for Pearson correlation.

4. **Interpretation**:
   - **$\rho = 1$**: A perfect positive monotonic relationship.
   - **$\rho = -1$**: A perfect negative monotonic relationship.
   - **$\rho = 0$**: No monotonic relationship.

## Example in Python

Let's explore how to calculate and interpret the Spearman rank correlation coefficient using Python.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
from scipy.stats import spearmanr
import matplotlib.pyplot as plt

# Sample data: hours studied and test scores
np.random.seed(42)
data = pd.DataFrame({
    'Hours_Studied': np.random.rand(100) * 10,
    'Test_Score': 3 + 2.5 * np.random.rand(100) * 10 + np.random.randn(100) * 2
})

# Calculate Spearman rank correlation coefficient
spearman_coefficient, p_value = spearmanr(data['Hours_Studied'], data['Test_Score'])

print(f"Spearman Rank Correlation Coefficient (ρ): {spearman_coefficient:.2f}")
print(f"P-value: {p_value:.4f}")

# Scatter plot with a non-linear trend line
plt.figure(figsize=(8, 6))
plt.scatter(data['Hours_Studied'], data['Test_Score'], color='blue')
plt.title('Scatter Plot with Non-linear Trend Line')
plt.xlabel('Hours Studied')
plt.ylabel('Test Score')

# Fit a non-linear trend line
z = np.polyfit(data['Hours_Studied'], data['Test_Score'], 2)
p = np.poly1d(z)
plt.plot(data['Hours_Studied'], p(data['Hours_Studied']), color='red')

plt.show()
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied and test scores.
- **Spearman Correlation Calculation**: We use the `spearmanr()` function from `scipy.stats` to calculate the Spearman rank correlation coefficient and the associated p-value.
- **Scatter Plot with Non-linear Trend Line**: We plot the data and fit a non-linear trend line (a quadratic polynomial) to visualize the relationship between hours studied and test scores.

## Example in R

Let's perform the same Spearman rank correlation analysis using R.

### R Code

```r
# Sample data: hours studied and test scores
set.seed(42)
Hours_Studied <- runif(100, min=0, max=10)
Test_Score <- 3 + 2.5 * runif(100, min=0, max=10) + rnorm(100, mean=0, sd=2)

# Calculate Spearman rank correlation coefficient
spearman_coefficient <- cor(Hours_Studied, Test_Score, method="spearman")
p_value <- cor.test(Hours_Studied, Test_Score, method="spearman")$p.value

cat("Spearman Rank Correlation Coefficient (ρ):", round(spearman_coefficient, 2), "\n")
cat("P-value:", round(p_value, 4), "\n")

# Scatter plot with a non-linear trend line
plot(Hours_Studied, Test_Score, main="Scatter Plot with Non-linear Trend Line",
     xlab="Hours Studied", ylab="Test Score", pch=19, col="blue")

# Fit a non-linear trend line (quadratic)
model <- lm(Test_Score ~ poly(Hours_Studied, 2))
lines(sort(Hours_Studied), predict(model, newdata=data.frame(Hours_Studied=sort(Hours_Studied))), col="red", lwd=2)
```

### Explanation

- **Sample Data**: We generate a dataset with 100 observations, including hours studied and test scores using `runif()` and `rnorm()` functions.
- **Spearman Correlation Calculation**: We use the `cor()` function with `method="spearman"` to calculate the Spearman rank correlation coefficient and the `cor.test()` function to obtain the p-value.
- **Scatter Plot with Non-linear Trend Line**: We plot the data and fit a non-linear trend line using a quadratic polynomial model to visualize the relationship between hours studied and test scores.

## Interpretation of Results

### Spearman Rank Correlation Coefficient (\( \rho \))

- **$\rho > 0$**: Indicates a positive monotonic relationship between the variables. As one variable increases, the other tends to increase.
- **$\rho < 0$**: Indicates a negative monotonic relationship between the variables. As one variable increases, the other tends to decrease.
- **$\rho = 0$**: Indicates no monotonic relationship between the variables.

### P-value

The p-value indicates the significance of the correlation:
- **Low p-value ($p \leq \alpha$)**: Suggests that the observed correlation is statistically significant (commonly, \( \alpha = 0.05 \)).
- **High p-value ($p > \alpha$)**: Suggests that the observed correlation is not statistically significant.

### Visualization

The scatter plot with a non-linear trend line provides a visual representation of the relationship between the two variables. The non-linear trend line is useful when the relationship between the variables is not strictly linear, which is often the case in Spearman correlation.

## Applications

Spearman rank correlation is widely used in various fields:

- **Education**: To assess the relationship between students' ranks in different subjects.
- **Healthcare**: To evaluate the relationship between ordinal variables, such as pain severity and patient satisfaction.
- **Social Sciences**: To analyze the association between ranked data, such as socioeconomic status and quality of life.

## Conclusion

Spearman rank correlation is a valuable tool for assessing the strength and direction of monotonic relationships between two variables, especially when the data does not meet the assumptions required for Pearson correlation. By calculating the Spearman rank correlation coefficient, interpreting the results, and visualizing the relationship, researchers and analysts can gain insights into the associations within their data. Whether in education, healthcare, social sciences, or other fields, Spearman rank correlation provides a robust method for exploring monotonic relationships.
