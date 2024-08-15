# Chapter: Chi-Square Test

## Introduction

The Chi-Square Test is a non-parametric statistical test used to determine whether there is a significant association between categorical variables. It is commonly used in situations where data are presented in frequency tables. There are two main types of Chi-Square tests: the Chi-Square Test for Independence and the Chi-Square Goodness-of-Fit Test.

- **Chi-Square Test for Independence**: Used to test whether two categorical variables are independent of each other.
- **Chi-Square Goodness-of-Fit Test**: Used to test whether the distribution of a categorical variable matches an expected distribution.

## Key Concepts

1. **Observed Frequencies**: The actual counts or frequencies observed in the data.
2. **Expected Frequencies**: The counts or frequencies expected under the null hypothesis, assuming no association between the variables.
3. **Chi-Square Statistic ($\chi^2$)**: The formula for calculating the Chi-Square statistic is:
 
   $\chi^2 = \sum \frac{(O_i - E_i)^2}{E_i}$

   where:
   - $O_i$ are the observed frequencies,
   - $E_i$ are the expected frequencies.
4. **Degrees of Freedom (df)**: For the Chi-Square Test for Independence, degrees of freedom are calculated as:

   $df = (r - 1) \times (c - 1)$

   where $r$ is the number of rows and $c$ is the number of columns in the contingency table.
5. **P-value**: The p-value indicates the probability of observing the data assuming the null hypothesis is true. A low p-value (typically $\leq 0.05$) suggests rejecting the null hypothesis.

## Example in Python

Let's explore how to perform a Chi-Square Test for Independence using Python's `scipy` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
from scipy.stats import chi2_contingency

# Sample data: survey responses on two categorical variables
data = pd.DataFrame({
    'Gender': np.random.choice(['Male', 'Female'], size=100),
    'Preference': np.random.choice(['Product A', 'Product B'], size=100)
})

# Create a contingency table
contingency_table = pd.crosstab(data['Gender'], data['Preference'])

print("Contingency Table:")
print(contingency_table)

# Perform Chi-Square Test for Independence
chi2, p, dof, expected = chi2_contingency(contingency_table)

print(f"\nChi-Square Statistic: {chi2:.2f}")
print(f"P-value: {p:.4f}")
print(f"Degrees of Freedom: {dof}")
print("\nExpected Frequencies:")
print(expected)
```

### Explanation

- **Sample Data**: We generate a dataset with two categorical variables: `Gender` and `Preference` for two products.
- **Contingency Table**: We create a contingency table that shows the frequency of responses for each combination of `Gender` and `Preference`.
- **Chi-Square Test**: We use `chi2_contingency()` from `scipy.stats` to perform the Chi-Square Test for Independence, which returns the Chi-Square statistic, p-value, degrees of freedom, and expected frequencies.

## Example in R

Let's perform the same Chi-Square Test for Independence using R.

### R Code

```r
# Load necessary libraries
library(MASS)

# Sample data: survey responses on two categorical variables
set.seed(42)
Gender <- sample(c("Male", "Female"), 100, replace=TRUE)
Preference <- sample(c("Product A", "Product B"), 100, replace=TRUE)
data <- data.frame(Gender, Preference)

# Create a contingency table
contingency_table <- table(data$Gender, data$Preference)

cat("Contingency Table:\n")
print(contingency_table)

# Perform Chi-Square Test for Independence
chi_square_test <- chisq.test(contingency_table)

cat("\nChi-Square Statistic:", round(chi_square_test$statistic, 2), "\n")
cat("P-value:", round(chi_square_test$p.value, 4), "\n")
cat("Degrees of Freedom:", chi_square_test$parameter, "\n")
cat("\nExpected Frequencies:\n")
print(round(chi_square_test$expected, 2))
```

### Explanation

- **Sample Data**: We generate a dataset with two categorical variables: `Gender` and `Preference` using `sample()` in R.
- **Contingency Table**: We create a contingency table using the `table()` function that shows the frequency of responses for each combination of `Gender` and `Preference`.
- **Chi-Square Test**: We use `chisq.test()` to perform the Chi-Square Test for Independence, which returns the Chi-Square statistic, p-value, degrees of freedom, and expected frequencies.

## Interpretation of Results

### Chi-Square Statistic and P-value

- **Chi-Square Statistic**: This value indicates how much the observed frequencies deviate from the expected frequencies. A larger Chi-Square statistic suggests a greater difference between observed and expected frequencies.
- **P-value**: If the p-value is less than the chosen significance level (typically \( \leq 0.05 \)), we reject the null hypothesis and conclude that there is a statistically significant association between the variables.

### Contingency Table and Expected Frequencies

- **Contingency Table**: This table shows the observed frequencies of each combination of categorical variables.
- **Expected Frequencies**: These are the frequencies that would be expected if there were no association between the variables. If observed and expected frequencies differ significantly, it suggests that the variables are not independent.

## Applications

The Chi-Square Test is widely used in various fields:

- **Marketing**: To analyze the relationship between customer demographics (e.g., age, gender) and product preferences.
- **Healthcare**: To assess the association between patient characteristics (e.g., smoking status, disease outcome) and health conditions.
- **Social Sciences**: To study the relationship between categorical variables, such as education level and political affiliation.

## Conclusion

The Chi-Square Test is a powerful non-parametric tool for analyzing the association between categorical variables. By calculating the Chi-Square statistic, p-value, and expected frequencies, researchers can determine whether there is a statistically significant relationship between the variables. Whether in marketing, healthcare, social sciences, or other fields, the Chi-Square Test provides valuable insights into the relationships within categorical data.
