# Chapter: Wilcoxon Signed-Rank Test

## Introduction

The Wilcoxon Signed-Rank Test is a non-parametric statistical test used to compare two related samples or paired observations. It is the non-parametric equivalent of the paired t-test and is used when the data does not meet the assumptions of the t-test, such as normality. The Wilcoxon Signed-Rank Test assesses whether the median difference between pairs of observations is significantly different from zero.

## Key Concepts

1. **Paired Samples**: The test is used for comparing two related samples or paired observations, such as measurements taken before and after a treatment on the same subjects.
2. **Non-Parametric Test**: The Wilcoxon Signed-Rank Test does not assume a normal distribution of the differences between pairs. Instead, it ranks the absolute differences and uses the ranks to assess the significance.
3. **Null Hypothesis ($H_0$)**: The null hypothesis states that the median difference between the paired observations is zero.
4. **Alternative Hypothesis ($H_a$)**: The alternative hypothesis states that the median difference between the paired observations is not zero.

## Test Statistic

The Wilcoxon Signed-Rank Test statistic is calculated by ranking the absolute differences between paired observations, assigning positive or negative signs to these ranks based on the direction of the difference, and summing the ranks. The test then compares this sum to the expected value under the null hypothesis.

## Example in Python

Let's explore how to perform the Wilcoxon Signed-Rank Test using Python's `scipy` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
from scipy.stats import wilcoxon

# Sample data: before and after treatment scores
np.random.seed(42)
before_treatment = np.random.normal(50, 10, 30)
after_treatment = before_treatment + np.random.normal(5, 10, 30)

# Perform Wilcoxon Signed-Rank Test
w_statistic, p_value = wilcoxon(before_treatment, after_treatment)

print(f"Wilcoxon Signed-Rank Statistic: {w_statistic:.2f}")
print(f"P-value: {p_value:.4f}")

# Visualization: Boxplot
import matplotlib.pyplot as plt
import seaborn as sns

data = {'Before Treatment': before_treatment, 'After Treatment': after_treatment}
sns.boxplot(data=data)
plt.title('Boxplot of Before and After Treatment Scores')
plt.ylabel('Scores')
plt.show()
```

### Explanation

- **Sample Data**: We generate paired data for 30 subjects, representing scores before and after a treatment.
- **Wilcoxon Signed-Rank Test**: We use the `wilcoxon()` function from `scipy.stats` to perform the Wilcoxon Signed-Rank Test, which returns the Wilcoxon statistic and p-value.
- **Visualization**: We create a boxplot to visually compare the distributions of scores before and after treatment.

## Example in R

Let's perform the same Wilcoxon Signed-Rank Test using R.

### R Code

```r
# Load necessary libraries
library(ggplot2)

# Sample data: before and after treatment scores
set.seed(42)
before_treatment <- rnorm(30, mean=50, sd=10)
after_treatment <- before_treatment + rnorm(30, mean=5, sd=10)

# Perform Wilcoxon Signed-Rank Test
wilcox_test <- wilcox.test(before_treatment, after_treatment, paired=TRUE)

cat("Wilcoxon Signed-Rank Statistic:", wilcox_test$statistic, "\n")
cat("P-value:", round(wilcox_test$p.value, 4), "\n")

# Visualization: Boxplot
data <- data.frame(
  Treatment = factor(rep(c("Before", "After"), each=30)),
  Scores = c(before_treatment, after_treatment)
)

ggplot(data, aes(x=Treatment, y=Scores)) +
  geom_boxplot() +
  labs(title="Boxplot of Before and After Treatment Scores", y="Scores") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We generate paired data for 30 subjects, representing scores before and after a treatment using `rnorm()` in R.
- **Wilcoxon Signed-Rank Test**: We use the `wilcox.test()` function in R to perform the Wilcoxon Signed-Rank Test, specifying the `paired=TRUE` argument to indicate that the samples are paired.
- **Visualization**: We create a boxplot using `ggplot2` to visually compare the distributions of scores before and after treatment.

## Interpretation of Results

### Wilcoxon Signed-Rank Statistic and P-value

- **Wilcoxon Signed-Rank Statistic**: This value indicates the sum of the signed ranks of the differences between paired observations. A smaller statistic suggests that most differences are in the same direction (either positive or negative).
- **P-value**: The p-value assesses the significance of the median difference between paired observations. If the p-value is less than the chosen significance level (typically $\leq 0.05$), we reject the null hypothesis and conclude that there is a significant difference between the paired observations.

### Boxplot Visualization

The boxplot provides a visual comparison of the distributions before and after treatment. Differences in medians, spreads, and outliers can be observed, helping to understand the effect of the treatment.

## Applications

The Wilcoxon Signed-Rank Test is widely used in various fields:

- **Healthcare**: To compare patient outcomes before and after a treatment when the data is not normally distributed.
- **Psychology**: To assess the effect of an intervention on participants' scores before and after the intervention.
- **Education**: To evaluate the impact of a teaching method by comparing student performance on pre-tests and post-tests.

## Conclusion

The Wilcoxon Signed-Rank Test is a powerful non-parametric tool for comparing paired samples when the data does not meet the assumptions of the paired t-test. By calculating the Wilcoxon statistic and p-value, and visualizing the data with boxplots, researchers can determine whether there is a significant difference between paired observations. Whether in healthcare, psychology, education, or other fields, the Wilcoxon Signed-Rank Test provides valuable insights when analyzing paired data.
