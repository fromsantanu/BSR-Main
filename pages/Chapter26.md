# Chapter: Repeated Measures ANOVA

## Introduction

Repeated Measures ANOVA is a statistical technique used to analyze data where the same subjects are measured multiple times under different conditions. This method is commonly used in within-subjects designs where each participant is exposed to all levels of the independent variable. Repeated Measures ANOVA is particularly useful for reducing variability caused by individual differences since each subject serves as their own control.

## Key Concepts

1. **Within-Subject Factor**: The independent variable where each subject is exposed to all its levels (e.g., time points, conditions).
2. **Sphericity**: An assumption of repeated measures ANOVA that requires the variances of the differences between all combinations of related groups to be equal. Violation of sphericity can lead to incorrect conclusions, and adjustments like the Greenhouse-Geisser correction may be applied.
3. **Main Effect**: The effect of the independent variable on the dependent variable, averaged across all levels of other variables.
4. **Interaction Effect**: The combined effect of two or more independent variables on the dependent variable.
5. **Null Hypothesis ($H_0$)**: The null hypothesis states that the means of all conditions or time points are equal.
  
   $H_0: \mu_1 = \mu_2 = \mu_3 = \ldots = \mu_k$
  
6. **Alternative Hypothesis ($H_a$)**: The alternative hypothesis states that at least one condition mean is different from the others.

## Example in Python

Let's explore how to perform Repeated Measures ANOVA using Python's `statsmodels` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
from statsmodels.stats.anova import AnovaRM
import matplotlib.pyplot as plt
import seaborn as sns

# Sample data: reaction times under different conditions
np.random.seed(42)
data = pd.DataFrame({
    'Subject': np.tile(np.arange(1, 11), 3),
    'Condition': np.repeat(['Condition1', 'Condition2', 'Condition3'], 10),
    'ReactionTime': np.concatenate([np.random.normal(30, 5, 10),
                                    np.random.normal(35, 5, 10),
                                    np.random.normal(40, 5, 10)])
})

# Perform Repeated Measures ANOVA using statsmodels
rm_anova = AnovaRM(data, depvar='ReactionTime', subject='Subject', within=['Condition']).fit()
print(rm_anova)

# Visualization: Line plot with error bars
plt.figure(figsize=(8, 6))
sns.pointplot(x='Condition', y='ReactionTime', data=data, ci=95, join=True)
plt.title('Reaction Time by Condition')
plt.xlabel('Condition')
plt.ylabel('Reaction Time (ms)')
plt.show()
```

### Explanation

- **Sample Data**: We simulate reaction times for 10 subjects measured under three different conditions.
- **Repeated Measures ANOVA Calculation**: We use `AnovaRM` from `statsmodels` to perform the repeated measures ANOVA. The dependent variable is `ReactionTime`, the subject variable is `Subject`, and the within-subject factor is `Condition`.
- **Visualization**: We use a line plot with error bars to visualize the mean reaction times across the conditions.

## Example in R

Let's perform the same Repeated Measures ANOVA analysis using R.

### R Code

```r
# Load necessary libraries
library(ggplot2)
library(ez)

# Sample data: reaction times under different conditions
set.seed(42)
Subject <- factor(rep(1:10, each=3))
Condition <- factor(rep(c("Condition1", "Condition2", "Condition3"), times=10))
ReactionTime <- c(rnorm(10, mean=30, sd=5),
                  rnorm(10, mean=35, sd=5),
                  rnorm(10, mean=40, sd=5))
data <- data.frame(Subject, Condition, ReactionTime)

# Perform Repeated Measures ANOVA using ezANOVA
anova_result <- ezANOVA(data=data, dv=.(ReactionTime), wid=.(Subject), within=.(Condition))
print(anova_result)

# Visualization: Line plot with error bars
ggplot(data, aes(x=Condition, y=ReactionTime, group=1)) +
  stat_summary(fun=mean, geom="line", color="blue") +
  stat_summary(fun.data=mean_cl_boot, geom="errorbar", width=0.2) +
  labs(title="Reaction Time by Condition", x="Condition", y="Reaction Time (ms)") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We simulate reaction times for 10 subjects measured under three different conditions using `rnorm()` in R.
- **Repeated Measures ANOVA Calculation**: We use the `ezANOVA` function from the `ez` package to perform the repeated measures ANOVA. The dependent variable is `ReactionTime`, the subject variable is `Subject`, and the within-subject factor is `Condition`.
- **Visualization**: We use `ggplot2` to create a line plot with error bars to visualize the mean reaction times across the conditions.

## Interpretation of Results

### Main Effect

- **F-statistic and P-value**: The ANOVA table provides an F-statistic and p-value for the main effect of the within-subject factor (Condition). If the p-value is less than the chosen significance level (commonly $\leq 0.05$), we reject the null hypothesis and conclude that there is a statistically significant difference between the conditions.

### Visualization

The line plot with error bars provides a visual representation of how the mean reaction times vary across different conditions. The error bars represent the 95% confidence intervals for the means. Non-overlapping error bars suggest significant differences between the conditions.

### Sphericity

- **Sphericity Assumption**: If the sphericity assumption is violated (checked using Mauchly's test in some cases), adjustments like the Greenhouse-Geisser correction may be applied to the degrees of freedom to prevent inflated Type I error rates.

## Applications

Repeated Measures ANOVA is widely used in various fields:

- **Psychology**: To analyze the effect of different stimuli on participants' responses measured at different time points.
- **Medicine**: To compare the effectiveness of treatments administered to the same group of patients over time.
- **Education**: To assess the impact of different teaching methods on the same group of students' performance across different tests.

## Conclusion

Repeated Measures ANOVA is a powerful statistical tool for analyzing data collected from the same subjects under multiple conditions or time points. By calculating the F-statistics and p-values and visualizing the data with line plots, researchers can determine whether the conditions have a significant effect on the outcome variable. Whether in psychology, medicine, education, or other fields, Repeated Measures ANOVA provides valuable insights into how conditions or time points influence the dependent variable within the same subjects.
