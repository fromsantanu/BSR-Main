# Chapter: Sampling Methods (Random, Stratified, Cluster, Systematic)

## Introduction

Sampling is a fundamental aspect of statistical analysis, where a subset of a population is selected to represent the entire population. Different sampling methods are used depending on the nature of the population and the goals of the study. The four primary sampling methods are:

1. **Random Sampling**: Every member of the population has an equal chance of being selected.
2. **Stratified Sampling**: The population is divided into strata (subgroups), and random samples are taken from each stratum.
3. **Cluster Sampling**: The population is divided into clusters, and entire clusters are randomly selected.
4. **Systematic Sampling**: Every nth member of the population is selected after a random starting point.

Each of these methods has its own advantages and is suitable for different types of studies.

## Random Sampling

### Concept

In random sampling, each individual in the population has an equal chance of being selected. This method is straightforward and reduces selection bias, making it a commonly used sampling technique.

### Example in Python

```python
# Import necessary libraries
import numpy as np

# Population of 1000 individuals
population = np.arange(1, 1001)

# Random sample of 100 individuals
random_sample = np.random.choice(population, 100, replace=False)

print("Random Sample:", random_sample)
```

### Example in R

```r
# Population of 1000 individuals
population <- 1:1000

# Random sample of 100 individuals
random_sample <- sample(population, 100, replace=FALSE)

print("Random Sample:")
print(random_sample)
```

## Stratified Sampling

### Concept

In stratified sampling, the population is divided into homogeneous subgroups or strata (e.g., by age, gender, income level), and random samples are drawn from each stratum. This method ensures that each subgroup is adequately represented in the sample.

### Example in Python

```python
# Import necessary libraries
import numpy as np
import pandas as pd

# Creating a sample dataset
np.random.seed(42)
data = pd.DataFrame({
    'Age_Group': np.random.choice(['Youth', 'Adult', 'Senior'], size=1000),
    'Income': np.random.randint(20000, 80000, size=1000)
})

# Stratified sampling based on Age_Group
stratified_sample = data.groupby('Age_Group', group_keys=False).apply(lambda x: x.sample(50))
print("Stratified Sample:")
print(stratified_sample.head())
```

### Example in R

```r
# Load necessary library
library(dplyr)

# Creating a sample dataset
set.seed(42)
data <- data.frame(
  Age_Group = sample(c("Youth", "Adult", "Senior"), 1000, replace = TRUE),
  Income = sample(20000:80000, 1000, replace = TRUE)
)

# Stratified sampling based on Age_Group
stratified_sample <- data %>% group_by(Age_Group) %>% sample_n(50)
print("Stratified Sample:")
print(head(stratified_sample))
```

## Cluster Sampling

### Concept

In cluster sampling, the population is divided into clusters, which are often naturally occurring groups such as geographic areas or schools. Instead of sampling individuals from each cluster, entire clusters are randomly selected, and all members of the selected clusters are included in the sample.

### Example in Python

```python
# Import necessary libraries
import numpy as np
import pandas as pd

# Creating a sample dataset
np.random.seed(42)
data = pd.DataFrame({
    'Cluster_ID': np.random.choice(['Cluster1', 'Cluster2', 'Cluster3', 'Cluster4'], size=1000),
    'Value': np.random.randn(1000)
})

# Cluster sampling: randomly select 2 clusters
selected_clusters = np.random.choice(data['Cluster_ID'].unique(), 2, replace=False)
cluster_sample = data[data['Cluster_ID'].isin(selected_clusters)]

print("Cluster Sample:")
print(cluster_sample.head())
```

### Example in R

```r
# Load necessary library
library(dplyr)

# Creating a sample dataset
set.seed(42)
data <- data.frame(
  Cluster_ID = sample(c("Cluster1", "Cluster2", "Cluster3", "Cluster4"), 1000, replace = TRUE),
  Value = rnorm(1000)
)

# Cluster sampling: randomly select 2 clusters
selected_clusters <- sample(unique(data$Cluster_ID), 2)
cluster_sample <- data %>% filter(Cluster_ID %in% selected_clusters)

print("Cluster Sample:")
print(head(cluster_sample))
```

## Systematic Sampling

### Concept

Systematic sampling involves selecting every nth member of the population after a random starting point. This method is simple to implement and is useful when dealing with a large population.

### Example in Python

```python
# Import necessary libraries
import numpy as np

# Population of 1000 individuals
population = np.arange(1, 1001)

# Systematic sample of 100 individuals: every 10th individual after a random start
start = np.random.randint(0, 10)
systematic_sample = population[start::10]

print("Systematic Sample:", systematic_sample)
```

### Example in R

```r
# Population of 1000 individuals
population <- 1:1000

# Systematic sample of 100 individuals: every 10th individual after a random start
start <- sample(1:10, 1)
systematic_sample <- population[seq(start, 1000, by=10)]

print("Systematic Sample:")
print(systematic_sample)
```

## Comparison and Applications

- **Random Sampling**: Best for ensuring each individual in a population has an equal chance of selection, reducing bias.
- **Stratified Sampling**: Useful when the population has distinct subgroups, ensuring representation from each subgroup.
- **Cluster Sampling**: Effective when a population is naturally divided into clusters, reducing cost and time for sampling.
- **Systematic Sampling**: Simple to implement, especially for large populations, and useful when a complete list of the population is available.

Choosing the appropriate sampling method depends on the research goals, population structure, available resources, and desired accuracy. Each method has its advantages and limitations, and understanding these can lead to more accurate and reliable results in statistical analysis.
