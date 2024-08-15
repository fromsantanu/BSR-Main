# Chapter: Two-way ANOVA

## Introduction

Two-way Analysis of Variance (ANOVA) is a statistical method used to examine the effect of two independent categorical variables (factors) on a continuous dependent variable. Unlike one-way ANOVA, which considers only one factor, two-way ANOVA allows researchers to analyze the main effects of each factor and the interaction effect between the two factors. This method is useful when you want to understand how multiple factors simultaneously influence a dependent variable.

## Key Concepts

1. **Main Effects**:
   - **Factor A**: The effect of the first independent variable on the dependent variable.
   - **Factor B**: The effect of the second independent variable on the dependent variable.

2. **Interaction Effect**: The combined effect of Factor A and Factor B on the dependent variable. An interaction occurs when the effect of one factor depends on the level of the other factor.

3. **Null Hypotheses**:
   - **$H_{0A}$**: The means of the dependent variable are the same across the levels of Factor A.
   - **$H_{0B}$**: The means of the dependent variable are the same across the levels of Factor B.
   - **$H_{0AB}$**: There is no interaction between Factor A and Factor B.

4. **F-statistic**: The F-statistic is used to test each null hypothesis. If the F-statistic is large and the corresponding p-value is small (typically \( \leq 0.05 \)), we reject the null hypothesis.

5. **Assumptions**:
   - **Independence**: Observations within each group are independent of each other.
   - **Normality**: The data in each group are normally distributed.
   - **Homogeneity of Variances**: The variances of the groups are equal.

## Example in Python

Let's explore how to perform a two-way ANOVA using Python's `statsmodels` library.

### Python Code

```python
# Import necessary libraries
import numpy as np
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
import statsmodels.api as sm
from statsmodels.formula.api import ols

# Sample data: test scores influenced by teaching method and study time
np.random.seed(42)
data = pd.DataFrame({
    'Scores': np.concatenate([np.random.normal(75, 10, 30),
                              np.random.normal(80, 10, 30),
                              np.random.normal(85, 10, 30),
                              np.random.normal(70, 10, 30),
                              np.random.normal(82, 10, 30),
                              np.random.normal(90, 10, 30)]),
    'Method': np.repeat(['Method1', 'Method2', 'Method3'], 60),
    'StudyTime': np.tile(['Short', 'Medium', 'Long'], 60)
})

# Perform two-way ANOVA using statsmodels
model = ols('Scores ~ C(Method) + C(StudyTime) + C(Method):C(StudyTime)', data=data).fit()
anova_table = sm.stats.anova_lm(model, typ=2)
print(anova_table)

# Visualization: Interaction plot
sns.pointplot(x='StudyTime', y='Scores', hue='Method', data=data,
              markers=["o", "s", "D"], linestyles=["-", "--", "-."])
plt.title('Interaction Plot: Scores by Method and Study Time')
plt.xlabel('Study Time')
plt.ylabel('Scores')
plt.show()
```

### Explanation

- **Sample Data**: We generate test scores for three different teaching methods and three different study times, creating a factorial design with 9 groups (3 methods × 3 study times).
- **Two-way ANOVA Calculation**: We use `statsmodels` to perform the two-way ANOVA by fitting the model with the `ols()` function and generating the ANOVA table with `anova_lm()`.
- **Interaction Plot**: We visualize the interaction effect between the teaching method and study time using a point plot. This plot helps to see how the effect of one factor changes across the levels of the other factor.

## Example in R

Let's perform the same two-way ANOVA analysis using R.

### R Code

```r
# Load necessary libraries
library(ggplot2)

# Sample data: test scores influenced by teaching method and study time
set.seed(42)
Scores <- c(rnorm(30, mean=75, sd=10),
            rnorm(30, mean=80, sd=10),
            rnorm(30, mean=85, sd=10),
            rnorm(30, mean=70, sd=10),
            rnorm(30, mean=82, sd=10),
            rnorm(30, mean=90, sd=10))
Method <- factor(rep(c("Method1", "Method2", "Method3"), each=60))
StudyTime <- factor(rep(c("Short", "Medium", "Long"), times=60))
data <- data.frame(Scores, Method, StudyTime)

# Perform two-way ANOVA
anova_result <- aov(Scores ~ Method * StudyTime, data=data)
summary(anova_result)

# Visualization: Interaction plot
ggplot(data, aes(x=StudyTime, y=Scores, color=Method, group=Method)) +
  geom_point() +
  geom_line() +
  labs(title="Interaction Plot: Scores by Method and Study Time", x="Study Time", y="Scores") +
  theme_minimal()
```

### Explanation

- **Sample Data**: We generate test scores for three different teaching methods and three different study times using `rnorm()` in R, resulting in 9 groups (3 methods × 3 study times).
- **Two-way ANOVA Calculation**: We perform two-way ANOVA using the `aov()` function and summarize the results with `summary()`.
- **Interaction Plot**: We use `ggplot2` to create an interaction plot that visualizes how the scores change across different study times for each teaching method.

## Interpretation of Results

### Main Effects and Interaction Effect

- **Main Effects**: The ANOVA table provides F-statistics and p-values for each main effect (Method and Study Time). If the p-value for a main effect is less than the significance level (typically $\leq 0.05$), it suggests that the factor has a statistically significant effect on the dependent variable.
- **Interaction Effect**: The interaction effect's p-value tells us whether the effect of one factor depends on the level of the other factor. A significant interaction effect (p-value $\leq 0.05$) indicates that the relationship between the factors and the dependent variable is not additive.

### Interaction Plot

The interaction plot provides a visual representation of the interaction effect between the two factors. If the lines are not parallel, it suggests that there is an interaction between the factors, meaning that the effect of one factor varies depending on the level of the other factor.

## Applications

Two-way ANOVA is widely used in various fields:

- **Education**: To assess the impact of different teaching methods and study habits on student performance.
- **Healthcare**: To evaluate the effects of different treatments and patient demographics on health outcomes.
- **Agriculture**: To study the effects of different fertilizers and irrigation levels on crop yield.

## Conclusion

Two-way ANOVA is a powerful statistical tool for analyzing the effects of two independent variables on a dependent variable, including the interaction between the two factors. By calculating the F-statistics and p-values and visualizing the data with interaction plots, researchers can determine whether the factors have significant effects on the outcome and whether these effects interact. Whether in education, healthcare, agriculture, or other fields, two-way ANOVA provides valuable insights into the complex relationships between multiple factors.
