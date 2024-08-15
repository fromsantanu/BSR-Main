# Chapter: Mann-Whitney U Test

## Introduction

The Mann-Whitney U Test, also known as the Wilcoxon rank-sum test, is a non-parametric test used to compare the distributions of two independent groups. It is particularly useful when the assumptions of the t-test, such as normality, are not met. The Mann-Whitney U Test assesses whether one group tends to have higher (or lower) values than the other group, based on the ranks of the data.

## Key Concepts

1. **Non-Parametric Test**: The Mann-Whitney U Test does not assume a normal distribution of the data. Instead, it ranks the data from both groups together and compares these ranks.
2. **Independent Groups**: The test is used for comparing two independent groups, meaning the observations in one group are not related to those in the other group.
3. **Null Hypothesis ($H_0$)**: The null hypothesis states that the distributions of the two groups are equal, meaning there is no difference between the groups.
4. **Alternative Hypothesis ($H_a$))**: The alternative hypothesis states that one group tends to have higher or lower values than the other group.

## Test Statistic

The Mann-Whitney U statistic is calculated by comparing the ranks of the observations in the two groups. The U statistic is given by:


$U = n_1 n_2 + \frac{n_1(n_1 + 1)}{2} - R_1$


where:
- $n_1$ and $n_2$ are the sample sizes of the two groups,
- $R_1$ is the sum of ranks in the first group.

The test also provides a p-value to assess the significance of the results.

## Example in Python

Let's explore how to perform the Mann-Whitney U Test using Python's `scipy` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
from scipy.stats import mannwhitneyu

# Sample data: two independent groups
np.random.seed(42)
group1 = np.random.normal(50, 10, 30)
group2 = np.random.normal(55, 10, 30)

# Perform Mann-Whitney U Test
u_statistic, p_value = mannwhitneyu(group1, group2, alternative='two-sided')

print(f"Mann-Whitney U Statistic: {u_statistic:.2f}")
print(f"P-value: {p_value:.4f}")

# Visualization: Boxplot
import matplotlib.pyplot as plt
import seaborn as sns

data = {'Group 1': group1, 'Group 2': group2}
sns.boxplot(data=data)
plt.title('Boxplot of Two Independent Groups')
plt.ylabel('Values')
plt.show()
```

### Explanation

- **Sample Data**: We generate two independent groups with 30 observations each, drawn from normal distributions with slightly different means.
- **Mann-Whitney U Test**: We use `mannwhitneyu()` from `scipy.stats` to perform the Mann-Whitney U Test, which returns the U statistic and p-value.
- **Visualization**: We create a boxplot to visually compare the distributions of the two groups.

## Example in R

Let's perform the same Mann-Whitney U Test using R.

### R Code

```r
# Load necessary libraries
library(ggplot2)

# Sample data: two independent groups
set.seed(42)
group1 <- rnorm(30, mean=50, sd=10)
group2 <- rnorm(30, mean=55, sd=10)

# Perform Mann-Whitney U Test (Wilcoxon rank-sum test in R)
wilcox_test <- wilcox.test(group1, group2, alternative="two.sided")

cat("Mann-Whitney U Statistic:", wilcox_test$statistic, "\n")
cat("P-value:", round(wilcox_test$p.value, 4), "\n")

# Visualization: Boxplot
data <- data.frame(
  Group = factor(rep(c("Group 1", "Group 2"), each=30)),
  Values = c(group1, group2)
)

ggplot(data, aes(x=Group, y=Values)) +
  geom_boxplot() +
  labs(title="Boxplot of Two Independent Groups", y="Values") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We generate two independent groups with 30 observations each using `rnorm()` in R, with slightly different means.
- **Mann-Whitney U Test**: We use the `wilcox.test()` function in R to perform the Mann-Whitney U Test, which is referred to as the Wilcoxon rank-sum test in R.
- **Visualization**: We create a boxplot using `ggplot2` to visually compare the distributions of the two groups.

## Interpretation of Results

### U Statistic and P-value

- **U Statistic**: The Mann-Whitney U statistic indicates the sum of ranks for the observations in one group relative to the other. A smaller U statistic suggests that the values in one group tend to be lower than those in the other group.
- **P-value**: The p-value assesses the significance of the difference between the two groups. If the p-value is less than the chosen significance level (typically \( \leq 0.05 \)), we reject the null hypothesis and conclude that there is a significant difference between the groups.

### Boxplot Visualization

The boxplot provides a visual comparison of the distributions of the two groups. Differences in medians, spreads, and outliers between the groups can be easily observed in the boxplot.

## Applications

The Mann-Whitney U Test is widely used in various fields:

- **Healthcare**: To compare the effectiveness of two treatments when the data are not normally distributed.
- **Psychology**: To assess differences between two independent groups on a non-parametric measure, such as a rank-order scale.
- **Marketing**: To evaluate customer satisfaction ratings between two independent groups of customers.

## Conclusion

The Mann-Whitney U Test is a powerful non-parametric tool for comparing the distributions of two independent groups. By calculating the U statistic and p-value, and visualizing the data with boxplots, researchers can determine whether there is a significant difference between the groups. Whether in healthcare, psychology, marketing, or other fields, the Mann-Whitney U Test provides valuable insights when the assumptions of parametric tests are not met.
