# Chapter: Friedman Test

## Introduction

The Friedman Test is a non-parametric statistical test used to detect differences in treatments across multiple test attempts. It is an extension of the Wilcoxon Signed-Rank Test to more than two related groups and serves as a non-parametric alternative to the repeated measures ANOVA. The Friedman Test is particularly useful when the assumptions of normality required by repeated measures ANOVA are not met.

## Key Concepts

1. **Non-Parametric Test**: The Friedman Test does not assume normality of the data. It ranks the data within each block (or subject) and analyzes these ranks.
2. **Related Groups**: The test is used for comparing three or more related groups, such as repeated measurements on the same subjects or matched subjects in different conditions.
3. **Null Hypothesis ($H_0$)**: The null hypothesis states that the distributions of the groups are equal, meaning there is no difference between the related groups.
4. **Alternative Hypothesis ($H_a$)**: The alternative hypothesis states that at least one group distribution is different from the others.

## Test Statistic

The Friedman test statistic is calculated by ranking the data within each block and comparing the sum of ranks for each group. The test statistic is given by:


$\chi^2_F = \frac{12}{n k (k+1)} \sum_{i=1}^{k} R_i^2 - 3n(k+1)$


where:
- $n$ is the number of blocks (e.g., subjects),
- $k$ is the number of groups (e.g., treatments),
- $R_i$ is the sum of ranks for the $i$-th group.

The test provides a Chi-Square statistic and a p-value to assess the significance of the results.

## Example in Python

Let's explore how to perform the Friedman Test using Python's `scipy` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
from scipy.stats import friedmanchisquare

# Sample data: three related groups (e.g., scores from three different time points)
np.random.seed(42)
group1 = np.random.normal(50, 10, 10)
group2 = np.random.normal(55, 10, 10)
group3 = np.random.normal(60, 10, 10)

# Perform Friedman Test
friedman_statistic, p_value = friedmanchisquare(group1, group2, group3)

print(f"Friedman Test Statistic: {friedman_statistic:.2f}")
print(f"P-value: {p_value:.4f}")

# Visualization: Boxplot
import matplotlib.pyplot as plt
import seaborn as sns

data = {'Time 1': group1, 'Time 2': group2, 'Time 3': group3}
sns.boxplot(data=data)
plt.title('Boxplot of Scores Across Time Points')
plt.ylabel('Scores')
plt.show()
```

### Explanation

- **Sample Data**: We generate data for 10 subjects measured at three different time points, each with slightly different means.
- **Friedman Test**: We use `friedmanchisquare()` from `scipy.stats` to perform the Friedman Test, which returns the Friedman test statistic and p-value.
- **Visualization**: We create a boxplot to visually compare the distributions of scores across the three time points.

## Example in R

Let's perform the same Friedman Test using R.

### R Code

```r
# Load necessary libraries
library(ggplot2)

# Sample data: three related groups (e.g., scores from three different time points)
set.seed(42)
group1 <- rnorm(10, mean=50, sd=10)
group2 <- rnorm(10, mean=55, sd=10)
group3 <- rnorm(10, mean=60, sd=10)

# Perform Friedman Test
friedman_test <- friedman.test(y=c(group1, group2, group3), 
                               groups=factor(rep(1:3, each=10)), 
                               blocks=factor(rep(1:10, times=3)))

cat("Friedman Test Statistic:", friedman_test$statistic, "\n")
cat("P-value:", round(friedman_test$p.value, 4), "\n")

# Visualization: Boxplot
data <- data.frame(
  Time = factor(rep(c("Time 1", "Time 2", "Time 3"), each=10)),
  Scores = c(group1, group2, group3)
)

ggplot(data, aes(x=Time, y=Scores)) +
  geom_boxplot() +
  labs(title="Boxplot of Scores Across Time Points", y="Scores") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We generate data for 10 subjects measured at three different time points using `rnorm()` in R, with slightly different means.
- **Friedman Test**: We use the `friedman.test()` function in R to perform the Friedman Test, specifying the scores, groups (time points), and blocks (subjects).
- **Visualization**: We create a boxplot using `ggplot2` to visually compare the distributions of scores across the three time points.

## Interpretation of Results

### Friedman Test Statistic and P-value

- **Friedman Test Statistic**: The Friedman test statistic indicates how much the observed ranks differ from the ranks expected under the null hypothesis. A larger statistic suggests greater differences between the groups.
- **P-value**: The p-value assesses the significance of the differences between the groups. If the p-value is less than the chosen significance level (typically \( \leq 0.05 \)), we reject the null hypothesis and conclude that there is a significant difference between at least one pair of groups.

### Boxplot Visualization

The boxplot provides a visual comparison of the distributions across the related groups (e.g., time points). Differences in medians, spreads, and outliers between the groups can be easily observed in the boxplot.

## Applications

The Friedman Test is widely used in various fields:

- **Healthcare**: To compare the effectiveness of treatments measured on the same patients at different time points.
- **Education**: To assess differences in student performance across multiple tests administered over time.
- **Psychology**: To evaluate the impact of different interventions on the same participants across different conditions.

## Conclusion

The Friedman Test is a powerful non-parametric tool for comparing the distributions of three or more related groups when the data does not meet the assumptions of repeated measures ANOVA. By calculating the Friedman test statistic and p-value, and visualizing the data with boxplots, researchers can determine whether there is a significant difference between the related groups. Whether in healthcare, education, psychology, or other fields, the Friedman Test provides valuable insights when analyzing repeated measures data.
