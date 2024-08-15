# Chapter: Kruskal-Wallis H Test

## Introduction

The Kruskal-Wallis H Test is a non-parametric statistical test used to compare the distributions of three or more independent groups. It is an extension of the Mann-Whitney U Test to more than two groups and serves as a non-parametric alternative to one-way ANOVA. The Kruskal-Wallis H Test does not assume that the data are normally distributed and instead ranks the data to assess whether the distributions of the groups differ significantly.

## Key Concepts

1. **Non-Parametric Test**: The Kruskal-Wallis H Test does not assume normality of the data. It uses the ranks of the data rather than the raw data itself.
2. **Independent Groups**: The test is used for comparing three or more independent groups, where the observations in one group are not related to those in the other groups.
3. **Null Hypothesis ($H_0$)**: The null hypothesis states that the distributions of the groups are equal, meaning there is no difference between the groups.
4. **Alternative Hypothesis ($H_a$)**: The alternative hypothesis states that at least one group distribution is different from the others.

## Test Statistic

The Kruskal-Wallis H statistic is calculated by ranking all the data together and comparing the sum of ranks for each group. The H statistic is given by:


$H = \frac{12}{N(N+1)} \sum_{i=1}^{k} \frac{R_i^2}{n_i} - 3(N+1)$


where:
- $N$ is the total number of observations across all groups,
- $R_i$ is the sum of ranks for the \( i \)-th group,
- $n_i$ is the number of observations in the \( i \)-th group,
- $k$ is the number of groups.

The test also provides a p-value to assess the significance of the results.

## Example in Python

Let's explore how to perform the Kruskal-Wallis H Test using Python's `scipy` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
from scipy.stats import kruskal

# Sample data: three independent groups
np.random.seed(42)
group1 = np.random.normal(50, 10, 30)
group2 = np.random.normal(55, 10, 30)
group3 = np.random.normal(60, 10, 30)

# Perform Kruskal-Wallis H Test
h_statistic, p_value = kruskal(group1, group2, group3)

print(f"Kruskal-Wallis H Statistic: {h_statistic:.2f}")
print(f"P-value: {p_value:.4f}")

# Visualization: Boxplot
import matplotlib.pyplot as plt
import seaborn as sns

data = {'Group 1': group1, 'Group 2': group2, 'Group 3': group3}
sns.boxplot(data=data)
plt.title('Boxplot of Three Independent Groups')
plt.ylabel('Values')
plt.show()
```

### Explanation

- **Sample Data**: We generate three independent groups with 30 observations each, drawn from normal distributions with different means.
- **Kruskal-Wallis H Test**: We use `kruskal()` from `scipy.stats` to perform the Kruskal-Wallis H Test, which returns the H statistic and p-value.
- **Visualization**: We create a boxplot to visually compare the distributions of the three groups.

## Example in R

Let's perform the same Kruskal-Wallis H Test using R.

### R Code

```r
# Load necessary libraries
library(ggplot2)

# Sample data: three independent groups
set.seed(42)
group1 <- rnorm(30, mean=50, sd=10)
group2 <- rnorm(30, mean=55, sd=10)
group3 <- rnorm(30, mean=60, sd=10)

# Perform Kruskal-Wallis H Test
kruskal_test <- kruskal.test(list(group1, group2, group3))

cat("Kruskal-Wallis H Statistic:", kruskal_test$statistic, "\n")
cat("P-value:", round(kruskal_test$p.value, 4), "\n")

# Visualization: Boxplot
data <- data.frame(
  Group = factor(rep(c("Group 1", "Group 2", "Group 3"), each=30)),
  Values = c(group1, group2, group3)
)

ggplot(data, aes(x=Group, y=Values)) +
  geom_boxplot() +
  labs(title="Boxplot of Three Independent Groups", y="Values") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We generate three independent groups with 30 observations each using `rnorm()` in R, with different means.
- **Kruskal-Wallis H Test**: We use the `kruskal.test()` function in R to perform the Kruskal-Wallis H Test, which returns the H statistic and p-value.
- **Visualization**: We create a boxplot using `ggplot2` to visually compare the distributions of the three groups.

## Interpretation of Results

### H Statistic and P-value

- **H Statistic**: The Kruskal-Wallis H statistic indicates how much the observed ranks differ from the ranks expected under the null hypothesis. A larger H statistic suggests greater differences between the groups.
- **P-value**: The p-value assesses the significance of the differences between the groups. If the p-value is less than the chosen significance level (typically \( \leq 0.05 \)), we reject the null hypothesis and conclude that there is a significant difference between at least one pair of groups.

### Boxplot Visualization

The boxplot provides a visual comparison of the distributions of the three groups. Differences in medians, spreads, and outliers between the groups can be easily observed in the boxplot.

## Applications

The Kruskal-Wallis H Test is widely used in various fields:

- **Healthcare**: To compare the effectiveness of three or more treatments when the data are not normally distributed.
- **Education**: To assess differences in test scores across multiple teaching methods.
- **Marketing**: To evaluate customer satisfaction ratings across different product categories.

## Conclusion

The Kruskal-Wallis H Test is a powerful non-parametric tool for comparing the distributions of three or more independent groups. By calculating the H statistic and p-value, and visualizing the data with boxplots, researchers can determine whether there is a significant difference between the groups. Whether in healthcare, education, marketing, or other fields, the Kruskal-Wallis H Test provides valuable insights when the assumptions of parametric tests are not met.
